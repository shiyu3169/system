# Top 7 Most-Used Distributed System Patterns

## Ambassador
Picture yourself as a busy CEO with a personal assistant who handles all your appointments and communication. That's precisely what the Ambassador pattern does for your application. It acts as a "go-between" for your app and the services it communicates with, offloading tasks like logging, monitoring, or handling retries. For instance, Kubernetes uses Envoy as a Ambassador to simplify communication between services. The Ambassador pattern can help reduce latency, enhance security, and improve the overall architecture of your distributed systems.

## Circuit Breaker
Imagine a water pipe bursting in your house. The first thing you'd do is shut off the main value to prevent further damage. The Circuit Breaker pattern works similarly, preventing cascading failures in distributed systems. When a service becomes unavailable, the Circuit Breaker stops requests, allowing it to recover. Netflix's Hystrix library uses this pattern. It ensures a more resilient system. This pattern can be particularly useful when dealing with microservices or cloud-based applications, where failures are more likely to occur.

## CQRS (Command Query Responsibility Segregation)
CQRS is like having a restaurant with separate lines for ordering food and picking up orders. By separating the command, or write operations from the query, or read operations, we can scale and optimize each independently. An e-commerce platform might have high read requests for product listings but fewer write requests fro placing orders. CQRS allows each operation to be handled efficiently. This pattern becomes especially valuable in systems where read and write operations have different performance characteristics, with different latency or resource requirements. 

## Event Sourcing
Think of Event Sourcing as keeping a journal of the life events. Instead of updating a record directly, we store events representing changes. This approach provides a complete history of the system and enables better auditing and debugging. Git version control is a great example of Event Sourcing, where each commit represents a change. With Event Sourcing, we can also implement advanced features like time-travel debugging or replaying events for analytics purposes. 

## Leader Election
Imagine a classroom of students electing a class representative. In a distributed system, the Leader Election pattern ensures only one node is responsible for a specific task or resource. When a leader node fails, the remaining nodes elect a new leader. ZooKeeper and etcd use this pattern to manage distributed configurations. By having a designated leader, we can avoid conflicts and ensure consistent decision-making across the distributed system. 

## PubSub
The Publisher/Subscriber pattern is like a newspaper delivery service. Publishers emit events without knowing who'll receive them, and subscribers listen for events they're interested in. This pattern allows for better scalability and modularity. For example, Google Cloud Pub/Sub enables asynchronous messaging between services, making it easier to maintain and scale complex applications. Pub/Sub systems are well-suited for scenarios where we need to propagate changes or updates across multiple components, for example, updating a user's profile across various services. 

## Sharding
Sharding is like dividing a large pizza into smaller slices, making it easier to handle. It's a technique for distributing data across multiple nodes in a system. It improves performance and scalability. Each shard contains a subset of the data, reducing the load on any single node. Databases like MongoDB and Cassandra use sharding to handle large amounts of data efficiently. Sharding can also help us achieve better data locality, reducing network latency and speeding up query execution. 

## Bonus: Strangler Fig Pattern
This pattern is inspired by the strangler fig tree, which grows around other trees and eventually replaces them. In software, the Strangler Fig pattern is a method for gradually replacing legacy systems with new implementations. Instead of performing a risky "big bang" migration, we can incrementally replace parts of the old system with new components. This approach can help us manage the risks and complexities associated with system migrations. 