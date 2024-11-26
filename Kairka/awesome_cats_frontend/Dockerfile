# Step 1: Build the application
FROM node:16-alpine AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json (or yarn.lock) to install dependencies
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Build the production-ready React app
RUN npm run build

# Step 2: Set up the production environment
FROM nginx:alpine

# Copy the build files from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx server
CMD ["nginx", "-g", "daemon off;"]
