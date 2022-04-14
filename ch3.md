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

**A:** In the A-to-B segment the source port number serves as part of a â€œreturn address" (you can also think of our mail analogy from earlier. The return address is always written on the letter before its sent out. When B wants to send a segment back to A, the destination port in the B-to-A segment will take its value from the source port value of the A-to-B segment


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
- incomplete