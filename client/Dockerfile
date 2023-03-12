
# Use an official Node.js runtime as a parent image
FROM node:13.12.0

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the container's /app directory
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Copy the rest of the application code to the container's /app directory
COPY . .

# Set the environment variable to use the application's proxy
ENV http_proxy http://localhost:5000

# Expose the container's port (if applicable)
EXPOSE 3000

# Define the command to run the application when the container starts
CMD [ "npm", "start" ]
