2 - SignalR

Thursday, July 12, 2018

7:31 AM

 

![Module Overview What is SignalR? Transports Hubs Differences Scaling out ](001_2_-_SignalR_000.png)

 

 

SignalR is an open source framework that wraps the complexity of real-time web transports mentioned in the previous chapter.

 

Real time web techniques such as long polling and web sockets are called TRANSPORT on SingalR.

 

**SignalR is divided in 2 parts:**

1.  Server side

2.  Client side

 

![Transports WebSockets, Server Sent Events, Long Polling Requires client and server that supports transport Fallback mechanism ](001_2_-_SignalR_001.png)

 

![Transports and SignalR WebSockets Server Sent Events (SSE) Long Polling Newer browsers and web servers ](001_2_-_SignalR_002.png)

 

One of SignalR most amazing usefulness is that it does not rely on specific technologies. If the browser being used by the client does not support WebSocket, then SignalR will painlessly switch back to using SSE or even Long Polling.

 

**Remote Procedure Call (RPC)\
**SignalR uses RPC to let the Server call a function in the client. Part of these calls can be paramters

 

![Browser NewOrder(Order order) ](001_2_-_SignalR_003.png)

 

This logic also applies to Browser =\> Server calls

 

**HUBS**

 

A Hub is a server-side class that sends messages to and receives messages from clients. It is a communication HUB\
 

![Hubs and Clients ASP.NET Core APP Hub ](001_2_-_SignalR_004.png)

 

The communication between the server and all the clients using SingalR is done through HUB Protocols. And the default protocol is JSON.

 

![JSON and MessagePack JSON (38 bytes) {\"Product\": \"Americano\", \"Size\":\"Vente\"} MessagePack (30 bytes) 82 a7 50 72 6f 64 75 63 74 a9 41 6d 65 72 69 63 61 6e 6f a4 53 69 7a 65 as 56 65 6e 74 65 ](001_2_-_SignalR_005.png)

 

Message pack is smaller and easier to process.

 

**What are the differences between ASP.NET Core SignalR and Classic ASP.NET SignalR?**

 

ASP.NET SignalR for .NET Core is a re-write of SignalR from scratch.

 

![Simplified connection model Single hub per connection Async Binary and custom protocols No jQuery dependency for JavaScript client Sticky sessions required ](001_2_-_SignalR_006.png)

 

![Summary SignalR simplifies real-time applications Utilizes transports Calls functions over the wire Hubs can receive and send messages Core version is different Complexity when scaling out ](001_2_-_SignalR_007.png)

 
