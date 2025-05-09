---
title: Introduzione a Java&trade; API QuickStart
description: Scopri come eseguire le operazioni di AEM Forms utilizzando l’API fortemente tipizzata di AEM Forms Java&trade abilitata con la connessione SOAP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5ae164d-d0c0-40d0-baeb-0e646fc71f55
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Introduzione a Java™ API Quick Start {#introducing-java-api-quickstart}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Guida introduttiva alle API AEM Forms di Adobe consente di accelerare gli sforzi per sviluppare programmi che interagiscono con i servizi di AEM Forms. *Guida rapida* s sono programmi completi che puoi copiare e incollare nei tuoi progetti e utilizzare come punto di partenza. Puoi eseguire una Guida rapida per vedere come si comporta e modificarla in base alle tue esigenze.

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

La Guida introduttiva dell’API fortemente tipizzata Java™ fornisce un elenco dei file JAR necessari per eseguire l’applicazione Java™. La maggior parte delle applicazioni Java™ Quick Starts sono applicazioni console eseguite in `main`. Tuttavia, Forms Java™ Quick Start per API fortemente tipizzate è implementato come servlet Java™ che viene eseguito all’interno di un’applicazione web.

L’elenco dei file JAR si trova in una sezione di commenti all’inizio della Guida introduttiva. Ad esempio, il seguente commento si trova in un Quick Start di output ed è un tipico elenco di file JAR presente in ogni Quick Start Java™.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Guida introduttiva a più servizi {#multiple-services-quick-start}

La maggior parte degli avvii rapidi in *Programmazione con AEM Forms su JEE* richiama un servizio specifico per eseguire un&#39;operazione. Tuttavia, alcuni Quick Starts richiamano più servizi AEM Forms per eseguire un determinato flusso di lavoro. L’elenco seguente fornisce avvii rapidi Java™ che richiamano più di un servizio AEM Forms:

[Guida rapida (modalità SOAP): passaggio di un documento nel repository AEM Forms al servizio di output tramite l&#39;API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (richiama il servizio di repository e output)

[Guida rapida (modalità SOAP): creazione di un documento PDF basato su frammenti tramite l&#39;API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (richiama il servizio Assembler e Output)

[Guida rapida (modalità SOAP): creazione di documenti PDF con dati XML inviati tramite l&#39;API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (richiama il servizio Forms, Output e Document Management)

[Guida rapida (modalità SOAP): passaggio di documenti al servizio Forms tramite l&#39;API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (richiama il servizio Forms e Document Management)

[Guida rapida (modalità SOAP): firma digitale di un modulo basato su XFA tramite l&#39;API Java™](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (richiama il servizio Forms e Signature)

[Guida rapida (modalità SOAP): gestione di ruoli e autorizzazioni tramite l&#39;API Java™](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (richiama il servizio DirectoryManager e AuthorizationManager )

[Guida rapida (modalità SOAP): passaggio di documenti al servizio di output tramite l&#39;API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (richiama il servizio di output e gestione dei documenti)

>[!NOTE]
>
>Gli avvii rapidi nella programmazione con AEM Forms si basano sull’implementazione di AEM Forms su JBoss® Application Server e sul sistema operativo Microsoft® Windows®. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX®, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La maggior parte dei servizi Web Quick Starts sono scritti in C# e utilizzano .NET Framework. Tuttavia, puoi creare una logica dell’applicazione client in grado di richiamare i servizi AEM Forms in qualsiasi ambiente di sviluppo che supporti gli standard SOAP. (Vedi [Chiamata di AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
