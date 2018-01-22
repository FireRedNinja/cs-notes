---
layout: post
title:  "Cyber Security Fundamentals\t"
date:   2018-01-08 12:00:00
categories: Level3 Semester2
author: noel
---

# Lecture 1 - Introduction

- **Security** State/Condition of being pretected from or not exposed to danger from some internal or external threat
<!--excerpt-->
- Hacking against the law
    - Unauthorised access to computer material
    - Unauthorised access with intent to commit or facilitate a crime
    - Unauthorised modification of computer material.
    - Making, supplying or obtaining anything which can be used in computer misuse offences.

> "..prevention and detection of unauthorised actions by users of a computer system" - Deiter Gollman

> "the prevention and detection of unauthorised actions by users of a computer" - Microsoft

## Socio-technical Systems
-  **System** is a purposefull collection of interrelated ocmponents of differen kinds, which work together to achive some ovjective

- **Socio-Technical systems** include technical ystems,but also organisational processses and people who use and interact with the technical sustem
- governed b organisational and regulatory policies and rules


<br>

- **Computer Security** - protection of hardware, software & data assets
- **Information Security** - protection of information and information systems from unauthorized access, use, disclosure, disruption, modification, or destruction in order to provide confidentiality, integrity, and availability


## Security model
![security model](/cs-notes/assets/images/csf/securityModel.PNG)

### CIA
- **Confidentiality** - Prevention of unauthorised disclosure

- **Integrity** - Prevention of unauthorised modification of information

- **Availability** - Prevention of unauthorised withholding of information and rescources

![CIA](/cs-notes/assets/images/csf/CIA.png)


- **Vulnerability** - Weakness in your system
    - Hardware
    - Software
    - Network
    - Personnel
    - Location
    - Organisational


- **Threat** - Potential exploitation of vulnerability

- **Attack** - Attempted violation of vulnerability

- **Passive** - Just watches and maybe collect data

- **Active** - Attempts to change resources or operations

### Threat Types
![Threat Types](/cs-notes/assets/images/csf/threatTypes.PNG)

- Physical Damage
- Natural Events
- Loss of essential services
- Disturbances due to radiation
- Compromise of Information
- Technical Failures
- Unauthorised Access
- Compromise of Functions

### Deal with threats
- Reduce/Remove threats by
    - Prevent
    - Detect
    - React
    - Correct
- Accepted ("it's not a bug its a feature")
- Avoided
- Transfered (give the problem to someone else)


> Doing Security == Risk Management

- Asset identification
- Risk identification
    - Find assest's vulnerabilities
    - Find the relavent threats
- Risk treatment analysis
- Treat the risk


 - Asset protection
 - What are my assets
 - What danger are they in
 - How can I protect it


## Section 4 - Security Engineering

- **Security Engineering** is about building systems to remain dependable in the face of malice , error or mischance

- What are ny security requirements
- What are my policies
- Policy and Guidence
- **Policy**- What you want to achieve?


## Poits of Interest
- Simple > Rich mechanisms
- Trade-offs
    - cost/speed
    - effort
- Should the effort I put in to securing the data be relatied to the worth of the data?


### Key principles
- Easist penetration
- Adequate protection
- Weakest link
- Effectiveness


- Security should not be an afterthought


- Crytography is not a silver bullet

### Actors
- Amatues/Script kiddies
- Hackers
    - Black Hat
    - White Hat
    - Gray Hat
- Hactivist
- Carrer criminals
- Terrorists
- Government

------------------------------------------------

# Intro to Cryptography
- Confidentiality
    - Public key encryption
    - Block ciphers
    - Stream ciphers
- Integrity
    - Cryptograhic hash function
    - Message authentication codes
- Authenticity
    - Digital signatures

## Primitives
### Hashfunctions/Message digiest
- Takes some data in
- Gets signiture out
> Funcion to compute a unique random signature for some data


![Hash Function](/cs-notes/assets/images/csf/cryptographicHashFn.PNG)
- Guarantee towards: Data Integrity
- Preimage resistance
- Second Preimage resistance
- Collision resistance
- Eg: MD, SHA

