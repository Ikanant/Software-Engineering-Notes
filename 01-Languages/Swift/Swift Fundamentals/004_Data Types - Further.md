Data Types - Further

Tuesday, May 10, 2022

8:08 PM

 

**Enumeration**

 

Same old Enum type...\
 

![](004_Data_Types_-_Further_000.png)

 

Using a string is not ideal in most situations of course. Same with ints and whatnot... but how does Swift does it different?

 

![??? // Book, Movie, Music, Game, Event var itemType: new enqmerA4•tovx 4ype ](004_Data_Types_-_Further_001.png)

 

![// Style guide enum MediaType case book, is to make our types to start with capital case movie, music, game var itemType: MediaType itemType Media Type. book media type is of type: \\ (itemType) \" ) ](004_Data_Types_-_Further_002.png)

Easy... I can also write the enum cases in separate lines

 

Now, the one thing to note in Swift is that for enum types we often do not see the TYPE of the enum before consuming one of its properties... Apple allows for shortening things like so:

 

![override func didReceiveMemoryWarning() { super. didReceiveMemoryWa rning( ) // Dispose of any resources that can be recreated. func configureTextFie1d() { // these are all configured with enumerations = .nonel myTextFie1d. autocapita1izationType myTextFieId.autocorrectionType = . yes myTextFieId. returnKeyType = . default myTextFieId. keyboardAppearance = . light myTextFie1d. clearButtonMode = . never ](004_Data_Types_-_Further_003.png)

 

RAW VALUES are a great way to have some extra information for my enums. In order to set those raw values we just need to include the LITERAL data type we will be storing for the enum

![Enumerations: Raw Values { // String, Int, Double\... BottleSize : String case case case case case case case half = standard = \"1.5 lit resi magnum = jeroboam = \"3 lit resi rehoboam = \"4.5 lit resi methuselah = \"6 lit resi balthazar = \"12 lit resi myBott1e : BottleSize - . jeroboam var print (\"Your \\ ( ) is \\ ( myBott1e . rawVa1ue) myBott1e jeroboam is 3 litres \> Your ](004_Data_Types_-_Further_004.png)

 

![Standard Literals A literal is a representation Of a value in source code, such as a number or a string. Swift provides the following kinds of literals: Name Integer Floating- Point String Extended Grapheme Cluster Unicode Scalar Boolean Nil Dictionary Default Inferred Type Int Double String Character Unicode. Sca r Bool Optional Array Dictionary Examples 123, øblølø, 00644, øx 3.14, 6. ø2e23, øxAp-2 \"Hello\" , true, false nil \[\'la\": 1, \"b\": 21 ](004_Data_Types_-_Further_005.png)

 

**Associated Values**

When dealing with enums we might also NOT know the values that are going to be stored across some of the enums... for something like that we can have:\
 

![Enumerations: Associated Values MediaType { enum movie (String case music (Int) case book(String case ](004_Data_Types_-_Further_006.png)

 

Where we use the parenthesis (AND NOT THE COLON) to set the type of each case

![MediaType { enum movie (String case music (Int) case book (String case firstltem : Media Type var secondltem : Media Type var firstltem { switch . movie(let genre) case - . movie ( \"Comedy\" ) = . music(120) print(\"lt\'s a \\ ( ) movie\") genre . music(let bpm) case print( \"The music is \\(bpm) beats per minute\") . book (let author) case print (\"It\'s by \\ (author) ) ](004_Data_Types_-_Further_007.png)

This is a bit funny... but doing something like this we can use the keyword LET as the way we have a more descripting information about the enum itself

![10 15 16 17 19 20 21 23 // Test associated media types enum AssociatedMediaType { case book(String) case music(lnt) case movie(String) let associatedItemType: AssociatedMediaType = switch (associatedItemType) { case .bOOk(Iet bookGenre) : book genre is \\ (bookGenre)\") case . music: . book( \"comedy\" ) print ( \"The song has a bpm Of case .movie(let randomPropertyName) : book genre is \\ (randomPropertyName) ](004_Data_Types_-_Further_008.png)

 

 

**STRUCTS**

In my head I immediately think of these as POCO/POJO(s) ... but they are a bit more than that. Structs are the way Swift allows us to define new types... other languages of course have the concept of. Structs, but swift has a few differences.

 

Structures are important in Swift... the data types I\'ve been writing so far (String, Int, etc...) are all structs as far as Swift is concerned. This can be a bit confusing for people (including me) due to thinking String for example is coming from a class... and when we instantiate a string we are just creating an instance of that class... in Swift this is NOT the case.

 

Structs and Classes are very similar in swift though. When defining a struct, we should always define it with upper camel case. When variables are defined inside of a struct, we just say these are properties of the struct. When defining a property, we can always give it an initial value (which would then do type inference) but if we don\'t, then we will need to make sure we do some Type annotation.

 

![2S 31 32 33 struct Movie { var name: String var yearRe1ease: Int var rating = e var genre: String var dune Movie(name: \"Done\", \"Action\" print (dune. rating) yearRe1ease : 2021, rating: le, genre : ](004_Data_Types_-_Further_009.png)

Quick notes from the image above...

1.  See how we can define a default value for a property in the struct, when I did this I did not have to include it\'s value in the constructor (**in swift known as memberwise initializer).** That being said, when I tried to add the rating, I did so at the end of the constructor and this DID NOT work... I have to send the values to the constructor in the order that the properties got defined

2.  I can create a variable of type movie, but accessing it without having initialized it will result in your typical object not set to an instance of an object deal

    a.  ![35 38 39 struct Simple { var simpleName = \"Jon\" var banana: Simple print (banana. simpleName) @ Variable \'banana\' used before being initialized ](004_Data_Types_-_Further_010.png)

    b.  Notice how the struct only had one property that technically was already initialized... that will still throw an error

 

![25 35 struct Movie { var name: String var yearRe1ease: Int var rating var genre: String func summary String return \"My movie was release in and got a score Of \\ (rating) even though it was a movie!\" var dune = Movie(name: \"Done\" , yearReIease: 2e21, rating: Iø, genre: \"Action \" ) ](004_Data_Types_-_Further_011.png)

 

**OOP Questions**

Yes, this looks very similar to a class.. We got properties, initializers and now even methods. So what is the differences?

Easy:

1.  Structs cannot take part in inheritance

2.  Structs are VALUE type while Classes are REFERENCE types

 

Later, as we go into classes we will be expanding a bit more on structs... computed/lazy properties are incoming!

 

**DICTIONARIES**

So far, nothing special from what I already know

 

![Dictionaries (In various languages, called a Map, \...or Symbol Table, ..or Associative Array \...or Dictionary) 0 1 2 3 4 5 Hydrogen Lithium Sodium Potassium Rubidium Caesium Array keys SWA BAW CPA AAL BHA DAL values Southwest Airlines British Airways Cathay Pacific American Airlines Buddha Air Delta Air Lines Dictionary ](004_Data_Types_-_Further_012.png)

 

![2 3 4 5 6 7 8 9 10 11 12 13 14 15 // Dictionaries var airlines --- C SWA\": \'Southwest Airlines\" \"BAW . \"British Airways\" , BHA . \"Buddha Air\" , \"Cathay Pacific\" \] // Dictionary of String keys and String values var periodicE1ements: // Dictionary of Int var employees: \[Int: \[String: String\] keys and String values String\] ](004_Data_Types_-_Further_013.png)

 

Swift is smart enough to figure out (infer) the Dictionary type whenever we provide the format as the image above OR if we do not ... then we just do the \[\<keyType\>: \<valueType\>\]

 

One important thing to note is that EVEN THOUGH we might define a dictionary values as String types, they will return as Optionals... since when we search the key we want, swift doesn\'t know for sure if it exists or not in the dictionary

 

![43 48 // DICTIONARIES let airlines: \[String: string\] airlines = \[\'13B\": \"JetB1ue\", \"AA\": \"American Airlines\", var result: String = airlinest\"JE3\"\] ?? \"NOT FOUND\" print(result) \"D\": \"Delta\") ](004_Data_Types_-_Further_014.png)

 

 

**TUPLES**

Tuples are dope... in Swift they don\'t just store two values.. I typically think of Tuples like that... Tuples store a set of values... so as long as we wrap them in parenthesis, Swift will be happy... the real question is why? EASY, awesome return types!

 

If I wanted to grab individual items out of a tuple I can just treat it like an array... and have **myTuple.0** for grabbing the item from index zero of my tuple.

 

![// Don\'t need to specify the label Of my returned tuple func randomFunction() (String, year: Int) { let title = \"Random title\" let year = 123 return ( title, year) one = randomFunction() print (\"First: \\ (one.e) and print (\"First: \\ (one .ø) and Mane. year)\" ) (two, three) = randomFunction() print (two) print (three) ( \_ , five) --- print (five) ](004_Data_Types_-_Further_015.png)

 
