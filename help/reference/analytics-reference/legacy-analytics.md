---
description: En översikt över hur Experience Cloud Identity Service fungerar med det äldre analys-ID:t.
keywords: ID Service
seo-description: En översikt över hur Experience Cloud Identity Service fungerar med det äldre analys-ID:t.
seo-title: Analyser och Experience Cloud ID-förfrågningar
title: Analyser och Experience Cloud ID-förfrågningar
uuid: 28beed16-7ef9-4824-8e82-853930756eca
translation-type: tm+mt
source-git-commit: e6d65f1bfed187d7440512e8f3c2de0550506c95

---


# Analyser och Experience Cloud ID-förfrågningar{#analytics-and-experience-cloud-id-requests}

En översikt över hur Experience Cloud Identity Service fungerar med det äldre analys-ID:t.

## Sammanfattning {#section-64d8523ff7634cb987d0c6480f587dd3}

Historiskt sett har Experience Cloud Identity Service integrerats nära i Adobe Analytics. Det är fortfarande en viktig del av Analytics men har nu viktiga funktioner för andra lösningar och funktioner i [!DNL Experience Cloud]. På grund av detta historiska arv fungerar kontroll eller skrivning av ett analys-ID lite annorlunda än med den allmänna processen som beskrivs i [How the Experience Cloud Identity Service Requests and Sets IDs...](../../introduction/id-request.md#concept-2caacebb1d244402816760e9b8bcef6a). Mer information om ordningen för åtgärder för att kontrollera ID:n finns i [Ställa in analys- och Experience Cloud-ID:n](../../reference/analytics-reference/analytics-ids.md#concept-f381dd18ee184c6c8e48286937a161d6).

## AMCV Cookie är inte inställd i webbläsaren {#section-cccf10cd775e4a95a7e98d3c3c0ff9a9}

Om [!DNL Experience Cloud]-cookien (AMCV) inte finns genererar ett ID-tjänstanrop till [!DNL Adobe] ett svar som varierar beroende på om det finns ett äldre Analytics-ID eller inte. Det gamla [!DNL Analytics]-ID:t lagras i [s_vi-cookien](https://marketing.adobe.com/resources/help/en_US/whitepapers/cookies/?f=cookies_analytics.html). I tabellen nedan beskrivs hur ID:n skrivs till AMCV-cookien baserat på läget för s_vi-cookien.

<table id="table_DC85FECE26DD424E841BA1059AF1E57F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> s_vi Cookie-status </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b> s_vi Cookie har inte angetts</b> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten tilldelar besökare ett <span class="keyword"> Experience Cloud</span> ID (MID). MID:t identifierar era besökare till <span class="keyword"> Analytics</span> och andra <span class="keyword"> Experience Cloud</span> -lösningar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>s_vi Cookie är inställt</b> </p> </td> 
   <td colname="col2"> <p>När en besökare med en s_vi-cookie först stöter på Experience Cloud Identity Service, den här tjänsten: </p> 
    <ul id="ul_BE584810280D4874AF802A9247011787"> 
     <li id="li_AA395B09A3174AF78F3EC10053E2E4F5">Skriver det <span class="keyword"> analys</span> -ID som lagras i s_vi-cookien till AMCV-cookien. Detta skrivs som <span class="keyword"> analys</span> -ID (AID). Den här åtgärden <i>påverkar inte</i> antalet besökare. <span class="keyword"> Analyserna</span> fortsätter att identifiera användare med deras gamla ID:n. </li> 
     <li id="li_8735DE21FEA542BA8024109B8FE1E2ED">Skriver MID till AMCV-cookien. MID identifierar användare över olika lösningar. </li> 
    </ul> <p> <p>Obs! Med en <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local"> respitperiod</a>innehåller datacentrets svar alltid ett äldre ID som lagras i s_vi-cookien. Under respitperioden skrivs det gamla ID:t till AMCV-cookien som AID-värde. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Användare som identifieras av s_fid-cookien kommer inte att ha sina gamla FID-värden migrerade till AMCV-cookien. Med s_fid-cookie migreras användare som om ingen s_vi-cookie fanns (se ovan) och visas som nya besökare på din webbplats. Mer information finns i [Analytics Cookies](https://marketing.adobe.com/resources/help/en_US/whitepapers/cookies/?f=cookies_analytics.html) .

## AMCV Cookie är inställd i webbläsaren {#section-01c088fc565c4b24ba1722c7cc240310}

Om det finns en AMCV-cookie använder Analytics MID som [!DNL Analytics] identifierare om det inte finns något äldre [!DNL Analytics] ID-värde i cookien.
