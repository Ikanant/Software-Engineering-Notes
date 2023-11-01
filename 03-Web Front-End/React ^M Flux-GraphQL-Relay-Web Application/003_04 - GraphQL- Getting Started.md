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
                 

                -   ![](003_04_-_GraphQL-_Getting_Started_000.png)

**What is GraphQL**

1.  Express data needs hierarchically

2.  Get data with a single round trip

Example Query:

![](003_04_-_GraphQL-_Getting_Started_001.png)

-   Execution engine on server

-   Query language on client

> *[The Lingua Franca of data communication]*
>
>  
>
>  

![](003_04_-_GraphQL-_Getting_Started_002.png)

![](003_04_-_GraphQL-_Getting_Started_003.png)

![](003_04_-_GraphQL-_Getting_Started_004.png)

![](003_04_-_GraphQL-_Getting_Started_005.png)

![](003_04_-_GraphQL-_Getting_Started_006.png)

![](003_04_-_GraphQL-_Getting_Started_007.png)

![](003_04_-_GraphQL-_Getting_Started_008.png)

![](003_04_-_GraphQL-_Getting_Started_009.png)

**GraphQL Core Principles**

1.  Mental Model

    a.  Models data exactly how we think about it and how we use it

    b.  It's a two way mental model. It is very easy to write a GraphQL query if we know the data we are dealing with

    c.  ![](003_04_-_GraphQL-_Getting_Started_010.png)

2.  Introspection

    a.  Allows us to type the type system dynamicly

    b.  ![](003_04_-_GraphQL-_Getting_Started_011.png)

>  

c.  ![](003_04_-_GraphQL-_Getting_Started_012.png)

```{=html}
<!-- -->
```
3.  Composition

    a.  We can split and combine queries to match the different fragments of our app...allowing us for complete isolation of what data every subcomponents is asking for

    b.  It allows MULTIPLE views within to use the SAME fragment without any duplication of logic or data fetch

4.  Fragments

    a.  Map perfectly to the components of our system\
         

    b.  ![](003_04_-_GraphQL-_Getting_Started_013.png)

>  

c.  ![](003_04_-_GraphQL-_Getting_Started_014.png)

d.  By using fragments we do not care for repetition of similar queries

e.  ![](003_04_-_GraphQL-_Getting_Started_015.png)

```{=html}
<!-- -->
```
5.  GraphQL is NOT a Storage Engine

    a.  It is a RUNTIME

    b.  It does not assume anything with where data is from. And it can even be implemented using multiple datasources

6.  Mutations

    a.  A Special kind of query which changes data on the server

    b.  ![](003_04_-_GraphQL-_Getting_Started_016.png)

![](003_04_-_GraphQL-_Getting_Started_017.png)
