03 - Setting up Gulp

Friday, April 29, 2016

11:37 AM

 

![](002_03_-_Setting_up_Gulp_000.png)

 

**Gulp:**

-   Gulp is a Task Manager for our web projects

-   Can be installed with NPM

-   Easy to use

-   Code base configuration

-   Package based

    -   If I wanna do inject I just pull that package and just wrap gulp around it

 

-   **npm install gulp \--save-dev**

    -   What the keyboard dev is doing here is that in our package.json file, we are no longer going only have one \"dependency\" attribute...instead we are going to have another \"devDependencies\" that will contain our gulp dependency. The reason why we have this is because when we potentially deploy our application to a production environment, we are not going to need gulp any more there. By having a separate gulp dependency will are save some future time.

 

In order to use gulp we will use a file called: gulpfile.js

This is where we are going to do EVEYTHING for our gulp stuff...

 

 

**Code Quality**

 

**Coding Standards:**

JSHint: Responsible for the CODE QUALITY enforcement javascript files. It checks for some errors, and enforces some coding conventions like remembering to use \';\' in your code. It is very easy to configure... and Open Source

 

**Coding Style:**

JSCS: Enforces style conventions.... Right amount of indentions, and not having multiple lines, etc...

 

JSHint and JSHint provide you with pretty much everything we need to ensure our code is good.

 

 

**Wiredep**

Deal with our CSS and JavaScript file in our html... So, what we want to do is have Gulp INJECT those packages from Bower into my HTML automatically

 

 

**Nodemon**

 

Nodemon is a great tool that will allow our application to automatically update as we add or delete js and css files to our application.

 

Monitor files... Whenever anything changes it will automatically restart the server

 

 

![](002_03_-_Setting_up_Gulp_001.png)
