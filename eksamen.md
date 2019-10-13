# Eksamensoppgave PGR301

## Fra Læreplan

Egenutviklet applikasjon (eller prototype) med tilhørende dokumentasjon: teller 100% av karakteren i emnet. Applikasjonen skal være utviklet, og være vedlikeholdbar, i et DevOps- miljø i skyen. Kildekode, og annen dokumentasjon, skal gjøres tilgjengelig for allmenheten."

Siden et kontinuerlig kjørende DevOps-miljø kan være kostnadsbærende for studentene vil vi lette på kravet om miljøet skal kjøre kontinuerlig i skyen. Applikasjonen må istedet være mulig å etablere i skyen ved hjelp av infrastruktur som kode (Terraform) - og enkel automatisering.

På den måten kan de som måtte ønske å ta løsningen i bruk ( for eksempel eksaminator ) bruke egen infrastruktur (og da ta kostnaden for drift av miljøet)

## Beskrivelse

"DominiGeiger" er et selskap som skal starte salg av personlige «wearable» geigertellere til privatpersoner i Europa. Veksten har vært astronomisk grunnet en befolkning i stor panikk etter serien «Chernobyl» på HBO. Selskapet  planlegger utvidelse i Asia etter det ble kjent at Japansk Franchise, «Fukushima Daiichi » også skal vises på HBO i 2020.

Data kommer inn i høy hastighet, over HTTP, og det forventes at nær 90% av familier i Europa,  med høy grad av strålingsangst,  vil skaffe seg en slik teller. Dette er naturligvis bra for DominiGeiger, men det betyr samtidig at løsningen må skalere bra, og de har derfor valgt å satse på skyen.

Geigertellerne er festet på brukerens klær, og derfor samler DomiGeiger inn hyppig og nøyaktig lokasjonsdata. Denne informasjonen skal selges til store internasjonale selskaper i en auksjonsløsning som skal utvikles senere (ikke en del av oppgaven)

Din jobb er å få prosjektet raskt i gang på riktig måte, med DevOps prinispper.

## Krav til Applikasjonen

* REST Endepunkt for ny geigerteller. Svare på POST til /device og returnere et objekt med en unik identifikator "deviceId"
* REST Endepunkt for ny måling av stråling og lokasjon (lat, lng, sievert). POST /device/{deviceId}/measurement  
* REST Endepunkt for å hente en eller flere målinger for en device. GET til /device/{id}/measurements
* REST Endepunkt for å liste alle målere. GET til /devices

Payload for responser kan dere bestemme selv.

## Krav til leveransen

* Applikasjonen og tilhørende DevOps infrastruktur skal gjøres tilgjenglig på GitHib
* Repositories som du lagert må være offentlige
* Du skal lage to repositories, ett for infrastruktur og ett for applikasjon. 
* Du skal levere et dokument (tekstfil) i wiseflow som lenker til leverte repositories i GitHub.
* Applikasjonen må ha database, men kan bruke en "embeded" som feks H2
* Applikasjonen må ha *meningsfylte* enhetstester, testdekning er ikke viktig.
* Du må lage en annonym Github bruker - brukernavnet må være utformet slik at det ikke går ann å utlede hvem du er basert på navnet.(Det må ikke være mulig ut ifra koden å identifsere studenten. Det er viktig å ikke benytte @author tags osv.)

## Evaluering

