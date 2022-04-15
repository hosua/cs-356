# CHAPTER 4 - The Network Layer: Data Plane

- **SDN**: Software-defined networking
- **Bus**: A bus is a subsystem that is used to connect computer components and transfer data between them. For example, an internal bus connects computer internals to the motherboard. A “bus topology” or design can also be used in other ways to describe digital connections.

## 4.1 Overview of the Network Layer
### 4.1.1 Forwarding and Routing: The Data and Control Planes

The primary role of the network layer is deceptively simple—to **move packets from sending host to a receiving host**. 
To do so, two important network-layer functions can be identified: 

- Forwarding. When a packet arrives at a router’s input link, the router must movethe packet to the appropriate output link. 
A packet might also be blocked from exit-ing a router(for example, if the packet originated at a known malicious sending
host, or if the packet were destined to a forbidden destination host), or might be duplicated and sent over multiple outgoing links.
	* **Forwarding** refers to the router-local action of transferring a packet from an input link interface to the appropriate output link interface. Forwarding takes place at very short timescales (typically a few nanoseconds), and thus is typically implemented hardware. 

- Routing. The network layer must determine the route or path taken by packets as they flow from a sender to a receiver. 
The algorithms that calculate these paths are referred to as **routing algorithms**. Routing is implemented in the control plane of the network layer.
hardware. 
	* **Routing** refers to the network-wide process that determines the end-to-end paths that packets take from source to destination. Routing takes place on much longer timescales (typically seconds). Implmented in software.

- A key element in every network router is its **forwarding table**.
	* A router forwards a packet by examining the value of one or more fields in the arriving packet’s header, and then using these header values to index into its forwarding table. The value stored in the forwarding table entry for those values indicates the outgoing link interface at that router to which that packet is to be forwarded

### 4.1.2 Network Service Model

The **network service model** defines the characteristics of end-to-end delivery of packets between sending and receiving hosts.
- Let’s now consider some possible services that the network layer could provide.
These services could include:

	* **Guaranteed delivery**. This service guarantees that a packet sent by a source host will eventually arrive at the destination host. 
	* **Guaranteed delivery** with bounded delay. This service not only guarantees delivery of the packet, but delivery within a specified host-to-host delay bound(for example, within 100 msec). 
	* **In-order packet delivery** This service guarantees that packets arrive at the destination in the order that they were sent
	* **Guaranteed minimal bandwidth** This network-layer service emulates the behavior of a transmission link of a specified bit rate (for example, 1 Mbps) between sending and receiving hosts. As long as the sending host transmits bits (as part of packets) at a rate below the specified bit rate, then all packets are eventually delivered tother destination host. 
	* **Security**. The network layer could encrypt all datagrams at the source and decrypt them at the destination, thereby providing confidentiality to all transport-layer segments.

- The Internet’s network layer provides a single service, known as best-effort
service. With best-effort service, packets are neither guaranteed to be received in the
order in which they were sent, nor is their eventual delivery even guaranteed.

### 4.2 What’s Inside a Router?

A router’s input ports, output ports, and switching fabric are almost always **implemented in hardware**.
- Input ports. An input port performs several key functions. It performs the physical layer function of terminating an incoming physical link at a router.
	* An input port also performs link-layer functions needed to interoperate with the link layer at the other side of the incoming link.
	* **A lookup function** is also performed at the input port. It is here that the forwarding table is consulted to determine the router output port to which an arriving packet will be forwarded via the switching fabric.
	* **Control packets** (for example, packets carrying routing protocol information) are forwarded from an input port to the routing processor.
	* The number of ports supported by a router can range from a relatively small number in enterprise routers, to hundreds of 10 Gbps ports in a router at an ISP’s edge, where the number of incoming lines tends to be the greatest.

