02 - Data Types and Operations & Branching and Looping

Friday, April 29, 2016

12:15 PM

 

**Data Types and Operations**

**Primitive Data Types:**

While we will get the regular String and Integers soon, we will get some new stuff that will be interested.

*func main() {*

*     var myInt int*

*     VARIABLE - NAME -DATATYPE*

     *var myFloat32 float32 = 42.*

*     Notice we have to specify the size of floats (32) but we didn\'t with an INT/ There are INT 32s and 64s but it is generally advised to stick with the standard. The other way around though, with floats there are not standards to choose between 32 and 64 bit sizes. A PERIOD at the end will explicitly tell GO that this is a FLOATING point number. Even though this isn\'t necessary, it is a good habit to get into since GO will sometimes refuse to implicitly convert between types for us. That means that adding a INT to a FLOAT won\'t work without help.*

*     myString := "Hello Go\"*

*     The COLON in front of the EQUAL sign will tell GO that we want to use the short variable declaration syntax. The GO compiler looks at the assign value and infers the type from that value. In this case the compile determines the compiler is a String type and offers it that type*

*     myComplex := complex(2,3)*

*     Having complex primitive datatypes is a great tool for any fancy mathematic operations, the first element inside the complex function determines the real number, while the second one will determine the complex one... complex(a,b) is the same as: a + bi.*

*     real(myComplex)*

*     imaginary(myComplex)*

*     Will retrieve the values accordingly*

**Constants**

Constants have some tricks that makes them more powerful than other constants in other languages.

*const (*

*     first = "first\"*

*     second = "second\"*

*     third = "third\"*

*)*

This way the output of these methods will be the same as usual. BUT, with GO we have a especial keyword that works in the context of a CONST block called iota

const (

     first = iota

     second

     third

)

In any regular programming language, this would mean a problem because we have constant values that aren\'t assign to anything. But surprise! if we print this functions in order we ould get: 0 1 2

iota: [Gives us an Auto Incremental Number]{.underline} that we can use to determine the values of our integers. We can use this as a basic type of enumeration.

How about if we have two consts blocks that are both using IOTA? 

**NOTE:** We can declare multiple const blocks.

The vale of iota will reset to zero in the following case:

**NOTE2:** If we write a constant (let\'s say a String) in the const block where the iota function is utilized, then we will get that variable to get the value we just assigned. If we then create any other const value after that, it will automatically get the value of the constant we just created:

package main

const(

    one = iota

    two

    three = \"Hello\"

    four = 5

    five

)

func main(){

    println(one)

    println(two)

    println(three)

    println(four)

    println(five)

}

will result in:

0

1

Hello

5

5

**Constant Expression:**

We can do some pretty cool things to determine the value of a constant to determine it\'s content, with the only requirement being: that it has to be able to be resolve at Compile time... So, no functions need to be involved.

package main

const(

    one = 1 \<\< (2 \* iota)

    two

    three

)

func main(){

    println(one)

    println(two)

    println(three)

    print("Result: \",(1\<\<2))

}

1

4

16

Result: 4

**Collections**

In many languages, when we deal with Collections, we often thing of the language standard library and getting some kind of list, map or dictionary. These data structures are so common that the designers of GO decided that it made sense to build this basic structures directly into the language:

*myArray := \[3\]int{}*

We declare an array by starting with the Array size and later the data type.

Printing Array elements are a bit too complicated for the plain println function so we need to use "fmt" for it. We are talking about doing something cool like:

fmt.Println(myArray)

This will print the whole array accordingly.

**NOTE:** We can actually include the values for the array inside the { }.... The cool thing is that we do not need to specify the size of the array when creating it....we can simply do a:

myArray += \[*...*\] int { 4, 1, 6, 2, 3}

*And Go will know how big the array will be no problem.*

If we want to know the size of the array, we can simply use the *len* function\...

fmt.Println(len(myArray))

We can use the len function in many more data structures\...

Arrays are no often use in GO....instead a more FLEXIBLE datatype is used called: Slice

Slice: A Slice represent a subset of an Array. The trick about a slice is that GO will take care of the underlying array. So we can just insert and remove elements of the slice and Go will take care of the Array manipulation

*mySlice := myArray\[:\]*

Notice that the \[ : \] format means that we will be taking everything from the Array to the Slice. The proper format is more like := \[ a : b \] which a is inclusive while b is not.

example:

mySlice += myArray\[0:5\]

Means that my Slice will take elements from position 0 (including 0) to position 4 (not including 5)

The Slice data structure has many methods like "len" that can help us use our data. For example we can append stuff using:

*mySlice = append(mySlice, 100)*

When dealing with Slices, we do not need to worry about the underlying array. We can initialize a Slice really easily by:

mySlice := \[\]int {1, 2, 3}

We do not need to specify the size, or even the three dots we used with the Array. Leaving them out means we have a slice. Something important to consider is that the underlying array is always the right size. While this works well in lots of scenarios, this might actually be a problem with Slices that require lots of adding and removing of data.

To get around this, we can just create a large original Array by using the built in MAKE function:

Which takes 2 or 3 arguments:

mySlice := make(\[\]float32, 100)

In this case we are creating a slice with the size specified. In this case the Slice and the underlined Array are the same length.

If however, we want a small slice to start with a large capacity then we can pass a 3rd value into our make function

[MAPS]{.underline}

Similar to any other programming language, the map will allow to store data to then be accessed by customizable keys.

myMap := make(map\[int\]string)

In this case we have created a map that holds string values organized by a set of int keys

 

**Arithmetic Operations**

println(intVar++) is NOT Allowed

Everything else is the same\...

**Putting it Together: Variables and Operations**

Atom Work

 

![](001_02_-_Data_Types_and_Operations_&_Branching_and_Looping_000.png){width="2.5416666666666665in" height="3.125in"}
