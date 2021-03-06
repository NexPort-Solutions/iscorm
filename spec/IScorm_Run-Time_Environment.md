# IScorm Run-Time Environment
This document contains only those sections of the ADL SCORM 1.2 Runtime that have been changed for the IScorm specification. 
More about the Advanced Distributed Learning (ADL) Initiative can be found here: http://www.adlnet.org

- [IScorm Additions](#iscorm-additions)
  * [Additional API Properties](#additional-api-properties)
- [IScorm Changes](#iscorm-changes)
  * [3.3.2.1. SCO To LMS Communications API Details](#3321-sco-to-lms-communications-api-details)
    + [LMSInitialize](#lmsinitialize)
    + [LMSFinish](#lmsfinish)
    + [LMSCommit](#lmscommit)
# Getting Started
> **NOTE** Async methods are disabled by default in v1.0 and must be enabled via the `SetAsync` method on the API.

An IScorm implementation of the SCORM 1.2 runtime should work fine with the vast majority of SCOs in the field today. The major difference is that the LMSCommit, LMSInitialize and LMS Finish commands are all async when the SetAsync option is set to true
## Determining if IScorm is supported by the API
The easiest way to determine if the SCORM API supports the IScorm spec is to look for the ISCORMVersion property:
```javascript
/// This code assumes you have already discovered the scorm api object
if('ISCORMVersion' in api){
   /// Treat this like an IScorm API
}else{
   /// Treat this like a normal SCORM 1.2 API
}
```
# IScorm Additions

## Additional API Properties
Iscorm adds the following properties to the api object

- **ISCORMVersion** (Type:string): The version of IScorm this api implementation implements. Example: 1.0
- **SCORMVersion** (Type: string): The ADL SCORM version. Always 1.2.
- **DefaultAsyncOptions** (Type: [IScormAsyncOptions](iscorm-async-options.md)): Default async options for all ASYNC method calls. These options will be used if the options are not 
passed into the async method call. If only a subset of the options are set when calling an async method then the "unset" options will fall back to the default.

## Additional API Methods

### SetAsync
**Description:** Used to set or get the async property on the API. The default is false. When false the api should behave exactly like the ADL SCORM 1.2 spec.
If set to true then calls to LMSInitialize, LMSCommit and LMSFinish will be made asyncronously and the asyncOptions of each method must be used to determine if a call failed. 

**Syntax:** SetAsync([boolean _async_])

**boolean async:** Optional parameter set to either true or false. If not set then this method just returns the current setting for async on the api. Default value is false. 

**Return Value:** Current state of the async property, if no parameter is passed in. If a boolean value is passed to the async param then it will set the property to that value and return the new value.

# IScorm Changes
## 3.3.2.1. SCO To LMS Communications API Details

### LMSInitialize
**Description**: This function indicates to the API Adapter that the SCO is
going to communicate with the LMS. It allows the LMS to handle LMS
specific initialization issues. It is a requirement of the SCO that it call this
function before calling any other API functions.

**Syntax:** LMSInitialize(string _parameter_, [[IScormAsyncOptions](iscorm-async-options.md) _options_])

**Parameter:** "" An empty string must be passed for conformance to this
standard. Values other than "" are reserved for future extensions.

**options:** An object with properties for success and error callbacks. See [IScormAsyncOptions](iscorm-async-options.md)
```javascript
options = {success: function(){
                //Do success stuff
                },
               error: function(e){
                //Do error stuff
               }
              };
```
**Return Value:** String representing a boolean.
- **ALWAYS** "true", in order to capture failure or success you must use the options callbacks

If the error callback is triggered, then this signifies to the SCO that the
LMS is in an unknown state and that any additional API calls will not be
processed by the LMS. The 'e' parameter of the error callback will contain the error code...see the [IScormAsyncOptions](iscorm-async-options.md).

**Example:** 
```js
var options = {success: function(){
                alert("LMS Initialize Successful!");
                },
               error: function(e){
                alert("LMS Initialize Failed!");
               }
              };
api.LMSInitialize('', options);
```
The SCO tells the API Adapter that the content wants to establish
communication with the LMS. 

### LMSFinish
**Description:** The SCO must call this when it has determined that it no
longer needs to communicate with the LMS, if it successfully called
LMSInitialize at any previous point. This call signifies two things:
1. The SCO can be assured that any data set using LMSSetValue() calls
has been persisted by the LMS.
2. The SCO has finished communicating with the LMS.

**Syntax**: LMSFinish(string _parameter_, [[[IScormAsyncOptions](iscorm-async-options.md) _options_])

**Parameter:** "" An empty string must be passed for conformance to this
standard. Values other than "" are reserved for future extensions.

**options:** An object with properties for success and error callbacks. See [IScormAsyncOptions](iscorm-async-options.md)
```javascript
options = {success: function(){
                //Do success stuff
                },
               error: function(e){
                //Do error stuff
               }
              };
```

**Return Value:** String representing a boolean.
- **ALWAYS** "true", in order to capture failure or success you must use the options callbacks

If the error callback is triggered, then the SCO may no longer call any
other API functions.
If the error callback is triggered, then this signifies to the SCO that the
LMS is in an unknown state and that any additional API calls may or may not
be processed by the LMS. The 'e' parameter can be used to get the error code of the last call....see the [IScormAsyncOptions](iscorm-async-options.md)

**Example:**
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

### LMSCommit
**Description:** If the API Adapter is caching values received from the SCO
via an LMSSetValue(), this call requires that any values not yet persisted by
the LMS be persisted. _The SCO should assume that no values in the CMI model have 
been persisted until LMSCommit or LMSFinish are called._
~~In some implementations, the API Adapter may persist set values as soon as
they are received, and not cache them on the client. In such implementations,
this API call is redundant and would result in no additional action from the
API Adapter.~~ This call ensures to the SCO that the data sent, via an
LMSSetValue() call, will be persisted by the LMS upon completion of the
LMSCommit().

**Syntax:** LMSCommit(string _parameter_, [[[IScormAsyncOptions](iscorm-async-options.md) _options_])

**Parameter:** "". An empty string must be passed for conformance to this
standard. Values other than "" are reserved for future extensions.

**options:** An object with properties for success and error callbacks. See [IScormAsyncOptions](iscorm-async-options.md)
```javascript
options = {success: function(){
                //Do success stuff
                },
               error: function(e){
                //Do error stuff
               }
              };
```

**Return Value:** String representing a boolean.
- **ALWAYS** "true", in order to capture failure or success you must use the options callbacks

If the error callback is triggered, then this signifies to the SCO
that the LMS is in an unknown state and that any additional API
calls may or may not be processed by the LMS.
**Example:**
```js
var options = {success: function(){
                alert("LMS Commit Successful!");
                },
               error: function(e){
                alert("LMS Commit Failed! Code: " + e.errorCode );
               }
              };
api.LMSCommit('', options);
```
Requires that any cached values, previously set via SCO calls to
LMSSetValue(), that have not been persisted by the LMS be persisted.
