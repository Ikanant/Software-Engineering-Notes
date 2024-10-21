 Open Systems Interconnect. Model created in the 70's used to describe networking operations. It gave us a way to categorize protocols as well as to give the order in which these operations need to occur.

In the most fundamental way possible, when I make a request to a site, google for example, sending the request from my phone... I first make that request to the router, which then connects to a modem (sometime same device in my case)... which then connects to a tower of some kind ... to a set of devices in between, to then the server hosting google.com. This is often referred as the **Physical Layer** in OSI. Layer 1.

Across the different devices my request goes too, there are a set of **protocols** that define how that data is transferred around... In this case for example, between my phone and my router, data is more often than not transferred using **ethernet** protocol. The connection between the modem and the Internet as a whole is often **DOCSIS-3** .... these protocols are different but ultimately are doing the same thing, transfer data between devices securely. All these protocols provide all of the structure to be able to use the cables that connect all the devices across the internet. These protocols and rules is under layer 2:  **Data Link Layer**.

So, let's say we want to reach out to google servers... the Data Link Layer refers to the protocol used to stablish that connection, but I do not yet have the *method* to accomplish the task. For that we need a new protocol otherwise known as the Internet Protocol Or **IP Addressing** (or **IP Routing**) this protocol would then fit under the layer 3: **Network Layer**.

In order for me to talk to google server, we need a way to build a **session** in order for the computers to talk to one another and understand that the conversation is meant for *specific* things in that conversation. This is known as Transmission Control Protocol (TCP) ... the easiest way to think of this in my mind is a connection between two phones. The process that I have to use to pick up the phone, *dial a number*, stablish the connection to whoever I am calling once they pick up, it's essentially TCP. This session that I would establish with the google server from my computer (similar to a phone call) that allows data to be sent between devices is Layer 4: **Transport Layer**.

Now I need a way to transfer data that is in a *usable* format. That is often the task of a browser. Browser in my case is just retrieving a web *page*, which is nothing more than a document with some information in it. The browser is just making use of a protocol in order to request that information. This protocol is known as **Hypertext Transfer Protocol (HTTP or HTTPS)**. This protocol uses text written in a language that everyone knows called **Hypertext Markup Language (HTML)**. All of this process is happening outside of the layers I mentioned above, which puts this in Layer 7: **Application Layer**

Notice I skipped layers 5/6. These were outdated since these layers were defined in the 70s.
Layer 6 is the **Presentation Layer**
Layer 5 is the **Session Layers**

Summary:
OSI Model:
1. Physical Layer
2. Data Link Layer
3. Network Layer
4. Transport Layer
5. *Session Layer*
6. *Presentation Layer*
7. Application Layer


