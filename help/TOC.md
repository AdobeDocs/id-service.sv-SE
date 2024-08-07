---
audience: end-user
user-guide-title: Hjälp med Experience Cloud Identity Service
breadcrumb-title: Användarhandbok om Identity Service
user-guide-description: Adobe Experience Cloud Identity Service är ett universellt, beständigt ID som identifierar besökarna i alla lösningar i Experience Cloud. Den ersätter tidigare ID-genereringskod för lösningar och tjänster från Experience Cloud.
user-guide-url: /content/help/en/id-service/using/home.html
source-git-commit: 6ef86bdb7bc10e24dbd3efe2481cb2e6e6c270fb
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 13%

---


# Hjälp med Experience Cloud Identity Service {#using}

+ [Hjälp för identitetstjänst](home.md)
+ Översikt {#intro}
   + [Översikt](introduction/overview.md)
   + [Om ID-tjänsten](introduction/about-id-service.md)
   + [Cookies och ID-tjänsten](introduction/cookies.md)
   + [Hur ID-tjänsten begär och ställer in ID:n](introduction/id-request.md)
   + [Synkroniserings- och matchningsfrekvenser](introduction/match-rates.md)
+ Implementering {#implementation}
   + [Implementeringsmetoder](implementation-guides/implementation-methods.md)
   + [Implementeringsguider](implementation-guides/implementation-guides.md)
   + [Implementera med Experience Platform-taggar](implementation-guides/ecid-implement-with-launch.md)
   + [Implementering för Analytics](implementation-guides/setup-analytics.md)
   + [Implementera för mål](implementation-guides/setup-target.md)
   + [Implementering för Analytics och Audience Manager](implementation-guides/setup-aam-analytics.md)
   + [Implementering för Analytics, Audience Manager och Target](implementation-guides/setup-aam-analytics-target.md)
   + [Använda ID-tjänsten med A4T och en implementering på serversidan av Target](implementation-guides/ecid-a4t-target.md)
   + [Direktintegrering med ID-tjänsten](implementation-guides/direct-integration.md)
   + [Användningsexempel för direktintegrering](implementation-guides/direct-integration-examples.md)
   + [Testa och verifiera ID-tjänsten](implementation-guides/test-verify.md)
   + Anmälningstjänst {#opt-in-service}
      + [Översikt över anmälningstjänsten](implementation-guides/opt-in-service/optin-overview.md)
      + [Konfigurera anmälningstjänst](implementation-guides/opt-in-service/getting-started.md)
      + [Validerar anmälningstjänst](implementation-guides/opt-in-service/testing-optin-and-iab-plugin.md)
      + [Konfigurera deltagande med Experience Platform Launch](implementation-guides/opt-in-service/launch.md)
      + [Konfigurera deltagande med DTM](implementation-guides/opt-in-service/optin-dtm.md)
      + [Åtgärder för kontroll av Experience Cloud baserat på användares samtycke](implementation-guides/opt-in-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.md)
      + [Användningsexempel](implementation-guides/opt-in-service/use-cases.md)
      + [Anmälningsreferens](implementation-guides/opt-in-service/api.md)
      + [Använda Opt-in-tjänster med IAB Framework](implementation-guides/opt-in-service/iab.md)
+ ID-tjänst-API {#id-service-api}
   + [API-översikt för ID-tjänst](library/library.md)
   + Konfiguration {#configurations}
      + [Konfigurationer - översikt](library/function-vars/function-vars.md)
      + [auditionManagerServer och auditionManagerServerSecure](library/function-vars/subdomain-config.md)
      + [cookieDomain](library/function-vars/cookiedomain.md)
      + [cookieLifetime](library/function-vars/cookielifetime.md)
      + [disableIdSyncs](library/function-vars/disableidsync.md)
      + [disableThirdPartyCall](library/function-vars/disablethirdpartycalls.md)
      + [disableThirdPartyCookies](library/function-vars/disable-cookies.md)
      + [idSyncAttachIframeOnWindowLoad](library/function-vars/idsyncattachiframeonwindowload.md)
      + [idSyncContainerID](library/function-vars/idsyncontainerid.md)
      + [idSyncSSLUseAkamai](library/function-vars/idsyncssluseakamai.md)
      + [loadTimeout](library/function-vars/loadtimeout.md)
      + [overwriteCrossDomainMCIDAndAID](library/function-vars/overwrite-visitor-id.md)
      + [resetBeforeVersion](library/function-vars/resetbeforeversion.md)
      + [sdidParamExpiry](library/function-vars/sdidparamexpiry.md)
      + [Säkra konfigurationer och samma webbplats](library/function-vars/secure-samesite-config.md)
      + [secureCookie](library/function-vars/securecookie.md)
      + [useCORSOnly](library/function-vars/use-cors-only.md)
      + [whitelistParentDomain och whitelistIframeDomains](library/function-vars/whitelistdomain.md)
   + Metoder {#methods}
      + [Metoder](library/get-set/get-set.md)
      + [appendSupplementalDataIDTo](library/get-set/appendsupplementaldataidto.md)
      + [appendVisitorIDsTo (spårning mellan domäner)](library/get-set/appendvisitorid.md)
      + [callTimeOut-metoder](library/get-set/timeout-functions.md)
      + [ID-synkronisering efter URL eller Data Source](library/get-set/idsync.md)
      + [getInstance](library/get-set/getinstance.md)
      + [getAnalyticsVisitorID](library/get-set/getanalyticsvisitorid.md)
      + [getCustomerIDs](library/get-set/getcustomerids.md)
      + [setCustomerIDs](library/get-set/setcustomerids.md)
      + [getMarketingCloudVisitorID](library/get-set/getmcvid.md)
      + [getLocationHint](library/get-set/getlocationhint.md)
      + [getVisitorValues](library/get-set/getvisitorvalues.md)
      + [isClientSideMarketingCloudVisitorID](library/get-set/client-side-id.md)
      + [resetState](library/get-set/resetstate.md)
+ Referens {#reference}
   + [Referensöversikt](reference/reference.md)
   + Analysreferens {#analytics-reference}
      + [Analysreferensöversikt](reference/analytics-reference/analytics-reference.md)
      + [CNAME-implementering - översikt](reference/analytics-reference/cname.md)
      + [Ställa in analyser och Experience Cloud-ID](reference/analytics-reference/analytics-ids.md)
      + [Åtgärdsordning för analys-ID:n](reference/analytics-reference/analytics-order-of-operations.md)
      + [Beslutspunkter för migrering av ID-tjänst](reference/analytics-reference/migration-decisions.md)
      + [Migreringsscenarier för ID-tjänst](reference/analytics-reference/migration-scenarios.md)
      + [Analys- och identitetsförfrågningar](reference/analytics-reference/legacy-analytics.md)
      + [Implementering på serversidan blandat med JavaScript](reference/analytics-reference/server-side.md)
      + [Giltighetsperioden för ID-tjänsten](reference/analytics-reference/grace-period.md)
   + [Google Chrome SameSite-etikettändringar](reference/chrome-samesite-labelling.md)
   + [Skyddsprofiler för innehåll och ID-tjänsten](reference/csp.md)
   + [Stöd för COPPA i ID-tjänsten](reference/coppa.md)
   + [CORS-stöd i ID-tjänsten](reference/cors.md)
   + [Kund-ID och autentiseringstillstånd](reference/authenticated-state.md)
   + [ECID-biblioteksmetoder i en Safari ITP-värld](reference/ecid-library-methods.md)
   + [Identifiera unika besökare](reference/unique-vis-method.md)
   + [Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten](reference/regions.md)
   + [Krav för ID-tjänsten](reference/requirements.md)
   + [Videopulsslag och ID-tjänst](reference/heartbeat.md)
   + [Data Workbench och ID-tjänst](reference/dwb.md)
   + [SHA256 Hash-stöd för setCustomerIDs](reference/hashing-support.md)
+ Vanliga frågor {#faqs}
   + [Frågor och svar - översikt](faq-intro/faq-intro.md)
   + [Vanliga frågor om ID-tjänster](faq-intro/faq.md)
   + [Vanliga frågor om analys och ID-tjänster](faq-intro/analytics-faq.md)
   + [Frågor och svar för andra Experience Cloud-lösningar](faq-intro/other-faq.md)
+ Versionsinformation för ID-tjänsten {#release-notes}
   + [Versionsinformation 2022](release-notes/notes-2022.md)
   + [Versionsinformation 2021](release-notes/notes-2021.md)
   + [Versionsinformation 2020](release-notes/notes-2020.md)
   + [Versionsinformation 2019](release-notes/notes-2019.md)
   + [Versionsinformation 2018](release-notes/notes-2018.md)
   + [Versionsinformation 2017](release-notes/notes-2017.md)
   + [Versionsinformation 2016](release-notes/notes-2016.md)
   + [Versionsinformation 2015](release-notes/notes-2015.md)
+ [Analystestet är dolt från innehållsförteckningen](analytics-test-file-hidetoc.md)
