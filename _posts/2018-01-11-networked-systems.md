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
  
[Example](#internet_checksum)

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

### Intra-Domain Routing

###### Routing:

* the network layer that routes data from source to destination across multiple hops
* hopping across nodes
  * learn network topology
  * run routing algorithms to determine best path
* end hosts usually only know the local network topology
* gateway devices exchange topology information and decide on best route (routers)

###### Unicast Routing:

* one-to-one transmission
* choice of alg. affected by
  * intra-domain routing
  * inter-domain routing
  * politics and economics
  
###### Routing in the Internet:

* different ISP groups have their own local networks
* some nodes in a group are connected to nodes in another group
* each network is an autonomous system
  * with different technologies and policies
  * distrust each other
  
###### Intra-Domain Unicast Routing:

* routing within an autonomous system (AS)
* no policy restrictions on who determines the topology/which links can be used
* need efficient routing --> shortest path
  * use distance vector - routing information protocol (RIP)
  * use link state - open shortest path first routing (OSPF)
  
###### Distance Vector Protocols:

* each node has vetor containing distance to every other node
  * periodically exchange this info with neighbours
  * routing table "converges" on a steady state
  * unknown distance is ∞
* send packets with least distance to destination
* example
  * <img src="/cs-notes/assets/images/ns/distance_vector_0.jpg" nopin="nopin" />
  * time 0 - nodes initialised, know only their immediate neighbours
  * time 1 - nodes also know neighbours of their neighbours, routing data has spread one hop
  * time 2 - routing data has spread two hops, table complete
  * time 3 - nodes continue to exchange distance metrics in case the topology changes
  * time 4 - link between F and G fails, F and G notices, set the link distance to ∞, pass an update to A and D
  * time 5 - A sets distance to G to ∞, D sets distance to F to ∞, both pass on news of link failure
  * time 6 - C knows it can reach F and G in 2 hops via alternate paths, so advertise shorter routes, network begins to converge
  * time 7 - eventually the network is stable in a new topology, as shown below
  * <img src="/cs-notes/assets/images/ns/distance_vector_7.jpg" nopin="nopin" />
  
###### Count to Infinity Problem:

* if link A-E fails
  * A advertises distance ∞ to E at the same time that C advertises distance 2 to E
  * B receives both, concludes that E can be reached in 3 hops via C, and advertises this to A
  * C sets distance to E to ∞ and advertises this
  * A receives advertisement from B, decides it can reach E in 4 hops via B, and advertises this to C
  * C receives advertisement from A, decides it can reach E in 5 hops via A....
* solution
  1. define ∞ = 16
     * bounds duration of disruption
     * provided the network is never more than 16 hops across
  2. split horizon
     * when updating route, don't send the route learned from a neighbour back to that neighbour
	 * prevents two-node loops
	 * doesn't prevent three-node loops
	 
###### Distance Vector Limitations:

* tries to minimise state at nodes --> slow to converge
* count-to-infinity generally unsolvable - implies distance vector alg. only suitable for small networks

###### Link State Protocols:

* nodes know links to neighbours and cost of using those links
  * link state information
* flood this info.
  * all nodes have complete map of network
* each nodes calculates shortest path to every other node
  * use this as routing table
  
###### Link State Information:

* updates flooded on start-up and whenever topology changes
* updates contain
  * address of sender node
  * list of directly connected neighbours of that node
    * with cost
  * a sequence number
* example
  * <img src="/cs-notes/assets/images/ns/flood_updates.jpg" nopin="nopin" />
  * C sends update to each of its neighbours
  * each receiver compares sequence number with that of the last update from C, if greater, forwards update on all links ecxept the one on which it was received
  * this repeats until eventually the entire network has received the update
  
###### Calculate Shortest Paths:

* nodes use Dijkstra's alg. to find optimal route to every other node
  * shortest path by weight
* [pseudocode](#dijkstra) of Dijkstra's alg.

###### Forwarding and Route Updates:

* static forwarding decision based on weights
  * doesn't take into account network congestion
* recalculate shortest paths on every update
  * occur if a link fails/new link addded
  
###### Distance Vector vs Link State:

* distance
  * simple implementation
  * routers only store distance to each other - O(n)
  * suffers slow convergence - unsuitable for large networks
* link state
  * more complex
  * requires each router to store complete map - O(n<sup>2</sup>)
  * much faster convergence
  
###### Intra-Domain Routing in Practice:

* within any network that operates as a single entity
  * local, nationwide, or worldwide
  * operates a single routing protocol
  * running on IP routers within an AS
  * typically with fibre connections and ethernet
  * exchange routes to IP prefixes, representing regions in the topology
  
### Inter-Domain Routing

* unicast routing
* find best route to destination network
* treat each network as a single node
* route without reference to internal network topology
* each network is an autonomous system
  * eg an ISP that operates a network and wants to participate in interdomain routing
  * some organisations have more than one AS
  * identified by a unique number allocated by the RIR
* routing problem - finding best AS-level path from souce to destination
  * treat each AS as a node on the routing graph
  * treat connections between them as edges
  
###### Default Routes:

* AS-level topology is
  * well connected core networks
  * sparsely connected edges
  * edges get service from core networks
* edge networks can use a default route to the core
* core networks need full routing table - the default free zone (DFZ)

<img src="/cs-notes/assets/images/ns/as_network.jpg" nopin="nopin" />

###### Routing at the Edge:

<img src="/cs-notes/assets/images/ns/edge_routing.jpg" nopin="nopin" />

###### Routing in the DFZ:

Well-connected core networks so need to know about every other network

* DFZ has no default route
* route based on policy (not necessarily shortest path), eg
  * use one AS in preference over another
  * use one AS only to reach addresses in the same range
  * avoid ASes located in a particular country
* requires complete AS-level topology info

###### Routing Policy:

* interdomain routing is between competitors
  * unlikely to trust neighbours
* consider policy restrictions on
  * who can determine your topology
  * which route data can follow
* prefer control over routing, even if it means data doesn't follow the shortest path
  * might pass through an expensive/competitor/political opponent's network
  
###### Border Gateway Protocol:

Internet IDR uses the Border Gateway Protocol (BGP)

* external BGP
  * exchange routing info between ASes
  * neighbouring systems configure an eBGP session to exchange routes
  * runs over TCP between routers
  * used to derive best route to each destination
  * installed in routers to control forwarding
* internal BGP
  * propagate routing info to routers within an AS
  * intra-domain routing protocol handles this
  * iBGP distributes info on how to reach external destinations
  
###### Info exchanged with eBGP:

* routers advertise lists of IP address ranges (prefixes) and their associated AS-level paths
* combined to form a routing table
  * prefix
  * next hop
  * AS path
* example AS topology graph

<img src="/cs-notes/assets/images/ns/as_topology.jpg" nopin="nopin" />

###### eBGP Routing Policy:

* each AS chooses what routes to advertise to neighbours
* doesn't need to advertise everything it receives
* common policy - Gao-Rexford rules
  * routes from customers advertised to everyone
  * routes from peers and providers only advertised to customers
  * ensures AS graph is valley-free 
  
###### BGP Routing Decision Process:

* routers receive path vectors from neighbours giving possible routes to prefixes
  * filtered based on policy
* choose what route to install for destination prefix in forwarding table
  * based on criteria such as policy, shortest path etc
  * doesn't always find a route (policy may prohibit)
  * routes often not shortest path
  * mapping business goals to BGP processes is poorly documented process
  * many operational secrets
  
### The Transport Layer:

* isolates upper layers from network layer
  * hides network complexity
  * hides problems within network
* provides useful, convenient, easy service
  * easy to understand service model
  * easy to use API
    * Berkeley Sockets
	* Compare to Network Layer
* functions
  * addressing and multiplexing
  * reliability
  * framing
  * congestion control
* operates process-to-process, not host-to-host

###### Addressing and Multiplexing:

* NL address identifies a host
* TL address identifies a user process (service with unique TL address) running on a host
* provides demultiplexing point

###### Reliability:

* NL is unreliable
  * best effort packet switching
* TL enhances quality of service provided by network to match application needs
  * appropriate end-to-end reliability
  
###### The End-to-End Argument:

* better to place functionality within network or at end points?
  * put necessary functions within network
    * eg reliability service in TL
	* if not guaranteed 100% reliability, app will have to check data anyway
	* don't check data in network, leave to the end-to-end transport protocol, where check is visible to app
  * this is one of the defining principles of the Internet
  
###### TL Reliability:

* email/file transfer - all data must arrive in the order sent, time of delivery not strict
* voice/video streaming - can tolerate small amount of data loss but requires timely delivery
* NL provides timely but unreliable service
* TL protocol adds reliability if needed

###### Framing:

* apps may wish to send structured data
* TL responsible for maintaining boundaries
  * **frame** original data if this is part of service model
  
###### Congestion and Flow Control:

* TL controls app sending rate
  * congestion control - match rate at which NL can deliver data
  * flow control - match rate at which receiver can process data
* end-to-end, since end points know characteristics of entire path
* email/file transfer - elastic apps, faster is better, but don't care about sending rate
* voice/video streaming - inelastic apps, have min/max sending rates, care about the actual sending rate
* need range of congestion control algs at TL within network constraints

###### Internet Transport Protocols:

* User Datagram Protocol
* Transmission Control Protocol
* Datagram Congestion Control Protocol
* Stream Control Transmission Protocol
* each makes different design choices

###### UDP:

* simplest TP
* exposes raw IP service to apps
  * connectionless
  * best effort
  * framed, but unreliable
  * no congestion control
* adds 16-bit port number to identify services

Service model:

<img src="/cs-notes/assets/images/ns/udp_model.jpg" nopin="nopin" />

Packet format:

<img src="/cs-notes/assets/images/ns/udp_packet_format.jpg" nopin="nopin" />

###### UDP apps:

* for apps that prefer timeliness to reliability
* must be able to tolerate data loss
* must be able to adapt to congestion in app layer

###### TCP:

* reliable byte stream protocol over IP
  * packets contain sequence number to detect loss
  * lost packets are retransmitted
  * data delivered to higher layers in order
  * no gaps
* added congestion control
* adds 16-bit port number as service identifier
* no framing
  * app must impose structure
  
Service model:

<img src="/cs-notes/assets/images/ns/tcp_model.jpg" nopin="nopin" />

Packet format:

<img src="/cs-notes/assets/images/ns/tcp_packet_format.jpg" nopin="nopin" />

###### TCP apps:

* for apps that require reliable data delivery and can tolerate timing variation
* default choice for most apps

###### DCCP:

* unreliable
* connection oriented
* congestion controlled datagram service - alg negotiated at connection setup
* potentially easier for NAT boxes and firewalls than UDP
* adds 32-bit service code in addition to port number
* use for streaming multimeda and IPTV

###### SCTP:

* reliable datagram service ordered per stream
* multiple streams within a single association
* multiple connection management
  * fail-over from one IP address to another for reliable multi-horning
* TCP-like congestion control
* use for telephony signalling ("a better TCP")

###### Deployment Considerations:

* IP agnostic of the TL protocol
* firewalls perform deep packet inspection and look beyond IP header to make policy decisions
  * only secure policy is disallowing anything not understood
  * so difficult to deploy new TPs (DCCP and SCTP) in the Internet
  * so limits future evolution of the network
  
###### Tunnelling New Transports:

* if protocols can't be deployed natively, they can be tunnelled
* UDP passes through NATs and firewalls
* native TPs do not
* so tunnel new transport inside UDP packets

### TCP and Congestion Control

###### Berkeley Sockets API:

* widely-used
* low-level C
* largely compatible cross-platform
* sockets provice standard interface between network and app
  * stream
    * virtual circuit service
	* map onto TCP connections
  * datagram
    * delivers individual packets
	* map onto UDP connections
* independent of network type
  * commonly used with IP sockets, but not actually specific to any protocol
  
###### TCP Sockets:

* server 
  * initialises a file descriptor to a socket, then binds it
  * listens for connections with the file descriptor
  * accepts connections
  * receive/send data across network
  * close connection
* client
  * initialises a file descriptor to a socket
  * connects to open server using the file descriptor
  * receive/send data across network
  * close file descriptor
  
###### TCP Socket Services:

* service differentiation
* connection-oriented
* point-to-point
* reliable, in-order delivery of a byte stream
* congestion control
* provided by OS via the API

###### Client-server or Peer-to-peer?

* sockets initially unbound
* most commonly used as client-server
  * one host listens and accepts connections on a well-known port
  * other host makes the socket connect to that port on the server
  * after connection, either side can send/receive data
* simultaneous connections are possible

###### TCP Port Number:

* server must listen on a known port
* do not distinguish between system and user ports - security problems
* there is insufficient port space available
* usually clients connect from randomly chosen port from ephemeral
  * to prevent spoofing attacks
* 0 - 1023
  * well known system ports
  * used by trusted OS services
* 1024 - 49151
  * registered user ports
  * used by user apps and services
* 49152 - 65535
  * dynamic ephemeral ports
  * for private use
  * peer-to-peer apps
  * source ports for TCP client connections
  
###### Setting up a TCP Connection:

* **3-way handshake**
* happens during `connect()/accept()` calls
  * SYN and ACK flags in TCP header signal connection progress
  * initial packet has SYN bit set
    * includes randomly chosen initial sequence number
  * reply also has SYN bit set and random number
    * acknowledges initial packet
  * handshake is complete by acknowledgement of second packet
* combination ensures robustness
  * random number give robustness to delayed packets or restarted hosts
  * acknowledgements ensure reliability
  
<img src="/cs-notes/assets/images/ns/tcp_setup.jpg" nopin="nopin" />
  
###### Reading/Writing Data over TCP:

* call `send()` to transmit data
  * enqueues data for transmission
  * data split into segments
    * each placed in a TCP packet
	* sent when allowed to by congestion control alg.
	* segments have sequence numbers to be acknowledged by receiver
	* several `send()` requests might be aggregated into a segment
  * blocked until data can be written
  * returns actual amount of data sent
  * returns -1 `errno`
* call `receive()` to read up to BUFLEN bytes of data from connection
  * blocked until some data available/connection is closed
  * returns number of bytes read from socket
  * returns 0 if sender closed connection
  * returns -1 `errno`
  * received data is **not** null-terminated
    * potential security risk
  * data returned doesn't necessarily correspond to a single `send()` call
  
###### Application Level Framing:

* apps must be written to cope with getting data in unpredictably sized chunks from `recv()`
* ideally 
  * all headers are received in one `recv()` call 
  * then parsed to extract Content-Length
  * then entire body is read
* parsing can be complex if TCP splits response arbitrarily

###### TCP is Reliable:

* each packet has sequence and acknowledgement numbers
  * sequence - counts how many bytes are sent
  * acknowledgement - specifies next byte expected to be received
    * cumulative position
	* only acknowledge contiguous packets (neighbouring)
	* lost packets --> receipt of subsequent packets trigger duplicate acknowledgements
	  * retransmitted (invisible to app)
	  
###### How Loss is Detected:

* triple duplicate ACK = 4 identical ACKs in a row
  * some packets lost, but later packets arriving
* timeout = receiver or network path has failed
  * send data but acknowledgements stop returning
  
###### Packet Reordering:

* packet delay --> reordering --> duplicate ACKs received
* gives appearance of loss, when data was merely delayed
* triple duplicate ACK used as indication of packet loss
  * prevent reordered packets causing retransmissions
* packets will only be delayed a little; if delayed enough that a triple duplicate ACK is generated, TCP will treat the packet as lost and send a retransmission

###### Head of Line Blocking in TCP:

* data always delivered in order, even after loss
* a `recv()` for missing data will block until it arrives

<img src="/cs-notes/assets/images/ns/tcp_blocking.jpg" nopin="nopin" />

A complete TCP connection:

<img src="/cs-notes/assets/images/ns/complete_tcp.jpg" nopin="nopin" />

###### Congestion Control:

* adapting transmission speed to match available end-to-end network capacity
* prevents congestion collapse of network - where no useful work is done
* congestion happens when packets send and delivered reaches maximum capacity
* can be implemented at either network or transport layer
  * network
    * safe - ensures all TPs are congestion controlled
	* requires all apps to use same CC scheme
  * transport
    * flexible - TPs can optimise CC for apps
	* misbehaving transport can congest the network
	
###### CC Principles:

* these ensure stability of network
  * conservation of packets
  * additive increase and multiplicative decrease of sending rate
  
###### Packet Conservation:

* network has capacity
  * `bandwidth x delay` is the product of the path
* when in equilibrium at that capacity, send one packet for each acknowledgement received
  * total packets in transit is constant (ACK clocking)
* sending rate automatically reduced as network gets more congested --> delivers packets more slowly

###### AIMD algs.:

* adjust sending rate according to additive increase/multiplicative decrease alg.
  * start slowly and increase gradually to find equilibrium
    * add small amount to sending speed each time there is an interval without loss
	* `wi = wi-1 + α` for each RTT where `α = 1`
  * respond to congestion rapidly
    * multiply sending window by some factor `β < 1` for each loss seen
	* `wi = wi-1 * β` for each RTT where `β = 1/2`
* faster reduction than increase --> stability

###### Internet Congestion:

* transport receives congestion signal from network, either
  1. packet arrives at router but queue for outgoing is full --> packet discarded
  2. packet arrives at router but queue for outgoing is getting close to full, and transport has signalled that it understands ECN --> router sends ECN-CE bit in packet header
* TP detects congestion signal and reacts
  * loss detected by receiver due to gap in sequence number space/receiver notices ECN-CE marker
  * when no congestion signal --> gradual additive increase in sending rate
  * when congestion signal --> multiplicative decrease in sending rate
  * AIMD alg. following the CC principles

###### TCP CC:

* TCP uses window-based CC alg.
  * **sliding window** onto available data - determines how much can be sent according to the AIMD alg.
  * slow start and congestion avoidance
  * gives approx. equal share of bandwidth to each flow that shares a link
  
###### TCP Reno Sliding Window Protocol:

* state of the art in TCP as of ~1990
* stop and wait
  * transmit packet -->  wait for acknowledgement --> send next packet
  * if no acknowledgement after some time --> retransmit
  * limits sender to one frame outstanding --> poor performance
* link utilisation
  * stop and wait takes time `ts` to send a packet
    * `ts = packet size / link bandwidth`
  * acknowledgement returns `tRTT` seconds later
  * link utilisation `U = ts / tRTT` - fraction of the time the link is in use sending packets
    * ideally `U ~ 1.0`
    * eg for gigabit link sending 1500 byte packet from GLA to LON
	  * `ts = 1500 * 8 bits / 10^9 bits per second = 0.000012s`
	  * `tRTT ~ 0.010s`
	  * `U ~ 0.0012`
	  * ie link is in use 0.12% of the time
* sliding window improves on stop-and-wait by sending more than one packet before stopping for acknowledgement
  * allow several frames to be outstanding
  * acknowledgement received --> window slides along one packet
  * how to size the window?
    * should be `bandwidth x delay`, but neither are known to the sender
	
<img src="/cs-notes/assets/images/ns/sliding_window.jpg" nopin="nopin" />

###### Choosing Initial Window Size Winit:

* need to measure path capacity
* start with small window --> increase until congestion
  * `Winit` of one packet per round-trip is only safe option
  * equivalent to stop-and-wait but overly pessimistic
  * modern TCP uses intial window of 10 packets per RTT
    * network capacity increased so Google thinks this is pretty safe

###### Finding Link Capacity:

* how to find correct window for path when new connection starts (slow start)
* how to adapt to changes in available capacity once connection is running (congestion avoidance)
* slow start
  * `Winit = 1` packet per RTT
  * need to rapidly increase to correct value for network
    * each ACK increases window by 1
	* on loss, immediately stop increasing window
  * send two packets for each ACK
  * window doubles on each round trip until loss occurs --> rapidly finds correct window size for the path
  
<img src="/cs-notes/assets/images/ns/slow_start.jpg" nopin="nopin" />

* congestion avoidance
  * mode to probe for changes in network capacity
    * eg sharing connection with other traffic
  * window increased by 1 packet per RTT
  * slow, additive increase
  * until congestion observed --> respond to loss
* detecting congestion
  * TCP uses cumulative positive ACKs --> 2 ways to detect congestion
    1. triple duplicate ACK --> packet lost due to congestion
	2. ACKs stop arriving --> no data reaching receiver --> link failed somewhere
  * how long to wait before assuming ACKs have stopped
    * `Trto = max (1 second, average RTT + (4 * RTT variance))`
* responding to congestion
  * loss by triple duplicate ACK
    * transient congestion but data still being received
	* multiple decrease in window `wi = wi-1 * 0.5`
	* rapid reduction in sending speed allows congestion to clear quickly --> avoid congestion collapse
  * loss by time-out
    * no packets being received for a long time --> significant problem with network
	* return to initial sending window --> probe for new capacity using slow start
	* assume route changed and you know nothing about the new path
	
###### Congestion Window Evolution:

Assuming `Winit = 1`:

<img src="/cs-notes/assets/images/ns/tcp_window_evolution.jpg" nopin="nopin" />

* buffering and throughput
  * `buffer size = badwidth x delay`
  * bottleneck queue never empty
  * bottleneck link never idle --> sending rate varies, but receiver sees continuous flow
  
<img src="/cs-notes/assets/images/ns/tcp_buffering.jpg" nopin="nopin" />

###### Performance and Limitations of TCP:

* TCP CC highly effective at keeping bottleneck link fully utilised
  * provided sufficient buffering in network
  * packets queued in buffer --> delay
  * TCP trades extra delay for high throughput
* unless ECN used, TCP assumes loss due to congestion
  * too much traffic queued at intermediate link --> some packets dropped
  * this is not always true
    * WiFi
	* high speed long distance optical networks
  * much research into improved TCP for wireless links

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

<a name="dijkstra"></a>

###### Dijkstra's algorithm

Definitions:

* `N` - set of all nodes in graph
* `l(i, j)` - weight of link from `i` to `j`
* `s` - source node from which we're calculating paths

For an undirected connected graph:

```javascript

M = {s} // set of nodes that have been checked
for each n in N - {s}: // distance to directly connected neighbours
  C(n) = l(s, n)
  
while (N != M):
  c = ∞
  for each n in (N - M):
    if C(w) < c then w = n // find node w such that C(w) is minimum for all nodes in (N - M)
  M += {w} // add one node at a time, starting with closest
  for each n in (N - M):
    if C(n) > C(w) + l(w, n) then C(n) = C(w) + l(w, n) // best route to n is via w
	
result = C(x) // cost of shortest path from s to x

```