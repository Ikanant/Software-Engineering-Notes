01 - The Core 
 
Friday, April 29, 2016 
 
12:19 PM 

About GO:

- Work started 2007
- Initial release 2009
- Started as a \*systems\* language
- Like C ... but simpler
- Only \~25 keywords
- Cross platform
- Produces \*compiled\* code
    - **Gets compiled to machine language when it is RUN**
    - Since it doesn\'t need an interpreter....machines will be able to run GO code FAST
- Strongly Typed
    - PICKY when it comes to variables etc
    - If you try to add an Integer with a Float, we will get an error
- Support type inference:
    - a := 5.5 or a := 10

**Important:**

Go requires a WORKSPACE (not the same as with Eclipse)... within that Workspace we wil need three SPECIFIC folders: src, packages, lib...

The main difference between regular Eclipse workspaces and Golang worksapces is that we need to tell Windows WHERE our go workspace is in order to run successfully. (With Eclipse you can pretty much have as many Workspaces as you want)..... The are ways for you to write Go code outside such Worskpace, but this will be problematic once we start downloading Packages from online repositories (often from opensource projects) that we will use along the lifespam of our application.

We can check where our GOPATH is by typing:

- go env

**Package main**

We are telling the compiler to compile this file as a stand alone executable, and not as a shell library. Any executable we will write will need **package main** as its first line of code.

**Functions and packages**

Functions are first class citizens

**Variables**

When writing variables in GO, we can often use the INFERENCE tool to create our variables....but this holds true ONLY when we are inside of a function. When creating global variables in our go file we will need to use our reguar syntax to make things work....which is:

**var \<variable name\> \<variable type\>**

example: var name string

We can also create multiple variables at a time like:

Var (

> Name, course string
>
> Module float64

)

Variables that are declared and NOT initialized will be given a DEFAULT zero value

Keep in mind this is also valid:

**var name, course, module = \"Jonathan\", \"Docker Deep Dive\", 21.3**

Go will be smart enough to know what variable type to assign each variable....but this can be messy

**POINTERS**

Go passes arguments by VALUE and not by REFERENCE...

Meaning: When passing an argument to a function, Go actually makes a copy of that value and it places the copy of that value onto the stack of the function beiong called.

Similar to C and C++, if we want to pass values by reference in Go, we just need to use & and \*

& to get the memory address

\* To get the value inside that memory address

**Constants**

Constants will work very similar to variables....the two main differences are:

1.  We will use **const** instead of **var** (Simple enough)\\
2.  And with **const** we will not be able to use the shorthand notation := to initialize their values

**Global Variables**

When getting and setting environment varibales, do NOT forget of the \"os\" package. It will be most likely the tool to use for such instances.

**Functions**

