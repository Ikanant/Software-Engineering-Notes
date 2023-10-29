Displaying Data and Responding to Events

Saturday, September 21, 2019

8:00 PM

 

The mechanism that allow us to accomplish the title of this section is Data Bindings and Event Handlers.

 

![How do we display data? How do we allow the user to edit data? How do we make the UI change based on data? How do we handle user interactions? ](001_Displaying_Data_and_Responding_to_Events_000.png){width="6.4in" height="3.425in"}

 

![-bind github\" target=\" \_blank\' \> class= \" fab fa-github fa-2x\"\>\</i\> \<a \"twitter\" target= \" \_ blank \" \> \<i class=\"fab fa-twitter fa-2x\"\>\</i\> Full v-bind syntax Shortcut syntax ](001_Displaying_Data_and_Responding_to_Events_001.png){width="8.066666666666666in" height="2.2916666666666665in"}

 

Looking at the above code it is pretty straight forward how we get things binded in our html code. With vue with have the option to use v-bind (Keep in mind that v-something it\'s a sign that we are dealing with a vue owned directive) we can bind whatever variable we want that\'s setup within our script tag (export section for the component itself).

 

![](001_Displaying_Data_and_Responding_to_Events_002.png){width="6.491666666666666in" height="3.7583333333333333in"}

 

It works something like the code above. We have 2 variable strings that lead to different sites that we specify through the data function on our component declaration.

 

[What else can might we want to bind?]{.underline}

In the example above I am binding an ancher tag.. But we can also bind to a CLASS, or maybe an image tag and we want to bind to the src property... all these are valid scenarios

 

**Displaying Text**

Alright, but let\'s say I want to show some value out of a variable within my component.... Binding is not what we want in this case... The way to accomplish this is by using INTERPOLATION. We are gonna get some properties from our model in order to display data in our page. We will accomplish this, similar to Angular with double curly braces {{ }}

 

Notice that we CAN use regular binding by doing something like v-text... but using curly braces makes things a bit simpler.

 

One thing I noted a bit fast before is the DATA MODEL of our component... (the data function)... This is a VERY important aspect of VUE components because it holds all the data the component is using at a given time. **The data model comes from a data function** that returns an OBJECT that contains the PROPERTIES that we consider our data. Take:

 

![\<div\>Hello \< / template\> \<script\> export default name data() { return name : Display models with {{ model Can also use v-text=\"model\" Also known as interpolation The data() function identifies the data models \" John \" ](001_Displaying_Data_and_Responding_to_Events_003.png){width="6.95in" height="3.158333333333333in"}

 

 

 

**Handling Events**

 

Now, I would like to capture whenever an event happens inside my component. Like a click or a text typed in a input box. The way to do that is by using VUE\'s directive v-on. Then the name of the event (like click) and then the name of the function we would like to call when the event happens

 

![heroes.vue Event Bindings Execute when an event occurs \<input v-model=\"name\" type= \"text\" \> v-on:event=\"method-name\" \<button /button\> @ is the shortcut syntax for v-on escript\> export default { data() { methods : ok() { return { name: \" John\" Y ; do something ](001_Displaying_Data_and_Responding_to_Events_004.png){width="7.258333333333334in" height="4.041666666666667in"}

 

Now... Looking at the picture above one thing to note is that I am not using v:on ..... Just like v-bind has a shortcut syntax as : v-on has the same with the @ character.

 

One other thing to not is that on the function name that we are passing to the \@click directive, we are NOT adding parenthesis to our function name... this is not necessary, but adding them would not hurt. This is helpful in the case that we want to pass in a value to the function we are in the process of calling when handling an event. This is more of a convenience deal.

 

**Two WAY binding:**

 

![Two-way Binding The hero.firstName is shown in the input The user types and the value of hero.firstName changes heroes.vue \<div class=\"field\"\> \<label class=\" label \" \<input class=\" input\' Two-way binding for:\" firstName\" \>first name\</label\> id=\"firstName\" v-model= \"hero . firstName \" ](001_Displaying_Data_and_Responding_to_Events_005.png){width="6.633333333333334in" height="3.8666666666666667in"}

 

 

**In summary:**

 

![\@event :property v-model Interpolation Handle an event Bind to a property Two-way binding ](001_Displaying_Data_and_Responding_to_Events_006.png){width="4.8in" height="4.5in"}

 

 

**Displaying Lists and Conditional Content**

 

Three main things to consider here:

1.  How do we display lists?

2.  How do we add content to the DOM when needed?

3.  How do we hide and show content THAT\'S ALREADY IN the DOM?

>  

![\< Ii in heroes\' { { hero.name } } \</li\> Render a List : key- - \" hero . Iterate over a list of items in a model with v-for=\"item in item-list\" Repeats the HTML content for each item in the list Bind to a unique :key, for faster rendering ](001_Displaying_Data_and_Responding_to_Events_007.png){width="6.966666666666667in" height="3.966666666666667in"}

 

 

Note the :key property. That\'s gonna be the unique identifier for each hero. This will help us out so that VUE can swap values in and out of each row as they change (or if they change). It is essentially a way for vue to identify each row uniquely.

 

 
