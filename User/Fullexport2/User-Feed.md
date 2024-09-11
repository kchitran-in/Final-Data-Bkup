* [Problem statement ](#problem-statement )
* [Solution:](#solution:)
  * [APIs details:](#apis-details:)
  * [Workflow from Consumption:](#workflow-from-consumption:)
    * [Case 1: State user logs in](#case-1:-state-user-logs-in)
    * [Case 2: Custodian user logs in](#case-2:-custodian-user-logs-in)
  * [Deleting of user feed:](#deleting-of-user-feed:)
* [Storing User message](#storing-user-message)
  * [Approach:](#approach:)



# Problem statement 
 User needs to validate his/her external id, to migrate from custodian org to non-Custodian org. This migration process required a sequence of the popups (Ref: [SC-1243](https://project-sunbird.atlassian.net/browse/SC-1243)). 

  Example: 

   1: "Are you a {{matched tenant object}} teacher"

   2: "Please enter your {{teacher id}}"


# Solution:
  The system will introduce the following APIs:


1. GET /user/v1/feed/{userId} :  ThisAPI will provide a list of user feeds.
1. POST /user/v1/migrate : This API will be used when the user will click on reject or accept.


## APIs details:



```java
URL: {BaseUrl}/api/user/v1/feed/{userId}
Method: GET

Response: 
      {
    "id": "api.user.feed",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": null,
        "status": "success",
        "errmsg": null
    },
    "responseCode": "OK",
    "response": {
        "userFeed": [
             {
                "id": "feed unique id",
                "userId": "",
                "category": "OrgMigrationAction", 
                "priority": 1,
                "createdBy" : "userId or system",
                "createdOn" : "created time stamp",
                "channel": "user channel value",  
                "status": "unread",
                "expireOn": "time stamp",
                "data": {
                        "prospectChannels": ["TN"]
                }
            }
        ]
    }
}

URL : {BaseUrl}/api/user/v1/migrate
Method : POST
 Request: 
    {
    "params": {},
    "request": {
        "userId": "userid",
        "externalId": "user external id",
        "channel" : "channel value for which u are trying to verify"
        "action": "accept" or "reject",
        "feedId":""   
      // in case of reject only userId and action required.
      // in case of accept , all three mandatory.
    }
 }

Response: 200 (Migrated successfully)
  {
    "id": "api.user.migrate",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": null,
        "status": "success",
        "errmsg": null
    },
    "responseCode": "OK",
    "response": { 
          "message": "success"
       }
    }

Response: 400 (Data error, some problem with request data)
  {
    "id": "api.user.migrate",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": "Code of error",
        "status": "CLIENT-ERROR",
        "errmsg": "Error message"
    },
    "responseCode": "CLIENT-ERROR",
    "response": { 
         
       }
    }

Response: 401 (Unauthorize user, means either x-authenticated-user-token value is incorrect or user id found from header and in request does not match)
  {
    "id": "api.user.migrate",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": "Code of error",
        "status": "CLIENT-ERROR",
        "errmsg": "Error message"
    },
    "responseCode": "CLIENT-ERROR",
    "response": { 
         
       }
    }

Response: 404 (User try to validate it , but provided details not matched in DB)
  {
    "id": "api.user.migrate",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": "Code of error",
        "status": "CLIENT-ERROR",
        "errmsg": "Error message"
    },
    "responseCode": "CLIENT-ERROR",
    "response": { 
         
       }
    }


Response: 429 (if user try "N" number of incorrect attempt)
  {
    "id": "api.user.migrate",
    "ver": "v2",
    "ts": "2019-11-08 07:50:16:122+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": "Code of error",
        "status": "CLIENT-ERROR",
        "errmsg": "Error message"
    },
    "responseCode": "TOO_MANY_REQUESTS",
    "response": { 
         
       }
    }
```



## Workflow from Consumption:

### Case 1: State user logs in
           No workflow change required.


### Case 2: Custodian user logs in
Invoke GET /feed API → check response 200 and it has category value as " **OrgMigrationAction** " then read  **data**  → inside data you will find " **prospectChannels** " key with value as channel list.

           ** case a** :  if response is 200 and userFeed is empty -> then NO need to show popup

            **case b:  ** if response is 200 and userFeed has some data but category value is not " **OrgMigrationAction** " then no need to show popup.

           ** case c**  : if response is 200 and userFeed has data and category is " **OrgMigrationAction** " then read  **data**  and extract  **prospectChannels**  key value.



Example :

              1. User match with only one channel/state

                ...  "data": { "prospectChannels": \["AP"]}  ...

             2. User match with multiple channel/state

               ...  "data": { "prospectChannels": \["AP","TN"]}




## Deleting of user feed:
 User feed will be deleted in following scenarios:

          **case a:** If user reject migration , then we will delete user feed from cassandra and ES both , so that user won't get migration feed again

         **case b:** If user try to do migrate and he exceed with max attempt count then we need to delete feed from cassandra and ES both

         **case c: **  After successfull user migration , feed data need to be deleted from cassandra and ES both 


# Storing User message

## Approach:
Message can be stored in a separate table as user_feed. This table can be used for another notification purpose as well.

Schema design to store notification data: 
```sql
Table name : user_feed
 id (pk) - text auto generated
 userId - text identity of user
 category - text (enum of category value) // this will define message type
 priority - int  // importance of this message (1- urgent , 0 - no priority)
 status - text (read/unread/bookmark)
 expireOn - timestamp
 data  - text // property bag. Fill any - feedData can differ based on category. only mandatory value is list of Object
 updatedOn - timestamp
 updatedBy - text //userId
 createdBy - text // "userId or system"
 createdOn -  timestamp //"time stamp when this message was created"
      
```
All attributes will not be used as of now.

Same data will be stored inside ElasticSearch as well. Feed read will happen from ElasticSearch.







*****

[[category.storage-team]] 
[[category.confluence]] 
