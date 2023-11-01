Bean Scopes

Monday, February 18, 2019

8:31 PM

Beans ARE NOT Patterns

![Scopes 5 Scopes Valid in any configuration Singleton Prototype Valid only in web-aware Spring projects Request Session Global ](005_Bean_Scopes_000.png)

**Singleton**

The singleton design pattern restricts the instantiation of a class to ONE object. A singleton is the default BEAN SCOPE inside of Spring. So if you don\'t give a bean a SCOPE it will automatically get assigned the Singleton Scope.

-   One Instantiation

-   Default Bean Scope

-   Single instance per Spring container

![\@Service( \" customerService \" ) \@Scope ( \" singleton\" ) public class CustomerServiceImp1 implements CustomerService { Singleton - Java Config \@Scope Requires AOP jar ](005_Bean_Scopes_001.png)

![\<bean name=\"customerService\" class=\"com.pluralsight.service.CustomerServiceImpI\" autowire= \" by Type \" scope=\" singleton\" \> Singleton - XML Config ](005_Bean_Scopes_002.png)

**Prototype**

The Prototype design pattern guarantees a UNIQUE instance per request. Each time a request is made from the container you are guaranteed a unique instance.

-   Per Request

-   Guaranteed unique

-   Opposite of Singleton

**Web Scopes:\
**Outside of the scope of the course but just keep in mind:

1.  Request

    a.  Returns a bean per HTTP request. Similar to Prototype except is for the lifecycle of the request (short, but longer than prototype which is one instance per every time I ask the container for a bean)

2.  Session

    a.  Return a single bean pero http session. That will live for as long as that user session is alive

3.  GlobalSession

    a.  Alive for the duration of our application
