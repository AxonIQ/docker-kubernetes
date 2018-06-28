FROM openjdk:8-jre-alpine
VOLUME /tmp /data
EXPOSE 8024 8124
COPY axonhub-server.jar /
COPY axonhub.properties /
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-Xms512M", "-Xmx512M", "-jar", "/axonhub-server.jar"]
