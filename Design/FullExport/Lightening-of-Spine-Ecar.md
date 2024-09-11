
## Introduction
This wiki explains the provisioning of light weighted spine ecar.


## Background
For every collection type content, knowledge platform generates spine ecar. It is bundle of menifest.json (details of the TextBook and its units) and folders for all the contents (holding thumbnail images). Menifest.json contains the relative path of all the thumbnails as appicon.


## Problem Statement
Since all the thumbnail images are already present in the bundle, sometime (if hierarchy is big) ecar size is becoming huge which needs more bandwith for downloading the ecar. 




## Proposed Design

* Generate a separate ecar file which will be light weighted.
* It will not contain the physical copy of thumbnails.
* It will have only menifest.json file bundled into the ecar.
* Instead of relative path of the thumbnail, appIcon field will hold the actual path of the thumbnail available on Azure/S3.
* Depends upon the network bandwith mobile app will decide to download the version of spine ecar.



 **Current appIcon value in menifest.json file:** 

"appIcon": "do_31268439334042828814811/1db4c446ed0425fdd694cad0ca8e1c80_1496381357005.thumb.jpeg"

 **Proposed appIcon value in menifest.json file:** 

 **"appIcon": "<Azure/S3 path>/1db4c446ed0425fdd694cad0ca8e1c80_1496381357005.thumb.jpeg"** 



 **A new entry will be introduced into variants field:** 



| "variants": {      "online": {           "ecarUrl": "[https://ekstep-public-dev.s3-ap-south-1.amazonaws.com/ecar_files/do_11268733615261286411/test-textbook_1548758055948_do_11268733615261286411_12.0_online.ecar](https://ekstep-public-dev.s3-ap-south-1.amazonaws.com/ecar_files/do_11268733615261286411/test-textbook_1548758055948_do_11268733615261286411_12.0_online.ecar)",           "size": 1316      },      "spine": {           "ecarUrl": "[https://ekstep-public-dev.s3-ap-south-1.amazonaws.com/ecar_files/do_11268733615261286411/test-textbook_1548758055359_do_11268733615261286411_12.0_spine.ecar](https://ekstep-public-dev.s3-ap-south-1.amazonaws.com/ecar_files/do_11268733615261286411/test-textbook_1548758055359_do_11268733615261286411_12.0_spine.ecar)",           "size": 8395      } } | 
|  --- | 



*****

[[category.storage-team]] 
[[category.confluence]] 
