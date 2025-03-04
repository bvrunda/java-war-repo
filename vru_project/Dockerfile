# Use an official base image
FROM maven:3.8.5-openjdk-17 AS builder

# Set working directory
WORKDIR /ops-app

RUN git clone https://github.com/bvrunda/java-war-repo.git .

RUN mvn clean package

FROM tomcat:10.1-jdk17

WORKDIR /usr/local/tomcat/webapps/

COPY --from=builder /ops-app/target/*.war opskill.war

# Expose port 80
EXPOSE 80

# Define the default command
CMD ["catalina.sh", "run"]


