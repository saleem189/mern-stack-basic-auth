# mern-stack-auth-example

![image](https://user-images.githubusercontent.com/75361545/236814024-c2bd3218-997e-4e94-874b-1fd58191eca4.png)

![image](https://user-images.githubusercontent.com/75361545/236813675-cab43f59-795e-447c-9a72-d1e4b4007746.png)
![image](https://user-images.githubusercontent.com/75361545/236813829-5877b5be-aeca-4fc7-871e-4c3a79ef2b0e.png)

Minimal full-stack MERN app with authentication using passport and JWTs.

This project uses the following technologies:

- [React](https://reactjs.org) and [React Router](https://reacttraining.com/react-router/) for frontend
- [Express](http://expressjs.com/) and [Node](https://nodejs.org/en/) for the backend
- [MongoDB](https://www.mongodb.com/) for the database
- [Redux](https://redux.js.org/basics/usagewithreact) for state management between React components

## Configuration

Make sure to add your own `MONGOURI` from your database in `config/keys.js`.

```javascript
module.exports = {
  mongoURI: "YOUR_MONGO_URI_HERE",          //example  "mongodb://localhost:27017/database_name" OR "mongodb://127.0.0.1:27017/database_name"
  secretOrKey: "secret" //any secret you want to provide like "root"
};
```

## Quick Start

```javascript
// Install dependencies for server & client
npm install && npm run client-install

// You can also run these commands separately
  navigate to project folder and run 
      npm install
  then navigate to client folder in Project
      npm install
      
// Run client & server with concurrently
npm run dev

// Server runs on http://localhost:5000 and client on http://localhost:3000
```

## setting up on server 
  Setup/launch amazon ec2 instance
  
## configuring server 
run this directly 
```
sudo curl https://gist.githubusercontent.com/saleem189/7feda6ab97a09fa95558e2da9eb19c92/raw/cd951a133e5638cb246d877623b73d0d6a80375e/setup-nodejs-mongodb-production-server-on-ubuntu-1804.sh | bash
```

or write form here 
```
#!/usr/bin/env bash

echo "
----------------------
  NODE & NPM
----------------------
"

# add nodejs 18 ppa (personal package archive) from nodesource
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -

# install nodejs and npm
sudo apt-get install -y nodejs


echo "
----------------------
  MONGODB
----------------------
"
# Import the public key used by the package management system.
sudo apt-get install gnupg

# Issue the following command to import the MongoDB public GPG Key from https://pgp.mongodb.com/server-6.0.asc
curl -fsSL https://pgp.mongodb.com/server-6.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg \
   --dearmor
   


# Create the /etc/apt/sources.list.d/mongodb-org-6.0.list file for Ubuntu 22.04 (Jammy):
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# reload local package database
sudo apt-get update

# install the latest version of mongodb
sudo apt-get install -y mongodb-org

# start mongodb
sudo systemctl start mongod

# set mongodb to start automatically on system startup
sudo systemctl enable mongod


#create new database commands to create dbs in mongo
# type      mongosh       in Linux terminal  
#when mongosh is open then type        `use database_name` after that `db.myCollection.insertOne( { x: 1 } );` 

echo "
----------------------
  NODEMON
----------------------
"
# you can change this line as you want but i added noedmon in devdependinces
# Install nodemon globally: Once you have Node.js installed, you can install nodemon globally by running the following command:
#npm install -g nodemon

echo "
----------------------
  PM2
----------------------
"

# install pm2 with npm
sudo npm install -g pm2

# set pm2 to start automatically on system startup
sudo pm2 startup systemd


echo "
----------------------
  NGINX
----------------------
"

# install nginx
sudo apt-get install -y nginx


echo "
----------------------
  UFW (FIREWALL)
----------------------
"

# allow ssh connections through firewall
sudo ufw allow OpenSSH

# allow http & https through firewall
sudo ufw allow 'Nginx Full'

# enable firewall
sudo ufw --force enable
```

## install dependincies of app
navigate to folder
```
sudo npm install
```
navigate to client foler in project 
```
sudo npm install
```
and in client foler run
```
sudo npm run build
```
[read more about pm2](https://pm2.keymetrics.io/)
## running backend using PM2. Process Manager 2 is a production process manager for Node.js applications. It provides a set of features to manage and monitor Node.js processes in a production environment. PM2 is designed to ensure high availability and performance for applications running on a server.
navigate to project foler (backend where server.js is present "not client ----which is subfolder ")
```
sudo pm2 start server.js
```
## setting up nginx configuration (basic for this project)
### first remove default nginx site-avaliables config
```
sudo rm /etc/nginx/sites-available/default
```

### create new file and add below configurations init
```
sudo nano /etc/nginx/sites-available/default
```
```
server {
  listen 80 default_server;
  server_name _;

  # react app & front-end files
  location / {
    root /opt/mern-stack-basic-auth/client/build;
    try_files $uri /index.html;
  }

  # node api reverse proxy
  location /api/ {
    proxy_pass http://localhost:5000;
  }
}
```
restart nginx 
```
sudo systemctl restart nginx
```

## snippets from amazon ec2 instace
![image](https://github.com/saleem189/mern-stack-basic-auth/assets/75361545/de7e4c97-2713-418c-a45f-415b1f548662)

#mern-app snippets
![image](https://github.com/saleem189/mern-stack-basic-auth/assets/75361545/fd339d80-d280-4464-9320-f8c466c11a37)




