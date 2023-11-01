05 - Creating Custom Angular Directives

Sunday, September 4, 2016

8:05 PM

**Why do we need directives?**

The easy answer to that is that when HTML was created it was never intended to have the features we have today. It was intended to create static documents...but before long we started to use it as a platform for collecting and showing dynamic data and documents. Evidence of our need to have more functionality through our HTML code can be found through Web Components.

**Web Components**

Allows us to create our own custom html elements with embedded functionality.

![Machine generated alternative text: \<element extends=\"button\" name=\"x-fancybutton\" constructor=\" FancyButton \" \> \<script\> FancyButton . prototype. razzle FancyButton. prototype. dazzle \</script\> \</element\> = function = function ](004_05_-_Creating_Custom_Angular_Directives_000.png)

The only problem with web components is that they are not supported with most browsers. Since they are only a draft from the people at W3 school. The solution to this: Angular Directives... which are commonly known to be more powerful and easier to understand than web components themselves.

In the past notes of this course we have already seen many instances of Directives working in our benefit by adding special elements to our page or eventual functions with the help of ng-click, etc.... Which allowed us to run our own fine functions when necessary.

![Machine generated alternative text: Uses for Directives Custom Elements Custom Events Observe and React to Changes ](004_05_-_Creating_Custom_Angular_Directives_001.png)

**How do we create a custom directive?**

Similarly as we did to add custom services with a **.factory** for our AngularApp object, we can just type **.directive** to add a custom Directive. The two inputs of that function call are:

1.  The new directives name

    a.  When writing the name in the JS file we can write it using camel case syntax BUT, once we go to our html code, Angular will turn the name divided into dashes

        i.  Example: \"myDirectiveName\" == \"my-directive-name\"

2.  Function to create the directive itself

    a.  The function will **return** a DIRECTIVE DEFINITION OBJECT.

    b.  A directive Definition Object has multiple properties like:

The LINK function:

> Our directive definition object will have a link method on it and that link element will take 4 parameters:

1.  Scope

2.  Element

3.  Attributes

4.  Controller

> In the example bellow we will just create a **var** element with the mark up text for what we want to reflect in our Angular Directive. In this case we will go with a simple input field. NOW, the interesting thing about this process is that we will need to tell Angular to process that markup using
>
> **angular.element(element).html(markup);**
>
> By doing this, we are telling Angular to look for the element we want and add the html code in our markup var inside of it.
>
>  
>
> We now have an interesting problem though. Our element officially has the markup code we wanted it to have BUT, we have yet to tell Angular that it needs to compile the code and check for any data bindings {{ }} in it.
>
>  
>
> ![Machine generated alternative text: 4 5 6 8 9 10 11 \'use strict\' eventsApp. directive( \'myDirective\' , function(){ return { link: function (scope, element, attrs, controller) { \'\<input type=\"text\" name=\"apple\" ng---model(test)/\> ; var markup angular. element (element) . html (markup) ; ](004_05_-_Creating_Custom_Angular_Directives_002.png)

> Will result in:
>
>  
>
> ![Machine generated alternative text: Home Create Event fsdff {{test}} ](004_05_-_Creating_Custom_Angular_Directives_003.png)
>
>  
>
> So, what is going on? Well, since Angular doesn\'t know that the markup actually contains some angular code it will not compile it.... So the fix would be:
>
>  
>
> ![Machine generated alternative text: 2 3 4 5 6 8 9 10 11 eventsApp. directive( \'myDirective\' , function(\$compile){ return { link: function (scope, element, attrs, controller) { \'\<input type=\"text\" name=\"apple\" ng---model=\"test\"/\> ; var markup angular. element (element) . (scope) ) ; ](004_05_-_Creating_Custom_Angular_Directives_004.png)
>
>  
>
> Keep in mind that the scope we are passing in the compile function is in fact the scope we inserted in the link function above. The scope for this example is the parent scope (or the scope of the page calling this directive BUT this might not always be the case)
>
>  
>
> The element is pretty much the element calling this directive... which in our case right now is our div.
>
>  

Now, what if we just wanted to create a directive called mySample instead of calling it in the div?

Well that is as easy as coming to the return object in our directive and typing:

> **return {**
>
> **restrict: \'E\',**
>
> **link: function ....**
>
> **}**

By default this value is \'A\' which means that it expects the directive to be used as an ATTRIBUTE... E pretty much forces the page to be used as an ELEMENT. We can also change it to \'C\' and introduce our new directive through a Class... which not only work the same but it would also give us a chance to change the css properties of our new element.

**Important:** If all we are going to do is replace the directory with some html... then we really don\'t need this complex system we wrote above. We can just used the **template** property of the Directive Definition Object to the HTML that we want to use. For this case we WOULD NOT need to compile the mark-up code we write... which is great.

There is one issue with creating directives the how we have done it so far... imagine we have the same directive in our page three times... well in that case since we only have one global scope surrounding our code, the data binding will work with every element in the page and if we change a variable connected to another output, it will reproduce the change across ALL other instances of that variable. It would look something like this:

![Machine generated alternative text: Home Create Event test test test ](004_05_-_Creating_Custom_Angular_Directives_005.png)

So, how do we fix this? Simple. When creating our custom directive we just need to set the isolated scope there. Inside this scope field in our custom directive we can provide properties as part of the isolated scope that map to the isolated html. In this case we don\'t need any.

![](004_05_-_Creating_Custom_Angular_Directives_006.png)

Now, if we added the above code to our existing custom directive we would run into an issue. In the above example we are setting the scope of our code right at the template level.... BUT with our event code, we are binding our variable to an already existing event (that we setup within our controller) ... Unlike other scopes within Angular, this scope will not inherit from its parent scope so we have to set it ourselves.

**Solution:** We just need to pass in our event (from ng-repeat) into our custom directive

![](004_05_-_Creating_Custom_Angular_Directives_007.png)

![](004_05_-_Creating_Custom_Angular_Directives_008.png)

Keep in Mind that we are setting the event: \_\_\_\_\_ equal to the attribute: **event=**\"...\" so as long as those match we are good to go. We will visit this in the future but, if we are setting the scope variable to the same name as what we set in our html element we don\'t need to repeat it\'s name we can just set it equal to \"=\"

> **event: \"=\"**
>
>  

![](004_05_-_Creating_Custom_Angular_Directives_009.png)

In the above picture we are passing in three different elements to our child scope. We do not need to specify the name of the attributes because they match with what we are declaring in our custom directive declaration....but we do deal with three different options:

1.  & - This symbol means we will run the function being passed in our PARENT scope NOT in the Isolated one we are creating

2.  = - This symbol allows us to send an object

3.  @ - This will pass the exact string in

**Creating Directives that listen to events**

![\'use strict\' eventsApp . directive( \' gravatar , 3 return { restrict : template: \'\<img / \> \' , replace: true, 1 1 14 1 1 function (gravatarUr1Bui1der) { link: function(scope, element, attrs, controller){ attrs .\$observe( \'email\' , function(newvalue, oldVa1ue) { if (newVa1ue !== oldVa1ue) { attrs.\$set( src gravatarUr1Bui Ider. buildGravatarUr1 (newVa1ue)) ; ](004_05_-_Creating_Custom_Angular_Directives_010.png)

**Isolated Controllers Inside Custom Directives**

So far we have seen (with the up vote methods above) how to use the parent controller to run various functions that we need within our custom Directive elements. But, how about if we want to have our own controller to Fully encapsulate the logic of our directive. Simple, we would just need to add the controller attribute to our directive\'s code and it\'s done:

![events App . directive ( \'greeting\' , return restrict: \'E\' replace: true, function ( ) template: \"\<button class=\'btn\' sayHe110() \'\>Say controller: function (EZE) { Sscope.sayHe110 = function ( ) { alert ( ) ; 1 n: ](004_05_-_Creating_Custom_Angular_Directives_011.png)

Or even Simpler:

![events App . directive ( \'greeting\' , return restrict: \'E\' replace: true, function ( ) template: \"\<button class=\'btn\' ng-click=\' sayHe110() \'\>Say controller: \'GreetingContrc11e eventsApp. controller ( GreetingContr011er , function GreetingContr011er(é.E.QE) sayHe11c = function ( ) alert ( ](004_05_-_Creating_Custom_Angular_Directives_012.png)

**Sharing Controllers among Directives**

Sometimes we might want to have different directives share the same controller. That way we can save a lot of time if we are using the same method all around with minor tweaks. For example, lets say we have a Say hello Directive we have implemented in our code that uses a Greeting controller. If we later on add different other attributes (for this example we can have them be ATTRUBUTES but they can be any type of directives) then we just need to set the **require** element in our custom directive to be the same name as the desired directive (parent with an EXISTING) controller... and we are done. Our child directive will automatically have this new controller wired up to be used.

Now, lets say we want to have some changes to the method we are trying to use in our child directives, please view the bellow example to see how simple this can be achieved:

**Note:** Notice how we are using (for the first time in my notes) the controller attribute in the Link element of our controller.

![events App . directive ( , function ( ) return restrict: \'E\' replace: true, template: \"\<button class=\'btn\' \'\>Say controller: function { Var greeting 3 = \[\'hello\'\] : = function() ( alert (greetings. join ( ) ; this. addGreeting = function gree tings . push ; 1 1) .directive ( \'finnish\' , function ( ) return restrict: requi re : \'greeting\' , Link: function ( scope, , addGreeting ( \' hei \' ; .directive( , function() return restrict: require : \'greeting\' , link: function gpntroller. addGreeting( ) ; ](004_05_-_Creating_Custom_Angular_Directives_013.png)

Priority: One important note about having multiple attribute directives on an element and we would like to execute one before the other we need to play with the **priority** option in out directive. We can just give it **priority: 1** and that will automatically work for what we need.

Terminal: If we set **terminal: true** as one of our options in our custom directive. We will be forcing the directive to not execute (use) any of the directives that have a priority with a value less than the one with the terminal option.

**Using Require (for controllers) with Nested Directives**

In simple words, what about the case in which we are trying to \"require\" a controller in a directive that is not found within the same element of our current directive. In such instances we would just need to do something like:

**Require: \^directiveName**

And this way our directive will go up the scope are currently dealing with until we find a directive with the name that we have specified and we take in it\'s controller.

![.directive ( \'hindi \' , function ( ) return restrict: requi re : •greeting\' , link: function ](004_05_-_Creating_Custom_Angular_Directives_014.png)

**IMPORTANT:** In order to nest directives inside other directives we need to use **TRANSCLUTION**

**Transclusion:**

The word transclusion typically refers to taking a portion of a document and embedding it inside another element. With Angular, we will think of it as taking HTML and embedding it into a Directive.

![event---App. directive ( , function ( ) return restrict: \'E\' replace: true, template: \'\<divxh4 {title) , sccpe: title: \'@\' n; ](004_05_-_Creating_Custom_Angular_Directives_015.png)

In the above image we have a custom directive called \<collapsible\> found in one of our html templates. Within that directive I have written various elements that seemed to work before. BUT, since we added this template inside our Custom directive with the Title value.... All the other information in the html page is GONE. So, what happens, how can we get the code we write as our template in our Custom directive and still maintain the code found within our html?

Answer: Transclusion

> ![return { restrict : replace: true, template: class=\"we11-tit1e\"\>{{tit1e}}\</h4\>\<div , transclude: true, scope: { title: ](004_05_-_Creating_Custom_Angular_Directives_016.png)

Keep in mind that once we tell our directive that we are going to be using transclusion we need to also specify where in our template code will we insert the html code.

**Using the Compile Function to transform the DOM**

So far we have used the link function all over our custom directives. The link function has allowed us to play with the DOM after the directive\'s code has been executed. For example we went over watching events and reacting to certain user actions in our page. The **compile** function in a custom directive can be though as the link function that runs PRIOR to the directive executing.

![eventsApp.directive ( repeatX\' , function (Eæüg) return for (var i=o; \< i\*+) \[ element. after clone ( ) . attr ( repeat---x\' , 1 ](004_05_-_Creating_Custom_Angular_Directives_017.png)

So, lookinjg at the image above... we are trying to clone a tag a certain amount of times.... But, without the compile function, we we had any piece of Angular code within the cloned element it would just show up as plain html since Angular would not know to compile it in the first place.

In the image above we see how we tried to compile the element every time we do a clone.....and this works BUT..... The \$compile function is quite an expensive one. Anguler would need to go and parse the whole DOM file and examine for everthing before doing each compilation and in the long run this could be really problematic.... So the solultion to this problem lied in separating the compile function from the link function all together.

![eventsApp.directive( \'repeatx•, function(){ return { compile: function(element, attributes) { for (var i=e; i\<Number(attributes. repeatX)-1; i++){ element. . attr( \'repeat-x\', 8) ) ; ](004_05_-_Creating_Custom_Angular_Directives_018.png)

The above image will result in the same output as the link function but in a way more efficient way. Keep in mind that the compile function will only take in the element and attributes inputs. We will not have any access to the scope of the function since nothing has been output yet.

The compile function only runs ONCE and affect all instance of the directive in the same way and that the link function will run individually for each function.

Compile function can ALSO return values. From the compile function we can return the LINK function:

![eventsApp.directive( \'repeatx•, function(){ return { compile: function(element, attributes) { for (var i=e; i\<Number(attributes. repeatX)-1; i++){ element. after(element.clone() . attr( \'repeat-x\', 8) ) ; return function (scope, element, attributes, controller){ attributes.\$observe( •text\' , function(newVa1ue) { if (newVa1u \'John element. css( color\' , \'red\'); ](004_05_-_Creating_Custom_Angular_Directives_019.png)

**Making Jquery more EXPLICIT with directives**

We can use Jquery plugin alongside AngularJS directives and in fact directives can make our Jquery plugins more explicit

**Summary**

![Custom Elements Observe and React to Changes Handle Events Make jQuery Plugins Explicit ](004_05_-_Creating_Custom_Angular_Directives_020.png)

44
