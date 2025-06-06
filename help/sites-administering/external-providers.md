---
title: Analytics con provider esterni
description: Scopri come configurare una tua istanza di snippet generici di Analytics per definire una nuova configurazione di servizio.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 73f40fd7-69b9-436c-b6b4-a7d6bfbaae6f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Analytics con provider esterni {#analytics-with-external-providers}

Analytics può fornirti informazioni importanti e interessanti su come viene utilizzato il tuo sito web.

Sono disponibili diverse configurazioni pronte all’uso per l’integrazione con il servizio appropriato, ad esempio:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Puoi anche configurare la tua istanza dei **snippet generici di Analytics** per definire una nuova configurazione del servizio.

Le informazioni vengono quindi raccolte da piccoli snippet di codice che vengono aggiunti alle pagine web. Ad esempio:

>[!CAUTION]
>
>Non racchiudere gli script nei tag `script`.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Tali snippet consentono la raccolta dei dati e la generazione dei rapporti. I dati effettivi raccolti dipendono dal provider e dal frammento di codice effettivo utilizzato. Le statistiche di esempio includono:

* quanti visitatori nel tempo
* quante pagine visitate
* termini di ricerca utilizzati
* pagine di destinazione

>[!CAUTION]
>
>Il sito demo Geometrixx-Outdoors è configurato in modo che gli attributi forniti nelle Proprietà pagina vengano aggiunti al codice sorgente html (appena sopra il tag di fine `</html>`) nello script `js` corrispondente.
>
>Se `/apps` non eredita dal componente pagina predefinito ( `/libs/foundation/components/page`), è necessario (o gli sviluppatori) assicurarsi che gli script `js` corrispondenti siano inclusi, ad esempio, includendo `cq/cloudserviceconfigs/components/servicescomponents` o utilizzando un meccanismo simile.
>
>In caso contrario, nessuno dei servizi (Generico, Analytics, Target e così via) funzionerà.

## Creazione di un servizio con uno snippet generico {#creating-a-new-service-with-a-generic-snippet}

Per la configurazione di base:

1. Apri la console **Strumenti**.
1. Dal riquadro di sinistra, espandere **Configurazioni servizi cloud**.
1. Fai doppio clic su **Frammento generico di Analytics** per aprire la pagina:

   ![Snippet generico di analisi](assets/analytics_genericoverview.png)

1. Fate clic su + per aggiungere una nuova configurazione utilizzando la finestra di dialogo. Come minimo, assegna un nome, ad esempio Google Analytics:

   ![Crea configurazione](assets/analytics_addconfig.png)

1. Fai clic su **Crea**. Viene visualizzata immediatamente la finestra di dialogo dello snippet. Incolla lo snippet di JavaScript appropriato nel campo:

   ![Modifica del componente](assets/analytics_snippet.png)

1. Fare clic su **OK** per salvare.

## Utilizzo del nuovo servizio nelle pagine {#using-your-new-service-on-pages}

Dopo aver creato la configurazione del servizio, è necessario configurare le pagine richieste per utilizzarla:

1. Passa alla pagina.
1. Apri **Proprietà pagina** dalla barra laterale, quindi la scheda **Servizi cloud**.
1. Fai clic su **Aggiungi servizio**, quindi seleziona il servizio richiesto. Ad esempio, il **frammento generico di Analytics**:

   ![Aggiunta di un servizio cloud](assets/analytics_selectservice.png)

1. Fare clic su **OK** per salvare.
1. Sei tornato alla scheda **Servizi cloud**. Lo snippet **Generic Analytics** è ora elencato con il messaggio `Configuration reference missing`. Utilizza l’elenco a discesa per selezionare la tua istanza di servizio specifica. Ad esempio, google-analytics:

   ![Aggiunta della configurazione del servizio cloud](assets/analytics_selectspecificservice.png)

1. Fare clic su **OK** per salvare.

   Ora è possibile visualizzare lo snippet se si visualizza la pagina Source per la pagina.

   Trascorso un certo periodo di tempo, puoi visualizzare le statistiche raccolte.

   >[!NOTE]
   >
   >Se la configurazione è associata a una pagina che ha pagine figlie, il servizio viene ereditato anche da queste.
