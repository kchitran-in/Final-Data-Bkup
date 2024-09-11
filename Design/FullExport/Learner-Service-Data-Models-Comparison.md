The purpose of this document is to review schema of data synched between Cassandra and Elasticsearch by Learner Service. Also, this would serve the purpose of identifying unused or irrelevant fields that can be removed. The fields requiring discussion are highlighted in red font color.

 **USER**  :

  



| Cassandra | Elastic Search | 
|  --- |  --- | 
|  **User TABLE**  |  **user Topic**  | 
| id : "text" | id,identifier | 
| avatar : "text" |  | 
| channel : "text" | channel | 
| countrycode : "text" | countryCode | 
| createdby : "text" | createdBy | 
| createddate : "text" | createdDate | 
| currentlogintime : "text" | currentLoginTime | 
| dob : "text" | dob : "Date" | 
| email : "text" | email | 
| emailverified :"boolean" | emailVerified | 
| firstname : "text" | firstName | 
| framework: " map<text, frozen<list<text>>>" | framework : {"board" : "List""gradeLevel" : "List""id" : "text","medium" : "List""subject" : "List" } | 
| gender: "text" | gender | 
| grade :"list<text>" | grade | 
| isdeleted : "boolean" | isDeleted | 
| language : "list<text>" | language | 
| lastlogintime  : "text" | LastLoginTime | 
| lastname : "text" | lastName | 
| location : "text" | location | 
| locationids : "list<text>" | locationIds | 
| loginid : "text" | loginId | 
| password : "text" |  | 
| phone :"text" | phone (mask Phone)  (encPhone - phone as encrypted) | 
| phoneverified : "boolean" | phoneVerified | 
| registryid :"text" |  | 
| roles : "list<text>" | roles | 
| rootorgid : "text" | rootOrgId | 
| status" : "int" | status | 
| subject : "list<text>" | subject | 
| temppassword :"text" |  | 
| thumbnail : "text" |  | 
| tncacceptedon  : "timestamp" | tncAcceptedOn :  : "date" | 
| tncacceptedversion : "text" | tncAcceptedVersion | 
| updatedby : "text" | updatedBy | 
| updateddate : "text" | updatedDate | 
| userid : "text" | userId | 
| username : "text" | userName | 
| usertype : "text" | usertype | 
| webpages : "list<frozen<map<text, text>>>" |  | 
| profilevisibility : "map<text, text>" | this is  **userProfilevisibility**  topic from elastic search{"email":"text","gender":"list","grade": "list","identifier":"text","language": "list","location": "list","loginId": "text","phone":  "text","userId":"text","userName":  "text"} | 
|  **User Education TABLE**  |  | 
| id : "text" | id | 
| addressid : "text" | addressId | 
| boardoruniversity : "text" | boardOrUniversity | 
| coursename : "text" | CourseName | 
| createdby : "text" | createdBy | 
| createddate : "text" | createdDate | 
| degree : "text" | degree | 
| duration : "int" | duration | 
| grade : "text" | grade | 
| isdeleted : "boolean" | isDeleted | 
| name : "text" | name | 
| percentage : "double" | percentage | 
| updatedby : "text" | updatedBy | 
| updateddate : "text" | updatedDate | 
| userid : "text" | userId | 
| yearofpassing :"int" | yearOfPassing | 
|  ** USER_EXTERNALID_TABLE**  |  | 
| id : "text" |  | 
| createdby : "text" |  | 
| createdon : "timestamp" |  | 
| externalid : "text" |  | 
| provider : ""text |  | 
|  ** user_job_profile TABLE**  |  | 
| addressid :"text" | addressId | 
| createdby :"text" | createdBy | 
| createddate :"text" | createdDate | 
| enddate :"text" | endDate | 
| iscurrentjob: "boolean" | isCurrentJob | 
| jobname :"text" | jobName | 
| joiningdate :"text" | joiningDate : "date" | 
| orgid :"text" | orgId | 
| orgname :"text" | orgName | 
| role :"text" | role | 
| subject : "list<text>" | subject | 
| updatedby :"text" | updatedBy | 
| updateddate :"text" | updateDate | 
| userid :"text" | userId | 
| boardname :"text" |  | 
| isdeleted : "boolean" |  | 
| isrejected: "boolean" |  | 
| isverified :"boolean" |  | 
| verifiedby :"text" |  | 
| verifieddate :"text" |  | 
|  **user_badge_assertion TABLE**  |  | 
| id :"text" | id | 
| assertionid :"text" | assertionId | 
| badgeclassimage :"text" |  | 
| badgeclassname :"text" | badgeClassName | 
| badgeid :"text" | badgeId | 
| createdts : "timestamp" | createdTs | 
| issuerid :"text" | issuerId | 
| userid :"text" | userId | 
|  |  | 
|  **user_org TABLE**  |  **user.Organisations **  | 
| id :"text" | id | 
| addedby :"text" | addedBy | 
| addedbyname :"text" | addedByName | 
| approvaldate :"text" | approvalDate | 
| approvedby :"text" | approvedBy | 
| hashtagid :"text" | hashTagId | 
| isapproved :"boolean" | isApproved | 
| isdeleted :"boolean" | isDeleted | 
| isrejected :"boolean" | isRejected | 
| organisationid :"text" | organisationId | 
| orgjoindate :"text" | orgJoinDate | 
| orgleftdate :"text" | orgLeftDate | 
| position :"text" | position | 
| roles : "list<:text>" | "roles" | 
| updatedby :"text" | updatedBy | 
| updateddate :"text" | updatedDate | 
| userid :"text" | userId | 
|  |  | 
|  **address TABLE**  |  **user.address**  | 
| id :"text" | id | 
| addressline1 :"text" | addressLine1 | 
| addressline2 :"text" | addressLine2 | 
| addtype :"text" | ? | 
| city :"text" | city | 
| country :"text" | country | 
| createdby :"text" | createdBy | 
| createddate :"text" | createdDate | 
| isdeleted :"boolean" | isDeleted | 
| state :"text" | state | 
| updatedby :"text" | updatedBy | 
| updateddate :"text" | updatedDate | 
| userid :"text" | ? | 
| zipcode :"text" | zipCode | 
|  |  | 

 **ORGANISATION**  :





