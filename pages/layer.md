# Services, Physical Layer, and Link Layer
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/g/personal/bowermanjess_seattleu_edu/EYBOY1J5qAlDsHmv-Vz12SEBwzygHpKxa3KZYxF6L2bJRA?e=RjkeQb)
---

## Types of Network Services
Layer can provide two types of services to the layer above it 

<br>

**<font color="#A72608">Connection-oriented</font>** service
- Establish (logical) connection between source and destination
  - Might include negotiation to deicde on parameters
- Use connection to transfer data
- Release/end connection

**<font color="#A72608">Connection-less</font>** service
- No connection is established between source and destination
- Each unit of data carries full destination address
- Data unit routed though network independent of other data unit

<br>

Each of these services can be of two kinds 

<br>

**<font color="#A72608">Reliable</font>** service
- Ensure data accuracy and integrity
- Requires acknowledgment by receiver
- Has significant overhead

**<font color="#A72608">Unreliable</font>** service
- Does not check to see whether data was received
- Data could sometimes get lost/delayed/corrupted
- Less overhead

---

## The Physical Layer
**Fundamental Purpose** <br>
- Defines the electrical, timeing, and other interfaces for transferring data bits between two adjaceent nodes
- **Adjacent nodes:*** nodes that are directly connected by some kind of communication channel that conceptually behaves like a wire
  - Bits sent from one end of the channel are delivered in the same order on the other end of the channel

---

## The Link Layer
Provides a well-defined service to be used by the network layer <br>
- Fundamental service is to transfer data units between adjacent nodes (over single link)
  - At this level we are no longer dealing with raw bits like in a physical layer but rather a **logical unit of data** which is given by the network layer and is termed a **packet**
  - To transfer data to another node the link later uses the physical address of the receiver node
  - Receiver must be able to distinguish packets from each other

- Because physical communication channels could introduce electrical noise and cause errors the link layer is responsible for detecting and possibly even correcting certain types of transmission errors
  - Ensures that packet reaches receivers network layer is error free (error control)

- Because its possible for a sender to be faster in its operation than the receiver the link later regulates the flow of packets over the link
  - Ensure receiver does not get flooded with more packets than it can handle (flow control)
