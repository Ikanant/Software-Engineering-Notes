01 - Integration with Apache Camel

Friday, May 20, 2016

10:16 AM

 

-   Enterprise Integration

    -   Enterprise Integration Pattern

-   Camel Fundamentals

    -   Mediation Engine

        -   Handles communication of messages between end points

    -   Routing

        -   Rule based routing

    -   Endpoints

        -   URL...Camel can route message to anything... WebService, Database, etc... (this wide support makes Apache Camel so important

-   Case Study

    -   Order Fulfillment

    -   Introduce Camel Mediation

 

**Enterprise Integration**

 

This refers to the communication between different systems across the network. In most cases, such systems have various properties and deal with different protocols to send and receive information.

 

**Enterprise Application Integration**

 

[3 Different Approaches:]{.underline}

 

1.  Storefront \<\-- File \--\> File Transfer \<\-\-- File \--\> Order Processing\
     

2.  Storefront \<\-- Message \--\> Web Services \<\-- Message \--\> Order Processing\
     

3.  Storefront \<\-- Message \--\> Messaging \<\-- Message \--\> Order Processing\
     

Camel, as a mediation engine, uses all three of the mentioned approaches

 

 

**Mediator Behavioral Design Pattern:**

\"Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.\" (Gamma, Helm, Johnsons and Vlissides, 1995)

 

**Enterprise Integration Pattern Review:**

 

1.  Message

    a.  Unit of Data

    b.  Data is packaged in Header (Metadata about the message) & Body (Actual Data)

2.  Message Endpoint

    a.  Sends and receives messages between an application and a messaging system

3.  Message Channel

    a.  How Applications communicate with one another

    b.  Often a Channel is implemented using a message queue

4.  Pipes and Filters

    a.  Pipes are implemented using message channels

    b.  Filters are components that provide an interface to receive a message, process it and then forward it

    c.  Core of the architecture of Apache Camel

 

![Machine generated alternative text: Order Service run Fulfillment Processor execute Order Retrieval get orders send orders Order Processor Process Fulfillment File save orders get orders 1 save orders process orders Fulfillment Center 2 Fulfillment Center 1 Order Source Orders DB ](000_01_-_Integration_with_Apache_Camel_000.png)

 

**Why should we consider Apache Camel for this Case Study:**

 

For this case study we already have an Order Processor working... but sadly, it is not flexible or robust enough to provide results.

 

![Machine generated alternative text: Orders Apache Camel Endpoint Pipes and Filters Endpoint Fulfillment Center 1 Endpoint Fulfillment Center 2 Endpoint ](000_01_-_Integration_with_Apache_Camel_001.png)
