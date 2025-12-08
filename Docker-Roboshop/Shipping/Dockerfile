# FROM maven:3
# EXPOSE 8080
# WORKDIR /opt/app
# COPY pom.xml .
# COPY src ./src/
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST=mysql 
# CMD ["java","-jar","shipping.jar"]    
#CMD ["sleep", "1000"]



FROM maven:3.9.11 AS build
WORKDIR /opt/app
COPY pom.xml .
COPY src ./src/
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 


FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080  
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/app
WORKDIR /opt/app
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST=mysql 
COPY --from=build /opt/app/shipping.jar shipping.jar
USER roboshop
CMD ["java","-jar","shipping.jar"]   