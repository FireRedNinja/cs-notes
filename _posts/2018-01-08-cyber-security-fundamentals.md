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

- Why love crypto?
  - Provides mathematical guarantee
  - CIA

## Block Cipher
- symmetric ciphers
- same key to encrypt & decrypt
- Bitwise operations on fixed size blocks of data
  - XOR with key
  - initialisation vectors
  - take data
  - keep encrypting until unreadable
  - fast
  - easy to implement in hardware

- 2 families
  - feistel, IDEA

### DES
- Project Lucifer
  - several transforamtions repeated one after the other
  - sub keys generated from one main key
- Insecure Algorithm
  - NSA reduced key-length to 56 bits
  - This made it easier to bruteforce


### Triple DES
- use DES 3 times
  - encrypt wiht 1 key
  - decrypt with 2nd key
  - encrypt with 3rd key
- noone uses this anymore
- if use same key there are backwards compatability
- dont use this

- is it just XOR? no

### AES
- symmetric crypto is inherantly insecure
- DES is insecure
- replaced by AES

- Rijndael won in a competition

### Rijndael
- Based on permutations and substitutions
- Block and Key size
  - 128, 192, 256, 512
- variable number of rounds dependent on key size
- Fast
- implemented in hardware
- currently no serious weakness

### Modes of Operation
- ECB
![ECB Encryption](/cs-notes/assets/images/csf/ECB_encryption.svg)
![ECB Decryption](/cs-notes/assets/images/csf/ECB_decryption.svg)
> [Wikipedia - Block cipher mode of operation](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)

- ECB can leave plaintext data patterns

- break into blocks
- encrypt and concatinate back

- operating on each chunck individually
- no block big enough for the wholemessage

- problem
    - you dont know when the blocks end
    - order of blocks?

- CBC
![CBC Encryption](/cs-notes/assets/images/csf/CBC_encryption.svg)
![CBC Decryption](/cs-notes/assets/images/csf/CBC_encryption.svg)
> [Wikipedia - Block cipher mode of operation](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)

- ouput fed in to the next round
- creates random noise
- operates on each block individually

- PCBC
- CFB
- OFB
- CTR

### IV and Padding
- initialisation vectors
    - dont have to be secret
    - keep secret key
    - different init block vector with diff keys
- last block padding
    - ensure final block has correct length

## Secret Sharing
### Deffie-Hellman Key Exchange
![Deffie-Hellman](/cs-notes/assets/images/csf/Diffie-Hellman_Key_Exchange.png)
> [Wikipedia - Diffie-Helman](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange)

### PRNGs
- want to makesure they are truely random
- virtually impossible
- always have some sort of structure
  - hidden deep inside the structure
    - enough to generate sequnce from a seubsequence

- cryptographic
    - cannot be predicted from some of the numbers in the sequence

### Generation Strats
- Computer clocks
- Keyboard latency
- Using random noise
- Basically you mash on your keyboard and it takes bits from the clock and mash it together

### Message Digests
- given any message, easy to compute the digest
- given any hash, hard to compute the message
- need to limit
    - hash collision
    - birthday attack given 2 random message, should not produce the same digest

## Designing
- DES in secret
- AES in open competitions

- Kerckhoffs 2 Principle
    - security in your algorithms should be in your operations and in your keys

- Linus law
    - many eyes, catch many bugs
- NOTHING IS SECURE

------------------------------------

# Lecture 4 - Cryptography in the wild

## Applied
- Primatives & Schemes not enough for security
- Key are just numbers

- Algorithms
    - Which one to use?

> Data at rest is data that doesn't "move"

- Can be solved by crypto
  - KEM/DEM
  - Public Key Encryption, Symmetric Encryption...
- Key management is the real issue
  - Public Key Infrastructure: Centralised/Decentralised
- Expensiveness of Encryption
  - perfect forward secrecy
  - end to end encryption
  - additional mechanisms to manage permissions


  > Data in flight is data beign moved from one domain to another

- Securing data in flight

- Crypto to construct secure channels
  - End-2-End Encryption
- what level of the osi am i opperating at
  - Network Layer has IPSec
  - Transport Layer has TLS
  - Application signal, Cryptocat, OTR...
- Keys?
  - Centralised/Decentralised

> DONT IMPLEMENT OR DESIGN YOUR OWN CRYPTO. unless you are a **trained** engineer

- Theroetically secure != Implementation secure

