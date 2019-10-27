# Bli kjent med Terraform provider for OpsGenie

Målet for denne øvingen er å bli bedre kjent med terraform ved å bruke verktøyet til å provisjonere noe "ikke teknisk" som brukere, team
og grupper for overvåkning av en løsning.

## Obs Obs 

Viktig informasjon om eksamen: Det viser seg at Terraform provideren til OpsGenie, ikke lar brukere på gratisplan opprette e-post integrasjoner. Dette kommer av at provider (ennå) ikke har støtte for å sette teameierskap på integrasjon - og at "globale" integrasjoner ikke er tillat på gratisplanen.  Dette er "straffen" for å leve på bleeding edge - Provider gikk live 18 september. (https://community.atlassian.com/t5/Opsgenie-articles/Opsgenie-s-Terraform-provider-is-now-live/ba-p/1181712)
Så derfor til eksamen angående OpsGenie; Terraformkode skal opprette brukere, team, schedule & rotation. Hensikten med oppgaven er å vise at Terraform kan brukes til ikke-tekniske ting, og at dere klarer å gjøre dere kjent med en terraform provider ut ifra dokumentasjon og eksperimentering - samt å sette denne inn i pipeline.

Bruk dokumentasjonen (som kanskje ikke er verdens beste) på https://www.terraform.io/docs/providers/opsgenie/index.html - for å 
opprette følgende med terraform. (Du kan kjøre terraform lokalt)

- Brukere
- Team
- Kalender for Teamet
- Vaktrotasjon

For å få dette til må du ha følgende provider deklarasjon 

```provider "opsgenie" {
  version = "0.2.3"
  api_url = "api.eu.opsgenie.com"
}

resource "opsgenie_user" "glenn" {
  username  = "post@glennbech.no"
  full_name = "Glenn Bech"
  role      = "User"
  locale    = "no_NO"
  timezone  = "Europe/Oslo"
} ... osv osvosv 
```

Miljøvariabel for Token settes feks slik ;set/export OPSGENIE_API_KEY=xyz123455-488b-4a1b-a2a7-æøå543212
Kjør terraform på lokal maskin. Det er bare å begynne å se på dokumentasjonen og improvisere ut ifra det.