Applikasjonen skal være skrevet i henhold til  prinsipper i [the twelve factor app](https://12factor.net/)

Det vil bli gjort en vurdering per oppgavene nevnt under; Pipeline, Docker, Overvåkning, Metrics og logger. En samlet vurdering av selve applikasjonen og disse oppgavene vil utgjøre karakteren.   

# Terraform state

Terraform har et konsept om "state" som i praksis er et JSON dokument som holder orden knytningen til de faktiske ressurser i infrastrukturen og terraform koden. Denne JSON filen oppdateres kontinuerlig når infrastrukturen endrer seg, og må deles av teamet og med CI server. En mekanisme for lagring av en slik fil kalles en "backend" i Terraform.

Deter laget AWS nøkler for dere slik at dere kan lagre terraform state på objektlagringstjenesten til Amazon Web Services, S3. Disse finner dere på Slack og på Canvas. Disse må på ingen måte sjekkes inn i github. Hvis disse under eksamensperioden må invalideres på grunn av lekasje - vil det bli gitt informasjon på både Slack og Canvas. 

# Oppgave 1 -  Pipeline

## Infrastruktur

* Det skal opprettes tre applikasjoner i Heroku i en Heroku Pipeline. 

- CI (Contuinous integration) - Master branch i applikasjon-repository skal til enhver tid deployes i dette miljøet, dersom enhetstestene i prosjektet ikke feiler.
- Stage - Dette er et miljø som typisk brukes for tester, for eksmpel ytelses- eller sikkerhetstester.
- Prod - Dette er miljøet som kundene- eller brukerene av løsningen opplever.

Nødvendig infrastruktur skal  opprettes med Terraform.  * Eksaminator har ikke terraform installert på sin maskin. Travis skal opprette infrastrukturen * 

## Oppgave 1 - CI Pipeline

* Det skal lages en CI/CDpipeline for applikasjonen ved hjelp av Travis CI. 
* Det skal også være en tilsvarende pipeline for infrastruktur.
* Pipeline skal  deploye hver commit på master branch til "CI" miljøet i heroku, ved ok bygg og når testene ikke feiler. 
* Deployment fra CI-miljø videre til Stage og produksjon skal skje manuelt ved at man promoterer applikasjonen i Heroku UI (Eller CLI). Studentene kan fritt velge å implementre kontinuerlig deployment til stage, og fra stage til prod - men det gis ikke poeng for dette.

## Oppgave 2 Docker

I denne oppgaven skal dere sørge for at Travis bygger et nytt Docker image for hver commit til applikasjonen sin master branch - deretter gjør en push av dette til DockerHub. Heroku har begrenset støtte for Docker i pipelines, så dere trenger i denne oppgaven ikke løse deployment av Docker Image fra Docker hub til Heroku. 

Oppgaver som må løses

* Du skal skrive en Dockerfil som kan brukes for å bygge et Container Image av Spring Boot applikasjonen din.
* Du skal  utvide pipeline, til å bygge et Docker image fra Docker filen
* Docker image skal lastes opp til Docker Hub

## Oppgave 3 og Overvåkning og varsling

Denne oppgaven består av å implementere overvåkning, og varsling i applikasjonen.

- Implementer infrastruktur for varsling ved hjelp av SAAS tjenesten OpsGenie  
- Implementer infrastruktur for overvåkning ved hjelp av SAAS tjenesten StatusCake

Infrastrukturen skal opprettes ved hjelp av Terraform.

## Oppgave 4 Metrics

Applikasjonen skal logge egendefinerte metrics. Med det menes at man på valgte steder i applikasjonskoden skal logge datapunkter ved hjelp av rammeverket Micrometer.

I evalueringen vektlegges det at man ppplikasjonen er innholdsrik nok til å demonstrere forståelse av - og bruk av minst følgende type metrics  gauge, counter, DistributionSummary, Timer, LongTaskTimer.

Applikasjonen skal være konfigurert for levering av Metrics mot InfluxDB. Dere kan anta at influxDB kjører lokalt i en egen container på  eksaminator sin maskin når  oppgaven rettes. 


## Oppgave 5 Applikasjonslogger

Denne oppgaven består av å bruke en SAAS tjeneste, [Logz.io](https://app.logz.io/) for innsamling, visualisering og analyse av logger. Dere skal utvide applikasjonen på en slik måte at logger sendes til denne tjenesten. Spring boot applikasjonen må modifiseres slik at loggene sendes til tjenesten. 

OBS. Dere må ikke bruke Logz.io som en Heroku-addon. Det koster penger.

LYKKE TIL!
