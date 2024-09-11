Some of the steps in sunbird installation that can be automated.


1. Creation of VM in Azure or AWS with the minimum requirement
    1. Note down the private IP address and also make sure that the basic required ports are open and are accessible.
    1. Install the Minimum operating system on the VM's

    
1. Create an Azure account to 
1. Install git on the created VM's 
1. Clone the DevOps repo for Sunbird Installation
1. Update the Config with the values.
1. Start the Installation
1. After Each stage update the user about the stage completion and once the stage six is completed (badger service is completed) generate the sunbird_SSO_key and update the Confg 


1. complete the sunbird Installation and check for the health of all the services.
1. Use the Created tools to Create Org and Create Users and assign Users to Org.
1. use the tool to update the Taxonomy





Open Questions.


1. The Ekstep API key is a one time process. should the generation of the same should it be automated or can it be a manual process
1. can we use the Test automation tool to check the sanity of the installed Sunbird.



*****

[[category.storage-team]] 
[[category.confluence]] 
