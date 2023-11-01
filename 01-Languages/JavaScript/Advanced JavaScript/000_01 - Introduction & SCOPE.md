01 - Introduction & SCOPE

Friday, April 29, 2016

10:53 AM

Author: Kyle Simpson

**The Advanced \"Basic\" Class\...**

**[Agenda:]**

-   **Scope, Closures**

    -   Nested Scope

    -   Hoisting

    -   this

    -   Closure

**SCOPE**

The WHERE to look for things

JavaScript has function scope only (until now but this might change)

LHS & RHS = Left hand side & Right hand side

Global variable leakage: When in non-strict mode with JavaScript, if we make a call like *[bam = \"hello\"] *where bam is an undefined variable, JavaScript will try to be the \"Good\" guy for you and create such variable in the GLOBAL scope.

Undefined and Undeclared are VERY DIFFERENT

Undeclared: There is no present declaration for the variable in any of the scopes

Undefined: It was declared, but it has a special empty value mistakingly called undefined but is more like: Uninitialized

Keep in mind that when dealing with LHS calls, JavaScript will automatically create what we need and place it in the global scope. On the other hand, when dealing with RHS calls, JavaScript will NOT do the same, instead it will throw a reference error.

Function Declaration VS Function Expressions: The way to figure this out is whether or not the function keyboard is the very first word in the statement (Not the first thing on the line - remember that statements can break into multi-lines)

***function bar() {}** // *This is a function DECLARATION

***var foo = function bar() {}** // *This is a function EXPRESSION

In Expressions: We often see expressions as ANONYMOUS functions

When dealing with function expressions, we will not be able to call these functions from outside their local scopes. This means these functions will only be available through themselves

Functions that do not posses a name\..... like:

***var foo = function (){}***

are called anonymous functions.

Negatives of using Anonymous function expressions:

1.  No way inside of the function to refer to our self\... no ability to do any recursion. There are a lot of people who think that the **this** keyboard is a reference to yourself, this is NOT true

2.  Error in production. Debugging. A stack trace for anonymous functions are EXTREMELY hard to track down

3.  Self document code. For anonymous functions you need to look everywhere to understand what it will do

Block scope:

catch (err) {} 

The err is only available from the catch block. NOT anywhere else

**Lexical Scope** (what we have been using so far) **& Dynamic Scope**

Lexical Scope means COMPILE time scope. At the time that you write your code and later compile it, the decision for how all the scoping for the things that we are gonna do are made at compilation time. The compile decides what your scope is.

**eval** keyboard: Takes any given string and it treats the content as if it was code. that existed at that point in the compilation\...

**eval(\"var bar = 42;\");**

It has the power to modify the existing Lexical scope of functions

Using eval to cheat on JavaScript, you will make your code run SLOWER.

**IIFE pattern**

We can wrap a function expression with parenthesis.

***(function(){***

***     var foo = \"foo2\";***

***     console.log(foo);***

***})(); // \<\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--***

The gain from using this pattern is to potentially hide functions and code that do not need to be public in the global scope. If we have 100 functions and only 1 of them needs to be added to the global scope, then we just add that function as a property of the window function and thats it. We end up with the other 99 functions private inside their own private scope.

It is always recommended to name our IIFEs

There are various ways to deal with IIFEs but we can send inputs to the IIFEs:

**var foo = \"foo\"**

***(function (bar) {***

***     var foo = bar;***

***     console.log(foo) // \"foo\"***

***})(foo);***

**Block Scope**

Block scope is something that is coming as of IE6 that is coming to us through a new keyboard called: **let**

**let** is going to be a cousin of the **var** keyboard.

The difference is that when we use the **let** keyboard, it will immediately hijack the scope of whichever block we happen to be in and it will add that variable to that block rather than the enclosing function.

**for (let i=0; i**

**}**

**console.log(i)**

// Some people say we should always use **let\...**

One of the main problems with the **let** keyboard is that it does not HOIST\...What this means is that if we have a **let** in the middle of a block, if that variable is used ABOVE such code we would get a ReferenceError\.... the best way to understand this is with a **var\...** if we declare a var in the middle of any block but used it before hand, this would be VALID\....because that var was HOISTED during compile time.

A solution to this is creating explicit blocks\....** Depricated**:

**let (baz = bar) {**

     **console.log(baz); // \"bar\"**

**}**

**console.log(baz); // Error**

**Dynamic Scope:**

This is not present in current JavaScript

**function foo() {**

**     console.log(bar); // \"dynamic\"**

**}**

**function baz() {**

**     var bar = \"dynamic\";**

**     foo();**

**}**

**baz();**

**Hoisting**

Hoisting is not actually a thing\...it\'s a mental construct we have actually invented to explain the behaviors of JavaScript\...

Hoisting is a beautiful way to understand what goes on with JavaScript and how the Compiler deals with things before execution time.

**[example:]**

**a;**

**b;**

**var a = b;**

**var b = 2;**

**b;**

**a;**

**BECOMES:**

**var a;**

**var b;**

**a;**

**b;**

**a = b;**

**b = 2;**

**b;**

**a;**

This process will be the SAME with functions.

Do realize that function expression will NOT Hoist

[Functions are HOISTED before variables !]

**foo()**

**var foo = 2;**

**function foo() {**

**     console.log(\"hello\");**

**}**

**function foo() {**

**     console.log(\"world\");**

**}**

For the code above, the first thing that will happen is that the first foo() function will be HOISTED, then when second one comes it REPLACES our original function\....then when the variable comes\....it gets IGNORED. Functions with the same name being HOISTED are always going to replace their counter parts, Variables will ALWAYS get IGNORED in these kind of scenarios.

The above code will log \"foo\"

**mutual recursion:** Two or more classes can only each other\...

**this** (detour)

This topic will seem weird in this section of code but it makes sense to talk about it now because it will give us a great sense of contrast with the Lexical Scoping model.

*[Every function, while **executing**, has a reference to its current execution context, called **this.**]*

In order to really understand how to properly use the **this** keyboard, we will have to set aside all known fact about using **this** in other programming languages like the ones designed for OOP. 

Understanding **this** properly will rely on 4 main questions we need to as ourselves:

Take this code into consideration

**function foo() {**

**     console.log(this.bar);**

**}**

**var bar = \"bar1\";**

**var o2 = {bar: \"bar2\", foo: foo};**

**var o3 = {bar: \"bar3\", foo: foo};**

**foo();        **  // \"bar1\"

**o2.foo();    ** // \"bar2\"

**o3.foo();    ** // \"bar3\"

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

**var o1 = {**

**     bar: \"bar1\",**

**     foo: function() {                          **// Notice that this function will work normally and be used by other objects by simply calling the o1 object

**          console.log(this.bar);**

**     }**

**};**

**var o2 = {bar: \"bar2\", foo: o1.foo };**

**var bar = \"bar3\";**

**var foo = o1.foo;**

**o1.foo();          **// \"bar1\"

**o2.foo();          **// \"bar2\"

**foo();            **   // \"bar3\"

**4 RULES** (dependent of the call site)

1.  a

2.  b

3.  Implicit Binding Rule

    -   That object at the call site (or the context object) becomes the **this** keyboard\.... [o2 nad o3 object on top]

    -   note: In JavaScript, everything is a reference to an object\....or everything is a reference to a function

4.  Default Binding Rule

    -   If you are in **strict** mode, default to **this** keyboard to the **undefined** value\.... [foo() object on top]

    -   If you are NOT in **strict** mode, default to **this** keyboard to the global object
