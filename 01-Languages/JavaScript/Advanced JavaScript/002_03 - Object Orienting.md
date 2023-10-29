03 - Object Orienting

Friday, April 29, 2016

11:07 AM

 

**Agenda:**

-   Common OO Patterns

-   Prototype

-   "Inheritance" vs. "Behavior Delegation\"

 

**Singleton**

*var Router = function() {*

*     if(Router.\_\_instance\_\_) {*

*          return Router.\_\_instance\_\_;*

*     }*

*     Router.\_\_instance\_\_ = this;*

*     this.routers = {};*

*}*

*Router.prototype.setRoute = function(match, fn) {*

*     this.routes\[match\] = fn;*

*};*

*var myrouter = new Router();*

*var another = new Router();*

***myrouter === another;***

 

***Observer***

*function PageController(router) {*

*     this.router = router;*

*     this.router.on("navigate",*

*          this.fetchPage.bind(this)*

*     );*

*}*

*PageController.prototype.fetchPage = function(d) {*

*     \$.ajax({*

*          url: d.page_url*

*     })*

*     .done(this.loaded.bind(this, d.page_url));*

*};*

*PageController.prototype.loaded = function(d,u) {*

*// Display the page content from \'d\'*

*     this.router.emit("pageLoaded", u);*

*}*

*var router = new Router();*

*var thepage = new PageController(router);*

 

**Prototype**

Every single "object" is built by a constructor function

Each time a constructor is called, a new object is created

A constructor makes an object "[based on]{.underline}" its own prototype. (THIS IS NOT TRUE)

Based on implies that we take a prototype and we make a copy of it. Thats the way it works on Class Oriented languages. Thats not what happens in JavaScript.

**Right Answer:** The constructor makes an object that is **[linked to]{.underline}** its own prototype

\_ \_ we are gonna call: Dunder 

\_ \_ proto \_ \_ : dunder proto

I will insert the diagram that explain the Prototype model but keep in mind that it is VERY similar to the Scope model. If an object does not contain a certain property it will go up the chain and check if the Prototype object has it...

 

 

Simple Diagram to study:

![](002_03_-_Object_Orienting_000.png)

 

 

A more complex version of that:

![](002_03_-_Object_Orienting_001.png)

 

**Quiz:**

 

1.  What is a constructor?

    a.  It is a function that is called with the NEW keyboard

2.  What is \[\[Prototype\]\] and where does it come from ?

    a.  Is a linkage from one object to another object

3.  How does a \[\[Prototype\]\] affect an object?

    a.  We can call a property or method on an object reference and if it can\'t find it it delegates to its prototype object

4.  How do we find out where an object\'s \[\[Prototype\]\] points to?

    a.  Dunde proto: \_\_proto\_\_

    b.  Object.getprototypeof

    c.  .constructor.prototype (HACK)

 

 

**Inheritance**

 

When dealing with common Object Oriented programming we were tought to think of classes as blue prints. What does this mean? Well, in general a class only contained the characteristics of such class, and when we instanciated the class we pretty much made COPIES (physical) from that blue print. Later on we were able to make changes to such classes and did not need to worry about the status of the original blue print at all. For example, if an architect creates a blue print of a builder and a constructor builds such building, that physical building is not connected in any way to the blue print. If they deside to demolish the last floor, it doesn't mean that every time a new building is going to get constructed from the blueprint is going to be missing the last floor information. In JavaScript this is different...

 

Inheritance means: COPY......so, if JavaScript copying does not exists....then we should not call it inheritance

 

So, rather than stating that JavaScript has inheritance, we can say JavaScript has *[Bhavior Delegation]{.underline}*

 

**OLOO**

 

So far we have learned a way to \"practice\" some sort of inheritance by using Prototypes.....the way we have done it though has been a bit confusing a lengthy....right now we can learn how to go a bit a head....and simplify things a little...

 

OLLO: **O**bjects **L**inked to **O**ther **O**bjects

 

![](002_03_-_Object_Orienting_002.png)

 

**Quiz**

 

1.  How is JavaScripts \[\[Prototype\]\] chain not like traditional/classical inheritance?

    a.  It does not copy. The arrows go in the opposite direction

2.  What does \"behavior delegation\" mean and how does it describe object linking in JS?

    a.  Objects delegate up the chain. What that object happens to be is arbitrary

3.  Why is \"behavior delegation\" as a design apttern a helpful thing? What are the tradeoffs?

    a.  With delegation we are embracing that all object continue to exists and they are dynamically changing...With classes, they are sort of a snapshot.

    b.  Tradeoff: Everything is public. Which means you don't get any private states

4.   

 

 

04 - Async Patterns

 

**Agenda**

-   Async Patterns

    -   Callbacks

    -   Generators / Coroutines

    -   Promises

 

**Callbacks**

 

Our brain works synchronously. So, why are we talking about this?

 

