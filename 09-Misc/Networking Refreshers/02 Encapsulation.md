One thing that's important for everyone to remember is that sites can be quite large. Every web developer should know that with the introduction of front-end frameworks, sites often sent quite a bit of data to the client side to be managed, rendered and ran by the user's browser. So, taking care of the size of these files is quite important. Some of the protocols I mentioned in the previous note, literally have a **maximum** about of data that they can send.

![[Pasted image 20241021135441.png]]
When dealing with a web page, we can just split files.


![[Pasted image 20241021135450.png]]
Once we have the data broken down into smaller pieces, we can then add it to a HEADER. The transport layer sets up the session between the client and the server. Once we have this connection stablished there are a few things that happen, we will have info above to keep track of everything that happens. The analogy to be used here is similar to when you write a birthday card to a family member. The card  is inside of an envelope that gets sealed up. The envelope contains data like the address of the person you are mailing it too as well as a return address for yourself and then you have the message that is considered the *Payload*.

The envelope is pretty much known as a **SEGMENT**. Any chunk of data with a transport layer header.
![[Pasted image 20241021140128.png]]
This particular SEGMENT HEADER is known as a TCP Header. This info allows the client and the server to keep track about what information has been sent/received.

**Segment: A chunk of data, with a transport layer header**

![[Pasted image 20241024164214.png]]
Now, something really cool needs to happen. Our computers need to find a way to know where to go and where to send the information to... well, that's where the Network layer comes into place. And similar to the Transport Layer we now have another __ that contains the source IP and destination IP as well as TimeToLive which tells how long the package could live. AND the payload in this case, is the SEGMENT we had before. Which contains the TCP Header and a payload with a chunk of the website... this is called **PACKET** ... This particular packet is a INTERNET PROTOCOL Header. (specifically an ip4 - more on that later). Ultimately it is setting what to end-points on the network we are sending data to/from.

**Packet: A Chunk of data, with a network layer header**

![[Pasted image 20241024164841.png]]
Next level down the matryoshka doll game we are playing here, we need to know HOW do we transfer this data between one device and the next. Remember my previous note, essentially from my phone to the router, from the router to the modem, from the modem to the cell tower ... etc ...

In this case we send out Network Layer PACKET and we put it as the payload of a  FRAME

**Frame: A chunk of data, with a Data Link layer header**

The particular screenshot above refers to an ETHERNET HEADER.

![[Pasted image 20241024165249.png]]
The important thing for me to remember is that ultimately, a part of our website is inside this FRAME, and we need to keep in mind the size constraints that we have across all these protocols. When working with ETHERNET data link layer header, we have something known as the **MTU - Maximum Transmission Unit** ... this is often set to a limit of 1,500 bytes (1.5MB). It *can be made larger* but rarely it is done.

![[Pasted image 20241024165509.png]]
Last but not least, is us converting the message into the physical layer... which is, as most things with computers, just a set of ONES and ZEROES all around
![[Pasted image 20241024165556.png]]
which will just be transferred through cables/wires/fiber-optics ... etc


 