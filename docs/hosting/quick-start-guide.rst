Quick-start Guide: Running an Application
=========================================

Introduction
------------

This guide will give you a quick introduction to the steps necessary to launch an application in the Girl Effect hosting environment and the requirements you need to meet to do so.

Requirements
------------

Before you begin you need the following:

#. Your application needs to be a docker container
#. Your application needs to have met the :ref:`tech requirements <developer-requirements>`
#. You need to have supplied your requirements for AWS resources like RDS databases and S3 buckets via the support process
#. You need to have supplied a list of the Docker Hub repositories that hold the images you need for running your application via the support process

Initial deployment
------------------

Once you have met the initial requirements you will be supplied with the following:

#. An account on the Girl Effect Developer Okta platform
#. Access to Spinnaker and Sumo Logic via the Okta account
#. An account on the relevant Grafana instances for your account
#. The connection parameters and credentials for all the resources you have requested
#. The Spinnaker Application name that has been created for your application

To set up the initial container in the QA cluster in Spinnaker you need to follow these steps:

#. Log in to Spinnaker and click on your application name in the applications list
#. On the Clusters screen of your application, click the "Create Server Group" button
#. Fill in the details of your container
    * The account which you want to launch this container into (either PRD or QA)
    * The stack and detail names by following :ref:`the Spinnaker naming convention patterns <spinnaker-naming-convention>`
    * The container image and tag
    * Always select "Bridge" for the Network Type and then add "Service Endpoint" entries for any ports that need to be exposed
    * The environment variables that define your containers configuration parameters
    * The labels (if required) for routing external traffic to your container via our automated HAProxy setup
    * The HTTP healthcheck endpoint that DC/OS should use to determine if your application is healthy
#. Click the "Create" button

This will launch the first version of your container into the QA hosting environment.

Once the Spinnaker server group is running an healthy you can click on it and use the "Server Group Actions" menu to perform common actions like resizing, disabling, destroying and cloning.