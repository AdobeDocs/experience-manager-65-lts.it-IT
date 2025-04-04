---
title: Mappatura personalizzata dei gruppi di utenti in AEM 6.5
description: Scopri come funziona la mappatura dei gruppi di utenti personalizzati in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: e95f382b-ae89-46d5-b109-ea3257b6b046
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Mappatura personalizzata dei gruppi di utenti in AEM 6.5 {#custom-user-group-mapping-in-aem}

## Confronto del contenuto JCR relativo a CUG (gruppo utenti personalizzato) {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versioni precedenti di AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugEnabled</p> <p>Dichiarazione tipo di nodo: N/D, proprietà residua</p> </td>
   <td><p>Autorizzazione</p> <p>Nodo: rep:cugPolicy del tipo di nodo rep:CugPolicy</p> <p>Dichiarazione tipo di nodo: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticazione</p> <p>Tipo mixin: granite:AuthenticationRequired</p> </td>
   <td><p>Per limitare l’accesso in lettura, al nodo di destinazione viene applicato un criterio CUG dedicato.</p> <p>NOTA: i criteri possono essere applicati solo ai percorsi supportati configurati.</p> <p>I nodi con nome rep:cugPolicy e tipo rep:CugPolicy sono protetti e non possono essere scritti utilizzando chiamate API JCR regolari; utilizza invece la gestione del controllo di accesso JCR.</p> <p>Per ulteriori informazioni, consulta <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">questa pagina</a>.</p> <p>Per applicare il requisito di autenticazione a un nodo, è sufficiente aggiungere il tipo mixin granite:AuthenticationRequired.</p> <p>NOTA: rispettato solo sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugPrincipals</p> <p>Dichiarazione tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: rep:principalNames</p> <p>Dichiarazione tipo di nodo: rep:CugPolicy</p> </td>
   <td><p>La proprietà contenente i nomi delle entità autorizzate a leggere il contenuto sotto il CUG con restrizioni è protetta e non può essere scritta utilizzando normali chiamate API JCR; al suo posto, utilizza la gestione del controllo di accesso JCR.</p> <p>Consulta <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">questa pagina</a> per ulteriori dettagli sull'implementazione.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugLoginPage</p> <p>Dichiarazione tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: granite:loginPath (facoltativo)</p> <p>Dichiarazione tipo di nodo: granite:AuthenticationRequired</p> </td>
   <td><p>Un nodo JCR con il tipo mixin granite:AuthenticationRequired definito può facoltativamente definire un percorso di accesso alternativo.</p> <p>NOTA: rispettato solo sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugRealm</p> <p>Dichiarazione tipo di nodo: NA, proprietà residua</p> </td>
   <td>ND</td>
   <td>Non più supportato con la nuova implementazione.</td>
  </tr>
 </tbody>
</table>

## Confronto dei servizi OSGi {#comparison-of-osgi-services}

**Versioni precedenti di AEM**

Etichetta: Supporto per gruppi utenti chiusi (CUG) di Adobe Granite

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Etichetta: Configurazione CUG di Apache Jackrabbit Oak

  Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

  ConfigurationPolicy = OBBLIGATORIO

* Etichetta: elenco di esclusione CUG di Apache Jackrabbit Oak

  Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

  ConfigurationPolicy = OBBLIGATORIO

* Nome: com.adobe.granite.auth.requirements.impl.RequirementService
* Etichetta: Requisiti di autenticazione di Adobe Granite e gestore del percorso di accesso

  Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

  ConfigurationPolicy = OBBLIGATORIO

**Commenti**

* Configurazione dell’autorizzazione del gruppo utenti chiusi (CUG) e attivazione/disattivazione della valutazione.
Servizio per configurare l&#39;elenco di esclusione di entità che non dovrebbero essere interessate dall&#39;autorizzazione CUG.

  >[!NOTE]
  > 
  >Se `CugExcludeImpl` non è configurato, `CugConfiguration` torna al valore predefinito.

  È possibile collegare un’implementazione personalizzata di CugExclude in caso di esigenze particolari.

* Il componente OSGi implementa LoginPathProvider che espone un percorso di accesso corrispondente a LoginSelectorHandler. Include un riferimento obbligatorio a RequirementHandler utilizzato per registrare l&#39;osservatore che ascolta i requisiti di autenticazione modificati memorizzati nel contenuto tramite il tipo di mixin granite:AuthenticationRequired.
* Il componente OSGi che implementa RequirementHandler notifica a SlingAuthenticator le modifiche apportate ai authrequirements.

  Poiché il criterio di configurazione per questo componente è OBBLIGATORIO, viene attivato solo se è specificato un set di percorsi supportati.

  L’abilitazione del servizio avvia RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation if there are special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
