## MySQL Installation and Deployment

It is recommended to use MySQL version 8.0.

### Opening Specified Ports or Disabling Firewall

1. View the ports that are already open:
   ```bash
   firewall-cmd --list-ports
   ```

2. Open a specified port (e.g., port 3306 for MySQL):
   ```bash
   firewall-cmd --zone=public --add-port=3306/tcp --permanent
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

### Basic Environment Preparation

1. Create a user and group for MySQL:
   ```bash
   groupadd mysql
   useradd -r -g mysql -s /sbin/nologin mysql
   ```

2. Install dependencies for MySQL:
   ```bash
   yum install -y libncurses* libaio* lrzsz*
   ```

3. Extract the MySQL installation package:
   ```bash
   tar -xvf mysql-8.0.28-linux-glibc2.12-x86_64.tar -C /usr/local/
   ```

4. Rename the extracted directory:
   ```bash
   mv mysql-8.0.28-linux-glibc2.12-x86_64/ mysql
   ```

5. Create required directories:
   ```bash
   cd /usr/local/mysql/
   mkdir data
   ```

6. Change directory ownership:
   ```bash
   chown -R mysql:mysql /usr/local/mysql/
   ```

### Deploy MySQL Service

1. Initialize the database:
   ```bash
   /usr/local/mysql/bin/mysqld --user=mysql --basedir=/usr/local/mysql/ --datadir=/usr/local/mysql/data/ --initialize
   ```

2. Edit `my.cnf` configuration:
   Create/Edit the configuration file `/etc/my.cnf` and add the following content:
   ```
   [mysqld]
   basedir=/usr/local/mysql
   datadir=/usr/local/mysql/data
   socket=/usr/local/mysql/data/mysql.sock
   bind-address = 0.0.0.0
   user=root
   port=3306
   log-bin=mysql-bin
   server-id=1
   max_connections=2048
   character-set-server=utf8
   default-storage-engine=INNODB

   [client]
   socket=/usr/local/mysql/data/mysql.sock
   ```

3. Configure environment variables:
   ```bash
   echo "export PATH=$PATH:/usr/local/mysql/bin" >> /etc/profile
   source /etc/profile
   ```

4. Configure startup script:
   ```bash
   cp /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld
   chmod +x /etc/rc.d/init.d/mysqld

   cat > /lib/systemd/system/mysqld.service <<EOF
   [Unit]
   Description=mysqld
   After=network.target

   [Service]
   Type=forking
   ExecStart=/etc/rc.d/init.d/mysqld start
   ExecReload=/etc/rc.d/init.d/mysqld restart
   ExecStop=/etc/rc.d/init.d/mysqld stop
   PrivateTmp=true

   [Install]
   WantedBy=multi-user.target
   EOF
   ```

5. Reload systemd configuration:
   ```bash
   systemctl daemon-reload
   ```

6. Set MySQL to start on boot:
   ```bash
   systemctl enable mysqld
   ```

7. Start MySQL:
   ```bash
   systemctl start mysqld
   ```

8. Check if MySQL port is active:
   ```bash
   netstat -tunlp | grep 3306
   ```

### Configure Password for Remote Connection

1. Enter the printed password to log in to MySQL:
   ```bash
   mysql -u root -p
   ```

2. After logging in, change the root password:
   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
   ```

3. Check user information:
   ```sql
   select user, host, ssl_type from mysql.user;
   use mysql;
   ```

4. Update the host field to `%` to allow remote connections:
   ```sql
   update user set host = '%' where user = 'root';
   ```

5. Refresh privileges:
   ```sql
   flush privileges;
   ```

### Adding Archive Platform Fields

1. Log in to MySQL:
   ```bash
   mysql -u root -p
   ```

2. Create a database:
   ```sql
   create database filing;
   ```

3. Add data from the provided SQL file:
   ```sql
   use filing;
   source /usr/local/filing.sql;
   ```

4. Check the added tables:
   ```sql
   use filing;
   show tables;
   ```

As always, ensure that you adapt paths, filenames, and other specifics to match your system's configuration.