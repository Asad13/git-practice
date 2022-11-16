# Campaign Builder - Backend


# Environment vars
This project uses the following environment variables:

| Name                                | Description                                        | Default Value                                  |
| ----------------------------------- | -------------------------------------------------- | -----------------------------------------------|
| NODE_ENV                            | Node Environment                                   | development                                    |
| PORT                                | Server Port                                        | 3001                                           |
| USER                                | Postgresql database user name(default is used)     | postgres                                       |
| HOST                                | host of postgresql server                          | localhost                                      |
| DATABASE                            | Name of the Database                               | campaign_builder                               |
| PASSWORD                            | Database Password(User yours)                      | pg1234                                         |
| PG_PORT                             | Port used by Postgresql(default is used)           | 5432                                           |
| ACCESS_TOKEN_SECRET_KEY             | Secret Key to generate Access Token                | 22d2c9d44f0354c24fdb8b0e7286112a96aa8ae0d7dbd86c644e5a2a08c832655c1b8a35e7a4dd7271d0eff3a8b87f7acac14fc1750f81858814266de8e99f10      |
| REFRESH_TOKEN_SECRET_KEY            | Secret Key to generate Access Token                | 717d31efdda19fb3494eac54986bb6268029d58a905627173f8cb5e83392f666ec7d607847f53d0842fb66b14598fc080f9dff0cb1dcff6174c260deb0909d14      |
| ACCESS_TOKEN_MAX_AGE                | Lifespan of Access Token(1 hour)                   | 3600                                           |
| REFRESH_TOKEN_MAX_AGE               | Lifespan of Refresh Token(30 days)                 | 2592000                                        |
| REDIS_HOST                          | Host of Redis(My one is in WSL2 of windows)        | 127.0.0.1                                      |
| REDIS_PORT                          | Port used by Redis(default is used)                | 6379                                           |
| EMAIL_HOST                          | SMTP Host(Gmail used)                              | smtp.gmail.com                                 |
| EMAIL_SERVICE                       | Service used to send email                         | gmail                                          |
| EMAIL_PORT                          | Port used by email service                         | 587                                            |
| EMAIL_SECURE                        | secured                                            | true                                           |
| EMAIL_USER                          | Sender's email address(Temp)                       | testing.email.2029@gmail.com                   |
| EMAIL_PASSWORD                      | Sender's email  App password(Temp,)                | arjrsqrrvldtzhll                               |
| EMAIL_VERIFICATION_TOKEN_SECRET_KEY | Secret Key to generate Email Verification Token    | d912b6fe8387f52a24bc654695abf0431bcfaacdbf116efc7e6954f04775c4d70d38cce19c7aa484e05861347b798c0e005451a8aa0cd68d795f565247387d60            |
| EMAIL_TOKEN_MAX_AGE                 | Lifespan of Email Verification Token(1 hour)       | 3600                                           |
| SERVER_URL                          | Server url                                         | http://localhost:3001                          |
| CLIENT_URL                          | Client url                                         | http://localhost:3000                          |


# Pre-requisites
- Install [Node.js](https://nodejs.org/en/) version 16.18.1
- Install [PostgreSQL](https://www.postgresql.org/download/) version 15.1
- Install [Redis](https://redis.io/docs/getting-started/installation/) version 7.0.5
- Install [VS Code](https://code.visualstudio.com/download) For development
- Install [VS Code Extension for Redis]() For development only on Windows (Redis by Weijan Chen) [More Info](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)


# Getting started

- ### Clone the repository
```
git clone git@github.com:Buzzier/campaign-backend.git
```

- ### Install dependencies
```
cd campaign-backend
npm i
```

- ### Build and run the project in development environment
```
npm run dev
```

Note: You need nodemon, an npm package to run in development mode. If you don't
have it either run `npm i -g nodemon` for installing and using it globally for
all the node applications or `npm i -D nodemon` to install it as Dev
dependencies to use it for this application only.

You can run `npm start` in development mode too but then you have to
run it manually everytime you make any change.

- ### Build and run the project in production environment
```
npm start
```

Navigate to http://localhost:3001
If it says "Hello World" then everything is okay.
## Start PostgreSQL

- ### Connect to PostgreSQL(From Terminal/Bash)
```
psql -U postgres
```

Note: postgres is the default user name PostgreSQL set during installation.
If you change it or using other user replace it with yours. Then you have
to provide your password for the user.

Note: You have to run the next commands only once(now) to setup tha database
and users table.
- ### Create a Database
```
CREATE DATABASE campaign_builder;
```

```
\c campaign_builder;
```

```
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

```
CREATE TABLE users(
    ID SERIAL,
    uid uuid DEFAULT uuid_generate_v4 (),
    company VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(1024) NOT NULL,
    verified BOOLEAN DEFAULT FALSE,
    PRIMARY KEY (uid) 
);
```

Some useful commands for PostgreSQL:

- ### To see all the tables in the campaign_builder database:
```
\dt
```

- ### To see all the entries of users table:
```
SELECT * FROM users;
```

- ### To stop PostgreSQL:
```
\q
```

## Start Redis

- ### Connect to Redis by Bash
```
sudo service redis-server start
```

- ### To Check Connection
```
redis-cli ping
```
Note: If the bash replies `PONG` then the connection is okay

-  ### Windows(WSL2) only : You have to connect to the Redis database through the redis extention providing the host and port

-  ### To stop Connection after finish testing/coding
```
sudo service redis-server stop
```
