Getting Resources

Saturday, April 25, 2020

6:00 PM

![](002_Getting_Resources_000.png)

As noted before, REST stops at the level of the outer facing contract... Whatever is happening byond that is of no importance to REST. From that, we know that the entity model, should be different from the outer facing model. These models are known as DTOs orViewModels, but that also leads to problems

![](002_Getting_Resources_001.png)

![](002_Getting_Resources_002.png)

**Return Types**

Most actions have an EXCPLICIT return type. For our GetAuthors method that should be an ienumerable of authors... for those cases there is an implementation of action result available... **ActionResult\<T\>**

Having the return type of the method explicitly defined other pieces of code can infer the action expected... That will integrate better with our actions. This will only become an obvious benefit when implementing something like Swashbuckle for documenting the API.

**Automapper**

So from the screenshot above we successfully get the Authors entity converted into the authorDto that will be exposed to our customer... BUT, I do not want to do that every time. That sounds like a nightmare... that\'s when a tool like Automapper comes into place. My first instinct was to just install the automapper nuget package... but we won\'t be needing that (at least, not just that)... It is better to look for:

**AutoMapper.Extensions.Microsoft.DependencyInjection** package.

This will contain extensions that will make auto mapper work nicely with ASP.NET Core\'s dependency injection system. This package has a dependency on Automapper, so that will get installed as well.

![](002_Getting_Resources_003.png)

Now I need to ensure automapper services are registered on the container. This method allows us to import a SET of assemblies. This assemplies will AUTOMATICALLY scan for **profiles** that contain mappings configurations.

AppDomain.CurrentDomain.GetAssemblies() we are LOADING profiles from ALL assemblies in the current domain.

**What is an automapper profile?**

A profile is a neat way to organize our mappings configuration.

To create an automapper map we just need to run the CreateMap (from within the Profile class I am working with) and pass in the Source Type and the Destination Type

![](002_Getting_Resources_004.png)

AutoMapper will take the properties with the SAME name from one entity to the next... By default it will ignore null reference exceptions from null to target. But, how about if I want to concatenate string properties, or do some sort of extra logic to the source property... well that\'s where I can introduce projection...

**Projection** transforms a source to a destination BEYOND flattening the object model. Without extra config, automapper requries a flattened destination to match the source naming structure...

![](002_Getting_Resources_005.png)

That\'s what I am doing in the code above. I am stating that:

-   For member \<Name\> on the DESTINATION object I want it to be mapped from the SOURCE First and Last name...

![](002_Getting_Resources_006.png)

The code above removes the forEach loop from before and just uses the mapper interface to Map the DTO. I pass through the type I want to get back and the parameter will be the source. And that\'s done.

**Dealing with Parent Child Relationships**

In the code I\'ve been following so far, we have been dealing with authors... BUT for each Author there might be Courses... we don\'t want expose Courses directly, so we want to expose through an URI that reflects this.

So in our API I would end up with something like:

**/api/members/{membersID}/photos/{photoID}**

![](002_Getting_Resources_007.png)

So far so good... BUT I do have a problem. One of the constraints I noted before for a REST api is that the response from the API should have enough information to modify it OR delete.... Is that the case from the image above? More or less... We have the ID which should be enough BUT we can also include the resource URI... the Identifier of the resource. The way to do this is by implementing HATEOAS... For now I plan to skip this.

**Server Side Exception**

So there is much to be said about this, but the main thing right now is that if an exception is thrown from our server (like DB offline exception) then we will just get a 500 error from the consumer side of things... that\'s alright.... BUT we would also (by default) send more information to the user than he might need... like the Stack Trace, which could cause logic to leak. Dotnet Core is really cool and by default, if the API is running in Production Mode it WILL NOT send info back to the consumer other than the error code.

Custom behavior can be accomplished too...

![](002_Getting_Resources_008.png)

**HTTP HEAD**

![](002_Getting_Resources_009.png)

Looking back to the table above... HEAD is IDENTICAL to GET except that the API should NOT return a response BODY. It can be used to obtain information on the resource. Or simply checking if the resource exist. That is valuable.

The creators of Dotnet Core wanted to make our lifes easier, so by just adding the attribute to our existing GET methods we should be covered.

![](002_Getting_Resources_010.png)

All the code will still get executed, it will just NOT transport back the BODY. We get back 200 OK message but NO body.
