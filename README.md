# Adonis fullstack application

This is the fullstack boilerplate for AdonisJs, it comes pre-configured with.

1. Bodyparser
2. Session
3. Authentication
4. Web security middleware
5. CORS
6. Edge template engine
7. Lucid ORM
8. Migrations and seeds

## Setup
1. Get your AWS ec2 Instance setup
2. Clone this repo
3. Run this command to start the server (MAKE SURE IT WORKS)
```shell
adonis serve --dev
```

### Getting the server to run after ssh logout
This must be done so that the website works even when your computer is off. You can use pm2 to do so.
1. ```shell 
npm install pm2 -g
```
2. 
