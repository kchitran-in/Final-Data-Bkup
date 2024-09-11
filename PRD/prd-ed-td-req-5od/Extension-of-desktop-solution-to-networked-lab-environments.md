 **Context** 

In situations where there is a server connected through a LAN network with individual clients, there should a mechanism where


* Content can be hosted on the server and distributed to the clients. 
* Telemetry can be synced from the clients to the server, and eventually synched back online from the server. 



 **Assumptions** 


* Only the server machine will be provided with capabilities of import/export content and telemetry. Individual client machines purely query the server to show content to users. This is because bulk of the users (teachers/students) in a school environment are not tech savvy - and it is preferable not to provide local content management at every client level, when there is a centralised mechanism of handling this. 
* If a user wants to convert a client machine into a server machine, they will uninstall the client app and install the server version of the app. 
* The server machine can be Linux/Windows, and similarly the client machines can be on Windows/Linux. 
* This kind of a setup is connected via LAN, and may have intermittent access to the internet. 



 **Scope** 


* Provide a client and server version of the desktop app.
* The client app should have bare minimum content playing capabilities. It should sync all telemetry, logs and support tickets to the server. 
* The server version only should have content management and export/import telemetry capabilities. 
* The amount of config to be done to setup this environment should be minimal - like maybe a page to view the IP address and port the server is hosted on (in the server app), and a page to configure which IP to point to in the client apps. 



*****

[[category.storage-team]] 
[[category.confluence]] 
