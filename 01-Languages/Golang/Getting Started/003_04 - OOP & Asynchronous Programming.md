04 - OOP & Asynchronous Programming

Friday, April 29, 2016

12:16 PM

 

**[Structs and Fields]{.underline}**

For most people, this topic will be somewhat related to Classes... but instead we will explain how Go has a different take on Object Orientation than those languages. It uses the term: STRUCT to represent the same more or less concept than classes do in other languages.

*[Keep in mind though:]{.underline}* Structs are not another name for classes. They are different things.

**func main() {**

**    foo := myStruct{}**

**    foo.name = \"John\"**

**    fmt.Println(\"Hello\", foo.name)**

**}**

**type myStruct struct{**

**    name string**

**}**

We can also just assign the values to fields when initializing the object, but we need to be careful. We need to assign values of the fields *[In the same order they are declared in the struct.]{.underline}* 

**foo := myStruct{"John"}**

When declaring an object like we did on the above code we create an object in the **local execution stack...** while this is not as big of a deal in GO as it is in other languages, it is often better to create objects on the HEAP instead. For these cases we will not be able to assign values to the object parameters upon the objects declaration

**foo := new(myStruct)**

**foo.name = "John\"**

In this case, foo is already a memory address. We might have expected us to dereference the object in order to work with it. IT turns out that the creators of GO already took care of that for us. This feature will make it more pleasant to work with reference datatypes.

**foo := new(myStruct)**

**fmt.Println(foo)**

*[&{John}]{.underline}*

**foo := myStruct{"John\"}**

**fmt.Println(foo)**

*[{John}]{.underline}*

**foo := &myStruct{"John\"}**

**fmt.Println(foo)**

*[&{John}]{.underline}*

This is a way to create an object in the HEAP a simpler way

 

 

**[Constructor Functions]{.underline}**

In many object oriented languages, methods are created inside of the class definition. Often there is a special type of method Constructor that allows the object to be set up while is being created so that the user of the object don\'t have to worry about initializing variables, etc... GO does NOT use any methods like this and; therefore, does not have the concept of a constructor. Instead, plain old functions are tapped to work as constructors. These so called constructor functions are not special in any way but they are a common pattern in GO.

**func main() {**

**    foo := new(myStruct)**

**    foo.myMap\[\"bar\"\] = \"closed\"**

**    fmt.Println(foo)**

**}**

**type myStruct struct{**

**    myMap map\[string\]string**

**}**

If we take a look at the above code, we would get an error. We try to work with an object inside our myStruct struct that has not been initialized. So, what to do ?

*[We are going to create a function whose only purpose is to create a properly initialized object and return it to the caller.]{.underline}* Functions that have this responsibility are called **[Responsive Functions]{.underline}** in GO.

By convention, the name of Responsive Functions are called ***new+\[nameOfStruct\]***

The return type could be a Struct, or a pointer to a struct. *[Normally, the author returns a pointer since that is generally the better way to create objects that are going to have a non-trivial live span.]{.underline}*

**func main() {**

**    foo := newMyStruct()**

**    foo.myMap\[\"bar\"\] = \"closed\"**

**    fmt.Println(foo)**

**}**

**type myStruct struct{**

**    myMap map\[string\]string**

**}**

**func newMyStruct() \*myStruct{**

**    result := myStruct{}**

**    result.myMap = map\[string\]string{}**

**    return &result**

**}**

 

**[Methods]{.underline}**

So far, the only thing that we can do with objects is store data in them. It also often helpful to create methods that execute in the context of an object.

//\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

//\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

**func main() {**

**    mp := messagePrinter{\"hello\"}**

**    mp.printMessage()**

**}**

**type messagePrinter struct{**

**    message string**

**}**

**func (mp \*messagePrinter) printMessage() {**

**    println(mp.message)**

**}**

//\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

//\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

That new element between func and the function name is what determines the context of the function turning it into a method

While this syntax can be a little odd, there are several advantages:

1.  The data in the struct is clearly separated from the methods

2.  New methods to the struct can be added from anywhere in the package

**[Object Composition]{.underline}**

One of the main topics when discussing Object Oriented Programming is Inheritance. While this is a power concept, it is easy to abuse. THe designers of GO decided that it should not follow this pattern and used instead a different technique to share functionality.

COMPOSITION:

Instead of a CLASS (or SRTUCT) inheriting a child sort of relationship, GO allows sort STRUCTS to be included inside of the STRUCT that wants to take advantage of the functionality of the first STRUCT.

**func main() {**

**    emp := enhancedMessagePrinter{}**

**    emp.message = \"foo\"**

**    emp.printMessage()**

**}**

**type messagePrinter struct{**

**    message string**

**}**

**func (mp \*messagePrinter) printMessage() {**

**    fmt.Println(mp.message)**

**}**

**type enhancedMessagePrinter struct {**

**    messagePrinter**

**}**

 

**[Asynchronous Programming]{.underline}**

How to call functions asynchronously using tools that GO offers us.

**goroutines** = Are the name given to GO\'s thread like constructs

**channels** = Channels are designed to address on of the most difficult challenges of this type of program. Sharing DATA between threads. We pretty much use channels to set the bridge for the gaps between goroutines.

*[Concurrency is NOT the same as Parallelism.]{.underline}*

![](003_04_-_OOP_&_Asynchronous_Programming_000.png)

 

 

**Channels are a construct in GO that allow messages to be passed between TWO goroutines in a matter that insures that the data is safely transferred between them. That means that only one goroutine at a time owns the messages content and is able to work with it.**

We will work with two things about channels:

1.  Sending a receiving messages

2.  Ranging over channels** **

**[PLEASE LOOK OVER DEMO CODE]{.underline}**

![](003_04_-_OOP_&_Asynchronous_Programming_001.png)

THE END
