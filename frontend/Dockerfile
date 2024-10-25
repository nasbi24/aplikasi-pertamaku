# Stage 1: Build the application
FROM node:18-slim AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve the application using Node.js
FROM node:18-slim

# Set the working directory
WORKDIR /app

# Install a simple static server globally
RUN npm install -g serve

# Copy the built application from the previous stage
COPY --from=build /app/dist /app

# Expose port 3000
EXPOSE 5173

# Serve the static files
CMD ["serve", "-s", "/app"]
