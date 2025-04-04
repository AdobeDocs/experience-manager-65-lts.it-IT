---
title: 'Sviluppo AEM: linee guida e best practice'
description: Linee guida e best practice per lo sviluppo su AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7fd478a6-ddc6-4c7f-b09b-e4de6ec0e897
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Sviluppo AEM: linee guida e best practice{#aem-development-guidelines-and-best-practices}

## Linee guida per l’utilizzo di modelli e componenti {#guidelines-for-using-templates-and-components}

I componenti e i modelli di Adobe Experience Manager (AEM) comprendono un potente toolkit. Possono essere utilizzati dagli sviluppatori per fornire agli utenti aziendali dei siti web, agli editor e agli amministratori la funzionalità di adattare i loro siti web alle mutevoli esigenze aziendali (agilità dei contenuti). Tutto questo mantenendo l&#39;uniformità del layout dei siti (protezione del marchio).

Una sfida tipica per una persona responsabile di un sito Web o di un insieme di siti Web (ad esempio, in una filiale di un&#39;azienda globale) consiste nell&#39;introdurre un nuovo tipo di presentazione dei contenuti sui propri siti Web.

Supponiamo che sia necessario aggiungere ai siti web una pagina di elenco delle novità, in cui sono elencati estratti da altri articoli già pubblicati. La pagina deve avere la stessa progettazione e struttura del resto del sito web.

Il modo consigliato per affrontare tale sfida consiste nel:

* Riutilizzare un modello esistente per creare un tipo di pagina. Il modello definisce approssimativamente la struttura della pagina (elementi di navigazione, pannelli e così via), che viene ulteriormente perfezionata dal relativo design (CSS, grafica).
* Utilizza il sistema paragrafo (parsys/iparsys) nelle nuove pagine.
* Definire il diritto di accesso alla modalità Progettazione dei sistemi paragrafo, in modo che solo le persone autorizzate (in genere l’amministratore) possano modificarli.
* Definisci i componenti consentiti nel sistema paragrafo specificato in modo che gli editor possano quindi inserire i componenti richiesti nella pagina. In questo caso, potrebbe essere un componente elenco, che può attraversare una sottostruttura di pagine ed estrarre le informazioni in base a regole predefinite.
* Gli editor aggiungono e configurano i componenti consentiti sulle pagine di cui sono responsabili, per fornire all’azienda le funzionalità (informazioni) richieste.

Questo illustra come questo approccio consenta agli utenti e agli amministratori del sito web che vi contribuiscono di rispondere rapidamente alle esigenze aziendali senza richiedere il coinvolgimento di team di sviluppo. I metodi alternativi, come la creazione di un modello, sono in genere costosi e richiedono un processo di gestione delle modifiche e il coinvolgimento del team di sviluppo. Ciò rende l&#39;intero processo più lungo e costoso.

Gli sviluppatori di sistemi basati su AEM devono quindi utilizzare:

* modelli e controllo di accesso alla progettazione del sistema paragrafo per uniformità e protezione del brand
* sistema paragrafo, incluse le opzioni di configurazione per la flessibilità.

Le seguenti regole generali per gli sviluppatori hanno senso nella maggior parte dei progetti comuni:

* Mantieni basso il numero di modelli, anche se si tratta solo del numero di strutture di pagina fondamentalmente diverse sui siti web.
* Fornisci la flessibilità e le funzionalità di configurazione necessarie ai componenti personalizzati.
* Sfrutta al massimo la potenza e la flessibilità del sistema di paragrafi AEM: i componenti parsys e iparsys.

### Personalizzazione di componenti e altri elementi {#customizing-components-and-other-elements}

Quando crei componenti personalizzati o personalizzi un componente esistente, spesso è più semplice (e sicuro) riutilizzare le definizioni esistenti. Gli stessi principi si applicano anche ad altri elementi all’interno di AEM, ad esempio il gestore degli errori.

Questo può essere fatto copiando e sovrapponendo la definizione esistente. In altre parole, copia della definizione da `/libs` a `/apps/<your-project>`. Questa nuova definizione, in `/apps`, può essere aggiornata in base alle tue esigenze.

>[!NOTE]
>
>Per ulteriori dettagli, vedi [Utilizzo delle sovrapposizioni](/help/sites-developing/overlays.md).

Ad esempio:

* [Personalizzazione di un componente](/help/sites-developing/components.md)

  Ciò comportava la sovrapposizione di una definizione di componente:

   * Creare una cartella di componenti in `/apps/<website-name>/components/<MyComponent>` copiando un componente esistente:

      * Ad esempio, per personalizzare la copia del componente Testo:

         * da `/libs/foundation/components/text`
         * a `/apps/myProject/components/text`

* [Personalizzazione delle pagine visualizzate dal gestore degli errori](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Questo caso prevede la sovrapposizione di un servlet:

   * Nell’archivio, copia uno o più script predefiniti:

      * da `/libs/sling/servlet/errorhandler/`
      * a `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**Non** modificare nulla nel percorso `/libs`.
>
>Il motivo è che il contenuto di `/libs` viene sovrascritto al prossimo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Per la configurazione e altre modifiche:
>
>1. copia l&#39;elemento in `/libs` in `/apps`
>1. apportare modifiche entro `/apps`

## Quando utilizzare le query JCR e quando non utilizzarle {#when-to-use-jcr-queries-and-when-not-to-use-them}

Le query JCR sono uno strumento potente se utilizzato correttamente. Essi sono appropriati per:

* query reali degli utenti finali, ad esempio ricerche full-text sul contenuto.
* occasioni in cui i contenuti strutturati devono essere trovati nell’intero archivio.

  In questi casi, assicurati che le query vengano eseguite solo quando necessario. Ad esempio, all’attivazione di un componente o all’annullamento della validità della cache (anziché, ad esempio, Passaggi dei flussi di lavoro, Gestori di eventi che si attivano in caso di modifiche del contenuto e Filtri).

Non utilizzare mai query JCR per richieste di rendering puro. Ad esempio, le query JCR non sono appropriate per i seguenti elementi:

* navigazione rendering
* creazione di una panoramica sulle &quot;prime 10 ultime notizie&quot;
* visualizzazione dei conteggi degli elementi di contenuto

Per il rendering del contenuto, utilizza l’accesso di navigazione alla struttura del contenuto anziché eseguire una query JCR.

>[!NOTE]
>
>Se si utilizza il [Generatore di query](/help/sites-developing/querybuilder-api.md), si utilizzano le query JCR, poiché il Generatore di query genera query JCR dal punto di vista tecnico.
>

## Considerazioni sulla sicurezza {#security-considerations}

>[!NOTE]
>
>È inoltre utile fare riferimento all&#39;[elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md).

### Sessioni JCR (archivio) {#jcr-repository-sessions}

Utilizza la sessione utente, non la sessione amministrativa. Ciò significa che deve utilizzare:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protezione da vulnerabilità cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Il cross-site scripting (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. Prevenire l’XSS è data la massima priorità sia durante lo sviluppo che durante il test.

Inoltre, un firewall dell&#39;applicazione Web, ad esempio [mod_security per Apache](https://modsecurity.org), può fornire un controllo centrale e affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere da attacchi di cross-site scripting non rilevati in precedenza.

>[!CAUTION]
>
>Il codice di esempio fornito con AEM potrebbe non proteggere da tali attacchi e in genere si basa sul filtraggio delle richieste da parte di un firewall dell’applicazione web.

La scheda di riferimento rapido API XSS contiene informazioni necessarie per utilizzare l’API XSS e rendere più sicura un’app AEM. Puoi scaricarlo qui:

Scheda di riferimento rapido XSSAPI.

[Ottieni file](assets/xss_cheat_sheet_2016.pdf)

### Come proteggere la comunicazione per informazioni confidenziali {#securing-communication-for-confidential-information}

Come per qualsiasi applicazione su Internet, accertati che quando trasporti informazioni riservate

* il traffico è protetto tramite SSL
* Se applicabile, viene utilizzato HTTP POST

Questo vale per le informazioni riservate al sistema (come la configurazione o l&#39;accesso amministrativo) e per le informazioni riservate ai suoi utenti (come i dati personali)

## Attività di sviluppo distinte {#distinct-development-tasks}

### Personalizzazione delle pagine di errore {#customizing-error-pages}

Le pagine di errore possono essere personalizzate per AEM. È consigliabile evitare che l’istanza riveli tracce sling in caso di errori interni del server.

Per informazioni dettagliate, vedere [Personalizzazione delle pagine di errore visualizzate dal gestore degli errori](/help/sites-developing/customizing-errorhandler-pages.md).

### Apri file nel processo Java™ {#open-files-in-the-java-process}

Poiché AEM può accedere a molti file, si consiglia di configurare in modo esplicito per AEM il numero di [file aperti per un processo Java™](/help/sites-deploying/configuring.md#open-files-in-the-java-process).

Per ridurre al minimo questo problema, lo sviluppo deve garantire che qualsiasi file aperto venga chiuso correttamente quando (significativamente) possibile.
