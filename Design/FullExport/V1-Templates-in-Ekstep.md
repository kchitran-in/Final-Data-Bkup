This document contains details about the older v1 templates available in ekstep. It provides information about how to


* Create and upload templates.
* Create questions(MCQ, FTB and MTF) in ekstep portal.
* How to debug template issues.

 **Types of templates** 


1. MCQ
1. FTB
1. MTF



 **How to create questions using templates** 


1. Login to dev.ekstep.in or qa.ekstep.in
1. Click on Resources → Question Bank'
1. It will show you the list of available templates and the preview
1. To create a new question, Click on Add Question
1. And select a template and click start creating
    1. For FTB,
    * Enter the question text, the question text may be the title for the question or may be the question itself.
    * Enter the answer text, the answer text can be single or multiple
    * It may have the additional Model field to be filled for some templates.
    * For some templates, the questions and answers can be generated randomly.

    
    1. For MCQ,
    * Enter the question text, the question text may be the title for the question or may be the question itself.
    * Enter the answer text, the answer text can be single or multiple
    * It may have the additional Model field to be filled for some templates.
    * For some templates, the questions and answers can be generated randomly. 

    
    1. For MTF,
    * Enter the question text, the question text may be the title for the question or may be the question itself.
    * Enter the answer text, the answer text can be single or multiple
    * It may have the additional Model field to be filled for some templates.
    * For some templates, the questions and answers can be generated randomly. 

    

    
1. Click on "save" and "save & create another"
1. The created question will be available in the question bank.



 **List of available v1 templates in QA and Production** 


1. Measuring Angles
1. Number Chart
1. Place Value In Numbers
1. MCQ - General
1. Comparing Angles
1. Horizontal Operations with Place Value Models
1. Vertical Operations with Place Value Models
1. Comparing Numbers
1. Place Value Bundles
1. Comparing Size
1. Counting Objects
1. Comparing Quantities
1. Place Value Models - Learn
1. Text Question, Text Options (Vertical)
1. Text + Image Question, Text or Image Options
1. Counting with Place Value Models - 1
1. Counting with Place Value Models - 2
1. Image Question, Image or Audio Option
1. Mcq long text
1. Sequencing
1. TEXT AND IMAGE MATCHING (HORIZONTAL)
1. Text and Image Matching (Vertical)
1. Reordering Letters & Numbers
1. Sorting Template
1. Reordering Words
1. Operations with images
1. Fill in the Blanks (with Image) - Word Answers
1. Vertical Operations
1. Division
1. Addition/Subtraction (with place value markers)
1. Addition/Subtraction
1. Multiplication (with parametrization)
1. Fill in the Blank - Number Answers
1. Multiplication
1. Sudoku
1. Multiple Blanks
1. Division
1. Vertical Operations
1. Fill in the Blank (sentence) - Number Answers
1. Custom Keyboard



 **How to debug templates in browser** 


