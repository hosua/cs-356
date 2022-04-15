# Jargon
* Acknowledgment (ACK): Packets that are used to confirm that the data packets have been received, also used to confirm the initiation request and tear down requests
* Active Optical Networks (AONs)
* Automatic Repeat reQuest (ARQ)
* Available Bite Rate (ABR)
* Berkeley Internet Name Domain (BIND)
* CWR - Congestion Window Reduced - "OK, I saw your ECE, you can turn it off now"
* Cable Modem Termination System (CMTS)
* Central Office (CO)
* Content Distribution Networks (CDNs)
* Data Over Cable Service Interface Specifications (DOCSIS)
* Demultiplexing - The job of deliverying the data in a transport-layer segment to the correct socket
* Digital Subscriber Line (DSL)
* Digital Subscriber Line Access Multiplexer (DSLAM)
* Distributed Hash Table (DHT)
* Domain Name System (DNS)
* Dynamic Adaptive Streaming over HTTP (DASH)
* Dynamic Host Configuration Protocol (DHCP)
* ECE - Echo of Congestion Encountered - starts being set in TCP packets when "CE" is seen
* Exponential Weighted Moving Average (EWMA)
* FIN (finish): Indicate that the connection is being torn down. Both the sender and receiver send the FIN packets to gracefully terminate the connection
* Fiber To The Home (FTTH)
* Finite State Machine (FSM)
* Frequency-Division Multiplexing (FDM)
* Go-Back-N (GBN) - Chapter 3.4.333
* Head Of Line (HOL)
* Hybrid Fiber Coax (HFC)
* Internet Corporation for Assigned Names and Numbers (ICANN)
* Internet Exchange Point (IXP) - A Meeting Point Where Multiple ISPs Can Peer Together
* Internet Mail Access Protocol (IMAP)
* Low-Earth Orbiting (LEO) - In The Context Of Satellites
* Maximum Segment Size (MSS) - Section 3.5
* Maximum Transmission Size (MTU) - Section 3.5
* Multiplexing - The job of gathering data chunks at source host from different sockets, encapsulating each data chunk with header information (to be used in demultiplexing later) to create segments, and also, passing those segments to the network layer
* Negative Acknowledgement (NAK)
* Optical Carrier (OC) 
* Optical Network Terminator (ONT)
* PSH (push): Indicate that the incoming data should be passed on directly to the application instead of getting buffered
* Passive Optical Networks (PONs)
* Points Of Presence (PoPs)
* Positive Acknowledgement (ACK)
* Protocol Pipelining - a technique in which multiple requests are written out to a single socket without waiting for the corresponding responses
* RST (reset): Signify the connection is down or maybe the service is not accepting the requests
* Reliable Data Transfer (RDT)
* Requests For Comments (RFCs)
* Resource Records (RRs)
* Round-Trip Time (RTT) - Is The Time It Takes For A Small Packet To Travel From Client To Server And Then Back To The Client
* SYN (synchronize): Packets that are used to initiate a connection.
* Selective Repeat (SR) - Chapter 3.4.4
* TCP Reset (RST) - used by a TCP sender to indicate that it will neither accept nor receive more data.
* The maximum amount of data that can be grabbed and placed in a segment is limited by the 
* Throughput - The Maximum Rate At Which A Router Can Forward Packets.
* Time To Live (TTL) - The amount of time that a packet "lives" before it is discarded
* Time-Division Multiplexing (TDM)
* Top-level domain (TLD) servers
* Transmission Control Protocol (TCP)
* Transport Layer Security (TLS)
* URG (urgent): Indicate that the data that the packet is carrying should be processed immediately by the TCP stack
* User Datagram Protocol (UDP)
* Voice-Over-IP (VoIP) 



# CHAPTER 1 - COMPUTER NETWORKS AND THE INTERNET

## 1.1 What Is the Internet?

### 1.1.1 A Nuts-and-Bolts Description

- End systems are connected together by a network of **communication links** and **packet switches**.
- Different links can transmit data at different rates, with the **transmission rate** of a link measured in bits/second.
- When one end system has data to send to another end system, the sending end system segments the data and adds header bytes to each segment (a.k.a **packets**).
- **Packet switches** come in many shapes and flavors, but the two most prominent types in today's Internet are **routers** and **link-layer switches**.
- The sending end system to the receiving end system is known as a **route** or **path** through the network.
- End systems access the Internet through **Internet Service Providers (ISPs)**, including residential ISPs such as local cable, telephone companies, etc.
- The **Transmission Control Protocol (TCP)** and the **Internet Protocol (IP)** are two of the most important protocols in the Internet.
- The Internet's principal protocols are collectively known as **TCP/IP**.

- **Internet standards** are developed by the Internet Engineering Task Force (IETF) [IETF 2020]. 
- The IETF standards documents are called **requests for comments (RFCs)**.

- **RFCs**
	* RFCs tend to be quite technical and detailed.
	* They define protocols such as **TCP**, **IP**, **HTTP** (for the Web), and **SMTP** (for e-mail).
	* There are currently nearly 9000 RFCs.

### 1.1.2 A Services Description

- Internet applications include mobile smartphone and tablet applications, including Internet messaging, mapping with real-time road-traffic information, music streaming movie and television streaming, online social media, video conferencing, multi-person games, and location-based recommendation systems. The applications are said to be **distributed applications**, since they involve multiple end systems that exchange data with each other.

**Q:** How does one program running on one end system instruct the Internet to deliver data to another program running on another end system?

**A:** End systems attached to the Internet provide a **socket interface** that specifies how a program running on one end system asks the Internet infrastructure to deliver data to a specific destination program running on another end system.

**Q:** What are packet switching and TCP/IP? 

**A:** Packet switching is: a mode of data transmission in which a message is broken into a number of parts which are sent independently, over whatever route is optimum for each packet, and reassembled at the destination. TCP/IP is a protocol that uses packet switching.

**Q:** What are routers? 

**A:** A router is a device that connects two or more packet-switched networks or subnetworks. 

**Q:** What kinds of communication links are present in the Internet? 

**A:** Links are made up of different types of physical media: **coaxial cable**, **copper wire**, **fiber optics**, and **radio spectrum**. Different links can transmit data at different rates.  The link **transmission rate** is often called the **link bandwidth**, and is typically measured in bits/second.

**Q:** What is a distributed application?

**A:** A **distributed application** consists of one or more local or remote clients that communicate with one or more servers on several machines linked through a network.

### 1.1.3 What is a Protocol?

**Q:** What is a protocol? 

**A:** A **protocol** is an established set of rules that determine how data is transmitted between different devices in the same network.

**Q:** What does a protocol do?

**A:** A **protocol** defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event.

## 1.2 The Network Edge

- The computers and other devices connected to the Internet are often referred to as end systems. 
- They are referred to as end systems because they sit at the edge of the Internet
- The Internet's end systems include desktop computers (e.g., desktop PCs, Macs, and Linux boxes), servers (e.g., Web and e-mail servers), and mobile devices (e.g., laptops, smartphones, and tablets).
- End systems are also referred to as hosts because they host (that is, run) application programs such as a Web browser program, a Web server program, an e-mail client program, or an e-mail server program.
- Hosts are sometimes further divided into two categories: **clients** and **servers**.
- Today, most of the servers from which we receive search results, e-mail, Web pages, videos and mobile app content reside in large **data centers**.

- Data centers serve three purposes
	* They serve Amazon e-commerce pages to users. For example, pages describing products and purchase information.
	* They serve as massively parallel computing infrastructures for Amazon-specific data processing tasks.
	* They provide **cloud computing** to other companies. Indeed, today a major trend in computing is for companies to use a cloud provider such as Amazon to handle essentially all of their IT needs.

### 1.2.1 Access Networks


- Today, the two most prevalent types of broadband residential access are **digital subscriber line (DSL)** and cable.
- Thus, when DSL is used, a customer's telco is also its ISP.
- While DSL makes use of the telco's existing local telephone infrastructure, **cable Internet access** makes use of the cable television company's existing cable television infrastructure.
- Although DSL and cable networks currently represent the majority of residential broadband access in the United States, an up-and-coming technology that provides even higher speeds is **fiber to the home (FTTH)** [Fiber Broadband 2020].
- FTTH can potentially provide Internet access rates in the gigabits per second range.
- The simplest optical distribution network is called direct fiber, with one fiber leaving the CO for each home. More commonly, each fiber leaving the central office is actually shared by many homes; it is not until the fiber gets relatively close to the homes that it is split into individual customer-specific fibers.
- There are two competing optical-distribution network architectures that perform this splitting:
	* active optical networks (AONs)
	* passive optical networks (PONs) - Used by Verizon FiOS

- On corporate and university campuses, and increasingly in home settings, a **local area network (LAN)** is used to connect an end system to the edge router.
- Ethernet is by far the most prevalent access technology in corporate, university, and home networks.
- Ethernet users use **twisted-pair** copper wire to connect to an Ethernet switch,

### 1.2.2 Physical Media

- HFC uses a combination of fiber cable and coaxial cable
- DSL and Ethernet use copper wire
- Mobile access networks use the radio spectrum
- When bits travel from their source to their destination, they pass through a series of transmitter-receiver pairs. For each transmitter-receiver pair,
the bit is sent by propagating electromagnetic waves or optical pulses across a **physical medium**.

- Examples of physical media
	* twisted-pair copper wire 
	* coaxial cable 
	* multimode fiber-optic cable
	* terrestrial radio spectrum
	* satellite radio spectrum

- Physical media fall into two categories: **guided media** and **unguided media**.
- many builders install twisted pair, optical fiber, and coaxial cable in every room in a building

