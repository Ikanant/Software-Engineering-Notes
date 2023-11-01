01 - Creating a Resource Server & Templating

Friday, April 29, 2016

11:06 AM

> Go is not specifically design for Web server development, but it is really good at it.
>
> Why this course?

-   New to Go

-   Web Developer

-   System Developer

-   Curious

> **[Goals of the course]**

-   Working with Templates

-   MVC Framework

-   Database Access (Sequel)

-   Unit Testing (Built into GO)

-   Session Management

-   Only Core

> **[Demonstration Application]**
>
> Our web application will sell and lead the web market for Lemonade Stand Supply businesses.
>
> **[Setting up the Environment]**

-   Go Dev tool

-   Eclipse

-   gocode //offer editors like Eclipse

>  
>
> **[Defining a Resource Server]**
>
> A resource server was one of the first type of server. A server is setup to receive request via HTTP or a similar protocol. It determines if the request resource such as a file in the requested resource exists. If it does then the server sends the requested file back to the client. This process is a basic concept that we are going to use in this example\...
>
> Our server needs to do two things:

-   Listen on a TCP port 

    -   We could do this with other protocols. but HTTP is built on top of the TCP protocol so we will use that.

-   Logic to handle request

    -   Return a file if it is found or an error if it isn\'t.

> **[Basic HTTP Objects]**
>
> Go is gonna make this really easy for us. Most of what we will need is already located in the net/http package of the standard library. Specifically:

-   http.ListenAndServe

    -   When called this function will block our main thread, so it is important to call this after all other configuration of the server is complete.

    -   When the application is running, GO will manage each request by the use of GOROUTINES. This are lightwave construct used by GO to support concurrent use such as listening to HTTP request while also responding to requests.

-   http.Handle

    -   Allows the URL path to be handled by an object that implements the HTTP handler interface.

    -   Using this method is good to deal with scenarios with a lot of custom logic is required to deal with the request.

    -   This style lends itself to be turned into controllers really easily.

-   http.HandleFunc

    -   Other major way that we can use to register a listener on a specific request path.

    -   In this case we register a FUNCTION to handle the request instead of an object.

    -   Meant for simpler requests.

