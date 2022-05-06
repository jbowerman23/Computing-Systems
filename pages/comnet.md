# Computer Networks
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/g/personal/bowermanjess_seattleu_edu/Ed4CQ8kXlw1GhKuQccyG50YBS7KQJQC1rm4jVfwH6aCe5A?e=GLTfoE)
---

## Example Networks

- Postal network
  - Delivers letters/packages between sender and reciever
  - Send and reciever identified by postal address
- Telephone network
  - Provides voice communication between users
  - User Identified by telephone number

---

## Computer Network
- Provides communication between computers
  - Mechanism where computers can exchange data
- Need a way to identify computers
  - In the internet, this is done vis IP addresses

### What can computer networking give us?
- Communication or information sharing
  - electronic mail, message broadcast
- Resource sharing (both hardware and software)
  - printers disss space, application software (central location)
- Remote computing (location independence)
  - Geography need not be a restriction

---

## IP Address
- IP address identifies any device connected to the Internet
- IPv4 (older version) dotted decimal notation
  - Four 8-bit numbers separated by dots
  - 10101100 00010000 00000000 01100100 -> 172.16.0.100
- IPv6 notation
  - 8 groups of 4 hexadecimal digits each separated by colons
  - 2001:0DB8:0000:0000:0000:ff00:0042:8329

---

## Details on Communication
- Source or sender (host/end system)
  - generates data to be transmitted
- Transmitter (router/switch)
  - Converts data into transmittable form (signals)
- Communication medium
  - Carries data (in the form of signals)
- Receiver (router/switch)
  - Converts signals into data
- Destination or receiver (host/end system)
  - Receives data

## Medium of communication
Networks may use different communication media
- Wired network
  - Co-axial cables, fiber-optic cables
- Wireless network
  - Wifi, Bluetooth

## Who is connected to whom?
Every computer can directly commincate with every other computer
- <font color="#A72608">**Mesh** topology</font> 
  - Each computer connected to every other computer
- <font color="#A72608">**Bus** topology</font> 
  - All computers connected to common bus

We can always get to a computer via another
- <font color="#A72608">**Ring** topology</font> 
  - Each computer connected to two neighbors
- <font color="#A72608">**Star** topology</font> 
  - Computers connected to central hub/computer through spokes
- <font color="#A72608">**Extended star** topology</font> 
  - Improves scalability of star topology

---

## How large is a computer network?
Network scale can vary...
- Within **1 square meter** or so
  - Personal Area Network (<font color="#A72608">PAN</font>)
    - Medium: Wifi/Bluetooth
- Within **room, building or single campus**
  - Local Area Network (<font color="#A72608">LAN</font>)
    - Medium: cox cable/wired
- **City Wide**
  - Metropolitan Area Network (<font color="#A72608">MAN</font>)
    - Medium: coax cable/fiber/wireless medium

- **Country or continent** wide and beyond
  - Wide Area Network (<font color="#A72608">WAN</font>)
    - Medium: telephone lines/satellite

---

## Network architecture/model
- Central computer provides services and resources
- Other computers request for services and resources
- Client-server model (online banking)

- **Peer to peer model**
  - All computers in network are equal ... no hierarchy
  - BitTorrent
    - A given computer can be both a **provider** of data or services and a **consumer** of data or services 

---

## Network software
- Special software is needed on a computer to enable networking
  - To enable sending/receiving of data to/from a given computer
- Computer initiating data transfer -> sender/source computer
- Eventual recipient of data -> receiver/destination computer

## Design Goals
Realiability -> should operate correctly <br>
Security -> should provide data protection <br>
Resource sharing -> should efficiently share available network resources <br>
Scalability -> should be able to support increase in size

## Network Software Design
- Layered design used to manage complexity of software
  - Divide responsibilities among different layers
- Each layer
  - Abstracts set of services (hides underlying details) & provides well-defined interface to layer above it
  - Directly interacts only with layer immediately below and above it

## Layered Approach
- Data travels from top to bottom layer on sender side (Host 1)
- Data travels from bottom to top layer on receiver side
- Each layer uses protocols for interaction with same layer in other computers
  - Alothough there is no direct interation layer n of one computer understands information communicated by later n on other computer
