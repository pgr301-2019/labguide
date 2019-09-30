# Vi lar Travis bygge og deploye container image

Før dere begynner

* Pass på at dere har travis CLI installert
* Dere må ta utgangspunkt i et prosjekt gjort i tidligere lab, som bygger og deployer en enkel Spring Boot applikasjon ved hjelp av Travis
* Dere trenger ikke tenke på Heroky deployment i denne labben, og dere kan ta utgangspunkt i en tidligere lab som ikke deployer til Heroku for å redusere kompeksitet. 

## Sette miljøvariable for prosjektet

For at Travis skal kunne jobbe på vegne av deg mot Docker Hub trenger vi i å Travis nødvendige "credentials"

Travis kan lagre miljøvariabler per repository. Les igjennom dokumentasjonen (https://docs.travis-ci.com/user/environment-variables/) for bruk av disse

Brukernavn er ikke spesielt sensitivt (kanskje) så det legger vi inn på følgende måte 

```
travis login
travis env set DOCKER_USERNAME myusername
```

og etterpå 

```
travis encrypt DOCKER_PASSWORD=<password> --add env.matrix
```

Dette krypterer passordet med en offentlig nøkkel som er spesifikt for et repository, og legger det krypterte passordet inn i .travis.yml filen. Fordi kun travis CI, har den private nøkkelen kan dette nå trygt sjekkes inn i versjonskontroll. 

Vi vil lage et shell script som gjør det vi gjorde på Docker kommandolinje - og legge dett til i prosjektet.

```sh
#!/bin/bash
echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
docker build . --tag <image_name> --build-arg JAR_FILE=./build/libs/demo3-0.0.1-SNAPSHOT.jar
docker tag <image_name> <dockerhub_username>/<image_name>:latest
docker push <dockerhub_username>/pgr301
```

Så må vi vi endre i .travis.yml

``` 
deploy:
  skip_cleanup: true
  provider: script
  script: bash push.sh
  on:
    branch: master
```
