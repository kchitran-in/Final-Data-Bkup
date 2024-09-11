



IntroductionState conducts in-person teacher classroom training for different grades and subjects under SSA (Samagra Shiksha Abhiyan). However, budget constraints limit the number of teachers who are trained in these programs (on an avg less than 15% of total teachers are usually trained). Rest of the teachers have to wait for their turn to be nominated for these trainings leading to a delay in fulfilling the training needs of the state’s teacher population. Secondly, the content in these training sessions is revised annually (validated with AP state) hence a teacher who was trained last year is not aware of the new concepts introduced in this year’s training.

Hence, there is a need for the state to roll out online courses inline with classroom training sessions and make them available for consumption to target teacher audience anytime or within a defined duration.

 **_What_** : Helping state toprovide access to training content for all teachers;

 **_Who_** : State;

 **_Why_** : Budgetary concerns preventing the state to provide in-person trainings to all teachers in the state;





|  **Who is the user and what is the user trying to do which is currently a struggle**  |  **What is the context**  |  **Functional Goal**  |  **Emotional/Social Goal**  | 
|  --- |  --- |  --- |  --- | 
| State, when trying to conduct training sessions, does not have necessary budget to conduct in-person trainings to all teachers in the state. | Teacher Training |  _Ability to provide online courses for all the teachers in state_  |  _Recognition for the state within the teaching community for providing them to access to training content._  | 



JTBD
*  **Jobs To Be Done:**  ** ** State, when trying to conduct training sessions, does not have necessary budget to conduct in-person trainings to all teachers in the state.
*  **User Personas:** 
    *  **Content Creator:**  Role which has access to create courses
    *  **Content Reviewer:**  Role which has access to review and publish courses
    *  **Course Mentor:**  Role which has access to create batches and monitor batches via course dashboard
    *  **Badge Creator:**  Role which has access to create badges

    

All the above roles are envisioned as admin activities and hence typically are carried out by state admin or authorized personnel from SCERT office.


* 
    *  **User:**  End user who consumes the course - typically a state teacher

    
*  **System or Environment:**  Admin related functionalities - course creation and review, batch creation and monitoring of batches - are designed to work on desktop/laptop form factor. Consumption experience is designed to work on mobile, tablet and desktop/laptop form factors.

 _Portal:_ 


1. Min. internet speed (download): [1 Mbps](https://docs.google.com/spreadsheets/d/12dyQL2Mcwahon5Tpx45RPjXYUUvvDpEJEwRC73SaKmQ/edit#gid=0)
1. Time to load any webpage (first meaningful paint): 3 seconds
1. Max. time for any webpage to be interactive (consumption side): 5 seconds
1. Max time to load a content slide in player (streaming/online play): 3 seconds
1. Accessibility (basic level): All images with alt tags 
1. Cross-browser support: Chrome 50 + (desktop + mobile), UC Web (mobile only), Firefox (desktop only) 
1. Resolution: 
1. Active devices per day:  _70,000 (Predicted - 200,000 to 500,000)_ 
1. Concurrent users:  400 requests/sec, concurrent logins

 _Mobile App:_ 


1. Time taken to show book details after downloading spine: <3 seconds
1. Time taken to show ‘Play’ after downloading content: <3 seconds

Requirement SpecificationsThis section consists of requirement specifications for specific use cases in the User JTBD. The requirements for each use case are elaborated in detail through sub-sections for:


* Use case overview
* Overall process workflow
* Associated user stories 
* Non-functional requirements
* Localization requirements  
* Telemetry requirements
* Dependencies
* Impact on other products
* Impact on existing data  

Use Case 1: Issue of Course Completion Certificate - OverviewThis use case is related to providing a course completion certificate to a user who has completed a course, if there is a certificate associated to it. Once a certificate is associated to a course all the batches created for that course within the tenant inherit the certificate. This certificate is a digitized completion certificate equivalent of an existing paper certificate which can be accessed from the user profile page.

 **Why Certificates?** Teachers deem a certificate provided by a valid authority as an important artefact:


* serves as an evidence of completing a training


* collection of multiple certificates can potentially build teachers' learning profile


* permanence of the certificate since it is in a digitized format



Hence, the value of including this use case as an integral part of the teacher's online course journey.  

Further, awarding a certificate is a common mechanism used to recognize people with a set of skills and accomplishments:


* Helps to create a standard system of recognition across organizations. A certificate is recognizable and verifiable. It brings in  **_Trust_** 
* Helps teachers to showcase their skills and achievements to others to get a sense of  **_Satisfaction_**  and  **_Recognition_** . It can also lead to material benefits such as, monetary rewards, promotions, recommendations etc.

 **In-scope for this use case** There are broadly two types of certificates:

 _Digital certificates_  - certificates which are based on the principles of verifiability and portability

 _Digitized certificates_  - pdf certificates which are equivalent of a paper based certificate which the users can download

The scope for this use case is  **'Digitized Certificates'. ** 

Epic JIRA Ticket ID[SB-11097 System JIRA](https:///browse/SB-11097)

Use Case 1: Issue of Course Completion Certificate - Overall Process Workflow![](images/storage/Certificate%20workflow%20(1).jpg)



Use Case 1: Issue of Course Completion Certificate: Assertion of certificate to a course - OverviewMain Scenario:Assertion of a certificate to a course will be done using a API from the back end. API will be used to carry out the following functions:

1) Associate a certificate to the course2) Update existing course certificate <if the certificate is already set>3) Remove association between certificate and the course

