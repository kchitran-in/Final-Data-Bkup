
# Objective
Achieve multi-lingual support in inQuiry


# Fields that needs multilingual support

* body


* answer


* instructions


* feedback


* hints




# User Flow

## Scenario 1 : Create and consume questions & question set in any language

1. Creator / Editor


    1. A dropdown will be present at the beginning of Question or Question set creation.


    1. A default list of languages will be available in the drop down. Additional languages to be displayed in the dropdown list can be configured.


    1. The language will be pre-selected as English by default.


    1. The user will be able to choose any language from the dropdown menu.


    1. Allow free-text ie. the user should be able to type a language that is not in the drop down



    
    1. Upon selecting a language, the corresponding language code is stored.


    1. Option 1 :


    1. There will be a drop-down across each of the fields, for which multiple languages are supported.


    1. The language selected for the first field, will be retained as the default for the rest of the fields, unless selected otherwise. 


    1. Eg. While creating a question set, if the creator first chooses the language for the ‘instructions’ field as `Hindi`, the rest of the fields - ‘body’, ‘options’ etc, should automatically have ‘Hindi’ as default language.



    

    
    1. Option 2 :


    1. There will be only one drop down where the language is selected, and will be applied for all fields within a question/question set.



    
    1. Option 3:


    1. Dropdown for language selection will be present at 3 places :


    1. At Question Set Root node, where it will cover the following fields :


    1. Name (Need to add QuML spec)


    1. Instructions



    
    1. At each Section, where it will cover the following fields :


    1. Instruction



    
    1. At each Question, where it will cover the following fields:


    1. Question body


    1. Options


    1. Solution


    1. Feedback


    1. Hint

    



    

    

    
    1. Creator is able to type or copy paste in any language (question body/instruction/options..).


    1. Validate if the entered language is same as the selected language.


    1. If the entered language is different from the selected language, an error message will be displayed. This is not going to be a validation, it will just be an alert.



    
1. Player


    1.   A dropdown option will be present at the beginning of the Question or Question set, that is selected for playing. 


    1. For eg : Alongside the button for editing the player configurations, add another dropdown for the language selection.



    
    1. The drop down will be populated based on the languages that are available in the question set or question


    1. Eg 1 : If a question set contains questions that are in English and in Hindi, the dropdown will show English & Hindi only.



    
    1. The user will be able to choose any language based on the available languages in the dropdown.


    1. No support for free-text ie the user can only choose from the existing options and cannot enter any type in a new entry



    
    1. At the question set level


    1. The player will only display the questions in the question set, which are present in the selected language.


    1. For eg: 


    1. There are 10 questions in a question set. Questions 1,2 & 3 have only English data (body) and 


    1. questions 4,5,6 & 7 have entries in Hindi and English i.e. the same question is present in both the languages.


    1.  Questions 8, 9 & 10 have entries only in Hindi.


    1. Upon selecting Hindi from the dropdown, the question set will contain questions 4,5,6,7,8,9,10



    

    

    
    1. At each question level


    1. A dropdown option will be present at the beginning (could be near the progress bar info legend)


    1. The dropdown will display only the languages in which the question body is present.


    1. Upon selecting a language from the dropdown, the question will be displayed in the selected language.


    1. By default the language will be English


    1. If the options are not present in the selected language, display the options from the default language.


    1.  _Selecting value on the question drop-down could override the question set drop-down?_ 



    

    

    

    


## Scenario 2 : Create a Question / Question Set in multiple languages

1. Creator


    1.  User should be able to choose the language(s) from a dropdown and create a question in that language


    1. Creator will be able to select maximum five languages



    
    1. Dropdown for language selection will be present at 3 places :


    1. At Question Set Root node, where it will cover the following fields :


    1. Name (not multi-lingual right now)


    1. Instructions



    
    1. At each Section, where it will cover the following fields :


    1. Instruction



    
    1. At each Question, where it will cover the following fields:


    1. Question body


    1. Options


    1. Solution


    1. Feedback


    1. Hint



    

    
    1. Incase the user selects a non-english language, the Google Input Tool prompt pops-up in the selected language.


    1. Incase of MCQ (or other interactive questions), the creator can enter the options in the selected language.


    1. If the language of the entered text is different from the selected language, an error message will be displayed. This is not going to be a validation, it will just be an alert.


    1. Corresponding text boxes for entering questions are displayed for all the selected languages


    1. A button can be displayed which can display the translated text on-demand.


    1. The text box will have the translation of the original text (primary language) in the selected language, which can be edited by the creator.



    
    1. User will be able to copy the options from any of the previously entered set of options (for eg. in-case of MCQ with options which are numeric values)


    1. User could enter the options for the corresponding language



    
    1. Similarly for instructions and other fields

    



    
1. Player


    1. A dropdown will be present at the beginning of the Question or Question set, that is selected for playing.


    1. The user will be able to choose any language based on the available languages in the dropdown.


    1. The language in the dropdown will be populated based on the  languages in which the question / question set is available.



    
    1. The drop down can have multi-select options ie the user will be able to select multiple languages


    1. Player will be able to select maximum of two languages.



    
    1. The question / question set will be rendered in the selected language/languages


    1. The question level language selection will override the question set level language selection ie, the user will be able to view the question is any language that is available in the dropdown



    
    1. \[Question] What will happen when the questions/option/etc has a media file (eg. image) in all the different language entries and while rendering more than one language, the same media will be shown twice? 



    



Reference :

![](images/storage/Screenshot%202023-02-23%20at%2011.31.55%20AM.png)![](images/storage/Screenshot%202023-02-23%20at%2011.47.55%20AM.png)
## Scenario 3 : The Editor and Player should support rendering in any language



1. Creator


    1. Will be able to choose any language based on their preference, before entering the Editor


    1. The form on the editor will be loaded in the selected language. Eg : labels, Info etc


    1. Assumption : The entries for the labels and texts for various languages is already stored.


    1. Support scenario 1 & scenario 2



    

    
1. Player


    1. Will be able to choose any language based on their preference, before entering the Editor/ Player


    1. Assumption : The dropdown contains only the languages for which is entry to required fields \[TBD]



    
    1. All the questions, questions sets in the selected language will be loaded.


    1. Select a question of question set to play


    1. Assumption : The entries for the items under menu etc (TBD) are entered in the selected language


    1. Support scenario 1 & scenario 2



    

    





*****

[[category.storage-team]] 
[[category.confluence]] 
