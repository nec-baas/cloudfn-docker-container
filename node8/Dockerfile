FROM node:8

ENV no_proxy 127.0.0.1,localhost

# Expose logic server port to server manager
EXPOSE 9000

# Set environment (Default fallback)
ENV HOST_IP '172.17.0.1'

# Set workdir
WORKDIR /tmp

# Set execute user
RUN useradd nodejs
USER nodejs

# Start logic server
CMD node /opt/emitter/bin/server.js

