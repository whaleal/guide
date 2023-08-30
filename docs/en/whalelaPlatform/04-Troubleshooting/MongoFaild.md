# Mongo Issues

### Creation Failed

- Check if the host is running properly.
- Verify that the port used by the node is not already in use.
- Ensure that the data directory doesn't contain data from other clusters.

### Replica Set Initialization Failed

- If replica set initialization fails, manual initialization can be performed.

### Failed to Add Replica Set Node

- When adding a node, make sure the port is not already in use.
- Check if the data storage directory contains data from other clusters.

### Version Upgrade/Downgrade Failed

- During version upgrades/downgrades, ensure that the target version is higher than the current version for upgrades and lower for downgrades.
- Version upgrades/downgrades must be done sequentially and cannot skip versions.
  (For example, you cannot directly upgrade from version 4.2 to 5.0. You would first upgrade to 4.4, then to 5.0. Similarly, downgrading from 5.0 to 4.2 is not allowed. You would first downgrade to 4.4, then to 4.2.)
- If upgrading an arbiter node in a replica set fails, manually replace the arbiter node's data directory.

### Authentication Enable/Disable Failed

- Authentication toggles are only available for the "admin" database and use the username/password method.

### Sharded Cluster Addition Failed

- Ensure that port conflicts are resolved and that the data directory does not contain data from other clusters.
- When adding a replica set to a sharded cluster, arbiters and hidden delay nodes cannot be added.

### Node Showing "No State" After Creation

- Clicking the "Update Node Information" button will resolve this.

### Member Node Becomes Primary and Reverts

- Check if the nodes have different priority settings. A higher-priority node will become the primary node.

### Monitoring Displays No Data

- Some monitoring data is collected only after specific actions are performed.
- If there's no data in monitoring, adjust the time range to view more data.

### Sharding Addition Failed

- Check if ports or data directories are already in use. If so, replace them.

### Authentication Deactivation Failed

- The cluster may not be accessible externally, requiring manual startup.

### Hidden Delay Node Operation Abnormality

- When a cluster with hidden delay nodes has authentication enabled, abnormal operations can occur. This is because the state of the primary node must be synchronized with the hidden delay nodes after the delay period.