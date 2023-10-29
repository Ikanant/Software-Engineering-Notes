**Why React?**

Monday, January 21, 2019

1:37 PM

 

![Machine generated alternative text: History 2011 2012 2013 2014 2015 2016 Created by Facebook Used on Instagram Open sourced Embraced by many large companies React Native released React 15 released (previous version was 0.14) Today Over 30k components at Facebook Full-time dev staff Used by many in Fortune 500 ](000_Why_React-_000.png){width="4.925in" height="2.675in"}

 

**Why React?**

**\
1. Flexibility:**

One of the main attractions to REACT is that, ONCE you learn it, you can build user interfaces for a huge number of platforms and use cases. REACT is extremely flexible!

 

REACT is known to embed fewer opinions than the competition.

![Library React Frameworks A Angular Opinion Ember ](000_Why_React-_001.png){width="7.533333333333333in" height="3.591666666666667in"}

 

**Where Can I Use REACT?**

When REACT was originally produced, it had a simple purpose. Create components for web applications. As the library has gained popularity here are some of the use cases commonly using the new technology.

 

![Web apps Desktop Static sites NEkT .JS Server-rendered React Native Mobile React VR Virtual Reality ](000_Why_React-_002.png){width="5.158333333333333in" height="2.2416666666666667in"}

 

REACT is HIGHLY versatile because the RENDER is separate from REACT itself.

 

-   Web apps: react-dom

-   Mobile: react-native

-   VR: react-vr

 

