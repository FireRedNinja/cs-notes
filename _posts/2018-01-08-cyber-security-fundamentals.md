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