Dealing with functions is simple and familiar....the only note I will make of them is when dealing with Variadic Functions (Functions for which we do not know what the input values will be...

When dealing with Variadic functions we use the ELIPSIS in front of the type...

Example: **func \<functionName\> (finishes ...int) int {**

**Conditionals**

If \<Boolean expression\>

The expression for IF statements NEED to be boolean expressions. NO numbers or strings

Operators:

==

!=

\<

\<=

\>

\>=

&&

\|\|

![Machine generated alternative text: if <simple statement> <code block> , <B001ean expression> { ](000_01_-_The_Core_000.png)

**Switch Statement**

Switches are very much similar from what we know from JAVA.... Only thing to note is that when a case is triggered in a switch statement, we do not need to write **break** to stop it from going to the other cases..... It will assume that automatically....

On the other hand, if we WANT the code to go to the NEXT (not all) switch statement we will use: **fallthrough** . That will jump to the next case even if it was not triggered by default

**The Role of IF in Error Handling**

Idiomatic to return an error as the last return from functions and methods

**LOOPS**

FOR and that's it......in Golang, there is no other (while) or any other version of looping.....only different versions of FOR

Infinite Loop (same as while(true)):

**for {**

> **\<code\>**

**}**

**Break from Loop**

Consider the case in which we have 3 for loops that are nested.... By default, when we break from the inner most loop, and just exit to the second loop....bu what if we actually want to break to the first loop (skip a value)... in that case we would use LABELS

![Machine generated alternative text: for <expr. <code> breakPoint for <expr...> { <code> for <expr...> { <code> break breakPoint ](000_01_-_The_Core_001.png)

In the above code, when we break inside the YELLOW for loop, we will head out to the RED loop instead of the BLUE... the only thing to keep in mind in these kind of situation is that we need to name our LABELS carefully and not something already taken by the Golang programming language itself

**Important Note:** The Label needs to be right on top of the FOR loop it directs too....nothing in between

**Continue:** if we have a Continue inside the for loop, it wills tart from the beginig :

![Machine generated alternative text: for timer --- le; timer timer % 2 continuel fmt . Print ln (timer) e, timer-- { time. Sleep(l * time. Second) ](000_01_-_The_Core_002.png)

**Arrays And Slices**

When dealing with Arrays and Slices remember you can\'t have an array with different types

![Machine generated alternative text: Arrays Arrays vs Slices Slices O 2 3 4 5 6 "Apples" "Oranges" "Bread" "Milk" "Hummus" "Cheese" "Chocolate" O 2 3 4 5 6 "Apples" "Oranges" "Bread" "Milk" "Hummus" "Cheese" "Chocolate" Numbered list of a single type • Fixed length • Numbered list of a single type • Can be resized ](000_01_-_The_Core_003.png)

**Sintax:**

One way to create a slice is by writing:

mySlice := make (\[\]string, 5, 10)

When using this syntax we just need to remember we will be creating an (underlying) array with 0 values for its 5 elements... even though we are creating a slice with a capacity of 10. Using the built in make method would not allow us to initialize our slice though. For that we will use:

mySlice := \[\]string{\"A\", \"B\", \"C\"}

We can also do a Slice of Slices. Just like this (Left side is INCLUSIVE.... And right side is EXCLUSIVE

sliceOfSlice := \[2:5\]mySlice

**Maps**

Very similar to how we make slices. Just add a key type inside square braquets:

**map \[keyType\] valueType**

Key type has to be able to be compared (int, strings, floats, etc...) but no slices or Arrays or anything like that.

Syntax Examples:

myMap := make(map\[string\]int)

myNewMap := map\[string\]int{

> \"A\": 1,
>
> \"B\": 2,
>
> \"C\": 3,
>
> }

**Iteration**

When iterating through a map using the range method, we will iterate through the map in a \*random order. Go does not iterate through a map similar to a Slice.

**Manipulation**

When wanting to edit or add a new value to a map is simple and equal... We just write **myMap\[\<key\>\] = newValue**. If the key already exists in the map, it will get replaced with the new Value; if not, then it will get added to the map.

**Maps are reference types:**

- Passed to functions by reference
- Changes made by functions visible to caller
- Unsafe for concurrencty
- Cheap to pass

**Specify size for large maps**

- make( map\[\<keyType\>\] \<valueType\>, size)
- Can improve performace

**[Structs]**

Structs are proven to be useful when dealing with CUSTOM DATA TYPES.

Structs are basically a collection of NAMED fields. Each field are of specific type and each field has its own important name.

Example:

**type Circle strict {**

> **R float64**
>
> **D float64**
>
> **C float64**

**}**

**Object Oriented Programing in Go (or not)**

OOP is the application of creating small, modular sections that speciae in doing pretty much one thing.

**Structs**

Simple but not the same as a regular class

**[Concurrency]**

**What is Concurrency ?**

Creating multiple [proceses] that execute [independently] (not the same as simultaneously)

The best way to explain Concurrency is by understanding its core difference from parallelism. Take for example... this morning when I woke up I decided to answer a couple of emails. Once I did this, I did not just wait around for those emials to get back to me to continue my day. Once I clicked send, I started doing some coding work I wanted to push to my GitHub page. When I coded for around 1 hours I got tired and then proceeded to watch an episode of Game of Thrones... then, code a bit more, and then.... Remember! I needed to check if someone replied to one of my emails..... This IS concurrency. It is the ability of working on multiple task (not necessarily at the same time) and be able to interchangebly work on each of them without having to finish one of them first.

_\"... concurrency is the composition of independently executing processes, while parallelism is the simultaneous execution of (possibly related) computations. Concurrency is about **[dealing]** with lots of things at once. Parallelism is about **[doing]** lots of things at once.\"_ - Rob Pike

**What is Concurrent Program?**

![Machine generated alternative text: ssa)0Jd ddv ](000_01_-_The_Core_004.png)

![Machine generated alternative text: ssa)0Jd JJJJ ddv ](000_01_-_The_Core_005.png)

Even though back in the day, threads were a GREAT way to apply concurrency to our applications (vs potentiall running a single application with various processes)...with Go, Threads are again a bit expensive, and therefore we need to create something better: GOROUTINES

**GO-ROUTINES**

Go Concurrency model DOES use Threads.... But it\'s just that all of the concurrency action in a Go program happens by a lightway construct that gets layered on TOP of threads:

![Machine generated alternative text: goroutine ](000_01_-_The_Core_006.png)

Go routines are NOT schedulled by the OS (because recall that with Threads, the OS is the one in charge of handling the Threads of a process). Go routines are actually schedulled by the Go Runtime.

**Goroutines vs OS Threads:**

- Lighter weight

    - Usually one thread stack size is: 1 MB

    - Go routines are more in the : KB (single digits)

- Go manages goroutines (simpler for programmers)

    - From creating them all the way to tearing them down.

- Less switching

    - Thread switching is expensive, and so it is when it comes to GoRoutines, but with GoRoutines we just get Less of them

- Faster start-up times.

- Safe Communication

    - SideNote: Thanks to Channels, GoRoutines can easily and safely communicate with one another.

Summary: GoRoutines are great way of squeezing the MOST out of a number of small threads... And this is achieved by getting a number of GoRoutines to run under the same thread...

**Golang\'s Concurrency Mode:** Actor model: Model implementation of Communicating Sequential Processes (CSP)...

Actors (GoRoutines) safely pass messages between eachothers by using channels.

Channels (Simple) are like pipes:

![Machine generated alternative text: goroutine Channel (safe comms) goroutine ](000_01_-_The_Core_007.png)

>

**IMPORTANT NOTE FORGOTTEN:**

Placing a OpenAndClose Paranthesis after closing the braquet of a function will make that funcion **Self-Executing**.

Example:

_func () {_

_fmt.Println(\"Hello\")_

_} ()_

**Concurrency Again:**

For a function, the only thing we need to create concurrency is add \"go\" in front of the function. This will turn each function into a Go_Routine

Even though our Main function is NOT technically a GO routine.... In Go, when the main function exists, the whole program is done....no matter who is done and who is not...so for this case we have to be careful.

When creating channels for our Go_Routines we can do so simply by using the built in **make** function....

An un-buffered channel is a channel we create using the **make** keyboard BUT we don\'t specify a size or number of buffers for the channel:

**_myChannel := make(chan int)_**

The important thing about un-boffered channels is that when a Go_Routine wants to share some data through such channel, it will wait (locK) until another go_routine grabs such data... Forcing some kind of Synchronous criteria:

![Machine generated alternative text: myChanne1 c, Channel (un-buffered) - make(chan int) ](000_01_-_The_Core_008.png)

A **buffered** channel works differently... It is still created using the **chan and make** keywords BUT it needs a SIZE and a number of Buffers...

**_myChannel := make (chan int, 5)_**

When a Go_Routine wants to drop off some information on this BUFFERED channel...as long as the channel is not full..... It will drop off the data and it will not lock..... On the other hand, if the channel IS full, then our Go_Routine will wait until it gets some space (Lock) and then proceed to enter the data...

For **BOTH** cases, if a Go_Routine tries to READ from a Channel (Buffered or Un-Buffered) and there is NO data there, it will automatically LOCK

![Machine generated alternative text: myChanne1 Channel (buffers 5) - make(chan int, ](000_01_-_The_Core_009.png)

![Machine generated alternative text: Summary Concurrency Concurrency = independently executing processes The go keyword go sender(myChan, waitGrp) goroutines O Channels ](000_01_-_The_Core_010.png)
