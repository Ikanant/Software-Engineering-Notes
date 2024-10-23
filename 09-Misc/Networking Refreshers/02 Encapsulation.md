One thing that's important for everyone to remember is that sites can be quite large. Every web developer should know that with the introduction of front-end frameworks, sites often sent quite a bit of data to the client side to be managed, rendered and ran by the user's browser. So, taking care of the size of these files is quite important. Some of the protocols I mentioned in the previous note, literally have a **maximum** about of data that they can send.

![[Pasted image 20241021135441.png]]
When dealing with a web page, we can just split files.


![[Pasted image 20241021135450.png]]
Once we have the data broken down into smaller pieces, we can then add it to a HEADER. The transport layer sets up the session between the client and the server. Once we have this connection stablished there are a few things that happen, we will have info above to keep track of everything that happens. The analogy to be used here is similar to when you write a birthday card to a family member. The card  is inside of an envelope that gets sealed up. The envelope contains data like the address of the person you are mailing it too as well as a return address for yourself and then you have the message that is considered the *Payload*.

The envelope is pretty much known as a **SEGMENT**. Any chunk of data with a transport layer header.
![[Pasted image 20241021140128.png]]
This particular SEGMENT HEADER is known as a TCP Header. This info allows the client and the server to keep track about what information has been sent/received.


 