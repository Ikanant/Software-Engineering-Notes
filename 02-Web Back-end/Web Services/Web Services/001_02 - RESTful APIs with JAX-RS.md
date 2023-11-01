02 - RESTful APIs with JAX-RS

Friday, April 29, 2016

12:27 PM

**\[ 1 - INTRODUCTION \]**

Sections:

1.  REST API concepts

2.  Implementation with JAX-RS

REST Web Services - SOAP Web Services

Web Services Characteristics:

1.  They are web services, so their exchange of data happens over the web or HTTP

    -   Client ---HTTP Request---\> Web service

    -   Client

2.  Protocol:

    -   When we try to send a message to a web service, or receive one as a client, this message needs to be written in a certain format. This format can be referred as the protocol.\
        Sometimes, web service can use STANDARD protocols like SOAP.

        -   The standard protocol used by SOAP Web services is SOAP. Simple Object Access Protocol. This is a specific format of messages (XML) and the certain rules about how this XML should be used

    -   REST has no PROTOCOL.

        -   REST clients can send messages using XML or they can also send messages using JSON or even TEXT. As long as the client and the server understand each other, everything is ok.

3.  HOW

    -   Through HTTP there are different methods that are available to send and receive data. GET, POST, etc... so which of these methods do we need to use to exchange data between client and web services??

        -   There is NO answer to this. Messages can be sent and received using any or all of the HTTP methods available. There are guidelines to use in order to efficiently utilize RESTful web services, but we can technically use which ever one we want.

        -   SOAP web services only use POSTs

4.  Service Definition

    -   When using a certain library within your application, you need to know a series of things before officially using the tool. You need to know the name of the class,the name of the methods to use, the input parameters, the return type, etc... In the web service world we have the same concept. This information is typically known as Service Definition:

        -   In SOAP web service we have the WSDL: The WSDL file will be the one containing all the information about your web service. What are the methods, input types, etc... This document is available to all clients

        -   For REST: There is NONE.

            -   Most REST web service have little to no documentation.

            -   If they have documentation they are typically found within the websites that offer such web services

            -   IN FACT, the BEST designed RESTful web services wouldn\'t even need documentation.

            -   WADL is the similar file that RESTful web services can use but it is very very rarely used.

**REST ---\> REpresentational State Transfer**

     

     Representational State Transfer is actually not a web service at all. It is more like an architectural style.

Let\'s think that we are working on the architecture of a new application we are building, there are certain decision we need to take, there are certain choices we have to make, certain criteria to think about. REST consist of a coordinated set of these criteria and constraints that it can use to guide you in your application architecture. A set of GUIDELINES that work well together. It is a style of architecture. We can use the style of architecture for any application however if we apply the styles and guidelines when architecting a WEB SERVICE you have: a RESTful Web Service.

*Unlike SOAP web services where a committee tells what we should be doing, in the rest full web service world we don\'t have any specific rules to follow. You can have a spectrum.*

People often categorize web services as:

1.  Completely RESTful

2.  Not fully RESTful

3.  Not RESTful

The goal when building RESTful web services is to make it as RESTful as practically possible. There are no strict rules, these are guidelines, and we try to follow this guidelines as strictly as possible.

In general the main thing to think when writing a RESTful web service is to make it easy for your consumers.

**\[ 2 - REST AND HTTP \]**

REST is inspired by a lot of the concepts of the HTTP specifications

HTTP - **Hyper Text Transfer Protocol**

HTTP is a way to exchange and communicate information online.

The stuff that we transfer through HTTP messages is known as Hyper Text. Hence Hyper Text Transfer Protocol

Hypertext: A structured form of text with an interesting property. It contains logical links to other text. Knows as HyperLinks

A common way to write Hyper Text is in a common language called: **H**yper **T**ext **M**arkup **L**anguage (HTML)

Going over HTML code is a little beyond this lesson, instead we are going to go over some of the concepts that inspired REST from HTML and how this concepts apply to RESTful APIs and services.

**Concepts**:

1.  Resource location

    -   Similiar to regular web sites, web services have regular url and addresses too. Since these APIs are not meant to be read by humans, these RESTful APIs pretty much contain the bare data.

        -   Resource based URL:

            -   Example: Lets say we want to access the weather information for our current location based on our zip code. For a regular page, we would commonly use something like:\
                *weatherapp.com/weatherLookup.do?zip-12345\
                *For this case, we are pretty much telling our website to DO something, to perform some sort of action related to the information we are providing.

            -   Example2: On the other hand, when using web services we would commonly see things like:\
                *weatherapp.com/ipcode/12345\
                *In this case are are pretty much not telling the site WHAT to do, we are rather providing some information that will return us some relevant data back. Looking up something that already exists

