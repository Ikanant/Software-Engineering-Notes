Control Flow

Sunday, May 8, 2022

6:49 PM

 

Honestly, I am going to fast forward this module UNLESS I see something different...

 

Oh snap... hitting the ground running:\
 

![Parentheses aren\'t required if ( core \> 1 ) s greater than 101\') else { print (\"It\'s not greater than 10\") ](002_Control_Flow_000.png)

 

No parentheses?! Woah

 

![// If var score --- lee Braces are always required if score \> 10 { (\"It\'s greater than 10\") else { pri (\"It\'s not greater than 10\") ](002_Control_Flow_001.png)

 

Braces are ALWAYS required

 

![if else { print (\' Conditions must be true or false \'It\'s true \" ) false\" ) ](002_Control_Flow_002.png)

 

Always need to be true/false... don\'t assume 0 is false and 1 is true

 

![In Swift, a switch must be exhaustive. ](002_Control_Flow_003.png)

 

![16 17 18 19 20 21 22 23 24 switch apple { case e: print ( \"ZERO\" ) case 1: print( \"ONE\" ) case 123: TWO THREE\") Switch must be exhaustive ](002_Control_Flow_004.png)

 

This is hilarious.... Since the apple variable can be way more than just these three cases, swift will FORCE you to define a default case to cover all the bases for the statement. Cool!

 

It also DOES NOT allow for fall through pattern commonly used in other languages:

![// In many C-style languages switch (levelNumber) { case 1: fallthrough case 2: case 3: pri tf(\"Beginner level\"); break; case 4: fallthrough case 5: case 6: printf(\"lntermediate level\") ; break; case 7: I fallthrough case 8: printf(\"Advanced level\") ; break; ](002_Control_Flow_005.png)

 

Since we do not allow for the fall through pattern, SWIFT does then NOT need to ever have a break keyword at the end of every case. That\'s neat.

 

![// In Swift switch levelNumber { case 1,2,3: print Beginner level\" ) case 4,5,6: ](002_Control_Flow_006.png)

 

AH! I was feeling a bit weird about not being able to cover multiple cases without repeating myself.. Swift technically DOES allow for it to happen, simply using COMMAS.

 

![Swift Ranges case 1\...10 ne t roug ten\') prxnt case print (\"Eleven through twenty\") case 21 : print ( \" Twenty-one \" ) default: print Anything else! \") ](002_Control_Flow_007.png)

 

WOAH WOAH WOAH !!! I can use ranges too! Can I do that in C#? Need to check. Neat

 

So, as stated on the previous page... whenever I see a **...** that\'s called the RANGE OPERATOR. It just means I am dealing with a range of values... For it I only need to know where does the RANGE start and where does the RANGE ends... easy

 

There are TWO range operators! \"**...\"** is the first one

 

LOOPS are the boring same:\
 

![paren4keses op4•tonAl Creating Loops // Swift-style \"while\" while itemsToProcess \> 0 Il a function make a constant print a message call another function braces vee•tred ](002_Control_Flow_008.png)

 

The lesser used cousin of the while loop in SWIFT used to be the C based DO WHILE loop... this is something that does not exist in SWIFT anymore... now it\'s known as the REPEAT WHILE... the reason to use something like it is to allow for a loop to potentially run AT LEAST ONCE.

![// Swift-style \" repeat-while\" repeat { call a function make a constant print a message call another function } while itemsToProcess \> 0 ](002_Control_Flow_009.png)

 

This will run at least once as I just mentioned... even if the condition is FALSE.

 

WOAH WOAH! SWIFT does NOT have the classic FOR loop? WHAT?!

![// Classic C-style \"for\" for ( int i = loop 11 make call anoe--- function ](002_Control_Flow_010.png)

 

Notice how Xcode tells me how many times a loop runs on the right side.

![41 \"one\", \"rando\... 42 43 44 45 46 47 48 49 50 51 var bunchOfWords: \[String\] // Straight forward. but \[\"one\", \"random\", \" car , \"coffee\"\]; interesting how I was NOT allowed to use parenthesis here for for word in bunchOfWords { print (word) randomVarName in 1.. 10 { print (randomVarName) (4 times) (10 times) ](002_Control_Flow_011.png)

 

 

Remember when I said there were two different range operators? HERE IS THE OTHER ONE:

![10 closed range operator inclusive of both values half-open range operator range will not include the value on the right ](002_Control_Flow_012.png)

 

**String Interpolation is pretty much the same, EXCEPT for the syntax:**

**\\ ( )**

That\'s all. One thing to not is that when using string interpolation in swift we will NOT need to explicitly convert my variables into strings. Swift is smart enough to just do that for you in the case that it CAN make the conversion. That\'s not necessarily guaranteed though.

 

 

 
