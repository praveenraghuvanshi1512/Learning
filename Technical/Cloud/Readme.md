##  Cloud Learning

 

| S.No. | Topic                                                        | Date          | Mode   | Cloud | Resource | Remarks                                                      |
| ----- | ------------------------------------------------------------ | ------------- | ------ | ----- | -------- | ------------------------------------------------------------ |
| 1     | [Azure Messaging Crossroads](https://particular.net/webinars/azure-messaging-crossroads) | 22-March-2020 | Online | Azure |          | Different messaging solutions within Azure - Storage Queues, Service Bus, Event Grid, Event Hubs, etc. |
|       |                                                              |               |        |       |          |                                                              |
|       |                                                              |               |        |       |          |                                                              |



## Notes

**1. Azure Messaging Crossroads**

<img src=".\Azure_Messaging_Crossroads\azure-messaging-types.png" alt="Azure Messaging Types" style="zoom:50%;" />

- Send a Message

  <img src=".\Azure_Messaging_Crossroads\storage-queue-service-bus.png" alt="Send a Message - Storage Queue and Service Bus" style="zoom:50%;" />

- Publish an Event

  <img src=".\Azure_Messaging_Crossroads\publich-event.png" alt="Publish an event" style="zoom:50%;" />

- Azure SignalR seems like a messaging service, but its not durable.

- Messages are not stored anywhere and we'll loose it if delivery fails

  <img src=".\Azure_Messaging_Crossroads\azure-signalr.png" alt="Azure SignalR" style="zoom:50%;" />

- **Storage Queues(a.k.a Simple Queues)**

  <img src=".\Azure_Messaging_Crossroads\storage-queue-simple.png" alt="Storage Queue a.k.a Simple Queue" style="zoom:50%;" />

  <img src=".\Azure_Messaging_Crossroads\storage-queue-details.png" alt="Storage Queue Details" style="zoom:50%;" />

- Its not intended for sophisticated scenario

- Messages contain data and senders have expectations in the sense they expect some command to be executed by receiver

- Service is implemented on top of Http

- Message size is 64kb considering we are only sending small amount of data only. 

  <img src=".\Azure_Messaging_Crossroads\storage-queue-limitations.png" alt="Storage Queue Limitations" style="zoom:50%;" />

- Limited features means compute features

- No headers/metadata: The payload sent by storage queue is the only data.

- Need to encode in the payload

- No Pub/Sub: Sending messages to a single destination

- No Scheduling: Impossible to send a message in Future.

- No Dead-lettering

- No transactional guarantees

- Cannot peek more than 32 messages : for production 

- The intent of Storage queue is tasks, tasks that are fast 

- Only 7 days retention period

  <img src=".\Azure_Messaging_Crossroads\storage-queue-action.png" alt="Storage Queue in Action" style="zoom:50%;" />

  ![image-20200322030307318](.\Azure_Messaging_Crossroads\storage-queue-remember.png)

- **Azure Service Bus**

  ![Service Bus Introduction](.\Azure_Messaging_Crossroads\service-bus-intro.png)

- Also known as Enterprise Service Bus

- Example is an E-Commerce website

- Customers have orders which are processed at backend

- Communication between frontend and backend is done view Service Bus (Queue/Topic/Subscription)

- Its done for loose coupling and scalability as both frontend and backend can be scaled individually

- Three types of entities : Queue/Topic/Subscription

- For e.g on black friday, we wanted to scale out FE and not necessarily BE.

- We expect certain guarantee for orders/money/transactions.

  <img src=".\Azure_Messaging_Crossroads\service-bus-features.png" alt="Service Bus features" style="zoom:50%;" />

- Message Headers/Metadata:

  - Indicate what type of serialization is used
  - Add additional data that describe how to process the message
  - It could be used to manipulate routing of message

- Duplicate Detections

  - Same purchase order received multiple times
  - Duplication is performed based on message Id and not on the payload. Workaround is to create a hash of payload and assign to Message Id

- Auto-forwarding

  - Ability to transmit message not only to single queue but multiple

- Dead-lettering

  - Puts messages that are continuously failing to dead letter queue
  - Message could be poisonous message
  - There might be a bug in our code that is not handled properly

- Scheduled delivery

  - Messages can be scheduled for future.

- Message Expiration

  - Messages can be purged if they are processed by certain amount of time.

- Message Deferral

  - Message is received by not capable of being processed as of now. Need to defer the message
  - Message is kept aside under some conditions and will be picked up later when receiver is ready to process

- Auto-delete on Idle

  - Delete both message and queue if there was not action on queue for certain amount of time

- Batching 

- Transactions

  - Not like DB transactions
  - More of a transaction between input and output messages
  - Input and output message is transacted in a atomic way

- Message sessions

- Pub/Sub : being able to decouple sender and receiver

- Filtering and Actions: 

- Claim Check

- Standard and Premium tier difference is message size

  <img src=".\Azure_Messaging_Crossroads\azure-servicebus-client-features.png" alt="Azure service bus client features" style="zoom:50%;" />

- Lock renewal

  - Message bus does not allow locking unlimited queues.
  - Message is generally released after 5 mins.
  - In case processing takes more than 5 mins, lock can be renewed.
  - We need to be careful, as lock renewal is not a guaranteed operation.
  - Its not initiated by broker, but initiated by client, means if there is a connectivity issue, renewal can fail and message will loose its lock and will be available for other competing consumers.

- Java Messaging Service(JMS) support

  <img src=".\Azure_Messaging_Crossroads\service-bus-premium-features.png" alt="Service bus - Premium features" style="zoom:50%;" />

- Premium Features

  - Scale Up(MUs)
    - The ability to control scaling up and down, also known as Messaging Units(MUs)
    - When a premium namespace is provisioned, an instance of service bus, we can specify no of messaging units
    - MUs starts with 1 and goes till 8.
    - With this we are specifying a throughput and latency
    - Usually based on the no of messages on throughput, we'll be able to scale up and down the system
  - Geo-DR
    - Handles failover 
    - Failover due to site failure
  - Availability Zones
    - It serves the purpose of High Availability
    - There will be 3 replicas of eveything
    - It handles failure within a site or zone.
  - Virtual Network Service Endpoints
    - Its to make sure there are virtual networks in the Azure
    - It ensures that none of the networks are travelling through public network
  - Metered Throttling
    - It can be defined at what point to scale up/down
    - Throttling will occur if there is high utilization of CPU and Memory
    - Azure monitor will help in checking 
    
    
    

- <img src=".\Azure_Messaging_Crossroads\service-bus-migration.png" alt="Service Bus Migration" style="zoom:50%;" />

- Migrating from Standard to Premium tier

  - No Downtime
  - Additional namespace is required to be provisioned for premium
  - Supports upto 1000 entities
  - For more than 1000, connect with service bus support

  <img src=".\Azure_Messaging_Crossroads\service-bus-conclusion.png" alt="Service Bus Conclusion" style="zoom:50%;" />

- Remember

  - Queues and Topics: No single destination, broadcast mechanism
  - Rich Compute based features
  - Only service that has transactionality on the message level
  - Extremely reliable
  - Allows implementing complex workflows(Auto-forwarding)
  
- **Event Hub**

  <img src=".\Azure_Messaging_Crossroads\eventhub-banner.png" alt="Event Hub" style="zoom:50%;" />

  ​	<img src=".\Azure_Messaging_Crossroads\eventhub-features.png" alt="Event Hub Features" style="zoom:50%;" />

  - Event hub is like a cassette tape

  - It doesn't handle messages, it handles them as stream

  - You can play stream over and over again. We can retrieve messages any time by them again

    <img src=".\Azure_Messaging_Crossroads\eventhub-architecture.png" alt="Event Hub Architecture" style="zoom:50%;" />

  - Event Hub has partitions and and each partition record different messages which are streams of messages

  - Event are produced by different sources with different protocols such as Http, AMQP and Kafka

  - On the receiving side, we have Consumer groups to read the events via streams

  - The flow of message is not from event hub to receiver. Its vice-versa. Receiver need to pull messages

  - We can have multiple receivers with different consumer groups

    <img src=".\Azure_Messaging_Crossroads\eventhub-kafka.png" alt="Event Hub Vs Kafka" style="zoom:50%;" />

  - Event hub is similar to Kafka

  - Both are ingesting technologies, they are not queue

  - Storage queue and Service bus are queueing service

  - Event hub is an ingestor and not a queue

  - Client manages the cursor and not the other way around

  - Client needs to remember location of last message in the stream that they have processed already as opposed to storage queue and service bus services which will remember what message needs to be sent to client which is asked

    <img src=".\Azure_Messaging_Crossroads\eventhub-kafka1.png" alt="Event hub compatibility" style="zoom:50%;" />

    <img src=".\Azure_Messaging_Crossroads\eventhub-scaling.png" alt="Event Hub Scaling" style="zoom:50%;" />

  - Event hub scaling

    - Throughput units(TUs)

    <img src=".\Azure_Messaging_Crossroads\eventhub-auto-inflation.png" alt="Event Hub - Auto Inflation" style="zoom:50%;" />

  - Event hub has only 7 days retention 

    ![Event Hub - Capture](.\Azure_Messaging_Crossroads\eventhub-capture.png)

    <img src=".\Azure_Messaging_Crossroads\eventhub-capture-working.png" alt="Event Hub - Capture working" style="zoom:50%;" />

  - How Capture works

    - We have Event Hub with partitions and have the data.
    - We define capture rule for storage account
    - We usually need a container to be defined with two parameters - size and time
    - For e.g we can specify size of blob file should not be more than 100 MB Or Time should not exceed 10 mins.
    - So whatever comes first will generate a blob and those blobs are automatically generated as the data streams into event hub
    -  
    - 

    <img src=".\Azure_Messaging_Crossroads\eventhub-helpers.png" alt="Event Hub - Helpers" style="zoom:50%;" />

    <img src=".\Azure_Messaging_Crossroads\eventhub-conclusion.png" alt="Event Hub - Conclusion" style="zoom:50%;" />

  - **Event Grid**

    <img src=".\Azure_Messaging_Crossroads\eventgrid-banner.png" alt="EventGrid" style="zoom:50%;" />

    <img src=".\Azure_Messaging_Crossroads\eventgrid-traditional.png" alt="EventGrid-Traditional" style="zoom:50%;" />

    - Traditionally we need to poll 24x7 for new events even if there are no events happening.

      <img src=".\Azure_Messaging_Crossroads\eventgrid-event.png" alt="EventGrid - Event" style="zoom:50%;" />

    - 

    - Most of the earlier messaging services are based on Pull model.

    - Push model is easier to comprehend and makes much more sense in Reactive systems

      <img src=".\Azure_Messaging_Crossroads\eventgrid-need.png" alt="EventGrid - Need" style="zoom:50%;" />

    - Serverless apps is a good use case where it needs to operate/process on a trigger

      <img src=".\Azure_Messaging_Crossroads\eventgrid-services.png" alt="EventGrid - Services" style="zoom:50%;" />

    - Event Grid is the man in the middle

    - Cloud Events are the events originated from any cloud providers

    - Event Grid has inbuilt services such as Key-vault, Machine Learning and SignalR

    - Preview services such as Azure App Service, Redis

      <img src=".\Azure_Messaging_Crossroads\eventgrid-concepts.png" alt="Eventgrid Concepts" style="zoom:50%;" />

      <img src=".\Azure_Messaging_Crossroads\eventgrid-schema.png" alt="Eventgrid Schema" style="zoom:50%;" />

      

    - Message size is 64KB earlier and now it can grow to 1MB

    - Charge happens based on no of 64K chunks
    
      ![Eventgrid - Filtering](.\Azure_Messaging_Crossroads\eventgrid-filtering.png)
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-domains.png" alt="Eventgrid - Domains" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-different.png" alt="Eventgrid - Difference" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-cloud-native.png" alt="Eventgrid - CloudNative" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-scale.png" alt="Eventgrid -  Scale" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-deadletter.png" alt="Eventgrid - DeadLetter" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-cloud-events.png" alt="Eventgrid CNCF Cloud Events" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-cncf-schema.png" alt="Eventgrid - Cloud event schema" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\eventgrid-conclusion.png" alt="Eventgrid - Conclusion" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\messages-serverless-queue-eventgrid.png" alt="Serverless - Storage queue and Event grid" style="zoom:50%;" />
    
    - With Serverless, Storage Queue and Event grid are good choice
    
      <img src=".\Azure_Messaging_Crossroads\bigdata-eventhub.png" alt="Bigdata-eventhub" style="zoom:50%;" />
    
      <img src=".\Azure_Messaging_Crossroads\enterprise-service-bus.png" alt="Enterprise - Service Bus" style="zoom:50%;" />
    
    - Enterprise systems: Service Bus 
    
    - When system is not interacting with external systems
    
    - <img src=".\Azure_Messaging_Crossroads\service-bus-event-grid.png" alt="Service Bus Event Grid" style="zoom:50%;" />
    
    - 

## Questions

- What is the size of MUs in our application?
- We already have blob trigger, still why do we need EventGrid?
- 

## Further Reading

- Poisonous messages
- Dead letter queue
-  Message expiration and deferral
- Claim Check pattern
- Message Units(MUs)
- Event Hub
  - Throughput Units(TUs)
  - Auto Inflation
  - Event Hub Capture
- EventGrid
  - Topic
  - Atleast once delivery
- Service Bus + Event Grid
- [DIY Async Message Pump: Lessons from the trenches](https://particular.net/webinars/diy-async-message-pump-lessons-from-the-trenches)