2.  HTTP Methods:

    -   GET

        -   Lets you get information from the server

    -   POST

        -   Lets you submit information to the server

    -   PUT

        -   Not commonly used in regular application but often used in RESTful APIs.

        -   Lets you submit data to the server but not the same as POST

    -   DELETE

        -   Remove a resource from the server

    -   A good RESTful APIs makes good use of all these HTTP methods.

3.  Metadata:

    -   For web SITES, one useful snip of information that every method has is the Status Codes

        -   Number that shows up in the very first line of the HTTP response

        -   200 - Success

        -   500 - Server error

        -   404 - Not found

        -   Why send status codes? Well, they are helpful to understand the problem that the user faced when doing something within your application. So, what happens with web services?

            -   Web services depends on this status codes too to really understand what is going on with the web service request.

4.  Format:

    -   There is no specification that enforces what the format of the data should be. Could be XML, could be JSON, could be other format....so, how can the server even identify what kind of data is sent? Similarly, how does the client know what data format is returned by the server?

        -   HEADER VALUE called CONTENT TYPE

        -   The header value contains Metadata.

        -   Content Types:

            -   text/xml

            -   application/json

            -   etc

        -   The same API could potentially return various content type...this is done with the 

            -   **CONTENT NEGOTIATION**

                -   Basically the client says I process XML (prefer XML) and then the server that could return XML or JSON looks at that and determines "this is a client that uses XML, so I will give him XML\"

**Summarize:**

     When you design a RESTful API:

1.  Resource based URIs

2.  HTTP methods (we need to choose the right one)

3.  HTTP status codes (it needs to return the right status codes...success, failures, etc)

4.  Message headers (example: format of the messages)

**\[ 3 - Resource URL \]**

Before we get into writing code for our REstful API we will work on Design. so, how are REST APIs designed ?

For this course we will create a Messenger App:

-   We will POST messages

-   Comment on messages

-   Like and Share messages

-   User Profiles

There is no right or wrong way to create URI, but if we are writing an REST API it is better that we follow this best practices.

Back in the day, (around the 1980s) the pages used often were stored as static web pages. (Static HTML web pages). To access the pages of that site, we enter the URL and the path to the html page. So every page had a UNIQUE URI. To start working on RESTful webs services it is often helpful to start thinking about static pages. Think now for example a site like Facebook...when you open an account on Facebook we get our own profile. (That is obviously dynamically generated pages)...if this were to be static HTML pages, then we would have individual HTML pages containing the profile information of each person. So the name of the html page would most likely be the name of the person who owns that profile. If this was the case I will probably not want to put all this files in the root directory, for this example I would most likely use a sub directory called profiles in which I would store all the HTML profile pages. SO if I had to access my page in this profiles I would end up with:

     /profiles/jonathan.html

Now if we drop the html extension then we would have a RESTful URI.

     /profiles/Jonathan

This would be a RESTful base resource URI. So, when creating URIs think of resources and create unique URIs for them. Now, how about POSTs or messages. Ok, so, lets think that every message has a unique ID. For example:

    

     /messages/1

     /messages/10

Notice that URI contain NOUNS and not verbs. Things in the system. All resources. We don\'t have URIs called /fetchMessages. Typically there should be no verbs within our URIs.

Resource paths should all be PLURAL. It\'s not /message or /profile. This is good practice because it makes it clear there are multiply messages and profiles, etc\...

The advantage of using such resource based URIs is that they are not dependent of the framework. So there is no .do or .action on our URIs. Or ?id=123 parameters. These details are of no significancy of our client. Another advantage is that, by using resource based URIs we make our code stand future changes.

So, let\'s say we have a comment with ID 20. How would our URI look like? message/20 ? This is not necessarily incorrect, but we do have another important thing to think about.

**Resource Relations:**

From time to time we will encounter resources that dependent of other resources. For example lets say we have a message and then a series of comments (1-many relation). By looking a certain comment as /comments/20 we would then not effectively connect the relation that the comments have with the proposed message. Let\'s say we have 2 messages:

-   Message ID:1

    -   Comment 1

    -   Comment 2

    -   Comment 3

-   Message ID:2

    -   Comment 4

    -   Comment 5

If I happen to place all the messages inside a common messages folder, I would then loose all the relationship that such messages have with their respective comments. What would a proper solution be ?

Well, we can just create a sub folder under the proper messages folder that would include such comments. If I do this, what would be the proper URI for comment ID 2?

     Simple ---\> /messages/1/comments/2

So, how about MANY-MANY or ONE-ONE relationships. We will put this topics aside from now to better explain web services.

**\[ 4 - Collection URIs \]**

We can think of Restful URIs as belonging to two types:

1.  Instance resource URIs

    1.  used for example when retrieving some data based on an ID. For example if we get the user info with ID=1

2.  Collection resource URIs

    1.  used for example when retrieving a collection of elements. for example, messages/2/comments. This will give us all comments for message with id = 2
