# CHAPTER 5 - The Network Layer: Control Plane

## 5.1 Introduction //389 in text
- discuss the formulation of the network control plane
- how are forwarding and flow tables are computed, maintain, and installed
- each router on a network communicates with others to develop this table
- Logically Centeralized Control, sets up assigning ip addresses, loadsharing, NAT and other stuff
- controller talks with Control Agent(CA) to configure each routers flow table

## 5.2 Routing Algorithms
- Routing Algorithms determine good paths(routes) from senders to recievers, good having the lowest cost
- rules can also forbid ceartin nodes in a path
- graph $G=(N,E)$ where $N \rarr $ nodes ; $E \rarr$ edges
- a node y is said to be a neighbor of node x if (x, y) belongs to E.
- There are typically many paths between the two nodes, with each path having a cost. One or more of these paths is a least-cost path. The least-cost problem is therefore clear: Find a path between the source and destination that has least cost.
- If all edges in the graph have the same cost, the least cost path is also the shortest path
- **Centralized Routing Algorithm**- Computes the least-cost path between a source and destination using complete, global knowledge about the network.
- **Link-state(LS) Algorithm**- Algorithms with global state information; the algorithm must be aware of the cost of each link in the network.
- **Decentralized Routing Algorithm**- The least-cost path is carried out in an iterative, distributed manner by the routers. No node has complete information about the costs of all network links. Instead, each node begins with only the knowledge of the costs of its own directly attached links.
- **Static Routing Algorithm**- routes change very slowly over time, often as a result of human intervention
- **Dynamic Routing Algorithm**- change the routing paths as the network traffic loads or topology change.
- **Load-Sensitive Algorithm**- link costs vary dynamically to reflect the current level of congestion in the underlying link. If a high cost is associated with a link that is currently congested, a routing algorithm will tend to choose routes to avoid such a congested link.
- **Load-Insensitive**- link’s cost does not explicitly reflect its current (or
recent past) level of congestion.(Examples: RIP, OSPF, and BGP))

### 5.2.1 The Link-State (LS) Routing Algorithm
- Link-state algorithm: the network topology and all link costs are known, that is, available as input to the LS algorithm.
- A common link-state routing algorithm is known as Dijkstra’s algorithm, named after its inventor (lmao 288).
- Time complexity: $O(n^2)$
### 5.2.2 The Distance-Vecctor (DV) Routing Algorithm
- In use today
- using global information, the distance vector (DV) algorithm is iterative, asynchronous, and distributed.
- Time complexity: $d_x(y) = min_y \{ c(x,v) + d_v (y)\}$
- In the DV algorithm, a node x updates its distance-vector estimate when it either sees a cost change in one of its directly attached links or receives a distance-vector update from some neighbor.
- When a node running the DV algorithm detects a change in the link cost from itself to a neighbor, it updates its distance vector and, if there’s a change in the cost of the least-cost path, informs its neighbors of its new distance vector.
- **Distance-Vector Algorithm: Adding Poisoned Reverse**
    - If z routes through y to get to destination x, then z will advertise to y that its distance to x is infinity, that is, z will advertise to y that Dz(x) = ∞ (even though z knows Dz(x) = 5 in truth). z will continue telling this little white lie to y as long as it routes to x via y. Since y believes that z has no path to x, y will never attempt to route to x via z, as long as z continues to route to x via y (and lies about doing so).
- **A Comparison of LS and DV Routing Algorithms**
    - The DV and LS algorithms take complementary approaches toward computing routing. In the DV algorithm, each node talks to only its directly connected neighbors, but it provides its neighbors with least-cost estimates from itself to all the nodes (that it knows about) in the network. The LS algorithm requires global information.
    - In the end, neither algorithm is an obvious winner over the other; indeed, both algorithms are used in the Internet.

## 5.3 Intra-AS Routing in the Internet: OSPF
- Problems arise as we consider the network as a bunch of routers
- Scale. As the number of routers becomes large, the overhead involved in communicating, computing, and storing routing information becomes prohibitive.
- Administrative autonomy. As described in Section 1.3, the Internet is a network of ISPs, with each ISP consisting of its own network of routers.
- Both of these problems can be solved by organizing routers into autonomous systems (ASs), with each AS consisting of a group of routers that are under the same administrative control.
- The routing algorithm running within an autonomous system is called an intra-autonomous system routing protocol.
- **Open Shortest Path First (OSPF)**
    - OSPF is a link-state protocol that uses flooding of link-state information and a Dijkstra’s least-cost path algorithm. With OSPF, each router constructs a complete topological map (that is, a graph) of the entire autonomous system. Each router then locally runs Dijkstra’s shortest-path algorithm to determine a shortest-path tree to all subnets, with itself as the root node. Individual link costs are configured by the network administrator.
    - Some advantages to using OSPF are Security, Multiple same-cost paths, Integrated support for unicast and multicast routing, Support for hierarchy within a single AS
