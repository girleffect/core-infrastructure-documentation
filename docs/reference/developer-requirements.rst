Development Partner Requirements
================================

.. _developer-requirements:

These are the technology related requirements that need to be adhered to by all development teams and partners that want to run applications in the Girl Effect Core Infrastructure.

.. contents::
    :depth: 4


Hosting Environment
-------------------

Docker
~~~~~~

All applications must be docker containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Our entire clustered hosting environment is built on containerisation technology, we therefore require all applications to be built into docker containers to run in any of our clusters.

Applications must get configuration parameters from the environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Applications are expected to be configurable via environment variables that are passed from Spinnaker to the running instances. How much configuration is made customisable via the environment is ultimately up to the application developer's needs but we have a blanket policy of not allowing any secrets to be included in the Docker image, so they at least must be provided via environment variables.

`The Twelve-Factor App <https://12factor.net>`_ methodology is a good pattern to adopt that covers this.

Applications must not use mounted or shared volumes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sharing volumes across container instances has proven to be a reliability and scalability problem for us in the past so we require all application developers to rather use AWS native solutions like S3 for the storage needs.

Applications must be able to handle being started and stopped without notice
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

While we do our best to make sure container instances are not arbitrarily stopped and started, application developers are expected to be handle this behaviour without notice from the system.


Applications must expect the local filesystem to be temporary
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As described in the previous point, applications need to be able to handle being started and stopped at any time by the cluster. This means that any files created or stored on the local filesystem that are not part of the Docker Image need to be treated as ephemeral as they will not persist between launches.

Applications that are required to handle local files in a more permanent manner should use AWS native solutions like S3.


Applications should only log to stderr and stdout
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There is no need for logging to specific files in a container. All data in the container filesystem is transient to that instance and will disappear when the instance is stopped. All logging should rather be directed at either the standard output log (stdout) or the standard error log (stderr). All container stdout and stderr logs will be automatically passed on to our consolidated logging service where they can be accessed and filtered.

Networking
~~~~~~~~~~

Applications cannot be accessed by SSH or other shell invocations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is our policy across the Core Infrastructure that applications are not accessible via any kind of remote shell session. It is our belief that management commands or other ad hoc commands that need to be run are rather codified by the application itself and made available via a UI, API endpoint or single-run Docker image job.

Applications must handle HTTPS-only switch over if needed
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Our cluster load balancers will forward both HTTP and HTTPS traffic to the specified container instances so it is the application's responsibility to handle redirecting from HTTP to HTTPS if serving traffic over HTTPS only is a requirement.

Resources
~~~~~~~~~

Applications should only require other AWS-based resources and services
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

AWS provides a wide range of services and resources that application developers can request access to, for example RDS, ElasticCache, Elasticsearch, etc. We will provide the required access to these services as required but we cannot guarantee access to custom services not provided AWS.

Direct access to AWS services is not provided from outside of the clusters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

AWS services like RDS databases or ElasticCache services are not publicly accessible from outside of the cluster they belong to. This means that developers will not have direct access to those resources from anywhere but their running container instances.