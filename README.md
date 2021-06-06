# Spring-Native-Study

### Descrição do Projeto
🚀 Projeto que constrói uma api que realiza um CRUD de forma reativa com MongoDB e utiliza a nova spec do Spring o Spring Native eque compila a aplicação e executa como imagem nativa junto ao GraalVM


## Instalação ##

É necessário instalar alguns itens: 
- Docker 
- Java 11
- Maven
- GraalVM

###  Native Image
Native image é uma tecnilogia que permite compilar de forma antecipada o código Java e torná-lo um executável. Esse executável contém classes do aplicativo, classes de suas dependências, classes de bibliotecas de tempo de execução e o código nativo vinculado a JDK.  Após o processo de compilação, ele constrói o executável para o sistema operacional, esse processo se chama construção de imagem. Linguagens baseadas na JVM tem essa capacidade como, Java, Scala, Clojure e Kotlin.

### Spring Native
Em Março de 2021, o Spring liberou uma versão ainda experimental a comunidade o seu módulo nativo, o Spring-Native. Tendo em vista que seus concorrentes já conseguem ter uma integração mais flúida com o GraalVM, o spring precisou correr atrás do Quarkus e do Micronaut para conseguir tornar sua stack compatível com imagens nativas.

O Spring Native fornece a carga de trabalho ideal para computação em containers e Kubernetes. Utilizar imagem nativa forte uma inicialização instântanea, desempenho máximo instântaneo e consumo de memória reduzido.

Como tudo não é perfeito, é preciso entender que há etapas desse processo que precisam ser melhoradas, como p processo de geração de uma imagem nativa é muito pesado e demorado.


### Passos Necessários

Depois de configurar todo o ambiente, é necessário colocar as dependências necessárias para o projeto. Feito isso e você estruturando os endpoints que serão utilizados e o que será persistido, precisamos executar alguns comandos do maven para gerar o empacotamento do projeto. O primeiro comando a ser executado é o: mvn clean package spring-boot:build-image

Nesse projeto nos temos um plugin do maven que são gerados metadados necessários para o GraalVM no momento de compilação, o Spring  utiliza o paketo build. O paketo é um buildpack que transforma o código construiído em uma imagem que pode ser executado de qualquer forma. muito utilizado para execução de códigos em cloud.

Após ter gerado a imagem, será necessário executar o seguinte comando: mvn clean package spring-boot:build-image -Pspring-native,build-docker-image -DskipTests Dependendo de quanto de memória você tem disponível ou quanto de memória você tem para o startup do seu Docker, esse processo poderá falhar por falta de memória ou demorar até gerar a imagem.

Esse comando irá gerar uma imagem nativa GraalVM para realizar o build do aplicativo como um executável nativo.

Após a execução do comando que gera a imagem nativa da aplicação precisaremos subir o nosso banco de dados, nesse exemplo estamos utilizando o MongoDB, dessa forma o comando que será executado será: docker-compose up mongodb


Por último iremos rodar nossa aplicação reativa/Nativa com SpringWebFlux e Spring Native executando o seguinte comando: docker run spring-native-demo


### Tecnologias

Para a realização do projeto foram utilizada as seguintes tecnologias: 
- Java 11
- Maven
- SpringBoot
- Spring Webflux
- MongoDB
- Docker
- GraalVM
- PacketoBuild
