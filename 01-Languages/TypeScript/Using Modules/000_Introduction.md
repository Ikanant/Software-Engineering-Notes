Introduction

Wednesday, August 26, 2020

10:04 AM

![](000_Introduction_000.png)

 

Here is an example from within the Angular framework that creates a module... Not only we see a module being created, but we also see imported modules being consumed by the new module.

 

**Why use modules?**

With growing application it is critical to break up the application into discrete chunks that will allow to encapsulate logic within the application that can be re-used in the future.

 

**DRY:** Don\'t Repeat Yourself.... If at all possible, code should NOT be shared rather than duplicated.

 

![Importing and Exporting O Easily make code in a module public or private Avoid repetition and boiler-plate code ](000_Introduction_001.png)

 

Another important feature of ES and therefore TS: They are always evaluated in **Strict Mode**. This was generally caused by the amount of bugs we often saw in early versions of JS. Strict mode was added in JS version 5.

 

**What Makes a Module a Module?**

By this I mean, why do we need to categorize modules to begin with? What is different than just having JS TS files that we can just re-use? They key: IMPORT AND EXPORT statements

 

![import { x } from \' . / some-module\' ; export x; The Primary Distinction of Modules import and/or export statements ](000_Introduction_002.png)

 

Any file that contains an IMPORT or EXPORT statement will be treated like a module.

 

**Global Scope:** In a regular JS TS file, the code can live anywhere really but when dealing with modules, this is NOT the case. The scope is always local to the module itself. The WINDOW object is available, but we can\'t access code defined in other modules UNLESS we explicitly import that module.

 

For security reasons: Modules CANNOT be used in a purely local environment. We CANNOT just click on an HTML that loads modules because the modules will NOT be loaded and we will generate CROS origin errors in the console.

 

**Modules are ALWAYS deferred:** In order to avoid blocking page rendering with scripts, the defer attribute will be used... Which means we will LOAD the script BUT not execute it until the HTML parsing has finished.

 

 

**Internal vs External Modules**

 

This is OLD though. TS USED to have the concept of internal/external modules. External modules is what is now the standard really. This refers to the type of module that uses IMPORT/EXPORT statements. In TS now a module is simply an external module.

 

TS now has the module **keyword** which is used to create what used to be known as **Named Internal Module.** Any variables/functions inside a module will be scoped ONLY to that module...

 

![module MyNamedInterna1Modu1e { private\' ; const privateVar - \'public\'; export const publicVar = Named Internal Module Values can be exported ](000_Introduction_003.png)

 

![console . log(MyNamedInterna1Modu1e . publicVar) ; / /public ](000_Introduction_004.png)

 

Here the module ITSELF is added to the global scope... so outside of the module we would be able to access the public var const as if it was a property of the module. The privateVar however would ONLY be available INSIDE the module.

 

**NAMESPACES**

This is [important:]{.underline} Internal Modules are not referred as NAMESPACES. The module keywords now has been updated to the namespace keyword.

 

![namespace MyNamespace { private\' ; const privateVar - \'public\'; export const publicVar = console . log(MyNamespace . publicVar) ; / /public ](000_Introduction_005.png)

 

This behaves EXACTLY as the code above. *[This is the preferred syntax if what we need is an object added to the GLOBAL namespace.]{.underline}*

 

ANY code inside a file, that is not explicitly a module IS attached to the global scope.

 
