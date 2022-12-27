[[Dockerfile]]

Внимание на 28 строку
```Dockerfile
FROM maven:3.6.0-jdk-11-slim AS builder  
  
WORKDIR /opt/build  
  
COPY pom.xml /opt/build/pom.xml  
COPY /src /opt/build/src/  
  
RUN mvn -f ./pom.xml clean package  
  
  
#============================================================
FROM openjdk:11-jre-slim  
  
WORKDIR /opt/app  
  
EXPOSE 8080:9000  
  
  
ENV ARTIFACT springDocker-0.0.1-SNAPSHOT.jar  
COPY --from=builder /opt/build/target/${ARTIFACT} ./app.jar  
  
ENTRYPOINT ["java", "-jar", "./app.jar"]  
# используется spring, у него префикс параметров '--'
CMD ["--server.port=9000"]
```

```bash
# используется стандартное значение cmd
docker run -p 8080:9000 -d image-name

# передача параметров
docker run -p 8080:9999 -d image-name --server.port=9999
```