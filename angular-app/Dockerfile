# Step 1: Use an official Node.js image to build the Angular app
FROM node:18 as builder

# Set working directory inside the container
WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json* ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular app in production mode
RUN npm run build --prod

# Step 2: Use NGINX to serve the built app
FROM nginx:alpine

# Copy the built Angular app from previous stage
COPY --from=builder /app/dist/ /usr/share/nginx/html

# Copy custom nginx config (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start NGINX server
CMD ["nginx", "-g", "daemon off;"]
