
## Problem Statement :  
            AS page api is constructed with list of sections. So before creating page user need to first create sections and then associate those sections with page.


1. As of now all page api is public , so without any key it can be access, that can have potential security issues. 
1. Most of the time user is doing section settings with invalid data type and that will cause page api issues.
1. Number of sections inside page has no limits, So if user has set too many sections then it won't work as expected.
1. As of now System can make section call to Content search only or only one end point but there might be scenarios where we need different sections data end to  be collected from different endpoints. 




## Proposed Solution 1: 
         We can divide page api in two category one for public access and another for private access(only after login). So during page creation user need to indicate it.

  



| Public | Private | 
|  --- |  --- | 
| Number of section can be very small. Ex: Max 3 sections allowed | Number of sections can be configured little more  | 
| On public access, we can avoid filter options | private page will have all filters and other options | 
| Public page response can be catch with some ttl |  | 


## Changes Required.
       1.  in page_management table need to add one column "visibility" with value as {"public" or "private"}

       2.  Section validation will happen during create/update page based on visibility.

       3.  Authentication will be checked conditionally. Means if it's public then authentication not required but for private it's required.

       


## Proposed Solution 2:
     Define a separate end point for public page access. 



| Pros | Cons | 
|  --- |  --- | 
| no impact on existing api's | need to manage one more endpoint | 
| Required to make public api secure. Based on this we can't configure some rate limit |  | 
|  |  | 


## Proposed Solution 3:
 We can Implement Captcha for public api, if captcha is valid then only api call will be process. 

 Example: In case of page api. By default user can make page assemble call and default response system can Catch it for some TTL. So if user is again making same call (means without passing any filters or with default filters only) then catch response will be served. Now user can select different filters and then call apply button , then we can ask user to verify Captcha and once captcha is verified then only call will trigger. 

OR, For public user we can asked Captcha verification first once Captcha is Verified , internally it will create user session for Particular time and then user can do all activity.




## Problem Statement 2:

## Proposed Solution 1:
 During section create or update time , system will do the section data type validation, in case  section query is not valid then it won't allow to create it. 


```js
 {
                "display": "{\"name\":{\"en\":\"Popular Story\",\"hi\":\"लोकप्रिय कहानी\"}}}",
                "alt": null,
                "description": null,
                "sectionDataType": "content",
                "imgUrl": null,
                "searchQuery": "{\"request\":{\"query\":\"\",\"filters\":{\"language\":[\"English\"],\"contentType\":[\"Story\"],\"status\":[\"Live\"]},\"sort_by\":{\"me_averageRating\":\"desc\"},\"limit\":10,\"exists\":[\"me_averageRating\"]}}",
                "name": "Popular Story"
            }


Or 

{
                "display": "{\\"name\\":{\\"en\\":\\"Popular Story\\"}}}",
                "alt": null,
                "description": null,
                "sectionDataType": "content",
                "imgUrl": null,
                "searchQuery": "{\\"request\\":{\\"query\\":\\"\\",\\"filters\\":{\\"language\\":[\\"English\\"],\\"contentType\\":[\\"Story\\"],\\"status\\":[\\"Live\\"]},\\"sort_by\\":{\\"me_averageRating\\":\\"desc\\"},\\"limit\\":10,\\"exists\\":[\\"me_averageRating\\"]}}",
                "name": "Popular Story"
            }

```



```js
{
"request":{
		"name": "Featured Content",
		"sectionDataType": "content",
		"display": {
			"name":{
				"en":"Featured Content"
			}
		},
		"searchQuery": {
			"request":{
				"filters":{
					"contentType":["Course","TextBook","Resource"],
					"status":["Live"]
				},
				"sort_by":{"me_averageRating":"desc"},
				"limit":10
			}
		}
    }
}

```




| Pros | Cons | 
|  --- |  --- | 
| System will have only valid sections |  | 
| it's a preventive action |  | 


## Proposed Solution 2:
         System Will do section validation during page assemble api call, if section is wrongly configured then it will throw proper error. This scenario is already implemented in release-1.13.

  



| Pros | Cons | 
|  --- |  --- | 
| it's a corrective action | DB will have incorrect section | 




## Problem Statement 3 :

## Proposed Solution:
    Sunbird can put some configuration for maximum number of sections inside page. This check will happen during page create/update.

    env: "sunbird_max_page_section_allowed"


## Problem Statement 4 :

##    Proposed Solution:
        System will define list of target and during section create or update time user need to set target as well, if user is not defining any target then default target will be applied.   

       We need to define a separate table to hold target info. id,url, methodType,auth-key etc.











*****

[[category.storage-team]] 
[[category.confluence]] 
