01 - Getting Started

Sunday, February 25, 2018

12:01 PM

 

All of the code samples I wrote during the course can be found at:\
<https://github.com/Ikanant/BasicTypeScript>

 

**Starting simple...... why use Typescript instead of custom JavaScript?\
\
**The answer to that question can be somewhat relative. For a lot of developers, JavaScript can feel a bit messy at times \*what some people call Spaghetti code\*. Using the \"Revealing module pattern, or the Revealing Prototype pattern, or others\" can be helpful but in general it just makes things a bit more complicated.\
\
What we are after with Typescript is that we want something that is MAINTENABLE and easy to re-use across our application.\
\
JOHN PAPA: \"Most JS developers write spaghetti code.... But we want to do things more like Ravioli code\
\
**JavaScript Dynamic Types\
** 

-   JavaScript provides dynamic type system

-   **The Good**

    -   Variables can hold any object

    -   Types determined on the fly

    -   Implicit type coercion (ex: string to number)

-   **The Bad**

    -   Difficult to ensure proper types are passed without tests

    -   Not all developers use ===

    -   Enterprise-scale apps can have 1000s of line of code to maintain

 

**What are the Alternatives?**

 

![](000_01_-_Getting_Started_000.png){width="6.408333333333333in" height="4.608333333333333in"}

 

 

\*\*\* **TypeScript** is more a SUPER set of JavaScript, than a whole other language.

 

One good way to think of Typescript, is the way we think of JAVA. People are sometime hesitant to write Typescript because since it gets generate to JS, then why not write JS ?? When working with JAVA developers are dependent on the JVM Java Virtua Machine, which pretty much compiles the code written by the developer into Assembly code (which everyone agrees is not a good idea code in).... So Typescript is similar, it saves us developers time by converting easy to understand code, into JS (spaghetti code)\
 

 

**Typescript Features**

 

-   Any Browser

-   Any Host

-   Any OS

-   Open Source

-   Tool Support\
     

