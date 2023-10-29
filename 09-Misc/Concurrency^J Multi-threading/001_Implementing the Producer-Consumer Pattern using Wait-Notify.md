Implementing the Producer/Consumer Pattern using Wait/Notify

Tuesday, February 19, 2019

10:31 PM

 

Before getting into the Producer/Consumer pattern let\'s understand what the Runnable pattern is. The Runnable pattern was the first pattern to use threads in JAVA. This was introduced all the way back in JAVA 1.0. New patterns were introduced in JAVA 5

 

**How to launch a new thread?**

A thread executes a task. IN JAVA 1, the model for a task is a Runnable interface

 

![Machine generated alternative text: public Interface Runnable void ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_000.png)

 

Since this interface has only one method in JAVA 8 it became a functional interface. Where we added an annotation to it \@FuncionalInterface. This did not add any sort of backwards incompatibility. It just leverage a tool of JAVA8.

 

This runnable interface can be implemented using LAMBDA expressions

 

![Machine generated alternative text: Runnable task System . out \"Hello world! \" ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_001.png)

 

The runnable pattern consists in creating an Instance of Runnable (like the image above), then creating a thread object by passing the runnable task as a parameter to the constructor of the THREAD class... and then launching this thread by calling the .start method:

 

Watch out... we need to Start the thread and NOT the RUN method since this might cause problems and actually try to run the RUN method of the task object we have passed as the parameter but it will not execute this code in another thread, it will execute it in the current thread...

 

![Machine generated alternative text: Runnable task Thread thread o; new System . out Thread(task Ill \"Hello world! \" thread. w, // NO ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_002.png)

 

Notice that we can easily figure out what thread we are actually executing by simply running the static method currentThread() to the Thread we have just created.

 

**How to stop a thread?**

This is a bit tricky. And there are traps. You should NOT use the method stop(). The people behind JAVA1 introduced this method and by the time they realized that it was not a good idea it was too late. They could not take the stop() method out considering it would introduce backwards incompatible changes to the code.

 

The way to stop a thread is by using the interrupt() method. This will not stop the thread, but just send the signal to the task the thread is running telling it is time to stop the thread.

![Runnable while task Thread the task o. itself ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_003.png)

 

This would be implemented like above.

 

![Stopping a Thread The call to interrupt() causes the islnterrupted() method to return true If the thread is blocked, or waiting, then the corresponding method will throw an InterruptedException The methods wait() / notify(), join() throw InterruptedException ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_004.png)

 

**Producer / Consumer pattern**

Easy to understand pattern.

![Producer / Consumer A producer produces values in a buffer A consumer consumes the values from this buffer Be careful: the buffer can be empty, or full Producers and consumers are run in their own thread ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_005.png)

 

 

![: lass Producer public \*\'Oid buffer buffer \[count++l ) lass Consumer public joid while buffer \[- buffer -count ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_006.png)

 

Now, looking at the image above we can see how this is obviously a producer consumer pattern BUT it is quite the naïve one. It is pretty evident that there is race condition in this example. This will corrupt the array.

 

How can we fix this?

1.  We can synchronize the access to the array (as we mentioned in the previous page)

    a.  ![class Consumer public void synchronized while buffer buffer \[ \--count class Producer public \'Oid synchronized while buffer \[count buffer ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_007.png)

2.  This is actually not a good idea because we could still try to access our buffer while each thread is in which ever method and potentially getting out of sync again. The real fix comes from using a single synchronized object we can use around.

    a.  ![private class Consumer public void synchronized(lock) { (buffer)) buffer \[ \--count lock ; class Producer public \'Old synchronized(lock) { buffer buffer \[count++\] ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_008.png)

 

But wait! **What happens if the buffer is empty?**

Well we could run into a nasty problem. We could have a thread get into the Consume method and therefore get stuck in our while loop waiting for the buffer to fill up. Since the produce method is waiting for the lock to get release, this will just make our application crash.

 

![Fixing the producer / consumer (again) We need a way to \"park\" a thread while he is waiting for some data to be produced Without blocking all the other threads So the key held by this thread should be released while this thread is \"parked\" This is the wait / notify pattern ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_009.png)

 

**Wait / Notify pattern**

![wait() / notify() wait ( ) and notify() are two methods from the Object class They are invoked on a given object The thread executing the invocation should hold the key of that object So: wait() and notify() cannot be invoked outside a synchronized block ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_010.png)

 

What happens when a thread calls the wait() method? Well, simply this will cause the key to be released from this thread. This will also put our current thread in a WAIT state. This is not the same state as when a thread is waiting at the entrance of a synchronized thread. The ONLY way to release a thread from its WAIT state is to call the Notify() on the lock object.

 

So what happens when we call notify()? This will release the thread that\'s in wait() state and it puts it in the runnable state.

 

If there are more than one thread in the WAIT state (common), the release thread will be chosen randomly. NotifyAll() method will also release all thread in the wait state.

 

![private class Producer public void synchronnzed(lock) { lock ; class Consumer public void synchronized(lock) { if lock . buffer)) o; if lock . buffer)) o; buffer \[count lock. o; buffer \[ -count lock. o; ](001_Implementing_the_Producer-Consumer_Pattern_using_Wait-Notify_011.png)

 

 

•