These certificates will be modelled after the physical certificate currently issued by the state and will comprise of the following components:



| Name | Description | Optional/Mandatory | 
|  --- |  --- |  --- | 
| Issuer | will be the state body issuing the certificate (organization or institution) | Mandatory | 
| Recipient | will be the teacher who has completed the course | System populated | 
| Training program name | will be the name of the course which they have completed | System populated | 
| Signatory | will be name of the individual signing the certificate  | Optional | 
| Signature | will be the digital signature image of the signatory | Optional | 
| Completion date | will be the <month, year> when the teacher completed the training | System populated | 

 **Mapping of the components:** 
* A state can have multiple unique issuers.
* Each issuer will have single signatory and signature.
* Each certificate will have a single issuer, signatory and signature.



The structural model for certification infra needs to be built on Open badges model and add extensions where necessary.

 **Pre-requisites:** 
* Course is published


* Certificate template is available


* State has provided the details needed to assert the certificate


    * Issuing authority/Issuer name - The issuer will be an organisation or institution which is a competent authority to certify recipients. Note that the issuer is different from the signatory (i.e. the individual(s) who applies his/her signature to the credential). 


    * Signatory - will be the name of the individual/authority signing the certificate. 


    * Signature - will be the digital signature of the signatory. 



    



| Srl. No. | User Action (API) | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Assert certificate to a course which does not have any certificates attached | Asserted certificate to be added to the course | 
| 2 | Assert certificate to a course which already has a certificate attached | Should fail with proper error message | 
| 3 | Update certificate to a course which has a certificate attached | The updated certificate will be asserted to the course | 
| 4 | Remove asserted certificate to a course | Asserted certificate will be disassociated | 
| 5 | Update/Remove certificate when no certificate is attached to a course | Should fail with proper error message | 

Alternate Scenario 1:N/A

Exception Scenarios: **_When the signatory changes?_** 

In this scenario, the digital signature image is updated with the new signature image by the DIKSHA implementation team. The new signature image is provided by the state.

WireframesN/A

For Future Release
* As a badge creator, I want to assert certificates to courses created within my tenant so that users receive the certificate upon course completion.

