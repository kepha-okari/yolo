# Use the official Node.js 16.17.0-bullseye-slim image as the base image
# FROM node:16.17.0-bullseye-slim

FROM node:buster-slim

# Set the working directory to /backend and set an environment variable for the working directory
ENV WORKDIR=/backend
WORKDIR ${WORKDIR}

# Copy the package.json file to the working directory
COPY package.json package.json

# Run npm install to install dependencies
RUN npm install

# Copy the remaining application files to the working directory
COPY . ${WORKDIR}

# Expose port 5000 for the container
EXPOSE 5000

# start the app when the container start
CMD ["npm","run" , "start"]
