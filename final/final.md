# NOT DONE
In general, an application-layer protocol does NOT define:

Rules of when and how a message is sent or received
The content of the format of message exchange

1. The syntax of various message types
2. ~~The sequence of message exchanged~~
3. The type of messages exchanged
4. The usage of each field
5. The format of the message exchanged

### FILL
You are installing Git, a screen shows the following:

This means Git uses HTTPS, a secure communication ________

1. **PROTOCOL**

where two machines can communicate securely over the network by encrypting the data in the _________

1. ~~TRANSPORT~~

layer to provide privacy and data integrity between two or more communicating computer applications.

### FILL
Content creators upload to Youtube several million videos everyday. 
They upload their videos from client to server over __________

1. **HTTP**

Not only that, YouTube videos streamed from server to client over  __________
1. ~~DASH~~

### MCQ
### There was another answer for this question
When you bring your laptop to NJIT, applying what we’ve learned in class (not in reality), 
which of the following values is NOT a possible IP address your laptop will obtain from NJIT’s network?
1. 123.45.67.89
2. **192.168.256.2 <-- Valid range is 0-255**
3. 192.168.0.1
4. 172.29.10.9
5. 10.1.0.0

### FILL
Most major e-commerce sites use _______.

1. proxy servers
2. **cookies** <-- I believe this was right, not 100%.
3. extra memory
4. caches
5. load balancers

today to track their customers’ activities at their site.  This is because HTTP itself  _________.

1. does not have RDT
2. ~~Only limits to several operations: (GET PUT, etc)~~ <---- I believe this one was wrong
3. is stateless
4. has limited memory capabilities

One application for this is the ability to maintain a shopping 
cart that contains a list of items that a customer has clicked the 'Purchase' button so that 
he can pay for them at the end of the session.

### FILL
Fill in the blank with 1 word. No space in front or after the comma.

A Content Distribution Networks (CDNs) installs many geographically 
distributed ______ (a.k.a. proxy servers) throughout the region it services, 
thereby localizing much of the traffic.

### OPEN-ENDED
---------------------
45 Terabytes need to be sent from Boston to Los Angeles. FedEx overnight will reach the destination in 
12.5 hours. If a dedicated link can be used to send the data, what should be its transmission rate (Mbps) 
to break even?

Note that Mbps != MBps.
Little b represents bits
Big b represents bytes

Tera: 10^12 bytes
Mega: 10^6 bytes

Conversion from ``TeraByte->MegaByte`` = 45*(10^6)

Conversion from ``MegaByte->MegaBit`` = (45*(10^6))*8 = 360,000,000

Time = 12.5 * 60 * 60 = 45000 seconds

transmission rate = size/time = 360000000/45000 = **8000 Mbps**

---------------------


# DONE

### T/F
When you watch Netflix, you know that the content is being streamed either from an access ISP or 
from a server at a nearby Internet exchange point that has Netflix CDN server rack installed within it. 
This is possible thanks to the fact that Netflix uses DNS to redirect to connect a particular client to a 
CDN server.

**False**

### FILL
1. ~~BGP~~
2. ~~SIP~~
3. **DNS**
4. ~~ICMP~~

protocol provides the ability to translate hostnames to IP addresses. 
Without appropriate entries within it, no one can access a website even if it is of a too-big-too-fail 
company such as facebook.com. 
It is a  ______________-layer protocol

1. ~~physical~~
2. **application**
3. ~~link~~
4. ~~network~~
5. ~~transport~~

and is a great example of the design philosophy that much of the complexity in the 
Internet architecture is located at the  __________ of the network.

1. ~~Core~~
2. **Edge**


### OPEN-ENDED
You notice that Netflix offers its services in other regions of the world. 
You know that your account can be used worldwide but Netflix servers will determine the content you can 
watch based on the IP address it can see from your host. You are determined to watch programs that are not 
yet available in the US. Thus, you think of purchasing the right to access 
a __________ in the region which contains the content you want to watch.

Answer: 
**VPN**

### OPEN-ENDED
Fill in each blank with one word. Separate your answer using commas. No space in front of or after a comma.

TCP _______ limits the amount of unACKed data to TCP ________’s 
free buffer space to ensure the buffer will not overflow. It will have to track two variables, 
they are lastbysent and lastbyteacked

Answer: 
**sender,receiver**
