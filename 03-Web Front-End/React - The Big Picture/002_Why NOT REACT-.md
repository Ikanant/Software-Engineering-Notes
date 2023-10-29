**Why NOT REACT?**

Monday, January 21, 2019

8:30 PM

 

**1. JSX Differs from HTML**

 

I already wrote about the uses of JSX vs HTML in the previous page of this NOTE.. BUT a valid concern is: **What happens with the lots of HTML that we have to convert?**

 

![Ctrl+F find/replace HTML to JSX Compiler Online compiler htmltojsx on npm ](002_Why_NOT_REACT-_000.png)

 

**2. Build Step Required**

 

As mentioned before, we need to compile JSX code to plain Javascript calls so the browser can understand it.

 

![Minify Transpile Test and lint ](002_Why_NOT_REACT-_001.png)

 

![Babel Typescript Both transpile JSX ](002_Why_NOT_REACT-_002.png)

 

**3. Version Conflicts**

We CAN\'T run 2 version of REACT at the same time on the same page. This means we have to keep REACT components on the same version throughout.

 

**4. Old Stuff Online**

 

REACT has a huge community online and it has evolved since it was open sourced by Facebook. Searching for REACT example on Google and we get million of results (no different from Angular really).

 

Many Resources is great no? well, some of that content is outdated. So when searching the web for REACT topics we have to be careful not to run into patterns that are no longer popular today.

 

Features have been extracted from REACT Core

 

![Features Extracted from React Core Old import {render} from React. createClass \' react\'; import {render} from \' react---domi var crc = require( \' \' ) ; import {PropTypes} from mixins: \[mixinNameHere\] \' react\'; import PropTypes from \'prop-types \' ; Higher order components, render props ](002_Why_NOT_REACT-_003.png)

 

**5. Decision Fatigue**

 

REACT is a small non-opinionated library, so it is quite easy to do the same thing in multiple ways.

 

-   **Dev Environment**

    -   \>100 boiler plates for starting REACT projects.

        -   Some of these are limited though. For instance the popular **create-react-app** does not include tools like React Router (Routing) OR Redux (State Management)\
             

-   **ES Class or Original Create Class syntax**

    -   ![createClass ES Class = require( ) ; var createReactClass = createReactClass({ var Greeting render: function() { return \<h1\>He110\</h1\>; import React from react\' ; class Greeting extends React. Component { render() { return \<h1\>He110\</h1\>; ](002_Why_NOT_REACT-_004.png)

-   **Types**

    -   PropTypes

        -   ![import React from \"react\"; import PropTypes from \'prop---types\' ; function Greeting(props) { return ( \<h1\>Hello {props. name}\</hl\> { Type checked at runtime Greeting. propTypes = name: PropTypes. string ](002_Why_NOT_REACT-_005.png)

        -   With PropTypes Types are checked at run time and ONLY during development

    -   TypeScript

        -   Super set of Javascript

        -   ![import \* as React from interface Props { name: string function Greeting(props return ( \" react\" ; . Props) { Type checked at compile {props. name}\</hl\> ](002_Why_NOT_REACT-_006.png)

    -   Flow

        -   You add type annotations to plain JS and flows infers types throughout our codebase

        -   You annotate the files we want to be checked

        -   ![// \@flow import React from type Props { name: string \" react\" ; Type checked function Greeting(props: Props) { return ( \<h1\>HeIIo {props. when you run flow ](002_Why_NOT_REACT-_007.png)

-   **State Management**

    -   State: Our App\'s Data

    -   Plain REACT, Flux, Redux and MobX

    -   ![State Management Popular Flux alternative Plain React Component state Flux Centralized state Redux Centralized state MobX Observable State ](002_Why_NOT_REACT-_008.png)

-   **Styling**

    -   Use whatever you know today. REACT works great with CSS, SCSS, etc...

 

 

![Decision Dev environment ES Class vs createClass Types State Styling Recommendation create-react-app ES Class PropTypes Plain React What you already know ](002_Why_NOT_REACT-_009.png)

 

 

![Summary JSX differs from HTML - Easy to convert Build step is typically required - You need a build step anyway Potential version conflicts Easy to upgrade via codemods Old features in searches Note features extracted from core Decision fatigue - Start simple - Add complexity as needed ](002_Why_NOT_REACT-_010.png)

 
