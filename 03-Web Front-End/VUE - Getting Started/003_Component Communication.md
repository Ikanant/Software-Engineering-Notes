Component Communication

Monday, January 20, 2020

5:08 PM

 

![000 How do we Create a parent and child component relationship? Pass values from a parent to a child component? Create and fire events in child components Listen to those events in the parent component Refactor one component into parent and child components Share logic across components ](003_Component_Communication_000.png)

 

Creating component trees (or in other words consuming components from within another other vue components) is very self explanatory... there is only ONE thing to keep in mind... we can\'t just add the component inside our parent component html code. We first need to tell our parent component about our new child one by importing it and declaring it in our **components** property of our parent component:

 

![12 13 14 15 16 17 18 paagLEVS \< / template\> tmport heoderBar from \'û/components/headel-bar import Heroeô from ; export default { \'App\', name: components: { HeaderBar, \< / script\> Heroes output OEHLJG CONSOLE TERMINAL ](003_Component_Communication_001.png)

 

 

**Passing values from parent components to child components**

 

![\<HeroDetaiI v- \" selectedHero \" : hero=\" selectedHero\" hero-detail.vue export default props: { hero: { type: Object, default: ( ) o, ](003_Component_Communication_002.png)

 

\^\^\^ We are essentially binding variables on our parent component and having them be \*props\* in the child one.

 

![Casing Types Dynamic vs Static Prop Tips camelCased prop names use kebab-cased equivalents in templates String, Number, Boolean, Array, Object, Function, Promise Dynamic: : title= \"hero. name\" Static: title=\"Mrs Awesome\" Use v-bind (or : ) with static non-strings ](003_Component_Communication_003.png)

 

![Validation Any string, or undefined, null Default value generated from a function Simple default value This prop is required Child Component props: { message: String, hero: { type: Object, default: ( ) =\> { } limit: { type: Number, default: lee title: { type: String, required: true ](003_Component_Communication_004.png)

 

Now when passing in props to our subcomponents we have to be very careful. In essence... if we pass in an object as a prop to our sub component, and in fact this sub-component changes this object, the parent component will be affected by this change and could potentially cause problems in our code. This should not be mistaken by a two way binding architecture though.... As soon as the parent component re-renders... the data will then be passed in again to our sub-component and we will see the parent content again.

 

![\<HeroDetai1 : hero= \" selectedHero \" \" saveHero\" Method in heroes.vue which accepts the parameters hero-detail.vue methods: { saveHero() { .\$emtt(\" save \" , this. theHero) ; Pass the hero from the child component Fire the event ](003_Component_Communication_005.png)

 

 

**Sharing logic between components**

 

This can be accomplished BOTH by sharing modules... but also using something called mixins.

Mixins allow us to share different parts of components across MULTIPLE components. We can take things like methods, computed, lifecycle hooks, etc... and share it between multiple components.

 

![Mixins Distribute reusable functionality across components Example: methods, computeds, life cycle hooks, data, watches my-mixins.Js export const mymix = { created() { console. log(\'created lifecycle methods: { clear: function() { this unselect\' ) ; hook\' ); heroes.vue import { mymix } from export default mixins: \[mymix\] , \' ./my-mixins\' ; This mixin is merged into this component ](003_Component_Communication_006.png)

 

Mixins will be MERGED into the component... what about if already have some of the methods declared in the mixin inside of the component?

 

![methods, components and computeds data watch and hooks Merged, precedence given to the component\'s method Merged superset, precedence given to component\'s data Both run, with mixins running before component ](003_Component_Communication_007.png)
