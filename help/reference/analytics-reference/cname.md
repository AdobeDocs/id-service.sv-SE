---
description: 'null'
keywords: order of operations;ID Service
seo-description: 'null'
seo-title: CNAME för datainsamling och spårning mellan domäner
title: CNAME för datainsamling och spårning mellan domäner
uuid: ba42c822-b677-4139-b1ed-4d98d3320fd0
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# CNAME för datainsamling och spårning mellan domäner{#data-collection-cnames-and-cross-domain-tracking}

Om du har en huvudwebbplats där kunder kan identifieras innan de besöker andra domäner kan en CNAME aktivera spårning av korsdomäner i webbläsare som inte accepterar cookies från tredje part (som Safari).

I webbläsare som accepterar cookies från tredje part anges en cookie av datainsamlingsservrarna under begäran om ett besökar-ID. Denna cookie gör det möjligt för besökar-ID-tjänsten att returnera samma Experience Cloud-besökar-ID på alla domäner som har konfigurerats med samma Experience Cloud Org-ID.

I webbläsare som avvisar cookies från tredje part tilldelas varje domän ett nytt besökar-ID för Experience Cloud.

Med cookie-filen demdex.net kan besökar-ID-tjänsten tillhandahålla samma nivå av korsdomänsspårning som s_vi-cookien i Analytics, där cookien accepteras i vissa webbläsare och används i olika domäner, men avvisas av andra webbläsare.

## CNAME för datainsamling {#section-48fd186d376a48079769d12c4bd9f317}

När Analytics-cookien angavs av datainsamlingsservern har många kunder konfigurerat datainsamlingsserverns CNAME-poster som en del av en [förstahandsimplementering](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) för att undvika problem med webbläsare som avvisar cookies från tredje part. Den här processen konfigurerar din datainsamlingsserverdomän så att den matchar din webbplatsdomän så att cookien för besökar-ID anges som en cookie för en första part.

Eftersom besökar-ID-tjänsten ställer in besökarens cookie direkt på domänen för den aktuella webbplatsen med JavaScript behövs inte längre den här konfigurationen för att ställa in cookies från första part.

Kunder som har en enda webbegenskap (en enda domän) kan migrera bort från CNAME för datainsamling och använda sitt standardvärdnamn för datainsamling i stället (antingen `omtrdc.net` eller `2o7.net`).

Det finns dock en ytterligare fördel med att använda en CNAME för datainsamling som gör att du kan spåra besökare mellan en huvudlandningsdomän och andra domäner i webbläsare som inte accepterar cookies från tredje part. Kunder som har flera webbegenskaper (flera domäner) kan ha nytta av att underhålla en CNAME för datainsamling. I följande avsnitt förklaras hur spårning av besökare mellan domäner fungerar.

## Så här aktiverar CNAME-filer spårning mellan domäner {#section-78925af798e24917b9abed79de290ad9}

På grund av hur cookies från första part kan användas i ett tredjepartssammanhang i Apple Safari och vissa andra webbläsare kan du med en CNAME spåra kunder mellan en primär domän och ytterligare domäner som använde samma spårningsserver.

Du har till exempel en primär plats på `mymainsite.com`. Du konfigurerade CNAME-posten så att den pekar på din säkra datainsamlingsserver: `smetrics.mymainsite.com`.

När en användare besöker webbplatsen `mymainsite.com`anges ID-tjänstens cookie av datainsamlingsservern. Detta är tillåtet eftersom domänen för datainsamlingsservern matchar webbplatsens domän och är vad som kallas att använda en cookie i en *förstahandskontext*, eller bara en *förstapartscookie*.

Om du även använder samma datainsamlingsserver på andra webbplatser (till exempel `myothersiteA.com`och `myothersiteB.com`) och en besökare senare besöker dessa webbplatser, skickas den cookie som angavs under besöket till `mymainsite.com` i HTTPS-begäran till datainsamlingsservern (kom ihåg att webbläsare skickar alla cookies för en domän med alla HTTPS-begäranden till den domänen, även om domänen inte matchar domänen för den aktuella webbplatsen). Detta kallas att använda en cookie i ett *tredjepartskontext*, eller bara en cookie *från en* tredje part, och gör att samma besökar-ID kan användas på dessa andra domäner. Observera att webbläsare hanterar cookies i tredjepartskontexter på ett annat sätt än cookies från första part.

*Obs! Safari blockerar alla cookies i tredjepartskontexten oavsett hur de ställs in.*

Därför bör din samlingsdomän vara en domän som folk vanligtvis besöker för att en besökare ska kunna identifieras över domäner. Om det inte finns någon *gemensam* domän att använda för datainsamlingsdomänen finns det ingen korsdomänfördel med att underhålla en CNAME för datainsamlingsdomänen. Om den huvudsakliga startwebbplatsen inte besöks först identifieras besökare olika på den sekundära platsen och huvudwebbplatsen.

## Aktivera CNAME-stöd med Experience Cloud Identity Service {#section-25d4feb686d944e3a877d7aad8dbdf9a}

Stödet för datainsamlingsservern CNAME aktiveras genom att `visitor.marketingCloudServerSecure` variablerna anges.
