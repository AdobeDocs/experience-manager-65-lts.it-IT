---
title: API per richiamare il servizio modello dati modulo da moduli adattivi
description: Spiega l’API invokeWebServices che è possibile utilizzare per richiamare i servizi web scritti in WSDL dall’interno di un campo modulo adattivo.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: e36be2da-af72-485f-87a6-cef6172037c6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# API per richiamare il servizio modello dati modulo da moduli adattivi {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

AEM Forms consente agli autori dei moduli di semplificare e migliorare ulteriormente l’esperienza di compilazione dei moduli richiamando i servizi configurati in un modello di dati del modulo dall’interno di un campo di modulo adattivo. Per richiamare un servizio del modello dati, è possibile creare una regola nell&#39;editor visivo o specificare un JavaScript utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` nell&#39;editor di codice dell&#39;[editor di regole](/help/forms/using/rule-editor.md).

Questo documento si concentra sulla scrittura di un JavaScript utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare un servizio.

## Utilizzo dell’API {#using-the-api}

L&#39;API `guidelib.dataIntegrationUtils.executeOperation` richiama un servizio dall&#39;interno di un campo modulo adattivo. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La struttura dell&#39;API `guidelib.dataIntegrationUtils.executeOperation` specifica i dettagli sull&#39;operazione del servizio. La sintassi della struttura è la seguente.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La struttura API specifica i dettagli seguenti sull’operazione del servizio.

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Struttura per specificare l'identificatore del modello dati del modulo, il titolo dell'operazione e il nome dell'operazione</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Specifica il percorso del repository del modello dati del modulo, incluso il nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Specifica il nome dell'operazione di servizio da eseguire</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Esegue il mapping di uno o più oggetti modulo agli argomenti di input per l'operazione di servizio</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Esegue il mapping di uno o più oggetti modulo ai valori di output dell'operazione del servizio per compilare i campi modulo<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Restituisce valori in base agli argomenti di input per l'operazione di servizio. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visualizza un messaggio di errore se la funzione di callback di successo non visualizza i valori di output in base agli argomenti di input. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
 </tbody>
</table>

## Script di esempio per richiamare un servizio {#sample-script-to-invoke-a-service}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `getAccountById` configurata nel modello dati del modulo `employeeAccount`.

L&#39;operazione `getAccountById` utilizza il valore nel campo modulo `employeeID` come input per l&#39;argomento `empId` e restituisce il nome del dipendente, il numero di conto e il saldo del conto per il dipendente corrispondente. I valori di output vengono compilati nei campi modulo specificati. Ad esempio, il valore nell&#39;argomento `name` viene popolato nell&#39;elemento modulo `fullName` e il valore per l&#39;argomento `accountNumber` nell&#39;elemento modulo `account`.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Utilizzo dell’API con la funzione di callback {#using-the-api-callback}

È inoltre possibile richiamare il servizio del modello dati modulo utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` con una funzione di callback. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La funzione di richiamata può avere `success` e `failure` funzioni di richiamata.

### Script di esempio con funzioni di callback riuscite e non riuscite {#callback-function-success-failure}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `GETOrder` configurata nel modello dati del modulo `employeeOrder`.

L&#39;operazione `GETOrder` accetta il valore nel campo modulo `Order ID` come input per l&#39;argomento `orderId` e restituisce il valore della quantità dell&#39;ordine nella funzione di callback `success`.  Se la funzione di callback `success` non restituisce la quantità dell&#39;ordine, la funzione di callback `failure` visualizza il messaggio `Error occured`.

>[!NOTE]
>
>Se si utilizza la funzione di callback `success`, i valori di output non vengono inseriti nei campi modulo specificati.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
