Filtering and Searching

Tuesday, April 28, 2020

7:10 PM

 

 

![](003_Filtering_and_Searching_000.png)

 

**Most common:**

 

![](003_Filtering_and_Searching_001.png)

 

![](003_Filtering_and_Searching_002.png)

 

\^\^\^ These are some of the examples of ways we can get our data and pass in the authorId in different ways... **Use binding source attributes to explicitly state where the action parameter should be bound from...** But until now I have not done this... how does my code work then?

 

**By default** ASP.NET Core attempts to use the **complex object model binder**. This pulls data from the values provided in the defined order. In my case so far I have been using the:

**\[ApiController\]** attribute.... Which by default changes the rules a bit to better fit the APIs.

 

When using **\[ApiController\]:**

![](003_Filtering_and_Searching_003.png)

 

This doesn\'t mean we can\'t use the attributes above though...

 

**Filter / Searching**

![](003_Filtering_and_Searching_004.png)

 

![](003_Filtering_and_Searching_005.png)

 

**Deferred Execution**

Query exaction occurs sometime after the query is contracted. This is important so that we keep our search/filtering more efficient.

 

![](003_Filtering_and_Searching_006.png)

 

Singleton queries are the ones like: .Count .First .Average

 

**Grouping Action Parameters**

So what if I have things that I keep having to add to the controller parameters.. I really don\'t want to keep changing the function signature for that... we can group them into our own DTO class.
