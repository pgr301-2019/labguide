# Lab 3

## Verifiser Docker på egen maskin

Fra med med forelesning 4 vil Docker være et sentralt verktøy i labbene - så
hvis du ennå ikke har Docker på plass, må dette gjøres i denne labben

## Bli kjent med skymiljø Travis & Heroku

I denne labben skal vi bli kjent med skytjenesten Heroku. Heroku er en tjenste i kategorien PAAS (Platform as a service). Den beste måten å bli kjent mer Heroku på, er å lage en Spring Boot applikasjon - og deploye den.

Vi skal  også bli kjent med Travis som er en SAAS løsning for CI med en generøs gratisplan. 

## Registrer for tjenester

* Registrer som bruker på GitHub (hvis ikke fra før)
* Registrer som ny bruker på Heroku
* Registrer som ny bruker på Travis - med GitHub brukeren din som identitet

## Installer CLI verktøy

* Installer CLI for Heroku
* Installer CLI for Travis

### Lag en en eksempelapplikasjon med spring initializer

Gå til https://start.spring.io/ - og lag en start-applikasjon etter eget ønske (maven/gradle/cotlin/java). Du må huske minst en dependency "Web starter" - for å få ting til å fungere. Du må også lag en ny RESTController - for eksempel ved å ta utgangspunk i denne koden; 

```java
package com.glennbech.lab3;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class Lab3Application {

	public static void main(String[] args) {
		SpringApplication.run(Lab3Application.class, args);
	}

	@RestController
	public static class SomeController {

		@RequestMapping("/hello")
		public String hello() {
			return "world";
		}

	}
}
```

Alternativt kan du ta utgangspunkt i dette repositoryet; https://github.com/pgr301-2019/lab3

### Deploy applikasjonen på Heroku.

Pakk ut applikasjonen i en mappe på maskinen din - og følg instruksjonene https://devcenter.heroku.com/articles/git
stop  ved avsnittet "https://devcenter.heroku.com/articles/git#http-git-authentication"

### Lag et nytt Github repo

Lag et nytt GitHub repo i din konto - og sjekk koden inn der. 

```
git remote add origin git@github.com:glennbech/demo.git
git push -u origin master
```

### Konfigurer bygging av applikasjonen med Travis

https://docs.travis-ci.com/user/tutorial/

### Konfigurer deployment til Heroku med Travis

https://docs.travis-ci.com/user/deployment/heroku/

NB! Eksempelet i dokumentasjonen forutsetter samsvar mellom GitHub repo-navn og Heroku applikasjon. Hvis dere bare har valgt et default Heroku navn - så vil dere få problemer. Dere må legge til "app" property. .travis_yml skal se tilsvarende dette ut etter dere har lagt til kryptert API nøkkel 

```language: java
deploy:
  provider: heroku
  app: murmuring-hamlet-96561
  api_key:
    secure: mZ7v/zvjmmDTIFoQ9wwurbTl28KClhTYfr4JOxTiUeD04lKaaYo5722LoqDG9W2kBaiZ/uZJzmvduO8yqKrvgQRssQybh3mgiAWy36idWtAmJJ3+2VJuVCmVs4cSQxVwVJeRPBEzmavFIQa7GXIzVnOPdDzpgkZVcF3P6cbyMKHgb45GvAxGasgOMRySe/k1Lq3mprMng50HC2QSy6rSui0lUCaPjy3N582e0HFM6SnFCXXhDw2yvyMeYa+gwuvLL4F/eIJjUxNJQ3z9OeX/tFoMswieVzPu08n8xBMc1z6+QdUqyk6XMxzJYMod6WW9RW/71Vu/OYNk9iPZEWfLAODXI22uNW7cofu5iKRRwUzKVM6kkGXIFHXpuRJkKK+1n/4eQvTIxT1lP6L0RoOHklverqB4INkE9GsV3avcgT7hdTZe4ryBrzYvTnkc0UiBaov0KpEBYKXNfg4VasOZ7II1/8HgNSJBR6Iuc7uHAZcqYEoF0EWqF31/FsCMUeaY6dZmXQVcBb+VTFg9puu4OMs76xOWqBlyjvWzyq95RDKKyXteo/Qudsl6R3UtNz6PpfVzOoDne8BA3MALzHp0pg2RQ1xVuteOZw/DXtwRpYxNqZVfSXti1yRm5qQp/nxy3oS8Zva5jlQgoc4JKbj9n4odJA8psolnv0IGr+WkvnU=
```



