
## Introduction
As a Sourcing Org Contributor when I try to Add from Library, I will get the most relevant content.  _Most relevant content_  is defined based on the match between My textbook and Textbooks in Library.


1. As a Sourcing Org Contributor, I will get two options against each chapter (unit) in the textbook.


    1. (New) Add from Library


    1. Add New



    
1. (New) As a Sourcing Org Contributor, I will be able to Add from Library by  _Exploring_  and by viewing  _Suggestions_ .


1. Add from Library will have two ways: “Explore” (or “Library”) and “Suggestions” (or “Recommended”).


1. (New) As a Sourcing Org Contributor, I will be able to Explore pre-filtered set of textbooks, chapter (topic) wise.


1. (New) As a Sourcing Org Contributor, I will be able to Preview selected content quickly.


1. (New) As a Sourcing Org Contributor, I will Add Selected Content to any chapter (unit) in My Textbook.


1. (New) As a Sourcing Org Contributor, I will be able to view Suggested content, Preview, and Add to the Selected chapter (unit) in My Textbook.




## Problem Statement

1. Explore: When a textbook- TOC is uploaded, for each chapter/ topic, show similar chapter/ topic in other textbook and the content linked to those topics


    1. Based on the filter


    1. Search for Chapter/topics in other textbooks based on textbook  nodes as query



    
1. Suggest: When a textbook- TOC is uploaded, for each chapter/ topic, show  5 MVC Content that can be linked to each chapter/topic


    1. Search for enriched MVC Content based on textbook nodes as query


    1. Search for enriched MVC Content embeddings based on textbook nodes query as embedding



    


##  **MVC Content**  

1. Create a standard excel format for MVC Content


    1. State


    1. Type   


    1. Board \[Important]


    1. Grade \[Important] 


    1. Subject \[Important] 


    1. Medium \[Important] 


    1. Textbook Name \[Important]


    1. Chapter No. 


    1. Chapter Name (Level 1) \[Important]


    1. Chapter Concept Name (Level 1) \[Important]


    1. Topic Name (Level 2) \[Important]


    1. Topic Concept Name (Level 2) \[Important]


    1. Sub Topic Name (Level 3) \[Important]


    1. Sub Topic Concept Name (Level 3) \[Important]


    1. Source \[Important]


    1. Content URL \[Important]



    
1. Existing excel data needs to be preprocessed so that standard structure can be achieved.


1. Please note that one Content URL can have multiple entries.


1. If the Content URL is multiple then we need to merge that in the Excel. There should be only one row per content URL. 


1. There are many cases where the Content URL is not valid so we will have to ignore those entries.


1. Columns Field Values mentioned in the excel will be considered as final and rest of the data will be read from Diksha Content Read API




## Design
![](images/storage/Screenshot%202020-06-23%20at%209.57.56%20AM.png)


* Using Elasticsearch 7.4 to make use of vector indexing for semantic search.


* Using strict mapping for better performance.



 **Implementation Flow** 
1. Develop a script which will read the data from google sheets and merge the data into one CSV.


1. mvc-content-create API should handle


    1. Excel (xls)


    1. JSON



    
1. Develop a new  **mvc-content-create API**  which will accept the field and values defined in the excel.


    1. Check whether the Content URL is valid or not.


    1. Basis the Content URL, extract Content ID and other properties of the content using Content Read API of Diksha.


    1. Board, Grade, Subject and Medium data will be picked from the excel and not from the Diksha Content and pass the values to Auto Create Event.


    1. Trigger Auto Create Job with some extra parameters in event JSON


    1. textbookname


    1. level1name


    1. level1concept


    1. level2name


    1. level2concept


    1. level3name


    1. level3concept


    1. label (MVC)


    1. source \[Diksha, iDream, ToonMasti etc...]


    1. sourceurl



    
    1. Auto Create JOB internally calls the Content Create API of Vidyadaan and passes the appropriate request.


    1. Auto Create JOB internally trigger Publish Pipeline of Vidyadaan.



    
1. Content Create API of Vidyadaan Changes


    1. Change content definition of Neo4J to handle below mentioned additional columns


    1. textbookname


    1. level1name


    1. level1concept


    1. level2name


    1. level2concept


    1. level3name


    1. level3concept


    1. label (MVC)


    1. source \[Diksha, iDream, ToonMasti etc...]


    1. sourceurl



    
    1. Content Create API will insert this data in Neo4J



    
