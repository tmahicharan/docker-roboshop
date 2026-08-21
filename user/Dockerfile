FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.22
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
EXPOSE 8080
LABEL Project="roboshop" \
      component="user" \
      OWNER="mahi"
ENV mongo="true"  \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users" 
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop 
CMD ["server.js"]
ENTRYPOINT [ "node" ]


# FROM node:20
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV mongo="true"  \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users" 
# CMD [ "node","server.js" ]