- Switching fabric. The switching fabric connects the router’s input ports to its output ports. This switching fabric is completely contained within the router.
- **Output ports**. An output port stores packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary link-layer and physical-layer functions. When a link is bidirectional (that is, carries traffic in both directions), an output port will typically be paired with the input port forthat link on the same line card.
- **Routing processor**. The routing processor performs control-plane functions. In traditional routers, it executes the routing protocols, maintains routing tables and attached link state information, and computes the forwarding table for the router. In SDN routers, the routing processor is responsible for communicating with the remote controller in order to (among other activities) receive forwarding table entries computed by the remote controller, and install these entries in the router’s input ports. The routing processor also performs the network management functions.
- Forwarding hardware can be implemented either using a router vendor’s own hardware designs, or constructed using purchased merchant-silicon chips.
- Destination-based forwarding:
	* In destination based forwarding, an input packet arriving consists of the destination address where the packet has to reach. The routers now select the path and forward the packet in the same path that will to the final destination mentioned in the header field.
- Generalized forwarding:
	* Decision of where data packets are forwarded is not based on the destination address.

### 4.2.1 Input Port Processing and Destination-Based Forwarding

- The lookup performed in the input port is central to the router’s operation—it is here that the router uses the for-
warding table to look up the output port to which an arriving packet will be forwarded via the switching fabric.
- The forwarding table is either computed and updated by the routing processor (using a routing protocol to interact with the routing processors in other network routers) or is received from a **remote SDN controller**. The forwarding table is copied from the routing processor to the line cards over a separate bus.
- With such a shadow copy at each line card, forwarding decisions can be made locally, at each input port, without invoking the **centralized routing processor** on a per-packet basis and thus avoiding a **centralized processing bottleneck**.
- Let’s now consider the “simplest” case that the output port to which an incoming
packet is to be switched is based on the packet’s destination address. In the case of
32-bit IP addresses, a brute-force implementation of the forwarding table would have
one entry for every possible destination address. Since there are more than 4 billion
possible addresses, this option is totally out of the question.

### 4.2.2 Switching

The switching fabric is at the very heart of a router, as it is through this fabric that
the packets are actually switched (that is, forwarded) from an input port to an output port.

- **Switching via memory**. The simplest, earliest routers were traditional computers,
with switching between input and output ports being done under direct control of
the CPU (routing processor).

	* Input and output ports functioned as traditional I/O
devices in a traditional operating system. An input port with an arriving packet first signaled the routing processor via an interrupt. 
The packet was then copied from the input port into processor memory. 
	* The routing processor then extracted the destination address from the header, looked up the appropriate output port
in the forwarding table, and copied the packet to the output port’s buffers. In this scenario, if the memory bandwidth is such that a maximum of B packets per second canbe written into, or read from, memory, then the overall forwarding
throughput (the total rate at which packets are transferred from input ports to output ports) must be less than B/2. 
	* Note also that **two packets cannot be forwarded at the same time**, even if they have different destination ports, since only one memory read/write can be done at a time over the shared system bus.

- **Switching via a bus**. In this approach, an input port transfers a packet directly to the output port over a shared bus, without intervention by the routing processor. This is typically done by having the input port pre-pend a switch-internal label (header) to the packet indicating the local output port to which this packet is being transferred and transmitting the packet onto the bus.

	* All output ports receive the packet, but only the port that matches the label will keep the packet. The label is then removed
at the output port, as this label is only used within the switch to cross the bus. If multiple packets arrive to the router at the same time, each at a different input port, all but one must wait since only one packet can cross the bus at a time. Because every packet must cross the single bus, the switching speed of the router is limited to the bus speed. 
	* Nonetheless, switching via a bus is often sufficient for routers that operate in small local area and enterprise networks.
- **Switching via an interconnection network**. One way to overcome the bandwidth limitation of a single, shared bus is to use a more sophisticated interconnection net-
work, such as those that have been used in the past to interconnect processors in a multiprocessor computer architecture.

	* A **crossbar switch** is an interconnection network consisting of 2N buses that connect N input ports to N output ports.
	* **Crossbar switches** are capable of forwarding multiple packets in parallel. A crossbar switch is non-blocking—a packet being forwarded to an output port will not be blocked from reaching that output port as long as no other packet is currently being forwarded to that output port.
	* However, if two packets from two different input ports are destined to that same output port, then one will have to wait at the input,
