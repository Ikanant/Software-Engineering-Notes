03 - Branching and Looping & Functions

Friday, April 29, 2016

12:15 PM

 

**[Branches]{.underline}**

*IF statements:*

Regular stuff... When dealing with IF statements we have some minor rules to follow differently:

1.  We do not need to have a parenthesis for the if statement:\
    if foo == 1 {\
    }

2.  We need to have the curly bracket right next to the if statement. This is MANDATORY

With GO, we can insert the variable initialization right inside the IF statement:

     if foo:=2; foo == 1 {

*Just because we can do this, doesn\'t mean we actually should. However, if the result of the initialization is needed later on in the code, we will run into problem\...*

*SWITCH statements:*

It comes in two forms:

1.  Regular:

***    test := 1***

***    switch test{***

***        case 1:***

***            fmt.Println(\"Hello\")***

***        case 2:***

***            fmt.Println(\"World\")***

***    }***

2.  Fancy:

***    test := 3***

***    switch{***

***        case test == 3:***

***            fmt.Println(\"Hello\")***

***        case test \> 2:***

***            fmt.Println(\"World\")***

***    }***

 

*LOOPS:*

FOR loop is the same as usual without parenthesis

WHILE loops will take the form of:

**    *foo := 0***

***    for {***

***        foo++***

***        fmt.Print(foo)***

***        if foo==10 {***

***            break***

***        }***

***    }***

Let\'s say we want to loop through the content of a Slice:

*   *

***    mySlice := \[\]string{\"one\", \"two\", \"three\"}***

***    for indx, val:= range (mySlice){***

***        fmt.Println(indx, \"=\", val)***

***    }***

How about a map situation?

***    myMap := make(map\[int\]string)***

***    myMap\[0\] = \"Hello\"***

***    myMap\[1\] = \"World\"***

***    for k, v := range myMap {***

***        fmt.Println(k, \" and \", v)***

***    }***

 

 

**[FUNCTIONS]{.underline}**

**[Functions and Parameters]{.underline}**

1.  Passing by Value

    -   Allow us to send a copy of a variable\'s value into the function and protect it form getting it changed

2.  Passing by Reference

    -   Allows the function to manipulate the data of the variable being sent

```{=html}
<!-- -->
```
1.  Variadic Functions

    -   This is a special type of parameter that will turn the function into a variadic function

    -   [Variadic function:]{.underline} A function that can take in an arbitrary long list of arguments

Everything is more or less the same for creating functions with various parameters and all. Similar to C with dealing with pointers.

 

***func main() {***

***    text := \"Hello\"***

***    saySomething(&text)***

***    fmt.Println(text)    ***

***}***

***func saySomething(message \*string){***

***    fmt.Println(\*message)***

***    \*message = \"World\"***

***}***

 

[Variadic Functions:]{.underline}

Similar to the code shown above, we just need to replace the asterisc before the string type and replace it with three dots (. . .)

Doing this, Go will take all the parameters going into the function and treat them as a slice of strings.

***func main() {***

***    saySomething(1, \"test\", \"Hello\", \"There\", \"You\")***

***}***

***func saySomething(num int, test string, messages \...string){***

***    fmt.Println(num)***

***    fmt.Println(test)***

***    fmt.Println(messages)***

***}***

 

[Return Values]{.underline}

Similar to most languages, GO lets us return data from our functions. We have several options though:

1.  Return a SINGLE value (common in most languages)

2.  Return MULTIPLE values

    -   Often used to return a value and a flag indicating the function was successful or not

3.  Named Return Parameters

    -   Technique that when properly used can be the function more readable

***func main() {***

***    fmt.Println(add(1,2,3))***

***}***

***func add(terms \...int) int {***

***    result := 0***

***    for \_, val := range terms{***

***        result += val***

***    }***

***    return result***

***}***

Let\'s now try returning multiple results:

***func main() {***

***    numTerms, sum := add(3,2,3)***

***    fmt.Println(\"Added:\", numTerms, \" terms for a total of\", sum)***

***}***

***func add(terms \...int) (int, int){***

***    result := 0***

***    for \_, val := range terms{***

***        result += val***

***    }***

***    return len(terms), result***

***}***

Now, lets try to give names to our return values: For that we just need to place their name values in front of the type in the function signature\...

***func add(terms \...int) (numTerms int, sum int){***

By doing this we could then remove the variables we created within our function and just use the name of our return types accordingly. By naming our return values we can then remove the variable names from our return line...

***func main() {***

***    numTerms, sum := add(3,2,3)***

***    fmt.Println(\"Added:\", numTerms, \" terms for a total of\", sum)***

***}***

***func add(terms \...int) (numOfTerms int, result int){***

***    for \_, val := range terms{***

***        result += val***

***    }***

***    numOfTerms = len(terms)***

***    return // \<\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--***

***}***

 

 

[Anonymous Functions]{.underline}

GO support functions as first class citizens of the language...this means that they can be assigned to variables and passed around the application without needing to be wrapped with some sort of container like a class... This opens up a lot of functionaloties...

 

***func main() {***

***    addFunc := func(terms \...int) (numOfTerms int, result int) {***

***        for \_, term := range terms {***

***            result += term***

***        }***

***        numOfTerms = len(terms)***

***        return***

***    }***

***    numTerms, sum := addFunc(1,2,3)***

***    fmt.Println(\"Added:\", numTerms, \" terms for a total of\", sum)***

***}***

 

 

 

![](002_03_-_Branching_and_Looping_&_Functions_000.png){width="4.158333333333333in" height="2.225in"}
