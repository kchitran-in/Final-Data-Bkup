

|  **Title**  | Dashlet Page Wise Configuration. | 
|  **Problem Statement**  | Ability to inject dashlets widgets into any page via configuration. | 



Solution is divided into 3 phases :-


1. Create Configuration for the Dashlets < **CREATION** >


1. Linking the page id to the Dashlets Configuration < **LINKING** >


1. Rendering the Dashlets < **RENDERING** >




## Proposed Solutions 

### CREATION PHASE

1. This phase deals in creation of the dashlets configuration.


1. Use the Report Service API’s to store the configuration just like we’re doing for the Admin Reports.


1. In order to prevent these dashlets widget to show in admin Dashboard list page we’ll make use of two cols -


    1.  **report_type** : 'dashlet'


    1.  **type** : ‘private'



    
1.  Following are the PROS of using the report service API’s for storing dashlets configuration.


    1. Parameterization support ($slug, $board, $state and $channel).


    1. Tags Support


    1. Life Cycle support - Draft, Live and Retired


    1. Can also be clubbed with Summaries API’s.


    1. Authorized Roles field to target specific role to access the Dashboard.


    1. Link to Documentation - [http://docs.sunbird.org/latest/apis/reports/](http://docs.sunbird.org/latest/apis/reports/)



    
1. Sample Create API payload


```json
{
    "request": {
        "report": {
            "title": "title of the report",
            "description": "Description of the report",
            "authorizedroles": [
                "ORG_ADMIN"
            ],
            "status": "draft",
            "type": "private",
            "report_type": "dashlet",
            "parameters": [],
            "createdby": "ravinder",
            "reportconfig": {
                "dataSource": [
                    {
                        "id": "up_data",
                        "path": "/reports/fetch/$slug/xyz.json"
                    }
                ],
                "tables": [],
                "charts": [],
                "dashlets": [{type, data, config}],
                "reportLevelDataSourceId": "first"
            },
            "slug": "sunbird",
            "reportgenerateddate": "2020-04-12T00:00:00.000Z",
            "reportduration": {
                "enddate": "Thu May 7 2020",
                "startdate": "Thu May 7 2020"
            },
            "tags": [
                "Dashboard",
                "Engagement"
            ],
            "updatefrequency": "DAILY"
        }
    }
}
```




Another Solution is to store whole dashlet configuration inside form only.

 **LINKING PHASE** 


1. This phase deals with linking a certain page to an existing report configuration.


1. We’ll be using a form  to establish a link between a page and Report .


1. Additional meta-data can also be defined at this stage.


1. Sample config


```
{
    "request": {
        "type": "dashboard",
        "subType": "dashlet",
        "action": "link",
        "data": {
            "templateName": "defaultTemplate",
            "action": "link",
            "fields": [
                {
                    "pageId": "profile",
                    "configuration": {
                        "reportId": "51bcad49-e7b5-41b8-8171-163da1af6c52",
                        ...additionalMetadataIfRequired
                    }
                }
            ]
        }
    }
}
```




 **additionalMeta could be** 

slug - if configuration is enabled for only specific slug

component - to load an existing component <can vary as per the platform>

redirectRoute - redirect to already existing route

Other vars….

 **Question** :-

Only single form should exist with all the links or individual form for each page id.

 **RENDERING PHASE** Solution 1 - Using a structural Directive![](images/storage/Untitled%20Diagram.png)
1. We’ll attach the directive to an element (For example button) in any part of the page.


1. If it’s a button it will load a certain component and will get the context object from the report service using the page id of the page where it is attached


1. Element → Form Service → Report Service → Template Component


1. Redirection logic or which component to render can be defined at the form level



![](images/storage/Screenshot%202021-05-25%20at%2012.46.01%20PM.png)

 **Pros**  :-

Directive can be implemented in such a way that a specific dashlet can be injected at the specified position also.

 **Con**  :- 

Whenever a new dashboard is required in certain a minor code change is required for attaching the directive to an element.

Solution 2 - Showing Additional Dashboard tab in the main menu/ any common header element for all pages.There will be an additional tab in the main menu. For instance Dashboard

It’ll look for the router change events and will asynchronously load the configuration using the page id of the loaded route.

We can configure it to redirect to any component/template using menubar form and pass the required context.<can vary as per the platform>

If no report is configured for that page button won’t appear.

![](images/storage/Screenshot%202021-05-25%20at%2012.49.46%20PM.png)Pros: 

no code changes , everything automated using form service and report service

Cons :-

Unneccesary API calls for newly loaded route, though we can cache the response of the already loaded routes.

Might not be very user friendly experience  & can be misguiding to the user.



 **** We also need to standarise the context object which will be passed to the template pages in order to create multiple templates**** 

CONS

Two changes required in each environment- form creation/update and report creation/update.

Resources : 

[http://docs.sunbird.org/latest/apis/reports/](http://docs.sunbird.org/latest/apis/reports/)

[[Dashlets Design Doc|Dashlets-Design-Doc]]





*****

[[category.storage-team]] 
[[category.confluence]] 
