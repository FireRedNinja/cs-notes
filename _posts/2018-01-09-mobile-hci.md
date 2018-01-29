---
layout: post
title:  "Mobile HCI\t"
date:   2018-01-09 10:00:00
categories: Level3 Semester2
author: noel
---

# Introduction

- Notion of mobiles varies from coutruy to countriy
    - UK - mobile
    - Germany - andly
    - Finish - travel phone
    - Japanese - portable telephone

<!--excerpt-->

- What is mobile to me?
    - Helper, Communication, Keys to Internet

- Do we check our mobiles too much?

- How are people using cameras?

- Reading books - phisical/electronic?


- Impact on Humans
    - Addiction
    - Controlling our world/being controlled by our phone
    - Negative in social sitiations
    - Gradually deskill us

- Social aspects
    - Social media faster than news
    - More power to the citizens
    - It changes the way we communicate with each other

- Consequences on society?


------------------------------

# Android

## Android Architecture
![Android Architecture](/cs-notes/assets/images/mobhci/androidArchitecture.PNG)

## Android Stack
![Android Software Stack](/cs-notes/assets/images/mobhci/androidStack.PNG)
- Java apps running on Java-based, object-oriented application framework on top of Java core libraries running on Dalvik virtual machine



- Android apps written in Java
- Bundled by *aapt tool* to return a **.apk** file


- By default each app runs in its own Linux process
- Each process has its own VM
- Each app is assigned a unique Linux user ID

## Components
- Activity
- Intent
- Service
- Content Provider
- Broadcast Receiver

### Activity
- An **activity** is a single, focused thing that the user can do
- Forms a UI, but each activity is independent from others

- **Task** consists of a *stack* of activity elements
    - eg: You open Gmail and it shows a list of emails. When you open a message, it is pushed into the stack and you will see the message. When you press back, it is popped out of the stack and you will see the list of emails

### Android Lifecycle
![Android Lifecycle](/cs-notes/assets/images/mobhci/androidLifecycle.png)

### Intent
- An **intent** is a messaging object you can use to request an action from another app
    - eg: From Gmail, you click a website link and it starts an intent to open the web browser, from there if you click a YouTube link, it starts an intent to open YouTube

### Service
- A **service** is an application component that can perform long-running operations in the background, and it doesn't provide a UI
    - eg: Playing music in the background

### Broadcast receivers
- A broadcast receiver is a component that receive and react to broadcast announcements
    - eg: If you are playing music and you get a phonecall(broadcast announcement), and your receiver can take this annoucement and stop the music.

### Content providers
- A **content provider** makes a specific set of application's data available to other aplications

### Manifest
- Provides essential information about your app to the Android system.



## Android UI
### Basic Concepts
- View
    - UI elements that can be drawn
- View group
    - eg: Linear Layout
- Intent
- Content privider
- Service

- XML Layout
    - Where you describe how the activity looks

### Layouts
- Linear
- Relative
- Table
- Grid
- Frame

- To make UI, you can write Java code like Swing(Procedural) or write XML code(Declarative)
- Preferably Declarative

### Resources
- Images, text, XML layouts, sound files, databases...
- Held in res/ directory


- To attach the view to hierarchy tree to screen for rendering, the activity must call setContentView() in the Java file (usually made one for you by default for you)


### Widget
- Anything you can interact with
    - Eg: Buttons, Radiobutton, checkbox, textview

### Fragments
- Represebts a *behavior* or a *portion of UI* in activity.
- eg: you can combine multiple fragments in a single activity to build a multi-pane UI and reuse a fragmet in multiple activities

-------------------------------------------------------------

# Lecture 3 - Constraints
- How has mobiles changed?

- Given the different types of phones what problems does software engineers face?

- You wont have access to your favourite libraries

- compatability problems
    - less of an issue over time

- diff platforms diff licencing

- speed is an uissue but it has implications of battery life

- coprocessor to save battery

- memory often limited

- allocating mem is more costly than not
- forcing garbage collection causes hicups

- ios has to manage manually

- data cost money, energy, battery life

- sensors

- mobiles are limited in resources(data, memory, batterylife, processing power...)
- but as time goes it becomes less important
- always remember about memory
- docs suck, libraries suck, but it sucks less over time
- if you shitty app has smalltext noone can read
- think about the users ( they are stupid)
- 

-------------------------------------------------------------

# Ubiquitous Computing

## UbiComp/Ambience intelligence:

* post-desktop model of HCI
* informatin processing integrated with everyday life
* you may not even be aware that you're using computing
* contrasts traditional desktop computing
* machines that fit the human environment
* third era of computing (after mainframes and PCs)

Weiser envisioned a world like this in '91 and then further in '96, calling the approach "calm computing":

* mobile and embedded processors communicating with each other
* used to support everyday practices, making lives more **convenient, comfortable and informed**
* information appearing in centre of out attention when needed and disappear effortlessly when not
* a central vision was our homes, things and environments being aware and adaptable

Examples:

* HP Cooltown
  * every object has a webpage
  * communicate with other objects
  * knows what you're doing at all times through the environment around you
  * implications
    * false alarms
    * privacy
    * malicious access
    * making sure people's valuable records aren't distributed
* NOKIA
  * wearable tech
* IBM
  * WAP-based flight check-in system
* Oyster travel in London
* other projects that never made it onto the market
* whereabouts clock
  * at a brief glance, get info on where family members are
  * well defined amount of detail
    * know where people are without crossing personal boundaries
    * only people in the house have access to it
    