* Clone the content-player([https://github.com/project-sunbird/sunbird-content-player](https://github.com/project-sunbird/sunbird-content-player)) repo of sunbird.
* Inside content-player → player → public → fixture-stories, Add your template folder containing (index.ecml, assets etc)
* Inside content-player → player → app-data → fixture-content-list.json, Add the below object structure to the json object result → contnet

                    {

                         "identifier": "template-name",

                         "mimeType": "application/vnd.ekstep.ecml-archive",

                         "localData": {

                                    "questionnaire": null,

                                     "appIcon": "fixture-stories/template_folder_name/logo.png",

                                     "subject": "literacy_v2",

                                     "description": "epub - Beyond Good and Evil",

                                     "name": "Custom Eval",

                                     "downloadUrl": "",

                                     "checksum": null,

                                     "loadingMessage": "Without requirements or design, programming is the art of adding bugs to an empty text file. ...",

                                     "concepts": \[{

                                                     "identifier": "LO1",

                                                     "name": "Receptive Vocabulary",

                                                     "objectType": "Concept"

                                        }],

                                     "identifier": "org.ekstep.customeval",

                                     "grayScaleAppIcon": null,

                                     "pkgVersion": 1

                          },

                         "isAvailable": true,

                         "path": "fixture-stories/custom_eval"

              },


* In the browser, click on the template logo you added for the template, the player will show the template, If the ECML is valid.
* Inside content-player → player, Open command prompt and type "node app.js" and press enter.
* In the browser type "localhost:3000".



 **How to create templates** 


* Create a folder with the template name. The template folder structure should contain

    
    * assets
    * images.png

    
    * widgets
    * css
    * index.css

    
    * js
    * index.js

    

    
    * items
    * assessment.json

    
    * index.ecml

    




*  **Assets**  folder contains images required for the template
*  **Widgets**  folder contains additional js and css required for the template
*  **Items**  folder contains assessment.json file which is used by the template
*  **index.ecml**  contains the ECML for the template. The basic structure of the template is 
    * <theme id="theme" startStage="splash" ver="0.2">

    <manifest>

                <media id="id" src="image.png" type="image"/>

    </manifest>

    <stage id="baseStage" preload="true">

        <image asset="image"/>

    </stage>

    <controller id="assessment" name="assessment" type="items"/>

    <template id="tempalate_name"></template>

<stage h="100" id="splash" iterate="assessment" var="item" w="100" x="0" y="0" preload="true">

           <param name="next" value="stage1"/>

       <g h="88" w="76" x="12" y="0">

                <embed template="item" var-item="item"/>

           </g>

    </stage>

    <stage h="100" id="stage1" w="100" x="0" y="0" preload="true">

           <param name="next" value="stage2"/>

           <param name="previous" value="splash"/>

           <image assest="image">

    </stage>

    <stage h="100" id="stage2" w="100" x="0" y="0" preload="true">

    <param name="previous" value="stage1"/>

           <image assest="image">

    </stage>

</theme>

    
*  **Tags used in ECML** 
    * theme -  Which is the entry point of the ecml. It should specify the id as theme and the stage which is to be rendered first.
    * manifest - it contains the media tags of medias(images, audio), js and css files used inside the template
    * media - it is used to include the medias(images, audio), js and css files used inside the template
    * stage - this tag specifies each screen inside the renderer. One can add multiple stages. The start stage should be "splash" and should be included in the theme tag. If you want to include the json add attribute iterate and var = item
    * embed - Embed tag is used to embed the template inside the stage
    * param - name attribute of param can be next, previous to specify the navigation to the next and previous stages.
    * controller - this tag is used to include the json file inside the items folder. specify the json file name as id and name attribute.
    * template - contains unique id for the template and the tag contains various tags which specify the UI for the template.

    
*  **assessment.json** 
    * For  **MCQ** 
    * {

    "identifier": "template_name",

    "title": "template_name",

    "total_items": 1,

    "shuffle": false,

    "max_score": 1,

    "subject": "LIT",

    "item_sets": \[{

             "id": "set_1",

             "count": 1

    }],

    "items": {

             "set_1": \[{

             "identifier": "protractor.que1",

             "qid": "protractor.que1",

             "type": "MCQ",

              "template_id": "template_name",

              "template": "template_name",

              "title": "Question text here",

              "question_audio": "",

              "question": "Question_title",

              "model" : {

                        "angleRange":"0-180" // for example, and it can be anything depands on the model

              },

             "question_image": "angle_img",

             "options": \[{

                    "value": {

                          "type": "mixed",

                          "text": "120",

                          "audio": "",

                          "image": "",

                          "asset": ""

                    }

             }, {

             "value": {

                         "type": "mixed",

                         "text": "180",

                          "audio": "",

                          "image": "",

                          "asset": ""

                         }

             },{

            "value": {

                          "type": "mixed",

                          "text": "75",

                         "audio": "",

                         "image": "",

                         "asset": ""

                     },

                     "answer": true

              }]

          }

    }

    
    * For  **FTB** 
    * {

    "identifier": "template_name",

    "title": "template_name",

    "total_items": 1,

    "shuffle": false,

    "max_score": 1,

    "subject": "LIT",

    "item_sets": \[{

             "id": "set_1",

             "count": 1

    }],

    "items": {

             "set_1": \[{

             "identifier": "protractor.que1",

             "qid": "protractor.que1",

             "type": "MCQ",

              "template_id": "template_name",

              "template": "template_name",

              "title": "Question text here",

              "question_audio": "",

              "question": "Question_title",

              "model: {

                    "keys": "A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z"

              },

             "answer":  {

                    "ans1": {

                             "value": "जजज",

                             "score": 1

                     }

                }

          }

    }

    
    * For  **MTF** 
    * {

    "identifier": "template_name",

    "title": "template_name",

    "total_items": 1,

    "shuffle": false,

    "max_score": 1,

    "subject": "LIT",

    "item_sets": \[{

             "id": "set_1",

             "count": 1

    }],

    "items": {

             "set_1": \[{

             "identifier": "protractor.que1",

             "qid": "protractor.que1",

             "type": "MCQ",

              "template_id": "template_name",

              "template": "template_name",

              "title": "Question text here",

              "question_audio": "",

              "question": "Question_title",

              "model" : {

                        "angleRange":"0-180" // for example, and it can be anything depands on the model

              },

             "question_image": "angle_img",

            "lhs_options": \[{

                 "value": { "type": "mixed", "audio": "", "image": "home", "text": "" },

                 "index": 0

               }, {

                  "value": { "type": "mixed", "audio": "", "image": "home", "text": "" },

                  "index": 1

              }, {

                   "value": { "type": "mixed", "audio": "", "image": "", "text": "3" },

                   "index": 2

              }, {

                 "value": { "type": "mixed", "audio": "", "image": "", "text": "4" },

                 "index": 3

             }, {

                "value": { "type": "mixed", "audio": "", "image": "", "text": "5" },

                 "index": 4

             }, {

                "value": { "type": "mixed", "audio": "", "image": "", "text": "6" },

                "index": 5

      }],

    "rhs_options": \[{

              "value": { "type": "mixed", "audio": "", "image": "home", "text": "" },

               "answer": 0

          }, {

               "value": { "type": "mixed", "audio": "", "image": "", "text": "the" },

               "answer": 1

         }, {

              "value": { "type": "mixed", "audio": "", "image": "home", "text": "" },

              "answer": 2

        } ,{

              "value": { "type": "mixed", "audio": "", "image": "", "text": "the" },

              "answer": 3

        }, {

              "value": { "type": "mixed", "audio": "", "image": "", "text": "school" },

              "answer": 4

        }, {

             "value": { "type": "mixed", "audio": "", "image": "", "text": "team." },

            "answer": 5

        }],

       }

    }

    

    

 **Steps to upload templates in Ekstep portal** 


1. Go inside the template folder and create a zip of the template folder.
1. Login to [dev.ekstep.in](http://dev.ekstep.in) or [qa.ekstep.in](http://qa.ekstep.in)
1. Click on "Create new lesson" button
1. Select "Upload a file".
1. Fill all the required fields
1. Select the  **Content Type ** as "template"
1. Select the Template Type as "MCQ" or "FTB" or "MTF"
1. Enter the template name as same as template id in the ECML.
1. Upload the .zip file of the template.
1. Then save the template and send for review.
1. Once it is reviewed and published by other user your template will appear in the question bank.

 **Steps to create the lesson by adding the questions** 


1. Login to [dev.ekstep.in](http://dev.ekstep.in) or [qa.ekstep.in](http://qa.ekstep.in)
1. Click on "Create new lesson" button
1. Select "Create new lesson".
1. Fill all the required fields
1. Click on launch editor
1. Click on "Add question set" plugin from the core plugins bar
1. Select any questions from the list or apply filter (or) search to select the required question
1. Provide question title, Total marks and how many number of questions to be displayed, and the toggle button to show immediate feedback and the shuffle questions
1. Then click on "add Question set" will add the question set to the stage.
1. Then click on "preview to start the assessment.
1. Click on dowload icon to download it to the mobile and an email will be send to the email id.
1. Click on the button to play the lesson inside your Genie app

 **Other details about templates** 

[https://docs.google.com/spreadsheets/d/1fQ8ekSVjHG-QHTCffMa7K56WWIAXyGKnAWRSX7VgpdQ/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1fQ8ekSVjHG-QHTCffMa7K56WWIAXyGKnAWRSX7VgpdQ/edit?usp=sharing)

[https://docs.google.com/spreadsheets/d/1LvqQzHfhi4eNDl4LtBUJCqCfYBF71NwHYHO2Ko1B45k/edit#gid=1994775373](https://docs.google.com/spreadsheets/d/1LvqQzHfhi4eNDl4LtBUJCqCfYBF71NwHYHO2Ko1B45k/edit#gid=1994775373)

 **ECML Reference** 

[https://github.com/ekstep/Common-Design/wiki/ECML-Home](https://github.com/ekstep/Common-Design/wiki/ECML-Home)

[https://github.com/ekstep/Common-Design/wiki/Item-Templates-V1](https://github.com/ekstep/Common-Design/wiki/Item-Templates-V1).










## Related articles
Related articles appear here based on the labels you select. Click to edit the macro and add or change labels.

false5com.atlassian.confluence.content.render.xhtml.model.resource.identifiers.SpaceResourceIdentifier@4b0a743falsemodifiedtruepagelabel = "kb-how-to-article" and type = "page" and space = "SBDES"kb-how-to-article



true



|  | 
|  --- | 
|  | 









*****

[[category.storage-team]] 
[[category.confluence]] 
