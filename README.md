# HYPERTUBE PROJECT

## Description of the project :

HYPERTUBE is a plateform for video streaming

## Team

- Abdeljalil NACEUR
- Sacha Requiem
- Dimitri Hauet

## Project's Goals and objectives

## Technologies :

- NodeJs/Express v8.11.4
- ReactJs v16.3.2
- Redux v4.0.0
- MongoDb
- Docker 17.12.1-ce
- Bootstrap 3

## Screenshots

## Git flow

There are two branches:

- Master - origin
- Develop - follow master

The _Master_ branch is used for production. Only the features we know are perfectly working should be merged on _Master_
The _Dev_ branch is where new features are developped.

## Git Commit messages guidlines

Commit messages should conform to the following rules:  
 - Title in capital letters  
 - The title is separated from the body of the message by one empty line  
 - A line should not be longer than 80 characters  
 - The message must focus on the WHY and WHAT, not HOW.

This template can be used for the commit messages:

> COMMIT MESSAGE TITLE
>
> Here, I explain WHAT I did (the improvements I made to the code, what I removed
> from it, etc...)
> I alos explain WHY I did it.

A template ready for usage is also avaible in the _misc_ floder, at the root of the repo.

## Install the development environment

Get the source:

```bash
git clone https://me-me@bitbucket.org/me-me/hypertube.git
```

Edit your `/etc/hosts` file:

```
127.0.0.1   si.hpt.local
127.0.0.1   app.hpt.local
127.0.0.1   mongo.hptdb.local
```

## Build the project in dev

Navigate to frontend

```bash
cd frontend
```

Copy the env variables for developement environment

```bash
cp .env-template .env
```

Navigate to backend

```bash
cd backend
```

Copy the env variables for developement environment

```bash
cp .env-template .env
```

Within the backend path creat a new foldder (if it does not exist)

```bash
mkdir uploads
```

Build the project from the root directory

```bash
docker-compose up --build
```

Within the backend path creat a new foldder (if it does not exist)

```bash
mkdir uploads
```

#### Prerequisite :

- NodeJs v8.11.4
- Docker 17.12.1-ce
- Docker compose
- Port 3030 open (inbound/outBound)

#### Nice to know :

- We use google Oauth2 in the frontend
  so its required to change the clientId in frontend/src/components/pages/login/login.js line 78
- In your google console API remember to set the redirect URI to :
  [DOMAIN_NAME]
- And added it to the authorized this domain
- To deploy the frontend to production remember to build
  it first locally with its related environment variables "npm run build"
  if everything goes well then commit it to be depolyed.

Build the project from the root directory

```bash
docker-compose -f docker-compose-prod.yml up --build
```

#### TODO :

- There are some todos to be taken in consideration.
- For future deployment 'Continous Integration' (CI)
  and 'Continuous Delivery' (CD) has to be added to GitlabCI

### Help

Stop and remove all containers

```bash
docker stop $(docker ps -a -q)
```

Connect to a container via bash (get the container name you want to connect to via command `docker ps`)

```bash
docker exec -ti containername bash
```

Execute a command directly in a container without connecting in bash (get the container name you want to connect to via command `docker ps`)

```bash
docker exec -i containername yourcommand
```

Delete all images

```bash
docker rmi -f $(docker images -q)
```

Show images

```bash
docker images
```

if you face this error message :
"Error: /usr/lib/x86_64-linux-gnu/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by /usr/src/app/node_modules/bcrypt/lib/binding/bcrypt_lib.node)"

Cause : bcrypt is lib is not compatible.
Solution : To avoid this error do the following

```bash
# Connect to your container backend
docker exec -ti <container-name> bash

# Delete node_modules
rm -rf node_modules

# Re-install the packages
npm install
```

## FAQ

How to install abntorrent
1 - Remove the package from /backend/packaje.json
2 - Install it with npm
npm i bitbucket:me-me/abntorrentclient --save

Error :
ERROR: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network

Solution :
docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')

If on starting the containners in production mode
you face an error of refused connection to mongodb container then :

Solution : change the DB_HOST in backend/.env to localhost
Restart the containers.

If the error persiste then fetch the IpAddress of the mongo container

```bash
# Connect to your container backend
docker inspect hpt_mongo_dev  | grep IPAddress | tail -1 | cut -d '"' -f4
```

Replace this Ip addresse in your container and restart docker.
