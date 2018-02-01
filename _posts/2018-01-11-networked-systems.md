---
layout: post
title:  "Networked Systems H"
date:   2018-01-10 18:50:00
categories: Level3 Semester2
author: dasha
---

### Introduction

###### Networked System: Autonomous computing devices that exchange data to perform some application goal and how they communicate across a network

* internet
* digital broadcast
* mobile voice telephony
* sensor networks
* controller area networks
<!--excerpt-->

Communication: Messages transferred from source to destination(s) via some communications channel  
   How would you convert a message so that both source and destination understand it?  
   Limitations:
   
* size of messages is bounded on a channel at any one time
* simplex - send/receive in only one direction (broadcasting)
* half-duplex - send or receive, but not simultaneously (wifi)
* full-duplex - send and receive at the same time (two cables, for sending and receiving)

###### Information:

* information theory - amount of info in a message can be characterised mathematically
* capacity of channels can be modelled - physical limits exist here (amount, speed, power)

###### Signals:

* the physical form of a message - usually a wave
* analogue - smooth continuation of values
* digital - sequence of discrete symbols
* coding - mapping information to symbols

Analogue:

* amplitude directly codes value of interest
* can be arbitrarily accurate
* susceptible to noise and interference
* difficult to process with digital electronics
  * sample the signal at a suitable rate
  * quantise to nearest allowable discrete value
  * convert to digital representation
  * **sampling theorem** dictates rate of sampling
  
Digital:

* fixed alphabet
* underlying channel is almost always analogue
* modulation - map a digital signal onto the channel
* uses binary encoding

###### Networked systems often use non-binary encoding:

* complex modulation schemes with either 16, 64 or 256 possible symbols
* baud rate - number of symbols transmitted per second
  * can differ from bit rate
  
###### Channels and Network Links:

* signal may be directly conveyed or modulated onto an underlying carrier
* link - the combination of signal and channel
  * directly connects 1+ hosts (ethernet)
  * network comprises several links connected together (WAN)
  * switches/routers - connects the links
  
###### Circuit Switched Networks:

* dedicated circuit for A and B to communicate
* exchange arbitrary length messages
* guaranteed capacity once circuit is created
* can block other communications
* capacity of network gives blocking probability
* traditional telephone network

<img src="/cs-notes/assets/images/ns/circuit_switched.jpg" nopin="nopin" />

###### Packet Switched Networks:

* messages split into small packets before transmission
  * size constraint
* A-B and C-D can communicate all the time
* share bottleneck link
* connectivity guaranteed
* available capacity varies based on other people on the network
* internet

<img src="/cs-notes/assets/images/ns/packet_switched.jpg" nopin="nopin" />

All networked systems are build using these basic components:

* hosts - source and destination(s)
* links - physical realisation of channel
* switches/routers - connect multiple links

###### Network Protocols

Network protocols give meaning to the messages that are exchanged  
   Messages follow some well known **syntax**, and have agreed **semantics**
   
* an agreed language for encoding messages
* rules defining what messages mean and when they can be sent
* define the network behaviour

Syntax: 

* protocol data units (PDU) - types of message
* each PDU has a particular syntax
  * decribing what info is included and how it's formatted
  * may be formatted as textual info or binary data
    * textual PDU - has syntax and grammar that describes its format
	* binary PDU - similar rules
* define what messages are legal to send

Semantics:

* define when PDUs can be sent, and what response is needed
  * who can send and when
  * host roles
  * what the communicating entities are
  * how errors are handled
* described with state-transition diagram
  * states - stages of protocol operation
  * transitions - in response to PDUs, may result in other PDUs being sent
  
<img src="/cs-notes/assets/images/ns/state_transmission.jpg" nopin="nopin" />

###### Morse Code:

* signals on electrical cable form a channel
* syntax - pattern of dots and dashes
* semantics - different gap lengths to signal end of word, and "STOP" for end of message

###### Protocol Layering:

* organisation of communications systems (means of abstraction)
* structured design reduces complexity
* services - offered by a layer to the next higher layer
* well defined interfaces
  * highest layer is communicating application
  * lowest layer is physical communication channel
