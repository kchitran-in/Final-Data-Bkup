
# Process General Details




|  **Infrastructure monitoring process**  | 
| This document details out the standard operating processes for NOC team in the below mentioned areas while monitoring/managing DIKSHA production environment.
1. Service down
1. 5xx errors 
1. 4xx errors 
1. Telemetry Pipeline errors 
1. Publish Pipeline errors 
1. Daily Backups 
1. Monthly Restorations
1. Other critical services 

 | 
|  --- | 
|  --- | 
|  **Infrastructure monitoring process**  | 
| This document details out the standard operating processes for NOC team in the below mentioned areas while monitoring/managing DIKSHA production environment.
1. Service down
1. 5xx errors 
1. 4xx errors 
1. Telemetry Pipeline errors 
1. Publish Pipeline errors 
1. Daily Backups 
1. Monthly Restorations
1. Other critical services 

 | 




# 1. Service Down


| Area of Coverage | Which Alert to be Monitored | Course of Action | 
|  --- |  --- |  --- | 
| Service uptime   Following are monitored <ul><li>VM</li><li>Docker nodes</li><li>DBs</li><li>Managed service</li></ul> All the resources should be covered from the environment | Service downWe will receive an email alert or slack notification on this, this error will also start showing the 5xx errors from this service(s)Alerts are configured using prometheus or monet when the service is down and they will attempt to restart them if they are down. Docker swarm master will maintain the configured number of nodes for each service, On VMs monet will try restarting it twice before it gives up.  | If the auto restart has happened and the services are back to normal, then send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) If the service is either restarting continuously or unable to start, get access to the server\*\*, then debug\* and see if this can be resolved, if yes then the service is up. Do send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) If service is still down then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner  and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops log | 

\*Do refer to Cook Book / Jira / SOP document on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 2. 5xx Errors


