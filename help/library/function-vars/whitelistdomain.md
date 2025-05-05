---
description: Med dessa konfigurationer kan olika instanser av ID-tjänstkod som implementeras i en iFrame och på den överordnade sidan kommunicera med varandra. De är utformade för att lösa problem med två specifika användningsfall där du kan styra den överordnade sidan/domänen eller inte, och där du har ID-tjänstkoden inläst i iFrame för en domän som du har kontroll över. De är tillgängliga i VisitorAPI.js-koden version 2.2 eller senare.
keywords: ID-tjänst
title: whitelistParentDomain och whitelistIframeDomains
exl-id: 0ed1da79-7129-4f5f-b7ad-901348a13866
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# whitelistParentDomain och whitelistIframeDomains{#whitelistparentdomain-and-whitelistiframedomains}

Med dessa konfigurationer kan olika instanser av ID-tjänstkod som implementeras i en iFrame och på den överordnade sidan kommunicera med varandra. De är utformade för att lösa problem med två specifika användningsfall där du kan styra den överordnade sidan/domänen eller inte, och där du har ID-tjänstkoden inläst i iFrame för en domän som du har kontroll över. De är tillgängliga i VisitorAPI.js-koden version 2.2 eller senare.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/function-vars/whitelistdomain.md#section-f645198bbaba4fba8961acb6e88d1470" format="dita" scope="local"> Syntax </a> </li> 
 <li> <a href="../../library/function-vars/whitelistdomain.md#section-09d0049fe88a473baa69d404c50bf8ae" format="dita" scope="local"> Kodexempel </a> </li> 
 <li> <a href="../../library/function-vars/whitelistdomain.md#section-fc2eeb93546b406fae3b102dbcd11de7" format="dita" scope="local"> Användningsexempel </a> </li> 
 <li> <a href="../../library/function-vars/whitelistdomain.md#section-2b1ce31fab034e1ca0f6b1c3cc57a6e2" format="dita" scope="local"> Säkerhet och säkerhet för konfiguration </a> </li> 
 <li> <a href="../../library/function-vars/whitelistdomain.md#section-30c6a9f4dcdc4265a1149260b97cc057" format="dita" scope="local"> Visitor API-metoder som stöds </a> </li> 
</ul>

## Syntax {#section-f645198bbaba4fba8961acb6e88d1470}

Båda konfigurationselementen krävs när du använder den här koden.

