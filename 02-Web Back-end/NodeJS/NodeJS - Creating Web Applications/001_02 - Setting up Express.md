02 - Setting up Express

Friday, April 29, 2016

11:36 AM

**What are we doing in this course?**

We are going to write a library application...

When writing: *var express = require(\'express\');*

*That doesn\'t really give us the ability to do anything...so, we are actually going to create an instance of that variable...or an instance of express. Now we can do things with that.*

**Callbacks**

Function that app.listen is going to execute when is done doing what is doing

For our application we have been starting everyhting by typing **node app.js** but what happens if the next developer in the application does not know which js file will launch the server? In that case we can just do **npm start**

In order to use these functionallity we need to edit our package.json file and go to the section with scripts...here we are going to add another script that we are going to call

**\"start\": \"node app.js\"**

**Bootstrap Themes & Templates**

<http://www.bootstrapzero.com/>

When we create a public folder that contains all of our js and css files, we do not want to explicitly write down in our application the handlers to get those files sent to the users browser. Instead we are just going to set that public directory as just a static directory... So that everything we do and need will sit there and our express server will just serve that stuff up to the user...

**Static Files**

**app.use()**

This command will allow us to set up some middleware. With app.use() just know that whatever we put on in there is going to be used by Express FIRST. Before it does anything else...

**app.use(express.static(\'public\'));** // This will set the public directory as static

What this is going to do is that anytime there is any requests to our app... The first thing express is going to do is check on that folder and make sure it exits... if nothing is found within that directory, the express will start dealing with the requests using routes

**Bower**

Bower is our FRONT END package management system. Just like we use NPM to download and use all the latest libraries like Express, React, etc... We are going to use Bower to set up the latest stuff for our page for our front end...

We will take care of download the latest Bootstrap, Angular, FontAwesome, etc...

[Flat package hierarchy]: It doesn\'t install dependencies underneath the things that depend on it. For example Bootsrap depends on Jquery... Bower will install them both at the same level, instead of having Jquery multiple times for all the things that are going to depend on it.

![](001_02_-_Setting_up_Express_000.png)

-   **npm install bower -g**

    -   -g: Global

File: .bowerrc

When we get bower going, we realize we have a big folder in our application called bower_components...We don\'t really want this....because in general, it just crowds our application....So what we are going to do is make bower save all of our FRONT END dependencies inside our public folder inside a lib directory.....

Why lib if we already have a css and js folders?

Well, in order to have a cleaner environmet we are going to separate our css and js work from the one that bower will save from Bootstrap and or other libraries. So, at the end it is more of a clean target.

Insde .bowerrc we are going to include the following command:

> *{*
>
> *\"directory\": \"public/lib\"*
>
> *}*

**Summary:**

![](001_02_-_Setting_up_Express_001.png)
