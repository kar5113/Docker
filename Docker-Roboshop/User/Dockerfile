FROM node:20
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install
ENV MONGO_URL="mongodb://mongodb:27017/catalogue" \
    MONGO="true" \
    REDIS_URL="redis://redis:6379"
EXPOSE 8080
CMD ["node","server.js"]