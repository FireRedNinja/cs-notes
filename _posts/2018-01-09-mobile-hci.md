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