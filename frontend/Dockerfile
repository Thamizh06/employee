# Use the official Node.js image to build the project
FROM node:latest AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React project using Vite
RUN npm run build

# Use Nginx to serve the build files
FROM nginx:alpine AS production

# Copy the built files from the previous stage to Nginx's serving directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 5173

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
