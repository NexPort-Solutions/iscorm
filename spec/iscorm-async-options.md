# IScorm ASYNC Options Entity
This entity is primarily passed into IScorm api calls that are Asynchronously run

## Example
```js
var options = {success: function(){
                alert("LMS Finish Successful!");
                },
               error: function(e){
                alert("LMS Finish Failed!");
               }
              };
api.LMSInitialize('', options);
```
## Properties

### success 
**Type:** function()

**Description:** Function that will be called if the LMS API call is successful.

### error
**Type:** function([IScormErrorEntity](#IScormErrorEntity) e)

**Description:** Function that will be called if the LMS API call has failed. The e parameter can be used to determine
the cause of the failure.

# IScormErrorEntity

## Properties
### description
**Type:** string

**Description** System (LMS) descriptive string describing the error
### diagnostic
**Type:** string

**Description** System (LMS) diagnostic information
### errorCode
**Type:** string

**Description** ADL SCORM 1.2 Runtime error code as defined in the SCORM 1.2 Runtime
### errorString
**Type:** string

**Description** ADL SCORM 1.2 Runtime error code STRING as defined in the SCORM 1.2 Runtime
