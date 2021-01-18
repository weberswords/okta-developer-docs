The following code parses the Okta request body for the user name and email address, and stores the email address in the variable `patientName`.

```JavaScript
//Inline SAML Hook POST from Okta (endpoint: SAMLHook)

app.post("/SAMLHook", (request, response) => {
   
  console.log(" ");
  console.log("User email: " + request.body.data.context.user.profile["login"]);
  console.log("Name: " + request.body.data.context.user.profile["firstName"] + " " + request.body.data.context.user.profile["lastName"]);
 
  var patientName = request.body.data.context.user.profile["login"];
  ```
