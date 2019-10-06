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

### LAB 7

I denne labben skal vi lage en en Docker Container av en Spring Boot applikasjon, kjøre den lokalt, og laste den opp til Docker Hub. Vi skal også få Travis til å gjøre denne jobben for oss som respons på en endring i repository 

[Se lab guide for detaljer](lab7.md)


### LAB 8

I denne øvingen skal vi bli kjent med Metrics-rammeverket Micrometer for Spring Boot, og hvordan vi kan lagre data i en lokal influxDB Time series database 

[Se lab guide for detaljer](lab8.md)

