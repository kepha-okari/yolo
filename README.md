# Requirements

Make sure that you have the following installed:

- [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04)
- npm
- [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) and start the mongodb service with `sudo service mongod start`

## Navigate to the Client Folder

`cd client`

## Run the folllowing command to inititalize the package.json file

`npm init`

## Run the folllowing command to install the dependencies

`npm install`

## Run the folllowing to start the app

`npm start`

## Open a new terminal and run the same commands in the backend folder

`cd ../backend`

`npm install`

`npm start`

### Go ahead and add a product (note that the price field only takes a numeric input)

## Set up with docker-compose

This docker-compose file sets up three services:

- `backend`: A Node.js backend service that runs on port 5000 and connects to a MongoDB database on port 27017.
- `client`: A React.js frontend service that runs on port 3000 and connects to the same MongoDB database as the backend service.
- `mongodb`: A MongoDB database service that runs on port 27017.

## How to Run

### without docker compose

- run client container using the command below
  `docker run -p 3000:3000 rkepha/yolo-client:1.0.1-buster`

- run backed container using the command below
  `docker run -p 5000:5000 rkepha/yolo-backend:1.0.1-buster`
- install and start mongodb
  `wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -`

  `echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list`

  `sudo apt-get update && sudo apt-get install -y mongodb-org`

  `sudo systemctl start mongod`

### with doceker compose

1. Install Docker on your machine.
2. Open a terminal window and navigate to the directory containing the docker-compose.yml file.
3. Run the following command to start the services:

   `docker-compose up`
