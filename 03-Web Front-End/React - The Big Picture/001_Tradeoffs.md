**Tradeoffs**

Monday, January 21, 2019

3:30 PM

![Tradeoffs Framework Concise Template-centric Separate template Standard Community backed Library Explicit JavaScript-centric Single-file component Non-standard Corporate backed ](001_Tradeoffs_000.png)

 

**1. Framework vs Library**

Frameworks contains more opinions, so we will avoid spending time trying to choose between many options... which reduces fatigues and has less setup overhead. Not to mention more consistency...

 

REACT on the other hand is significantly smaller than most frameworks. **This allows us to sprinkle REACT components on existing applications** without worrying about cluttering our codebase. REACT allows you to only pull in the feature that you need to keep the app lean and fast to prioritize **performance.**

 

![Framework Clear opinions Less decision fatigue Less setup overhead More cross-team consistency Library Light-weight Sprinkle on existing apps Pick what you need Choose best tech Popular boilerplates exist ](001_Tradeoffs_001.png)

 

![Components Testing I-IT TP library Routing 118n Animation Form validation CLI Features React Jest, Mocha Fetch, Axios React Router react-intl react-motion react-forms create-react-app Angular angular-cli ](001_Tradeoffs_002.png)

 

**2. Concise vs Explicit**

 

With REACT we control what should happen on EVERY event. This means we can TRANSFORM and VALIDATE inputs before updating STATE and perform PERFORAMNCE optimizations as desired. We end up having to write more explicit code, but it helps with debugging.

 

Note that you can write single change handlers for an entire form. No need to write a handler PER input field!\
\
 

![Two-way binding Less coding Automatic let user --- - •cory\'; \<input type=\"text\" value={user} Don\'t worry, you can declare one per form. O One-way binding More control More explicit Easy to debug = { user: \'Cory\' } ; state function handleChange(event) { this. setState({ user: event. target. value \<input type=\"text\" state. user} hand leChange} ](001_Tradeoffs_003.png)

 

**3. Template-centric vs JavaScript-centric**

\* Already mentioned earlier: Angular and Ember for example look to make HTML more powerful, but adding their own unique syntax to the HTML code. REACT instead utilizes the power of JS to handle HTML. This is what makes REACT so elegant.

 

**Conditionals:**

 

![\<hl Admin\</hl\> \<hl v-if=\" isAdmin\"\>Hi Admin\</hl\> \<hl\>{{if isAdmin {isAdmin \'Hi Admin Since plain JS, you get: 1. Autocomplete support 2. Error messages ](001_Tradeoffs_004.png)

 

**Loops:**

 

![\<div user of \<div v---for=\"user in {{#each users as I user l}} {{/each}} users.map(user ](001_Tradeoffs_005.png)

 

**Events:\
\
** 

![\<button ) \<button \<button \<button \' de ](001_Tradeoffs_006.png)

 

 

**Pros / Cons**

 

![Template-centric Little JS knowledge required Avoid confusion with JS binding Rule of least power JavaScript-centric Little framework-specific syntax Fewer concepts to learn. It\'s JS. Less code Easy to read Encourages improving JS skills Skills transfer ](001_Tradeoffs_007.png)

 

**4. Separate Template VS Single File for a component**

 

Taking into consideration how patterns like the Model, View, Controller have grown in popularity across the industry, when REACT was originally introduced there was a A LOT of skepticism. After all, REACT will make the developer have everything about a component, EVEN the JSX code within just one file. This approach, among many others, creates concern about the standard **separation of concerns** design we have been so used too. In Web development separation of concerns looks more like having each tech in different files. **HTML, CSS, JS.** In REACT, the developers decided that separation of concerns is still a thing when it comes to **Components.** They have their own logic to be used, their own use cases.... Technologies is not that relevant and even sometimes gets things more confusing.

 

![HTML Separate technologies, css but intertwined concerns. JS Each component is a separate concern. 0 ](001_Tradeoffs_008.png)

 

-   Think of REACT components like Russian dolls

 

**5. Standard vs Non-Standard**

 

REACT is one of many non-standard component libraries out there.

 

What is a **Web Component?**

 

![Templates Custom Elements Shadow DOM Imports Inert, reusable markup Define our own elements Encapsulated styling Bundle HTML, JS, & CSS ](001_Tradeoffs_009.png)

 

Sadly, though having a standard across our code would be greatly beneficial... These web component standards have yet to be embraced by the development community. Why NOT? **Browser limitations\
\
**<https://caniuse.com/>

 

![Web Components Templates Custom Elements Shadow DOM Imports React JSX, JS Declare React components CSS modules, CSS in JS, \"inline\" One component per file ](001_Tradeoffs_010.png)

 

In Summary, Web Components uses nothing NEW compared to REACT today.

 

![Why Not Web Components? Spotty browser support = polyfills req\'d Doesn\'t enable anything new JS libraries keep innovating Only run in the browser ](001_Tradeoffs_011.png)

 

![Non-standard Today, the majority use these. Why? 1. Faster innovation 2. Strong user and developer experience 3. Broad browser support ](001_Tradeoffs_012.png)

**6. Community vs Corporate**

![Corporate Backed Driven by FB\'s needs Full-time development staff Over 1,000 contributors FB: World\'s 5th most valuable company 30,000 components in prod ](001_Tradeoffs_013.png)

 