#### Twisted-Pair Copper Wire
* The least expensive and most commonly used guided transmission medium
* More than 99 percent of the wired connections from the telephone handset to the local telephone switch use twisted-pair copper wire
* Twisted pair consists of two insulated copper wires, each about 1 mm thick, arranged in a regular spiral pattern
* The wires are twisted together to reduce the electrical interference from similar pairs close by
* A wire pair constitutes a single communication link
* **Unshielded twisted pair (UTP)** is commonly used for computer networks within a building, that is, for LANs
* Modern twisted-pair technology, such as category 6a cable, can achieve data rates of 10 Gbps for distances up to a hundred meters
* DSL (digital subscriber line) technology has enabled residential users to access the Internet at tens of Mbps over twisted pair
(when users live close to the ISP's central office)

#### Coaxial Cable
* Like twisted pair, coaxial cable consists of two copper conductors, but the two conductors are concentric rather than parallel
* With this construction and special insulation and shielding, coaxial cable can achieve high data transmission rates
* Cable television systems have recently been coupled with cable modems to provide residential users with Internet access at rates of hundreds of Mbps
* Coaxial cable can be used as a **guided shared medium**
* Specifically, a number of end systems can be connected directly to the cable, with each of the end systems receiving whatever is sent by the other end systems.

#### Fiber Optics
* An optical fiber is a thin, flexible medium that conducts pulses of light, with each pulse representing a bit
* A single optical fiber can support tremendous bit rates, up to tens or even hundreds of gigabits per second
* They are immune to electromagnetic interference, have very low signal attenuation up to 100 kilometers, and are very hard to tap
* fiber optics are the preferred long-haul guided transmission media, particularly for overseas links
* The Optical Carrier (OC) standard link speeds range from 51.8 Mbps to 39.8 Gbps

#### Terrestrial Radio Channels
* Radio channels carry signals in the electromagnetic spectrum
* Are an attractive medium because they require no physical wire to be installed, can penetrate walls, provide connectivity to a mobile user, and can potentially carry a signal
for long distances
* trial radio channels can be broadly classified into three groups: those that operate over very short distance (e.g., with one or two meters); those that operate in
local areas, typically spanning from ten to a few hundred meters; and those that operate in the wide area, spanning tens of kilometers

#### Satellite Radio Channels
* A communication satellite links two or more Earth-based microwave transmitter/receivers, known as ground stations
* The satellite receives transmissions on one frequency band, regenerates the signal using a repeater
* Two types of satellites are used in communications: **geostationary satellites** and **low-earth orbiting (LEO)** satellites
* Satellite links, which can operate at speeds of hundreds of Mbps, are often used in areas without access to DSL or cable-based Internet access
* There are currently many low-altitude communication systems in development. LEO satellite technology may be used for Internet access sometime in the future

## 1.3 The Network Core

- Having examined the Internet's edge, let us now delve more deeply inside the network core--the mesh of packet switches and links that interconnects the Internet's **end systems**

### 1.3.1 Packet Switching


- In a network application, end systems exchange **messages** with each other
- To send a message from a source end system to a destination endsystem, the source breaks long messages into smaller chunks of data known as **packets**
- Between source and destination, each packet travels through communication links and packet switches (for which there are two predominant types, **routers** and **link-layer switches**)
- Packets are transmitted over each communication link at a rate equal to the full transmission rate of the link. So, if a source end system or a packet switch is sending a packet of **L** bits over a link with transmission rate **R** bits/sec, then the time to transmit the packet is **L / R** seconds

#### Store-and-Forward Transmission
* Most packet switches use **store-and-forward** transmission at the inputs to the links
* Store-and-forward transmission means that the packet switch must receive the entire packet before it can begin to transmit the first bit of the packet onto the outbound link
* At time `L/R` seconds, since the router has just received the entire packet, it can begin to transmit the packet onto the outbound link towards the destination
* At time `2L/R`, the router has transmitted the entire packet, and the entire packet has been received by the destination. Thus, the total delay is `2L/R`.
* If the switch instead forwarded bits as soon as they arrive (without first receiving the entire packet), then the total delay would be `L/R` since bits are not held up at the router.

#### Calculate the amount of time that elapses from when the source begins to send the first packet until the destination has received all three packets:
* At time `L/R`, the router begins to forward the first packet
* Simultaneously at time `L/R`, the source will begin to send the second packet since it has just finished sending the entire first packet
* Thus, at time `2L/R`, the destination has received the first packet and the router has received the second packet 
* Similarly, at time `3L/R`, the destination has received the first two packets and the router has received the third packet
* Finally, at time `4L/R` the destination has received all three packets.

#### General Formula:
* `L` = number of bits being sent
* `R` = transmission rate (bits/second)
* `N` = number of links available
* dend-to-end (end-to-end delay) = `N(L/R)`

#### Queuing Delays and Packet Loss
* Each packet switch has multiple links attached to it
* For each attached link, the packet switch has an **output buffer** (also called an **output queue**)
* If an arriving packet needs to be transmitted onto a link but finds the link busy with the transmission of another packet, the arriving packet must wait in the output buffer
* Thus, in addition to the store-and-forward delays, packets suffer output buffer **queuing delays**
* Since the amount of buffer space is finite, an arriving packet may find that the buffer is completely full with other packets waiting for transmission
* In this case, **packet loss** will occur--either the arriving packet or one of the already-queued packets will be dropped

#### Forwarding Tables and Routing Protocols
* A router takes a packet arriving on one of its attached communication links and forwards that packet onto another one of its attached communication links
* How does the router determine which link it should forward the packet onto? Packet forwarding is actually done in different ways in different types of computer networks.
* In the Internet, every end system has an address called an IP address.
* When a packet arrives at a router in the network, the router examines a portion of the packet's destination address and forwards the packet to an adjacent router
* Each router has a **forwarding table** that maps destination addresses (or portions of the destination addresses) to that router's outbound links
* When a packet arrives at a router, the router examines the address and searches its **forwarding table**, using this destination address, to find the appropriate outbound link
* The router then directs the packet to this outbound link

**Q:** How do forwarding tables get set? Are they configured by hand in each and every router, or does the Internet use a more automated procedure?

**A:** the Internet has a number of special routing protocols that are used to automatically set the **forwarding tables**

### 1.3.2 Circuit Switching 
- There are two fundamental approaches to moving data through a network of links and switches: **circuit switching** and **packet switching**
- In **circuit-switched networks**, the resources needed along a path (buffers, link transmission rate) to provide for communication between the end systems are reserved for the duration of the communication session between the end systems
- In **packet-switched networks**, these resources are **not** reserved; a session's messages use the resources on demand and, as a consequence, may have to wait (that is, queue) for access to a communication link
- A **circuit** is the connection between the sender and the receiver
- When two hosts want to communicate, the network establishes a dedicated **end-to-end** connection between the two hosts.
- Thus, in order for Host A to communicate with Host B, the network must first reserve one circuit on each of two links.
- if each link between adjacent switches has a transmission rate of 1 Mbps and there are 4 links/switches, then each end-to-end circuit-switch connection gets 250 kbps
	* `1 Mbps = 10^6 	1 Kbps = 10^3     (1*10^6)/4 = 250*10^3`

#### Multiplexing in Circuit-Switched Networks
* A circuit in a link is implemented with either **frequency-division multiplexing (FDM)** or **time-division multiplexing (TDM)**
* With **FDM**, the frequency spectrum of a link is divided up among the connections established across the link
* Specifically, the link dedicates a frequency band to each connection for the duration of the connection
* This is where the term **bandwith** is derived from width
* For a TDM link, time is divided into frames of fixed duration, and each frame is divided into a fixed number of time slots.
* Proponents of packet switching have always argued that circuit switching is wasteful because the dedicated circuits are idle during **silent periods**

**Q:** Suppose that all links in the network use TDM with **24 slots** and have a **bit-rate of 1.536 Mbps**. Also suppose that it takes **500 ms** to establish an end-to-end
circuit before Host A can begin to transmit the file of size **640kb**. How long does it take to send the file?

**A:** each link speed = `(1.536Mbps)/24 = 64000 = 64Kbps, 640kbps/64kb = 10 seconds`

### 1.3.3 A Network of Networks
- the access ISP is said to be a **customer** and the global transit ISP is said to be a **provider**

#### Tier-1 ISP: 
* These ISPs are at the top of the hierarchy and they have a global reach they do not pay for any internet traffic through their network instead lower-tier ISPs have to pay a cost for passing their traffic from one geolocation to another which is not under the reach of that ISPs. 
* Generally, ISPs at the same level connect to each other and allow free traffic passes to each other. Such ISPs are called peers. Due to this cost is saved. 
* They build infrastructure, such as the Atlantic Internet sea cables, to provide traffic to all other Internet service providers, not to end users.  
* Examples: Cogent Communications, Hibernia Networks, AT&T
#### Tier-2 ISP:
* These ISPs are service provider who connect between tier 1 and tier 3 ISPs. 
* They have regional or country reach and they behave just like Tier-1 ISP for Tier-3 ISPs. 
* Examples: Vodafone, Easynet, BT
#### Tier-3 ISP:
* These ISPs are closest to the end users and helps them to connect to the internet by charging some money. 
* These ISPs work on purchasing model. 
* These ISPs have to pay some cost to Tier-2 ISPs based on traffic generated. 
* Examples: Comcast, Deutsche Telekom, Verizon Communications 

- **Internet Exchange Point (IXP)**, is a meeting point where multiple ISPs can peer together

- Google is currently one of the leading examples of a **content-provider network**
- Google has 19 major data centers distributed across North America, Europe, Asia, South America, and Australia with each data center having tens or hundreds of thousands of servers
- Google sucks
- Google has smaller data centers, each with a few hundred servers; these smaller data centers are often located within IXPs
- The Google data centers are all interconnected via Google's private **TCP/IP** network

## 1.4 Delay, Loss, and Throughput in Packet-Switched Networks

### 1.4.1 Overview of Delay in Packet-Switched Networks
- A packet starts in a host (the source), passes through a series of routers, and ends its journey in another host (the destination)
- The performance of many Internet applications--such as search, Web-browsing, e-mail, maps, instant messaging, and voice-over-IP--are greatly affected by network delays 
- As a packet travels from one node (host or router) to the subsequent node (host or router) along this path, the packet suffers from several types of delays at each node along the path
- The most important of these delays are the **nodal processing delay**, **queuing delay**, **transmission delay**, and **propagation delay**; together, these delays accumulate to give a **total nodal delay**

#### Processing Delay
* The time required to examine the packet's header and determine where to direct the packet is part of the **processing delay**
* The processing delay can also include other factors, such as the time needed to check for bit-level errors in the packet that occurred in transmitting the packet's bits from the upstream node to router A
* Processing delays in high-speed routers are typically on the order of microseconds or less

#### Queuing Delay 
* At the queue, the packet experiences a **queuing delay** as it waits to be transmitted onto the link
* The length of the queuing delay of a specific packet will depend on the number of earlier-arriving packets that are queued and waiting for transmission onto the link
* If the queue is empty and no other packet is currently being transmitted, then our packet's queuing delay will be zero
* If the traffic is heavy and many other packets are also waiting to be transmitted, the queuing delay will be long
* Queuing delays can be on the order of microseconds to milliseconds in practice

#### Transmission Delay
* Assuming that packets are transmitted in a first-come-first-served manner, as is common in packet-switched networks, our packet can be transmitted only after all the packets that have arrived before it have been transmitted
* Denote the length of the packet by `L` bits
* Denote the transmission rate of the link from router A to router B by `R` bits/sec
* For example, for a `10 Mbps` Ethernet link, the rate is `R = 10 Mbps`; for a `100 Mbps` Ethernet link, the rate is `R = 100 Mbps`
* The transmission delay is `L/R`. This is the amount of time required to push (that is, transmit) all of the packet's bits into the link

#### Propagation Delay
* The time required to propagate from the beginning of the link to router B is the **propagation delay**
* The propagation speed depends on the physical medium of the link (that is, fiber optics, twisted-pair copper wire, and so on) and is in the range of `2*10^8 meters/sec` to `3*10^8 meters/sec`
* This is equal to, or a little less than, the speed of light
* The **propagation delay** is the **d**istance between two routers divided by the propagation **s**peed, so the propagation delay is **d/s**
* Once the last bit of the packet propagates to node B, it and all the preceding bits of the packet are stored in router B
* In wide-area networks, propagation delays are on the order of milliseconds.

#### Comparing Tranmission and Propagation Delay
* The transmission delay is the amount of time required for the router to push out the packet; it is a function of the packet's length and the transmission rate of the link, but has nothing to do with the distance between the two routers
* The propagation delay, on the other hand, is the time it takes a bit to propagate from one router to the next; it is a function of the distance between the two routers, but has nothing to do with the packet's length or the transmission rate of the link
* Let **dproc**, **dqueue**, **dtrans**, and **dprop** denote the processing, queuing, transmission, and propagation delays
* then the total nodal delay is given by **dnodal** = **dproc** + **dqueue** + **dtrans** + **dprop**
* The contribution of these delay components can vary significantly. 
* For example, **dprop** can be negligible (for example, a couple of microseconds) for a link connecting two routers on the same university campus
* however, **dprop** is hundreds of milliseconds for two routers interconnected by a geostationary satellite link, and can be the dominant term in dnodal
* Similarly, **dtrans** can range from negligible to significant. Its contribution is typically negligible for transmission rates of 10 Mbps and higher (for example, for LANs)
* however, it can be hundreds of milliseconds for large Internet packets sent over low-speed dial-up modem links
* The processing delay, **dproc**, is often negligible; however, it strongly influences a router's maximum **throughput** which is the maximum rate at which a router can forward packets.

### 1.4.2 Queuing Delay and Packet Loss
- The most complicated and interesting component of nodal delay is the queuing delay, **dqueue**
- queuing delay is so important and interesting in computer networking that thousands of papers and numerous books have been written about it
- Unlike the other three delays (**dproc**, **dtrans**, and **dprop**), the queuing delay can vary from packet to packet
- For example, if 10 packets arrive at an empty queue simultaneously, the first packet transmitted will suffer no queuing delay, while the last packet will have to wait until the first 9 are done.
- when characterizing queuing delay, one typically uses statistical measures such as average queuing delay, variance of queuing delay, and the probability that the queuing delay exceeds some specified value.

**Q.** When is the queuing delay large and when is it insignificant?

**A.** This question depends on the rate at which traffic arrives at the queue, the transmission rate of the link, and the nature of the arriving traffic.

- `R` is the transmission rate (in bits/sec) at which bits are pushed out of the queue
- Also suppose, for simplicity, that all packets consist of `L` bits
- Then the average rate at which bits arrive at the queue is `La` bits/sec
- The ratio `La/R`, called the `traffic intensity`
- If `La/R > 1`, then the average rate at which bits arrive at the queue exceeds the rate at which the bits can be transmitted from the queue
- Therefore, one of the golden rules in traffic engineering is: Design your system so that the traffic intensity is no greater than 1
- Now consider the case `La/R <= 1` Here, the nature of the arriving traffic impacts the queuing delay.
- For example, if packets arrive periodically--that is, one packet arrives every `L/R` seconds--then every packet will arrive at an empty queue and there will be no queuing delay
- On the other hand, if packets arrive in bursts but periodically, there can be a significant average queuing delay
- For example, suppose **N** packets arrive simultaneously every `(L/R)N` seconds
- The first packet transmitted has no queuing delay; the second packet transmitted has a queuing delay of L/R seconds; the nth packet transmitted has a queuing delay of `(n - 1)L/R` secs
- If the traffic intensity is close to zero, then packet arrivals are few and far between and it is unlikely that an arriving packet will find another packet in the queue. Hence, the average queuing delay will be close to zero
- When the traffic intensity is close to 1, there will be intervals of time when the arrival rate exceeds the transmission capacity (due to variations in packet arrival rate), and a queue will form during these periods of time
- When the arrival rate is less than the transmission capacity, the length of the queue will shrink.


#### Packet Loss
* A queue preceding a link has finite capacity, although the queuing capacity greatly depends on the router design and cost
* Because the queue capacity is finite, packet delays do not really approach infinity as the traffic intensity approaches 1
* Instead, a packet can arrive to find a full queue. With no place to store such a packet.
* A router will **drop** this packet, resulting in **packet loss**

### 1.4.3 End-to-End Delay
* Suppose there are N - 1 routers between the source host and destination host. 
* Suppose that the network is uncongested (so that queuing delays are negligible), the processing delay at each router and at the source host is **dproc**
* Suppose the transmission rate out of each router and out of the source host is **R** bits/sec
* And suppose the propagation on each link is **dprop**
* `dend - end = N (dproc + dtrans + dprop)`
* The nodal delays accumulate and give an **end-to-end** delay where, once again, `dtrans = L/R`, where `L` is the packet size

#### Traceroute 
* Traceroute is a simple program that can run in any Internet host. 
* When the user specifies a destination hostname, the program in the source host sends multiple, special packets toward that destination
* As these packets work their way toward the destination, they pass through a series of routers. 
* When a router receives one of these special packets, it sends back to the source a short message that contains the name and address of the router.
* The output has six columns: the first column is the n value described above, that is, the number of the router along the route
* the second column is the name of the router 
* the third column is the address of the router (of the form xxx.xxx.xxx.xxx) 
* the last three columns are the round-trip delays for three experiments

#### End System, Application, and Other Delays
* In addition to processing, transmission, and propagation delays, there can be additional significant delays in the end systems
* For example, an end system wanting to transmit a packet into a shared medium (e.g., as in a WiFi or cable modem scenario) may purposefully delay its transmission as part of its protocol for sharing the medium with other end systems
* Another important delay is media packetization delay, which is present in Voice-over-IP (VoIP) applications

### 1.4.4 Throughput in Computer Networks
- In addition to delay and packet loss, another critical performance measure in computer networks is end-to-end throughput
- To define throughput, consider transferring a large file from Host A to Host B across a computer network
- This transfer might be, for example, a large video clip from one computer to another
- The **instantaneous throuput** at any instant of time is the rate (in bits/sec) at which Host B is receiving the file
- If the file consists of **F** bits and the transfer takes **T** seconds for Host B to receive all **F** bits, then the average throughput of the file transfer is **F/T** bits/sec
- 
- Consider the throughput for a file transfer from the server to the client
- Let `Rs` denote the rate of the link between the server and the router
- Let `Rc` denote the rate of the link between the router and the client
- Suppose that the only bits being sent in the entire network are those from the server to the client
- What is the server-to-client throughput?
- The server cannot pump bits through its link at a rate faster than `Rs` bps
- The router cannot forward bits at a rate faster than Rc bps.
- If `Rs < Rc`, then the bits pumped by the server will “flow" right through the router and arrive at the client at a rate of `Rs` bps, giving a throughput of `Rs` bps
- If `Rs > Rc`, then the router will not be able to forward bits as quickly as it receives them
- In this case, bits will only leave the router at rate `Rc`, giving an end-to-end throughput of `Rc`
- To summarize, the throughput is always the minimum of `{ Rc, Rs }`, a.k.a. transmission rate of the `bottleneck link`

- Example:
	* Suppose that you are downloading an MP3 file of `F = 32 million bits`, the server has a transmission rate of `Rs = 2 Mbps`, and you have an access link of `Rc = 1 Mbps`
	* `min{ Rs, Rc } = 1 Mbps`, therefore the time to download will be `(32*10^6)/(1*10^6) = 32 seconds`
	* If there are `N` links, the throughput will still be `min{ R1, R2, R3... RN }`. This is always the case.

- The constraining factor for throughput in today's Internet is typically the access network.

- But what if the rate of the common link is of the same order as Rs and Rc?
	* Suppose `Rs = 2 Mbps`, `Rc = 1 Mbps`, `R = 5 Mbps`, and the common link divides its transmission rate equally among the 10 downloads
	* Now the bottleneck for each download is no longer in the access network, but is now instead the shared link in the core, which only provides each download with `500 kbps of throughput`

## 1.5 Protocol Layers and Their Service Models

### 1.5.1 Layered Architecture
- A **layered architecture** allows us to discuss a well-defined, specific part of a large and complex system
- For large and complex systems that are constantly being updated, the ability to change the implementation of a service without affecting other components of the system is another important advantage of layering.

#### Protocol Layering
* To provide structure to the design of network protocols, network designers organize protocols--and the network hardware and software that implement the protocols in **layers**
* Each protocol belongs to one of the layers
* We are again interested in the **services** that a layer offers to the layer above--the so-called **service model** of a layer.
* Each layer provides its service by (1) performing certain actions within that layer and by (2) using the services of the layer directly below it
* A protocol layer can be implemented in software, in hardware, or in a combination of the two
* Application-layer protocols--such as **HTTP** and **SMTP** are almost always implemented in software in the end systems
* One potential drawback of layering is that one layer may duplicate lower-layer functionality. For example, many protocol stacks provide error recovery on both a per-link basis and an end-to-end basis. 
* A second potential drawback is that functionality at one layer may need information (for example, a timestamp value) that is present only in another layer; this violates the goal of separation of layers.
* When taken together, the protocols of the various layers are called the **protocol stack**. The Internet protocol stack consists of five layers: the physical, link, network, transport, and application layers
* We take a **top-down approach**, first covering the application layer and then proceeding downward

#### Application layer
* The application layer is where network applications and their application-layer protocols reside
* The Internet's application layer includes many protocols, such as the **HTTP** protocol (which provides for Web document request and transfer), **SMTP** (which provides for the transfer of e-mail messages), and **FTP** (which provides for the transfer of files between two end systems)
* **domain name system (DNS)** is an application layer protocol
* An application-layer protocol is distributed over multiple end systems, with the application in one end system using the protocol to exchange packets of information with the application in another end system
* We'll refer to this packet of information at the application layer as a **message**

#### Transport Layer
* The Internet's transport layer transports application-layer messages between application endpoints
* In the Internet, there are two transport protocols, **TCP** and **UDP**, either of which can transport application-layer messages
* **TCP** provides a connection-oriented service to its applications
* **TCP** also breaks long messages into shorter segments and provides a congestion-control mechanism, so that a source throttles its transmission rate when the network is congested
* The **UDP** protocol provides a connectionless service to its applications
* This is a no-frills service that provides no reliability, no flow control, and no congestion control this transport-layer packet will be referred to as a **segment** in the book

#### Network Layer
* The Internet's network layer is responsible for moving network-layer packets known as **datagrams** from one host to another
* The Internet transport-layer protocol (**TCP** or **UDP**) in a source host passes a transport-layer segment and a destination address to the network layer
* The Internet's network layer includes the celebrated IP protocol, which defines the fields in the datagram as well as how the end systems and routers act on these fields
* There is only one **IP** protocol, and all Internet components that have a network layer must run the **IP** protocol
* The Internet's network layer also contains routing protocols that determine the routes that datagrams take between sources and destinations
* Although the network layer contains both the **IP** protocol and numerous routing protocols, it is often simply referred to as the **IP layer**

#### Link Layer
* The Internet's network layer routes a datagram through a series of routers between the source and destination
* To move a packet from one node (host or router) to the next node in the route, the network layer relies on the services of the **link layer**
* In particular, at each node, the network layer passes the datagram down to the link layer, which delivers the datagram to the next node along the route
* At this next node, the link layer passes the datagram up to the network layer.
* Examples of link-layer protocols include Ethernet, WiFi, and the cable access network's DOCSIS protocol
* The network layer will receive a different service from each of the different link-layer protocols. In this book, the link-layer packets are called **frames**

#### Physical Layer
* While the job of the link layer is to move entire frames from one network element to an adjacent network element, the job of the physical layer is to move the **individual bits** within the frame from one node to the next
* The protocols in this layer are again link dependent and further depend on the actual transmission medium of the link (for example, twisted-pair copper wire, single-mode fiber optics)
* For example, Ethernet has many physical-layer protocols: one for twisted-pair copper wire, another for A coaxial cable, another for fiber, and so on
* In each case, a bit is moved across the link in a different way

### 1.5.2 Encapsulation
- At the sending host, an **application-layer** message is passed to the transport layer
- The application-layer message and the transport-layer header information together constitute the **transport-layer segment**
- The transport-layer segment thus **encapsulates** the application-layer message
- The transport layer then passes the segment to the network layer, which adds network-layer header information such as source and destination end system addresses, creating a **network-layer datagram**
- The datagram is then passed to the link layer, which will add its own link-layer header information and create a **link-layer frame**
- Thus, we see that at each layer, a packet has two types of fields: header fields and a **payload field**
- The **payload** is typically a packet from the layer above.
	

## 1.6 Networks Under Attack
- A compromised host may also be enrolled in a network of thousands of similarly compromised devices, collectively known as a **botnet**
- Many malware can **self-replicate**. once it infects one host, from that host it seeks entry into other hosts over the Internet
- Another broad class of security threats are known as **denial-of-service (DoS)** attacks
- A DoS attack renders a network, host, or other piece of infrastructure unusable by legitimate users. Web servers, e-mail servers, DNS servers (discussed in Chapter 2), and institutional networks can all be subject to DoS attacks
- **Vulnerability attack** - This involves sending a few well-crafted messages to a vulnerable application or operating system running on a targeted host. If the right sequence of packets is sent to a vulnerable application or operating system, the service can stop or, worse, the host can crash
- **Bandwidth flooding** - The attacker sends a deluge of packets to the targeted host--so many packets that the target's access link becomes clogged, preventing legitimate packets from reaching the server.
- **Connection flooding** - The attacker establishes a large number of half-open or fully open TCP connections (TCP connections are discussed in Chapter 3) at the target host. The host can become so bogged down with these bogus connections that it stops accepting legitimate connections
- In a **distributed DoS (DDoS) attack**, illustrated in Figure 1.25, the attacker controls multiple sources and has each source blast traffic at the target
- DDoS attacks leveraging botnets with thousands of comprised hosts are a common occurrence today
- DDos attacks are much harder to detect and defend against than a DoS attack from a single host
- When using LAN or Wifi, users are sending and receiving packets which can contain all kinds of sensitive information, including passwords, social security numbers, trade secrets, and private personal messages, the book later mentions that all of this is usually encrpyted, this is important because most of the sniffed data is unreadable. A passive receiver that records a copy of every packet that flies by is called a **packet sniffer**
- Packet-sniffing software is freely available at various Web sites and as commercial products i.e. Wireshark
- The ability to inject packets into the Internet with a false source address is known as **IP-spoofing**

## 1.7 History of Computer Networking and the Internet

### 1.7.1 The Development of Packet Switching: 1961-1972
- The first published work on packet-switching techniques was that of Leonard Kleinrock [Kleinrock 1961; Kleinrock 1964] , then a graduate student at MIT. 
- Using queuing theory, Kleinrock's work elegantly demonstrated the effectiveness of the packet-switching approach for bursty traffic sources.
- In 1964, Paul Baran [Baran 1964] at the Rand Institute had begun investigating the use of packet switching for secure voice over military networks, and at the National Physical Laboratory in England, Donald Davies and Roger Scantlebury were also developing their ideas on packet switching.
- J. C. R. Licklider [DEC 1990] and Lawrence Roberts, both colleagues of Kleinrock's at MIT, went on to lead the computer science program at the Advanced Research Projects Agency (ARPA) in the United States.
- Roberts published an overall plan for the ARPAnet [Roberts 1967], the first packet-switched computer network and a direct ancestor of today's public Internet.
- On Labor Day in 1969, the first packet switch was installed at UCLA under Kleinrock's supervision, and three additional packet switches were installed shortly thereafter at the Stanford Research Institute (SRI), UC Santa Barbara, and the University of Utah (Figure 1.26)
- By 1972, ARPAnet had grown to approximately 15 nodes and was given its first public demonstration by Robert Kahn. The first host-to-host protocol between ARPAnet end systems, known as the network-control protocol (NCP), was completed [RFC 001].
- With an end-to-end protocol available, applications could now be written. Ray Tomlinson wrote the first e-mail program in 1972.

### 1.7.2 Proprietary Networks and Internetworking: 1972-1980
- The initial ARPAnet was a single, closed network.
- In order to communicate with an ARPAnet host, one had to be actually attached to another ARPAnet IMP.
- In the early to mid-1970s, additional stand-alone packet-switching networks besides ARPAnet came into being: 
	* ALOHANet, a microwave network linking universities on the Hawaiian islands [Abramson 1970]
	* DARPA's packet-satellite [RFC 829] and packet-radio networks [Kahn 1978]
	* Telenet, a BBN commercial packet-switching network based on ARPAnet technology
	* Cyclades, a French packet-switching network pioneered by Louis Pouzin [Think 2012]
	* Time-sharing networks such as Tymnet and the GE Information Services network

- among others, in the late 1960s and early 1970s [Schwartz 1977]; IBM's SNA (1969–1974), which paralleled the ARPAnet work [Schwartz 1977].
- Pioneering work on interconnecting networks (under the sponsorship of the Defense Advanced Research Projects Agency (DARPA)), in essence creating a network of networks, was done by Vinton Cerf and Robert Kahn [Cerf 1974]
- Early experimentation with TCP, combined with the recognition of the importance of an unreliable, non-flow-controlled, end-to-end transport service for applications such as packetized voice, led to the separation of IP out of TCP and the development of the UDP protocol
- The three key Internet protocols that we see today--**TCP**, **UDP**, and **IP**--were conceptually in place by the end of the 1970s.

### 1.7.3 A Proliferation of Networks: 1980-1990
- By the end of the 1970s, approximately two hundred hosts were connected to the ARPAnet
- By the end of the 1980s the number of hosts connected to the public Internet, a confederation of networks looking much like today's Internet, would reach a hundred thousand
- The 1980s would be a time of tremendous growth
- BITNET provided e-mail and file transfers among several universities in the Northeast
- CSNET (computer science network) was formed to link university researchers who did not have access to ARPAnet
- In 1986, NSFNET was created to provide access to NSF-sponsored supercomputing centers
- 1983 saw the official deployment of TCP/IP as the new standard host protocol for ARPAnet (replacing the NCP protocol)
- The transition [RFC 801] from NCP to TCP/IP was a flag day event--all hosts were required to transfer over to TCP/IP as of that day
- In the late 1980s, important extensions were made to TCP to implement host-based congestion control [Jacobson 1988].
- The DNS, used to map between a human-readable Internet name (for example, gaia.cs.umass.edu) and its 32-bit IP address, was also developed [RFC 1034].
- in the early 1980s the French launched the Minitel project, an ambitious plan to bring data networking into everyone's home.
- he Minitel became a huge success in 1984 when the French government gave away a free Minitel terminal to each French household that wanted one

### 1.7.4 The Internet Explosion: The 1990s
- In 1991, NSFNET lifted its restrictions on the use of NSFNET for commercial purposes
- NSFNET itself would be decommissioned in 1995, with Internet backbone traffic being carried by commercial Internet Service Providers (ISPs)
- The main event of the 1990s was to be the emergence of the World Wide Web application, which brought the Internet into the homes and businesses of millions of people worldwide
- The Web was invented at CERN by Tim Berners-Lee between 1989 and 1991 [Berners-Lee 1989], based on ideas originating in earlier work on hypertext from the 1940s by Vannevar Bush [Bush 1945] and since the 1960s by Ted Nelson [Xanadu 2012].
- Berners-Lee and his associates developed initial versions of HTML, HTTP, a Web server, and a browser--the four key components of the Web. 
- Around the end of 1993 there were about two hundred Web servers in operation, this collection of servers being just a harbinger of what was about to come.
- At about this time several researchers were developing Web browsers with GUI interfaces, including Marc Andreessen, who along with Jim Clark, formed Mosaic Communications, which later became Netscape Communications Corporation [Cusumano 1998; Quittner 1998]
- By 1995, university students were using Netscape browsers to surf the Web on a daily basis.
- In 1996, Microsoft started to make browsers, which started the browser war between Netscape and Microsoft, which Microsoft won a few years later [Cusumano 1998].

#### Popular applications of the late 90s
* E-mail, including attachments and Web-accessible e-mail
* The Web, including Web browsing and Internet commerce
* Instant messaging, with contact lists
* Peer-to-peer file sharing of MP3s, pioneered by Napster

### 1.7.5 The New Millenium 
- Since the beginning of the millennium, we have been seeing aggressive deployment of broadband Internet access to homes--not only cable modems and DSL but also fiber to the home, and now 5G fixed wireless
- This high-speed Internet access has set the stage for a wealth of video applications, including the distribution of user-generated video (for example, YouTube), on-demand streaming of movies and television shows (e.g., Netflix), and multi-person video conference (e.g., Skype, Facetime, and Google Hangouts). Literally no one used Google Hangouts fuckin' liar.
- Many Internet commerce companies are now running their applications in the “cloud"--such as in Amazon's EC2, in Microsoft's Azure, or in the Alibaba Cloud. Many companies and universities have also migrated their Internet applications (e.g., e-mail and Web hosting) to the cloud.
- This Entire Chapter is nothing

# CHAPTER 2 - APPLICATION LAYER

## 2.1 Principles of Network Applications

### 2.1.1 Network Application Architectures
- From the application developer's perspective, the network architecture is fixed and provides a specific set of services to applications. The application architecture, on the other hand, is designed by the application developer and dictates how the application is structured over the various end systems.
- In a **client-server architecture**, there is an always-on host, called the server, which services requests from many other hosts, called clients.
- Another characteristic of the client-server architecture is that the server has a fixed, well-known address, called an **IP address**
- Some of the better-known applications with a client-server architecture include the **Web**, **FTP**, **Telnet**, and **e-mail**
- Often in a client-server application, a single-server host is incapable of keeping up with all the requests from clients.
- For this reason, a **data center**, housing a large number of hosts, is often used to create a powerful virtual server
- Google has 19 data centers distributed around the world, which collectively handle search, YouTube, Gmail, and other services.
- A **data center** can have hundreds of thousands of servers, which must be powered and maintained.

- In a **P2P architecture**, there is minimal (or no) reliance on dedicated servers in data centers.
- Instead the application exploits direct communication between pairs of intermittently connected hosts, called **peers**.
- P2P architectures are also cost effective, since they normally don't require significant server infrastructure and server bandwidth (in contrast with clients-server designs with datacenters). 

### 2.1.2 Process Communicating
- Processes on two different end systems communicate with each other by exchanging **messages** across the computer network
- Processes communicating with each other reside in the application layer of the five-layer protocol stack.

#### Client and Server Processes
- In a P2P file-sharing system, a file is transferred from a process in one peer to a process in another peer
- For each pair of communicating processes, we typically label one of the two processes as the **client** and the other process as the **server**.
- With the Web, a browser is a client process and a Web server is a server process
- With P2P file sharing, the peer that is downloading the file is labeled as the client, and the peer that is uploading the file is labeled as the server
- A process in a P2P file-sharing system can both upload and download files
- In P2P file sharing, when Peer A asks Peer B to send a specific file, Peer A is the client and Peer B is the server in the context of this specific communication session.

#### The Interface Between the Process and the Computer Network
- A process sends messages into, and receives messages from, the network through a software interface called a **socket**.
- A **socket** is the interface between the application layer and the transport layer within a host. It is also referred to as the **Application Programming Interface (API)** between the application and the network, since the socket is the programming interface with which
network applications are built
- Once the application developer chooses a transport protocol (TCP/UDP) (if a choice is available), the application is built using the transport-layer services provided by that protocol.

#### Addressing Processes
- To identify the receiving process, two pieces of information need to be specified: **(1) the address of the host** and **(2) an identifier that specifies the receiving process in the destination host.**
- In the Internet, the host is identified by its **IP address**
- An IP address is a 32-bit value that uniquely identifies a host
- In addition to knowing the address of the host to which a message is destined, the sending process must also identify the receiving process (more specifically, the receiving socket) running in the host. This is known as the **port number**
- Popular applications have been assigned specific port numbers. For example, a Web server is identified by port number 80.
- A mail server process (using the SMTP protocol) is identified by port number 25.

### 2.1.3 Transport Services Available to Applications
- The application at the sending side pushes messages through the socket.
- At the other side of the socket, the transport-layer protocol has the responsibility of getting the messages to the socket of the receiving process.
- When you develop an application, you must choose one of the available transport-layer protocols.
- We can broadly classify the possible services along four dimensions: 
	* reliable data transfer
	* throughput
	* timing
	* security

#### Reliable Data Transfer
- Web document transfers, and financial applications--data loss can have devastating consequences 
- Thus, to support these applications, something has to be done to guarantee that the data sent by one end of the application is delivered correctly and completely to the other end of the application.
- If a protocol provides such a guaranteed data delivery service, it is said to provide **reliable data transfer**.
- One important service that a transport-layer protocol can potentially provide to an application is process-to-process reliable data transfer
- When a transport protocol (TCP/UDP) provides this service, the sending process can just pass its data into the socket and know with complete confidence that the data will arrive without errors at the receiving process
- When a transport-layer protocol doesn't provide reliable data transfer, some of the data sent by the sending process may never arrive at the receiving process.
- This may be acceptable for **loss-tolerant applications**, most notably multimedia applications such as conversational audio/video that can tolerate some amount of data loss. (a.k.a lossy compression, get it right, book)


#### Throughput
- Because other sessions will be sharing the bandwidth along the network path, and because these other sessions will be coming and going, the available **throughput** can fluctuate with time.
- These observations lead to another natural service that a transport-layer protocol could provide, namely, guaranteed available throughput at some specified rate
- With such a service, the application could request a guaranteed throughput of **r** bits/sec, and the transport protocol (TCP/UDP) would then ensure that the available throughput is always at least **r** bits/sec
- If the transport protocol (TCP/UDP) cannot provide this throughput, the application would need to encode at a lower rate (and receive enough throughput to sustain this lower coding rate) or may have to give up, since receiving, say, half of the needed throughput is of little or no use
- Applications that have throughput requirements are said to be **bandwidth-sensitive applications**
- While bandwidth-sensitive applications have specific throughput requirements, **elastic applications** can make use of as much, or as little, throughput as happens to be available
- Electronic mail, file transfer, and Web transfers are all elastic applications.
- More throughput always is better 

#### Timing
- A transport-layer protocol can also provide timing guarantees
- An example guarantee might be that every bit that the sender pumps into the socket arrives at the receiver's socket no more than 100 ms later
- Long delays in Internet telephony, for example, tend to result in unnatural pauses in the conversation; in a multiplayer game or virtual interactive environment, a long delay between taking an action and seeing the response from the environment (a.k.a, ping. This book so out of touch it's ridiculous.)
- For non-real-time applications, lower delay is always preferable to higher delay, but no tight constraint is placed on the end-to-end delays.

#### Security
- A transport protocol can provide an application with one or more security services
- For example, in the sending host, a transport protocol can encrypt all data transmitted by the sending process, and in the receiving host, the transport-layer protocol can decrypt the data before delivering the data to the receiving process
- Such a service would provide confidentiality between the two processes, even if the data is somehow observed between sending and receiving processes.

### 2.1.4 Transport Services Provided by the Internet
- The Internet (and, more generally, TCP/IP networks) makes two transport protocols available to applications, UDP and TCP.
- When you (as an application developer) create a new network application for the nternet, one of the first decisions you have to make is whether to use **UDP** or **TCP**.

#### TCP Services
- The TCP service model includes a connection-oriented service and a reliable data transfer service.
- When an application invokes TCP as its transport protocol, the application receives both of these services from TCP
- **Connection-oriented service** 
	* TCP has the client and server exchange transport-layer control information with each other before the application-level messages begin to flow.
	* This so-called "handshaking procedure" alerts the client and server, allowing them to prepare for an onslaught of packets. After the handshaking phase, a **TCP connection** is said to exist between the sockets of the two processes.
	* The connection is a full-duplex connection in that the two processes can send messages to each other over the connection at the same time.
	* When the application finishes sending messages, it must tear down the connection.
- **Reliable data transfer service** 
	* The communicating processes can rely on TCP to deliver all data sent without error and in the proper order.
	* When one side of the application passes a stream of bytes into a socket, it can count on TCP to deliver the same stream of bytes to the receiving socket, with no missing or duplicate bytes.
	* TCP also includes a congestion-control mechanism, a service for the general welfare of the Internet rather than for the direct benefit of the communicating processes.
	* The TCP congestion-control mechanism throttles a sending process (client or server) when the network is congested between sender and receiver.

#### UDP Services
	* UDP is a no-frills, lightweight transport protocol, providing minimal services.
	* UDP is connectionless, so there is no handshaking before the two processes start to communicate.
	* UDP provides no guarantee that the message will ever reach the receiving process. Furthermore, messages that do arrive at the receiving process may arrive out of order. This makes it an **unreliable data transfer service**
	* UDP does not include a congestion-control mechanism, so the sending side of UDP can pump data into the layer below (the network layer) at any rate it pleases

#### Services Not Provided by Internet Transport Protocols
- We have organized transport protocol services along four dimensions: 
	* reliable data
	* transfer 
	* throughput
	* timing
	* security.
- Which of these services are provided by TCP and UDP?
	* TCP provides reliable end-to-end data transfer.
	* TCP can be easily enhanced at the application layer with transport layer security (TLS) to provide security services
	* E-mail, remote terminal access, the Web, and file transfer all use TCP.
	* These applications have chosen TCP primarily because TCP provides reliable data transfer, guaranteeing that all data will eventually get to its destination

```
Application                 Application-Layer Protocol          Underlying Transport Protocol
Electronic mail             SMTP [RFC 5321]                     TCP
Remote terminal access      Telnet [RFC 854]                    TCP
Web                         HTTP 1.1 [RFC 7230]                 TCP
File transfer               FTP [RFC 959]                       TCP
Streaming multimedia        HTTP (e.g., YouTube), DASH          TCP
Internet telephony          SIP [RFC 3261], RTP [RFC 3550]      UDP or TCP
```

- Developers of Internet telephony applications usually prefer to run their applications over UDP, thereby circumventing TCP's congestion control mechanism and packet overheads.
- Many firewalls are configured to block (most types of) UDP traffic
- Internet telephony applications are often designed to use TCP as a backup if UDP communication fails.

### 2.1.5 Application-Layer Protocols
- Network processes communicate with each other by sending messages into sockets.
- But how are these messages structured?
- What are the meanings of the various fields in the messages?
- When do the processes send the messages?
- The answers to these questions aren't important, basically, the Application-Layer Protocols take care of all of these things. 

- An **application-layer protocol** defines:
	* The types of messages exchanged, for example, request messages and response messages
	* The syntax of the various message types, such as the fields in the message and how the fields are delineated
	* The semantics of the fields, that is, the meaning of the information in the fields
	* Rules for determining when and how a process sends messages and responds to messages

- Some application-layer protocols are specified in (requests for comments) RFCs and are therefore in the public domain
- The Web's application-layer protocol, HTTP (the HyperText Transfer Protocol [RFC 7230]), is available as an RFC
- If a browser developer follows the rules of the HTTP RFC, the browser will be able to retrieve Web pages from any Web server that has also followed the rules of the HTTP RFC
- Many other application-layer protocols are proprietary and intentionally not available in the public domain. For example, Skype uses proprietary application-layer protocols.

- The Web is a client-server application that allows users to obtain documents from Web servers on demand
- The Web application consists of many components:
	* a standard for document formats (that is, HTML)
	* Web browsers (for example, Chrome and ~~Microsoft Internet Explorer~~ Firefox)
	* Web servers (for example, Apache and ~~Microsoft~~ servers) Windows servers are not real servers IMO
	* and an application-layer protocol

- The Web's application-layer protocol, HTTP, defines the format and sequence of messages exchanged between browser and Web server
- Netflix uses a DASH protocol

### 2.1.6 Network Applications Covered in This Book
- important applications: 
	* The Web
	* electronic mail
	* directory service
	* video streaming
	* and P2P applications

## 2.2 The Web and HTTP
- In the early 1990s, a major new application arrived on the scene--the World Wide Web [Berners-Lee 1994]
- Forms, JavaScript, video, and many other devices enable us to interact with pages and sites.

### 2.2.1 Overview of HTTP
- The **HyperText Transfer Protocol (HTTP)**, the Web's application-layer protocol, is at the heart of the Web
- It is defined in [RFC 1945], [RFC 7230] and [RFC 7540]
- HTTP is implemented in two programs:
	* a client program
	* a server program
- The client program and server program, executing on different end systems, talk to each other by exchanging HTTP messages
- HTTP defines the structure of these messages and how the client and server exchange the messages
- A **Web page** (also called a document) consists of objects
- An object is simply a file--such as an **HTML** file, a **JPEG** image, a Javascrpt file, a **CSS** style sheet file, or a video clip--that is addressable by a single **URL**
- Most Web pages consist of a base **HTML file** and several referenced objects
- Each URL has two components: 
	* the hostname of the server
	* object's path name
- In the URL: `http://www.someSchool.edu/someDepartment/picture.gif`
	* hostname = `www.someSchool.edu`
	* path name = `/someDepartment/picture.gif`
- Because **Web browsers** implement the client side of HTTP, in the context of the Web, we will use the words `browser` and `client` interchangeably
- **Web servers**, which implement the server side of HTTP, house Web objects, each addressable by a URL
- HTTP request messages for the objects in the page to the server
- HTTP uses TCP as its underlying transport protocol (rather than running on top of UDP)
- HTTP Process 
	* The HTTP client first initiates a TCP connection with the server
	* Once the connection is established, the browser and the server processes access TCP through their socket interfaces
	* The client sends HTTP request messages into its socket interface and receives HTTP response messages from its socket interface
	* Similarly, the HTTP server receives request messages from its socket interface and sends response messages into its socket interface
	* Once the client sends a message into its socket interface, the message is out of the client's hands and is “in the hands" of TCP
- The server sends requested files to clients without storing any state information about the client
- Because an HTTP server maintains no information about the clients, HTTP is said to be a **stateless protocol**

- Web server is always on, with a fixed IP address, and it services requests from potentially millions of different browsers.
- The original version of HTTP is called HTTP/1.0 and dates back to the early 1990's [RFC 1945]
- As of 2020, the majority of HTTP transactions take place over HTTP/1.1 [RFC 7230]
- However, increasingly browsers and Web servers also support a new version of HTTP called HTTP/2 [RFC 7540]

### 2.2.2 Non-Persistent and Persistent Connections
- Should each request/response pair be sent over a separate TCP connection? If so, this is a **non-persistent connection**
- Should all of the requests and their corresponding responses be sent over the same TCP connection? If so, this is a **persistent connection**
- Although HTTP uses persistent connections in its default mode, HTTP clients and servers can be configured to use non-persistent connections instead


#### HTTP with Non-Persistent Connections
- Suppose the page consists of a base HTML file and 10 JPEG images, and that all 11 of these objects reside on the same server.
- Suppose the URL for the base HTML file is `http://www.someSchool.edu/someDepartment/home.index`
- Here is what happens:
	1. The HTTP client process initiates a TCP connection to the server `www.someSchool.edu` on port number 80, which is the default port number for HTTP. Associated with the TCP connection, there will be a socket at the client and a socket at the server.
	2. The HTTP client sends an HTTP request message to the server via its socket. The request message includes the path name `/someDepartment/home.index`
	3. The HTTP server process receives the request message via its socket, retrieves the object `/someDepartment/home.index` from its storage (RAM or disk), encapsulates the object in an HTTP response message, and sends the response message to the client via its socket
	4. The HTTP server process tells TCP to close the TCP connection. (But TCP doesn't actually terminate the connection until it knows for sure that the client has received the response message intact.)
	5. The HTTP client receives the response message. The TCP connection terminates. The message indicates that the encapsulated object is an HTML file. The client extracts the file from the response message, examines the HTML file, and finds references to the 10 JPEG objects.
	6. The first four steps are then repeated for each of the referenced JPEG objects.

- The steps above illustrate the use of non-persistent connections, where each TCP connection is closed after the server sends the object--the connection does not persist for other objects
- HTTP/1.0 employes non-persistent TCP connections. Note that each non-persistent TCP connection transports exactly one request message and one response message
- **round-trip time (RTT)**, is the time it takes for a small packet to travel from client to server and then back to the client
- The **RTT** includes packet-propagation delays, packetqueuing delays in intermediate routers and switches, and packet-processing delays
- This causes the browser to initiate a TCP connection between the browser and the Web server
- This involves a “three-way handshake"
	* the client sends a small TCP segment to the server
	* the server acknowledges and responds with a small TCP segment
	* the client acknowledges back to the server
- The first two parts of the three-way handshake take one RTT
- the client sends the HTTP request message combined with the third part of the three-way handshake (the acknowledgment) into the TCP connection
- This HTTP request/response eats up another RTT. Thus, roughly, the total response time is two RTTs plus the transmission time at the server of the HTML file

#### HTTP with Persistent Connections
- Non-persistent connections have some shortcomings
	* a brand-new connection must be established and maintained for `each requested object`
	* For each of these connections, TCP buffers must be allocated and TCP variables must be kept in both the client and server
	* This can place a significant burden on the Web server, which may be serving requests from hundreds of different clients simultaneously
	* each object suffers a delivery delay of two RTTs--one RTT to establish the TCP connection and one RTT to request and receive an object
- With HTTP/1.1 persistent connections, the server leaves the TCP connection open after sending a response
- Subsequent requests and responses between the same client and server can be sent over the same connection
- In particular, an entire Web page (in the example above, the base HTML file and the 10 images) can be sent over a single persistent TCP connection
- Moreover, multiple Web pages residing on the same server can be sent from the server to the same client over a single persistent TCP connection
- Typically, the HTTP server closes a connection when it isn't used for a certain time (a configurable timeout interval)
- When the server receives the back-to-back requests, it sends the objects back-to-back
- The default mode of HTTP uses persistent connections with pipelining.

### 2.2.3 HTTP Message Format
- The HTTP specifications [RFC 1945; RFC 7230; RFC 7540] include the definitions of the HTTP message formats.
- There are two types of HTTP messages
	* **request messages** 
	* **response messages**

#### HTTP Request Message
```
Below we provide a typical HTTP request message:
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/5.0
Accept-language: fr
```

- The message is written in ordinary ASCII text, i.e. it is human readable
- The message consists of five lines, each followed by a carriage return and a line feed
- The last line is followed by an additional carriage return and line feed.
- The first line of an HTTP request message is called the **request line**
- The subsequent lines are called the **header lines**
- The request line has three fields:
	* method field
	* URL field
	* HTTP version field
- The method field can take several different values including:
 	* GET
	* POST
	* HEAD
	* PUT
	* DELETE.

- The great majority of HTTP request messages use the GET method. 
- The GET method is used when the browser requests an object, with the requested object identified in the URL field
- The header line `Host: www.someschool.edu` specifies the host on which the object resides
- By including the `Connection: close` header line, the browser is telling the server that it doesn't want to bother with persistent connections
- The `User-agent:` header line specifies the user agent i.e. the browser type that is making the request to the server
- The `Accept-language:` header indicates that the user prefers to receive a French version of the object, if such an object exists on the server; otherwise, the server should send its default version
- The entity body is empty with the GET method, but is used with the POST method
- An HTTP client often uses the POST method when the user fills out a form i.e. searching something on Google
- With a POST message, the user is still requesting a Web page from the server, but the specific contents of the Web page depend on what the user entered into the form fields
- If the value of the method field is POST, then the entity body contains what the user entered into the form fields
- The HEAD method is similar to the GET method. When a server receives a request with the HEAD method, it responds with an HTTP message but it leaves out the requested object
- Application developers often use the HEAD method for debugging
- The PUT method is often used in conjunction with Web publishing tools
- The PUT method is also used by applications that need to upload objects to Web servers
- The DELETE method allows a user, or an application, to delete an object on a Web server

#### HTTP Response Message

```
HTTP/1.1 200 OK
Connection: close
Date: Tue, 18 Aug 2015 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html

(data data data data data ...)
```
- The HTTP Response Message has three sections: 
	* an initial status line
	* six header lines
	* and then the entity body
- The entity body contains the requested object itself (represented by `data data data data data ...`) 
- The status line has three fields: 
	* the protocol version field
	* a status code
	* and a corresponding status message.
- In this example, the status line indicates that the server is using HTTP/1.1 and that everything is OK
- The server uses the `Connection: close` header line to tell the client that it is going to close the TCP connection after sending the message.
- The `Date:` header line indicates the time and date when the HTTP response was created and sent by the server
- The `Server:` header line indicates that the message was generated by an Apache Web server; it is analogous to the `User-agent:` header line in the HTTP request message
- The `Last-Modified:` header line indicates the time and date when the object was created or last modified.
- The `Content-Length:` header line indicates the number of bytes in the object being sent.

- Some common status codes and associated phrases include:
	* `200 OK:` Request succeeded and the information is returned in the response.
	* `301 Moved Permanently:` Requested object has been permanently moved; the new URL is specified in Location: header of the response message. The client software will automatically retrieve the new URL.
	* `400 Bad Request:` This is a generic error code indicating that the request could not be understood by the server.
	* `404 Not Found:` The requested document does not exist on this server.
	* `505 HTTP Version Not Supported:` The requested HTTP protocol version is not supported by the server.

**Q:** How does a browser decide which header lines to include in a request message?

**A:** A browser will generate header lines as a function of the browser type and version, the user configuration of the browser and whether the browser currently has a cached, but possibly out-of-date, version of the object.

**Q:** How does a Web server decide which header lines to include in a response message?

**A:** Web servers behave similarly: There are different products, versions, and configurations, all of which influence which header lines are included in response messages.

### 2.2.4 User-Server Interaction: Cookies
- An HTTP server is stateless
- This simplifies server design and has permitted engineers to develop high-performance Web servers that can handle thousands of simultaneous TCP connections
- However, it is often desirable for a Web site to identify users
- For these purposes, HTTP uses cookies. 
- Cookies, defined in [RFC 6265], allow sites to keep track of users. 
- Most major commercial Web sites use cookies today
- The first time a user visits a site, the user can provide a user identification (possibly his or her name)
- During the subsequent sessions, the browser passes a cookie header to the server, thereby identifying the user to the server
- Cookies can thus be used to create a user session layer on top of stateless HTTP
- For example, when a user logs in to a Web-based e-mail application (such as Hotmail), the browser sends cookie information to the server, permitting the server to identify the user throughout the user's session with the application
- Web site can learn a lot about a user through cookies and potentially sell this information to a third party

### 2.2.5 Web Caching
- A **Web cache**/**proxy server**is a network entity that satisfies HTTP requests on the behalf of an origin Web server
- The Web cache has its own disk storage and keeps copies of recently requested objects in this storage
- Suppose a browser is requesting the object `http://www.someschool.edu/campus.gif`
	1. The browser establishes a TCP connection to the Web cache and sends an HTTP request for the object to the Web cache.
	2. The Web cache checks to see if it has a copy of the object stored locally. If it does, the Web cache returns the object within an HTTP response message to the client browser.
	3. If the Web cache does not have the object, the Web cache opens a TCP connection to the origin server, that is, to `www.someschool.edu`. The Web cache then sends an HTTP request for the object into the cache-to-server TCP connection. After receiving this request, the origin server sends the object within an HTTP response to the Web cache.
	4. When the Web cache receives the object, it stores a copy in its local storage and sends a copy, within an HTTP response message, to the client browser (over the existing TCP connection between the client browser and the Web cache).

- Note that a cache is both a server and a client at the same time
	* When it receives requests from and sends responses to a browser, it is a server
	* When it sends requests to and receives responses from an origin server, it is a client
- Typically a Web cache is purchased and installed by an ISP
- Web caching has seen deployment in the Internet for two reasons. 
	* First, a Web cache can substantially reduce the response time for a client request, particularly if the bottleneck bandwidth between the client and the origin server is much less than the bottleneck bandwidth between the client and the cache
	* Second, as we will soon illustrate with an example, Web caches can substantially reduce traffic on an institution's access link to the Internet. By reducing traffic, the institution (for example, a company or a university) does not have to upgrade bandwidth as quickly, thereby reducing costs
	* Furthermore, Web caches can substantially reduce Web traffic in the Internet as a whole, thereby improving performance for all applications
- Examples: 
- The traffic intensity on the LAN
	* `(15 requests/sec) # (1 Mbits/request)/(100 Mbps) = 0.15`
- Whereas the traffic intensity on the access link (from the Internet router to institution router) is
	* `(15 requests/sec) # (1 Mbits/request)/(15 Mbps) = 1`

- A traffic intensity of 0.15 on a LAN typically results in, at most, tens of milliseconds of delay; hence, we can neglect the LAN delay	
- However, as discussed earlier, as the traffic intensity approaches 1, the delay on a link becomes very large and grows without bound ( it diverges )
- Thus, the average response time to satisfy requests is going to be on the order of minutes, if not more, which is unacceptable for the institution's users.
- Through the use of **Content Distribution Networks (CDNs)**, Web caches are increasingly playing an important role in the Internet

#### The Conditional GET
- HTTP has a mechanism that allows a cache to verify that its objects are up to date
- This mechanism is called the **conditional GET** [RFC 7232]

### 2.2.6 HTTP/2
- HTTP/2 [RFC 7540], standardized in 2015, was the first new version of HTTP since HTTP/1.1, which was standardized in 1997
- Since standardization, HTTP/2 has taken off, with over 40% of the top 10 million websites supporting HTTP/2 in 2020 [W3Techs]
- The primary goals for HTTP/2 are to reduce perceived latency by enabling request and response multiplexing over a single TCP connection, provide request prioritization and server push, and provide efficient compression of HTTP header fields
- HTTP/2 does not change HTTP methods, status codes, URLs, or header fields
- HTTP/2 changes how the data is formatted and transported between the client and server
- developers of Web browsers quickly discovered that sending all the objects in a Web page over a single TCP connection has a **Head of Line (HOL)** blocking problem

- Suppose there is a Web page that includes an HTML base page, a large video clip near the top of Web page, and many small objects below the video
- Suppose there is a low-to-medium speed bottleneck link (for example, a low-speed wireless link) on the path between server and client
- Using a single TCP connection, the video clip will take a long time to pass through the bottleneck link, while the small objects are delayed as they wait behind the video clip; that is, the video clip at the head of the line blocks the small objects behind it
- HTTP/1.1 browsers typically work around this problem by opening multiple parallel TCP connections, thereby having objects in the same web page sent in parallel to the browser
- **TCP congestion control**, discussed in detail in Chapter 3, also provides browsers an unintended incentive to use multiple parallel TCP connections rather than a single persistent connection
- TCP congestion control aims to give each TCP connection sharing a bottleneck link an equal share of the available bandwidth of that link; so if there are `n` TCP connections operating over a bottleneck link, then each connection approximately gets `1/nth` of the bandwidth
- By opening multiple parallel TCP connections to transport a single Web page, the browser can "cheat" and grab a larger portion of the link bandwidth
- Many HTTP/1.1 browsers open up to six parallel TCP connections not only to circumvent HOL blocking but also to obtain more bandwidth

#### HTTP/2 Framing
- The HTTP/2 solution for HOL blocking is to break each message into small frames, and interleave the request and response messages on the same TCP connection
- The ability to break down an HTTP message into independent frames, interleave them, and then reassemble them on the other end is the single most important enhancement of HTTP/2
- The framing is done by the framing sub-layer of the HTTP/2 protocol. 
- When a server wants to send an HTTP response, the response is processed by the framing sub-layer, where it is broken down into frames.
- In addition to breaking down each HTTP message into independent frames, the framing sublayer also binary encodes the frames. 
- Binary protocols are more efficient to parse, lead to slightly smaller frames, and are less error-prone.

#### Response Message Prioritization and Server Pushing
- **Message prioritization** allows developers to customize the relative priority of requests to better optimize application performance
- When a client sends concurrent requests to a server, it can prioritize the responses it is requesting by assigning a weight between 1 and 256 to each message. The higher number indicates higher priority
- In addition to this, the client also states each message's dependency on other messages by specifying the ID of the message on which it depends
- Another feature of HTTP/2 is the ability for a server to send multiple responses for a single client request
- In addition to the response to the original request, the server can push additional objects to the client, without the client having to request each one

#### HTTP/3
- QUIC, discussed in Chapter 3, is a new “transport" protocol that is implemented in the application layer over the bare-bones UDP protocol
- QUIC has several features that are desirable for HTTP, such as message multiplexing (interleaving), per-stream flow control, and low-latency connection establishment

## 2.3 Electronic Mail in the Internet
- Electronic mail has been around since the beginning of the Internet. It was the most popular application when the Internet was in its infancy [Segaller 1998]
- In contrast with postal mail, electronic mail is fast, easy to distribute, and inexpensive
- Modern e-mail has many powerful features, including messages with attachments, hyperlinks, HTML-formatted text, and embedded photos
- e-mail has three major components: 
	* **user agents** 
	* **mail servers**
	* **Simple Mail Transfer Protocol (SMTP)**
- User agents allow users to read, reply to, forward, save, and compose messages.
- Examples of user agents for e-mail include Microsoft Outlook, Apple Mail, Web-based Gmail, the Gmail App running in a smartphone, and so on
- Each recipient, has a mailbox located in one of the mail servers
- A typical message starts its journey in the sender's user agent, then travels to the sender's mail server, and then travels to the recipient's mail server, where it is deposited in the recipient's mailbox
- If Alice's server cannot deliver mail to Bob's server, Alice's server holds the message in a **message queue** and attempts to transfer the message later
- **SMTP** is the principal application-layer protocol for Internet electronic mail. It uses the reliable data transfer service of TCP to transfer mail from the sender's mail server to the recipient's mail server.
- As with most application-layer protocols, SMTP has two sides: 
	* a client side, which executes on the sender's mail server 
	* and a server side, which executes on the recipient's mail server
- Both the client and server sides of SMTP run on every mail server
- When a mail server sends mail to other mail servers, it acts as an SMTP client. 
- When a mail server receives mail from other mail servers, it acts as an SMTP server.


### 2.3.1 SMTP
- SMTP transfers messages from senders' mail servers to the recipients' mail servers.
- SMTP is much older than HTTP. (The original SMTP RFC dates back to 1982, and SMTP was around long before that.)
- Although SMTP has numerous wonderful qualities, it is nevertheless a legacy technology that possesses certain archaic characteristics
- For example, it restricts the body (not just the headers) of all mail messages to simple 7-bit ASCII.
- This restriction made sense in the early 1980s when transmission capacity was scarce and no one was e-mailing large attachments or large image, audio, or video files
- Today, the 7-bit ASCII restriction is a bit of a pain. It requires binary multimedia data to be encoded to ASCII before being sent over SMTP; and it requires the corresponding ASCII message to be decoded back to binary after SMTP transport
- HTTP does not require multimedia data to be ASCII encoded before transfer.
- Suppose Alice wants to send Bob a simple ASCII message.
	1. Alice invokes her user agent for e-mail, provides Bob's e-mail address (i.e., `bob@someschool.edu`), composes a message, and instructs the user agent to send the message
	2. Alice's user agent sends the message to her mail server, where it is placed in a message queue.
	3. The client side of SMTP, running on Alice's mail server, sees the message in the message queue. It opens a TCP connection to an SMTP server, running on Bob's mail server.
	4. After some initial SMTP handshaking, the SMTP client sends Alice's message into the TCP connection.
	5. At Bob's mail server, the server side of SMTP receives the message. Bob's mail server then places the message in Bob's mailbox.
	6. Bob invokes his user agent to read the message at his convenience.

- It is important to observe that SMTP does not normally use intermediate mail servers for sending mail, even when the two mail servers are located at opposite ends of the world
- If Alice's server is in Hong Kong and Bob's server is in St. Louis, the TCP connection is a direct connection between the Hong Kong and St. Louis servers
- In particular, if Bob's mail server is down, the message remains in Alice's mail server and waits for a new attempt--the message does not get placed in some intermediate mail server.

#### How does SMTP transfer a message from a sending mail server to a receiving mail server?
- The client SMTP (running on the sending mail server host) has TCP establish a connection to port 25 at the server SMTP (running on the receiving mail server host)
- If the server is down, the client tries again later
- Once this connection is established, the server and client perform some application-layer handshaking. 
- Similar to how humans would introduce themselves before transferring information from one to another, SMTP clients and servers introduce themselves before transferring information
- During this SMTP handshaking phase, the SMTP client indicates the e-mail address of the sender (the person who generated the message) and the e-mail address of the recipient
- Once the SMTP client and server have introduced themselves to each other, the client sends the message
- SMTP can count on the reliable data transfer service of TCP to get the message to the server without errors
- The client then repeats this process over the same TCP connection if it has other messages to send to the server; otherwise, it instructs TCP to close the connection

- Suppose the hostname of the client is `crepes.fr` and the hostname of the server is `hambuger.edu`
- The ASCII text lines prefaced with `C:` are exactly the lines the client sends into its TCP socket, and the ASCII text lines prefaced with `S:` are exactly the lines the server sends into its TCP socket.

- This is an an example transcript of messages exchanged between an SMTP client (C) and an SMTP server (S)
```
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr ... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

- In the example above, the client sends a message (“`Do you like ketchup? How about pickles?"`) from mail server `crepes.fr` to mail server `hamburger.edu`
- As part of the dialogue, the client issued five commands: 
	* HELO (an abbreviation for HELLO)
	* MAIL FROM
	* RCPT TO
	* DATA
	* QUIT
- In ASCII , each message ends with `CRLF`. `CRLF`, where `CR` and `LF` stand for carriage return and line feed, respectively
- The server issues replies to each command, with each reply having a reply code and some (optional) English-language explanation
- SMTP uses persistent connections: 
	* If the sending mail server has several messages to send to the same receiving mail server, it can send all of the messages over the same TCP connection
	* For each message, the client begins the process with a new `MAIL FROM: crepes.fr`, designates the end of message with an isolated period, and issues `QUIT` only after all messages have been sent.

- It is highly recommended that you use Telnet to carry out a direct dialogue with an SMTP server
	* you can do this by running the command `telnet serverName 25`
	* When you do this, you are simply establishing a TCP connection between your local host and the mail server.
	* After typing this line, you should immediately receive the `220` reply from the server
	* Then issue the SMTP commands `HELO`, `MAIL` `FROM`, `RCPT` `TO`, `DATA`, `CRLF`.
	* `CRLF`, and `QUIT` at the appropriate times.

### 2.3.2 Mail Message Formats
- As with HTTP, each header line contains readable text, consisting of a keyword followed by a colon followed by a value
- Some of the keywords are required and others are optional
- Every header must have a `From:` header line and a `To:` header line 
- A header may include a `Subject:` header line as well as other optional header lines
- It is important to note that these header lines are different from the SMTP commands, even though they contain some of the same words, such as `From:` and `To:` 
- The commands in the previous section were part of the SMTP handshaking protocol 
- The header lines examined in this section are part of the mail message itself

- A typical message header looks like this:
```
From: alice@crepes.fr
To: bob@hamburger.edu
Subject: Searching for the meaning of life.
```
- I think we all know what an email looks like.

### 2.3.3 Mail Access Protocols
- Once SMTP delivers the message from Alice's mail server to Bob's mail server, the message is placed in Bob's mailbox. 
- Given that Bob (the recipient) executes his user agent on his local host (e.g., smartphone or PC), it is natural to consider placing a mail server on his local host as well
- With this approach, Alice's mail server would dialogue directly with Bob's PC
- There is a problem with this approach, however. 
- A mail server manages mailboxes and runs the client and server sides of SMTP.
- If Bob's mail server were to reside on his local host, then Bob's host would have to remain always on, and connected to the Internet, in order to receive new mail, which can arrive at any time (Yes, no shit. This is how servers work.)
- Typically, most users run a user agent on the local host but accesses its mailbox stored on an always-on shared mail server. This mail server is shared with among other users.
- Let's consider the path an e-mail message takes when it is sent from Alice to Bob
- The e-mail message needs to be deposited in Bob's mail server. 
- This could be done simply by having Alice's user agent send the message directly to Bob's mail server. 
- However, typically the sender's user agent does not dialogue directly with the recipient's mail server
- Instead, Alice's user agent uses SMTP or HTTP to deliver the e-mail message into her mail server, then Alice's mail server uses SMTP (as an SMTP client) to relay the e-mail message to Bob's mail server

####  Why a two step procedure?
- If we sent the message directly to Bob's server while his computer is not on, the email would have nowhere to go. By first deposting the the email in her own server, Alice's mail server can reattempt to send the mail if it does not go through, until it finally does go through.
- How does a recipient like Bob, running a user agent on his local host , obtain his messages, which are sitting in a mail server?
- Bob's user agent can't use SMTP to obtain the messages because obtaining the messages is a pull operation, SMTP is a push protocol and cannot do this.
- Today, there are two common ways for Bob to retrieve his e-mail:
	* If Bob is using Web-based e-mail or a smartphone app (such as Gmail), then the user agent will use HTTP to retrieve Bob's e-mail. This case requires Bob's mail server to have an HTTP interface as well as an SMTP interface (to communicate with Alice's mail server)
	* The alternative is typically used with mail clients such as Microsoft Outlook, the **Internet Mail Access Protocol (IMAP)**
- Both the **HTTP** and **IMAP** approaches allow Bob to manage folders, maintained in Bob's mail server

## 2.4 DNS - The Internet's Directory Service
- One identifier for a host is its **hostname**, i.e. `www.facebook.com`
- **Hostnames** are mnemonic and preferred over using just a raw IP address. It is also a bit safer security wise to use hostnames, so that your website URL isn't displaying your server's IP address to every user that visits the website.
- While hostnames are nice, they do not tell us, (or more importantly, the computer) much about that website. Perhaps the URL ends in a country code such as `.fr` or `.io`. This however, still does not provide us much information about that website.
- For these reasons, hosts are also identified by **IP addresses**


### 2.4.1 Services Provided by DNS
- there are two ways to identify a host: 
	* by its hostname
	* by its IP address
- While human's will prefer hostnames, a computer prefers IP addresses. 
- This task can be resolved through the Internet's **domain name system (DNS)**
- The DNS is:
	1. distributed database implemented in a hierarchy of **DNS servers**
	2. an application-layer protocol that allows hosts to query the distributed database

- DNS servers are often UNIX machines running **Berkeley Internet Name Domain (BIND)** software

- DNS is commonly employed by other application-layer protocols, including HTTP and SMTP, to translate user-supplied hostnames to IP addresses

- Example: 
	* consider what happens when a browser (that is, an HTTP client), running on some user's host, requests the URL `www.someschool.edu/index.html`.
	* In order for the user's host to be able to send an HTTP request message to the Web server `www.someschool.edu`, the user's host must first obtain the IP address of `www.someschool.edu`
- This is done as follows:
	1. The same user machine runs the client side of the DNS application.
	2. The browser extracts the hostname, www.someschool.edu, from the URL and passes the hostname to the client side of the DNS application.
	3. The DNS client sends a query containing the hostname to a DNS server.
	4. The DNS client eventually receives a reply, which includes the IP address for the hostname.
	5. Once the browser receives the IP address from DNS, it can initiate a TCP connection to the HTTP server process located at port 80 at that IP address.

- We see from this example that DNS adds an additional delay which is sometimes substantial to the Internet applications that use it.
- However, in most cases, the desired IP address is often cached in a “nearby" DNS server, which helps to reduce DNS network traffic as well as the average DNS delay

- DNS provides a few other important services in addition to translating hostnames to IP addresses:
	* **Host aliasing**. A host with a complicated hostname can have one or more alias names. (i.e. the URL `relay1.west-coast.enterprise.com` being aliased to `enterprise.com` and/or `www.enterprise.com`. In this case, the hostname `relay1.west-coast.enterprise.com` is said to be a **canonical hostname**. The DNS can be invoked by an application to obtain the **canonical hostname** for a supplied alias hostname as well as the IP address of the host
	* **Mail server aliasing**. It is highly desirable to make e-mail addresses be mnemonic.If there were no **Mail serer aliasing**, we would have compicated email addresses... like `bob@relay1.west-coast.yahoo.com` for example. Or even worse, raw IP addresses as hostnames.
	* **Load distribution**. DNS is also used to perform load distribution among replicated servers, such as replicated Web servers
	* Busy sites, such as `cnn.com`, are replicated over multiple servers, with each server running on a different end system and each having a different IP address
	* For replicated Web servers, a set of IP addresses is thus associated with one alias hostname
	* The DNS database contains this set of IP addresses
	* When clients make a DNS query for a name mapped to a set of addresses, the server responds with the entire set of IP addresses, but rotates the ordering of the addresses within each reply
	* Because a client typically sends its HTTP request message to the IP address that is listed first in the set, DNS rotation distributes the traffic among the replicated servers
	* DNS rotation is also used for e-mail so that multiple mail servers can have the same alias name

### 2.4.2 Overview of How DNS Works
- Suppose that some application (such as a Web browser or a mail client) running in a user's host needs to translate a hostname to an IP address
- The application will invoke the client side of DNS, specifying the hostname that needs to be translated
- On many UNIX-based machines, `gethostbyname()` is the function call that an application calls in order to perform the translation.
- DNS in the user's host then takes over, sending a query message into the network. 
- All DNS query and reply messages are sent within UDP datagrams to port 53.
- After a delay, ranging from milliseconds to seconds, DNS in the user's host receives a DNS reply message that provides the desired mapping
- This mapping is then passed to the invoking application
- A simple design for DNS would have one DNS server that contains all the mappings. In this centralized design, clients simply direct all queries to the single DNS server, and the DNS server responds directly to the querying clients
- However, while this idea is simple, by today's standards, having only one DNS server to store all the mappings is a terrible idea. 
- The problems with a centralized design are:
	* A **single point of failure**. If the DNS server crashes, so does the entire Internet!
	* **Traffic volume**. A single DNS server would have to handle all DNS queries (for all the HTTP requests and e-mail messages generated from hundreds of millions of hosts).
	* **Distant centralized database**. A single DNS server cannot be “close to" all the querying clients. If we put the single DNS server in New York City, then all que- ries from Australia must travel to the other side of the globe, perhaps over slow and congested links. This can lead to significant delays.
	* **Maintenance**. The single DNS server would have to keep records for all Internet hosts. Not only would this centralized database be huge, but it would have to be updated frequently to account for every new host.

- In summary, a centralized database in a single DNS server simply doesn't scale.
- Consequently, the DNS is distributed by design. 
- In fact, the DNS is a great example of how a distributed database can be implemented in the Internet.

#### A Distributed, Hierarchical Database
- In order to deal with the issue of scale, the DNS uses a large number of servers, organized in a hierarchical fashion and distributed around the world
- No single DNS server has all of the mappings for all of the hosts in the Internet, the mappings are distributed across the DNS servers.
- There are three classes of DNS servers: 
	* root DNS servers
	* top-level domain (TLD) DNS servers
	* authoritative DNS servers

- **Root DNS servers**. There are more than 1000 root servers instances scattered all over the world. These root servers are copies of 13 different root servers, managed by 12 different organizations, and coordinated through the Internet Assigned Numbers Authority [IANA 2020]. Root name servers provide the IP addresses of the TLD servers.
- **Top-level domain (TLD) servers**. For each of the top-level domains--top-level domains such as com, org, net, edu, and gov, and all of the country top-level domains such as uk, fr, ca, and jp, there is TLD server (or server cluster).
- **Authoritative DNS servers**. Every organization with publicly accessible hosts (such as Web servers and mail servers) on the Internet must provide publicly accessible DNS records that map the names of those hosts to IP addresses
- An organization's authoritative DNS server houses these DNS records.
- An organization can choose to implement its own authoritative DNS server to hold these records; alternatively, the organization can pay to have these records stored in an authoritative DNS server of some service provider.
- Most universities and large companies implement and maintain their own primary and secondary (backup) authoritative DNS server.

- The root, TLD, and authoritative DNS servers all belong to the hierarchy of DNS servers.
- There is another important type of DNS server called the **local DNS server**
- A local DNS server does not strictly belong to the hierarchy of servers but is nevertheless central to the DNS architecture
- Each ISP--such as a residential ISP or an institutional ISP--has a local DNS server (also called a default name server)
- When a host connects to an ISP, the ISP provides the host with the IP addresses of one or more of its local DNS servers (typically through DHCP)

#### DNS Caching
- **DNS caching** is a critically important feature of the DNS system
- **DNS caching** is done in order to improve the delay performance and to reduce the number of DNS messages ricocheting around the Internet
- In a query chain, when a DNS server receives a DNS reply (containing, for example, a mapping from a hostname to an IP address), it can cache the mapping in its local memory.
- If you think about hash maps/Python dictionaries, that is what you would use to cache a DNS (it is far more efficient than a silly iterative approach)

### 2.4.3 DNS Records and Messages
- The DNS servers that together implement the DNS distributed database store **resource records (RRs)**
- Each DNS reply message carries one or more resource records
- A resource record is a four-tuple that contains the following fields:
	* `(Name, Value, Type, TTL)`
- TTL is the time to live of the resource record; it determines when a resource should be removed from a cache.
- The meaning of Name and Value depend on Type:
	* If `Type=A`, then Name is a hostname and Value is the IP address for the host- name. Thus, a Type A record provides the standard hostname-to-IP address mapping. As an example, (`relay1.bar.foo.com`, `145.37.93.126`, `A`) is a Type A record.
	* If `Type=NS`, then Name is a domain (such as `foo.com`) and Value is the host- name of an authoritative DNS server that knows how to obtain the IP addresses for hosts in the domain. This record is used to route DNS queries further along in the query chain. As an example, (`foo.com`, `dns.foo.com`, `NS`) is a Type NS record.
	* If `Type=CNAME`, then Value is a canonical hostname for the alias hostname `Name`. This record can provide querying hosts the canonical name for a hostname. As an example, (`foo.com`, `relay1.bar.foo.com`, `CNAME`) is a CNAME record
	* If `Type=MX`, then Value is the canonical name of a mail server that has an alias hostname Name. As an example, (`foo.com`, `mail.bar.foo.com`, `MX`) is an MX record. MX records allow the hostnames of mail servers to have simple aliases. Note that by using the MX record, a company can have the same aliased name for its mail server and for one of its other servers (such as its Web server). To obtain the canonical name for the mail server, a DNS client would query for an MX record; to obtain the canonical name for the other server, the DNS client would query for the CNAME record.

- If a DNS server is authoritative for a particular hostname, then the DNS server will contain a Type A record for the hostname.
- If a server is not authoritative for a hostname, then the server will contain a Type NS record for the domain that includes the hostname; it will also contain a Type A record that provides the IP address of the DNS server in the `Value` field of the NS record

- Suppose an edu TLD server is not authoritative for the host `gaia.cs.umass.edu`
- Then this server will contain a record for a domain that includes the host `gaia.cs.umass.edu`, for example, (`umass.edu`, `dns.umass.edu`, `NS`)
- The edu TLD server would also contain a Type A record, which maps the DNS server `dns.umass.edu` to an IP address, for example, (`dns.umass.edu`, `128.119.40.111`, `A`)

#### DNS Messages

- There are 2 different kinds of DNS messages.
	1. Queries
	2. Replies

- Semantics of a DNS message:
	* The first 12 bytes is the `header section`, which has a number of fields.
	* The first field is a 16-bit number that identifies the query
	* There are a number of flags in the flag field. A 1-bit query/reply flag indicates whether the message is a query (0) or a reply (1)
	* A 1-bit authoritative flag is set in a reply message when a DNS server is an authoritative server for a queried name
	* A 1-bit recursion-desired flag is set when a client (host or DNS server) desires that the DNS server perform recursion when it doesn't have the record
	* A 1-bit recursion-available field is set in a reply if the DNS server supports recursion
	* The `question section` contains information about the query that is being made.
	* This section includes (1) a name field that contains the name that is being queried, and (2) a type field that indicates the type of question being asked about the name
	* A reply can return multiple **RRs** in the answer, since a hostname can have multiple IP addresses
	* The `authority section` contains records of other authoritative servers.
	* The additional section contains other helpful records.
	* For example, the answer field in a reply to an MX query contains a resource record providing the canonical hostname of a mail server

**Q:** How would you like to send a DNS query message directly from the host you're working on to some DNS server?

**A:** This can easily be done with the **nslookup program**, which can be found on most Windows and UNIX platforms. 

#### Inserting Records into the DNS Database
- Suppose you have just created an exciting new startup company called Network Utopia.
- The first thing you'll surely want to do is register the domain name `networkutopia.com` at a registrar
- A **registrar** is a commercial entity that verifies the uniqueness of the domain name, entersthe domain name into the DNS database (as discussed below), and collects a small fee from you for its services
- Prior to 1999, a single registrar, Network Solutions, had a monopoly on domain name registration for `com`, `net`, and `org` domains
- Now there are many registrars competing for customers, and the Internet Corporation for Assigned Names and Numbers (ICANN) accredits the various registrars
- When you register the domain name `networkutopia.com` with some registrar, you also need to provide the registrar with the names and IP addresses of your primary and secondary authoritative DNS servers
- Suppose the names and IP addresses are `dns1.networkutopia.com`, `dns2.networkutopia.com`,`212.2.212.1`, and `212.212.212.2`
- For each of these two authoritative DNS servers, the registrar would then make sure that a Type NS and a Type A record are entered into the TLD com servers.
- Specifically, for the primary authoritative server for `networkutopia.com`, the registrar would insert the following two resource records into the DNS system

```
(networkutopia.com, dns1.networkutopia.com, NS)
(dns1.networkutopia.com, 212.212.212.1, A)
```

## 2.5 Peer-to-Peer File Distribution
- with a P2P architecture, there is minimal (or no) reliance on always-on infrastructure servers. You rely on the peers that are seeding.
- The peers are not owned by a service provider, but are instead PCs, laptops, and smartpones controlled by users.
- In P2P file distribution, each peer can redistribute any portion of the file it has received to any other peers, thereby assisting the server in the distribution process

#### Scalability of P2P Architectures
- Let the upload rate of the server's access link = `Us`
- Let the upload rate of the ith peer's access link = `Ui`
- Let the download rate of the ith peer's access link = `di`
- Let the size of the file to be distributed (in bits) = `F` 
- Let and the number of peers that want to obtain a copy of the file = `N`

- First, determine the distribution time for the client-server architecture, which we will denoted with `Dcs`
	* The server must transmit one copy of the file to each of the `N` peers. Thus, the server must transmit `NF` bits. Since the server's upload rate is `Us` , the time to distribute the file must be at least `NF/Us`
	* Let d min denote the download rate of the peer with the lowest download rate, that is, `d min = min{ d1, dp, ... , dN }`. The peer with the lowest download rate cannot obtain all `F` bits of the file in less than `F/dmin` seconds. Thus, the minimum distribution time is at least `F/dmin`
- Combining these two observations together, we get:
	* `Dcs >= max { (NF)/Us , F/dmin }`

Now, let's analyze the P2P architecture, where each peer can assist the server in distributing the file.
	* At the beginning of the distribution, only the server has the file. To get this file into the community of peers, the server must send each bit of the file at least once into its access link
	* Thus, the minimum distribution time is at least `F/Us`.
	* As with the client-server architecture, the peer with the lowest download rate cannot obtain all `F` bits of the file in less than `F/dmin` seconds. Thus, the minimum distribution time is at least `F/dmin`
	* Finally, observe that the total upload capacity of the system as a whole is equal
to the upload rate of the server plus the upload rates of each of the individual
peers, that is, `Utotal = Us + U1 + ... + uN` . The system must deliver (upload) `F` bits to each of the `N` peers, thus delivering a total of `NF` bits. This cannot be done at a rate faster than `Utotal` . Thus, the minimum distribution time is also at least `NF/(u s + u 1 + g + u N )`.
- Combining these two observations together, we get:
	* `Dp2p >= max { F/Us , F/dmin, (NF)/(Us + sum(1, N, Ui))`


#### BitTorrent

- BitTorrent is a popular P2P protocol for file distribution
- The collection of all peers participating in the distribution of a particular file is called a torrent
- Peers in a torrent download equal-size chunks of the file from one another, with a typical chunk size of 256 KBytes
- When a peer first joins a torrent, it has no chunks. 
- Over time it accumulates more and more chunks. While it downloads chunks it also uploads chunks to other peers.
- Once a peer has acquired the entire file, it may (selfishly) leave the torrent, or (altruistically) remain in the torrent and continue to upload chunks to other peers
- Also, any peer may leave the torrent at any time with only a subset of chunks, and later rejoin the torrent.
- Alice uses a technique called **rarest first**. The idea is to determine, from among the chunks she does not have, the chunks that are the rarest among her neighbors (that is, the chunks that have the fewest repeated copies among her neighbors) and then request those rarest chunks first.
- Seeders that supply high upload rates to leechers are said to be **unchoked**.
- A distributed hash table (DHT) is a simple database,
with the database records being distributed over the peers in a P2P system

## 2.6 Video Streaming and Content Distribution Networks
- By many estimates, streaming video--including Netflix, YouTube and Amazon Prime--account for about 80% of Internet traffic in 2020.

### 2.6.1 Internet Video
- From a networking perspective, perhaps the most salient characteristic of video is its high bit rate.
- Compressed Internet video typically ranges from 100 kbps for low-quality video to over 4 Mbps for streaming high-definition movies
- 4K streaming envisions a bitrate of more than 10 Mbp
- We can also use compression to create multiple versions of the same video, each at a different quality level. This is what YouTube does (and pretty much all other streaming services)

### 2.6.2 HTTP Streaming and DASH
- In HTTP streaming, the video is simply stored at an HTTP server as an ordinary file with a specific URL
- When a user wants to see the video, the client establishes a TCP connection with the server and issues an HTTP GET request for that URL
- The server then sends the video file, within an HTTP response message, as quickly as the underlying network protocols and traffic conditions will allow
- On the client side, the bytes are collected in a client application buffer
- **Dynamic Adaptive Streaming over HTTP (DASH)** is a HTTP-based streaming protocol.
- In DASH, the video is encoded into several different versions, with each version having a different bit rate and, correspondingly, a different quality level
- The HTTP server also has a **manifest file**, which provides a URL for each version along with its bit rate

### 2.6.3 Content Distribution Networks
- In order to meet the challenge of distributing massive amounts of video data to users distributed around the world, almost all major video-streaming companies make use of Content Distribution Networks (CDNs)
- A CDN manages servers in multiple geographically distributed locations, stores copies of the videos (and other types of Web content, including documents, images, and audio) in its servers, and attempts to direct each user request to a CDN location that will provide the best user experience
- The CDN may be a **private CDN**, a.k.a, owned by the content provider itself
- The CDN may alternatively be a **third-party** CDN that distributes content on behalf of multiple content providers

- CDNs typically adopt one of two different server placement philosophies:
	1. **Enter Deep**. One philosophy, pioneered by Akamai, is to enter deep into the access networks of Internet Service Providers, by deploying server clusters in access ISPs all over the world. Akamai takes this approach with clusters in thousands of locations. The goal is to get close to end users, thereby improving user-perceived delay and throughput by decreasing the number of links and routers between the end user and the CDN
server from which it receives content
	2. **Bring Home**. A second design philosophy, taken by Limelight and many other CDN companies, is to bring the ISPs home by building large clusters at a smaller number (for example, tens) of sites. Instead of getting inside the access ISPs, these CDNs typically place their clusters in Internet Exchange Points (IXPs). Compared with the enter-deep design philosophy, the bring-home design typically results in lower maintenance and management overhead, possibly at the expense of higher delay and lower throughput to end users

- Once its clusters are in place, the CDN replicates content across its clusters

#### CDN Operation
- When a browser in a user's host is instructed to retrieve a specific video (identified by a URL), the CDN must intercept the request so that it can:
	1. determine a suitable CDN server cluster for that client at that time
	2. redirect the client's request to a server in that cluster

- Example: 
	1. The user visits the Web page at NetCinema.
	2. When the user clicks on the link `http://video.netcinema.com/6Y7B23V`, the user's host sends a DNS query for `video.netcinema.com`.
	3. The user's Local DNS Server (LDNS) relays the DNS query to an authoritative DNS server for NetCinema, which observes the string "video" in the host- name video.netcinema.com. To “hand over" the DNS query to KingCDN, instead of returning an IP address, the NetCinema authoritative DNS server returns to the LDNS a hostname in the KingCDN's domain, for example, `a1105.kingcdn.com`.
	4. From this point on, the DNS query enters into KingCDN's private DNS infrastructure. The user's LDNS then sends a second query, now for `a1105.kingcdn.com`, and KingCDN's DNS system eventually returns the IP addresses of a KingCDN content server to the LDNS. It is thus here, within the KingCDN's DNS system, that the CDN server from which the client will receive its content is specified.
	5. The LDNS forwards the IP address of the content-serving CDN node to the user's host.
	6. Once the client receives the IP address for a KingCDN content server, it establishes a direct TCP connection with the server at that IP address and issues an HTTP GET request for the video. If DASH is used, the server will first send to the client a manifest file with a list of URLs, one for each version of the video, and the client will dynamically select chunks from the different versions.

- At the core of any CDN deployment is a **cluster selection strategy**, that is, a mechanism for dynamically directing clients to a server cluster or a data center within the CDN
- The CDN learns the IP address of the client's LDNS server via the client's DNS lookup. After learning this IP address, the CDN needs to select an appropriate cluster based on this IP address.
- CDNs generally employ proprietary cluster selection strategies.
- One simple strategy is to assign the client to the cluster that is **geographically closest**.
- In order to determine the best cluster for a client based on the current traffic conditions, CDNs can instead perform periodic **real-time measurements** of delay and loss performance between their clusters and clients

### 2.6.4 Case Studies: Netflix and YouTube

#### Netflix
- As of 2020, Netflix is the leading service provider for online movies and TV series in North America. 
- As we discuss below, Netflix video distribution has two major components: 
	* The Amazon cloud 
	* Its own private CDN infrastructure.
- Additionally, the Amazon cloud handles the following critical functions:
	* **Content ingestion**. Before Netflix can distribute a movie to its customers, it mustfirst ingest and process the movie. Netflix receives studio master versions of movies and uploads them to hosts in the Amazon cloud.
	* **Content processing**. The machines in the Amazon cloud create many different formats for each movie, suitable for a diverse array of client video players running on desktop computers, smartphones, and game consoles connected to televisions. A different version is created for each of these formats and at multiple bit rates, allowing for adaptive streaming over HTTP using DASH.
	* **Uploading versions to its CDN**. Once all of the versions of a movie have been created, the hosts in the Amazon cloud upload the versions to its CDN.
	* Once Netflix determines the CDN server that is to deliver the content, it sends the client the IP address of the specific server as well as a manifest file, which has the URLs for the different versions of the requested movie
	* The client and that CDN server then directly interact using a proprietary version of DASH
	
#### YouTube
- Similar to Netflix, Google uses its own private CDN to distribute YouTube videos, and has installed server clusters in many hundreds of different IXP and ISP locations
- From these locations and directly from its huge data centers, Google distributes YouTube videos
- Unlike Netflix, however, Google uses pull caching, as described, and DNS redirect.

## 2.7 Socket Programming: Creating Network Applications
- There are two types of network applications:
	1. One type is an implementation whose operation is specified in a protocol standard, such as an RFC or some other standards document; such an application is sometimes referred to as “open," since the rules specifying its operation are known to all. For such an implementation, the client and server programs must conform to the rules dictated by the RFC.
	2. The other type of network application is a proprietary network application. In this case, the client and server programs employ an application-layer protocol that has not been openly published in an RFC or elsewhere. A single developer (or development team) creates both the client and server programs, and the developer has complete control over what goes in the code. But because the code does not implement an open protocol, other independent developers will not be able to develop code that interoperates with the application.

- Recall from the previous chapters that:
	* TCP is connection oriented and provides a reliable byte-stream channel through which data flows between two end systems
	* UDP is connectionless and sends independent packets of data from one end system to the other, without any guarantees about delivery
	* Recall also that when a client or server program implements a protocol defined by an RFC, it should use the well-known port number associated with the protocol; conversely, when developing a proprietary application, the developer must be careful to avoid using such well-known port numbers

### 2.7.1 Socket Programming with UDP

**Q:** What goes into the destination address that is attached to the packet?

**A:** The destination host's IP address is part of the destination address. By including the destination IP address in the packet, the routers in the Internet will be able to route the packet through the Internet to the destination host. But because a host may be running many network application processes, each with one or more sockets, it is also necessary to identify the particular socket in the destination host, i.e., the **port number** is assigned to it. The packet's destination address also includes the socket's port number.

- In summary, the sending process attaches to the packet a destination address, which consists of the destination host's IP address and the destination socket's port number.

**Below is the TCP/UDP sending/receiving messages lab that we did in Python.**

```
1. The client reads a line of characters (data) from its keyboard and sends the data to the server.
2. The server receives the data and converts the characters to uppercase.
3. The server sends the modified data to the client.
4. The client receives the modified data and displays the line on its screen.
```

### 2.7.2 Socket Programming with TCP
- Unlike UDP, TCP is a connection-oriented protocol. 
- This means that before the client and server can start to send data to each other, they first need to handshake and establish a TCP connection
- One end of the TCP connection is attached to the client
socket and the other end is attached to a server socket
-  When creating the TCP connection, we associate it with the client socket address (IP address and port number) and the server socket address (IP address and port number)
- With the TCP connection established, when one side wants to send data to the other side, it just drops the data into the TCP connection via its socket. 
- This is different from UDP, for which the server must attach a destination address to the packet before dropping it into the socket.

- In TCP, the client has the job of initiating contact with the server. In order for the server to be able to react to the client's initial contact, the server has to be ready
- This implies two things:
	1. First, as in the case of UDP, the TCP server must be running as a process before the client attempts to initiate contact.
	2. Second, the server program must have a special door--more precisely, a special socket--that welcomes some initial contact from a client process running on an arbitrary host.

- With the server process running, the client process can initiate a TCP connection to the server. This is done in the client program by creating a TCP socket.
- When the client creates its TCP socket, it specifies the address of the welcoming socket in the server, namely, the IP address of the server host and the port number of the socket.
- After creating its socket, the client initiates a three-way handshake and establishes a
TCP connection with the server.
- The three-way handshake, which takes place within the transport layer, is completely invisible to the client and server programs
- During the three-way handshake, the client process knocks on the welcoming door of the server process.
- When the server "hears" the knocking, it creates a new door/socket dedicated to that client.

# Chapter 3 - Transport Layer 

## 3.1 Introduction and Transport-Layer Services
- A transport-layer protocol provides for **logical communication** between application processes running on different hosts
- Transport-layer protocols are implemented in the end systems but not in network routers
- On the sending side, the transport layer converts the application-layer messages it receives from a sending application process into transport-layer packets, known as transport-layer **segments** in Internet terminology.

### 3.1.1 Relationship Between Transport and Network Layers
- Transport layer lies just above the network layer in the protocol stack
- Whereas a transport-layer protocol provides logical communication between processes running on different hosts, a network-layer protocol provides logical-communication between hosts
- This distinction is subtle but important
- The services that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol
- If the network-layer protocol cannot provide delay or bandwidth guarantees for transport-layer segments sent between hosts, then the transport-layer protocol cannot provide delay or bandwidth guarantees for application messages sent between processes.
- A transport protocol can offer reliable data transfer service to an application even when the underlying network protocol is unreliable, that is, even when the network protocol loses, garbles, or duplicates packets
- A transport protocol can use encryption to guarantee that application messages are not read by intruders, even when the network layer cannot guarantee the confidentiality of transport-layer segments


### 3.1.2 Overview of the Transport Layer in the Internet
- Transport-layer protocols:
	1. **UDP** (User Datagram Protocol), which provides an unreliable, connectionless service to the invoking application.
	2. **TCP** (Transmission Control Protocol), which provides a reliable, connection-oriented service to the invoking application.

- When designing a network application, the application developer must specify one of these two transport protocols.

- The Internet's network-layer protocol has a name... **IP**, for Internet Protocol
- **IP** provides logical communication between hosts.
- The IP service model is a **best-effort delivery service**.
- This means that IP makes its "best effort" to deliver segments between communicating hosts, but it makes no guarantees.
- This is why **IP** is considered to be an **unreliable service**
- Extending host-to-host delivery to process-to-process delivery is called **transport-layer multiplexing** and **demultiplexing**.
- In particular, like IP, UDP is an **unreliable service**--it does not guarantee that data sent by one process will arrive intact (or at all!) to the destination process.
- TCP, on the other hand, offers several additional services to applications. First and foremost, it provides **reliable data transfer**.
- TCP thus converts IP's unreliable service between end systems into a reliable data transport service between processes
- TCP also provides **congestion control**.
- TCP congestion control prevents any one TCP connection from swamping the links and routers between communicating hosts with an excessive amount of traffic. 
- TCP strives to give each connection traversing a congested link an equal share of the link bandwidth. This is done by regulating the rate at which the sending sides of TCP connections can send traffic into the network.
- UDP traffic, on the other hand, is unregulated. An application using UDP transport can send at any rate it pleases, for as long as it pleases.

## 3.2 Multiplexing and Demultiplexing
- A process (as part of a network application) can have one or more **sockets**, i.e., where the data passes from the process to the network
- Each transport-layer segment has a set of fields in the segment for this purpose.
- At the receiving end, the transport layer examines these fields to identify the receiving socket and then directs the segment to that socket.
- This job of delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**
- The job of gathering data chunks at the source host from different sockets, encapsulating each data chunk with header information (that will later be used in demultiplexing) to create segments, and passing the segments to the network layer is called **multiplexing**.

- Analogy:

	* To illustrate the demultiplexing job, imagine a bunch of kids in a household. Each of them are identified by their names. 
	* When Bill receives a batch of mail from the carrier, he performs a **demultiplexing** operation by observing whom the letters are addressed to and then hand delivering the mail to his brothers and sisters.
	* Ann performs a **multiplexing** operation when she collects letters from her brothers and sisters and gives the collected mail to the mail person.

- Transport-layer multiplexing requires: 
	1. that sockets have unique identifiers
	2. that each segment have special fields that indicate the socket to which the segment is to be delivered.

- These special fields, are the **source port number field** and the **destination port number field**.
- Each port number is a 16-bit number, ranging from 0 to 65535.
- The port numbers ranging from 0 to 1023 are called well-known port numbers and are restricted, which means that they are reserved for use by well-known application protocols such as HTTP (which uses port number 80) and FTP (which uses port number 21)
- Transport layer **could** implement the demultiplexing service: Each socket in the host could be assigned a port number, and when a segment arrives at the host, the transport layer examines the destination port number in the segment and directs the segment to the corresponding socket. The segment's data then passes through the socket into the attached process. As we'll see, this is basically how UDP does it. However, we'll also see that multiplexing/demultiplexing in TCP is yet more subtle.

#### Connectionless Multiplexing and Demultiplexing

- Suppose a process in Host A, with UDP port 19157, wants to send a chunk of application data to a process with UDP port 46428 in Host B.
- The transport layer in Host A creates a transport-layer segment that includes the application data, the source port number (19157), the destination port number (46428), and two other values (which aren't important in this context)
- The transport layer then passes the resulting segment to the network layer.
- The network layer encapsulates the segment in an IP datagram and makes a best-effort attempt to deliver the segment to the receiving host.
- If the segment arrives at the receiving Host B, the transport layer at the receiving host examines the destination port number in the segment (46428) and delivers the segment to its socket identified by port 46428.
- Note that Host B could be running multiple processes, each with its own UDP socket and associated port number. As UDP segments arrive from the network, Host B directs (demultiplexes) each segment to the appropriate socket by examining the segment's destination port number.
- It is important to note that a UDP socket is fully identified by a two-tuple consisting of a destination IP address and a destination port number.
- As a consequence, if two UDP segments have different source IP addresses and/or source port numbers, but have the same destination IP address and destination port number, then the two segments will be directed to the same destination process via the same destination socket.

**Q:** So what is the purpose of the source port number?

**A:** In the A-to-B segment the source port number serves as part of a “return address" (you can also think of our mail analogy from earlier. The return address is always written on the letter before its sent out. When B wants to send a segment back to A, the destination port in the B-to-A segment will take its value from the source port value of the A-to-B segment


#### Connection-Oriented Multiplexing and Demultiplexing

- One subtle difference between a TCP socket and a UDP socket is that a TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).
- Thus, when a TCP segment arrives from the network to a host, the host uses all four values to direct (demultiplex) the segment to the appropriate socket.
- In particular, and in contrast with UDP, two arriving TCP segments with different source IP addresses or source port numbers will (with the exception of a TCP segment carrying the original connection-establishment request) be directed to two different sockets.

* The TCP server application has a "welcoming socket", that waits for connection-
establishment requests from TCP clients (see Figure 2.29) on port number 12000.
* The TCP client creates a socket and sends a connection establishment request
segment with the lines:
```
clientSocket = socket(AF_INET, SOCK_STREAM)
clientSocket.connect((serverName,12000))
```
* A connection-establishment request is nothing more than a TCP segment with destination port number 12000 and a special connection-establishment bit set in the TCP header. The segment also includes a source port number that was chosen by the client.
* When the host operating system of the computer running the server process receives the incoming connection-request segment with destination port 12000, it locates the server process that is waiting to accept a connection on port number 12000. The server process then creates a new socket:
```
connectionSocket, addr = serverSocket.accept()
```

- Also, the transport layer at the server notes the following four values in the connection-request segment: 
	1. the source port number in the segment, 
	2. the IP address of the source host, 
	3. the destination port number in the segment, and 
	4. its own IP address. 
- The newly created connection socket is identified by these four values; all subsequently arriving segments whose source port, source IP address, destination port, and destination IP address match these four values will be demultiplexed to this socket. With the TCP connection now in place, the client and server can now send data to each other.

- The server host may support many simultaneous TCP connection sockets, with each socket attached to a process, and with each socket identified by its own four-tuple. When a TCP segment arrives at the host, all four fields (source IP address, source port, destination IP address, destination port) are used to direct (demultiplex) the segment to the appropriate socket.

#### Web Servers and TCP
- Consider a host running a Web server, such as an Apache Web server, on port 80.
- When clients (for example, browsers) send segments to the server, all segments will have destination port 80.
- In particular, both the initial connection-establishment segments and the segments carrying HTTP request messages will have destination port 80
- The server distinguishes the segments from the different clients using source IP addresses and source port numbers.
- If the client and server are using persistent HTTP, then throughout the duration of the persistent connection the client and server exchange HTTP messages via the same server socket.
- However, if the client and server use non-persistent HTTP, then a new TCP connection is created and closed for every request/response, and hence a new socket is created and later closed for every request/response.
- This frequent creating and closing of sockets can severely impact the performance of a busy Web server


## 3.3 Connectionless Transport: UDP
- UDP, defined in [RFC 768], does just about as little as a transport protocol can do. Aside from the multiplexing/demultiplexing function and some light error checking, it adds nothing to IP.
- In fact, if the application developer chooses UDP instead of TCP, then the application is almost directly talking with IP. 
- UDP takes messages from the application process, attaches source and destination port number fields for the multiplexing/demultiplexing service, adds two other small fields, and passes the resulting segment to the network layer.
- The network layer encapsulates the transport-layer segment into an IP datagram and then makes a best-effort attempt to deliver the segment to the receiving host. If the segment arrives at the receiving host, UDP uses the destination port number to deliver the segment's data to the correct application process. Note that with UDP there is no handshaking between sending and receiving transport-layer entities before sending a segment. For this reason, UDP is said to be **connectionless**.
- DNS is an example of an application-layer protocol that typically uses UDP. When the DNS application in a host wants to make a query, it constructs a DNS query message and passes the message to UDP.
- The network layer encapsulates the UDP segment into a datagram and sends the datagram to a name server.
- If it doesn't receive a reply (possibly because the underlying network lost the query or the reply), it might try resending the query, try sending the query to another name server, or inform the invoking application that it can't get a reply.

**Q:** Why would an application developer would ever choose to build an application over UDP rather than over TCP? Isn't TCP always better?

**A:** In the context of gaming, streaming videos, streaming music, etc, UDP is preferred. This is because the loss of data is not nearly as much of a concern in these contexts, so a bit of **unreliable data transfer** is alright. Now, if we were discussing the matter of uploading and downloading files, this is different. When transferring most file types, you absolutely do not want to lose any bits during the process. This will more than likely corrupt a file, or modify it so much that it does not resemble the original file. UDP is also faster than TCP. UDP sacrificies reliability for speed, and when streaming anything or playing games, speed is what matters the most.

### 3.3.1 UDP Segment Structure
- The application data occupies the data field of the UDP segment
- For DNS, the data field contains either a query message or a response message.
- The UDP header has only four fields, each consisting of two bytes.
- As discussed in the previous section, the port numbers allow the destination host to pass the application data to the correct process running on the destination end system (that is, to perform the demultiplexing function).

### 3.3.2 UDP Checksum
- The **UDP checksum** provides for error detection. 
- That is, the checksum is used to determine whether bits within the UDP segment have been altered (for example, by noise in the links or while stored in a router) as it moved from source to destination
- You may wonder why UDP provides a checksum in the first place, as many link-layer protocols (including the popular Ethernet protocol) also provide error checking.
- The reason is that there is no guarantee that all the links between source and destination provide error checking; that is, one of the links may use a link-layer protocol that does not provide error checking.
- Furthermore, even if segments are correctly transferred across a link, it's possible that bit errors could be introduced when a segment is stored in a router's memory.
- Given that neither link-by-link reliability nor in-memory error detection is guaranteed, UDP must provide error detection at the transport layer, on an end-end basis, if the end-end data transfer service is to provide error detection. This is an example of the celebrated end-end principle in system design [Saltzer 1984], which states that since certain functionality (error detection, in this case) must be implemented on an end-end basis: "functions placed at the lower levels may be redundant or of little value when compared to the cost of providing them at the higher level."
- Although UDP provides error checking, it does not do anything to recover from an error.
- Some implementations of UDP simply discard the damaged segment; others pass the damaged segment to the application with a warning.


## 3.4 Principles of Reliable Data Transfer
-  Implementing reliable data transfer occurs not only at the **transport layer**, but also at the **link layer** and the **application layer** as well.
- It is the responsibility of a **reliable data transfer protocol** to implement this
service abstraction.
- TCP is a **reliable data transfer protocol** that is implemented on top of an unreliable (IP) end-to-end network layer. 
- This task is made difficult by the fact that the layer below the reliable data transfer protocol may be unreliable
- TCP is a reliable data transfer protocol that is implemented on top of an unreliable (IP) end-to-end network layer. 
- **unidirectional data transfer** - data transfer from the sending to the receiving side
- **bidirectional data transfer** - (or, full-duplex) data transfer bidirectional basically means it can both send and receieve data

## 3.4.1 Building a Reliable Data Transfer Protocol
-  In a computer network setting, reliable data transfer protocols based on such retransmission are known as **ARQ (Automatic Repeat reQuest)** protocols.
-  Fundamentally, three additional protocol capabilities are required in **ARQ protocols** to handle the presence of bit errors
	* **Error detection** - First, a mechanism is needed to allow the receiver to detect when bit errors have occurred.
	* **Receiver feedback** - Since the sender and receiver are typically executing on different end systems, possibly separated by thousands of miles, the only way for the sender to learn of the receiver’s view of the world (in this case, whether or not a packet was received correctly) is for the receiver to provide explicit feedback to the sender
	* **Retransmission** - A packet that is received in error at the receiver will be retransmitted by the sender.
- ACK - Positive acknowledgement
- NAK - Negative acknowledgement
- **rdt2.0** is a data transfer protocol employing error detection, positive acknowledgments, and negative acknowledgments.
- The send side of **rdt2.0** has two states. In the leftmost state, the send-side
protocol is waiting for data to be passed down from the upper layer.	
- If a **NAK** is received, the protocol retransmits the last packet and waits for an **ACK** or **NAK** to be returned by the receiver in response to the retransmitted data packet
-  It is important to note that when the sender is in the wait-for-ACK-or-NAK state, it cannot get more data from the upper layer; that is, the **rdt_send()** event can not occur; that will happen only after the sender receives an ACK and leaves this state. 
-  Thus, the sender will not send a new piece of data until it is sure that the receiver has correctly received the current packet. Because of this behavior, protocols such as **rdt2.0** are known as **stop-and-wait protocols**.
- Consider three possibilities for handling corrupted ACKs or NAKs:
  * First possibility - If the message is corrupted, **a request can be made for the same message again**, as if you were asking "can you repeat that?"
  * A second alternative is to **add enough checksum bits** to allow the sender not only
to detect, but also to recover from, bit errors. This solves the immediate problem for a channel that can corrupt packets but not lose them.
  * A third approach is to simply resend a data packet when it receieves a garbled ACK or NAK packet. However, this approach introduces **duplicate packets**. The fundamental difficulty with duplicate packets is that the receiver doesn’t know whether the ACK or NAK it last sent was received correctly at the sender. Thus, it cannot know a priori whether an arriving packet contains new data or is a retransmission
- A simple solution to this new problem (and one adopted in almost all existing data transfer protocols, including TCP) is to add a new field to the data packet and have the sender number its data packets by putting a **sequence number** into this field. 
-  Note that if a packet experiences a particularly large delay, the sender may retrans mit the packet even though neither the data packet nor its ACK have been lost. This introduces the possibility of **duplicate data packets** in the sender-to-receiver channel.
-  Implementing a time-based retransmission mechanism requires a **countdown timer** that can interrupt the sender after a given amount of time has expired
-  The sender will thus need to be able to: 
    1. start the timer each time a packet (either a first-time packet or
a retransmission) is sent 
    2. respond to a timer interrupt (taking appropriate actions),
and 
    3. stop the timer.
-  Because packet sequence numbers alternate between 0 and 1, protocol **rdt3.0** is sometimes known as the **alternating-bit protocol**.

## 3.4.2 Pipelined Reliable Data Transfer Protocols
- Protocol rdt3.0 is a functionally correct protocol. However, rdt3.0 is a **stop-and-wait protocol** which is the root cause of its poor performance.
- **utilization** of the sender - the fraction of time the sender is actually busy sending bits into the channel
- Rather than operate in a stop-and-wait manner, the sender is allowed to send multiple packets without waiting for acknowledgments. If the sender is allowed to transmit three packets before having to wait for acknowledgments, the utilization of the sender is essentially tripled. Since the many in-transit sender-to-receiver packets can be visualized as filling a pipeline, this technique is known as **pipelining**.
- Pipelining has the following consequences for reliable data transfer protocols:
	* The range of sequence numbers must be increased, since each in-transit packet (not counting retransmissions) must have a unique sequence number and there may be multiple, in-transit, unacknowledged packets.
	* The sender and receiver sides of the protocols may have to buffer more than one packet. Minimally, the sender will have to buffer packets that have been transmitted but not yet acknowledged. Buffering of correctly received packets may also be needed at the receiver, as discussed below.
	* The range of sequence numbers needed and the buffering requirements will depend on the manner in which a data transfer protocol responds to lost, corrupted, and overly delayed packets. Two basic approaches toward pipelined error recovery can be identified: **Go-Back-N** and **selective repeat**.

## 3.4.3 Go-Back-N (GBN)
- In a **Go-Back-N (GBN) protocol**, the sender is allowed to transmit multiple packets (when available) without waiting for an acknowledgment, but is constrained to have no more than some maximum allowable number, N, of unacknowledged packets in the pipeline.
- The range of permissible sequence numbers for transmitted but not yet acknowledged packets can be viewed as a window of size N over the range of sequence numbers. As the protocol operates, this window slides forward over the sequence number space. For this reason, N is often referred to as the **window size** and the GBN protocol itself as a **sliding-window protocol**. 
- In practice, a packet’s sequence number is carried in a fixed-length field in the **packet header**
- The GBN sender must respond to three types of events:
    * **Invocation from above** - When *rdt_send()* is called from above, the sender
first checks to see if the window is full, that is, whether there are N outstand-
ing, unacknowledged packets. If the window is not full, a packet is created and
sent, and variables are appropriately updated. If the window is full, the sender
simply returns the data back to the upper layer, an implicit indication that the
window is full. The upper layer would presumably then have to try again later.
   * **Receipt of an ACK** - In our GBN protocol, an acknowledgment for a packet with sequence number n will be taken to be a **cumulative acknowledgment**, indicating that all packets with a sequence number up to and including n have been correctly received at the receiver. We’ll come back to this issue shortly when we examine the receiver side of GBN.
   * A timeout event. The protocol’s name, “Go-Back-N,” is derived from the sender’s behavior in the presence of lost or overly delayed packets. As in the stop-and-wait protocol, a timer will again be used to recover from lost data or acknowledgment packets. If a timeout occurs, the sender resends all packets that have been previously sent but that have not yet been acknowledged. If an ACK is received but there are still additional transmitted but not yet acknowledged packets, the timer is restarted. If there are no outstanding, unacknowledged packets, the timer is stopped.
- In **event-based programming**, the various procedures are called (invoked) either by other procedures in the protocol stack, or as the result of an interrupt. In the sender, these events would be: 
  1. a call from the upper-layer entity to invoke *rdt_send()* 
  2. a timer interrupt 
  3. a call from the lower layer to invoke *rdt_rcv()* when a packet arrives.

## 3.4.4 Selective Repeat (SR)
  - **Selective-repeat protocols** avoid unnecessary retransmissions by having the sender retransmit only those packets that it suspects were received in error (that is, were lost or corrupted) at the receiver.
  - This individual, as-needed, retransmission will require that the receiver *individually* acknowledge correctly received packets
  - However, unlike GBN, the sender will have already received ACKs for some of the packets in the window.
  - The SR receiver will acknowledge a correctly received packet whether or not it is in order. Out-of-order packets are buffered until any missing packets (that is, packets with lower sequence numbers) are received, at which point a batch of packets can be delivered in order to the upper layer.


### Selective-repeat (SR) sender and receiver views
of sequence-number space
1. Data received from above. When data is received from above, the SR sender checks the next available sequence number for the packet. If the sequence number is within the sender’s window, the data is packetized and sent; otherwise it is either buffered or returned to the upper layer for later transmission, as in GBN.
2. Timeout. Timers are again used to protect against lost packets. However, each packet must now have its own logical timer, since only a single packet will be transmitted on timeout. A single hardware timer can be used to mimic the operation of multiple logical timers [Varghese 1997].
3. ACK received. If an ACK is received, the SR sender marks that packet as having been received, provided it is in the window. If the packet’s sequence number is equal to *send_base*, the window base is moved forward to the unacknowledged packet with the smallest sequence number. If the window moves and there are untransmitted packets with sequence numbers that now fall within the window, these packets are transmitted.

### Figure 3.24 - SR sender events and actions
1. Packet with sequence number in *[rcv_base, rcv_base+N-1]* is correctly received. /n this case, the received packet falls within the receiver’s window and a selective ACK packet is returned to the sender. If the packet was not previously received, it is buffered. If this packet has a sequence number equal to the base of the receive window (*rcv_base* in Figure 3.22), then this packet, and any previously buffered and consecutively numbered (beginning with *rcv_base*) packets are delivered to the upper layer. The receive window is then moved forward by the number of packets delivered to the upper layer. As an example, consider Figure 3.26. When a packet with a sequence number of *rcv_base*=2 is received, it and packets 3, 4, and 5 can be delivered to the upper layer.
2. Packet with sequence number in *[rcv_base-N, rcv_base-1]* is correctly received. In this case, an ACK must be generated, even though this is a packet that the receiver has previously acknowledged.
3. Otherwise. Ignore the packet.
 
* **Mechanism** - Use, Comments
* **Checksum** -  Used to detect bit errors in a transmitted packet. Timer Used to timeout/retransmit a packet, possibly because the packet (or its ACK) was lost within the channel. Because timeouts can occur when a packet is delayed but not lost (premature timeout), or when a packet has been received by the receiver but the receiver-to-sender ACK has been lost, duplicate copies of a packet may be received by a receiver.
* **Sequence number** -  Used for sequential numbering of packets of data flowing from sender to receiver. Gaps in the sequence numbers of received packets allow the receiver to detect a lost packet. Packets with duplicate sequence numbers allow the receiver to detect duplicate copies of a packet.

* **Acknowledgment (ACK)** - Used by the receiver to tell the sender that a packet or set of packets has been received correctly. Acknowledgments will typically carry the sequence number of the packet or packets being acknowledged. Acknowledgments may be individual
or cumulative, depending on the protocol.
* **Negative acknowledgment (NAK)** - Used by the receiver to tell the sender that a packet has not been received correctly. Negative acknowledgments will typically carry the sequence number of the packet that was not received correctly.
* **Window, pipelining** -  The sender may be restricted to sending only packets with sequence numbers that fall within a given range. By allowing multiple packets to be transmitted but not yet acknowledged, sender utilization can be increased over a stop-and-wait mode
of operation. 
## 3.5 Connection-Oriented Transport: TCP 

### 3.5.1 The TCP Connection

* TCP - the Internet’s transport-layer, connection-oriented, **reliable transport protocol.**
* **TCP** is said to be **connection-oriented** because before one application process can begin to send data to another, the two processes must first “handshake” with each other—that is, they must send some preliminary segments to each other to establish the parameters of the ensuing data transfer.
* As part of TCP connection establishment, both sides of the connection will initialize many TCP state variable associated with the TCP connection.
* Because the TCP protocol runs only in the end systems and not in the intermediate network elements (routers and link-layer switches), the intermediate network elements do not maintain TCP connection state.
* A TCP connection provides a **full-duplex service**: If there is a TCP connection between Process A on one host and Process B on another host, then application-layer data can flow from Process A to Process B at the same time as application-layer data flows from Process B to Process A.
* A TCP connection is also always **point-to-point**, that is, between a single sender and a single receiver.
* So-called **multicasting** - the transfer of data from one sender to many receivers in a single send operation—is not possible with TCP. With TCP, two hosts are company and three are a crowd
* The process that is initiating the connection is called the **client process**, while the other process is called the **server process**.
* The client application process first informs the client transport layer that it wants to establish a connection to a process in the server.
* The client first sends a special TCP segment; the server responds with a second special TCP segment; and finally the client responds again with a third special segment.
* The first two segments carry no payload, that is, no application-layer data; the third of these segments may carry a payload.
* Because three segments are sent between the two hosts, this connection-establishment procedure is often referred to as a **three-way handshake**.
* Once a TCP connection is established, the two application processes can send data to each other.
* The client process passes a stream of data through the socket (the door of the process)
* Once the data passes through the door, the data is in the hands of TCP running in the client.
* TCP directs this data to the connection’s **send buffer**, which is one of the buffers that is set aside during the initial **three-way handshake**.
* From time to time, TCP will grab chunks of data from the send buffer and pass the data to the network layer.
* The maximum amount of data that can be grabbed and placed in a segment is limited by the **maximum segment size (MSS)**
* The **MSS** is typically set by first determining the length of the largest link-layer frame that can be sent by the local sending host (a.k.a. **maximum transmission unit (MTU)**), and then setting the MSS to ensure that a TCP segment (when encapsulated in an IP datagram) plus the TCP/IP header length (typically 40 bytes) will fit into a single link-layer frame.
* The **MSS** is the maximum amount of application-layer data in the segment, not the maximum size of the TCP segment including headers.
* TCP pairs each chunk of client data with a TCP header, thereby forming **TCP segments**.
* The segments are passed down to the network layer, where they are separately encapsulated within network-layer IP datagrams.
* The IP datagrams are then sent into the network. When TCP receives a segment at the other end, the segment’s data is placed in the TCP connection’s receive buffer.

### 3.5.2 TCP Segment Structure
* The **TCP segment** consists of **header fields** and a **data field**. The data field contains a chunk of application data.
* The MSS limits the maximum size of a segment’s data field. When TCP sends a large file, such as an image as part of a Web page, it typically breaks the file into chunks of size MSS (except for the last chunk, which will often be less than the MSS).
* Interactive applications, however, often transmit data chunks that are smaller than the MSS; for example, with remote login applications such as Telnet and ssh, the data field in the TCP segment is often only one byte.
* As with UDP, the header includes **source and destination port numbers**, which are used for multiplexing/demultiplexing data from/to upper-layer applications.
* Also, as with UDP, the header includes a **checksum field**.
* A TCP segment header also contains the following fields:
	- The 32-bit **sequence number field** and the 32-bit **acknowledgment number field** are used by the TCP sender and receiver in implementing a reliable data transfer service
	- The 16-bit **receive window** field is used for flow control. It is used to indicate the number of bytes that a receiver is willing to accept.
	- The 4-bit **header length field** specifies the length of the TCP header in 32-bit words. The TCP header can be of variable length due to the TCP options field (which is typically empty).
	- The optional and variable-length **options field** is used when a sender and receiver negotiate the maximum segment size (MSS) or as a window scaling factor for use in high-speed networks.
	- The **flag field** contains 6 bits. The **ACK bit** is used to indicate that the value carried in the acknowledgment field is valid; that is, the segment contains an acknowledgment for a segment that has been successfully received.
	- The **TCP Reset packet (RST)**, 
	- 
* **SYN (synchronize)**: Packets that are used to initiate a connection.
* **ACK (acknowledgment)**: Packets that are used to confirm that the data packets have been received, also used to confirm the initiation request and tear down requests
* **RST (reset)**: Signify the connection is down or maybe the service is not accepting the requests
* **FIN (finish)**: Indicate that the connection is being torn down. Both the sender and receiver send the FIN packets to gracefully terminate the connection
* **PSH (push)**: Indicate that the incoming data should be passed on directly to the application instead of getting buffered
* **URG (urgent)**: Indicate that the data that the packet is carrying should be processed immediately by the TCP stack (indicated by the 16-bit **urgent data pointer field**)
* **ECE - Echo of Congestion Encountered** - starts being set in TCP packets when "Congestion Encountered (CE)" is seen
* **CWR - Congestion Window Reduced** - "OK, I saw your ECE, you can turn it off now"
* Two of the most important fields in the TCP segment header are the **sequence number field** and the **acknowledgment number field**. These fields are a critical part of TCP’s reliable data transfer service.
* TCP views data as an unstructured, but ordered, stream of bytes. TCP’s use of sequence numbers reflects this view in that sequence numbers are over the stream of transmitted bytes and not over the series of transmitted segments.
* The **sequence number for a segment** is therefore the byte-stream number of the first byte in the segment.
* Because TCP only acknowledges bytes up to the first missing byte in the stream, TCP is said to provide **cumulative acknowledgments**.
* Telnet - a popular application-layer protocol used for remote login
* It runs over TCP and is designed to work between any pair of hosts.
* Many users prefer to use the SSH protocol rather than Telnet, since data sent in a Telnet connection (including passwords) are not encrypted, making Telnet vulnerable to eavesdropping attacks.
* acknowledgment for client-to-server data is carried in a segment carrying server-to-client data; this acknowledgment is said to be **piggybacked** on the server-to-client data segment.
* For TCP (This was based of an example in the book):
	1. The first segment is sent from the client to the server, containing the 1-byte ASCII representation of the letter ‘C’ in its data field.
	2. The second segment is sent from the server to the client. It serves a dual purpose. First it provides an acknowledgment of the data the server has received. The second purpose of this segment is to echo back the letter ‘C.’
	3. The third segment is sent from the client to the server. Its sole purpose is to acknowledge the data it has received from the server.


### 3.5.3 Round-Trip Time Estimation and Timeout

* TCP, like the rdt protocol from section 3.4 uses a timeout/retransmit mechanism to recover from lost segments. The timeout should be larger than the connection’s **round-trip time (RTT)**, that is, the time from when a segment is sent until it is acknowledged. Otherwise, unnecessary retransmissions would be sent.
* The sample RTT, denoted *SampleRTT*, for a segment is the amount of time between when the segment is sent (that is, passed to IP) and when an acknowledgment for the segment is received.
* Instead of measuring a *SampleRTT* for every transmitted segment, most TCP implementations take only one *SampleRTT* measurement at a time. That is, at any point in time, the *SampleRTT* is being estimated for only one of the transmitted but currently unacknowledged segments, leading to a new value of *SampleRTT* approximately once every RTT.
* TCP never computes a *SampleRTT* for a segment that has been retransmitted; it only measures *SampleRTT* for segments that have been transmitted once
* The *SampleRTT* values will fluctuate from segment to segment due to congestion in the routers and to the varying load on the end systems.
* In order to estimate a typical RTT, it is therefore natural to take some sort of average of the *SampleRTT* values.
* TCP maintains an average, called *EstimatedRTT*, of the *SampleRTT* values. Upon obtaining a new *SampleRTT*, TCP updates *EstimatedRTT* according to the following formula: 
  - ```EstimatedRTT = (1 – α) # EstimatedRTT + α # SampleRTT```
* The formula above is written in the form of a programming-language statement - the new value of *EstimatedRTT* is a weighted combination of the previous value of *EstimatedRTT* and the new value for *SampleRTT*. The recommended value of ```α is α = 0.125``` in which case the formula above
becomes: 
  - ```EstimatedRTT = 0.875 # EstimatedRTT + 0.125 # SampleRTT```
* *EstimatedRTT* is a weighted average of the *SampleRTT* values. This weighted average puts more weight on recent samples than on old samples. This is natural, as the more recent samples better reflect the current congestion in the network.
* In statistics, such an average is called an **exponential weighted moving average (EWMA)**.
* The weight of a given *SampleRTT* decays exponentially fast as the updates proceed.
* It is also valuable to have a measure of the variability of the RTT. *DevRTT*, is an estimate of how much *SampleRTT* typically deviates from *EstimatedRTT*:
	- ```DevRTT = (1 – β) * DevRTT + β * | SampleRTT – EstimatedRTT |```
* Note that *DevRTT* is an EWMA of the difference between *SampleRTT* and *EstimatedRTT*. If the *SampleRTT* values have little fluctuation, then *DevRTT* will be small; on the other hand, if there is a lot of fluctuation, *DevRTT* will be large. 
* The recommended value of ```β is 0.25```.
* Given values of *EstimatedRTT* and *DevRTT*, the interval should be greater than or equal to *EstimatedRTT*, or unnecessary retransmissions would be sent.
* But the timeout interval should not be too much larger than *EstimatedRTT*; otherwise, when a segment is lost, TCP would not quickly retransmit the segment, leading to large data transfer delays.
* TCP’s method for determining the retransmission timeout interval:
	- ```TimeoutInterval = EstimatedRTT + 4 * DevRTT```
* An initial *TimeoutInterval* value of 1 second is recommended.
* When a timeout occurs, the value of *TimeoutInterval* is doubled to avoid a premature timeout occurring for a subsequent segment that will soon be acknowledged.
* However, as soon as a segment is received and *EstimatedRTT* is updated, the *TimeoutInterval* is again computed using the formula above.
 
### 3.5.4 Reliable Data Transfer
* Internet’s network-layer service (IP service) is unreliable. IP does not guarantee datagram delivery, does not guarantee in-order delivery of datagrams, and does not guarantee the integrity of the data in the datagrams. With IP service, datagrams can overflow router buffers and never reach their destination, datagrams can arrive out of order, and bits in the datagram can get corrupted.
* Because transport-layer segments are carried across the network by IP datagrams, transport-layer segments can suffer from these problems as well.
* TCP creates a **reliable data transfer** service on top of IP’s unreliable best-effort service.
* TCP’s reliable data transfer service ensures that the data stream that a process reads out of its TCP receive buffer is uncorrupted, without gaps, without duplication, and in sequence.
* There are three major events related to data transmission and retransmission in the TCP sender:
	1. Upon the occurrence of the first major event, TCP receives data from the application, encapsulates the data in a segment, and passes the segment to IP
		- Note that each segment includes a sequence number that is the byte-stream number of the first data byte in the segment
		- Also note that if the timer is already not running for some other segment, TCP starts the timer when the segment is passed to IP.
		- The expiration interval for this timer is the *TimeoutInterval*, which is calculated from *EstimatedRTT* and *DevRTT*
	2. The second major event is the timeout. TCP responds to the timeout event by retransmitting the segment that caused the timeout. TCP then restarts the timer.
	3. The third major event that must be handled by the TCP sender is the arrival of an acknowledgment segment (ACK) from the receiver (more specifically, a segment containing a valid ACK field value).
* One of the problems with timeout-triggered retransmissions is that the timeout period can be relatively long. When a segment is lost, this long timeout period forces the sender to delay resending the lost packet, thereby increasing the end-to-end delay.
* The sender can often detect packet loss well before the timeout event occurs by noting so-called **duplicate ACKs**. A duplicate ACK is an ACK that reacknowledges a segment for which the sender has already received an earlier acknowledgment.
* A proposed modification to TCP, the so-called **selective acknowledgment**, allows a TCP receiver to acknowledge out-of-order segments selectively rather than just cumulatively acknowledging the last correctly received, in-order segment.
* TCP looks a lot like our generic Selective Repeat (SR) protocol. Thus, TCP’s error-recovery mechanism is probably best categorized as a hybrid of Go-Back-N (GBN) and SR protocols.

### 3.5.5 Flow Control 
* The hosts on each side of a TCP connection set aside a receive buffer for the connection. When the TCP connection receives bytes that are correct and in sequence, it places the data in the receive buffer.
* The associated application process will read data from this buffer, but not necessarily at the instant the data arrives.
* The receiving application may be busy with some other task and may not even attempt to read the data until long after it has arrived. If the application is relatively slow at reading the data, the sender can very easily overflow the connection’s receive buffer by sending too much data too quickly.
* TCP provides a **flow-control service** to its applications to eliminate the possibility of the sender overflowing the receiver’s buffer.
* Flow control is a speed-matching service which matches the rate at which the sender is sending against the rate at which the receiving application is reading.
* A TCP sender can also be throttled due to congestion within the IP network; this form of sender control is referred to as **congestion control**.
* TCP provides flow control by having the *sender* maintain a variable called the **receive window**.
* The receive window is used to give the sender an idea of how much free buffer space is available at the receiver. Because TCP is **full-duplex**, the sender at each side of the connection maintains a distinct receive window.

* Define the following as:
  - *LastByteRead*: the number of the last byte in the data stream read from the buffer by the application process in B
  - *LastByteRcvd*: the number of the last byte in the data stream that has arrived from the network and has been placed in the receive buffer at B
  - Because TCP is not permitted to overflow the allocated buffer, we must have: 
  	- ```LastByteRcvd – LastByteRead <= RcvBuffer```
  - The receive window, denoted *rwnd* is set to the amount of spare room in the buffer:
	- ```rwnd = RcvBuffer – [LastByteRcvd – LastByteRead]```

* **How does the connection use the variable rwnd to provide the flow-control service?**
	- Host B tells Host A how much spare room it has in the connection buffer by placing its current value of *rwnd* in the receive window field of every segment it sends to A.
	- Initially, Host B sets *rwnd = RcvBuffer*. Note that to pull this off, Host B must keep track of several connection-specific variables.
	- Host A in turn keeps track of two variables, *LastByteSent* and *LastByteAcked*. Note that the difference between these two variables, *LastByteSent* – *LastByteAcked*, is the amount of unacknowledged data that A has sent into the connection.
	- By keeping the amount of unacknowledged data less than the value of rwnd, Host A is assured that it is not overflowing the receive buffer at Host B. Thus, Host A makes sure throughout the connection’s life is:
		- ```LastByteSent – LastByteAcked <= rwnd```

### 3.5.6 TCP Connection Management
* The TCP in the client establishes a TCP connection with the TCP in the server in the following manner:
	1. Step 1: The client-side TCP first sends a special TCP segment to the server-side TCP. This special segment contains no application-layer data. But one of the flag bits in the segment’s header , the SYN bit, is set to 1. In addition, the client randomly chooses an initial sequence number (*client_isn*) and puts this number in the sequence number field of the initial TCP SYN segment. This segment is encapsulated within an IP datagram and sent to the server.
	2. Step 2: Once the IP datagram containing the TCP SYN segment arrives at the server host, the server extracts the TCP SYN segment from the datagram, allocates the TCP buffers and variables to the connection, and sends a connection-granted segment to the client TCP. This connection-granted segment also contains no application-layer data. However, it does contain three important pieces of information in the segment header:
        1. First, the SYN bit is set to 1.
        2. Second, the acknowledgment field of the TCP segment header is set to *client_isn+1*.
        3. Finally, the server chooses its own initial sequence number (*server_isn*) and puts this value in the sequence number field of the TCP segment header. This connection-granted segment is saying, in effect, “I received your SYN packet to start a connection with your initial sequence number, *client_isn*. I agree to establish this connection. My own initial sequence number is *server_isn*.” The connection-granted segment is referred to as a **SYNACK segment**.
	3. Step 3: Upon receiving the SYNACK segment, the client also allocates buffers and variables to the connection. The client host then sends the server yet another segment; this last segment acknowledges the server’s connection-granted segment (the client does so by putting the value *server_isn+1* in the acknowledgment field of the TCP segment header). The SYN bit is set to zero, since the connection is established. This third stage of the three-way handshake may carry client-to-server data in the segment payload.
* Once these three steps have been completed, the client and server hosts can send segments containing data to each other. In each of these future segments, the SYN bit will be set to zero.
* In order to establish the connection, three must be sent between the two hosts. For this reason, this connection-establishment procedure is often referred to as a **three-way handshake**.
* During the life of a TCP connection, the TCP protocol running in each host makes transitions through various **TCP states**:
	- The client TCP begins in the CLOSED state.
	- The application on the client side initiates a new TCP connection by creating a socket.
	- This causes TCP in the client to send a SYN segment to TCP in the server.
	- After having sent the SYN segment, the client TCP enters the SYN_SENT state.
	- While in the SYN_SENT state, the client TCP waits for a segment from the server TCP that includes an acknowledgment for the client’s previous segment and has the SYN bit set to 1.
	- Having received such a segment, the client TCP enters the ESTABLISHED state.
	- While in the ESTABLISHED state, the TCP client can send and receive TCP segments containing payload (application-generated) data.
* Suppose that the client application decides it wants to close the connection:
	- This causes the client TCP to send a TCP segment with the FIN bit set to 1 and to enter the FIN_WAIT_1 state.
	- While in the FIN_WAIT_1 state, the client TCP waits for a TCP segment from the server with an acknowledgment.
	- When it receives this segment, the client TCP enters the FIN_WAIT_2 state.
	- While in the FIN_WAIT_2 state, the client waits for another segment from the server with the FIN bit set to 1; after receiving this segment, the client TCP acknowledges the server’s segment and enters the TIME_WAIT state.
	- The TIME_WAIT state lets the TCP client resend the final acknowledgment in case the ACK is lost.

### Random shit about nmap
* To explore a specific TCP port, say port 6789, on a target host, nmap will send a TCP SYN segment with destination port 6789 to that host. There are three possible outcomes:
	- The *source host receives a TCP SYNACK segment from the target host*. Since this means that an application is running with TCP port 6789 on the target post, nmap returns “open.”
	- The *source host receives a TCP RST segment from the target host*. This means that the SYN segment reached the target host, but the target host is not running an application with TCP port 6789. But the attacker at least knows that the segments destined to the host at port 6789 are not blocked by any firewall on the path between source and target hosts.
	- The *source receives nothing*. This likely means that the SYN segment was blocked by an intervening firewall and never reached the target host.

## 3.6 Principles of Congestion Control
* Packet loss is typically the result of over-flowing router buffers as the network becomes congested.
* Packet retransmission thus treats a symptom of network congestion (the loss of a specific transport-layer segment) but does not treat the cause of network congestion—too many sources attempting to send data at too high a rate.
* To treat the cause of network congestion, mechanisms are needed to throttle senders in the face of network congestion.

### 3.6.1 The Causes and the Costs of Congestion
### This section is just a bunch of dumb examples/scenarios. Not much worth taking notes for this section.
**Scenario 1: Two Senders, a Router with Infinite Buffers**

**Scenario 2: Two Senders and a Router with Finite Buffers**

**Scenario 3: Four Senders, Routers with Finite Buffers, and Multihop Paths**

### 3.6.2 Approaches to Congestion Control

* Methods of congestion control: 
	- *End-to-end congestion control* - In an end-to-end approach to congestion control, the network layer provides no explicit support to the transport layer for congestion-control purposes. Even the presence of network congestion must be inferred by the end systems based only on observed network behavior (for example, packet loss and delay). TCP segment loss (as indicated by a timeout or the receipt of three duplicate acknowledgments) is taken as an indication of network congestion, and TCP decreases its window size accordingly.
	- *Network-assisted congestion control* -  With network-assisted congestion control, routers provide explicit feedback to the sender and/or receiver regarding the congestion state of the network. For example, in **ATM Available Bite Rate (ABR)** congestion control, a router informs the sender of the maximum host sending rate it (the router) can support on an outgoing link. The Internet-default versions of IP and TCP adopt an end-to-end approach towards congestion control.

## 3.7 TCP Congestion Control
- TCP provides a reliable transport service between two processes running on different hosts.
- Another key component of TCP is its congestion-control mechanism.

### 3.7.1 Classic TCP Congestion Control
* The approach taken by TCP is to have each sender limit the rate at which it sends traffic into its connection as a function of perceived network congestion.
* If a TCP sender perceives that there is little congestion on the path between itself and the destination, then the TCP sender increases its send rate; if the sender perceives that there is congestion along the path, then the sender reduces its send rate.
* The TCP congestion-control mechanism operating at the sender keeps track of an additional variable, **the congestion window**.
* The **congestion window**, denoted *cwnd*, imposes a constraint on the rate at which a TCP sender can send traffic into the network. Specifically, the amount of unacknowledged data at a sender may not exceed the minimum of *cwnd* and *rwnd*, that is:
	- ```LastByteSent – LastByteAcked <= min{cwnd, rwnd}```
* Note that if acknowledgments arrive at a relatively slow rate (e.g., if the end-end path has high delay or contains a low-bandwidth link), then the congestion window will be increased at a relatively slow rate.
* On the other hand, if acknowledgments arrive at a high rate, then the congestion window will be increased more quickly.
* Because TCP uses acknowledgments to trigger (or clock) its increase in congestion window size, TCP is said to be **self-clocking**.
  
* **How should a TCP sender determine the rate at which it should send?**
	- If TCP senders collectively send too fast, they can congest the network, leading to congestion collapse.
	- However, if TCP senders are too cautious and send too slowly, they could under utilize the bandwidth in the network.
* **How then do the TCP senders determine their sending rates such that they don’t congest the network but at the same time make use of all the available bandwidth? Are TCP senders explicitly coordinated, or is there a distributed approach in which the TCP senders can set their sending rates based only on local information?** 
	* TCP answers these questions using the following guiding principles:
		- *A lost segment implies congestion, and hence, the TCP sender’s rate should be decreased when a segment is lost.* A timeout event or the receipt of four acknowledgments for a given segment (one original ACK and then three duplicate ACKs) is interpreted as an implicit “loss event” indication of the segment following the quadruply ACKed segment, triggering a retransmission of the lost segment. From a congestion-control standpoint, the question is how the TCP sender should decrease its congestion window size, and hence its sending rate, in response to this inferred loss event.
		- *An acknowledged segment indicates that the network is delivering the sender’s segments to the receiver, and hence, the sender’s rate can be increased when an ACK arrives for a previously unacknowledged segment.*  The arrival of acknowledgments is taken as an implicit indication that all is well—segments are being successfully delivered from sender to receiver, and the network is thus not congested. The congestion window size can thus be increased.
		- *Bandwidth probing*. Given ACKs indicating a congestion-free source-to-destination path and loss events indicating a congested path, TCP’s strategy for adjusting its transmission rate is to increase its rate in response to arriving ACKs until a loss event occurs, at which point, the transmission rate is decreased. The TCP sender thus increases its transmission rate to probe for the rate that at which congestion onset begins, backs off from that rate, and then to begins probing again to see if the congestion onset rate has changed. Note that there is no explicit signaling of congestion state by the network--ACKs and loss events serve as implicit signals--and that each TCP sender acts on local information asynchronously from other TCP senders.
* **TCP congestion-control algorithm**:
	1. slow start
	2. congestion avoidance
	3. fast recovery
* Slow start and congestion avoidance are mandatory components of TCP, differing in how they increase the size of cwnd in response to received ACKs. 
* Fast recovery is recommended, but not required, for TCP senders.

* **Slow Start** 
  -  When a TCP connection begins, the value of *cwnd* is typically initialized to a small value of 1 MSS, resulting in an initial sending rate of roughly MSS/RTT. For example, if MSS = 500 bytes and RTT = 200 msec, the resulting initial sending rate is only about 20 kbps.
  -  Since the available bandwidth to the TCP sender may be much larger than MSS/RTT, the TCP sender would like to find the amount of available bandwidth quickly. Thus, in the slow-start state, the value of *cwnd* begins at 1 MSS and increases by 1 MSS every time a transmitted segment is first acknowledged.
  -  TCP sends the first segment into the network and waits for an acknowledgment.
  -  When this acknowledgment arrives, the TCP sender increases the congestion window by one MSS and sends out two maximum-sized segments.
  -  These segments are then acknowledged, with the sender increasing the congestion window by 1 MSS for each of the acknowledged segments, giving a congestion window of 4 MSS, and so on.
  -  This process results in a doubling of the sending rate every RTT.
  -  Thus, the TCP send rate starts slow but grows exponentially during the slow start phase.
  - **But when should this exponential growth end?**
    1. First, if there is a loss event (i.e., congestion) indicated by a timeout, the TCP sender sets the value of *cwnd* to 1 and begins the slow start process. It also sets the value of a second state variable, *ssthresh* (short for “slow start threshold”) to *cwnd/2* a.k.a, half of the value of the congestion window value when congestion was detected.
    2. The second way in which slow start may end is directly tied to the value of *ssthresh*. Since *ssthresh* is half the value of *cwnd* when congestion was last detected, it might be a bit reckless to keep doubling *cwnd* when it reaches or surpasses the value of *ssthresh*. Thus, when the value of *cwnd* equals *ssthresh*, slow start ends and TCP transitions into congestion avoidance mode.
    3. The final way in which slow start can end is if three duplicate ACKs are detected, in which case TCP performs a fast retransmit and enters the fast recovery state.

* **Congestion Avoidance**
	- On entry to the congestion-avoidance state, the value of *cwnd* is approximately half its value when congestion was last encountered
	- Thus, rather than doubling the value of *cwnd* every RTT, TCP adopts a more conservative approach and increases the value of *cwnd* by just a single MSS every RTT
	- This can be accomplished in several ways. A common approach is for the TCP sender to increase *cwnd* by MSS bytes (MSS/*cwnd*) whenever a new acknowledgment arrives.
	- **But when should congestion avoidance’s linear increase (of 1 MSS per RTT) end?** 
    	* TCP’s congestion-avoidance algorithm behaves the same when a timeout occurs as in the case of slow start: The value of *cwnd* is set to 1 MSS, and the value of *ssthresh* is updated to half the value of *cwnd* when the loss event occurred.
		* However, a loss event also can be triggered by a triple duplicate ACK event.
		* In this case, the network is continuing to deliver some segments from sender to receiver (as indicated by the receipt of duplicate ACKs).
		* TCP halves the value of *cwnd* (adding in 3 MSS for good measure to account for the triple duplicate ACKs received) and records the value of *ssthresh* to be half the value of *cwnd* when the triple duplicate ACKs were received. The fast-recovery state is then entered.

* **Fast Recovery** 
# LEFT OFF ON PAGE 268