---
title: Creazione di temi di moduli adattivi personalizzati
description: Un tema per moduli adattivi è una libreria client di Adobe Experience Manager che puoi utilizzare per definire gli stili (aspetto) di un modulo adattivo. Scopri come creare temi di moduli adattivi personalizzati.
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
exl-id: e9853779-e22c-484e-8480-8e724d584ab7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# Creazione di temi di moduli adattivi personalizzati {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>Adobe Experience Manager (AEM) Forms fornisce la funzionalità [Editor temi](/help/forms/using/themes.md) per creare e modificare moduli adattivi [temi](/help/forms/using/themes.md). Eseguire i passaggi elencati in questo articolo solo se è stato eseguito l&#39;aggiornamento da una versione che non dispone di [Editor tema](/help/forms/using/themes.md) e si dispone di un investimento esistente in temi creati utilizzando file Less/CSS (metodo di editor pre-tema).

## Prerequisiti {#prerequisites}

* Conoscenza del framework LESS (Leaner CSS)
* Come creare una libreria client in Adobe Experience Manager
* [Creazione di un modello di modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md) per l&#39;utilizzo del tema creato

## Tema modulo adattivo {#adaptive-form-theme}

Un **tema modulo adattivo** è una libreria client di AEM che puoi utilizzare per definire gli stili (look and feel) di un modulo adattivo.

Si crea un **modello adattivo** e si applica il tema al modello. Puoi quindi utilizzare questo modello personalizzato per creare un **modulo adattivo**.

![Modulo adattivo e libreria client](assets/hierarchy.png)

## Per creare un tema per moduli adattivi {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>La procedura seguente viene descritta utilizzando nomi di esempio per oggetti AEM come nodi, proprietà e cartelle.
>
>Se si esegue la procedura seguente utilizzando i nomi, il modello risultante dovrebbe essere simile allo snapshot seguente:

![Snapshot modulo adattivo a tema foresta](assets/thumbnail.png)
**Figura:** *Esempio di tema foresta*

1. Creare un nodo di tipo `cq:ClientLibraryFolder` sotto il nodo `/apps`.

   Ad esempio, crea il seguente nodo:

   `/apps/myAfThemes/forestTheme`

1. Aggiungere una proprietà stringa multivalore `categories` al nodo e impostarne il valore in modo appropriato.

   Impostare ad esempio la proprietà su: `af.theme.forest`.

   ![Snapshot archivio CRX](assets/3-2.png)

1. Aggiungere due cartelle, `less` e `css`, e un file `css.txt` al nodo creato nel passaggio 1:

   * Cartella `less`: contiene i file delle variabili `less` in cui si definiscono le variabili `less` e `less mixins` utilizzate per gestire gli stili .css.

     Questa cartella è costituita da `less` file di variabili, `less` file mixin, `less` file che definiscono gli stili utilizzando mixin e variabili. Tutti questi file `less` vengono quindi importati in styles.less.

   * `css`cartella: contiene i file .css in cui si definiscono gli stili statici da utilizzare nel tema.

   **Meno file di variabili**: si tratta dei file in cui si definiscono o si sovrascrivono le variabili utilizzate per definire gli stili CSS.

   I moduli adattivi forniscono variabili pronte all’uso definite nei seguenti `.less` file:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   I moduli adattivi forniscono anche variabili di terze parti definite in:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   È possibile utilizzare le variabili `less` fornite con i moduli adattivi, ignorarle o creare nuove variabili `less`.

   >[!NOTE]
   >
   >Durante l&#39;importazione dei file del pre-processore meno, nell&#39;istruzione di importazione specificare il percorso relativo dei file.

   Esempio di variabili di sostituzione:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Per ignorare le `less` variabili:

   1. Importa variabili modulo adattive predefinite:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Quindi importa il file meno che include le variabili sovrascritte.

   Esempio di nuove definizioni di variabili:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Meno file mixin:** È possibile definire le funzioni che accettano le variabili come argomenti. L’output di queste funzioni è rappresentato dagli stili risultanti. Utilizza questi mixin in stili diversi, per evitare di ripetere gli stili CSS.

   I moduli adattivi forniscono mixin predefiniti definiti in:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   I moduli adattivi forniscono anche mixin di terze parti definiti in:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definizione mixin di esempio:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **File Styles.less:** Utilizzare questo file per includere tutti i file `less` (variabili, mixin, stili) che è necessario utilizzare nella libreria client.

   Nel seguente file `styles.less` di esempio, l&#39;istruzione di importazione può essere inserita in qualsiasi ordine.

   Le istruzioni per importare i seguenti file `.less` sono obbligatorie:

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   `css.txt` contiene i percorsi dei file .css da scaricare per la libreria.

   Ad esempio:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >Il file styles.less non è obbligatorio. Ciò significa che non è necessario creare questo file, se non sono stati definiti stili, variabili o mixin personalizzati.
   >
   >Tuttavia, se non si crea un file style.less, nel file css.txt è necessario rimuovere il commento dalla riga seguente:
   >
   >**`#base=less`**
   >
   >E commenta la seguente riga:
   >
   >**`styles.less`**

## Per utilizzare un tema in un modulo adattivo {#to-use-a-theme-in-an-adaptive-form}

Dopo aver creato un tema per moduli adattivi, effettua le seguenti operazioni per utilizzarlo in un modulo adattivo:

1. Per includere il tema creato in [per creare una sezione del tema del modulo adattivo](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p), crea una pagina personalizzata di tipo `cq:Component`.

   Ad esempio `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Aggiungere una proprietà `sling:resourceSuperType` e impostarne il valore come `fd/af/components/page/base`.

      ![Snapshot archivio CRX](assets/1-2.png)

   1. Per utilizzare un tema nella pagina, devi aggiungere al nodo un file library.jsp che esegue l’override.

      Puoi quindi importare il tema creato in Per creare una sezione del tema per moduli adattivi in questo articolo.

      Il seguente frammento di codice di esempio importa il tema `af.theme.forest`.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Facoltativo**: nella pagina personalizzata, eseguire l&#39;override di header.jsp, footer.jsp e body.jsp, come richiesto.

1. Creare un modello personalizzato (ad esempio: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) il cui jcr:content punta alla pagina personalizzata creata nel passaggio precedente (ad esempio: `myAfCustomizations/myAfPages/forestPage)`.

   ![Snapshot archivio CRX](assets/2-1.png)

1. Crea un modulo adattivo utilizzando il modello creato nel passaggio precedente. L’aspetto del modulo adattivo è definito dal tema creato nella sezione Per creare un tema per modulo adattivo di questo articolo.
