---
title: Scelta di un tipo di persistenza per un’installazione di AEM Forms
description: Scegli con saggezza un tipo di persistenza. Consente di creare un ambiente AEM Forms efficiente e scalabile.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 8ddfc767-08a5-4045-86a7-97150e028a14
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Scelta di un tipo di persistenza per un’installazione di AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Scegli con saggezza un tipo di persistenza. Consente di creare un ambiente AEM Forms efficiente e scalabile.

La persistenza è il metodo per archiviare il contenuto negli archivi fisici. Definisce la struttura effettiva dei dati e il relativo meccanismo di archiviazione. I microKernel fungono da gestori di persistenza in AEM Forms. AEM Forms supporta la persistenza (MicroKernals) di tipo TarMK, MongoMK e RDBMK. Puoi scegliere un tipo di persistenza per AEM Forms a seconda dello scopo e del tipo di distribuzione (server singolo, farm o cluster) di un’istanza AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utilizza la persistenza TarPM per archiviare il contenuto.

La tabella seguente elenca tutti i tipi di persistenza supportati e i vari parametri che consentono di scegliere un tipo di persistenza per l’ambiente:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo di installazione / Costo</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configurazione autonoma</strong></th>
   <td>Supportato<br /> </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Cluster Setup</strong></th>
   <td>Non supportato</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Costo licenza</strong></th>
   <td>Incluso in AEM </td>
   <td>È richiesta una licenza separata</td>
   <td>È richiesta una licenza separata</td>
  </tr>
 </tbody>
</table>

TarMK è progettato per garantire prestazioni elevate, mentre MongoMK e RDBMK sono progettati per offrire scalabilità. Adobe consiglia vivamente TarMK come tecnologia di persistenza predefinita per tutti gli scenari di distribuzione di AEM Forms, sia per le istanze Author che Publish, ad eccezione dei casi d&#39;uso descritti nella sezione [Scelta di Mongo o di un microkernel di database relazionale su TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Per l&#39;elenco dei microkernel supportati, vedere [AEM Forms sui requisiti tecnici OSGi](/help/sites-deploying/technical-requirements.md) <!--or [AEM Forms on JEE supported platform combinations](/help/forms/using/aem-forms-jee-supported-platforms.md) articles-->.

## Scelta di Mongo o di un microkernel di database relazionale su TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un ambiente AEM Forms scalabile (cluster) è un set di due o più istanze di authoring attive configurate orizzontalmente. Se un singolo server, che supporta tutte le attività di authoring simultanee, non è più sostenibile, è possibile scegliere di eseguire più istanze di authoring.

<!--Only MongoMK and RDBMK persistence type are supported for a scalable (clustered) AEM Forms on JEE environment.-->

Il numero di server o le dimensioni dell&#39;ambiente scalabile variano a seconda dell&#39;installazione. Per un elenco di considerazioni ed esempi, vedere l&#39;articolo [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md) e/o [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). È inoltre possibile contattare il supporto AEM Forms per informazioni dettagliate sulla pianificazione della capacità per AEM Forms con RDBMK e TarMK.
