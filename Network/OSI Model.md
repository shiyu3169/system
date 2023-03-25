# OSI Model

The OSI Model, or the Open Systems Interconnect model, is a theoretical framework that provides one way of thinking about networking. It splits the network communication between two devices on a network into seven abstraction layers. 

## Physical Layer
The physical layer is the bottom-most layer. It is responsible for transmitting raw bits of data across a physical connection. 

## Data link Layer
The data link layer is the second layer. It takes the raw bits from physical layer and organizes them into frames. It ensures that the frames are delivered to the correct destination. The Ethernet primarily lives in this layer. 

## Network Layer
The network layer is the third layer. It is responsible for routing data frames across different networks. The IP part of TCP/IP is a well-known example of this layer.

## Transport Layer
The transport layer is the fourth layer. It handles end-to-end communication between two nodes. This is the layer where TCP and UDP live. 

### TCP
TCP provides reliable, end-to-end communication between devices. It does this by dividing the data into small, manageable segments and sending each segment individually. Each segment has a sequence number attached to it. The receiving end uses the sequence numbers to reassemble the data in the correct order. TCP also provides error checking to make sure that the data was not corrupted during transmission. 

### UDP
UDP is another popular protocol in the transport layer. It is similar to TCP, but it is simpler and faster. Unlike TCP, UDP does not provide the same level of error-checking and reliability. It simply sends packets of data from one device to another. The receiving end is responsible for determining whether the packets were received correctly. If an error is detected, the receiving and simply discards the packet. 

## What else?

The remaining layers are the session, presentation, and application layers. This is where the OSI model loses its usefulness in practice. They are too fine-grained and do not really reflect reality. In general, it is sufficient to collapse them into a single layer and consider application protocols like HTTP as simply layer 7 protocols.


## Example
Let's go though an example and examine how data moves through the layers when transmitting over the network. When a user sends an HTTP request to a web server over the network, the HTTP header is added to the data at the application layer. Then a TCP header is added to the data. It encapsulated into TCP segments at the transport layer. The header contains the source port, destination port, and sequence number. The segments are then encapsulated with an IP header at the network layer. The IP header contains the source and destination IP addresses. A MAC header is added at the data link layer, with the source and destination MAC addresses. It is worth noting that in the real world this is a bit nuanced. The MAC addresses are usually not the MAC address of the sending and receiving ends. They are the MAC address of the routing devices in the next hop of a usually long journey across the internet. The encapsulated frames are sent over the network in raw bits in the physical layer. When the web server receives the raw bits from the network, it reverses the process. The headers are removed layer by layer, and eventually the web server processes the HTTP request. 

## Conclusion
To conclude, the OSI model is one way of thinking about networks. Its primary purpose is educational. Even though the layers don't fit the real-world use cases perfectly, they are still widely used by networking vendors and cloud providers as a shorthand to describe where their networking products sit in the OSI model. For example, cloud load balancers are broadly divided into two categories - L4 or L7. An L7 load balancer is a shorthand to mean that the load balancer operates at the application protocol layer like HTTP or HTTPS. An L4 load balancer, on the other hand, operates at the TCP level. 