04 - Routing

Wednesday, August 31, 2016

6:06 PM

**The how...**

By using Angular we can write a large range of applications that do not need to rely on a server call to serve html content to the client in a fast and efficient way.

The most polular way to tackle this is by building a Single Page application that only loads ones through the browser, but that appears to have different views and tabs to the user. The best way to understand this is by going back to the JavaScript file where we created our App module. In there will add a .config tag to our module that will dictate its \"templateUrl\" and its \"controller\". In our front end we would then not need to specify in the actual html the ng-controller tag, and we would render such route changes using the known: \<ng-view\>\</ng-view\> tag.

Notice that the url will change to urls using \'#\' symbol which is a way for the browser to load content into the page without reloading the page all together.

Note: When writing things like **getAllEvents()** in our EventData service and ask for our resources to get our information, we do not need to do a:

> resource.get(...);
>
>  

Instead we will do a:

> Resource.query();
>
>  

The only difference between get and query is that with query we will expect a Array to be returned back.

**The \# in the URL**

So far we have been seeing changes in the url that start with the \# sing. As we mentioned before this is used because the browser can handle that kind of query and understand we will not be re-submitting an http request and therefore reload the page accordingly.

The answer to removing the \# sign lies on using HTML 5 :)

With HTML5 the application can be more smart about our URL and allow redirection without the use of the \# sign. The one thing to note is that once we set our application to use html5 by adding this line to our module:

> ***\$locationProvider.html5Mode(true);***

Angular will know how to handle such request BUT our server (any server) will not. So in the case of the current one I am writing (NodeJS) I will just set my express app to listen to anything and default to my index.html page which has the ng-view that we are currently using for the rest of my pages.

![Machine generated alternative text: 17 app. get( /data/event/ : id , events. get) ; app.post( /data/event/ : id\' , events. save) ; app. get( /data/event\', events. getA11); function(req, res) { res. sendFi1e(rootpath + \'app/ index. html • ) ; ](003_04_-_Routing_000.png)

Once we are done setting up our error we will see how the index.html page will load properly in our browser when we try to access any url... BUT we are not done. When trying to access any of our pages we see index.html loading but not filling any of the ng-view tag with the proper content. What happens here is that ANGULAR does not know where our base route is to get such files. So in our main page (in our scenario index.html) we need to set the following line:

**\<base href=\"/\" /\>**

Just to clarify what the BASE tag we added does... in our URL (which for example can be /events) our single page app is mounted. It is possible that our base html page like our Index.html is placed inside an \"view\" folder or something along those lines. If that was the case, then we would rewrite the base address to the proper location. It tells Angular when it parses the url, where to start parsing from.

This no base error could be also handled from our eventsApp module to not require the html base tag (similar as we activated the HTML5 mode) but this will not work on IE9 and we would have to prefex some urls around because Angular is going to get confused on where to go then
