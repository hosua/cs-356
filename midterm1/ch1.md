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
	* They define protocols such as **TCP**, **IP**, **HTTP** (for the Web), and **SMTP** (for e-mai).
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
- Thus, in order for Host A to communicate with Host B, the network must first reserve one circuit on each of two linksA
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
* The propagation speed depends on the physical medium of the link (that is, fiber optics, twisted-pair copper wire, and so on) and is in the range of 2*10^8 meter/sec to 3*10^8 meters/sec
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
- If `Rs < Rc`, then the bits pumped by the server will â€œflow" right through the router and arrive at the client at a rate of `Rs` bps, giving a throughput of `Rs` bps
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

- among others, in the late 1960s and early 1970s [Schwartz 1977]; IBM's SNA (1969â€“1974), which paralleled the ARPAnet work [Schwartz 1977].
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
- Many Internet commerce companies are now running their applications in the â€œcloud"--such as in Amazon's EC2, in Microsoft's Azure, or in the Alibaba Cloud. Many companies and universities have also migrated their Internet applications (e.g., e-mail and Web hosting) to the cloud.
- This Entire Chapter is nothing