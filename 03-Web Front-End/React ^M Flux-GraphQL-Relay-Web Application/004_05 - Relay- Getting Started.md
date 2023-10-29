05 - Relay: Getting Started

Friday, April 29, 2016

11:50 AM

 

![](004_05_-_Relay-_Getting_Started_000.png)

 

 

**Relay Core Principles:\
** 

1.  **Storage & Caching**

    a.  Relay.Store

        i.  A single normalized Client Side data store in memory

        ii. When Relay loads on for the first time, it stores all data in the Relay.Store in memory

        iii. QueueStore: Relay manages inflight changes to the data (in front of MemoryStore. So queries can read from them as well. With the QueueStore we can also easily manage rollbacks. Instead of managing the state of a record, we just care about managing a faulty object form the queue store and we would be done.

        iv. CacheManager: Can be any storage engine (like local storage).\
            ** **

        v.  ![](004_05_-_Relay-_Getting_Started_001.png)

    ```{=html}
    <!-- -->
    ```
    b.  The hiarerchy of these three layers is NOT important....because the first layer that CAN resolve a record, WILL resolve that record.\
         

```{=html}
<!-- -->
```
2.  **Object Identification**

    a.  All objects in Realy have UNIQUE IDs over the entire system. This allows Relay to re-fetch any record at will when needed. And prevents disambiguate. Without Unique IDs...the data is bound to have duplicate records.

    b.  Relay has a DIFFING algorithm to make data fetching as efficient as possible.

        i.  If we already have some of the data but need more...we don't really need to ask for the whole object, we can just ask for the DIFFERENCE from what we NEED and what we HAVE.

        ii. \--\> **This is where we need to implement the NODE interface**

 

3.  **Connection Model**

    a.  Related to Pagination

        i.  Offset/Limit

            1.  ![](004_05_-_Relay-_Getting_Started_002.png)

>  

1.  ![](004_05_-_Relay-_Getting_Started_003.png)

```{=html}
<!-- -->
```
ii. After/First

    1.  ![](004_05_-_Relay-_Getting_Started_004.png)

>  
>
> ![](004_05_-_Relay-_Getting_Started_005.png)
>
>  
>
>  

 

**Tagged Template Strings**

 

This is an ES2015 feature...

 

Any template string can be tagged with a function name... This will allow us to preprocess the string before using...

 

-   **Let** titleCase = strings =\> strings.join().replace(/\\b\\w/g, match =\> match.toUpperCase());

-   titleCase\'abc apple\';

    -   \'Abc Apple\'

 

The titleCase function was invoked with the template string provided. The difference between just using a regular function is that the tag function will deal with a process argument list.
