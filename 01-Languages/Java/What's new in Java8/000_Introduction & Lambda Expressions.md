Introduction & Lambda Expressions 
 
Saturday, March 2, 2019 
 
10:12 AM 

Course Goals:

-   Most useful new parts of Java 8
-   Lambda expressions
-   The Stream API and Collectors
-   And many bits and pieces
-   Java FX - new Graphical user interface of Java
-   Nashorn - new Javascript engine introduced in the JVM

Let\'s look at a simple interface \'FileFilter\' being implemented and used in the classic Java way:

![• Let\'s implement this interface public class JavaFi1eFi1ter implements FileFi1ter { public boolean accept(Fi1e file) { return file. getName() . endsWith(\" . java\"); And use it: JavaFi1eFi1ter fileFi1ter = new JavaFi1eFi1ter(); File dir new /tmp\"); File\[\] javaFi1es = dir. listFi1es(fi1eFi1ter); ](000_Introduction_&_Lambda_Expressions_000.png)

Now let\'s do the same (most common way of handling this) is to create not a concrete class but an anonymous class instead. Anonymous classes are simply classes with no name. This will allow us to put the technical code that will filter out the technical source code at the same place as the place where the code is used.

![• Let\'s use an anonymous class FileFi1ter fileFi1ter = new FileFi1ter() { \@Override public boolean accept(Fi1e file) { return file. getName() .endsWith(\" . java\"); File dir new /tmp\"); File\[\] javaFi1es = dir. listFi1es(fi1eFi1ter) ; ](000_Introduction_&_Lambda_Expressions_001.png)

**What is a Lamda Expression for then?**

-   To make instances of anonymous classes easier to write... AND TO READ

![This is a Java 8 lambda expression: FileFi1ter filter = (File file) -Y file.getName() .endsWith(\". java\"); ](000_Introduction_&_Lambda_Expressions_002.png)

... **so, again, WHAT IS A Java 8 Lambda Expression?**

Just another way of writing instances of anonymous classes, and hopefully a more readable way to writing such instances.

![Several Ways of Writing a Lambda Expression The simplest way: FileFi1ter filter = (File file) -Y file .getName() .endsWith(\". java If I have more than one line of code: Runnable r for (int i = 0; i \< 5; i++) { System. out .println( \"Hello world! \" ) ; ](000_Introduction_&_Lambda_Expressions_003.png)

**Three Questions About Lambdas**

1.  **What is the type of a lambda expression?**
    a.  In JAVA everything has a type, so what is the type of a Lambda expression
2.  **Can a lambda be put in a variable?**
    a.  If this the case this would be a powerful tool because methods would be able to exchange lambdas to pass lambdas as parameters and to return lambdas
3.  **Is a lambda expression an object?**
    a.  Toughest question. In java EVERYTHING is an object. Every piece of code we write has to be written inside a class, so a Lambda expression an object?

Let\'s Dive in:

1.  **Functional Interface**
    a.  Functional Interfaces is simply an interface with some constraints (that we are going to see) so it is still quite a classic view of JAVA
    b.  **What is a Functional Interface?**
        i.  It is an interface with only ONE abstract method.
            1.  Why are we precising abstract methods? Until Java 7 we could not put anything else in an interface than an abstract method apart of a constant (public static final variables)... So in Java8 we see that Abstract methods are NOT the only piece of code that we can put in the interface (we will go into more detail on this later)
            2.  One important thing to not is that though functional interface is a concept newly introduced in JAVA8, old interfaces (which follow the pattern of having only ONE abstract method declared for them are now considered Functional interfaces as well
            3.  ![public interface Runnable { run ( ) ; public interface Comparator\<T\> { int compare(T t1, T t2); public interface FileFi1ter { boolean accept( File pathname); ](000_Introduction_&_Lambda_Expressions_004.png)
        ii. Methods from the Object class don\'t count!
            1.  When we count the method of an interface to check if that interface is functional or not, the method from the object class don\'t count. This can be confusing because technically all the object in Java are extending the Object class so why would they need to declare the methods from the object class into the interface? - When someone declares a method from the object class in the interface, it is usually to define some documentation to give some special semantic and to add some JavaDoc that might be different from the object class.
            2.  ![public interface MyFunctiona11nterface { someMethod ( ) ; \* Some more documentation equals(Object o); ](000_Introduction_&_Lambda_Expressions_005.png)
        iii. \@FunctionalInterface - Functional Interfaces can be annotated, BUT this is not a requirement. It is just here for convenience, the compiler can tell me whether the interface is functional or not
```{=html}
<!-- -->
```
2.  **YES**
    a.  I can easily put a Lambda expression in a variable. In fact, we did that across the 3 sample codes I wrote in this course. The consequences of this, is that a lambda expression can be taken is a parameter by a method, returned by a method and it can be moved around easily.
    b.  ![Comparator\<String\> c --- (String sl, String s2) -Y Integer s2.1ength()); ](000_Introduction_&_Lambda_Expressions_006.png)
3.  **This question is tougher:**
    a.  ![Comparator\<String\> c --- (String sl, String s2) -Y Integer. s2.1ength()); Comparator\<String\> c = new Comparator\<String\>(String sl, String s2) { public boolean compareTo(String sl, String s2) { Integer s2. length()); ](000_Introduction_&_Lambda_Expressions_007.png)
        i.  What is the biggest differences between the above two solutions? - The difference is that the instance of the anonymous class is created using the keyword **new** so we are explicitly telling the JVM to create a new object in this case. Creating a new object is NOT free. We need to create/allocate/clean memory, execute static initializers etc.... And once all of this is done it will execute the constructor from the object class and all their inheritance. This can be HEAVY... This is NOT the case when creating a Lambda expression!
            1.  The JVM does NOT create a new object every time I use a Lambda expression. So it is much LESS work to use a Lambda expression!
    b.  **Final Answer: NO** - but it is not a clear no. In fact the lambda expression is still recorded as an object inside the JVM. It is an object of a new kind (in Java8) which is called **Object without an identity.**
        i.  We are not going to dive too deep into this, but it is just worth nothing that Lambda expression should not be used as a regular object. We should never be calling the methods from the object class .equals() or .toString() on a Lambda expression. A Lambda expression should be seen as a piece of code that can used and moved around but NOT as an object.

**Functional Interfaces Toolbox**

In Java 8 we also got a pretty fancy package full of functional interfaces... more specifically 43 of them. Though we are not going to go in depth into each of them, they can all fall under 4 main categories. We are going to look into that.

1.  Supplier
    a.  Single interfaces that doesn\'t take any object but that provides a new object
    b.  ![\@Functiona11nterface public interface Supplier\<T\> { T get(); ](000_Introduction_&_Lambda_Expressions_008.png)
2.  Consumer
    a.  Accept an object and doesn\'t return anything back
    b.  Example: System.out.println(). This is the first consumer interface we can think off.
    c.  BiConsumer
        i.  This is a special kind of consumer. This type of interface takes 2 objects instead of 1. (they can be of different types)
    d.  ![unctionallnterface public interface { void accept(T t); \@Functiona11nterface public interface BiConsumer\<T, void accept(T t, U u); ](000_Introduction_&_Lambda_Expressions_009.png)
3.  Predicate / BiPredicate
    a.  Takes an object as a parameter and then returns a boolean.
    b.  ![\@Functiona11nterface public interface Predicate\<T\> { boolean test(T t); \@Functiona11nterface public interface BiPredicate\<T, { boolean test(T t, U u); ](000_Introduction_&_Lambda_Expressions_010.png)
4.  Function / BiFunction
    a.  Takes an object as a parameter and returns another object
    b.  ![\@Functiona11nterface public interface Function\<T, R apply (T t); \@Functiona11nterface public interface BiFunction\<T, R apply (T t, U u); U, ](000_Introduction_&_Lambda_Expressions_011.png)
    c.  Notice how in the above shot of the BiFunction we are dealing with 3 generic types T U R so we need to have some knowledge of generics in order to understand what\'s going on.
    d.  There are special cases of functions within this category:
        i.  UnararyOperator
            1.  Takes an object and returns an object of the same kind. For example the Identity method for instance, is an example of an UnaryOperator. We also have a BinaryOperator as well

Also:

![More Lambda Expressions Syntax Most of the time, parameter types can be omitted • • Comparator\<String\> c = (String sl, String s2) -Y Integer. compare (sl. 1 ength ( ) , Becomes: (sl, s2) -Y Integer. compare (s 1.1 ength ( ) , s2. length ( ) ) ; s2.1ength()); ](000_Introduction_&_Lambda_Expressions_012.png)

This is the first time in Java that we can declare a variable without declaring the type!

**Method Reference**

Here we can see yet another way of dealing with Lambda expressions.

![This lambda expression: Consumer\<String\> c = s -Y System.out .println(s); • Can be written like that: Consumer\<String\> c = System.out: :println; ](000_Introduction_&_Lambda_Expressions_013.png)

This new syntax is composed of the object (in our case System.out), the ColonColon and then the name of the method that is invoked by this lambda expression. Note: We can use STATIC and non-STATIC method with this syntax.

**How do we process Data in Java in PARALLEL? - using this new tools**

First concern. Where are our objects when we are in a JAVA application. The answer is simple: Most of the time our object are in an instance of Collection. They could be in a List, a Set or a Map... but it is still an instance of the collection API. The Collection framework has been at the CORE of every Java application for years and is universally used.

**Can I process this data with lambdas?**

![List\<Customer\> list = list. forEach(customer • Or: List\<Customer\> list = list. forEach(System. out : : -Y System.out.println(customer)); println) ; ](000_Introduction_&_Lambda_Expressions_014.png)

But.... Then where does this forEach method come from? Recall that the way interfaces work in Java 7 is that if I add a method to an existing interface then this method needs to be added to all implementation of this given interface. So looking back to our example, adding a forEach method on the Iterable interface implies to refactor ALL the existing implementation of iterable. This can be possible because the people who upgrade Java also have a hand on all this core features but all the custom implementations of Iterable of all the JAVA applications would have to do that too. (Impossible)

![How to Add Methods to Iterable? • Without breaking all the existing implementations? public interface Iterab1e\<E\> { // the usual methods void forEach(Consumer\<E\> consumer); ](000_Introduction_&_Lambda_Expressions_015.png)

Woah, if I can\'t put the implementation of a forEach in the ArrayList (for example) then the choice has been made to put the implementation directly in the interface. This will be able to be achieved in the JAVA 8 through a NEW kind of method that we can put in an interface called the **default** method. This is just a regular method except with a default keyword in front. Putting code inside an interface is a revolution introduced in Java 8birthday gift

![public interface Iterab1e\<E\> { // the usual methods default void forEach(Consumer\<E\> consumer) { for (E e : this) { consumer. accept (e) ; ](000_Introduction_&_Lambda_Expressions_016.png)

![Default Methods This is a new Java 8 concept • It allows to change the old interfaces without breaking the existing implementations It also allows new patterns! • And by the way\... Static methods are also allowed in Java 8 interfaces! ](000_Introduction_&_Lambda_Expressions_017.png)

![Examples Of New Patterns Predicates Predicate\<String\> pl Predicate\<String\> p2 Predicate\<String\> p3 \@Functiona11nterface = s -Y s.length() \< 20; = s -Y s. length() \> 10; = pl. and(p2); public interface Predicate\<T\> { boolean test(T t); default Predicate\<T\> and(Predicate\<? super T \> other) { Objects. requireNonNuLL (other) ; return (t) - \> test(t) && other. test(t); ](000_Introduction_&_Lambda_Expressions_018.png)

![• Summary The new « lambda expression » syntax A lambda expression has a type :a functional interface Definition of a functional interface, examples Method and constructor references Iterable.forEach method Default and static methods in interfaces, examples ](000_Introduction_&_Lambda_Expressions_019.png)
