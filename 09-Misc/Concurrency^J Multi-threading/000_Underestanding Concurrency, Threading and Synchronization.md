Underestanding Concurrency, Threading and Synchronization

Sunday, May 1, 2016

8:51 AM

 

![Machine generated alternative text: Concurrency: \"the art of doing several things at the same time\" What does correct code mean in the concurrent world How to improve your code by leveraging multi-core CPUs Writing code, implementing patterns Race condition, synchronization, volatility Visibility, false sharing, happens-before ](000_Underestanding_Concurrency,_Threading_and_Synchronization_000.png)

 

**[What is a Thread]{.underline}**

 

A Thread is defined at the Operating System Level. From the developer point of view, a thread is a SET of instructions that we write in our application and execute in a certain way. An application can be composed with many threads. Different threads can be executed at the same time. (not the same for all processor)

 

**[What does \"At the Same Time\" mean? (CPU level)]{.underline}**

 

We are considering that we have ONE Core CPU...which means that it can only do ONE thing at a time.

![](000_Underestanding_Concurrency,_Threading_and_Synchronization_001.png)

 

**Why do we have the feeling that everything is happening at the same time?**

 

Everything is a matter of a time scale. All actions are happening so fast that they appear to happen at the same time.

 

**Now lets consider a 2 Cored CPU**

 

On a multi-core system, we CAN have actions running at the same time.

 

![Machine generated alternative text: Core 1 Core 2 ](000_Underestanding_Concurrency,_Threading_and_Synchronization_002.png)

 

**Who is responsible for the CPU time sharing?**

 

-   A special element called a scheduler (Thread Scheduler)

-   There are three reasons for the scheduler to pause a thread:

    -   The CPU should be shared equally among threads

    -   The thread is waiting for some more data

    -   The thread is waiting for another thread to do something

 

 

**Race Condition**

 

-   Accessing data concurrently may lead to issues

    -   Two different threads my be needing the same data source

-   It means that two different threads are trying to read and write the same variable at the same time

-   This is called a race condition

-   \"same time\" does not mean the same thing on a single core and on a multi core CPU

 

**[Example: The Singleton Pattern]{.underline}**

 

![Machine generated alternative text: The Singleton Pattern public class Singleton Singleton private static private public static Singleton ± f (instance null instance new return instance instance ](000_Underestanding_Concurrency,_Threading_and_Synchronization_003.png)

 

 

**What is happening if two threads are calling getInstance() ?**

 

![Machine generated alternative text: Thread Tl Checks if instance is null? The answer is yes Enters the if block The thread scheduler pauses Tl Create an instance of Singleton Thread T 2 Waiting Checks if instance is null? The answer is yes Enters if the block Creates an instance of Singleton The thread scheduler pauses T 2 ](000_Underestanding_Concurrency,_Threading_and_Synchronization_004.png)

 

 

From the above example we can see that when Thread 1 tries to create an instance of the Singleton, it will not check if it already exists or not and therefore will create another instance of the object. Which is not what we expect as a client... so,

 

**How do we prevent that?**

 

Answer: [SYNCHRONIZATION]{.underline}

 

**Synchronization**

Prevents a block of code to be executed by more than one thread at the same time.

 

![Machine generated alternative text: pub 11 c class Singleton private static Singleton prxvate public static j f (instance instance instance Singleton null new return instance ](000_Underestanding_Concurrency,_Threading_and_Synchronization_005.png)

 

 

In JAVA, every instantiated object has a lock property that contains a key. In simple terms, whenever we try to synchronize a method in a certain object. Let\'s assume that we have a Thread1 trying to access the method. Because of the synchronization, the method will check its lock property and see if we have the key available for use. If yes, Thread1 will access the method accordingly. Now, let\'s consider we have Thread2 that tries to access the same method. When Thread2 makes the same request to the lock property of our object, it will not receive the key back and therefore not be able to access the method. Once Thread1 finishes doing what needed to be done, then the lock property gets reset and any other thread that needs to access the method (in this example Thread2 that is waiting) will access the object\'s method properly.

 

![Machine generated alternative text: Singleton CLASS lock synchronized o O 0 getlnstance() ](000_Underestanding_Concurrency,_Threading_and_Synchronization_006.png)

So for synchronization to work we need a special technical object that will hold the key... In fact, every JAVA object play this role....But as developers we can make such key object ourselves.

 

This key is also called a monitor. How can we designate this object?

 

There are 3 Different ways to achieve this:

 

1.  Using a static method will allow us to use the class itself as a key:

    a.  ![Machine generated alternative text: public static L f (instance instance Singleton null new return instance In this code, the key is the Singleton class itself A synchronized static method uses the class as a synchronization object ](000_Underestanding_Concurrency,_Threading_and_Synchronization_007.png)

2.  If using a non-static method. Then the key will be held by the instance of the class itself

    a.  ![Machine generated alternative text: public -eturn this. name String In this code, the key is the instance of the class A synchronized non-static method uses the instance as a synchronization object ](000_Underestanding_Concurrency,_Threading_and_Synchronization_008.png)

3.  We can write a dedicated, explicit object for the key (Synchronized block):

    a.  ![Machine generated alternative text: public class Person private final Object key public String (key) { // do some stuff o; new Object A third possibility is to use a dedicated object to synchronize It is always a good idea to hide an object used for synchronization ](000_Underestanding_Concurrency,_Threading_and_Synchronization_009.png)

 

**How about the case in which we have multiple synchronized methods?**

Well, assuming we did not explicitly declare our own private key object, a single key will be used for the 2 (or more) methods of the class.

 

![Machine generated alternative text: Synchronizing More Than One Method Mary lock synchronized 0 etName() synchronized o getAge() ](000_Underestanding_Concurrency,_Threading_and_Synchronization_010.png)

 

**How about if we have TWO instances of the Person Class?**

We will have 2 different keys:

 

![Machine generated alternative text: Synchronizing More Than One Method Mary lock synchronized o getName() synchronized John lock synchronized getName() synchronized get Age ( ) ](000_Underestanding_Concurrency,_Threading_and_Synchronization_011.png)

 

If we want is to prevent to threads to use two different methods in a class at the same time (even with different instances)... then we need our lock object to be bound NOT to each instance, but to the class itself. So it has to be a static field of the class Person itself.

 

![Machine generated alternative text: Synchronizing More Than One Method Person CLASS Mary synchronized o getName() synchronized getAge() lock synchronized getName() synchronized getAge() ](000_Underestanding_Concurrency,_Threading_and_Synchronization_012.png)

 

 

**[Reentrant Locks and Deadlocks]{.underline}**

 

**Reentrant:**

 

Reentrant: Considering we have two different methods that are synchronized for two separate objects. If Method1 is accessed by our thread which requires to access Method2 in the other object...when Thread tries to get to such object the key will NOT be available (because it is being held by that very same thread.... This then leads to the exception of the rule when it comes to accessing a method even though the key is not \"available\".... Our thread WILL be able to access Method2 without issues... This is what we call in JAVA Reentrant:

 

![Machine generated alternative text: Mary synchronized synchronized loc John synchronized synchronized o ](000_Underestanding_Concurrency,_Threading_and_Synchronization_013.png)

 

Locks are reentrant when a thread holds a lock, it can enter a block synchronized on the lock it is holding.

 

**Deadlock:**

 

![Machine generated alternative text: Mary synchronized o synchronized loc Deadlocks John synchronized synchronized loc ](000_Underestanding_Concurrency,_Threading_and_Synchronization_014.png)

 

Two threads waiting for each-other...... forever !

 

Deadlock: A deadlock is a situation where a thread T1 holds a key needed by a thread T2, and T2 holds the key needed by T1

 

The JVM is able to detect deadlock situation, and can log information to help debug the application. But there is not much we can do if a deadlock situation occurs, beside rebooting the JVM.

 

**[The Runnable Pattern]{.underline}**

 

The most basic way to create threads in Java is to use the Runnable Pattern.

First create an instance of Runnable... only one method to implement

Then we pass it to the constructor of the Thread class.

Then call the start() method of this thread object.

 

![Machine generated alternative text: Runnable runnable new Runnable public void String name System . out. Thread (\"I am running o. in thread name First create an instance of a Runnable This is the Java 7 way, with an instance of an anonymous class ](000_Underestanding_Concurrency,_Threading_and_Synchronization_015.png)

![Machine generated alternative text: Demo Let us see some code! Let us create threads on simple examples See what can go wrong with a race condition Fix our code with synchronization ](000_Underestanding_Concurrency,_Threading_and_Synchronization_016.png)

 

 

 
