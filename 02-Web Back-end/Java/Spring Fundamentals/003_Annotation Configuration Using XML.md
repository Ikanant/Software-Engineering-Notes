Annotation Configuration Using XML

Sunday, February 10, 2019

5:03 PM

 

Annotations were the second option for Spring to wire up our application. In the last samples we did we used autowiring in order for our classes to be dynamically discovered through our XML classes.

 

Now let\'s do the same but this time we will use Annotations without necessarily use BEANs inside of our application context.

 

![](003_Annotation_Configuration_Using_XML_000.png){width="6.25in" height="2.975in"}

 

There are 3 main annotations for CORE spring that help us define components or beans inside of our application. The main ones are:

 

![XML Stereotype Annotations \@Component, \@Service, \@Repository Semantically the same \@Component - any POJO \@Service - business logic layer \@Repository - data layer ](003_Annotation_Configuration_Using_XML_001.png){width="7.833333333333333in" height="3.941666666666667in"}

 

 

**Autowire**

A lot of developers feel like AUTOWIRING using annotations is way more straight forward. autowiring a method is hidden because it is tied from where you place the annotation tag.

 

We can autowire at three places:

1.  Member variables

    a.  ![Autowired Member Variable \@Autowired private CustomerRepository customerRepository; ](003_Annotation_Configuration_Using_XML_002.png){width="3.2666666666666666in" height="1.3333333333333333in"}

2.  Constructor

    a.  ![Autowired Constructor Injection \@Autowired public CustomerServiceImp1(CustomerRepository customerRepository) { System. out . are using constructor injection\"); this. customerRepository = customerRepository; ](003_Annotation_Configuration_Using_XML_003.png){width="3.3in" height="1.2833333333333334in"}

    b.  We create a constructor for the type of object we want to inject in (OR objects) and simply mark that constructor with autowire. This approach can be problematic if we at some point switch back to Setter injection since we would have eliminated our default constructor.

3.  Setter injection

    a.  ![Autowired Setter Injection private CustomerRepository customerRepository; \@Autowired public void setCustomerRepository(CustomerRepository customerRepository) { System. out. print1n(\"We are using setter injection\"); this . customerRepository = customerRepository; ](003_Annotation_Configuration_Using_XML_004.png){width="3.3333333333333335in" height="1.7166666666666666in"}

    b.  It is somewhat interesting to go with this route, because if we were to apply test driven development to our workload, this would be the right approach.

 

![O JSR-330 Dependency Injection for Java Beyond our scope Why Spring? ](003_Annotation_Configuration_Using_XML_005.png){width="6.641666666666667in" height="3.8583333333333334in"}

 

JSR-330 is not covered within this lecture. BUT it is important to note that JAVA started to noticed the importance of dependency injection and decided to offer a built in solution for JAVA project. Sadly, this tool (JSR-330) is not as feature full as Spring is... so though it does offer some convenience, for enterprise web development, Spring is the way to go.
