FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app

RUN git clone -b develop https://github.com/retoquesexpress/tienda-back.git .
RUN find src -type f -name "*.java" -exec sed -i 's|http://localhost:8081|http://192.168.94.3:8082|g' {} +
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENV SERVER_PORT=8080
ENTRYPOINT ["java","-Dserver.port=${SERVER_PORT}","-jar","app.jar"]
