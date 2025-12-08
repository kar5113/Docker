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



FROM maven:3.9.11 AS builder
WORKDIR /opt/app
COPY pom.xml .
COPY src ./src/
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 


FROM eclipse-temurin:17-jre-alpine
LABEL project="roboshop" \
      component="shipping" \
      version="2.0" 
EXPOSE 8080  
WORKDIR /opt/app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/app
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST=mysql 
COPY --from=builder /opt/app/shipping.jar shipping.jar
USER roboshop
CMD ["java","-jar","shipping.jar"]   