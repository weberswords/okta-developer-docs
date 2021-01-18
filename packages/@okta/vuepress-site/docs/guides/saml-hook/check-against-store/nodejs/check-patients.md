```JavaScript
// Example Patients Data Store

const patients = [
  {
    username: 'michelle.test@example.com',
    ExternalServicePatientID: '1235',
  },
  {
    username: 'bob.uncle@example.com',
     ExternalServicePatientID: '6789',
  },
    {
    username: 'mark.christie@example.com',
     ExternalServicePatientID: '4235',
  },

  ]

//Inline SAML Hook POST from Okta (endpoint: SAMLHook)

app.post("/SAMLHook", (request, response) => {
   
  console.log(" ");
  console.log("User email: " + request.body.data.context.user.profile["login"]);
  console.log("Name: " + request.body.data.context.user.profile["firstName"] + " " + request.body.data.context.user.profile["lastName"]);
 
  var patientName = request.body.data.context.user.profile["login"];
  
  if (patients.some(user => user.username == patientName)){
    
    const arrayPosition = patients.findIndex(user => user.username == patientName);
    const patientID = patients[arrayPosition].ExternalServicePatientID;

    ...

  }
})
```
