# Getting Started

### Rename your gradle project after cloning template project

Go to the unit test class 'io.github.astrapi69.InitialTemplateTest' and set your description for your repository in the
disabled unit test method testRenameToConcreteProject. Then enable the unit test method testRenameToConcreteProject by
comment or delete the annotation @Disabled and run it after. This will rename your gradle project. Now you can delete
all unrelated files and test dependencies that you do not need.

If you are use intellij ide than you can add the new gradle run configurations to git and delete the run configurations
for the unit test and the unit test class itself.

### Setting Secrets

When you clone from this repository you have to consider to set the secrets for the sonatype username and password.

In the project gradle.properties we have two properties:
(Note that the project gradle.properties is public and can see everyone)

```
projectRepositoriesUserNameKey=ossrhUsername
projectRepositoriesPasswordKey=ossrhPassword
```

The value of this properties keys are properties keys from your local file '~/.gradle/gradle.properties' were you keep
your username and your secret password that have to be kept secret. So in your local file '~/.gradle/gradle.properties'
looks for instance like this:

```
ossrhUsername=ReplaceThisWithYourSonatypeUsername
ossrhPassword=ReplaceThisWithYourSecretSonatypePassword
```
(Note that you have to replace 'ReplaceThisWithYourSonatypeUsername' and 'ReplaceThisWithYourSecretSonatypePassword'
with your corresponding username and password)

Your local build builds now successful. But the build in your actions fail because you do not have set the secrets
in your repository.

For setting secrets for your repository you can consider the following sections:

* [Creating encrypted secrets for a repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)
* [Creating encrypted secrets for an organization](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-an-organization)

Beware in step where you set the name you have to set for 'ossrhUsername' the value: 'ossrhUsername' and not 'OSSRHUSERNAME'
The same procedure for the secret 'ossrhPassword'

Note that for organizations you only need to set the secrets once.

The following source code is the complete gradle.yml in the repository folder '.github/workflows'

```
name: Java CI with Gradle

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout sources
      uses: actions/checkout@v4
    - name: Setup Java
      uses: actions/setup-java@v4
      with:
        java-version: '21'
        distribution: 'temurin'
    - name: Setup Gradle
      uses: gradle/actions/setup-gradle@v3
    - name: Execute Gradle build
      run: ./gradlew build
      env:
        ossrhUsername: ${{secrets.OSSRHUSERNAME}}
        ossrhPassword: ${{secrets.OSSRHPASSWORD}}
    - uses: codecov/codecov-action@v4
      with:
        token: ${{ secrets.CODECOV_TOKEN }} # not required for public repos

```

So you have to set two secrets: OSSRHUSERNAME, OSSRHPASSWORD. And one optional if your repository is not public
CODECOV_TOKEN where you save your codecov token value.

### Reference Documentation

For further reference, please consider the following sections:

* [Official Gradle documentation](https://docs.gradle.org)

### Additional Links

These additional references should also help you:

* [Gradle Build Scans – insights for your project's build](https://scans.gradle.com#gradle)


# Getting Started

### Reference Documentation

For further reference, please consider the following sections:

* [Official Gradle documentation](https://docs.gradle.org)
* [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/3.3.4/gradle-plugin)
* [Create an OCI image](https://docs.spring.io/spring-boot/3.3.4/gradle-plugin/packaging-oci-image.html)
* [Spring Boot Testcontainers support](https://docs.spring.io/spring-boot/3.3.4/reference/testing/testcontainers.html#testing.testcontainers)
* [Testcontainers Postgres Module Reference Guide](https://java.testcontainers.org/modules/databases/postgres/)
* [Spring Boot Actuator](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#actuator)
* [Spring Data JPA](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#data.sql.jpa-and-spring-data)
* [Rest Repositories](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#howto.data-access.exposing-spring-data-repositories-as-rest)
* [Spring Boot DevTools](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#using.devtools)
* [Docker Compose Support](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#features.docker-compose)
* [Flyway Migration](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#howto.data-initialization.migration-tool.flyway)
* [Testcontainers](https://java.testcontainers.org/)
* [Spring Web](https://docs.spring.io/spring-boot/docs/3.3.4/reference/htmlsingle/index.html#web)

### Guides

The following guides illustrate how to use some features concretely:

* [Building a RESTful Web Service with Spring Boot Actuator](https://spring.io/guides/gs/actuator-service/)
* [Accessing Data with JPA](https://spring.io/guides/gs/accessing-data-jpa/)
* [Accessing JPA Data with REST](https://spring.io/guides/gs/accessing-data-rest/)
* [Accessing Neo4j Data with REST](https://spring.io/guides/gs/accessing-neo4j-data-rest/)
* [Accessing MongoDB Data with REST](https://spring.io/guides/gs/accessing-mongodb-data-rest/)
* [Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)
* [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)

### Additional Links

These additional references should also help you:

* [Gradle Build Scans – insights for your project's build](https://scans.gradle.com#gradle)

### Docker Compose support

This project contains a Docker Compose file named `compose.yaml`.
In this file, the following services have been defined:

* postgres: [`postgres:latest`](https://hub.docker.com/_/postgres)

Please review the tags of the used images and set them to the same as you're running in production.

### Testcontainers support

This project
uses [Testcontainers at development time](https://docs.spring.io/spring-boot/3.3.4/reference/features/dev-services.html#features.dev-services.testcontainers).

Testcontainers has been configured to use the following Docker images:

* [`postgres:latest`](https://hub.docker.com/_/postgres)

Please review the tags of the used images and set them to the same as you're running in production.
