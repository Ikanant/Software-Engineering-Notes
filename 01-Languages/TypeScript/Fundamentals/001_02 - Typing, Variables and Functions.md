02 - Typing, Variables and Functions

Sunday, February 25, 2018

4:16 PM

**Grammar, Declarations and Annotations**

 

![Declare it var num 2 Name it 3 Set it ](001_02_-_Typing,_Variables_and_Functions_000.png){width="3.216666666666667in" height="1.7916666666666667in"}

The above example it\'s interesting. This syntax would work just fine when coding on JS.... But what is different now ? In essence, we are using TypeScript inference tool to set the **num** variable to a number. So, if this variable were to be compared to something else along the lines of our program, it would be treated like a number and NOT like any other data type.

 

![Declare rt 3 Annotate it var num: number = 5 Set it 2 Name iC 4 Type it ](001_02_-_Typing,_Variables_and_Functions_001.png){width="3.6166666666666667in" height="1.5833333333333333in"}

 

Note: In typescript we have a variable type of ANY.... Which is the base type of all variables.

 

![var anyl; var numl: number; var num2: var num3 = var num4 = num3 var strl = numl Type could be any type (any) number = 2 3; Type Annotation Type Annotation Setting Che Value Type Inference (number) Type Inference (number) lee; \' some string\'; Type Inference (string) var nothappy : number = numl + \' some string\' ; Error ! ](001_02_-_Typing,_Variables_and_Functions_002.png){width="5.866666666666666in" height="3.525in"}

 

Let\'s say we have a function:\
\
**function apple () { reuturn \'hello\'; }**

 

In Javascript, if we tried calling that function with some input in it: **apple (123);** that would not yield an error. In Typescript, this would be caught right away.

 

![// Bootstrap everything : (s: string, p: string, c: string) void = function (startButton, pauseButton, clearButton) document. getEIementById ( startButton) . addEventLi stener( \"click \" , start Timer, document. getE1ementById ( pauseButton) . addEventListener( \"click •t , pauseTimer, document . getE1ementById ( clearButton) . addEventListener( \"click • • , clearTimer, false) ; false) ; false) ; displayTimer(); window. onload = function linit( \' startButton\' , \' pauseButton \' \' clearButton \' ) ; ](001_02_-_Typing,_Variables_and_Functions_003.png){width="5.991666666666666in" height="3.7916666666666665in"}

 

 

One important thing in the above example is that we have the capability to specify variable types as well as function input types & return types:\
 

**Apple : (s: number) =\> void**

 

That line will assure us that the apple variable will be assigned to a function that only takes one number input parameter and returns nothing.

 

![TypeScript Static typing (optional) Type safety is a compile-time feature JavaScript Dynamictyping Type safety happens at run-time debugging ](001_02_-_Typing,_Variables_and_Functions_004.png){width="6.616666666666666in" height="3.7916666666666665in"}

 

An example of this relationship is as follows:

![JavaScript\'s Dynamic Types Could be any type var person; \'John Papa\' ; person = person. substring (1, person --- 1 substring(l, person. 4); Uncaught TypeError: Object 1 has no 4); method \'substring\' ](001_02_-_Typing,_Variables_and_Functions_005.png){width="6.15in" height="3.6in"}

 

**Ambient Declarations**\
\
These refer to the many cases in which we have no control over the type of the variables we are using which is quite common when using any type of framework in our code...

 

![TypeScript declare var document; document. title = \"Hello\" ; lib.d.ts is referenced by default and contains references for the DOM and JavaScript ](001_02_-_Typing,_Variables_and_Functions_006.png){width="3.0in" height="3.775in"}

 

When using the keyword **declare** we create an AMBIENT declaration. It just says that this variable that I just called is not necessarily in my file. What this allows us to do is catch any sort of error of assigning the wrong value to such variables by accident.\
\
Looking at the above example, if we set the title to a number accidentally,,, TS would tell us of our mistake right away, instead of us running into the issue during runtime.

 

![Type Definition Files (aka Declaration Source Files) var data = \"Hello John\" ; TypeScript /// \<reference path=\"jquery.d.ts\" / \> declare var \$; \$(\"div\") . text (data); Helps provide types forjquery JavaScript var data = \"Hello John\"; . text (data); Ambient Declarations do not appear anywhere in the JavaScript ](001_02_-_Typing,_Variables_and_Functions_007.png){width="7.466666666666667in" height="4.833333333333333in"}

 

**TYPINGs**

 

In the code bellow we run into a common problem in TS. We are trying to use a third party library in our code called Knockout. The issue is that when we try to declare such variable... but default it will be set to type ANY.... Or error out if we try to specify the type of something that the code does not know. In order to deal with these cases TS offers something called TYPINGS. Typings are a series of files (I will go over them in more detail in the near future) that end up in **.d.ts** . When we have a file like such, we can use it to make Typescript understand what our third party library actually is. (Type definition files)

 

There are a couple of ways to retrieve the typings files for various libraries:\
\
<http://typescript.codeplex.com>

 

OR\
\
<https://github.com/borisyankov/DefinitelyTyped>

 

The question now is.... How do we reference our typings file in our module.... Simple, we just drag (in VS) our d.ts file into our ts code and it will reference it like:\
\
 

![/// (reference Errodule demo ø2 ø4 { // KO beloin s to the imported Knockout nuget pacakge we installed declare var var name = Knoc koutStatic ; . obserwa ble \'Jonathan Hdez\' • ](001_02_-_Typing,_Variables_and_Functions_008.png){width="5.775in" height="1.4083333333333334in"}

 

 

In the above example, when I type in **ko.** I know even get Intellisense. Which is great!

 

**ANY and Primitive Types**

 

Whenever we declare a variable without specifying it\'s type, it will by default be set of type ANY.

 

Any can represent any value at all. ANY is the base type of TS and there is no type checking with variable of this type.

 

![var data: var info; any ; No static type checking on \"any\" ](001_02_-_Typing,_Variables_and_Functions_009.png){width="3.816666666666667in" height="1.825in"}

 

![age: number var score: number = 98.25; var var var var string = \'John\'; var var rating hasData : isReady firstName : lastName = = 98.25; boolean = true; \'Papa\'; = true; number boolean string ](001_02_-_Typing,_Variables_and_Functions_010.png){width="4.808333333333334in" height="2.5833333333333335in"}

 

![var names: string\[\] = \[\'John\', \'Dan var firstPerson: string; firstPerson = names\[0\]; indexer , \'Aaron\', \'Fritz\'\]; ](001_02_-_Typing,_Variables_and_Functions_011.png){width="5.066666666666666in" height="2.0083333333333333in"}

 

![var var var var var var num: number = null; str: string = null; isHappy: boolean = null; customer: { } = null; age: number; = undefined; customer null undefined Null type is a subtype ofall primitives (except void and undefined) ](001_02_-_Typing,_Variables_and_Functions_012.png){width="5.225in" height="3.325in"}

 

![var quantity: number; undefined var company = undefined; undefined type is a subtype of all types ](001_02_-_Typing,_Variables_and_Functions_013.png){width="5.25in" height="2.6166666666666667in"}

 

**Object Types\
\
** 

![• Examples Functions, class, module, interface, and literal types May contain Properties o public or private o required oroptional Call signatures Construct signatures Index signatures ](001_02_-_Typing,_Variables_and_Functions_014.png){width="6.625in" height="3.908333333333333in"}

 

![var squarelt = if (rect. w = rect. h return else { rect. h return var sqI: number console. log(sql) ; number sq2: var console.log(s 2 • function (rect: { h: --- undefined) { number, rect. h; rect. w; ](001_02_-_Typing,_Variables_and_Functions_015.png){width="4.766666666666667in" height="2.316666666666667in"}

 

 

Notice that the ? Sign in a functions input means that that value is optional. If we have a function that takes in a number x and we don\'t pass it in when calling such function in TS we would get an ERROR right away.
