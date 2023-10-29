The BASICS

Friday, April 26, 2019

9:28 AM

 

![React\'s design concepts JSX and events handlers, data, and APIs React hooks Communicating between components Creating a local development environment ](000_The_BASICS_000.png)

 

 

**Why do we want to commit to use REACT?**

React defines itself as a JavaScript **LIBRARY** for **building user interfaces.** Library and Framework mean different things in different contexts...but what is important to remember is that REACT is SMALL and it is not a COMPLETE solution... we will need to use OTHER Libraries with REACT to form solutions... REACT only focus on the UI.

 

Since Web browsers understand JS, we can use REACT to describe Web User Interfaces... \"Describe\" is a good word to define this process because we basically tell REACT what we want, and it will build our actual UI on our behalf in the web browser.

 

REACT is \"declarative\": Is what we described above. We tell REACT WHAT we want but not HOW to do it.

 

**Isn\'t HTML Already Declarative?**

Yes... but declarative for static content.... REACT will allow us to deal with Dynamic Data

**How exactly is NOT being a framework a good thing?**

Frameworks are great... when working with one, many smart design decisions are already made for us. However, frameworks can set some limitations in our code base, that at times when working with large scale applications, these disadvantages can be deal breakers.

-   Limited Flexibility

    -   Do things certain way

    -   Hard to deviate

-   Large and full of features

    -   Hard to customize

    -   Use the whole thing. (Some frameworks are going modular now though... but it still not great)

 

**Why is REACT so popular?**

-   The \"VIRTUAL\" browser (vs. DOM API)

-   \"Just JavaScript\"

    -   There is a small REACT API to learn... but after that, everything is set in regular good old JavaScript.

-   REACT Native (for the win)

-   Battle-tested

-   Declarative Language (model UI and state)

    -   REACT stablishes a new language between devs and browsers that allow developers to declarative describe state-ful user interfaces. Means: Instead of coming up with STEPS for transactions for the interfaces, developers just DESCRIBE their interfaces in terms of a final state...like a function.

    -   When transactions happen to that STATE, REACT takes care of updating the user interface based on that.

 

**REACT Basic Components (THE MAIN 3):**

1.  **Components**

    a.  We describe User interfaces using Components...

    b.  Components can be thought simply as FUNCTIONS.

    c.  Inputs:

        i.  Props

        ii. State \| Output: UI

    d.  Reusable and composable

        i.  Components CAN contain other components

    e.  \<Component /\>

    f.  Can manage a private state

        i.  Unlike pure functions... a REACT component can have a private state that can hold any data to hold over the lifecycle of the components

```{=html}
<!-- -->
```
2.  **Reactive Updates**

    a.  When the state of a react component\'s input changes, the user interface it represents changes as well. When this changes happen we actually DO NOT have to worry about how these changes get to the browser...essentially:

    b.  REACT will react

        i.  Take updates to the browser

3.  **Virtual Views in Memory**

    a.  Generate HTML using JavaScript

        i.  (Sounds weird but it\'s fine). To build HTML websites with REACT, we DO NOT write HTML code at all. We use JS to generate HTML

            1.  Why? When a web app receives some data from the server with AJAX, we need something more than HTML to work with that data. We have 2 options:

                a.  Use ENHANCED HTML template that has loops and conditionals

                b.  Power of JS to generate new HTML code from data **(REACT way)**

    b.  No HTML template language

    ```{=html}
    <!-- -->
    ```
    c.  **Tree reconciliation**

        i.  One of the advantages of having HTML generated through JS is that REACT is able to keep and use a VIRTUAL representation of HTML view in memory. (VIRTUAL DOM)...

        ii. REACT uses the Virtual DOM to compare versions of the UI in memory before it acts on them

 

**REACT Components**

Can be one of 2 types:

Both types can be STATEFUL and/or have side effects...or they can be purely presentational

-   Function Component

    -   Simpler

-   Class Component

    -   More powerful

 

![= (props) { const MyComponent return ( \<domE1ementOrComponent Props State class MyComponent extends React . Component { render ( ) { return ( \<domE1ementOrComponent . DOM ](000_The_BASICS_001.png)

 

Both types can be compared to regular functions when it comes to their construct. They both use a set of props and state as their input... and they output what LOOKS LIKE HTML but it\'s actually JSX.

 

The PROPS input is an explicit one. It is similar to the list of attributes an HTML element can have.

The STATE input is an internal one. It is the one that REACT uses to auto reflect changes in the browser.

 

**Important:** Within a component the STATE object CAN be changed, while the PROPS object represents values. PROPS are immutable.

 

![JSX Is NOT HTML class Hello extends React. Component { class Hello extends React .Component { render { render ( ) { return ( return ( div React. createE1enent( \"div\" , { classNane: \"container\"} , React. null, \"Getting Started\") ReactDOM. render(React . createE1ement(He110, null) , mountNode) ; ReactDOM. mountNode) ; ](000_The_BASICS_002.png)

 

 

<https://jscomplete.com/playground/rgs1.1>

![function return ReactDOM 110 He110() { React! \_ render( Hello React! document \_ getEIemen tById( noun tNode ) , ](000_The_BASICS_003.png)

We have a simple REACT function component that returns a DIV. This component has NO input... and no state either...we call these components: PURE components... to display a REACT component in the browser, we need to tell the REACT DOM Library to do that.

 

The function designed to do that is the ReactDOM.render( ... ) which takes in 2 arguments

1.  Component to Render

    a.  Above we just pass in like just another DOM element

2.  The DOM element in the Browser where we wish the REACT DOM element to show up

    a.  The playground in the link above we are using the mountNode element. The entry point of REACT essentially

 

**Q:** Explain line 2. How are we writing HTML inside a JS function? Why is this working and not throwing an error

**A:** That\'s not HTML, it\'s JSX. This line will NOT be executed by the browser (The browser doesn\'t know how to handle JSX)... this will be executed by the JSX extension added to this website and compiled to something else. (HTML)... The playground is using a special compiler named BABEL to convert JSX into REACT API calls

 

<https://babeljs.io/repl/#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwEwlgbgfAEgpgGwQewAQCU4EMDGOAuwA9ONEA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.4.3&externalPlugins=>

 

![Docs Setup 1 Reacct\</div\> Try it out 1 Videos Blog \'use strict\", Search Donate Team GitHub React. createE1ement(\" div null, \"Hello Reacct\"); ](000_The_BASICS_004.png)

 

BABEL compiles our JSX code into a call to the createElement function in the REACT TOP level API.

In the Code example above, the browser is not actually executing that JSX... instead it is doing the React.CreateElement with the following parameters:

1.  \"div\": the element to be created

2.  Null: any attributes this element will have

3.  \"Hello react\" : Child of that div element

 

**IMPORTANT NOTE:** A Component name HAS to start with an UPPER CASE letter... if you don\'t do that, REACT will think you are giving it a regular HTML element

 

**REACT Hooks:**

![useState() results: a) state object (getter) b) updater function (setter) ](000_The_BASICS_005.png)

>  

REACT has a special function called useState(). This function is going to return 2 items... The state object can be of any type you wish it to be. It\'s very simple to understand, the first element is the variable we want to track and change, while the second one is the function that will take care of what changes actually are going to be run.

 

Since JS function can only return a SINGLE value, the useState function will return an Array with exactly the 2 elements we need.

 

JS Descructuring feature is what helps us assign the 2 variables into one line

 

![](000_The_BASICS_006.png)

>  

JSX supports displaying DYNAMIC expressions if we place them within curly braces anywhere within JSX...

 

If we want to use the setCounter updater function declared above, we need to introduce an event handler. This is going to look similar to the regular DOM api. We declare a \'onClick\' attribute. **This is CASE SENSITIVE**. Unlike the DOM version of the onClick (which receives a string), the REACT version receives an function reference... so we need to specify that inside curly braces as well.

 

![\"Complete Home cmst return O but tm s ; O Help ](000_The_BASICS_007.png)

 

NOTE: We did not have to invoke the function. We just need to pass in the pointer to the function.

 

Now you can also inline the function inside the onClick curlyBrackets and that will work just fine... or even better... use the ARROW function syntax. () =\> console.log(Math.random()

 

![I •L function Button() { const \[counter, setCounterJ = useState(O); return render ( sButton docuænt .getEIementById( \'mountNode \' ) , ](000_The_BASICS_008.png)

 

This **useState** function is called a HOOK in the REACT world. It is similar to a module, but it is a stateful one, that hooks this simple component into a state. The important thing to note from the image above, is that we ultimately did not need to implement ANYTHING for the UI to get updated with the new value. We did not need to create a transaction of any kind on. Our UI implementation was basically telling REACT that we wanted the label of the button to always reflect what the counter object has stored.

 

![I • function Button() 10 12 13 const \[counter, setCounterJ z useState(O); return ( \<button (counter) C/ button\> ReacttM. render ( eButton getEIenentById( ) , return return o; X ](000_The_BASICS_009.png)

 

Note how we are using Parenthesis here and NOT curly braces. We are NOT returning an object. We are returning a function call. A React.createElement()

 

**Using multiple components at once:**

When compounding components, keep in mind that we can\'t just add it to the .render( function\'s call first parameter. The reason for that is because EACH one of the components passed in gets translated into a function call. The solution to this can vary.....

We can:

1.  Make the first element passed to the render function an array of REACT components, and pass in as many components as we want...

2.  Make the REACT components we want to include the children of a REACT component we want to include

    a.  ![rende r ( \<Button / \> kDtspIay \' nountNode ) , ](000_The_BASICS_010.png)

    b.  In fact... REACT has a special object for these type of cases... if we need to enclose components without introducing a new DIV parent... we can use React.Fragment

        i.  This will do the same as the div one... but NO new DOM parent will be introduced

        ii. **BEYOND THAT:** This case is so common in REACT that we can also just leave things as an empty tag... this will also get compiled into the React.Fragment version

            1.  \<\>

 

![14 23 function Button() { const \[counter, setCounter) - useSta te(ß); return ( \<button {counter} function Display() { return ( function App() { return ( C\<8utton \<Dtsplay ReactDOM\_ render ( document \_ getEIemen tById( nountNode ) , ](000_The_BASICS_011.png)

>  

Now let\'s say that we want to have our Display component grab the information of the counter state inside the Button component... The state in a REACT component can be accessed only by that component itself and no one else. In order to make this work, we would need to set that state of the component one level above in the parent component...

 

**Passing down PROPS to child components**

To pass a prop to a component we specify an attribute just like in HTML to our component.

> *\<Display message={counter} /\>*

The Display component can now use it\'s props object (which is the argument to the function (which it does not need to be named props)). All function components receive this object, even when they have no attribute.

Because a component can receive MANY attributes, this props will have a keyValue pair for each attribute.

To access the props we would do something like:

*\<div\>{props.message}\</div\>*

 

![I function Button(props) // const handleCIick setCounter(counter• return ( \<button c/ button\> function Display(props) return ( 16 • function App() { Const \[counter, return ( \<Button cm splay render ( CApp Is, nter\] useState(42); ](000_The_BASICS_012.png)

 

What we did here is called **The One Way Flow of Data**... Parents components can flow their data to their children components. (data and behavior)

 

![function Button(props) { return ( \<button function Display(props) { return ( \_ message} 24 26 function App() { const \[counter, setCounter) - useState(1); const incrementCounter = O setcounter(counter+l); return ( \<8utton \<Dtsplay ReactDOM\_ render ( document \_ getEIemen tById( nountNode ) , ](000_The_BASICS_013.png)

 

**IMPORTANT:** The onClick function property allowed the button to invoke the App component incrementCounter function... is like when we click that button, the Button component reaches out to the App component as says \"hey parent, go ahead and invoke that counter behavior now\"... **In reality** they App component is the one in control and the Button component is just following generic rules...

 

The Button component has NO CLUE what happens when it gets clicked. It just follows the rules defined by the parent... and invoke a generic inClick function... That is basically the concept of responsibility isolation. Each component has certain responsibilities and they get to focus on that.

 

Passing in values to functions in our components...

![function Button(props) { // const handleCltck () setcounter(counter+l); return ( \<button +{props \_ incremen t} ](000_The_BASICS_014.png)

 

Notice how this will not work. Assuming that the function declaration for our onClickFunction takes in a parameter. The reason why this is a problem is because we are now dealing with an invocation of a function. We are ONLY allowed to pass in function REFERENCES. We can simply wrap this invocation in an inline function to make it into a reference.

 

![function Button(props) { // const handleCltck () setcounter(counter+l); return ( \<button props \_onCItckFunctton(props +{props \_ incremen t} ](000_The_BASICS_015.png)

\^\^\^ Note how if we just set the handleClick function to our new onClick handler, things are a bit cleaner.

 

**Tree Reconciliation in Action**

![I w const render 10 22 docuænt.getEtementById( •mountNode\').tnnerHTHL = • Hello HTML \<input Date) ReactD(h4. render ( null, \"Hello React\" , React.createEIenent( \'input\', null), React.createElement( \'pre\', null, (new Date) . toLocaIeTtmeStrtng( ) ) , document. getElementById( \' • ) , setlnterval(render , 1000); ](000_The_BASICS_016.png)

 

\^\^\^ Taking a quick look at the code above, we can see that every 1 second, we are going to run the render function that is both setting up a regular HTML element on the page, as well as a REACT one. What\'s the difference? Simply put, the HTML code seems way simpler... so why do we need to learn a brand new API to write HTML code using JS ???

Answer: Virtual DOM. In the HTML version, we are basically throwing away the whole DOM and regenerating it onto that \'mountNode\' element on the page. Which means, when means, let\'s say we try to type something onto the input box above our time, since each second the div gets re-rendered all together, whatever we type in the text box gets lost right away.

 

However, if we try to type anything in the textbox that is rendered with REACT, we don\'t have any problem. Although we have our WHOLE rendering code within the ticking timer, REACT is smart enough to know we are only changing the timestamp text and NOT the whole node.

 

![I • const render z docuænt.getEIementById( \'mountNode\' ) . innerHTHL = • Hello HTML Hello HTML \<input Date) • .24 pm 1:45. 10 ReactDOM. render ( null, \"Hello React\" , React-createEIenent( \'input\', null), React-createElement( \'pre\', null, (new document. getEIementById( \' nountNOde2 • ) , Hello React Hello!! html div Styles Computed eleent.style { C Lass:\" container---fluid\" cdIQJ id2\"mountNode\" class= cdiv class= React\' • einput\> c,\'diw \< script type\" •text/ javascript••»--- c/ scripts Event Listeners DOM Breaks»ints : hov CLS Date) . toLocaIeTLmeStrLng ( ) ) , :before, box---sizing :before, 8:\' after { rent. css ](000_The_BASICS_017.png)
