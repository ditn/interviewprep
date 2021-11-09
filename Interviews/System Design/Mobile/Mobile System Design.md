# Mobile System Design Interviews

-   What are we being asked to design?
-   Who is the user, and how will they use our system?
-   What's the initial number of users? And the expected growth?
-   Are we being given an initial design/wireframes, or should we produce them as well?
-   Are we designing an MVP or final-product?
-   Are we building this from scratch, or can we leverage any existing components? Any existing patterns/architecture we should follow?
-   How big is the team who will implement and maintain our system?
-   Are we expected to design just the mobile application or other parts of the overall system too (e.g. API)?
-   Is it iOS or Android only, or cross-platform? Shall we support smartphones, tablets, both?

## Design Requirements
- Client-side only
- Client-side + API
- Client-side + API + Backend

Don't forget to gather key **functional**, **non-functional** and **out of scope** requirements.

For example, in the case of Twitter:

- Functional
	- Users should be able to scroll through an infinite list of tweets
	- Users should be able to click on a tweet to see replies
	- Users should be able to like a tweet
- Non-functional
	- Offline support
	- Real-time notifications
	- Optimal bandwidth/CPU usages
- Out of Scope
	- Login/Authentication
	- Sending Tweets
	- Followers/Retweets

## Identify Technical Requirements
- How many users to we expect?
- How big is the engineering team?

### Networking
- REST API? How is it provided and what does it look like?
- Any live updates? Websockets, polling, push notifications - tradeoffs

### Security
- Authentication - how will your design verify who the user of your app is?
- Storing sensitive data - will you save credentials? Access tokens? Refresh tokens? PII? Keychain/KeyStore
- Secure communications - cert pinning, TLS

### Availability
- Will the app support offline mode? If so, what solution will you use? How will you handle going online again?
- Caching for images or other media - what's the cleanup policy (LRU)

### Scalability
How will you build an app that can be worked on by dozens of engineers?

- Modularisation for features
- Breaking UI into standard components/design systems

### Performance
- Any UI-heavy operations such as animations? How do you ensure no jank?
- How do we load heavy resources like images asynchronously? What are the bottlenecks and challenges of your approach?

### Testing
- Explain your testing strategy - pyramid of tests
- Highlight strength of architecture - how easy is it to test an individual component?
- Use of DI

### Monitoring
- Crash reporting
- Analytics
- Performance monitoring
- Breadcrumbs

### Deployment
How do you forsee the app going live?
- CI/CD pipeline with automated releases
- Leveraging feature flags

# High-Level Solution
- Draw the main screens as boxes, describing the main content
- Go over the flow, adding arrows to represent the user journey
- Add more details to discuss each screen's composition - main UI elements, reusable components etc

# Principal Systems
(If required)

 - Mobile clients
 - API services
 - Backend apps
 - Databases
 - Notification services

# Define Basic Data Entities
- User object
- Posts/Stories/Whatever

# Describe Primary Endpoints
- POST `v1/auth` etc - don't forget versioning!
- Idempotency keys - can be a header
	- Cached by server, so subsequent requests with the same key get the same result (or error)
	- Makes sense for `POST` & `PUT` & `DELETE` & `PATCH` - `GET` is idempotent anyway 
	- See https://miro.medium.com/max/700/1*GhDYXaU9DSNEHXtR0x7GmA.png
- Describe input parameters, expected outputs

# Describe Client Architecture
- Presentation layer
	- MVVM, Coordinator, Activities + Fragments
- Domain layer
	- Use cases to combine data from the user and repositories
- Data layer
	- Repositories to coordinate fetching data from the network, caching, disk etc
- Helper services
	- Notifications
	- Networking
	- Session service for user info
	- Credentials store 

# Quality of Service
Assign a QoS to each of your network requests:
* **User-critical** - should be dispatched as fast as possible, fetching the next page of data in a feed, for instance
* **UI-critical** - dispatched after user-critical. Fetching thumbnails while scrolling, but could be cancelled if the user scrolls past the target tweet. May be delayed in the case of fast scrolling.
* **UI-non-critical** - dispatched after UI-critical. High-res images for the feed. Cancelled if the user scrolls past the target tweet.
* **Background** - should be dispatched after all of the above have finished. This can include posting "likes", analytics.

Use a priority queue for scheduling network requests and dispatch in the order of their priority. Suspend low-priority requests if the maximum number of concurrent operations is reached and a high-priority request is scheduled.

# Deep-Dive
- Chose the most interesting screen and draw it's architecture. Cover all layers, from UI components to ViewModels, repositories, endpoints, network layer, local store etc
- Trace the dependencies from the caller
- Walk over the flow - what does the user see at every step? Don't forget view states! Loading, Error, Data, No Data
- Think about the most challenging parts
	- Real-time updates
	- Image caching
	- Reusing data
	- Buffering requests
