## Zookeeper Installation and Deployment

### Opening Specific Ports or Disabling Firewall

1. Check already opened ports: `firewall-cmd --list-ports`
2. Open a specific port: `firewall-cmd --zone=public --add-port=2181/tcp --permanent`
3. Reload firewall configuration: `firewall-cmd --reload`
4. Confirm opened ports: `firewall-cmd --list-ports`
5. Stop the firewall: `systemctl stop firewalld`
6. Check firewall status: `systemctl status firewalld`

### Installation and Deployment

1. Unpack the installation package: `tar -zxvf apache-zookeeper-3.6.1-bin.tar.gz -C /usr/local/`
2. Rename the extracted folder: `mv apache-zookeeper-3.6.1-bin/ zookeeper`
3. Start Zookeeper: `/usr/local/zookeeper/bin/zkServer.sh start /usr/local/zookeeper/conf/zoo_sample.cfg`
4. Verify Zookeeper status: `/usr/local/zookeeper/bin/zkServer.sh status /usr/local/zookeeper/conf/zoo_sample.cfg`

This installation guide provides steps for deploying Zookeeper, opening the required ports, and starting the service. Make sure to follow each step carefully to ensure a successful deployment.