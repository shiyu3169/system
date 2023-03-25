# CAP Theorem
## What is CAP Theorem
The CAP theorem is a concept in computer science that explains the trade-offs between consistency, availability, and partition tolerance in distributed systems.

### Consistency
Consistency refers to the property of a system where all nodes have a consistent view of the data. It means all clients see the same data at the same time no matter which node they connect to.

### Availability
Availability refers to the ability of a system to respond to requests from users at all times.

### Partition Tolerance
Partition tolerance refers to the ability of a system to continue operating even if there is a network partition.

#### Network partition
A network partition happens when nodes in a distributed system are unable to communicate with each other due to network failures. 

when there is a network partition, a system must choose between consistency and availability. If the system prioritizes consistency, it may become unavailable until the partition is resolved. It the system prioritizes availability, it may allow updates to the data. This could result in data inconsistencies until the partition is resolved.

### Example
We have a tiny bank with two ATMs connected over a network. The ATMs support three operations: deposit, withdraw, and check balance. No matter what happens, the balance should never go below zero. There is no central database to keep the account balance. It is stored on both ATMs. 

When a customer uses an ATM, the balance is updated on both ATMs over the network. This ensures that the ATMs have a consistent view of the account balance. If there is a network partition and the ATMs are unable to communicate with each other, the system must choose between consistency and availability. 

If the bank priority consistency, the ATM may refuse to process deposits or withdrawals until the partition is resolved. This ensures that the balance remains consistent, but the system is unavailable to customers.

If the bank prioritizes availability, the ATM may allow deposits and withdrawals to occur, but the balance may become inconsistent until the partition is resolved. When there is a network partition, the customer could withdraw the entire balance from both ATMs. When the network comes back online, the inconsistency is resolved and now the balance is negative. That is not good.

### Example 2
Let's go though another example and see how a social media platform could apply the CAP theorem. 

During a network partition, if two users are commenting on the same post at the same time, one user's comment may not be visible to the other user until the partition is resolved. 

Alternatively, if the platform prioritizes consistency, the commenting feature may be unavailable to users until the partition is resolved. For a social network, it is often acceptable to prioritize availability at the cost of users seeing slightly different views some of the time.

### Summary
The CAP theorem may sound very simple, but the real world is messy. As with many things in software engineering, it is all about tradeoffs, and the choices are not always so black and white. The CAP theorem assumes 100% availability or 100% consistency. In the real world, there are degrees of consistency and availability that distributed system designers must carefully consider. This is where the simplistic model of the CAP theorem could be misleading.

Back to the back example, during a network partition, the ATM could allow only balance inquires to be processed, while deposits or withdrawals are blocked. 

Alternatively, the bank could implement a hybrid approach. For example, the ATM could allow balance inquires and small withdrawals to be processed during a partition, but block large withdrawals or deposits until the partition is resolved. 

It is worth noting that in the real word, reconciliation after a network partition could get very messy. The bank example above is simple to reconcile. In real life, the data structures involved could be complex and challenging to reconcile.

A good example of complex data structure is Google Docs. Resolving conflicting updates could be tricky.

So, is CAP theorem useful? Yes, it is useful tool to help us think through the high-level trade-offs to consider when there is a network partition. This is a good starting point, but it does not provide a complete picture of the trade-offs to consider when designing a well-rounded distributed system. Specifically, when the system is operating normally without any network failure, which is most of the time, there is an entire set of interesting trade-offs to consider between latency and consistency. This is covered by the PACELC theorem.