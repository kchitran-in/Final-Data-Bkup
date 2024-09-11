



Introduction **Purpose:** In the current context, once a course is published any changes done to the course will impact user progress. In the ideal state, although we do not recommend authors to make changes to published courses, we have encountered the following scenarios which mandate us to support dynamic updation of user progress:




1. Content creation for courses is a tedious and time taking activity. Hence, the actual time needed to create content sometimes poses a challenge for the state to meet the course launch date. To mitigate this, state would like to publish their courses in phases i.e., if the course has 5 units, in the first phase publish 3 units and launch the course by creating batches, and keep adding the rest of the units to the live course.
1. Post publishing the course, if the state identifies the need to correct content/typos etc there should be a way to get these edits in the live course.

JTBD



|  **Who is the user and what is the user trying to do which is currently a struggle**  |  **What is the context**  |  **Functional Goal**  | 
|  --- |  --- |  --- | 
| State admin is struggling to meet the course launch timelines | Course launch | Enable state to be able to launch courses in multiple phases. | 



Requirement SpecificationsUse Case 1 OverviewThis use case deals with enabling content creators to be able to make edits to a live course without impacting the progress of the enrolled users. This will provide flexibility to the state to launch online courses in a phased manner, and carry out corrections such as typos etc.



User Story 1 - Overview (Portal)As a state admin I want to publish a course in phases so that I can at-least launch the course per the deadline and add subsequent units post launch without affecting the progress of the users’ enrolled in the course.

Main Scenario(s)Pre-requisites
* Course is published.
* Course has batches - batch can be an open batch or an invite only batch.

Scenario 1: Addition of new units/sub-units/resources to a published course with live batches.
1. As a content creator I should be able to add units/sub-units/resources to a live course (course with batches and enrolled users) created by me and publish it.
1. As a user enrolled into a course which was edited and re-published, I should be able to consume the newly published course without impacting my progress. 



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Adds a new unit/sub-unit/resource to a live course and publishes it | The course should now contain the new unit/sub-unit/resource | 
| 2 | Enrolled user who has already completed the course logs in to DIKSHA |  **My courses section:**  Progress gets updated from 100% to the new number. Lets say the course had 9 resources. User has completed all the 9 resources. Now a new resource is added. Hence, the updated user’s progress would be 90%. (9 completed out of 10) **Course ToC:** a) The updated progress has to be reflected in the course ToC page. b) In the course ToC page, the newly added resource’s status should be similar to the status of resources which are not yet completed by users **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session. **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since the updated progress is less than 100%. | 
| 3 | Enrolled user who is in the process of completing the course (Course progress < 100%) |  **My courses section:**  Progress gets updated to the new number. Lets say the course had 8 resources. User has completed 4 resources. Now a new resource is added. Hence, the updated user’s progress would be 44% (4 completed out of 9) from 50%. **Course ToC:** a) The updated progress has to be reflected in the course ToC page. b) In the course ToC page, the newly added resource’s status should be similar to the status of resources which are not yet completed by users **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session. **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course. **Unenroll:** User should be able to unenroll from the batch since the updated progress is less than 100%. | 

Scenario 2: Removal of unit/sub-unit/resources from a published course
1. As a content creator, I should be able to remove unit/sub-unit/resources from a live course created by me and publish it.
1. As a user enrolled into a course which was edited and re-published, I should be to consume the newly published course without impacting my progress.



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Removes an existing unit/sub-unit/resource from a live course and publishes it | The course should not contain the removed unit/sub-unit/resource | 
| 2 | Enrolled user who has already completed the course logs in to DIKSHA |  **My courses section:**  User’s progress would remain as 100%.  **Course ToC:** a) The user’s course progress remains the same. b) Removed resource is removed from the course ToC page **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  _If the last viewed/completed resource is removed then it should take them to the beginning of the course_  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should not be able to unenroll from the batch since their progress is 100%. | 
| 3 | Enrolled user who is in the process of completing the course (Course progress < 100%) - User has already completed the removed resource |  **My courses section:**  Progress gets updated to the new number. Let’s say the course has 8 resources. User has completed 4 resources. Now one of the existing resource which the user has already completed is removed. Hence, the updated user’s progress would be 42.8%. (3 completed out of 7) **Course ToC:** a) The user’s course progress gets updated. b) Removed resource is removed from the course ToC page. **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  _If the last viewed/completed resource is removed then it should take them to the beginning of the course_  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since their progress is less than 100%. | 
| 4 | Enrolled user who is in the process of completing the course (Course progress < 100%) - User has not completed the removed resource |  **My courses section:**  Progress gets updated to the new number. Let’s say the course has 8 resources. User has completed 4 resources. Now one of the existing resource which the user has not completed is removed. Hence, the updated user’s progress would be 57%. (4 completed out of 7) **Course ToC:** a) The user’s course progress gets updated. b) Removed resource is removed from the course ToC page **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since their progress is less than 100% | 

