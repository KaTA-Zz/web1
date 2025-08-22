# Base Tomcat với JDK17
FROM tomcat:10.1-jdk17

# Cài Maven + build WAR
WORKDIR /app
COPY . .
RUN apt-get update && \
    apt-get install -y maven && \
    mvn clean package -DskipTests && \
    cp target/demo-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war && \
    apt-get purge -y --auto-remove maven && \
    rm -rf /var/lib/apt/lists/* /app

# Disable shutdown port để tránh warning
RUN sed -i 's/port="8005"/port="-1"/' /usr/local/tomcat/conf/server.xml

EXPOSE 8080
CMD ["catalina.sh", "run"]
