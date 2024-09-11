



| Version | Enhancements existing support (learner-service) | Comments | 
|  --- |  --- |  --- | 
| 3.3.0 | <ul><li>Refactoring keyspaces - separate for groups-service</li><li>Secondary indexing - prune or optimise</li><li>TG changes for request traceability</li><li>Unit test visibility in sonar</li><li>user id length or syntax standardisations</li></ul> | <ul><li>Focussed mainly on Cassandra optimisations and scale</li></ul> | 
| 3.2.0/5 | <ul><li>SVG support for eCreds </li><li>Migration of declarations from usr_external_identity to user_declarations</li><li>Migration of user_org to user_organisation</li><li>Introduction of persona in declarations and reporting</li><li>Self-service for migration of users (upon declaration validation)</li><li>Introduction of tenant/org preference APIs to support eCreds</li><li>user id is always English now</li></ul> | <ul><li>SVG support was developed and revoked later</li><li>self-service for migration of users was pulled out and likely will be part of 3.3</li></ul> | 
| 3.1.0 | <ul><li>Introduction of managed users and special auth scheme for MUA</li><li>Introduction of groups-service</li><li>Load testing cert/print-services</li><li>MDC context for play-seeder project - spike</li><li>Support for self-declarations and implementation route for migrating users</li></ul> | <ul><li>LIUA / LUA - Logged in user account - users with strong credentials (passwords)</li><li>MUA - Managed user account - users who don't have strong credentials</li></ul> | 
| 3.0.0 | <ul><li>Unified - single code base now - sunbird-lms-service </li><li>OTP issues resolved from field and put to rest</li></ul> | <ul><li>sunbird-lms-mw and sunbird-utils were absorbed</li><li>[SB-19484](https://project-sunbird.atlassian.net/browse/SB-19484) - OTP issues</li><li>2.10.0 and 3.0.0 were released together</li></ul> | 
| 2.10.0 | <ul><li>Support sigkill in cert-service, certificate-registry, notification-service</li><li>ecreds - html→pdf happens from print-service now (previously cert-service)</li><li>Review of password special characters and OTP related fixes </li><li>admin-user-reports - shadow db status changes</li><li>ability to migrate users based on shadow user</li></ul> | <ul><li>With print-service based PDF generation, regional language support got enabled.</li><li>It was believed print-service will help reduce the html→pdf conversion time, but didn't help.</li><li>email service actor Ask timeouts were fixed - 30s was wasted in wait during cert issuance.</li><li>Started getting scale hits</li></ul> | 

Discontinuing noting of registry changes; likely will not introduce anytime soon. An extended user profile is being imagined/discussed where registry could be used, but that's a long way off.



|  | Enhancements existing support (learner-service) | Registry integration efforts (user-service; suffixed '-prime')  | Comments | 
|  --- |  --- |  --- |  --- | 
| 2.8.0 | <ul><li>Upgrade KC s/w version to 6.0.1 - poc and trials start</li><li>eCreds for state level programs</li><li>Adding functional tests for most used and new APIs added since 2.6.0</li><li>On demand running of Quartz job</li><li>Load test for SSO</li></ul> | NONE | Percentage time spent on registry: legacy :: 100: 0 | 
| 2.7.0 | <ul><li>Testing cert-service</li><li>User login and signup testing</li><li>notification-service now async with Kafka</li><li>Enabling functional tests</li><li>Cert-service and Cert-registry generate, add functionality changes.</li><li>learner-service to use client secret to talk to KC</li></ul> | NONE | Percentage time spent on registry: legacy :: 100: 0 | 
| 2.6.0 | <ul><li>Admin manage users page - enhanced tables and introduced </li><li>Shadow DB - part 2 - Custodian org user migration based on external id and user feeds introduced</li><li>Org-level license attribute setting</li><li>Support attempts to upgrade KC</li></ul> | NONE | Percentage time spent on registry: legacy :: 100: 0 | 
| 2.5.0 | <ul><li>Admin manage users page - geo section and shadow db section introduced</li><li>Play framework upgraded to 2.7.2</li><li>Notification-service support for emails</li><li>Make all framework attributes optional</li><li>Support attempts to upgrade KC</li></ul> | NONE | Percentage time spent on registry: legacy :: 100: 0 | 
| 2.4.0 | <ul><li>Shadow DB based automated user migration</li><li>Users can add recovery details</li><li>Visible icons that users are state validated</li><li>New notification-service supporting targeted device to start with</li><li>KeyCloak upgrade steps identified</li></ul> | NONE | Percentage time spent on registry: legacy :: 100: 0 | 
| 2.3.0   | <ul><li>eCreds support</li><li>Forgot functionality moves to Portal from KeyCloak</li><li>Forgot password, merge account use-cases, including ability to free up identifiers</li></ul> | Org - Read and Search NONE | Percentage time spent on registry: legacy :: 90: 10 | 
| 2.2.0   | <ul><li>Client changes to ElasticSearch (transportClient to RestClient)</li><li>User external id column now in plain text (one time decryption job and API changes completed).</li><li>Notification-service design discussions</li></ul> | <ul><li>Deployment (dev) with Postgres store</li><li>Validation approach created </li><li>User - Create, Read, Search APIs implemented</li><li>Enc-service → Encryption service deployment enhancements</li><li>KeyCloak 3.2.4 → 6.0.1 upgrade attempted</li></ul> Offshoot → Akka-Play seeder project creation | <ul><li>Converting existing OS to jar took extra time (to lessen code changes) - Version clashes in logging, elastic search and extra spring-boot dependencies conflicting with Play.</li><li>Public utility (like KeyCloak, ProjectLogger) could be re-visited. Some, like ES-utils can be readily used.</li><li>User-service still doesn't use encryption</li><li>KeyCloak has not been updated ~2 years and our preferred version is no more available (DevOps uses a local copy and KeyCloak has made available only 4.8.3 onwards; last 4 major versions look to be supported).</li><li>Notification service is a new micro-service proposed to handle all user notifications.  With a Play seeder project, one can create an Akka-Play based service in minutes without worrying about the internal details.</li></ul>Percentage time spent on registry: legacy :: 50: 50 | 
| 2.1.0   | Automated SSO user migration One time migration external script (abandoned after build) | <ul><li>Team understanding development - internal and DevOps</li><li>Existing schema and its relevance/importance spelt out [here](https://drive.google.com/open?id=1Q7kdLNihihIpY0fRaLJy2s5_I-2IctldJBbvqesuknc).</li></ul> | The team is occupied with 2.0.0, load testing and telemetry changes for long, preventing understanding cum introspection of how to achieve this integration.Percentage time spent on registry: legacy :: 30: 70 | 





*****

[[category.storage-team]] 
[[category.confluence]] 
