Separation of Concerns

Wednesday, September 14, 2016

6:03 PM

 

**Benefits:**

-   Easier to Maintain

-   Easier to Extend

-   Reuse More Code

-   Easier to Test

-   Easier to Isolate bugs

 

**Summary**

SoC will help us manage all the complexity of our application.

 

**The Rule of One**

The heart of SoC is to be able to have our components do ONE thing and ONE thing well. \"When your component does everything, it does nothing well.\"

 

For example we want our controller to only handle the logic for a View. We do not want our controller to be caring about getting the DATA or any other business logic that might affect our application.

 

*A Component has ONE role. One Componet per file. Component has a singular purpose*

 

**How do we separate?**

When in comes to web development, we often thing of th efront end and the back end. In the back end we know terms like Controller, Model, and View....but how about in the front end? Well, that\'s where Angular\'s work takes place.

 

AngularJS has Familiar Terms:

-   Modules

-   Factories / Services

-   Directives (Widgets)

-   Models

-   Views

-   Controllers

 

 

**Tips for Separating with AngularJS**

 

 
