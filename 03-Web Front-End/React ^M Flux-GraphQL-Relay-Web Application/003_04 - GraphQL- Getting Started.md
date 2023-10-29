04 - GraphQL: Getting Started

Friday, April 29, 2016

11:49 AM

 

**Why GrapQH ?**

1.  Facebook and other big players. GraphQL has been proven to work on big environments. BIG applications such as Facebook.

    -   Data communication performance is great

        -   GraphQL was invented from an effort from facebook to get serious about mobile applications. Taking into consideration mobile devices are just smarter than your average web client.

        -   Smarter Clients means more complex and custom data fetching needs & less necessity to be dependent from the server

    -   Developers experience is even better

        -   Product-developers in mind from design

        -   Clear representation how developers think about their UI.....it is more natural to think of data as components with certain states....versus resources and join statements

        -   Declarative:

            -   A GraphQL models the output...rahter than the steps that get your there\
                 

                -   ![](003_04_-_GraphQL-_Getting_Started_000.png){width="4.075in" height="1.6166666666666667in"}

 

**What is GraphQL**

 

1.  Express data needs hierarchically

2.  Get data with a single round trip

 

Example Query:

 

![](003_04_-_GraphQL-_Getting_Started_001.png){width="2.575in" height="1.7083333333333333in"}

 

 

-   Execution engine on server

-   Query language on client

 

> *[The Lingua Franca of data communication]{.underline}*
>
>  
>
>  

![](003_04_-_GraphQL-_Getting_Started_002.png){width="5.0in" height="2.558333333333333in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_003.png){width="5.0in" height="2.7333333333333334in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_004.png){width="5.0in" height="2.7416666666666667in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_005.png){width="5.0in" height="2.625in"}

 

![](003_04_-_GraphQL-_Getting_Started_006.png){width="5.0in" height="2.575in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_007.png){width="5.0in" height="2.7in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_008.png){width="5.0in" height="2.7416666666666667in"}

 

![](003_04_-_GraphQL-_Getting_Started_009.png){width="5.0in" height="2.591666666666667in"}

 

 

**GraphQL Core Principles**

 

1.  Mental Model

    a.  Models data exactly how we think about it and how we use it

    b.  It's a two way mental model. It is very easy to write a GraphQL query if we know the data we are dealing with

    c.  ![](003_04_-_GraphQL-_Getting_Started_010.png){width="5.0in" height="2.6666666666666665in"}

2.  Introspection

    a.  Allows us to type the type system dynamicly

    b.  ![](003_04_-_GraphQL-_Getting_Started_011.png){width="5.0in" height="2.5083333333333333in"}

>  

c.  ![](003_04_-_GraphQL-_Getting_Started_012.png){width="5.0in" height="2.6in"}

```{=html}
<!-- -->
```
3.  Composition

    a.  We can split and combine queries to match the different fragments of our app...allowing us for complete isolation of what data every subcomponents is asking for

    b.  It allows MULTIPLE views within to use the SAME fragment without any duplication of logic or data fetch

4.  Fragments

    a.  Map perfectly to the components of our system\
         

    b.  ![](003_04_-_GraphQL-_Getting_Started_013.png){width="4.841666666666667in" height="4.808333333333334in"}

>  

c.  ![](003_04_-_GraphQL-_Getting_Started_014.png){width="5.0in" height="2.7416666666666667in"}

d.  By using fragments we do not care for repetition of similar queries

e.  ![](003_04_-_GraphQL-_Getting_Started_015.png){width="3.066666666666667in" height="2.933333333333333in"}

```{=html}
<!-- -->
```
5.  GraphQL is NOT a Storage Engine

    a.  It is a RUNTIME

    b.  It does not assume anything with where data is from. And it can even be implemented using multiple datasources

6.  Mutations

    a.  A Special kind of query which changes data on the server

    b.  ![](003_04_-_GraphQL-_Getting_Started_016.png){width="5.0in" height="2.55in"}

 

 

![](003_04_-_GraphQL-_Getting_Started_017.png){width="5.0in" height="2.5in"}