Scenario 3: Repetition of the same resource more than once in the published course
1. As a content creator, I should be able to add the same resource twice in a live course and publish it.
1. As a user enrolled into a course which has duplicate resources, I should be to consume the published course without impacting my progress.



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Add the same resource twice in the course | The course should have both the resources per the course structure designed and published by the author. | 
| 2 | Enrolled user completes the duplicate resource | Progress for both the resources in the course is marked as complete. i.e., if the course has 4 resources and one of them is repeated twice. If this resource is completed then the users' progress will be 50% (2/4 completed). | 

Exception Scenarios **Note:**  Any changes done to the course in the draft state should not impact the live version of the course until the course is published.

WireframesN/A

For Future ReleaseN/A

JIRA Ticket IDInsert the JIRA Ticket ID created for this story here. Click the + sign on the toolbar, select JIRA Issue/Filter from the list and either select a JIRA issue from the list or create one.   

User Story 2 Overview - Mobile AppAs a state admin I want to publish a course in phases so that I can at-least launch the course per the deadline and add subsequent units post launch without affecting the progress of the users’ enrolled in the course.

Main Scenario(s)Pre-requisites
* Course is published.
* Course has batches - batch can be an open batch or an invite only batch.

Scenario 1: Addition of new units/sub-units/resources to a published course with live batches.
1. As a content creator I should be able to add units/sub-units/resources to a live course (course with batches and enrolled users) created by me and publish it.
1. As a user enrolled into a course which was edited and re-published, I should be able to consume the newly published course without impacting my progress. 



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Adds a new unit/sub-unit/resource to a live course and publishes it | The course should now contain the new unit/sub-unit/resource | 
| 2 | Enrolled user who has already completed the course logs in to DIKSHA |  **My courses section:**  Progress gets updated from 100% to the new number. Lets say the course had 9 resources. User has completed all the 9 resources. Now a new resource is added. Hence, the updated user’s progress would be 90%. (9 completed out of 10) **Course ToC:** a) The updated progress has to be reflected in the course ToC page. b) In the course ToC page, the newly added resource’s status should be similar to the status of resources which are not yet completed by users **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session. **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since the updated progress is less than 100%. | 
| 3 | Enrolled user who is in the process of completing the course (Course progress < 100%) |  **My courses section:**  Progress gets updated to the new number. Lets say the course had 8 resources. User has completed 4 resources. Now a new resource is added. Hence, the updated user’s progress would be 44% (4 completed out of 9) from 50%. **Course ToC:** a) The updated progress has to be reflected in the course ToC page. b) In the course ToC page, the newly added resource’s status should be similar to the status of resources which are not yet completed by users **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session. **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course. **Unenroll:** User should be able to unenroll from the batch since the updated progress is less than 100%. | 

