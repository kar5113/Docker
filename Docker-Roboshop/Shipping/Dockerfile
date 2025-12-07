FROM maven:3
EXPOSE 8080
WORKDIR /opt/app
COPY pom.xml .
COPY src/ .
RUN mvn clean package 
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST=mysql 
CMD ["java","-jar","shipping.jar"]    