Answer: How do I take something that is fundamentally asynchronously like a timer, and express in such a fassion that I can reason about that asynchronous code in a synchronous fassion...

 

Callbacks is how we do this

 

Callback: Is a continuation

 

**Callback Hell**

 

Inversion of Control. When using utilities that we trusts like: SetTimeout...we are pretty much giving our program the trust to take care of whatever task we were originally dealing with. We are giving them the control.

 

We are going to try to fix this...

 

(This, along some other examples shown is not really correct)

![](002_03_-_Object_Orienting_003.png)

 

 

We are going to fix the \"callback\" problems with something called **Generators**

 

**Generators (yield)**

 

Everyone\'s assumption: As soon as the first line of a function runs, we all assume that it will run every single line of that function before anything else runs... That's called the run to completion....and we assume it can never be interrupted..... This is NOT true upon generatorrs

 

Generators: A type of functions that can be interrupted half way through its run time and continued later on...

 

New syntax: Function\* (not function pointer !!!) This functions have this new keyboard called yield. See the example:

 

![](002_03_-_Object_Orienting_004.png)

 

 

When you call a generator function, what you get back is an **Iterator.** When we type it.next() we are going to start running until we get to the yield statement. A generator can pause itself and an iterator will resume it.

 

Why do we need this ?????

![](002_03_-_Object_Orienting_005.png)

 

 

Note the the null will be the returned value for that first run() call. What we pretty much deal with is that when using yield we are having a two way conversation mechanism with the function... When the function comes back to run, we can then pass in a value and it will replace the yield null statement that we left hanging. **Two way message passing mechanism**

 

This is NOT asynchronous.....so what then?

 

Here we go:

![](002_03_-_Object_Orienting_006.png)

 

Generators...........are the \*new\* tech that will become the \*BIG\* thing...

 

**Promises**

 

Promises: (two metaphores for it)\\

1.  You walk at the counter at McDonalds...you hand the cashier some money, what usally happens is that you don't get your food right away, you get a receipt first with an order number on it. Do you step back with other people to wait for your order. Once you hear your number, you get your food in EXCHANGE of your food receipt.

    a.  This is an asynchronous transaction

    b.  **Promise: A call to a function that I want some end result to happen and that function tells me it can\'t finish it yet. But that function hands us back a promise and at some later time when the function finishes that task you exchange the order number for the value that you asked for\
        ** 

2.  What if we could call a function but we can subscribe to an event that can let us know when that function finishes....Like a continuation/completion event...That's essentailly what promises are....

    a.  We are calling a function that doesn\'t finish yet, but it allow us to subscribe to a continuation event

 

Code:

![](002_03_-_Object_Orienting_007.png)

>  
>
>  

So we can have something like:

![](002_03_-_Object_Orienting_008.png)

>  
>
>  

In this case we are pretty much getting our controller back (from back on top where we talked about the Inversion of Control. In these scenarios, we provide a function with the information that we need but instead get a promise back....which we can use however we want. And we decide what to do next... We are now in control of the entire completion of our program...

 

Promises are now built in after ES6

 

![](002_03_-_Object_Orienting_009.png)

 

 

 

**Asynquence**

 

Promises can be really really tedious in the real world... for that we have a set of tools that can help use get things simpler.

 

A recommended tool for such scenarios is called Asyquence

 

**Sequence = automatically chained promises**

 

Gates......Sequences are things that go this then this then this then this pattern. A gate says: two or more things are going to happen at the same time and I don\'t care when they finish and it what order, I just need them ALL to finish before I move on...

 

Example of code:

![](002_03_-_Object_Orienting_010.png)

 

 

Meaning of life example:

![](002_03_-_Object_Orienting_011.png)

 

 

**How about Generators and Promises put together?**

 

This is actually the most popular pattern we are getting used too...Runner utility it will receive promises, it will wait for them to complete before it starts back up the generator...It will automatically continue to the end for us...

 

![](002_03_-_Object_Orienting_012.png)

 

 

 

 

**This is some unexplored territory that is COOL. The idea of taking two or more generator and interleaving their operations:**

 

![](002_03_-_Object_Orienting_013.png)

 

 

**Quiz**

 

1.  What is \"callback hell\" ? Why doi callbacks suffer from \"inversion of control\"?

    a.  Inversion of Control. Is handing the control of the rest of your program over to some utlity and all of the trust that that involves

2.  How do we pause a generator? How do you resume it?

    a.  Yield keyboard

    b.  Next keyboard

3.  What is a promise? How does it solve inversion of control issues?

    a.  A future value... It's a continuation event....

    b.  Instead of passing my CONTINUATION into the function, I receive a promise back... It puts me in control back..

4.  How do we combine generators and promises for flow control?

    a.  Call a generator, have it yield out promises and when that promise is generated then restart the generator for us
