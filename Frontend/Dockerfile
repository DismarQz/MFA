FROM maven:3.9.9-eclipse-temurin-21 as build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN --mount=type=cache,target=/root/.m2 mvn -q -Dmaven.test.skip=true package

FROM eclipse-temurin:21-jre
ENV TZ=America/Santiago \
    JAVA_OPTS="-Xms256m -Xmx512m"
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["sh","-c","java $JAVA_OPTS -jar /app/app.jar"]
