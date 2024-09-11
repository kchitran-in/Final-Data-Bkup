


## Data Model:


|  | Dimension in Druid | Field in Telemetry | Description | Data Type | 
|  --- |  --- |  --- |  --- |  --- | 
| 1 | ets | ets | Event timestamp | Long | 
| 2 | eid | eid | Event Id | String | 
| 3 | syncts | syncts | Sync Timestamp | Long | 
| 4 | @timstamp | @timstamp | Sync Timestamp in String | String | 
| 5 | actor_id | actor.id | Actor Id of the event | String | 
| 6 | actor_type | actor.type | Type of the actor | String | 
| 7 | context_channel | context.channel | Channel Id | String | 
| 8 | context_pdata_id | context.pdata.id | Producer Id | String | 
| 9 | context_pdata_pid | context.pdata.pid | Producer Process Id | String | 
| 10 | context_pdata_ver | context.pdata.ver | Producer version number | String | 
| 11 | context_env | context.env | Context Environment | String | 
| 12 | context_sid | context.sid | Session Id | String | 
| 13 | context_did | context.did | Device Id | String | 
| 14 | context_cdata_type | context.cdata.type | Correlation Data Type | Array\[String] | 
| 15 | context_cdata_id | context.cdata.id | Correlation Data Id | Array\[String] | 
| 16 | context_rollup_l1 | context.rollup.l1 | Context level 1 rollup | String | 
| 17 | context_rollup_l2 | context.rollup.l2 | Context level 2 rollup | String | 
| 18 | context_rollup_l3 | context.rollup.l3 | Context level 3 rollup | String | 
| 19 | context_rollup_l4 | context.rollup.l4 | Context level 4 rollup | String | 
| 20 | object_id | object.id | Content Id | String | 
| 21 | object_type | object.type | Content Type | String | 
| 22 | object_version | object.ver | Content Version | String | 
| 23 | object_rollup_l1 | object.rollup.l1 | Content level 1 rollup | String | 
| 24 | object_rollup_l2 | object.rollup.l2 | Content level 2 rollup | String | 
| 25 | object_rollup_l3 | object.rollup.l3 | Content level 3 rollup | String | 
| 26 | object_rollup_l4 | object.rollup.l4 | Content level 4 rollup | String | 
| 27 | tags | tags | Tags | Array\[String] | 
| 28 | edata_type | edata.type | Event type | String | 
| 29 | edata_subtype | edata.subtype | Event subtype | String | 
| 30 | edata_mode | edata.mode | START event Mode of start | String | 
| 31 | edata_pageid | edata.pageid | Unique pageid | String | 
| 32 | edata_uri | edata.uri | IMPRESSION event Relative URI of the content | String | 
| 33 | edata_id | edata.id | Event data Id | String | 
| 34 | edata_duration | edata.duration | Duration of the event | Double | 
| 35 | edata_index | edata.index | ASSESS event Index of the question within a content | Integer | 
| 36 | edata_pass | edata.pass | ASSESS event Field to identify pass or fail for assessments | String | 
| 37 | edata_score | edata.score | ASSESS event Assessment score | Double | 
| 38 | edata_resvalues | edata.resvalues | ASSESS event Assessment results | Array\[Object] | 
| 39 | edata_item_id | edata.item.id | ASSESS event Assessment item id | String | 
| 40 | edata_item_title | edata.item.title | ASSESS event Assessment item title | String | 
| 41 | edata_item_maxscore | edata.item.maxscore | ASSESS event Assessment item max score | Double | 
| 42 | edata_target_id | edata.target.id | ASSESS event Assessment item target id | String | 
| 43 | edata_target_type | edata.target.type | ASSESS event Assessment item target type | String | 
| 44 | edata_rating | edata.rating | FEEDBACK event Ratings | Integer | 
| 45 | edata_comments | edata.comments | FEEDBACK event Comments | String | 
| 46 | edata_dir | edata.dir | SHARE event direction | String | 
| 47 | edata_items_id | edata.items.id | SHARE event shared item ids | Array\[String] | 
| 48 | edata_items_type | edata.items.type | SHARE item types | Array\[String] | 
| 49 | edata_items_origin_id | edata.items.origin.id | SHARE event source id | Array\[String] | 
| 50 | edata_items_origin_type | edata.items.origin.type | SHARE event source type | Array\[String] | 
| 51 | edata_items_to_id | edata.items.to.id | SHARE event destination id | Array\[String] | 
| 52 | edata_items_to_type | edata.items.to.type | SHARE event destination type | Array\[String] | 
| 53 | edata_plugin_id | edata.plugin.id | INTERACT event plugin id on which the interaction has happened  | String | 
| 54 | edata_plugin_ver | edata.plugin.ver | INTERACT  event plugin version | String | 
| 55 | edata_plugin_category | edata.plugin.category | INTERACT  event plugin category | String | 
| 56 | edata_props | edata.props | AUDIT event updated properties | Array\[String] | 
| 57 | edata_state | edata.state | AUDIT event current state | String | 
| 58 | edata_prevstate | edata.prevstate | AUDIT event previous state | String | 
| 59 | edata_size | edata.size | SEARCH event result size | Integer | 
| 60 | edata_filters_dialcodes | edata.filters.dialcodes | SEARCH event List of dialcodes | Array\[String] | 
| 61 | edata_topn_identifier | edata.topn.identifier | SEARCH event topn results | Array\[String] | 
| 62 | edata_visits_objid | edata.visits.objid | IMPRESSION event unique id for object visited | Array\[String] | 
| 63 | edata_visits_objtype | edata.visits.objtype | IMPRESSION event type of object visited | Array\[String] | 
| 64 | edata_visits_objver | edata.visits.objver | IMPRESSION event version of object visited | Array\[String] | 
| 65 | edata_visits_index | edata.visits.index | IMPRESSION event index of object within list | Array\[Integer] | 
| 66 | device_loc_state | devicedata.state | State location information for the device | String | 
| 67 | device_loc_state_code | devicedata.statecode | State ISO code information for the device | String | 
| 68 | device_loc_iso_state_code | devicedata.iso3166statecode | State ISO-3166 code information for the device | String | 
| 69 | device_loc_city | devicedata.city | City location information for the device | String | 
| 70 | device_loc_country_code | devicedata.countrycode | Country ISO code information for the device | String | 
| 71 | device_loc_country | devicedata.country | Country location information for the device | String | 
| 72 | device_loc_state_custom_code | devicedata.statecustomcode | State custom code information for the device | String | 
| 73 | device_loc_state_custom_name | devicedata.statecustomname | State custom name information for the device | String | 
| 74 | device_loc_district | devicedata.districtcustom | District custom information for the device | String | 
| 75 | user_declared_state | devicedata.userdeclared.state | State declared by the user | String | 
| 76 | user_declared_district | devicedata.userdeclared.district | District declared by the user | String | 
| 77 | device_os | devicedata.devicespec.os | Device OS name | String | 
| 78 | device_make | devicedata.devicespec.make | Device make and model | String | 
| 79 | device_id | devicedata.devicespec.id | Physical device id if available from OS | String | 
| 80 | device_mem | devicedata.devicespec.mem | Total memory in mb | Integer | 
| 81 | device_idisk | devicedata.devicespec.idisk | Total interanl disk | Integer | 
| 82 | device_edisk | devicedata.devicespec.edisk | Total external disk | Integer | 
| 83 | device_scrn | devicedata.devicespec.scrn | Screen size in inches | Integer | 
| 84 | device_camera | devicedata.devicespec.camera | Primary & secondary camera spec | String | 
| 85 | device_cpu | devicedata.devicespec.cpu | Processor name | String | 
| 86 | device_sims | devicedata.devicespec.sims | Number of sim cards | Integer | 
| 87 | device_uaspec_agent | devicedata.uaspec.agent | User agent of the browser | String | 
| 88 | device_uaspec_ver | devicedata.uaspec.ver | User agent version of the browser | String | 
| 89 | device_uaspec_system | devicedata.uaspec.system | User agent system identification of the browser | String | 
| 90 | device_uaspec_platform | devicedata.uaspec.platform | User agent client platform of the browser | String | 
| 91 | device_uaspec_raw | devicedata.uaspec.raw | Raw user agent of the browser | String | 
| 92 | device_first_access | devicedata.firstaccess | First access of the device | Long (Epoch) | 
| 93 | content_name | contentdata.name | Name of the content | String | 
| 94 | content_object_type | contentdata.objecttype | Type of the content | String | 
| 95 | content_type | contentdata.contenttype | Type of the resource | String | 
| 96 | content_media_type | contentdata.mediatype | Type of the media of the resource | String | 
| 97 | content_language | contentdata.language | List of languages in the content | Array\[String] | 
| 98 | content_medium | contentdata.medium | Language medium of the board | Array\[String] | 
| 99 | content_gradelevel | contentdata.gradelevel | List of grade levels in the content | Array\[String] | 
| 100 | content_subjects | contentdata.subject | List of subjects in the content | Array\[String] | 
| 101 | content_mimetype | contentdata.mimetype | Mimetype of the resource in the content | String | 
| 102 | content_created_by | contentdata.createdby | Content created by | String | 
| 103 | content_created_for | contentdata.createdfor | List of orgs for whom the content is created | Array\[String] | 
| 104 | content_framework | contentdata.framework |  | String | 
| 105 | content_board | contentdata.board | Board of affiliation | String | 
| 106 | content_status | contentdata.status | Status of the content - Draft, Published etc. | String | 
| 107 | content_version | contentdata.pkgversion | Version of the content | Double | 
| 108 | content_last_submitted_on | contentdata.lastsubmittedon | Last submitted date of the content | Long (Epoch) | 
| 109 | content_last_published_on | contentdata.lastpublishedon | Last published date of the content | Long (Epoch) | 
| 110 | content_last_updated_on | contentdata.lastupdatedon | Last updated date of the content | Long (Epoch) | 
| 111 | user_grade_list | userdata.gradelist | List of grades taught | Array\[String] | 
| 112 | user_language_list | userdata.languagelist | List of languages known | Array\[String] | 
| 113 | user_subject_list | userdata.subjectlist | List of subjects taught | Array\[String] | 
| 114 | user_type | userdata.type | Type of user | String | 
| 115 | user_loc_state | userdata.state | State info of the user | String | 
| 116 | user_loc_district | userdata.district | District info of the user | String | 
| 117 | user_loc_block | userdata.block | Block info of the user | String | 
| 118 | user_roles | userdata.roles | List of user roles | Array\[String] | 
| 119 | user_signin_type | userdata.usersignintype | User sign-in type info | String | 
| 120 | user_login_type | userdata.userlogintype | User login type info | String | 
| 121 | dialcode_channel | dialcodedata.channel | Channel for which dialcode is generated | String | 
| 122 | dialcode_batchcode | dialcodedata.batchcode | Batch for which dialcode belongs to | String | 
| 123 | dialcode_publisher | dialcodedata.publisher | Publisher of the dialcode | String | 
| 124 | dialcode_generated_on | dialcodedata.generatedon | Dialcode generated on | Long (Epoch) | 
| 125 | dialcode_published_on | dialcodedata.publishedon | Dialcode published on | Long (Epoch) | 
| 126 | dialcode_status | dialcodedata.status | Status of the dialcode | String | 
| 127 | dialcode_object_type | dialcodedata.objecttype | Object type - DialCode as a value | String | 
| 128 | collection_name | collectiondata.name | Name of the collection (Denormalised for  **object.rollup.l1**  field) | String | 
| 129 | collection_object_type | collectiondata.objecttype | Type of the collection | String | 
| 130 | collection_type | collectiondata.contenttype | Type of the resource | String | 
| 131 | collection_media_type | collectiondata.mediatype | Type of the media of resource | String | 
| 132 | collection_language | collectiondata.language | List of languages in the collection | Array\[String] | 
| 133 | collection_medium | collectiondata.medium | Language medium of the board | Array\[String] | 
| 134 | collection_gradelevel | collectiondata.gradelevel | List of grade levels in the collection | Array\[String] | 
| 135 | collection_subjects | collectiondata.subjects | List of subjects in the collection | Array\[String] | 
| 136 | collection_mimetype | collectiondata.mimetype | Mimetype of the resource in the collection | String | 
| 137 | collection_created_by | collectiondata.createdby | Resourse created By | String | 
| 138 | collection_created_for | collectiondata.createdfor | List of orgs for whom the resource is created | Array\[String] | 
| 139 | collection_framework | collectiondata.framework |  | String | 
| 140 | collection_board | collectiondata.board | Board of affiliation | String | 
| 141 | collection_status | collectiondata.status | Status of the collection - Draft, Published etc. | String | 
| 142 | collection_version | collectiondata.pkgversion | Version of the collection | Double | 
| 143 | collection_last_published_on | collectiondata.lastpublishedon | Last published date of the collection | Long(Epoch) | 
| 144 | collection_last_updated_on | collectiondata.lastupdatedon | Last updated date of the collection | Long(Epoch) | 
| 145 | collection_last_submitted_on | collectiondata.lastsubmittedon | Last submitted date of the collection | Long(Epoch) | 
| 146 | derived_loc_state | derivedlocationdata.state | Derived location state of the user | String | 
| 147 | derived_loc_district | derivedlocationdata.district | Derived location district of the user | String | 
| 148 | derived_loc_from | derivedlocationdata.from | Derived location  | String | 
| 149 | user_declared_state | userdeclared.state | User Declared State | String | 
| 150 | user_declared_district | userdeclared.district | User Declared District | String | 





*****

[[category.storage-team]] 
[[category.confluence]] 