since only one packet can be sent over any given bus at a time.	

### 4.2.3 Output Port Processing

- **Output port processing**, takes packets that have been stored
in the output port’s memory and transmits them over the output link. This includes
selecting (i.e., scheduling) and de-queueing packets for transmission, and perform-
ing the needed link-layer and physical-layer transmission functions.

### 4.2.4 Where Does Queuing Occur?

- The location and extent of queueing (either at the input port queues or the output port queues) will depend on
the traffic load, the relative speed of the switching fabric, and the line speed.
- Since as these queues grow large, the router’s memory can eventually be exhausted and packet loss will occur when no
memory is available to store arriving packets.
- Assume that all packets have the same fixed length, and that packets arrive to input ports in a synchronous
manner. That is, the time to send a packet on any link is equal to the time to receive a
packet on any link, and during such an interval of time, either zero or one packets can
arrive on an input link.
- Define the switching fabric transfer rate Rswitch as the rate at which packets can be moved from input port to output port. If Rswitch is N times faster
than Rline, then only negligible queuing will occur at the input ports.
- This is because even in the worst case, where all N input lines are receiving packets, and all packets
are to be forwarded to the same output port, each batch of N packets (one packet per input port) can be cleared through the switch fabric before the next batch arrives.

### Input Queuing
- **Head-of-line blocking** (HOL blocking) in computer networking is a performance-limiting phenomenon that occurs when a line of packets is held up in a queue by a first packet.
- **Head-of-the-line (HOL)** blocking in an input-queued switch
	* A queued packet in an input queue must wait for transfer through the fabric (even though its output port is free) because it is blocked by another packet at the
head of the line.

### Output Queuing
- A number of proactive packet-dropping and marking policies (which
collectively have become known as **active queue management (AQM) algorithms**)
have been proposed and analyzed. One of the most widely studied and implemented AQM algorithms is the **Random Early Detection
(RED) algorithm**. More recent AQM policies include **PIE (the Proportional Integral controller Enhance)**, and **CoDel**.
- **Package Scheduler** 
	* Packet scheduling is the means by which data (packet) transmission-governing — a key function of quality of service — is achieved. 
The packet scheduler is the traffic control module that regulates how much data an application (or flow) is allowed, 
essentially enforcing **quality of service** parameters that are set for a particular flow.

### How much buffering is enough?
- Packet queue forms when bursts of packets arrive at a router’s input or (more likely) output port, and the packet arrival rate temporarily
exceeds the rate at which packets can be forwarded. The longer the amount of time that this mismatch persists, the longer the queue will grow, until eventually a port’s
buffers become full and packets are dropped.
- How much buffering should be provisioned at a port:
	* When a large number of independent TCP flows (N) pass through a link, the amount of buffering needed is **B = RTT * C/sqrt(N)** (where B stands for buffering, C stands for link capacity,
and RTT stands for round-trip time).
	* In core networks, where a large number of TCP flows typically pass through large backbone router links, the value of N can be large, with
the decrease in needed buffer size becoming quite significant.
	* Larger buffers also mean potentially longer queueing delays.
	* Increasing the amount of per-hop buffer by a factor of 10 to decrease packet loss could increase the end-end delay by a factor of 10.
	* Increased RTTs also make TCP senders less responsive and slower to respond to incipient congestion and/or packet loss.
	* Buffering can be used to absorb short-term statistical fluctuations in traffic but can also lead to increased delay and the attendant concerns.

- Downsides to large buffers
	* Imagine a home router sending TCP segments to a remote game server. Suppose that it takes 20 ms to transmit a packet (containing a gamer’s TCP segment), that there are negligible queueing
delays elsewhere on the path to the game server, and that the RTT is 200. Suppose that at time t = 0, a burst of 25 packets arrives to
the queue.
	* One of these queued packets is then transmitted once every 20 ms, so that
