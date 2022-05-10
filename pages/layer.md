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

---

## Logical Unit of Data Transfer is a frame
- For this concept to work there needs to be an understanding between: 
  - The link layers on the sender and receiver sides on what the formats of the header and trailer are so tthe receiver can identify frame boundaries
    - Needs a link layer protocol that is understood by both computers

---

## Framing Ideas
---

## Byte Count
- Field in header part of the frame specifies the number of byte within a frame

## Flag Bytes with Byte Stuffing
- Each frame starts and ends with special bytes
  - Could use same byte - **<font color="#A72608">flag byte</font>** - for start and end
  - If receiver sees two consecutive flag bytes
    - End of one frame and beginning of next frame

## Possible Problems with Byte Stuffing
- What is the flag byte happens to occur within the original data/payload?
  - **<font color="#A72608">Byte stuffing</font>** - inserts special **<font color="#A72608">escape byte</font>** before flag byte
- What is the escape byte itself happens to occur as aprt of the original payload?
  - Escape byte itself can be escaped with another escape byte if necessary

## Flag Bits with Bit Stuffing
- Like byte stuffing
  - Each frame starts and ends with special sequence of btis
  - Difference is the sequence of bits doesn't need to be 8 bits long (1 byte long)
    -  If flag bits occur in data itself bit stuffinf is used
      - Similar in the concept to byte stuffing, it tells the receiver to treat the accidental flag bits as part of data

- Old protocol called **HTLC** uses the bit pattern 0x7e (01111110) as the flag bits
- Whenever link layer sees a sequence of five 1's in the data (11111), it stuffs a 0 bit after the sequence of five 1's
  - Ensures there will never be a sequence of six 1's in the original data on the receiver side
  - In byte/bit stuffing, frame lengths vary based on payload

## Physical Layer Coding Violations
- **Encoding** bits as signals (responsibility of physical layer) includes redundancy
  - Some signals can never actually occur within the data itself
  - Use these **"reserved"** signals as frame delimiters
  - In practice its possible that the link layer protocol may decide to use a combination of multiple methods
    - Ethernet uses a 72-bit long pattern called a preamble at the beginning of every frame
      - This preamble is also followed by a byte count for the frame

---

## How does Link Layer perform Error Control?
- Recall error control is needed because its possible that the transmission medium introduces errors in the bit stream ... resulting in certain btis flipping (0 to 1)
- This flip could result in frame header/trailers information to be wrong
- Frame header/trailers include information for error detection and possibly error correction to correct certain types of transmission errors

## Error Detection
Idea: Include information along with the data that can help the link layer on the receiver side detect whether certain kinds of transmission errors have occured
- If an error occured, reciever can request a re-transmission of that data
- Error detecting codes
  -  Parity
  -  Checksum
  -  Cyclic redundancy check
- Useful for transmission media where errors are rare (like fiber optics)
- Something like wireless medium that are prone to trans mission errors due to noise
  - End up with way too many retransmissions so you would need error correction as well

## Error Correction
- These are codes tha can not only allow the receiver to detect but also correct certain types of transmission errors
- More complex
- Error correcting codes
  - Hamming code
  - Reed-Solomon code
- Useful for transmission media where error occur often
