## Host information


```
Host information Has the following content：
 - Host basic information
 - Host updates and removals
 - Host details and operations
```


### Host basic information

Basic information display of the host

a.host name

b.system message

c.host kernel

d.Host agent survival time

e.Host Status

f.Host-specific operations

<br>



#### Host updates and removals

Demanage the host and update the host information

a.The host will be removed after leaving the management, detailed operation--> [RemoveHost](RemoveHost.md)

b.Updating the host information is to obtain the host information again, and then update the page content. Its main content is the static information of the host, its monitoring data and the status of the host.。<br> 
(Due to the abnormal downtime of the host, the front end will not directly update the status of the host after manual restart. Clicking Update Host Information will refresh the host status.)

<br>


### Host details and operations

Click the host name to enter the host information page to view host details and operations.

a.Host information

    Mainly displays some basic static information of the host

![img_5.png](/Users/jinmu/Desktop/guide/images/whalealPlatformImages/infomation.png)

<br>

b.monitor

    Monitoring information graphically displays some information about MEMORY, CPU, NET, and DISKIO.
    （1）You can choose to display graphic data in different time ranges, or display graphic data in different granularities within a time range.
    （2）Data can be hidden and displayed by clicking the graphic button.
    （3）Click the question mark icon to the right of the indicator name to view indicator details.

![img_7.png](/Users/jinmu/Desktop/guide/images/whalealPlatformImages/monitor.png)

<br>

c.log


    The log records the activities of the host, including the operator's operations, regularly executed tasks, etc. Display specific execution events, event execution status and execution details.（1）处是对日志的筛选功能，比如只看某Time period or log information of a certain type or with certain content.
    （2）The searched log information is displayed on the front-end page.

![img_8.png](/Users/jinmu/Desktop/guide/images/whalealPlatformImages/host_log.png)

<br>

d.命令

    命令即对主机层面的操作或对mongo集群的操作，其操作状态、内容、事件、结果与操作事件等一同显示。
    操作MSG：显示操作的功能，包括主机操作与人为操作。
    状态：操作不同功能时各阶段的状态（实时更新）。
    内容：点击查看详情可以查看到集群的详细内容等。
    事件：事件包括主机的操作事件与操作者的操作事件（在前端页面的操作会有事件组日志，可点击查看详情查看事件的执行过程）。
    （1）处对是过滤条件的设置，可以模糊查询MSG内容与对时间范围内的命令进行显示。
    （2）处点击查看详情可显示JSON格式的命令详细信息。
    （3）处点事件组日志可查看详细的事件执行情况。


![img_9.png](/Users/jinmu/Desktop/guide/images/whalealPlatformImages/host_command.png)



