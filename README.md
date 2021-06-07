# Spring-Native-Study

### Project description
🚀 Project that builds an api that performs a CRUD in a reactive way with MongoDB and uses the new Spring spec, the Spring Native and that compiles the application and runs as a native image with GraalVM


## Installation ##

It is necessary to install some items:
- Docker
- Java 11
- Maven
- GraalVM

### Native Image
Native image is a technology that allows you to compile Java code in advance and make it executable. This executable contains application classes, their dependency classes, runtime library classes, and native code linked to the JDK. After the build process, it builds the executable for the operating system, this process is called image build. JVM-based languages have this capability like Java, Scala, Clojure and Kotlin.

### Spring Native
In March 2021, Pivotal released a still-experimental version to the community of its native module, Spring-Native. Given that its competitors are already able to have a more fluid integration with GraalVM, spring had to chase after Quarkus and Micronaut to be able to make its stack compatible with native images.

Spring Native provides the ideal workload for computing in containers and Kubernetes. Use strong native image an instant boot, instant peak performance and reduced memory consumption.

As everything is not perfect, it is necessary to understand that there are steps in this process that need to be improved, as the process of generating a native image is very heavy and time-consuming.


### Necessary Steps

After configuring the entire environment, it is necessary to place the necessary dependencies for the project. Once this is done and you are structuring the endpoints that will be used and what will be persisted, we need to run some maven commands to generate the project's packaging. The first command to run is: mvn clean package spring-boot:build-image

In this project we have a maven plugin which generates necessary metadata for the GraalVM at compile time, Spring uses the build package. paketo is a buildpack that transforms the built code into an image that can be executed in any way. widely used for code execution in the cloud.

Once you have generated the image, you will need to run the following command: mvn clean package spring-boot:build-image -Pspring-native,build-docker-image -DskipTests Depending on how much memory you have available or how much memory you have for the startup of your Docker, this process may fail due to lack of memory or take time to generate the image.

This command will generate a native GraalVM image to build the application as a native executable.

After executing the command that generates the application's native image, we will need to upload our database, in this example we are using MongoDB, so the command that will be executed will be: docker-compose up mongodb


Finally we will run our reactive/native application with SpringWebFlux and Spring Native by executing the following command: docker run spring-native-demo


### Technologies

The following technologies were used to carry out the project:
- Java 11
- Maven
- SpringBoot
- Spring Webflux
- MongoDB
- Docker
- GraalVM
- PacketoBuild
