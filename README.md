# Convergent Website

## Setup
1. Get your AWS ec2 Instance setup (aws.amazon.com). Go with the default free tier options for everything.
2. ssh into your instance and Clone this repo
3. Run this command to start the server (MAKE SURE IT WORKS)
```shell
adonis serve --dev
```

### Getting the server to run after ssh logout
This must be done so that the website works even when your computer is off. You can use pm2 to do so.
1. Run this command
```shell 
npm install pm2 -g
```
2. Run this command
```shell 
pm2 start server.js
```
The server has now started! You must run this to stop it:
```shell 
pm2 stop all
```
Checkout pm2 documentation for more commands.

### Getting the port stuff resolved
Right now, the site requires a specific port to be accessed. We want to eliminate the need for a port number like 3333, 3000, 5000 etc. so we will get it working on the default port (80). We need nginx for this.

1. Run this command. If it gives an error, follow the error instructions for installation.
```shell
sudo yum install nginx
```
2. Change your AWS ec2 inbound rule to have the following port open: HTTP, TCP, Port 80, Source: 0.0.0.0/0

3. Now run this command
```shell
sudo nano /etc/nginx/nginx.conf
```

4. This opens nano, a text editor. Use nano to modify the file to look like this:
```javascript
server {
   listen         80 default_server;
   listen         [::]:80 default_server;
   server_name    localhost;
   root           /usr/share/nginx/html;
   location / {
       proxy_pass http://127.0.0.1:3000;
       proxy_http_version 1.1;
       proxy_set_header Upgrade $http_upgrade;
       proxy_set_header Connection 'upgrade';
       proxy_set_header Host $host;
       proxy_cache_bypass $http_upgrade;
   }
}
```

5. Finally, run this command:
```shell
sudo service nginx restart
```
