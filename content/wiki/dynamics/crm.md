---
title: "Microsoft Dynamics 365 CRM"
description: "Developing for and integrating with Microsoft Dynamics 365 CRM"
toc: true
menu:
    wiki:
        parent: "dynamics"
        weight: 30
---

# CRM Web API

* The Web API is the preferred API for CRM 2016 and upwards.
* OData 4.0 RESTful web service
* Not to be confused with the deprecated OData Endpoint (2011)
* Maximum records returned is 5000 before pagination kicks in
* Uses Open ID Connect / OAuth for authentication. Can use ADAL library for this in .NET
* Your application needs to be registered in Active Directory to be able to make requests
* The Web API URL is found in  Settings > Customizations > Developer Resources

## Registering your application for Dynamics 365

https://stackoverflow.com/questions/37215742/401-unauthorized-authentication-using-rest-api-dynamics-crm-with-azure-ad/48554845#48554845

App registration

* Log into portal.azure.com using your Office 365 administrator user of your Dynamics CRM subscription.
* Go to Azure Active Director\App registrations and add New application registrations
* Enter "Name" and "Sign-on URL", the URL could be anything (https://localhost for example)
* Select the registered app you just created, go to Settings\Keys
* Enter a key description, click Save and copy the Value (and keep it since you will need it later). Also copy the Application ID of the registered app.
* Go to "Required Permissions", click Add, select "Dynamics CRM Online" then tick "Access CRM Online as organisation users".

These steps enable a client application to access Dynamics CRM by using the Application ID and the client secret you created in step 5. Your client application is now able to be authenticated against Azure AD with permission to access CRM Online. However, CRM Online does not know about this "client application" or "user". CRM API will response a 401 if you try to access it.
Add CRM application user

To let CRM know about the "client application" or "user", you'll need to add an application user.

* Go to CRM\Security Roles, create a new Security Role or just copy the "System Administrator" Role
* Go to CRM\Settings\Security\Users, create a new User, change the form to "Application User"
* Enter the required fields with the Application ID that you have in previous step. Once saved, CRM will auto populate the Azure AD Object ID and the URI.
* Add the user to the Security Role created from previous step.

Now you should be able to access CRM API using HttpClient and ADAL using the sample code below:

```csharp
var ap = await AuthenticationParameters.CreateFromResourceUrlAsync(
                new Uri("https://*****.api.crm6.dynamics.com/api/data/v9.0/"));

String authorityUrl = ap.Authority;
String resourceUrl = ap.Resource;

var authContext = new AuthenticationContext(authorityUrl);
var clientCred = new ClientCredential("Application ID", "Client Secret");
var test = await authContext.AcquireTokenAsync(resourceUrl, clientCred);

Console.WriteLine(test.AccessToken);

using (var client = new HttpClient())
{
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", test.AccessToken);

    var response = await client.GetAsync("https://*****.api.crm6.dynamics.com/api/data/v9.0/contacts");
    var contacts = await response.Content.ReadAsStringAsync();

    Console.WriteLine(contacts);
}
```

# JavaScript

The JavaScript code below uses XMLHttpRequest to retrieve account records where the state = "WA", the customer type is "Customer", the record is active and the modified date is on or before 12/31/2014.

```javascript
var req = new XMLHttpRequest();
req.open("GET", Xrm.Page.context.getClientUrl() + "/api/data/v8.1/accounts?$select=name,_primarycontactid_value,telephone1&$filter=address1_stateorprovince eq 'WA' and  customertypecode eq 3 and  statecode eq 0 and  modifiedon le 2014-12-31T08:00:00.000Z&$orderby=name asc&$count=true", true);
req.setRequestHeader("OData-MaxVersion", "4.0");
req.setRequestHeader("OData-Version", "4.0");
req.setRequestHeader("Accept", "application/json");
req.setRequestHeader("Content-Type", "application/json; charset=utf-8");
req.setRequestHeader("Prefer", "odata.include-annotations=\"OData.Community.Display.V1.FormattedValue\"");
req.setRequestHeader("Prefer", "odata.maxpagesize=50");
req.onreadystatechange = function () {
    if (this.readyState === 4) {
        req.onreadystatechange = null;
        if (this.status === 200) {
            var results = JSON.parse(this.response);
            var recordCount = results["@odata.count"];
            for (var i = 0; i < results.value.length; i++) {
                 var name = results.value[i]["name"];
                 var _primarycontactid_value = results.value[i]["_primarycontactid_value"];
                 var _primarycontactid_value_formatted = results.value[i]["_primarycontactid_value@OData.Community.Display.V1.FormattedValue"];
                 var telephone1 = results.value[i]["telephone1"];
            }
        }
        else {
            alert(this.statusText);
```

# Resources

# References

* https://mscrmrocks.wikispaces.com/CRM+Web+API