# Latency Numbers
It is not critical to know the exact numbers. Developing a sense of the relative orders of magnitude difference between these things is way more important. Some of these numbers like disk seek time have changed drastically as technology evolves, while others like network latency between countries stay pretty consistent because they have to obey the laws of physics. We will group the latency numbers by order of magnitude, starting with sub-nanoseconds, all the way up to seconds. 

To lay the groundwork, let's get a sense of what these time units are first. 
* nanosecond = 10^-9 = 1/1,000,000,000 second
* microsecond = 10^-6 = 1/,1000,000 second
* millisecond = 1^-3 = 1/1,000 second

## 1ns - 10ns
Accessing CPU registers is sub-nanosecond. It is super fast to access CPU registers, but there are very few of them. A clock cycle of a modern CPU is also in the sub-nanosecond range. In the 1 to 10 ns range, we have L1 and L2 cache accesses. Some expensive CPU operations are also in this range. Something like a branch mispredict penalty could cost up to 20 CPU clock cycles, which is also in this range.

## 10ns - 100ns
The next range is 10 to 100ns. L3 cache access is usually at te fast end of this range. For a modern processor like the Apple M1, referencing main memory is at the slow end of this range. In other words, main memory access on a modern CPU is a few hundred times slower than CPU register access. 

## 100ns to 1ms
The next range is from 100ns to 1 microsecond. The most useful thing to know in this range is the cost of a system call. On Linux, making a simple system takes several hundred nanoseconds. This is just the direct cost of the trap into the kernel and back, it does not count for the cost of executing the system calls themselves. It takes about 200ns to md5 hash to a 64-bit number.

## 1us - 10us
Next up, the 1 to 10 us range. We've reached the level where things are about a thousand times slower than a CPU register access. Context switching between Linux threads takes at least a few microseconds. This is about the best-case scenario. Depending on the workload, if the context switch involves bringing pages of data from memory for the new thread, it could take significantly longer. To put it in perspective, copying 64KB from one main memory location to another also takes a few microseconds. 

## 10us - 100us
The next up is 10 to 100 microseconds. At this level, things are slow enough that we can start to include some higher-level operations. A network proxy like Nginx would take about 50 microseconds to process a typical HTTP request. Reading 1MB of data sequentially form the main memory takes about 50 microseconds. The read latency of the SSD is in this range, taking about 100 microseconds to read an 8K page. 

## 100us - 1ms
The next range is 100us to 1ms. This range has some interesting things. The SSD write latency is about 10 times slower than the read latency, and it is at the top end of this range, taking close to a millisecond to write a page. Intra-zone network round trip for modern cloud providers takes a few hundred micro seconds. This is one of the numbers updated for the 2020s. These days they trend closer to the fast end, some even clocked in at less than 100 microseconds. A typical memcache or Redis get operation takes about 1 millisecond as measured by the client. This includes the network round trip mentioned above. 

## 1ms - 10ms
Next up, 1 to 10ms. Inter-zone network round trip of the modern cloud is in this range. The seek time of the hard disk drive is about 5 milliseconds. It takes time to move the arms. 

# 10ms - 100ms
The next range is 10 to 100ms. The network round trip between the US east and west coast, or the US east coast and Europe is in this range. So is reading 1GB sequentially from main memory. 

# 100ms - 1s
There are several interesting things in the 100 to 1000 ms range. Using a slow hash function like bcrypt to encrypt a password. It takes 300ms to bcrypt a password. it is slow enough to render brute force password cracking ineffective. TLS handshake is typically in the 250ms to 500ms range. It adds several network round trips so the number depends on the distance between the machines. The network round trip between the US west coast and Singapore is in this range. Reading 1GB sequentially from an SSD is also in this range. 

# Over 1s
Lastly, here's an example of something taking over a second. Transferring 1GB over the network within the same cloud region takes about 10 seconds. 