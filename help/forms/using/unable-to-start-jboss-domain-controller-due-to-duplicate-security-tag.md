---
title: Impossibile avviare il controller di dominio JBoss
description: Nelle distribuzioni del cluster LTS di AEM Forms 6.5.1 che utilizzano JBoss EAP 8, il file di configurazione potrebbe contenere un tag duplicato.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: f24e7245-7b43-4b1c-ba7a-162344ef545c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '152'
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
