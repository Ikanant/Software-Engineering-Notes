What Your Data Means

Saturday, February 19, 2022

10:40 AM

 

As I mentioned on my previous note, we declare variables in swift using the simple **var** keyboard. This is fine for whenever I create a variable with a value BUT, if I don\'t, then we NEED to provide the type of the variable we are working with.

 

![6 va 7 va 8 va va bonusScore: Int environmentName: String levelCompleted: Bool progressPercentage: Double ](001_What_Your_Data_Means_000.png){width="5.0in" height="1.625in"}

 

In swift the convention is for our variables to be in a lower case letter WHILE the variable type start with an UPPER case letter. Doing this is called **Type Annotation**

 

These are some of the types we will be working with:\
 

![var myVariab1e • Int St ring Double Float Bool Ulnt Collection Types Character Array Dictionary Set ](001_What_Your_Data_Means_001.png){width="5.0in" height="1.425in"}

What about other types like **Date, File, URL, Button, Image**? Well, for those we will just import them from additional frameworks.

 

**Constants, Why are they important?**

In swift, if we want to create a constant we use the keyword **let.**

![var to make a variable myVariab1eMessage = \"Hello\" var // later, try to change it myVariab1eMessage Bye \" let to make a constant // OK let myConstantMessage = \"Hello\" // later, try to change it \" Bye \' myConstantMessage = // ERROR! ](001_What_Your_Data_Means_002.png){width="5.0in" height="3.3333333333333335in"}

 

*Why bother going over this though? How is it different than any other language?* Well, Swift really wants people to use const... to the point that in Xcode, if we define a variable that doesn\'t change, it will throw a warning. Using constants is known across any language as a way to write safer code.

 

One important thing to remember is that for either vars or lets, we cannot use them before having them be initialized. There is no default value that gets applied if we don\'t specify one.

 

**Operators**

Mostly the same BUT some new ones not found in any other language

-   We DO NOT have ++ and \-- operators in swift

-   New ones to keep track on:

    -   ??

        -   Nil coalescing operator

    -   ...

        -   Closed range operator

    -   ..\<

        -   Half-open range operator

    -   -\>

        -   Return arrow

    -   !

        -   Force unwrap

    -   ?

        -   Optionals

 

**Converting in Swift**

There is a way to figure out the type of a variable in swift... in our case it would be:\
\> *type(of: myVariable)*

 

![2 let a = 5 3 let b = 2 5 let myResuIt = a / b type (of: mvResu1t) 81 5 2 2 Int.Type ](001_What_Your_Data_Means_003.png){width="5.0in" height="1.0083333333333333in"}

\^\^\^ So here we run into a problem because Swift is wrongfully assuming the result will be of type Int.

![let 3 let myResuIt: Double type (of: myResu1t) Int -Type 81 ](001_What_Your_Data_Means_004.png){width="5.0in" height="1.05in"}

\^\^\^ I might be tempted to do this, but it will actually create a compilation error. This is happening because in Swift we DO NOT have implicit conversion between types.

 

In other languages this is actually common. It is called Coercion:\
 

![// make an integer variable int mylnteger = 40 // make a floating-point variable double myDoub1e = 2.5; // now add them together Console. WriteL ine(mylnteger myDoub1e); Some Implicit Conversion (Coercion) is Common Many languages perform some automatic \"behind the scenes\" conversion ](001_What_Your_Data_Means_005.png){width="5.0in" height="2.2916666666666665in"}

Making a converstion is pretty straight forward. All we need to do is tell swift the type of variable we plan to convert too and pass in our variable inside the parenthesis.

![// make a Float from an Int let myF10at = Float(somelnteger) // make a String from a Float let myString = String(myF10at) // make a Double from a String let myDoub1e = Double(myString) // make an Int from a Float = Int(myF10at) let mylnt Basic Conversion Syntax ](001_What_Your_Data_Means_006.png){width="5.0in" height="3.783333333333333in"}

This is not all of it though, because there are conversions that might not be supported. For instance converting a float into a Boolean we are still not guaranteed to get a value once we do a conversion.

 

**Optionals - An Introduction**

 

Optionals are the way SWIFT allows us to define type-safe values when there might NOT be any value at all.\
 

![// Traveler information var var var var var var firstName: String middleName: String lastName: String email: String secondaryEmai1: String daysUnti1NextTrip: Int \"Grace\" \"Murray\" so the next trip is today? or\... we haven\'t calculated it yet? or\... there is no next trip? ](001_What_Your_Data_Means_007.png){width="5.0in" height="1.925in"}

 

In SWIFT, variables are NOT initialized with values if nothing is explicitly provided by the developer.

 

OPTIONALS are the only type that might be **nil.** Essentially, a variable that has not been initialized will NOT have a value but it will still not be nill... it is just not initialized.... An optional that has not been initialized WILL be nil.

 

Trying to print/use a non-conditional variable in a program WILL result in an error.

![Int 100 unwrapping an optional not nil (there is a value) my0ptiona1 ](001_What_Your_Data_Means_008.png){width="5.0in" height="2.4166666666666665in"}

 

This is trivial stuff. We check if the conditional is null or not and then we proceed... ONE important thing to note is that I can use the EXCLAMATION mark to **force unwrap** the value out of my variable... so:\
 

 

**Force Unrwap**

![10 13 14 15 16 check for nil // this is \"forced unwrapping\" var unwrappedlnt = optional Int! ](001_What_Your_Data_Means_009.png){width="5.0in" height="1.725in"}

 

 

Forcing to unwrap an option that is **nil** will cause a **RUN TIME ERROR**

 

**Optional Binding**

![1 // this is \"optional binding\" if let unwrappedlnt = optional Int { print ( unwrappedlnt ) else { // there\'s no value\... ](001_What_Your_Data_Means_010.png){width="5.0in" height="1.575in"}

This IF LET syntax is a little weird, but it always just tells us that we are dealing with an optionalx

 

 

**Creating and Using Arrays**

 

Keep in mind we have three basic collection types in SWIFT

![o 2 \" Ionian \" \" Do rian \" \" Ph rygian\' Array an ordered collection of items Swift Collections \"United Parcel \" UPS \" Service\' \" FedEx \" \"Federal Express\" \'United States \" USPS \" Postal Service\" Dictionary a collection of key/value pairs \" Item \" \"Third item\" \"Second item\' Set an unordered collection of items ](001_What_Your_Data_Means_011.png){width="5.0in" height="2.408333333333333in"}

 

I think I mentioned this earlier... but of course there are other data structures available beyond these three. We can ALWAYS import those... but these three are part of the syntax of swift. They are built into the language.

 

Remember that swift is a C style language... like C our arrays are 0 based... meaning the index of the first item in the array is always 0.
