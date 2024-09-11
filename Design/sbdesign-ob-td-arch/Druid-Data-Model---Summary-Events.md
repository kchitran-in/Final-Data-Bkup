


## Data Model:




|  | Dimension in Druid | Field in Summary event | Description | Data Type | 
|  --- |  --- |  --- |  --- |  --- | 
| 1 | ets | ets | Event timestamp | Long | 
| 2 | eid | eid | Event Id | String | 
| 3 | ver | ver | Version | String | 
| 4 | syncts | syncts | Sync timestamp | Long | 
| 5 | uid | uid | User Id | String | 
| 6 | context_date_range_from | context.date_range.from | Start Date for the summary | Long (Epoch) | 
| 7 | context_date_range_to | context.date_range.to | End Date for the summary | Long (Epoch) | 
| 8 | context_rollup_l1 | context.rollup.l1 | Context level1 rollup | String | 
| 9 | context_rollup_l2 | context.rollup.l2 | Context level2 rollup | String | 
| 10 | context_rollup_l3 | context.rollup.l3 | Context level3 rollup | String | 
| 11 | context_rollup_l4 | context.rollup.l4 | Context level4 rollup | String | 
| 12 | dimension_channel | dimensions.channel | Channel Id as dimension from raw telemetry | String | 
| 13 | dimensions_did | dimensions.did | Device Id as dimension from raw telemetry | String | 
| 14 | dimensions_pdata_id | dimensions.pdata.id | Producer Id as dimension from raw telemetry | String | 
| 15 | dimensions_pdata_pid | dimensions.pdata.pid | Producer Process Id as dimension from raw telemetry | String | 
| 16 | dimensions_pdata_ver | dimensions.pdata.ver | Producer Process Ver as dimension from raw telemetry | String | 
| 17 | dimensions_sid | dimensions.sid | Session Id as dimension | String | 
| 18 | dimensions_type | dimensions.type | Type of summary | String | 
| 19 | dimensions_mode | dimensions.mode | Mode of action in the session | String | 
| 20 | object_id | object.id | Content Id | String | 
| 21 | object_type | object.type | Content Type | String | 
| 22 | object_version | object.ver | Content version | String | 
| 23 | object_rollup_l1 | object.rollup.l1 | Object level1 rollup | String | 
| 24 | object_rollup_l2 | object.rollup.l2 | Object level2 rollup | String | 
| 25 | object_rollup_l3 | object.rollup.l3 | Object level3 rollup | String | 
| 26 | object_rollup_l4 | object.rollup.l4 | Object level4 rollup | String | 
| 27 | tags | tags | Tags attached to a summary event | Array\[[[String|String]]] | 
| 28 | edata_time_spent | edata.eks.time_spent | Time spent in the session excluding idle time | Double | 
| 29 | edata_time_difference | edata.eks.time_diff | Total time in a session including idle time | Double | 
| 30 | edata_interaction_count | edata.eks.interact_events_count | Total count of interact events in a session | Long | 
| 31 | edata_env_summary_env | edata.eks.env_summary.env | High level env within the app(content, domain, resources, community) | Array\[String] | 
| 32 | edata_env_summary_count | edata.eks.env_summary.count | Count of times the environment has been visited | Array\[Integer] | 
| 33 | edata_env_summary_time_spent | edata.eks.env_summary.time_spent | Time spent per env | Array\[Double] | 
| 34 | edata_page_summary_id | edata.eks.page_summary.id | Page id | Array\[String] | 
| 35 | edata_page_summary_type | edata.eks.page_summary.type | Type of page e.g. view/edit | Array\[String] | 
| 36 | edata_page_summary_env | edata.eks.page_summary.env | Env of page | Array\[String] | 
| 37 | edata_page_summary_visit_count | edata.eks.page_summary.visit_count | Number of times each page was visited | Array\[Integer] | 
| 38 | edata_page_summary_time_spent | edata.eks.page_summary.time_spent | Time taken per page | Array\[Double] | 
| 39 | edata_item_responses_item_id | edata.eks.item_responses.itemId | Question Id passed in the ASSESS event | Array\[String] | 
| 40 | edata_item_responses_time_spent | edata.eks.item_responses.timeSpent | Time spent in seconds from ASSESS event | Array\[Double] | 
| 41 | edata_item_responses_pass | edata.eks.item_responses.pass | Pass response for a question from ASSESS event | Array\[String] | 
| 42 | edata_item_responses_score | edata.eks.item_responses.score | Score from ASSESS event | Array\[[[Integer|Integer]]] | 
| 43 | edata_item_responses_max_score | edata.eks.item_responses.maxScore | Max Score from ASSESS event | Array\[[[Integer|Integer]]] | 
| 44 | edata_item_responses_timestamp | edata.eks.item_responses.time_stamp | Timestamp for each response from ASSESS event | Array\[Long (Epoch)] | 
| 45 | device_loc_state | devicedata.state | State location information for the device | String | 
| 46 | device_loc_state_code | devicedata.statecode | State ISO code information for the device | String | 
| 47 | device_loc_iso_state_code | devicedata.iso3166statecode | State ISO-3166 code information for the device | String | 
| 48 | device_loc_city | devicedata.city | City location information for the device | String | 
| 49 | device_loc_country_code | devicedata.countrycode | Country ISO code information for the device | String | 
| 50 | device_loc_country | devicedata.country | Country location information for the device | String | 
| 51 | device_loc_state_custom_code | devicedata.statecustomcode | State custom code information for the device | String | 
| 52 | device_loc_state_custom_name | devicedata.statecustomname | State custom name information for the device | String | 
| 53 | device_loc_district | devicedata.districtcustom | District custom information for the device | String | 
| 54 | device_os | devicedata.devicespec.os | Device OS name | String | 
| 55 | device_make | devicedata.devicespec.make | Device make and model | String | 
| 56 | device_id | devicedata.devicespec.id | Physical device id if available from OS | String | 
| 57 | device_mem | devicedata.devicespec.mem | Total memory in mb | Integer | 
| 58 | device_idisk | devicedata.devicespec.idisk | Total interanl disk | Integer | 
| 59 | device_edisk | devicedata.devicespec.edisk | Total external disk | Integer | 
| 60 | device_scrn | devicedata.devicespec.scrn | Screen size in inches | Integer | 
| 61 | device_camera | devicedata.devicespec.camera | Primary & secondary camera spec | String | 
| 62 | device_cpu | devicedata.devicespec.cpu | Processor name | String | 
| 63 | device_sims | devicedata.devicespec.sims | Number of sim cards | Integer | 
| 64 | device_uaspec_agent | devicedata.uaspec.agent | User agent of the browser | String | 
| 65 | device_uaspec_ver | devicedata.uaspec.ver | User agent version of the browser | String | 
| 66 | device_uaspec_system | devicedata.uaspec.system | User agent system identification of the browser | String | 
| 67 | device_uaspec_platform | devicedata.uaspec.platform | User agent client platform of the browser | String | 
| 68 | device_uaspec_raw | devicedata.uaspec.raw | Raw user agent of the browser | String | 
| 69 | device_first_access | devicedata.firstaccess | First access of the device | Long (Epoch) | 
| 70 | content_name | contentdata.name | Name of the content | String | 
| 71 | content_object_type | contentdata.objecttype | Type of the content | String | 
| 72 | content_type | contentdata.contenttype | Type of the resource | String | 
| 73 | content_media_type | contentdata.mediatype | Type of the media of the resource | String | 
| 74 | content_language | contentdata.language | List of languages in the content | Array\[String] | 
| 75 | content_medium | contentdata.medium | Language medium of the board | Array\[String] | 
| 76 | content_gradelevel | contentdata.gradelevel | List of grade levels in the content | Array\[String] | 
| 77 | content_subjects | contentdata.subject | List of subjects in the content | Array\[String] | 
| 78 | content_mimetype | contentdata.mimetype | Mimetype of the resource in the content | String | 
| 79 | content_created_by | contentdata.createdby | Content created by | String | 
| 80 | content_created_for | contentdata.createdfor | List of orgs for whom the content is created | Array\[String] | 
| 81 | content_framework | contentdata.framework |  | String | 
| 82 | content_board | contentdata.board | Board of affiliation | String | 
| 83 | content_status | contentdata.status | Status of the content - Draft, Published etc. | String | 
| 84 | content_version | contentdata.pkgversion | Version of the content | Double | 
| 85 | content_last_submitted_on | contentdata.lastsubmittedon | Last submitted date of the content | Long (Epoch) | 
| 86 | content_last_published_on | contentdata.lastpublishedon | Last submitted date of the content | Long (Epoch) | 
| 87 | content_last_updated_on | contentdata.lastupdatedon | Last updated date of the content | Long (Epoch) | 
| 88 | user_grade_list | userdata.gradelist | List of grades taught | Array\[String] | 
| 89 | user_language_list | userdata.languagelist | List of languages known | Array\[String] | 
| 90 | user_subject_list | userdata.subjectlist | List of subjects taught | Array\[String] | 
| 91 | user_type | userdata.type | Type of user | String | 
| 92 | user_loc_state | userdata.state | State info of the user | String | 
| 93 | user_loc_district | userdata.district | District info of the user | String | 
| 94 | user_loc_block | userdata.block | Block info of the user | String | 
| 95 | user_roles | userdata.roles | List of user roles | Array\[String] | 
| 96 | user_signin_type | userdata.usersignintype | User sign-in type info | String | 
| 97 | user_login_type | userdata.userlogintype | User login type info | String | 
| 98 | collection_name | collectiondata.name | Name of the collection (Denormalised for  **object.rollup.l1**  field) | String | 
| 99 | collection_object_type | collectiondata.objecttype | Type of the collection | String | 
| 100 | collection_type | collectiondata.contenttype | Type of the resource | String | 
| 101 | collection_media_type | collectiondata.mediatype | Type of the media of resource | String | 
| 102 | collection_language | collectiondata.language | List of languages in the collection | Array\[String] | 
| 103 | collection_medium | collectiondata.medium | Language medium of the board | Array\[String] | 
| 104 | collection_gradelevel | collectiondata.gradelevel | List of grade levels in the collection | Array\[String] | 
| 105 | collection_subjects | collectiondata.subjects | List of subjects in the collection | Array\[String] | 
| 106 | collection_mimetype | collectiondata.mimetype | Mimetype of the resource in the collection | String | 
| 107 | collection_created_by | collectiondata.createdby | Resourse created By | String | 
| 108 | collection_created_for | collectiondata.createdfor | List of orgs for whom the resource is created | Array\[String] | 
| 109 | collection_framework | collectiondata.framework |  | String | 
| 110 | collection_board | collectiondata.board | Board of affiliation | String | 
| 111 | collection_status | collectiondata.status | Status of the collection - Draft, Published etc. | String | 
| 112 | collection_version | collectiondata.pkgversion | Version of the collection | Double | 
| 113 | collection_last_published_on | collectiondata.lastpublishedon | Last published date of the collection | Long(Epoch) | 
| 114 | collection_last_updated_on | collectiondata.lastupdatedon | Last updated date of the collection | Long(Epoch) | 
| 115 | collection_last_submitted_on | collectiondata.lastsubmittedon | Last submitted date of the collection | Long(Epoch) | 

      



*****

[[category.storage-team]] 
[[category.confluence]] 
