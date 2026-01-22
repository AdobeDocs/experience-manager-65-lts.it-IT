---
title: Impossibile avviare il controller di dominio JBoss
description: Nelle distribuzioni del cluster LTS di AEM Forms 6.5.1 che utilizzano JBoss EAP 8, il file di configurazione potrebbe contenere un tag duplicato.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Impossibile avviare il controller di dominio JBoss

## Problema

In **distribuzioni cluster AEM Forms 6.5.1 LTS** tramite **JBoss EAP 8**, il file di configurazione
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` (e varianti specifiche del database) possono contenere un **tag di apertura duplicato `<security>`**.

Ciò causa una **configurazione XML non valida**, causando un errore di avvio del controller di dominio **JBoss** e impedendo l&#39;inizializzazione del cluster.

## Si applica a

* **Prodotto:** AEM Forms 6.5.1 LTS
* **Tipo di distribuzione:** cluster
* **Server applicazioni:** JBoss EAP 8.x
* **File di configurazione:**

   * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## Passaggi per la risoluzione dei problemi

1. Durante l&#39;avvio del controller di dominio è possibile osservare i seguenti errori:

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. Apri il file di configurazione pertinente:

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. Individuare il tag di apertura `<security>` duplicato.

   **Configurazione non corretta:**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. Rimuovere il tag di apertura aggiuntivo `<security>` in modo che la configurazione venga corretta come illustrato di seguito:

   **Configurazione corretta:**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. Salva il file e avvia il controller di dominio JBoss.

6. Assicurarsi che la stessa configurazione convalidata venga applicata in modo coerente in tutti i nodi del cluster.
