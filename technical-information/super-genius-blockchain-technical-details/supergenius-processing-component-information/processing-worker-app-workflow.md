# Processing worker app workflow

1. The application starts a local gRPC processing service to allow other processing peers to communicate with it.

```
processingServiceServer = new ProcessingServiceServer("localHost:port");
processingServiceServer->Run();
```

2. Application connects to the local GRPC processing service.

```
processingServiceClient = new ProcessingServiceClient("localHost:port");
```

3. The application requests a list of available processing room names (IDs) from a database.

```
roomList = processingServiceClient->GetRoomList();
```

4. Application sequentially tries to join a room from the room list.

```
foreach( room in roomList)
    if (processingServiceClient->RoomJoin(room) == OK)
         break;
```

5. If a room is joined, the application receives data to process and starts local data processing.

Once a result is calculated, the worker publishes it to the room.

```
if (processingServiceClient->RequestProcessingData("room", out data) == OK)
{
    result = Calculation();
    processingServiceClient->PublishProcessingResult(roomName, result);
}
```

NOTE: Since data processing is implemented on the application side, requesting a new processing sub-block from the application is easier than initiating the processing from the room host.

6. The worker replicates the room creator job if the processing data request fails. See details in [Paragraph 2](https://github.com/GeniusVentures/SuperGenius/wiki/2-Processing-Workflow#2processing-room-workflow)

```
if (processingServiceClient->RequestProcessingData("room", out data) != OK);
{
    // Becomes a room manager
}
```

### 2 Processing room workflow

Assumptions: any processing node participles in a single processing room simultaneously.

1. If a room joining process fails, the application should create a new processing room and manage the processing.

```
data = RetrieveDataToProcess();
dataSubBlocks = SplitDataToChunks();
processingServiceClient->PublishDataToProcess(roomName, dataSubBlocks);
```

2. Once PublishDataToProcess() method is called the local gRPC service starts the room managing. Initially, it notifies other peers that the room host has changed:

```
PublishDataRoProcess(roomName, dataSubBlock)
{
    SaveDataSublocks();
    foreach(peer in peerList);
       peer.processingService->OnHostChanged(currentPeerInfo);
}
```

3. When any peer joins the room, it sends the join request to the room Pub/Sub channel. The room host checks if the room peers' limit is not reached and either accepts the request or rejects it. See details in [Paragraph 4](https://github.com/GeniusVentures/SuperGenius/wiki/2-Processing-Workflow#4room-join-process)

```
   RoomJoin(roomName, remotePeer)
   {
       channel = SubscribeToPubSubChannel(roomName);
       peerList = channel.GetlPeerList();
       if (peerList.size() <= 1)
          ROOM_DOES_NOT_EXIST;
       else
       {
           channel.Publish("Room join request")
           { CHECK_ASYNC_RESPONSE }
       }
  }
  
  // On room host side
  OnJoinRequestMessageReceived(message, peer)
  {
          if (peerList.size() < roomSizeLimit)
          {
              peerList.push_back(remotePeer);
              createDirectConnection(remotePeer);
              foreach(peer in peerList);
                   peer.processingService->OnPeerListChanged(peerList);

          }
 }
```

4. The room host keeps connections to remote peers. If a connection error occurs, the host removes the failed peer from the room peer list and notifies other peers about the list changes.

```
OnConnectionError(peer):
peerList.remove(peer);
peer.processingService->OnPeerListChanged(peerList);
```

5. When a data sub-block is requested, the host tracks the request time and peer. If a processing time limit is reached but the corresponding result is not received, the host excludes the peer from the processing room and notifies other peers about the peer list change.
6. If the room host leaves the room (due to a connection error, for instance), any other peer from the room should be able to take responsibility. Thus, another peer in the room should be notified when a worker requests data for processing.

```
RequestProcessingData(roomName, dataSubBlock)
{
    dataSubBlock = FindDataSubBlock(out subBlockID);
    foreach(peer in peerList);
       peer.processingService->OnSubBlockProcessingStarted(subBlockID, currentTime);
}
```

### 3 Results accumulation and verification

1. On the gPRC service side, once a PublishProcessingResult(roomName, result) is called, the service gets a list of peers connected to the room and sends the result to all of them using direct gRPC connections.

```
   foreach(peer in peerList);
       peer.processingService->OnProcessed(result);
```

2. TODO: if results should be accumulated on the DApp side it is necessary to decide how to pass them to DApp from the gRPC service. I haven’t found a way to declare streams in YAML while Proto supports them. A stream could be passed as an input parameter to a service call, and results could be obtained from the stream on the DApp side.

### 4 Room join process

When a peer tries to join a room with a specified name (ID) it subscribes to the corresponding Pub/Sub channel with a topic=ID. Once it is subscribed, it can get a list of peers subscribed to the same topic. If the list contains more than one peer, the room exists. In general, not all peers subscribed to a channel can participate in processing because there is a limit to the number of workers that can be included in a processing room. To join the room, it is necessary to publish a message to the channel:

"Room join request" Once a room host receives the message, it decides whether the peer can be joined. If the answer is "yes" the host is directly connected to the peer and sends it a list of the room peers.
