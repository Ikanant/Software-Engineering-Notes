General Notes

Tuesday, March 19, 2019

8:13 PM

![Uses babe/ used to convert .jsx and ES6 files into Js files Webpack Bundles set of files connected by import statements into one file Uses webpack-dev- server plugin to create convenient environment ](000_General_Notes_000.png){width="5.516666666666667in" height="2.933333333333333in"}

 

 

 

![Install Webpack, Babel and other libraries needed for bundling and transpilation Create . babe 1 rc file to define how .jsx and ES6 should be handled Create webpack. confi g. js file to describe how our app should be bundled Create stubs for index . html and i ndex.js, which will form the basis of our app On completion, app should say \"hello world\" in JS and HTML ](000_General_Notes_001.png){width="5.341666666666667in" height="3.966666666666667in"}

 

![Overview of Redux Manages underlying data Application state can be easily accessed Changing application state occurs only via actions Redux state is provided to React components via React-Redux, a small connector library ](000_General_Notes_002.png){width="4.95in" height="2.7583333333333333in"}

 

 

![Create default application state as JSON file for development Create basic Redux store to provide state to application as necessary Changes to state (mutations) will be added later ](000_General_Notes_003.png){width="4.791666666666667in" height="1.9166666666666667in"}

 

.

![](000_General_Notes_004.png){width="5.0in" height="2.475in"}

 

![Reducer must be updated to allow tasks array to be changed Adding New Tasks Tasks need random ID, reducers can\'t be random, therefore Saga or Thunk is needed Updated state is reflected automatically in React component appearance ](000_General_Notes_005.png){width="5.0in" height="2.75in"}

 

![O Sagas run in the background of Redux applications Sagas in Brief O O Respond to actions by generating \"side- effects\" (anything outside the app) functi on\* One of only a few places where generator functions are found ](000_General_Notes_006.png){width="5.0in" height="2.625in"}

 

![Standard JavaScript functions (non- generator) return a single value, instantly Generators in Brief Generators can return any number of values, not just one Generator values can be returned at a later time (asynchronously) ](000_General_Notes_007.png){width="5.0in" height="2.591666666666667in"}

 

![myGenerator(){ function\* let meaning = 42; while (true) { meaning 1; yield meaning ; function\*indicates special generator function type \< generator contains normal javascript code while (true) loops can exist in generator functions Yield keyword returns value to the generator\'s caller (can return many values) Yields 43, 44, 45\... ](000_General_Notes_008.png){width="5.0in" height="1.9083333333333334in"}

 

![](000_General_Notes_009.png){width="5.0in" height="2.325in"}

 

 
