06 - Docker Deep Dive - Working with Registries

Friday, April 29, 2016

11:44 AM

Course taught by: *Nigel Poulton*

**Creating a Public Repo on Docker Hub**

This is simple, the same way we pull images from the Docker Hub onto our machines, we will be able to create one ourselves. Right now I created under my account a public repo called hello world. As it stands, it is empty, right now we are just going to push the hello world Image we created in our previous module to see how it goes\...

**Using Our Public Repo on Docker Hub**

Let\'s start simple:

\- docker images

// Boom, that\'s it, we see our docker hub image.

[Notice:]

Before we do this, this is something about Docker that can be non-intuitive at first---\> In order to push an image to my Ikanant/helloworld repo that we created we first need to TAG our image like:

docker tag

ex:

\- docker tag ikanant/helloworld:1.0

Now if we look for images again:

\- docker images

// We see the new Image tagged. *[We can\'t tag images at build time.]*

\- docker push ikanant/helloworld:1.0

*[Remember to LOGIN:]*

\- docker login

Docker hub will skip certain layers because they might already exist on docker hub. (This actually didn\'t happen to me). Only new layers get pushed.

*[JUMP TO OUR CentOS:]*

To clean things out a little bit we will delete all the images we got going on right now. We check with:

\- docker images

In order to delete images we need to delete any containers that are linked to them.

\- docker ps -a

//Show all containers

\- docker rm ...

// Good bye to those containers

\- docker mi ...

// This will delete ALL of the layers in each image.

Now we don\'t have any images or containers\...

\- docker pull ikanant/helloworld:1.0

// This pulled our repo out of docker hub

Note: We can\'t delete an online repo from the terminal, for that we need to go to the browser interface.

**Building a Private Registry**

Note: We can have multiple Repos inside a registry.

The lesson is on a Debian based system running Docker

*[I did not write notes on this because this is changing and we don\'t really need to get too deep into it. It pretty much means that instead go pushing our code to the docker hub public registry, we can have our own personal one. It\'s not complicated.]*

![](005_06_-_Docker_Deep_Dive_-_Working_with_Registries_000.png)
