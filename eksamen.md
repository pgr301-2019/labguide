# Eksamensoppgave PGR301

## Fra Læreplan

"Egenutviklet applikasjon (eller prototype) med tilhørende dokumentasjon: teller 100% av karakteren i emnet. Applikasjonen skal være utviklet, og være vedlikeholdbar, i et DevOps- miljø i skyen. Kildekode, og annen dokumentasjon, skal gjøres tilgjengelig for allmenheten."

Siden et kontinuerlig kjørende DevOps-miljø kan være kostnadsbærende for studentene vil vi lette på kravet om miljøet skal kjøre kontinuerlig i skyen. Applikasjonen må istedet være mulig å etablere i skyen ved hjelp av infrastruktur som kode (Terraform) - og enkel automatisering.

På den måten kan de som måtte ønske å ta løsningen i bruk ( for eksempel eksaminator ) bruke egen infrastruktur (og da ta kostnaden for drift av miljøet)

## Beskrivelse

DominiGeiger er et selskap som skal starte salg av personlige «wearable» geigertellere til privatpersoner i Europa. Veksten har vært astronomisk grunnet en befolkning i stor panikk etter serien «Chernobyl» på HBO. Prosjektet er viktig for selskapet som ogspå planlegger utvidelse i Asia etter det ble kjent at Japansk Franchise, «Fukushima Daiichi » også skal vises på HBO i 2020.

Data kommer inn i høy hastighet, over HTTP, og det forventes at nær 90% av familier i Europa,  med høy grad av strålingsangst,  vil skaffe seg en slik teller. Dette er naturligvis bra for DominiGeiger, men det betyr samtidig at løsningen må skaledere bra, og de har valgt å satse på skyen. 

Geigertellerne er festet på brukerens klær, og derfor samler DomiGeiger inn hyppig og nøyaktig lokasjonsdata. Denne informasjonen skal selges til store internasjonale selskaper i  en auksjonsløsning som skal utvikles senere (ikke en del av oppgaven)

Din jobb er å få prosjektet raskt i gang på riktig måte, med DevOps prinispper. 

## Krav til leveransen

Applikasjonen og tilhørende DevOps infrastruktur skal gjøres tilgjenglig i GitHib repositories.

* Du må lage en annonym Github bruker - brukernavnet må være utformet slik at det ikke går ann å utlede hvem du er basert på navnet. 
* Repositories som du lagert må være offentlige
* Det må ikke være mulig ut ifra koden å identifsere studenten. Det er viktig å ikke benytte @author tags osv.
* Du skal levere et dokument (tekstfil) i wiseflow som lenker til relevante repositories i GitHub 

Det skal lages to repositories,

* Infrastruktur (terraform/ci)
* Applikasjon.

## Krav til Applikasjonen

* REST Endepunkt for ny geigerteller. Svare på POST til /device og returnere et objekt med en unik identifikator
* REST Endepunkt for ny måling av stråling. POST /device/{deviceId}  
* REST Endepunkt for å liste alle tellere. GET til /device
* REST Endepunkt for å hente alle målinger for en device. GET til /device/{id}

Payload for REST endepunkter kan dere bestemme selv. 

## Krav til Infrastruktur

* Det skal opprettes tre identiske miljøer

- CI (Contuinous integration) - Master branch i applikasjon-repository skal til enhver tid installeres i dette miljøet.   
- Stage - Dette er et miljø som typisk brukes for tester, for eksmpel ytelses- eller sikkerhetstester.
- Prod - Dette er miljøet som kundene- eller brukerene av løsningen opplever.

Nødvendig infrastruktur skal så langt det lar seg gjøre opprettes med Terraform. Det skal ikke være nødvendig å for eksaminator å ha terraform installert på PC for å etablere infrastrukturen - terraformkoden skal kjøres av CI/CD verktøy For Infrastruktur som på ingen måte kan opprettes med Terraform, kan dere lage instruksjoner i README.md i <infra-repository>    

## Krav til DevOps Pipeline

Det skal lages en CI/CDpipeline for applikasjonen.

* CI/CD Pipeline skal bygge både infrastruktur og kode.
* Pipeline skal kontinuerlig deploye hver commit på master branch til "CI" miljøet.
* Deployment fra CI-miljø videre til Stage og produksjon skal i utgangspunktet skje manuelt ved at man promoterer applikasjonen i Heroku UI () slik vi har gjort det i øvingene). Studentene kan fritt velge å implementre kontinuerlig deployment til stage, og fra stage til prod - men det gis ikke poeng for dette.

## Evaluering

Fullstendig oversikt over kriteriene for vurdering blir gitt innen tidsfrist. I grove trekk vil følgende bli vektlagt

### Bruk av Docker 

Oppgaven kan løses ved hjelp av Heroku og deres løsning for bygg av artifakter (slugs). Evalueringen vil gi poeng for bruk av Docker - en mer plattformnøttral teknologi

### Overvåkning og varsling 

Evalueringen vil basere seg på hvordan løsningen kan overvåkes - og hvordan varsling skjer ved feil. 

### Metrics 

Evalueringen vil ta hensyn til hvordan applikasjonen gir fra seg egendefinerte metrics. Med det menes at man på valgte steder i applikasjonskoden skal logge datapunkter.

### Logging 

Evalueringen vil ta hensyn til hvordan applikasjonen logger og legger til rette for sentralisert eller desentralisert loganalyse 


LYKKE TIL !!
