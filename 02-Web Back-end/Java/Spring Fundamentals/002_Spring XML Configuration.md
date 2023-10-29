Spring XML Configuration

Sunday, February 10, 2019

1:16 PM

 

Why use XML?\
XML configuration was one of the first solutions ever implemented to configure Spring and it is still widely used. Things are considered to be simpler using XML, and there is a clear cut of separation of concerns when using XML

 

![XML First Approach Simpler Separation of Concerns ](002_Spring_XML_Configuration_000.png){width="2.816666666666667in" height="1.0583333333333333in"}

 

 

XML configuration for Spring begins with a file that we will name applicationContext.xml. This file is name is arbitrary and can be named differently, but in the JAVA community it has become somewhat of a standard.

 

![Machine generated alternative text: XML applicationContext.xml Name doesn\'t matter Spring Context sort of a HashMap Can simply be a registry XML configuration begins with this file Namespaces aid in configuration/validation ](002_Spring_XML_Configuration_001.png){width="4.191666666666666in" height="1.925in"}

 

There are some namespaces that Spring developers have put together to help with the configuration and validation of our project. We will be adding one of those namespaces to the top of our application but basically we put an XML snippet at the top of our applicationContext and it knows what our bean namespace is to help us configure the rest of our file.

 

![](002_Spring_XML_Configuration_002.png){width="6.716666666666667in" height="2.091666666666667in"}

 

 

Xmlns (XML Namespace): Default namespace of beans

XSI: This just says this is an XML schema instance

SchemaLocation: Added to our XML file and it\'s what gives us context sensitive help inside of our application. IDE now will offer suggestions when inserting a \< inside the beans section.

 

![XML Declaration \<bean name=\" customerService\" class=\"com.pluralsight.service.CustomerServiceImp1\" autowire=\" byName \" \> \<property name-\"0\" ref=\" customerRepository \" \</bean\> ](002_Spring_XML_Configuration_003.png){width="5.758333333333334in" height="3.033333333333333in"}

 

\^\^\^ This is the definition of a BEAN in XML. This represents where we want to put our business logic inside of our application.\
 

Beans are basically classes. There are just POJOs to be used inside of our application context. Defining beans can be thought as replacing the keyboard NEW. So wherever we are using the keyword NEW within our poject\
\
like: CustomerService cs = **new** CustomerServiceImpl();

 

That\'s somewhere we can look into removing that configuration and placing it into an XML file. One thing that\'s important with this is that we always want to define the class but USE the interface.

 

By using beans, we can now change configurations without recompiling our code. We can switch from dev to test without recompiling. This technique is called **Separation of Concerns.**

![\<bean name=\"customerRepository\" class= \" com . pluralsight . repository. HibernateCustomerRepositoryImp1 \" Beans Essentially Classes Replaces keyword new Define Class, use Interface ](002_Spring_XML_Configuration_004.png){width="4.95in" height="2.1416666666666666in"}

 

Now that we have a bean defined, how do we use it? **INJECTION**

 

There are 2 types of INJECTION to remember:\
 

1.  Setter injection

    a.  Using exactly what it sounds like. Using the getters/setters of our bean

2.  Constructor Injection

    a.  Use the defined constructors

 

We can use BOTH ways of injection together

 

**Constructor Injection** guarantees us a bunch nice things using simple constructs in java but mainly it is that we have a defined contract when we create each object.

One positive & negative of this is that we have to have a constructor defined for each possible situation.

 

Constructor injections are INDEX based on NOT NAME based.

 

![14 \< bean n ame= \" customerServi ce \" \<constructor-arg \</beans ](002_Spring_XML_Configuration_005.png){width="5.691666666666666in" height="1.125in"}

>  

By Index we mean that if we have three arguments to pass in to our constructor, we have to specify that here in the applicationContext file.

 

**Autowire**

 

Early on (probably when I was originally working with Spring) Spring got a bad reputation for having way too much configuration done through XML. To counter this, Spring developers created a new method called Autowire, to make sure we wire beans together.

 

**Autowire Types:**

1.  byType

    a.  Allows a property to be AUTOWIRED if exactly ONE bean of that property type exists within a container

        i.  Example: Our customer repository was a bean of a specific type. If we had 2 beans of the same class but with different names, we would get an exception using this approach

2.  byName

    a.  Similar to the byType but it uses the name of the bean instead. Which would solve the issue above of multiple beans referenced within the same code

3.  Constructor

    a.  Constructor injector behaves similar to setter injection but it just uses constructors.

        i.  Constructor AUTOWIRING works very similar to autowire byType. It looks for an object of that type injecting the arguments of the constructor

4.  No (or none)

    a.  Way to specify that a bean cannot be autowired at all

 

![\< bean name= \"customerService \" \<constructor-gcg ](002_Spring_XML_Configuration_006.png){width="5.8in" height="0.9666666666666667in"}

 

 

![Summary applicationContext.xml Bean Definition Setter Injection Constructor Injection Auto wiring ](002_Spring_XML_Configuration_007.png){width="7.45in" height="3.783333333333333in"}

 
