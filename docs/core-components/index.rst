Our Core Components
===================

The next stage of the Core Infrastructure implementation was building services on top of the hosting environment that provide common functionality across Girl Effect’s platforms allowing future applications to focus on serving the core user needs rather than reinventing the same functionality while codifying Girl Effect’s values and best practices.

The first set of core services that have been developed are:


.. _core-components-user-identity:

User Identity
-------------

Together with Girl Effect, Praekelt has developed an identity provider service that adopts open industry standards (like OpenID Connect) that forms the base user identity for all end-users of Girl Effect’s digital applications and platforms.   This identity provider has allowed us to codify our best practices around user acquisition and informed consent for all applications and allow Girl Effect to efficient meet all the compliance requirements of legislation like the GDPR.

.. _core-components-user-data-storage:

User Data Storage
-----------------

Tied to the need for a universal user identity is the need to safely collect and store user information. The User Data Storage service allows Girl Effect’s applications and partners to no longer develop their own user data storage mechanism by having a centralised service that meets the strictest security and privacy needs.

.. _core-components-access-control:

Access Control
--------------

There are many different types of users making use of the universal user identity store, from end users that visit a user-facing product like Springster on their mobile device, to a content administrator requiring access to the CMS of various products in order to load an publish content.  Role Based Access Control allows us to assign roles to users, thereby segmenting users and managing their access levels on a global scale.

.. _core-components-authentication:

Authentication
--------------

Authentication is the process of positively confirming a user’s identity.  The user provides login credentials which are checked against our securely stored records and if they match,  the user will be authenticated.  Authentication mechanisms used varies from a basic four character password for end users, to a much stronger eight character complex password and two factor authentication (2FA) for system users.

.. _core-components-apis:

APIs
----

.. _core-components-analysis-insight:

Analysis and Insight
--------------------

A key requirement for Girl Effect’s work is being able to measure reach and impact across all of their applications and platforms. To achieve this Praekelt has built a centralised Data Platform that leverages the consolidated hosting environment to extract relevant data insights from each application and platform into a single place for Girl Effect’s evidence team to analyse and report and as needed




.. _core-components-guide:

Guide
-----

guide