* peers at a layer `i` communicate using layer `i` protocol
  * using lower layer services
  
Example with a web browser talking to web server:

<img src="/cs-notes/assets/images/ns/protocol_layering.jpg" nopin="nopin" />

###### OSI Reference Model:

* standard way of thinking about layered protocol design
* design tool

<img src="/cs-notes/assets/images/ns/osi.jpg" nopin="nopin" />

###### Physical Layer:

* defines characteristics of cable/optic fibre
  * size and shape of plugs
  * cable length
  * type of cable
    * electrical voltage
	* current
	* modulation
  * type of fibre
    * single or multi-mode
	* optical clarity
	* colour
	* power output
	* modulation of laser
* wireless
  * radio frequency
  * transmission power
  * modulation scheme
  * antenna type
  
###### Data Link Layer:

* structure and frame physical layer bit stream
  * split bit stream into messages
  * detect/correct errors
* perform media access control
  * assign addresses to hosts
  * arbitrate access to link
  * detemine when hosts can send messages
  * ensure fair access to link - flow control
* ethernet

###### Network Layer:

* interconnects links to form a WAN from source host --> destination host
  * data delivery
  * naming and addressing
  * routing
  * flow control
* IP

###### Transport Layer:

* end-to-end transfer of data from source --> destination
  * between session level service at the source, and corresponding service at the destination
  * provides reliability, ordering, framing, congestion control
* TCP

###### Session Layer:

* manages transport layer connections
* functions
  * open TCP/IP connections to download webpage with HTTP
  * use SMTP to transfer email messages over a TCP/IP
  * coordinate control, audio and video flows for video conference
  
###### Presentation Layer:

* manages presentation, representation and conversion of data
  * character set
  * data markup langs.
  * data format conversion
  * content negotiation
  
###### Application Layer:

* user application protocols (not the app. programs themselves)
* REST APIs/WebRTC

###### Protocol Standards:

* formal description of a protocol
* ensure interoperability of diverse implementations
* set procedures
  * open or closed standards development process
  * free or restricted standards availability
  * rules around disclosure of intellectual property rights
  * individual vs corporate vs national membership
  * lead technical dev. vs describing existing practices
  * collaborative vs combative process
* standards organisations
  * Internet Engineering Task Force
  * International Telecommunications Union
  * 3rd Gen Partnership Project
  * World Wide Web Consortium
  
  
### Physical and Data Link Layers

###### Physical Layer:

* concerned with transmission of raw data bits
  * type of cable/wireless link
  * encoding bits onto that channel
  * capacity of the channel
  
###### Wired Links:

* characteristics decided by standards bodies
* size and shape of plugs
* max cable length
* type of cable - electrical voltage, current, modulation
* type of fibre  - single/multi-mode, optical clarity, colour, power output, laser modulation

###### Unshielded Twisted Pair:

<img src="/cs-notes/assets/images/ns/unshielded.jpg" nopin="nopin" />

* 2 wires twisted together
* each pair is unidirectional
* twists reduce interference and nosie pickup (by shielding each other)
  * more twists --> less noise
* several miles of cable length possible at low data rates
  * longer cable --> more noise
* ethernet, telephone lines

###### Optical Fibre:

* glass core and cladding in plastic jacket for protection
* unidirectional data
  * transmission laser at one end
  * photodetector at the other end
* light travels down the fibre
* electromagnetic interference doesn't affect light --> very low noise
* 10s of Gbps over 100s of miles --> very high capacity
* cheap to make
* relatively expensive lasers required to operate

###### Wired Data Transmission:

* signal directly encoded onto channel
  * occupies baseband region
  * bandwidth is the frequency range used by signal

###### Baseband Data Encoding:

* encoded by varying the voltage in the cable/intensity of light in the fibre
* encoding schemes - NRZ, NRZI, Manchester, 4B/5B

<img src="/cs-notes/assets/images/ns/baseband.jpg" nopin="nopin" />

###### 4B/5B Encoding:

