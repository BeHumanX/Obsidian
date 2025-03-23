### What is Cloudflare?
Cloudflare is a could service that helps Security, Performance, DNS, Developer Services and Control of a Network.

Cloudflare offer lots of services, such as DNS,Emailing,[[SSL]]/TLS,Security,Tunnels and more 

### Setup Cloudflare [[SSL]]
1.Go To Cloudflare Dashboard
2.Go To SSL/TSL menu
3.Click Origin Server
4.Click Create Certificate
5.Input List of hostnames that gonna use the certificates
6.Copy the Certificate key and put it inside `/etc/ssl/yourdomain.pem`
7.Do the same but for Certificate Private key and put it inside `/etc/ssl/yourdomain.key`
