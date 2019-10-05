## Strange Bug 

A strange bug that I came across today. 

I was working on a project that had an angular frontend. I was building an api
that had to do form validation.

I check if the request return a selection for a certian field. If the request 
did not have the field. It would post a message to the frontend that the required
field was missing. However, if it did have the field it would set the field
and the field value would be saved on the client. So I was sure to reset the 
string back to an empty string value, so if the user where to fill at that 
form again it would not use the last used value.

I added a line of code on the client side which set the value to an empty 
string after the request.

In the code I recompiled the styles, and pushed to our staging environment. 
Everythin worked for me locally.

### The Bug

After the deployment went through the staging environment. The javascript
had an error. It was giving me a 404 and an angular error that the module
could not be found. I was suprised and thought it was a compiliation error
recompiled the assets and redeployed. However the problem persists.

I was able to access the file on the server. So I was not sure why it couldn't 
be found when the code was being run. 

### The Solution

It turned out the cache buster hash code that generated on the file was
being blocked by the network because it to closely resembled a cross
site scripting attack.

This was caused by a plus sign inside the generated hash. I changed the algorithm
to replace any instances of plus signs or equal signs because thats what caused
the error.