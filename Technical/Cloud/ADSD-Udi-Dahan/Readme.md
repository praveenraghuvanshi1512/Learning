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

- 

## Questions

- On server failure, messages gets accumulated in the queue and once queue is back online, the messages are replayed in a single threaded manner, how can we make it multithreaded ? Also how to handle any failure due to this multithreading?

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



## Takeaway

- Fallacies of distributed computing
- Benefits of messaging over web service
- Different type of coupling
- Versioning of messages for out-of-order
- Sagas
- Concurrency
- 

