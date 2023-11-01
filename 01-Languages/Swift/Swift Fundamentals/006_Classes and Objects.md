Classes and Objects

Wednesday, May 11, 2022

12:04 AM

IN SWIFT YOU CAN ONLY INHERIT ONE SUPER CLASS

Same as previous notes, I am only going to write what I see \*different in Swift.

Same as Structs if we provide initial values for the properties of the class, Swift will infer the type... if we don\'t we gotta make sure we give it the type... though this is weird because Swift WILL complain if I don\'t provide initial values for the properties of my class...

![1 class Person { var name; String Playground execution failed: expression failed to parse: error: Classes class Person { error: class •person has no initializers ](006_Classes_and_Objects_000.png)

The reason for this is because, when we make an instance of the class Swift will automatically need to set the value for each property... if we have our properties set as conditionals, then we don\'t need to have initializers.

Methods are easy and will work the same as any other OOP language... only note is that we do NOT need to set the **self** variable when using properties in the class. Swift is smart enough to figure that out... it CAN be used though.

![\\ (self. lastName)\") 10 11 12 13 class Person { var firstName: String = \" var lastName: String = func printName() print (\"Hi, my name is: var user = person() user. firstName = \"Jonathan\" user. lastName = \"Snow\" user ](006_Classes_and_Objects_001.png)

Similar to constructors in any other language, if I write **init** in a class, I won\'t even need to use the **func** keyword. Swift will be smart enough to know that\'s just the initializer... which then means I do NOT need to initialize all variables one by one.

![class Person { var firs tName: String var lastName: String init (firstName: String, lastName: String) { self. firstName = firstName self. lastName lastName func printName() { print (\"Hi, my name is: \\(firstName) \\(se1f.1astName)\") var user = person(firstName: \"Jon\", lastName: \"Snow\") 14 user. printName( ) 15 ](006_Classes_and_Objects_002.png)

Swift has the concept of DEINITIALIZERS... what? Apparently they are not super common!

They can be used if an object needs to perform some explicit clean up code.

Swift uses something called ARC (Automatic Reference Counting). This will manage memory for our objects. When we create INSTANCES OF CLASSES that are allocated in memory, ARC is what will determine what IS or IS NOT in use. When it detects an instance, ARC will take care of cleaning things for us... which is WHEN Swift WILL runt he DEINIT method. So, I never call DEINIT myself pretty much.

**TIME TO REVISIT CLASSES vs STRUCTS**

1.  When writing structs, not only I do NOT need to initialize my properties, but also when I create an instance of that struct, Swift will automatically create a init function for me. This is called **memberwise initializer**.

    a.  Classes on the other hand don\'t do this. So I will have to provide my own initializer... or make sure my properties have initial values

2.  Classes support inheritance

    a.  Structs DO NOT

3.  Structs are VALUE TYPES

    a.  Classes are REFERNCE TYPES

    b.  ![Structs (and Enums) Value types Assign it to a new variable or constant? The value is copied. Pass it into a function? The value is copied. Classes Reference types Assign it to a new variable or constant? Not copied - a reference is passed. Pass it into a function? Not copied - a reference is passed. ](006_Classes_and_Objects_003.png)

    c.  UNDESTAND THAT WELL \^\^\^

    d.  ![class PersonC1ass { var firstName: String var lastName: String init (firstName: String, lastName: String) { self. firstName = firstName self.1astName lastName 15 23 24 26 28 30 32 func printName() { print (\"Hi, my name is: \\(firstName) lastName)\" struct PersonStruct { var firstName: String var lastName: String func printName() { print (\"Hi, my name is: \\(firstName) lastName)\" var pl PersonC1ass(firstName: \"Jon\" , lastName: var sl = PersonStruct(firstName: \"Jon\", lastName var p2 = pl p2. firstName \"Peter\" print (pl. firstName ) var s2 = sl s2. firstName = \"Pedro\" print (sl. firstName) ](006_Classes_and_Objects_004.png)

>  

**INHERITANCE\
** 

![2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 // Inheritance class Appliance { var make: String var model: String init() { self.make = \"default\" self .model = \"default\" func printDetai1s() { superclass print( \"Make: \\ (self. make) \\nModeI: \\ (self .model) // define a new class class Toaster: Appliance { subclass ](006_Classes_and_Objects_005.png)

One quick thing to note is the problem of properties if we decide to add more in the sub class... see image bellow:\
![14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 // define a new class class Toaster: Appliance { // new property var slices: Int = d // new method func toast() { now\... var my Toaster = Toaster( ) myToaster.make = \"AcmeCorp\" myToaster.mode1 = \"Carbonizer\" my Toaster. printDetai1s ( ) my Toaster. toast( ) ](006_Classes_and_Objects_006.png)

Here the init() function from the Appliance class will no longer work...so we either have to give it a default value OR create new init function. If we just add **init** to my subclass I will deal with ANOTHER issue... init already exists in the parent class... SO here is where I will need to use **override** method.

Note1: In swift I DO NOT need to add the super.init call from my child class init function... but I CAN.

![2 3 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 // Inheritance class Appliance { var make: String var model: String init() { self.make = \"default\" self .model = \"default\" func printDetai1s() { print( \"Make: \\(self.make) \\nMode1: // definJ a new class class Toaster: Appliance { // new property var slices: Int override init() { self. slices = 2 super. init( \\ (self .model)\") ](006_Classes_and_Objects_007.png)

Note2: If I want to prevent a method from the super class to ever be overriden, then I just need to add the **final** keyword.Î

![2 3 5 6 7 8 // Inheritance class Appliance { var make: String var model: String init() { \"default\" self . make = self .model = \"default\" final Ifunc printDetai1s() { XCSe1EhåkéVAnMode1 : 11 .model)\") ](006_Classes_and_Objects_008.png)

Note3: If I want to prevent my class from being inherited at all... I can just use **final** before the class itself

**Adding Functionality with Extensions**

Simple, and not sure if we have that in any other language that I know? At least I have not used it. We can define extensions as a way to create any extra functionality for any Class/Struct/Enums we are using. The scope of this extensions will be limited though. We can do these with ANYTHING, even strings.

![extension String { func removeSpaces() String { so can use filter function // I can treat strings are arrays of characters. // Filter Will take a closure, and I can do the same as I did on the Closures.swift file above let newStringArray = self. filter return String (newStringArray) var banana: String = \"Hello Banana\" banana = banana. removespaces() Drint(banana) ](006_Classes_and_Objects_009.png)

**Stored Properties vs Computed Properties**

Don\'t have to watch video to know, this is just a variable that returns a mutation of some sort of another variable in the class.

So computed properties are essentially properties with explicit getters and setters

![// computed property var score: Int { get { set { ](006_Classes_and_Objects_010.png)

If I do NOT specify the set function, then I will NOT be able to set the value of this property and Xcode will yell at me.

![15 16 17 18 19 20 21 22 23 set { passed in \\ (newVaIue) but I\'m going to ignore it. init (name: String) { self.name = name self. livesRemaining = 3 self. enemiesDestroyed self. penaltv The final score is: 365128 You passed in g5øøø but I •m going to ignore it. ](006_Classes_and_Objects_011.png)

Funny how even if you set the value, it might not work... BUT do know that the input value for **set** is **newValue.**

IF we only have a GET computed property, then I won\'t even need to be explicit about it... just a code block after the property definition will suffice and Swift will know this is a READ ONLY property

![// computed property var score: Int { return (enemiesDestroyed \* 100) + bonus + (livesRemaining \* 5000) --- penalty ](006_Classes_and_Objects_012.png)

NOW... THESE computed properties are not the same as constants. Swift won\'t even allow me to use **let**.
