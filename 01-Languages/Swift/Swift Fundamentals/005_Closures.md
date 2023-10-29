Closures

Tuesday, May 10, 2022

11:01 PM

 

![Examples of Closure Use General Sorting, Filtering, Working with Collections Area-specific Animation, Fetching Data, Callbacks, Completion Handlers Task-specific Working with User Interface Controls ](005_Closures_000.png)

 

What is a closure in swift?

Simple, a closure let\'s us take a few lines of code in swift and group it together so we can use it later in the code. But, isn\'t hat what a function is?\... Yes, and technically functions are a TYPE of closure...

 

Now the difference is:\
 

![Functions // define it func myFunction() { // one or more lines of code // call it myFunction() ](005_Closures_001.png)

 

![Closures // one or more lines of code ](005_Closures_002.png)

 

![Functions vs Closures Function a block of code you intend to call Closure a block of code you intend to pass ](005_Closures_003.png)

 

![Passing Arguments // Call a function that takes an Int myFunction( 93278) // Call a function that takes an String myFunction( I\' Hello // Call a function that takes a Closure myFunction( print (\"This is inside a closure\") // more code. ](005_Closures_004.png)

 

 

**Function are blocks of code you CALL, Closures are blocks of code you want to PASS**

 

The concept here is what I already know as:

-   Blocks

-   Lamdas

-   Function Literals

-   Anonymous Functions

There are not 100% the same, but are very similar.

 

![func contain (where: (Element) ---\> Boo 1) ---\> Bool Returns a Boolean value indicating whether t sequence contains an element that satisfies the given predicate. ](005_Closures_005.png)

 

![Swift Function Type parameter types) return type (String) --- \> BOOI \"a block of code that takes a String and returns a Bool\" (Int) String \"a block of code that takes an Int and returns a String\" \[String\] (Double, Double) \"a block of code that takes two Doubles and returns an Array of Strings\" ](005_Closures_006.png)

 

So in the case I want to sort an array of objects:

![// are these two Book elements in the right order already? if secondBook. readingAge { firstBook. readingAge return true } else { false return ](005_Closures_007.png)

 

BTW I really enjoyed going over the HELP \> DEVELOPER DOCUMENTATION in XCode
