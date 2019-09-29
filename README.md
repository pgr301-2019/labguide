# labs

### Lab 1 & 2

Målet for Lab dag 1/2 er som følger

- Du skal ha Docker installert på maskinen din (og Docker skal fungere)
- For Windowsbrukere, valgfritt for MAC: Du skal ha en verktøy som git deg tilgang til et Ubuntu-miljø (Virtual Box feks)
- Du skal lage eller tilpasse en liten applikasjon som har en database (kan være in memory) helst er laget i Spring Boot og må bygge med Maven eller Gradle. Kan skrives i valgfritt språk så lange disse kravene er oppfylt
- Du skal ha en Github bruker, og sende brukernavnet til post@glennbech.no

### Lab 3
Github for versjonskontroll, Travis for bygg & deploy, blir kjent med Heroku og deployment. 

[Se lab guide for detaljer](lab03/README.md)

### Lab 4
Heroku pipelines

[Se lab guide for detaljer](lab04.md)

## Lab 5

Installere Terraform 

https://www.terraform.io/intro/getting-started/install.html

Tema for dagen er Infrastruktur som kode. Målet er å opprette Heroku pipeline som vi til nå har laget manuelt i Heroku UI ved å bruke Terraform. Eksempel på hvordan lage en enkel app med Terrfaform finner dere her;
https://github.com/PGR301-2018/heroku_example

Nå skal dere bruke dokumentasjonen, og lage en hel pipeline - https://www.terraform.io/docs/providers/heroku/index.html


## Lab 6 

Gjøre arbeid synlig 

I denne øvingen skal vi leke med trello.com - og lage et Team, og et Kanban board som er knyttet til et GitHub repository. 

Du skal gjøre følgende

* Registrer deg på trello.com - det er gratis. 
* Lag et team, og inviter minst en medstudent 
* Lag en nytt board - og lag passende kolonner (TODO, In progress, QA, Done , Prod - som eksempel) 
* Legg til en GitHub "Power up" til boardet.
* Sjekk at du kan lage en pull request i GitHub, og knytte den mot et "kort" i trello. Legg den til QA. For å få til dette er det enklest å knytte kortet til et offentlig repository

Mer avansert Terraform 

* Du skal lage en terraform modul, og publisere den på et offentlig github repository 
* Du skal konsumere en terraform modul som med medstudent publiserer på et offentlig GitHub repository

Det er lov å se på en eksemp klient https://github.com/pgr301-2019/terraform-module-client til en eksempel modul  https://github.com/pgr301-2019/terraform-module-example for inspirasjon - men finn grerne på moe selv.  Når dere er ferdig, post GitHub URL til kopmpoenten deres på Slack. 


# LAB 7

Dockerize en Spring Boot applikasjon

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
docker build . --tag pgr301 --build-arg build/libs/<artifactname>
```

For å starte en Container, kan dere kjøre 

```sh
docker run pgr301:latest
```

Vent litt. Dette fungerte jo ikke; dere må eksponere port 8080 fra Containeren på maskinen din. Dette kalles port mapping. 

```bash
 docker run -p 8080:8080 pgr301:latest
 ```
 


