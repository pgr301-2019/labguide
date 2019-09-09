
# Kontinuerlig deployment til Heroku med Pipeline 

Målet med oppgaven er at Travis skal gjøre kontinuerlig deployment av applikasjonen fra master- men at endringen ikke skal gå "live" før du selv velger å promotrere applikasjonen som er i "staging". 

## Create a new Heroku pipeline 

Øvingen bygger på forrige lab - får du begynner på denne laben, sørg for at du har følgende på plass

* Et GitHib repo med en Spring boot app
* At Travis bygger på hver commit til master i repoet
* At du har en Heroku App  - som kjører Spring Boot applikasjonen
* Hver commit til master lager ny versjon av applikasjonen

# Se på instruksjonene i Heroku dokumentasjon

https://devcenter.heroku.com/articles/pipelines  - stopp ved "Pipelines ownership and transfer"

Improviser med følgende; 

* Her skal du bruke applikasjonen fra forrige lab i pipeline i "Staging". 
* Lag en ny app for production 
  
# Legg feature toggles til applikasjonen 

Togglz rammeverket kan brukes til dette; 

https://github.com/togglz/togglz

Quick start guide er her; https://www.togglz.org/
 
For eksempel på bygg med gradle og Javakode kan dere se på min demo-applikasjon - https://github.com/glennbech/demo32 - 

