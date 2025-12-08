# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO_URL="mongodb://mongodb:27017/catalogue" \
#     MONGO="true" \
#     REDIS_URL="redis://redis:6379"
# EXPOSE 8080
# CMD ["node","server.js"]



FROM node:20.19.6-alpine3.23 as build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install



FROM node:20.19.6-alpine3.23
LABEL project="roboshop" \
      component="users" \
      version="2.0"   
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV MONGO_URL="mongodb://mongodb:27017/catalogue" \
    MONGO="true" \
    REDIS_URL="redis://redis:6379"
RUN chown -R roboshop:roboshop /opt/server  
COPY --from=build /opt/server .
USER roboshop   
EXPOSE 8080
CMD ["node","server.js"]