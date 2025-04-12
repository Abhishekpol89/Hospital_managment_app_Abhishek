# Use a Maven image with Java 17 to build the application
FROM maven:3.9.4-eclipse-temurin-17 AS builder

# Set working directory inside container
WORKDIR /app

# Copy everything into container
COPY . .

# Build the app (skip tests if you want faster build)
RUN mvn clean package -DskipTests

# Use a lightweight JDK base image for running the app
FROM eclipse-temurin:17-jdk

# Set working directory inside the runtime container
WORKDIR /app

# Copy only the JAR file from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose port (your app runs on 8085)
EXPOSE 8085

# Run the JAR
ENTRYPOINT ["java", "-jar", "app.jar"]

