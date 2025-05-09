---
title: Esportatore JSON per Content Services
description: AEM Content Services è progettato per generalizzare la descrizione e la distribuzione dei contenuti in/da AEM, non limitandosi alle pagine web. Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati che possono essere utilizzati da qualsiasi cliente.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 8c66b978-872e-4f5e-8f64-1e2dfb7d7dde
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 24%

---

# Esportatore JSON per Content Services{#json-exporter-for-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* [Applicazioni a pagina singola](spa-walkthrough.md)
* Applicazioni mobile native
* Altri canali e punti di contatto esterni ad AEM

Con i frammenti di contenuto che utilizzano contenuti strutturati, puoi fornire servizi di contenuto utilizzando la funzione di esportazione JSON per distribuire il contenuto di qualsiasi pagina AEM in formato di modello dati JSON. Questo metodo può quindi essere utilizzato dalle tue applicazioni.

>[!NOTE]
>
>La funzionalità qui descritta è disponibile per tutti i Componenti core a partire dalla [versione 1.1.0 dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it).

## Esportatore JSON con componenti core per frammenti di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando la funzione di esportazione JSON di AEM, puoi distribuire il contenuto di qualsiasi pagina AEM in formato di modello dati JSON. Questo metodo può quindi essere utilizzato dalle tue applicazioni.

In AEM, la consegna viene eseguita utilizzando il selettore `model` e l&#39;estensione `.json`.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Fornisce contenuti quali:

   ![chlimage_1-192](assets/chlimage_1-192.png)

In alternativa, puoi distribuire il contenuto di un frammento di contenuto strutturato eseguendo il targeting specifico.

Utilizza l&#39;intero percorso del frammento (tramite `jcr:content`); ad esempio, con un suffisso come.

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. Puoi inoltre utilizzare meccanismi quali i componenti elenco per cercare automaticamente contenuti rilevanti.

* Ad esempio, un URL come:

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* Fornisce contenuti quali:

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >Puoi [adattare i tuoi componenti](/help/sites-developing/json-exporter-components.md) per accedere e utilizzare questi dati.

  >[!NOTE]
  >
  >Anche se non si tratta di un&#39;implementazione standard, sono supportati [più selettori,](json-exporter-components.md#multiple-selectors) ma `model` deve essere il primo.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP di Assets

   * [API HTTP di Assets](/help/assets/mac-api-assets.md)

* Modelli Sling:

   * [Modelli Sling - Associazione di una classe di modelli a un tipo di risorsa dalla versione 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Ottenimento delle informazioni di pagina in formato JSON](/help/sites-developing/pageinfo.md)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, cfr.:

* L&#39;argomento [Frammenti di contenuto nella guida utente di Assets](/help/assets/content-fragments/content-fragments.md)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Abilitazione dell’esportazione JSON per un componente](/help/sites-developing/json-exporter-components.md)

* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it)
