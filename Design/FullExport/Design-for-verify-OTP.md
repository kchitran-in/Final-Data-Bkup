
## Problem statement:
  As a sunbird system it should be able to do the verification of generated OTP. 


## Proposed Solution:
  Sunbird will expose new api to verify OTP. Both Generate OTP and Verify OTP can be a single micro-service. New api structure will be as follow.  




```js
URI: v1/user/otp/verify
Method: POST
Request body :

 {
  "request": {
          "key":"either phone or email"
           "type":"email/phone"
           "otp": "otp value"
       }
  }

Response body:
   {
    {
    "id": "api.user.otp.verify",
    "ver": "v1",
    "ts": "2018-11-21 08:55:04:708+0000",
    "params": {
        "resmsgid": null,
        "msgid": "8e27cbf5-e299-43b0-bca7-8347f7e5abcf",
        "err": null,
        "status": "success", 
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
     
         }
  }

// in case of failure it will have errmsg and responseCode will be failure code (client-error, server-error)
```


This api will do following checks:


1. key should be either valid phone number format or email format.
1. Incoming OTP should match with configured one (example: configured is alphanumeric but it's coming only as numeric, or configured is 5 digits but it's having only 4 or more than 5 digits)
1. This email/phone should not be in blocked list (blocked for 24 hours or some configured time due to too many hits) -  **Design required , in case of blocked list where need to be store it** 
1. OTP generation/verification need to generate api access telemetry.


## Open points:

*  Once OTP is verified , DO we need to removed it completely from DB or Do we need to hold for 24 hours , so that within 24 hours also he should not exceed limit.

      



*****

[[category.storage-team]] 
[[category.confluence]] 
