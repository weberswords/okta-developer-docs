```JavaScript
//Inline SAML Hook POST from Okta (endpoint: SAMLHook)

app.post("/SAMLHook", (request, response) => {
   
  console.log(" ");
  console.log("User email: " + request.body.data.context.user.profile["login"]);
  console.log("Name: " + request.body.data.context.user.profile["firstName"] + " " + request.body.data.context.user.profile["lastName"]);
 
  var patientName = request.body.data.context.user.profile["login"];
  
  if (patients.some(user => user.username == patientName)){
    
    const arrayPosition = patients.findIndex(user => user.username == patientName);
    const patientID = patients[arrayPosition].ExternalServicePatientID;
    
    var returnValue = { "commands":[
                          { "type":"com.okta.assertion.patch",
                            "value": [
                                {
                                  "op": "add",
                                  "path": "/claims/extPatientId",
                                  "value": {
                                      //"attributes": {
                                      //"NameFormat": "urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"    
                                      //  },
                                       "attributeValues":[
                                       {  
                                       //"attributes": {
                                       //  "xsi:type": "xs:integer"
                                       //},
                                        "value": patientID,
                                       }  
                                       ]  
                                  }
                                } 
                            ]
                          } 
                      ]
                    }
 
  console.log("Added patient ID claim to SAML assertion: " + returnValue.commands[0].value[0].value.attributeValues[0]["value"]);
  
  response.send(JSON.stringify(returnValue)); 
  }
  else {
    
  console.log("Not a patient. No change to SAML assertion.");  
  response.status(204).send();
  }
  
}
);
```