![Web (+ NW & Electron) • react-dom - A declarative, efficient, and flexible JavaScript library for building user interfaces. • react-art - React Bridge to the ART Drawing Library. • react-canvas - High performance canvas rendering for React components. • react-three - React bindings to create and control a 3D scene using three.js. • React-GL - Render React components in WebGL for 60 FPS animations. • ReactLiberty - Connect, discover, be free to choose between WebGL I Canvas (PIXI) / DOM or any other UI renderer. • react-vr - Render React components in WebGL/WebVR for VR apps. react-konsul - A react renderer that renders to the browser\'s devtools console. • react-worker-dom - Experiments to see the advantages of using Web Workers to Render React Virtual DOM. • rax - A universal React-compatible render engine. Mobile • react-native - A framework for building native apps with React. • react-titanium - React custom renderer for Appcelerator@ TitaniumTM SDK. Command Line Interface • react-blessed - A react renderer for blessed. • ink - React for interactive command-line apps ](000_Why_React-_003.png){width="6.25in" height="4.458333333333333in"}

 

**Server-side Rendering:**

ReactDomServer.renderToString(): This is an example that renders a component to a string of HTML

 

REACT is a light-weight Library that makes it easy to update existing Apps (even server side render apps)

 

![javascript Courses by Cory Creating Reusable React Components by Cory House Intermediate 6h 21m Step 1: Replace the star rating with a React component 05 June 2017 ](000_Why_React-_004.png){width="5.125in" height="1.4583333333333333in"}

 

![Step 2: Replace each course list item with React Courses by Cory Creating Reusable React Components by Cory House Intermediate 6h 21m 05 June 2017 \* (47) ](000_Why_React-_005.png){width="5.125in" height="1.5666666666666667in"}

etc\...

 

**Broad Browser Support:**

Taking into consideration that REACT is used heavily by Facebook, we can trust that it will continue to be supported across all popular web browsers.

 

 

**2. Developer Experience**

The RAPID feedback development experience + Small logical API, gives a development experience that\'s very hard to beat. Few concepts to master, so REACT is a tool that developers don\'t need to check the docs often.

 

 

![import React from I react I ; function HelloWorld(props) { return \<div\>Hello {props. ](000_Why_React-_006.png){width="4.058333333333334in" height="1.3916666666666666in"}

 

With REACT, we will be writing basically functions that return what looks like HTML. We simply import REACT using a standard JS import statement THEN we declare a component using a regular JS function that takes in variables via an object called PROPs...

 

We can also write JS Classes, which involves a bit more typing, but offers slightly more power

 

![import React from I react I; class HelloWorld extends React. Component { render() { return \<div\>Hello {props. name}\</div\> ](000_Why_React-_007.png){width="4.008333333333334in" height="1.7083333333333333in"}

 

\*\*\* KEEP IN MIND: The return statements we are using in both cases look very much like HTML code (without being closed by double quotes) but it is actually JSX.

 

![The JSX above compiles down to this. This plain JS is sent to the browser. The call to createElement generates HTML. React. createElement ( Il hl JSX Compiles to JS color=\" here\</hl\> {color: \" red\"}, \"Heading here\") 11 ](000_Why_React-_008.png){width="4.391666666666667in" height="1.9083333333333334in"}

 

 

The markup that should sit inside our elements can contains calls to other elements if we have nested markup. We can 100% avoid JSX, but clearly the top example is simpler to read and nest (most commonly used by REACT developers).

 

**How does this compare to other tools?\
**The main thing to note with REACT is that, differently from other languages, REACT does not try to change (or use fake HTML) to accomplish certain functionalities. Instead of trying to make HTML more powerful, REACT just handles HTML with Javascript. You don\'t need to learn new framework specific keywords, rules or syntax for conditional looping and so on. For example JS already has a function meant for iterating on top of an array, so in react we just use that.

 

**Summary:** Traditional Libraries put fake Javascript in HTML vs REACT which puts fake HTML in Javascript

 

![\"JS\" in HTML \<div \*ngFor=\"let user of users\"\> \<div v-for=\"user in users\"\> {{#each user in users}} \"HTML\" in JS {users.map(createUser)} ](000_Why_React-_009.png){width="5.508333333333334in" height="2.691666666666667in"}

 

**Quick ways to run a REACT app:\
** 

1.  Use: create-react-app

    a.  Single command: NPM start we can start a simple REACT app in our machine ready for development

    ```{=html}
    <!-- -->
    ```
    b.  **EACH COMPONENT IS ATOMIC:** it stands alone

    c.  Every time we save, changes are immediately reflected in the browser

    d.  If we make a simple html mistake (like closing a tag) within JSX, we get a compile time msg with the precise line where we made a mistake.

    e.  Debugging is also nicely handled:

        i.  ![](000_Why_React-_010.png){width="5.416666666666667in" height="2.933333333333333in"}

>  

2.  Codesandbox: online editor for quick experimenting with REACT

    a.  <https://codesandbox.io/>

 

**3. Corporate Investment**

Created and maintained by Facebook. But REACT is Open Source though. Because of Facebook DEEP commitment to keeping REACT stable on production when **breaking changes** occur in REACT, Facebook consistently provides a codemod that automates the change. **Command line tool that will automate the change in our code.**

 

![import React from \'React\' ; // later\... React . prop Types . string import propTypes from \'prop-types\' // later\... propTypes . string \< Warning in React 15.5+ Codemod update ](000_Why_React-_011.png){width="4.866666666666666in" height="1.5416666666666667in"}

 

**4. Community**

![React AJavaScript library for building user interfaces 3.14K 3.32K Stacks 4.95K 0 Integraticwis 77 okc Jobs 3.05K 2.99K COMPANIES us.NG RENE I Use This o 79.5K 15.1K Datadog Oaf.\"ogs Website See comparisons Of similar tools event sky ](000_Why_React-_012.png){width="2.825in" height="2.1666666666666665in"}

 

 

**5. Performance**

 

When REACT was created, one of the main elements that distinguish it from the competition is how fast and efficient it was. REACT developers were aware that JS was fast, but it\'s de DOM that makes it feel slow. Updating the DOM is expensive... so they started the use of the Virtual DOM.

 

**Without Virtual DOM:** Blindly update DOM using new state.

**With Virtual DOM:** Update the DOM in the most efficient way. For example this allow us to use layout thrash (When the DOM has to figure out the position of everything, once an element changes on the page.

 

![Duration in milliseconds ± standard deviation (Slowdown = Duration / Fastest) angiAM-v1. replace all rows partial row swap 2 create mæ•w rows append rows to large table rows • t•bk of 6.3-keyed 2518 2B .20 8.1 4.7 • l.s 7.4 ,2.4 3108.7 17.6 .37 4.9-keyed 1973 2012 ts.9 128 4.9 \*3.4 13.5 46.4 , 2.0 1866.7 365.1 389.9 104.9 2-0 arÜuIar-v4. .2.keyed 193.1 1974 13.0 3.4 \*2.3 13.4 461 , 3.2 1946.0 324.6 379.9 84.3 2.6 13.0 344.6 \'3.8 292.7 \*\'2.\' 17.1 8.6 \*2.4 164 , 32 25693 \* 524.2 , 23.6 (1.5 3039 glimme-v 0.3.10 3263 263.0 233 13.6 190 60,9 2543.4 \* 406 .34.\' (1.7) 209.0 80.4 t 38 2.0 knockout- va.4.1 3582 307 140 .4.s 11.4 \*2.6 14.7 3485.6 \* 579.6 603 2.10 pre#t-v7. 1.0 182.2 2009 tsa 8.7 138 4SS ,2.\' 1862.0 \* 349.0 332.1 442 .2.2 react-v1S. 5.4-keyed 188.9 201.0 les 8.8 \*3.4 14.7 472 1852.4 345.6 3984 70.0 llajs-k eyed 1385 1480 14.1 11.4 1331.1 \* we-a 3.3. 1667 168.5 \* 17.3 .2.• 18.3 .ts 52.6 ,2.\' 15875 295.3 \*12.8 399.5 74.8 .42 startup time 118.1 5.1 and 254.5 566 t2.s ](000_Why_React-_013.png){width="5.0in" height="3.7583333333333333in"}

 

**6. Testability**

 

![Traditional UI tests Hassle to set up Requires browser Slow Brittle integration tests Time-consuming to write, maintain React Little to no config required Run in-memory via Node Fast Reliable, deterministic unit tests Write quickly, update easily ](000_Why_React-_014.png){width="5.0in" height="2.033333333333333in"}

 

For REACT the vast majority of our components can be plain pure functions. Which means a given function always return the same value for a given input

 

![c Mocha QUnit Testing Frameworks o Jasmine AVA Tape vv Jest ](000_Why_React-_015.png){width="3.325in" height="2.066666666666667in"}

 

 
