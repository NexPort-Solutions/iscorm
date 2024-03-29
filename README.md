# Improved SCORM 1.2 Specification (IScorm)

![iSCORM Logo](https://user-images.githubusercontent.com/2368069/137387161-222aee59-b206-4ceb-a3c7-38cc1fcec13b.png)

The IScorm Spec is a Super Set of the ADL SCORM 1.2 Specification. IScorm is designed to provide a few missing features to the SCORM 1.2 API while still mostly supporting the original SCORM 1.2 specification. Here are a few goals:

* Add ASYNC callbacks to LMSInitialize, LMSCommit and LMSFinish
* Expose an alternative to the standard window.api object instance that is less generic
* Expose versioning

The getting Started section below links to each of the extended SCORM specs. As of v1.0 only the SCORM 1.2 Runtime has been extended.

### Posible breaking changes

* LMSInitialize will always return 'true' and to retrieve the error information you must use the asyncOptions parameter
* LMSCommit will always return 'true' and to retrieve the error information you must use the asyncOptions parameter
* LMSFinish will always return 'true' and to retrieve the error information you must use the asyncOptions parameter

### Conventions

* Released versions will be tagged with a versionnumber like 1.0, 1.1, 1.2 etc.
* Working versions will live on branches named for the major working version (1.x, 2.x, 3.x etc.)
* This spec will only document changes to the SCORM 2.1 Specification
* Anything not identified as a change will be assumed to be unchanged from the original spec
* Every effort will be taken to ensure that this extension does not break the original specification except where listed in the breaking changes above.

### Getting Started

As we extend each part of the SCORM 1.2 spec we'll list the changes here:

* [IScorm Run-Time Environment](spec/IScorm\_Run-Time\_Environment.md)

You can download a copy of the original spec here: [ADL SCORM 1.2 Runtime](spec/SCORM-12-RunTimeEnv.pdf)
