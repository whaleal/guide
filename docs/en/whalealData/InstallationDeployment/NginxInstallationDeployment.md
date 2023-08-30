## Nginx Installation and Deployment

### Opening Specified Ports or Disabling Firewall

1. View the ports that are already open:
   ```bash
   firewall-cmd --list-ports
   ```

2. Open a specified port (e.g., port 80 for Nginx):
   ```bash
   firewall-cmd --zone=public --add-port=80/tcp --permanent
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

1. Extract the Nginx installation package:
   ```bash
   tar -zxvf nginx-1.16.1.tar.gz -C /usr/local/
   ```

2. Install dependencies:
   ```bash
   yum install -y pcre pcre-devel
   yum install -y zlib zlib-devel
   ```

3. Configure the installation path:
   ```bash
   cd /usr/local/nginx-1.16.1
   ./configure --prefix=/usr/local/nginx
   ```

4. Compile Nginx:
   ```bash
   make && make install
   ```

5. Configure local hostname resolution:
   Edit `/etc/hosts` and add an entry for your local domain:
   ```
   ip cloud.whalealmg.com
   ```

6. Edit the Nginx configuration file:
   ```nginx
   server {
       listen 80;
       server_name cloud.whalealmg.com;

       location / {
           root /usr/local/nginx/html/dist/;
           index index.html index.htm;
           try_files $uri $uri/ /index.html;
       }

       location /filingAdmin/ {
           proxy_pass http://127.0.0.1:8000/;
           proxy_set_header X-Forwarded-Proto $scheme;
           proxy_set_header X-Forwarded-Port $server_port;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection "upgrade";
       }

       location ~ .*\.(js|css|jpg|jpeg|gif|png|ico|pdf|txt)$ {
           root /usr/local/nginx/html/dist/;
           index index.html index.htm;
       }

       error_page 500 502 503 504 /50x.html;
       location = /50x.html {
           root html;
       }
   }
   ```

7. Start the Nginx service:
   ```bash
   /usr/local/nginx/sbin/nginx
   ```

Make sure to adjust paths, domain names, and other configurations as needed for your specific environment.