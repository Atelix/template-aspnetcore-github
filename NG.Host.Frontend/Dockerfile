# Use Node.js 18 as the base image
FROM node:22 AS Build

# Set the working directory
WORKDIR /build

# Copy package files
COPY package.json .
COPY pnpm-lock.yaml .
RUN npm install -g pnpm
# Install dependencies using npm
RUN pnpm install

# Copy the rest of the application files
COPY . .

# Build the application
RUN pnpm run build

# Expose port
EXPOSE 3000

# Set the entry point to start the application
ENTRYPOINT ["npm", "run", "host"]