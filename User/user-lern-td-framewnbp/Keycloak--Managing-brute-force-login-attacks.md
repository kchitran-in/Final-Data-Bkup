This document describes the steps of how to configure brute force login attacks management in keycloak, and how to create user accounts in keycloak with manage-users permission so that they unlock the locked users (because of a brute force attack on their account).


## Configure Brute Force Detection

* Open keycloak home by opening the url  **_{{host_name}}/auth_** , e.g.: [https://dev.sunbirded.org/auth/](https://dev.sunbirded.org/auth/)

![](images/storage/1_Keycloak_admin_home.png)


* Click on "Administration Console" and login with "admin" user credentials

![](images/storage/2_Keycloak_login.png)


* Click on "Realm Settings" in the left pane to open the "Sunbird" realm settings page

![](images/storage/3_Keycloak_realm_settings.png)


* Click on "Security Defenses" tab

![](images/storage/4_Keycloak_security_defenses.png)


* Click on "Brute Force Detection" tab to configure the brute force detection:
    * Set the  **Enabled**  flag to  **ON** 
    * Set  **Permanent Lockout**  flag to  **OFF** 
    * Set  **Max Login Failures**  to  **10** , to allow 10 unsuccessful attempts before the account gets locked
    * Set  **Wait Increment**  to  **24 Hours** , this will automatically unlock the user after 24 hours
    * Click on  **Save**  to save the settings

    

![](images/storage/5_Keycloak_brute_force_detection.png)

More details about brute force configuration are available at [https://www.keycloak.org/docs/2.5/server_admin/topics/threat/brute-force.html](https://www.keycloak.org/docs/2.5/server_admin/topics/threat/brute-force.html).
## Create User account with manage-users permission

* Switch to  **Master**  realm by changing the realm in the left pane

![](images/storage/6_Keycloak_master_realm.png)


* Click on  **Users**  in the left pane and click on  **Add user**  button in  **Users**  page to create a new user

![](images/storage/7_Keycloak_master_realm_users.png)


* Provide a user name for the user (e.g. support_user) and click on  **Save**  button

![](images/storage/8_Keycloak_new_user.png)


* User is created and the user details page is displayed

![](images/storage/9_Keycloak_new_user_2.png)


* Click on  **Role Mappings**  tab

![](images/storage/10_Keycloak_user_roles.png)


* Select  **sunbird-realm**  in the  **Client Roles**  drop down

![](images/storage/11_Keycloak_sunbird_realm_roles.png)


* Select  **manage-users**  role from  **Available Roles**  list and click on  **Add selected >>**  button

![](images/storage/12_Keycloak_assign_roles.png)


* Click on  **Credentials**  tab

![](images/storage/13_Keycloak_credentials.png)


* Set a password for the newly created user by providing  **New Password**  &  **Password Confirmation**  values, set the  **Temporary**  flag to  **OFF**  and click on  **Reset Password** 




* Click Change Password in the confirmation popup to confirm the password change

![](images/storage/15_Keycloak_update_password_2.png)

The newly created user can login to the Keycloak administration console with the username and password set in the creation steps. Note that this user have " **manage-users** " permissions and can perform operations like delete user, change password, etc. This user does not have permission to impersonate other users.
## Unlock a locked user

* Login to Keycloak administration console with the credentials of the newly created user (using the steps above)

![](images/storage/16_Keycloak_support_user_login.png)


* Go to the users list page by clicking on  **Users**  in the left pane

![](images/storage/17_Keycloak_users.png)


* Search for locked out user by typing the username in the search box and press Enter

![](images/storage/18_Keycloak_search_user.png)


* Click in the user  **ID**  to go to the user details page. If the user is locked out,  **User Enabled**  flag will be set to  **OFF** 

![](images/storage/19_Keycloak_user_details.png)


* Change the  **User Enabled**  flag to  **ON**  and click on  **Save** . Locked out user will be able to login now.




## Configuring the message for account lockout
The message to be displayed when a user account gets locked can be configured by updating the messages_en.properties file in sunbird-devops repository (or in the forked repository that is used to build and deploy keycloak in a sunbird instance).


* Open the file  **sunbird-devops/ansible/artifacts/sunbird/login/messages/messages_en.properties** 
* Update value for the key accountTemporarilyDisabledMessage
    * Ex: accountTemporarilyDisabledMessage=Your account has been locked due to too many incorrect login attempts. You can re-attempt to login after 24 hours. Please get in touch with the help desk team for support

    

 **accountTemporarilyDisabledMessage**  is displayed only in cases of a login attempt with valid credentials for a user account that is locked.

true



|  | 
|  --- | 
|  | 









*****

[[category.storage-team]] 
[[category.confluence]] 
