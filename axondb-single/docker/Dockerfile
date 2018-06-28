FROM openjdk:8-jre-alpine
VOLUME /tmp /data
EXPOSE 8023 8123
COPY axondb-server.jar /
COPY axondb.properties /
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-Xms512M", "-Xmx512M", "-jar", "/axondb-server.jar"]