JIRA Ticket ID[SB-11098 System JIRA](https:///browse/SB-11098)

Use Case 1: Issue of Course Completion Certificate: Auto issue of certificate upon completion of course - OverviewUsers who complete the course which has an active completion certificate associated will be awarded the completion certificate. This awarded certificate will be made available for download to the user in their profile page. 

Pre-requisites:
* Course is published


* Certificate is asserted to the course


* User is enrolled into the course batch


* User's course progress is 100%





| Srl. No. | User Action | Expected Result | 
|  --- |  --- |  --- | 
| 1 | Step1: User enrolls into an open/invite-only batchStep2: Completion certificate is associated to a courseStep3: User completes the course | User receives the certificate | 
| 2 | Step1: User enrolls into an open/invite-only batchStep2: User completes the course Step3: Completion certificate is associated to the course at a later date | User does not receive the certificate since they have completed the course before the certificate was associated | 
| 3 | Step1: User enrolls into an open/invite-only batchStep2: User completes the course which has a certificate associatedStep3: The associated certificate is removed from the course | User retains the certificate | 
| 4 | Step1: User enrolls into an open/invite-only batchStep2: User completes the course which has a certificate associatedStep3: A new certificate is associated to the course | User retains the old certificate | 
| 5 | Step1: User navigates to the profile page in the portal/mobile web view/mobile appStep2: User views the completed course under 'Trainings attended' section.Step3: User clicks on 'Certificate' | Certificate opens up as a pdf file | 

Alternate Scenarios: Once a certificate is associated to a course all the batches created for that course within the tenant inherit the certificate. i.e., teachers enrolled into batches created by mentors from other tenant will not be receiving the certificates.

Exception Scenarios: **Scenario 1** 

If for some technical reason valid user(s) who should have received the certificate have not received it.


* All these user details should be captured and shared with DIKSHA implementation team on a daily basis by an overnight batch job


* DIKSHA implementation team to manually assert these certificates to these users



 **Scenario 2** 

Lets say a user has completed the course but for some reason has not received the certificate. However, before the certificate was manually provided to the user, the certificate was updated or removed. 

In this scenario, the user should still be provided with the certificate that was active when the user completed the course.

Wireframes<Add UX links>

For Future Release(s)
* As a teacher, who'd want to enroll into courses, I want to be able to identify courses which offer completion certificates upon completion of the course so that I can decide whether to enrol into the course or not.


* As a state admin, I want to be able to ensure certificates are to be awarded ONLY to teachers from my state so that teachers from other states do not receive my state authorized certificates.


* As a state admin, I want to be able to view valid teachers who have not received certificates so that I can ensure that certificates are awarded to these teachers.


* As a teacher, I want to be notified via an email or mobile as soon as I receive the completion certificate so that I'm aware that I can now download my certificate.



JIRA Ticket ID[SB-11099 System JIRA](https:///browse/SB-11099)



Enhancement to download report in the Course Dashboard page - OverviewThe report currently captures the following fields:


* User Name
* Org Name (the tenant name)
* School Name (sub-org name)
* Enrolled on (date when the user has enrolled into the course)
* Course Progress
* Mobile Number (masked)
* Email ID (masked)

AP state has articulated the need that they will drive course enrollment and completion via their district nodal officers hence the need to include user’s district information in this report. This district information needs to be pulled from user profile information. In case users’ do not have district information updated in their profile it can be left blank. The new sequence of the report fields is as following:




* User Name
* Mobile Number (masked)
* Email ID (masked)
* Org Name (the tenant name)
* District Name
* School Name (sub-org name)
* Enrolled on (date when the user has enrolled into the course)
* Course Progress

JIRA Ticket ID[SB-11100 System JIRA](https:///browse/SB-11100)

Localization Requirements

| UI Element | Description | Language(s)/ Locales Required | 
|  --- |  --- |  --- | 
| Certificate Button | Localization needed for 'Certificate' button in the user profile page | To be translated in all languages currently in scope for DIKSHA | 



Telemetry Requirements

| Event Name | Description | Purpose | 
|  --- |  --- |  --- | 
| Click 'Certificate' in the user profile page | User can download the certificate by clicking on 'certificate' button in the user profile page | This data will enable us to measure the scale at which this functionality is used. | 
| Click 'Download File' in the course dashboard page | Mentor can download the report by clicking on 'Download File' button in the course dashboard page | This data will tell us how many users are actually clicking on this button to download the progress report. | 



Non-Functional Requirements

| Performance / Responsiveness Requirements | Load/Volume Requirements | Security / Privacy Requirements | 
|  --- |  --- |  --- | 
| Provide the perfomance or the responsivenes required from the system to ensure that the Use Case is effective.  | Provide the load or volume required from the system to ensure that the Use Case is effective. | Provide security and privacy requirements for an effective Use Case  | 
| <ul><li>Certificates to be issued in real time to teachers upon completion of the course.</li><li>Support certificate download sizes upto 200kb.</li><li>Certificate will be in pdf format.</li><li>In case of network connectivity failure show appropriate messages when user clicks on 'Certificate' to download certificate.</li><li>Any certificate issue failures are to be captured and reported</li><li>Course batch size to be upto 1L</li><li>Download file to support batch size upto upto 1L</li><li>Downloaded file is sent as an email attachment to the requestors email ID. The time lapsed between the request and receipt of the email should not exceed 30 mins. </li></ul> | <ul><li>Load time of the certificate < 3 secs.</li></ul> |  | 



Impact on other Products/Solutions

| Product/Solution Impacted | Impact Description | 
|  --- |  --- | 
| Teacher profile page | existing profile page will be enhanced to capture the certificate details in the trainings attended section | 



Impact on Existing Users/Data 

| User/Data Impacted | Impact Description | 
|  --- |  --- | 
| None |  | 



Key Metrics

| Srl. No. | Metric | Purpose of Metric | 
|  --- |  --- |  --- | 
| 1 | Portal + Mobile web + Mobile App: **Certificate download ratio**  = no. of certificate downloads/total number of certificates issuedThis ratio to be monitored at the level of:<ul><li>individual course and</li><li>all courses </li></ul> | This metric will provide insights on whether teachers are downloading the certificates awarded to them and hence will provide a objective feedback on the scale at which this functionality is used. | 





*****

[[category.storage-team]] 
[[category.confluence]] 