at t = 200 msec, the first ACK arrives, just as the 21st packet is being transmitted.
This ACK arrival causes the TCP sender to send another packet, which is queued at
the outgoing link of the home router.
	* At t = 220, the next ACK arrives, and another
TCP segment is released by the gamer and is queued, as the 22nd packet is being
transmitted, and so on.
	* In this scenario, ACK clocking results in a new packet arriving at the queue every time a queued packet
is sent, resulting in queue size at the home router’s outgoing link that is always five packets.
	* That is, the end-end-pipe is full (delivering packets to the destination at the
path bottleneck rate of one packet every 20 ms), but the amount of queueing delay is
constant and persistent.
	* This scenario above of long delay due to persistent buffering is known as bufferbloat and illustrates that not only is throughput important, but also minimal delay is important as well.

### 4.2.5 Packet Scheduling

### First-in-First-Out (FIFO)
- Packets arriving at the link output queue wait for transmission if the link is
currently busy transmitting another packet. If there is not sufficient buffering space
to hold the arriving packet, the queue’s packet-discarding policy then determines
whether the packet will be dropped (lost) or whether other packets will be removed
from the queue to make space for the arriving packet.
- The **FIFO (also known as first-come-first-served, or FCFS)** scheduling discipline
selects packets for link transmission in the same order in which they arrived
at the output link queue.

### Priority Queuing
- Under **priority queuing**, packets arriving at the output link are classified into priority classes upon arrival at the queue.
	* In practice, a network operator may configure a queue so that packets carrying network management information (for example, 
	as indicated by the source or destination TCP/UDP port number) receive priority over user traffic.
	* Additionally, real-time voice-over-IP packets might receive priority over non-real-time traffic such e-mail packets.
	* Each priority class typically has its own queue.
	* When choosing a packet to transmit, the priority queuing discipline will transmit a packet from the highest priority class that has a
nonempty queue (that is, has packets waiting for transmission). The choice among packets in the same priority class is typically done in a **FIFO manner**.
	* Under a non-preemptive priority queuing discipline, the transmission of a packet is not interrupted once it has begun.

### Round Robin and Weighted Fair Queuing (WFQ)
- Under the round robin queuing discipline, packets are sorted into classes as with
priority queuing. However, rather than there being a strict service priority among
classes, a round robin scheduler alternates service among the classes. 
	* In the simplest form of round robin scheduling, a class 1 packet is transmitted, followed by a class
2 packet, followed by a class 1 packet, followed by a class 2 packet, and so on. 
	* A so-called **work-conserving queuing** discipline will never allow the link to remain idle whenever there are packets (of any class) queued for transmission. 
	* A work-conserving round robin discipline that looks for a packet of a given class but finds none will immediately check the next class in the round robin sequence.

- A generalized form of round robin queuing that has been widely implemented in routers is the so-called weighted fair queuing (WFQ) discipline.
	* Arriving packets are classified and queued in the appropriate per-class waiting area. As in **round robin scheduling**,
a **WFQ scheduler** will serve classes in a circular manner—first serving class 1, then serving class 2, then serving class 3, and then (assuming there are three classes)
repeating the service pattern.
	* **WFQ (Weighted Fair Queueing)** is also a **work-conserving queuing** discipline and thus will immediately move on to the next class in the service sequence when it finds
an empty class queue.
	* WFQ differs from round robin in that each class may receive a differential amount
of service in any interval of time.
 
## 4.3 The Internet Protocol (IP): IPv4, Addressing, IPv6, and More

### 4.3.1 IPv4 Datagram Format
- Internet’s network-layer packet is referred to as a **datagram**. The key fields in the IPv4 datagram are the following:
	* **Version number**. These 4 bits specify the IP protocol version of the datagram.
By looking at the version number, the router can determine how to interpret the
remainder of the IP datagram. Different versions of IP use different datagram
formats. 
	* **Header length**. Because an IPv4 datagram can contain a variable number of
