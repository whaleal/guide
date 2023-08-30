# Host Issues

### Agent Jar Cannot Run

- When the agent jar cannot run, first check if you have Java environment installed on your host. If not, follow the [Java environment setup](../02-Usage/Host/AddHost.md) instructions.

### Host Abnormal Shutdown

- The platform will continuously monitor the status of each host that has been onboarded. If the platform shows that a host has abnormally shut down, first check if the host is running properly. If the host has shut down unexpectedly, take physical maintenance measures.
- If the host is running normally and hasn't actually shut down, check if the agent process is running properly. If the process has crashed or was killed abnormally, restart it.

### Cannot Connect to Server

- Check if the server side is functioning properly.
- Check if the agent ID is correct and restart if necessary.

### Insufficient Host Memory

- When creating clusters on a host, the platform allocates half of the available resources by default. If not properly configured, creating too many clusters can lead to host crashes.
- During cluster creation, configure an appropriate cache size in the advanced settings to prevent excessive resource consumption and waste.