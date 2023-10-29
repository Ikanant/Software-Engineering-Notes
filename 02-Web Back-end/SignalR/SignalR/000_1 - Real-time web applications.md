1 - Real-time web applications

Thursday, July 12, 2018

6:51 AM

![Module Real-time web applications Polling and long polling Server sent events WebSockets ](000_1_-_Real-time_web_applications_000.png){width="6.283333333333333in" height="2.625in"}

 

 

Real-time Web Applications examples:

-   Email clients (you don\'t have to keep reloading the page when a new email gets received)

-   Social Media

-   Web Documents

-   Auctions

-   Gaming

-   Stock quotes

 

SignalR can work with web applications, installed applications or even mobile software.

 

![04 」 」 OS ](000_1_-_Real-time_web_applications_001.png){width="7.083333333333333in" height="3.3in"}

 

There are several techniques SignalR uses in order to communicate with whatever client is using the server data... In SignalR these are called **Transports**

 

**This module will cover:**

 

-   Long polling

-   Server sent events

-   Websockets

 

Remember: AJAX is a technique to let the browser make requests to the server without the need of a page reload.

 

As we know, HTTP is pretty much the process in which the client requests data from the server... if we make our code in the front end periodically ask for data to the server.... This is called POLLING.

 

The problem with polling is that we can easily see how the server can potentially be overflown with requests and ultimately crash for us... SingalR resolves this by using LONG POLLING\
 

 

The idea of LONG POLLING is that the browser will make a request to the server, which is going to then be left OPEN until there is an update. When there is no update from the server, the clients request will timeout, when that happens then the browser will just make another request.

 

![](000_1_-_Real-time_web_applications_002.png){width="6.283333333333333in" height="3.2in"}

 

![adocument . .addEventListener(\"c1ick\", e { e. preventDefau1t() ; const product = document . getE1ementById( \" product \" ) . value; --- document .getE1ementById( \"size\") .value; const size --- fetch( \" /Coffee \" , method : \"POST\", body: { product, Size } . then(response response. text()) . then(text poll(text)); ](000_1_-_Real-time_web_applications_003.png){width="7.5in" height="3.225in"}

 

![• WiredB•ain JavaScript Files 1 2 4 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 24 pollWithTimeout (url, options, return Promise. fetch(url, options), new reject) timeout - - 9090) setTimeout(() reject(new Error( \'timeout\' j); = (orderld) { poll pollWithTimeout(• /coffee/\${orderld}• ) timeout) . then(response { if (response. status 200) { const statusDiv = document.getE1ementById(\"status\"); response.json().then(j { statusDiv. innerHTML j.update; if . finished) poll (orderld) ; . catc response poll orderld 152 % ](000_1_-_Real-time_web_applications_004.png){width="8.533333333333333in" height="5.183333333333334in"}

 

 

Though the code above is better than regular polling.... There is even a better solution....\
 

**SERVER SENT EVENTS (SSE)**

 

SSE are considered an HTML5 feature.

The server creates an HTTP connection to the browser... and then the browser will listen for messages that will later come in as a stream. The browser will use an object called **EventSource** to process incoming messages

 

![](000_1_-_Real-time_web_applications_005.png){width="8.533333333333333in" height="4.833333333333333in"}

 

![1 2 4 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 listen = (id) { var eventSource = new EventSource(• /Coffee/\${id}\" ); (event) { E eventsource .onmessage - const statusDiv = document.getE1ementById( \"status\" statusDiv. innerHTML = event. data; gdocument.getE1ementById( \" submit\") e { e. preventDefau1t(); const product document .getE1ementById( \"product\") . value; const size = . value; fetch( \" /Coffee\" , method: \"POST\" , body: { product, size } .then(response response.text()) .then(text listen(text)); ](000_1_-_Real-time_web_applications_006.png){width="8.575in" height="4.716666666666667in"}

 

SSE is a much better option than any type of Polling

 

Server Events Benefits:\
 

1.  Simple HTTP

2.  Auto reconnects

3.  No support for older browsers

4.  Easily polyfilled

5.  Maximum HTTP connections issue

6.  Just text messages

7.  One-way connection

 

**Web Sockets\
\
**Web sockets go even a step further than anything mentioned above:\
\
Web Sockets: A standardized way to use TCP socket through which messages can be sent from server to client and vice versa. (no latency of HTTP).

 

TCP Socket remains open until the stream of messages gets done. Most modern sites are using some type of web socket when working with up to date browsers efficient way of transport.

 

**Web Sockets**

1.  Full duplex messaging:

    a.  Client can receive and send web sockets simultaneously

2.  No 6 connection limit

3.  Multi data-type support

    a.  We can send not only text, but also BINARY (so we could support streaming audio and video)

4.  TCP socket upgrade. (regular HTTP request uses some kind of TCP socket as well)

5.  WS Protocol

 

![](000_1_-_Real-time_web_applications_007.png){width="6.025in" height="3.975in"}

 

 

Every web socket starts its life as a simple HTTP socket. Once the server gets the request from the client and aggress for the request, then it turns it into a web socket onward and it\'s ready to send messages through:

 

![](000_1_-_Real-time_web_applications_008.png){width="5.575in" height="3.0833333333333335in"}

 

![](000_1_-_Real-time_web_applications_009.png){width="5.583333333333333in" height="2.65in"}

 

**WebSocket Keys:**

-   Client sends random string

-   Server add constant and hashes and base64 encodes

-   Sends key back in accept header

-   Cache busting

 

 

 
