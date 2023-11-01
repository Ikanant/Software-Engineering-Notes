01 - SOAP Web Services in JAVA

Friday, April 29, 2016

12:27 PM

**SOAP: Simple Object Access Protocol**

There are 2 types of WEB Services:

1.  SOAP

    1.  Specification: JAX-WS

2.  REST

    1.  Specification: JAX-RS

**SOAP Web Services:** A Service that is provided over the network. How is it different from regular web-sites? A web-site is meant for human consumption, while a web-service is meant for code consumption, or application level consumption.

**What is a Web Service?**

Well, imagine you have a web application hosted in a server. Within this application, there will probably exist many methods that are really useful. Lets assume we have a method called: 

*getProducts()*. This method (within your application) will access a database (also hosted on your server) and will retrieve all the merchandise you are offering to your users. Now, consider we have a friend who also wrote his own web application and he decides to offer the same products as you and asks for the *getProducts()* method... One thing you can do is just package your function in a JAR file and send it to your friend. This option would bring a lot of problems. Some of them can be that your method contains certain dependencies that our second application does not yet contain. Another problem could be that because your database is hosted in your server, the second web application will most likely not have access to such information. In conclusion, providing the JAR files would not be a solution......HENCE the use of Web Services. As mentioned before, a web service is meant for application level consumption (code consumption) ..... the same way that a user goes to a website and access something, a web service offers external applications its methods, along with their access to certain databases and dependencies that will be useful for anybody. Then, going back to our example, if our *getProducts()* method is offered in a web service, then our second application could just access it by just acquiring the proper credentials

**What is Standard Technology for WebServices?**

INTEROPERABILITY

Interoperability is the MAGICAL option that we get with Web Services for which different application that use different programming languages can still access each other and grab their tools. For example, an application written in C++ or .NET can still access a Web Service written in JAVA.

**Web Services JARGONS**

Let\'s consider an implementation application that we have written in JAVA. If we want to make another consumer class use all or some of the methods found within our Implementation class, we would just create an interface.

CONSUMER ---\> INTERFACE ---\> IMPLEMENTATION

But now let\'s say we would like to do somewhat of the same thing for a web service implementation. In this case, one of the main problems that would arise, would be that we do not know what the consumer and the implementation technologies match or not. meaning we can have a JAVA implementation and a .NET Consumer.... so what is the solution to this? Well, the developers of the web services then thought of using a single FORMAT that would be understood by all the technologies and all the consumers: XML

**XML format**

So, whenever we create a web service from our application, we just export an XML document. This document is commonly known as a WSDL

**WSDL = WEB SERVICE DESCRIPTION LANGUAGE**

This document will contain the contract to your web service

Similar to an INTERFACE, a WSDL file contains:

1.  Methods

2.  Arguments

3.  Return types

**UDDI - Universal Description Discovery & Integration**

So, where would you as a developer get a hold of these WSDL files? Ok, so there exists an easy universal directory that contains tons of these Web Services along with their description about what they do...This YELLOW PAGES of web services is knows as UDDI.

When sending information to a web service, similar to how we receive XML files we will send another XML file. This is from what we talked about before that the client and the web services might be written in different technologies. The XML that will be sent to the server needs to be formatted very specifically....in a way, it is a protocol.

**What is the protocol name to use when sending XML files back to the web service?**

SOAP

 SOAP: A way in which the sender and the receive understand each other contents. Simple Object Access Protocol

**Who does the conversation from our client code to an XML message?**

This conversation will be done by a separate class within the clients application.This class is known as an SEI: **Service Endpoint Interface.**

**Service Endpoint Interface:**

It access an interface to your web service endpoint. We do not need to write this class, we can have it automatically generated for us!

The SEI will be different for the various technologies that will implement it. The SEI that is used for java application will know how to handle everything regarding that specific language (like data types) whereas with C++ the SEI will be different in a way that will know how to handle C++ data.

**Hands on:**

I will be writing a simple java project that will utilize a free to use web service online. The one that I am going to use will let us determine the geo location of a computer based on their ip address. So if you pass your IP address it should tell you the country you are in.

webservicex.net/ws/WSDetails.aspx?CATID=12&WSID=64

webservicex.net/geoipservice.asmx?WSDL

When looking at the second link we should not really care too much about its content because there are many tools to parse the XML information. BUT the one thing we should care about it (in this case at the button of the page) is the **wsdl:service name** and its attributes (port, etc).

To get all the code from the desired Web Service we would go to our terminal and type:

*\>wsimport* [*http://www.*webservicex.net/geoipservice.asmx?WSDL](http://www.webservicex.net/geoipservice.asmx?WSDL)

*w*simport is a command that comes with the basic JAVA JDK.

By default all the java files will be downloaded to your computer and automatically compiled into .class files. Right then the java files will be deleted. If the client wishes to get the java files to do some possible modification, then that\'s there the wsimport \[options\] link would come into place.

Some of the options are:

-keep //will keep the java code

-s //specify where to generate the source code

On the actual code that gets the Web service you first create an object of the web service name and then make a object of the original webserivce name\'s port instance. Once we have done this we will be able to use the webs service tools.

Example:

GeoIPService ipservice = new GeoIPService();

GeoIPServiceSoap geoIPServiceSoap = ipservice.getGeoIPServiceSoap();

GeoIP geoIP = geoIPServiceSoap.getGeoIP(ipAddress);

System.out.println(\"Country code: \" + geoIP.getCountryCode());
