Ambient Modules

Wednesday, August 26, 2020

11:41 AM

 

![Regular modules implement values and behaviours Ambient modules describe implementations ](002_Ambient_Modules_000.png){width="6.925in" height="2.2083333333333335in"}

 

 

 

Ambient Modules are the common tool used to describe the API that a NON-TS file exposes. These are often provided along the side of libraries or frameworks that can be used alongside TS.

 

 

![\"allowJs\" . true, • ](002_Ambient_Modules_001.png){width="3.716666666666667in" height="0.825in"}

 

First make sure we allow JS code inside of our own TS code.

 

![JS cube.js X JS cube.js \> \... 1 2 3 4 export function cube(num) { - return num num num; ](002_Ambient_Modules_002.png){width="5.966666666666667in" height="2.716666666666667in"}

 

Let\'s assume we are interested in using the above function in our existing TS code... we can import the file successfully BUT we would run into a problem. When figuring out what functions are available (depending on the editor we are using) we are gonna have limited visibility to the code we can use... commonly we can see function names but, how about the type of input parameter for our function??? This can be fixed with an ambient module.

 

![Ambient modules: Have .d.ts extensions Referred to as declaration files Have the same name as the file they describe ](002_Ambient_Modules_003.png){width="6.533333333333333in" height="2.3in"}

 

 

So for use we would do something along the lines of:

![JS cube.js tsconfig.json TS b.ts TS cube.d.ts TS cube.d.ts \> { } \'cube\' I 2 3 4 declare module - \' cube\' - { , export function cube(num: number) : number; ](002_Ambient_Modules_004.png){width="10.608333333333333in" height="3.575in"}

 

**IMPORTANT**: Our ambient module needs to have the SAME name as the file it describes.

 

![import { cube } from \'cube\' ; cube( \' 002%\') ; ](002_Ambient_Modules_005.png){width="4.991666666666666in" height="1.2166666666666666in"}

 

 

\^\^\^ Now, instead of passing in the path of the module, we can simply provide the name to the module we are trying to use, and as you can see..... We get an error when trying to pass a string to the function. This is a nifty thing the editor is able to do simply by seeing the two files in the same directory.

 

![ES modules must be referenced by path not by name ](002_Ambient_Modules_006.png){width="5.8in" height="1.8083333333333333in"}

 

This would be resolved by simply using webpack or some kind of bundler

 

 

**Third Party Libraries**

![15 16 17 18 19 20 21 22 23 25 \'\$\' is declared but its value is never read. ts(6133) Could not find a declaration file for module \'jquery\' . \' c : /Users/Dan/using-typescript- modules/node_modules/jquery/dist/jquery.js\' implicitly has an Try npm install \@types/jquery• if it exists or add a new (.d.ts) file containing \*declare module declaration \'jquery• ; • ts(7Ø16) import \$ from ](002_Ambient_Modules_007.png){width="4.85in" height="2.1666666666666665in"}

 

So let\'s assume we plan to use JQuery in our code... well, we can certainly do that but we will need to also bring up the declaration file for it... in here we can resource to the \@Types repository. This contains THOUSANDS of declaration files for many JS files

 

<https://github.com/DefinitelyTyped/DefinitelyTyped>

 

There are so many declaration files here that are too many to read from github... so in that case, we have a separate search engine we can use for it...

 

<https://microsoft.github.io/TypeSearch/>

 

By using this

![](002_Ambient_Modules_008.png){width="6.033333333333333in" height="2.4916666666666667in"}

 

BOOM now we are getting intellisense for JQuery.

 

![N PM dependencies are not included by the compiler by default ](002_Ambient_Modules_009.png){width="5.816666666666666in" height="1.8666666666666667in"}

 

 

 

**Augmenting Ambien Modules**

 

Taking into consideration we might want to edit/tweak something in the declaration file... This is probably not recommended since we are literally gathering such files from some third party process... in cases like that we can augment the \*ambient module by declaring another module named the same thing like so:

 

![declare module \'cube\' - export function - cube() : - string; ](002_Ambient_Modules_010.png){width="5.741666666666666in" height="1.6916666666666667in"}

 

 

In this scenario TS will MERGE the two DECLARATIONS for the module and INCLUDE the type information for both of them. Woah!

 

![= function() console. ) ; return \$(this); ](002_Ambient_Modules_011.png){width="4.55in" height="1.75in"}

 

Like here \^\^\^\^ we want to add a debug method to Jquery... how can we do that ?!?! We can simply augment the GLOBAL declaration to add the NEW method to Jquery.

 

![32 33 34 35 36 37 declare global { - interface - JQuery { debug(): JQuery; ](002_Ambient_Modules_012.png){width="4.958333333333333in" height="2.5416666666666665in"}

 
