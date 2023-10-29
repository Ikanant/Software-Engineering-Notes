02 - Markup & Controllers

Wednesday, August 24, 2016

4:43 PM

 

**Controllers & Scope**

 

Controllers primary responsibility is to create a SCOPE object.

 

A scope object is how we communicate with the VIEW. The Scope is able to communicate with the View through 2-way communication. The can bind combines the properties &results of functions in the Scope. Events on the View can call methods on the Scope. Data passes in this way through the Controller to the Scope, and form the Scope to the View.

 

The Scope is used to expose the MODEL to the view. But the Scope is not the model. The model is the data that is put on the Scope. If we want to modify the Model we can either use methods that are found on the Scope (perhaps in response to Events fired by the View) or using 2-way bindings. In this way users through the view can make modifications to the model (or data).

 

**Built-in Directives**

 

Directives: Directives are a way to teach HTML new tricks. Directives give HTML new functionality. As Angular parses through our HTML it will look for Directives and then activate some actions based on what it finds. For example if it finds an \"ng-click\" it will register **a click handler event** on that DOM object.

 

There are actually **FOUR** ways to specify directories in Angular:

 

1.  \<ng-form /\>

    a.  Tag itself.

2.  \<div ng-form /\>

    a.  Directives can be attributes of a tag

3.  \<div class=\"ng-form\" /\>

    a.  As a class itself.

 

Keep in mind not all directives can be written in all three of these forms...More often than not we can only write certain directives in 1 or 2 ways shown above.

 

4.  The fourth way of way of writing a directive is inside an HTML comment. This way of doing things is outside of the scope of this course so it will only be mentioned but not down in actual code.

 

**Event Directives**

 

-   ngClick

-   ngDblClick

-   ngMousedown

-   ngMouseenter

-   ngMouseleave

-   ngMousemove

-   ngMouseover

-   ngMouseup

-   ngChange

    -   ngChange will detect a Change event in a lot of different HTML input elements

    -   **Requires** that the ngModel directive is ALSO present on the TAG.

 

**Other Directives**

 

-   ngApp

-   ngBind

    -   We could assign values from our scope variables to our HTML objects:

    -   \<h2 ng-bind=\"event.name\"\>\</h2\>

-   ngBindTemplate

    -   Same as bind but we can put multiple items in here

    -   \<h2 ng-bind-template=\"{{event.name}} {{event.date}}\"\>\</h2\>

-   nngBindHtml

    -   Not actually in the MAIN Angluar Script file. Instead it is in the Angular sanitize file. We would need to add the file in our html scripts AND add it as a dependency in our app.js file...

    -   **Var** eventsApp =angular.*module*(\'eventsApp\',\[\'ngSanitize\'\]);

    -   The Sanetize module will look into the html code we are injecting and remove every \'style\' out. Cleaning our code a bit.

-   ngBindHtmlUnsafe

-   ngHide

-   ngShow

    -   Hide and show work like if statements to Hide and Show elements. They are pretty much the same but are mirrors of each other. Code with this directive will include a \"display: none\" code

-   ngCloack

    -   This will take care of holding on showing certain elements in our page until the rest of the elements are rendered/shown. This will let us avoid having random flashes within the page at different load times.

    -   We often add the ngCloak directive over in the body of the html code to cover up everything.

    -   Another option towards towards this subject is also to just write the Angular script code on top of the html code to achieve a similar result.

-   ngStyle

    -   ngClass

    -   ngClassEven & ngClassOdd

        -   These can be used for cases in which

 

-   ngDisabled

-   ngChecked

-   ngMultiple

-   ngReadonly

-   ngSelected

    -   All these directives take in True or False for their paramenters

>  
>
>  

-   ngForm

    -   The reason for this directive is because HTML does not allow any form to be nested.

    -   ngForm can be nested inside of other forms

-   ngSubmit

    -   A lot like the event directive shown above. Only this one allows us to call a method in our scope if the form is submited. If the form is submited, instead of submiting the form, it will call our function first.

-   ngHref

-   ngSrc

    -   For but ngHref and ngSrc the main idea is that if we have the \"source\" or \"refernce\" to an image or an ancher tag that is a variable determined within Angular, this directives will make sure to be added right on time so that we do not face empty images or wrong urls inside \<a\> tags

-   ngNonBindable

    -   This one will specify an area that might normal but that we have told Angular to not Parse and just do the Binding that happens inside this directive.

    -   Lets say we have {{1 + 2}} inside a text field, if we add ngNonBindable to to that field, the result in our page will display {{1 + 2}} instead of 3. Angular will simply just skip that element and not consider it an expression

 

**Expressions**

 

Are JavaScript like code snippets that we can put inside the HTML of our page. They are generally placed inside of bindings.

 

Expression can incorporate more than just variable names

 

Expressions are NOT fully using JavaScript syntax. We cannot call functions on the object or call an alert inside of an expression

 

**Filters**

 

Filters are a way to tell Angular that we want to modify something for output. Filters can do 3 main things:

1.  Formating

    a.  Making Strings uper case or formating numbers around

    b.  Sort records in a Data set. So when records are rendered they are rendered in the order that we want.

    c.  Filter the records in the data set

 

**Using Filters**

 

To do a filter we just need to add \'\|\' character and then name the filter we want to use.

 

![Machine generated alternative text: Using Filters expression I filter } } ](001_02_-_Markup_&_Controllers_000.png)

 

**Writing Custom Filters**

 

![Machine generated alternative text: module. filter( \'name\' , function() { return function(input / \* , filter parameters \*/) { // modify input return modifiedOutput; ](001_02_-_Markup_&_Controllers_001.png)

 

 

**Two Way Binding**

 

Allow us to use the Typical Form controls and keep our model up to date automatically.

 

This capability revolves around the **ngModel**

 

**ngModel:** The model directive works with three main html elements.

1.  Input

2.  Select

3.  Textarea

 

We can add the Model directive to all three of these html elements. These will automatically hook up the two way binding between the html form fields and some items on our scope.

 

![](001_02_-_Markup_&_Controllers_002.png)

 

**Validation**

 

![](001_02_-_Markup_&_Controllers_003.png)

 

 

![](001_02_-_Markup_&_Controllers_004.png)

 

 

If we have a certain input element that we mark as \"required\" angular will take care of marking the form that input value is in as \"invalid\" using this method we can go ahead and send out the info from such form over to our controller and perform deeper validations for the user.

 

When sending a form out to our controller for validation we will be getting all of the services shown in the picture above. The most relevant ones that we want are:

 

-   \$dirty

    -   Indicates that the form has be CHANGED

-   \$invalid

    -   Indicates that the form is invalid

-   \$pristine

    -   Exact opposite of dirty

-   \$valid

    -   Exact opposite of valid

 

CSS: Angular also takes care of adding CSS classes on our angular fields and our forms to indicate what field and state those forms are at. As developers we can use such classes to our advantage to further help the user navigate through our page.

 

Example: *\<style\> input.ng-invalid.ng-dirty { background-color: pink;} \</style\>*

For this case, any element in our form that has been modified in any way that is not valid with our validation will change its background to pink until fixed.

 