>  
>
> **[Handling Request with http.Handler]**
>
> package main
>
>  
>
> import(
>
> \"net/http\"
>
> \"strings\"
>
> \"os\" // Will allow me to access OS specific functions like opening a file
>
> \"bufio\" // Will alow me to implement the buffering logic
>
> )
>
>  
>
> func main(){
>
> http.Handle(\"/\", new(MyHandler))
>
> http.ListenAndServe(\":8000\", nil)
>
> }
>
>  
>
> type MyHandler struct {
>
> http.Handler
>
> }
>
>  
>
> func (this \*MyHandler) ServeHTTP (w http.ResponseWriter, req \*http.Request) {
>
>  
>
> path := \"public\" + req.URL.Path
>
>  
>
> //data, err := ioutil.ReadFile(string(path))
>
> f, err := os.Open(path) // Will open the file without actually reading anything
>
>  
>
> if err == nil {
>
> bufferedReader := bufio.NewReader(f) // Will be assigned during the bufio new reader function
>
> var contentType string
>
>  
>
> if strings.HasSuffix(path, \".css\"){
>
> contentType = \"text/css\"
>
> } else if strings.HasSuffix(path, \".html\"){
>
> contentType = \"text/html\"
>
> } else if strings.HasSuffix(path, \".jpg\"){
>
> contentType = \"image/jpg\"
>
> } else if strings.HasSuffix(path, \".png\"){
>
> contentType = \"image/png\"
>
> } else if strings.HasSuffix(path, \".js\"){
>
> contentType = \"application/javascript\"
>
> } else {
>
> contentType = \"text/plain\"
>
> }
>
>  
>
> w.Header().Add(\"Content-Type\", contentType)
>
> //w.Write(data)
>
> bufferedReader.WriteTo(w)
>
> } else {
>
> w.WriteHeader(404)
>
> w.Write(\[\]byte(\"404 - \" + http.StatusText(404)))
>
> }
>
> }
>
> With the above code it has been really easy to handle HTTP requests to our application. But guess what, GO offers even better functionality to our code... we actually only needed:
>
> package main
>
>  
>
> import(
>
> \"net/http\"
>
> )
>
>  
>
> func main(){
>
> http.ListenAndServe(\":8000\", http.FileServer(http.Dir(\"public\")))
>
> }
>
>  
>
> **[HTML Templates]**
>
> **[Delivering Static Content with Templates]**
>
> In the past module we already worked on returning static content from our web application. We did by either returning a string literal, or a file retrieved from the file system.
>
> Now, we are gonna start our investigation of templates by returning static content, but using templates instead. While this is a very inefficient way to return static content, it will lay the foundation that we will build on upon this module and the next.
>
> So, whats inside the [Templating Library?]

-   template.New

    -   Allows to create a new template.

    -   Why do we have this function instead of using the GO default new () one?

        -   The answer lies in the fact that GOs strcut type does NOT have the concept of the constructor function like in other OO languages

    -   Takes a String parameter that will be used as the NAME of the template

-   template.Parse

    -   This is a METHOD instead of a FUNCTION... since this method is bound to the template struct, it runs in the context of those objects

    -   its role is to accept a string resource and use that for the definition of an actually template

-   template.Execute

    -   It accepts 2 parameters: A writer and an arbitrary object

    -   When called it will evaluate the template and bind the object parameters into it.

    -   Finally it will stream the resulting text into the provided writer

> **[Demo: Static Tempaltes]**
>
> package main
>
>  
>
> import(
>
> \"net/http\"
>
> \"text/template\"
>
> )
>
>  
>
> func main(){
>
> http.HandleFunc(\"/\", func(w http.ResponseWriter, req \*http.Request) {
>
> w.Header().Add(\"Content-Type\", \"text/html\")
>
> tmpl, err := template.New(\"test\").Parse(doc)
>
>  
>
> if err==nil {
>
> tmpl.Execute(w, nil)
>
> }
>
> })
>
>  
>
> http.ListenAndServe(\":8000\", nil)
>
> }
>
>  
>
> // \` = Multiyline string (using the back tick)
>
>  
>
> const doc = \`
>
> \`
>
> **[Making Dynamic Templates using Strings]**
>
> {{.}} The period here is what is called a PIPELINE in GOs templating terms. It is a path that the template will take through the data context to get to the value that needs to be injected.
>
> {{.}} When setting the pipeline equal to the **. (period)** tells the template to use the data context itself as the value
>
> tmpl.Execute(w, req.URL.Path)
>
> **Hello {{.}}**
>
>  
>
> Go will also accept arbitrary objects to generate the templates final output\...
>
> If we want to send an arbitrary object for our template we would do:
>
>  
>
> type Context struct{
>
> Message string
>
> }
>
> if err==nil {  
>
>      context := Context{\"Object Message\"}
>
>      tmpl.Execute(w, context)
>
> }
>
> **Hello {{.Message}}**
>
> If the member used for the context is a datafield (like above) then that value will be used. Otherwise, if it is a method, that would also work and just get the return value of such method.
>
>  
>
> **[Adding Branching Logic to Templates]**
>
> The main branching logic used for templates are:

-   if

-   else if

-   if else if

> Logical tests:

-   eq

    -   "equal\"

    -   eq 1 (0+1) (2-1) =\> true

    -   ne

        -   "not equal\"

        -   lt

            -   "less than\"

            -   gt

                -   "greater than\"

                -   le

                    -   "less than or equal too\"

>  
>
>  
>
>  
>
>  
>
> **[Looping & Sub-templates (FULL CODE TO STUDY)]**
>
> package main
>
>  
>
> import(
>
> \"net/http\"
>
> \"text/template\"
>
> )
>
>  
>
> func main(){
>
> http.HandleFunc(\"/\", func(w http.ResponseWriter, req \*http.Request) {
>
> w.Header().Add(\"Content-Type\", \"text/html\")
>
> templates := template.New(\"templates\")
>
> templates.New(\"test\").Parse(doc)
>
> templates.New(\"header\").Parse(header)
>
> templates.New(\"footer\").Parse(footer)
>
>  
>
> context := Context{
>
> \[3\]string{\"Lemon\", \"Orange\", \"Banana\"},
>
> \"BIG TITLE\",
>
> }
>
> templates.Lookup(\"test\").Execute(w, context)
>
> })
>
>  
>
> http.ListenAndServe(\":8000\", nil)
>
> }
>
>  
>
> type Context struct{
>
> Fruits\[3\] string
>
> Title string
>
> }
>
>  
>
> // \` = Multiyline string (using the back tick)
>
> const doc =
>
> \`
>
> {{template \"header\" .Title}}
>
>  
>
>  
>
> {{template \"footer\"}}
>
> \`
>
>  
>
> const header =
>
> \`
>
>  
>
>  
>
>  
>
>  
>
>  
>
> \`
>
>  
>
> const footer =
>
> \`
>
> \`
>
> ![](000_01_-_Creating_a_Resource_Server_&_Templating_000.png)
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
> **Hello world**
>
>  
>
> **List of Fruit**
>
>  
>
>  
>
> {{range .Fruits}}

-   {{.}}

> {{end}}
