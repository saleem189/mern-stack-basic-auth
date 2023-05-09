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

// Run client & server with concurrently
npm run dev

// Server runs on http://localhost:5000 and client on http://localhost:3000
```
