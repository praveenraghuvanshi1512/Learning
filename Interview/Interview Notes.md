# Interview Notes

## Application

- Performance
- Memory
- Concurrency
  - Deadlocks
- Multithreading

## Cloud

- Reliability/Resiliency
  - Queue
  - Retry : Immediate, incremental
- Scalability
- Availability
- Fault Tolerance
- Monitoring
- Troubleshooting
  - App Insights(Group)

## General

- Three V's - Velocity, Variety and Volume

- Project Architecture: Process, Solution and Technology

  <img src=".\assets\project-architecture.png" alt="Project Architecture" style="zoom:80%;" />

  

  <img src=".\assets\process-architecture.png" alt="Process Architecture" style="zoom:80%;" />

  

  <img src=".\assets\solution-architecture" alt="Solution Architecture" style="zoom:80%;" />

  

  <img src=".\assets\tech-archtiecture.png" alt="Technology Architecture" style="zoom:80%;" />

  

  <img src=".\assets\unified-solution.png" alt="Unified Solution" style="zoom:80%;" />

- fad

## Use cases

### Cloud

- Azure

  - Service Bus

    1. Error: **Microsoft.Azure.ServiceBus.MessageSizeExceededException**

       "The received message (delivery-id:0, size:289349 bytes) exceeds the limit (262144 bytes) currently allowed on the link.

       This is the issue caused by an event/message of size 289KB which is greater than defined limit of 256 KB in Azure service bus.

       Solution:

       

    2. Best Practices : https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-performance-improvements?tabs=net-standard-sdk

    3. Failing to process a message. 

       There is a possibility that messages are not handled properly in registered handlers due to a bug in code or something similar. In that case, service bus queue might throttle and can be easily seen in service bus explorer as pending messages.

    4. **Message Throttling:** Generally happens when there is an issue in processing a message by the server and client keeps on sending the messages. The messages gets accumulated in the messaging queue. It might be due to service unavailable or a bug in processing the message by the service
    
    5. A tool to monitor the DLQ and send an email beyond a threshold.