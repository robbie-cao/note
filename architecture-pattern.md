# Architectural Patterns and Styles

## Architectural Patterns

### General

An architectural pattern is a general, reusable solution to a commonly occurring problem in software architecture within a given context. Architectural patterns are similar to software design pattern but have a broader scope.

- Model-View-Controller
- Presentation-Abstraction-Control
- Pipe-And-Filter
- Layered Systems
- Microkernel
- Client-Server and N-Tier Systems
- Repository
- Blackboard
- Finite State Machine
- Process Control
- Multi Agent System
- Broker a.k.a. Service Oriented Architecture
- Master-Slave
- Interpreter a.k.a. Virtual Machine
- Hub-And-Spoke
- Message Bus a.k.a. Event Bus
- Structural Model
- Ports-And-Adapters a.k.a. Hexagonal Architecture
- Peer-to-peer
- Event sourcing
- CQRS

> http://www.dossier-andreas.net/software_architecture/

### Layered Architecture

![](https://d3ansictanv2wj.cloudfront.net/sapr_0101-df339e516c077c33fae16623c8ec80c1.png)

### Event-Driven Architecture

![](http://s.radar.oreilly.com/wp-files/2/2015/02/sapr_0201.jpg)

The topology is illustrated below, there is no central event-mediator component controlling and orchestrating the initial event; rather, each event-processor component is responsible for processing an event and publishing a new event indicating the action it just performed.

![](http://s.radar.oreilly.com/wp-files/2/2015/02/sapr_0203.jpg)

### Microkernel Architecture

![](http://pafel.net/wp-content/uploads/2015/10/Screen-Shot-2015-10-13-at-10.57.08-AM.png)

### Microservice Architecture

![](https://www.safaribooksonline.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0401.png)

> http://www.oreilly.com/programming/free/files/software-architecture-patterns.pdf

> https://github.com/ruanyf/articles/blob/master/2016/2016-09-02-software-architecture.md

## Architectural Styles

An architectural style, sometimes called an architectural pattern, is a set of principles—a coarse grained pattern that provides an abstract framework for a family of systems. An architectural style improves partitioning and promotes design reuse by providing solutions to frequently recurring problems. You can think of architecture styles and patterns as sets of principles that shape an application.

Architecture style | Description
----|----
Client/Server | Segregates the system into two applications, where the client makes requests to the server. In many cases, the server is a database with application logic represented as stored procedures.
Component-Based Architecture | Decomposes application design into reusable functional or logical components that expose well-defined communication interfaces.
Domain Driven Design | An object-oriented architectural style focused on modeling a business domain and defining business objects based on entities within the business domain.
Layered Architecture | Partitions the concerns of the application into stacked groups (layers).
Message Bus | An architecture style that prescribes use of a software system that can receive and send messages using one or more communication channels, so that applications can interact without needing to know specific details about each other.
N-Tier / 3-Tier | Segregates functionality into separate segments in much the same way as the layered style, but with each segment being a tier located on a physically separate computer.
Object-Oriented | A design paradigm based on division of responsibilities for an application or system into individual reusable and self-sufficient objects, each containing the data and the behavior relevant to the object.
Service-Oriented Architecture (SOA) | Refers to applications that expose and consume functionality as a service using contracts and messages.

The following table lists the major areas of focus and the corresponding architectural styles.

Category | Architecture styles
---|---
Communication | Service-Oriented Architecture (SOA), Message Bus
Deployment | Client/Server, N-Tier, 3-Tier
Domain | Domain Driven Design
Structure | Component-Based, Object-Oriented, Layered Architecture

> https://msdn.microsoft.com/en-us/library/ee658117.aspx

## Message Bus

Message bus architecture describes the principle of using a software system that can receive and send messages using one or more communication channels, so that applications can interact without needing to know specific details about each other. It is a style for designing applications where interaction between applications is accomplished by passing messages (usually asynchronously) over a common bus.

Connect all applications through a logical component known as a message bus. A message bus specializes in transporting messages between applications. A message bus contains three key elements:

- A set of agreed-upon message schemas
- A set of common command messages [Hohpe04]
- A shared infrastructure for sending bus messages to recipients

When you use a message bus, an application that sends a message no longer has individual connections to all the applications that must receive the message. Instead, the application merely passes the message to the message bus, and the message bus transports the message to all the other applications that are listening for bus messages through a shared infrastructure. Likewise, an application that receives a message no longer obtains it directly from the sender. Instead, it takes the message from the message bus. In effect, the message bus reduces the fan-out of each application from many to one.

![](https://i-msdn.sec.s-msft.com/dynimg/IC136906.gif)

The shared infrastructure between a message bus and the listening applications can be achieved by using a ***Message Router*** [Hohpe04] or by using a ***Publish/Subscribe*** mechanism.

There are three types of Publish/Subscribe implementations:

- List-Based Publish/Subscribe
- Broadcast-Based Publish/Subscribe
- Content-Based Publish/Subscribe.

![](https://i-msdn.sec.s-msft.com/dynimg/IC97398.gif)

> https://msdn.microsoft.com/en-us/library/ff647328.aspx

## Reference

- https://en.wikipedia.org/wiki/Architectural_pattern
- https://en.wikipedia.org/wiki/List_of_software_architecture_styles_and_patterns
- https://msdn.microsoft.com/en-us/library/ee658117.aspx
- https://msdn.microsoft.com/en-us/library/dn568099.aspx
- http://www.dossier-andreas.net/software_architecture/
- http://www.slideshare.net/kronat/3-architetture-software-architectural-styles
