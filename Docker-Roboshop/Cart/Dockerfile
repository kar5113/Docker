# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV REDIS_HOST="redis" \
#     CATALOGUE_HOST="catalogue" \
#     CATALOGUE_PORT="8080"
# EXPOSE 8080
# CMD ["node","server.js"]  
  

FROM node:20.19.6-alpine3.23 AS build
WORKDIR /opt/server
COPY package.json .
RUN npm install



FROM node:20.19.6-alpine3.23
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build /opt/server .
COPY *.js .
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
RUN chown -R roboshop:roboshop /opt/server
USER roboshop    
EXPOSE 8080
CMD ["node","server.js"]  
