---
title: Monitoraggio delle distribuzioni di AEM Forms
description: È possibile monitorare le distribuzioni di AEM Forms sia a livello di sistema che a livello interno. Ulteriori informazioni sul monitoraggio delle distribuzioni di AEM Form sono disponibili in questo documento.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: aa02139f-7e47-4979-9560-5d270c36080b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Monitoraggio delle distribuzioni di AEM Forms {#monitoring-aem-forms-deployments}

È possibile monitorare le distribuzioni di AEM Forms sia a livello di sistema che a livello interno. Puoi utilizzare strumenti di gestione specializzati come HP OpenView, IBM® Tivoli e CA UniCenter e un monitor JMX di terze parti denominato *JConsole* per monitorare in modo specifico l&#39;attività Java™. L’implementazione di una strategia di monitoraggio migliora la disponibilità, l’affidabilità e le prestazioni delle distribuzioni di AEM Forms.

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## Monitoraggio tramite MBean {#monitoring-using-mbeans}

AEM Forms fornisce due MBean registrati che forniscono informazioni di navigazione e statistiche. Queste parti sono le uniche MBean supportate per l&#39;integrazione e l&#39;ispezione:

* **ServiceStatistic:** Questo MBean fornisce informazioni sul nome del servizio e sulla relativa versione.
* **OperationStatistic:** questo MBean fornisce le statistiche di ogni servizio del server AEM Forms. In questo MBean gli amministratori possono ottenere informazioni su un particolare servizio, ad esempio il tempo di chiamata e il numero di errori.

### Interfacce pubbliche ServiceStatisticMbean {#servicestatisticmbean-public-interfaces}

È possibile accedere alle seguenti interfacce pubbliche di ServiceStatistic MBean a scopo di test:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfacce pubbliche OperationStatisticMbean {#operationstatisticmbean-public-interfaces}

È possibile accedere alle seguenti interfacce pubbliche di OperationStatistic MBean a scopo di test:

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### Statistiche operazioni e struttura MBean {#mbean-tree-operation-statistics}

Utilizzando una console JMX (JConsole), sono disponibili le statistiche di OperationStatistic MBean. Queste statistiche sono attributi di MBean e possono essere visualizzate nella seguente struttura gerarchica:

**albero MBean**

**Nome dominio Adobe:** dipende dal server applicazioni. Se il server applicazioni non definisce il dominio, l&#39;impostazione predefinita è adobe.com.

**ServiceType:** AdobeService è il nome utilizzato per elencare tutti i servizi.

**AdobeServiceName:** Nome di servizio o ID di servizio.

**Versione:** Versione del servizio.

**Statistiche operazione**

**Tempo di chiamata:** Tempo impiegato per l&#39;esecuzione del metodo. Questa chiamata non include l&#39;ora in cui la richiesta viene serializzata, trasferita dal client al server e deserializzata.

**Conteggio richiami:** il numero di volte in cui il servizio viene richiamato.

**Tempo medio di chiamata:** Tempo medio di tutte le chiamate eseguite dall&#39;avvio del server.

**Tempo massimo di chiamata:** la durata della chiamata più lunga eseguita dall&#39;avvio del server.

**Tempo minimo di chiamata:** la durata della chiamata più breve eseguita dall&#39;avvio del server.

**Conteggio eccezioni:** numero di chiamate che hanno generato errori.

**Messaggio di eccezione:** Messaggio di errore dell&#39;ultima eccezione che si è verificata.

**Data e ora ultimo campionamento:** la data dell&#39;ultima chiamata.

**Unità di tempo:** Il valore predefinito è millisecondi.

Per abilitare il monitoraggio JMX, in genere i server applicazioni richiedono una certa configurazione. Per informazioni dettagliate, consulta la documentazione del server applicazioni.

### Esempi di come impostare l’accesso aperto JMX {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - configura l&#39;avvio JVM**

Per visualizzare MBean da JConsole, configurare i parametri di avvio JVM del server applicazioni JBoss. Assicurati che JBoss sia avviato dal file run.bat/sh.

1. Modifica il file run.bat che si trova in InstallJBoss/bin.
1. Trova la riga JAVA_OPTS e aggiungi quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configura l&#39;avvio JVM**

1. Modificare il file startWebLogic.bat che si trova in `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Trova la riga JAVA_OPTS e aggiungi quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Riavviare WebLogic.

>[!NOTE]
>
>Per WebLogic, è possibile accedere a MBean utilizzando remoto o IIOP.

**Accesso remoto a MBean**

1. Avviare JConsole per la nuova connessione e fare clic sulla scheda remota.
1. Immetti il nome host e la porta (9088, il numero specificato durante le opzioni di avvio di JVM).

**WebSphere® 6.1 - configurazione avvio JVM**

1. In Admin Console (Server applicazioni > server1 > Definizione processo > JVM), aggiungi la seguente riga al campo Argomento JVM generico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Aggiungi o rimuovi il commento dalle tre righe seguenti nel file /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;JRE WebSphere>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Riavviare WebSphere.
