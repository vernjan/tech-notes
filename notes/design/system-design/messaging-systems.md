# Messaging Systems
- asynchronous cross-service communication - producer pushes the message and immediately continues
- types
    - **point-to-point** (FIFO or priority queue)
    - **publish-subscribe** (topics)
- AMQP, STOMP
- RabbitMQ, ActiveMQ, Apache Kafka, Amazon SQS, Azure Service Bus

## Sources
- [System Design — Message Queues](https://medium.com/must-know-computer-science/system-design-message-queues-245612428a22) (Medium blog)
- [Demystifying Apache Kafka Message Delivery Semantics](https://keen.io/blog/demystifying-apache-kafka-message-delivery-semantics-at-most-once-at-least-once-exactly-once/) (Keen blog)
- [You Cannot Have Exactly-Once Delivery](https://bravenewgeek.com/you-cannot-have-exactly-once-delivery) (BRAVE NEW GEEK)

## Use cases
- **fault-tolerance** - the receiver can be offline
- **buffering of messages** (handling peak loads)
- **loose coupling of services**
- **enable scaling** - connect many producers to many consumers
- **publish-subscribe model** (broadcast, fanout)
- **batching**

## Producer delivery semantics
- **async** - fire and forget, producer sends data and continues, no guarantees, fast, good for metrics
- **committed to leader** - persisted on leader
- **committed to leader and quorum** - slowest, most durable

## Consumer delivery semantics
- consumer can read only those messages that have been written to a set of in-sync replicas
    - i.e. not influenced by producer delivery semantics

- **at-most-once** - 0 or 1
    - message offset number is increased and committed to the broker upon receiving
    - if the consumer fails to receive or process the message, it is "lost"
    - default in Kafka
    - good for reading IoT sensors or some other not critical data
- **at-least-once** - 1 or more
    - message offset number is increased and committed to the broker after processing
    - message gets always delivered, possible multiple times
    - worse performance (retries, acknowledgments)
- **exactly-once** - 1
    - message cannot be dropped nor duplicated
    - hard to achieve - consumer must be transactional - increase offset number upon transaction commit
    - highest implementation overhead