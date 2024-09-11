
## Value for each persona (JTBD)
Refer to EPIC: [SB-11947 System JIRA](https:///browse/SB-11947)

 **Vision**  : To enable teachers to be able to teach in a better way, and students to understand topics in a better way & prepare for exams.

 **Goal** : Provide access to resources to enable teachers (to teach) and students (to understand topics, prepare for exams) by providing a bouquet of resources.

To enable better teacher preparation, provide 


1. Lesson Plans: Engage students in a systematic way with variety of teaching ideas
1. Curiosity Questions: Pique students’ interest while initiating a new chapter
1. Focus Spots: Explain confusing topics in an easy manner
1. Learning Outcome Definition: Know expected outcomes of the chapter
1. Marking Scheme Rubric: Know scoring rules and weightage for the chapter

Additionally a teacher may also find useful


1. Explanation resource: Refresh my own concepts and Explain concepts better
1. Experiential resource: Get students to relate better to the topic through real-life application
1. Practice Q-A Sets: Give diverse practice beyond textbook

 **Objective** : These resources can be provided in a well organised manner by leveraging textbook on Sunbird. A textbook containing these resources would be structured as below


* Textbook
    * Chapter 1 (Topic 1)
    * Teach
    * Lesson Plan
    * Curiosity Questions
    * Focus Spot
    * Learning Outcome Definition
    * Marking Scheme Rubric

    
    * Learn
    * Explanation resource
    * Experiential resource

    
    * Practice
    * Multiple Choice Question Practice Set
    * .. (other practice sets)

    

    
    * Chapter 2 (Topic 2)
    * ..
    * Chapter n (Topic n)

    

Enable teachers and students to engage with a textbook using a variety of resources. Some of the possible JTBDs for a teacher, student, or parent are

![Value for a senior student](images/storage/CBSE%20Launch_Value%203.jpg)

![Value for an experienced teacher](images/storage/CBSE%20Launch_Value%201.jpg)

![Value for a young teacher](images/storage/CBSE%20Launch_Value%202.jpg)

![Value for a middle school student](images/storage/CBSE%20Launch_Value%204.jpg)

![Value for a parent (mother)](images/storage/CBSE%20Launch_Value%205.jpg)


### Resources to enable JTBDs
To deliver these values, following types of resources can be made available using Textbook in SunbirdEd

![](images/storage/CBSE%20Launch_Value%20Resources.png)






## Workflow for creation programmes
A SunbirdEd adopter tenant wants to crowdsource content from its users (primarily teachers) for teacher & student enablement.

Admin of a program will ensure that following things are in place


1. Taxonomy framework including Learning Objectives mapped to Topics
1. Users with required permission rights for Administration, Creation, and Review
1. Program ID is created

For programs portal, following setup needs to be done


1. Content Types: This program supports only Practice Set creation, review, publishing, and linking to textbooks.
1. Textbooks for Contribution: Create textbooks on SunbirdEd textbook editor and link them to a program ID
1. Participating Teams (Schools): Setup list of Schools for program portal
1. Publishing and Linking logic: Build logic as per predefined textbook structure. Current logic supports textbook structured as \[ Textbook > Level 1 Unit (Chapter) > Level 2 Unit (Question Bank) > .. ]. All Practice Sets published are linked to 'Question Bank' folder if it is present at Level 2 Unit
1. Question Types & Categories: Question types - mcq, reference; Question categories - vsa, sa, la, mcq
1. Roles: Program portal supports 3 roles - Contributor, Reviewer, Publisher

Contributor onboarding


1. First time sign-in / sign-up with Google will grant Contributor role
1. On first time sign-in, the user needs to select onboarding details (B, M, C, S) and School

Contribution Workflow


1. Sign-in with Google
1. Select Class & Subject
1. Select Textbook
1. Select Chapter. Only Textbook Level 1 Unit which are linked to topic are shown as "Textbook Unit Name (Topic)"
1. For each chapter, contributor can see Total, Created by Me, Needs Attention
1. Select Question Category to start creating questions
1. Question creation page is open with empty form for first question to be created. User can Preview or Submit the question.
    1. User cannot Save questions. If user goes back without submitting, the question is cleared / lost.

    
1. Select Learning Outcome for the question. Learning Outcomes only for current selected chapter (topic) are shown.
1. Select Learning Level for the question


### Watch following videos to learn more about 'How to contribute'
How to use the Question Bank Contribution Website. Instructions on how to Sign up and Sign in and set up the tool for yourself as a teacher. Then a small walk through of what a textbook looks like. 

[https://www.youtube.com/watch?v=BXs8hYNp68Q&feature=youtu.be](https://www.youtube.com/watch?v=BXs8hYNp68Q&feature=youtu.be)   



How to create Question Packages. A walk through of all the different types of questions, and how to add the Question, Answer, Learning outcome and learning level, in each type and how to submit a question and a watch out that a Teacher must create at least 5 questions in each type, across all chapters of a textbook for it to be a complete package. 

[https://www.youtube.com/watch?v=rJM5nX_153E&feature=youtu.be](https://www.youtube.com/watch?v=rJM5nX_153E&feature=youtu.be)    



How to add Formula and Equations. A guide on using the  _Mathtype_ and  _Chemtype_ features on the tool so teachers can add any mathematical or chemical formula or equation on the tool and the drawing tool to add the same. Video also shows the possible problems with copy-pasting formulates from other sources and how to solve the issues that come up. 

[https://www.youtube.com/watch?v=VTF4ueR2uaU&feature=youtu.be](https://www.youtube.com/watch?v=VTF4ueR2uaU&feature=youtu.be)   



How to add images. A simple video on how to upload and add images to questions, answers or even options and how to align them. 

[https://www.youtube.com/watch?v=sIh3Ecd1d4g&feature=youtu.be](https://www.youtube.com/watch?v=sIh3Ecd1d4g&feature=youtu.be)   



How to use MCQ templates. A guide to understanding the 4 four different templates provided under MCQ, how to select them and when and why to use each template depending on the teacher's requirement, 

[https://www.youtube.com/watch?v=vvFFMl4O4j0&feature=youtu.be](https://www.youtube.com/watch?v=vvFFMl4O4j0&feature=youtu.be) 




## Summary of requirements


|  | Resource | Audience | Available as | Stored as | Knowledge Platform  | Creation | Review | Resource Creation | Consumption | Sample for Reference | 
|  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- |  --- | 
| 1 | Learning Outcome Definition | Teacher | Bullet points | JSON(Asset) | Required - Add a new framework category | eVolve & Bulk upload | On Platform | Will be packaged as Resource per chapter via bulk upload job | Plugin to be developed | [Link](http://www.ncert.nic.in/publication/Miscellaneous/pdf_files/tilops101.pdf) | 
| 2 | Lesson Plan | Teacher | Documents | PDF(Resource) | TBD | Bulk upload(from eVolve) | on eVolve | Default | PDF player enhancements | [Link](https://diksha.gov.in/explore/1?contentType=lessonPlan&appliedFilters=true) | 
| 3 | Hard Spot | Teacher | Paragraph Text | JSON(Asset) | None | eVolve & Bulk upload | On Platform | Will be packaged as Resource per chapter via bulk upload job | Plugin to be developed | [Link](https://docs.google.com/spreadsheets/d/1QXUm_UWuXV4RA0vE7B7UjxbvyJxgii29XcpP16azQMk/edit?usp=sharing) | 
| 4 | Transdisciplinary Teaching | Teacher | Document | PDF(Resource) | Required | Bulk upload | Offline | Default | PDF player enhancements |  | 
| 5 | Curiosity Questions | Teacher | Paragraph Text | JSON(Asset) | TBD | eVolve & Bulk upload | On Platform | Will be packaged as Resource per chapter via bulk upload job | Plugin to be developed | [Link](https://preprod.ntp.net.in/play/collection/do_21270930228983398415165) | 
| 6 | Marking Scheme Rubric | Teacher | Documents | PDF(Resource | Required | Bulk Upload | Offline | Default | PDF player enhancements |  | 
| 7 | How-to Teach | Teacher | Video | MP4(Resource) | To be enhanced | Bulk upload(from eVolve) | on eVolve | Default | TBD |  | 
| 8 | Explanation | Student &Teacher | Video | MP4(Resource) | To be enhanced | Bulk upload | on eVolveor Offline | Default | TBD | [Link](https://preprod.ntp.net.in/play/collection/do_21270930228983398415165) | 
| 9 | Experiential Learning | Student &Teacher | Video | MP4(Resource) | To be enhanced | Bulk upload(from eVolve) | eVolve | Default | TBD | [Link](https://preprod.ntp.net.in/play/collection/do_21270930228983398415165) | 
| 10 | Suggested Rubric forSelf-Assessment | Student &Teacher | Document | PDF(Resource) | Required | Bulk upload | Offline | Default | PDF player enhancements |  | 
| 11 | Questions for Practice | Student &Teacher | Rich text with formulae, image | QuML(Asset) | To be enhanced | Required | Required  | Will be packaged as Resource per chapter through a job | Plugin to be developed | [Link](https://preprod.ntp.net.in/play/collection/do_21270930228983398415165) | 
| 12 | Additional Resources for Teaching Pedagogy | Teacher | Document orVideo | PDF orMP4 | To be enhanced | TBD | TBD |  |  |  | 




### PDF player enhancements

1. Auto-hide navigation bar on top
1. Navigate to next page on scroll
1. Pinch to zoom
1. Allow orientation change to portrait (optional)
1. Download PDF for printing

[SB-11946 System JIRA](https:///browse/SB-11946)


### Plugin to be developed

1. Learning Outcome Definition, Hard Spot, Curiosity Question, Questions for Practice will have similar plugin design [SB-11790 System JIRA](https:///browse/SB-11790)
1. Navigation needs to be changed as per [SB-8305 System JIRA](https:///browse/SB-8305) 


### Question Review 
Review should be able to view questions by Textbook > Chapter (B, M, C, S > Topic)

For each question, reviewer should be able to accept or reject with comments

Question creator should receive email notification post review


### Question Creation
Creator should be able to create question for Textbook > Chapter (B, M, C, S > Topic)

Question types to be supported: 


1. Self-Study (VSA, SA, LA, Curiosity): These questions do not get evaluated on device, user can read question and then read answer for self-study. These are essentially two text paragraphs which may contain rich text, formulae and one image per question
    1. Ability to create & review these questions on system is required
    1. UX designs are being finalised by next week

    
1. MCQ: Few enhancements to current capabilities
    1. Layout selection for MCQ needs to be made upfront so that user will provide only required details for selected layout. UX designs being finalised by next week
    1. Enhancements as listed

    

[ System JIRA](https:///browse/)


### Knowledge Platform changes

1. Ability to store each of the above resource & asset types


### Workspace changes

1. Creator (Workspace 'Create') & Reviewer (Workspace 'Up for Review') should be able to start contributing by selecting Textbook > Chapter (B, M, C, S > Topic)
1. UX design to be finalised by next week 


## Additional Information

### Changes to eVolve
These are being estimated by 12th April and are expected to be ready by 22-25 April



Contribution and review of documents
1. Allow uploading documents (doc, ppt, pdf)
1. Show preview of these documents to reviewer
1. Ability to tag these documents as any one of Lesson Plan, Concept map (Mind map), Marking Scheme Rubric, Suggested Rubric for Self-Assessment (will have one separate link for contribution and review for each of this type)
1. Ability to download these in a csv format



Contribution and review of other text
1. Allow entering  text, similar to Hard Spot and tag it as either Learning Outcome Definition, Curiosity Question  (will have one separate link for contribution and review for each of this type)
1. Show preview to reviewer
1. This will be plain text - no formulae, images, or text styling
1. Ability to download these in a csv format

Contribution and review of two types of videos
1. Allow uploading video and tag it as Explanation or Experiential  (will have one separate link for contribution and review for each of this type)
1. Show preview to reviewer 
1. Currently supported video formats - no further enhancements
1. Ability to download these in a csv format

Each content / resource type will be launched as an independent eVolve programme. Users can contribute or review by going to unique links for each one. Reviewers will be on-boarded individually for each one.



*****

[[category.storage-team]] 
[[category.confluence]] 
