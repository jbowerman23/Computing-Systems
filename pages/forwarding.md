# IP Forwarding & Subnetting
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7BE625E7F5-B22B-4232-AC92-48ECF7700415%7D&file=9-IP-Forwarding-Subnetting.pptx&action=edit&mobileredirect=true)
---

### IP Addresses Review
- Defining feature of IP is an IP address
  - IPv4 -> 32 bit address
- IP address uniquely identifies a network interface
  - Host typically has one network interface -> one IP address
  - Routers have multiple network interfaces -> multiple IP addresses
- IPv4 addresses are represented as dotted decimal notation
  - Four 8-bit numbers (octets) separated by dots
  - 10101100 00010000 00000000 01100100 -> 172.16.0.100

Can be public or private <br>
**Public**
- Represent valid destinations on the internet
- Globally known IP addresses

**Private**
- Can be used freely within just private networks
  - Home, mail company, etc
- Still need public IP addresses to connect to the Internet
  - Will need a Network Address Translation (NAT) to translate private to public IP

---

### Public IP Adresses
- Since public IP addresses need to be unique across the internet they can't just be assigned randomly
- Public IP addresses are allocated and managed hierarchically
  - An org know as Internet Assigned Numbers Authority (IANA) owns the entire IP address space
  - IANA delegates blocks of addresses to regional authorities called Regional Internet Registries (RIR)

- RIR delegates smaller blocks of IP addresses within the blocks they are given to ISPs/organizations
- ISPs/organizations assign addresses to customers/computers

---

### IPv6 Addresses
- Future of the Internet Protocol
  - 128-bit addresses
IPv6 notation
- 8 groups of 4 hexadecimal digits each separated by colons
  - 2001:0DB8:0000:0000:0000:ff00:0042:8329
- Still long so often leading zeros are omitted
  - 2001:DB8:0:0:0:ff00:42:8329
- Con omit groups of zeros altogether
  - 2001:DB8::ff00:42:8329

### Biggest issue with IPv6
- Wide-scale deployment of IPv6
  - Deployment has started way back in the late 90's
  - Now deployment has started to progress in a somewhat exponential manner
- Antricipated that IPv6 and IPv4 will have to co-exist for several more years
  - Communication between computers with IPv4 and IPv6 addresses must be reconciled

---

### Review
- To make management and organization more convenient
  - IP addresses assigned to nodes in each network are not just assigned randomly

- IP addresses are allocated in contiguous blocks called prefixes
- Most significant L bits in the address form a prefix or netowkr address
  - Indentifies an entire network of nodes that have consecutive IP addresses
- Remaining (32-L) bits identify host within that network
  - Such a netwokr of consecutive IP addresses is called a subnet
  - There can be 2^(32-l) - 1 hosts in the subnet
  - In reality some of the IP addresses within a subnet are reserved for special cases so the actual # is a little bit less

**Prefix representation**
- Using what is called slash notation
- /prefix length in bits -> /24 for 24-bit prefix

A network of computer addresses can be represented using
- Start address within network/length of prefix in bits
  - 172.16.0.0/24
- Represents a subnet where
  - First IP address is 172.16.0.0 since we have 24 bit prefix that means
  - Least significant 8 bits form the host identifier
  - Addresses range from 
    - 172.16.0.0 to 172.16.0.255
    - 172.16.0.0000 0000 -> 172.16.0.1111 1111

---

### Subnetting
- Like the way the IANA divides the entire range of available IP addresses into smaller block to assign to Regional Internet Registers
- As well as like the way RIR's further divide these blocks into smaller blocks for different ISP's and Orgs
- An individual Org can also partition its own block of IP addresses
  - Orgs create smalled subnet within their assigned subnet
- Consider a university network 128.208.0.0/16
  - University could use these least signigicant 16 bits to assign sequential IP addresses
    - Starting from all zeros to all ones in those 16 bits

**Uni network 128.208.0.0/16**
- May be more useful to divide network into smaller subnets
- Could provide for better organization and management
  - Different subnets for different departments
- Uni could decide to divide subnet based on number of maximum hosts in department

- EE department needs at most 16,380 host IP
  - 2^14 = 16380
- Needs the least sig 14 bits in order to create at least 16380 unique consecutive IP addresses within this subnet
- All hosts inside the EE subnet have the same prefix
- Uni needs to fix the values for these two bits for EE subnet
  - Means uni decides that all EE addresses will start with 00 in these two positions

- CS department may need larger chunck of IP addresses
- Uni decides that CS may beed at most 3200 unique IP addresses
  - 2^15 = 32000

- CS:. Needs the least significant 15 bits in order to create at least 32,000 unique consecutive IP addresses within this subnet
- All hosts inside the CS subnet have the same prefix
- University needs to fix the values for this one bit for CS subnet
- Means university decides that all CS addresses will start with 1 in this position

- Art department smaller chunck of IP
- 2^13 = 8000
- All hosts inside ART subnet have same prefix
- Uni needs to fix values for these three bits for art subnet

- E.g., consider a university network 128.208.0.0/16
  - EE.: 10000000 11010000 00|xxxxxx xxxxxxxx
  - CS:  10000000 11010000 1|xxxxxxx xxxxxxxx
  - Art: 10000000 11010000 011|xxxxx xxxxxxxx

- Subnet with shorter prefix
  - Larger block of IP addresses are within that subnet
    - Larger block of IP addresses share that same prefix
  - Less specific prefix

- Subnet with longer prefix
  - Smaller block of IP addresses are within that subnet
  - More specific prefix - bc it is longer

---

### IP Forwarding
- Router looks at the destination IP address within the packet and forwards the packet to an appropriate node based on this destination IP address
- All IP addresses on a single subnet will have the same prefix
  - Router outside subnet only needs to look at the prefix
  - Only when you reach a router within subnet you care about host identifier
  - Can combine destination addresses within subnet
  - Routing tables only need to store just one entry for each prefix

- When router recieves a packet; Router mathces destination IP address w/ prefixes in table
  - In order to extract just the prefix bits from a destination IP address
  - Router performs a bit-wise AND operation on the IP address and subnet mask to extract prefix bits
  - Subnet mask contains 1's in all prefix bits and 0's for all host bits

- Routing or forwarding tables of a router typically also store corresponding subnet masks for each prefix entry



<img width="528" alt="Screen Shot 2022-05-23 at 10 23 49 AM" src="https://user-images.githubusercontent.com/102563482/169874187-dcae18ec-582f-4ea7-a660-27a31b5d6934.png">
<img width="524" alt="Screen Shot 2022-05-23 at 10 24 06 AM" src="https://user-images.githubusercontent.com/102563482/169874224-e846699a-5d3b-4c54-bc53-dbf36f5c6fac.png">
<img width="615" alt="Screen Shot 2022-05-23 at 10 24 26 AM" src="https://user-images.githubusercontent.com/102563482/169874280-51adac0b-1334-4f99-aaf5-43f2644271c8.png">


