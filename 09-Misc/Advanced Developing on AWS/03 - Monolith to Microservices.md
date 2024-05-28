Agenda:
* Microservices
* Serverless
* A look at Cloud Air
* ...

![[Pasted image 20231114173729.png]]
So far in the Lab we got the app deployed in Elastic BeanStalk

...
Now we want o migrate ASPECTS of that service our of the monolith

![[Pasted image 20231114174010.png]]

If we break up app into their own function, each can have their own data store... their own mini-database... instead of communicating with one giant data source.

Don't confuse with SOA
![[Pasted image 20231114174131.png]]

* Organized around business capabilitites
* Decentralized ownership of services
	* Loosely coupled components. Each micro-service is in charge of its own component and processes
* Automated deployment
	* Tinker with code, save and push it... I want to be able to deploy without affecting ANYTHING else
* Intelligent endpoints
	* Be able to independently communicate with that service... no need to use ports ... use DNS!

![[Pasted image 20231114174346.png]]

![[Pasted image 20231115100940.png]]

Here is the goal that we are going to try to build up in the demo

![[Pasted image 20231115101423.png]]

![[Pasted image 20231115104728.png]]

This is the direction that we are going? 

When going to the cloud, we have to think about the services/functions that we need for our product and THEN, we just look at the modules/building-blocks that ALREADY live in the Cloud. Don't re-invent the wheel! When we build apps in the cloud, we are sequencing together what already lives in the cloud!

**PROCESS** (this is going by the 12-factor mentioned above)
Keep it separate from storage. Allows us to maintain statelessness 

![[Pasted image 20231115110137.png]]
How do we know if our app can be good for serveless applications... Do we NEED a direct connection to the underlying machine in order to do it's job? then maybe not.... BUT if the application can run in its own bubble... then we are good.

**LAMBDAS ARE THE FUTURE**
![[Pasted image 20231115111403.png]]

Lambdas are limited to 15 minutes only... at least by default.

Lambdas are supposed to be light-weight... generally single purposed functions. Don't try to put a giant library in there

... AVOID USING RECURSIVE CODE IN LAMBDAS

FarGate is the way to use the server less infrastructure with CONTAINERS

![[Pasted image 20231115115806.png]]
So, whenever we NEED access tot he outside world (or the outside world coming to us) ... we SHOULD use Gateways... we can in fact create a leaky application but it is not recommended. The API Gateway is the way to go.

Think of it as the door between all the function calls and the requests/responses that are coming from the outside world.

Powered by CDN? - It's a service that's DNS resolvable that lives and uses the DNS caching functionality in our Content Delivery Network.
When creating a Gateway, it generates a URL that is a DNS resolvable end point. So when we create the gateway it has a home and the way the world finds it, it uses the CDN.

![[Pasted image 20231115122348.png]]

![[Pasted image 20231115123133.png]]

![[Pasted image 20231115123331.png]]
Cognito is the primary tool to authenticate ourselves with our API gateways... but if for some reason we got some weird unique authentication protocol... one that Gateway by default does not support.... you CAN extend the functionality of gateway with our own custom Lambdas ... write additional code to add more to what Gateway is.

Want to test lambdas locally???
![[Pasted image 20231115123737.png]]
It's not EVERYTHING that lambdas can do, but pretty amazing still


![[Pasted image 20231115140410.png]]

AWS Cloud Development Kit (Not SDK - Software Development Kit)
Bridge between programming languages with services that we are trying to control.

![[Pasted image 20231115140456.png]]
For example, here we are crating a FarGate serivce... only with CODE



How about Databases?
![[Pasted image 20231115152120.png]]
