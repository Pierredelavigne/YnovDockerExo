# ===== 1) Builder stage =====
FROM maven:3.9-eclipse-temurin-21 AS builder
WORKDIR /app

# cache deps
COPY pom.xml .
COPY .mvn .mvn
COPY mvnw mvnw
RUN chmod +x mvnw
RUN ./mvnw -q -DskipTests dependency:go-offline

# build
COPY src src
RUN ./mvnw -q -DskipTests clean package

# ===== 2) Runtime stage =====
FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
