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
	* Once the client sends a message into its socket interface, the message is out of the client's hands and is â€œin the hands" of TCP
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
- This involves a â€œthree-way handshake"
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
- QUIC, discussed in Chapter 3, is a new â€œtransport" protocol that is implemented in the application layer over the bare-bones UDP protocol
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

- In the example above, the client sends a message (â€œ`Do you like ketchup? How about pickles?"`) from mail server `crepes.fr` to mail server `hamburger.edu`
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
- However, in most cases, the desired IP address is often cached in a â€œnearby" DNS server, which helps to reduce DNS network traffic as well as the average DNS delay

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
	* **Distant centralized database**. A single DNS server cannot be â€œclose to" all the querying clients. If we put the single DNS server in New York City, then all que- ries from Australia must travel to the other side of the globe, perhaps over slow and congested links. This can lead to significant delays.
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
	3. The user's Local DNS Server (LDNS) relays the DNS query to an authoritative DNS server for NetCinema, which observes the string "video" in the host- name video.netcinema.com. To â€œhand over" the DNS query to KingCDN, instead of returning an IP address, the NetCinema authoritative DNS server returns to the LDNS a hostname in the KingCDN's domain, for example, `a1105.kingcdn.com`.
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
	1. One type is an implementation whose operation is specified in a protocol standard, such as an RFC or some other standards document; such an application is sometimes referred to as â€œopen," since the rules specifying its operation are known to all. For such an implementation, the client and server programs must conform to the rules dictated by the RFC.
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