Scenario 2: Removal of unit/sub-unit/resources from a published course
1. As a content creator, I should be able to remove unit/sub-unit/resources from a live course created by me and publish it.
1. As a user enrolled into a course which was edited and re-published, I should be to consume the newly published course without impacting my progress.



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Removes an existing unit/sub-unit/resource from a live course and publishes it | The course should not contain the removed unit/sub-unit/resource | 
| 2 | Enrolled user who has already completed the course logs in to DIKSHA |  **My courses section:**  User’s progress would remain as 100%.  **Course ToC:** a) The user’s course progress remains the same. b) Removed resource is removed from the course ToC page **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  _If the last viewed/completed resource is removed then it should take them to the beginning of the course_  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should not be able to unenroll from the batch since their progress is 100%. | 
| 3 | Enrolled user who is in the process of completing the course (Course progress < 100%) - User has already completed the removed resource |  **My courses section:**  Progress gets updated to the new number. Let’s say the course has 8 resources. User has completed 4 resources. Now one of the existing resource which the user has already completed is removed. Hence, the updated user’s progress would be 42.8%. (3 completed out of 7) **Course ToC:** a) The user’s course progress gets updated. b) Removed resource is removed from the course ToC page. **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  _If the last viewed/completed resource is removed then it should take them to the beginning of the course_  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since their progress is less than 100%. | 
| 4 | Enrolled user who is in the process of completing the course (Course progress < 100%) - User has not completed the removed resource |  **My courses section:**  Progress gets updated to the new number. Let’s say the course has 8 resources. User has completed 4 resources. Now one of the existing resource which the user has not completed is removed. Hence, the updated user’s progress would be 57%. (4 completed out of 7) **Course ToC:** a) The user’s course progress gets updated. b) Removed resource is removed from the course ToC page **Resume Course:** User clicks on ‘Resume course’ or the ‘Course card’ from My courses section, it should take them to the last viewed/completed resource in the previous session.  **Navigation:** Should work as normal - clicking on next should navigate the user to the next resource in the course; clicking on previous should navigate the user to the previous resource in the course **Unenroll:** User should be able to unenroll from the batch since their progress is less than 100% | 

Scenario 3: Repetition of the same resource more than once in the published course
1. As a content creator, I should be able to add the same resource twice in a live course and publish it.
1. As a user enrolled into a course which has duplicate resources, I should be to consume the published course without impacting my progress.



| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Content creator: Add the same resource twice in the course | The course should have both the resources per the course structure designed and published by the author. | 
| 2 | Enrolled user completes the duplicate resource | Progress for both the resources in the course is marked as complete. i.e., if the course has 4 resources and one of them is repeated twice. If this resource is completed then the users' progress will be 50% (2/4 completed). | 

Exception Scenarios **Note:**  Any changes done to the course in the draft state should not impact the live version of the course until the course is published.

WireframesN/A

For Future ReleaseN/A

JIRA Ticket IDInsert the JIRA Ticket ID created for this story here. Click the + sign on the toolbar, select JIRA Issue/Filter from the list and either select a JIRA issue from the list or create one.   

Localization RequirementsUse this section to provide requirements to localize static content and/or design elements that are part of the UI in the following table. Localization of either the framework, content or search elements should be elaborated as a user story. To add or remove rows in the table, use the table functionality from the toolbar.    



| UI Element | Description | Language(s)/ Locales Required | 
|  --- |  --- |  --- | 
| Mention the UI Element that requires localization. e.g. Label, Button, Message, etc.  | Provide the exact details of the element that requires localization. e.g. User ID, Submit, 'The content is currently unavailable'  | Mention all the languages or locales for which localization is required  | 
|  |  |  | 



Telemetry RequirementsN/A



Non-Functional RequirementsUse this section to capture non-functional requirements in the following table. To add or remove rows in the table, use the table functionality from the toolbar.    



| Performance / Responsiveness Requirements | Load/Volume Requirements | Security / Privacy Requirements | 
|  --- |  --- |  --- | 
| Updated progress (depending on whether a new resource was added or removed) should reflect real time to the users when they log in/refresh the page. | 
1. Courses can have upto 5 active batches running in parallel
1. Each open batch can have participants upwards of 1L

 |  | 
| Prev/Next navigation should take the user to the Prev/Next resource/unit as per the updated course structure |  |  | 



Impact on other Products/SolutionsN/A



|  |  | 



Impact on Existing Users/Data N/A



Key MetricsN/A



|  |  | 





*****

[[category.storage-team]] 
[[category.confluence]] 
