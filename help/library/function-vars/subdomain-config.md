---
description: Ändra det standarddomännamn som används av anrop till Experience Cloud Identity Service till ditt eget underdomännamn med dessa konfigurationer.
keywords: ID-tjänst
title: auditionManagerServer och auditionManagerServerSecure
exl-id: b740eb5c-ac4e-46f4-ba7c-1080d8d9292d
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---

# audiensManagerServer och auditionManagerServerSecure{#audiencemanagerserver-and-audiencemanagerserversecure}

Ändra det standarddomännamn som används av anrop till Experience Cloud Identity Service till ditt eget underdomännamn med dessa konfigurationer.

**Syntax:**

* ` audienceManagerServer: " *`ditt underdomännamn`*.demdex.net"`
* ` audienceManagerServerSecure: " *`ditt underdomännamn`*.demdex.net"`

**Syfte**

Vanligtvis gör ID-tjänsten [!DNL Experience Cloud] anrop till [!DNL Adobe] på `dpm.demdex.net`. Ibland kanske du inte vill ringa anrop till den här destinationen eftersom den ser för generisk ut eller &quot;från tredje part&quot;. Om du vill att ID-tjänstanropet ska se mer ut som ett förstahandsanrop använder du de här konfigurationerna för att lägga till ditt [!DNL Audience Manager]-underdomännamn till `demdex.net` enligt nedan. Mer information om `dpm.demdex.net`-anropet finns i [Förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html).

**Krav**

Dessa konfigurationer kräver att du använder:

* Postens [!DNL Audience Manager]-underdomännamn för ditt företag. Bekräfta eller hämta det här namnet från din konsult.
* Det underdomännamn som är associerat med din [!UICONTROL Organization ID].
* *Båda* konfigurationsparametrarna med samma underdomännamn.

**Exempel på kod**

Låt oss i det här exemplet säga att vi har ett mediespelarföretag som har uttryckt juridiska betänkligheter när det gäller att ringa till `dpm.demdex.net`. I [!DNL Audience Manager] är företagets underdomännamn för posten Music1. I följande kodexempel visas hur ID-tjänstanropet varumärkesprofileras med det här kundspecifika underdomännamnet.

```
//Instantiate Visitor 
var visitor = Visitor.getInstance("Insert Experience Cloud Organization ID here",{ 
     ... 
     //Configure ID service call 
     audienceManagerServer: "Music1.demdex.net", 
     audienceManagerServerSecure: "Music1.demdex.net" 
     } 
);
```
