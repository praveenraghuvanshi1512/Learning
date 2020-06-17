# Interview Notes

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

       