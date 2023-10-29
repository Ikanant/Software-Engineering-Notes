Creating Basic TS Modules

Wednesday, August 26, 2020

10:53 AM

**EXPORTS:**

 

Export is pretty straight forward, we essentially only require to use the export keyword and we will have a module that\'s exporting something like:

![Prefix any declaration with the export keyword var/let/const - function() class ](001_Creating_Basic_TS_Modules_000.png){width="4.55in" height="1.7666666666666666in"}

 

 

![TS Qts Ts a-ts 1 export const aString = Welcome to TypeScript\' ; ](001_Creating_Basic_TS_Modules_001.png){width="5.55in" height="1.0583333333333333in"}

 

This type of export \^\^\^ By far the most common one is known as a NAMED export. Because we actually export the identifier. In this case \'aString\'

 

Expressions CANNOT be exported (yet)... we can\'t export something like

![](001_Creating_Basic_TS_Modules_002.png){width="1.8416666666666666in" height="0.44166666666666665in"}

 

If we do want to export an expression we NEED to convert it to a declaration:

![2 export const fn --- ](001_Creating_Basic_TS_Modules_003.png){width="3.725in" height="0.5416666666666666in"}

 

Export are a block statement so we can also wrap whatever we want to export in curly braces. One of the coolest things of using the export statement is that we can rename whatever we are exporting with the AS operator.

 

![1 2 3 const aString = \'Welcome to TypeScript\' ; export { aString as bString export const -fn --- ](001_Creating_Basic_TS_Modules_004.png){width="4.966666666666667in" height="0.975in"}

 

**Re-exporting**

One other thing we can do is re-export something without even using it in our module. I am unsure why I would ever do this, but it looks like this:\
 

![TS a.ts Ts a.ts \> 1 2 3 4 5 6 X TS re-export.ts const aString = const bString --- \'Welcome to TypeScript\' ; Something ; { aString, bString y; export export const --- { message } from- \' . Ire-export\'; export ](001_Creating_Basic_TS_Modules_005.png){width="5.333333333333333in" height="2.5416666666666665in"}

 

 

**Using the \* character.. .BARREL FILES**

 

![TS a.ts utils \> 1 2 TS index.ts export expo rt TS string.ts TS wrapRr.ts \* frorn \' . \[number \' ; \_ \* frorn ./string•; TS numtkr.ts TS index.ts X TS re-export.ts ](001_Creating_Basic_TS_Modules_006.png){width="8.291666666666666in" height="1.3in"}

 

At times we can do something like this. What we are saying here is that we are grabbing all variables/functions from the respective modules (which could be exporting ONE or MORE things) an we are exporting EVERYTHING... This is useful because when we have a file that consumes both of these modules, it would be better to consolidate everything into the ONE (commonly known barrel file) instead of all

 

![Barrel Files Useful for simplifying imports Watch out for circular imports! ](001_Creating_Basic_TS_Modules_007.png){width="7.583333333333333in" height="3.4in"}

 

 

**DEFAULT EXPORTS**

I guess by far the most common type of export I have done. We can ONLY have a SIGNLE default export per module. We can export variables, classes or even functions are default exports and in this case NO identifier is needed for those exported items... meaning we don\'t have to name them.

 

![TS a.ts x TS a.ts \> @ defaultFn 1 2 3 4 5 6 7 8 9 10 11 12 13 14 const aString = • \'Welcome to, TypeScript \' ; const bString = \'Something ; export { aString, bString y; export const fn / / export - default • f n; export { message } from \' . / re-export\' ; // export - default- \'default\' ; export default -function defaultFn() - return \' default - function \' ](001_Creating_Basic_TS_Modules_008.png){width="3.975in" height="3.7583333333333333in"}

 

COMMON JS has the concept of an EXPORT object. This single exported object can serve as a namespace for all of the exported values of the module... With this, there is ONE more way of exporting something that allows to specify a single exported object for a module.

![11 export = \'test\' • ](001_Creating_Basic_TS_Modules_009.png){width="3.4833333333333334in" height="0.7583333333333333in"}

 

This is known as the EXPORT EQUALS... This is NOT supported when we compile to ES code and can only be used with common js, amd, along another few. When using this method it also has to be the ONLY export in the file.

 

![Can exist next to other exports Supported by all module loaders Recommended by TypeScript Mainly useful for libraries/frameworks Poor editor support/discoverability ](001_Creating_Basic_TS_Modules_010.png){width="8.4in" height="3.1166666666666667in"}

 

 

 

**IMPORTS:**

 

![import { aString } from console. log(aString) ; \'./a\'; ](001_Creating_Basic_TS_Modules_011.png){width="5.158333333333333in" height="1.0916666666666666in"}

 

\^\^\^ This is commonly known as a named import.... And here we can import one or however many identifiers from whatever module we are using. The identifiers NEED to match the name in the module.

 

IMPORT statement NEED to be at the top of the file.... And identifiers can be renamed:

 

![1 2 3 import , { aString as - theString, - bString } from import \* as strings from \' . / a\' ; con sole. ; ](001_Creating_Basic_TS_Modules_012.png){width="7.541666666666667in" height="1.3416666666666666in"}

 

Notice that we can also use the \* character to get everything from the module BUT we do need to user the **as** keword.

 

**DEFAULT IMPORTS:**

Pretty much the same as the previously mentioned BUT we do not need to use the curly brackets.. Since a module can only have a single default export when importing it we are grabbing the one and only part of that module that has been exported.... Since default exports don\'t even need to have a name, we can name them whatever we want when importing WITHOUT using the **as** keyword:

 

![import customStringName from \' . / a \' ; 9 10 console. log(customStringNam ) ; // default ](001_Creating_Basic_TS_Modules_013.png){width="5.0in" height="0.8583333333333333in"}

 

 

**HOW ABOUT IMPORTING IMPORT the EXPORT EQUAL syntax?**

For this we will use the **require** keyword.D

 

![12 13 import test = require console. log(test); // - test ](001_Creating_Basic_TS_Modules_014.png){width="4.1in" height="0.7583333333333333in"}

 

The required function is a globally available function that takes in the path of the module we wish to import. One thing to not is that we can\'t re-export an export equal export

 

**OPTIONALLY LOAD MODULES**

 

![if (condition) { import { something } from \' . /somewhere \' // error Imports must be at the top level of a file Cannot be nested! ](001_Creating_Basic_TS_Modules_015.png){width="7.7in" height="3.8666666666666667in"}

 

 

 

![if (condition) { import( ./somewhere\' ) ; // works! Imports must be at the top level of a file Can be nested! Must be used with the ESNext as the module target ](001_Creating_Basic_TS_Modules_016.png){width="7.658333333333333in" height="3.9in"}

 

 

Though we can\'t nest the import statements, we CAN nest import expressions... THIS IS ONLY Allowed when we are compiling COMMON JS or ESNext.

 

![if (Math . random() 0.5) { import (\' ./a \' ) . then(a =\> - console. log( \'The message - is: \' , a . aString) ) ; ](001_Creating_Basic_TS_Modules_017.png){width="7.508333333333334in" height="0.8833333333333333in"}

 

 

 

**LOADING JSON FILES**

![import \* as config from ](001_Creating_Basic_TS_Modules_018.png){width="6.741666666666666in" height="0.5416666666666666in"}

 

Simply importing a json file (that contains valid json) is not enough to import into our TS module.

![L // • \"allowUmdG10ba1Access\": tr \"resolveJsonModu1e\" : true, ](001_Creating_Basic_TS_Modules_019.png){width="4.941666666666666in" height="1.175in"}

 

In order to get this to work we need to add the above line to the tsconfig.json

 

![import\* as config from \' ./config.json \' con sole. log( config. userSetting1 ) ; ](001_Creating_Basic_TS_Modules_020.png){width="6.816666666666666in" height="0.9083333333333333in"}

 

There is one caveat here though... in ES Modules ONLY JavaScript files can be modules.

 

![Some 3rd party module loaders can allow JSON files to be loaded as modules ](001_Creating_Basic_TS_Modules_021.png){width="5.208333333333333in" height="1.3in"}
