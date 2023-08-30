# Introduction to DDT (Document Data Transfer)

## Part 1: DDT Overview

DDT is a next-generation MongoDB database migration and synchronization tool developed by Shanghai Jinmu Information Technology Co., Ltd. (referred to as "Jinmu Information"). It is designed to meet various customer needs and leverages Jinmu Information's years of experience in MongoDB services and research and development.

DDT is a versatile data transfer software developed in JAVA that offers high robustness, high transferability, and high availability. It allows for fast and stable data migration, helping users with tasks such as data backup, real-time migration, disaster recovery, and more. Users can also customize configuration parameters to achieve efficient data transfer for different scenarios.

Given the limitations of the built-in primary-secondary synchronization in MongoDB replica sets for certain business scenarios, Jinmu Information developed the DDT synchronization tool. DDT can be used for instance-level, data center-level, and cross-data center replication, catering to disaster recovery and multi-active requirements.

Traditional MongoDB data synchronization is limited to data transfers between similar architectures. However, DDT supports data transfers between three types of architectures: standalone nodes, replica sets, and sharded clusters. This flexibility enables data synchronization between different types of architectures, such as from a standalone node to a sharded cluster or from a sharded cluster to a standalone node.

The core of DDT's real-time synchronization lies in its efficient parsing and application of the OPLOG log, allowing for high-performance and secure real-time synchronization. The source MongoDB can be a standalone instance, a replica set, or a sharded cluster, while the target can be a mongod or mongos instance. For replica sets, it's recommended to source data from secondary/hidden nodes to reduce the load on the primary node. For sharded clusters, each shard should connect to DDT.

## Part 2: Features

DDT is characterized by its simplicity, security, versatility, multiple functionalities, and high performance.

### 2.1 High Performance

#### Efficient Data Validation

- Ensures consistent data volume.
- Ensures consistent data information.
- Ensures consistent data indexes.
- Ensures consistent data structure.

#### Multiple Synchronization Scenarios

- Full data replication.
- Real-time data synchronization.
- Incremental data synchronization.
- Customizable synchronization scope.
- Composite data synchronization scenarios.

#### High-Speed Synchronization Mechanism

- Utilizes 100% of available bandwidth.
- Controlled CPU utilization.
- Configurable memory usage.
- Supports parallel synchronization of multiple tables.

#### Compact, Stable, and Efficient

- Compact in size.
- Supports seamless resume in case of interruption.
- Supports synchronization across multiple MongoDB versions.

### 2.2 Synchronization Modes

Synchronization Modes: Full, Real-time, Full and Incremental, Full and Real-time. Incremental synchronization refers to real-time synchronization with a specified time range for the Oplog.

- Full Synchronization: Splits source MongoDB collections for querying, and multithreadedly writes the queried data into the target MongoDB collections. In this mode, higher resource availability generally leads to higher QPS.

- Real-time Synchronization: Replicates data from the source MongoDB to another MongoDB to create redundant copies. It captures the oplog from the source MongoDB and replays it in the target MongoDB.

### 2.3 Resumable Transfer

In case of an unexpected source MongoDB shutdown, DDT can still synchronize data seamlessly upon restart. When DDT is unexpectedly closed, it can automatically resume from the last checkpoint and continue with the data transfer.

### 2.4 Multi-Version Support

DDT currently supports MongoDB versions 3.2 to 6.0. It reliably supports the synchronization of tables and bucket collections in newer versions.

### 2.5 DDL Operations

During real-time synchronization, users can customize the synchronization of certain DDL operations. Additionally, these DDL operations are recorded in logs for auditing purposes.

### 2.6 Oplog Delay

Oplog delay synchronization allows for easy failover in case of issues.

### 2.7 Synchronization Scope

In real-time synchronization, users can set the start and end times for synchronizing the Oplog within a specified time range.

There are additional features such as filtering the list of synchronized tables, data validation, and more.

## Part 3: Company Overview

Shanghai Jinmu Information Technology Co., Ltd. is a professional IT data consulting and service provider. The company is committed to delivering high-quality information products, consulting, and services to users. Established in 2015 in Shanghai, Jinmu Information has branches in Beijing, Shenzhen, and Guangzhou.

Jinmu Information is a core partner for MongoDB in the Greater China region and a core partner for Akamai and Vonage in China. The company provides professional technical services, consulting, and application development to clients.

As a technology-driven IT service provider prioritizing innovation and customer needs, Jinmu Information's products and services have gained recognition from leading domestic enterprises. The company has over 50 core clients and offers premium services and innovative product solutions in industries such as finance, insurance, securities, gaming, and e-commerce, covering mainland China and Hong Kong.

<div style="text-align: right">
        <p>Jinmu Information Website: www.jinmuinfo.com</p>
        <p>Consultation Email: support@jinmuinfo.com</p>
        <p>Contact Numbers: 021-58870038, 021-66696778</p>
</div>