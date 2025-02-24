FROM eclipse-temurin:21-jdk-jammy
 
WORKDIR /app

COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:resolve

COPY src ./src
RUN echo "This is a new layer" > /new_layer.txt

CMD ["./mvnw", "spring-boot:run"]
