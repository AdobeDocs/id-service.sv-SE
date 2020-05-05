---
description: Ändra standarddomännamnet som används av anrop till Experience Cloud Identity Service till ditt eget underdomännamn med dessa konfigurationer.
keywords: ID Service
seo-description: Ändra standarddomännamnet som används av anrop till Experience Cloud Identity Service till ditt eget underdomännamn med dessa konfigurationer.
seo-title: auditionManagerServer och auditionManagerServerSecure
title: auditionManagerServer och auditionManagerServerSecure
uuid: e21cacbf-5151-4d34-b0f7-9e90275f4c7c
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# auditionManagerServer och auditionManagerServerSecure{#audiencemanagerserver-and-audiencemanagerserversecure}

Ändra standarddomännamnet som används av anrop till Experience Cloud Identity Service till ditt eget underdomännamn med dessa konfigurationer.

**Syntax:**

* ` audienceManagerServer: " *`ditt underdomännamn`*.demdex.net"`
* ` audienceManagerServerSecure: " *`ditt underdomännamn`*.demdex.net"`

**Syfte**

Vanligtvis gör ID- [!DNL Experience Cloud] tjänsten anrop till [!DNL Adobe] på `dpm.demdex.net`. Ibland kanske du inte vill ringa anrop till den här destinationen eftersom den ser för generisk ut eller &quot;från tredje part&quot;. Om du vill att ID-tjänstsamtalet ska se mer ut som ett förstahandsanrop använder du de här konfigurationerna för att lägga till ditt [!DNL Audience Manager] underdomännamn `demdex.net` enligt nedan. Mer information om `dpm.demdex.net` samtalet finns i [Förstå anrop till domänen](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/demdex-calls.html)Demdex.

**Krav**

Dessa konfigurationer kräver att du använder:

* Postens [!DNL Audience Manager] underdomännamn för ditt företag. Bekräfta eller hämta det här namnet från din konsult.
* Underdomännamnet som är associerat med ditt [!UICONTROL organisations-ID].
* *Båda* konfigurationsparametrarna med samma underdomännamn.

**Kodexempel**

Låt oss i det här exemplet säga att vi har ett mediespelarföretag som har uttryckt rättsliga farhågor när det gäller att ringa till `dpm.demdex.net`. I [!DNL Audience Manager]det här fallet är företagets underdomännamn Musik1. I följande kodexempel visas hur ID-tjänstanropet varumärkesprofileras med det här kundspecifika underdomännamnet.

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

