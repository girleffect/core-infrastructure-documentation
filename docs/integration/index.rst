Integration Guide
=================


.. _integration-integration-guide:


Before getting started with integrating your application with the GE Core Infrastructure, there are some things to take into account.
Below is a checklist of items that will need to addressed in order to integrate successfully.

* Get permission from the relevant authority inside Girl Effect (exact details to be defined)
* Provide URL to the Core Infrastructure Team for Terms & Conditions page on your application (used as consent during User Registration)
* Document method of deleting User Generated Content (UGC) as well as any cached local copies of user account information living on the application. This is needed when a user requests their account to be deleted.
* If you application has an existing user case, define a User Data Migration strategy & timelines
* Create Theme for application and provide to Core Infrastructure Team for setup, or decide on existing theme to use
* Create Application Roles & Permissions matrix and get approval from GE
* Map Application Roles to Core Infra Roles and get approval from GE
* Setup QA instances of your application to test integration with

Existing User Data Migration

Choose an OIDC Client Library

Set Up Development environment

Set up QA Testing instances

Integrate Registration

Integrate login

Integrate Edit Profile
  Reset password
  Update Security Questions
  Request Account Deletion
