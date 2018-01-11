---
layout: post
title:  "Networked Systems H"
date:   2018-01-10 18:50:00
categories: Level3 Semester2
author: dasha
---

# Introduction

Networked System: Autonomous computing devices that exchange data to perform some application goal and how they communicate across a network

* internet
* digital broadcast
* mobile voice telephony
* sensor networks
* controller area networks

Communication: Messages transferred from source to destination(s) via some communications channel  
   How would you convert a message so that both source and destination understand it?  
   Limitations:
   
* size of messages is bounded on a channel at any one time
* simplex - send/receive in only one direction (broadcasting)
* half-duplex - send or receive, but not simultaneously (wifi)
* full-duplex - send and receive at the same time (two cables, for sending and receiving)

Information:

* information theory - amount of info in a message can be characterised mathematically
* capacity of channels can be modelled - physical limits exist here (amount, speed, power)

Signals:

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

Networked systems often use non-binary encoding:

* complex modulation schemes with either 16, 64 or 256 possible symbols
* baud rate - number of symbols transmitted per second
  * can differ from bit rate
  
Channels and Network Links:

* signal may be directly conveyed or modulated onto an underlying carrier
* link - the combination of signal and channel
  * directly connects 1+ hosts (ethernet)
  * network comprises several links connected together (WAN)
  * switches/routers - connects the links
  
Circuit Switched Networks:

* dedicated circuit for A and B to communicate
* exchange arbitrary length messages
* guaranteed capacity once circuit is created
* can block other communications
* capacity of network gives blocking probability
* traditional telephone network

<img src="/cs-notes/assets/images/ns/circuit_switched.jpg" nopin="nopin" />

Packet Switched Networks:

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

## Network Protocols

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

Morse Code:

* signals on electrical cable form a channel
* syntax - pattern of dots and dashes
* semantics - different gap lengths to signal end of word, and "STOP" for end of message

Protocol Layering:

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

OSI Reference Model:

* standard way of thinking about layered protocol design
* design tool

<img src="/cs-notes/assets/images/ns/osi.jpg" nopin="nopin" />

Physical Layer:

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
  
Data Link Layer:

* structure and frame physical layer bit stream
  * split bit stream into messages
  * detect/correct errors
* perform media access control
  * assign addresses to hosts
  * arbitrate access to link
  * detemine when hosts can send messages
  * ensure fair access to link - flow control
* ethernet

Network Layer:

* interconnects links to form a WAN from source host --> destination host
  * data delivery
  * naming and addressing
  * routing
  * flow control
* IP

Transport Layer:

* end-to-end transfer of data from source --> destination
  * between session level service at the source, and corresponding service at the destination
  * provides reliability, ordering, framing, congestion control
* TCP

Session Layer:

* manages transport layer connections
* functions
  * open TCP/IP connections to download webpage with HTTP
  * use SMTP to transfer email messages over a TCP/IP
  * coordinate control, audio and video flows for video conference
  
Presentation Layer:

* manages presentation, representation and conversion of data
  * character set
  * data markup langs.
  * data format conversion
  * content negotiation
  
Application Layer:

* user application protocols (not the app. programs themselves)
* REST APIs/WebRTC

Protocol Standards:

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