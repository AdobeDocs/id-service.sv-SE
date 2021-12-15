---
description: Dessa instruktioner är till för A4T-kunder med blandade server- och klientimplementeringar av Target, Analytics och ID-tjänsten. Kunder som behöver köra ID-tjänsten i en NodeJS- eller Rhino-miljö bör också granska den här informationen. Den här instansen av ID-tjänsten använder en förkortad version av kodbiblioteket VisitorAPI.js, som du hämtar och installerar från NPM (Node Package Manager). I det här avsnittet finns installationsanvisningar och andra konfigurationskrav.
keywords: ID-tjänst
title: Använda ID-tjänsten med A4T och en implementering på serversidan av Target
exl-id: 6f201378-29a1-44b7-b074-6004246fc999
source-git-commit: e171c94ccfa1f4fe9b8d909d0204adb94f20cbb6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Använda ID-tjänsten med A4T och en implementering på serversidan av Target {#using-the-id-service-with-a-t-and-a-server-side-implementation-of-target}

Dessa instruktioner är till för A4T-kunder med blandade server- och klientimplementeringar av Target, Analytics och ID-tjänsten. Kunder som behöver köra ID-tjänsten i en NodeJS- eller Rhino-miljö bör också granska den här informationen. Den här instansen av ID-tjänsten använder en förkortad version av kodbiblioteket VisitorAPI.js, som du hämtar och installerar från NPM (Node Package Manager). I det här avsnittet finns installationsanvisningar och andra konfigurationskrav.

## Introduktion {#section-ab0521ff5bbd44c592c3eaab31c1de8b}

A4T (och andra kunder) kan använda den här versionen av ID-tjänsten när de behöver:

* Återge webbsidesinnehåll på deras servrar och skicka det till en webbläsare för slutlig visning.
* Gör serversidan [!DNL Target] samtal.
* Göra klientanrop (i webbläsaren) till [!DNL Analytics].
* Synkronisera separat [!DNL Target] och [!DNL Analytics] ID:n som avgör om en besökare som ses av en lösning är samma person som den andra lösningen.

## Kodnedladdning och medföljande gränssnitt {#section-32d75561438b4c3dba8861be6557be8a}

Se [NPM-databas för ID-tjänst](https://www.npmjs.com/package/@adobe-mcid/visitor-js-server) för att hämta kodpaketet på serversidan och granska gränssnitten som ingår i den aktuella versionen.

## Arbetsflöde {#section-56b01017922046ed96536404239a272b}

Diagrammet och avsnitten nedan beskriver vad som händer och vad du behöver konfigurera i varje steg i implementeringsprocessen på serversidan.

![](assets/serverside.png)

## Steg 1: Sidan Begär {#section-c12e82633bc94e8b8a65747115d0dda8}

Aktiviteten på serversidan börjar när en besökare gör en HTTP-begäran om att läsa in en webbsida. Under det här steget tar servern emot den här begäran och söker efter [AMCV cookie](../introduction/cookies.md). AMCV-cookien innehåller besökarens [!DNL Experience Cloud] ID (MID).

## Steg 2: Generera nyttolast för ID-tjänst {#section-c86531863db24bd9a5b761c1a2e0d964}

Sedan måste du skapa en server *`payload request`* till ID-tjänsten. En nyttolastbegäran:

* Skickar AMCV-cookien till ID-tjänsten.
* Begär data som krävs av Target och Analytics i efterföljande steg som beskrivs nedan.

>[!NOTE]
>
>Den här metoden begär en enda mbox från [!DNL Target]. Om du behöver begära flera mbox i ett enda samtal, se [generateBatchPayload](https://www.npmjs.com/package/@adobe-mcid/visitor-js-server#generatebatchpayload).

Nyttolastbegäran ska se ut så här: I kodexemplet `visitor.setCustomerIDs` -funktionen är valfri. Se [Kund-ID och autentiseringstillstånd](../reference/authenticated-state.md) för mer information.

```js
//Import the ID service server package 
var Visitor = require("@adobe-mcid/visitor-js-server"); 
 
//Pass in your Organization ID to instantiate Visitor 
var visitor = new Visitor("Insert Experience Cloud ID here"); 
 
// 
<i>(Optional)</i> Set a custom customer ID 
visitor.setCustomerIDs({ 
     userid:{ 
          id:"1234", 
          authState: Visitor.AuthState.UNKNOWN //AuthState is a static property of the Visitor class 
     } 
}); 
 
//Parse the visitor's HTTP request for the AMCV cookie 
var cookies = cookie.parse(req.headers.cookie || ""); 
var cookieName = visitor.getCookieName(); // Visitor API that returns the cookie name. 
var amcvCookie = cookies[cookieName]; 
 
//Generate the payload request pass your mbox name and the AMCV cookie if present 
var visitorPayload = visitor.generatePayload({ 
     mboxName: "bottom-banner-mbox", 
     amcvCookie: amcvCookie 
});
```

ID-tjänsten returnerar nyttolasten i ett JSON-objekt som liknar följande exempel. Nyttolastdata krävs av [!DNL Target].

```js
{ 
    "marketingCloudVisitorId": "02111696918527575543455026275721941645", 
    "mboxParameters": { 
        "mboxAAMB": "abcd1234", 
        "mboxMCGLH": "9", 
        "mboxMCSDID": "56BE026543F7E211-1CC51BCAAE88F0D2", 
        "vst.userid.id": "1234567890", 
        "vst.userid.authState": 0 
    } 
}
```

Om besökaren inte har en AMCV-cookie utelämnar nyttolasten följande nyckelvärdepar:

* `marketingCloudvisitorId`
* `mboxAAMB`
* `mboxMCGLH`

## Steg 3: Lägg till nyttolast i Target-anropet {#section-62451aa70d2f44ceb9fd0dc2d4f780f7}

När servern har tagit emot nyttolastdata från ID-tjänsten måste du initiera ytterligare kod för att sammanfoga den med data som skickas till [!DNL Target]. Det sista JSON-objektet som skickas till [!DNL Target] skulle se ut ungefär så här:

```js
{ 
"mbox" : "target-global-mbox", 
"marketingCloudVisitorId":"02111696918527575543455026275721941645", 
"requestLocation" : { 
     "pageURL" : "http://www.domain.com/test/demo.html", 
     "host" : "localhost:3000" 
     }, 
"mboxParameters" : { 
     "mboxAAMB" : "abcd1234", 
     "mboxMCGLH" : "9", 
     "mboxMCSDID": "56BE026543F7E211-1CC51BCAAE88F0D2", 
     "vst.userid.id": "1234567890", 
     "vst.userid.authState": 0, 
     } 
} 
```

## Steg 4: Hämta servertillstånd för ID-tjänsten {#section-8ebfd177d42941c1893bfdde6e514280}

Serverstatusdata innehåller information om arbete som har utförts på servern. Tjänstkoden för klient-ID kräver den här informationen. Kunder som har implementerat ID-tjänsten via [!DNL Dynamic Tag Manager] (DTM) kan konfigurera DTM så att servertillståndsdata skickas via det verktyget. Om du har konfigurerat ID-tjänsten via en icke-standardprocess måste du returnera servertillståndet med din egen kod. Klientsidans ID-tjänst och [!DNL Analytics] koden skickar lägesdata till Adobe när sidan läses in.

**Hämta servertillstånd via DTM**

Om du har implementerat ID-tjänsten med DTM måste du lägga till kod på sidan och ange ett namn/värde-par i DTM-inställningarna.

**Sidkod**

Lägg till den här koden i `<head>` -tagg på din HTML-sida:

```js
//Get server state 
var serverState = visitor.getState(); 
 
Response.send(" 
... 
<head> 
     <script> 
          //Add 'serverState' as a stringified JSON global variable. 
          "var serverState = "+ JSON.stringify(serverState) +";  
     </script> 
     <script src = "DTM script (satellite JS)"> 
     </script> 
</head> 
...
```

**DTM-inställningar**

Lägg till dessa som namnvärdespar i **[!UICONTROL General > Settings]** i din ID-tjänstinstans:

* **[!UICONTROL Name:]** serverState
* **[!UICONTROL Value:]** %serverState%

   >[!IMPORTANT]
   >
   >Värdenamnet måste matcha variabelnamnet som du angav för `serverState` i sidkoden.

Dina konfigurerade inställningar bör se ut så här:

![](assets/server_side_dtm.png)

**Hämta servertillstånd utan DTM**

Om du har en icke-standardimplementering av ID-tjänsten måste du konfigurera den här koden så att den körs på servern medan den sammanställer den begärda sidan:

```js
//Get server state 
var serverState = visitor.getState(); 
 
Response.send(" 
... 
<head> 
     <script src="VisitorAPI.js"></script> 
     <script> 
          var visitor = Visitor.getInstance(orgID, { 
          serverState: serverState  
          ... 
     </script> 
</head> 
...
```

## Steg 5: Servera en sida och returnera Experience Cloud data {#section-4b5631a0d75a41febd6f43f8c214c263}

Nu skickar webbservern sidinnehåll till besökarens webbläsare. Från och med nu gör webbläsaren (inte servern) alla återstående ID-tjänster och [!DNL Analytics] samtal. I webbläsaren:

* ID-tjänsten tar emot tillståndsdata från servern och skickar SDID:t till AppMeasurement.
* AppMeasurement skickar data om sidträffen till [!DNL Analytics], inklusive SDID.
* [!DNL Analytics] och [!DNL Target] jämför SDID för den här besökaren. Med ett identiskt SDID, [!DNL Target] och [!DNL Analytics] sammanfoga anropet på serversidan och samtalet på klientsidan. Nu ser båda lösningarna besökaren som samma person.

>[!MORELIKETHIS]
>
>* [Tjänstpaket för serverkod-ID från nodpakethanteraren](https://www.npmjs.com/package/@adobe-mcid/visitor-js-server)

