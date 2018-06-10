=============================================
Girl Effect Core Infrastructure Documentation
=============================================

Introduction
============

The Girl Effect Core Infrastructure project is a multi-stage endeavour to consolidate the hosting, data storage and data analysis needs for the entire Girl Effect digital ecosystem, along with providing tools and services that codify our values, goals and best practices.

The Core Infrastructure project will form the shared base of all of Girl Effect's current and future digital platforms. This will enable Girl Effect's teams and application partners to quickly roll out new platforms and services across the globe in a rapid and scalable way while ensuring our user's data privacy and security.

There are three main layers to the Core Infrastructure project:

.. figure:: images/overview_simple.png
    :alt: A simplified overview of the Core Infrastructure project
    :align: center

    Core Infrastructure Layers


Applications
    The application layer is the top most layer and builds on the Core Components and Hosting Environment. This layer is where all the Girl Effect digital applications and services will run, whether they are developed internally at Girl Effect or with outside partners.

    The applications in this layer are expected to leverage the functionality provided by the Core Components and Hosting Environment to enable quick roll out, rapid iteration and easy scaling.

:doc:`Core Components <core-components/index>`
    The Core Component layer builds on the Hosting Environment layer to provide the shared functionality that all the applications can make use of.

    Some of the initial functionality that will be provided by the Core Components is: safe user data storage, authorisation and access control; user and system event logging; platform-wide data analysis; platform-wide media asset management.

:doc:`Hosting Environment <hosting/index>`
    The Hosting Environment layer is the base that the other two layers build on top of. This layer is where all the hosting resources are consolidated into a single system that provides security, scalability, fault tolerance and simplified usage for both the Core Component and Application developers.


Core Concepts
-------------

Sites

A Site refers to a client application that has been registered on the Core Infrastructure. Typically a Site is an interface where users can Log in, Register etc.

Domains

Domains in this context does not refer to DNS domains like "girleffect.org", but rather "containers" on the GE Domain Hierarchy Map.  Client Applications (sites) all live under a domain in the hiearchy, the root or "top" node being "Girl Effect".  System Users can either be assigned roles on a specific Site directly, or be given roles on a Domain, or group of sites, which will make the roles "trickle down" to all Sites below the domain.


End users

End Users are users that use the "public facing" interfaces of the various applications and services.  They do not have any elevated priviledges, and cannot access any administration interfaces, e.g. CMS backends

System users

System Users are the various GE staff members and external contractors that manage the various client applications on the Core Infrastructure.  They use administrative interfaces to manage users, content, application features etc.  In order to be classified as a System User, a user's account will need to have the Organisation field set.
System Users are

Client Application

The term "client application" refers to any application that has been integrated with the Core Infrastructure Core Components, using the Authentication Service, User Data Store etc.

Global Management Portal

The Global Management Portal (GMP) is an administrative interface where System Users can log in to perform various actions.  The main functions of the GMP are:

* Manage User Roles - Allows System Users with the required Roles to assign / remove to other System Users.  This allows teams to self manage, without the need for Girl Effect to be involved with each access request.  That said, Girl Effect still has the ability to manage all System Users, and give or take away roles at their discretion.
* Search Users - This interface allows System Users to search for user profiles across all GE applications that have integrated with the Core Infrastructure.
* Activate / Deactivate users - In the event that a user account is detected by moderators to be in violation of the terms of service, this interface can be used to Deactivate the account, which will prevent the user from logging in to any client application on the Core Infrastructure.

Authentication Service

The Authentication Service is a component of the Core Infrastructure, that handles all User Profile related functions, like Registration, Edit Profile, Login etc.  Client applications redirect users to the Auth Service for these functions, while passing Client Secrets, Configuration, and Access Tokens through with the request.



2FA






Details
-------

One of the main goals of the Core Infrastructure project is to make it possible to rapidly build and deploy scalable applications that still protect our user's data and privacy. To help get application developers up to speed, we provide the following documentation:

* A :ref:`technical overview of our Hosting Environment <hosting-overview>`, including the :ref:`key technologies <hosting-key-technologies>` we have chosen
* A :ref:`reference guide to the technologies needing to be adopted <hosting-requirements>` to run applications in our Hosting Environment
* :doc:`Detailed descriptions of the Core Components <core-components/index>`, :ref:`the APIs they provide <core-components-apis>` and an :ref:`adoption and best practice guide <integration-integration-guide>`.
* Development best practices that we follow
* Our support and escalations procedures

.. toctree::
    :maxdepth: 2
    :hidden:

    hosting/index
    core-components/index
    core-components/oidc
    integration/index
    integration/process-flows
    development-best-practices
    support-escalation
