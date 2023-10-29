Getting Started

Saturday, April 25, 2020

12:03 PM

 

Starting things off assuming I created a new dotnet core web app in VS2019. While writing this notes I selected Dotnet Core 3.1...

 

*Removed default controller and default poco...*

 

**Program.cs**

Starting point of my application... We are starting a web application and it NEEDS to be hosted...that\'s what\'s created by the **CreateHostBuilder** function.... We call build on the builder and run to get it started... Leaving everything untouched will just get us the default settings and by default the builder will use the *Startup* class to get started...

 

![\[S namespace CourseLibray.API public class Program public static void Main (string\[\] args) CreateHostauiIder(args) . Build . Run ; public static IHostauiIder Cre eHostauiIder(stringC\] args) Host. CreateDefauIt8uiIder(a . Conf igu reWebHostDef a u It s Builder webau ilder. LlseSta rtup\<Sta rtup\> ; ](000_Getting_Started_000.png)

 

**Startup.cs**

In the constructor the configuration object is injected. This configuration is the only thing we need \*for now\* to get info from app settings and whatnot.

 

**Methods of importance:**

-   *ConfigureServices*

    -   Used to ADD services to the BUILT IN dependency injection container AND to configure those services.

    -   Services (just like the architecture we choose at work)... are a broad concept. A Service is a COMPONENT that intended for common consumtion in an app... SO the services we add here, can be later be injected into OTHER pieces of code that live in our application... WITHOUT the need of XML files.

    -   In previous versions of DotNet core this is where we saw: **services.AddMvc**

        -   We can still do this... BUT addMvc still registers services that are not typically required when building APIs... like service for VIEWS, PAGES and HELPERS

    -   AddController

        -   Only registers services that are typically required by APIs

            -   Controllers

            -   Model Binding

            -   Data Annotation

            -   Formatters

>  

-   Configure

    -   This is the spot where we configure the services that are added in the ConfigureServices method. So we call this function after that.

    -   Here is where we define how the application will respond to individual HTTP requests

    -   I will write some further notes here once I start creating controllers... the IMPORTANT thing to note here is that EACH request travels through ALL pieces of middleware we add here... IN ORDER... and each piece of middleware can short circuit request so it doesn\'t pass through to the next one.

 

**Entity Framework**

So, this is the part where I don\'t have much experience working with this... BUT for me right now it doesn\'t matter all that much. For REST it DOES NOT matter what technology the data store is accessed through.. Nor how the data is stored... The code we will write will be over a repository, where we will keep our data persistent agnostic.

 

We will need some references to our project in order to use Entity Framework Core though:

-   Microsoft.entityFrameworkCore

-   Microsoft.entityFrameworkCore.SqlServer

    -   We will work with VS local DB instance

-   Microsoft.entityFrameworkCore.Tools

    -   Will allow me to easily add migrations.

>  
>
>  

Before I start changing things into the official Photography API ... I will follow the pluralsight course to create Authors and Courses in our DB. I will import:

-   Entities:

    -   2 Have been added: Author and Course.cs

-   DBContexts

    -   DB Context that will hold the COurseLibraryContext

    -   Exposes TWO DB sets... One of Authors and one of Courses and it ALSO contains some code to SEED the DB with some dummy data for testing purposes . This will need to run with a migration

    -   ![public Authors { get; public Courses { get; set; set; protected override void modelauilder) // seed the database with dummy data modelauilder. ) . HasData ( new Author() Guid . Parse (\"d28888e9-2ba9-473a-a4øf-e38cb54f9b35\"), FirstName = \"8ery\" \"Griffin Beak Eldritch\", LastName --- DateOfairth new DateTime(165ø, 7, 23), Maincategoty = \"Ships\" new Author() Guid . Parse ( \"da2fd6ß9-d754-4feb-8acd- c4f9ff13ba96\" ) , FirstName = \"Nancy\" \"Swashbuckler Rye\", LastName --- DateOfairth new DateTime(1668, 5, 21), Maincategoty = \"Rum\" ](000_Getting_Started_001.png)

-   Repository:

    -   I don\'t plan to change much here for now...the only thing to care about is that I will be able to call the repo from my controller to change/update/delete my data in the DB.

-   **Startup.cs** changes:

    -   I am now registering the repo and the context.

    -   For now I am hard coding the connection string:

    -   ![public void ConfigureSetwices (ISe:wiceCoIIection setwices) services . AddControIIers ; services .AddScoped\<ICourseLibrayReposit0D\', CourseLibrayReposit0D\' services . option s . LlseSq ISen•er ( ( Id b ) sq Iloca b ; Data ba se=Cou rseLibra ; Tru sted_Con nection=True ; \" ) ](000_Getting_Started_002.png)

-   **Program.cs** changes:

    -   Ensure the DB is deleted so we start with clean slate each time... FOR NOW

    -   We then ensure is created and migrated

> ![// migrate using (var try the database. aest practice = in Main, scope = host.Setwices .CreateScope()) using service scope var context = // for demo purposes, delete the database & migrate on startup so // we can start with a clean slate context. Database. EnsureDeIeted ( ) ; context. Database. Migrate ( ) ; catch (Exception ex) var logger s cope. Setwiceprovider. GetReq u iredSetwic I Logger\< ( ) ; logger. LogError(ex, \"An error occurred while migrating the database. // run the web app host. Run(); ](000_Getting_Started_003.png)

-   In order to get the migration part to work I will first have to add a Migration:

    -   Package Manager Console

    -   Add-Migration \<Name of my migration\>

    -   ![ackage Manager Console Package source: All Default project HdezPhotography.Api Each package is licensed to you by its owner. NuGet is not responsible to determine any dependencies . Package Manager Console Host Version 5.5.0.6473 Type •get-help NuGet\' to see all available NuGet connands. Add-Migration InitialMigration ](000_Getting_Started_004.png)

 

 

**REST is...**

REST isn\'t just about building an API that consists of a few HTP services that return JSON. That\'s a web API... REST is much broader than that...it is an ARCHITECTURAL STYLE.

 

Definition: **Representational State Transfers** intended to evoke an image of how a well-designed web application behaves:

-   A network of web pages (a virtual state-machine)...

-   ... where the user progresses through an application by selecting links (state transitions)...

-   ... resulting in the next page (representing the next state of the application) being transferred to the user and rendered for their use

 

![Introducing REST REST is an architectural style, not a standard We use standards to implement this architectural style REST is protocol agnostic ](000_Getting_Started_005.png)

 

**How do I build such a system then?** An architectural style is defined by a set of constraints... and these constraints is what WE have to adhere too.

 

![Learning What the REST Constraints Are About REST is defined by 6 constraints (one optional) A constraint is a design decision that can have positive and negative impacts ](000_Getting_Started_006.png)

 

 

**REST 6 Constraints to keep in mind:\
** 

1.  Uniform Interface

    a.  The API and its consumers **share one single**, technical interface. As we are typically working with HTTP protocol, this interface will be seen as a combination of:

        i.  Resource URIs: Where we can find the resources

        ii. HTTP methods: How do we interact with them

        iii. HTTP media type: Like json or xml

    b.  **There are 4 sub-constraints** to worry about:

        i.  Identification of Resources. A resource is conceptually separate from tis representation. This just means that the URI we use should not worry about what kind of data we get back.. We use the same uri and just change the media type and we will get different type. So that is 2 different representations of the same resource.

        ii. Manipulation of Resources through Representations. This state that is returned by the API should be enough to update or delete that data (granted we have the right permissions)

        iii. Self-descriptive Message. Each message MUST include enough information to describe how to process it.

        iv. HATEOAS - Hypermedia as the Engine of Application State

            1.  This is the one that a lot of RESTful systems fail to implement. Hypermedia is a generalization of Hypertext (links)

            2.  This just drives HOW to consume and use the API. It tells the consumer what I can do with the API. Can I delete the resource or edit it? How can I create.... This allows for a self-documenting API

            3.  ![](000_Getting_Started_007.png)

            4.  Through these links we drive application state

2.  Client-Server

    a.  Client and server are separated... which allow us to have separation of concerns. The CLIENT and the SERVER are completely separated.

3.  Statelessness

    a.  The necessary state to handle every request is contained within the request itself. The state is NOT kept on the server but on the client... and when the client request a resource, that request contains the info necessary to SERVE the request

4.  Layered System

    a.  Client CANNOT tell what the layer it\'s connected to.

5.  Cacheable

    a.  EACH response message must explicitly state if it can be cached or not

6.  Code on Demand (optional)

    a.  Server can extend client functionality. Let\'s say the client is a web app, the server can transfer JS code to the client to extend its functionality. This is optional and typically applies to web apps and NOT apis.
