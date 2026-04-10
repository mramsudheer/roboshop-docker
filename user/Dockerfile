# FROM node:20
# # this creates /app and move there
# WORKDIR /app
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue" \
#     REDIS_URL="redis://redis:6379"
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# CMD ["node", "server.js"]
#--------------------------------------------------------#
FROM maven:3.9.14 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 

FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=builder /app/shipping.jar .
USER roboshop
ENTRYPOINT ["java", "-jar", "shipping.jar"]