 **Overview: ** Currently, Deskstop App has a logging system that stores the log in the file system. These logs have the type of log, error message, time-stamp. We can debug the errors locally by accessing the log files. 

 **Problem  statement: ** As part of the error log sync to the server, the system should not have the repetitive/duplicate logs, and it should have the required data to make debugging easier. So we should have listed down some possible errors along with there unique CODE and Identifier

 **Solution: ** We will list all the possible scenarios where fatal errors might come. Code is a Unique key for error where ID is a combination of the CODE and ID, where ID is an individual attribute for the error such as do_id, batchId. For better implementation, we can encode ID with base64 Encoding.

The following are some Generic errors which may occur during the App lifecycle:



|  |  **CODE**  |  **ID**  | 
| 1 | ecar_filename | 
| 2 | low_disk_space | 
| 3 | ecar_already_added | 
| 4 | content_do_id | 
| 5 | content_do_id | 
| 6 | content_do_id | 
| 7 | content_do_id | 
| 8 | content_do_id | 
| 9 | batchId | 
| 10 | file_path | 
| 11 | batch_ID | 
| 12 | help_desk_down | 
| 13 | type_subtype_action | 
| 14 | channel_id | 
| 15 | language_code | 
| 16 | tenant_id | 
| 17 | do_id | 
| 18 | do_id | 
| 19 | device_profile_id | 
| 20 | status (online/offline) | 
| 21 | search_keyword | 
| 22 | app_update | 
| 23 | system_info | 
| 24 | change_content_location | 
| 25 | user_create | 
| 26 | user_id | 
| 27 | user_id | 
| 28 | location_keyword | 
| 29 | location_keyword | 
| 30 | app_start | 
| 31 | app_crash | 
| 32 | req_id   (e.g. '/dialog/content/export') | 
| 33 | crash_reporter | 
| 34 | unknown | 
|  --- |  --- |  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
| 1 | ecar_filename | 
| 2 | low_disk_space | 
| 3 | ecar_already_added | 
| 4 | content_do_id | 
| 5 | content_do_id | 
| 6 | content_do_id | 
| 7 | content_do_id | 
| 8 | content_do_id | 
| 9 | batchId | 
| 10 | file_path | 
| 11 | batch_ID | 
| 12 | help_desk_down | 
| 13 | type_subtype_action | 
| 14 | channel_id | 
| 15 | language_code | 
| 16 | tenant_id | 
| 17 | do_id | 
| 18 | do_id | 
| 19 | device_profile_id | 
| 20 | status (online/offline) | 
| 21 | search_keyword | 
| 22 | app_update | 
| 23 | system_info | 
| 24 | change_content_location | 
| 25 | user_create | 
| 26 | user_id | 
| 27 | user_id | 
| 28 | location_keyword | 
| 29 | location_keyword | 
| 30 | app_start | 
| 31 | app_crash | 
| 32 | req_id   (e.g. '/dialog/content/export') | 
| 33 | crash_reporter | 
| 34 | unknown | 





*****

[[category.storage-team]] 
[[category.confluence]] 
