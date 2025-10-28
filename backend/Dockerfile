# Use an official JDK image
FROM openjdk:17-jdk-slim AS build

WORKDIR /app

# Copy pom + sources
COPY pom.xml mvnw ./
COPY .mvn .mvn
COPY src src

# Build the jar
RUN ./mvnw clean package -DskipTests

# Run stage
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copy the built jar (adjust name if different)
COPY --from=build /app/target/*.jar app.jar

# Expose port (adjust if your Spring Boot runs on different port)
EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
