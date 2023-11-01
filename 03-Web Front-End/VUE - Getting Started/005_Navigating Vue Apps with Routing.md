Navigating Vue Apps with Routing

Monday, January 27, 2020

7:51 AM

Vue router is a library that allows us to add routing to our application. So we can route to pages/componnets and maintain the browser\'s history...

Main benefits:

1.  Modular, component-based configuration

    a.  Makes it easy to point right to the components

2.  Navigation API

    a.  Will allow us to do fun things like route to another route and pull/push parameters

3.  Route parameters

4.  Links with automatic active CSS class

5.  HTML5 history mode or hash mode

    a.  Hash mode is when we have \# inside the url

![Adding Routing to Your Vue App Add the router to your Vue app Define your routes Tell your app about the routes Add nav links and a place for the components to display ](005_Navigating_Vue_Apps_with_Routing_000.png)

Adding Vue Router is simple.. We just need to run the Vue-cli command:

**vue add router**

This command will install the router and add routing code to the app

![Add the Router to Vue Import the route definitions Add the routes to the app The Vue CLI does the work for you vue add router main.js import import \*import Vue from \'vue\'i from \'@/app.vue\' ; App router from \' ./router\' ; new Vue({ router, render: h =\> h(App) .\$mount( • #app\' ) ; ](005_Navigating_Vue_Apps_with_Routing_001.png)

The mode of our router is set to **history** by default because we don\'t want to use hash routing. This will allow the browser history to maintain all the different routes we will navigate too.

![Vue.use(Router); export default new Router({ : \'history\' , mode base: process.env.BASE URL, routes: \[ Add the router to this app Enable history mode redirect: \'/heroes\' } , path: Default route component: Heroes } , path: \'/heroes\' , : \'heroes\', name path: component: Villains } , \' /villains\', name: \'villains \' , component: NotFound } path: ](005_Navigating_Vue_Apps_with_Routing_002.png)

The one important thing to note about routes in vue is that instead of inserting our MAIN component directly into the app.vue file like before....we are now simply going to add the \<router-view\> component that will be used as the spot where our router is going to put all of our routed components

![1 2 3 4 5 6 7 8 9 10 \<template\> \<div id- \"app\" \> \<HeaderBar / \> \<div clan; \"main-section columns\" \> \<main \< router-view 8/ router-view \</main\> \</div\> \</div\> \< / template\> ](005_Navigating_Vue_Apps_with_Routing_003.png)

We will no longer need any import components in this vue file

**Adding navigation**

![Routing in the Template The Vue CLI adds the \<router-view\> and some \<router-link\> components Modify them as you need app.vue \<div \<div \<router-link \<router-link \</div\> \< router-view/ \> to=\"/\"\>Vi11ains\</router-1ink\>l to= \" /heroes \" link\> Navigate to this route Put the component that you navigate to, ](005_Navigating_Vue_Apps_with_Routing_004.png)

If we wanted to have some parameter in our routing we do something like this:

![path: \' / heroes/:id\' , \'hero-detail\', name: componet: HeroDetaiI, ](005_Navigating_Vue_Apps_with_Routing_005.png)

Where whenever we go into the heroes route and pass in an id we will be going to our HeroDetail component

Now we can parse that parameter by doing something like

**this.\$router.params.id**

But we want to do it cleaner like using props... easy:

![\' /her path \'hero import HeroDetait name : component: HeroDetai1, props: true, 1, ](005_Navigating_Vue_Apps_with_Routing_006.png)

We just set our route to have props:true. Done

This can cause problems though

When we are routing let\'s consider a component that we are routing too that takes in an ID as a param... when we traverse there (i.e. we click on a to: routing-link) we will pass in a number to our router BUT if we refresh the page (with the id parameter in the url... the browser is going to take that as a string... which could cause problems to our business logic. The solution to these type of problems is the fact that our props property in our route not only takes a boolean, it also takes a function... so we can do:

![path \' / heroes/:id\' . \'hero-detail\', name • component: HeroDetai1, ( { i d: parselnt(r.paramo. } ) , ](005_Navigating_Vue_Apps_with_Routing_007.png)

This will essentially continue to take a prop.... BUT do a small transformation before returning it back

**Eager vs Lazy Loading**

Eager loading: We load our components at once with all the JS it wants

![29 30 31 32 33 34 35 36 37 \' / about\', path : \'about\', name // route -eevec code-opt it ting // thio generateo a aeparate chunk (about .jö) for thio route // which tazy-toaded when the route i 4 viöited. component : webpackChunkName: \"about\" . / views/ about. vue\'), ](005_Navigating_Vue_Apps_with_Routing_008.png)

Taking a look at the syntax we are using for our /about routing... we are doing lazy loading

What it is saying is that when going to /about... make a separate bundle (or a chunk) for this entire route... lazy load it OR get that JS when the route is visited

Notice how we have a section of code that\'s commented out \'webpackChunkName\' this is important and needs to be present in order to use Lazy loading... this is how we are going to group the same file components in the same bundles... like:

![.1ting \> begin \> vue-heroes \> src name -r router.js \> ycomponent path: \' / heroes\' , : \'heroes\', // component: Heroeö, component : import(/\* webpackChunkName: \"heroezs \" path: \' / heroes/:id\' , \'hero-detail\', name : \*/ // component: HeroDetaiC, component : webpackChunkName: props: parseProps, \"b eroeo \" \' . / views/ heroes.vue\') \' . / views/ hero-detail.vue\'), ](005_Navigating_Vue_Apps_with_Routing_009.png)

We don't NEED to add this comment. If it\'s there, our bundle is going to use that name.... If not, it will make one for us.

**Routing through code**

There will be times where we want to route but also want to do something before hand... like saving.... In cases like these we want to route in code.... The way to do this is like:

![methods: { cancelHero() { thiö .\$router . name: \'heroes\' cnync oaveHero() { await dataService.updateHero(thO.hero); thi4.\$router . name: \'heroes\' } ) ; ](005_Navigating_Vue_Apps_with_Routing_010.png)

Simple.
