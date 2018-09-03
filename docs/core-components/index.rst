Our Core Components
===================

The next stage of the Core Infrastructure implementation was building services on top of the hosting environment that provide common functionality across Girl Effect’s platforms allowing future applications to focus on serving the core user needs rather than reinventing the same functionality while codifying Girl Effect’s values and best practices.

The first set of core services that have been developed are:

.. _core-components-authentication:

Authentication Service / User Identity
--------------------------------------

Together with Girl Effect, Praekelt has developed an identity provider service that adopts open industry standards (like OpenID Connect) that forms the base user identity for all end-users of Girl Effect’s digital applications and platforms. This identity provider has allowed us to codify our best practices around user acquisition and informed consent for all applications and allow Girl Effect to efficient meet all the compliance requirements of legislation like the GDPR.

Authentication is the process of positively confirming a user’s identity.  The user provides login credentials which are checked against our securely stored records and if they match,  the user will be authenticated.  Authentication mechanisms used varies from a basic four character password for end users, to a much stronger eight character complex password and two factor authentication (2FA) for system users.

The Authentication Service provides users with security measures to protect their online profile. When creating an account, the authentication service enables a user to protect their profile with a password, secret pin or a list of questions that they keep private to protect access to their profile. It can also verify that a specific user is indeed the person they claim to be through account verification.

Previously, user authentication did not exist for users in the Girl Effect ecosystem. With the Core Infrastructure, all users of the Girl Effect Ecosystem will be required to authentication against this service before being granted their relevant roles & permissions by the Access Control Service.

.. _core-components-user-data-storage:

User Data Storage
-----------------

Tied to the need for a universal user identity is the need to safely collect and store user information. The User Data Storage service allows Girl Effect’s applications and partners to no longer develop their own user data storage mechanism by having a centralised service that meets the strictest security and privacy needs.

In conjunction with the Core User Fields, the User Data Store caters for additional Site Specific Data fields that can be stored and retrieved by individual applications.

Previously, user data was stored in individual databases, for each application in the ecosystem. This resulted in data fragmentation and duplication. With the Core Infrastructure, large amounts of data from various sources are stored in a central data store, enabling an organisation to realise the value of insights garnered from one set of data.

.. _core-components-access-control:

Access Control
--------------

There are many different types of users making use of the universal user identity store, from end users that visit a user-facing product like Springster on their mobile device, to a content administrator requiring access to the CMS of various products in order to load an publish content.  Role Based Access Control allows us to assign roles to users, thereby segmenting users and managing their access levels on a global scale.

Access Control means that, at a global level, Girl Effect are able to assign different permissions to the multiple types of users, based on the level of access they require to the infrastructure. Examples of different user types include: End users visiting the site, Content Managers, Application Developers, Data Scientists.

There was no overarching access control governance which could have resulted in variations in access across the applications. An access control governance structure enables Girl Effect to efficiently manage the access throughout the core infrastructure from one role based access control matrix.

.. _core-components-apis:

APIs
----

Internal development APIs
+++++++++++++++++++++++++

====================== ===
Component              URL
====================== ===
Access Control         http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-access-control/develop/swagger/access_control.yml
User Data Store        http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-user-data-store/develop/swagger/user_data_store.yml
Authentication Service http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-authentication-service/develop/swagger/authentication_service.yml
====================== ===

External development API
++++++++++++++++++++++++

====================== ===
Component              URL
====================== ===
Management Layer       http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-management-layer/develop/swagger/management_layer.yml
====================== ===

Internal production APIs
++++++++++++++++++++++++

====================== ===
Component              URL
====================== ===
Access Control         http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-access-control/master/swagger/access_control.yml
User Data Store        http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-user-data-store/master/swagger/user_data_store.yml
Authentication Service http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-authentication-service/master/swagger/authentication_service.yml
====================== ===

External production API
+++++++++++++++++++++++

====================== ===
Component              URL
====================== ===
Management Layer       http://petstore.swagger.io/?url=https://raw.githubusercontent.com/girleffect/core-management-layer/master/swagger/management_layer.yml
====================== ===

.. _core-components-analysis-insight:

Analysis and Insight
--------------------

A key requirement for Girl Effect’s work is being able to measure reach and impact across all of their applications and platforms. To achieve this Praekelt has built a centralised Data Platform that leverages the consolidated hosting environment to extract relevant data insights from each application and platform into a single place for Girl Effect’s evidence team to analyse and report and as needed
