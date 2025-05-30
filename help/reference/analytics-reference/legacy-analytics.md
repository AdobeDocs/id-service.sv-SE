---
description: En översikt över hur identitetstjänsten Experience Cloud fungerar med det gamla Analytics-ID:t.
keywords: ID-tjänst
title: Begäranden om analyser och Experience Cloud ID
exl-id: 8c682159-e23a-4641-9ffd-e0028dc2f305
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 14%

---

# Begäranden om analyser och Experience Cloud ID{#analytics-and-experience-cloud-id-requests}

En översikt över hur identitetstjänsten Experience Cloud fungerar med det gamla Analytics-ID:t.

## Sammanfattning {#section-64d8523ff7634cb987d0c6480f587dd3}

Historiskt sett har Experience Cloud Identity Service integrerats nära i Adobe Analytics. Den är fortfarande en viktig del av Analytics men utför nu viktiga funktioner för andra lösningar och funktioner i [!DNL Experience Cloud]. På grund av detta historiska arv fungerar kontroll eller skrivning av ett analys-ID lite annorlunda än med den allmänna processen som beskrivs i [How the Experience Cloud Identity Service Requests and Sets IDs..](../../introduction/id-request.md#concept-2caacebb1d244402816760e9b8bcef6a). Mer information om ordningen för åtgärder för att kontrollera ID:n finns i [Ställa in analyser och Experience Cloud ID:n](../../reference/analytics-reference/analytics-ids.md#concept-f381dd18ee184c6c8e48286937a161d6).

## AMCV Cookie är inte inställd i webbläsaren {#section-cccf10cd775e4a95a7e98d3c3c0ff9a9}

Om [!DNL Experience Cloud]-cookien (AMCV) inte finns genererar ett ID-tjänstanrop till [!DNL Adobe] ett svar som varierar beroende på om det finns ett äldre Analytics-ID eller inte. Det gamla [!DNL Analytics]-ID:t lagras i [s_vi-cookien](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-analytics.html?lang=sv-SE). I tabellen nedan beskrivs hur ID:n skrivs till AMCV-cookien baserat på läget för s_vi-cookien.

<table id="table_DC85FECE26DD424E841BA1059AF1E57F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> s_vi Cookie-status </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b> s_vi-cookie har inte angetts</b> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten tilldelar besökare ett <span class="keyword"> Experience Cloud </span>-ID (MID). MID identifierar dina besökare till <span class="keyword"> Analytics </span> och andra <span class="keyword"> Experience Cloud </span>-lösningar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>s_vi Cookie är inställd</b> </p> </td> 
   <td colname="col2"> <p>När en webbplatsbesökare med en s_vi-cookie träffar på Experience Cloud Identity Service första gången: </p> 
    <ul id="ul_BE584810280D4874AF802A9247011787"> 
     <li id="li_AA395B09A3174AF78F3EC10053E2E4F5">Skriver det <span class="keyword"> Analytics</span>-ID som lagras i s_vi-cookien till AMCV-cookien. Detta skrivs som <span class="keyword"> Analytics</span>-ID (AID). Den här åtgärden <i>påverkar inte </i> antalet besökare. <span class="keyword"> Analytics</span> fortsätter att identifiera användare med deras gamla ID:n. </li> 
     <li id="li_8735DE21FEA542BA8024109B8FE1E2ED">Skriver MID till AMCV-cookien. MID identifierar användare över olika lösningar. </li> 
    </ul> <p> <p>Obs! Med en <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local">-respitperiod </a> innehåller datacentrets svar alltid ett äldre ID som lagras i s_vi-cookien. Under respitperioden skrivs det gamla ID:t till AMCV-cookien som AID-värde. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Användare som identifieras av s_fid-cookien kommer inte att ha sina gamla FID-värden migrerade till AMCV-cookien. Med s_fid-cookie migreras användare som om ingen s_vi-cookie fanns (se ovan) och visas som nya besökare på din webbplats. Mer information finns i [Analytics Cookies](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-analytics.html?lang=sv-SE).

## AMCV Cookie är inställd i webbläsaren {#section-01c088fc565c4b24ba1722c7cc240310}

Om det finns en AMCV-cookie kommer Analytics att använda MID som identifierare för [!DNL Analytics] om det inte finns något äldre [!DNL Analytics] ID-värde i cookien.
