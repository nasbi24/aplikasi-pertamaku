# Use a lightweight Node.js image
FROM node:18-slim

# Create a new user and set up the working directory
RUN useradd -m backenduser && mkdir /app && chown backenduser /app
WORKDIR /app

# Copy only the package.json and package-lock.json for efficient dependency installation
COPY package.json package-lock.json ./

# Install dependencies (production only) and rebuild any native modules
RUN npm install --only=production

# Copy the rest of the backend code to the /app directory
COPY . .

# Set the user to avoid root privileges
USER backenduser

# Expose the port that the backend server will run on
EXPOSE 3000  

# Start the backend server
CMD ["npm", "start"]
