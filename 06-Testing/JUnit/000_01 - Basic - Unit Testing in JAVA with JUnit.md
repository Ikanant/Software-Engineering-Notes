01 - Basic - Unit Testing in JAVA with JUnit

Friday, April 29, 2016

12:24 PM

 

JUnit is design to be a unit testing framework for JAVA. JUnit is packaged as a single JAR file that is basically a library of functionalities that makes it easier for a developer to create Unit tests in JAVA and verify the results of those tests. JUnit can be thought of as the set of common things required for doing UNIT testing in JAVA (we can perform such tests in many other ways).

**JUnit Features:**

1.  Asserts

    -   Specify what you expect and compare it with what you actually got by using a power set of assertions

2.  Test setup and teardown

    -   Setup test data before our test actually run and tear down that data or context after it ran

3.  Exception testing

    -   Verify that an exception was/not thrown

4.  Test suites

    -   Organize JUnit test cases into test suites

5.  Parameterized testing

    -   You can create tests that opperate on sets of data that you feed into those tests

6.  Assumptions

    -   Ignore tests that aren\'t even qualfiied to run on a particular platform or context

7.  Rules & Theories

    -   Rules allow us to extend the funcionality of JUnit by adding behaviors that happen whenever we use a particular rule

    -   Theories work under different contexts. We can set them up with different data and make sure those theories still hold

8.  Integration with popular build systems

    -   Maven

**What is Unit Testing?**

The idea is to take the smallest Unit of code and test it by itself. In Java, this is a class. If you start doing tests that involve multiple classes, then you can consider this to be Integration or System testing. If we are using a database or calling a webservice then it may be a good test, but it is not a UNIT test.

**Start using JUnit on Eclipse (it come integrated)**

When wanting to start using JUnit for testing when developing in JAVA, we usually want to create a brand new project in our workspace with the same name except that it will have a \"test\" or \"tests\" appended at the end.

**JUnit Test Method**

\@Test

For JUnit 4 all we have to do is to define a method that is PUBLIC and that it has a VOID return type. Then we simply add the JUnit \@Test annotation to it

**JUnit Basic Annotations:**

-   \@Test

-   \@Before

-   \@After

    -   These two annotations work together to allow us to specify some behavior to happen before or after each test is run

-   \@BeforeClass

-   \@AfterClass

    -   Allows you to specify some behavior that happens before any method in the test class is executed and after all the methods are executed

-   \@Ignore

    -   Tells the JUnit runner to ignore this test to temporarily disable a test

-   \@Test(expected = Exception.class)

    -   Allows us to expect that an exception will be thrown

-   \@Test(timeout = 100)

    -   Allows us to specify a period that the test should run otherwise it will timeout

\@Test

**public void** NewTrackingServiceTotalIsZero(){

      TrackingService service = **new** TrackingService();

      

      *assertEquals*(\"Tracking Service Total was NOT 0\" , 0, service.getTotal());

}

\@Test

**public void** WhenAddingProteinTotalIncreases(){

      TrackingService service = **new** TrackingService();

      

       **int** val = 5;

       service.addProtein(val );

      

      *assertEquals*(\"Total was not added correctly\" , val , service.getTotal());

}

 

Using the BEFORE and AFTER annotations tend to be VERY useful to avoid having duplications in our code. When Unit test have too much duplication it tends to be really hard to troubleshoot.

One major thing about the BEFORE annotation is that it will run EVERY TIME a test is ran. This means that if we place a \"new\" object in the before\...it will be a clear object for every time it enters a test. We do not have to worry about one test having some left over values that might affect the second test that runs afterwards.

AFTER has the same properties as BEFORE

AFTER is not used quite as often but can be useful when dealing with databases for example, were we can do ROLLOUTS etc\...

When dealing with the BEFORECLASS and AFTERCLASS annotations. Also, these methods MOST be STATIC methods. These annotation will be useful if we only have to set up data once before testing and clearing things afterwards.

IGNORE is really helpful whenever we want to temporarily remove a test. 

\@Test

\@Ignore

\@Test(expected=Exception.class)

The test will ONLY pass if an exception of that class is thrown

In the advanced module we will also check for the message that the exception will throw as well

\@Test(expected=InvalidGoalException.**class**)

**public void** CheckForInvalidGoalException() **throws** InvalidGoalException{

       service.setGoal(-1);

}

**Timeout testing:**

\@test(timeout = -)

We will deal with timeout tests whenever we want a specific test to run for a certain amount of time only. If the test takes too long we can then do something/ The value given for the timeout will be measured in milliseconds

 

**Assertions (Basic):**

-   assertArrayEquals

-   assertEquals

-   assertTrue

-   assertFalse

-   assertNull

-   assertNotNull

-   assertSame

-   assertNotSame

-   fail

From \<<https://www.facebook.com/>\>
