Introduction

Saturday, September 21, 2019

10:50 AM

 

Note goals:

![Get Vue from a CDN Create the HTML Create a Vue instance Bind a model from the Vue instance to the HTML ](000_Introduction_000.png){width="5.5in" height="3.15in"}

CDN = Content Delivery Network

 

**Tooling**

First we will be needing Node installed... note will bring NPM and that\'s the easiest way to retrieve all the VUE packages we will need to start scaffolding our application.

 

**\<npm install -g \@vue/cli\>**

 

**Why do we need to install VUE CLI?**

-   Stylus

-   Linting

-   PWA

-   Webpack

-   Jest

-   Babel

-   Nightwatch

-   Cypress.io

-   Modern mode

-   Mocha

-   Sass

-   Less

-   Typescript

-   Web Component

 

Well the VUE CLI does all the setup for us. So we don\'t need to worry about any of it or have headaches through the setup process.

 

John Papa recommends 2 main editor plugins:

1.  Vetur

    a.  Gives us language services inside of VS Code. So VS Code knows what VUE files are

2.  Vue Snippets

    a.  Cool for having VS code write a lot of the syntax for us.

 

It is also recommended to use the VUE Dev browser extension to make our debug process even easier.

 

Once all these are setup... we can simply use the VUE-CLI to create our first app with simple commands like:\
 

**\<vue create hello-world -d\>** // d flag means to just use all the defaults

**\<npm run serve\>** // d flag means to just use all the defaults

 

 

**How a Vue App Starts**

 

The application will run through the scripts we setup in the package.json file.

\<npm run serve\>

\<npm run build\>

\<npm run lint\>

Are the defaults when creating a vue project through the vue-cli.

 

\<npm run build\>: This script will run a production build process and it will through the files generated in a folder called **dist**.

 

Well when all this happens, is inside the src folder and it\'s the **main.js** file. Inside this file is where we see this:\
 

![1 2 3 4 5 6 7 8 9 import Vue import App new from from \'vue\'; \'@/app\' , Vue . config. productionTip False; render: h h(App), j\]) . \$mount( \'#app\' ) ; ](000_Introduction_001.png){width="4.658333333333333in" height="2.466666666666667in"}

 

**new Vue:** This is created a new instance of VUE and it\'s taking the **App** component (will go into that in future notes) and it\'s mounting it to the ID (in the index.html) called \'app\'.

 

Where is this index.html? The public folder of our project is the one that contains all the assets that will be distributed by our application. Here we will see our index.html and the div with the id of \'app\'. We DO NOT serve from public... these files will get moved to DIST later...

 

Now back in main.js.... Where is the App component... well, that is our app.vue file that\'s also inside the src folder. Inside the file we can see inside the \<template\> tag we have our div with an id of \'app\' as well... We are using another Vue component called \<HeaderBar\> and then some more HTML.

 

The \<HeaderBar\> component is being pulled from the component folder:\
*import HeaderBar from \'@/components/header-bar\';*

 

And one important thing to notice here as well is that after we import the component, we ALSO need to tell our new component (the one we are exporting) that it depends on the imported component in the components property.

 

![import HeaderBar from \'@/components/headel-bar\' ; export default { App name : components: { HeaderBar } , ](000_Introduction_002.png){width="5.0in" height="2.1333333333333333in"}

 

**Is \<template\> and \<script\> sections all we need in a .vue file?**

No. We could also have a \<style\> section... This style can be done with lots of various css frameworks like scss, less, stylus, etc...

![\<style scoped\> ](000_Introduction_003.png){width="2.875in" height="0.975in"}

 

Notice the \'scoped\' tag... This means this style is SCOPED to this component TREE and it\'s children ONLY. If we remove it, the entire application can see our styles.

 

If we took a closer look at the app.vue file that we went over earlier, that also has a style section pulling from the design folder called index.scss... this style is accessible by any component in the application since it\'s NOT scoped.
