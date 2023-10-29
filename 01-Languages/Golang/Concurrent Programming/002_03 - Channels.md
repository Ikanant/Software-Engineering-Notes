03 - Channels

Wednesday, May 4, 2016

4:31 PM

 

Powerful Features:

 

1.  Communication

    a.  Safe way to send messages through our application

    b.  Independent objects. Channels can be distributed to Actors in our application without them knowing about eachother. HIGHLY decoupling architecture that is great to test AND debug

2.  Isolation

    a.  Isolation of Actors in an application

3.  Synchronization

    a.  Hopefully never have to think about

    b.  When sharing data between threads in a concurrent application, it can be difficult to get the synchronization of the actors correct...

    c.  Internal synchronization mechanism allows to have neither the sender NOR the receiver have to wait... (not quite but we will see in the code)

 

**Memory Isolation**

 

In the past we used to store our memory globally... forcing developers to be careful when manipulating the data...

 

The solution to this problem was to ISOLATE the memory into smaller, more manageable pieces. Like for example doing Object Oriented Programming... This worked great and all, until new processors came along with multiple cores... For such cases we then encountered that some of the objects being handled by multiple threads could have issues and therefore, create headaches for developers...

 

An answer to this issue was implemented when functional programming allowed to have data being immutable.

 

This is NOT was GO does. Go just creates channels available to create a secure pipeline through which information can safely flow. This ensures that one actor can access it at a time, no matter how many entities are waiting for it

 

 

**Buffered Channels:**

 

When creating channels for our Go_Routines we can do so simply by using the built in **make** function....

 

An un-buffered channel is a channel we create using the **make** keyboard BUT we don\'t specify a size or number of buffers for the channel:

***myChannel := make(chan int)***

 

The important thing about un-boffered channels is that when a Go_Routine wants to share some data through such channel, it will wait (locK) until another go_routine grabs such data... Forcing some kind of Synchronous criteria:

![](002_03_-_Channels_000.png)

 

 

A **buffered** channel works differently... It is still created using the **chan and make** keywords BUT it needs a SIZE and a number of Buffers...

***myChannel := make (chan int, 5)***

 

When a Go_Routine wants to drop off some information on this BUFFERED channel...as long as the channel is not full..... It will drop off the data and it will not lock..... On the other hand, if the channel IS full, then our Go_Routine will wait until it gets some space (Lock) and then proceed to enter the data...

 

For **BOTH** cases, if a Go_Routine tries to READ from a Channel (Buffered or Un-Buffered) and there is NO data there, it will automatically LOCK

 

![](002_03_-_Channels_001.png)

 

 

![](002_03_-_Channels_002.png)

 

 

**Closing Channels**

 

Channels that are destroyed are not sent to be garbage collected....so why do this? (It just makes it useless to the sender and receiver

 

It turns out that closing a channel is a GREAT way to inform that channels [receivers]{.underline} that there are no more messages to be sent. This is GREAT

 

Closing a channel will ONLY close the sending side of the channel. Any message that is still inside the channel will stick around until is picked up by some receiver
