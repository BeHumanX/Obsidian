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

##### A developer sauce

create a file with `nano /etc/nginx/sites-available/your_domain`

```
server{
	listen 80;
	listen [::]:80;
	server_name your_domain;
	return 301 https://$server_name$request_uri;
}
server {
    listen 443 ssl; 
    listen [::]:443 ssl;
	server_name your_domain;
	
	ssl_certificate /etc/ssl/your_domain;
	ssl_certificate_key /etc/ssl/your_domain;
	ssl_protocols TLSv1.2 TLSv1.3;
	ssl_prefer_server_ciphers on;
	ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
	sendfile off;
	tcp_nodelay on;
	absolute_redirect off;
	root /var/www/your_apps;
	index index.php index.html index.htm;
	# Logging
	access_log /var/log/nginx/hxqi.my.id.access.log;
	error_log /var/log/nginx/hxqi.my.id.error.log;
	# Deny access to .htaccess files (if applicable)
	location ~ /\.ht {
		deny all;
	}
	# Handle requests to the root path
	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}
    	# Handle PHP files
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php8.3-fpm.sock; # Use PHP 8.3 FPM socket
		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;	
		include fastcgi_params;
	}
	# Deny access to sensitive files
	location ~ /\.env$ {
		deny all;
		return 404;
	}
}
```
And also don't forget to add [[SSL]] so you can access the website through https