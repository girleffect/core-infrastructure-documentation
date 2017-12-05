.. GOAL: provide a summary of the hosting environment and its key parts, link to detailed descriptions, processes and ways of working.

Our Core Hosting Environment
============================

.. _hosting-overview:

Overview
--------

The previous way Girl Effect approached the hosting of our digital applications and services was on an ad hoc basis, hosting different applications in completely different environments and providers around the world. This approach had a number of drawbacks: 

* It was not cost efficient
* There was no unified view of what was running and where
* It made rapid development and deployment of applications difficult
* It was not possible to share infrastructure and hence not possible to reach economies of scale across all applications
* Applications in different hosting environments could not share secure data storage systems, making data privacy, security and compliance concerns something every application had to solve on their own

The goal of the Core Infrastructure project is to centralise all applications and services into a global cloud-based solution that would help us address all of the above points. To achieve that we are leveraging the best-in-class infrastructure provided by Amazon Web Services (AWS) to build a centralised, scalable and fault tolerant cluster in which all of our current and future applications will be hosted.

At the centre of how we have built the Core Infrastructure Hosting Environment is containerization, which provides us with the key benefits of portability, security and efficiency. Utilising containerization, we provide two dynamically scalable and fault tolerant clusters (Production: for running the production / live versions of the applications; and Quality Assurance (QA): for running testing versions of the applications during development).

.. figure:: /images/hosting_overview.png
    :alt: A simple overview diagram of the Hosting Environment services
    :align: center

    Hosting Environment Overview

Supporting both the Production and QA clusters are a range of infrastructure-level services:

Continuous Delivery
    Spinnaker is the continuous delivery platform we are using for managing all of the applications and services running in the Hosting Environment.

.. TODO: fill in the details of the finalised log provider

Logging
    Consolidated logging functionality is provided by a hosted logging service (Sumo Logic). Log data from the containers will feed into the service for review and processing.

.. TODO: link to the dashboards where appropriate

Monitoring
    Current system health dashboards and notice boards are provided for the core platforms, along with automated alerting for sever system events.

Metrics
    Reports of key performance metrics for the containers and other infrastructure are provided to application providers.
    

Usage & Billing
    Detailed breakdowns of resource usage and — potentially — costs are provided for applications.

.. _hosting-key-technologies:

Key Technologies
----------------

There are four key technologies that form the backbone of our Core Infrastructure Hosting Environment:

.. figure:: /images/hosting_breakdown.png
    :alt: A breakdown diagram of the key technologies that make up our hosting environment
    :align: center

    Hosting Environment Key Technologies

Amazon Web Services (AWS)
~~~~~~~~~~~~~~~~~~~~~~~~~

AWS provides the resources we use as the basic compute and networking building blocks of the hosting environment:

.. TODO: details about how these resources are used to build the cluster.

* Elastic Compute (EC2)
* Elastic IPs
* Virtual Private Cloud (VPC)
* Elastic Load Balancers (ELB)
* Route 53

AWS is the current market leading cloud service provider and on top of its best-in-market cloud hosting environment and compute resources (EC2) AWS also provides the following key advantages for us:

Multiple regions across the globe
    While we are currently only hosting in a single region (Ireland-Europe), AWS provides us with the flexibility to quickly roll out infrastructure across the globe to best serve all markets if needed.

Multiple Availability Zones in each region
    In a single region we run our cluster infrastructure across multiple availability zones to ensure that downtime in a single AZ does not result in downtime for the whole cluster. 

Relational Database Service (RDS)
    RDS allows us to quickly provide fast, efficient and safe access to database services like PostgreSQL and MySQL to all the applications running in our infrastructure. RDS also provides us with at-rest encryption and solid backup strategies for all of our critical data sources.

Additional Services
    AWS provides many additional services that can be immediately used with little additional administrative burden. From data warehousing to machine learning and conversational interfaces, AWS provides all the tools we will need to quickly build out many applications.


Docker
~~~~~~

We have standardised on Docker as the base unit of computation for all application workloads that need to run in our hosting environment. This provides us and application developers with some key benefits:

.. TODO: expand on each of these

* lightweight
* standards based
* consistency
* security
* portability


DC/OS
~~~~~

DC/OS (the datacenter operating system) is an open-source, distributed operating system based on the Apache Mesos. 

Spinnaker
~~~~~~~~~

* CD
* orchestration
* immutable
* multi cluster

.. _hosting-requirements:

Application Requirements
------------------------

To run an application in our Core Infrastructure Hosting Environment there are a few requirements that must be adopted:

#. Applications must run as Docker containers
#. Applications must get configuration parameters from the environment
#. Applications must not use mounted / shared volumes
#. Applications must be able to be torn down and / or restarted elsewhere without notice

We also strongly recommend adopting the following best-practices:

#. Follow our Docker best-practices
#. Log to only to stderr and stdout
#. Use a RDS-compatible database service (preferably PostgreSQL, MySQL is also possible)
#. Open source first

Requirements
~~~~~~~~~~~~

**Applications must run as Docker containers**

All applications are expected to be run as Docker images that are managed by Spinnaker. Typically how the resulting Docker image is built is not really a concern, but we do provide a guide on how we build and test our images and recommendations on best practices that should be adopted.

**Applications must get configuration parameters from the environment**

Applications are expected to be configurable via environment variables that are passed from Spinnaker to the running instances. How much configuration is made customisable via the environment is ultimately up to the application developer's needs but we have a blanket policy of not allowing any secrets to be included in the Docker image.

`The Twelve-Factor App <https://12factor.net>`_ methodology is a good pattern to adopt that covers this.

**Applications must not use mounted / shared volumes**

Sharing volumes across container instances has proven to be a reliability and scalability problem for us in the past so we require all application developers to rather use AWS native solutions like S3 for the storage needs.

**Applications must be able to be torn down and / or restarted elsewhere without notice**

While we do our best to make sure container instances are not arbitrarily stopped and started, application developers are expected to be handle this behaviour without notice from the system. 

Recommendations
~~~~~~~~~~~~~~~

**Follow our Docker best-practices**

.. TODO: link all the supporting docs here

While a Docker image is self contained there are best-practices that we follow for how we structure and build our own Docker images. Would strongly recommend all applications that will run in our environment follow the same or comparable best-practices.

**Log to only to stderr and stdout**

.. TODO: link to log service and guides here

There is no need for logging to specific files in a container. All data in the container file system is transient to that instance and will disappear when the instance is stopped. All logging should rather be directed at either the standard output log (stdout) or the standard error log (stderr). All container stdout and stderr logs will be automatically passed on to our consolidated logging service where they can be accessed and filtered.

**Use a RDS-compatible database service**

We currently only support applications using a RDS provisioned database service. Some applications may not need a database, but for any that do we expect them to use a RDS compatible database.

**Open source first**

.. TODO: link policy and licensing docs here

Our policy is Open Source first for all our code and we recommend application providers do the same unless specifically asked not to.


Further Reading
---------------

* in-cluster traffic routing and load balancing
* resource creation
