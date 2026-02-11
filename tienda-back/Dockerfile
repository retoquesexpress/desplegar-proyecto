FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app

RUN git clone -b develop https://github.com/retoquesexpress/tienda-back.git .
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
