# Frequently Asked Questions and Answers

- ## Which operating systems are supported by Whaleal platform?

      Currently, the platform supports CentOS 6, CentOS 7, and CentOS 8. Other operating systems are under development.

- ## Which databases are supported by the Whaleal platform?

      Currently, only MongoDB is supported. Other databases are under development.

- ## Can I reset my password?

      Regular users cannot reset their passwords. You need to contact an administrator to reset your password.

- ## How do I add a new host?

  - For details on adding a new host, refer to [AddHost](../02-Usage/Host/AddHost.md).

- ## How do I create a cluster?

  - For details on creating a cluster, refer to the following links:

    - Create Standalone: [CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
    - Create Replica Set: [CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
    - Create Sharded Cluster: [CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)

- ## What does an alarm condition mean?

      An alarm condition refers to setting threshold values for CPU, memory, swap, disk, and bandwidth based on your needs. When these thresholds are triggered, abnormal conditions are sent to administrator users.

- ## After configuring alarm information, how do I receive alarms?

      Once an alarm condition is configured and triggered, alarm notifications will be sent through email, DingTalk, SMS, and other methods.

- ## I configured alarm information and notifications, but I didn't receive any alarms.

      In the user settings, there's an option to configure whether to receive alarm notifications. Make sure this option is turned on.

- ## Do MongoDB nodes support synchronization?

      Currently not supported; under development.

- ## What MongoDB authentication methods are supported?

      Currently, only username and password authentication is supported.

- ## When I remove a node from management, is it shut down?

      When a cluster is removed from management, it is no longer managed and displayed on this platform, but it is not shut down on the host. Deleting a node involves shutting it down.

- ## What should I do if adding a shard fails?

      Manually check the MongoDB logs and investigate the error message to identify the cause.