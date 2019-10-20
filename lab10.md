# Lab 10 - Logz.io

I denne labben skal vi se hvor enkelt det er å sende logger til en SAAS tjeneste som heter logz.io fra Spring Boot applikasjonen

## Sign up

https://app.logz.io - Det er meldt om problemer med å gjør sign up med Chrome og enkelt ad- blokkere. Bruk annen nettleser hvis dere ikke 
kommer dere forbi side en i registreringsskjemaet. 

## Ship logs 

* Se på "Ship logs" fanen i Logz.io, og let deg frem til "Libraries" og "Java Logback appender". Kopier logback.xml inn i en applikasjon du 
har gjort fra tidligere Lab (src/main/resources)
* Se på kodeeksemplet og lag punker i applikasjonen din som logger på ulike lognivåer 

Start applikasjonen lokalt - og du vil se at det kommer mindre logger i konsollet. Se på "Live view" i logz.io - loggene fra applikasjonen slal nå havne der.

## Pass på å logge både til standard out OG Logz.io

Modifiser Logback.xml slik at du også kan se loggene uten å gå til logz.io

```xml
<!-- Use debug=true here if you want to see output from the appender itself -->
<configuration>
    <!-- Use shutdownHook so that we can close gracefully and finish the log drain -->
    <shutdownHook class="ch.qos.logback.core.hook.DelayingShutdownHook"/>
    <appender name="LogzioLogbackAppender" class="io.logz.logback.LogzioLogbackAppender">
        <token>asasaas</token>
        <logzioUrl>https://listener.logz.io:8071</logzioUrl>
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
</configuration>```
