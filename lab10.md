# Lab 10 - Logz.io

I denne labben skal vi se hvor enkelt det er å sende logger til en SAAS tjeneste som heter logz.io fra Spring Boot applikasjonen. Vi skal også se på 12 factor prinsippet "Config" ved å ikke hardkode token og endepunlt for Logz.io i property filer. 

## Registrer deg på logz.io

https://app.logz.io - Det er meldt om problemer med å gjør sign up med Chrome og enkelt ad- blokkere. Bruk annen nettleser hvis dere ikke 
kommer dere forbi side en i registreringsskjemaet. 

## Ship logs 

* Se på "Ship logs" fanen i Logz.io, og let deg frem til "Libraries" og "Java Logback appender". Kopier logback.xml inn i en applikasjon du 
har gjort fra tidligere Lab (src/main/resources)
* Se på kodeeksemplet og lag punker i applikasjonen din som logger på ulike lognivåer 

Start applikasjonen lokalt - og du vil se at det kommer mindre logger i konsollet. Se på "Live view" i logz.io - loggene fra applikasjonen slal nå havne der.

## Pass på å logge både til standard out og Logz.io

Modifiser Logback.xml slik at du også kan se loggene uten å gå til logz.io

```xml
<!-- Use debug=true here if you want to see output from the appender itself -->
<configuration>
    <!-- Use shutdownHook so that we can close gracefully and finish the log drain -->
    <shutdownHook class="ch.qos.logback.core.hook.DelayingShutdownHook"/>
    <appender name="LogzioLogbackAppender" class="io.logz.logback.LogzioLogbackAppender">
        <token>asasaas</token>
        <logzioUrl>https://some url: some port </logzioUrl>
        <logzioType>myType</logzioType>
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <level>DEBUG</level>
        </filter>
    </appender>

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <!-- encoders are assigned the type
             ch.qos.logback.classic.encoder.PatternLayoutEncoder by default -->
        <encoder>
            <pattern>%-4relative [%thread] %-5level %logger{35} - %msg %n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <!-- IMPORTANT: make sure to include this line, otherwise the appender won't be used -->
        <appender-ref ref="LogzioLogbackAppender"/>
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

## Heroku - Eksternalisering av config (12 factor app prinsipp)

Som du har lært i "The twelve factor app", skal konfigurasjon eksternaliseres til miljøet. Ta ut logzio IRL pg logzio token til miljøvariable. Dette kan gjøres ved å sette inn $LOGZ_TOKEN og $LOGZ_URL inn i logback filen, og sette verdiene LOGZ_URL og LOGZ_TOKEN som miljøvariable 
 
Bli kjent med hvordan dette gjøres ved å deploye applikasjonen til heroku - og la URL og Token være miljøvariable istedet for en del av logback.xml - Følg instruksjoner på ; https://devcenter.heroku.com/articles/config-vars

For å lage en Heroku applikasjon av Spring Boot koden du jobber med (dersom du ikke har en allerede)

```bash
heroku create
git push heroku master
```

Se ; https://devcenter.heroku.com/articles/git - hvis du trenger repetisjon av hvordan dette gjøres. 

## Lek med Logz.io

Bli kjent med minst 

* Live Tail
* kibana og "Discover" panelet, der man kan søke etter logger og filtrere på ulike felter i loggene
* Visialiering. Prøv gjerne mer avanserte greier - men i alle fall et Pie chart som fordeler logger i INFO, DEBUG, ERROR


