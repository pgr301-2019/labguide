# LAB 9 - Terraform i Travis CI pipeline 

I denne oppgaven skal vi se nærmere på terraform - og hvordan vi kan få Travis til å kjøre infrastrukturkoden , og ikke være avhengig av at 
teammedlemmer kjører Terraform fra lokal maskin.

# Terraform state

Terraform har et konsept om "state" som i praksis er et JSON dokument som holder orden knytningen til de faktiske ressurser i infrastrukturen og 
ressurser i terraform koden. Denne JSON filen oppdateres kontinuerlig, og må deles av teamet og med CI server. En lagring av slik state
kalles en "backend" i Terraform. 

Jeg har laget AWS nøkler for dere slik at dere kan lagre terraform state på objektlagringstjenesten til Amazon Web Services, S3. 

Terraform _provider.tf_ skal da se slik ut 

```
terraform {
  backend "s3" {
    bucket = "pgr301bucket"
    key    = "<unik_id>/terraform.tfstate"
    region = "eu-north-1"
  }
}
```

# Infrastruktur - repo

Det kan være god praksis å skille infrastruktur fra app (det er diskusjoner rundt dette...) - og i dette faget velger i å lage et eget github repository for Github koden vår. Da er det enklere å lage en egen Travis pipeline, som reagerer på kun endringer i infrastrukturkoden. 

* Lag et helt nytt repo for infrastruktur for Spring boot eksemplet. 
* Flytt Terraform koden som du brukte for å lage en pipeline i Heroku dit. 
* Se på https://github.com/pgr301-2019/infra-repo-example for inspirasjon

## Hemmeligheter 

For at Travis skal kunne deploye kode til Heroku - og for at Travis skal få lov til å skrive terraform state til AWS S3 - må vi legge til "hemmeligheter" med travis encrypt på kommandlinje 

travis encrypt HEROKU_EMAIL=your.email@somewhere.com --add
travis encrypt HEROKU_API_KEY=69ecad49-7d50-416a-8861-329ca3fa2940 --add
travis encrypt AWS_ACCESS_KEY_ID=<KEY> --add
travis encrypt AWS_SECRET_ACCESS_KEY=<SECRET_ACCESS_KEY>
  
Disse kommandoene krypterer hemmeligheter med repoets offentlige nøkke, og legger veridiene inn i .travis.yml - du må huske på å sjekke inn/pushe - filen etterpå. Disse verdiene / nøklene blir miljøvariabler og gjort tilgjengelig for Travis og applikasjonen.

# Lek med pipeline

Dere skal nå være i stand til å endre på infrastruktur koden, og Travis vil endre på infrastrukturen. Det er slik dere bør 
jobbe med IAC - og det er det eneste som virker for team og prosjekter av litt størrelse. 




