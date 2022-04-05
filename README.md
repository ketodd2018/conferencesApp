# Conferences App

For our tutorial A RESTful API generated by [generator-rest](https://github.com/diegohaz/generator-rest).

See the API's [documentation](DOCS.md).

## Running locally

First, you will need to install and run [MongoDB](https://www.mongodb.com/) in another terminal instance.

```bash
$ mongod
```

After cloning this repo

```bash
$ cd conferencesApp && npm install
```

Then, run the server in development mode.

```bash
$ npm run dev
Express server listening on http://0.0.0.0:9000, in development mode
```

If you choose to generate the authentication API, you can start to play with it.

> Note that creating and authenticating users needs a master key (which is defined in the `.env` file)

Create a user (sign up):

```bash
curl -X POST http://0.0.0.0:9000/users -i -d "email=test@example.com&password=123456&access_token=MASTER_KEY_HERE"
```

It will return something like:

```bash
HTTP/1.1 201 Created
...
{
  "id": "57d8160eabfa186c7887a8d3",
  "name": "test",
  "picture":"https://gravatar.com/avatar/55502f40dc8b7c769880b10874abc9d0?d=identicon",
  "email": "test@example.com",
  "createdAt": "2016-09-13T15:06:54.633Z"
}
```

Authenticate the user (sign in):

```bash
curl -X POST http://0.0.0.0:9000/auth -i -u test@example.com:123456 -d "access_token=MASTER_KEY_HERE"
```

It will return something like:

```bash
HTTP/1.1 201 Created
...
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9",
  "user": {
    "id": "57d8160eabfa186c7887a8d3",
    "name": "test",
    "picture": "https://gravatar.com/avatar/55502f40dc8b7c769880b10874abc9d0?d=identicon",
    "email": "test@example.com",
    "createdAt":"2016-09-13T15:06:54.633Z"
  }
}
```

## Directory structure

### Overview

You can customize the `src` and `api` directories.

```
src/
├─ api/
│  ├─ user/
│  │  ├─ controller.js
│  │  ├─ index.js
│  │  ├─ index.test.js
│  │  ├─ model.js
│  │  └─ model.test.js
│  └─ index.js
├─ services/
│  ├─ express/
│  ├─ facebook/
│  ├─ mongoose/
│  ├─ passport/
│  ├─ sendgrid/
│  └─ your-service/
├─ app.js
├─ config.js
└─ index.js
```

### src/api/

Here is where the API endpoints are defined. Each API has its own folder.

#### src/api/some-endpoint/model.js

It defines the Mongoose schema and model for the API endpoint. Any changes to the data model should be done here.

#### src/api/some-endpoint/controller.js

This is the API controller file. It defines the main router middlewares which use the API model.

#### src/api/some-endpoint/index.js

This is the entry file of the API. It defines the routes using, along other middlewares (like session, validation etc.), the middlewares defined in the `some-endpoint.controller.js` file.

### services/

Here you can put `helpers`, `libraries` and other types of modules which you want to use in your APIs.

---

### THIS SPACE IS FOR KAREN TO SUBMIT AND SHARE FINDINGS IN THE ACTIVITIES PORTION OF THE COURSE https://www.ministryoftesting.com/dojo/courses/improving-your-testing-through-operability WITH ASH WINTER.

Application Setup Chapter:
Activity 1
Explore the application to discover:

Which of the applications endpoints need admin user privileges to use them.

1. Create Conferences - auth_token
2. Update Conference by Id - auth_token
3. Create User - master_token
4. Authenticate User - master_token
5. Get Current User from Token - auth_token
6. Get All Users As Admin - admin_auth_token
7. Create Admin User - master_token
8. Authenticate Admin User - master_token
9. Create Speaker - auth_token
10. Create Session - auth_token

Which endpoints don’t need a token.

1. Retrieve All Conferences - access token is unchecked
2. Get Conference By Id - access token is unchecked
3. Delete Conference By Id - access token is unchecked


Event Logging Chapter:
Activity 1 
Review the application to identify 3 events for these categories:
 1-Application events (things we can control)
 2-Integration events (what do we depend on)
 3-Domain events (things outside of our control)
 
Application
1. Delete user
2. Create a conference
3. Sign in

Integration
1. MongoDB
2. Passport
3. jwt

Domain
1. Parking garage cell signal
2. Airplane mode
3. Age of mobile/desktop device