| Area of Coverage | How is it Monitored | Course of Action | 
|  --- |  --- |  --- | 
| Service degradation  All services which are running in the application, right from APIs, DBs, etc.. Reference [link here](https://diksha.gov.in/grafana/d/-2-h4TZZk/noc-dashboard?orgId=1&from=now-30m&to=now&fullscreen&panelId=12) | We receive alerts from monitoring about any 5xx errors > 0.1% This can be observed by watching the grafana nginx dashboard  | Identify which service is giving us the 5xx error. Get the server access\*\* and debug\*to find the root cause to resolve the issue, if the issue is resolved, do send an email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops logs | 

\*you can start from Grafana to identify the API / Service giving 5xx error, check Kibana and logs server to find the details of the error and refer to CookBook / Jira / SOP documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 3. 4xx Errors


| Area of Coverage | How is it Monitored  | Course of Action | 
|  --- |  --- |  --- | 
| Client side errors All services which are running in the application, right from APIs, DBs, etc.. Reference [link here](https://diksha.gov.in/grafana/d/-2-h4TZZk/noc-dashboard?orgId=1&from=now-30m&to=now&fullscreen&panelId=11)  | We receive alerts from monitoring about any 4xx errors > 1% This can be observed by watching the grafana nginx dashboard  | Identify which service is giving us the 4xx error. Get the server access\*\* and debug\*to find the root cause to resolve the issue, if the issue is resolved, do send an email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1 for 499*** error** and **S2 for any other 4xx error**  and assign to DIKSHA Infra Owner  and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops log | 

\*you can start from Grafana to identify the API / Service giving 4xx error, check Kibana and logs server to find the details of the error and refer to CookBook / Jira / SOP documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 

\*\*\* 499 error refer to client closing browser before the response is sent, this generally refers to early signs of service degradation. Other 4xx errors are to be investigated for the purpose of identifying the  source of client side error patterns 


# 4. Telemetry Pipeline


| Area of Coverage | How is it Monitored | Course of Action | 
|  --- |  --- |  --- | 
| Telemetry pipeline \* this has direct impact to reportsDashboard [link here](https://diksha.gov.in/grafana/d/Mvh2VoWWk/ep-pipeline-metrics?orgId=1)Lag monitoring [link here](https://docs.google.com/spreadsheets/d/1hKUGiMXjilNUv7Btpnv0e1gzRTYID7eLTZKB0Wcv8tY/edit?ts=5d089b08#gid=1473572078) | Samza jobs status Redis cache server Lag monitoring between each topic in pipeline <ul><li>Samza jobs and Redis cache servers have alerts configured, you would receive monitoring alerts if the service is down</li><li>Lag monitoring has to be done via the grafana dashboard and  manually (if dashboards are not in sync or in questions)</li></ul> | Identify which service is giving us the error. Get the server access\*\* and debug\* to find the root cause to resolve the issue, if the issue is resolved, do send an email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner  and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops logs | 

\*you can start from Gra

fana to identify the API / Service giving errors, check Kibana and logs server to find the details of the error and refer to CookBook / Jira / SOP  documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 5. Publish Pipeline


| Area of Coverage | How is it Monitored | Course of Action | 
|  --- |  --- |  --- | 
|  Publish pipeline \* this has direct impact to content creation in the applicationDashboard [link here](https://docs.google.com/spreadsheets/d/1XDq7Q9kTriOnoHzEr3JWDcj0fBDodl1AcpK_qD7WEcQ/edit#gid=0) | Samza jobs status Redis cache server #Lag monitoring between each topic in pipeline <ul><li>Samza jobs and Redis cache servers have alerts configured, you would receive monitoring alerts if the service is down</li><li>Grafana dashboards is enabled for publish pipeline metrics</li><li>#Lag monitoring is not yet enabled </li></ul> | Identify which service is giving us the error. Get the server access\*\* and debug\*to find the root cause to resolve the issue, if the issue is resolved, do send an email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner  and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops logs | 

\*you can start from Grafana to identify the API / Service giving errors, check Kibana and logs server to find the details of the error and refer to CookBook / Jira / SOP  documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 6. Daily Backups


| Area of Coverage | How is it Monitored | Course of Action | 
|  --- |  --- |  --- | 
| Database backups Reference [link here](https://docs.google.com/spreadsheets/d/1oMgqltpwKyVLWefIB305nrsAiqD0asXqPb-7ZKYPDm0/edit#gid=0)  | All backups are done via Jenkins jobs and managed services via its configurationAll the backups are stored in Azure Blob store Need to check whether the files are created as per the schedule If the backup file does not exists that is an incident  | Identify which backup is not done, check logs from jenkins or get the server access\*\* and debug\*to find the root cause to resolve the issue, you can manually run the backup, if the issue is resolved, do send an email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops logs | 

\*you can start from Jenkins backup job logs to find the details of the error and refer to CookBook / Jira / SOP  documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 7. Monthly Backups Restoration


| Area of Coverage | How is it Monitored | Course of Action | 
|  --- |  --- |  --- | 
| Restorations of backed up databases This activity is taken up  once in a month  Reference [link here](https://docs.google.com/spreadsheets/d/1dQqCa6JS-fyDirbFNULZdKhiR-xFQu7FZfXrqiAXUik/edit#gid=0) | You will pick last days backups for the restoration Backups are restored on to the pre-allocated servers based on the type and size of the database If any backup is not restorable, then that is an issue  Get server access\*\* for this activity | Identify which database is not restorable and debug\*to find the root cause to resolve the issue, if the issue is resolved, do send email to the [notify@teamdiksha.org](mailto:notify@teamdiksha.org)If the issue is not resolvable, then raise the ticket in DIKSHA Jira with  **S1**  and assign to DIKSHA Infra Owner  and send an email to [notify@teamdiksha.org](mailto:notify@teamdiksha.org) Update this in ops logs | 

\*you can check logs to find the details of the error and refer to CookBook / Jira / SOP  documents on the history of same type of issue

\*\* Get access approval from DIKSHA Infra Owner  via DIKSHA Jira to servers 




# 8. Other Critical Services


| Area of Coverage | How is it Monitored  | Course of Action | 
|  --- |  --- |  --- | 
|  **SMS Gateway Limit** Frequency: Twice a weekReference [link here](https://control.msg91.com/signin/)  | MSG91 account We have SMS credits in this account, alert if the threshold is <20% of total allocated credits | Raise  **S1**  and assign to DIKSHA Infra Owner, if the account credits are getting exhausted, we need to purchase more credits  | 
|  **Email Gateway Limit ** Frequency: Twice a weekReference [link here](https://app.sendgrid.com/login?redirect_to=%2Faccount%2Fdetails)  | SendGrid service on Azure, if the limits are exceeding for their monthly limits | Raise  **S1**  and assign to DIKSHA Infra Owner, you may need to upgrade to the next subscription to increase the limit  | 
|  **Video streaming service**  | We use Azure Media Service for streaming, Reference [link here](https://portal.azure.com/#@deepikaekstep.onmicrosoft.com/resource/subscriptions/5af454cb-5087-411d-a651-2d7d6c1b93a1/resourceGroups/production_all/providers/Microsoft.Media/mediaservices/ntpprodmedia/) | If they are failures, Raise  **S1**  issue and assign to DIKSHA Infra Owner  | 
|  **Report jobs**  | Reference [link here](http://10.20.0.9:8080/job/OpsAdministration/job/production/job/DataScience/job/daily_metrics/) | If they are not run for the day,Raise  **S1**  issue and assign to DIKSHA Infra Owner  | 




# PROCESS IN DIKSHA JIRA
The issues raised in Jira, needs to raised with Severity S1 or S2 based on the issue type defined above. 

The ticket needs to be assigned to DIKSHA Infra Owner, in his absence the designated SPOC he nominates. 

If there is any S1 which is created, do call DIKSHA Infra Owner and get the prioritisation set for the ticket immediately by him. Once it is Prioritised as P1, this needs to be followed up by NOC team every 30 mins or hourly based on the type of issue / impact of the issue to the end user.

If you are moving this issue to L3 team, post your discussions with DIKSHA Infra Owner/ SPOC, you are creating the bug in Sunbird Jira, it will be assigned to Release Management team member with S1 severity and Tag DIKSHA Infra Owner. 

Once the ticket is moved to L3, there will be a hot fix released for the same, which need to be tested in pre production and then moved to production. If any S1/P1 created in the last week of the release (in UAT phase) that will be going along with the release, the same needs to be tested and pushed along with that. 

All such issues needs to be verified and validated in pre production thoroughly and post explicit sign off gets moved to production. 




# Exceptions 
 _There are no exceptions to the process._ 


# Process Metrics

* Average percentage of 5xx errors per day  - this metric indicates if there are any server side errors from our services / components / infrastructure 
* Max TPS per day  - this metric indicates the current load against the benchmark level for the infra scale set
* TOP 10 API Response time 95 percentiles - these metrics indicate service response times from server 
* Average percentage of 4xx errors per day - this metric indicates the client side errors, but indirectly indicate any errors from our mobile app or any other known source. 





*****

[[category.storage-team]] 
[[category.confluence]] 
