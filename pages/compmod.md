# Network Models
---
## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B793C4E35-B1B5-467E-8BBD-598E2D8B1353%7D&file=6%20-%20Computer%20Networks%20-%20Week%206%20-%20OSI%20-%20Final.pptx&action=edit&mobileredirect=true)
---

## Network Model - OSI Reference Model
- OSI stands for Open Systems Interconnection
- Has 7 layers
- Specifies function of each layer but does not specifiy exact services/protocols to use at each layer or what exact interfaces to provide at each layer

---

## OSI Layers Overview - Reference Model
<font color="#A72608">**Application**</font> layer
- User interface to networking services
- Provides variety of commonly used functions
  - File transfer, email, etc (actual data/message resides)

<font color="#A72608">**Presentation**</font> layer
- Handles formatting details for data to be communicated
  - Encryption, compression, stream formatting, etc

<font color="#A72608">**Session**</font> layer
- Provides services to initiate, maintain and evenutally terminate a connection between sender and receiver

<font color="#A72608">**Transport**</font> layer
- Provides end to end message delivery service (deliver to transport layer on recipient's side)
- Controls rate of transfer and ensures network is not overloaded
  - Flow control and congestion control (helps prevent bottleneck)

<font color="#A72608">**Network**</font> layer
- Controls actual transfer of data units through the network
- Determines path to take from source to destination (routing)
- Responsible for forwarding units of data to next node/router in path
- Shares congestion control responsibility with Transport layer

<font color="#A72608">**Data Link**</font> layer
- Transmits data over link between two nodes
  - May not be the endpoints
  - May be any two nodes that have a link between them on the communication path determined by network layer
- Performs error and flow control over link
- Determines when computer has the right to access medium
  - Medium is shared by a bunch of computers
  - Taken care of by Medium Access Control (MAC) sub-layer

<font color="#A72608">**Physical**</font> layer
- Consists of basic networking hardware
- Transmits or receives raw bits over communication channel
- Determines how a physical connection is established and mode of transmission

---

## OSI Model (7 Layers)
Every computer will have the same 7 layers within its networking software <br>

![Computing Systems!](https://freesvg.org/img/osi-model.png)

---

## TCP/IP Reference Model
- Has four layers
  - Was originally used in ARPANET (research network sponsored by DoD)

![Computing Systems!](https://www.guru99.com/images/1/102219_1135_TCPIPvsOSIM1.png)

- Named after two of its primary protocols (TCP & IP)
  - In this model, protocols are specified and are more important than strict layering

### Layer Overview

<font color="#A72608">**Application**</font> layer









