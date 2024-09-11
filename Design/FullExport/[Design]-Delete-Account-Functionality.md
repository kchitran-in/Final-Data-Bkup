
## Introduction
This wiki explains the design for delete user account feature. As of now there is no hard delete of user profile flow available in Sunbird. At present, we have functionality to BLOCK/UNBLOCK users.


## Background & Problem Statement
Sunbird supports the mobile app for Android and iOS. As per the latest policy update of the Apple App Store and Google Play Store, mandates the user deletion from the app, if the app is having the signup from app. The specific policy mandates can be found using the following links:


* Apple App Store Policy - [https://developer.apple.com/app-store/review/guidelines/#data-collection-and-storage](https://developer.apple.com/app-store/review/guidelines/#data-collection-and-storage)


* Apple App Store Policy - [https://developer.apple.com/support/offering-account-deletion-in-your-app](https://developer.apple.com/support/offering-account-deletion-in-your-app)


* Google Play Store Policy - [https://support.google.com/googleplay/android-developer/answer/13327111?hl=en](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en)



Registered users must have access to a "Delete Account" option on both the app and the portal. This option will allow them to initiate the account deletion process themselves.


### Key Design Problems
User should not able to do the following things after successful deletion of account:


* User should not be able to login by using the existing login credentials post account deletion.


* Any of the Personally Identifiable Information (PII) of the user, such as name, email, and phone number should not be available in any DB in any format (even encrypted format). 


* Other than PII data should not be deleted. User transactional data and user created contents ( _usage,_  _rating etc_ ) are to be retained.


* Certificates issued to the deleted users should not be accessible, but should be verifiable. (Storing only the name of the user in Sunbird RC to display in certificate).


* External id of the SSO user should be removed.


* List the deleted user list to admin dashboard.


* Deleted user’s asset should be transferred to the other user after successful deletion.




## Design

### Delete User
![](images/storage/delete-user-api-flow.png)


* Send the OTP to the user’s email/phone to validate the user. (OTP templates for user account deletion verification)



Sync


* Delete login credentials and sessions from Keycloak. 


* Update the sunbird.user table. Set the following fields as empty: (redis data for the following fields will become empty for that user) 


    * firstName


    * lastName


    * email


    * dob


    * phone


    * maskedEmail


    * maskedPhone


    * prevUsedEmail


    * prevUsedPhone


    * recoveryEmail


    * recoveryPhone



    
* Update the status from  **ACTIVE** to **DELETED** . 


* Remove the user entry from sunbird.user_lookup table. 


* Remove the SSO user entry from sunbird.user_external_identity .


* Send the AUDIT telemetry event after successful/failure update/deletion of the above tables.


* Trigger the delete user kafka event {{env_name}}.delete.user



User Deletion Flink Job
* Verify the sync steps is successfully completed else perform the pending actions.


* Update the user entry in sunbird.user_organisation (async) - May not be required.


    *  isdeleted - True


    * orgleftdate - system date



    
* Update the user’s name in nodeBB as  **Deleted User**  to display in discussion forum.


* Group - TBD


* Send the AUDIT telemetry event after successful/failure update/deletion of the above tables.





User delete API:DELETE '{{host}}/api/user/v1/delete/{{userId}}'
```
curl --location --request DELETE '{{host}}/api/user/v1/delete/{{userId}}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{api_key}}' \
--header 'x-authenticated-user-token: {{user_token}}'
```
Response
```
{
    "id": "api.user.delete",
    "ver": "1.0",
    "ts": "2023-08-28T13:54:45Z+05:30",
    "params": {
        "resmsgid": "a638c46e-63a5-47de-bf00-029cbe435e5e",
        "msgid": null,
        "err": null,
        "status": "successful",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "response": "SUCCESS",
        "userId": "{{userId}}"
    }
}
```
Delete User Kafka Event

|  **Property**  |  **Description**  | 
|  --- |  --- | 
| organisationId | It helps to identify user belongs to which organisation | 
| userId | Deleted user id | 
| suggested_user | If user have role other than PUBLIC, than suggested user list can be send in the event for each role user is having. | 

Sample event
```
{
  "eid": "BE_JOB_REQUEST",
  "ets": 1619527882745,
  "mid": "LP.1619527882745.32dc378a-430f-49f6-83b5-bd73b767ad36",
  "actor": {
    "id": "delete-user",
    "type": "System"
  },
  "context": {
    "pdata": {
      "id": "org.sunbird.platform",
      "ver": "1.0"
    }
  },
  "object": {
    "id": "<deleted-userId>",
    "type": "User"
  },
  "edata": {
    "organisationId": "<organisationId>"
    "userId": "<deleted-userId>",
    "suggested_users": [
    	{
    		"role": "ORG_ADMIN",
    		"users": ["<orgAdminUserId>"]
    	},
    	{
    		"role": "CONTENT_CREATOR",
    		"users": ["<contentCreatorUserId>"]
    	},
    	{
    		"role": "COURSE_MENTOR",
    		"users": ["<courseMentorUserId>"]
    	}
    ],
    "action": "delete-user",
    "iteration": 1
  }
}
```

### Deleted Users search curl
User search API can be used to get the more detail about user. e.g. name.  

Curlcurl --location '{{host}}/api/user/v3/search' \

--header 'Authorization: {{kong_api_key}}' \

--header 'X-Authenticated-User-token: {{keycloak_access_token}}' \

--header 'Content-Type: application/json' \

--data '{

    "request": {

        "filters": {

           "status": 2,
          "updatedDate": {">=": "2023-05-10 08:41:50:752+0000"}     

        }

    }

}'



 **OTP Template** Email Template<html><head><meta name="viewport" content="width=device-width"><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title></title><style>@media only screen and (max-width:620px){table\[class=body] h1{font-size:28px!important;margin-bottom:10px!important}table\[class=body] a,table\[class=body] ol,table\[class=body] p,table\[class=body] span,table\[class=body] td,table\[class=body] ul{font-size:16px!important}table\[class=body] .article,table\[class=body] .wrapper{padding:10px!important}table\[class=body] .content{padding:0!important}table\[class=body] .container{padding:0!important;width:100%!important}table\[class=body] .main{border-left-width:0!important;border-radius:0!important;border-right-width:0!important}table\[class=body] .btn table{width:100%!important}table\[class=body] .btn a{width:100%!important}table\[class=body] .img-responsive{height:auto!important;max-width:100%!important;width:auto!important}}@media all{.ExternalClass{width:100%}.ExternalClass,.ExternalClass div,.ExternalClass font,.ExternalClass p,.ExternalClass span,.ExternalClass td{line-height:100%}.apple-link a{color:inherit!important;font-family:inherit!important;font-size:inherit!important;font-weight:inherit!important;line-height:inherit!important;text-decoration:none!important}}</style></head><body class="" style="color:#000!important;background-color:#f6f6f6;font-family:sans-serif;-webkit-font-smoothing:antialiased;font-size:14px;line-height:1.4;margin:0;padding:0;-ms-text-size-adjust:100%;-webkit-text-size-adjust:100%"><table border="0" cellpadding="0" cellspacing="0" class="body" style="border-collapse:separate;mso-table-lspace:0;mso-table-rspace:0;width:100%;background-color:#f6f6f6"><tbody><tr><td style="font-family:sans-serif;font-size:14px;vertical-align:top"> </td><td class="container" style="font-family:sans-serif;font-size:14px;vertical-align:top;display:block;Margin:0 auto;max-width:580px;padding:10px;width:580px"><div class="content" style="box-sizing:border-box;display:block;Margin:0 auto;max-width:580px;padding:10px"><span class="preheader" style="color:transparent;display:none;height:0;max-height:0;max-width:0;opacity:0;overflow:hidden;mso-hide:all;visibility:hidden;width:0"></span><table class="main" style="border-collapse:separate;mso-table-lspace:0;mso-table-rspace:0;width:100%;background:#fff;border-radius:3px"><tbody><tr><td class="wrapper" style="font-family:sans-serif;font-size:14px;vertical-align:top;box-sizing:border-box;padding:20px"><table border="0" cellpadding="0" cellspacing="0" style="border-collapse:separate;mso-table-lspace:0;mso-table-rspace:0;width:100%"><tbody><tr><td style="font-family:sans-serif;font-size:14px;vertical-align:top"><table border="0" cellpadding="0" cellspacing="0" class="btn btn-primary" style="border-collapse:separate;mso-table-lspace:0;mso-table-rspace:0;width:100%;box-sizing:border-box"><tbody><tr><td align="left" style="font-family:sans-serif;font-size:14px;vertical-align:top;font-family:sans-serif;font-size:14px;font-weight:400;margin:0;Margin-bottom:15px">Hello User,<br><p>To confirm the deletion of your $installationName account, please enter the following OTP: $otp.</p><p>This OTP is valid for the next $otpExpiryInMinutes.</p><p>If you did not request this account deletion, please ignore this message or contact our support team immediately at $supportEmail.</p><p>Thank you for using $installationName.</p>Best regards,<br>The $installationName Team</td></tr></tbody></table></td></tr></tbody></table></td></tr></tbody></table></div></td><td style="font-family:sans-serif;font-size:14px;vertical-align:top"> </td></tr></tbody></table></body></html>


```
Hello User,

To confirm the deletion of your Sunbird Ed account, please enter the following OTP: [OTP Code].

This OTP is valid for the next [Time Limit, e.g., 5 minutes]. 

If you did not request this account deletion, please ignore this message or contact our support team immediately at [Support Email].

Thank you for using Sunbird Ed.

Best regards,
The Sunbird Ed Team
```

* SMS




```
Dear User, to confirm the deletion of your Sunbird Ed account, please enter the following OTP: [OTP Code].This OTP is valid for the next [Time Limit, e.g., 5 minutes]. If you did not request this account deletion, please ignore this message or contact our support team immediately.
```


 **Backward compatibility Approach:** 

As part of backward compatibility, ‘User Deletion Flink Job’ mentioned above can be deployed; ‘delete-user’ kafka topic can be created and events to the kafka topic can be inserted via scripts by passing users' information as part of the topic for completing user deletion activity.




### Manage Learn - 
As part of the Manage Learn use case, the user’s PII data is captured and/or used in the below-mentioned workflows - 


1. A complete snapshot of a user’s profile which includes  **name (first and last name) as well as masked email and phone**  is captured under various collections in  **MongoDB (observations, projects, survey, and programUsers)** at the start of any transaction i.e. the moment a user starts working on a [survey](https://ed.sunbird.org/learn/functional-capabilities/manage-learn/what-is-observation), or [project](https://ed.sunbird.org/learn/functional-capabilities/manage-learn/what-is-a-project) or decides to join a [program](https://ed.sunbird.org/learn/functional-capabilities/manage-learn/what-is-a-program). This is done to give the Program manager the details of the user as it was when he/she started working on the resource and is not affected by his/her profile change later. This means a user’s name, location, role, and sub roles which is later used for certificate generation using Sunbird RC is the same when he/she started the resource.


1. When the Program Manager requests reports via the Program Dashboard about the details of each and every user who has worked on a resource or has joined the program, the user’s email and phone along with the name is provided via a CSV using the [Lern Data Product](https://lern.sunbird.org/learn/product-and-developer-guide/data-products/program-exhaust). These details are fetched in real-time at the moment of generating the on-demand report from the common and shared Redis and Cassandra storage.  **_No change is required here since the expectation is user’s name, email phone will be deleted from the common storage and replaced with the “Deleted User” string, We will just need to test this once to confirm the entry from the reports is not removed but just the PII data is removed._** 



Note - No other place in Logs, Druid, ES or Neo4j does Manage Learn workflow write to

As part of the user delete flow we plan to implement the following changes in the Mangage Learn side:-


* Build a Kafka consumer in each micro-service (Survey, Projects, and ML Core) to listen to Kafka events on topic -  **TBD Point 4** which will do the following thing.


    * Check if any transactions are recorded for this user and if yes, remove all user name, email, and phone entries based on the userId from all collections i.e. projects, surveySubmissions, observations, observationSubmissions, and programUsers of MongoDB.


    * Update the status via API in sunbird.user_deletion_status table.  **Refer - TBD Point 2** 



    
* Build a Kafka consumer in each micro-service (Survey, Projects, and ML Core) to listen to Kafka events on topic -  **{{envName}}.tranfer.ownership.job.request** which will do the following thing.


    * Check if any assets are owned by the deleted user and that the new owner has required platform roles (i.e. Program Manager or Program Designer), if yes update the owner/author in the collections i.e. programs, solutions of MongoDB.


    * Update the status via API in sunbird.user_ownership_transfer table.  **Refer - TBD Point 3** 



    



 **NOTE: None of the services should log the user PII data.** 




## References

* [[\[PRD] Delete Account functionality|[PRD]-Delete-Account-functionality]]


* [https://docs.google.com/presentation/d/1EoRJD8KWd0002hHtxc4PWwAVB0FQr_Z5l4PUOsvxpdQ/edit?pli=1#slide=id.p](https://docs.google.com/presentation/d/1EoRJD8KWd0002hHtxc4PWwAVB0FQr_Z5l4PUOsvxpdQ/edit?pli=1#slide=id.p)


* Apple App Store - [https://developer.apple.com/support/offering-account-deletion-in-your-app](https://developer.apple.com/support/offering-account-deletion-in-your-app)


* Google Play Store - [https://support.google.com/googleplay/android-developer/answer/13327111?hl=en](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en)





*****

[[category.storage-team]] 
[[category.confluence]] 
