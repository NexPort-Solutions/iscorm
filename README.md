# Improved SCORM 1.2 Specification (IScorm)

The IScorm Spec is a Super Set of the IMS SCORM 1.2 Specification.  IScorm is designed to provide a few missing features to the SCORM 1.2 API while still mostly supporting the original SCORM 1.2 specification. Here are a few goals:

- Add ASYNC callbacks to LMSInitialize, LMSCommit and LMSFinish
- Expose an alternative to the standard window.api object instance that is less generic
- Expose versioning 

The getting Started section below links to each of the extended SCORM specs. As of v1.0 only the SCORM 1.2 Runtime has been extended.

## Posible breaking changes
- LMSInitialize will always return 'true' and to retrieve the error information you must use the asyncOptions parameter
- LMSCommit will always return 'true' and to retrieve the error information you must use the asyncOptions parameter
- LMSFinish will always return 'true' and to retrieve the error information you must use the asyncOptions parameter

## Conventions
- This spec will only document changes to the SCORM 2.1 Specification
- Anything not identified as a change will be assumed to be unchanged from the original spec
- Every effort will be taken to ensure that this extension does not break the original specification except where listed in the breaking changes above.


## Getting Started

As we extend each part of the SCORM 1.2 spec we'll list the changes here:
- [IScorm Run-Time Environment](spec/IScorm_Run-Time_Environment.md)

You can download a copy of the original spec here: [ADL SCORM 1.2 Runtime](spec/SCORM-12-RunTimeEnv.pdf)
