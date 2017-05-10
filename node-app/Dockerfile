FROM readytalk/nodejs

# Add files
WORKDIR /app
ADD . /app
RUN npm install
EXPOSE 80

# start container
ENTRYPOINT ["/nodejs/bin/npm", "start"]



