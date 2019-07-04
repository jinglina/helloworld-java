FROM 10.180.249.20:30002/mips64le/loongnix-openjdk8:latest

# USER root
# ARG ZIP_FILE
ADD ./target/service-0.0.1-SNAPSHOT.jar /images
# RUN chown -R jboss:root /deployments/incloudos
ENV JAVA_APP_DIR=/images

# USER jboss
WORKDIR /images
ENTRYPOINT ["java"]
CMD ["-jar", "/images/service-0.0.1-SNAPSHOT.jar"]
