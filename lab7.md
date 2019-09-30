# LAB 7

Dockerize en Spring Boot applikasjon - og push denne til docker hub

Før du starte må du ha Docker installert på maskinen din. Hvis du kjører

```docker run hello-world``` 

Skal du få en output som ser slik ut ; 

```Unable to find image hello-world:latest locally
 Pulling repository hello-world
 91c95931e552: Download complete
 a8219747be10: Download complete
 Status: Downloaded newer image for hello-world:latest
 Hello from Docker.
 This message shows that your installation appears to be working correctly.

 To generate this message, Docker took the following steps:
  1. The Docker Engine CLI client contacted the Docker Engine daemon.
  2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
     (Assuming it was not already locally available.)
  3. The Docker Engine daemon created a new container from that image which runs the
     executable that produces the output you are currently reading.
  4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
     to your terminal.

 To try something more ambitious, you can run an Ubuntu container with:
  $ docker run -it ubuntu bash

 For more examples and ideas, visit:
  https://docs.docker.com/userguide/

```
For å lage en Docker Container av Spring Boot applikasjonen din må du lage en Dockerfile

```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","app.jar"

```

For å bruke Docker til å lage et Container Image kjører dere. Artifactname er filnavnet på JAR filen. 
Merk at dere må bygge med Maven eller Gradle før dere kjører kommandoen

```sh
docker build . --tag pgr301 --build-arg JAR_FILE=./build/libs/<artifactname>
```

For å starte en Container, kan dere kjøre 

```sh
docker run pgr301:latest
```

Vent litt. Dette fungerte jo ikke; dere må eksponere port 8080 fra Containeren på maskinen din. Dette kalles port mapping. 

```bash
 docker run -p 8080:8080 pgr301:latest
 ```
# Docker hub
 
Docker hub er en tjeneste som gjør det mulig å lagre container images sentralt, og dele disse med hele verden - eller bare et prosjekt eller team/organisasjon. 

For å fullføre denne labben må dere registrere dere på Dockerub. Dere skal deretter bygge  et container images lokalt - og "pushe" dette til Docker Hub.

## Registrer deg som bruker på Docker Hub

https://www.docker.com/products/docker-hub

## Bygg container image og push til docker hub

```
docker login
docker tag <tag> <username>/<tag_remote>
docker push <username>/<tag_remote>
```

Verdien <tag> er en *tag* som du bestemte deg for når du gjorde docker build. <tag_remote> kan du bestemme deg for, fordi det er verdien som skal brukes for docker hub. 

## Del på Slack

Når dere har pushet container image til Docker Hub - del navnet på slack (brukernavn/image) - og forsøk å kjøre andre sine images slik 

```
docker run brukernavn/image 
```
Husk eventuelle port mappings.





 
