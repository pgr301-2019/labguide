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

Det kan være god praksis å skille infrastruktur fra app (det er diskusjoner rundt dette...) - og i dette faget velger i å lage et eget 
github repository for Github koden vår. Da er det enklere å lage en egen Travis pipeline, som reagerer på kun endringer i infrastrukturkoden. 

* Lag et helt nytt repo for infrastruktur for Spring boot eksemplet. 
* Flytt Terraform koden som du brukte for å lage en pipeline i Heroku dit. 
* Se på https://github.com/pgr301-2019/infra-repo-example for inspirasjon

# Lek med pipeline

Dere skal nå være i stand til å endre på infrastruktur koden, og Travis vil endre på infrastrukturen. Det er slik dere bør 
jobbe med IAC - og det er det eneste som virker for team og prosjekter av litt størrelse. 




