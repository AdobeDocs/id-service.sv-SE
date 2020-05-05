---
description: Den här implementeringen gör att kunder kan använda ID-tjänsten på enheter som inte kan acceptera eller arbeta med vår JavaScript- eller SDK-kod. Detta omfattar enheter som spelkonsoler, smarta TV-apparater eller andra internetanslutna enheter. I det här avsnittet finns syntax, kodexempel och definitioner.
keywords: ID Service
seo-description: Den här implementeringen gör att kunder kan använda ID-tjänsten på enheter som inte kan acceptera eller arbeta med vår JavaScript- eller SDK-kod. Detta omfattar enheter som spelkonsoler, smarta TV-apparater eller andra internetanslutna enheter. I det här avsnittet finns syntax, kodexempel och definitioner.
seo-title: Direktintegrering med Experience Cloud Identity Service
title: Direktintegrering med Experience Cloud Identity Service
uuid: de502f7e-cffd-4130-b3ca-7d6b9a9caae9
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# Direktintegrering med Experience Cloud Identity Service {#direct-integration-with-the-experience-cloud-id-service}

Den här implementeringen gör att kunder kan använda ID-tjänsten på enheter som inte kan acceptera eller arbeta med vår JavaScript- eller SDK-kod. Detta omfattar enheter som spelkonsoler, smarta TV-apparater eller andra internetanslutna enheter. I det här avsnittet finns syntax, kodexempel och definitioner.

## Syntax {#section-a4754afec5ad40b6be00d6f1011d68bb}

Enheter som inte kan använda kodbiblioteken VisitorAPI.js eller SDK kan anropa direkt till de datainsamlingsservrar (DCS) som används av ID-tjänsten. Om du vill göra det ringer du `dpm.demdex.net` och formaterar din begäran enligt nedan. *Kursiv anger* en variabelplatshållare.

![](assets/directSyntax.png)

I det här syntaxexemplet identifierar `d_` prefixet nyckelvärdepar i anropet som en systemnivåvariabel. Du kan skicka flera `d_` parametrar till ID-tjänsten, men fokusera på nyckelvärdepar enligt koden ovan. Mer information om andra variabler finns i [Attribut som stöds för DCS API-anrop](https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys.html).

ID-tjänsten stöder HTTP- och HTTPS-anrop. Använd HTTPS för att skicka data från en säker sida.

## Exempelbegäran {#section-26302b8851704888b6f8e6b2071bcdb0}

Din förfrågan kan se ut som exemplet nedan. Långa variabler har förkortats.

![](assets/directExample.png)

## Exempelsvar {#section-89bc103b3e9e4a8b98e74c32897b1200}

ID-tjänsten returnerar data i ett JSON-objekt enligt nedan. Ditt svar kan vara annorlunda.

```js
{
     "d_mid":"12345",
     "dcs_region":"6",
     "id_sync_ttl":"604800",
     "d_blob":"wxyz5432"
}
```

## Parametrar för begäran och svar har definierats {#section-4a9912b545364dc4acad4f1ea5ec641d}

**Parametrar för begäran**