> Typescript Supports standard JavaScript code.. (meaning that if we create a .ts file with regular JS in it, it will compile into it\'s proper JS output no problem.
>
>  
>
> Typescript provides **static typing**, so it is a lot easier to work with various data types across our program without worrying about variables being passed around the code.
>
>  
>
> **Encapsulation through classes and modules** is a critical piece. We can write classes and we can even use naming containers (called modules)
>
>  
>
> **Support for constructors, properties, functions** **\
> ** 
>
> **Support of INTERFACES !!** While JS doesn\'t support interfaces natively this is something that can be done through JS. If we create an object that we expect to contain FIRST NAME and LAST NAME once we compile the code we could CATCH the error right there before it turns into erroneous JS.
>
>  
>
> **=\> function support (lambdas)** This is something that is coming out across multiple languages including ES6 that allows us developers to write arrow functions. Very helpful stuff for writing anonymous functions for things like CALLBACKS, etc\
> \
> **Intellisense and Syntax checking** .... So if using an Editor that allows for such tools, we can figure out errors in our code even before compiling once

 

 

**The Typescript Compiler\
\
** 

![TypeScript JavaScri pt tsc first.ts ](000_01_-_Getting_Started_001.png){width="4.791666666666667in" height="1.825in"}

 

It is worth noting that when writing TS code in various tools like VS, we sometimes do not need top run the tsc command from our terminal since VS will automatically convert your TS file into JS rapidly on SAVE.

 

 

![TypeScript Encapsulation class Greeter { greeting: string; Static Typing var constructor (message: string) { this . greeting greet() { return \"Hello, = message; \" + this. greeting; JavaScript --- (function ( ) { Greeter --- function Greeter(message) { this . greeting = message; Greeter. prototype. greet = function ( ) { + this. greeting; return \"Hello, return Greeter; ](000_01_-_Getting_Started_002.png){width="7.658333333333333in" height="3.7416666666666667in"}

 

**TypeScript Syntax, Keywords and Code Hierarchy**

 

Since TS is a superset of JavaScript we will be using the same syntax rules that we already know from JS. Hence:\
\
 

![• TypeScript is a superset of JavaScript • Follows the same syntax rules: { } brackets define code blocks Semi-colons end code expressions • JavaScript keywords: a for o if More.. ](000_01_-_Getting_Started_003.png){width="5.183333333333334in" height="4.091666666666667in"}

There are on the other hand a couple of more keywords and operations we will need to familiarize ourselves with:

 

 

![Important Keywords and Operators Keyword class constructor exports extends implements imports interface module / namespace public/private \<typeName\> Description Container for members such as properties and functions Provides initialization functionality in a class Export a member from a module Extend a class or interface Implement an interface Importa module Defines code contract that can be implemented by types Container for classes and other code Member visibility modifiers Rest parameter syntax Arrow syntax used with definitions and functions \< \> characters use to cast/convert between types Sepa rator between variable/pa rameter names and type ](000_01_-_Getting_Started_004.png){width="6.783333333333333in" height="4.966666666666667in"}

 

**Code Hierarchy\
** 

In Javascript we only have functions... which, with the help of various design patterns out there, can be used with a simulated hierarchy and even deal with things like Namespaces to take things our of the global scope.

 

In the case of TS we will have a very defined hierarchy that is built in.

 

-   **TOP Level: Module / Namespace**

    -   Act as a naming container that can EXPORT different members. Inside of a module we can have many things, but one of them and the post important is the **CLASS**

-   **MID Level: Class**

    -   Class is a container for different members which can range from

    -   Classes can Implement Interfaces

-   **LOW Level: Fields, Constructor, Properties & Functions**

>  

These points are a very basic way of looking at what Typescript has to offer but we will go over that in future modules:\
 

![Interface Module/Namespace Class Fields Constructor Properties Functions ](000_01_-_Getting_Started_005.png){width="5.508333333333334in" height="4.175in"}

 

 

**Tooling/Framework Options\
\
**One of the areas where TS real excels is it\'s support for tooling and frameworks that are out there.

 

![Node.js Emacs Visual Studio VS Code, Atom, and WebStorm are also great tooling cross platform options Sublime TypeScript Playground ](000_01_-_Getting_Started_006.png){width="6.025in" height="3.4166666666666665in"}

 

 

There is an online tool commonly used by developers that will turn TS code into JS code on the fly in order to help devs better understand what\'s going on behind the scenes for our code.

 

<https://www.typescriptlang.org/play/>

 

![lea 1 2 3 4 6 7 8 11 12 13 14 15 16 17 18 21 22 IYpeScrip! TypeScript Walkthrough: Classes v class Greeter { greeting: string; constructor (message: string) { this. greeting = message; greet() { return \"Hello, showGreeting() { return \"Greeting: get it run it join in Run JavaScript 1 2 3 4 s 6 7 8 10 11 13 14 IS 16 17 18 20 var (function () { Greeter = function Greeter(message) { this . greeting message; Greeter. prototype. greet = function () { return \"Hello, \" + this.greeting; Greeter . prototype. showGreeting = function () { return \"Greeting: \" + this.greeting; return Greeter; \" + this.greeting; 1 \" + this.greeting; var greeter = new Greeter( \"world\"); var button --- document . createE1ement( \'button\') button . innerText = \"Say Hello\" button. onclick = function() { alert (greeter. ) 12 var greeter = new var button = document. createEIement( button\' ) ; button. innerText - \"Say Hello\"; button . onclick = function () { alert (greeter. greet ( ) ) ; document . body . appendChi1d(button) ; ](000_01_-_Getting_Started_007.png){width="8.275in" height="4.716666666666667in"}

 

Here is another example of a simple TS file:\
\
 

![// Interface E interface IPoint { getDist(): number; / / module Errodule Shapes { // Class E export class Point implements I Point { // Constructor constructor(public x: number, public y: number) { } // Instance member getDist(): number { return Math. sqrt(this.x // Static member static origin = new Point (e, e); \* this.y + this.y \* this•y); // Local variables var p: IPoint = new Shapes. Point(3, 4); dist = . etDist ](000_01_-_Getting_Started_008.png){width="6.8in" height="3.9166666666666665in"}

 

 

**Summary\
\
** 

![Summary • TypeScript is an open source language that compiles to JavaScript . Key features: Code encapsulation Type support • Supports multiple tools: Node.js Sublime (and others) Visual Studio ](000_01_-_Getting_Started_009.png){width="7.3in" height="5.65in"}

 
