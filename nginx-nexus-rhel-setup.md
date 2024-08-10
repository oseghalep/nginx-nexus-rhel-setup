## Steps for Using NGINX to Terminate SSL Traffic for Nexus
## Prerequisites
1. NGINX Installed: Ensure NGINX is installed on your RHEL  server (follow the previous installation steps).
2. Nexus Installed: Ensure Nexus Repository Manager is installed and running on your server.
3. SSL Certificate: Obtain a valid SSL certificate (from a Certificate Authority or generate a self-signed certificate).

## Step 1: Configure SSL Certificate in NGINX
Create a Directory for SSL Certificates:
sudo mkdir -p /etc/nginx/ssl

Place Your SSL Certificate and Key in the Directory:
ssl_certificate: Path to your SSL certificate file.
ssl_certificate_key: Path to your SSL private key.
Example:
sudo cp /path/to/your/certificate.crt /etc/nginx/ssl/nexus.crt
sudo cp /path/to/your/private.key /etc/nginx/ssl/nexus.key

Set Permissions:
sudo chmod 600 /etc/nginx/ssl/nexus.key

## Step 2: Configure NGINX as a Reverse Proxy with SSL Termination
Edit NGINX Configuration:
Open the default server block configuration file or create a new one:
sudo vi /etc/nginx/conf.d/nexus.conf

Add the Following Configuration:
Replace nexus.example.com with your domain name, and adjust the SSL paths if necessary:
# ..........
nginx
Copy code
server {
    listen 80;
    server_name nexus.example.com;

    # Redirect all HTTP traffic to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name nexus.example.com;

    ssl_certificate /etc/nginx/ssl/nexus.crt;
    ssl_certificate_key /etc/nginx/ssl/nexus.key;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Nexus reverse proxy settings
    location / {
        proxy_pass http://localhost:8081;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Increase buffer size for large Nexus files
    client_max_body_size 1G;
    proxy_buffer_size 128k;
    proxy_buffers 4 256k;
    proxy_busy_buffers_size 256k;
}
# ..........
Save and Exit the File.

## Step 3: Adjust Nexus Configuration
Ensure Nexus Is Only Listening on localhost:
By default, Nexus listens on all interfaces. Restrict it to localhost to ensure it only accepts traffic from NGINX.
Edit the Nexus application.properties file.
sudo vi /opt/nexus/nexus-3.70.1-02/etc/nexus-default.properties


Modify the nexus.web.http.host setting:
nexus.web.http.host=127.0.0.1
nexus.web.http.port=8081

Restart Nexus:
sudo systemctl restart nexus

## Step 4: Restart NGINX
After making the changes, restart NGINX to apply the configuration:
sudo systemctl restart nginx

## Step 5: Adjust Firewall Rules
Ensure that only HTTPS traffic is allowed:
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --remove-service=http --permanent
sudo firewall-cmd --reload

## Step 6: Verify the Setup
Open a browser and navigate to https://nexus.example.com.
Ensure that Nexus is accessible only via HTTPS and that HTTP traffic is redirected to HTTPS.

Additional Considerations
Security Enhancements: You may consider configuring HSTS (HTTP Strict Transport Security) and enabling additional SSL/TLS security settings.
Automatic Certificate Renewal: If using Let's Encrypt, consider setting up automatic certificate renewal with certbot.
This will ensure that Nexus is securely served over HTTPS, with NGINX handling the SSL termination.