- Use good standard libraries
-
- you have to look at domain, cost and effort
[keylength.com](http://www.keylength.com)

### ISO 27K
- Guidence on how to do things
- Regulation of Cryptographic Controls
    - what you need to be aware of when implementing
    - are there import/export restrctions
    - are there restrictions on using encryptions
    - law enforced access to encrypted info
    - get legal advice
- Policies
    - where we are we going to use it
    - impact of policy
    - roles and responsibilities
    - management approach
    - mobile data
- key management

- complience
  - national and international Laws
  - decrees
  - industrial regulations
  - codes of conduct
  - stakeholder expectations
  - contracts/agreements
  - best practices
  - company specific policies and standards & guidelines
  - regulations/administratives orders
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
    - factorising composite numbers
    - taking discrete logarithms
### Attack the standard
- make sure the system has a backdoor

#### Attacking the System
- Attackers cna
    - evesdrop
    - insert message
    - impoersonate
    - hijack
    - DOS

#### Human Factors
- Espionage
    - send your agents
- rubber hose cryptoanalysis
    - how can you do rubber-hose resistant crypto?
- Token Attacks

#### Code Vulnerability
- just leave it to the experts
- dont make your own

#### Side channel attacks
- Differential Power Analaysis
    - estimate key lengths from power consumption of computations
- Timing attacks
    - find timings for computatioins
- Electromagnetic attacks
    - analasys the electromagnetic radiation
- Ghost data
    - non-deletion of sensitive data
    - cold boot attack
- Differential Fault Analaysis
    - inducing faults in operation
- Acoustic cryptanalysis
    - listening to CPU output for computation noise
- most of these are defeated by noise


## Tutorial
1. a
2. DAE is open, DES is closed. open i sbetter
. AES is more cheaper. des on its own is insecure.
3. tuxPenguin, cbc has the chain,
4. there is a small amount of digests to cycle through
5. s
6. they are different algs, diff fundamentals, so cost/efort to attack is different
7. encrypt message with private key, exchange, encrypt wih private key, exchange. not vulnerable to MITM attack, no way to make sure who you are talking to s who you are talking to
8. not possible to get truely random number, psudo there is structure, crypto, hard to determine what it means
9. ifyou know theseed you can guess the random number.

------------------------------------------------------------

# Lecture 4  - Authentication

- Enrollment : Establish Credentials
- Challenge & Response : Check validity of credentials
- Styles
    - Direct/Brokered

## Local
- Commonly used: (Identity * Password)
- Store **salted** digest of passowrd for security
  - MD5, SHA
- when logging in
  - password salted & hashed
  - compared with stored hash

### Dictionary Attacks
- attackers can calculate variations of a password and form salts hashes
  - if there is a match, we found the password that is begin used
- david kliein
  - gets usernames, initias, login name
  - female and male names
  - places, names of famous people, numbers, vulgar phrases, keyboard patterns
  - created permutations of above
  - capitalisations from previous lists

### Salting
- a random string or value that is added to password before encryption
  - add randomness to password so its harder to guess
  - large salts are good
- salt string is publicly vailable, each password has individual salt
- dont store password as you are given, add some randomness
- keep password securely

### password complexity
- UPPER & lower case
- numbers
- don't common words
- use special characters
- at lease X characters long

- entropy - how guessable
    - can measure password strength using information theory
    - how much information is carried in a single characters
    - first character ~ 4.7bits
    - 2-8 ~2.3bits per character
    - 9=> ~1.5bits per character

### Passphrases
- trend
- long and easy to remmeber
- depending on what device you use, use different passowrd

## Remote
- What is a secure channel

- there might be someone evesdroppting
  - impersonating the sendee
  - they can manipulate it

- how do we talk securely?
  - we can use cryptography
  - use secrecy with signature with appendix using KEM/DEM
  - use symmetruc crypto & deffie-hellman

- how to prevent replay attackers?
  - ensure message freshness by adding
      - random info
      - identity & timestamps

### Brokered Authentication
- have a trusted third Party
- trusting thirdparty for keys
  - we are assuming he is good
  - we are trusting him to be honest
- he might be malicious

### Needham-Schroeder Protocols
- based off deffie Hellman
- trusted key server that generates session keys

- symmetric & asymemetric public key

- both symmetric and assymetric are suscepible to replay attackers

- flaw
    - ryan can get alice's id and send it to ken
- solution
    - add ID to the message
    - if ID changes, we know there is a man-in-the-middle

## Kerberos
### User Authentication in a Distributed systems
1. User based client auth
2. client-led auth
3. mutual auth

### Kerberos
- 3 headed dog of secure authenticated netowrk communication
- each network authenticated
- each message authenticated
- each message encrypted

- requires
    - authentication service
    - ticket granting service

### overview
- sign to service
  - alice signs in with password used to create shared secret
  - create a ticket to authorise with ticket services
  - ticket contains who it was generated for, and a key to enable communication with ticket service
  - restricted lifetime to prevent replay attacks

- get permission to talk to bob
  - alice asks ticket service for ticket to enable communcation with bob
  - T~ttl is proof that Alice can use TGS
  - timestamp is for freshness
  - TGS sends somthing for Bob
- Talk to bob
  - alice uses ticket to talk to bob
  - Alice is sending Bob information on how to talk that could have only been created by TGS
  - Modification of timestamp tells Alice, that Bob is who he says he is
  - Bob already has K~B, TGS and this can gain access to K~A,B
- repeat steps 2 & 3

- Authentication Protocol based on Needham-Schroeder with fixes
- Single-Sign on
    - authenticate with AS and get timed access to system
    - this ticket can be used to request access to other servicies like bob
- Simplified public key variants

- advantages
    - auth on distributed system
    - single-sign-on
- disadvantages
    - single point of failure
    - not federated

---------------------------------------------
# Lecture 6 - Publc Key Infrastructure

## PKI
- Third party to deal with public keys
- certificate authorities binds public keys to IDs
    - when regestering your pub key
    - when authority generates your public/private keys
    - binding is done with digital signitures

### PK Certificates
- proof of identity
- forged certificates?
    - attackers need the ability to sign the certificate which is hard for them to do
- fake certificates?
    - Authority must berify the owner's ID before signing trhe certificate
    - Need certificate authority's verifying key to check authenticity

### Key Management
- certificate issuing and publication
- certificate revocation
    - compromised keys
    - identity change
    - termination of membership
- key pair Generation
- private key escrow, backup, arhiving, and recovery
- public key archiving
- update
- logging of actions

## Certificate Chains
- problem
    - who trusts the trusters...
    - how to balance certificate creation
        - multiple certificate authorities at different levels
- answer
    - each authority verification key is signing by more trustworth body
- Shape of chain
- more trustwrth keys can be embedded in hardware
    - so they are tamper resistant/tamper evident

![Chain Shapes](/cs-notes/assets/images/csf/chainShapes.png)

-----------------------------------

## Tutorial
1. w
2. a
3. a
4. how you deal with enrolment.
5. easy to remmber, more entropy so its harder to guess, easier to type on a different device like a mobile. easier to be attacked by over-the-shoulder attacks.
6. a
7. Password crackers
8. a
9. a
10. a


---------------------------------------------------------
# Web security
### How does it wokr
- browser ask webserver for a website which might be connected t a backend
- executed on the client

### http
- used in most transmition
- stateless
  - easier to implement
  - must provide id with every transmission
- no built in encryptions

### GET
- retrive index.hmtl
- asks webserver for specific resourve
- answer- get the resource you want
- only for info retreival
- can jave variables which is sent to webserver

### POST
- used to send data and retrive changed rescources
- sending Data
- sending credentials is worst way to use it

### Cookies
- data that a webserver can store in a client
- like session id
- should e complex
- shoulnt be easyto guess


### OWASP Top 10 Applicatoin Security Risk 2017
1. Injection
  - send data to a server that doesnt chack for the Data
  - then used in a interpreter
  - user provided data is used without sufficient checks
  - eg SQL Injection
  - stolen user data, creditcard Data
  - DOS
  - take over host
2. broken auth
  - able to bruteforce. since a lot of people use weak passwords
  - incorrect implementation/lack of knowledge
  - eg login page bruteforce
  - compromise of systems
  - money laundering
  - unauth info disclosure
3. sensitive data exposure
  - be careful how you save your Data
  - not putting enough though/energy into data protection
  - eg. using automatic database encryption
  - offences againt priv Laws
  - loss of trust
4. a way to retrive files that are not retriveable
  - trusting external prvided inpout
  - extract databaseinfo gathering
5. broken access control
  - ability to switch to more privlaged user/access to privlageed user
  - trusting external provided input
  - SQL Inj
  - privelage escalation
6. security misconfig
  - insecure default configs
  - Lack of knowledge
  - enabling directory listing
  - unauth Access
  - sys takeover
  - info gathering
7. XSS
  - injection
  - user provided data is used witout sufficient checks
  - data loss
8. insecure deserialization
  - influence control flow
  - remote code execution
  - accept serialised objects from instusted sources or user provided data without sufficient checks
  - eg. supper cookie containing id, passowr, hashed
    - attacker can cahgne those values
  - privilae escalation
  - remote code execution
9. using components with known vulnerabilities
  - lack of knowledge
  - dont ignore software update notifications
  - privlaged excalation
  - data Lossremote code execution
10. insufficient logging & monitoring
  - without identifying an attak you cant attacks
  - vulnerabuility scanning
  - bruteforce password attackers
  - being succussfully attacked

--------------------------------------------------
# Websecurity 2

1. Injection
- SQL Injection
```SQL
$user = $_POST['user'];
$pass = $_POST['passoword'];
$query = "select * from u_list where u_name = '$user' and password = '$pass';"
```

- Command Injection
```SQL
$cmd = "python get_data.py".$_GET['sort'];
$list = system($cmd);
```

# blind sqlinjection
- true or false Injection
- more difficult but can lead to same Effectiveness


how to prevent This
#### NEVER TRUST USER PROVIDED INPUT
- use functs to escape inputs
- only use frameworks that are considered safe
- use ```LIMIT```


## broken auth
- weak passwords
- one password for all == single point of failure
- use multi factor authenticator
- password rotation

- weak passowrd storage
  - plain plaintext
  - unsalted hashes
  - weak hashes

  - prevention
    - use moden hash fn
    - check for weak password
    - pwd at least 8 char long
    - harden against account enum attack
    - multifactor auth
    - log auth failure and aleart admins

## broken access control
- prevention
  - dont let attacker modify the checks or metadata
  - disable directory listing
  - log access control failres and trigger alerts

## XSS
- Prevention
  ### dont trust user input ffs
  - use frameworks that already does this for you
  - escape data



### Tutorial
1. w
2. w
3. w
4. w
5. w
6. w
7. w
8. w
9. w
