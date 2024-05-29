![[Pasted image 20231116101651.png]]

The command query responsibility segregation (CQRS) pattern separates the data mutation, or the command part of a system, from the query part. You can use the CQRS pattern to separate updates and queries if they have different requirements for throughput, latency, or consistency. The CQRS pattern splits the application into two parts: the command side and the query side. The command side handles `create`, `update`, and `delete` requests. The query side runs the `query` part by using the read replicas.

![[Pasted image 20231116101816.png]]

![[Pasted image 20231116102218.png]]

Now.... in a Microservice world here is a possible path:
![[Pasted image 20231116102326.png]]

THEN:
![[Pasted image 20231116120332.png]]

**NOW, how are we going to share data between microservices?**

It really depends on what kind of data we are sharing... is it images, is it files, is it text

Amazon Kinesis is one way to handle this:
![[Pasted image 20231116103328.png]]

How about when dealing with Internet of Things ???
![[Pasted image 20231116103813.png]]
![[Pasted image 20231116104400.png]]

![[Pasted image 20231116105123.png]]
![[Pasted image 20231116105150.png]]

![[Pasted image 20231116110650.png]]

We want to generate idempotent data... but a one to many relationship 
![[Pasted image 20231116110730.png]]

A combination of these two is the ideal
![[Pasted image 20231116110949.png]]
The combination of these two is the way to create resilient pipelines 

![[Pasted image 20231116112011.png]]

Amazon Kinesis cost-effectively processes and analyzes streaming data at any scale as a fully managed service. With Kinesis, you can ingest real-time data, such as video, audio, application logs, website clickstreams, and IoT telemetry data, for machine learning (ML), analytics, and other applications.

**What about if we are dealing with text data that I would like to parse?**
Let's say I want parse a subset of the data. Can I do that in real time? Parse and navigate text information? That's high speed ??? This is what OpenSearch Service is for
![[Pasted image 20231116113204.png]]


**SERVERLESS EVENT BUS**
Can I have a generic connector between things... so that I don't have to choose connectors (SQS / Fan out Message Passing / etc) ... That's what a service Event Bus does

![[Pasted image 20231116114648.png]]

Is this EventBridge?
![[Pasted image 20231116115120.png]]

What if it's event driven?
![[Pasted image 20231116115202.png]]

The event bus acts as BOTH one to many relationship AND allows for queuing system. Using an event bus helps a lot of actions that require us to make sure services don't go down.

Amazon EventBridge
* Removes friction of writing "point-to-point" integrations
* Works across dozens of AWS and SaaS applications
* Provides simple programming model
* Use rules to match against values in the metadata and payloads

![[Pasted image 20231116120411.png]]
