# Mongo Issues

### 集群创建失败

- 查看主机是否运行正常，排除主机问题。
- 查看节点使用端口是否重复，当端口被占用时则会创建失败。
- 查看数据目录是否有其他集群数据，当数据目录有其他数据文件配置时则会引起异常


### 复制集添加节点失败

- 添加节点时确保使用端口未被占用，端口被占用时会添加失败。
- 查看数据存放目录是否没有其他集群数据内容，有则清空或使用新目录进行添加。


### 版本升降级失败

- 升降级时确保目标版本高于当前版本，同理降级时确保目标版本低于当前版本。
- 版本的升降级不能进行跨版本操作，升降级只能在同版本下进行操作。<br>
（例如不能将4.x版本升级成5.x，可以将4.2升级为4.4，同理不能不能将5.x降级为4.x版本，可将4.4降级为4.2。）

### 开关认证失败

- 当前认证的开关都是关于admin的操作，无其他库的认证开关。
- 其认证方式只有username/password一种。

### 分片添加集群失败

- 一般集群的添加都要确保端口没有重复，同时data的目录内无其他集群的数据信息。
- 当前分片添加复制集config集群时不能添加仲裁节点与隐藏延时节点。


### 节点创建后显示无状态

- 点击操作更新节点信息即可。

### 集群中成员节点成为主节点后又变了回来

- 查看节点的优先级是否不同，当某个节点优先级较高时最终优先级较高的节点会成为主节点。


### 监控显示无数据

- 一些监控数据是在操作处开启才会进行数据的收集。
- 当前监控无数据，可进行时间范围的调整查看更多范围内的监控。

### 


