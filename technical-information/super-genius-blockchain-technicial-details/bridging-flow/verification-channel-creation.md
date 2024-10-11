
# Leader Ownership and Verification Channel Creation

## Channel Creation
- **Pub/Sub Setup**: Once the leader is determined, it creates a verification channel on IPFS pub/sub. This channel acts as the communication medium for all selected nodes participating in verification.
- **Inviting Participants**: The leader sends out an invitation to other nodes to join the channel and contribute to verification.

## Ownership Persistence
- **Lock Persistence**: The job remains in the queue with the leader’s node ID. If the leader fails or disconnects, the job remains, and other nodes can attempt to acquire the ownership.

```cpp
void setupPubSubChannel(std::string topic) {
    log("Leader setting up verification channel: " + topic);
    pubsub.createTopic(topic);
}

void inviteNodesToChannel(std::string topic) {
    log("Inviting nodes to channel: " + topic);
    pubsub.inviteToTopic(topic, selectedNodes);
}
```
    