options (which are included in the IPv4 datagram header), these 4 bits are needed to determine where in the IP datagram the payload 
(for example, the transportlayer segment being encapsulated in this datagram) actually begins. Most IP datagrams do not contain options, so the typical IP datagram has a **20-byte header**
. If the datagram carries a TCP segment, then each datagram carries a total of
40 bytes of header (20 bytes of IP header plus 20 bytes of TCP header) along with
the application-layer message.
	* **Type of service**. The type of service (TOS) bits were included in the IPv4 header
to allow different types of IP datagrams to be distinguished from each other. For
example, it might be useful to distinguish real-time datagrams (such as those
used by an IP telephony application) from non-real-time traffic (e.g., **FTP(File Transfer Protocol)**). The
specific level of service to be provided is a policy issue determined and configured by the network administrator for that router.
	* **Datagram length**. This is the total length of the IP datagram (header plus data), meas-
ured in bytes. Since this field is 16 bits long, the theoretical maximum size of the IP
datagram is **65,535 bytes**. However, datagrams are rarely larger than 1,500 bytes, which
allows an IP datagram to fit in the payload field of a maximally sized Ethernet frame.
	* **Identifier, flags, fragmentation offset**. These three fields have to do with so-called
IP fragmentation, when a large IP datagram is broken into several smaller IP datagrams which are then forwarded independently to the destination, where they are
reassembled before their payload data (see below) is passed up to the transport layer at the destination host. The new version of IP, IPv6, does not allow for fragmentation.
	* **Time-to-live**. The time-to-live (TTL) field is included to ensure that datagrams
do not circulate forever (due to, for example, a long-lived routing loop) in the
network. This field is decremented by one each time the datagram is processed by
a router. If the TTL field reaches 0, a router must drop that datagram.
	* **Protocol**. This field is typically used only when an IP datagram reaches its final
destination. The value of this field indicates the specific **transport-layer protocol**
to which the data portion of this IP datagram should be passed. For example, a
value of 6 indicates that the data portion is passed to **TCP**, while a value of 17 indi-
cates that the data is passed to **UDP** Note that the **protocol number** in the IP datagram has
a role that is analogous(comparable in certain respects, typically in a way which makes clearer the nature of the things compared.) to the role of the port number field in the transport-layer
segment. The protocol number is the glue that binds the network and transport layers together, whereas the port number is the glue that binds the transport and application layers together. 
	* **Header checksum**. The header checksum aids a router in detecting bit errors in a received **IP datagram**. The header checksum is computed by treating each 2 bytes
in the header as a number and summing these numbers using 1s complement arithmetic. The 1s complement of this sum, known as
the **Internet checksum**, is stored in the checksum field. A router computes the header checksum for each received IP datagram and detects an error condition if the checksum carried in the datagram header 
does not equal the computed checksum. Routers typically discard datagrams for which an error has been detected.
Note that the checksum must be recomputed and stored again at each router, since the **TTL(Time-to-live)** field, and possibly the options field as well, will change.
	* **Source and destination IP addresses**. When a source creates a **datagram**, it inserts
its IP address into the source IP address field and inserts the address of the ultimate destination into the destination IP address field. 
Often the source host determines the destination address via a **DNS (Domain Name System) lookup**.
	* **Options**. The options fields allow an **IP header to be extended**. Header options were meant to be used rarely—hence the decision to save overhead by 
not including the information in options fields in every datagram header. Existence of options does complicate matters—since datagram headers can
be of variable length, one cannot determine a priori where the data field will start.
Also, since some **datagrams** may require options processing and others may not,
the amount of time needed to process an IP datagram at a router can vary greatly.
These considerations become particularly important for **IP processing** in high-
performance routers and hosts. For these reasons and others, IP options were not
included in the IPv6 header.
	* **Data (payload)**. In most circumstances, the data field of
