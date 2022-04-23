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
- This jobof delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**
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


# LEFT OFF ON PAGE 268
* **TCP Splitting: Optimizing The Performance of Cloud Services**
	* One way to mitigate this problem and improve user-perceived performance is to (1) deploy front-end servers closer to the users, and (2) utilize TCP splitting by breaking the TCP connection at the front-end server. With TCP splitting, the client establishes a TCP connection to the nearby front-end, and the front-end maintains a persistent TCP connection to the data center with a very large TCP congestion window
	* In summary, TCP splitting can reduce the networking delay roughly from 4 #RTT to RTT, significantly improving user-perceived performance, particularly for users who are far from the nearest data center.
* **Fast Recovery**
	- In fast recovery, the value of cwnd is increased by 1 MSS for every duplicate ACK received for the missing segment that caused TCP to enter the fast-recovery state.
	- Eventually, when an ACK arrives for the missing segment, TCP enters the congestion-avoidance state after deflating cwnd.
	- If a timeout event occurs, fast recovery transitions to the slow-start state after performing the same actions as in slow start and congestion avoidance: The value of cwnd is set to 1 MSS, and the value of ssthresh is set to half the value of cwnd when the loss event occurred.
	- It is interesting that an early version of TCP, known as TCP Tahoe, unconditionally cut its congestion window to 1 MSS and entered the slow-start phase after either a timeout-indicated or triple-duplicate-ACK-indicated loss event. The newer version of TCP, TCP Reno, incorporated fast recovery.
* **TCP Congestion Control: Retrospective**
	- For this reason,TCP congestion control is often referred to as an additive-increase, multiplicative-decrease (AIMD) form of congestion control. AIMD congestion control gives rise to the “saw tooth” behavior shown in Figure 3.53, which also nicely illustrates our earlier intuition of TCP “probing” for bandwidth—TCP linearly increases its congestion window size (and hence its transmission rate) until a triple duplicate-ACK event occurs.
* **TCP Cubic**
	- TCP CUBIC differs only slightly from TCP Reno. Once again, the congestion window is increased only on ACK receipt, and the slow start and fast recovery phases remain the same.
* **Macroscopic Description of TCP Reno Throughput**
	- average throughput (0.75*W)/RTT
### 3.7.2 Network-Assisted Explicit Congestion Notification and Delayed-based Congestion Control
- Explicit Congestion Notification
	- One setting of the ECN bits is used by a router to indicate that it (the router) is experiencing congestion. This congestion indication is then carried in the marked IP datagram to the destination host, which then informs the sending host, as shown in Figure 3.55. RFC 3168 does not provide a definition of when a router is congested; that decision is a configuration choice made possible by the router vendor, and decided by the network operator.
	- As shown in Figure 3.55, when the TCP in the receiving host receives an ECN congestion indication via a received datagram, the TCP in the receiving host informs the TCP in the sending host of the congestion indication by setting the ECE (Explicit Congestion Notification Echo) bit (see Figure 3.29) in a receiver-to-sender TCP ACK segment.
- Delay-Based Congestion Control
	- In TCP Vegas [Brakmo 1995], the sender measures the RTT of the source-to-destination path for all acknowledged packets. Let RTTmin be the minimum of these measurements at a sender; this occurs when the path is uncongested and packets experience minimal queueing delay.
	- TCP Vegas operates under the intuition that TCP senders should “Keep the pipe just full, but no fuller”
### 3.7.3 Fairness
- Is TCP’s AIMD algorithm fair, particularly given that different TCP connec-
tions may start at different times and thus may have different window sizes at a given point in time?
- Suppose that the TCP window sizes are such that at a given point in time, con-
nections 1 and 2 realize throughputs indicated by point A in Figure 3.56. Because the amount of link bandwidth jointly consumed by the two connections is less than R, no loss will occur, and both connections will increase their window by 1 MSS per RTT as a result of TCP’s congestion-avoidance algorithm.
* **Fairness and UDP**
	- Many multimedia applications, such as Internet phone and video conferencing, often do not run over TCP for this very reason—they do not want their transmission rate throttled, even if the network is very congested. Instead, these applications prefer to run over UDP, which does not have built-in congestion control. When running over UDP, applications can pump their audio and video into the network at a constant rate and occasionally lose packets, rather than reduce their rates to “fair” levels at times of congestion and not lose any packets.
* **Fairness and Parallel TCP Connections**
	- This is because there is nothing to stop a TCP-based application from using multiple parallel connections. For example, Web browsers often use multiple parallel TCP connections to transfer the multiple objects within a Web page. (The exact number of multiple connections is configurable in most browsers.) When an application uses multiple parallel connections, it gets a larger fraction of the bandwidth in a congested link.
## 3.8 Evolution of Transport-Layer Functionality
- **QUIC: Quick UDP Internet Connections**
	- Connection-Oriented and Secure. Like TCP, QUIC is a connection-oriented protocol between two endpoints. This requires a handshake between endpoints to set up the QUIC connection state.
	- Streams. QUIC allows several different application-level “streams” to be multiplexed through a single QUIC connection, and once a QUIC connection is established, new streams can be quickly added.
	- Reliable, TCP-friendly congestion-controlled data transfer. As illustrated in Figure 3.59(b), QUIC provides reliable data transfer to each QUIC stream separately. Figure 3.59(a) shows the case of HTTP/1.1 sending multiple HTTP requests, all over a single TCP connection.
	- it’s worth highlighting again that QUIC is an application-layer protocol providing reliable, congestion-controlled data transfer between two endpoints.
## 3.9 Summary
- We learned in Section 3.4 that a transport-layer protocol can provide reliable data transfer even if the underlying network layer is unreliable.
- In Section 3.5, we took a close look at TCP, the Internet’s connection-oriented and reliable transport-layer protocol. We learned that TCP is complex, involving connection management, flow control, and round-trip time estimation, as well as reliable data transfer.
- In Section 3.6, we examined congestion control from a broad perspective, and in Section 3.7, we showed how TCP implements congestion control.
- In Chapter 1, we said that a computer network can be partitioned into the“network edge” and the “network core.” The network edge covers everything that happens in the end systems.