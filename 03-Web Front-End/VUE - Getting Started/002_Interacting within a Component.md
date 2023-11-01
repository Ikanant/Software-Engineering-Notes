Interacting within a Component

Wednesday, January 15, 2020

8:51 PM

![000 000 000 define data models? define functions to for a component? tap into specific events in the component life cycle? define custom properties that react to model changes? run custom logic when model\'s change? format data for the users? ](002_Interacting_within_a_Component_000.png)

**Data Models:\
**The most important piece of a component is the DATA itself...

I\'ve already noted things about the data function inside of a component... the data function returns PROPERTIES or MODELS that the VUE reactivity system can see...

VUE\'s reactivity system keeps and eye on these properties in order to update the view of the component accordingly.

![data() { return { heroes: selectedHero: message: undefined, Component\'s data model Function as a best practice Vue reacts to changes in all defined properties ](002_Interacting_within_a_Component_001.png)

**Computed Properties**

These are properties that can calculate their value. A computed property is created inside of the component AND it will fire whenever any dependency value changes... (NOT ALL THE TIME).... And it caches the value based on other dependencies....

![heroes.vue computed: { fuLLName() { When either dependency changes, the computed evaluates return hero. firstName} \${this .hero. LastNameF ; ](002_Interacting_within_a_Component_002.png)

\^\^\^ The above syntax is the default way to create computed properties.... BUT we can also use GETTERS and SETTERS to perform the same type of task...

![Computed get/set Use get() to compute the value Create getter and setter functions Use set() to modify computed dependencies computed: { fullName: { get() { Let value = this. first; value this. Last ? \${this. Last}\' return value; set(value) { Let names this. first this. Last = vaLue.spLit(\' = names\[0\]; = names . length names \[names . length - 1\]; ](002_Interacting_within_a_Component_003.png)

**Lifecycle Hooks**

There are the functions that run when a component gets rendered/added to our DOM.

Hooks:

-   beforeCreate & created

    -   At this point the DOM is NOT yet created. We can\'t manipulate anything inside the Template BUT we CAN retrieve data from an API for example to get our DATA

-   beforeMount & mounted

    -   This is often where we want to interact with 3rd party components... So if we are using a Jquery UI component for example or just plain old JS sometimes we need to grab that code and mount it somewhere specific in the DOM...

-   beforeUpdate & updated

    -   These are the ones we deal with when our data changes

-   beforeDestroy & destroyed

    -   These are for doing any cleanup that we might have3

![created Invoked when the component is created Frequently used to fetch data for your component Templates and virtual DOM are not yet mounted nor rendered eroes.vue created() { this. getHeroes() . then (heroes this. heroes = heroes ; ](002_Interacting_within_a_Component_004.png)

**Watching Properties**

In Vue there is a reactivity system that\'s always watching our model... we can do this too.... Using watchers.

For these watchers we need the value the SAME as the reactive value that we want to watch.

If we need to watch dotted properties, then we just use quotes.

![watch: { hero(newVaIue, oldVaIue) { console. log( old=\$ {oldVaIue}, // execute Logic \' selectedHero. capeCounter \' : immediate: true, handler(newVa1ue, oldVa1ue) { // execute Logic ---\${newVaIue} new--- React when this model changes React to data changes Named same as reactive value Accepts new and old values Ideal for asynchronous operations i Use quotes when needed ](002_Interacting_within_a_Component_005.png)

**Filters**

![filters: { capitalize: function(value) { if (!value) return value = vaLue.toString(); return value . charAt(Ø) .toUpperCase() + vaLue.sLice(I); Filters Local filters are defined in a component Apply in the template {{ firstName I capitalize Filters can be chained {{ firstName I capitalize I reverse Optionally pass arguments {{ someDate I myDateFilter(\'MM-DD-YY\') ](002_Interacting_within_a_Component_006.png)

![import Vue from •vue• ; Vue.fiLter( capitalize\', function(value) { if (!value) return value = value. toString(); return value. charAt(Ø) .toUpperCase() + value.sLice(1); Global Filters Define once, use everywhere When defining a global filter, it must come before the Vue instance ](002_Interacting_within_a_Component_007.png)
