# Whaleal Platform ChangeLog

### Whaleal Platform V1.0.0

Whaleal Platform V1.0.0 is the initial release version of the platform. It includes the following functional modules:

#### 1. Login and Registration

- Registration

  User registration only requires basic format validation and checks for existing accounts. It's recommended to provide a phone number (limited to mainland China) and an email address.

- Login

  Login methods include phone number + password, email + password, and account + password.

#### 2. Dashboard

- Host Overview

  - Displays the status of hosts, CPU, memory, and disk in a pie chart.

- Host Summary

  - Displays detailed information about CPU, memory, disk, network in/out, and other metrics in graphical form.

- Mongo Overview

  - Displays real-time information about MongoDB nodes, clusters, and cluster types in a pie chart.

- MongoDB Summary

  - Displays summary data for clusters, collections, crashed nodes, QPS, connections, and slowest queries in graphical form.

#### 3. Host List

- Host Statistics

  - Displays general information about managed hosts and allows actions like detaching a host or updating its data.

- Add Host

  - Allows adding new hosts, with details about the process in the [AddHost](../02-Usage/Host/AddHost.md) section.

- Host Information

  - Clicking on a host's name opens a detailed page with information about the host, including monitoring, logs, commands, and alerts. More details can be found in [HostInfos](../02-Usage/Host/HostInfos.md).

#### 4. MongoDB List

- MongoDB Static Information

  - Displays information about managed MongoDB clusters. You can search for clusters and perform various operations, such as updating node information, starting, stopping, restarting, detaching from management, and renaming.

- Create Project

  - Allows creating different types of MongoDB clusters. Cluster types include standalone, replica set, and sharded cluster. You can also manage existing clusters.
    - Detailed steps for creating a standalone deployment --> [CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
    - Detailed steps for creating a replica set --> [CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
    - Detailed steps for creating a sharded cluster --> [CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)

- MongoDB Cluster Operations

- MongoDB Media Package Management

  - When creating a cluster, you can select different MongoDB versions. You can upload MongoDB media packages using the MongoTars page.
    - Detailed steps for uploading a media package --> [UploadMongoTar](../02-Usage/MongoDB/UploadMongoTar.md)

#### 5. User Center

- Personal Center

  - Displays personal information provided during registration and allows updates and additions.

- User Management

  - User management is accessible only to the "admin" account. This page allows user deletion and role assignment.
    - Clicking on a username opens a user's resource page, where you can manage their permissions, such as adding hosts and creating clusters. On the Server and Mongo pages, you can show or hide specific hosts or clusters for the user.

- Account Configuration

  - Account configuration lets you set the time zone and choose whether to receive alert notifications.

#### 6. Support & Help

- [Documentation Column](https://docs.whaleal.com/)
  - Whaleal Community Documentation

- [Community Address](https://www.whaleal.com/)
  - Whaleal Community

---

##### Whaleal Platform Agent V1.0.0

```



```