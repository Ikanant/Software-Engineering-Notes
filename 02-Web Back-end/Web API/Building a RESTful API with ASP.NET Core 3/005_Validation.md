Validation

Wednesday, April 29, 2020

7:09 PM

 

![](005_Validation_000.png){width="5.558333333333334in" height="2.6166666666666667in"}

 

When reporting back to the user the validation errors we encountered, I do not need to specify anything to the consumer to determine if he or the server made a mistake... that\'s what the STATUS CODE is used for

 

![](005_Validation_001.png){width="5.933333333333334in" height="1.7in"}

 

![](005_Validation_002.png){width="5.966666666666667in" height="1.8in"}

 

![](005_Validation_003.png){width="7.0in" height="2.091666666666667in"}

 

Let\'s assume I send in a post body with various properties as null... properties that are annotated as Required and have MaxLength... so we get back a 500 internal server error... (this error will only show up for the customer since we are running in developer mode... BUT, still... 500 server error shouldn\'t be the way we deal with these... after all, is the customer sending the bad data to the server...

 

.Net Core is awesome, so for me the only thing that I would have to do is make sure the DTO class I use to send the data to the API also has been annotated as my entity... when doing this, the error message sent back to the user will be more explicit... cool!

 

![](005_Validation_004.png){width="7.908333333333333in" height="2.475in"}

 

![](005_Validation_005.png){width="7.075in" height="3.175in"}

 

 

**Cross Property / Class Level Validation**

 

Often times my validation does not get covered by some of the possible data annotations that the component model offers me... let\'s say the firstName and the lastName of an entity can never be the same... how can I get this done? Custom rules... there is an interface we can implement called IValidatableObject.

 

![](005_Validation_006.png){width="4.2in" height="1.7666666666666666in"}

 

One thing to note is that in .Net Core, our custom validation will not get fired if one of the default validation annotated rules are invalid.

 

**Class Level Validation**

 

![](005_Validation_007.png){width="4.966666666666667in" height="2.816666666666667in"}

 

![](005_Validation_008.png){width="5.05in" height="2.341666666666667in"}

 

 

**Customizing Error Messages**

 

![](005_Validation_009.png){width="7.341666666666667in" height="2.6333333333333333in"}

 