### Tangible Interaction:

* tangible interface - things that think
  * give physical form to digital info
  * use physical form to model interations with digital content
    * making it more intuitive/engaging
    * info directly graspable and manipulable
* eg disaster simulation
  * place physical source marker on tabletop display depicting map of city
  * detects the disaster and simulates impact
* eg media blocks
  * one block associated with a digital frontend (text, image etc) 
  * program a block by writing its contents on a whiteboard
  * take block anywhere to run it
    * eg to a printer
  * transfer content easily
* eg Ishii
  * bottles with music inside
  * open bottle and music comes out
  * interact with different bottles to DJ
* eg shape-changing phones
  * shifting mass
    * weight inside phone to help you know what's going on without looking at the screen
  * shifting shape
    * thin --> thick shows you where there is more content off-screen
  * breathing
    * has a heartbeat
    * know when relaxed/something happening
    * calm it by patting
* eg Shoogle
  * balls inside case physically jangle
    * eg different message senders get a different pitch of sound
  * when this was tested, people didn't get it
    * so important to initially demonstrate the system with a visual correspondence
* advantages
  * natural for people to interact with physical objects
  * easy for anyone to interact with
  * playfulness
  * encourage spatial thinking
  * can be distributed in environment
  * simultaneous interaction
  
### Space-multiplexing:

* graspable interface offers multiple input devices
* input and output distributed over space
* allows for simultaneous, but independent and persistent selection of objects
* eg marble answering machine
  * marble colour corresponds to message sender
  * keep a message by putting it back in the machine/listen to it by putting it in your phone
  
### Ambient user interfaces:

* display info in the background
* output only (no full interaction with system)
* often visually appealing
* eg dangling string network display
  * string attached to motor hangs from ceiling
  * speed of spinning corresponds to amount of network traffic
  
### Scales of experience:

* the distance of interaction between device and user
* 1cm - badges, watches, fobs
* 10cm - mobile phones
* 1m - person-sized (exercise equipment)
* 10m - environmental (control rooms)
* 100m - architectural (large screens)
* 1km - urban (managing traffic flows)

### Internet of Things:

Uniquely identifiable embedded computing devices within Internet infrastructure.

* everyday objects with network connectivity
* ease of communication
* ease of connecting 3rd world to the internet
* currently 9-10 billion devices on the IoT
* eg smart homes, body sensors with alarm for doctors

### Cyborgs?

* constantly relying on a piece of tech
* from behavioural standpoint, this is indistinguishable from us being implanted with tech
* we're getting used to the fact that we don't need to constantly worry about our memory
* if you control your phone, then by definition your phone is not remote from you
* how does this behaviour shape what kind of digital surfaces we create?

### Merging of mobile and ubicomp:

* borders between mobile interaction and ubicomp are disappearing
* phones are WiFi enabled, location aware and motion sensitive
* many ubicomp inventions are happening through mobile devices, rather than building specially designed devices for them
* services come to fruition when we make something new out of the sensors the phone already uses

### Who is in charge?

* normally app in charge of workflow
* with ubicomp, who influences the interaction between user and computer?

-------------------------------------------------------------

# Interaction Design

Designing interactive products to support people in their everyday and working lives.

* identify needs and establish requirements
  * target users
* develop alternative designs
  * conceptual and physical design
* build interactive versions of the designs
  * paper-based prototypes
  * role-playing users
* evaluate designs
  * determing usability and acceptability of the product
  * involve users throughout the process
  
Tips:

* beauty and elegance comes from simplicity
* don't make the user think
* go to the core of the matter
* don't just recreate a desktop app
* design with the mobile user in mind from the start

Desktop User:

* stable connection
* always plugged in
* big screen
* full attention
* control over environment

Mobile User:

* unstable signal
* network source changing
* limited battery life
* costly data plan
* divided attention
* small screen
* limited input capabilities

Mobile Opportunities:

* GPS
* gyroscope
* accelerometer
* compass
* heart rate
* camera

## Building a good mobile app:

* understand
  * what can target device do
  * know your user
* imagine
  * enhance features with device's capabilities
  * use unique features to take input/give feedback to users
* context
  * what is user doing
  * where is user
  * who or what is near user
  * who is user
* make use of online data
  * info from APIs
  * esp after relying on contextual data

## Skeuomorphism:

Design concept of making items represented resemble their real-world counterparts.

## Finding out what people want:

* what are user's values
* what activities are performed
* how does context constrain/facilitate these behaviours
* what did people do before the task could be done on a phone

## App definition statement:

Concist, concrete declaration of an app's main purpose and intended audience.

* created early in development
  * help turn an idea and list of features into a coherent product
  * use throughout development to decide if potential features and behaviours make sense

1. list all features you think the user might like
2. determine who users are
3. filter feature list through the audience definition

## Typical mobile app behaviour:

Microtasking

* getting things done in short bursts
* quick access to info
* accomodate the users in a hurry
* optimise for brief recurring tasks

Local

* about things close by
* who or what is available nearby
* use sensors to reduce need to enter text and to narrow options

Bored

* games or entertainment focus
* passing the time

## Paper prototyping:

* give people something concrete they can interact with
* focus on observing behaviour
* don't waste time making things look perfect
* make changes **during** usability process
* people on team can contribute to design

## Spectrum of prototypes:

Paper prototypes have lowest fidelity, followed by static wireframes linked together, then interactive prototypes, and finally fully coded prototypes.

-------------------------------------------------------------