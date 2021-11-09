# Latency and Throughput

## Latency
Latency is a measure of how long it takes for data to go from one part of a system to another - from client to server, from disk to processor, from distributed DB to some other component etc.

There's tradeoffs to be made here - speed vs cost vs consistency vs persistence etc.

## Comparisions
Reading 1 MB from:

| Transaction | Latency |
|-|-|
| RAM | $0.25 ms$ |
| SSD | $1 ms$ |
| Network</br>(1 Gbps, no geographical distance) | $10 ms$ |
| HDD | $20 ms$ |
| Intercontinental round trip for a packet | $150 ms$ |

## Throughput
Throughput is a measure of how much work a machine can handle in a given timeframe - measured in Gbps/Mbps/Kbps or in Requests Per Second (RPS).

Typically we increase the throughput of a system by adding more servers, but this has a tradeoff.

When designing a system, you have to consider where your throughput bottlenecks will be - there's no point having a server which can handle thousands of RPS, only to be constrained by a single database which can only handle a few tens of RPS.
