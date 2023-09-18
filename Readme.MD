# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install application dependencies, if any change is detected in package.json or package-lock.json
RUN npm ci --only=production

# Copy the rest of the application source code to the working directory
COPY . .

# Expose the port your application will run on
EXPOSE 3000

# Define an environment variable (optional)
# ENV NODE_ENV=production

# Start the Node.js application
CMD ["node", "app.js"]

Explanation :
Use a Minimal Base Image: We use the official Node.js image, which is based on a minimal Linux distribution. This helps keep the image size small.

Set the Working Directory: We set the working directory to /usr/src/app, which is a common convention for Node.js applications.

Copy Dependencies First: We copy package.json and package-lock.json separately and run npm ci before copying the rest of the application files. This leverages Docker's caching mechanism to avoid reinstalling dependencies unless the package.json or package-lock.json files change.

Copy the Application Code: We copy the application code into the working directory.

Expose Ports: We expose port 3000, which is the port our Node.js application is expected to listen on. You should replace this with the actual port your application uses.

Set Environment Variables (optional): You can set environment variables if needed, like NODE_ENV=production.

Define the Start Command: We use the CMD instruction to specify how the container should start the Node.js application. You should replace "app.js" with the actual entry point file for your application.

To build the image:
docker build -t my-node-app .

To create a container:
docker run -p 3000:3000 my-node-app

Node.js application listens on port 3000
