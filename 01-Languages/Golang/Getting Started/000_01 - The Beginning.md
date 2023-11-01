01 - The Beginning

Friday, April 29, 2016

12:13 PM

**The First Program**

For easy access to a simple playground to experiment with Go, please visit: *play.golang.org*

*Hello world*

Package declarations are required for ALL code files (also called Modules. We are not going to talk to much about packages in this course but we will mention the "main" package:

*package main*

Which is used by the Go compiler to determine the application entry point.

Inside of the main package we also need a function (func) that is also called "main" and accepts NO arguments. This function defines the entry point that we just mentioned.

*Notice this function is not wrapped in a class like we need to do in JAVA or C#. Functions are first class citizens in GO with all of the advantages that the style bring.*

*println*

Not meant for production use. Good for debugging.

We can create constant values within our program with the (const) key and setting values inside of the parenthesis:

*const (*

*     message = "Hello\"*

*     message2 = "World\"*

*)*

Constants can\'t be changed in GO. Similar to anything else

"var" keyboard similar to "const\"

Keep in mind that if we declare a var value inside the var parenthesis and we later on change the variable to something else within a method in our code. Go will take the value edited and disregard the originally defined one.

If we declare a variable inside our var tag and not initialize it, we can still use it on our code. Go does have the concept of NULL but it is not the same as any other language. If we use a not initialized String variable, it would just display as an empty string in our code.

There is another special function that each module can have called: init()

*init(){*

*}*

This init method will run every time this module gets called, wether it is in the main package or just called by another module. If we declare a variable inside the var tag and later change it in our init function, our message displayed in our main function will be the one stated inside init. The order is simple: VAR & CONST ---\> INIT ---\> MAIN

We can import packages to use in our module.

*import "fmt\"*

or

*import (*

*     "fmt\"*

*)*

If we have an import inside the module of a package that is never used. then we will get an error. This is meant for clean code.

![](000_01_-_The_Beginning_000.png)
