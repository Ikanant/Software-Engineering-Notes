03 - Creating and Using Angular Services

Tuesday, August 30, 2016

11:10 AM

**What is a Service?**

The term \"Service\" is an overloaded term. Sometimes when people talk about a service they are referring to over the wire like a web service or a wcf service. Or sometime it means simply an object that encapsulates some sort of business logic.

With respect to Angular a service refers to a the later description.

An Angular service is just a **worker object that performs some sort of business logic**. It is NOT access over the wire although it might be used to perform operations that do go over the wire (such as AJAX calls).

Services are often (not always) stateless. (it\'s not unusual to have services that cache some data) Services are literally just an object that has some methods and properties for us to reuse.

![Machine generated alternative text: The Term Service Is Overloaded Not Necessarily Over-the-Wire A Worker Object Often Stateless ](002_03_-_Creating_and_Using_Angular_Services_000.png)

With angular, we will be dealing with both plenty of built-in services as well as a easy way to create our own. Applications are often a match between the two options.

**Why do we use a Service?**

Services allow us to encapsulate re-usable business logic into an object that could be shared and re-used along an application. (so \*reusability). It will allow to break down the logic of our application into smaller sections are EASIER to maintain. In one hand we could just add all of our logic into our controller, but that would end up being much difficult to manage as the system grows and it violates the single responsibility principle.

SRP (Single Responsibility Principle) is one of the 5 solid principles of Solid Object Oriented Design and states that an object should only have a single responsibility.

Another great use for services is that we can just inject them into multiple controllers of our application that might need them. This allows us to have access to the functionality that we need when we need it in our application. Angular will behave like a fully functional Dependency injection container.

Services makes a lot of the testing of our code easier to perform. Smaller parts make it easier to test

![Machine generated alternative text: Reusable Dependency Injection SRP Testable ](002_03_-_Creating_and_Using_Angular_Services_001.png)

**What is an AngularJS Service?**

An AngularJS Service (whether it is built-in or custom) is really like the services we just talked about. It\'s simply just another worker object. When writing Angular services angular will not know how to identify our services until is registered with Angular. Once a service is registered it becomes part of the Angular world.

Services can be injected into other Services

Note: Remember when registering a controller like:

eventApp.controller(\'cotrollerName\', function EventController(**\$scope**)....

In here **\$scope** is a built-in Angular service.

Keep in mind that when creating a custom service we should not name it using a \$ symbol at the beginning of the name because this might create problems over-writing some built-in services within Angular. There is no problem at all naming our service with regular letters.

Creating an Angular service is simple. We just call the factory method onto our AnuglarApp...soemthing like:

*eventsApp.factory(\'serviceName\', function(){ return \'something\' });* **done**

**Built in Services**

![](002_03_-_Creating_and_Using_Angular_Services_002.png)

-   \$http

    -   The http service will allow us to make http request to our servers easily.... Similar as we would do for ajax calls

    -   The \$http will return a promise (success or error) after is ran

-   \$log

    -   It\'s pretty much the same thing as saying console.log();

-   \$resource

    -   Resource is often used for the same sort of things the http servers for making AJAX calls but the DIFFERENCE is that is based on a restful architecture. It assumes that your web server is using some web rest architecture.

    -   Unlike the \$http service, the \$resource service can be bind back directly without the need of a success promise or not.

    -   \$resource is not in the Standard angular module and will need to be imported similarly as the ngSanitize we have seen before.

    -   The services takes in a few parameters:

        1.  The url

        2.  Object that specifies default values that are used in the route

            1.  Then we call the .get method and we specify what we want to retrieve.

    -   Because with a resource service we don\'t get a promise, it will take a while for the result to popup back since we have to wait for the result to get to the client. If we dealt with a promise, the program will continue doing some logic and react to the result given based on the success message back

    -   Even though the \$resource service is NOT a promise, the object that is returned from it DOES have a promise stored. Which we can use to use a .then logic to it

        -   To achieve this we would just call \$promise.then

Within the \$resource service we have multiple functions. We implemented the .get and the .save functions but there are three other important ones:

1.  Query

    a.  Just like get but it expects an Array to be returned

2.  Remove/Delete

    a.  Identical. They perform a delete action

3.  **We can create our own action**

    a.  We just set an object and it expects:

        1.  Name of the action

        2.  Method: Get / Post

        3.  Expects an Array or not

        4.  Parameters

    b.  Example:

![](002_03_-_Creating_and_Using_Angular_Services_003.png)

**Anchor Scroll**

The \$anchorScroll is one popular services that allows angular to move the page around to center an html element based on their id. It is simple to implement, just include it in the top of your controller and run the function \$anchorScroll();

**Angular Compile Service**

The compile service is used **heavily** internally by Angular. It is used whenever a page is loaded. Whenever a page is loaded, angular use the compile service to look through the page\'s html and process any ng- tags along the way. Even though this is useful, we can also use the compile service ourselves. Typically we would do this inside a directive but it can also be done inside a controller.

![](002_03_-_Creating_and_Using_Angular_Services_004.png)

The thing to note is that the compile method will return a function that will allow us to insert whatever result we get into another element in the page.

Though this is possible, using this is quite dangerous and would allow very simple hacking through Javacript injection.

![](002_03_-_Creating_and_Using_Angular_Services_005.png)

**The Parse Service**

Quite similar to the compile service. It is also used internally by Angular when processing a page. A parse service is often used to evaluate an expression which later gets turned into a function.

![](002_03_-_Creating_and_Using_Angular_Services_006.png)

That would return 3.

**The Locale Service**

Service used for localization of date time in numeric format.

**The TIMEOUT Service**

Very much like the default JavaScript Timeout function. One some key differences...

The \$timeout service returns a promise, which we can use for various reasons like potentially canceling the action that is waiting on timeout to be performed.

In order to cancel a timeout we can do something like: *\$timeout.cancel(promise);*

We would just pass the promise that was created when the timeout was first instantiated.

Now, why don\'t we just use a regular timeout in our page? Well, when we write a regular timeout and let\'s say we give a variable a certain value, the content on the page is not going to refresh (be updated) until something triggers the bindings to be re-evaluated in our page.

For example, lets say we have a label that contains a content that says \"apple\" and within our controller we have a regular JavaScript timeout function that triggered after 1 second to change \'Apple\' to \'Tomato\'. After one second in our page, nothing will happen. The label will continue to be named \'Apple\'. BUT, let\'s say we have ANY other type Angular binding in our page like a button who runs another Angular function in our controller (completely unrelated to the \'Apple\' logic) this will force our page to be re-evaluated and our \'Apple\' label will then turn into a \'Tomato\' label.

![](002_03_-_Creating_and_Using_Angular_Services_007.png)

**Less Common Services**

-   \$interpolate

    -   Used internally by the \$compile service.

    -   There are various scenarios in which we have issues with Angular {{ }} battling with a list of other javascript tools often used in other applications. When using the interpolate service we can potentially change what angular uses (symbols wise)

    -   ![](002_03_-_Creating_and_Using_Angular_Services_008.png)

-   \$log

    -   .log

    -   .info

    -   .warn

    -   .error

-   \$rootScope

    -   Used mostly behind the scene. There is ONE rootScope per Angular application. It is used whenever a new scope is generated. Whenever we use a new controller, a new scope is generated from the rootScope and it prototypal inherits from the rootScope.

    -   If we change things in the rootScope we can see such changes in every \$scope object in our application.

    -   This should not be taken lightly and we should not use it as a dump it ground for our global data.

-   DOM Services

    -   \$window

        -   Gives you access to the Window object in JS

    -   \$document

        -   Gives you access to the Document object in JS

    -   \$rootElement

        -   Gives us access to Angular root element. **Whatever element we put our ngApp directive on**.

    -   Not a good practice to play around with these

>  
