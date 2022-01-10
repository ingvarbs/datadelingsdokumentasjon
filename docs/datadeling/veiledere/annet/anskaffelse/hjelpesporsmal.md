---
description: "Punkt til hjelp i vurderingen av IT-tjenester eller -systemer.\n\n\n\
  TBD: M\xE5 diskuterast td med innkj\xF8psfolka i Unit. Eller nokon i Uninett? Andre\
  \ p\xE5 USIT?"
title: "Hjelpesp\xF8rsm\xE5l ved anskaffelser av IT-tjenester"
---

# Hjelpespørsmål ved anskaffelser av IT-tjenester

Punkt til hjelp i vurderingen av IT-tjenester eller -systemer.


TBD: Må diskuterast td med innkjøpsfolka i Unit. Eller nokon i Uninett? Andre på USIT?

Punktene er utledet av [integrasjonsprinsippene](/docs/datadeling/prinsippene), [vedtak](/docs/datadeling/vedtak) og [anbefalingene](/docs/datadeling/god-praksis) i UH:IntArk.


IT-tjenesten må/bør ha et API vi kan integrere med.


* Har systemet et åpent grensesnitt?
* Det må være praktisk mulig å utvikle integrasjoner mot API-et.
* Integrasjonen må kunne utvikles av hvem som helst, og ikke bare leverandøren av IT-tjenesten.
* Dagens anbefaling er Web Services av typen RESTfulle API, eventuelt GraphQL, og at autentisering skjer via Oauth2.
	+ TODO: Lenker
	+ TBD: Kva ender vi med å anbefale i prosjektet?
* TODO: Sei noko om utforming av API?


Hvis systemet blir kildesystem for visse data, eller vil inneholde data som potensielt kan bli det senere:


* Kan API-et gi ut **alle** kildedata?
* Hvordan er ytelsen til API-et?
* Hvor godt dokumentert er API-et?
* Kan systemet gi ut data til alle mulige konsumenter, eller har leverandøren begrensinger? For eksempel maks antall spørringer over en periode eller maks antall konsumenter.
* Støtter systemet å sende ut notifikasjoner eller andre former for meldinger ved endringer i kildedata? Dette er nødvendig for å kunne støtte oppdateringer i sanntid.
	+ Per i dag bruker UH:IntArk meldingskøen RabbitMQ, med protokollen AMQP 0.91. Støttes alternativer bør kostnadene av konvertering vurderes. TODO: Lenke.


Hvis sluttbrukere skal logge på tjenesten:


* Pålogging skal skje via Feide med SAML eller OIDC. TODO: lenk til vedtak om autentisering, og Feide sin dokumentasjon.


Hvis systemet skal provisjoneres:


* Støtter systemet provisjonering via API, eller må data skrives inn manuelt? Manuelle dobbelregistreringer må vektlegges tungt negativt, siden det skaper ekstraarbeid og dårligere datakvalitet.
* Har systemet egen provisjonering, som kan hente fra andre API, eller må vi utvikle dette selv? Hvis ikke bør vurderingen legge på ekstrakostnad ved utvikling av konnektor for dette.
* Har API-et begrensinger ved skrivetilgang?
	+ Noen skytjenester har for eksempel rate limiting, som kan vere et hinder ved for eksempel studiestart, når tusenvis av studenter vil måtte registreres på kort tid.
* Har systemet noen form for opprydding i gamle data?


Hvis systemet skal brukes som [datalager for andre presentasjonslag](/docs/datadeling/god-praksis/integrasjonsmonster/datalager):


* Støtter API-et Oauth2 mot Feide?
* Kan systemet knytte endringer mot riktig bruker?
* Hva er responstiden til API-et? Å bruke et API mot et presentasjonslag setter høye krav til ytelsen, siden sluttbrukerne forventer rask respons.