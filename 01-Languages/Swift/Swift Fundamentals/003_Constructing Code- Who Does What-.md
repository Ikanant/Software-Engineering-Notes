Constructing Code: Who Does What?

Monday, May 9, 2022

6:22 PM

 

Methods of a class and functions in Swift are pretty much the same thing. The syntax is EXACTLY the same.

 

**Func** is the keyword to remember.

 

![func helloWor1d (name: String) { print(\"He110 Indeed helloWor1d(name: \"Jon\") ](003_Constructing_Code-_Who_Does_What-_000.png){width="4.716666666666667in" height="1.8in"}

 

Also, notice how each time I call a function, I ALWAYS need to include the argument label. Just passing in the string \"Jon\" (which would work on any other language) ... would NOT work on swift.

 

![Calling Functions // C-style function call showMessage(123) ; // Swift style function call showMessage(number: 123) argument label // Swift style function showMessage(number: 123 , call with three arguments largeFont: true) name: \"Grace\" , ](003_Constructing_Code-_Who_Does_What-_001.png){width="5.0in" height="2.5083333333333333in"}

 

 

![Function parameters are constants, and immutable by default. ](003_Constructing_Code-_Who_Does_What-_002.png){width="5.0in" height="1.7083333333333333in"}

 

I CANNOT change the value of the input arguments in my swift functions

 

**Returning Values**

 

Simple. We will just use the return arrow... the Format is as follows:\
 

**(parameters) -\> return-type**

 

![Functions Without Return Values func simpleFunction(number: Int) -s Void { // code ](003_Constructing_Code-_Who_Does_What-_003.png){width="5.0in" height="2.183333333333333in"}

 

One interesting thing to note is that Void (notice how we capitalize it since it\'s treated as a type, same as Int or String)... is different than nil... nil is ONLY used for Optionals. Void is simpler... There is no MAY or MAY NOT have a value... it\'s that straight forward.

 

**Function Types**

 

![Swift Function Type (parameter \_ type) return\_ type (String) example functions playMP3 ( filename : playOGG( : showlmage(at url: loadVector(\_ url: Bool q) ](003_Constructing_Code-_Who_Does_What-_004.png){width="5.0in" height="3.1166666666666667in"}

 

Function types essentially are just defined as the string above... Input parameters in Parenthesis, followed by return arrow followed by return type.

![Functions Without Return Values func verySimp1eFunction() { // code goes here Has the Function Type: o Void \"a function that takes no parameters and returns nothing\" ](003_Constructing_Code-_Who_Does_What-_005.png){width="5.0in" height="3.341666666666667in"}

 

 

**Correctly Ignoring Return Values**

 

Writing a function without doing anything with it in the playground is fine... even in a proper application is also fine BUT Xcode will create a warning and there is a cleaner way.

 

Just use the \_ character. That\'s the way to ignore a return value.

 

Also, for the function signature, I can make sure to include the label for the input argument to my function. Which might make things cleaner in the long run. Once I add a label to the argument, then I cannot use the variable name that\'s defined for me.

 

![func showMessage(number: Defining and Calling Functions nickname: \"Grace\") Int, name: String) { name // later. showMessage(nX . 123, ](003_Constructing_Code-_Who_Does_What-_006.png){width="5.0in" height="2.5166666666666666in"}

 

![Naming Functions // in JavaScript typeof someVariab1e // in C# typeof( someVariab1e) // in Swift type (of: someVariab1e) ](003_Constructing_Code-_Who_Does_What-_007.png){width="5.0in" height="2.5166666666666666in"}

 

![// could be written as a choice of strideThrough(E3, 256, 16) // or strideT0(e, 256, 16) // in Swift stride(from : // or stride(from: e, e, through • . 256, by: by: 16) to: 256, 16) ](003_Constructing_Code-_Who_Does_What-_008.png){width="5.0in" height="2.816666666666667in"}

 

 

The only thing to note here is that since Swift forces you to always call your functions providing the right input label on... it is common then to not see functions be super explicit with their names. Why bother, have a show(name: \"Jon\") easily reads as showName.