the IP datagram contains the **transport-layer segment (TCP or UDP)** to be delivered to the destination. However, the data field can carry other types of data, such
as ICMP (Internet Control Message Protocol) messages.

### 4.3.2 IPv4 Addressing
- A host typically has only a single link into the network; when IP in the host wants to send a datagram, it does
so over this link. The boundary between the host and the physical link is called an **interface**.
- A router’s job is to receive a datagram on one link and forward the datagram on some other link, a router
necessarily has two or more links to which it is connected. The boundary between the
router and any one of its links is also called an **interface**.
- A router thus has **multiple interfaces**, one for each of its links. Because every host and router is capable of send-
ing and receiving **IP datagrams**, IP requires each host and router interface to have its own IP address.
- Thus, an IP address is technically associated with an interface, rather than with the host or router containing that interface.
- Each IP address is **32 bits long (equivalently, 4 bytes)**, and there are thus a total
of **2 32 (or approximately 4 billion)** possible IP addresses. These addresses are typi-
cally written in so-called **dotted-decimal notation**, in which each byte of the address
is written in its decimal form and is separated by a period (dot) from other bytes in
the address.
	* For example, consider the IP address 193.32.216.9. The 193 is the deci-
mal equivalent of the first 8 bits of the address; the 32 is the decimal equivalent of
the second 8 bits of the address, and so on. Thus, the address 193.32.216.9 in binary
notation is: 11000001 00100000 11011000 00001001 

- Each interface on every host and router in the global Internet must have an IP address
that is globally unique (except for interfaces behind NATs).
- A portion of an interface’s IP address will be determined by the **subnet** to which it is connected.
- Example: Network interconnecting three host interfaces and one router
interface forms a **subnet** (IP network).
- IP addressing assigns an address to this subnet:
223.1.1.0/24, where the /24 (“slash-24”) notation, sometimes known as a **subnet
mask**, indicates that the leftmost 24 bits of the 32-bit quantity define the subnet
address.
	* Any additional hosts
attached to the 223.1.1.0/24 subnet would be required to have an address of the form
223.1.1.xxx.

- To determine the subnets, detach each interface from its host or router, creating
islands of **isolated networks**, with interfaces terminating the end points of the
isolated networks. Each of these isolated networks is called a **subnet**.
- The Internet’s address assignment strategy is known as **Classless Interdomain
Routing (CIDR)**
	* **CIDR** generalizes the notion of
subnet addressing. As with subnet addressing, the 32-bit IP address is divided into
two parts and again has the **dotted-decimal form a.b.c.d/x**, where x indicates the
number of bits in the first part of the address.
	* The x most significant bits of an address of the **form a.b.c.d/x** constitute the
network portion of the IP address, and are often referred to as the **prefix (or network
prefix)** of the address.
	* An organization is typically assigned a block of contiguous
addresses, that is, a range of addresses with a common prefix
	* In this case, the IP addresses of devices within the organization
will share the common prefix.
	* Before **CIDR** was adopted, the network portions of an IP address were constrained
to be 8, 16, or 24 bits in length, an addressing scheme known as **classful addressing**, since subnets with 8-, 16-, and 24-bit subnet addresses were known as class A, B, and
C networks, respectively.
	* The ability to use a **single prefix** to
advertise multiple networks is often referred to as **address aggregation** (also route
aggregation or route summarization).

### Obtaining a Block of Addresses
- In order to obtain a **block of IP addresses** for use within an **organization’s subnet**,
a **network administrator** might first contact its ISP, which would provide addresses
from a larger block of addresses that had already been allocated to the ISP.
	* For example, the ISP may itself have been allocated the address block 200.23.16.0/20.
The ISP, in turn, could divide its address block into eight equal-sized contiguous
address blocks and give one of these address blocks out to each of up to eight organi-
zations that are supported by this ISP.

