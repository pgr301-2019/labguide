
# Kontinuerlig deployment til Heroku med Pipeline 

Målet med oppgaven er at Travis skal gjøre kontinuerlig deployment av applikasjonen fra master- men at endringen ikke skal gå "live" før du selv velger å promotrere applikasjonen som er i "staging". 

## Create a new Heroku pipeline 

Øvingen bygger på forrige lab - får du begynner på denne laben, sørg for at du har følgende på plass

* Et GitHib repo med en Spring boot app
* At Travis bygger på hver commit til master i repoet
* At du har en Heroku App  - som kjører Spring Boot applikasjonen
* Hver commit til master lager ny versjon av applikasjonen

# Se på instruksjonene i Heroku dokumentasjon

https://devcenter.heroku.com/articles/pipelines 

Her skal du bruke applikasjonen fra forrige lab i pipeline i "Staging". 

* Lag en ny app for production 

Sluttresultatet skal være som følger; 

* Du skal kunne gjøre commit mot github - travis skal bygge og deploye koden til staging
* Du skal kunne promotere staging til production i UI og på kommandolinje 
 
  
