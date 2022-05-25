# Transport Layer
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B689DDC5D-DB38-4626-A6F5-5C59AA594345%7D&file=9-Transport-Layer.pptx&action=edit&mobileredirect=true)
---

### Transport Layer Basics
- Provides logical end-to-end communication between source and destination
- Runs entirely on host computers
  - Transport layer data is not examined by any node between source and destination nodes
  - Network layer protocols run on hosts and routers (intermediate nodes)

#### Purpose of Transport Layer
- Supports concurrent network usage by multiple application processes on the hosts
  - Provides logical end to end communication between specific application processes on these hosts
  - Both file transfer and email applications can use network services at a given time
  - Provides clean interface for all these processes to use
- Transport layer uses underlying network services and can enchance the services in several ways

- Can provide connection oriented or connectionless service depending on protocol
- Some transport layer protocols can provide additional features
  - Realiability (even on top of an unreliable netowrk)
  - Flow control
  - Congestion control

---

### Supporting multiple processes
- In order to support multiple processes on each host the Transport layer needs to identify a specific process within a host
  - It does so by using a **Port** number
  - Known as Transport Service Access Point
- Host address + process port number -> **socket**

---

### USer Datagram Protocol (UDP)
Unreliable (best-effort) service
- Possible that some segmets of a message may get lost
- Possible that segments may arrive in the wrong order at destination

Connectionless
- Each segment of a message is transmitted to destination independently of other segments of same message

- Limited error control
- No flow control or congestion control
- Simple protocol that does not do much beyond what the network layer already provides

Suitablke for:
- Simple request response communication with limited concern for error/flow control
  - Cheap and efficient
- Useful for applications that want to handle error/flow control in their own way within the application layer
- Great for multicast or broadcast communication

---

### Transmission Control Protocol (TCP)
- Provides stream service
  - Allows potentially infinite stream of data to be transmitted between two application processes
  - Reliable, connection-oriented service
    - Ensures entire stream of data is delivered to receiving application processes
    - Ensures stream of data is delivered to destination application processes that same order as it was sent
- Flow control
- Congestion control
- Has significant overhead
  - Suitable for applications that need this degree of reliablity

#### Connection-Oriented
- Host 1 wants to communicate with host 2 will attempts to establish connection with host 2
- Host being connected to (host 2) must be ready to accept incoming connection requests
  - Listen or passive open state
    - Application process on host 2 is ready to accept incoming connections on certain port numbers
- Host that wants to establish connection(host 1)
  - Connect or active open state
- Server is in passive open state and clients can establish connections with server

---

### Mechanisms Behind Reliable, In-Order Delivery
1. Acknowledgement
  - Receiver sends acknowledgements for each segment that it receives (ACK)
2. Retransmission
  - When segment is sent, retransmission timer started
  - If ACK recieved before timer expires, timer is stopped
  - If timer goes off, segment is retransmitted
  - Sender should set timer carefully

Because sender sends a stream of segments over single connection

3. Sequence number
  - During connection establishment phase initial sequence number is agreed upon form each direction of commination
  - Data bytes sent in one direction are assigned consecutive sequence numbers
  - Every segment simply includes the sequence number of the first byte of data in that segment
  - Segments may be sent out of order(network layer provides unreliable service) but…
  - Sequence numbers are used by receiver to identify correct order of stream!

---

### Connections in TCP
- Requires 3-way handshake to start connection between hosts
  - Host 2 -> passive open state
  - Host 1 -> requests new connection
    - Host 1 sends segment with SYN = 1 & SEQ num = x
    - Host 2 responds with segment with ACK = 1, ACK num = x+1, SYN = 1 & SEQ num = y
    - host 1 sends segment with SYN = 0, ACK flag = 1, ACK num = y+1
  - Connection is now active
    - Now data can be sent back and forth
    - During actualy data transfer
      - The SYN flag remains 0
      - SEQ # is that of first data byte in each segment

#### Terminate Connection
- Connection termination happens independently for each direction of communication
  - When one computer (Host 1) has no more data to send from its side it sends a segment with the FIN = 1
  - Other computer (host 2) acknowledges the FIN segment
  - Communication from Host 1 to Host 2 stops
- Connection termination in TCP consists of pair of two way handshakes

**What is a host sends a segment with FIN = 1 and never recieves an acknowledgement?**
- To avoid host waiting indefinitely for this acknowledgement it will set a timer with it sends out the FIN segment
- If time expires before acknowledgement, then host releases connection

---

### Flow control in TCP
- Flow control ensures sender does not overwhelm reciever
- Mechanism used in TCP is known as sliding window protocol
  - Receiver sets the window field in the header to some number
  - This number indicates how many more sequence numbers beyond the last acknowledged one the sender is allowed to send to the receiver before it must stop and wait for more acknowledgements

---

### Congestion control in TCP
Congestion control is used to avoid/recover from congestion
- Network layer detects congestion and notifies sender
- Transport layer on sender side will adjust transmission rate
- Uses a congestion window to restrict the number of segments it puts into the network  
