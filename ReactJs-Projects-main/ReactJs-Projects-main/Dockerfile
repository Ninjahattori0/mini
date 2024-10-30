# Step 1: Use Node.js to build the React app
FROM node:18 AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Step 2: Use nginx to serve the app
FROM nginx:alpine

# Copy the build files from the builder stage to the nginx HTML directory
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80 to the external network
EXPOSE 80

# Start nginx server
CMD ["nginx", "-g", "daemon off;"]
