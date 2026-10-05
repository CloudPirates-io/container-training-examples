# Define Base Image
# Best Practice: Use Digest (sha265) instead of tag
FROM node:alpine

# Use non root for app install and run command
RUN adduser -D -g '' app
RUN mkdir /app && chown app:app /app

# All following steps will be executed as "app" user, not as root
USER app

# Add a workdir inside the current image
WORKDIR /app

# Copy package.json and package-lock.json to workdir (/app)
COPY package*.json ./

# Install dependencies over npm
RUN npm ci --omit=dev

# Copy application files (server.js)
COPY . ./

# Expose application on Port 8080
EXPOSE 8080

# Default Entrypoint (overwrite with "docker run --entrypoint my-custom-entrypoint")
ENTRYPOINT [ "node" ]

# Default start command for the image (overwrite with additional flags, 
# i.e. "docker run IMAGE cmd1 cmd2 cmd3")
CMD ["server.js"] 

# docker run my-image
# -> node server.js

# docker run my-image test
# -> node test

# docker run --entypoint foobar my-image test
# -> foobar test
