# An inefficient image.
# Use full Node 22 image (not alpine - bigger!)
FROM node:22

# Set working directory
WORKDIR /app

# Enable corepack for yarn
RUN npm install --global corepack
RUN corepack enable

# Create React app
RUN yarn create react-app test-app

# Change to app directory
WORKDIR /app/test-app

# Install dependencies (already done by create-react-app, but explicit)
RUN yarn install

# Build the app
RUN yarn build

# Install serve to serve static files
RUN yarn global add serve

# Expose port 3000
EXPOSE 3000

# Serve the built app
CMD ["serve", "-s", "build", "-l", "3000"]
