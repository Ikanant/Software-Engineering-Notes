JavaScript Crash Course

Tuesday, April 30, 2019

10:32 AM

JS is a very different language that is used to be just a few years ago. ECMAScript, which is the official specification that JS conforms too has improved A LOT in the past few years, after a rather long period of no updates to the language at all. Today, the ECMAScript technical committee, also known as TC39, perform yearly releases of ECMA script and modern browsers shortly follow by implementing its new features. This whole thing started in 2015 (or it\'s other commonly known name ES6) and since then we have head yearly releases.

**Variable and Block Scopes**

{{{}}} // Is this valid?\
Testing in the console yields no errors...which means there is no error... So what did they do? These are NESTED block scopes. We could write code in there and then access the v variable outside the blocks and it would work just fine.

A block scope is created with a pair of curly braces. These apply to IF statements and FOR statements as well.

Block scopes are DIFFERENT than function scopes. One difference is dealing with variables within a function scope. If we declare a **var** inside a function, we are NOT able to reference that variable outside of that function... On the other hand, if we declare a **var** inside a block scope, you can totally access them outside the scope afterwards. The solution to this is **let.**

One note is that we could also use **const** keyword. **Let** and **const** behave almost the same way, except that **const** is meant to be represent a constant REFERENCE to a variable.

Note: We are saying references and NOT values. Defining an object with **const** does NOT make it an immutable object. It just means a constant reference to it. We can still make changes to that OBJECT. \-\--\> if the variable defined for a **const** is a scalar one, then we CAN think of it as an immutable object. We CANNOT mutate their values. However, placing an array or object in a **const** is a different story. The **const** will guarantee the variable is pointing to the same array or object, but the content of the array of object can be mutated.

**Arrow Functions**

A way to define a function without having to use the keyword function:

![const X function () // \"this\" here is the caller of X const Y S NOT the caller Of Y // It\'s the sane \"thts\" found in Y\'s scope ](001_JavaScript_Crash_Course_000.png)

This shorter syntax is preferable, not only because it\'s shorter, but also because it behaves more predictable with closures... An arrow function DOES NOT care who calls it. While an regular function DOES.

Regular functions ALWAYS binds the value for the \'this\' keyword, for its caller. If it didn\'t have an explicit caller, then the value of the \'this\' keyword will be determined by the calling environmnet. In the image above that would be the global window object.

**IMPORTANT:** An arrow function will close over the value of the \"this\" keyword for its scope at the time it was defined! - This works great for delayed executions cases like events and listeners, because it makes it have easy access to the defining environment, NOT the calling environment.

![](001_JavaScript_Crash_Course_001.png)

The \'this\' keyword on the function2 refers to what was available to the \'this\' variable at the time it was called.

![le e e z Ea.enbs asuoa za•enbs e u\'ruaJ ) (e) lauenbs asuoa ](001_JavaScript_Crash_Course_002.png)

\^\^\^ Syntax fun.

**Object Literals**

![const const const 10, 28 answer mystery = InverseOfPI - 1 / math_P1; obj = 10, 20, Cmystery): 42, InverseOfPI , console \_ log(obj \_ answer) ; console \_ log(obj \_ Inver seOfPI) ; ](001_JavaScript_Crash_Course_003.png)

\^ Notice Dynamic properties: \[mystery\]. It looks like an Array literal, but actually JS will evaluate what\'s inside the square bracket and make the result of that the property name.

**Destructuring Syntax**

Works for both Arrays and objects. We need to think of Destructuring in terms of the cases in which we want to retrieve some values out of an object... we could do it trivially line by line, OR we can use the curly bracket syntax.

![// const PI Hath.P1; // const E Hath.E; // const SQRT2 Hath.SQRT2; const (PI, E, - Hath; ](001_JavaScript_Crash_Course_004.png)

It destructures the three properties out of the right object and into the left hand side scope.

*Const {Component, Fragment, useState} = require(\'react\');*

Destructors also works inside function argumnets. If the argument we are passing to the function is an object, instead of using the name of the object, we can use the destructuring syntax within the function parenthesis to destruction just the properties we are worried about and make them local to that function.

![Il const circle 14 16 19 label: \'circleX\', const circleArea z (radius)) (PI • radius • radius). toFtxed(2); console. Iog( circleArea(ctrcIe) ](001_JavaScript_Crash_Course_005.png)

In the case of Arrays we got:

![// const (first, second„ forth) z \[10, 20, 30, 40); ](001_JavaScript_Crash_Course_006.png)

![const \[first, . restofltems\] Cle, 20, 30, 40\] console. first) ; console. log(restOfItems) ; Hide network log Context Group Console cleared ](001_JavaScript_Crash_Course_007.png)

![const (first, ..restOfItems) = t 10, 20, 30, 40); console. log(first); console. log(restOfItems) ; 6 • const data tempt: \'001\', temp2: \'oe2\', firstNane: \'John\', LastNaæ: \'Doe\', const (tempt, temp2, 13 19 z data; \[ ..restofltems\]; const newArray const z person ](001_JavaScript_Crash_Course_008.png)

\^\^\^ Notice how we will be dealing with Shallow Copies here. Any nested objects or arrays will be shared between these copies

**Template Strings**

We can define strings in JS by using either single quotes or double quotes. These two ways are equivalent. Modern JS has a third way to define strings... that\'s by using the back-tick characters... which these new strings are called Template Strings.

Template strings can have dynamic values through something called INTERPOLATION. We can inject any dynamic expression in JS within \${} expressions.

![const const const 7 htmll greeting z \"Hello World\"; answer html - • Forty TWO • ; ](001_JavaScript_Crash_Course_009.png)

With template strings, we can also have MULTIPLE lines of a string. Something that was not possible before.

**Classes**

JS offers many programming paradigms... and OBJECT ORIENTED programming is one of them. Everything in JS is an object, included functions! - Moderns JS also added support for a class syntax..

A class is template (or blueprint) for us to define shared structure and behavior between similar objects. We can define them, make them extend other classes and instantiate objects out of them using the **new** keyword.

![I • class Person ( Constructor (name) this.name z name; greet() console. tog( •Hello \${thts .name)! • 9 e, class Student extends Person ( Prwerve Ico Selected context only Group Simuar Console was cleared Hello Max! Hello Tina from 1st Grade I am special! 10 • 13 1B 19 24 constructor (name, Level) super(nane); this. level level; greet() const 01 const 03 = from ) ; const 02 new \"1st Grade\"); \"2nd Grade\"); ( ) console. log(\'l am special! • 03.greet 01. 02. greet(); 03. greet(); ](001_JavaScript_Crash_Course_010.png)

**Promises and Async/Await syntax**

In regular JS I have already worked with plenty of promises. Utilizing the .then syntax is relatively straight forward and useful... but at times (especially when dealing with nested cases) we run into some dirty looking code (hard to read).

![I • const fetchData = C) 2 fetch( console. log(data) fetchData() ; ](001_JavaScript_Crash_Course_011.png)

We can simply the code above using the modern way to consume promises in JS. Essentially we just \*await\* on the asynchronous call the returns a promise. That will give us back the response object. To make these away calls, we simply **NEED** to label the function as **async** like the image bellow:

![9 • const fetchData async 10 1B const resp z await fetch( const data await resp.json(); console. (data) ; fetchData() ; 1 ](001_JavaScript_Crash_Course_012.png)

**Note:** Keep in mind that once we **await** on anything in a function like fetchData like above, the function itself becomes asynchronous and will return a promise object.
