## Installation and Deployment of Whaleal-data

### High Availability Deployment

To achieve high availability, deploy the service on multiple machines and distribute traffic through a load balancer to balance and share the requests. Common load balancing algorithms include round-robin, least connections, and hash algorithms. Use multiple servers with the same configuration to maintain system continuity by having other servers take over in case of a failure. Common redundancy backup modes include master-slave mode, active-active mode, and N+1 mode.

### Package Deployment

#### Frontend Service Startup

1. After compiling the source code, generate the "dist" distribution package.
2. Send the "dist" package to the server.
3. Path: The installation path configured in the Nginx configuration.

#### Restart Nginx

```bash
/usr/local/nginx/sbin/nginx -s reload -t
```

#### Backend Service Startup

1. After compiling the source code, generate the "filing-system-0.0.1-SNAPSHOT.jar" distribution package.
2. Upload the distribution package to the server.
3. Edit the configuration file "application.yml".

#### Configuration File Content

```yaml
# Application server port
server:
  port: 8000

# Database and other configurations...
```

#### Start the Service

```bash
nohup java -jar -Xms2048M -Xmx20000M -XX:PermSize=768M -XX:MaxPermSize=1536M -server -jar filing-system-0.0.1-SNAPSHOT.jar --spring.config.location=application.yml --jasypt.encryptor.password=SfXlqZmK4P257 &
```

#### Check Logs for Successful Startup

```bash
tail -f nohup.out
```

### Docker Container Deployment

1. Navigate to the directory containing the `docker-compose.yml` file.
2. Start the service using the command: `docker-compose up -d`.

After the Docker service starts successfully, you can view the logs using the command: `docker logs -f root_whaleal-data_1`.

For local access, bind the server's IP with the domain name in the hosts file using: `sudo sh -c 'echo "docker_server_ip whaleal-data.com" >> /etc/hosts'`.

Access the Whaleal-data service:

- Web URL: `http://docker_server_ip` or `http://whaleal-data.com`
- Initial login:
    - User: "admin"
    - Password: "123456"
    - The system will force you to change the password upon first login.

Tips:
Cold Data Archiving:
The default path for cold data archiving is `/whalealdb`. For Docker, the service is mapped to an external path `/opt/whalealdb`.

### Quick Access

Start the Whaleal-data service using Docker containers. This service depends on `mysql`, `mongodb`, `redis`, and `zookeeper` services. It runs in a local browser through the `nginx` service proxy.