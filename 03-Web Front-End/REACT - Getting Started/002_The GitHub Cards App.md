The GitHub Cards App

Tuesday, April 30, 2019

2:59 PM

Will use Class components. Though the REACT team might decide to face out class components in order to use state-full functions... class components have been the norm in react for a long time. Many REACT project will continue to use them. We should be very familiar with both solutions as REACT developers.

The first thing that we need to think of when creating a new REACT application is the Component structure. We need decide how many components to use and what each component should describe... practically this can be challenging...

So, how do we turn a REACT component written like:

![= ({tttle}) - const App \<dtv ](002_The_GitHub_Cards_App_000.png)

As a class react component? Easy - we just make a JS class that extends React.Component

![class App extends React_Component { ](002_The_GitHub_Cards_App_001.png)

Each REACT component **MUST HAVE** a render() function! And we make the render function return the virtual DOM description of our component. However, instead of receiving props as arguments, in class components both the props and the state are managed on an instance of the class.

![I • class Card extends React. Component 2 render ( ) return sdiv One CitHub Profile\... 11• class App extends 12 render() { \<div The GitHub Cards App One Gitkub Profile.„ 20 23 return ( e/ div, render( CApp title;\" The GitHub Cards App mountNOde, ](002_The_GitHub_Cards_App_002.png)

**Styles without using global CSS stylesheet**

If we do not care to use classic css class names on our JSX elements, we can always use the **style** property. Now, before people start to freak out.... This is NOT a regular HTML style syntax. This is a REACT style property. Just like events, instead of passing a string we just pass in a JS object... we use a { } for a dynamic value AND THEN another set of curly braces { } to start an object literal. This is NOT a special double curly brace syntax. This is just an object literal inside the normal JSX dynamic expression syntax that we do with curly braces.

Inside the style object, we can now specify any styling we want this element to have using the JS api for styles.

There is a LOT of debates about whether or not this is similar to using inline styles... but the main difference to keep in mind is that this will be using JS. We can generate it, and re-use it... and have the complete power of JS to do that. [We can do conditional styles here without having to deal with conditional class names.]

![I class ConditionatStyte extends 2 • render() { How do you like this? return ( ediv color: Math. random() O.S ? do you like this? 1 ReactDM. render ( green Il 14 ](002_The_GitHub_Cards_App_003.png)

\^\^\^ This code will make the text appear red / green at random without the use of multiple class names.

**Working with DATA**

Note: We can mix and match component types within an application. Essentially we are able to nest function components and class components without problem.

![Const z (props) ( \<Card name:\"\" companF\"\" CCard 14 • class Card extends React-Component { 1 S render() // const profite testOata\[O\]; return ( cdiv ediv \<div c / div\* 1 ](002_The_GitHub_Cards_App_004.png)

One way of doing something cool when passing properties to our component is use the spread operator. When using it**, ALL** the props for that object will become props for this components... in the image above the profile variable would become: **const profile = this.props;**

The **this** keyword above refers to an instance of the CARD component.

What is an instance in a REACT application? - Well, every time we use a class component, REACT internally creates an instance of the component and uses it to render the element. The thing to remember here is that, each time we use a component, we get a different instance.

![](002_The_GitHub_Cards_App_005.png)

**Initializing and Reading the State Object**

So let\'s now take into consideration we do not want our testData array to be a global variable and instead have it be handled by the CardList... one thing to keep in mind is that the Form component will also be appending values to the data array, and there is NO way we can pass in data from sibling components... the solution would then be to have the testData array be declared on the App component. *We will be putting the testData array on the **state** of the top level APP component.*

In a CLASS component, the STATE is also managed on the in-memory instance that react associates with every mounted components... To initialize the state object for the app component, we need to tap into the native CLASS CONSTRUCTOR method.... **Which gets called for every instantiated object.**

This constructor method receives the instances props as well. It HAS to call the JS super() method! - super is neededto honor the link between the App class and the class that it extends from, in this case react.Component.

Once inside the constructor we have access to the special STATE object that react manages for each class component .

***Note:** Unlike useState in function components, this state instance property has to be an object in class components. It can\'t be a string or an integer for example.*

![39 • class App extends React.Cævonent 40 • 46 54 constructor(props) { super(props); thfs.state profiles: testData, render() { return ( ediv CCardLtst profilesz{this.state.proftlesb ](002_The_GitHub_Cards_App_006.png)

There is a simpler and shorted syntax to handle things...

![40 44 class App extends React.Cc•wonent // constructor(props) ( Super (props); this.state { profiles: testData, State { profiles: testData ](002_The_GitHub_Cards_App_007.png)

\^\^\^ This is not yet part of the official JS language...but is going to be. The syntax works in the playground because we are using babel to compile things to normal JS the browser will understand...

When dealing with REACT we will ultimately use tools like Babel to compile JSX into JavaScript... so we can use the latest tools of the language if needed

**Taking inputs from the user**

We can simply define an onClick event on the button, BUT we can just as well have an onSubmit for the HTML form itself. By using onSubmit, we can utilize native submit features like adding **required** tag to the input box.

Every react EVENT function receives an event argument (can be named anything). It is just the last argument that the function receives. For REACT events, this argument is just a wrapper around the native JS event object. Every method that\'s available on the native event object are also available here... For example, since we want to take over the HTML submit logic, we should prevent the default form submission here that might cause a page reload... **event.preventDefault();**

Now let\'s consider the case in which we want to pull in the value if what the user typed in the input box... we could simply use the DOM api. We could give the input box an ID attribute and use getElementById to read its value. REACT has a special property named **ref** that we can use to get a reference to this element... This is kind of fancy ID that REACT keeps in memory and associates with every rendered element..

![28 • class Form extends React.Component userNaneInput handleSubnit React.createRef(); (event) { 39 36 event. preventDefauIt() ; log( this. userNameInput. current. valuel render() return ( cforn . handteSubmit)s \<inpu t type:\" text \" usern . userNaæInput) required ](002_The_GitHub_Cards_App_008.png)

REACT has another method to control the values of input box directly through REACT itself rather than reading from DOM. This method is often labeled and **Control Components** and it has some advantages over simple refs. (It requires a bit more code).

We can use the State object and use the value in the input box... Once we do this 2 steps we have a problem. We can\'t really type anything in the input box now because REACT is controlling the value of the element... so to fix this we need a **onChange** so that the DOM can tell REACT something has changed in this input box and we need to reflect it in the UI. This function will receive the **event** object as its arguments... and it just needs to change the value of the userName

![28 Class Form extends React. Component { 30 • 34 48 state userNaæ: \' \' l; handleSubnit (event) event. preventDefault() ; console. log() render() return ( ctnpu t type: \" text \" state. userNane} this. userName: event.target.vatue l)) username\" required outton»Add cards/button» c/forn» ](002_The_GitHub_Cards_App_009.png)

This is the syntax we need to use in order to change the state of a class component... it\'s a bit different than function components hooks because this function is always named **setState** that **always** receives an object and will merge this object with the current state of the component.

**Working with AJAX calls**

When working with AJAX calls we can simply use the native fetch() call but the playground above also has the axios library. Library is a simple one to use

> *Axios.get*
>
>  

Axios get function will return back a PROMISE... so in order to work with it properly we are going to use the keyword **await.** Remember if we do this we will have to label the handleSubmit function as **async:**

![](002_The_GitHub_Cards_App_010.png)

Now, in the example we are dealing with we have a another problem. If we get the data from the API call on our FORM component, we are out of luck updating the state of the parent App component. **REACT Components have ONLY one way flow of data.** A component CAN\'T change the state of its parent... but remember, the App component CAN pass properties down to its child component and those properties can be primitive values OR function references

![](002_The_GitHub_Cards_App_011.png)

<https://jscomplete.com/playground/rgs2.7>

\^\^\^ final code sample
