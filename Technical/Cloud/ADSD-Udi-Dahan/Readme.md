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

- fdasf

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
- Srevice Agent Problem
- Content based Routing/Document based messaging : Avoid it
- Header based Routing
- 

