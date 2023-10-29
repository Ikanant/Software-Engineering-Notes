03 - Integrating JUnit - Unit Testing in JAVA with JUnit

Friday, April 29, 2016

12:25 PM

 

The real power of JUnit relies on creating automated regression tests. In order to do this, we need to learn how to integrate JUnit to systems like Ant and Maven.

**Alternative Runners**

The JUnit runner built into Eclipse is great for running tests quickly while running projects on Eclipse but it isn\'t really a great option for automating the running of JUnit tests. 

We can run JUnit directly from the Command line or just create a separate class with a main method that uses JUnitCore file to run tests from within JAVA.

public class ConsoleRunner {

public static void main(String\[\] args){

JUnitCore junit = new JUnitCore();

junit.addListener(new TextListener(System.out));

junit.run(TrackingServiceTest.class);

}

}

**Continuous Testing**

Continues testing: Will monitor your source code and when it detects a change automatically run a JUnit test that is related to that code.

Simple useful tool for continuous testing: **[Infinitest]{.underline}**

Infinitest is a simple plugin that can be added to Eclipse to auto determine when something that is connected to a test has been changed. Just by clicking save we can see a bar at the bottom of eclipse that describes how many tests were affected by the latest change and if something went wrong with it.

**Dependencies**

In most cases it is really easy to go over JUnit tests with simple examples\....in real life, this can be a little more tricky. Most real life projects posses a series of dependencies that can overcome the difficulty of the test written development that we are targeting.

The solution to this is: Stubs and Mocks

**Stub**

Some code that pretends to be the dependency your code needs. It allows you to test your code without having to test any other dependency the code uses.

**Mocks**

One major problem from using stubs is that stubs don\'t actually do anything.

A mock object will act like the real dependency and also record what calls are made to it. And it can be setup to return specific data under certain conditions

JMock is a plugin that can be used for using Mocks

**Integration Testing**

JUnit can used to do more than just Unit testing, JUnit can also be used to do some Integration testing\... When doing Integration testing we do not care about the dependencies of our code, because when we test we want EVERYTHING to be checked as a whole. This can be dangerous because if we are testing the whole code we need to be aware if we touch any kinda of database query that can change the status of our code in a negative way.

**Selenium**

We can even use JUnit to drive other testing frameworks such as Selenium to enable to even do higher level automated testing. Selenium will help us write automated tests that will simulate having a real user behind the test of our web application tests

**public class** ConsoleRunner {

       **public** **static** **void** [main(String\[\]]{.underline} [args)]{.underline} {

             [WebDriver]{.underline} driver = **new** [FirefoxDriver]{.underline}();

             driver.get(\"http://google.com\" );

             [WebElement]{.underline} searchBox = driver.findElement([By]{.underline}.name( \"q\"));

             searchBox.sendKeys(\"Pluralsight\" );

             searchBox.submit();

      }

}
