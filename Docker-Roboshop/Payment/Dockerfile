FROM python:3.9
EXPOSE 8080
WORKDIR /opt/app
COPY requirements.txt .
COPY *.py .
COPY *.ini .
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    RABBITMQ_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uswgi", "--ini","payment.ini"]