Creating Resources

Tuesday, April 28, 2020

9:46 PM

GET / HEAD are considered safe methods... they should be updating anything in the DB... as you should always be getting the same value out of them regardless of the amount of times that you call them. This is called idempotency.

![](004_Creating_Resources_000.png)

![](004_Creating_Resources_001.png)

When trying to figure out what HTTP method to use when creating an API, I should resource back to this table to determine which one works best for my usecase

![](004_Creating_Resources_002.png)

In the example above they created a brand new class for the author to be used as the DTO to be saved.. I think that\'s a bit uncessesary... so I will skip for now... Important not is though.... When we return CreatedAtRoute... we return a **201** create response... This one allows us to create a response with a location header.... This location header should contain the URI where the new created entity will be found...

**routeName** is the name of the route used to get the URI for the location header... For us that would be the HttpGet that retrieves a single Photo.... In order to make this work we just need to give the HttpGet attribute a Name....

**\[HttpGet(\"{photoID}\", Name = \"GetPhoto\"\]**

![](004_Creating_Resources_003.png)

This is really cool, because other than we successfully saving a row to the database, if we check the HEADER of our request we got:\
![](004_Creating_Resources_004.png)

\^\^\^ The URI that would load the very sae entry I just saved. Cool!

Following the same logic as above I was able to then save a new member AND all the photos belonging to this member in one go... BUT.... How about if I wanted to save multiple members at once... Meaning instead of sending the one member to the API controller, send a list of them?

I can do that simply by having a POST method in my controller that handles a list of members... but

![](004_Creating_Resources_005.png)

But the problem I face here is that I don\'t know what to return as far as created objects goes. They get saved into the DB properly but we want a 201 CREATE msg instead of a 200 Ok one... so I am not there yet. This leads me into tackling the LOCATION header issue... (or in other words, working with ARRAY keys)

**Keys:**

-   Array key: 1,2,3 // This is a comma separated list

-   Composite key: key1 = value1, key2 = value2 // The key is a combination of key/value pairs

This is more of a URI design issue than implementation... we need array key for our location when creating a member collection.

I was not understanding this too well... but what I am trying to do is have a function that retrieves multiple entities (in 1this case members) but passing in an array of keys... this is being brought up because of the above code that inserts multiple entries in the DB.

![](004_Creating_Resources_006.png)

My method needs to be able to get a comma separated list of ids. In the template we add () and a parameter name ids... There is NO IMPLICIT binding to such an array that\'s part of the route (there used to be in the old ASP.NET api) so that\'s why I have to specify \[FromRoute\] to ensure my method gets the value from the route...

**By default, it looks in the BODY for Collections** and a GET request shouldn\'t have a request body.. So /shrug

**We CAN\'T accept an Ienumerable of IDs in the parameter list and expect it to be filled out.** At least not automatically... so instead of relying on implicit binding... so I have to provide it myself... hence CUSTOM MODEL BINDERS

**Custom model Binders**

![](004_Creating_Resources_007.png)

![](004_Creating_Resources_008.png)

**\^\^\^ Trying to note this pattern is a bit confusing... the code makes more sense in my opinion**

The code above works with Array keys...... my requests looking like:

<http://localhost:51001/api/members/(1001,1002)>

How about with composite keys?

<http://localhost:51001/api/members/key1=firstValue,key2=secondValue>

For this we just use a route template with 2 keys... which would map to 2 parameters in the action signatures...easy piecy.

**POST to a single resource**

So far I have ONLY posted to collection resources until now... but how about a POST to a resource URI that includes the ID in the URI. I am not talking about having a single resource in the BODY... we have done that.... In other words:

[*http://localhost:51044/api/members/123*](http://localhost:51044/api/members/123)

POSTING to a single resource CAN NEVER return a successful request. It either returns a 404 if the member doesn\'t exist, or a 409 conflict if the member already exist... If we allowed the consumer to create a request like this.... Then it should be idempotent... and POST is NOT idempotent... We CANNOT rely on the idea that multiple POST request would result in the same outcome. The really cool thing is that, without doing anything, .Net Core 3 already takes care of things without me having to write anything...it returns a 405 - Method not allowed by default... in previous versions I had to write code for this...

This raises another question though... HOW can consumers know what IS and IS NOT allowed in a certain URI? The answer is OPTIONS

An **OPTIONS** request represent a request for information about the communication options available on a certain URI. Options are returned in the ALLOW response HEADER as a comma separated list of methods... so for us:

![](004_Creating_Resources_009.png)

We can include a response body describing the options, but the format of that is not covered by the HTTP standard.

**Dealing with various CONTENT TYPES**

Only thing to note here is that if we don\'t pass in a Content-Type in our POST request header, then I should (and .Net Core does by default here) return a 415 Unsupported Media Type message back to the user)
