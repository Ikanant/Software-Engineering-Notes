02 (4) - Performance

Friday, April 29, 2016

12:22 PM

 

Database schemas are best stored using the 3NF (3rd Normal Form).

Even though this is also the case for MongoDB, it is also important to organize our data by how ofter some of the values get read or written within our application.

MongoDB:

-   Rich Documents

    -   We can store an Array of item or a value for certain keys can be entire other documents

    -   Allow us to rejoin data for fast access

        -   MongoDB doesn\'t support JOINS inside the Kernel. Instead, we will be doing our join on our application itself

        -   Joins are hard to scale -\> bad performance

-   No Constrains

    -   No foreign key or primary key:

        -   Problem solved with embedding

-   Atomic Operations: Either all occurs or nothing occurs. (No transactions though)

-   MongoDB has no declared schema... even though this is the case we will build structures similar to a schema

**GOAL:** Match the data access patterns of your application

**Alternative Schema Design for Blog:**

![](001_02_(4)_-_Performance_000.png)

 

MongoDB has NO transactions

Transactions offer: ACID

-   Atomicity (everything or nothing)

-   Consistency

-   Isolation

-   Durability

MongoDB HAS atomic operations

**How to overcome lack of transactions:**

1.  Restructure

    1.  Try to work within a single document

2.  Implement in SW

    1.  Create controllers within your software like semaphores, etc.

3.  Tolerate

    1.  Tolerate small inconsistancy. Often is not critical in system design for everyone to have the latest info from the database

Example of operations that are atomic within MongoDB:

-   Update

-   findAndModify

-   \$addToSet(within an update)

-   \$push within an update

**1-1 Relations:**

example: Employe:Resume relation \--\> each employee has a resume and each resume has an employee

There are multiple ways to make this work properly.

-   We can have a resume ID that points to the resume collection

-   We can have a employee ID that point to the employee collection

-   We can EMBED the resume collection inside the employee collection

    -   Determining if embedding is a good idea can be confusing and we should always consider the following points:

        -   Frequency of access

        -   Size of the items

            -   if Resume collection is larger that 16mb then we have a problem

        -   Atomicity of data

            -   If we know we cannot have ANY inconsistency within our document, embedding will be our best option

**1-MANY Relations:**

example: City:Person

-   We can create 2 collections that will allow us to link our data

    -   1: People collections: contains a CITY attribute

    -   2: City collections: \'\_id\' would then include the city name

How about **1-FEW **?

example: BlogPost:Comments

-   In this situation is feasible to have a collection of the 1 (POST) and within each post we can have an ARRAY of the comments

    -   We are not gonna have duplication because every comment falls under each particular post

-   This case will work very well having a single collection

**     **

**MANY-MANY Relations:**

example: Books-Authors \|\| Students-Teachers

Although it is a many to many relation there are not very large numbers for these examples. It tends to be Few to Few scenarios.

**Multikey Indexes**

---\> One of the main reasons why linking and embedding work so well within MongoDB

**Benefits of Embedding**

-   Improved READ performance

-   One round trip to the DataBase

 

**ODM - Object Document Mapper**

When having a regular application we deal with code sent to the database from APPLICATION ---\> DRIVER ---\> DB. An ODM will be inserted between the APP and the DRIVER

You tell the ODM how to handle your classes and you just hand your objects to it.

Advantages:

-   Helps shields from DRIVERS changes. If the API and the drivers change, we will be protected from those

-   The low level details to deal with when directly using a driver can be overwhelming and complicated. The ODM will be able to simplify that provided we use  can write our application without being concerned with all the inner workings of the mongo query language for example

Disadvantages:

-   Typically a very generic framework. It\'s the designed to work with pretty much any code based. There are certain inefficiencies that arise out of that

    -   Can give performance issues
