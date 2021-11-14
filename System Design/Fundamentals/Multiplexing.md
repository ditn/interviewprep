# Multiplexing

At it's most basic, multiplexing allows clients to fire multiple requests at the same time on the same connection, and receive events back in any order. 

Historically with HTTP 1.1, clients have been limited to 6 simultaneous connections. This is a lot of connections to manage and impacts both the client and the server.

![[mentalmodel-HTTP2_in_Action2.png]]