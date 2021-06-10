---
description: En CSP (Content Security Policy) är en HTTP-rubrik och säkerhetsfunktion som ger webbläsarna kontroll över vilken typ av resurser som läses in på en webbsida. Granska det här avsnittet om du använder ID-tjänsten och har strikta CSP:er som använder vitlistor för att ta emot resurser från betrodda domäner. Du måste lägga till de Adobe-domäner som listas här i dina CSP-vitlistor.
keywords: ID-tjänst
title: Skyddsprofiler för innehåll och Experience Cloud Identity Service
exl-id: e35c6809-764e-4c3e-9139-88bb92e82338
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Skyddsprofiler för innehåll och identitetstjänsten Experience Cloud {#content-security-policies-and-the-experience-cloud-id-service}

En CSP (Content Security Policy) är en HTTP-rubrik och säkerhetsfunktion som ger webbläsarna kontroll över vilken typ av resurser som läses in på en webbsida. Granska det här avsnittet om du använder ID-tjänsten och har strikta CSP:er som använder vitlistor för att ta emot resurser från betrodda domäner. Du måste lägga till de Adobe-domäner som listas här i dina CSP-vitlistor.

## CSP-granskning {#section-5fde5c00a678455c914b8307a8caab82}

CSP använder HTTP-huvudet `Content-Security-Policy` för att styra vilken typ av resurser en webbläsare accepterar eller läser in på en sida. Med en CSP kan du förhindra följande:

* JavaScript-filer läses in om källan är okänd eller inte ingår i en vitlista.
* Serveröverskridande skriptattacker (XXS).
* Datainmatningsattacker.
* Anfall av webbplatsdefacement.
* Distribution av skadlig kod.

Användningen av CSP är vanlig och väl underbyggd. Syftet med den här dokumentationen är inte att förklara CSP i detalj (se relaterade informationslänkar nedan för mer information). Det viktiga är att du förstår vilka Adobe-domännamn du ska lägga till i en CSP om du använder dessa och har strikta säkerhetsregler. Genom att lägga till dessa domäner kan besökarwebbläsare som har åtkomst till din webbplats göra de viktiga anropen till de Experience Cloud-resurser som du använder.

## Experience Cloud-domäner för vitlistning {#section-30693e9a96834edfbf04de9e698cf2aa}

Lägg till dessa domännamn eller URL:er i din CSP för varje listlösning eller tjänst som du använder i Experience Cloud.

<table id="table_EC9FC999A62D4B7A830CE73B0AB9EF3C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Experience Cloud-lösning eller -tjänst </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>AppMeasurement</b> </p> </td> 
   <td colname="col2"> <p>Ändra din CSP så att den innehåller följande: </p> <p> 
     <ul id="ul_7522AE83A03A4115A84DF5B32D6DD79B"> 
      <li id="li_AB1EC161FB154BEDA1BEFE76C8A38A90"> <span class="codeph"> *.2o7.net</span> </li> 
      <li id="li_4B12A283716746949201528CD6AF529E"> <span class="codeph"> *.omtrdc.net</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Målgrupp</b> </p> </td> 
   <td colname="col2"> <p>Ändra din CSP så att den inkluderar <span class="codeph"> *.tt.omtrdc.net</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Experience Cloud ID-tjänst och Audience Manager</b> </p> </td> 
   <td colname="col2"> <p>Ändra din CSP så att domänerna nedan inkluderas.</p> 
   <p><ul>
   <li>connect-src 'self' <code>https://*.demdex.net https://cm.everesttech.net https://assets.adobedtm.com;</code></li>
   <li>img-src 'self' <code>https://*.demdex.net https://cm.everesttech.net https://assets.adobedtm.com;</code></li>
   <li>script-src 'self' <code>https://*.demdex.net https://cm.everesttech.net https://assets.adobedtm.com;</code></li>
   <li>frame-src 'self' <code>https://*.demdex.net;</code></li>
   <li>Om du använder Adobe Launch för att distribuera taggar måste du också lägga till <code>https://assets.adobedtm.com</code> i listan med domäner.</li></ul></p> <p>Anrop till domänen <span class="codeph"> demdex.net</span> används för att generera <a href="../introduction/cookies.md" format="dita" scope="local">-cookies och Experience Cloud Identity Service</a> och för ID-synk. Se även <a href="https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html" format="https" scope="external"> Förstå anrop till Demdex-domänen</a>. </p> </td> </tr> 
 <tr>
 <td colname="col1"> <p> <b>Activity Map plugin</b> </p> </td> 
 <td colname="col2"> <p>Ändra din CSP så att den inkluderar *.adobe.com. **Obs**: Om du redan hade Activity Map installerat före januari 2020 kommer webbläsaren fortfarande att se en första begäran till *.omniture.com, men den kommer att omdirigeras till *.adobe.com. </p></td> 
 </tr>
 <tr>
 <td colname="col1"> <p> <b>Advertising Analytics</b> </p> </td> 
 <td colname="col2"> <p>Om du har kontroller för frågesträngsparametrar måste du se till att vitlista parametrarna "s_kwcid" och "ef_id". Tekniskt sett använder Advertising Analytics endast "s_kwcid", men om du hämtar Ad Cloud Search eller DSP använder det också "ef_id". Dessa frågesträngsparametrar är alfanumeriska. Parametern "s_kwcid" använder "!" och parametern "ef_id" använder tecknet ":". Om du blockerar "!" i URL:en måste du vitlista den också.</p></td> 
 </tr>
 </tbody> 
</table>

>[!MORELIKETHIS]
>
>* [Referens för skyddsprofil för innehåll](https://content-security-policy.com/)
>* [MDN: Skyddsprofil för innehåll](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
>* [Wikipedia: Skyddsprofil för innehåll](https://en.wikipedia.org/wiki/Content_Security_Policy)

