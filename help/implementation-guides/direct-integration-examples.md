---
description: Exemplen omfattar två vanliga användningsfall som rör direkt integrering och Experience Cloud ID (MID). MID är ett unikt, beständigt ID för webbplatsens besökare.
keywords: ID Service
seo-description: Exemplen omfattar två vanliga användningsfall som rör direkt integrering och Experience Cloud ID (MID). MID är ett unikt, beständigt ID för webbplatsens besökare.
seo-title: Användningsexempel vid direkt integration
title: Användningsexempel vid direkt integration
uuid: 6de1eb8b-4783-4545-8a64-ab6b9ef93432
translation-type: tm+mt
source-git-commit: ec67177fc6491e4c8cea835d198574c9fdb4b01f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---


# Användningsexempel vid direkt integration {#direct-integration-use-cases}

Exemplen omfattar två vanliga användningsområden som rör direkt integrering och Experience Cloud ID (ECID eller MID). Detta ID är ett unikt, beständigt ID för webbplatsbesökarna.

>[!TIP]
>
>* Granska och förstå [kodsyntaxen och variablerna](../implementation-guides/direct-integration.md#concept-4cd3206a84bb4687af0b312ae09648b9) innan du dykar upp i användningsexemplen.
>* Mer information om MID finns i [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

>



## Användningsfall 1: Jag har ett Experience Cloud-ID (MID) men vill skicka mina besökar-ID:n och ange ett autentiseringstillstånd {#section-a67d89a343754d1286d03cf08d34b806}

<table id="table_DA8840FCB51541109FE6DF20430E8924"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Element i användningsexempel </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Villkor</b> </p> </td> 
   <td colname="col2"> <p>Det här användningsexemplet förutsätter att du: </p> 
    <ul id="ul_F20231F83EE84889B78971A64E758757"> 
     <li id="li_20F3E96493724CD2BAF4B20AEE5CBF23">Ha ett MID för besökaren. Ring detta ID 1234. </li> 
     <li id="li_A358C58CC58C4FCBB7250F5ED108AA71">Lär känna besökaren med ditt eget unika ID. Ring detta ID 9876. </li> 
     <li id="li_D93CE7182EBE4927A5C7A0BF414C03BC">Vill länka MID (1234) till ditt eget unika ID (9876). </li> 
     <li id="li_4611146E56624C2AB647733487A3F046"> <i>(Valfritt)</i> Vill ange autentiseringsstatus för den här besökaren. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Åtgärder</b> </p> </td> 
   <td colname="col2"> <p>Under dessa förhållanden kan du ringa till ID-tjänsten som innehåller: </p> 
    <ul id="ul_9ECB1A65266644E89E949C57D202D5A4"> 
     <li id="li_10A6F5A9C54D44A08F4F2E405E6019E2">MID (1234). </li> 
     <li id="li_4869572B40E54C54B88A2474DAC475A8">Ditt ID för dataleverantör. Detta är ett unikt ID som tilldelats ditt företag. Ring detta ID 4444. </li> 
     <li id="li_05C8ED47488C4E289D84093127EC7B19">Ditt ID för besökaren (9876). </li> 
     <li id="li_3D1556AD18C843828A362CC604A9F76B"> <i>(Valfritt)</i> Ett status-ID som definierar autentiseringstillståndet för den här besökaren. </li> 
    </ul> <p>Och om du råkar ha någon av de andra parametrarna som listas i guiden <a href="../implementation-guides/direct-integration.md#concept-4cd3206a84bb4687af0b312ae09648b9" format="dita" scope="local"> för</a> direkt integration (t.ex.<span class="codeph"> d_blob</span> eller <span class="codeph"> dcs_region</span>osv.) Det är ok att skicka in dem också. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Lösningar och kodexempel</b> </p> </td> 
   <td colname="col2"> <p>Formatera ditt samtal till ID-tjänsten så här: </p> <p> <span class="codeph">https://dpm.demdex.net/id?d_mid=1234&amp;d_cid=4444%019876%011&amp;d_ver=2</span> </p> <p>Observera hur exempelanropet innehåller följande: </p> 
    <ul id="ul_0667FBFD8D3C46BDBD027F484691EC97"> 
     <li id="li_FAB1FAE703DB48D1A32EE72684028964">MID: <span class="codeph">d_mid=1234</span> </li> 
     <li id="li_C97B74FF444F4BB4B4A5CB1CBBE52249">MID kopplat till ditt unika ID för besökaren: <span class="codeph">d_mid=1234&amp;d_cid=4444%019876%011</span> </li> 
     <li id="li_D428DBF765234DD78DDF152C5EE8AB69">ID för autentiseringstillstånd: <span class="codeph">...d_cid=4444%019876%011</span> (tips: den sista siffran). </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Användningsfall 2: Jag har inget MID och behöver generera ett {#section-8e81291f8b684de8b88fae4002ae0029}

<table id="table_666A92693F8A413096DF6A64770C1141"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Element i användningsexempel </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Villkor</b> </p> </td> 
   <td colname="col2"> <p>Det här användningsexemplet förutsätter att du: </p> 
    <ul id="ul_BF3BD821907B46A4B2EFA63146D35722"> 
     <li id="li_E658AE0671D14558B65FDD8992F25996">Har inget MID för besökaren. </li> 
     <li id="li_28A48BB3F71C4E4297F95A2D3E10AD7B">Begär ett MID från ID-tjänsten. </li> 
     <li id="li_E2C306B9308D41E5BFE2F23EF48F5A41">Lär känna ditt <a href="../reference/requirements.md#section-a02f537129a64ffbb690d5738d360c26" format="dita" scope="local"> organisations-ID</a>. Ring 5555. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Åtgärder</b> </p> </td> 
   <td colname="col2"> <p>Under dessa förhållanden kan du ringa till den ID-tjänst som innehåller ditt organisations-ID. </p> <p>Och om du råkar ha någon av de andra parametrarna som listas i guiden <a href="../implementation-guides/direct-integration.md#concept-4cd3206a84bb4687af0b312ae09648b9" format="dita" scope="local"> för</a> direkt integration (t.ex.<span class="codeph"> d_blob</span> eller <span class="codeph"> dcs_region</span>osv.) Det är ok att skicka in dem också. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Lösningar och kodexempel</b> </p> </td> 
   <td colname="col2"> <p>Formatera ditt samtal till ID-tjänsten så här: </p> <p> <span class="codeph">https://dpm.demdex.net/id?d_orgid=5555&amp;d_ver=2</span> </p> <p>Observera hur exempelanropet innehåller ditt organisations-ID, <span class="codeph">d_orgid=5555</span>. Det returnerar ett <span class="keyword"> Experience Cloud</span> -ID för den här besökaren. </p> </td> 
  </tr> 
 </tbody> 
</table>

