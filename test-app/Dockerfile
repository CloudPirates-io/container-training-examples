# Define Base Image
FROM node:8.16.2-alpine

# Use non root for app install and run command
RUN adduser -D -g '' app
RUN mkdir /app && chown app:app /app

# All following steps will be executed as "app" user, not as root
USER app

# Add a workdir inside the current image
WORKDIR /app

# Copy package.json and package-lock.json to workdir
COPY package*.json ./

# Install dependencies over npm
RUN npm ci --only=production

# Copy application files (server.js)
COPY . ./

# Expose application on Port 8080
EXPOSE 8080

# Default Entrypoint (overwrite with "docker run --entrypoint IMAGE")
ENTRYPOINT [ "node" ]

# Default start command for the image (overwrite with additional flags, 
# i.e. "docker run IMAGE cmd1 cmd2 cmd3")
CMD ["server.js"] 
