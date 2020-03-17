---
description: När du har distribuerat besökar-ID-tjänsten kan en besökare identifieras på fem olika sätt i Analytics.
keywords: ID Service
seo-description: När du har distribuerat besökar-ID-tjänsten kan en besökare identifieras på fem olika sätt i Analytics.
seo-title: Åtgärdsordning för analys-ID:n
title: Åtgärdsordning för analys-ID:n
uuid: cb1d136e-093f-43b0-a7e1-96f1e61fdad0
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# Åtgärdsordning för analys-ID:n{#order-of-operations-for-analytics-ids}

När du har distribuerat besökar-ID-tjänsten kan en besökare identifieras på fem olika sätt i Analytics.

I många scenarier kan du se två eller tre olika ID:n för ett samtal, men Analytics använder det första ID:t som finns i listan som officiellt [!DNL Experience Cloud] ID. Om du till exempel anger ett anpassat besökar-ID (som ingår i `vid` frågeparametern) kommer detta ID att användas före andra ID:n som kan finnas i samma träff. Mer information finns i [Ange analyser och Experience Cloud-ID](../../reference/analytics-reference/analytics-ids.md#concept-f381dd18ee184c6c8e48286937a161d6) .

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
   <td colname="col2"> <p> <a href="https://marketing.adobe.com/resources/help/en_US/sc/implement/?f=visid_custom" format="http" scope="external"> vid (s.visitorID)</a> </p> </td> 
   <td colname="col3"> <p>s.visitor <span class="codeph"> ID</span> har angetts. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>2<sup>nd</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://marketing.adobe.com/resources/help/en_US/sc/implement/?f=visid_analytics" format="http" scope="external"> hjälp (s_vi cookie)</a> </p> </td> 
   <td colname="col3"> <p>Besökaren hade en befintlig s_vi-cookie innan du distribuerade <span class="keyword"> Experience Cloud</span> ID-tjänsten, eller så har du konfigurerat en <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local"> respitperiod</a> . </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>3<sup>rd</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="../../introduction/cookies.md#section-7ff7d96d6e4141b08a84a75a63d7814c" format="dita" scope="local"> Experience Cloud ID (MID) </a> </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar cookies från första part. Detta anges av AMCV-cookien. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>4<sup>:e</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://marketing.adobe.com/resources/help/en_US/sc/implement/?f=visid_fallback" format="http" scope="external"> fet (återgångscookie i H.25.3 eller senare, eller AppMeasurement för JavaScript)</a> </p> </td> 
   <td colname="col3"> <p>En webbläsare accepterar inte cookies från tredje part och Analytics tracking-servern är konfigurerad som en spårningsserver från tredje part. </p> <p> <p>Obs! Det <span class="codeph"> här fältet</span> är en äldre identifierare och används inte om du har implementerat ID-tjänsten på din plats. I det här fallet behövs inte <span class="codeph"> sökningen</span> eftersom den första parten, <a href="../../introduction/cookies.md" format="dita" scope="local"> AMCV cookie</a> , gör den föråldrad. Den har bibehållits för att stödja äldre kod och av historiska skäl. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>5<sup>:e</sup></b> </p> </td> 
   <td colname="col2"> <p> <a href="https://marketing.adobe.com/resources/help/en_US/sc/implement/?f=visid_fallback" format="http" scope="external"> IP-adress, användaragent, gateway-IP-adress</a> </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar inte cookies. </p> </td> 
  </tr> 
 </tbody> 
</table>

