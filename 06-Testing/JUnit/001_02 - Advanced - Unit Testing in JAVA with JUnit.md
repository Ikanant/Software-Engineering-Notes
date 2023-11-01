02 - Advanced - Unit Testing in JAVA with JUnit

Friday, April 29, 2016

12:25 PM

**Test Suites**

There will be a time were we are going to want to run multiple test classes together without having to individually select and TestRun each class. JUnit provides Test Suites to fix this issue.

We will create test suite classes by annotating them with the \@RunWith annotation and then tell it to use the Suite.class. This tells JUnit to run this particular test suite using the suite runner. The suite runner is capable of reading the Suite class annotation and running any test classes contained in it

![](001_02_-_Advanced_-_Unit_Testing_in_JAVA_with_JUnit_000.png)

**import** org.junit.runner.RunWith;

**import** org.junit.runners.Suite;

\@RunWith(Suite.**class**)

\@Suite.SuiteClasses ({

      HelloJUnitTest. **class**,

      TrackingServiceTest. **class**

}) // This is going to tell us what classes this particular suite is going to made of

**public class** ProteinTrackerSuite {

}

**Categories**

Are similar to Suites in JUnit, in fact, the categories runner is just a special kind of suite in JUnit. Keep in mind that the \@Category method can be added to both test methods and test classes

![](001_02_-_Advanced_-_Unit_Testing_in_JAVA_with_JUnit_001.png)

\@RunWith(Categories.**class**)

\@IncludeCategory({

      GoodTestCategory. **class**

})

\@ExcludeCategory({

      BadTestCategory .**class**

})

\@Suite.SuiteClasses ({

      HelloJUnitTest. **class**,

      TrackingServiceTest. **class**

})

**public class** GoodTestsSuite {

}

\@Test(expected=InvalidGoalException.**class**)

\@Category(BadTestCategory.**class**)

**public void** CheckForInvalidGoalException() **throws** InvalidGoalException{

       service.setGoal(-1);

}

\@Test(timeout= 200)

\@Category({

      GoodTestCategory. **class**,

      BadTestCategory. **class**

})

**Parameterized Tests**

In many circumstances, developers end up writing a series of tests that only vary on the elements that are inserted and expected from such tests. For this kind of scenarios, JUnit offers parameterized tests. A great help to avoid rewriting code over and over.

\@RunWith(Parameterized.**class**)

**public class** ParameterizedTests {

       \@Parameters

       **public** **static** List data() {

             **return** Arrays.*asList*( **new** Object\[\]\[\]{

                  {5, 5}, // This means if we add 5 protein, the total should be 5

                  {5, 10}, // Then after 5 more, the total should be 10 \...

                  {-12, 0},

                  {50, 50},

                  {1, 51}

            });

      }

      

       **private** **static** TrackingService *service* = **new** TrackingService();

       **private** **int** input ;

       **private** **int** expected ;

       **public** ParameterizedTests(**int** input, **int** expected) {

             **this**.input = input;

             **this**.expected = expected;

      }

      

       \@Test

       **public** **void** test(){

             **if**(input \>= 0){

                   *service*.addProtein(input );

            }

             **else** {

                   *service*.removeProtein(-input );

            }

            

             *assertEquals*(expected, *service*.getTotal());

      }

}

**Advanced Assertions**

**Matchers & AssertThat**

Using Packages like org.hamcrest.com

-   AllOff

-   AnyOf

-   DescribedAs

-   Is

-   IsAnything

-   IsEqual

-   IsInstanceOf

-   IsNot

-   IsNull

-   IsSame

Consider that if we have multiple asserts in a method, we have a valid statement. If any assert is false, then it will fail the test as a result.

\@Test

\@Category(GoodTestCategory.class)

public void WhenAddingProteinTotalIncreases() {

//Use AssertThat now\...

int val = 5;

service.addProtein(val);

assertEquals(\"Total was not added correctly\", val, service.getTotal());

assertThat(service.getTotal(), is(5));

// allOf checks that every condition inside the parenthesis is true

assertThat(service.getTotal(), allOf(is(5), instanceOf(Integer.class)));

}

**Advanced Exception Testing**

With the latest version of JUnit we get the \@Rule annotation. With it, we will further improve how we deal with exceptions. In some cases we will even get to read the message inside the Exception from our test code.

public void setGoal(int value) throws InvalidGoalException{

if (value \< 0) {

throw new InvalidGoalException(\"Goal was less than zero\");

}

goal = value;

}

On the code above we pretty much return an exception with a custom message on it\...

\@Rule

public ExpectedException thrown = ExpectedException.none();

\@Test

\@Category(BadTestCategory.class)

public void CheckForInvalidGoalException() throws InvalidGoalException{

thrown.expect(InvalidGoalException.class);

//thrown.expectMessage(\"Goal was less than zero\");

//or

thrown.expectMessage(containsString(\"Goal\"));

service.setGoal(-1);

}

**Rules**

-   TemporaryFolder

-   ExternalResource

-   ErrorCollector

-   Verifier

-   TestWatcher

-   TestName

-   Timeout

-   ExpectedException

-   RuleChain

Rules are going to be helpful when setting custom rules we wish to apply to our test. For example, the \@Test(timeout = ) annotation we used before does not apply to multiple methods, so as developers we end up having to rely on single method timeout capabilities. This is not the case with Rules...

Rules will be applied to EVERYTHING inside of the class. So for example, with the timeout rule, it applies to every single method inside the test class.

\@Rule

public Timeout timeout = new [~~Timeout~~(20)]; // 20 milliseconds

With the above code, we ensure that every test times out at 20 milliseconds

**Theories**

Theories are almost the same as parameterized tests.

[A theory is TEST that holds true under all conditions that meet a set of assumptions.]

We can create a Theory by simply using the Theory annotation instead of the Test annotation. The big difference between a theory and a parameterized test is that the theory will have the same expected result for all inputs.
