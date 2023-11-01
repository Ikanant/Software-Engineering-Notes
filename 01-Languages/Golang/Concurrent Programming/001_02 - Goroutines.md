02 - Goroutines

Tuesday, May 3, 2016

9:18 PM

A Goroutine is Go's name for its light weight thread like construct... It belongs to a an object called green or virtual threads.

Due to the fact that they are NOT tighed to the Operating System Processors Thread, the language can shape Goroutines in a way that is optimized for the type of problems that Go is trying to solve.

- Lightweight
  - We let them start extremelly small and give them the ability to grow should the app demanded
- Scale
- Schedule
  - Since they are Virtual, the Go run time can manage the way they are allocated to the processor thread that is available to the application.

**Parallelism:**

If we want our application to run Goroutines in parallel we only need to know one thing: GOMAXPROCS

With GOMAXPROCS we tell the program how many processors we want taking care of our application... By default, all go applications can only use the single logical processor...

GOMAXPROCS: sets the maximum number of CPUs that can be executing simultaneously and returns the previous setting

**package main**

**func main() {**

> **go func() {**
>
> **println(\"Hello\")**
>
> **}()**

> **go func() {**
>
> **println(\"Go\")**
>
> **}()**

**}**

With the code above, we will not get any result if running the go file.... It turns out we are pretty much dealing with 3 (THREE) Goroutines here...meaning that the main routine is also sort of consider one. When the main routine is done... the whole app exits
