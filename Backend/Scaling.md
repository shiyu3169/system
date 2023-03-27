# Scaling

## Scenario
In this example, we have a machine that is running some web application for your company with stand request model. It works very well at beginning. However, you get more customers and the number of customers that accessing your application concurrently starts to grow very rapidly and you find that latency for API calls are starting to degrade from 500ms to 2 or 3 seconds. 

## How do we fix this problem? 
We can fix this problem by modifying some "scalable dimensions":
1. Concurrent Connections
2. CPU
3. Memory (Quantity + Speed)
4. Network Interfaces

If we don't have a bound on CPU or memory or anything like that we can just increase the concurrent connections that we can handle more traffic at a given point in time. Eventually, you will figure out you will hit some very real physical maximum where if you increase that  amount of concurrent connections too high, your hardware maximum will be reached, so your CPU maximum will be reached. If that's the case, your CPU utilization is running really high. How do you fix that? Well, you can just throw a better CPU, right? You can upgrade to maybe an i5 or an i7. And you can alleviate the pressure on your machine that way so now you're able to handle all this additional traffic, right?

Another dimension is memory.Giving a very memory intensive application, you can increase both the quantities to add an additional stick, or maybe increase the frequency or the speed of your memory, so that it can be quicker. And finally maybe you want to modify the network interface. Adding a better ethernet card to make sure it can handle more traffic and give a quicker response back to your client.

The above dimensions are physical modifications that we can make to our hardware to increase its capacity so they can serve more traffic. So what are the problems with this? What if this machine ever goes down?