1. Publish Pipeline Changes


    1. Publish Pipeline will insert data in vidyadaan content ES with above additional columns.


    1. if the label parameter exists and its value is MVC, it triggers mvc-processor pipeline.


    1. We need to insert below mentioned values in MVC ES and Cassandra


    1. textbookname


    1. level1name


    1. level1concept


    1. level2name


    1. level2concept


    1. level3name


    1. level3concept


    1. label (MVC)


    1. source \[Diksha, iDream, ToonMasti etc...]


    1. sourceurl



    

    


### Elastic Search Index Structure: 
 **Name:**  mvc-content



|  **Property**  |  **Data Type**  |  **Tokenization**  |  **Group**  |  **Description**  | 
|  --- |  --- |  --- |  --- |  --- | 
| name | Text | Yes | core - metadata |  | 
| description | Text | Yes |  | 
| mimeType | Text | No |  | 
| contentType | Text | No |  | 
| resourceType | Text | No |  | 
| artifactUrl | Text | No |  | 
| streamingUrl | Text | No |  | 
| previewUrl | Text | No |  | 
| downloadUrl | Text | No |  | 
| framework | Text | No |  | 
| board | Text | Yes |  | 
| medium | Text | Yes |  | 
| subject | Text | Yes |  | 
| gradeLevel | Text | Yes |  | 
| keywords | Text | Yes |  | 
| source | Text | Yes | source - metadata | URI of the content. This is the public URI to access the source of the MVC. | 
| ml_level1Concepts | Text | Yes | ml - metadata |  | 
| ml_level2Concepts | Text | Yes |  | 
| ml_level3Concepts | Text | Yes |  | 
| ml_contentText | Text | Yes | Text extracted form the pdf, video or ecml Content  | 
| ml_keywords | Text | Yes |  | Keywords identified from ml_contentText | 
| ml_content_text_vector | Dense vector | No |  | Vector representation of ml_contentText and description using pertained ml model | 
| label | Text | Yes |  | Tags that represent the Content. ex: MVC | 




### Content-service 
We can use the existing code of Content Search API for MVC Search by following two approaches.


1. Create a new route of MVC reuse in the existing API. 


    1. Pros 


    1. All the existing utilities and dependencies can be reused. 


    1. Manageability becomes easy and both the Search API is part of one project.  



    
    1. Cons


    1. It could impact the performance, though it is very less.


    1. Deployment of Diksha will impact Vidyadaan application as well.


    1. ES version has to be same for both Diksha and Vidyadaan.



    

    
1. Create a new API for MVC reuse


    1. Pros


    1. No impact on existing Diksha Search Service


    1. No dependency on Deployment now, as both are separate services.


    1. Latest ES version can be used for Vidyadaan



    
    1. Cons


    1. Maintainability would be an issue both at Code and DB level.



    

    

![](images/storage/Screenshot%202020-06-23%20at%209.57.56%20AM.png)

 **API Spec:** 
