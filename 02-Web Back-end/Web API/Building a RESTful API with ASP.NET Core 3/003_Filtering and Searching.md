Filtering and Searching

Tuesday, April 28, 2020

7:10 PM

 

 

![](003_Filtering_and_Searching_000.png){width="6.741666666666666in" height="1.9166666666666667in"}

 

**Most common:**

 

![](003_Filtering_and_Searching_001.png){width="3.6416666666666666in" height="3.6333333333333333in"}

 

![](003_Filtering_and_Searching_002.png){width="6.05in" height="1.0916666666666666in"}

 

\^\^\^ These are some of the examples of ways we can get our data and pass in the authorId in different ways... **Use binding source attributes to explicitly state where the action parameter should be bound from...** But until now I have not done this... how does my code work then?

 

**By default** ASP.NET Core attempts to use the **complex object model binder**. This pulls data from the values provided in the defined order. In my case so far I have been using the:

**\[ApiController\]** attribute.... Which by default changes the rules a bit to better fit the APIs.

 

When using **\[ApiController\]:**

![](003_Filtering_and_Searching_003.png){width="4.275in" height="3.2in"}

 

This doesn\'t mean we can\'t use the attributes above though...

 

**Filter / Searching**

![](003_Filtering_and_Searching_004.png){width="4.2in" height="1.625in"}

 

![](003_Filtering_and_Searching_005.png){width="5.258333333333334in" height="2.0in"}

 

**Deferred Execution**

Query exaction occurs sometime after the query is contracted. This is important so that we keep our search/filtering more efficient.

 

![](003_Filtering_and_Searching_006.png){width="6.541666666666667in" height="2.933333333333333in"}

 

Singleton queries are the ones like: .Count .First .Average

 

**Grouping Action Parameters**

So what if I have things that I keep having to add to the controller parameters.. I really don\'t want to keep changing the function signature for that... we can group them into our own DTO class.
