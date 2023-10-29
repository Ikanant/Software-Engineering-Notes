01 - Introduction

Wednesday, August 24, 2016

1:48 PM

 

**What is Angular?**

Angular is a JavaScript library. It\'s falls under the category of MV\* framework (like: Knockout or Backbone). Angular is an opinionated MV\* framework... Opinionated means that the framework will guide into doing things a certain way.

 

![Machine generated alternative text: View MV\* Frameworks Model Controller/ Presenter/ ViewModel/ ](000_01_-_Introduction_000.png){width="6.0in" height="4.525in"}

 

**Angular Features:**

 

Angular will handle the AJAX communication from our server so we can both send and receive data as Plain JavaScript Objects that will not need HTTP request like GETs and SETs when updating data.

 

Angular will take care of modifying that data on the page itself

 

Angular will also take care of listening of users input for any change occurring in the page

 

Angular handles Routing. Moving from one View to another. Key into building single page applications. This way we can completely change the view of the page based on the users interaction with the page. Angular can also update the url in the browser so that the new view can be bookmarked for later.

 

Angular was built with test in mind. Angular supports isolated Unit test and Integrated end-to-end test.

 

**Angular extends HTML Vocabulary** by providing its own elements and properties called **[Directives]{.underline}** that are used to interact with our HTML DOM...

 

![Machine generated alternative text: Extended HTML Vocabulary \<input id=\"username\" type=\"text\" focus / \> \<mu1tiStateButton id=\"buttonl\" / \> \<userTi1e id=\"userTi1e1\" user=\"currentUser\" / \> ](000_01_-_Introduction_001.png){width="6.0in" height="5.041666666666667in"}

 

**Review:**

 

**Angular thinks of HTML as if it had been designed to do what?**

Build applications instead of documents.

 

**What kinds fo tests does angular support?**

Unit tests and end to end tests

 

**Name one of the ways that angular is forward thinking.**

Web Components / Object.observe

 

**Angular Architecture:**

-   Two way binding

    -   User input in form fields is INSTANTLY updated in the Form models. This will allow us to avoid manually watching elements for certain events in order to change things in the page.

-   Dirty Checking

    -   We don\'t need to place our data in special functions or need getters and setter functions to access our data. We can simply put our model data into Plain Old Javascript Objects

-   Dependency Injection

    -   Allow us to encapsulate pieces of our application better and Improve testability

 

**Angular Components**

-   Controllers

    -   With Angular everything starts with a Controller. Controllers will take care of BOTH Logic and State

-   VIEW

    -   Made up of bindings and directives. This is how Angular talks to and listens to the user.

-   Services

    -   Give you a place to contain real logic of the application. Business logic, etc... Services will be the place where we will want to communicate with the server

>  

 

**Course Application: Angular EventReg**

 

-   List of Angular Events

-   Event Details

-   Create New Events & Sessions

-   Edit vents & Sessions

-   Login

-   Server

 

 
