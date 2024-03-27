

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