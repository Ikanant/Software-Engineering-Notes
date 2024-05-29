Something brings us to the cloud... 
 ![[Pasted image 20231114104435.png]]

Data centers live separate but we treat them as one as Availability Zones. When we create resources we are usually at the availability zones (AZ). Multiple AZ(s) are wired together to crate Regions! 

West Coast - East Coast - etc

Pops / Edge locations: These are extra machines ready to own requests. DNS help, etc... 

Within multiple data centers, if you have distributed data stores... within a region we can ensure STRONG consistency... AS LONG AS IT IS WITHIN A REGION (multiple datacenters - AZ) we have strong connection.... as long as we start connecting to different Regions, then things are not as ideal....

![[Pasted image 20231114105048.png]]

Back in the day we had:
![[Pasted image 20231114105150.png]]

THEN WE HAD:
![[Pasted image 20231114105241.png]]

This in not easily scalable though. One giant app running on a single server, not ideal.

This seems familiar:
![[Pasted image 20231114111043.png]]

How does the cloud fixes this?
* Cloud infrastructure introduces new concepts
* Off-cloud design doesn't always translate to cloud principles
* Lift and shift often limits the value proposition but addresses our time constraints for the compelling event
	* Fastest way to get us to the cloud, but not ideal. We wouldn't be taking advantage of the cloud really
* Applications that don't embrace cloud-native design don't fully realize
	* Scalability
	* Availability
	* Cost  benefits
* Cloud design principles are still emerging, but are based on well-known highly scalable application patterns.

**Migration to the Cloud**

These are NOT AWS specific... 
* 6 R's of migration
	* ![[Pasted image 20231114112124.png]]
* Twelve factor app methodology
* Cloud patterns
* DevOps
* CI/CD
* Automation
* Domain Driven Design
* Microservices
* Observability
* API-first approach
* Contract testing


**Technical Solution to our problems**
* Deploy to AWS Elastic Beanstalk Plantform as a Service immediately
	* We will drop our monolith into a beanstalk. Kinda like a contianer.. It's a simple OS that has everything for me to run an application on it. **AWS Elastic Beanstalk** ... We can START here
* Migrate over time to a microservices architecture
	* We are looking at the monolith and deciding what can we pull OUT.
* Use **AWS Lambda** to host our microservices
	* We want code to NOT be tied to an OS... this is what Lambdas are for. 
* Restructure the organization around business capabilities.
	* Organization of the application
	* Organization of the dev team
	* Organization around the PROBLEM and NOT as the technologies
* Delegate the ownership of each microservice to a dedicated team


The twelve factor app
![[Pasted image 20231114113726.png]]
https://12factor.net

Twelve Factor Manifesto:
1. Codebase
2. Dependencies
3. Config
4. Backing Services
	1. What are we talking to? Seamless conversation. We want this to be PORTABLE.
5. Build, release, run
	1. Quick, fast. No need to build for 3 weeks before moving forward. Quick
6. Processes
	1. The idea that module we are working on has process separate from storage. (We will come back to this) ... Stateless-ness within our services. A microservices has a chunk of code that is processing data... but we want it to WRITE ITS RESULT TO STORAGE... There is an active process that is executing the function in code... and storing the result... store it in DB, or whatever.
7. Port-binding
	1. Keeping it old school. These factors pre-date cloud. Port binding back in the day for monoliths, we could have multiple services on our server (WE ARE DOING THIS TODAY)... Back in the day we would communicate using port numbers.... not anymore... 
	2. In the cloud we NOW give it DNS resolvable names. DNS resolvable end points... nvm, this is what we actually DO today.
	3. This point highlights the importance of communicating with independent services
8. Concurrency
	1. Having the option for concurrency is IMPORTANT
9. Disposability
	1. I can get rid of old services relatively easily.
10. Dev/Prod parity
11. Logs
	1. We need to know what is going on across our systems. We still have sys-logs ... cloud watch / cloud trails act like system logs that help us with our observability. This is going to be important!
12. Administrative processes
	1. How do we control ALL OF THE ANIMAS IN THE FARM? We need tools to control all the components that create my system. We need admin tools to support it all

![[Pasted image 20231114115654.png]]

DOMAIN DRIVEN DESIGN
![[Pasted image 20231114115903.png]]

This should resonate with Object Oriented Programmers. We would look at the process/the nouns.. we would figure out the pieces in code/data that represented modules (cars/traffic-lights/wheels)... then the programming became controlling / modulating the pieces together... The closer 

