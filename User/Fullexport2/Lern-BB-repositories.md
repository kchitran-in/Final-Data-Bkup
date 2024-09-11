
* 2 new repositories will be created - 


    1. [github.com/Sunbird-Lern/data-products](https://github.com/Sunbird-Lern/data-products/)


    1. [github.com/Sunbird-Lern/data-pipeline](https://github.com/Sunbird-Lern/data-pipeline)



    
* No devops repo in Lern, continue to use sunbird-devops and sunbird-devops-private (For API, Env and ES Mappings, Jenkins and Kubernetes scripts)


* for Cassandra migration, sunbird-utils will be moved to Lern 


* All the core microservices will be moved from  **project-sunbird**  and  **Sunbird-Ed**  to Lern 





|   | UserOrg Service | Batch Service | Notification Service | Groups Service | Discussion Forum | 
|  **Core Microservices**  | 
1. sunbird-lms-service


1. sunbird-auth


1. sunbird-apimanager-util



 | 
1. sunbird-course-service


1. sunbird-viewer-service


1. certificate-registry


1. cert-service



 | 
1. sunbird-notification-UI 


1. sunbird-notification-service



 | 
1. groups-service



 | 
1. discussions-UI 


1. discussions-middleware


1. nodebb-plugin-sunbird-api


1. nodebb-plugin-sunbird-oidc


1. nodebb-plugin-azure-storage


1. nodebb-plugin-sunbird-telemetry


1. sunbird-nodebb



 | 
|  **Data Products**   |  **data-products repository** /adhocscripts(scala/python/java) /jobs(reports/etl)
1. Geo report (stateadmingeoreport)


1. User-consent report( stateadminreport)


1. User declaration report


1. user details report


1. course status updater


1. collection reconcilation


1. coursebatch status updater


1. progressexhaustjob


1. responseexhaust


1. userinfoexhaust


1. course consumption


1. course enrolment


1. collectionsummaryjobv2



 | 
|  **Flink Jobs** -  |  **data-pipeline repository** 
1. Notification job


1. assessment aggregate updater


1. merge courses job


1. activity aggregate updater


1. certificate processor


1. collection-cert-pre-processor


1. collection-certificate-generator


1. relation cache updater


1. enrolment-reconciliation



 | 


## Jenkins Details
Jenkins jobs need to trigger for all LERN components.



|  **Service**  |  **Build**  |  **Artifact upload**  |  **Deploy**  | 
|  --- |  --- |  --- |  --- | 
| DiscussionsMW | [DMW-Build](http://10.20.0.5:8080/job/Build/job/Core/job/DiscussionsMiddleware/) | [DMW-Artifact](http://10.20.0.5:8080/job/ArtifactUpload/job/dev/job/Core/job/DiscussionsMW/) | [DMW-Deploy](http://10.20.0.5:8080/job/Deploy/job/dev/job/Kubernetes/job/DiscussionsMW/) | 
| Nodebb | [NBB-Build](http://10.20.0.5:8080/job/Build/job/Core/job/Nodebb/) | [NBB-Artifact](http://10.20.0.5:8080/job/ArtifactUpload/job/dev/job/Core/job/Nodebb/) | [NBB-Deploy](http://10.20.0.5:8080/job/Deploy/job/dev/job/Kubernetes/job/Nodebb/) | 
| DataProducts | [DP-Build](http://10.20.0.5:8080/job/Build/job/DataPipeline/job/EdDataProducts/) | [DP-Artifact](http://10.20.0.5:8080/job/ArtifactUpload/job/dev/job/DataPipeline/job/EdDataProducts/) | [DP-Deploy](http://10.20.0.5:8080/job/Deploy/job/dev/job/DataPipeline/job/EdDataProducts/) | 
| DataPipeline | [Pipeline-Build](http://10.20.0.5:8080/job/Build/job/KnowledgePlatform/job/FlinkJobs/) | [Pipeline-Artifact](http://10.20.0.5:8080/job/ArtifactUpload/job/dev/job/KnowledgePlatform/job/FlinkJobs/) | [Pipeline-Deploy](http://10.20.0.5:8080/job/Deploy/job/dev/job/KnowledgePlatform/job/FlinkJobs/) | 





*****

[[category.storage-team]] 
[[category.confluence]] 
