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
