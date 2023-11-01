05 - Routing

Friday, April 29, 2016

11:37 AM

When dealing with Express, we can use multiple Routes under one express Router:

![](004_05_-_Routing_000.png)

And then just use:

App.use(\'/Books\', bookRouter);

**App.js is starting to look a bit crowed. We will need to start spliting it...**

...

Now, when dealing with single book pages, we are going to deal with routes that are dynamic. For example, all of our books will have an id... in that case, we need to handle routes like: /books/2

**Solution:** bookRouter.route(\'/:id\')

![](004_05_-_Routing_001.png)
