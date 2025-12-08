# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/app
# COPY requirements.txt .
# COPY *.py .
# COPY *.ini .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     RABBITMQ_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi", "--ini","payment.ini"]


FROM python:3.12.12-alpine3.23 AS build 
WORKDIR /opt/app
COPY requirements.txt .
COPY *.py .
COPY *.ini .
RUN pip3 install -r requirements.txt


FROM python:3.12.12-alpine3.23
LABEL project="roboshop" \
      component="payment" \
      version="2.0" 
EXPOSE 8080
WORKDIR /opt/app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/app
COPY --from=build /opt/app .
USER roboshop
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    RABBITMQ_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi", "--ini","payment.ini"]