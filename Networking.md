# Networking

## OSI Model

1. Physical Medium
    * Coax
    * Radio
2. Data Link
    * Wifi
    * Ethernet
3. Network Layer
    * IP & Routing (ipv4, ipv6)
4. Transport Layer
    * Segmentation (tcp)
    * Ordering (tcp)
    * Reliability (tcp)
5. Session Layer
    * Resource management, port assigning, OS stuff
6. Presentation Layer
    * Compression (gZip)
    * Encryption (SSL)
    * Conversion 
7. Application Layer
    * Provides protocols & services required by network aware applications to connect to the network
    * http
    * ftp

## WebRTC notes

Protocol Built on top of `SCTP`.

* Configurable

~~Unknown: So `SCTP` sits on layer 4, does that mean every router along the way needs to “support sctp”?~~ Routers operate at layer 3.

Allows realtime connections, and is written as a p2p protocol. Optimized for things like video chatting.

Due to it being p2p, it butts heads with the way ipv4 is currently configured.  Due to ipv4’s limited addressing space people use `NAT`. `NAT` allows “servers” to “address” clients without every “client” being assigned a public facing IP address. 

As a result of this 2 peers don’t know their public facing IP address and can’t communicate by default.

WebRTC introduces the concept of the following protocols to remedy this situation:

* `STUN`: Session traversal utilities for nat.
	* Allows a client to obtain a transport address (IP & Port) which may be useful for receiving packets from a peer. 
	* Not usable by all peers based on network topography.
* `TURN`: Traversal Using Relays around `NAT`
	* Fallback if STUN fails
* `ICE`: Abstraction that takes care of the fallback process

Okay so peers can find their addresses using `ICE`, but they need to find other peers, they do so through a process called signaling. `Signaling` is application specific. 

After signaling clients are ready to start exchanging packets directly. They’re required by WebRTC to complete a handshake known as the Session Description Protocol (`SDP`). This is where peers exchange infromation about their media capabilities.

So the flow is roughly:

1. Signalling
2. ICE
3. Exchange data

This description is often wrapped in an `Offer` which is routed through the signaling server.

The `Offer` is reponded too with an `Answer` which contains the responder's media capabilities.

The peers will now get their public addresses via ICE, and exchange it via the signalling server. The response from `STUN` servers is known as `INCE Candidate` information. 

At this point each client has the other's public IP information as well as media capabilities. They ping one another and the connection is established, they can now send information via Data Channels. 

[For information on how you could setup client/server](http://blog.brkho.com/2017/03/15/dive-into-client-server-web-games-webrtc/)

[TCP performs very poorly for games](https://gafferongames.com/post/udp_vs_tcp/) and unfortunately [UDP is not an option for browsers](https://gafferongames.com/post/why_cant_i_send_udp_packets_from_a_browser/). Games subsequently have to use WebRTC for realtime information.