- **IP addresses** are managed under the authority of the
Internet Corporation for Assigned Names and Numbers **(ICANN)**.
	* The role of the nonprofit ICANN organization is not only to **allocate IP addresses**, but also to manage the **DNS root servers**.
	* It also has the very contentious job of **assigning domain names** and resolving domain name disputes.
	* The ICANN allocates addresses to regional **Internet registries** (for example, ARIN, RIPE, APNIC, and LACNIC, which together form the **Address Supporting Organization** of ICANN,
and handle the allocation/management of addresses within their regions.
	* The African Network Information Center (AFRINIC) serves Africa.
    * The American Registry for Internet Numbers (ARIN) serves Antarctica, Canada, parts of the Caribbean, and the United States.
    * The Asia-Pacific Network Information Centre (APNIC) serves East Asia, Oceania, South Asia, and Southeast Asia.
    * The Latin America and Caribbean Network Information Centre (LACNIC) serves most of the Caribbean and all of Latin America.
    * The Réseaux IP Européens Network Coordination Centre (RIPE NCC) serves Europe, Central Asia, Russia, and West Asia.

### Obtaining a Host Address: The Dynamic Host Configuration Protocol
- Once an organization has obtained a **block of addresses**, it can assign individual
IP addresses to the **host and router interfaces** in its organization.
- A system administrator will typically manually configure the IP addresses into the router (often
remotely, with a **network management tool**). 
- Host addresses can also be configured manually, but typically this is done using the **Dynamic Host Configuration
Protocol (DHCP)**.
	* DHCP allows a host to obtain (be allocated) an IP address automatically.
	* A network administrator can configure DHCP so that a
given host receives the same IP address each time it connects to the network, or a
host may be assigned a **temporary IP address** that will be different each time the
host connects to the network.
	* DHCP also allows a host to learn additional information, such as its **subnet mask**, the address
of its **first-hop router** (often called the default gateway), and the address of its local
DNS server.
	* Because of DHCP’s ability to automate the network-related aspects of connecting a host into a network, it is often referred to as a **plug-and-play** or **zeroconf** (zero-configuration) protocol.
	* DHCP is a **client-server protocol**. A client is typically a newly arriving host
wanting to obtain network configuration information, including an IP address for itself.

- For a newly arriving host, the DHCP protocol is a four-step process:
	* **DHCP server discovery**. The first task of a newly arriving host is to find a DHCP
server with which to interact. This is done using a **DHCP discover message**,
which a client sends within a UDP packet to port 67. The UDP packet is encap-
sulated in an **IP datagram**. The DHCP client
creates an IP datagram containing its DHCP discover message along with the
**broadcast destination IP address** of 255.255.255.255 and a “this host” **source IP
address** of 0.0.0.0. The DHCP client passes the IP datagram to the **link layer**,
which then broadcasts this frame to all nodes attached to the subnet.
	* **DHCP server offer(s)**. A DHCP server receiving a DHCP discover message
responds to the client with a **DHCP offer message** that is broadcast to all nodes on the subnet, again using the IP broadcast address of 255.255.255.255.
Each server offer message contains the **transaction ID** of the received
discover message, the proposed IP address for the client, the **network mask**,
and an IP address lease time—the amount of time for which the IP address
will be valid. It is common for the server to set the lease time to **several hours
or days**.
	* **DHCP request**. The newly arriving client will choose from among one or more
server offers and respond to its selected offer with a **DHCP request message**,
echoing back the configuration parameters.
	* **DHCP ACK**. The server responds to the DHCP request message with a **DHCP
ACK message**, confirming the requested parameters.

- Once the client receives the **DHCP ACK**, the interaction is complete and the
client can use the **DHCP-allocated IP address** for the lease duration.
- Since a client
may want to use its address beyond the lease’s expiration, DHCP also provides a
mechanism that allows a client to renew its lease on an IP address.

### 4.3.3 Network Address Translation (NAT)
- Network Address Translation (NAT) is a process that enables one, **unique IP address** to represent an entire group of computers. 
In **network address translation**, a network device, often a router or NAT firewall, assigns a computer or computers inside a **private network a public address**.
- The NAT-enabled router does not look like a router to the outside world. Instead
the NAT router behaves to the outside world as a **single device** with a **single IP
address**.
- The NAT-enabled router is hiding
the details of the home network from the outside world.
- The router gets its address from the ISP’s **DHCP server**, and the router runs a DHCP server to provide
addresses to computers within the **NAT-DHCP-router-controlled** home network’s
address space.
- How do all hosts on a local network share the same public IP address? 
	* **Network Address Translation (NAT)** re-assigns IP addresses and port numbers and keeps track of these re-assignments using its **NAT translation table.**
	* When the router receives a packet from a **local host** containing a public IP address, it changes the source IP address to use its Internet IP address and 
changes the **source port number** so it knows which local host process to deliver received packets to. This re-assignment is entered into the translation table.

- **Network address translation (NAT)** traversal is a computer networking technique of establishing and maintaining Internet protocol connections across gateways that implement 
network address translation (NAT).

### 4.3.4 IPv6

### IPv6 Datagram Format
- The most important changes introduced in **IPv6** are evident in the datagram format:
	* **Expanded addressing capabilities**. IPv6 increases the size of the IP address from
**32 to 128 bits**. IPv6 has introduced a new type of address, called an **anycast
address**, that allows a datagram to be delivered to any one of a group of hosts.
	* **A streamlined 40-byte header**. The resulting **40-byte fixed-length** header allows
for faster processing of the IP datagram by a router. A new encoding of options
allows for more flexible options processing.
	* **Flow labeling**. IPv6 has an elusive definition of a **flow**. This
allows labeling of packets belonging to particular flows for which the sender requests special handling, such as a non-default quality of service or real-time
service Audio and video transmission might likely be treated as
a flow. More traditional applications, such as file transfer
and e-mail, might not be treated as flows.
	
- The following fields are defined in **IPv6**:
	* **Version**. This 4-bit field identifies the **IP version number**. IPv6
carries a **value of 6** in this field. Note that putting a 4 in this field does not create
a valid IPv4 datagram.
	* **Traffic class**. The **8-bit traffic class field** can be used
to give priority to certain datagrams within a **flow**, or it can be used to give priority to datagrams from certain applications (for example, voice-over-IP) over
datagrams from other applications (for example, SMTP e-mail).
	* **Flow label**. This **20-bit field** is used to identify a flow of datagrams.
	* **Payload length**. This **16-bit value** is treated as an unsigned integer giving the
number of bytes in the IPv6 datagram following the fixed-length, **40-byte datagram header**.
	* **Next header**. This field identifies the protocol to which the contents (data field) of
this datagram will be delivered (for example, to TCP or UDP). The field uses the
same values as the protocol field in the IPv4 header. 
	* **Hop limit**. The contents of this field are **decremented** by one by each router that
forwards the datagram. If the hop limit count reaches zero, a router must discard
that datagram. 
	* **Source and destination addresses**. The various formats of the **IPv6 128-bit address**. 
	* **Data**. This is the payload portion of the IPv6 datagram. When the datagram
reaches its destination, the payload will be removed from the IP datagram and
passed on to the protocol specified in the next header field.

- Several fields appearing in the **IPv4 datagram** are no longer present in the **IPv6 datagram**:
	* **Fragmentation/reassembly**. IPv6 does not allow for fragmentation and reassembly at intermediate routers; these operations can be performed only by the source and destination.
**Fragmentation and reassembly** is a time-consuming operation; removing this functionality from
the routers and placing it squarely in the end systems considerably speeds up IP
forwarding within the network.
	* **Header checksum**. As with fragmentation and reassembly, this too was a costly operation in IPv4, and thus removed in IPv6.
	* **Options**. An options field is no longer a part of the standard IP header but, it has not gone away. Instead, the options field is one of the possible next
headers pointed to from within the IPv6 header. That is, just as TCP or UDP protocol headers can be the next header within an IP packet, so too can an
options field. The removal of the options field results in a **fixed-length, 40-byte IP header**.


