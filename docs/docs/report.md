# Individuell Examination – ITSX26
**Valt spår:** Case A – AI-phishing mot en kommun  
**Målnivå:** G (30 poäng)  

---

## 1. Executive summary
Denna rapport analyserar en misstänkt phishing-incident riktad mot en kommunal förvaltning. Flera medarbetare har tagit emot e-postmeddelanden som ser ut att komma från den interna IT-supporten. I meddelandena uppmanas mottagarna att klicka på en länk för att behålla åtkomsten till ett internt system. En medarbetare har klickat på länken men uppger att inga inloggningsuppgifter har lämnats. Det finns i nuläget inga bekräftade tecken på intrång eller skada på organisationens system. Det är ännu inte fastställt om meddelandena har skapats med hjälp av AI.

För att hantera risken och förhindra framtida incidenter föreslås tre prioriterade och proportionerliga åtgärder baserade på ramverket CIS Controls v8.1: införande av multifaktorautentisering (CIS 6), centraliserad loggning (CIS 8) samt riktad utbildning och verifieringsrutiner för personalen (CIS 14). Med dessa åtgärder stärkts säkerheten i kommunen utan att det skapar hinder i den dagliga verksamheten.

---

## 2. Fakta, antaganden och scope

### Givna fakta
* E-postmeddelanden har skickats till flera medarbetare i kommunen.
* Avsändarnamnet liknar den interna IT-supportens namn.
* En mottagare har klickat på länken i meddelandet.
* Inga autentiseringsuppgifter har bekräftats lämnade.
* Det finns ännu ingen bekräftad incident eller konstaterat intrång.
* Användning av AI är en möjlighet, men inte ett fastställt faktum.

### Antaganden
* Länken ledde till en extern webbplats utformad för att samla in inloggningsuppgifter.
* Kommunens e-postfilter saknar tillräckligt skydd mot avsändarförfalskning.
* Medarbetaren kan ha lämnat uppgifter utan att vara helt medveten om det.

### Frågor som behöver verifieras
* Kördes några skadliga skript eller laddades något ned till klientdatorn när länken öppnades?
* Finns det avvikande inloggningsförsök i loggarna för användarens konto?
* Hur många medarbetare har totalt tagit emot meddelandet i e-postservern?

---

## 3. Tillgångar och händelsekedja

### Identifierade tillgångar
1. **Kommunala användarkonton:** Medarbetarnas identiteter i Active Directory eller Entra ID.
2. **Internt kommunalt system:** Systemet som e-postmeddelandet påstods gälla.
3. **Klientdator:** Medarbetarens arbetsdator som användes för att klicka på länken.
4. **E-postinfrastruktur:** Kommunens e-postserver och mailgateway.

### Händelsekedja
1. **Leverans:** Angriparen skickar förfalskade e-postmeddelanden till flera anställda.
2. **Mottagande:** E-postmeddelandena passerar e-postfiltret och når medarbetarnas inkorgar.
3. **Interaktion:** En medarbetare öppnar mejlet och klickar på länken.
4. **Anslutning:** Webbläsaren ansluter till den externa webbplatsen.
5. **Rapportering:** Händelsen uppmärksammas och IT-avdelningen påbörjar sin utredning.

---

## 4. CIA och enkel riskbedömning

### Casespecifik påverkan
* **Confidentiality (Konfidentialitet) – HÖG RISK:** Om inloggningsuppgifter har läckt kan obehöriga få tillgång till känsliga kommunala handlingar eller personuppgifter.
* **Integrity (Integritet) – MEDEL RISK:** Om ett konto tas över kan en angripare ändra eller radera information i det interna systemet.
* **Availability (Tillgänglighet) – LÅG RISK:** Ingen direkt påverkan i dagsläget, men ett framtida angrepp via ett övertaget konto skulle kunna störa drift och tillgänglighet.

### Kvalitativ riskbedömning
* **Sannolikhet:** Medel. Phishing är en mycket vanlig angreppsmetod och det är lätt för medarbetare att råka klicka.
* **Konsekvens:** Hög. Ett intrång i en kommunal förvaltning kan leda till läckta personuppgifter och brutna sekretesskrav.
* **Sammanvägd risk:** HÖG. Det finns ett tydligt behov av förebyggande och kontrollera åtgärder.

---

## 5. CIS-mappning

| CIS Control | Fokus i caset | Konkret åtgärd | Verifiering |
| :--- | :--- | :--- | :--- |
| **CIS 6: Access Control Management** | Stärka åtkomstkontroll och begränsa konsekvenser vid läckta uppgifter. | Införa tvingande multifaktorautentisering (MFA) för alla användare. | Kontrollera i systemet att inga konton kan logga in utifrån utan MFA. |
| **CIS 8: Audit Log Management** | Säkra loggning för att upptäcka och utreda misstänkta händelser. | Centralisera loggar från e-postserver, webbfilter och inloggningssystem. | Genomföra en sökkontroll i loggsystemet efter den klickade adressen. |
| **CIS 14: Security Awareness and Skills Training** | Minska risken att medarbetare luras av bluffmejl. | Genomföra utbildning i phishing och införa en knapp för att rapportera misstänkta mejl. | Följa upp hur många som slutfört utbildningen och testa med en övning. |

---

## 6. Prioriterade åtgärder

1. **Aktivera multifaktorautentisering (MFA) på alla konton (CIS 6):** Det skyddar kontot även om lösenordet skulle ha hamnat i fel händer.
2. **Konfigurera e-postsäkerhet med SPF, DKIM och DMARC (CIS 8 / E-postsäkerhet):** Gör det svårare för angripare att skicka mejl som ser ut att komma från kommunens egen IT-support.
3. **Etablera rutin för incidentrapportering och utbilda personalen (CIS 14):** Hjälper medarbetarna att upptäcka och rapportera misstänkta mejl snabbt.

---

## 7. Teknisk koppling

För att utreda vad som hände när medarbetaren klickade på länken används logganalys. Genom att granska kommunens webbproxy och DNS-loggar går det att se vilken IP-adress och webbadress datorn anslöt till vid tidpunkten för klicket.

Därefter kontrolleras inloggningsloggarna i kommunens identitetssystem (t.ex. Entra ID eller Active Directory) för att se om det finns några lyckade inloggningar från okända IP-adresser eller från utlandet kort efter händelsen.

---

## 8. Slutsats

Incidenten visar hur viktig kombinationen av tekniskt skydd och mänsklig vaksamhet är. Eftersom inga uppgifter bekräftats läckta är den omedelbara skadan låg. Genom att införa MFA, förbättra e-postskyddet och utbilda personalen får kommunen ett bra och rimligt skydd framöver.

**Kvarvarande osäkerhet:** Det går inte att helt utesluta att datorn påverkades när länken öppnades förrän en teknisk skanning av datorn har genomförts.
