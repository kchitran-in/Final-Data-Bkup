 **Functionality: ** 

The admin is able to manually send actionable progress based messages to contribution org contributors & reviewers



 **Challenges in the current solution flow:** 

There are 3 overarching use cases for which Prashnavali is being used for creation of good quality questions:-


1. Assessments


1. Practice Worksheets


1. Question Banks



The mentioned use cases require a quick turnaround time and close monitoring on the progress of the status and regular reminders to users to complete the assigned task. Just to add some colour:-


* For an assessment, usually 5 days are allotted to the contribution org contributor & reviewer to create, review, make required changes, resubmit and re-review around 40 questions each.  


* For a practice worksheet, each contribution org contributor has to complete two chapters per week (15 questions each), and each reviewer has to review questions for around 4 chapters per week (15 questions each)





Currently, to send reminders to all contribution contributors & reviewers, the admin has to do these steps:-


1. Login to the contribution portal


1. Go to ‘My Projects’


1. Open the desired project (approx. 46 projects in chapter worksheets)


1. See the overall progress status of the project


1. Open the desired question set (approx 15-30 question sets per project in case of chapter worksheets)


1. See the progress in that particular question set


1. Send a reminder/nudge to all contribution org contributors & reviewers





 **_Steps 3-7 need to be repeated for all projects & all question sets in that project_** 



 **Functional solution:** 

The admin is able to send reminders/nudges to users (contribution org contributors & reviewers) based on their progress on a project level



The proposed solution is:


1. Login to the sourcing portal


1. Go to “Create New Project”


1. Select content type


1. Fill the details of the project like name, description


1. Admin finds a default selected “Send Reminder” check box before moving to contribution and project end date


1. “Send Reminder” functionality has a description : “Send reminder messages to all assigned contribution org contributors/reviewers or both to remind them to contribute/review before contribution end date”


1. Go to ‘My Projects’


1. Open the desired project (approx. 46 projects in chapter worksheets)


1. Select a question set to check on progress


1. Send a reminder/nudge to all contribution org contributors & reviewers


1. Select contribution org contributors/ reviewers or both 





Slide[26-32](https://docs.google.com/presentation/d/13_KfHUE53_jqaGS6WBpDactC4b9KK7UT/edit#slide=id.g1591b24080d_0_84) attached for wireframes of the solution



 **Technical solution:** 

 **Approach** 


1.  **Adding Checkbox to send Reminder** 


    1. There will be one checkbox added to the UI on the project page by updating the sourcing project creation page. 


    1. This checkbox will only be visible to the users creating project type as Questionsets.



    

1incompleteUnderstand and propose updated to sourcing project creation page. 
1. Have to add an system environment variable: isSendReminderEnable, this key will have a boolean value. By default, isSendReminderEnable: false.


    1. Depending upon the system environment variable, the checkbox will be blank in the beginning. SourcingOrg Admin can enable it, if required.


    1. The updated value of the checkbox will be stored in the config of sourcing project.



    

2incompleteFind out system variable file.3incompletePropose new variable to be added.
1.  **Adding a button “‘Send a Reminder”** 


    1. Only if isSendReminderEnable: true in the config of collection, we’ll show the button “Send a Reminder” on the nomination page at question set level.


    1. On click of this button we’ll open a modal which will have UI as given below:

    [https://docs.google.com/presentation/d/13_KfHUE53_jqaGS6WBpDactC4b9KK7UT/edit#slide=id.g13681ada685_0_135](https://docs.google.com/presentation/d/13_KfHUE53_jqaGS6WBpDactC4b9KK7UT/edit#slide=id.g13681ada685_0_135)

    



    
1.  **Fetching User Details** 


    1. To have a list of users, we’ll have the data from following API on click of Send Reminder button.

    Nomination list(Existing API):


    1. API: program/v1/nomination/list

    We are already hitting this API on opening of nomination page.



    
    1. This API has Key: result\[0].rolemapping, which will give us the userIds of contribution org contributors and reviewers.


    1. For the complete details of users we will hit following API: 

    API: program/v1/contributor/search

    With the help of the above mentioned API we will show 2 fields as contribution org contributors and reviewers on UI.

    This checkbox will be disabled if users aren’t assigned to the project yet.



    
1.  **Sending Message** 


    1. On selecting at least one checkbox out of  contributor and reviewer, a button to send a message will be enabled on modal.


    1. On click of that button a template mail/SMS will be sent to selected users.

    For above mentioned functionality first we will hit search API to get the template of message and then SMS/Email API will get hit.


    1. Send SMS API:

API: user/v1/notification/email

    Doc: [http://docs.sunbird.org/latest/apis/notificationapi/#section/Authentication](http://docs.sunbird.org/latest/apis/notificationapi/#section/Authentication)



    



*****

[[category.storage-team]] 
[[category.confluence]] 
