# Cache
Caching is a common technique in modern computing to enhance system performance and reduce response time. From the frontend to the backend, caching plays a crucial role in improving the efficiency of various applications and systems. A typical system architecture involves several layers of caching. At each layer, there are multiple strategies and mechanisms for caching data depending on the requirements and the constraints of the specific application. 


## Hardware cache
Before diving into a typical system architecture, let's zoom in and look at how prevalent caching is within each computer itself. Let's first look at the computer hardware. The most common hardware caches are L1, L1, and L3 caches. 

### L1
L1 cache is the smallest and fastest cache typically integrated into the CPU itself. It stores frequently accessed data and instructions allowing the CPU to quickly access them without having to fetch them from slower memory. 

### L2
L2 cache is larger but slower than L1 cache. It is typically located on the CPU die. 

### L3 
L3 cache is even larger and slower than L2 cache. It is often shared between multiple CPU cores.


### Translation Lookaside Buffer
Another common hardware cache or TLB. It stores recently used virtual to physical address translations. It is used by the CPU to quickly translate virtual memory addresses to physical memory addresses reducing the time needed to access data from memory.

## Operating System Cache
At the operating system level, there are page cache and other file system caches.

### Page Cache
Page cache is managed bu the operating system and resizing main memory. It is used to store recently used disk blocks in memory. When a program requests data from the disk, the operating system can quickly retrieve the data from memory instead of reading it from disk.

### Inode Cache
There are other caches managed by the system, such as the inode cache. These caches are used to speed up file system operations by reducing the number of disk accesses required to access files and directories. 


## Application System Architecture Cache
Now let's zoom out and look at how caching is used in a typical application system architecture. 

### Frontend
On the application front end, web browser can cache HTTP responses to enable faster retrieval of data when we request data over HTTP for the first time and it is returned with an expiration policy in HTTP header. We request the same data again, and the browser returns the data from its cache if available.

### Content Deliverable Network
Content Deliverable Network (CDN) is widely used to improve the delivery of static content such as images, videos, and other web access. One of the way that CDNs speed up content delivery is through caching. When a user requests contents from a CDN. The CDN Network looks for the requested content in its cache. If the content is not already in the cache, the CDN fetches it from the origin server and caches it on its edge servers. When another user requests the same content, the CDN can deliver the content directly from his cache eliminating the need to fetch it from the origin server again.

### Load Balancer
Some load balancers can cache resources to reduce the low on backend servers. When a user requests content from a server behind a load balancer, the load balancer can cache the response and serve it directly to future users who request the same content. This can improve response time and reduce the low on backend servers. 

### Disk Cache
Caching does not always have to be in memory. In messaging infrastructure, message broker such as Kafka can cache a massive amount of messages on disk. This allows consumers to retrieve the messages at their own pace. The messages can be cached for a long period of time based on the retention policy.

### Distributed Caches
Distributed caches such as Redis can store key value pairs in memory providing high read, write performance compared to traditional databases. 

### Full Text Engines
Full text engines such as elasticsearch can index data for document search and log search providing quick and efficient access to specific data

### Database
Even in the database, there are multiple levels of caching available. Data is typically written to a wirehead log before being indexed in a b tree. The buffer pool is a memory area used to cache query results while materialized views can pre-compute query results for faster performance. The transaction log records all transactions and updates to the database while the replication log tracks the replication state in a database cluster. 

## Summary
Overall caching data is an essential technique for optimizing system performance and reducing response time. From frontend to the backend, there are many layers of caching to improve the efficiency of various applications and systems