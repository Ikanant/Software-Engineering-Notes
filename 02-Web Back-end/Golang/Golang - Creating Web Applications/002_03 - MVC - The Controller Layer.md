03 - MVC - The Controller Layer

Friday, April 29, 2016

11:20 AM

 

The controller layer will allow us to receive the user\'s requests and route it through the application eventually feeding data into the application being bound by the templates and later on returning the full functional web page.

Normally the controller layer is made of 2 basic components:

1.  Router (Front controller)

    -   Receive the request from the browser and determine which sub controller (back controller) will handle the request

2.  Back controller

Right now, we will relieve our main function of all the responsibilities we have given it.

 

![](002_03_-_MVC_-_The_Controller_Layer_000.png){width="5.0in" height="3.1666666666666665in"}

 

Controller main tasts:

1.  Receive the request from the client and coordinate how the application handles the request

2.  Inform the model of the request so that it can apply whatever business logic or data access might be required

3.  It may get a response from the Model of the action

4.  Forwarding the results from the Model and to the View layer

```{=html}
<!-- -->
```
5.  **Middleware**

    -   **Many applications require additional support services that are not directly inline with the core applications purpuse such as:**

        1.  User authentication

        2.  Session management

        3.  Compressing the response streams

    -   **These tasks are often not the responsibility of any layer, but the controller is the one that is MOST aware of the fact that it is operating in the context of a web application**

    -   **Summary: Sessions of code that are called before or after the controller handles the request itself**

 

**[Parameterized Routes]{.underline}**

![](002_03_-_MVC_-_The_Controller_Layer_001.png){width="5.0in" height="2.6166666666666667in"}

 

Gorilla Mux Code added

This toolkit consist of a collection of packages that are intended to augment the out of the box experience that GO provides. This is an HTTP server that extents the basic capabilities that come with the default server in many ways. Specifically we are interested in its option to provide parameterized routing.

**[DATA Compression]{.underline}**

When generating a Page in our system, we are currently creating such page and sending it fully to our client. In many circumstances this can be a problem because pages can be large and occupy a big space. One tool we can use is to compress such file to make things more efficient

![](002_03_-_MVC_-_The_Controller_Layer_002.png){width="5.0in" height="2.591666666666667in"}

**[Unit Testing]{.underline}**

Go test should be really easy. We can just head to the src folder of our application and type:

\> go test ./\...

This tells GO to start in the current folder, and head down the whole applications folder structure for any go testing files

In order to write a test file for GO, we just need to create a Go file like the following:

packagewhatever

import (

"testing\"

)

func Test_myFunctionThatStartsWithTEST(t \*testing.T) {

     i := 1

     if(i!=1){

          t.Log("Detail about error")

          t.Fail()

     }

}

AND BOOM GOES THE DYNAMITE

![](002_03_-_MVC_-_The_Controller_Layer_003.png){width="5.0in" height="2.65in"}
