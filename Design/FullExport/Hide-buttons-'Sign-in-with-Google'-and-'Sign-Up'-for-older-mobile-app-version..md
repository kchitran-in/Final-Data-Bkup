 **Problem** Hide buttons 'Sign in with Google' and 'Sign Up' for older version mobile app on the login page.
## Solution 
This can be done by passing the query parameter with the login URL and displaying buttons only when the parameter has expected value. 
## Implementation


These buttons will be hidden on the page by default so that it won't be displayed in the older app version. The buttons will be only displayed when if it finds  **`version=1` ** in query params. We can read this query parameter value in keycloak login theme javascript file and show these buttons. 
```

```
 **Query parameter name: ** The proposed name for query parameter is  **version**  so that if needed in future we can increase the version value and perform the additional logic as well as we can maintain backward compatibility if needed.
```

```
 **_Note:_**  As of now there is no way available in keycloak to read custom query parameter in .ftl file. 
```

```
 **E.g login URL for will be.** [https://DOMAIN/auth/realms/sunbird/protocol/openid-connect/auth?redirect_uri=https://](https://staging.open-sunbird.org/auth/realms/sunbird/protocol/openid-connect/auth?redirect_uri=https://staging.open-sunbird.org/oauth2callback&response_type=code&scope=offline_access&client_id=android&)[DOMAIN](https://staging.open-sunbird.org/auth/realms/sunbird/protocol/openid-connect/auth?redirect_uri=https://staging.open-sunbird.org/oauth2callback&response_type=code&scope=offline_access&client_id=android&)[/oauth2callback&response_type=code&scope=offline_access&client_id=android&](https://staging.open-sunbird.org/auth/realms/sunbird/protocol/openid-connect/auth?redirect_uri=https://staging.open-sunbird.org/oauth2callback&response_type=code&scope=offline_access&client_id=android&) **version=1**  **Cons** 
* login URL change will be needed in the portal as well as in tenant pages. 



*****

[[category.storage-team]] 
[[category.confluence]] 
