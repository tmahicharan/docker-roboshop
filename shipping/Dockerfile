FROM maven:3.9.11 AS build
WORKDIR /opt/server
COPY pom.xml .
COPY src ./src
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 

FROM eclipse-temurin:17-jre-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
EXPOSE 8080
LABEL Project="roboshop" \
      component="shipping" \
      OWNER="mahi"
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --from=build --chown=roboshop:roboshop /opt/server/shipping.jar .
USER roboshop 
ENTRYPOINT [ "sh","-c","sleep 30 && java -jar shipping.jar" ]



# FROM maven:3.9.11
# EXPOSE 8080
# WORKDIR /opt/server
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java","-jar","shipping.jar" ]