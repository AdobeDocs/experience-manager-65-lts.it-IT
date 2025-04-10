---
title: Gestione degli utenti Forms | Gestione dei dati utente
description: Scopri come il componente Gestione utenti di AEM Forms JEE consente di creare, autorizzare e gestire gli utenti che hanno bisogno di accedere ad AEM Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3f673798-7557-4cba-96b5-2f326e7e73a9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Gestione degli utenti Forms | Gestione dei dati utente {#forms-user-management-handling-user-data}

La gestione degli utenti è un componente di AEM Forms JEE che consente di creare, gestire e autorizzare gli utenti di AEM Forms ad accedere ad AEM Forms. La gestione degli utenti utilizza i domini come directory per ottenere informazioni sugli utenti. Sono supportati i seguenti tipi di dominio:

**Domini locali**: questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. Le password vengono memorizzate localmente e l&#39;autenticazione viene eseguita utilizzando un database locale.

**Domini ibridi**: questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. A differenza dei domini locali, i domini ibridi utilizzano un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

**Domini aziendali**: sono costituiti da utenti e gruppi che risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utenti non scrive sul sistema di storage di terze parti. Gestione utenti sincronizza invece le informazioni su utenti e gruppi con il database Gestione utenti. I domini Enterprise utilizzano anche un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Dati utente e archivi dati {#user-data-and-data-stores}

La gestione utente memorizza i dati utente in un database, ad esempio My Sql, Oracle, MS® SQL Server e IBM® DB2®. Inoltre, qualsiasi utente che abbia eseguito l&#39;accesso almeno una volta nelle applicazioni Forms su AEM Author all&#39;indirizzo `https://'[server]:[port]'lc`, verrà creato nell&#39;archivio di AEM. Pertanto, la gestione degli utenti viene memorizzata nei seguenti archivi di dati:

* Database
* Archivio AEM
* Archiviazione di terze parti come la directory LDAP

>[!NOTE]
>
>I dati archiviati in archivi di terze parti non rientrano nell&#39;ambito di questo documento. Contatta direttamente il fornitore di terze parti per gestire i dati utente in tali archivi.

### Database {#database}

Gestione utenti memorizza i dati utente nelle tabelle di database seguenti:

<table>
 <tbody>
  <tr>
   <td>Tabella di database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Memorizza informazioni sulle entità principali. Un’entità principale può essere un utente, un gruppo o un ruolo.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Memorizza le informazioni personali (PII, personally identifiable information) degli utenti. Contiene una voce per ogni utente dai domini locali, aziendali e ibridi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(database Oracle e MS® SQL)</p> </td>
   <td>Memorizza i dati solo per gli utenti locali.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(database Oracle e MS® SQL)</p> </td>
   <td>Contiene le voci di tutti gli utenti dai domini locali, aziendali e ibridi. Contiene gli ID e-mail degli utenti.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (database Oracle e MS® SQL)</p> </td>
   <td>Memorizza la mappatura tra utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Memorizza il mapping tra ruoli e utenti/gruppi/ruoli sia per gli utenti che per i gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Memorizza la mappatura tra entità e autorizzazioni per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (database Oracle e MS® SQL)</p> </td>
   <td>Memorizza i valori di attributo vecchi e nuovi corrispondenti a un'entità.<br /> </td>
  </tr>
 </tbody>
</table>

### Archivio AEM {#aem-repository}

I dati di gestione utente per gli utenti che hanno effettuato almeno un accesso alle applicazioni Forms in `https://'[server]:[port]'lc` vengono memorizzati anche nell&#39;archivio di AEM.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

Puoi accedere ed esportare i dati di gestione utente per gli utenti nei database di gestione utenti e nell’archivio AEM e, se necessario, eliminarli definitivamente.

### Database {#database-1}

Per esportare o eliminare i dati utente dal database di gestione utenti, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID entità in base ad alcuni dati PII dell&#39;utente. Ad esempio, per recuperare l&#39;ID entità di un utente che utilizza un ID di accesso, eseguire il comando `select` seguente nel database.

Nel comando `select`, sostituire `<user_login_id>` con l&#39;ID di accesso dell&#39;utente di cui si desidera recuperare l&#39;ID principale.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta individuato l’ID principale, puoi esportare o eliminare i dati utente.

#### Esporta dati utente {#export-user-data}

Eseguire i seguenti comandi di database per esportare i dati di gestione utente per un ID entità dalle tabelle di database. Nel comando `select`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera esportare i dati.

>[!NOTE]
>
>I comandi seguenti utilizzano i nomi delle tabelle di database nei database My SQL e IBM® DB2®. Quando si eseguono questi comandi su database Oracle e MS® SQL, sostituire i seguenti nomi di tabella nei comandi:
>
>* Sostituisci `EdcPrincipalLocalAccountEntity` con `EdcPrincipalLocalAccount`
>
>* Sostituisci `EdcPrincipalEmailAliasEntity` con `EdcPrincipalEmailAliasEn`
>
>* Sostituisci `EdcPrincipalMappingEntity` con `EdcPrincipalMappingEntit`
>
>* Sostituisci `EdcPrincipalGrpCtmntEntity` con `EdcPrincipalGrpCtmntEnti`
>

```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Elimina dati utente {#delete-user-data}

Per eliminare i dati di gestione utenti per un ID entità dalle tabelle del database, procedere come segue.

1. Eliminare i dati utente dal repository di AEM, se applicabile, come descritto in [Eliminare i dati utente](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Arresta il server AEM Forms.
1. Eseguire i seguenti comandi di database per eliminare i dati di gestione utente per un ID entità dalle tabelle di database. Nel comando `Delete`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera eliminare i dati.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Avvia il server AEM Forms.

### Archivio AEM {#aem-repository-1}

Gli utenti di Forms JEE hanno i propri dati nell’archivio di AEM se hanno effettuato l’accesso all’istanza di authoring di AEM Forms almeno una. Puoi accedere ai dati utente ed eliminarli dall’archivio di AEM.

#### Accedere ai dati utente {#access-user-data}

Per visualizzare l&#39;utente creato nel repository di AEM, accedere a `https://'[server]:[port]'/lc/useradmin` con le credenziali di amministratore AEM. Tieni presente che `server` e `port` nell&#39;URL sono quelli dell&#39;istanza Autore AEM. Qui puoi cercare gli utenti con il loro nome utente. Fare doppio clic su un utente per visualizzare informazioni quali proprietà, autorizzazioni e gruppi per l&#39;utente. La proprietà `Path` per un utente specifica il percorso del nodo utente creato nell&#39;archivio di AEM.

#### Elimina dati utente {#delete-aem}

Per eliminare un utente:

1. Vai a `https://'[server]:[port]'/lc/useradmin` con le credenziali di amministratore AEM.
1. Cercare un utente e fare doppio clic sul nome utente per aprire le proprietà utente. Copia la proprietà `Path`.
1. Vai a AEM CRXDE Lite all&#39;indirizzo `https://'[server]:[port]'/lc/crx/de/index.jsp` e naviga o cerca nel percorso utente.
1. Elimina il percorso e fai clic su **[!UICONTROL Salva tutto]** per eliminare definitivamente l&#39;utente dall&#39;archivio di AEM.
