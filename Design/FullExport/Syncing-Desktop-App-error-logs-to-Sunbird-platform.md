
##  **Overview** : 
Currently, Deskstop App has a logging system that stores the log in the file system. We can debug the errors locally by accessing the log files. 

 **Problem  statement: ** Remote analysis of the error logs is not possible with the current setup. It is not possible to always debug locally. So we need to sync the error logs to the Sunbird platform from where the logs can be debugged remotely.

 **Solution 1: Storing logs in DB and then syncing** 
1. Error logs will be read from the error log folder in the file system.
1. The error logs will be stored in the DB with some dynamic values of the application and device.


1. Whenever the internet is available, we will read the logs from DB whose ' **createdOn'**  is less than 2 months and then will create the request body for the sync API.
1. Call the API with endpoint '/data/v1/client/logs'. On the successful response of the API, the log will be deleted from the DB. 
1. Will run a delete job every 7 days which will delete the logs which are older than 2 months.

Database Model: 


```js
{
  "id": ""
  "appVersion": "", // String - mandatory
  "createdOn": 1560786734444,
  "updatedOn": 1560786734444,
  "deviceSpec": {
    "totalMemory": 8589934592,
    "availableMemory": 6182776832,
    "totalHarddisk": 250685575168,
    "availableHarddisk": 113083383808,
    "cpuSpeed": "2.30",
    "cpuLoad": 45.18,
    "systemTime": 1571985802602,
    "servicePack": "Service Pack 1"
  },
  "errorTrace": {
    "id": "", // Log id that can co-relate to the corresponding telemetry error event
    "ts": 1560786734444, // Epoch timestamp - non zero - mandatory
    "stackTrace": "", // String - stack Trace log - mandatory            
    "pageid": "" // page id - optional
  }
}
```
Pros: 
1. Error logs can be kept in DB as long as data is not synced to the server.
1. Easy to fetch data and keep track of which all logs are synced.

Cons: 
1. The error will be kept in both DB and file system in log folders.
1. Need to maintain this DB



![](images/storage/error_logging_with_DB.png)



 **Solution 2: Reading logs from the file system and syncing** 
1. Error logs will be read from the error log folder in the file system whenever the internet is available.
1. The error logs will be enhanced with some dynamic values of the application and device to create the request body for the sync API.
1. Call the API with endpoint '/data/v1/client/logs'.

Pros:
1. No duplication - Error logs will only be kept in the file system.

Cons:
1. Logs will only be available for the configured time.
1. Hard to keep track of which all data is synced.![](images/storage/error_logging_without_DB.png)





 **Telemetry Events** 
1. LOG event for error syncing API.
1. ERROR event for error syncing API.









*****

[[category.storage-team]] 
[[category.confluence]] 