<table id="table_C8FFA89AB74E4E31A6926CDE5CD54217"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Parameter </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> dpm.demdex.net</span> </p> </td> 
   <td colname="col2"> <p>En äldre domän som styrs av <span class="keyword"> Adobe</span>. Se <a href="https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/demdex-calls.html" format="https" scope="external"> Förstå anrop till Demdex-domänen</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_mitt</span> </p> </td> 
   <td colname="col2"> <p>Besökar-ID för Experience Cloud. See <a href="../introduction/cookies.md" format="dita" scope="local"> Cookies and the Experience Cloud Identity Service</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_orgid</span> </p> </td> 
   <td colname="col2"> <p>Ditt Experience Cloud-organisations-ID. Mer information om hur du hittar det här ID:t finns i <a href="../reference/requirements.md" format="dita" scope="local"> Krav för Experience Cloud Identity Service</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_cid</span> </p> </td> 
   <td colname="col2"> <p>En valfri parameter som skickar Data Provider ID (DPID), det unika användar-ID:t (DPUUID) och ett <a href="../reference/authenticated-state.md" format="dita" scope="local"> autentiserat tillstånds-ID</a> till ID-tjänsten. Som du kan se i kodexemplet separerar du DPID och DPUID med kontrolltecknet som inte skrivs ut, <span class="codeph"> %01</span>. </p> <p> <b>DPID och DPUID</b> </p> <p>I parametern <span class="codeph"> d_cid</span> tilldelar du varje relaterad DPID- och DPUID-kombination till samma <span class="codeph"> d_cid</span> -parameter. På så sätt kan du returnera flera ID-uppsättningar i en enda begäran. Separera också DPID, DPUID och valfri autentiseringsflagga med kontrolltecknet som inte skrivs ut, <span class="codeph"> %01</span>. I exemplen nedan markeras provider- och användar-ID i <b>fet</b> text. </p> 
    <ul id="ul_2E19D837296B40E9ACD096495CF711C5"> 
     <li id="li_5B94B057654440B99B989BA60E4ED053">Syntax: <span class="codeph">...d_cid=DPID%01DPUUID%01autentiseringsläge..</span> </li> 
     <li id="li_B07833EF51D54F088574B7B7F9FB841A">Exempel: <span class="codeph">...d_cid=123%01456%011..</span> </li> 
    </ul> <p> <b>Autentiseringstillstånd</b> </p> <p>Detta är ett valfritt ID i parametern <span class="codeph"> d_cid</span> . Uttryckt som ett heltal identifierar det användare utifrån deras autentiseringsstatus enligt nedan: </p> 
    <ul id="ul_E2B36922B11C4AA2A9016B6E2DC9EDAA"> 
     <li id="li_31C018E3F9514B938C73EF40C436715F"> <span class="codeph"> 0</span> (okänd) </li> 
     <li id="li_1F125C3879324C2F8EF4613C0ECB5F02"> <span class="codeph"> 1</span> (autentiserad) </li> 
     <li id="li_EF6792D0115D407485079D5D7480D965"> <span class="codeph"> 2</span> (utloggad) </li> 
    </ul> <p>Om du vill ange ett autentiseringstillstånd anger du den här flaggan efter variabeln för användar-ID (UUID). Avgränsa UUID- och autentiseringsflaggan med kontrolltecknet som inte skrivs ut, <span class="codeph"> %01</span>. I exemplen nedan markeras autentiserings-ID:n i <b>fet</b> text. </p> <p>Syntax: <span class="codeph">...d_cid=DPID%01DPUUID%01autentiseringsläge</span> </p> <p>Exempel: </p> 
    <ul id="ul_4C1054CE860A4D9C8DD85C2A8020C47F"> 
     <li id="li_AD4000BF3E0146C0BD37B1EC513EC314">Okänd: <span class="codeph">...d_cid=123%01456%010...</span> </li> 
     <li id="li_B037D424AADA4D41BF29381A9602AE61">Autentiserad: <span class="codeph">...d_cid=123%01456%011..</span> </li> 
     <li id="li_0410FCB9E60D4DD08E7898D814E1C3C9">Utloggad: <span class="codeph">...d_cid=123%01456%012...</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> dcs_region</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten är ett geografiskt distribuerat och lastbalanserat system. ID:t identifierar den region i datacentret som hanterar anropet. Se <a href="https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html" format="https" scope="external"> DCS-regions-ID, -platser och -värdnamn</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_cb</span> </p> </td> 
   <td colname="col2"> <p> <i>(Valfritt)</i> En callback-parameter som gör att du kan köra en JavaScript-funktion i begärandetexten. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_blob</span> </p> </td> 
   <td colname="col2"> <p>Ett krypterat segment med JavaScript-metadata. Storleksbegränsningar begränsar blobben till 512 byte eller mindre. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> d_ver</span> </p> </td> 
   <td colname="col2"> <p>Obligatoriskt. Detta anger API-versionsnumret. Låt den här uppsättningen vara <span class="codeph"> d_ver=2</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Svarsparametrar**

Vissa svarsparametrar ingår i begäran och har definierats i avsnittet ovan.

<table id="table_58D0E8876DDC4A81B1F24F845E87EC18"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Parameter </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id_sync_ttl</span> </p> </td> 
   <td colname="col2"> <p>Intervallet för omsynkronisering, angivet i sekunder. Standardintervallet är 604 800 sekunder (7 dagar). </p> </td> 
  </tr> 
 </tbody> 
</table>

