# Vi lar Travis bygge og deploye container image

## Sette miljøvariable fro prosjektet

```
travis login
travis env set DOCKER_USERNAME myusername
travis env set DOCKER_PASSWORD secretsecret
```

Vi vil lage et shell script som gjør det vi gjorde på Docker kommandolinje 

```sh
#!/bin/bash
echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
docker build . --tag <image_name> --build-arg JAR_FILE=./build/libs/demo3-0.0.1-SNAPSHOT.jar
docker tag <image_name> <dockerhub_username>/<image_name>:latest
docker push glennbech/pgr301
```

* the $DOCKER_PASSWORD and $DOCKER_USERNAME refererer nå til miljøvariablene vi satte på travis CLI

Så må vi vi endre i .travis.yml

``` 
deploy:
  provider: script
  script: bash push.sh
  on:
    branch: master
```
