---
description: Experience Cloud Identity Service aktiverar det gemensamma identifieringsramverket för Experience Cloud program och tjänster. Det fungerar genom att tilldela ett unikt, beständigt ID som kallas Experience Cloud-ID (ECID) till en besökare.
keywords: ID-tjänst; identitetstjänst; Experience Cloud-identitetstjänst
title: Experience Cloud Identity Service
exl-id: fe1368db-06ca-4c79-b655-b7064e316d74
source-git-commit: f7c25f5ebd0690c56c081422949eb34f1f277ae1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 2%

---

# Adobe Experience Cloud Identity Service {#experience-cloud-id-service}

Experience Cloud Identity Service aktiverar det gemensamma identifieringsramverket för Experience Cloud program och tjänster. Det fungerar genom att tilldela ett unikt, beständigt ID som kallas Experience Cloud-ID (ECID) till en besökare.

## Förstå de viktigaste entiteterna i identiteten

För att få en bättre förståelse för hur Adobe kan hjälpa till att identifiera besökare unikt och lösa identitetsinformation kan du göra följande:

* **Experience Cloud-identitetstjänsten**: Experience Cloud-identitetstjänsten **ansvarar för att ställa in Experience Cloud ID (ECID)**. Mer information finns i översikten över [Experience Cloud-identitetstjänsten](./introduction/overview.md).
* **Experience Cloud ID (ECID)**: ECID är ett delat ID-namnområde som används i Adobe Experience Platform- och Adobe Experience Cloud-program för att identifiera personer och enheter. Mer information om ECID finns i [ECID-översikten](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html).
* **Experience Platform Identity Service**: Med identitetstjänsten Experience Platform får du en heltäckande bild av dina kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system. Mer information finns i [Översikt över identitetstjänsten i Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv).

<!-- The Adobe Experience Cloud Identity Service provides a universal, persistent ID that identifies your visitors across all the solutions in the Experience Cloud. It can replace ID generation code for Experience Cloud solutions and services. -->

<table id="table_5E612F746A704FE095B809A013EE977F" class="simpletable"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Komma igång</b> </p> <p> 
     <ul id="ul_D5EC6A54A03F4AB595B588116A7C1296"> 
      <li id="li_845F6DE25A1241439BCDCBC00459D7EB"> <a href="introduction/overview.md" format="dita" scope="local"> Översikt </a> </li> 
      <li id="li_47F399E1D4AF4F08BD647DF01A423BA7"> <a href="reference/requirements.md" format="dita" scope="local"> Krav för identitetstjänsten Experience Cloud </a> </li> 
      <li id="li_CBEEE79B45644F28A52B58DDF23DAD4F"> <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en" format="html" scope="external"> Standardimplementering med plattformstaggar </a> </li> 
     </ul> </p> <p><b>JavaScript-bibliotek med Experience Cloud </b> </p> <p>JavaScript för identitetstjänsten Experience Cloud finns på: <a href="https://github.com/Adobe-Marketing-Cloud/id-service/releases" format="https" scope="external"> https://github.com/Adobe-Marketing-Cloud/id-service/releases</a> </p> <p> <b>Nya eller Aktuella objekt</b> </p> <p> 
     <ul id="ul_B0A25B6827734D55BB1E20D12334AC21"> 
      <li id="li_A66924F4948F4A5ABA545A89A28A6F6A"><a href="implementation-guides/opt-in-service/optin-overview.md#concept-f9b5db0d27a245fbadd3e19162319360" format="dita" scope="local"> Anmälningstjänst </a> </li> 
      <li id="li_92D49CB788AD478EA74BCF5328CB9A14"> <a href="library/get-set/getvisitorvalues.md#reference-b8c9e17c170c4291829a792df46ce279" format="dita" scope="local"> getVisitorValues </a> </li> 
      <li id="li_9E512C6DD15C46C3ABD06ACD60D97E4A"> <a href="faq-intro/faq-intro.md" format="dita" scope="local"> Vanliga frågor </a> </li> 
      <li id="li_7744A4898EA542B9BF009D2066810050"> <a href="library/function-vars/idsyncontainerid.md#reference-5cfbed2240fa4def90f535f017a36015" format="dita" scope="local"> idSyncContainerID </a> </li> 
     </ul> </p> 
     <!-- 
     <p> <b>Announcements:</b> </p> 
     <p> <p>Important:  ID service support for Internet Explorer 6, 7, and 8 is deprecated and will be discontinued in a future release. </p> </p> 
     --> </td> 
   <td colname="col2"> <p> <b>Versionsinformation</b> </p> <p><b>Version 4.4</b> 17 juli 2019 innehåller stöd för hash-algoritmen <a href="reference/hashing-support.md" format="dita" scope="local"> SHA-256 </a> som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n.</p><p><b>Version 4.0</b> 12 februari 2019 innehåller den <a href="implementation-guides/opt-in-service/optin-overview.md#concept-f9b5db0d27a245fbadd3e19162319360" format="dita" scope="local"> anmälningstjänst </a> som används för att identifiera om du kan placera en cookie på en användares enhet eller webbläsare när du besöker din webbplats. </p> <p> 
     <ul id="ul_4F06F170F214492780C7D25A069F799F"> 
      <li id="li_45A7CD556FE44F4DAB035C736A058F36"> I den senaste <a href="https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=en" format="https" scope="external"> versionsinformationen för Experience Cloud </a> finns information om nya funktioner och korrigeringar. </li> 
      <li id="li_10CC4FBFEFC947CA9AD15F52D9715257">Mer information om äldre versioner finns i avsnittet <a href="https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=en" format="html" scope="external"> Tidigare versionsinformation</a>. </li> 
     </ul> </p> <p> <b>Resurser för Experience Cloud</b> </p> <p> 
     <ul id="ul_E30EC96BDC624B5591F0470D430B7F41"> 
      <li id="li_F3A5CCFAE0F247CEB41A03CA8E03106B"> <a href="http://www.adobe.com/privacy.html" format="http" scope="external"> Adobe Privacy Center</a> </li> 
      <li id="li_A54C1EB170EA4B8FA6A81B90AB0C39DD"> <a href="https://experienceleague.adobe.com/docs/home.html?lang=en" scope="external" format="http"> Adobe Experience Cloud</a> </li> 
      <li id="li_1938F7044F544481A6CC0F45CC22B80A"> <a href="http://helpx.adobe.com/learning.html?promoid=KAUDK" scope="external" format="http"> Adobe-utbildning och Tutorials </a> </li> 
      <li id="li_C71459E0D1464C05B8B9387C43541F17"> <a href="https://helpx.adobe.com/se/support/experience-cloud.html" scope="external" format="https"> Produktdokumentation - startsida</a> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
