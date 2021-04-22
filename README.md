# Spring-Native-Study
Steps necessários para executar a imagem
 
mvn clean package spring-boot:build-image

mvn clean package spring-boot:build-image -Pspring-native,build-docker-image -DskipTests

docker-compose up mongodb

docker run spring-native-demo
