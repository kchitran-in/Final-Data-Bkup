
# Background: 
Currently, Sunbird has one portal instance that has all the modules and has multiple tenant support. If a tenant request any changes to an existing feature or a new feature, all tenants will get these changes as well.


# Problem statement:
Sunbird should support experimenting with the portal, which allows customers to load the different portal app/module with new features. This should follow the below principle


1. Experiment feature should be isolated from the main app.
1. Deployment of the experiment should not affect the main app.
1. Loading of the experiment app should be configurable and loading logic should reside in the server.
1. Determine experiment Id  and fetch experiment details before the app loads .
1. It should not have any impact on the load times for the users who are not part of an experiment.
1. All telemetry generated from the portal thereafter should contain the experiment id (in tags section)


# Prerequisites :- 

* APP_INITIALIZER :- The "APP_INITIALIZER" is an instance of InjectionToken in angular that  will be executed when an application is initialized. We will make use of it and perform our device register call and get the experiment details at this step.
* Currently device register call is done after the app is initialized.


# Loading Experiment specific app:
 **Solution :- ** 

![](images/storage/Untitled%20Diagram%20(1)%20(1)%20(1)%20(2).jpg)



 **Workflow for Anonymous users  : -** 


1. Anonymous user opens the sunbird portal by entering the url .
1. before the portal loads in browser a middleware is called in portal backend that determines which app to load
    1. if expID is set in the express session load the experiment app
    1. else load the default portal app .

    
1. App_initializer factory method is called before the angular bootstrap process.
    1. generate the Did and uaspec from browser. 
    1. makes an device register api call from portal backend (did and uaspec are passed as parameters)

    
    1. From portal backend make a device register call passing " **url and did"** as extra parameters to fetch the experiment details .

    
    1. If any experimentation details is present then
    1. check for experiment build in blob
    1. if exists set the  **experiment id**  in express session.
    1. return the api response.

    

    
    1. If no experimentation details present 
    1. return the api response.

    

    

    
    1. API response from device register is received
    1. if experimentation details present then
    1. check whether expId is set
    1. continue with the portal bootstrap process.

    
    1. if expId is not set 
    1. reload the app.
    1. process continues from step 2.

    

    
    1. if experimentation details not present then
    1. continue with the portal bootstrap process.

    

    

    



 **Workflow for Logged in users  : -** 


1. Anonymous user opens the sunbird portal by entering the url .
1. before the portal loads in browser a middleware is called in portal backend that determines which app to load
    1. if expID is set in the express session load the experiment app
    1. else load the default portal app .

    
1. App_initializer factory method is called before the angular bootstrap process.
    1. generate the Did and uaspec from browser. 
    1. makes an device register api call from portal backend (did and uaspec are passed as parameters)

    
    1. From portal backend make a device register call passing " **url and did and uid"** as extra parameters to fetch the experiment details .

    
    1. If any experimentation details is present then
    1. check for experiment build in blob
    1. if exists set the  **experiment id**  in express session.
    1. return the api response.

    

    
    1. If no experimentation details present 
    1. return the api response.

    

    

    
    1. API response from device register is received
    1. if experimentation details present then
    1. check whether expId is set
    1. continue with the portal bootstrap process.

    
    1. if expId is not set 
    1. reload the app.
    1. process continues from step 2.

    

    
    1. if experimentation details not present then
    1. continue with the portal bootstrap process.

    

    

    





*****

[[category.storage-team]] 
[[category.confluence]] 