### Block Cyphers/Symmetric crytography
![Symmetric Cryptography](/cs-notes/assets/images/csf/symmetricCrypto.PNG)
- Guarantee towards: Confidentiality
- Uses sameto encrypt and decrypt
- Efficient for large messages
- Eg: Blowfish, TripleDES, Skipjack, AES

### Asymmetric ciphers
- 3 functions
- 1 to Encrypt
- 1 to Decrypt
- 1 to create key
![Asymmetric Ciphers](/cs-notes/assets/images/csf/asymmetricCipher.PNG)
- Guarantee towards: Confidentiality
- Key Pairs
- Encrypting and signing
- Inefficient on large data
- Eg: DSA, (EC)DSA, ECC, RSA, ElGamal

## Workflows
- Primitives can be used to have guarantees for more than one of
    - Information Security
    - Efficient Information Security
    - Sender Authentication
    - Secrecy with Authentication
    - Secrecy with Signature
    - Secrecy with Integrity
    - Signature with Appendix
    - Secrecy with Signature with Appendix


### Digital Signitures
- Authenticity of message origin
- Non-Repudiation of message origin
- Message Integrity

### Public Key Encryption & Digital Signitures (Combination)
- Message confidentiality & integrty
- Authenticity of message origin
- Non-Repudiation of message origin

### KEM/DEM (Hybrid)
- Symmetric Encryption to encrypt data
- Assymetric to encrypt symmetric key

## Implementing
- RSA System
    - Encryption
    - Digital signitures
- Descrete logarithm system
    - Key exchange
    - Digital signiture algorithm
    - Discrete logarithm integrated encryption scheme

 ------------------


# Lecture 3 - Introduction Cryptography 2


why love crypto - guarantee
## Block Cipher
symmetric ciphers
same key to encrypt & decrypt

XOR with key
initialisation vecotors

take data
keep encrypting until unreadable

fast =
easy to implement in hardware

2 families
    feistel, IDEA

### DES
- Project Lucifer
    - devide intor blocks
    -
- Insecure Algorithm


### Triple DES
- modification
- use DES 3 times
- encrypt wiht 1 key
- decrypt with 2nd key
- encrypt with 3rd key
- noone uses this anymore
- if use same key there are backwards compatability
- dont use this

-is it just XOR? no

- symmetric crypt is inherantly insecure

- DES is insecure
- replaced by
- AES

- copetition
- Rijndael won

### rijndael
- permutations and substitutions
- variable number of rounds dependent on key size

- ECB -
- CBC -
- PCBC
- CFB
- OFB
- CTR

### ECB
<!--diagram-->
- take each text and map it to

- break into blocks
- encrypt and concatinate back

- operating on each chunck individually
- no block big enough for the wholemessage

- problem
    - you dont know when the blocks end
    - order of blocks?

### CBC
<!-- diagram -->
- ouput fed in to the next round
- creates random noise
- operates on each block individually

## iv and padding
- initialisation vectors
    - dont have ot be secret
    - keeep secret key
    - different ini vecto with diff keys
    -
- last block padding
    - ensure final block has correct lenght

## Secret Sharing
### Deffie-Hellman Key Exchange
<!-- diagram -->



## PRNGs
- want to makesure they are truely random
- virtually impossible
- always have some sort of structure
- - hidden deep inside the structure

- cryptographic
    - cannot be predicted from someof the numbers in the sequence


## strats
- computer clocks
- keyboard latency
- using random noise


## Message Digests
- given any message, easy to compute thedigest
- given any hash, hard to compute themessage
- neet  to limit
    - hash collision
    - birthday attack given 2 random message, should not produce the same digest
- sha -1,2 -
-
## Designing
- DES in secret
- AES in open competitions

- Kerckhoffs 2 Principle
    - security in your algorithms should be in tyour algorithm and in your keys

- Linus law
    - many eyes, catch many bugs
- NOTHING IS SECURE

------------------------------------

# Lecture 4 - Cryptography in the wild

## Applied
- Primatives & Schemes not enough for security
- kes are just numers

- alorithms
    - which one to use

> data at rest is data tat doesn't "move"



- keymanagement is the real issue

- perfect forward secrecy
- end to end encryption



- Securing data in flight
    - data in flight is moved from onedomain to another

- what kevek of the osi am i opperating at

- key management

- wha else is there?
    - publoc key systems


