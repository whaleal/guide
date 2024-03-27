## Find BottleNeck In Host

```
Find BottleNeck In Host This can be done by doing the following：
 - Check the monitor
 - CPU
 - RAM
 - I/O
```

### Check the monitor

​			On Linux, the main bottlenecks are memory (RAM), compute (CPU), or I/O (disk operations). Speed may be a factor when it comes to memory, which is a big problem if you've run out of memory. With CPUs, if you're using older hardware, each CPU core will work much slower, and probably not enough. For I/O, reading from mechanical hard drives and excessive disk writes can be the problem.

### CPU

​			View CPU monitoring data to check CPU usage. While the application is providing services, if the CPU reaches more than 95% and the memory (Mem) and swap (Swp) are within the normal usage range, it proves that the CPU has reached a bottleneck.

​			If an application or process is not running at the correct performance level and you see a constant 95% + CPU utilization, you can do the following:

* Emergency solution: Increase the number of CPUs for the server
* Troubleshooting: Check and locate the application, and troubleshoot and solve the corresponding problems

​			If after increasing the number of CPUs, the CPU usage is still above 95%, but it provides better performance and throughput to the application service, then consider adding more CPUs to solve the problem. Otherwise, consider troubleshooting the problem in the application.

### RAM

​			Looking at the RAM monitoring data, if Memory is using 100% and Swap is using 50%, the system is almost certainly doing a lot of swapping. Swapping is the process of exchanging content between disk and main memory (using a special swap partition). Because Memory is used at 100%, once the system boots and continues to swap, it will become extremely slow.

​			For example, there might be 20% of memory in use, but a lot of memory remaining. This may indicate that the operating system has moved some infrequently used memory areas to disk to optimize main memory. Since there is still a lot of memory free, there is no problem with this situation.

### I/O

​			When we observe the monitoring data, we find that neither CPU nor RAM has reached the bottleneck. Next, we need to look at I/O.

​			For example, we see that the I/O in SSD is not very high, but the read and write I/O to HDD per second is quite intensive. In this case, we need to solve the I/O problem, such as stopping some rewriting and upgrading. I/O system, replace I/O devices with faster reading and writing, or replace with faster SSD.