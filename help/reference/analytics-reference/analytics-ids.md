---
description: Experience Cloud Identity Service ersätter de gamla ID-metoderna för Analytics-besökare.
keywords: ID-tjänst
title: Ställa in analyser och Experience Cloud-ID
exl-id: 7399ea16-d13e-452c-b8d9-8d0699566aa2
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Ställa in analyser och Experience Cloud-ID{#setting-analytics-and-experience-cloud-ids}

Experience Cloud Identity Service ersätter de gamla ID-metoderna för Analytics-besökare.

När ID-tjänsten har implementerats körs den här koden före AppMeasurementet. ID-tjänsten hämtar Experience Cloud och analys-ID:n så att dessa värden är klara när AppMeasurementet läses in.

När AppMeasurementet läses in begärs ID-värdena för Experience Cloud och analys från ID-tjänsten och skickas till datainsamling med varje serveranrop. Eftersom ID-tjänsten avgör besökar-ID:t och skickar det till AppMeasurementet, måste ID-tjänsten inkluderas och implementeras på varje sida innan AppMeasurement JavaScript-filen skickas.

## Ändringar i analys-ID-processen {#section-79bb86ae63f546419bb1a7ef5e710462}

Den största förändringen när du migrerar till ID-tjänsten [!DNL Experience Cloud] är att ID-cookien ställs in med JavaScript, i stället för i HTTP-huvudet som returneras från webbservern för datainsamling. För att förstå den här ändringen beskriver följande avsnitt hur cookies ställs in med dessa två metoder.

**HTTP-huvud**

Ett HTTP-svar från en webbserver anger cookies i en webbläsare. Så här är cookien `s_vi` inställd. Cookien `s_vi` identifierar Analytics-besökare. När en cookie har angetts skickas den med alla efterföljande HTTP-begäranden till den servern.

När en begäran skickas till datainsamlingsservern Adobe kontrolleras rubriken för cookien `s_vi`. Om den här cookien finns i begäran används den för att identifiera besökaren. Om cookie-filen inte finns i begäran genererar servern ett unikt [!DNL Experience Cloud]-ID, anger den som en cookie i HTTP-svarshuvudet och skickar tillbaka den med begäran. Cookien lagras i webbläsaren och skickas tillbaka till datainsamlingsservern vid efterföljande besök på webbplatsen. På så sätt kan besökaren identifieras vid olika besök.

Vissa webbläsare, till exempel Apple Safari, accepterar dock inte cookies från tredje part. Detta är cookies som anges i webbläsaren från andra domäner än den aktuella webbplatsen. Dessutom blockerar Safari cookies i tredjepartsdomäner om en besökare inte har varit i den domänen tidigare. Om du till exempel är på `mysite.com` och din datainsamlingsserver är `mysite.omtrdc.net` kan den cookie som returneras i HTTP-huvudet från `mysite.omtrdc.net` avvisas av webbläsaren.

För att undvika detta har många kunder implementerat CNAME-poster för sina datainsamlingsservrar. Detta kan vara en effektiv del av en [förstapartsstrategi för cookie-implementering](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html). Om en CNAME-post har konfigurerats för att mappa ett värdnamn på kundens domän till datainsamlingsservern (t.ex. mappning `metrics.mysite.com` till `mysite.omtrdc.net`), lagras [!DNL Experience Cloud]-ID-cookien eftersom datainsamlingsdomänen nu matchar webbplatsens domän. Detta ökar sannolikheten för att ID-tjänstens cookie lagras. Detta medför emellertid en viss belastning eftersom du måste konfigurera CNAME-poster och upprätthålla SSL-certifikat för datainsamlingsservrarna.

**JavaScript**

JavaScript kan läsa och skriva cookies som angetts i förstahandsdomänen (domänen för den aktuella webbplatsen). ID-tjänsten [!DNL Experience Cloud] använder den här metoden för att ange cookien `AMCV_###@AdobeOrg` som innehåller alla besökar-ID:n, så spårningsserverns domän behöver inte längre matcha webbplatsens domän för att besökar-ID-cookien ska kunna lagras. I de flesta fall är det här det bästa sättet att ange ID-tjänstens cookie eftersom den eliminerar overheadkostnaden för CNAME-poster och SSL-certifikat.

<!---However, there are a few situations where setting the cookie in the HTTP header is beneficial for cross-domain tracking, which is described in [Data Collection CNAMEs and Cross-Domain Tracking](../../reference/analytics-reference/cname.md#concept-4df91f8a30ad4ec7a01eb943d579cc9d).-->

## ID för anpassade analyser {#section-b6a7bd19e9ff432390010062450808f6}

Att ange ett kund-ID med `s.visitorID` är ett sätt att identifiera användare i Analytics. Integrationer där Analytics-data exporteras eller importeras med ID-tjänsten kommer dock inte att fungera när en besökare identifieras med `s.visitorID`.

Detta omfattar, men är inte begränsat till, delade målgrupper, analys för mål (A4T) och kundattribut. För dessa integreringar stöds inte inställning av ett anpassat analys-ID.

## Analysbesökarens ID-ordning {#section-de1dc9fc9b6d4388995b70e35b8bcddf}

När du har distribuerat besökar-ID-tjänsten finns det fem sätt som en besökare kan identifieras i Analytics (listas i följande tabell i prioritetsordning):

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
   <td colname="col1"> <p> <img id="image_9F3E58898A1B4F40BBDEF5ADE362E55C" src="assets/step1_icon.png" /> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html" format="http" scope="external"> vid (s.visitorID)</a> </p> </td> 
   <td colname="col3"> <p>s.visitorID har angetts </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <img id="image_77A06981672745B6AEA8BB4D55911CCA" src="assets/step2_icon.png" /> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-analytics.html" format="http" scope="external"> hjälp (s_vi cookie)</a> </p> </td> 
   <td colname="col3"> <p>Besökaren hade en befintlig s_vi-cookie innan du distribuerade ID-tjänsten <span class="keyword"> Experience Cloud</span>, eller så har du konfigurerat en <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local"> respitperiod </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <img id="image_0A950B1A6B004387AFEE8EED882739CB" src="assets/step3_icon.png" /> </p> </td> 
   <td colname="col2"> <p>mitten (AMCV_ cookie inställd av Experience Cloud besökar-ID-tjänst) </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar cookies från första part </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <img id="image_6F0ED8FE3EF846CA8E6ECCC3C0070D85" src="assets/step4_icon.png" /> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html" format="http" scope="external">-sökning (grundcookie på H.25.3 eller senare, eller AppMeasurement för JavaScript)</a> </p> </td> 
   <td colname="col3"> <p>En webbläsare accepterar inte cookies från tredje part och Analytics tracking-servern är konfigurerad som en spårningsserver från tredje part. </p> <p> <p>Obs! <span class="codeph">-fältet </span> är en äldre identifierare och används inte om du har implementerat ID-tjänsten på din plats. I det här fallet behövs inte fältet <span class="codeph"> </span> eftersom den första parten, <a href="../../introduction/cookies.md" format="dita" scope="local"> AMCV cookie </a>, gör den föråldrad. Den har bibehållits för att stödja äldre kod och av historiska skäl. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <img id="image_23D8C0EB69EC4084BC237B5B98C036F4" src="assets/step5_icon.png" /> </p> </td> 
   <td colname="col2"> <p> <a href="https://experienceleague.adobe.com/docs/analytics/technotes/visitor-identification.html" format="http" scope="external"> IP-adress, användaragent, gateway-IP-adress </a> </p> </td> 
   <td colname="col3"> <p>Besökarens webbläsare accepterar inte cookies. </p> </td> 
  </tr> 
 </tbody> 
</table>

I många scenarier kan du se två eller tre olika ID:n för ett samtal, men Analytics använder det första ID:t som finns i listan som officiellt [!DNL Experience Cloud]-ID. Om du till exempel anger ett anpassat besökar-ID (som ingår i frågeparametern&quot;vid&quot;) kommer detta ID att användas före andra ID:n som kan finnas i samma träff.

>[!MORELIKETHIS]
>
>* [Åtgärdsordning för analys-ID:n](../../reference/analytics-reference/analytics-order-of-operations.md#concept-b92935b4fff545adb4773f3728bc15ef)
