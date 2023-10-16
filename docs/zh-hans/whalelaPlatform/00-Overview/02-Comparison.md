## Popular Solution

#### MongoDB Ops Manager Server

```
Safely, securely, and seamlessly manage MongoDB in your own environment. Available through the MongoDB Enterprise Advanced subscription, Ops Manager eliminates operational overhead by automating key administration tasks such as deployment, upgrades, and more.
```

- Monitoring
> Monitor, visualize, and alert on 100+ performance metrics

- Backup
> Capture continuous, incremental backups, with point-in-time recovery

- Automation
> Perform single-click installations, upgrades, and index maintenance, with zero downtime

- Query Optimization
> Seamlessly identify and address slow-running queries with the Visual Query Profiler, index suggestions, and automated index roll-outs

#### Zabbix 
```
Zabbix is an open source monitoring software tool for diverse IT components, including networks, servers, virtual machines (VMs) and cloud services. Zabbix provides monitoring metrics, such as network utilization, CPU load and disk space consumption.
```

> collect from any source

> flexible metric collection

> agent/agent-less mointoring

> custom collection method

#### Percona Monitoring and Management
```
Percona Monitoring and Management Percona Monitoring and Management (PMM) is an open source database monitoring, management, and observability solution for MySQL, PostgreSQL, and MongoDB.

It allows you to observe the health of your database systems, explore new patterns in their behavior, troubleshoot them and perform database management operations no matter where they are located - on-prem or in the cloud.
```

> PMM collects thousands of out-of-the-box performance metrics from databases and their hosts.

> The PMM web UI visualizes data in dashboards.

> Additional features include advisors for database health assessments.


#### Homogeneous Comparison

```
基于如上信息, 进行同类横向对比
```

|     |Ops Manager  | Zabbix   |PMM  |WAP  |
|  :----:  | :----:  |:----: | :----: |:----: |
| 变更管理  | √ |× |× |√ |
| 监控告警  | 详细 | 一般 | 详细 | 详细 |
| 备份恢复  | √ | × | 其他方案 | 其他方案 |
| 使用限制  | 企业版 | 开源 | 开源 | 开源 |
| 优势点  | 官方工具、最全面的平台 | 企业最广泛的监控平台，易集成其他组件； | 开源MySQL的监控平台，集成了MongoDB； | 多年的排障经验沉淀，更符合国人的使用习惯 |
| 劣势点  | 要求对MongoDB一定了解，使用门槛偏高；| 指标不够详细，不易排查诊断； |Dashboard过多，很难直观排查；  | 现阶段仅支持CentOS6/7/8 |


