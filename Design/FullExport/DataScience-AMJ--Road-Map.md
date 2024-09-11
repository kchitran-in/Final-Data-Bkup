

 **1. Use Case: Profanity Filter** 

 **Problem** : Detect profanity words and flag such Content.

RoadMap:


1. Feasibility Track (effort: one week)
    1. [review](https://github.com/vzhou842/profanity-check) existing methods: look-up based and model-based
    1. create positive and negative test data
    1. seed test data from public data sets: [cmu](https://www.cs.cmu.edu/~biglou/resources/), [kaggle](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data) and other sources, [word list](https://github.com/snguyenthanh/better_profanity/blob/master/better_profanity/profanity_wordlist.txt), [word list](https://github.com/ben174/profanity/blob/master/profanity/data/wordlist.txt): 
    1. create own test data

    
    1. run [profanity](https://github.com/ben174/profanity), and [better_profanity](https://github.com/snguyenthanh/better_profanity/blob/master/better_profanity/profanity_wordlist.txt), [profanity_check](https://github.com/vzhou842/profanity-check)
    1. ensemble them
    1. evaluate the performance on individual and ensemble approaches on test data
    1. design document

    
1. Production Track (effort: one week)
    1. Design Review and Documentation (telemetry, and data models for capturing feedback)
    1. Write test cases for positive and negative examples 
    1. Add profanity flagging tag to existing Auto Tagging Module
    1. And possibly write an "alert event" if a profanity tag turn positive

    

Rest of the flow is same as Productionizing Auto Tagging

Task Dependency Graph

1 → 2

(1a | 1b) → 1c → 1d → 1d → 1e → 1f 

2a → 2b → 2c → 2d

External Dependencies


1. DS VM 

DS Resources:


1. Tech Manager 
1. One DS developer  (can be split between two)
1. Solution Manager: Mohit

 **TBD** : Align it with AMJ Sprint Cycles

 **2. Use Case: Content Reuse** 

 **Problem** : [Story](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/overview)

RoadMap:

 **Experiment Track** 


1. Data Sourcing (effort: one week)
    1. Pick Maths, NCERT Grade 10 Textbook (which is the basis for NCF or NCERT framework in the platform), convert it to JSON data using
    1. Google ocr-uri
    1. pypdf2

    
    1. Filter and prepare MVC test data

    
1. Taxonomy Enrichment (effort: one week)
    1. Extract reference Taxonomy
    1. Take the reference framework and map the taxonomy pointers to the corresponding section in the digital twin of the textbook

    
1. Index this data in ES (effort: one week)
    1. Index enriched taxonomy
    1. Get the pointer text object, given taxonomy pointer, 
    1. Write ES Query 

    
1. Test and Iterate (two weeks)
    1. retrieval performance, and benchmark against baseline (existing) and iterate

    
1. If performance is acceptable
    1. Design Review
    1. Prod Roadmapping

    

Task Dependency Graph

(1a | 1b) → 2 → 3 → 4 → 5 



External Dependencies


1. DS VM



DS Resources:


1. Tech Manager
1. Two DS developers
1. Solution Manager: Mohit

 **TBD** : Align it with AMJ Sprint Cycles



 **3. (Potential) Use Case: EQB Curation Smart Tagging** 

 **Context** : [Context and Architecture](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/1017053393/EQB+Architecture)

Problem: Figure out a way to assert quality of the question bank, and use those Quality tags to rank the questions

 **Experiment Track: ** 


1. Manual Rules
    1. Check if Marking Schema (meant for a teacher) can be graduated to an Answer (that can be shown to a student)

    
1. Learn Model based Rules (variable depending on scope)

    
    1. NLP + Image Processing to detect if a question/answer has special symbols like
    1. polynomial
    1. matrix
    1. shapes ...

    

    
1. Load Rules (effort: 2 days)
    1. Code/Load the rules/models

    
1. Apply the Rubrics and Summarize the results (effort: 2 days)
1. Populate this data back to Google Sheets (as a means of sharing data with EQB team)
1. Evaluate
    1. Pick a sample and see if rules are holding well against the data
    1. Validate the generated tag by EQB team. 
    1. Summarize the results

    
1. If results are acceptable, 
    1. Design Review for Prod

    

DS Resources:


1. Tech Manager 
1. One/Two DS developers depending on availability and urgency
1. Solution Manager: Suren

Task Dependency Graph

(1 | 2) → 3 → 4 → 5 → 6 → 7

External Dependencies


1. Rubric from EQB team
1. Bandwidth from EQB team for providing validation inputs
1. Making the Question and Marking Scheme available for easy view by Validation team
1. DS VM



 **TBD** : Align it with AMJ Sprint Cycles

 **4. Use Case: Taxonomy Alignment** 

 **Context** : [Context and Architecture](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/1017053393/EQB+Architecture)

Problem: A Textbook will be created that uses a Framework (Taxonomy) available in the platform. And against the chapter, topic of that Textbook, question-answer packets have to be created. However, the Taxonomy terms available on the Question Bank may not necessarily align completely with the Taxonomy on the platform. How do we align them?

 **Experiment Track: ** 


1. Manual Mapping
    1. Extract Taxonomy Terms from Question Bank
    1. Done using scripts. 

    
    1. Select a corresponding Framework, for a given, board, subject, grade, medium,

    
    1. All existing Frameworks were extracted and kept in an Spreadsheet

    
    1. Manually align the terms
    1. Once the terms are mapped, every Question can be tagged to Framework on the platform

    

    
1. Mapping via Search
    1. Take data at the end of previous step as ground truth
    1. Use Enriched Taxonomy from Content Reuse Use Case (see above)
    1. Enrich Question Data (extract Text data from the Questions, do Smart Tagging)
    1. Treat Mapping as a Search Problem: Given a Question, which Taxonomy Term it should be mapped to
    1. Validate based on ground truth above

    

 **Production Track: ** 


1. Proposal and Review
1. Define the data models
1. Ingest the Platform taxonomy terms or have look up (from at step 3 above)



DS Resources:


1. Tech Manager 
1. One/Two DS developers depending on availability and urgency
1. Solution Manager: Suren

Task Dependency Graph

(1 | 2) → 3 → 4 → 5 → 6 → 7

External Dependencies


1. Rubric from EQB team
1. Bandwidth from EQB team for providing validation inputs
1. Making the Question and Marking Scheme available for easy view by Validation team
1. DS VM



 **TBD** : Align it with AMJ Sprint Cycles



 **5. (Explore) Use Cases: Content Reuse and EQB Search** 

 **Problem** : [Content Reuse](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/overview) and [EQB](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/1017053393/EQB+Architecture) are two sides of the same coin. They both are search problems at their core. We did a quick and dirty POC [here](https://project-sunbird.atlassian.net/browse/SC-874)  to try Deep Learning models. The results were very encouraging but we have to cautious as the model is probably overfit. We have not done thorough evaluation.



 **Experiment Track A** 


1. Validate the results from previous spike, and see if they are generalizing well.

 **Experiment Track B** 


1. Data Sourcing (effort: one week)
    1. prepare query, document data pairs (done)
    1. prepare query, document data pairs based on Taxonomy Enrichment words, and Enriched Content Model data (use normalized words only withtout lemming and stemming)

    
1. Model Sourcing (effort: 3 days)
    1. Download ELMO, Universal Sentence Encoders (from tensorhub), and work with them

    
1. Update the architecture (2 days)
    1. Instead of using bilstm, use ConvNets as query documents are bag of words and not really sentences
    1. Use Google UST as phrase, sentences representations, and learn a simple classifier (replace bi-lstms with a ffn)

    
1. Model Search (two weeks)
    1. use DNN with single dense layer as baseline 
    1. Use AutoML or NAS or Ray for automatic architecture search

    
1. Test and Iterate (two weeks)
    1. retrieval performance, and benchmark against baseline (existing) and iterate

    
1. If performance is acceptable
    1. Design Review
    1. Prod Roadmapping

    

Task Dependency Graph

A → B

(B1a | B1b) →  B2 → (B3a | B3b ) → (B4a | B4b) → B5 → B6 

External Dependencies


1. DS VM

DS Resources:


1. Tech Manager
1. Two DS developers
1. Solution Manager: Mohit

 **TBD** : Align it with AMJ Sprint Cycles



*****

[[category.storage-team]] 
[[category.confluence]] 
