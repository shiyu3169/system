# Consistent Hashing
What do DynamoDB, Apache Cassandra, Discord, and Akamai CDN have in common? They all use consistent hashing. Now, what is consistent hashing? Why do all the cool kids use it? In this video, we'll learn all about it. Let's dive right in. In a large scale distributed system, data does not fit on a single server. They are distributed across many machines. This is called horizontal scaling. To build such a system with predictable performance, it is important to distribute the data evenly across those servers. A common method to distribute data as evenly as possible among servers is simple hashing. 

This is how it works. First, for each object, we has its key with a hashing function like MD5 or Murmurhash. This maps the object key to a known range of numerical values. A good hashing function distributes the hashes evenly across the entire range.

Second, we perform the modulo operation on the hash against the number of servers. This determines which servers the object belongs to. As long as the number of servers stays the same, an object key will always map to the same server. 

Here's a concrete example. We have four servers with eight string keys. With simple hashing, this is how we distribute the eight string keys among the four servers. Now, this approach works well when the size of the cluster is fixed, and the data distribution is even. But what happens when new servers get added to meet new demand or when existing servers get removed? 

Back to our example, if server 1 goes down, the size of the cluster is now three. Even though the hashes for the object keys stay the same, we are now applying the modulo operation to a different set of n. In this case, it is now three. The impact is pretty drastic. Most of the keys get redistributed. This affects almost all objects, it's not just the objects originally stored in the server that is now offline. 

This triggers a storm of misses and lots of objects to be moved. For situations where servers constantly come and go, this design is untenable. Consistent hashing is an effective technique to mitigate this issue. The goal of consistent hashing is this. We want almost all objects to stay assigned to the same server even as the number of servers changes. Here is the core insight of consistent hashing. 

In addition to hashing the object keys like before, we also hash the server names. The objects and servers are hashed with the same hashing function to the same range of values. In our example, we have a range of x0 to xn. This range is called a hash space. Next, we connect both ends of the hash space to form a ring. This is a hash ring. Using a hashing function, we hash each server by its name or ip address, and place the server onto the ring. 

Here, we place our four servers onto the ring. Next, we hash each object by its key with the same hashing function. Unlike simple hashing where we perform a modulo operation on the hash, here we use the hash directly to map the object key onto the ring. Here is what it would look like for our four objects. To locate the server for a particular object, we go clockwise from the location of the object key on the ring until a server is found. Continue with our example, key 0 is on server 0, and key 1 is on server 1. 

Now let's take a look at what happens when we add a server. Here we insert a new server s4 to the left of s0 on the ring. Note that, only k0 needs to be moved from s0 to s4. This is because s4 is the first server k0 encounters by going clockwise from k0's position on the ring. Keys k1, k2, and k3 are not affected. 

With simple hashing, when a new server is added almost all the keys need to be remapped. With consistent hashing, adding a new server only requires redistribution of a fraction of the keys. 

Let's walk through a quick example of removing a server. When s1 is removed, only k1 needs to be remapped to s2. The rest of the keys are unaffected. 

Let's recap. What have we learned so far: 
1. We map both servers and objects onto the hash ring using a  uniformly distributed hash function.
2. To locate a server for an object, we go clockwise on the ring from the object's position until a server is found. 
   
Now, let's consider a potential issue with this design. The distribution of the objects in the servers on the ring is likely to be uneven. Conceptually, we pick n random points on the ring, we are very unlikely to get a perfect partition of thr ring into equally sized segments. For example, if servers are mapped on the ring like this, most of the objects are stored in s2, with s1 and s3 storing no data. This problem gets worse if servers come and go frequently. 

In our example, even if the servers were originally evenly spaced, if s1 is removed, the segment for s2 is now twice as large as the ones for s0 and s3. 

Virtual nodes are used to fix this problem. The idea is to have each server appear at multiple locations on the ring. Each location is a virtual node representing a server. In this hash ring, we have two servers, with each having three virtual nodes. Instead of having s0 and s1, we now have s0_0, s0_1, and s0_2 to represent server 0, and s1_0, s1_1, and s1_2 to represent server 1 on the ring. With virtual nodes, each server handles multiple segments on the ring. In our example, the segments labeled s0 are managed by server 0, and those labeled s1 are handled by server 1. In real world systems, the number of virtual nodes is much larger than three. As the number of virtual nodes increases, the distribution of objects becomes more balanced. 

Having more virtual nodes means taking more space to store the metadata about the virtual nodes. This is a trade-off, and we can tune the number of virtual nodes to fit our system requirements. 

Let's see how consistent hashing is used in the real world. Some popular NoSQL databases like Amazon DynamoDB and Apache Cassandra use consistent hashing, where it is used for data partitioning. It helps these databases minimize data movement during rebalancing. Content delivery networks like Akamai use consistent hashing to help distribute web contents evenly among the edge servers. Load balancers like Google Load Balancer use consistent hashing to distribute persistent connections evenly across backend servers. This limits the number of connections that need to be re-established when a backend server goes down. 