1. Request:


    1. HTTP Verb: POST


    1. URL: "'[https://dock.sunbirded.org/api/mvc/v3/search'](#)["](https://dock.sunbirded.org/action/mvccomposite/v3/search%22)


    1. Header Parameters


    1. Content-Type: “application/json“


    1. Authorization: “Bearer <auth-token>“



    
    1. Request Parameters:


    1. mode: soft/hard


    1. filters


    1. softConstraints


    1. vector - search



    

    


```
{
  "request": {
    "mode": "explore",
    "filters": {
      "medium": [
        "Telegu"
      ],
      "gradeLevel": [
        "Class 4",
        "Class 5",
        "Class 6"
      ],
      "status": [
        "Live"
      ],
      "textbookName": [
        "Science"
      ],
      "level1Name": [
        "Sorting Materials Into Groups"
      ],
      "level1Concept": [
        "Materials"
      ],
      "level2Name": [
        "Objects Around Us"
      ],
      "level2Concept": [
        "Various Objects"
      ]
    }
  }
}
```

1. Response




```
{
  "id": "ekstep.mvc-composite-search.search",
  "ver": "1.0",
  "ts": "2020-05-21T22:23:43ZZ",
  "params": {
    "resmsgid": "c1658c85-e0a1-41ed-bd9a-72df223f505d",
    "msgid": null,
    "err": null,
    "status": "successful",
    "errmsg": null
  },
  "responseCode": "OK",
  "result": {
    "count": 3,
    "content": [
      {
        "organisation": [
          "Vidya2"
        ],
        "channel": "sunbird",
        "framework": "NCF",
        "board": "State(Tamil Nadu)",
        "subject": "English",
        "medium": [
          "Telegu"
        ],
        "gradeLevel": [
          "Class 4",
          "Class 5",
          "Class 6"
        ],
        "name": "15_April_ETB",
        "description": "Enter description for TextBook",
        "language": [
          "English"
        ],
        "appId": "dev.dock.portal",
        "contentEncoding": "gzip",
        "identifier": "do_113025640118272000173",
        "node_id": 5244,
        "nodeType": "DATA_NODE",
        "mimeType": "application/vnd.ekstep.content-collection",
        "resourceType": "Book",
        "contentType": [
          "TextBook"
        ],
        "objectType": "Content",
        "textbookName": [
          "Science"
        ],
        "level1Name": [
          "Sorting Materials Into Groups"
        ],
        "level1Concept": [
          "Materials"
        ],
        "level2Name": [
          "Objects Around Us"
        ],
        "level2Concept": [
          "Various Objects"
        ]
      }
    ]
  }
}
```



### ML Workbench api:
Request:


```
POST /daggit/submit
{
	"request":{
		"input":{
			"APP_HOME": "/daggit_home/content_reuse",
			"content":[{
				"subject": "Science",
				"downloadUrl": "https://ntpproductionall.blob.core.windows.net/ntp-content-production/ecar_files/do_312533255910883328118977/muulyvaan-yogdaankrtaa-10th-vijnyaan_1532071348607_do_312533255910883328118977_2.0.ecar",
				"language": ["English"],
				"mimeType": "application/vnd.ekstep.ecml-archive",
				"objectType": "Content",
				"gradeLevel": ["Class 10"],
				"artifactUrl": "https://ntpproductionall.blob.core.windows.net/ntp-content-production/content/do_312533255910883328118977/artifact/1529938853455_do_312533255910883328118977.zip",
				"contentType": "Resource",
				"identifier": "do_312533255910883328118977",
				"graph_id": "domain",
				"nodeType": "DATA_NODE",
				"node_id": 575061}, 
				 {...},...]
		},
		"job":"diksha_content_keyword_tagging"
	}
}
```
Response:


```
api_response = {
        "id": "daggit.api",
        "ver": "v1",
        "ts": "",
        "params": {
            "resmsgid": "null",
            "msgid": "",
            "err": "null",
            "status": "fail",
            "errmsg": "null"
        },
        "responseCode": "OK",
        "result": {
            "status": 200
        }
    }
```



### Text Vectorisation API:
Request:


```json
port:1729
endpoint: /ml/vector/search
{
	"request":{
		"text":["Class 11 English medium mathematics", "Today we will talk about Photosynthesis"],
		"language": "en",
		"model": "BERT",
		"params": {"dim": 768,"seq_len":25, ....} // optional. Default values configured based on the model
	}
}
```
Response:


```
{
    "id": "api.ml.vector",
    "ets": 1591603456223,
    "params": {
            "resmsgid": "null",
            "msgid": "",
            "err": "null",
            "status": "success",
            "errmsg": "null"
        },
    "result":{
        "action":"get_BERT_embedding",
        "vector": [[-0.34,1.2,.....],[0.5,1.8,.....]]         
    }
}
```
 **action = getContentVec** 


```
GET /ml/vector/contentText
{
	"request":{
		"text":["Class 11 English medium mathematics", "Today we will talk about Photosynthesis"],
		"language": "en",
		"model": "BERT",
		"params": {"dim": 768,"seq_len":25, ....} // optional. Default values configured based on the model
	}
}
```



```
{
    "eid": "MVC_JOB_PROCESSOR",
    "ets": 1591603456223,
    "mid": "LP.1591603456223.a5d1c6f0-a95e-11ea-b80d-b75468d19fe4",
    "actor": {
      "id": "UPDATE ML CONTENT TEXT VECTOR",
      "type": "System"
    },
    "context": {
      "pdata": {
        "ver": "1.0",
        "id": "org.ekstep.platform"
      },
      "channel": "01285019302823526477"
    },
    "object": {
      "ver": "1.0",
      "id": "do_113036318281465856163"
    },
    "edata":{
        "action": "update-ml-contenttextvector",
        "stage": 3,
        "ml_contentTextVector": [-0.34,1.2,.....]
    }
}
```



# MVC Content Create API
Request:


*  **To create MVC content using JSON** 




```json
endpoint: /v3/mvccontent/create
{
  "request": {
    "content": [
      {
        "board": "State(Tamil Nadu)",
        "subject": [
          "English"
        ],
        "medium": [
          "Telegu"
        ],
        "gradeLevel": [
          "Class 4",
          "Class 5",
          "Class 6"
        ],
        "textbookName": [
          "Science"
        ],
        "level1Name": [
          "Sorting Materials Into Groups"
        ],
        "level1Concept": [
          "Materials"
        ],
        "level2Name": [
          "Objects Around Us"
        ],
        "level2Concept": [
          "Various Objects"
        ],
        "source": [
          "Diksha 1",
          "TN 1.1"
        ],
        "sourceurl": ["https://diksha.gov.in/play/content/do_31283180221267968012331"]
      }
    ]
  }
}
```

*  **To create MVC content using Excel** 




```
curl --location --request POST '/v3/mvccontent/create' \
--form 'File=@{{LOCATION OF FILE}}/{{NAME OF FILE}}.xlsx'
```


Response:


```
{
    "id": ektep.mvc.content.create,
    "ver": "3.0",
    "ts": null,
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": null,
        "status": "successful",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {}
}
```

## MVC Processor Samza Job - Event JSON
 **Stage 1: This job will get triggered from the Publish pipeline, if the Label is “MVC“** 


```
{
    "eid": "MVC_JOB_PROCESSOR",
    "ets": 1591603456223,
    "mid": "LP.1591603456223.a5d1c6f0-a95e-11ea-b80d-b75468d19fe4",
    "actor": {
      "id": "UPDATE ES INDEX",
      "type": "System"
    },
    "context": {
      "pdata": {
        "ver": "1.0",
        "id": "org.ekstep.platform"
      },
      "channel": "01285019302823526477"
    },
    "object": {
      "ver": "1.0",
      "id": "do_113036318281465856163"
    },
    "eventData":{
        "identifier":"do_113036318281465856163",
        "action": "update-es-index",
        "stage": 1
    }
}
```
 **Stage 2: ML Keyword Extraction API will be triggering this event** 


```
{
    "eid": "MVC_JOB_PROCESSOR",
    "ets": 1591603456223,
    "mid": "LP.1591603456223.a5d1c6f0-a95e-11ea-b80d-b75468d19fe4",
    "actor": {
      "id": "UPDATE ML KEYWORDS",
      "type": "System"
    },
    "context": {
      "pdata": {
        "ver": "1.0",
        "id": "org.ekstep.platform"
      },
      "channel": "01285019302823526477"
    },
    "object": {
      "ver": "1.0",
      "id": "do_113036318281465856163"
    },
    "eventData":{
        "identifier":"do_113036318281465856163",
        "action": "update-ml-keywords",
        "stage": 2,
        "ml_Keywords":["maths", "addition", "add"],
        "ml_contentText":"This is the content text for addition of two numbers."
    }
}
```
 **Stage 3: ML Vectorization API will be triggering this event** 


```
{
    "eid": "MVC_JOB_PROCESSOR",
    "ets": 1591603456223,
    "mid": "LP.1591603456223.a5d1c6f0-a95e-11ea-b80d-b75468d19fe4",
    "actor": {
      "id": "UPDATE ML CONTENT TEXT VECTOR",
      "type": "System"
    },
    "context": {
      "pdata": {
        "ver": "1.0",
        "id": "org.ekstep.platform"
      },
      "channel": "01285019302823526477"
    },
    "object": {
      "ver": "1.0",
      "id": "do_113036318281465856163"
    },
    "eventData":{
        "identifier":"do_113036318281465856163",
        "action": "update-ml-contenttextvector",
        "stage": 3,
        "ml_contentTextVector":""
    }
}
```
 **MVC Cassandra Table Modification** 


```
ALTER TABLE content_data 
ADD (textbook_name list<text>, 
        level1_name list<text>, level1_concept list<text>, 
        level2_name list<text>, level2_concept list<text>, 
        level3_name list<text>, level3_concept list<text>, 
        ml_content_text list<text>, ml_keywords list<text>, 
        ml_content_text_vector frozen <set<decimal>>, 
        source list<text>, source_url text, label text);
```

```
select  content_id, textbook_name, level1_name, level1_concept, level2_name, level2_concept,
        level2_name, level2_concept, ml_content_text, ml_keywords, ml_content_text_vector, 
        source, source_url, content_type, label
from content_data;
```






*****

[[category.storage-team]] 
[[category.confluence]] 
