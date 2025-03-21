>NGINX is a high-performance, open-source web server, reverse proxy, and [[Load Balancer]].

### SSL/TLS encryption with let's encrypt
1. Update apt and install CertBot
```
   sudo apt update 
   sudo apt install software-properties-common 
   sudo add-apt-repository ppa:certbot/certbot 
   sudo apt update 
   sudo apt install certbot python3-certbot-nginx
```
2. Generate and renewing SSL certificates
	   `sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com`
3. Automated Renewal with cron
	   `sudo crontab -e`
	   `0 2 * * * /usr/bin/certbot renew --quiet`
##### Extra step for security
By adding this inside a server block in `/etc/nginx/nginx.conf`
- Disabling server token with `server_tokens off;` 
- Configuring strong ssl policy with `ssl_protocols TLSv1.2 TLSv1.3;` 
- Rate limiting with `limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;`
- Configuring the fail2ban:
	-`sudo apt install fail2ban`
	-`sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
	-`sudo systemctl restart fail2ban`

#### Setting Up an Nginx [[Reverse Proxy]]
the steps:
1. Update apt and install [[Nginx|Nginx webserver]]
2. Disable default preconfigured virtual host
	   `sudo unlink /etc/nginx/sites-enabled/default`
3. Create reverse-proxy configuration file at `/etc/nginx/sites-available`
	   `cd /etc/nginx/sites-available`
	   `nano reverse-proxy.conf`
4. Add the reverse proxy configuration
```
	   server {  
listen 80;  
server_name example.com *.example.com;  
  
access_log /var/log/nginx/reverse-access.log;  
error_log /var/log/nginx/reverse-error.log;  
  
location / {  
proxy_pass http://127.0.0.1:5001;  
}  
}
```
5. Create symbolic link.
```
   sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf 
   /etc/nginx/sites-enabled/reverse-proxy.conf
```