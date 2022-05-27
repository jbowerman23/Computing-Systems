# UNIX Socket Programming
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7BA1962C6D-8B6E-4FD0-ACC1-B2C3035E7874%7D&file=9-socket_prog.pptx&action=edit&mobileredirect=true)
---

## Delivering the Data: Division of Labor
Network
- Deliver data packet to the destination host
- Based on the destination IP address

Operating System
- Deliver data to the destination socket
- Based on the destination port number

Application
- Read data from and write data to the socket
- Interpret the data

--- 

## Socket: End Point of Communication
- Sending message from one process to another
  - Message must traverse the underlying network
- Process sends and receives through a "socket"
  - The doorway leading in/out of the house
- Socket as an Application Programming Interface
  - Supports the creation of network applications

---

## Two Types of Application Processes Communication
Datagram Socket (UDP)
- Collection of messages
- Best effort
- Connectionless

Stream Socket (TCP)
- In-order, stream of bytes
- Reliable
- Connection-oriented

---

## User Datagram Protocol (UDP): Datagram Socket
UDP
- Single socket to recieve messages       
- No guarantee of delivery                
- Not necessarily in-order delivery      
- Datagram - independent packets         
- Must address each packet   

Postal Mail
- Single mailbox to receive letter
- Unreliable
- Not necessarily in-order delivery
- Letters sent independently
- Must address each mail

---

## Transmission Control Protocol (TCP): Stream Socket
TCP
- Reliable
- Byte stream - in order delivery
- Connection-oriented - single socket per connection
- Set up connection followed by data transfer

Telephone Call
- Guaranteed delivery
- In order delivery
- Connection oriented
- Setup connection followed by conversation

---

## Socket Identification
Receiving host
- Destination address that uniquely identifies host
- IP address: 32-bit

Receiving socket
- Host may be running many different processes
- Destination port that uniquely identifies socket
- Port number: 16

---

## Client-Server Communication
Client "sometimes on"
- Initiates a rquest to the server when interested
  - Web browser on your laptop or cellphone
- Doesn't commmunicate directly with other clients
- Needs to know server's address

Server is "always on"
- Handles service requests from many client hosts
  - Web server for a website
- Doesn't initiate contact with the clients
- Needs fixed, known address

---

## Knowing what Port Number to use
- Popular applications have well-known ports
  - port 80 for web and for 25 for email

- Well known vs ephemeral port
  - Server has a well known port 
    - Between 0 and 1023
  - Client picks and unused ephemeral (temporary) port
    - Between 1024 and 65535

- "5 tuple" uniquely indentifies traffic between hosts
  - Two IP addresses and two port numbers
  - Underlying transport protocol

---

## Domain names
- Most people can't remember numbers
  - Prefer names
- Requeires software (DNS) to translate easy to remember names into IPv4 address/port numbers
- https://google.coom <--> 108.177.122.139 | port 80

---

## UNIX Socket API
- In UNIX everything is like a file
  - All input is like reading a file
  - All output is like writing a file
  - File is represented by an integer file descriptor

- API implemented as system call
  - Connect, send/write, receive/read, close, etc... 

