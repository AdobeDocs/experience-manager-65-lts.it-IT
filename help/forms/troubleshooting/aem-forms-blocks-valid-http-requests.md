---
title: AEM Forms blocca le richieste HTTP valide
description: I controlli di convalida XSS di AEM Forms possono bloccare le richieste HTTP valide per i clienti che utilizzano componenti personalizzati. Scopri come identificare il problema e ridurre temporaneamente i controlli di convalida.
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%
---
# AEM Forms blocca le richieste HTTP valide {#aem-forms-blocks-valid-http-requests}

## Problema {#issue}

AEM Forms include controlli di sicurezza per impedire attacchi cross-site scripting (XSS). Questi controlli possono bloccare alcune richieste HTTP valide per i clienti che utilizzano componenti personalizzati in AEM Forms. Quando una richiesta viene bloccata, nei registri del server viene visualizzato il seguente messaggio:

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>Per una richiesta POST, il valore predefinito per il parametro è **1048576**. Per una richiesta GET, il valore predefinito del parametro è **2000**. Per modificare il valore del parametro per una richiesta POST, passare l&#39;argomento `com.adobe.idp.dsc.provider.rest.httpParamMaxSize` durante l&#39;avvio del server.

## Causa {#cause}

Il regex di convalida XSS è più rigido del formato del valore del parametro inviato dal componente personalizzato, pertanto AEM Forms rifiuta la richiesta.

## Risoluzione {#resolution}

>[!CAUTION]
>
>La rimozione dei controlli di sicurezza rende il sistema vulnerabile ad attacchi cross-site scripting (XSS). Rimuovere i controlli di sicurezza solo come soluzione temporanea.

Per rimuovere temporaneamente i controlli di sicurezza e consentire tutte le richieste HTTP:

1. Arresta il server AEM Forms.

1. Creare un backup del file `[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear`.

1. Estrarre il file `esapi-helper-2.x.x.jar` dal file `adobe-livecycle-<server_name>.ear`. La posizione del file `esapi-helper-2.x.x.jar` varia per ciascun server applicazioni:

   | Server applicazioni | Posizione del file esapi-helper-2.x.x.jar |
   | --- | --- |
   | JBoss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle WebLogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. Aprire i file `[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties` e `[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties` per la modifica.

1. Impostare il valore delle proprietà seguenti su `^[\\s\\S]*$`. Ad esempio, `Validator.HTTPParameterName=^[\\s\\S]*$`. Salvare e chiudere i file.

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. Crea il pacchetto di `esapi-helper-2.x.x.jar` aggiornato in `adobe-livecycle-<application_server_name>.ear`. Distribuire `adobe-livecycle-<application_server_name>.ear` aggiornato nel server applicazioni.

1. Avvia il server AEM Forms.

## Riferimento {#references}

* [Mitigazione delle vulnerabilità SSRF (Server-Side Request Forgery) per AEM Forms in JEE 6.5 LTS SP2](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
