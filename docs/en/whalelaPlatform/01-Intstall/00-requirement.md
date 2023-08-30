## Pre-Flight Check

Before installing Whaleal Platform (WAP), you need to review the following materials:
- Server Requirement
- Agent Requirement

### Server Requirement

#### Hardware Requirement

All hosts that install the following Whaleal Platform (WAP) components must meet RAM and Disk requirements:

* Whaleal Platform Application
* Whaleal Platform Application Databases

**Whaleal Platform Application Hardware Requirement**

All hosts deploying Whaleal Platform Application must meet the following hardware requirements:

| Number of Monitored Nodes | CPU         | Memory     | Disk               |
| ------------------------- | ----------- | ---------- | ------------------ |
| 50                        | 4+          | 8GB+       | 10GB + logs storage |
| 200                       | 8+          | 16GB+      | 10GB + logs storage |
| 200+                      | Contact Whaleal Team | Contact Whaleal Team | Contact Whaleal Team |

**Whaleal Platform Application Database Hardware Requirement**

All hosts deploying Whaleal Platform Application Database must meet the following hardware requirements:

| Number of Monitored Nodes | CPU         | Memory     | Disk               |
| ------------------------- | ----------- | ---------- | ------------------ |
| 50                        | 4+          | 8GB+       | 256GB              |
| 200                       | 8+          | 16GB+      | 512GB              |
| 200+                      | Contact Whaleal Team | Contact Whaleal Team | Contact Whaleal Team |

> For better performance, it is recommended to use:
>
> * SSD for Application Database storage
> * WiredTiger storage engine for Application Database

#### Software Requirement

**Java Environment Requirement**

| JAVA     | Version |
| -------- | ------- |
| jdk      | 1.8.x   |
| open-jdk | 1.8.x   |

**Operating System Compatibility**

Whaleal Platform Application must be deployed on a 64-bit operating system.

| Operating System         | Version        |
| ------------------------ | -------------- |
| Red Hat Enterprise Linux | 6.x, 7.x, 8.x |
| CentOS                   | 6.x, 7.x, 8.x |

#### Network Security

**TCP Connection Requirement**

All Whaleal Platform Application services must be able to communicate properly with the following services:

* Whaleal Platform Application Database
* Whaleal Platform Application Agent Monitor MongoDB

**Hosts**

To ensure the principle of "out-of-the-box" use, Whaleal Platform Application uses the domain name cloud.whaleal.com to provide services externally.

All hosts that access Whaleal Platform Application must configure host resolution:

```
Whaleal_Platform_Application_IP cloud.whaleal.com
```

**Port**

Whaleal Platform Application must meet the following basic requirements:

* Users and Whaleal Platform Application Agent must be able to access via HTTP/HTTPS requests
* Whaleal Platform Application must be able to access Whaleal Platform Application Database
* All Whaleal Platform Application and Whaleal Platform Application Agent must be able to access the monitored MongoDB services
* Whaleal Platform Application must be able to send messages to users via email, SMS, and DingTalk

Therefore, Whaleal Platform Application must have the following ports open:

| Service          | Default Port | Transport | Direction | Description |
| ---------------- | ------------ | --------- | --------- | ----------- |
| HTTP             | 8080         | TCP       | Inbound   |             |
| HTTPS            | 8443         | TCP       | Inbound   |             |
| Whaleal Platform | 9600         | TCP       | Inbound   |             |
| MongoDB          | 27017        | TCP       | Outbound  |             |
| SMTP             | 587          | TCP       | Outbound  |             |
| SMS              |              | TCP       | Outbound  |             |
| DingTalk         |              | TCP       | Outbound  |             |

> For custom ports, please open the specified ports.

**Ports on Host**

Whaleal Platform Application can complete most operations, but some processes require administrator access to the Whaleal Platform Application host to complete. Therefore, the following port must be open:

| Service | Default Port | Transport | Direction | Description |
| ------- | ------------ | --------- | --------- | ----------- |
| ssh     | 22           | TCP       | Inbound   |             |

### Agent Requirement

#### Hardware Requirement

All hosts that install the following Whaleal Platform (WAP) components must meet RAM and Disk requirements:

* Whaleal Platform Application Agent

**Whaleal Platform Application Agent Hardware Requirement**

All hosts deploying Whaleal Platform Application Agent must meet the following hardware requirements:

| Number of Managed/Monitored Nodes | CPU         | Memory     | Disk               |
| ---------------------------------- | ----------- | ---------- | ------------------ |
| 1                                  | 1+          | 2GB+       | 2GB + logs storage |
| 5                                  | 2+          | 4GB+       | 2GB + logs storage |
| 5+                                 | Contact Whaleal Team | Contact Whaleal Team | Contact Whaleal Team |

#### Software Requirement

**Java Environment Requirement**

| JAVA     | Version |
| -------- | ------- |
| jdk      | 1.8.x   |
| open-jdk | 1.8.x   |

**Operating System Compatibility**

Whaleal Platform Application Agent must be deployed on a 64-bit operating system.

| Operating System         | Version        |
| ------------------------ | -------------- |
| Red Hat Enterprise Linux | 6.x, 7.x, 8.x |
| CentOS                   | 6.x, 7.x, 8.x |

#### Network Security

**TCP Connection Requirement**

All Whaleal Platform Application services must be able to communicate properly with the following services:

* Whaleal Platform Application Database
* Whaleal Platform Application Agent Monitor MongoDB

**Hosts**

To ensure the principle of "out-of-the-box" use, Whaleal Platform Application uses the domain name cloud.whaleal.com to provide services externally.

All hosts that access Whaleal Platform Application must configure host resolution:

```
Whaleal_Platform_Application_IP cloud.whaleal.com
```

**Port**

Whaleal Platform Application Agent must meet the following basic requirements:

* Users and Whaleal Platform Application must be able to access the server and MongoDB

Therefore, Whaleal Platform Application Agent must have the following ports open:

| Service          | Default Port | Transport | Direction         | Description |
| ---------------- | ------------ | --------- | ----------------- | ----------- |
| Whaleal Platform | 9600         | TCP       | Outbound          |             |
| MongoDB          | 27017        | TCP       | Inbound, Outbound |             |

> For custom ports, please open the specified ports.

**Ports on Host**

Whaleal Platform Application Agent can complete most operations, but some processes require administrator access to the Whaleal Platform Application host to complete. Therefore, the following port must be open:

| Service | Default Port | Transport | Direction | Description |
| ------- | ------------ | --------- | --------- | ----------- |
| ssh     | 22           | TCP       | Inbound   |             |