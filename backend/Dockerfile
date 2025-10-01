# Use official Java image
FROM openjdk:17-jdk-alpine

# Set working directory
WORKDIR /app

# Copy project files
COPY target/springboot-microservice-1.0.0.jar app.jar

# Expose port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java","-jar","app.jar"]


