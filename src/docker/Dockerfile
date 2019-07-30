FROM openjdk8:latest
USER root
RUN mkdir /images
ADD ./target/service-0.0.1-SNAPSHOT.jar /images
CMD ["java", "-jar", "/images/service-0.0.1-SNAPSHOT.jar"]
WORKDIR /images
