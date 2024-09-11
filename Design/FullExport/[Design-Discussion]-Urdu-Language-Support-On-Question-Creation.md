
# Background
  Current Implementation of Question Creation in Question Unit Plugins provides ability add question details through CK-Editor.





Click here to See The Current Implementation![](images/storage/Quesiton%20Creation.png)


# 

Design Requirements [SB-6814 System JIRA](https:///browse/SB-6814)
  1. Language selection to be moved out of Text and to the top of each question type.

  2. Placeholder message for Question text: Select language for this question

  3. On selecting Urdu, reduce default font size by 2

  4. Cursor movement to be made in accordance with RTL

  5. For custom keyboard in FTB, Urdu selection should result in changes accordingly

  6. Question details (metadata) will be stored as - is. Medium = Urdu will allow consumption clients (Question search) to right align if required.


# Problem Statement

## Statement 1 : The Language List is not defined in the requirements
Refer the Design Requirement  1 and 2

What languages should be listed out is not defined in the requirement.

To understand item 1 and 2 refer the below Image.![](images/storage/Language%20Select.png)




## Statement 2 : In Question Bank filter there is no Medium field
As per Design requirement 6, When a user selected Medium in Urdu in Question Bank it is required to make the search box to support Right to Left input. But there is no Medium in Filter in Question Bank.



Click Here to see Design Requirement 6![](images/storage/Filter_Questionbank.png)


## Key Design Issue
1. All the language List 

2. No Medium field in Question Bank Filter













*****

[[category.storage-team]] 
[[category.confluence]] 
