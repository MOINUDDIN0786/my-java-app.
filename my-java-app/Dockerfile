# Base image (Java 17)
FROM openjdk:17-jdk-slim

# Set working directory
WORKDIR /app

# Copy the built JAR file from Jenkins workspace to container
COPY target/my-java-app-1.0-SNAPSHOT.jar app.jar

# Expose the port (change if needed)
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]
