# Availability

How stable does the system you're designing need to be? Consider the usecase:
- What is the financial cost of downtime? Missed transactions, customers getting frustrated etc
- Is it a critical service? Air Traffic Control probably has greater availability constraints than Twitter, for instance. How much downtime is acceptable in these scenarios?
- Does your service enable other services? For instance, Cloudflare going down is really really bad.
- Do different parts of your services require different availability? A system that provides profile photos might well be allowed to be less robust than the system that takes payments

### SLA/SLO
Service Level Agreements/Service Level Objectives are guarantees that services make with customers about availability. Would your service provide an SLA? 

What would be the penalty for breaking this SLA? For reference, Google Cloud provides refunds below certain levels of availability.

## Redundancy
The way that we ensure high availability is by building systems with redundancy.
- Ensure that there's no single point of failure in your system - if you only have one server and it goes down, how screwed are you?

### Passive Redundancy
Multiple components for a specific layer of your architecture. For instance, you might have several load balancers - if one goes down, the others handle the increased load just fine, but there has to be available bandwidth for them.

### Active Redundancy
This is more complex, but in essence it's having machines which agree which one or subset of them does the incoming work. If a machine fails, the other machines agree upon a way to route around the problem by taking up the work themselves or distributing it to others.

See [[Leader Election]].

## Resolving Issues
What happens if some machines _do_ go down? Does a human need to intervene?

## Nines
Over the course of a year:

| Uptime | Nines | Time Down |
|-|-|-|
| 99% | Two 9s | 87.7 hours |
| 99.9% | Three 9s | 8.8 hours |
| 99.99% | Four 9s | 52.6 minutes |
| 99.999% | Five 9s | 5.3 minutes |
