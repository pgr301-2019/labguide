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
* Registrer som ny bruker på Travis

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
helt frem til avsnittet "https://devcenter.heroku.com/articles/git#http-git-authentication"

### Konfigurer bygging av applikasjonen med Travis

### Konfigurer deployment til Heroku med Travis
