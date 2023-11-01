Updating Resources

Wednesday, April 29, 2020

7:09 PM

![](006_Updating_Resources_000.png)

![](006_Updating_Resources_001.png)

**Side Note:**

![](006_Updating_Resources_002.png)

![](006_Updating_Resources_003.png)

What is often misunderstood about the repository pattern is the concept of **Persistence Ignorant.** Sometimes it is said that for a Repo we can simply switch out the persistence technology when needed.... And while that is technically true... that\'s not the purpose of the repository pattern. What it is useful for IS allowing us WHICH persistence technology to use for a specific method on the repository...

Getting an order with some complex logic might be advisable to use ADO.NET.... Or even call an external service. For consumers of the repos (like my controllers) it is of NO interest what goes on in the repo

![](006_Updating_Resources_004.png)

The reason why I am writing about the repository contract right now is because while writing my first PUT method, I used an UpdatePhoto() function to my repo that does NOT have any body in it... it has not been implemented... so, why? In summary, because of the nature of the pattern, we don\'t know if in the future that function might actually be required OR contain some new logic that needs to be shared across multiple functions that update photos.... soD

![](006_Updating_Resources_005.png)

But getting back to business... why is my UpdatePhoto(Photo photo) function empty? In Entity Framework Core the entities are tracked by the context...SO when I changed the entity in the controller it already made the \*update that I needed. Running Save() should be enough...

As far as returning something out of an update in my controller is all relative... I can simply return a NoContent()... or I can return an Ok() call with the newly edited object in it.

Now let\'s assume I send a PUT request and I only specify the value of the Title of my object and NOT the Description... then we end up with something like:

![](006_Updating_Resources_006.png)

Which is correct... PUT should FULLY update the resource... so what\'s sent in the request body should be considered a modified version of the resource.

**Validation**

For most resources (if not most) this will behave exactly like POST... but, it doesn\'t have to be. For updating an entity I ended up creating yet another DTO... so, for it I can add the same annotations as before and things are going to work just fine.. BUT, that\'s a lot of reusable code... so instead of going this route, I can always create ANOTHER abstract class that contains the \*\*\* common properties (alongside their annotations) for the various other DTOs I have for my entity... this works really well... but now let\'s say I want to have a custom message for my update validation for one of those shared properties... first idea is to make the property abstract.... BUT that would force us to add an implementation in the classes that extend this abstract class with abstract properties... this is when a virtual property comes into place... virtual allow our sub classes to use the base.Get Set implementation of my parent class BUT also allows me to override the property to append whatever annotation I want for this scenario. Works out well.

**Updating Collection Resources**

![](006_Updating_Resources_007.png)

Doing this can be quite destructive... while it seems like we are updating the entities, what we are actually doing is deleting things and re-inserting... I am not gonna implement something like this for my API.

**Upserting**

![](006_Updating_Resources_008.png)

![](006_Updating_Resources_009.png)

**Partially Updating a Resource**

![](006_Updating_Resources_010.png)

![](006_Updating_Resources_011.png)

![](006_Updating_Resources_012.png)

ASP.NET Core will in fact accept application/json content type (and most RESTful APIs will as well)... But if we want to follow the correct standard we should use the json+patch+json

There are 6 operations possible:

1.  Add

    a.  Will add a property at a path location with a specific value... Pass through by value. If the path is unexacting, the property should be added to the resource... (this is often seen with dynamic resources... not my case)

2.  Remove

    a.  Remove property... or in non-dynamic cases, set it to its default value

3.  Replace

    a.  Replaces the value at the specified path... and it is functionally the same as a remove operation followed by an add operation

4.  Copy

    a.  Take the value from the from property and take it to the path property

5.  Move

    a.  Same as copy but it will remove the value from the from property

6.  Test

    a.  Test that a value at the path is equal to the specified value

>  

![](006_Updating_Resources_013.png)

![](006_Updating_Resources_014.png)

So I just have to remember that a JSON Patch property is a LIST of operations that have to be applied to the resource....allowing for partial updates.

Jumping into code... the first thing I noted from what I wrote above, is that my HTTP method will take in a JsonPatchDocument\<ObjectDtoIAmDealingWith\>

**Nugget get Microsoft.AspNetCore.JsonPatch**

![](006_Updating_Resources_015.png)

\^\^\^ That\'s a NO NO. We shouldn\'t allow the core DTO to be updated... because it contains an ID... we don\'t want to change that... so we need to use UpdateDto.

![](006_Updating_Resources_016.png)

Another note is that there are many ways this ApplyTo method can break for me. If we try to apply a change to a property that\'s read only for example, or one that does not exist... I need to apply some validation for this issue.

Alright...when I tried running this for the first time things failed :/

*The JSON value could not be converted to Microsoft.AspNetCode.JsonPatch.JsonPatchDocument*

Why? Issue is that the default JSON parser in ASP.NET Core 3 is not as feature complete as something like Json.Net.... At least not yet.... To fix this problem I can jump into using JSON.Net then... which I will need to up from another nugget package provided by Microsoft....

**Microsoft.AspNetCore.Mvc.NewtonsoftJson**

Then the only thing to do is to chain the newtonsoftjson to the IMvcBuilder inside my startup class...

One side effect of

![](006_Updating_Resources_017.png)

\^\^\^ By adding JSON.Net as output/input formatter AFTER we added the seralizer xml formatters I changed the DEFAULT formatter... the default formatter is simply the one added first.... So when making request without and ACCEPT header in the request, we will get XML code back... which is not ideal.... So in order to fix this, SWAP the lines!

Validation for PATCHing is also somewhat tricky. Main problem lies on the fact we pass in a JSONPatchDocument to my method and hence the previously written validation to my DTO file is no longer applicable... so I need to manually check this once my patch has been applied to see if it\'s valid...

**TryValidateModel(photoToPatch);**

![](006_Updating_Resources_018.png)

\^\^\^ How about if we try to edit/remove a property that does not exist? For that I just simply pass in the ModelState to my ApplyTo method... if I do this any errors in the PATCH document will make the model state invalid! - so later when I do my check (tryValidateMode) will take care of returning the error.

Custom Validation Message is important but I will work on that in the future \<skipping for now\>\
<https://app.pluralsight.com/course-player?clipId=68eaa3a9-309d-4515-8d50-84890fc71c38>

**Upserting**

So I already did this when dealing with a PUT request... it was not too bad... but what if I wanted to do it with PATCH? One issue I have with it is that previously we were sending the dto itself which could easily be updated/inserted.... But now since we are passing in a jsonpatchdocument, things are not the same...

Technically we still have memberID and photoID....

![](006_Updating_Resources_019.png)
