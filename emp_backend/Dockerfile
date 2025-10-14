# ===========================
# Stage 1: Build the JAR
# ===========================
FROM maven:3.9.3-eclipse-temurin-17 AS build
WORKDIR /app

# Copy pom.xml and download dependencies first (for caching)
COPY ../pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code
COPY ../src ./src

# Build the application
RUN mvn clean package -DskipTests

# ===========================
# Stage 2: Run the JAR
# ===========================
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

# Copy built jar file from previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose port 8080 (default for Spring Boot)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
