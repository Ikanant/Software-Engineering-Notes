Stream API and Collectors

Sunday, March 3, 2019

9:42 PM

 

> **Map / Filter / Reduce Algorithm**
>
> Simple concept widely used in the industry.
>
> ![Map / Filter / Reduce • Example: • Let\'s take a list a Person List\<Person\> list = new ArrayList\<\>() ](001_Stream_API_and_Collectors_000.png)
>
>  
>
> ![Map / Filter / Reduce 1 st step: mapping The mapping step takes a List\<Person\> and returns a List\<lnteger\> The size of both lists is the same ](001_Stream_API_and_Collectors_001.png)
>
>  
>
> ![Map / Filter / Reduce 2nd step: filtering The filtering step takes a List\<lnteger\> and returns a List\<lnteger\> But there some elements have been filtered out in the process ](001_Stream_API_and_Collectors_002.png)
>
>  
>
> ![Map / Filter / Reduce 3rd step: average This is the reduction step, equivalent to the SQL aggregation ](001_Stream_API_and_Collectors_003.png)
>
>  
>
>  
>
> **What is a Stream?**
>
> A Stream is a Java TYPES interface. This Type is \<T\> so we can have Streams of integers, persons, Strings, etc... A stream in Java8 is a brand new concept. We could think of it as being a collection, but in fact is completely different.
>
> **What does it do?**
>
> It gives a ways to efficiently process large amount of data (in parallel even!). (Good for large/small amount of data)
>
> **What does efficiently mean?**

1.  Data can be process in parallel, to leverage the computing power of multicore CPUs

    a.  No parallelism logic needs to be written by me as the developer. Everything gets taken care of by just using this new tool

2.  Pipelined, to avoid unnecessary intermediary computations

    a.  Even if I have several operations on a given stream of data....all the operations are conducted on ONE task over the data

> **Why can\'t a Collection be a Stream?**
>
> Because Stream is a new concept and we don\'t want to change the way the Collection API works. Too many things already learned with the Collection API that would cause confusion to people learning the new tools with previous JAVA knowledge.
>
> **...again, what is a Stream? - How can I build one?**

-   A stream is an object which one can define operations. By operations we can think of a map / filter / reduce operations.

-   This object DOES NOT hold any data

-   An object that SHOULD NOT change the data it processes. If we are doing parallel work on certain datasets, modifying such data would cause major problems in our code. This rule is not enforced. Not by the compiler nor the JVM.

-   An object able to process data in ONE pass. Let\'s consider want to deal with a Stream for which we wish to map & filter & reduce ... we can do this in one task... we do not want intermediaries to deal with our data.

-   The stream object is optimized from the algorithm point of view, and able to process data in parallel.

> **How can we build a Stream?**
>
> Multiple ways... Lots of patterns...here is the most popular one:
>
> ![List\<Person\> persons = Stream\<Person\> stream = persons . stream(); ](001_Stream_API_and_Collectors_004.png)
>
>  
>
> ![= new ArrayList\<\>(); List\<String\> result List\<Person\> persons = = result: :add; Consurner\<String\> cl --- System.out: : print In; Consumer\<String\> c2 persons. stream() . forEach(c1. andThen (c2)) ; ](001_Stream_API_and_Collectors_005.png)
>
>  
>
> If we want to declare several consumers in a single stream...because the forEach function doesn\'t return anything the only way we could do that is by chaining the consumers into ONE and then passing it as a parameter for the forEach method.
>
>  
>
> **Now let\'s look at a second operations: Filter**
>
> ![Predicates combinations examples: Predicate\<lnteger\> Predicate\<lnteger\> Predicate\<lnteger\> Predicate\<lnteger\> Predicate\<lnteger\> pl --- p2 --- p3 p pl. and (p2) . or(p3); // (pi AND p2) OR p3 = p3. or(pl) .and(p2); // (p3 OR pi) AND p2 ](001_Stream_API_and_Collectors_006.png)
>
>  
>
> ![Machine generated alternative text: Use case: Predicate\<String\> p = Predicate. isEquaL (\"two\") Stream\<String\> streaml Stream\<String\> stream2 = \"two\", \"three\") = streaml.filter(p) ; The filter method returns a Stream This Stream is a new instance ](001_Stream_API_and_Collectors_007.png)
>
> The .of method above it\'s just creating a Stream out of the list of strings we are passing in... Same thing as if we had a list and we ran the .stream() on it. In this case notice how this .of method is static... which is something we need to remember was introduced as a capability of Java 8 to have static default methods declared in functional interfaces
>
>  
>
> ![A Second Operation: Filter Question: what do I have in this new Stream? • Simple answer: WRONG! The right answer is: nothing, since a Stream does not hold any data ](001_Stream_API_and_Collectors_008.png)
>
>  
>
> ![So, what does this code do? List\<Person\> list = Stream\<Person\> stream = list. stream(); Stream\<Person\> filtered = stream. filter(person -Y person.getAge() \> 20); Answer is: nothing This call is only a declaration, no data is processed ](001_Stream_API_and_Collectors_009.png)
>
>  
>
> The call to the filter method is what is commonly known as a LAZY call. It means that when we invoke that method, we can think of it as only a declaration but NO data is processed. NO DATA!
>
>  
>
> All the methods of Stream that return another Stream are LAZY. **An operation on a Stream that returns a Stream is called an intermediary operation.**
>
>  
>
> In the shot bellow we will look into another method we can use similar to the forEach function. The only difference between these two is that the peek method returns a Stream, while the forEach does NOT.
>
> ![• What does this code do? List\<String\> result = new ArrayList\<\>(); List\<Person\> persons = persons. stream( ) . peek(System.out : : print In) . filter(person -Y person.getAge() \> 20) . peek(result: : add) ; ](001_Stream_API_and_Collectors_010.png)
>
> **Answer:** This code does NOTHING. The first println is NEVER invoked, same as the add function call. These are just not doing anything since we are essentially trying to println on a stream.
>
>  
>
> ![stream . peek(System.out: : println) . filter (pl. or(p2)) . forEach (list: : ](001_Stream_API_and_Collectors_011.png)
>
>  
>
> Now in the above picture we DO in fact get things printed in the first System.out.println call, get things filtered and then added to the list. WHY though? Well, because the forEach doesn\'t return anything and it is NOT an intermediary operation.. It is a FINAL operation. Which triggers the processing of the data that the stream is connected too.
>
>  
>
> So just remember... only a FINAL operation will trigger the processing of the data the stream is connected too!
>
>  
>
> ![Summary The Stream API defines intermediary operations We saw 3 operations: forEach(Consumer) • peek(Consumer) • filter(Predicate) ](001_Stream_API_and_Collectors_012.png)
>
>  
>
> **The Map Operation**
>
> The map() returns a Stream, so it is an intermediary operation... so it DOES NOT process any data. The mapper function is modeled by the Function interface... (Recall this is provided in the standard functional interfaces toolbox from the JDK) and it has only one abstract method called apply. This method takes an object as parameter and returns another object... In our example the parameter would be a instance of Person and the return object would be an Integer.
>
>  
>
> **Flatmapping Operation**
>
> flatMap() takes a function as an argument. (same type of function as our map method)... for our map we get an object and return an object... but for a flatmap we get an object and we receive an stream of object
>
>  
>
> ![If the flatMap was a regular map, it would return a Stream\<Stream\<R\>\> Thus a « stream of streams » ](001_Stream_API_and_Collectors_013.png)
>
>  
>
>  
>
> **Reduction**
>
> There are two kinds of reduction in the Stream API.

1.  Aggregation = min, max, sum, etc...

    a.  ![How does it work? List\<lnteger\> ages = ; Stream\<lnteger\> stream = ages stream(); Integer sum = stream. reduce(Ø, (agel, age2) -\> agel + age2); 1 st argument: identity element of the reduction operation 2nd argument: reduction operation, of type BinaryOperator\<T\> ](001_Stream_API_and_Collectors_014.png)

    b.  What happens if the Stream is empty?

        i.  The reduction of an empty Stream is the identity element.

    c.  What happens if the Stream has only one element?

        i.  If the stream has only one element, then the reduction is that element.

    d.  ![• Examples: Stream\<lnteger\> stream = ; BinaryOperation\<Integer\> sum = (il, i2) -Y il + i2; Integer id = 0; // identity element for the sum int red = stream.reduce(id, sm); Stream\<lnteger\> stream = Stream.empty(); int red = stream.reduce(id, sum); System. out. println ( red) ; • Will print: ](001_Stream_API_and_Collectors_015.png)

>  
>
>  

1.  ![Machine generated alternative text: Optionals Then what is the return type of this call? List\<lnteger\> ages = ; stream = ages .stream(); max = stream. max( Comparator. natural Order ( ) ) ; Optional means « there might be no result » ](001_Stream_API_and_Collectors_016.png)

>  
>
>  
>
> ![• Reductions Available reductions: a max(), min() count() Boolean reductions allMatch(), noneMatch(), anyMatch() Reductions that return an optional findFirst(), findAny() ](001_Stream_API_and_Collectors_017.png)
>
>  
>
> Reductions are terminal operations! - Reductions do not return a new stream!! Reductions are called terminal operations!
>
>  
>
> **Terminal Operations**
>
> ![List\<Persony persons = ; minAge = persons. stream( ) .map(person -Y person.getAge()) . filter(age -Y age \> 20) . min (Comparator. natura LOrder( ) ) ; Stream\<lnteger\> Stream\< Int eger\> terminal operation ](001_Stream_API_and_Collectors_018.png)
>
>  
>
> ![Example, optimization: List\<Persony persons = ; persons. stream() . map(person person. getLastName()) . allMatch (length \< 20); // terminal op. The map / filter / reduce operations are evaluated in one pass over the data ](001_Stream_API_and_Collectors_019.png)
>
>  
>
> In the above example it is interesting to note that, let\'s assume the first person that is in the list does not have a Last name with a length greater than 20, then the process is done and we do not waste time checking the rest of the list. Efficient!
>
>  
>
>  
>
> **Collectors**
>
> This is the SECOND type of reduction!! - earlier we went over the FIRST one.

-   Mutable Reduction

-   Instead of aggregating elements, this reduction put them in a \<\<container\>\>

    -   What container is a string

>  
>
> ![• Example: List\<Person\> persons = String result - persons. stream() . filter(person - \> person .getAge() \> 20) . map(Person : : getLastName) . col lect( Collectors. joining( , Result is a String with all the names of the people in persons, older than 20, separated by a comma ](001_Stream_API_and_Collectors_020.png)
>
>  