<table id="table_237108A4D40F4AAC981D0060BA68F881"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Konfigurationssyntax </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> whitelistParentDomain: <span class="varname"> Domännamn för överordnad sida </span> </span> </p> </td> 
   <td colname="col2"> <p>Accepterar ett domännamn som skickas som en sträng. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> whitelistIframeDomains: [ <span class="varname"> "iFrame domain","iFrame domain","iFrame domain" </span>] </span> </p> </td> 
   <td colname="col2"> <p>Accepterar ett eller flera iFrame-domännamn som skickas som en array. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Kodexempel {#section-09d0049fe88a473baa69d404c50bf8ae}

Den konfigurerade [!UICONTROL ID service]-koden kan se ut ungefär som i det här exemplet.

```js
//Instantiate Visitor 
var visitor = Visitor.getInstance("Insert Experience Cloud Organization ID here",{ 
 ... 
 //Add parent page domain name and iFrame domain names 
 whitelistParentDomain: "parentpageA.com", 
 whitelistIframeDomains: ["iFrameDomain1.com","iFrameDomain2.com"], 
 ... 
 } 
);
```

## Användningsfall {#section-fc2eeb93546b406fae3b102dbcd11de7}

Dessa konfigurationer hjälper dig att lösa problemet med att ställa in en cookie för en ID-tjänst och tilldela ett besökar-ID när webbläsare blockerar cookies från tredje part och om något av dessa villkor gäller:

* Du kontrollerar eller kontrollerar inte den överordnade sidan/domänen.
* ID-tjänstkoden är inte installerad på den överordnade sidan, men implementeras i en iFrame.

>[!TIP]
>
>Du kanske också vill implementera de här konfigurationerna när du visar video i en iFrame med [videominnen](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=sv-SE). Videopulsen behöver ett ID-tjänst-ID (MID) för att fungera korrekt.

**Användningsfall 1: Webbläsaren blockerar cookies från tredje part och ID-tjänsten implementeras på iFrame- och överordnad sida**

<table id="table_B479AA96DBE64685A253A6DF98D81B31"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Använd skiftlägeselement </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Villkor</b> </p> </td> 
   <td colname="col2"> <p>Detta användningsexempel omfattar följande villkor: </p> <p> 
     <ul id="ul_DC748846585745B0AB74398D82BDA53A"> 
      <li id="li_6E04CF0B6A204B4D8856656B0C9EF2A5">Företag A implementerar ID-tjänsten på sin hemsida. </li> 
      <li id="li_B53AE0F0C69844E7B6C4D3464C57883B">Företag A implementerar ID-tjänsten i iFrame på sin hemsida. </li> 
      <li id="li_07E0A6D7BEB140E4B9FB6C7B9629B860">Företag A äger den överordnade sidan och iFrame och har implementerat ID-tjänsten på båda platserna. </li> 
      <li id="li_76967BD69DDB40A8A9C915DADC58AC62">En kund läser in den överordnade sidan i en webbläsare som blockerar cookies från tredje part. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Resultat</b> </p> </td> 
   <td colname="col2"> <p>Med tanke på dessa villkor kan ID-tjänsten: </p> <p> 
     <ul id="ul_12356701501E40DFA57903494FFE58F7"> 
      <li id="li_B57EDF1B0762486F95FA6526C047390C">Fungerar korrekt på den överordnade sidan. Den begär och ställer in AMCV-cookien och tilldelar ett unikt ID till besökaren. </li> 
      <li id="li_BA9F42C759E747EAAE14DD3FBB6130A5">Fungerar inte i iFrame. Detta beror på att webbläsaren ser iFrame som en tredjepartsdomän och förhindrar att ID-tjänsten ställer in AMCV-cookien. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Lösning</b> </p> </td> 
   <td colname="col2"> <p>Ändra ID-tjänstens <span class="codeph"> Visitor.getInstance </span>-funktion i iFrame med dessa vita listkonfigurationer. Ange de överordnade och underordnade domänerna i koden. Dessa konfigurationer gör att ID-tjänstkoden i iFrame kan kontrollera ID-tjänstkoden på den överordnade sidan för ett besökar-ID. </p> <p>Om ID-tjänstkoden i iFrame inte får någon överordnad svarssida genererar dessa konfigurationer ett lokalt besökar-ID. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Använd fall 2: Begär ett ID från en iFrame som är inbäddad i en överordnad sida som du inte kontrollerar eller som inte använder ID-tjänsten**

<table id="table_1F21710F9D5F493BA6BA5974F2966DF4"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Använd skiftlägeselement </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Villkor</b> </p> </td> 
   <td colname="col2"> <p>Detta användningsexempel omfattar följande villkor: </p> <p> 
     <ul id="ul_356E8FB0B1D14F46A844FE5281967E28"> 
      <li id="li_1285D945361842268B46FB492A3B5AA5">Företag A använder inte ID-tjänsten. </li> 
      <li id="li_880D6D473F8342FF9BB49FCE111FD61A">Företag A läser in en iFrame på sidan. Den här iFrame ägs av företag B och läses in i en separat domän än som företag A. </li> 
      <li id="li_7988F0272B094FE0B398006AD4E6F81B">Webbläsaren blockerar cookies från tredje part. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Resultat</b> </p> </td> 
   <td colname="col2"> <p>Med tanke på dessa villkor kan ID-tjänsten: </p> <p> 
     <ul id="ul_A92D90896E5A42C5804AC5CE83E8EB25"> 
      <li id="li_9734EA9C5D9D4F908DE783188C9E5530">Fungerar inte i iFrame. Detta beror på att webbläsaren ser iFrame som en tredjepartsdomän och förhindrar att ID-tjänsten ställer in AMCV-cookien. </li> 
      <li id="li_3F4BE9048E774902A867D67E5A80674D">Det går inte att hämta ett besökar-ID från den överordnade sidan eftersom företag A inte använder den här tjänsten. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Lösning</b> </p> </td> 
   <td colname="col2"> <p>Ändra ID-tjänstens <span class="codeph"> Visitor.getInstance </span>-funktion i iFrame med dessa vita listkonfigurationer. Ange de överordnade och underordnade domänerna i koden. Dessa konfigurationer gör att ID-tjänstkoden i iFrame kan kontrollera ID-tjänstkoden på den överordnade sidan för ett besökar-ID. </p> <p>Om ID-tjänstkoden i iFrame inte får någon överordnad svarssida genererar dessa konfigurationer ett lokalt besökar-ID. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Säkerhet och säkerhet för konfiguration {#section-2b1ce31fab034e1ca0f6b1c3cc57a6e2}

Du kan implementera dessa konfigurationer på ett säkert sätt eftersom:

* ID-tjänsten som implementeras på den överordnade domänen och iFrame-domänen måste använda samma organisations-ID. De här konfigurationerna för vit lista fungerar inte när organisations-ID:n på den överordnade eller iFrame är olika.
* Dessa konfigurationer kommunicerar bara med den domän och iFrames som anges i koden.
* Kommunikationen mellan iFrame och den överordnade sidan har ett visst format. Om ID-tjänsten på den överordnade sidan inte tar emot någon begäran i det förväntade formatet kommer denna delningsprocess att misslyckas.

## API-metoder för besökare som stöds {#section-30c6a9f4dcdc4265a1149260b97cc057}

ID-tjänsten har stöd för en begränsad uppsättning publika API-metoder när du implementerar dessa konfigurationer för vit lista. Vilka metoder som stöds varierar beroende på vilka scenarier för användningsfall som beskrivs ovan.

<table id="table_0FF9E529FD1C43A8A3B2B0D789C8E83C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Användningsfall </th> 
   <th colname="col2" class="entry"> Metoder som stöds </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Fall 1</b> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_99FAC8608F4C4B39805EEAA6297DB771"> 
      <li id="li_B13F6C4119F44F17963794B1E2046B1F"> <span class="codeph"> getMarketingCloudID </span> </li> 
      <li id="li_9C1B5C00A17F467CAB7EFE5F0D040777"> <span class="codeph"> getAudienceManagerLocationHint </span> </li> 
      <li id="li_30D4608F4C3849659FCBA97D88A10F0C"> <span class="codeph"> getAudienceManagerBlob </span> </li> 
      <li id="li_BA359596C80147EEA89CABCE83F123CA"> <span class="codeph"> getSupplementalDataID </span> </li> 
      <li id="li_26774089B6854CD6A3216043B6EEA01B"> <span class="codeph"> getCustomerID:n </span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Fall 2</b> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_CCAD7E362E7F4DAB9D5C3E166EEE6BDD"> 
      <li id="li_1F0B006BAD044ECBA5604625DE411E84"> <span class="codeph"> getSupplementalDataID </span> </li> 
      <li id="li_C6022223C8314B9C923202207C7472EA"> <span class="codeph"> getMarketingCloudVisitorID </span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
