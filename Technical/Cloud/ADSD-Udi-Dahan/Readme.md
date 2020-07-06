# Advanced Distributed System Design(ADSD) - Udi Dahan

## Resources

- [Course Page](https://particular.net/adsd)
- [Slides](adsd_slides_Feb2017-1490880187992.pdf)
- Last: 190

## Notes

- One drawback of DI is method call is hidden, we don't know if its going to make a local or Remote call

- As seen in below code, first call to create an object is definitely a local call, but we are not sure if second line call is a local/Remote.

  ```
  var svc = new MyService();
  var result = svc.Process(data);
  ```

  

- First law of distributed system is NOT to distribute

- On-Prem Vs Cloud is like Pets vs Cattle. You take care of Pets and doesn't bother much for cattle.

- Lots of lots of remote call is bad, bad, bad

- Messaging is like putting a letter in postbox and it'll be delivered sometime

- Afferent(incoming) coupling is independent of domain such as Logging as we don't have Insurance logging, healthcare logging etc.

- Efferent(Outgoing) coupling is domain specific

- We check are we coupled to stable things or volatile things

- DTOs should be self contained

- Make Coupling explicit/visible

- HTTP doesn't do one to many communication

- SMTP and UDP does one to Many

- SMTP is most reliable

- SOAP provides a definition of an envelope

- People reinvent things present in SOAP by putting wrapper on REST

- WSDL allows to have interoperability on the structure of input XML and output XML

- WSDL : Given a response structure what is the input structure and what is the output structure

- HATEOS is impractical

- Synchronous communication has a high degree of Temporal Coupling

- Avoid Multi-threading

- Determining caching at what level is important

- Its not a question of if you are going to cache, its a question where to cache

- Data will be somewhat stale in a distributed system

- Avoid request/command such as 'SaveCustomerRequested'

- Add validity to an event

  <img src=".\assets\coupling.png" alt="Coupling" style="zoom:80%;" />

- Adding Resiliency by using Queue

  <img src=".\assets\store-and-forward.png" alt="Store and Forward" style="zoom:80%;" />

- Messages over methods

  <img src=".\assets\standard- service-interfaces.png" alt="Standard Service Interfaces" style="zoom:80%;" />

  <img src=".\assets\messages-over-methods.png" alt="Messages over methods" style="zoom:80%;" />

- Message becomes DTO

- Using message queuing system, there is no Data Loss.

- No cross cutting concerns in WebAPI or message handlers

- HTTP timeout is 30 seconds

- Database timeout is 10 minutes

  <img src=".\assets\database-down.png" alt="Database Down" style="zoom:80%;" />

- NServiceBus has a retry logic inbuilt

- In old RPC kind of systems, when bad things happens they are very susceptible for data loss

- When choosing infrastructure, it has to be reliable and fast

- RPC is very very fast but unsafe/unreliable

- Messaging is safe and try to be as fast as possible

- RPC is like a car without airbag which is fast but unsafe 

- Messaging is like a car with airbag or safety measures, but slow compared to RPC

  <img src=".\assets\messaging-server-crash.png" alt="Messaging in server crash" style="zoom:80%;" />

- Message ID and header are very important in a queueing systems

- Eventual Inconsistency

- Transactions in Messaging systems such as RabbitMQ

- Query before submit

- Cache is dangerous and needs to be submitted

- Async makes system cost effective, not the messaging system

- Storage is cheap but processing is costly. If done synchronous, need more hardware/servers to handle the load. In this case, asynchronous messaging is helpful in reducing the cost

- Versioning helps solve concurrency problems

- Architecture styles need not enforce a particular architecture to the whole system

  <img src=".\assets\architecture-style.png" alt="Architecture Style" style="zoom:80%;" />

- SOA was a reaction to the failings of the centralized broker style of Enterprise Application Integration(EAI) 

- A mix of both Broker and Bus archtiecture

  <img src=".\assets\broker-bus.png" alt="Broker vs Bus" style="zoom:80%;" />

- Stateless actor -> handlers

- Stateful actors -> sagas

- Everything must be in service, nothing should be left over.

  <img src=".\assets\not-a-service.png" alt="Not a Service" style="zoom:80%;" />

- Delay naming services. Give them Color based names.

- Start with capabilities in a box and name that box later

- Wait until you know much about the domain

- A service contains multiple libraries

- ITOps service is not business oriented

- Upgrades should be done incrementally and not in a leap. For e.g upgrading from 4 to 6, better go with 4 -> 5 -> 6 and stabilize in-between things.

- Finding service boundaries is an art and it takes time.

- Finding boundaries is the hard part and explaining it is easy.

- **Don't blindly map boundaries based on company's boundaries such as Marketing, Sales, Engineering etc.**

- Billing, shipping, mainly ending with 'ing' are processes and not capabilites.

- These processes may contain many capabilities and spread across services

- Process, business departments, entities(Hotel, Guest, Room) are out.

- These all things creates a coupling and we need to do whole bunch of request/response.

- Most of the time we end up having bits and pieces of different entities end up in different services.

- **OOAD doesn't help in finding service boundaries.**

- **Anti-requirements**

-  Services with consistent boundary

- When NOT to do SOA

- Purpose is to find what is stable and what is volatile in business

- In software, its about finding stable business abstractions and to align with software abstractions according to same boundaries

- The parts that are volatile gets encapsulated both at business and software level.

- Create Data Model and not entities

- Copy less volatile concept instead of copying more volatile. For e.g rather than copying Price, copy booking id.

- Yes, we are allowed to copy business data

- But we shouldn't copy data across services.

- Should things be kept together or split them more

- Its better to start with individual and move it later.

- If something can be separated, prefer to have it separated.

- Try not to over optimize when we do not have complete or good enough picture

- Service to service interaction happens in process and any remote invocation happens in a service boundary

- A detrimental effect may occur as a result of duplicating the data across services

- Udi dahan is not a proponent of DDD.

- Business component is similar to Bounded Context

  <img src=".\assets\business-component.png" alt="Business Component" style="zoom:80%;" />

- Autonomous components are like nuget packages

  <img src=".\assets\ac-bc-services.png" alt="AC's, BC's and Services" style="zoom:80%;" />

- Reporting is one of the difficult things to do with SOA as it might spread across the services

- Reporting is not a business capability

- Cascade delete is evil

- Soft delete is a term related to database and signifies bottom up approach

- We must think from Top to bottom from a business capability point of view.

- IT/Ops is the interface to the business

- SOA is for stable business and not for startup who doesn't know what service they are in.

- Don't do CQRS for entire system, do it for subsystem.

- CQRS as an approach is designed for much narrower problem

  <img src=".\assets\cqrs-multi-user-collaboration.png" alt="CQRS - Multi user collaboration" style="zoom:80%;" />

  

- Single writer, multiple reader OR Many writer context

- While working with CQRS, we need to ask question if the domain is collaborative

- A collaborative domain might bring in high contention and it might bring the whole system down.

- When we are reading rows only, database doesn't lock 

- Lot of CQRS is data modelling and data storage technology selection

- The reasons things fail at server side is due to collaboration

- Identify instantaneous and eventual need of user experience

- Think of Reads and Writes separately

- Design commands so that they can't fail

- Partition Tolerant in CAP is it can't be distributed in case we need high availability and consistency

- Running counter in Event Sourcing

- If a transaction fails, and a compensating command is raised, its possible that compensation is not pure.

- Sagas are like message handlers but with state

  <img src=".\assets\saga-problem-flowchart.png" alt="Saga Problem Flowchart" style="zoom:80%;" />

- SAGA should not update master data and it should avoid querying master data

- Sliding window using Timeout

- Don't try to model real world as it doesn't exist

- Sagas are something we should unit test especially the time bound sagas.

- If you are doing TDD, sagas are a good place to do it.

- Unit testing is critical for time bound processes

  

  <img src=".\assets\traditional-architecture.png" alt="Traditional Architecture" style="zoom:80%;" />

- <img src=".\assets\domain-model-pattern.png" alt="Domain Model Pattern" style="zoom:80%;" />

  <img src=".\assets\domain-model-pattern-use-or-not-use.png" alt="Domain Model Pattern - Use or not" style="zoom:80%;" />

- Domain model should be pure, no injecting of repositories as well.

  <img src=".\assets\domain-model-no-dependency.png" alt="Domain Model with no dependency" style="zoom:80%;" />

  <img src=".\assets\domain-model-pojo.png" alt="Domain Model - POJOs" style="zoom:80%;" />

- It's not necessary to use all the patterns of GoF.

- If there is no complex changing things, its not necessary to use Domain Model Pattern

- The above one is an Anemic domain model

  <img src=".\assets\multi-domain-model.png" alt="Multi Domain Model" style="zoom:80%;" />

- Optimistic concurrency: Last one wins is a problematic than first one wins

- Pessimistic concurrency: The person who has lock wins

  <img src=".\assets\realistic-concurrency.png" alt="Realistic Concurrency" style="zoom:80%;" />

- Entity relationship in a domain model exposes us to possible inconsistency

- How do you design your domain model without entity relationship?

- Entities are bad and entity relationship is worse

- Entity may be good for single user system(non-collaborative), but not for distributed systems(collaborative).

- Race condition == Collaboration

- In CQRS, commands don't fail

  <img src=".\assets\realistic-concurrency-tips.png" alt="Realistic Concurrency - Tips" style="zoom:80%;" />

  <img src=".\assets\realistic-concurrency-business-objectives.png" alt="realistic-concurrency-business-objectives" style="zoom:80%;" />

- Always try to find the probability distribution of an action over time.

- Sagas are one of the best implementation of aggregate root, because they have true consistency boundaries

- Whereas an average entity doesn't have a consistency boundary.

  <img src=".\assets\realistic-concurrency-pojo-entities.png" alt="Domain models with entities" style="zoom:80%;" />

- A transaction should sit within that consistency boundary

- Sagas do that, regular entities don't.

- Sagas are like Policies(Refund policy)

- In SOA, we don't end up with lot of entities and process. We end with business capabilities and policies

- True business world is focused on Business process and not on the policy

- SOA aligns business from process and entities to capabilities and policy centric.

- Capability centric via services and policy centric via sagas.

- Rewrites of big thing won't work.

- Rewrite tax

- Rather than going for a big bang rewrite, go with incremental rewrite such as converting a bus to a plane

- Have the rewrite conversation for the budget

- Develop feature by feature

- Ensure business should never stop during this activity of refactoring

- Need to communicate, sell your work and share your wins

- Keep big ball of mud stable, don't do BIG rewrites.

- Going maxim slow as possible and fast as necessary

- Rewrite is attractive as its a blank slate

- Multi-phase Transition plan a fun way

  - First : Setup, Expose and publish events
  - Second: Subscribe events and modify them in case a need arises
  - Third: Scavenge big ball of mud and start creating boundaries 
  - Fourth: Scavenge big ball of DB, reorg, Never stop evolving 
  - Fifth and beyond: Never stop evolving

- dfa

  

## Questions

- On server failure, messages gets accumulated in the queue and once queue is back online, the messages are replayed in a single threaded manner, how can we make it multithreaded ? Also how to handle any failure due to this multithreading?
- How we will persist the model, if there is no dependency on repository? Even interface injection is not allowed.

## References

- das

## Further Reading

- Service Agent Pattern
- Strongly-typed messaging Vs Document-centric messaging
- Return Address Pattern
- Correlated Request/Response
- Service Bus Topic Hierarchies - How to design Topics
- Bus Vs Broker pattern
- 4 + 1 View Architecture
- Referential Integrity Vs Eventual Consistency
- "Disposable" code
- JFHCI
- Competing Consumer Pattern
- Interoperable Protocols : HTTP vs SMTP vs UDP
- SOAP vs WSDL vs REST
- RMI
- Schema is for developer productivity and not for interoperability
- Deadlocks, Livelocks, Race conditions
- Service Agent Problem
- Content based Routing/Document based messaging : Avoid it
- Header based Routing
- Correlation Id
- ETag
- Difference between RabbitMQ and Azure service bus
- Data Deduplication
- Messages/events Out of order
- Most effective way of finding bugs is by code reading
- Log info for immediate retries, warning for every subsequent retry and error on final retry with message going to error queue
- Engine pattern
- Hub and spoke pattern
- Sharding
- Running Counter in Event Souring(ES)
- CAP theorem
- The Engine Pattern
- SAGA 



## Takeaway

- Fallacies of distributed computing
- Benefits of messaging over web service
- Different type of coupling
- Versioning of messages for out-of-order
- Sagas
- Concurrency
- Code walkthrough
- Event Out of order messages
- Bus vs broker architecture style
- Great analogies and case studies
- Amazon checkout page
- Business and Autonomous Component (BC/AC)
- CQRS
- Think of Read and Writes separately
- Evolving from a single user mentality in CRUD based to multiple user in CQRS
- The Engine Pattern
- Compensation is not pure
- Entities are BAD and Entity relationship is worse
- Finding the right boundaries
- Focused on SOA and not on technology/framework/language
- Udi Dahan, the simplicist
- 

## References

- [Workshop (with examples in NServiceBus)](https://github.com/Particular/Workshop)