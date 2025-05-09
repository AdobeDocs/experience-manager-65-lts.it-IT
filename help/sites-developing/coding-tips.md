---
title: Suggerimenti per la codifica
description: Scopri alcuni suggerimenti sulle best practice per la codifica in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: e431a240-45a2-4222-b854-32b90e5cd100
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Suggerimenti per la codifica{#coding-tips}

## Utilizza il più possibile taglib o HTL {#use-taglibs-or-htl-as-much-as-possible}

L’inclusione di scriptlet nei JSP rende difficile il debug dei problemi nel codice. Inoltre, includendo gli scriptlet nei JSP, è difficile separare la logica di business dal livello di visualizzazione, il che rappresenta una violazione del principio di responsabilità singola e del modello di progettazione MVC.

### Scrivi codice leggibile {#write-readable-code}

Il codice viene scritto una volta, ma letto molte volte. Dedicare un po&#39; di tempo prima per pulire il codice scritto dà i suoi frutti mentre tu e altri sviluppatori lo leggete in seguito.

### Scegli nomi che rivelano le intenzioni {#choose-intention-revealing-names}

Idealmente, un altro programmatore non dovrebbe aprire un modulo per capire cosa fa. Allo stesso modo, dovrebbero essere in grado di dire cosa fa un metodo senza leggerlo. Più si possono sottoscrivere a queste idee, più facile è leggere il codice e più veloce è la scrittura e la modifica del codice.

Nella base di codice di AEM vengono utilizzate le seguenti convenzioni:


* Una singola implementazione di un&#39;interfaccia è denominata `<Interface>Impl`, ovvero `ReaderImpl`.
* Le implementazioni multiple di un&#39;interfaccia sono denominate `<Variant><Interface>`, ovvero `JcrReader` e `FileSystemReader`.
* Le classi base astratte sono denominate `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* I pacchetti sono denominati `com.adobe.product.module`. Ogni artefatto Maven o bundle OSGi deve avere un proprio pacchetto.
* Le implementazioni Java™ vengono inserite in un pacchetto impl sotto la relativa API.


Queste convenzioni non si applicano necessariamente alle implementazioni dei clienti, ma è importante che vengano definite e rispettate in modo che il codice possa rimanere gestibile.

Idealmente, i nomi dovrebbero rivelare la loro intenzione. Un test di codice comune per i casi in cui i nomi non sono chiari come dovrebbero essere è la presenza di commenti che spiegano a cosa serve la variabile o il metodo:

<table>
 <tbody>
  <tr>
   <td><p><strong>Non chiaro</strong></p> </td>
   <td><p><strong>Cancella</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tempo trascorso in giorni</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>list pubblica getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Non ripeta  {#don-t-repeat-yourself}

DRY afferma che lo stesso set di codice non deve mai essere duplicato. Questo vale anche per elementi come i valori letterali stringa. La duplicazione dei codici consente di individuare eventuali difetti in qualsiasi momento, che devono essere individuati ed eliminati.

### Evita le regole CSS nude {#avoid-naked-css-rules}

Le regole CSS devono essere specifiche per l’elemento di destinazione nel contesto dell’applicazione. Ad esempio, una regola CSS applicata a *.content .center* sarebbe troppo ampia e potrebbe potenzialmente avere un impatto su molti contenuti nel sistema, richiedendo ad altri di ignorare questo stile in futuro. *.myapp-centertext* sarebbe invece una regola più specifica in quanto specifica *testo* centrato nel contesto dell&#39;applicazione.

### Eliminare l’utilizzo delle API obsolete {#eliminate-usage-of-deprecated-apis}

Quando un’API è obsoleta, è sempre meglio trovare il nuovo approccio consigliato invece di affidarsi all’API obsoleta. Questo garantirà aggiornamenti più fluidi in futuro.

### Scrivi codice localizzabile {#write-localizable-code}

Eventuali stringhe non fornite da un autore devono essere racchiuse in una chiamata al dizionario i18n di AEM tramite *I18n.get()* in JSP/Java e *CQ.I18n.get()* in JavaScript. Questa implementazione restituirà la stringa che gli è stata passata se non viene trovata alcuna implementazione, quindi offre la flessibilità di implementare la localizzazione dopo aver implementato le funzioni nella lingua primaria.

### Esci dai percorsi delle risorse per la sicurezza {#escape-resource-paths-for-safety}

Anche se i percorsi nel JCR non devono contenere spazi, la loro presenza non deve causare l’interruzione del codice. Jackrabbit fornisce una classe utilità Text con metodi *escape()* e *escapePath()*. Per i JSP, l&#39;interfaccia utente Granite espone una funzione *granite:encodeURIPath() EL*.

### Utilizza l’API XSS e/o HTL per proteggere da attacchi di scripting tra siti {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM fornisce un’API XSS per pulire facilmente i parametri e garantire la sicurezza da attacchi di scripting tra siti diversi. Inoltre, HTL dispone di queste protezioni integrate direttamente nel linguaggio dei modelli. Una scheda di riferimento API è disponibile per il download da [Sviluppo - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementare la registrazione appropriata {#implement-appropriate-logging}

Per il codice Java™, AEM supporta slf4j come API standard per la registrazione dei messaggi e deve essere utilizzato con le configurazioni rese disponibili tramite la console OSGi per motivi di coerenza dell’amministrazione. Slf4j espone cinque diversi livelli di registrazione. Adobe consiglia di utilizzare le seguenti linee guida nella scelta del livello in cui registrare un messaggio:

* ERRORE: quando si è verificato un errore nel codice e l’elaborazione non può continuare. Ciò si verifica spesso a seguito di un’eccezione imprevista. In questi scenari è utile includere le tracce dello stack.
* AVVERTENZA: se qualcosa non funziona correttamente, l’elaborazione può continuare. Questo sarà spesso il risultato di un&#39;eccezione prevista, ad esempio *PathNotFoundException*.
* INFORMAZIONI: informazioni utili per il monitoraggio di un sistema. Tieni presente che questa è l’impostazione predefinita e che la maggior parte dei clienti la lascerà nei propri ambienti. Pertanto, non utilizzarlo in modo eccessivo.
* DEBUG: informazioni di livello inferiore sull’elaborazione. Utile quando si esegue il debug di un problema con il supporto.
* TRACE: informazioni di livello più basso, ad esempio l’immissione o l’uscita dai metodi. Di solito questo viene utilizzato solo dagli sviluppatori.

Se è presente JavaScript, *console.log* deve essere utilizzato solo durante lo sviluppo e tutte le istruzioni di registro devono essere rimosse prima del rilascio.

### Evita la programmazione delle sette cargo {#avoid-cargo-cult-programming}

Evita di copiare il codice senza capire cosa fa. In caso di dubbi, è sempre meglio chiedere a qualcuno che ha più esperienza con il modulo o l’API su cui non hai chiarezza.
