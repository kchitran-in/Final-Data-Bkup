 **Introduction:** This wiki explains the current structure of external store data for content and the proposed changes in the structure to bring consistency.

 **Background & Problem statement:** 

| Content-Type | Identifier in Neo4J | Identifier in Cassandra | Version 0 | Version 1..10 | Data | 
|  --- |  --- |  --- |  --- |  --- |  --- | 
| ECML | do_123 | do_123 | Draft, Live | Live | Draft and Live version object have the same format for the data. | 
| do_123.img | do_123.img |  | Draft | 
| Collection | do_123 | do_123.img | Draft |  | Draft version will not have the root-object metadata. | 
| do_123 | do_123 | Live | Live | 
| do_123.img | do_123.img |  | Draft | 

 **Design:**  **Option 1:** 

| Content-Type | Identifier in Neo4J | Identifier in Cassandra | Version 0 | Version 1..10 | Data | 
|  --- |  --- |  --- |  --- |  --- |  --- | 
| ECML | do_123 | do_123 | Draft, Live | Live | Draft and Live version object have the same format for the data. | 
| do_123.img | do_123.img |  | Draft |  | 
| Collection | do_123 | do_123 | Draft, Live | Live | A draft version will not have the root-object metadata. | 
| do_123.img | do_123.img |  | Draft |  | 

 **Implementation Changes** 


1. Get hierarchy API for Live version(without mode=edit) should validate status in Cassandra data and throw resource not found if status is not part of hierarchy data
1. In publish pipeline, read data from neo4j and based on identifier from neo4j, fetch hierarchy data from Cassandra
1. Migrate hierarchy data of draft collection content which does not contain pkgVersion in it.

 **Option 2:** 

| Content-Type | Identifier in Neo4J | Identifier in Cassandra | Version 0 | Version 1..10 | Data | 
|  --- |  --- |  --- |  --- |  --- |  --- | 
| ECML | do_123 | do_123 |  Live | Live | Draft and Live version object have the same format for the data. | 
|  | do_123.img | do_123.img | Draft | Draft | 
| Collection | do_123 | do_123 |  Live | Live | A draft version will not have the root-object metadata. | 
| do_123.img | do_123.img | Draft | Draft | 

 **Implementation Changes** 


1. Changes required to store draft version in external store for create, update and read contents
1. Publish pipeline changes to read ECML draft only from do_id.img
1. Migrating all draft ECML content with do_id.img





*****

[[category.storage-team]] 
[[category.confluence]] 
