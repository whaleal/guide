## Redis Installation and Deployment
### Opening Specified Ports or Disabling Firewall

1. View the ports that are already open:
   ```bash
   firewall-cmd --list-ports
   ```

2. Open a specified port (e.g., port 6379 for Redis):
   ```bash
   firewall-cmd --zone=public --add-port=6379/tcp --permanent
   ```

3. Reload the firewall configuration:
   ```bash
   firewall-cmd --reload
   ```

4. Confirm the opened ports:
   ```bash
   firewall-cmd --list-ports
   ```

5. If needed, you can stop the firewall:
   ```bash
   systemctl stop firewalld
   ```

6. Check the firewall status:
   ```bash
   systemctl status firewalld
   ```

### Installation and Deployment

1. Extract the Redis installation package:
   ```bash
   tar -zxvf redis-4.0.9.tar.gz -C /usr/local/
   ```

2. Rename the extracted folder:
   ```bash
   mv redis-4.0.9 redis
   ```

3. Install the required dependencies (e.g., GCC):
   ```bash
   yum install gcc -y
   ```

4. Compile the Redis files:
   ```bash
   cd /usr/local/redis
   make && make install
   ```

### Edit Configuration File

1. Edit the Redis configuration file:
   ```bash
   vi redis.conf
   ```

2. Set a password (e.g., "123456"):
   ```conf
   # Before
   # requirepass foobared
   
   # After
   requirepass 123456
   ```

3. Enable background daemon mode:
   ```conf
   # Before
   # daemonize no
   
   # After
   daemonize yes
   ```

4. Allow remote access:
   ```conf
   # Before
   # bind 127.0.0.1
   
   # After
   bind 0.0.0.0
   ```

5. Save the configuration file and exit the editor.

### Start Redis

1. Start Redis using the modified configuration file:
   ```bash
   redis-server /usr/local/redis/redis.conf
   ```

2. Validate the Redis server is running:
   ```bash
   redis-cli
   ```

Make sure to adjust paths, passwords, and other configurations as needed for your specific environment.