
##  Objective
LERN Dataproducts is collection of scripts which will be used to generate reports for LERN related data creation and consumption.

Current data products are using some of the data locations from other building blocks.

From this migration, other building block data dependencies will be decoupled.


##  Building block dependencies and approaches


|  **Job Name**  |  **Dependency**  |  **Approach**  | 
|  --- |  --- |  --- | 
|  **Exhaust Jobs** <ul><li>Progress Exhaust

</li><li>Response Exhaust

</li><li>Userinfo Exhaust

</li></ul> |  **_Lern BB_** <ul><li>user_enrolments 

</li><li>assessment_aggregator

</li><li>user_activity_agg

</li></ul> **_Obsrv BB_** <ul><li>User Redis

</li><li>Postgres Job_request table

</li></ul> **_User ORG_** <ul><li>user_consent

</li><li>system_settings

</li></ul> **_Public API_** <ul><li>Content Search API

</li></ul> | <ul><li>Move exhaust APIs to Lern

</li><li>Deploy Usercache redis in Lern

</li><li>Move job_request table under LERN environment

</li><li>Add custodian org details in job config or fetch using system settings API

</li></ul>Need discussion for user_consent table -  | 
|  **Course Consumption**  |  **_Lern BB_** <ul><li>Course_batch cassandra table 

</li></ul> **_User ORG_** <ul><li>Organization table from sunbird keyspace

</li></ul> **_Obsrv BB_** <ul><li>Summary-events druid datasource

</li></ul> **_Public API_** <ul><li>Content search API

</li></ul> | <ul><li>Use public API for getting ORG details

</li><li>Disable these jobs via config - cronjob configuration

</li><li>Instead of accessing tables directly use apis - scaling issues will come

</li><li>internal api calls to druid or public api with token authentication

<ul><li>OPA layer implementation for authentication and code changes for the API key credentials in Druid API call.

</li></ul></li></ul> | 
|  **Course Enrollment**  |  **_Lern BB_** <ul><li>Course_batch cassandra table

</li><li>Course batch elasticsearch index

</li></ul> **_User ORG_** <ul><li>Organization table from sunbird keyspace

</li></ul> **_Public API_** <ul><li>Content search API

</li></ul> | <ul><li>Use org search API ( **Public API** ) for getting organization details

</li></ul> | 
|  **State Admin Report**  |  **_User ORG BB_** <ul><li> **cassandra table** 

<ul><li>User

</li><li>User_declaration

</li><li>User_consent

</li><li>Location

</li></ul></li></ul> | <ul><li>Use Location search API instead of cassandra table - scaling issue

</li><li>Add User_declaration, User_consent to Usercache and use it as single data point for user related reports. - multiple entries are there for declaration and consent respective to course and orgs.

<ul><li>During update or revoke of consent, cache should be in sync.

</li></ul></li></ul>Need discussion for user related tables | 
|  **State Admin Geo Report**  |  **_User ORG BB_** <ul><li> **cassandra table** 

<ul><li>Organisation 

</li><li>Location

</li></ul></li></ul> |  | 
|  **Collection Summary Job V2**  |  **_Lern BB_** <ul><li>user_enrolments 

</li><li>course_batch

</li></ul> **_Obsrv BB_** <ul><li>User Redis

</li><li>Druid API to trigger ingestion task for  **collection-summary-snapshot** 

</li></ul> **_Public API_** <ul><li>Content Search API

</li></ul> | <ul><li>internal api calls to druid or public api with token authentication

<ul><li>OPA layer implementation for authentication and code changes for the API key credentials in Druid API call.

</li></ul></li></ul> | 
|  **Exhaust API**  | Postgres table for job_request | <ul><li>Moving Exhaust API service to LERN

</li><li>Move job_request table under LERN environment

</li></ul> | 





*****

[[category.storage-team]] 
[[category.confluence]] 
