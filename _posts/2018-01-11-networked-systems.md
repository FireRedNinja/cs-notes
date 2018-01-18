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