> DONT IMPLEMENT OR DESIGN YOUR OWN CRYPTO. unless you are a **trained** engineer

- Theroetically secure != Implementation secure

- use good standard libraries


- you hav to ook at domain, cost and effort

[keylength.com](http://www.keylength.com)


- ISO 27K
- guidence on howto do things
- regulation of cryptographic controls
    - what you need to be aware ofwhen implementing
    - are there import/export restrctions

- policies
    - where we are we going to use it
    - impac of policy

- complience


- what is your indsutry doing, what are the best practives
- stakeholder expectations


- Laws
    - EU Laws
    - British Laws



## Advanced
- Encryption Schemes
- Signature Schemes
- Secret Sharing Schemes
- Provable Crytographic

- how are these used

- Authentication protocols
- Anonymous Protocols
- eVoting
- Multi-Party Computation
- Distributed Authorisation
- Searching Encrypted Data



## Attacking
- if you want to attack the mathematics of encryptions, get a PHD

### Attack the standard
- make sure the system has a backdoor

#### human factors
- send your agents
- rubber hose cryptoanalysis
    - how can you do rubber-hose resistant crypto?

### side channel attacks




## Tutorial
1. a
2. DAE is open, DES is closed. open i sbetter
. AES is more cheaper. des on its own is insecure.
3. tuxPenguin, cbc has the chain,
4. there is a small amount of digests to cycle through
5. s
6. they are different algs, diff fundamentals, so cost/efort to attack is different
7. encrypt message with private key, exchange, encrypt wih private key, exchange. not vulnerable to MITM attack, no way to make sure who you are talking to s who you are talking to
8. not possible to get truely randomnumber, psudo there is structure, crypto, hard to determine what it means
9. ifyou know theseed youcan guess the random number.

------------------------------------------------------------

# Lecture 4  - Authentication

- Enrollment : establish credentials
- Challenge & Response : Check validity of credentials

## Local
- Commonly used: Identity * Password
- Store **salted** digest of passowrd for security
  - MD5, SHA
- when loggin in
  - password salted & hashed
  - compared with stored hash

### Dictionary attacks
- how to chose a Password
- attackers can calculate variations of a password and form salts hashes
  - if there is a mactch it we dound the password that is begin used
- david kliein
  - gets usernames, initias, login name
  - femail and male usernames
  - ...
  - created permutations of above

### salting
- hava a random string or value and add to Password
  - add randomness to password so harder to guess
  - large salts are good
- salt string is publicly vailable, each password has individual salt
- dont store password as you are given, add some randomness
- keep password securely

### password complexity
- uPPer & lowwer case
- numbers
- dont common words
- use special characters
- at lease X long

- entropy
  - how much information is carried in a single characters
  - first character ~ 4.7bits
  - 2-8 ~2.3bits per characters9=> ~1.5bits per character

### Passphrases
- trend
- long and easy to remmeber
- depending on what device you use, use different passowrd

## Remote
- What is a secure channel

- there might be someone evesdroppting
  - impersonating the sendee
  - they can manipulate it

- how to talk securely
  - we can use Cryptography
  -
- how to prevent replau attackers
  - ensure message freshness
  - mayinclude identity & timestamps

### Brokered Authentication
- have a trusted third Party
- we trust Ted
- trusting thirdparty for keys
  - we are assuming hes good
  - we are trusting him to be honest

### Needham-Schroeder Protocols
- based off deffie Hellman
- trusted key server tha generates session keys


- asymemetric public key

- both symmetric and assymetric are suscepible to replay attackers

- flaw
  - ryan can get alice's id and send it to ryan


### User Authentication in a Distributed systems
#### client machine that autehntiactes

#### client lef

#### Mutual authentiaction


## Kerberos
- 3 headed dog
- each network authenticated
- each message autehnticated
- each message encrypted


### overview
- sign to service
  - alice signs in with Password used to cread shared Secret
  - create a ticket to authorise with tichet services
- get permission to talk to bob
  - alice asks ticket serice for ticket to enable communcation with bob
- Talk to bob
  - alice uses ticke ot talk to bob
- repeat spteps 2 & 3

### signing intoservice
- ticket contains who it was generated fo, and a key to enable communication wit ticket service
- restricted lifetime to prevent replau attacks
