# Contents
[[Mobile System Design]]

## TL;DR
-   Write down as much as possible
    -   Write-talk-write-talk if necessary
    -   Concise and neat is better than quick and illegible
-   Engage with the interviewer
    -   describe what you’re doing
    -   ask questions
    -   signpost frequently
    -   check understanding
    -   handle interruptions gracefully
-   Mention relevant tech
    -   but don’t bluff
    -   and don’t let it take over the interview
-   Track and mention considerations
    -   like security, accessibility, and testing

## Interview Overview

Systems design interviews are very different to coding interviews - there's no 100% correct or 100% wrong answer. Because of this, you must be able to defend your position, or adjust it as new data emerges - convincing your interviewer that your solution is thought through.

Questions are intentionally very vague - sometimes just two words. "Design Facebook", "design YouTube" etc. Consequently, it's extremely important that you ask a tonne of clarifying questions with your interviewer to help narrow down the scope of the system and tease out which components they're expecting to see.

Systems design interviews can be thought of in 4 broad sections:

### Foundational knowledge
This is the core stuff, without it you really can't bullshit your way through these interviews. We're talking fundamentals, such as:
- [[Client-Server Model]]
- [[Network Protocols]]
- [[Storage]]

### Key Characteristics
You need to decide what they key characteristics of your system are going to be, as this informs the technical choices you make later and it makes it clear to the interviewer that you've thought about the system.

Examples include:
- [[Latency and Throughput]]
- [[Availability]]
- [[Hashing]]
- [[Strong vs Eventual Consistency]]
- Leader election
- Rate limiting

### Key Components
Once you've decided what your system's key characteristics are, which subsystems are you going to use, in what combinations, to fulfill these requirements?

Examples might be:
- [[Caching]]
- [[Proxies]]
- [[Load Balancers]]
- [[Relational Databases]]
- [[Microservices]]
- [[Microservices#The API Gateway]]
- [[Partitioning]]
- [[Duplication]]

### Actual Tech
This is where you get to show that you actually have experience with this stuff. What existing tech out there fulfills your requirements?

Tools include:
- Amazon S3
- Google Cloud Storage
- Redis
- Nginx
- MapReduce
- Zookeeper
- Kubernetes

# Strategies
See [here](https://cternus.net/blog/2018/01/26/tackling-the-system-design-interview/) for more information.

1) Immediately write down the question in the top corner of the board so that you don't forget and can go back to it. At this stage, write down any constraints that have been mentioned.
2) Ask clarifying questions - write down any revealed constraints in bullet point form
3) Think through the broad strokes of the solution and write this on the board. "I'm going to draw out a basic solution here as a starting point".
4) Drill down into individual sections, changing things as you go. Describe how it works and the tradeoffs that you're making, as well as the failure modes.
	1) Keep a list of "considerations" on one side of the board. Add to these as you remember facets that haven't been tackled yet, and cross these out as you sort them.
5) Write down a timeline of an interaction with the system, if appropriate
6) Towards the end, summarise your system. Are there any outstanding issues that you would have tackled if you had more time?

### Write. Down. Everything.
You cannot write down too little. Interviewers won't be paying 100% attention and may miss things, so write as much as you can.

### Interact with your interviewer!

Think of yourself as a tour guide walking the interviewer through your solution. 

- Does that seem reasonable?
- Should I discuss X or Y next?
- What would you like to see more of?
- Does it seem like I’m missing anything?

# Considerations
- Security and compliance
	- Who has access? How much access? Are there bad actors? How might the system be attacked? How does authentication work?
- Compliance 
	- GDPR, medical data, payment data
- Accessibility
	- Physical and mental disabilities, cultural/internationalisation
- Backups
	- How will backups occur? How much data could you afford to lose?
- Testing, monitoring, alerting
	- How will you verify that your solution is correct? How will you know that it's working? If the system goes down, who fixes it?
