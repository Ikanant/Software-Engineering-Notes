Java Configuration

Sunday, February 10, 2019

10:29 PM

 

This module will just cover the configuration of Spring using JUST Java. Java configuration for Spring is the latest method available to hook our applications up with Spring. This method was generated from the desire of some developers to avoid mixing XML and source code together for configurations.

 

![No applicationContext.xml JAVA Too much XML Namespaces helped Enter Java Configuration ](004_Java_Configuration_000.png){width="4.166666666666667in" height="2.4166666666666665in"}

 

 

 

![\@Configuration public class AppConfig { \@Bean(name = \" customerRepository\" public CustomerRepository getCustomerRepository() { return new HibernateCustomerRepositoryImp1(); \@Configuration applicationContext replaced by \@Configuration \@Configuration at class level Spring Beans defined by \@Bean \@Bean at method level ](004_Java_Configuration_001.png){width="4.958333333333333in" height="3.3333333333333335in"}

 

**Setter Injection**

 

![\@Bean ( name= \" customerService \" ) public Customerservice getCustomerService() CustomerServiceImp1 customerService - w CustomerServiceImp customerservice. setCustomerReposito (getCustomerRepository()) ; return customeöService; = \"customerRe ory\" ) public CustomerReposit y getCustomerRepository() { return new HibernateCu rRe ositorylm 1 Setter Injection Simple as a method call \"Mystery\" of injection goes away Setter Injection simply calling a setter ](004_Java_Configuration_002.png){width="5.875in" height="3.816666666666667in"}

With XML there is a lot of wondering with what\'s going on... a lot of that goes away with JAVA configuration approach. Setter injection is just a matter of calling a setter on a Bean. We will define a bean of type CustomerService that will return a bean of type CustomerService (OR a bean named customerService).

CustomerServiceImpl

The circles in the image above are just emphasizing that we are wiring the customer repository inside of our customerService.

 

Keep in mind within this code, Spring is still doing A LOT of work behind the scenes. For instance, this beans by default are SINGLETON and will only execute the first time is called and then return the cached instance after that.

 

**Constructor Injection**

 

Works just like setter injection. Instead of calling the setter we just call the defined constructor that we have for that instance.

 

The main difference to note is that now we have things stored in a container and we are no longer passing around objects. We can pull things from the framework using the bean and getBean aliases we set up in our configurations

 

![\" customerService \" ) public CustomerService getCustomerService() { CustomerServiceImp1 customerservice = new return customerService; \@Bean(name = \"customerRepository\") public CustomerRepository getCustomerRepository() { return new HibernateCustomerRepositoryImp1(); Constructor Injection Just like setter injection ](004_Java_Configuration_003.png){width="4.291666666666667in" height="2.825in"}

 

**Autowired**

To Autowire our application when using JAVA configuration, we just need to add the \@ComponentScan({\"com.pluralsight\"}) to our AppConfig.java

 

Like the XML configuration, we just mark whatever we want to be autowired by NAME or by TYPE.

 

One thing different for the JAVA configuration over the XML configuration is by using JAVA I can mix pieces I want more natural.

 

One really power thing I ended up committing last... is that by using autowired and \*Stereotypes (@Service && \@Repository for example) I didn\'t even need to manually mention the beans I was using within the appConfig.java file. Spring is smart enough to parse through the code and find all of our components automatically. Cool!

 

 
