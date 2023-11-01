01 - Introduction

Friday, April 29, 2016

11:46 AM

![](000_01_-_Introduction_000.png)

**WHAT IS REACT ?**

1.  React is all about components and building complete views using them.

2.  Reuse a single component in multiple places with different properties

3.  Components and composible and we can build components from other components

4.  Components are STATEFUL. Not static. They have private state and that state changes over time and REACT will take are of handling the changes

5.  **Simple: Write HTML using JavaScript**

Why React?

> In most applications we generate all the data server side, build the HTML and then send it to the user....the way React does things is that it sends the user the data and it efficiently manages it in the front end.
>
>  
>
> ![Machine generated alternative text: HTML in JS? why?? Data HTML PHP/JSP server-side Send only the Data to the client Enhance HTML: Loops, Conditionals Generate HTML with JavaScript Virtual DOM ](000_01_-_Introduction_001.png)
>
>  

**React Disadvantages:**

-   Why leave HTML

    -   We don't need to give up HTML. We will use JSX. JSX allows us to take React structures and automatically convert them into JavaScript React function calls. So we write in HTML, and then transform the JSX into native React calls before serving to the client. (This will be automated). JSX is not required though.

-   Integration with other languages

    -   We can easily React component: **Lifecycle Methods**. Which are specific points in a components lifecycle where we can invoke custom behaviors

-   There are no Models or Controllers in React

    -   We will focus on the VIEW and what it needs. We replace a V with an R (View = React)

    -   Model: GraphQL

    -   Controller: Relay

    -   MVC ===\> RGR

**React Advantages:**

-   Powerful JavaScript

-   No learning curve. It is just JavaScript

-   PERFORMANCE !!

    -   Virtual DOM

        -   Allows REACT to re-render Views Virtually in Memory to compute what exactly has changed and only apply what needs to be applied to the Client Browsers

        -   This is called: Reconciliation

-   React updates

    -   We don\'t need to keep track to what is changing. We define our views once and then just manage the data. REACT will take care of re-rendering our view in the optimal way

-   Not only for the browser

    -   Since REACT has its own representation of a document, it is not tight to HTML or a DOM....In face we need a separate library called: React DOM to make REACT work with the DOM

    -   iOS or Android !

**What is GraphQL ?**

![Machine generated alternative text: GraphQL JSON without the values address• person: { name• No custom endpoints Clients ask exactly what they want One endpoint to rule them all ](000_01_-_Introduction_002.png)

1.  JSON without the values

    a.  JSON is basically a set of keys and values...with nested sets and arrays of sets. We know that the values will come from the server as they are basically the data...the keys on the other hand are exactly what the VIEW uses to render itself. So if we strip the values from the JSON object we end up with the exactly what the view needs from the Serve...

        i.  That representation is exactly what GraphQL string is.

2.  No custom endpoings

3.  Clients ask exactly what they want

4.  One endpoint to rule them all

GraphQL can be the killer of Rest APIs

**What is FLUX ?**

![Machine generated alternative text: Flux No data binding, one-way data flow Views do not change the models A single dispatcher Views listen, React reacts What\'s wrong with MVC? Constraints are good ](000_01_-_Introduction_003.png)

Flux is a pattern for building Web Application using Unidirectional Data Flows... Instead of Data bindings between the Views and the Models the front end system should have a a one way data flow...

Your View should never change the model directly. They can READ from the model, but for write Operations they trigger actions that get eventually dispatched to the model.

React fits perfectly in this flow because the way it reacts to data changes in the stores.

**What is wrong with MVC?**

On a small scale, MVC works well. When an application grows into multiple models and multiple views the relationships between start to get complicated, and even hard to understand. Multiple things reading a writing in multiple direction.

According to the FLUX pattern the solution is in constrains..... An enforced ONE WAY data flow. Any way in the application you know there is only one way to go to. No guessing

**What is Relay ?**

![](000_01_-_Introduction_004.png)

Relay builds on top of the FLUX pattern and basically reduces the pattern onto one store. Handles the connection between Views and Models...

In MVC we separate the Data and View completely....but the View is the one that know which data element they need to be able to render correctly....In RELAY we do NOT separate them AT ALL.....instead we Co-locate them to have the data requirement express directly in the view component itself...
