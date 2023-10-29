Setting up a Development Environment

Thursday, May 02, 2019

3:53 PM

 

 

![Dragons Ahead Multiple tools - APIs Configurations Releases Multiple environments Development - Production - Test Different renderers - DOM - SSR ](004_Setting_up_a_Development_Environment_000.png){width="5.0in" height="3.441666666666667in"}

 

Managing and creating REACT applications from scratch is always a bit challenging... Luckily, as developers we have various tools that will make our life\'s a bit easier...

 

**Create-React-App**

Single command will allow us to create a new REACT app. This is a good/bad thing... by automating everything for the creation of your app, developers will often miss what is actually required to run the application.

 

**To follow how to create a REACT app from scratch follow:**

<https://jscomplete.com/reactful>

 

**WHAT is WebPack?\
**Webpack is a module bundler. When we take our REACT application into the file system, we are going to put it in multiple modules. We are going to depend on external modules as well (like react / react-dom) ... so when we ship things to the browser we need to ship every single bundle. Because browsers don\'t know how to work with modules YET.

 

The normal way to handle bundling our applications is to bundle EVERYTHING in a single file and ship that to the browser. So the webpack package is gonna do the bundling for us. We will tell it to start from File X and everything that file X requires, bring it under a single bundle file so we can server that bundle file to our webserver and use it to mount our react web server to the DOM.

 

**Babel**

Babel is the package that compiles JSX into regular REACT API calls. We need to hook babel into the webpack process because webpack is gonna be bundling our system... we need to tell webpack that if it sees any JSX code, it should invoke babel to convert that into REACT API calls.

 

**Nodemon**

Package that will let us automatically restart node when we change anything in our application.

 

![4. Creating an Initial Directory Structure This really depends on your style and preferences, but a simple structure would be something like: fulljs/ dist/ main \_ js src/ index \_ js components/ App \_ js server/ server \_ js ](004_Setting_up_a_Development_Environment_001.png){width="5.0in" height="2.3833333333333333in"}

 

 
