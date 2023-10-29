How Garbage Collection Works in the Oracle JVM

Tuesday, February 19, 2019

9:02 PM

 

There are many ways the garbage collection works within the JVM... One quick thing to keep in mind is that there are various different TYPES of Garbage Collectors working with our memory:\
 

-   Reference Counted Garbage Collector

    -   It will keep a counter of each object initialized in our application and it will add a count and decrease a count accordingly for every reference that calls the object... Once count goes to 0 the Garbage Collector takes care of the clean up properly

    -   Major problem here is when we have circular references happening... we have an object1 referencing object2 and the same object2 referencing object1... in this case this memory is going to have a hard time being marked as removable and we might end up with memory leaking

-   Mark and Sweep

    -   Technically: Mark, Sweep and Compact

    -   This method will analyze each address space and figure out of there are any objects referencing it. If so, it continue its work, if not then this address gets clean and on the collector goes

    -   Once the whole memory has been cleaned in the heap for example: the garbage collector gets each memory address and allocates in order within the stack... so everything is nice and tight.... The process would continue on from there. One buffer to another

    -   Remember:

        -   Heap: A heap is an area of the pre-reserved computer main storage (Memory) that a program process can use to store data in some variable amount that won\'t be known until the program is running

        -   Stack: A stack is similar to a heap except that the blocks are taken out of storage in a certain order and returned in the same way

-   Generational

    -   The idea behind this one is that if an object survives a garbage collection, it is likely this will be an object that will stay around for a long time. The collector just places the memory address into an older generation group and continue checking and cleaning up younger memory spaces.

-   Incremental

    -   Generational is a form of Incremental GC. Incremental GC is one that doesn\'t look at the memory ALL THE TIME.

 

Important Note: Most garbage collectors have a mix of all the types mentioned above.

 

 

**Introduction**

 

When going over specifically over the JVM garbage collector we need to consider a few things:\
 

-   Stop the world events

    -   GC pauses the entire application and proceeds to run. We want to minimize this type of work

-   Memory fragmentation

-   Throughput

    -   How quickly can it run

-   Different GCs

    -   Generational GC

    -   Copying

    -   Mark and Sweep

-   Multi-core

 

**Basic Ideas**

 

![Memory - Young Generation Eden The Players Tenured Permanent Generation Permanent Old Generation ](000_How_Garbage_Collection_Works_in_the_Oracle_JVM_000.png){width="4.75in" height="3.283333333333333in"}

 

![Basic Ideas • Has a \'young generation\' and an \'old generation\' • Most initial objects allocated in \'Eden space\' Part of young generation • Young generation also has two \'survivor\' spaces Objects that survive a GC get moved to the survivor space Only one survivor space in use at a time Objects copied between survivor spaces Old generation is where long lived objects go to die ](000_How_Garbage_Collection_Works_in_the_Oracle_JVM_001.png){width="4.758333333333334in" height="3.2916666666666665in"}

 

![Young Generation • Most objects live for a very short time The \'turtle\' theory of garbage collection i.e. you die young or live \'forever\' ](000_How_Garbage_Collection_Works_in_the_Oracle_JVM_002.png){width="4.783333333333333in" height="1.7083333333333333in"}

 

![Copying to Old Generation • JVM will eventually promote to old generation After a certain number of garbage collects If survivor space is full If JVM has been told to always create objects in old space -XX:+AlwaysTenure flag to JVM ](000_How_Garbage_Collection_Works_in_the_Oracle_JVM_003.png){width="4.116666666666666in" height="2.1416666666666666in"}

 

![What Does Live Mean? • Live roots From stack frames Static variables Others such as JNI and synchronization \'monitors\' • References from live rooted objects are followed to other objects What about references from Old Generation to Young? ](000_How_Garbage_Collection_Works_in_the_Oracle_JVM_004.png){width="4.133333333333334in" height="2.1666666666666665in"}

 