## 5.4 Routing Among the ISPs: BGP
- We need an *inter-autonomous system routing protocol*. Since an inter-AS routing protocol involves coordination among multiple ASs, communicating ASs must run the same inter-AS routing protocol. In fact, in the Internet, all ASs run the same inter-AS routing protocol, called the Border Gateway Protocol, more commonly known as *BGP*

### 5.4.1 The Role of BGP
- In BGP, packets are not routed to a specific destination address, but instead to CIDRized prefixes, with each prefix representing a subnet or a collection of subnets.
- As an inter-AS routing protocol, BGP provides each router a means to: Obtain prefix reachability from neighboring ASs and Determine the "best" routes to the prefixes

### 5.4.2 Advertising BGP Route Information
- For each AS, each router is either a gateway router or an internal router. A gateway router is a router on the edge of an AS that directly connects to one or more routers in other ASs. An internal router connects only to hosts and routers within its own AS.
- Each such TCP connection, along with all the BGP messages sent
over the connection, is called a BGP connection. Furthermore, a BGP connection that spans two ASs is called an external BGP (eBGP) connection, and a BGP session between routers in the same AS is called an internal BGP (iBGP) connection.

### 5.4.3 Determining the Best Routes
- Each such TCP connection, along with all the BGP messages sent over the connection, is called a BGP connection. Furthermore, a BGP connection that spans two ASs is called an external BGP (eBGP) connection, and a BGP session between routers in the same AS is called an internal BGP (iBGP) connection.
- Here, each BGP route is written as a list with three components: NEXT-HOP; AS-PATH; destination prefix. In practice, a BGP route includes additional attributes, which we will ignore for the time being.
- **Hot Potato Routing**
    - As just described, this router will learn about two possible BGP routes to prefix x. In hot potato routing, the route chosen (from among all possible routes) is that route with the least cost to the NEXT-HOP router beginning that route.
    - In the name “hot potato routing,” a packet is analogous to a hot potato that is burning in your hands. Because it is burning hot, you want to pass it off to another person (another AS) as quickly as possible.
- **Route-Selection Algorithm**
    - A route is assigned a local preference value as one of its attributes (in addition to the AS-PATH and NEXT-HOP attributes).
    - From the remaining routes (all with the same highest local preference value), the route with the shortest AS-PATH is selected. If this rule were the only rule for route selection, then BGP would be using a DV algorithm for path determination, where the distance metric uses the number of AS hops rather than the number of router hops.
    - From the remaining routes (all with the same highest local preference value and the same AS-PATH length), hot potato routing is used, that is, the route with the closest NEXT-HOP router is selected.
    - If more than one route still remains, the router uses BGP identifiers to select the route.

### 5.4.4 IP-Anycast
- In addition to being the Internet’s inter-AS routing protocol, BGP is often used to implement the IP-anycast service
- Although the above CDN example nicely illustrates how IP-anycast can be used, in practice, CDNs generally choose not to use IP-anycast because BGP routing changes can result in different packets of the same TCP connection arriving at different instances of the Web server.

### 5.4.5 Routing Policy
- When a router selects a route to a destination, the AS routing policy can trump all other considerations, such as shortest AS path or hot potato routing. Indeed, in the route-selection algorithm, routes are first selected according to the local-preference attribute, whose value is fixed by the policy of the local AS.
- multi-homed access ISP, since it is connected to the rest of the network via two different providers (a scenario that is becoming increasingly common in practice).
- **Why Are There Diffrent Inter-AS and Intra-AS Routing Protocols?**
    - Policy. Among ASs, policy issues dominate. It may well be important that traffic originating in a given AS not be able to pass through another specific AS.
    - Scale. The ability of a routing algorithm and its data structures to scale to handle routing to/among large numbers of networks is a critical issue in inter-AS routing.
    - Performance. Because inter-AS routing is so policy oriented, the quality (for example, performance) of the routes used is often of secondary concern (that is, a longer or more costly route that satisfies certain policy criteria may well be taken over a route that is shorter but does not meet that criteria).
### 5.4.6 Putting the Pieces Together: Obtaining Internet Presence
- To meet these goals, you first need to obtain Internet connectivity, which is done by contracting with, and connecting to, a local ISP. Your company will have a gateway router, which will be connected to a router in your local ISP.
- In addition to contracting with an ISP, you will also need to contract with an Internet registrar to obtain a domain name for your company.
## 5.5 The SDN Control Plane
- notes

### 5.5.1 The SDN Control PLane: SDN Controller and SDN Network-control Applications
- notes

### 5.5.2 OpenFlow Protocol
- notes

### 5.5.3 Data and Control PLane Interaction: An Example
- notes

### 5.5.4 SDN: Past and Future
- notes

## 5.6 ICMP: The Internet Control Message Protocol
- notes

## 5.7 Network Management and SNP, NETCONF/YANG
- notes

### 5.7.1 The Network Management Framework
- notes

### 5.7.2 The Simple Network Management Protocol(SNMP) and the Management Information Base (MIB)
- notes

### 5.7.3 The Network Configuration Protocol (NETCONF) and YANG
- notes

## 5.8 Summary

## Questions