* Manchester encoding is inefficient - only 50% of link capacity is used
* so, insert extra bits to break up sequences of the same bit
  * each 4-bit data symbol changed to a 5-bit code for transmission, and reversed at the receiver
  * then transmit 5-bit codes using NRZI
* this way, 80% of link capacity is used
* ethernet 
  * 10Mbps with Manchester
  * 100Mbps with 4B/5B
  
###### Wireless Links:

* use carrier modulation
* performance affected by
  * carrier frequency
  * transmission power
  * modulation scheme
  * type of antenna
  
###### Carrier Modulation:

* carrier wave applied to channel at frequency F
* signal modulated onto carrier
* shifts signal from baseband to a higher carrier frequency
* allow multiple signals on a single channel
* can be used on wired links (ADSL and voice telephones sharing a phone line)

###### Amplitude, Frequency, Phase Modulation:

<img src="/cs-notes/assets/images/ns/afpm.jpg" nopin="nopin" />

###### Complex Modulations:

* use multiple levels of the modulated component
  * gigabit ethernet - amplitude modulation with 5 levels instead of binary signalling
* combine modulation schemes
  * vary phase and amplitude --> quadrature amplitude modulation
* complex combinations regularly used

###### Spread Spectrum Communication:

* single frequency channels prone to interference, so
* repeatedly change carrier frequency many times/second
* use pseudo-random sequence to choose which carrier frequency is used for each time slot
  * seed of random generator is a shared secret between sender and receiver
* 802.11b Wi-Fi uses frequencies centered around 2.4GHz with phase modulation

###### Bandwidth and Channel Capacity:

* bandwidth determins frequency range
* digital signals?
  * sampling theorem - to accurately digitise an analogue signal, you need 2H samples/second
  * max transmission rate (R<sub>max</sub>) of digital signal depends on channel bandwidth (H)
  * number of discrete values per symbol (V)
  * R<sub>max</sub> = 2H log<sub>2</sub> V
* this would presumably give a perfect, noise-free channel

###### Noise:

* electrical interference
* cosmic radiation
* thermal noise
* can measure signal power `S` and noise floor `N` in a channel for signal-to-noise ratio `S/N`
  * `dB = 10log10 S/N`
* ADSL modems report `S/N ~30` for good quality

###### Capacity of Noisy Channel:

* depends on noise type
  * uniform/bursty --> affects all or some frequencies
  * Gaussian noise --> noise that impacts all frequencies equally
    * R<sub>max</sub> of Gaussian = Hlog<sub>2</sub>(1 + S/N)
  * dial-up modem bandwidth limitation
  
###### Implication - bandwidth and signal-to-noise ratio limit amount of info. that can be transferred

###### Data Link Layer:

* arbitrate access to physical layer
  * identify devices
  * structure and frame the raw bitstream
  * detect and correct bit errors
  * control access to channel
* turn raw bitstream into structured comms. channel

###### Addressing:

* physical links can be point-to-point/multi-access
  * multi-access requires host addresses to identify senders/receivers
