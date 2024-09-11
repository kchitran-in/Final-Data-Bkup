

 **Introduction** This wiki details the different ways to provide the app updates to the end-user and there pros and cons and finally conclude on the approach

 **Approach 1 - New installer** 

In this approach, we will provide the latest version of the app to the end-user then he needs to install with the new app which will be as follow

![](images/storage/App%20Updates%201.png)





| Operating System | Works | 
|  --- |  --- | 
| Windows | Yes | 
| Mac | Yes | 
| Ubuntu | Yes | 

 **Pros** 
1. Simple and secure
1. No development required for the app updates

 **Cons** 
1. User need to update the app manually 
1. Can't provide force update
1. Can override new version of the app with the old one
1. User should know that new update available which requires communication to the user



 **Approach 2 - Electron auto-updater** Here app updates are provided using [electron builder](https://www.electron.build/) by building the app with publishing flag which will generate metadata to check for the update here we need to add electron-updater as a dependency require to code for to check and install the update







| Operating system | Works | 
|  --- |  --- | 
| Windows | Yes | 
| Ubuntu | No | 
| Mac | Yes | 



![](images/storage/App%20Updates%20electron%20builder.png)



 **Pros** 
1. Can provide force update 
1. Comes out of the box
1. Code signature validation not only on macOS but also on Windows.
1. All required metadata files and artifacts are produced automatically.
1. Download progress and [staged rollouts](https://www.electron.build/auto-update#staged-rollouts) supported on all supported platforms.
1. It provides logs for the app update

 **Cons** 
1. Doesn't work in Ubuntu  OS
1. No granular control

 **Approach 3 - Custom update** Here we will provide the app update in signed zip format which will be downloaded and install in the app which requires development to check for the update and install the update



| Operating system | Works | 
|  --- |  --- | 
| Windows | Yes | 
| Ubuntu | Yes | 
| Mac | Yes | 

![](images/storage/App%20Updates%20Custom.png)

 **Pros** 
1. Can auto-update the app
1. More granular control
1. Works for all the operating systems
1. Can provide force update

 **Cons** 
1. Development effort (Managing the update versions)
1. Reliability needs to be proven
1. UI to show update and check for updates
1. It needs the packaging structure 
1. Code required to push and pull the updates

 **Conclusion** 

Based on the above we will provide an app update with approach 1 which is providing a new installer for app update currently then we will move onto providing updates with approach 3 where we have control to update the app.



After design review conclusion is since we will have desktops which may not be connected or connected we will go with showing predictable update URL like  **<baseUrl>/latest/Desktop_1.0.1.exe ** to the user based on the different dimension like the new version of the content being imported in the old app or if the app is connected to the internet then check if there is new app is available and show the user URL and QR code of the URL to download in other device or same device and update the app.

  



*****

[[category.storage-team]] 
[[category.confluence]] 
