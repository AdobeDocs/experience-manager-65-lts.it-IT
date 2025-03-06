---
title: Accesso WebDAV
description: Scopri come accedere ad Adobe Experience Manager utilizzando WebDAV.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 7aa0e3b3-69de-4991-a1c8-06c9de5404c4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# Accesso WebDAV{#webdav-access}

Per connettersi ad AEM tramite WebDAV con KDE:

AEM offre il supporto WebDAV che consente di visualizzare e modificare il contenuto dell’archivio. La connessione tramite WebDAV consente l&#39;accesso diretto all&#39;archivio dei contenuti attraverso il desktop. I file di testo e PDF aggiunti all’archivio tramite la connessione WebDAV vengono automaticamente indicizzati in formato full-text e possono essere cercati con le interfacce di ricerca standard e tramite le API Java™ standard.

## Generale {#general}

[In questo documento sono incluse istruzioni dettagliate per il sistema operativo](/help/sites-administering/webdav-access.md#connecting-via-webdav). Tuttavia, per connettersi al repository utilizzando il protocollo WebDAV, il client WebDAV deve essere indirizzato al percorso seguente:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Questo URL, se connesso dal livello del sistema operativo, fornisce accesso WebDAV all&#39;area di lavoro predefinita ( `crx.default`). Pur essendo più semplice per l&#39;utente, non offre la flessibilità aggiuntiva di specificare i nomi dell&#39;area di lavoro, che può essere eseguita utilizzando ulteriori [URL WebDAV](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visualizza il contenuto dell’archivio come segue:

* Un nodo di tipo `nt:folder` viene visualizzato come cartella. I nodi sotto il nodo `nt:folder` vengono visualizzati come contenuto della cartella.

* Un nodo di tipo `nt:file` viene visualizzato come file. I nodi sotto il nodo `nt:file` non vengono visualizzati, ma costituiscono il contenuto del file.

Quando si utilizza WebDAV per creare e modificare cartelle e file, AEM crea e modifica i nodi `nt:folder` e `nt:file` necessari. Se si prevede di utilizzare WebDAV per importare ed esportare contenuti, provare a utilizzare il più possibile i tipi di nodo `nt:file` e `nt:folder`.

>[!NOTE]
>
>Prima di configurare WebDAV, controllare i [requisiti tecnici](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL WebDAV {#webdav-urls}

L&#39;URL del server WebDAV ha la seguente struttura:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Descrizione</strong></td>
   <td>Host e porta su cui viene eseguito AEM</td>
   <td>Percorso per l’app web dell’archivio di AEM</td>
   <td>Percorso a cui è mappato il servlet WebDAV</td>
   <td>Nome dell’area di lavoro</td>
  </tr>
 </tbody>
</table>

Modificando l&#39;elemento dell&#39;area di lavoro nel percorso, è possibile mappare aree di lavoro diverse da quelle predefinite ( `crx.default`). Ad esempio, per mappare un&#39;area di lavoro denominata `staging`, utilizzare il seguente URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Connessione tramite WebDAV {#connecting-via-webdav}

[Come indicato in precedenza](/help/sites-administering/webdav-access.md#general), per connettersi all&#39;archivio utilizzando il protocollo WebDAV, puntare il client WebDAV alla posizione dell&#39;archivio. Tuttavia, a seconda del sistema operativo in uso, i passaggi necessari per la connessione del client sono diversi e potrebbe essere necessaria una configurazione del sistema operativo.

Vengono fornite istruzioni su come collegare i seguenti sistemi operativi:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Per connettere correttamente un sistema Microsoft® Windows 7 (e versioni successive) a un&#39;istanza di AEM non protetta con SSL, l&#39;opzione per stabilire l&#39;autenticazione di base su una rete non protetta deve essere abilitata in modo esplicito in Windows. Questa funzionalità richiede una modifica nel Registro di sistema di Windows di WebClient.

Una volta aggiornato il Registro di sistema, è possibile mappare l’istanza AEM come unità.

#### Configurazione Windows 7 e versioni successive {#windows-and-greater-configuration}

Per aggiornare il Registro di sistema in modo da consentire l&#39;autenticazione di base su una rete non protetta:

1. Individuare la seguente sottochiave del Registro di sistema:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Impostare la sottochiave della voce del Registro di sistema `BasicAuthLevel` su un valore pari o superiore a `2`.

   Se non è presente, aggiungi la sottochiave.

1. Riavviare il sistema per rendere effettiva la modifica del Registro di sistema.

>[!NOTE]
>
>Adobe consiglia di creare un utente di Windows con le stesse credenziali dell&#39;utente del repository, altrimenti potrebbero verificarsi conflitti di autorizzazioni.

#### Configurazione Windows 8 {#windows-configuration}

Per Windows 8, modificare la voce del Registro di sistema [come descritto per Windows 7 e versioni successive](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Tuttavia, prima di eseguire questa operazione, è necessario abilitare Esperienza desktop per visualizzare la voce del Registro di sistema.

Per abilitare l&#39;esperienza desktop, aprire **Server Manager**, quindi **Funzionalità**, **Aggiungi funzionalità**, quindi **Esperienza desktop**.

Dopo il riavvio, è disponibile la voce del Registro di sistema descritta per Windows 7 e versioni successive. Modificarlo come descritto per Windows 7 e versioni successive.

#### Connessione in Windows {#connecting-in-windows}

Per connettersi a AEM tramite WebDAV in un ambiente Windows:

1. Apri **Esplora risorse** o **Esplora risorse** e fai clic su **Computer** o **Questo PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Per avviare la procedura guidata, fare clic su **Mappa unità di rete**.
1. Immetti i dettagli della mappatura:

   * **Unità**: scegliere una lettera disponibile
   * **Cartella**: `http://localhost:4502`
   * Seleziona **Connetti utilizzando credenziali diverse**

   Fai clic su Fine

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizza tale numero di porta invece di 4502. Inoltre, se non si esegue l&#39;archivio dei contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. Immettere nome utente `admin` e password `admin`. Adobe consiglia di utilizzare l’account admin preconfigurato per i test.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. La procedura guidata si chiude e l&#39;unità appena mappata viene aperta in una finestra Esplora risorse o Esplora file.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

AEM è ora mappato come unità tramite WebDAV e può essere utilizzato come qualsiasi altra unità.

### macOS {#macos}

Non sono necessari passaggi di configurazione per la connessione tramite WebDAV su macOS. È possibile connettersi al server WebDAV.

1. Passare a una finestra di **Finder** e fare clic su **Vai** e **Connetti al server** oppure premere **Comando+k**.
1. Nella finestra **Connetti al server**, immettere il percorso di AEM:

   * `http://localhost:4502`

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizza tale numero di porta invece di 4502. Inoltre, se non si esegue l&#39;archivio dei contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. Quando viene richiesta l&#39;autenticazione, immettere il nome utente `admin` e la password `admin`. Adobe consiglia di utilizzare l’account admin preconfigurato per i test.

macOS è ora connesso ad AEM tramite WebDAV e può essere utilizzato come qualsiasi altra cartella sul Mac.

### Linux® {#linux}

La connessione tramite WebDAV su Linux® non richiede alcuna configurazione, ma richiede alcuni passaggi per effettuare la connessione, che variano a seconda dell&#39;ambiente desktop.

#### GNOME {#gnome}

Per connettersi ad AEM tramite WebDAV con GNOME:

1. In Nautilus (Esplora file), selezionare **Places** e **Connetti al server**.
1. Nella finestra **Connetti al server**, selezionare WebDAV (HTTP) in Tipo di servizio.

1. In **Server**, immettere `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizza tale numero di porta invece di 4502. Inoltre, se non si esegue l&#39;archivio dei contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. In **Cartella**, immetti `/dav`
1. Immettere il nome utente `admin`. Adobe consiglia di utilizzare l’account admin preconfigurato per i test.
1. Lascia vuota la porta e immetti un nome per la connessione.
1. Fai clic su **Connetti**. AEM richiede la password.
1. Immettere la password `admin` e fare clic su **Connetti**.

GNOME ha ora montato AEM come volume e puoi utilizzarlo come qualsiasi altro volume.

#### KDE {#kde}

1. Aprire la Creazione guidata cartella di rete.
1. Selezionare **WebFolder**(webdav) e fare clic su Avanti.
1. In **Nome** digitare un nome di connessione.
1. In **Utente**, immetti `admin.`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato.
1. In **Server**, immettere `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizza tale numero di porta invece di 4502. Inoltre, se non si esegue l&#39;archivio dei contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente

1. In **Cartella**, immetti `dav`

1. Fai clic su **Salva e connetti**.
1. Quando viene richiesta la password, immettere la password `admin` e fare clic su **Connetti**.

KDE ora ha montato AEM come volume e puoi utilizzarlo come qualsiasi altro volume.
