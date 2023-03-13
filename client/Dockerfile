# Use the official Node.js 16.17.0-bullseye-slim image as the base image
FROM node:16.17.0-bullseye-slim

# Set the working directory to /client
WORKDIR /client

# Copy the package.json file to the working directory
COPY package.json package.json

# Run npm install to install dependencies
RUN npm install

# Copy the remaining application files to the working directory
COPY . .

# Expose port 3000 for the container
EXPOSE 3000

# Set the default command to kill all port 3000 services and fire up the app when the container starts
CMD kill $(lsof -t -i :3000) || true && npm start
