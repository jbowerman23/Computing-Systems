# Network Layer - Internetworking & Congestion Control
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B40351912-11B8-4D9F-8405-C7CC84B2C8AD%7D&file=CPSC-3500-Computing-Systms-Monday-Week-9-Network-Layer-Internetworking-Confestion-Control.pptx&action=edit&mobileredirect=true)
---
  
### Network Layer Review
Must provide
- Routing & forwarding
- Congestion control
- Internetworking

---

### Internetworking
- Several routing algorithms considered so far assume 
  - Homogeneous network
  - All nodes use common protocols in all layers

- This is not always true in reality
  - Networks may differ in several ways...
  - ... It is the goal of a network algorithm to reconcile these differences in such a way that a computer on one network can communicate with the computer on a different network

In what way do networks differ?
- Services: connectionless versus connection oriented
  - This is kind of like trying to combine a postal network and the telephone network we talked about
- Addressing: different sizes, flat numbering system or hierarchical addressing
- Packet size: different maximum sizes
  - Typically due to restritions of the technology being used in the link layer
- Quaility of Service: priority
  - ... may distinguish between regular and priority packets and provide special service to those priority packets
  - If you try to combine a network that accommodates priority, and another network has no clue about priorities
  - ... This is a big difference and such a difference may never be able to be reconciled

---

### What happens when you send a packets from source to destination?
1. Need to be able to specifiy the address of the destination computer
  - Need to find some way of providing a common addressing scheme
    - Internal addressing schemes used by these two networks may be different

2. Lets say we resolved the issue of providing a common addressing scheme
  - MPLS network uses connection-oriented service
    - It assigns labels to packets to tell it what connection the packet belongs to
      - The individual packet originated from a connection less service
      - Must be mapped to a specific connection and this a specific label with MPLS
    - The connection somehow needs to be set up ahead of time

2. Lets say we find a way of accommodating different types of services
  - Now we can get to the other end of the MPLS network
    - Next, connection details and labels need to be stripped and the packet needs to now be sent into the ethernet network
    - Finally we are in the network of the destination computer

3. Ethernet supports smaller frame sizes
  - The packet needs to be divided into smaller packets before it can reach destination
  - There are many things that need to be done seamlessly for a communication to be successful

---

### Cerf & Kahn
Hides all these differences in the physical and link layers
- Common network layer above different physical networks
  - Use common protocol in the network layer that all nodes understand regardless of the underlying link and physical layers
- Internet Protocol (IP): foundation of the internet
  - Main reason the internet can allow communication across different types of networks
  - IP basically provides packet format that most routers recognize and are able to pass through almost every type of network

---

### Details of IP
- Common network layer protocol used by most nodes
  - Glue that hold the internet together
- IP provides a connectionless, best effort service
  - No reliability guarantees
  - No ordering guarantees
- Two versions of IP
  - IPv4 - widely used today
  - IPv6 - new version of IP

### IP version 4
- When IPv4 is in use - IPv4 header is included in all network layer packets before sending it down to the link layer

- IPv4 addresses are 32-bits each
  - Total number of addresses are limited to what can be represented using 32 bits
  - IPv4 can't keep up with the growing size of the internet

- New version -> **IPv6**
  - Supports 128-bit address
  - Has simpler header -> reduces process overhead due to simplicity
  - Better support for options
- Has not been easy to deploy on the internet-scale
  - Does not internetwork easily with IPv4

Concept of internetworking relies on a common protocol at the network layer
- IPv4 and IPv6 are similar but not the same

---

### Congestion
- Congestion is when the network gets flooded with more packets than it can handle
- Could cause excessive delays, packet drops, etc

- Responsibility of congestion control is shared by transport and network layers

Serveral approaches can be taken to handle congestion
1. Let routing algorithm handle congestion (traffic-aware routing)
  - In addition to topology of network being considered also consider traffic at anytime

2. Decreases traffic/load being placed on the network
  - Find some way to inform hosts that they should reduce the number of packets being transmitted

3. Increase capacity of the network
  - Allocate more resourced to the network (provisioning)
  - More of a long-term solution

---

### Traffic-aware routing
Goal: consider current load & direct traffic away from hotspots
- Choose route depending on traffic, not just topology
- Could lead to oscillations in routing table

Some solutions to oscillation
- Change route slowly,not all at once
  - Use external traffic engineering to decided weights etc, based on big picture
- Use multiple paths at once
  - Distribute traffic over links (use both CF and EI) to try and balance the load

---

### Traffice throttling
- Routers determine when congestions is impending
- Routers notify senders of impending congestions
- Some approaches
  - Send choke packet to senders causing congestion
    - Sender required to reduce rate of transmission
  - Set flag in packet notifying impending congestion
    - Explicity congestion notifying impedning congestion

---

### Admission control
- Useful in connection-oriented service
  - This is a service where a sender first sets up a connection before starting to send a stream of packets to a destination
- If network is congested, refuse new connection (virtual circuit) if network can handel it without being congested
- How do you know if a new connection will cause congestion?
  - Need some way to represent traffic state
  - Approaches include leaky bucket
    - When the bucket is full of water, additional water that enters spills over the sides and is lost

---

### If nothing else works
- Routers resort to load shedding
  - Routers drop packets
- Which packets should be dropped?
  - Depends on situation
  - File transfer -> old pakcet worth more than new one bc order matters
  - Real-time streaming -> new packet worth more than oldone
    - Drop delayed packets to provide better streaming for a movie
