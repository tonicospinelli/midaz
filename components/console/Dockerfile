# Use an official Node.js runtime as the base image
FROM node:22-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY components/console/package*.json ./

# Configure npm to use GitHub token temporarily, without exposing it in the Dockerfile
RUN echo "//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}" > ~/.npmrc && \
    apk update && apk add bash && \
    npm install && \
    npm cache clean --force && \
    rm -f ~/.npmrc

# Copiar o arquivo .env.example para o diretório de trabalho
COPY components/console/.env.example .env.example

# Run the command to set environment variables
RUN npm run set-env

# Copy the rest of the application code
COPY components/console/   .

# Build the app
RUN npm run build

# Expose the port the app runs on
EXPOSE 8081

# Command to run the applications
ENTRYPOINT ["npm", "start"]
