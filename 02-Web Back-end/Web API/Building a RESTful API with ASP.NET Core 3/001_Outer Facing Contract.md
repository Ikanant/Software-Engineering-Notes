Outer Facing Contract

Saturday, April 25, 2020

3:36 PM

![](001_Outer_Facing_Contract_000.png)

 

![](001_Outer_Facing_Contract_001.png)

 

 

-   **Resource Identifier:**

    -   There is no standard to name these...just best practices:

        -   Should always be a noun. Things, not actions...the actions will be our HTTP methods

        -   ![](001_Outer_Facing_Contract_002.png)

        -   Stay predictable

        -   ![](001_Outer_Facing_Contract_003.png)

        -   Represent hierarchy when naming resources

        -   ![](001_Outer_Facing_Contract_004.png)

        -   We should NOT try to filter, sort orders. These are not resources

        -   ![](001_Outer_Facing_Contract_005.png)

        -   **EXCEPTION:**

            -   Sometimes, RPC-style calls don\'t easily map to pluralized resource names

            -   ![](001_Outer_Facing_Contract_006.png)

>  

Time to add a Controller to my API... we are gonna make one and simply make it implement the ControllerBase abstract class. This controller base class contains basic functionality my controller will need... like Access to the model state, the current user and common methods for common responses... **Note:** We can also inherit from Controller... BUT by doing so we would also add support for VIEWS... which si not what we need.

 

Next: Apply \[ApiController\] attribute... this is NOT necessary but by doing so we are configuring this controller with features and behaviors that will improve our experience... think of it similar as when we require attribute routing... automatically returning a 400 bad request on bad input... This is cool...after I added a method to my controller it failed because it didn\'t have the attribute about what kind of attribute routing... this is the ApiController at work...

 

**Routing:** Routing matches a request URI to an action on a controller... We send an HTTP request and the mvc app tries to match it to a controller... in Dotnet Core 3 the preferred way to set this up is through EndPoint routing

 

![](001_Outer_Facing_Contract_007.png)

 

In older Dotnet Core versions routing was setup by using MVC or useRouting()... So what\'s the advantage of using Endpoint routing? We can NOW INJECT middleware that runs IN BETWEEN selecting the end point AND executing the end point. In other words: We can inject pieces of middleware that know which endpoint was selected and can potentially select a different one... the most common example of this is authentication:

 

![](001_Outer_Facing_Contract_008.png)

 

Either way I still need to map the endpoint. Can be done either through convention based or attribute based.

 

Convention based Routing is usually used for web applications.... For APIs it\'s better to use Attribute-based Routing.

 

 

![](001_Outer_Facing_Contract_009.png)

 

 

![](001_Outer_Facing_Contract_010.png)

 

![](001_Outer_Facing_Contract_011.png)

 

![](001_Outer_Facing_Contract_012.png)

 

If using some of Microsoft templates to generate a controller for us, we can see something like that... which takes the prefix of the name of the class we are in and uses it as the name of the route... This is not ideal because if we ever refactor our class name in the future, then the API would change and further side effects can be experienced

 

Route constraints are also possible when using attributes

![](001_Outer_Facing_Contract_013.png)

 

 

**The Importance of Status Codes:**

 

![](001_Outer_Facing_Contract_014.png)

 

![](001_Outer_Facing_Contract_015.png)

 

 

![](001_Outer_Facing_Contract_016.png)

 

**Content Negotiation:**

The process of selecting the BEST representation for a given response when there are multiple representations available. Meaning we often think of this RESTful apis as only capable of returning JSON back to the client, but as noted above this is not the case.

 

This is where the Accept header is used for when sending a request... this is where we can specify application/json or application/xml.

The deal is that if the user specifiers the Accept header in the request, then IF the api supports the requested format, it should return that. If no accept header is available or the api doesn\'t support the format then the API can go into the default format: like JSON. This should be avoidable though... at least when I can\'t support the format requested... if they ask for XML and I default to JSON this will cause more headaches... a 406 Not acceptable code is probably the best practice here.

 

![](001_Outer_Facing_Contract_017.png)

 

![](001_Outer_Facing_Contract_018.png)

 
