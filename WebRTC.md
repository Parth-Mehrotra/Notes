# WebRTC notes

Protocol Built on top of SCTP.

* Configurable
* Unknown: So SCTP sits on layer 4, does that mean every router along the way needs to “support sctp”?

Allows realtime connections, and is written as a p2p protocol. Optimized for things like video chatting.

Due to it being p2p, it butts heads with the way ipv4 is currently configured.  Due to ipv4’s limited addressing space people use NAT. NAT allows “servers” to “address” clients without every “client” being assigned a public facing IP address. 

As a result of this 2 peers don’t know their public facing IP address and can’t communicate by default.

WebRTC introduces the concept of the following protocols to remedy this situation:

* STUN: Session traversal utilities for nat.
	* Allows a client to obtain a transport address (IP & Port) which may be useful for receiving packets from a peer. 
	* Not usable by all peers based on network topography.
* TURN: Traversal Using Relays around NAT
	* Fallback if STUN fails
* ICE: Abstraction that takes care of the fallback process

Okay so peers can find their addresses using ICE, but they need to find other peers, they do so through a process called signaling. Signaling is application specific. 

After signaling clients are ready to start exchanging packets directly. They’re required by WebRTC to complete a handshake known as the Session Description Protocol. This is 

#notes
