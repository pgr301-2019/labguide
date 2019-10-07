# Metrics med Spring Boot, Micrometer og InfluxDB

I denne labben skal dere bli kjent med hvordan man instrumenterer en Spring Boot applikasjon med Metrics. Vi skal bruke rammeverket 
Micrometer som er integrert i Spring Boot - og tidsseriedatabasen influxDB


## Start influxDB

(Kilde https://blog.laputa.io/try-influxdb-and-grafana-by-docker-6b4d50c6a446) 

Vi kan få ut en influxdb konfigurasjonsfil fra container ved å kjøre kommandoen 

```sh
docker run --rm influxdb:1.0 influxd config > influxdb.conf
```

Dette kan være greit dersom vi ønsker å endre noe. Vi vil sende filen tilbake til containeren og overskrive med våre verdier 
når vi kjører influx

Vi kan starte influx med følgende docker kommando. Legg merke til av vi overstyrer konfigurasjonsfilen

```
docker run --name influxdb \
  -p 8083:8083 -p 8086:8086 -p 25826:25826/udp \
  -v $PWD/influxdb:/var/lib/influxdb \
  -v $PWD/influxdb.conf:/etc/influxdb/influxdb.conf:ro \
  -v $PWD/types.db:/usr/share/collectd/types.db:ro \
  influxdb:1.0
````

hvis dere går til http://localhost:8083/ får dere opp et enkelt brukergrensesnitt. 
 
## Instrumenter Spring Boot applikasjonen din med MicroMeter

I grove trekk kan dette gjøres ved å legge til de riktige avhengighetene til prosjeketet, og la Spring Boot plukke disse opp med 
autokonfigurasjon. Micrometer rammeverket kommer som en transitiv avhengighet med Spring Boot Actuator. Så, disse to linjene i build.gradle er det som skal til 

```groovy
	compile('org.springframework.boot:spring-boot-starter-actuator')
	compile 'io.micrometer:micrometer-registry-influx:latest.release'

```
Klassene deres kan da AutoWire inn en Spring Bean av typen MeterRegistry
```
  @Autowired
  private MeterRegistry meterRegistry;
```

# Ekstraoppgave

* Start Grafana lokalt med Docker - og få den til å vise data fra InfluxDB
* Deploy til Heroku og push metrikker til SAAS InfluxDB https://www.influxdata.com/products/influxdb-cloud/