* host addresses - link-local/global scope
  * sufficient to be unique among the devices connected to a link
  * many data link protocols use globally unique addresses
    * simpler to implement if devices can move (don't need to change address when connected to different link)
	
###### Framing and Synchronisation:

* raw bitstream unreliable
  * bits corrupted
  * timing disrupted
* data link corrects these problems
  * break bitstream into **frames**
  * transmit and repair individual frames
  * limit scope of transmission errors
  
###### Ethernet:

<img src="/cs-notes/assets/images/ns/ethernet.jpg" nopin="nopin" />

###### Synchronisation:

* detecting start of message
  * leave gaps between frames
    * but physical layer doesn't guarantee timing
  * precede each frame with a length field
    * but length could be corrupted
  * add **start code** to beginning of frame
    * a unique bit pattern
	* enables synchronisation after an error - wait for next start code, begin reading frame headers
	* start code should generate a regular pattern after physical layer coding
* what if start code appears in data? **bit stuffing** can give a transparent channel
  * sender inserts `0` after sending 5 consecutive `1's` (unless start code)
  * receiver looks at 6th bit if it sees 5 consecutive `1's`
    * if 0, has been stuffed, so remove
	* if 1, look at 7th bit
	  * if 0, start code
	  * if 1, corrupt frame
  * this is a binary-level escape code
  
<img src="/cs-notes/assets/images/ns/stuffing.jpg" nopin="nopin" />

###### Error Detection:

* common in wireless systems
* add error detecting code to each packet
* parity codes
  * calculate **parity** of data
    * odd number of `1's` in data - parity 1
	* even number of `1's` in data - parity 0
	* parity bit is XOR of data bits
  * send parity with data
  * check at receiver
  
[Example](#internet_checksum) - The Internet Checksum

###### Other Error Detecting Codes:

* parity and checksums relatively weak
  * simple implementation
  * undetected errors likely
* cyclic redundancy code (CRC)
  * more complex
  
###### Error Correction:

* extended error detecting codes to correct errors
  * transmit correcting code as additional data in each frame
  * receiver can correct errors without contacting sender
* Hamming code
  * at the sender
    * send `n` data bits and `k` check bits
	* each check bit codes parity for some data bits
	  * starting at check bit `i`
	  * check `i` bits
	  * skip `i` bits
	  * repeat
  * at the receiver
    * set `counter = 0`
	* recalculate check bits `k = 1, 2, 4, 8,...` in turn
	* if `k` incorrect, `counter += k`
	* if `counter == 0`, no errors
	* else, bit `counter` is incorrect
* allows receiver to detect and correct all possible errors that corrupt only a single bit (and some errors affecting multiple bits)
	  
<img src="/cs-notes/assets/images/ns/hamming.jpg" nopin="nopin" />

* other error correcting codes tradeoff copmlexity and amount of data added for the ability to correct multi-bit errors
* can also request retransmission as a way of fixing errors

###### Media Access Control:

* arbitrating access to a link
  * point-to-point typically 2 unidirectional links
    * separate cables for each direction
	* need framing in each direction
	* stop-and-wait/sliding-window for flow control
  * multi-access typically share a bidirectional link
    * single cable - nodes contend for access to link
	* single radio frequency
	
###### Link Contention:

* 2 hosts transmit simultaneously --> collision
* signals overlap --> garbage received

###### Contention-based MAC:

* 2-stage access to channel
  * detect that collision will occur by listening to channel while/before sending
  * send if no collision/back off or retransmit data to avoid collision
* probabilistic, variable latency access to channel

###### ALOHA Network:

* developed at Uni of Hawaii in 1970
* first wireless packet-switched network
* uses contention-based MAC
  * try to transmit whenever data is available
  * if collision occurs, wait random amount of time, then retransmit
* poor performance
  * long delays
  * low channel utilisation
  
###### Carrier Sense Multiple Access:

* when propagation delay low, listen before sending
  * if another transmission active, back off without sending anything
  * if link idle, send data immediately
* improves utilisation
  * only new sender backs off if channel is active
  
###### CSMA/CD:

* high propagation delay --> increased collision rate
* CSMA updated with collision detection 
  * listen to channel before and while transmitting
  * if collision, immediately stop sending, back off, and retransmit
    * collision still corrupts both packets
	* time channel blocked due to reduced collisions
* ethernet, 802.11 Wi-Fi
* how long is back-off interval?
  * should be random
  * should increase with number of collisions that affect a transmission
    * repeated collisions signal congestion
	* reduced transmission rate allows network to recover
  * initial back off interval `x seconds +-50%`
  * each repeated collision before success `x --> 2x`
  
###### Summary - combination of physical and data layers allows transmission of structured frames of data accross a single physical link

### Bridging

###### Link-layer Topology Evolution:

* media access control assumes a single link
  * on wired networks, with a single cable
  * vulnerable to cable damage
* hub - cable in a box
  * no intelligence
  * cable damage disconnects only one single host
    * so doesn't partition the network
* bridge - intelligent device
  * understands media access control protocol 
  * joins multiple links together
  
<img src="/cs-notes/assets/images/ns/bridge_types.jpg" nopin="nopin" />

###### Extending Link-layer Networks:

* hub - physical layer interconnection of links
* equivalent to runnning a longer cable
* doesn't improve network scalability

* bridge - data layer interconnection of physical networks
* understands and processes data link layer frames
* identifies hosts
* forwards frames of interest
* automatic - no configuration needed
* eg ethernet switches

###### Bridge Operation:

* learn addresses on each link
  * observe sources of packets
  * has **soft-state** timeout to respond to failure/node mobility
* forward traffic as appropriate
  * unicast based on host locations
  * multicast based on group membership
  * broadcast
  
The following are examples of communication on this setup of bridged links

<img src="/cs-notes/assets/images/ns/bridge_operation.jpg" nopin="nopin" />
  
* on initialisation - neither bridge knows location of any hosts
  * host A sends packet for host B
    * received at bridge 1, which now records location of A
    * location of B unknown, so bridge 1 floods packet to all outgoing links
	  * which is also received at bridge 2, which doesn't know location of B
	  * so flood the packet to all outgoing links (plus record location of A)
	* B is one of the outgoing links from bridge 1
	* packet received at B, so responds with a packet for A
	  * received at bridge 1, which knows A's location
	  * directly forward packet without flooding (plus record location of B)
  * later, host E sends packet for host B
    * received at bridge 2, which doesn't know location of B
	* so floods packet to outgoing links (plus records location of E)
	  * received at bridge 1, which knows B's location
	  * directly forward packet to B (plus record how to reach E)
  * over time, bridges learn location of every host, sending packets without flooding

So:

* learning protocol - finds hosts without config
* flooding - ensure connectivity maintained even with no knowledge
* performance never worse than a hub
* use of soft state and timeouts - ensure knowledge of failed devices disappears
* poor scalability - every bridge knows about every host

###### Loops in Bridged Networks:

<img src="/cs-notes/assets/images/ns/bridge_loops.jpg" nopin="nopin" />

* host A sends packet for host X, which does not exist
  * received at bridge 1, which doesn't know X's location
  * flood to outgoing links
    * received at bridges 2 and 3, which also don't know X's location
	* flood to outgoing links
	  * packets cross in transit between bridge 2 and 3
	  * causes a loop unless countermeasures taken
* solution - build **spanning tree** over network
* forward packets along tree
* model as an undirected graph `G`
* tree over that graph comprised of all vertices and some edges of `G`
* edges removed to eliminate loops
  * leaves minimal edges that still connect to all vertices
* so, previous graph now looks like this:

<img src="/cs-notes/assets/images/ns/bridge_spanning.jpg" nopin="nopin" />

###### Spanning Tree Algorithm:

* developed by Radia Perlman
* each bridge has globally unique address
  * root bridge has lowest address
  * periodically, each bridge informs its neighbours what it thinks the root's address is
* determined root port - port with shortest path to root bridge
  * each bridge has one except the root
* for each LAN, select a **designated bridge** for it - bridge with shortest path to root (tie-break based on address)
  * **designated port** - port connecting the designated bridge to LAN
* enable all root ports and designated ports
* disable all other ports
* forward traffic through enabled ports

<img src="/cs-notes/assets/images/ns/spanning_tree_alg.jpg" nopin="nopin" />

So:

* bridge 1 is root
* root ports are `2/1` and `3/5`
* designated bridges are
  * 1 for hosts A, B, H and links α and β
  * 2 for hosts F, G and link γ
  * 3 for hosts C, D, E
* designated ports are
  * bridge 1: `1/1`, `1/2`, `1/3`, `1/4`, `1/5`
  * bridge 2: `2/2`, `2/3`, `2/4`
  * bridge 3: `3/2`, `3/3`, `3/4`
* port `3/1` is neither a root nor designated
  * it is **disabled**

# Algorhyme

**I think that I shall never see  
   A graph more lovely than a tree.  
   A tree whose crucial property  
   Is loop-free connectivity.  
   First the root must be selected.  
   By ID it is elected.  
   Least cost paths from root are traced.  
   In the tree these paths are placed.  
   A mesh is made by folks like me.  
   Then bridges find a spanning tree.**
   
### Internetworking

###### Role of Network Layer:

* first end-to-end layer in OSI reference model
* end-to-end delivery of data
  * across multiple link-layer hops
  * across multiple autonomous systems
* building an internet (interconnected networks - **not** capitalised, just a noun)
  * each network administered separately (autonomous - makes independent policy and tech choices)
  
###### Components of an Internet:

* common end-to-end network protocol
  * seamless service to transport layer
* set of gateway devices (routers)
  * implements said protocol
  * hides differences in link layer technologies
  * must perform least amount of translation necessary
  * framing, addressing, flow control, error detection/correction
  
###### The Internet (capitalised, proper noun):

* globally interconnected networks running the **Internet Protocol**
* 1965 - packet switching
* 1969 - wide-area packet networks
* 1973 - first non-US ARPANET sites
* 1974 - initial version of IP
* 1981 - access to ARPANET from non-DARPA-funded sites
* 1983 - IPv4
* 1992 - development of IPv6

###### Internet Protocol:

* packet delivery service
* provides abstraction layer
* simple, best effort, connectionless
* uniform network and host addressing, uniform end-to-end connectivity, fragmentation and reassembly
* global standard
* the protocol stack is hourglass-shaped

<img src="/cs-notes/assets/images/ns/protocol_stack.jpg" nopin="nopin" />

###### IP Service Model:

* connectionless - just send
* best effort - no guarantees on packet delivery success
* easy to run over any type of link layer
* can easily simulate a circuit over packet, but simulating packets over a circuit is difficult

###### Versions:

* IPv4 - current production Internet
* IPv6 - next gen Internet
* IPv5 - experimental multimedia streaming protocol

IPv4 packet format:

* 32-bit addresses
* will router fragmented packets that are larger than MTU
* header contains checksum to detect transmission errors
  * protects header only, not payload data

<img src="/cs-notes/assets/images/ns/ipv4.jpg" nopin="nopin" />

IPv6 packet format:

* simpler header format
* 128-bit addresses
* removed support for fragmentation
  * hard to implement for high rate links
  * end-to-end principle
* added flow label for DSCP
  * groups related traffic flows together
* no header checksum
  * assumes data protected by a link layer checksum

<img src="/cs-notes/assets/images/ns/ipv6.jpg" nopin="nopin" />

###### Addressing:

* every network interface on every host has a unique address
  * hosts may change it over time to give illusion of privacy
  
###### Fragmentation:

* link layer has maximum packet size (MTU)

###### Loop Protection:

* packets include a forwarding limit
  * non-zero when packet is sent
  * each router that forwards the packet reduces this value by 1
  * if 0 reached, packet discarded
* stops packets circling forever in case of network error

###### Differentiated Services:

* end systems can request special service from the network
  * ask for low latency over high bandwidth
  * emergency traffic prioritised
  * background software updates asking for low priority
* signalled by differentiated service code point (DSCP) in the header
* provices hint to network, not a guarantee
  * often stripped at network boundaries
  * economic and network neutrality issues - who can set the DSCP?
  
###### Explicit Congestion Notification:

* typically routers respond by dropping packets
  * TP's can detect the loss and request retransmission if necessary
* notification gives routers a way to signal approaching congestion
  * if ECN == 00, notification is disabled
  * if a sending host sets ECN = 10 or 01, routers will monitor link usage
  * ECN == 11 signals need to reduce sending rate (congested)
  
###### Header Checksum:

* used to detect transmission errors

###### Transport Layer Protocol Identifier:

* network packets include transport data as payload
* must identify what protocol the transport layer uses
  * TCP = 6
  * UDP = 17
  * DCCP = 33
  * ICMP = 1
  
###### IPv4 or IPv6:

* IPv4 has insufficient addresses left
* primary goal of IPv6 is to increase size of address space - allow more hosts on network
* it also simplifies the protocol - high-speed implementations easier
* straight-foward to build apps that work with both versions
* DNS query `getaddrinfo()` returns version used

###### IP Addressing:

* how to name hosts in a network
  * does the address name the host, or its location at which it's attached to the network?
* how they should be allocated
  * hierarchical
  * flat
* address format
  * human/machine readable
  * structured/unstructured
  * fixed length binary
    * easier and faster for machines to process
  * variable length textual
    * easier for humans to read
  * size
  
###### Identity and Location:

* give hosts a consistent address, irrespective of their location
* simple upper-layer protocols
  * transport and app unaware of multi-homing or mobility
* leave complexity to network layer
  * must determine location of host before it can route data
  * requires in-network DB to map identity to routable addresses (eg mobile phone numbers)
* alternatively, address can indicate a host **location**
  * address structure matches network structure (eg geographic phone numbers)
  * simplifies network layer
  * multi-homing/mobility must be handled by transport or apps (transport layer connections break when the host moves)
  
###### Address Allocation:

* hierarchical
  * allows routing on aggregate addresses
    * eg +1 703 243 9422
	* look at `+1`, know to route to US instantly
  * forces address structure to match network topology
  * requires rigid control of allocations
* flat
  * flexible allocations
  * no aggregation --> not scalable
  
###### IP Addresses:

* specify location of a network interface
* allocated hierarchically
* fixed length binary values
* domain names are a separate **app level** namespace
* both IPv4 and IPv6 addresses encode location
  * **netmask** describes number of bits in network part of address
  * network itself has the address with the host part equal to 0
  * broadcast address for a network has all bits of host part equal to 1
  * a host with several network interfaces will have one IP address per interface
    * eg laptop with Ethernet and WiFi interfaces will have 2 IP addresses

###### IPv4 Addresses:

* 32-bit
* IP address - `130.209.247.112 = 10000010 11010001 11110111 01110000`
* netmask - `255.255.240.0 = 11111111 11111111 11110000 00000000`
  * the `1's` are 20 bits long which refer to the network (130.209.240.0/20)
* broadcast address - `130.209.255.255 = 10000010 11010001 11111111 11111111`
* management - IANA administers the pool of unallocated addresses (4,294,967,296)
  * assigned to regional Internet registries as needed
  * RIRs allocate addresses to ISPs and large enterprises within their region
  * ISPs allocate addresses to their customers
* the last available RIR allocation was made on 3rd February 2011

###### IPv6 Addresses:

* provides 340,282,366,920,938,463,463,374,607,431,768,211,456 addresses
* written as 8 separated 16-bit fields with `:` delimiter
* usually written in shortened form (leading 0's in each field are suppressed)
  * a field with all 0's is compressed to `::` (or more)
  * the `::` must not be used to replace a single 16-bit field
* local identifier part is 64 bits
  * last 4 fields
  * can be derived from Ethernet/WiFi MAC address
  * or randomly chosen, with bit 6 set to 0 to give illusion of privacy
* routers advertise the network part, and hosts auto-configure the address
  * first 4 fields
  * split into global routing prefix (up to 48 bits) and a subnet identifier
* deployment issues
  * requires changes to every single host, router, firewall and app
  * many OS have already been updated
  * backbone routers generally support IPv6
  * home routers and firewalls starting to be updated
  * many apps have been updated

###### NAT:

* no host changes
* hugely complicated for peer-to-peer apps
* difficult to debug problems/deploy new classes of app

<a name="internet_checksum"></a>

###### The Internet Checksum:

* sum data values
* send checksum in each frame
* receiver recalculates checksum
  * mismatch --> bit error
* more effective than parity codes
  * detect multiple bit errors
  
```c
#include <stdint.h>
// assume data padded to a 16-bit boundary

uint16_t
internet_cksum(uint16_t, *buf, int buflen) {

  uint32_t sum = 0;
  
  while (buflen--) {
  
    sum += *(buf++);
	if (sum & 0xffff0000) {
	  // carry occured, wrap around
	  sum &= 0x0000ffff;
	  sum++;
	}
  
  }
  
  return ~(sum & 0x0000ffff);

}
```