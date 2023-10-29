Reactive Config via Key/Value Store

Sunday, March 22, 2020

5:00 PM

Consul deals with its key value pairs like a TREE. At the base there is only one part of one tree, but as it grows upwards it goes around in many different directions.

 

It all starts at the root of our tree. The way to determine we are there is by looking at the url and seeing we are at the /kv/ url...

On the ui we can add a key by tapping the CREATE button...

 

We can either create a FOLDER or a VALUE

When creating a folder simply add a / at the end of the key name and the value box will disappear

 

![Explosion of Services Customers Portal ailuun Order Inventory Stripe Loggly ](002_Reactive_Config_via_Key-Value_Store_000.png)

 

 

So we could add a prod/ folder followed by an swa folder and then we start to create our tree structure. There is no right/wrong way to accomplish this and we have the freedom to adhere to the rules as we go.

 

**Getting data out**

Getting information in it\'s simple as explained above... but how do we resolve to get the info out? We can always use the UI like above, or we can also just use the API

 

curl <http://localhost:8500/v1/kv/?recurse'&'pretty>

 

The main thing to note out of the JSON that we get back from this curl command is that the values of our keys are not readable by human eyes. These are base64 encoded.

 

**Side note:** We can also submit values to the api as follows:

Curl -X PUT -d \'true\' <http://localhost:8500/v1/kv/prod/swa/variable_three>

**Or delete:**

Curl -X DELETE <http://localhost:8500/v1/kv/prod/swa/variable_three>

 

 
