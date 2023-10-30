FROM azul/zulu-openjdk-alpine:17.0.5-17.38.21  as builder 
LABEL stage=intermediate
ARG JAR_FILE=./build/libs/*.jar
WORKDIR app
COPY $JAR_FILE application.jar    

RUN java -Djarmode=layertools -jar application.jar extract  

FROM azul/zulu-openjdk-alpine:17.0.5-17.38.21
ENV SPRING_PROFILE="default"
ARG DOCKER_IMAGE_EXPIRES="never"
LABEL quay.expires-after=${DOCKER_IMAGE_EXPIRES}
VOLUME /tmp 
 
COPY --from=builder /app/dependencies/ ./
COPY --from=builder /app/snapshot-dependencies/ ./
COPY --from=builder /app/spring-boot-loader/ ./
COPY --from=builder /app/application/ ./


EXPOSE 80
ENTRYPOINT ["java", "-Dspring.profiles.active=${SPRING_PROFILE}", "org.springframework.boot.loader.JarLauncher"]
