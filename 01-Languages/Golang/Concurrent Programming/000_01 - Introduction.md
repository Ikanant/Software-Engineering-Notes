01 - Introduction

Monday, May 2, 2016

10:10 PM

**[Introduction]**

Concurrency is NOT Parallelism ( I have already expanded on this topic in my Go Fundamentals notes)

**Concurrency Models :**

- Processor Threads
- Events
  - Triggering Background work based on a users action
- Callbacks and Promises
- Communicating Sequential Process (The Actor Model)
  - Allows massive concurrency with amazing reliability

**Processor Thread**

Highest level of control we will find.

Process: Is the name given about HOW the operating systems views the execution of a single instance of an application... Exactly, what this is depends on the OS...

Process is often responsible for managing the resources needed for the application such as memory.

A **Process** has one or more execution **Threads**. A Thread consist of Sequences of Programming instructions that execute in order... These are what is actually running an application in the context of a process. [All threads share the same memory space, which is managed by the process.]

**Advantages for Processor Threads in Applications:**

1.  Control:
    a. Nothing will ever give me the same level of control as using processor threads since we are working right against the operating system by manipulating such low level code
2.  Performance (maybe)
    a. We will see in the next note how we might see some decrease in performance on some instances of using Process Threads in our application
3.  Responsive User Interface
    a. Having at least two threads.... One for the User Interface.....

Disadvantages:

1.  Poor Performance
    a. This can be caused when over-using synchronization constructs such as Mutaxes that force Threads to wait for each other.
2.  Memory Consumption
    a. Each thread requires memory for their execution stack... there is a limit to the amount of threads that are practical
3.  Shared Memory:
    a. The memory of a thread is managed by its process, the execution threads often have access to the same memory....which can lead to big problems
4.  Race Conditions

**Events**
This model is often found in User Interfaces that the user initiates some sort of acction by entering some data or clicking on a control.

We deal with an Emiter, Receiver and Event Object

Advantages:

1.  Memory Isolation
2.  Separate Callee from Caller
    a. The Emiters don\'t have to know about the receiveers... which increases the level of decopouling of the application... (The receivers DO need to know about the emiters though)

Disadvantages:

1.  Traceability
    a. Since Emiters don\'t know abnout their receivers, we are faced with a challenge to trace down possible errors within the application
2.  Synchroniziing Receivers
    a. Since each Receiver runs independently, it can be difficult for two receivers to cordinate their activities AND if a receivers action takes a long time... this can be problematic.

**Callbacks & Promises**

In languages that recognize functions as first class citizens, callbacks and promises are often used to register an action that should be taken after a certain task has been completed.

- Callback
  - When a function is complete, then the callback function is invoked
- Promise
  - Advance of the regular Callback
  - With a promise, the long runnning function actually returns before its done executing... This return value is the promise object... This helps the client feel we are working with a synchronous fassion even though we are doing some asynchronously.

Advantages:

1.  Memory Isolation
2.  Simplify Async Opeartions

Disadvantages

1.  Pyramid of DOOM
    a. Typically asociated more with callbacks...
    b. This occurs when we have a function that takes a callback... that callback then takes his own callback and so own... This could be really problematic if any of the deeply nested callbacks decide to have an error.
2.  Handling Multiple Receivers

**Communicating Sequential Process (CSP or Actor Model)**

This model allows individual entities to work in a purely synchronous and isolated fassion working with data that they are provided with... and then passing the results on for whatever is downstream for them... The magic happens in between this entities where all of the asynchronous logic and cordination are buriend into the infrastructure of the language or framework.

Components:

- Actor
  - Receives information in, applying some logit to it, and then passing it along on to the next actor in the chain... This actors don\'t have to worry about any asynchronously programming within themselves...
- Message
  - Object that is passed between two actors

Advantages:

1.  Fully Decoupled
    a. The actors NEVER have to know about each other at all... they only have to know where are they getting messages from and where they put messages when they are ready.
2.  Multiple Handlers
3.  Memory Isolation

Disadvantages:

1.  Complicated Mental Model
    a. Hard to understand at first.... But once it clicks, it clicks
2.  Traceability
    a. If not carefully designed, an application can get very difficult to trouble shoot

![Machine generated alternative text: Concurrency in Go No Thread Primitives Goroutines Channels ](000_01_-_Introduction_000.png)
