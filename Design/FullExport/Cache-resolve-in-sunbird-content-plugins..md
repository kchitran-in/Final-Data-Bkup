
## Introduction:
This wiki explains the design and implementation of resolving sunbird-content-plugins cache.


## Background:
Currently, If any fix/feature goes to contributed plugins other than the core plugins, The developers are publishing the plugins without any version bump-up and sunbird-portal deployment.


## Problem Statement:
Currently, When the contributed/dynamic plugins are published the end user fails to get the latest changes of the published plugin due to cache.




## Solution 1 - Bundle plugins with editor's artifact
We need to bundle plugins along with editor artefact, Let's say if Diksha (or) Sunbird instance needs some  **X**  Amount of plugins out of  **Y**  then only bundle and load  **X**  amount of plugin rather than making all plugins to globally available. This 

Plugins should follow the release deployment cycle similar to editor's. 

![](images/storage/Screenshot%202018-11-07%20at%2011.00.12%20AM.png)



Pros:


1. Cache issue will resolve
1. Intermediate fix and publish will not be available



Cons: 


1.  Sunbird deployment is required 
1. Dynamic plugins loading features will not be available. Due to editor is bundled with specific X amount of plugins








## Solution 2 - Plugin version bump-up for the contributed plugins
 **Present:** 







 **Proposal:** 

![](images/storage/Screenshot%202018-11-07%20at%203.37.10%20PM.png)

As soon as the plugin fix is done before plugin get publish the developer must update the version of the plugin, sunbird-player config update and plugin search index update.

The search API should return the latest version of the plugin.



Pros:


1. Due to version maintains, Plugin cache will resolve.
1. Avoids the multiple portal deployment.



Cons:


1. Maintenance - As soon as version update, Admin as to update the sunbird player config through API .
1. Content Upgrade is required 






## Solution 3 - Dynamic updating of param tag(publish time) to plugins network request call 


 **API:** 


```
API Name: '/search'

request:{
identifier”: [“plugin1”, “plugin2"]
}
```


As soon as plugin fix is done,Sunbird as to make an api to get the plugins metadata and pass lastUpdateOn time as config to editor's, The plugins framework should append the lastUpdatedOn field to plugins network request calls

 **Pros:** 


1. Cache will resolve
1. No need to portal or editor deployment
1. No need to version update



 **Cons:** 


1. To get last updateOn filed sunbird as to make an API call.



 **Metadata** 




```
 {
  lastUpdatedOn(ms)

}
```


 While loading respective plugin the plugin framework should append the last updated on time to network request call by reading from metadata



Pros:


1. No need to multiple deployment
1. Plugins cache will resolve



Cons:


1. Plugin framework need to update.








## Conclusion:


Cache problem can not be resolved by using param tags. So each plugins as to follow the deployment process and developer need to bump up the plugin version, If any incompatibility issue. Along with user may required to upgrade the content as well.

We need further design discussion for the plugin version bump-up and content upgrade.



  



   









    









*****

[[category.storage-team]] 
[[category.confluence]] 
