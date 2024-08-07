---
description: Webbläsare använder Cross Origin Resource Sharing (CORS) för att begära resurser från en annan domän än den aktuella domänen. Experience Cloud Identity Service stöder CORS-standarder som möjliggör dessa serverförfrågningar på klientsidan. ID-tjänsten återgår till JSONP-begäranden i äldre webbläsare eller webbläsare som inte stöder CORS.
keywords: ID-tjänst
title: CORS-stöd i Experience Cloud Identity Service
exl-id: 0e8ffe85-8d1f-42a0-aae3-a2b3b28c7bce
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# CORS-stöd i Experience Cloud Identity Service {#cors-support-in-the-experience-cloud-id-service}

Webbläsare använder Cross Origin Resource Sharing (CORS) för att begära resurser från en annan domän än den aktuella domänen. Experience Cloud Identity Service stöder CORS-standarder som möjliggör dessa serverförfrågningar på klientsidan. ID-tjänsten återgår till JSONP-begäranden i äldre webbläsare eller webbläsare som inte stöder CORS.

## Problem med samma ursprung-principer och ID-serviceförfrågningar {#section-6608cf46d27143eeaeabacaa6aa14e8e}

Principer för samma ursprung är säkerhetskontroller eller begränsningar som används av en webbläsare. När den används på den här nivån avgör webbläsaren själv om en begäran om resurser som skapats från en sida till en annan ska tillåtas eller blockeras. För att avgöra om en begäran är en begäran med samma ursprung jämför webbläsaren följande:

* URI (Uniform Resource Identifiers)
* Värdnamn (t.ex. http://www.my-webpage-example.com)
* Portnummer (t.ex. port 80 och 440 för HTTP- och HTTPS-begäranden)

Webbläsaren tillåter en begäran att lyckas om båda sidorna delar dessa egenskaper och blockerar resursbegäranden om de inte gör det.

## CORS löser problem med principer med samma ursprung {#section-76c87ec3295d447bab220c84f138c235}

CORS erbjuder ett säkert och effektivt sätt att begära resurser över olika domäner. CORS-specifikationen innehåller en uppsättning HTTP-rubriker som används i webbläsare för att skicka, ta emot och utvärdera resursbegäranden. Utvärderingen av en resursbegäran kallas *`preflight check`*. Med den här kontrollen kan webbläsare och servrar avgöra vilka begäranden som tillåts eller blockeras. Preflight-kontrollen är genomskinlig för programmet, API:t eller skriptet som begär en resurs. Två huvuden som är viktiga i resursförfrågningsprocessen är:

* `Origin`: Ett begärandehuvud som identifierar källan för en begäran.
* `Access-Control-Allow-Origin`: Ett svarshuvud som anger om en resurs kan delas med den som gjorde begäran.

Låt oss titta på hur de här rubrikerna fungerar. I det här exemplet ska vi säga att vi har ett finansserviceföretag som har implementerat ID-tjänsten [!DNL Experience Cloud] på sin webbplats, www.finance-website.com. Följande tabell definierar hur CORS-begärande och svarshuvuden kontrollerar om det finns åtkomst till en resurs.

<table id="table_B004ACF52B5A4D33B1DCF7EA77BE4E6D"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Åtgärd </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Begäran</b> </p> </td> 
   <td colname="col2"> <p>När finansföretagets sida läses in gör webbläsaren en begäran till <span class="codeph"> dpm.demdex.net</span>. Detta är ett anrop till domänen för de datainsamlingsservrar (DCS) som används av ID-tjänsten. Denna korsdomänbegäran innehåller rubriken: </p> <p> 
     <ul class="simplelist"> 
      <li> <span class="codeph"> Origin:https://www.finance-website.com </span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Svar</b> </p> </td> 
   <td colname="col2"> <p>Svaret från DCS-domänen innehåller följande rubriker som ger det finansiella företagets webbplats tillgång till nödvändiga resurser: </p> <p> 
     <ul class="simplelist"> 
      <li> <span class="codeph"> Access-Control-Allow-origin: https://www.finance-website.com</span> </li> 
      <li> <span class="codeph"> Access-Control-Allow-Credentials: true</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

Se även [useCORSOnly](../library/function-vars/use-cors-only.md#reference-8a9a143d838b48d6b23329b84b13e1fa).

## Andra fördelar med att använda CORS {#section-6f44f30694c44f95bf9854b8a2af8449}

Tabellen nedan beskriver några av de fördelar CORS ger kunder som använder ID-tjänsten.

<table id="table_AEB51A263D454F90B66E8C8D0513CF79"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Fördelar </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>Ökad säkerhet</b> </p> </td> 
   <td colname="col2"> <p>CORS använder <a href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest" format="https" scope="external"> XMLHttpRequest</a> för att begära och överföra data. Den här metoden är säkrare än en JSONP-begäran. Det säkerställer att det inte finns något sätt att köra godtyckliga JavaScript som kan finnas i svaret från DCS. CORS XMLHttpRequest-svarsnyttolasten tolkas av ID-tjänsten JavaScript och körs inte bara i en callback-funktion. </p> <p> <p>Obs! Om du vill acceptera cookies måste egenskapen <span class="codeph"> withCredentials</span> anges till <span class="codeph"> true </span> för objektet <span class="codeph"> XMLHttpRequest</span> . Den här egenskapen stöds i Chrome, Firefox, Internet Explorer (v10+), Opera och Safari. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Prestandaförbättringar</b> </p> </td> 
   <td colname="col2"> <p>CORS förbättrar prestanda eftersom: </p> 
    <ul id="ul_EC3A178003A94D70883B914050D7C464"> 
     <li id="li_F8B44352BFBB46CDBD07AE40B9F2D0EC">Webbläsaren hanterar resursbegäranden. Begärandeprocessen är transparent för ID-tjänsten. </li> 
     <li id="li_C63E43A4CAB84210AB6A39100E5864BE">Till skillnad från asynkrona JSONP-begäranden avprioriterar inte webbläsaren CORS-begäranden och placerar dem i kö. </li> 
     <li id="li_1A2A15F591B84D1BAED3CFAB391EEBEC">ID-tjänsten svarar frivilligt. Detta innebär att när en URL som skickades som <span class="codeph"> Origin</span>, ger ID-tjänsten sidåtkomst till de nödvändiga resurserna. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
