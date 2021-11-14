# The Client-Server Model

The client-server model is the dominant paradigm for the modern internet.

### Clients
- A machine or process that sends data to, or requests data from, a server. Typically this is a personal computer, browser, phone or app, but it can also be another server.

### Servers
- A machine or process that provides data or some kind of service to clients, typically by listening for network calls. A server can also be a client for another server.

### DNS Queries
- A client will ask a pre-determined set of servers: what's the IP address of some other server?
- An IP address is a unique identifier for a specific server
- These IPs are assigned by some kind of authority - Amazon/Google Cloud

### Requests
- A **source IP address** sends a series of bytes as packets
- The server uses this source IP adddress to return another series of packets

### Ports
- If an IP address is similar to a mailing address, a port is equivalent to the flat number
- Machines have 16k (14 bits?) ports
- You can attempt to communicate with any of them, but typically the port you have to request is dictacted by the protocol
	- `http` uses port 80
	- `https` uses port 443
