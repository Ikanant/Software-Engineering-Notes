Protocols

Wednesday, May 11, 2022

8:00 PM

 

Protocols are the way that Swift allows me to formalize what a class/struct/enum should do. Doing so without worrying about inheritance. Part of the reason why I won\'t be seeing a lot of inheritance in Swift, is because of these protocols.

 

LOL Apple calls. Swift a Protocol-Oriented Programming Language

 

![Swift Is a Protocol-Oriented Programming Language ](007_Protocols_000.png){width="5.0in" height="2.75in"}

 

Simple put (NOT SWIFT RELATED)\
**Protocol:** The official procedure or system of rules governing affairs of state or diplomatic occasions: protocol forbids the prince from making any public statement in his defense.

 

A PROTOCOL in Swift is a SIMPLE list of methods or properties than a class/struct/enum is supposed to have.

 

![General Purpose Creating Collections, Comparing Instances, Converting, Sorting, Debugging App-specific Loading Data, Saving Data, Spellchecking, Resizing UIs ](007_Protocols_001.png){width="5.0in" height="2.0416666666666665in"}

 

I can consume protocols the exact same way I inherit classes... though remember I can only inherit one class... I can use multiple protocols.

 

To me, protocols seem to be pretty much good old interfaces. It contains no implementation or code... just tells me I need something...

 

![class MyNewC1ass: SomeSuperC1ass , SomeP rotocol OtherProtoc01 Inheritance and/or Protocol Adoption Swift classes allow single class inheritance Swift classes, structs and enums allow multiple protocols ](007_Protocols_002.png){width="5.0in" height="1.7in"}

 