DDD is pretty much the same thing. We are looking at the modules. the pieces. the information needed between the different pieces I have. how are my components going to talk. DDD is about looking at a problem, modeling in code and splitting that model into DOMAINS... so only certain data is shared in this module... ALL modules don't need to know what everything is doing at the same time. Scope things based on the component I am modeling. This allows me to create more modular/scalable code. Break things into zones of responsibilities. What needs to be shared and what doesn't.

Look at a problem, how do I split into pieces and how do I allow those pieces to talk to one another.

Don't break up a problem based on technology only...Use ubiquitous language so everyone can contribute.

**Bounded Context**: Central pattern. It is the focus of DDDs strategic design section. Deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships - Martin Fowler.

**here is the timeline:**
![[Pasted image 20231114120826.png]]


Goals:
* Introduce automation deployment
	* We already do this ... great
* Use pipelines for build and deploy
	* What is the repeatable process that I am using to get code pushed up the repo.
	* Building, Testing, Packaging, Deploying
* Each microservice will be its own codebase and build/deploy pipeline for isolation and independence.
	* Own codebase? That will be nice!
* Microservices will be exposed via Amazon API Gateway
	* Standardized API calls will make the communication between microservices WAY better.
		* Microservices for the most part are secure and in the bubble that is the cloud. How do we communicate with the outside world? It is a good idea to have a SINGLE point of connection to get this done... this is where the AMAZON API GATEWAY comes in
* Quality increases by:
	* Testing during build
		* Scope of our modules are smaller so hopefully things are going to be easier to test.
	* Suggest visibility into application performance with AWS X-Ray
	* Logging via Amazon CloudWatch metrics and CloudWatch logs


**Architectures and Patterns**
![[Pasted image 20231114122440.png]]

Instead of having one giant application... instead of having a few large applications talking to one another, we will build pieces of applications that live independently from one another.

![[Pasted image 20231114122532.png]]

CQRS: Command-Query-

Seems like AWS allows us to re-architect and re-use the same legacy infrastructure in the cloud... this is exactly what we are doing today:
![[Pasted image 20231114123220.png]]

We have pretty much replicated our setup in the cloud. All the discrete components that I used to know... now e have them again in the cloud:
![[Pasted image 20231114123441.png]]
These are called the foundation services

EVERY service in the world of AWS... the way we communicate with them is using API Calls. We communicate with the AWS Services:
1. AWS Cloud UI Console
2. Terminal. Just using the AWS CLI
3. Using code in Amazon SDK

![[Pasted image 20231114124131.png]]

There are TWO Levels of API calls for talking to services
* Low-Level APIs: Developers have full control over behavior
	* Offer more elemental control over what we need to do. Communicate more verbose/robust way... but by tinkering under the hood there is more responsibility to the system 
* High-Level APIs: Abstract complex flows for common tasks:
	* Try to keep it simple!
		* Amazon S3 TransferManager
		* Amazon SQS Batched Client
		* Amazon DynamoDBMapper

Advanced developers will be inclined to use low-level apis ... but using high-level ones are pretty nice.

Just know that EVERY service has high-level and low-level methods of communication.

**How do I get services to communicate with one another SECURELY?**
* All interactions are signed with AccessKeyId and SecretAccessKey using SigV4
* AccessKeyId and SecretAccessKey map to users or roles in IAM.
* You can:
	* Attach IAM roles and policies to allow or deny actions
	* Avoid the need to embed credentials in your applications.

**Security credentials: Priority Order**
1. Specified in the code
	1. Is there an accessKey / secretKey included in the code? That lets me know who this is
		1. YES: Uses those credentials to authenticate those requests
		2. NO: Blocks the request
	2. Not a great idea to put keys in the code. Even though this is the first place the env looks
2. Environment variables
	1. It's gonna look at the environment that is doing the requests...
3. Default credential profile in the credentials file
4. Amazon ECS container credentials
5. Amazon EC2 instance role

If it finds the key in step 1... then it will ignore the others... so take that into consideration.
![[Pasted image 20231114125728.png]]

Listen with your **EAR**
E: Effect
A: Action: What are the commands we are allowing them to use
R: Resources: On what resources do we want to apply this to?

The NEW way of doing this:
![[Pasted image 20231114125939.png]]

How do we Authenticate?
![[Pasted image 20231114130215.png]]


**CREATING YOUR BASE INFRASTRUCTURE WITH AWS CLOUDFORMATION**
Is this like Terraform? Yes

AWS BVeanstalk... pretty much we can think of it as a container... it's a sliver of the OS, the SDK of choice... and then we drop off our code... Easy
![[Pasted image 20231114142700.png]]

The lab I am going to work on will be:
![[Pasted image 20231114142904.png]]
![[Pasted image 20231114142941.png]]
