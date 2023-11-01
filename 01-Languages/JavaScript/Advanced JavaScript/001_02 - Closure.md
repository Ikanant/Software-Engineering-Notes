02 - Closure

Friday, April 29, 2016

11:05 AM

Closure is a mathematical concept. But thats not what we need to know.

**[Definition]:** Closure is when a function "remembers" its lexical scope even when the function is executed outside that lexical scope.

Example:

**function foo() {**

**     var bar = "bar";**

**     function baz() {**

**          console.log(bar);**

**     }**

**     bam(baz);**

**}**

**function bam(baz) {**

**     baz();              ** // "bar" This IS closure. the fact that the lexical scope stayed attached to this function no matter what

**}**

**foo();**

Now lets consider the following example. Within the given for loop we would expect to have 1 through 5 printed every second. But what is happening? Here we need to understand that when using Closure, we dont simply take a snapshot of the variable we are trying to use. We directly access whatever value that variable has in real time... 

**for (var i=1; i\<=5; i++) {**

**     setTimeout(function() {**

**          console.log("i: " + i);**

**     }, i\*1000);**

**}**

What we end up when we run this code is 5 \'6\'s printed to the console. why? because when the first second passes, the loop already finished all together and the last value that i has in this case is 6.

How do we fix it? We can just create a IFIE around our loop, creating our own new Scope for EACH iteration\...

**for (var i=1; i\<=5; i++) {**

**    (function(i){**

**         setTimeout(function() {**

**              console.log("i: " + i);**

**         }, i\*1000);**

**     })(i);**

**}**

Another solution is just using **let**

**for (let i=1; i**

This would also work

**[Classic Module Pattern]**

Two main characteristics:

1.  There most be an outer wrapping function that gets it executed. (It doesn\'t have to be an IFIE)

2.  There most be ONE or more functions that get return from that function call...that have a closure over the inner private scope

**[Modern Pattern]**

**define("foo", function() {**

**     var o = {bar: "bar"};**

**     return {**

**          bar: function(){**

**               console.log(o.bar);**

**          }**

**     };**

**});**

IMPORTANT: Future & ES6+ Module Pattern:

**File based !** We are going to treat the contents of a file as that it exists inside of a function so it will have its own swop (similar to a IFIE)...and instead of returning things we are going to use a new keyboard called: **export**

Everything we export will get added to the public API of that module.

The way we later load other modules is using the keyboard **import**

Import: Allows us to import one or many members of the API as first class thing

Example: **import** bar from "foo"; // This will ONLY import the br

If I want the whole module, then I use the **module** keyboard

Example: **module** foo from "foo";
