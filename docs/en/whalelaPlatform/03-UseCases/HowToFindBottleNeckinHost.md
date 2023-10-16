## Find Bottleneck in Host

You can identify and address bottlenecks on a host using the following operations:

### Check the Monitor

On Linux systems, the primary bottlenecks are typically related to memory (RAM), computation (CPU), or I/O operations (disk). For memory, speed could be a factor, and running out of memory is a significant issue. For the CPU, if older hardware is used, the performance of each CPU core may be slow, and there might not be enough processing power. Regarding I/O, reading from mechanical hard drives and excessive disk writes can be problematic.

### CPU

Check CPU monitoring data to inspect CPU usage. If the CPU reaches 95% or more while memory (Mem) and swap (Swp) are within normal ranges, it indicates a CPU bottleneck.

If the application or process isn't running at the expected performance level and consistently shows 95%+ CPU utilization, you can take the following steps:

* **Immediate Solution**: Add more CPU cores to the server.
* **Troubleshooting**: Investigate and locate the problematic application and address the issues accordingly.

If adding more CPU cores still results in CPU utilization above 95%, but the application's performance and throughput improve, consider adding CPUs to address the problem. Otherwise, focus on troubleshooting issues within the application.

### RAM

Review RAM monitoring data. If Memory usage is at 100%, and Swap usage is at 50%, the system is likely swapping heavily. Swapping is the process of moving content between disk and main memory (using a specialized swap partition), and with Memory at 100%, the system will become significantly slower as it continues to swap.

For example, you might see that only 20% of memory is actively used, yet a lot of memory remains free. This might indicate that the operating system has moved some infrequently used memory regions to disk to optimize the main memory. As long as there is still plenty of free memory available, this situation is not a problem.

### I/O

When observing monitoring data and neither CPU nor RAM appear to be bottlenecks, you should focus on I/O.

For example, if you notice that I/O on an SSD is not very high, but there is heavy read/write I/O to an HDD, you'll need to address the I/O issue. This could involve actions such as stopping some excessive write operations, upgrading the I/O system, replacing slower I/O devices with faster ones, or upgrading to faster SSDs.