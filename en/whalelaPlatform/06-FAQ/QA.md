

# Frequently Asked Questions and Answers

- ## What operating systems does the WAP platform support?

      This platform currently only supports centos 6, centos 7, and centos 8, and other operating systems are yet to be developed.


- ## What databases does the WAP platform support?

      At this stage, only mongoDB is supported, and other databases are yet to be developed.

- ## Can I reset my password?

      Ordinary users cannot, they can ask the administrator to reset their password.

- ## How to add a new host?

  - Add new host details reference
  [AddEC2](../02-Usage/Server/EC2.md),[Add K8S](../02-Usage/Server/K8S.md)


- ## How to create a cluster?

  - For details on creating a cluster, refer to the following link
  
    - Create a single node[CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
    - Create a replica set[CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
    - Create shards[CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)
    - Managed cluster[ExistingMongoDBDeployment](../02-Usage/MongoDB/CreateDeployment/ExistingMongoDBDeployment.md)



- ## What do warning conditions mean?

      The alarm condition is to set the CPU, memory, swap, disk, bandwidth and other thresholds according to your own needs. When the threshold is triggered, the abnormal situation will be sent to the administrator user.

- ## Alarm information is configured, how to accept the alarm?

      When the alarm conditions are configured and the alarm is triggered, the alarm information will be notified via email, DingTalk, SMS, etc.

- ## When alarm information and acceptance were configured, no alarm was received.
  
      There is an option to configure whether to receive alarm notifications on the user page, just turn it on.


- ## Does synchronization between mongos be supported?

      Not supported yet, pending development.

- ## What MongoDB authentication methods are supported?

      1. No authentication is enabled
      2. Account and password
      3. Account number and password and CA certificate

- ## Was the node shut down after it left management?

       When the cluster is taken out of management, it is only not managed and displayed on this platform, and it is not closed on the host. The operation of deleting a node is to shut down the node.

- ## What to do if adding shard fails

      Manually check the mongo log and find the cause based on the error reported in the log.

* ## Is it possible to perform some monitoring operations on the cluster based on the permissions of the system user without performing update operations?

   ```
  Currently, it is not supported to enable the WAP platform to have only view permissions on Mongodb through low-privilege users, but we can use WAP user management to assign only read permissions to users using the platform.
   ```

* ## Can the alarm be written somewhere first and then pull the information myself?

   ```
  Supports writing alarms to appdb and reading alarm information from the database through third-party tools.
   ```

* ## Does it support Kirin system?

  ```
  First, the customer needs to provide Jinmu with the version information and kernel information of the Kirin system currently in use, and then we can provide a reply after conducting targeted testing.
  ```

* ## The principle of horizontal expansion of the platform

  ```
  Horizontal expansion is ordinary high availability, building multiple wap services and sharing one appdb
  The managed agent can be hashed and assigned to different wap, reducing the pressure on a single wap.
  When a certain wap service hangs up, other wap will not be affected. The affected agent will re-hash and distribute it to the healthy wap.
  ```

* ## What does load management mean?

  ```
  Load management of appdb
  ```

* ## When wap expands nodes, is there one or multiple interfaces for providing external services?

  ```
  One or more can be used, depending on the configuration. All nodes of the wap use an appdb.
  ```

* ## How many can the stress test support at the same time? 

  ```
  Deploy 4c 8GB wap service under EC2 (except MongoDB and nacos services + data volume), support the concurrent creation of 200 hosts and support the concurrent creation of 400 MongoDB nodes
  ```

* ## How long will the oplog be stored?

  ```
  Depends on the number of recovery days configured by the user, up to half a year and at least one day
  ```

* ## Which mongodbs does the host correspond to? Can it be put on one page?

  ```
  You can add it to the server later
  ```

* ## Every time a node is managed, a read permission is added to the user?

  ```
  User permissions should be managed one-to-one for each cluster, and users need to be given read permissions when adding nodes.
  ```

* ## Can the Home page be searched and displayed based on the cluster name?

  ```
  The homepage is equivalent to a large screen. You cannot select a cluster for display. You can only view the monitoring information for a specific cluster on the MongoDB page.
  ```

* ## If the CPU is high, can you tell which query caused the CPU to be high?

  ```
  This function is not supported. High CPU is often caused by many factors. The platform cannot provide SQL that directly causes high CPU.
  ```

* ## The data is too large. There are currently more than 200 nodes (customer portraits, user footprints, direct car customers). One node may be 1T+. Will the backup speed be affected?

  ```
  If there is only one backup (DDT) server, the full backup only supports full backup of one cluster at the same time. After the full backup is completed, incremental backup supports multiple clusters at the same time. The specific evaluation needs to be based on the resources of the backup (DDT) server.
  If the data dropped to disk is larger than 1T, the full backup may be interrupted. The official mongodb management tool opsmanager cannot fully back up such large data. Opsmanager will interrupt unfinished full backup tasks within two days by default.
  ```