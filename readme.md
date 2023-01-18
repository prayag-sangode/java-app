# DevOps - Deploy Java Application using CI/CD Pipeline - Using Jenkins & Google Kubernetes Engine
## Author - Prayag Sangode

## Diagram

<img src="https://github.com/prayag-sangode/java-app/blob/main/jenkins-helm-java-app.png" alt="Alt text" title="DevOps - Deploy Java Application using CI/CD Pipeline">

## Services -

- GitHub - Host Java Spring Boot Apllication, Jeninsfile & Helm Charts
- Jenkins - For CI/CD Pipeline
- Artifact Registry - For Docker Images
- GKE - Google Kubernetes Engine where Java App is deployed
- Helm - Deploy Java App Helm charts

## Create service account for authentication

## Create Jenkins Github Webhook


## Running Application locally
You can build a jar file and run it from the command line (it should work just as well with Java 11 or newer):


```
git clone https://github.com/prayag-sangode/java-app.git
cd java-app
./mvnw package
java -jar target/*.jar
```

You can then access petclinic here: http://localhost:8080/

Or you can run it from Maven directly using the Spring Boot Maven plugin. If you do this it will pick up changes that you make in the project immediately (changes to Java source files require a compile as well - most people use an IDE for this):

```
./mvnw spring-boot:run
```

## Building a Container

You can build a container image (if you have a docker daemon) using the Spring Boot build plugin:

```
./mvnw spring-boot:build-image or docker build -t <image-tab> .
```

## Database configuration

In its default configuration, application uses an in-memory database (H2) which
gets populated at startup with data. The h2 console is automatically exposed at `http://localhost:8080/h2-console`
and it is possible to inspect the content of the database using the `jdbc:h2:mem:testdb` url.
 
A similar setup is provided for MySQL and PostgreSQL in case a persistent database configuration is needed. Note that whenever the database type is changed, the app needs to be run with a different profile: `spring.profiles.active=mysql` for MySQL or `spring.profiles.active=postgres` for PostgreSQL.

You could start MySQL or PostgreSQL locally with whatever installer works for your OS, or with docker:

```
docker run -e MYSQL_USER=petclinic -e MYSQL_PASSWORD=petclinic -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=petclinic -p 3306:3306 mysql:5.7.8
```

or

```
docker run -e POSTGRES_USER=petclinic -e POSTGRES_PASSWORD=petclinic -e POSTGRES_DB=petclinic -p 5432:5432 postgres:14.1
```


