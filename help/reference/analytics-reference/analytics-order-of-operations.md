---
description: När du har distribuerat besökar-ID-tjänsten kan en besökare identifieras på fem olika sätt i Analytics.
keywords: ID-tjänst
title: Åtgärdsordning för analys-ID:n
exl-id: 8ee340fe-ef3b-40e6-9441-7ee0c9e20357
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# Åtgärdsordning för analys-ID:n{#order-of-operations-for-analytics-ids}

När du har distribuerat besökar-ID-tjänsten kan en besökare identifieras på fem olika sätt i Analytics.

I många scenarier kan du se två eller tre olika ID:n för ett samtal, men Analytics använder det första ID:t som finns i listan som officiell [!DNL Experience Cloud] ID. Om du till exempel anger ett anpassat besökar-ID (ingår i `vid` frågeparameter), kommer detta ID att användas före andra ID:n som kan finnas i samma träff. Se [Ställa in analyser och Experience Cloud-ID:n](../../reference/analytics-reference/analytics-ids.md#concept-f381dd18ee184c6c8e48286937a161d6) för mer information.

<table id="table_D267D36451F643D1BB68AF6FEAA6AD1A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Använd order </th> 
   <th colname="col2" class="entry"> Frågeparameter (samlingsmetod) </th> 
   <th colname="col3" class="entry"> Presentera när </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>1<sup>st</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html" format="http" scope="external"> vid (s.visitorID)</a> </p> </td> 
   <td colname="col3"> <p>The <span class="codeph"> s.visitorID</span> är inställt. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>2<sup>end</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-analytics.html" format="http" scope="external"> hjälp (s_vi cookie)</a> </p> </td> 
   <td colname="col3"> <p>Besökaren hade en befintlig s_vi-cookie innan du distribuerade <span class="keyword"> Experience Cloud</span> ID-tjänst, eller så har du en <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local"> respitperiod</a> konfigurerad. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>3<sup>rd</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="../../introduction/cookies.md#section-7ff7d96d6e4141b08a84a75a63d7814c" format="dita" scope="local"> Experience Cloud ID (MID) </a> </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar cookies från första part. Detta anges av AMCV-cookien. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>4<sup>th</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html" format="http" scope="external"> fet (återgångscookie i H.25.3 eller senare, eller AppMeasurement för JavaScript)</a> </p> </td> 
   <td colname="col3"> <p>En webbläsare accepterar inte cookies från tredje part och Analytics tracking-servern är konfigurerad som en spårningsserver från tredje part. </p> <p> <p>Obs! The <span class="codeph"> fet</span> är en äldre identifierare och används inte om du har implementerat ID-tjänsten på din plats. I det här fallet <span class="codeph"> fet</span> behövs inte eftersom förstaparten, <a href="../../introduction/cookies.md" format="dita" scope="local"> AMCV cookie</a> gör det föråldrat. Den har bibehållits för att stödja äldre kod och av historiska skäl. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>5<sup>th</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/analytics/technotes/visitor-identification.html" format="http" scope="external"> IP-adress, användaragent, gateway-IP-adress</a> </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar inte cookies. </p> </td> 
  </tr> 
 </tbody> 
</table>
