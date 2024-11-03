# SuperGenius processing component information

The SuperGenius processing component uses the ifps-pubsub gossip protocol, similar to how a game has a lobby system for a peer-to-peer game.

All SuperGenius nodes subscribe to the processing channel.

To begin processing a request is made to the channel for any open processing requests with a slot open. If a slot is open, the node joins the sub-channel processing- where UUID is a unique ID created by a processor node; see next section.

If no slots are open, the processing node grabs the block-lattice branch (database records) of their synced database records which have block data of request to process.

The node grabs the UUID from the db record and then opens up a processing- channel, and publishes the UUID to the main channel.

The channel publish/subscribe system uses ipfs-pubsub with communication protocol using gRPC.