![1 class player: CustomStr ngConvert le // stored properties protocpVCustomStringConverti\>G var name: String var livesRemaining: Int var enemiesDestroyed: Int penalty: Int var var bonus: Int // computed property var score: Int { return (enemiesDestroyed \* 100) + bonus + (livesRemaining \* 5eøø) --- init (name: String) { self. name name self .1ivesRemaining 3 self. enemiesoestroyed = self .penalty e self = penalty ](007_Protocols_003.png){width="5.0in" height="1.95in"}

 

![1 class Player: Customstringconvertible // stored properties var var var var var var name: String livesRemaining: Int enemiesDestroyed: Int penalty: Int bonus: Int description: String = \"test\" ](007_Protocols_004.png){width="5.0in" height="2.316666666666667in"}

 

And same as inheritance, the protocol does NOT care if I did something meaningful with my property... it just expects it to be there.

 

**Writing my own protocol!**

 

Typically this is what other trainings focus on, but it is important to understand before writing it out... which is super easy... just use the keyword: **protocol**

 

![Il 14 16 protocol myCooIProtocoI { // EVERYTHING that adopts this protocol NEEDS to provide a method that takes no parameters and return nothing: func // When it comes to properties they are a bit different than methods // Protocol just says we need a property Of THIS NAME and THIS that\'s it TYPE\... // Well, sort Of\... we also NEED the curly braces to set the specifiers! --- Not for behavior.. but just to mention either GET or GET/SET\... so we define if this is a ReadOnIy or Writable property var name: String { get set class banana: myC001ProtocoI func showNessages() print (\"Banana\") name: String = \"Hello\" ](007_Protocols_005.png){width="5.0in" height="3.375in"}

 

**Adopt / Conform**

 

These are almost the same... but it\'s important to define..

Adopt: When we just add the colon, protocol to our class. We are telling Swift what we are going to do... but NOT do it yet...

Conform: Is when we actually implement whatever the protocol required us to do.

 

 

**ERROR HANDLING IN SWIFT**

Dealing with recoverable errors.

 

![Three Parts to Error Handling 1. Define it What is it? Connection error? Save error? Calculation error? 2. Throw it Where and when can it happen? 3. Handle it What are you going to do about it? ](007_Protocols_006.png){width="5.0in" height="2.2583333333333333in"}

 

 

For many programing languages there are standard error classes defined for us... in Swift this is NOT the case. Errors are whatever we want them to be.

 

![SomeKindOfError { struct // whatever you need. Swift Errors Can be created from any type ](007_Protocols_007.png){width="5.0in" height="3.033333333333333in"}

 

Errors can be **classes/structs/enums** ... easy... enums are actually a great way to definer errors

 

![1 // Define 2 enum ServerError { case noConnection case serverNotFound case authenticationRefused ](007_Protocols_008.png){width="4.466666666666667in" height="1.4083333333333334in"}

 

 

Now, so that we can tap into the Swift error handling system, there is something we can do... adopt the Error protocol

 

![// Define enum ServerError: Error { case noConnection case serverNotFound case authenticationRefused ](007_Protocols_009.png){width="4.908333333333333in" height="1.8416666666666666in"}

 

This guy is weird BECAUSE it does NOT require us to implement anything. Because I adopt it I can now **throw** it... which is great...

 

***If a function MIGHT throw an error... we NEED to add the word throw to the function signature.. After the input parameters and BEFORE the arrow.***

 

![9 func checkStatus(serverNumber: Int) throws switch serverNumber { case 1: print(\"You have no connection.\" ) throw ServerError.noConnection case 2: print(\"Authentication failed. ---s String { throw ServerError. authenticationRefused case 3: print(\"Server 3 is up and running!\" ) default: find that server. throw ServerError return \"Success! \" ](007_Protocols_010.png){width="5.0in" height="3.025in"}

 

ANY TIME a throw occurs in swift, it will mean the immediate return from the method. Now though, anywhere in the code I call this method I will have to do something different... because I cannot guarantee I will get something back:\
\
 

![27 // handle itl 028 let result ghecKStatus(serverNunber: 29 print(result) ](007_Protocols_011.png){width="5.0in" height="0.8in"}

 

In order to call this function, I can simply do a DO CATCH statement... (Same as good old try/catch)...

 

![do { let result try checkStatus(serverNumber: print (result) 32 catch { problem is: \\ (error) ](007_Protocols_012.png){width="5.0in" height="1.2166666666666666in"}

 

When something is thrown into the catch, we will automatically have a generic variable called **error**.

 

![29 do { let result = try checkStatus (serverNumber print (result) 32 catch ServerError. noConnection { // no connection print( \"NO connection. Please try later. \" ) 35 catch ServerError. authenticationRefused { // authentication error? print( \"Authentication error. Please check your username and password. n) 38 catch print( \"The problem is: \" ) ](007_Protocols_013.png){width="5.0in" height="1.45in"}

 

NOW, how about if I don\'t care to catch the result... well, I can make my variable just an conditional... like so:\
 

![// Handle it 26 let result: String? 27 do { 29 result = try checkStatus catch { result --- nil ](007_Protocols_014.png){width="5.0in" height="1.6083333333333334in"}

If I do this then I won\'t care and can set the result to nil... but swift has a more concise way to do this:

**Try?**

![// Handle it let result = try? checkStatus(serverNumber: 1) ](007_Protocols_015.png){width="5.0in" height="0.4666666666666667in"}

 

 

**USING GUARD AND DEFER\
** 

These count as CONTROL FLOW statements... similar to our good old IF ELSE stuff.

 

**GUARD:\
**Behaves just like IF ELSE ... but it makes things a bit more legible in a very specific scenario

 

![guard itemsRequested \< itemsInStock else print (\"Cannot fulfil request. return Guard Statement ](007_Protocols_016.png){width="5.0in" height="1.9416666666666667in"}

 

![guard some-condition-i-need-to-be-true else what-we-do-if-it-isn\'t ](007_Protocols_017.png){width="5.0in" height="0.8166666666666667in"}

 

![guard let unwrappedVa1 optional Val return / throw / break / continue else ](007_Protocols_018.png){width="5.0in" height="0.8666666666666667in"}

 

When using a GUARD we always need to be ready to return/exit as soon as the condition is NOT met

 

Common way:

![func updateSearchResu1ts (for searchContr011er; UISearchContr011er) { guard searchContr011er.isActive else { return ](007_Protocols_019.png){width="5.0in" height="0.6583333333333333in"}

 

So, why is this important really? Well, it is super common for me to write IF statements at the beginning of my functions... typically I want to know whether what I got passed in is valid info or not... so you typically have things like this which CAN be done in Swift:\
 

OPTION 1:\
 

![2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 func process Track(trackName: String? , artist: String? , duration: Int? ) { // check to see if we have values. nil I I duration if trackName nil Il artist print( \"Values were not provided! // might even throw an error here. return } else { nil { = (\"\\(trackName!) by \\ (artist!) is \\ (duration! / 60)m \\ (duration! % 60)s\") let message print (message) now, start processing\... ](007_Protocols_020.png){width="5.0in" height="1.4333333333333333in"}

 

OPTION 2:

Pyramid of DOOM... multiple if let statements nested inside one another:\
 

![// check to see if we have values. if A.e..Ly.nyr.@.ppe.d.TxackName = trackName { if = artist { duration { if = i/ now we have ail three\... ](007_Protocols_021.png){width="5.0in" height="1.6583333333333334in"}

 

OPTION 3:

![// check to see if we have values. if let ynyxappedTrackName = trackName, = artist, let let = // now we have } else { print (\"Values were not // might even throw an duration { all three\... provided! \") error here .1 ](007_Protocols_022.png){width="5.0in" height="2.3333333333333335in"}

This is a bit better BUT I would still need to have an ELSE statement to do something... still not ideal...

 

BEST OPTION:

**Guard** just lets us focus to what needs to be true... if it is not, then we bail.

 

So, what does the guard statement do if the condition is true? NOTHING

 

**There is another use though:\
**We have seen this:

![if let unwrappedName print (\"We have the } else { print (\"It was nil. optionalName unwrappedName) ) value \\ ( ](007_Protocols_023.png){width="5.0in" height="1.35in"}

 

Here, even if we DO have a value, it will NO LONGER exist outside of the IF statement. If we do a GUARD LET then the name of what we give the unwrapped version WILL be available once the guard statement is over!

 

![guard guard guard // if let let let unwrapped Track unwrappedArtist unwrappedA1bum else { optional Track optionalArtist else else { optionalA1bum they\' re all unwrapped return } { return } return } we get to this line, print( \" \\ (unwrappedA1bum) unwrappedA1bum) ) unwrappedArtist Using Optional Binding with Guard ](007_Protocols_024.png){width="5.0in" height="1.7666666666666666in"}

 

This can be even simplified to:\
 

![guard let let let unwrapped Track unwrappedArtist unwrappedA1bum optional Track optionalArtist else { return } optionalA1bum ](007_Protocols_025.png){width="5.0in" height="0.775in"}

 

**Again,** guard does NOT offer anything we couldn\'t do any other way... but it certainly helps for having a very concise syntax.

 

 

 

**DEFER** keyword

This is the same as other languages.... If we always need to do something right before the function is about to exit... like this:\
 

![func processCart (myCart: ShoppingCart) { // open the resource m Cart.o en() // get first one let firstltem = myCart.first() // make sure the first item is active guard firstltem.isActive else { // early return? close the resource first! myCart . close ( ) return // process items for item in myC011ection { let validatedltem = validate(item) myCart . close( ) if // all validatedltem. status == . failure { // close the resource! myCart. close ( ) throw ItemError. reserved items processed? close the resource! ](007_Protocols_026.png){width="5.0in" height="4.608333333333333in"}

 

DEFER takes care of that...

 

![func someFunction() { defer { // your cleanup code // code\... ](007_Protocols_027.png){width="5.0in" height="2.933333333333333in"}

 

The right way to describe it is that this code block will run RIGHT BEFORE the block you\'re in (most likely a function) will fall out of scope

 

![processCart (myCart: ShoppingCart) { func // open the resource m Cart.open() defer myCart . close ( ) // get first one let firstltem = myCart.first() // make sure the first item is active guard firstltem.isActive else { // early return? close the resource first! return // process items for item in myC011ection { let validatedltem = validate(item) if validatedltem.status . failure { throw ItemError.reserved ](007_Protocols_028.png){width="5.0in" height="4.391666666666667in"}

 
