# Network Layer - Routing & Forwarding - Dijkstra's algorithm practice
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7BA1C76553-D4C7-497D-A94F-9BE533DB1D60%7D&file=CPSC-3500-Networking-Layer-Routing-Basics-Final.pptx&action=edit&mobileredirect=true)
---

### What does the network layer do?
- Goal: Transfer packets of data between endpoints (source/orgin -> destination) via multiple links
  - This is the lowest layer that deals with end-to-end aspects
    - Link layer simply transfers a packet over a single link between two adjacent nodes

Routing and Forwarding
- Routing: Identifying the path that a packet must take to get from source node to destination node
  - Possibly via multiple intermediate nodes
- Forwarding: Forwarded packets along path

Congestion control
- Must avoid/recover from network congestion

Internetworking
- Must support joining of multiple networks into a single network of networks
- Must provide uniform addressing across entire network of networks
- Details of physical network, number/types of nodes and network topology, etc. must be hidden from transport layer
  - Transport layer must have a uniform way of specifying any computer's address and must not care about the details

---

### Routing Basics
- Routing -> identify path between endpoints for communication
- What happens at each node along this path between endpoints?
  - This is where forwarding comes into play
  - Most common option: **Store-and-forward** packet switching
    - When the start of a new frame is received by the link layer of a certain node 
    - First: it waits for entire frame to arrive and the link layer will verify the integrity of that frame
    - Then: Link layer send the packet within that frame to the network layer

  - Determines/Forwards packets to next router along identified route
  - When destination reached, send packet up to transport layer on that destination node
    - One intermediate nodes, packets only travel up to the network layer

---

### Routing Goals
- Could have multiple possible routes between A & B
  - Routing algorithm needs to make appropriate choice
- Goals of routing algorithm
  - Deliver packets to their intended destination
  - Have low overhead (simplicity)
  - Be efficient (minimize delay, maximize throughput)
  - Cope with changes in topology and traffic (robustness)
  - Not take forever to converge to routing choice (stability)
  - Treat different nodes fairly

---

### Types of Routing Algorithms
Non-adaptive or static
- Routes fixed offline and routing information is simply stored in tables
- Makes sense if there's only one clear choice

Adaptive or dynamic (caters to robustness)
- Routes changed to reflect changes in network state
  - Topology, traffic changes
- Have some optimization criteria

### Examples
- Shorest path routing
- Flooding
- Distance vector routing
- Link state routing
- Hierarchical routing

### Shortest Path Routing
Goal: Route Packets along the shortest path between source and destination nodes
- Shorest path is calculated and stored in a routing table
- Shortest path could mean
  - Lowest number of hops (links)
  - Shortest geographic distance
  - Lowest average delay (fastest path)
- Can assign labels using weighted "distance"

See slides for Dijkstra's Algorithm

---

### Hierarchical Routing
- As the size of a netowrk increases, routing tables can get very large
  - Dijkstra's may be hard to scale for large networks
- In practice its typical to set up a hierarchy of routers
  - A group of routers for a region
  - Each router in its region knows details about router in its own region
  - If it needs to send packets to some destination outside its own region
  - Designated routers are used to go outside a region

---

### When are routing decisions made?
Connectionless service (widely used)
- Routing decisions are made independently for every single pakcet
- All packets that are going from a given source to a given destination may not take the same route ... depends on the algorithm and state of netowrk

Connection-oriented service
- Routing decisions are made once during the connection establishment phase
- Same route is actually used for all packets that are part of the same connection

