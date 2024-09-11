



IntroductionThis report will provide you the total list of Live contents created or uploaded in that state with the consumption matrixes for those content.   

JTBD
*  **Jobs To Be Done: ** As a state admin, I want to have a look at various aspects of the content such as creation failures, etc.
*  **User Personas:**  The logged-in users who have State Admin role, Report Viewer role can access this report.
*  **System or Environment:**  Works on for desktops with Chrome browser only.

Requirement SpecificationsThis content consumption report generates in 3 types, For all these reports the data fields will be the same as bellow.


1. Content Consumption Aggregated metrics till date
1. Content Consumption Metrics for the last 6 weeks
1. Content Consumption Metrics for the last weeks



|  **STATE**  |  **BOARD**  |  **MEDIUM**  |  **Class**  |  **SUBJECT**  | Content-Type |  **CONTENT ID**  | Content Name |  **Creator (User Name)**  |  **CONTENT MIME TYPE**  |  **Created On**  |  **Last Published Date**  | Linked Textbook Id | Linked Textbook Name |  **No. of Downloads (App only)**  | No. of  Plays (on App and Portal) | No. of  Plays on App | No. of  Plays on Portal |  **Average Play Time in mins (on App and Portal)**  |  **Average Play Time  in mins on App**  |  **Average Play Time in mins on Portal**  | Total No of Ratings |  **Average  Rating (Out of 5)**  | End Date  of the Week | 
|  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- | 
| Rajasthan | RJ | ENGLISH | 10 | ENGLISH | Resource | do_123456 |  | XYZ | MP4 | 04/10/2017   | 24/11/2017 | do_7890 | Science |  |  |  |  |  |  |  |  |  |  | 



 **Key points:** 


1. Display records for all published content
1. The report will have one record for each content which is in "LIVE" status
1. Explanation of specific fields in the report:
1. This will have all the contents sorted by State, Board, Medium, Class, Subject.
1. This report is generated based on the state tenant.
1. This report should be updated on a weekly basis.
1. Last updated on Field should be shown on the top in the "content consumption metric for the last 6 weeks" report.
1. This report will have only 1 table, No graphs are shown.
1. In the table, the overall "Content Consumption Aggregated metrics till date" will be shown and there will be 3 download buttons on the top, One is for "content consumption Aggregated metrics till date" and followed by the other two reports.
1.  No table view for  "Content Consumption Metrics for the last 6 weeks" and "Content Consumption Metrics for the last weeks", Only Download CSV option.
1. Whenever the report is updated in portal the Last "updated on" field should show that date.
1. In the portal, This report should be shown below the "Daily Usage " Report.
1. When the report is downloaded the file name should be as follows 
    1. Content aggregated metrics:- content_aggregated
    1. Content Consumption Metrics for the last 6 weeks:- content_consumption
    1. Content Consumption Metrics for the last weeks:- content_consumption_lastweek

    



 **Sample Report** 


1. Content Consumption Aggregated metrics till date

 **https://docs.google.com/spreadsheets/d/1tMDUwDjwD-6x3U4Fmiu1CEQeBOIyL1em2R3lQIEOT8k/edit?usp=sharing** 

2. Content Consumption Metrics for the last 6 weeks

3. Content Consumption Metrics for the last weeks

 **https://docs.google.com/spreadsheets/d/1a_QlkFdBuGJYXkB0JjtljUs6I6GFmRyhPQFVEXKqWRs/edit#gid=1530612835** 

WireframesJIRA Ticket ID[SB-13557 System JIRA](https:///browse/SB-13557)[SB-17458 System JIRA](https:///browse/SB-17458)[SB-17609 System JIRA](https:///browse/SB-17609)



 **Title and the Description** 

 **Title:** Content Consumption Report

 **Report Description** : This report provides details about all content that are published and their consumption statistics. The details are specific to each state and is updated on a weekly basis.

Localization RequirementsN/A

Telemetry Requirements

| Event Name | Description | 
|  --- |  --- | 
| Open Reports Page | This event is generated when a user opens Reports page in a Program. Apart from common set of data, Program Id should be captured in the event. | 
| Download Aggregated Metrics | This event is generated when a user clicks on "Download Aggregated Metrics" option in the Reports page. Apart from common set of data, Program Id should be captured in the event. | 
| Download Metrics for the last 6 weeks | This event is generated when a user clicks on "Download Metrics for the last 6 weeks" option in the Reports page. Apart from common set of data, Program Id should be captured in the event. | 
| Download Metrics for the last weeks | This event is generated when a user clicks on "Download Metrics for the last weeks" option in the Reports page. Apart from common set of data, Program Id should be captured in the event. | 



Non-Functional Requirements

| Performance / Responsiveness Requirements | Load/Volume Requirements | Security / Privacy Requirements | 
|  --- |  --- |  --- | 
| Report should work correctly for English and Non-English content |  | NA | 



Impact on other Products/SolutionsN/A

Impact on Existing Users/Data N/A

Key Metrics

| Srl. No. | Metric | Purpose of Metric | 
|  --- |  --- |  --- | 
|  | Number of users downloading the Reports | Track the effectiveness of features through their usage. | 





*****

[[category.storage-team]] 
[[category.confluence]] 
