---
title: Creazione di un handler per l’invito di utenti esterni
description: Scopri come creare un handler per l’invito di utenti esterni. Consente al servizio Rights Management di invitare utenti esterni a diventare utenti Rights Management.
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 5e1f1f3c-a2f3-4bf1-ba96-a02f8b16c180
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Creazione di un handler per l’invito di utenti esterni {#create-invite-external-users-handler}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Puoi creare un gestore per l’invito di utenti esterni per il servizio Rights Management. Un gestore per l’invito di utenti esterni consente al servizio Rights Management di invitare utenti esterni a diventare utenti di Rights Management. Dopo che un utente diventa un utente di Rights Management, può eseguire attività quali l’apertura di un documento PDF protetto tramite policy. Dopo aver distribuito ad AEM Forms il gestore per l’invito di utenti esterni, puoi utilizzare la console di amministrazione per interagire con esso.

>[!NOTE]
>
>Un gestore per l’invito di utenti esterni è un componente di AEM Forms. Prima di creare un gestore per l’invito di utenti esterni, è consigliabile acquisire familiarità con la creazione dei componenti.

**Riepilogo dei passaggi**

Per sviluppare un handler per l’invito di utenti esterni, è necessario attenersi ai seguenti passaggi:

1. Configura l’ambiente di sviluppo.
1. Definisci l’implementazione del gestore di invito degli utenti esterni.
1. Definite il file XML del componente.
1. Distribuisci il gestore di invito degli utenti esterni.
1. Verifica il gestore Invita utenti esterni.

## Configurazione dell’ambiente di sviluppo {#setting-up-development-environment}

Per configurare l’ambiente di sviluppo, devi creare un progetto Java, ad esempio un progetto Eclipse. La versione di Eclipse supportata è `3.2.1` o successiva.

L&#39;SPI di Rights Management richiede che il file `edc-server-spi.jar` sia impostato nel percorso della classe del progetto. Se non fai riferimento a questo file JAR, non puoi utilizzare la SPI di Rights Management nel tuo progetto Java. Questo file JAR è installato con AEM Forms SDK nella cartella `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`.

Oltre ad aggiungere il file `edc-server-spi.jar` al percorso della classe del progetto, è necessario aggiungere anche i file JAR necessari per utilizzare l&#39;API del servizio Rights Management. Questi file sono necessari per utilizzare l’API del servizio Rights Management nel gestore Invita utenti esterni.

## Definizione dell’implementazione del gestore di inviti di utenti esterni {#define-invite-external-users-handler}

Per sviluppare un gestore di inviti esterni, è necessario creare una classe Java che implementi l&#39;interfaccia `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Questa classe contiene un metodo denominato `invitedUser` che il servizio Rights Management richiama quando gli indirizzi e-mail vengono inviati tramite la pagina **Aggiungi utenti invitati** accessibile tramite la console di amministrazione.

Il metodo `invitedUser` accetta un&#39;istanza `java.util.List` che contiene indirizzi di posta elettronica di tipo stringa inviati dalla pagina **Aggiungi utenti invitati**. Il metodo `invitedUser` restituisce un array di `InvitedUserProviderResult` oggetti, che in genere è un mapping di indirizzi e-mail a oggetti utente (non restituisce null).

>[!NOTE]
>
>Oltre a dimostrare come creare un gestore di inviti di utenti esterni, questa sezione utilizza anche l’API AEM Forms.

L&#39;implementazione del gestore di inviti di utenti esterni contiene un metodo definito dall&#39;utente denominato `createLocalPrincipalAccount`. Questo metodo accetta un valore stringa che specifica un indirizzo e-mail come valore di parametro. Il metodo `createLocalPrincipalAccount` presuppone la preesistenza di un dominio locale denominato `EDC_EXTERNAL_REGISTERED`. Puoi configurare questo nome di dominio come qualsiasi altro nome desiderato; tuttavia, per un’applicazione di produzione, potrebbe essere utile eseguire l’integrazione con un dominio aziendale.

Il metodo `createUsers` scorre ogni indirizzo e-mail e crea un oggetto User corrispondente (un utente locale nel dominio `EDC_EXTERNAL_REGISTERED`). Infine, viene chiamato il metodo `doEmails`. Questo metodo viene lasciato intenzionalmente come stub nel campione. In un’implementazione di produzione, conterrebbe la logica dell’applicazione per inviare messaggi e-mail di invito agli utenti appena creati. Viene lasciato nell’esempio per dimostrare il flusso logico dell’applicazione di un’applicazione reale.

### Definizione dell’implementazione del gestore di inviti di utenti esterni {#user-handler-implementation}

L’implementazione del gestore di inviti esterni riportata di seguito accetta gli indirizzi e-mail inviati dalla pagina Aggiungi utenti invitati accessibile tramite la console di amministrazione.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>Questa classe Java viene salvata come file JAVA denominato InviteExternalUsersSample.java.

## Definizione del file XML del componente per il gestore autorizzazioni {#define-component-xml-authorization-handler}

Utilizza un file XML di componente per distribuire il componente gestore inviti utenti esterni. Esiste un file XML per ciascun componente che fornisce i metadati relativi al componente.

Il seguente file `component.xml` è utilizzato per il gestore di inviti di utenti esterni. Si noti che il nome del servizio è `InviteExternalUsersSample` e che l&#39;operazione esposta dal servizio è denominata `invitedUser`. Il parametro di input è un&#39;istanza `java.util.List` e il valore di output è un array di `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` istanze.

### Definizione del file XML del componente per il gestore di inviti di utenti esterni {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## Creazione del pacchetto del gestore di inviti di utenti esterni {#packaging-invite-external-users-handler}

Per distribuire il gestore di inviti di utenti esterni in AEM Forms, è necessario creare un pacchetto del progetto Java in un file JAR. Verificare che nel file JAR siano inclusi anche i file JAR esterni da cui dipende la logica di business del gestore inviti utenti esterni, ad esempio i file `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar`. Deve essere presente anche il file XML del componente. Il file `component.xml` e i file JAR esterni devono trovarsi nella radice del file JAR.

>[!NOTE]
>
>Nell&#39;illustrazione seguente viene visualizzata una classe `BootstrapImpl`. In questa sezione non viene illustrato come creare una classe `BootstrapImpl`.

L’illustrazione seguente mostra il contenuto del progetto Java inserito nel file JAR del gestore invita utenti esterni.

![Invita utenti](assets/ci_ci_InviteUsers.png)

A. File JAR esterni richiesti dal file JAVA del componente B.

Crea un pacchetto del gestore di inviti di utenti esterni in un file JAR. Nel diagramma precedente, si noti che sono elencati i file .JAVA. Una volta inseriti in un file JAR, è necessario specificare anche i file .CLASS corrispondenti. Senza i file .CLASS, il gestore autorizzazioni non funziona.

>[!NOTE]
>
>Dopo aver creato il pacchetto del gestore di autorizzazione esterno in un file JAR, puoi distribuire il componente in AEM Forms. È possibile distribuire un solo gestore di inviti di utenti esterni alla volta.

>[!NOTE]
>
>Puoi anche distribuire un componente a livello di programmazione.

## Verifica del gestore di inviti di utenti esterni {#testing-invite-external-users-handler}

Per testare il gestore di inviti di utenti esterni, puoi aggiungere utenti esterni da invitare utilizzando la console di amministrazione.

Per aggiungere utenti esterni da invitare tramite la console di amministrazione:

1. Distribuisci il file JAR del gestore inviti utenti esterni tramite Workbench.
1. Riavviare il server applicazioni.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Accedere alla console di amministrazione.
1. Fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configurazione]** > **[!UICONTROL Registrazione utente]** invitata.
1. Abilitare la registrazione degli utenti invitati selezionando la casella **[!UICONTROL Abilita registrazione utenti invitati]**. In **[!UICONTROL Usa sistema di registrazione predefinito]**, fare clic su **[!UICONTROL No]**. Salva le impostazioni.
1. Dalla home page della console di amministrazione, fare clic su **[!UICONTROL Impostazioni]** > **[!UICONTROL Gestione utente]** > **[!UICONTROL Gestione dominio]**.
1. Fare clic su **[!UICONTROL Nuovo dominio locale]**. Nella pagina seguente creare un dominio con il nome e il valore dell&#39;identificatore `EDC_EXTERNAL_REGISTERED`. Salva le modifiche.
1. Dalla home page della console di amministrazione, fare clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Utenti invitati e locali]**. Viene visualizzata la pagina **[!UICONTROL Aggiungi utente invitato]**.
1. Immetti gli indirizzi e-mail (poiché il gestore di inviti esterni corrente non invia effettivamente i messaggi e-mail, l’indirizzo e-mail non deve essere valido). Fare clic su **[!UICONTROL OK]**. Gli utenti vengono invitati al sistema.
1. Dalla home page della console di amministrazione, fare clic su **[!UICONTROL Impostazioni]** > **[!UICONTROL Gestione utente]** > **[!UICONTROL Utenti e gruppi]**.
1. Nel campo **[!UICONTROL Trova]**, immetti un indirizzo e-mail specificato. Fare clic su **[!UICONTROL Trova]**. L&#39;utente invitato viene visualizzato come utente nel dominio locale `EDC_EXTERNAL_REGISTERED`.

>[!NOTE]
>
>Il gestore di inviti di utenti esterni ha esito negativo se il componente viene arrestato o disinstallato.
