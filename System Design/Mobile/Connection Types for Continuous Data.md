# Connection Types for Continuous Data

## Long/Short Polling
Otherwise known as client pull.

### Cons
- Every request is a full HTTP request - including headers which can actually represent quite a lot of data transferred. This is inefficient e.g. 15KB of headers for 5KB of data.
- Maximal latency - the server responds, then cannot respond again until the next request from the client.
	- This means the maximal latency is actually three network requests - response, request, response
	- Infact, it's _at least_ three, factoring in packet-loss, retransmission etc.
	- This is a huge problem when switching cell networks etc.

## Websockets
Websockets allow you to open an interactive session with the server, sending messages and receiving event-driven responses without having to poll for a reply.

This protocol provides full-duplex communication channels over a single TCP connection (at TCP layer 4). It is not automatically multiplexed over HTTP/2 connections because it doesn't really run ontop of HTTP at all. Connections are established over HTTP ports 80 and 443 via an Upgrade header to change protocol from HTTP to websockets.

### Cons
- Load balancing is very complicated as there can be many sockets open at the same time
	- You can potentially suffer from a wave of "reconnect" messages which overwhelms your server
	- It isn't possible to move socket connections to a different server if one experiences high load: they must be closed and re-opened.
- Without WiFi, websockets require the full-duplex antenna to work almost constantly, drawing huge amounts of power. Typically, mobile devices use a low-power antenna to receive data, and full duplex in order to establish calls.

## Server-Sent Events

Server-Sent Events are similar to websockets in that they happen in real-time, but they're very much one-way. A server emits these events in real-time and they're received by the client, with the client sending very few events.

### Pros
- The connection stream is coming from the server and is read-only
- Uses regular HTTP requests, no special protocol - so [[multiplexing]] over HTTP/2 works out of the box.
- If the connection drops, the EventSource fires an error event and tries to reconnect, with a timeout
- Clients can send a unique ID with each message. When a client tries to reconnect after a dropped connection, it sends the last know ID
	- The server can then send `n` number of missed messages from a backlog