| Cassandra | ElasticSearch | 
|  --- |  --- | 
|  **organisation TABLE**  |  **org topic**  | 
| id :"text" | id | 
| addressid :"text" | addressId | 
| approvedby :"text" |  | 
| approveddate :"text" |  | 
| channel :"text" | channel | 
| communityid :"text" |  | 
| contactdetail :"text" | contactDetail | 
| createdby :"text" | createdBy | 
| createddate :"text" | createdDate | 
| datetime : "timestamp" |  | 
| description :"text" | description | 
| email :"text" | email | 
| externalid :"text" | externalId | 
| hashtagid :"text" | hashTagId | 
| homeurl :"text" | homeUrl | 
| imgurl :"text" | imgUrl | 
| isapproved :"boolean" |  | 
| isdefault :"boolean" | isDefault | 
| isrootorg :"boolean" | isRootOrg | 
| locationid :"text" | locationId | 
| locationids : "list<text>" | locationIds | 
| noofmembers : " int " | noOfMembers :"long" | 
| orgcode :"text" | orgCode | 
| orgname :"text" | orgName | 
| orgtype :"text" | orgType | 
| orgtypeid :"text" | orgTypeId | 
| parentorgid :"text" | parentOrgId | 
| preferredlanguage :"text" | preferredLanguage | 
| provider :"text" | provider | 
| rootorgid :"text" | rootOrgId | 
| slug :"text" | slug | 
| status : " int " | status | 
| theme :"text" | theme | 
| thumbnail :"text" |  | 
| updatedby :"text" | updatedBy | 
| updateddate :"text" | updatedDate | 
|  | "address" : {"addressLine1" : "text","addressLine2" : text","city" : "text","createdBy" : "text" ,"createdDate" :"text" ,"id"  :"text" ,"state" : "text" ,"updatedBy" : " text ","updatedDate" :"text","zipcode" : "text"} | 
|  |  | 
|  **org_external_identity TABLE** (PRIMARY KEY (provider, externalid) **)**  |  | 
| provider :"text" | provider | 
| externalid :"text" | externalId | 
| orgid :"text" | organisationId | 
|  |  | 





 **Course Batch :** 



| Cassandra | ElasticSearch | 
|  --- |  --- | 
|  **course_batch TABLE**  |  **batch topic**  | 
| id :"text" | id | 
| countdecrementdate :"text" | countDecrementDate | 
| countdecrementstatus :"boolean" | countDecrementStatus | 
| countincrementdate :"text" | countIncrementDate | 
| countincrementstatus :"boolean" | countIncrementStatus | 
| courseadditionalinfo : "map<text, text>" | courseAdditionalInfo | 
| coursecreator :"text" | courseCreator (?) | 
| courseid :"text" | courseId | 
| createdby :"text" | createdBy | 
| createddate :"text" | createdDate | 
| createdfor : "list<text>" | createdFor | 
| description :"text" | description | 
| enddate :"text" | endDate | 
| enrollmenttype :"text" | enrollmentType | 
| hashtagid :"text" | hashTagId | 
| mentors : "list<text>" | mentors | 
| name :"text" | name | 
| participant : "map<text, boolean>" | participant | 
| startdate :"text" | startDate | 
| status : "int" | status | 
| updateddate :"text" | updatedDate | 



 **userCourses :** 



| Cassandra | ElasticSearch | 
|  --- |  --- | 
|  **userCourse TABLE**  |  **usercourse topic**  | 
| id :"text" | id | 
| active :"boolean" | active | 
| addedby :"text" | addedBy | 
| batchid :"text" | batchId | 
| completedon : "timestamp" | completedOn | 
| contentid :"text" | contentId | 
| courseid :"text" | courseId | 
| courselogourl :"text" | courseLogoUrl | 
| coursename :"text" | courseName | 
| datetime : "timestamp" | dateTime : "text" | 
| delta :"text" |  | 
| description :"text" | description | 
| enrolleddate :"text" | enrolledDate | 
| grade :"text" | grade | 
| lastreadcontentid :"text" | lastReadContentId | 
| lastreadcontentstatus : "int" | lastReadContentStatus | 
| leafnodescount : "int" | leafNodeCount | 
| progress :" int " | progress | 
| status :" int " | status | 
| tocurl :"text" | tocUrl | 
| userid :"text" | userId | 



 **Location :** 



| Cassandra | ElasticSearch | 
|  --- |  --- | 
|  **location TABLE**  |  **location topic**  | 
| id :"text" | id | 
| code :"text" | code | 
| name :"text" | name | 
| parentid :"text" | parentId | 
| type :"text" | type | 





*****

[[category.storage-team]] 
[[category.confluence]] 
