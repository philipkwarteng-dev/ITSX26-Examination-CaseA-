# Individuell Examination: Case A – AI-phishing mot en kommun

**Författare:** Philip Kwarteng  
**Kurs:** ITSX26 - IT- och cybersäkerhet (Kursvecka 6, vecka 40)  
**Nivå:** Godkänt (G)  
**Datum:** 2026-10-15  

---

## 1. Executive Summary (Svenska)
Denna rapport analyserar en misstänkt phishing-incident riktad mot en kommunal förvaltning. Ett flertal medarbetare har tagit emot e-postmeddelanden som utger sig för att komma från intern IT-support, med uppmaning att logga in på en extern länk för att behålla åtkomsten till ett internt system. En medarbetare har klickat på länken men uppger att inga inloggningsuppgifter har lämnats. 

För närvarande finns det inga bekräftade tecken på intrång eller komprometterade konton. Användningen av generativ AI för att skapa meddelandena är en hypotetisk möjlighet men saknar teknisk bekräftelse. Risken bedöms för närvarande som Medium på grund av den potentiella konsekvensen om inloggningsuppgifter läcks.

För att minimera risken och öka spårbarheten rekommenderas tre prioriterade åtgärder:
1. Införande av tvingande flerfaktorsautentisering (MFA) för alla användarkonton (CIS 6).
2. Aktivering och centralisering av DNS- och inloggningsloggar för att verifiera trafiken (CIS 8).
3. Genomförande av rollanpassad utbildning och etablering av en tydlig rapporteringsrutin för nätfiske (CIS 14).

---

## 2. Fakta, antaganden och scope

### 2.1 Givna fakta
- Nätfiskemejl har skickats till flera medarbetare inom förvaltningen.
- Avsändarnamnet har förfalskats för att likna den interna IT-supporten.
- En medarbetare har öppnat den medföljande länken.
- Medarbetaren uppger att inga autentiseringsuppgifter fyllts i eller lämnats.
- Det finns i dagsläget ingen bekräftad incident eller konstaterat intrång.
- AI-användning för att skapa meddelandena är en möjlighet, inte ett bekräftat faktum.

### 2.2 Antaganden
- Länken ledde till en falsk inloggningssida (phishing proxy/phishing site) avsedd för att stjäla användaruppgifter.
- Medarbetarens enhet (dator) kan ha exponerats för skadlig kod (drive-by download) i samband med klicket, även om inga uppgifter matades in.

### 2.3 Osäkerheter och frågor som behöver verifieras
- Har medarbetaren faktiskt låtit bli att fylla i sina uppgifter, eller finns det osäkerhet i användarens minnesbild?
- Innehöll den externa webbplatsen några skadliga skript eller drive-by-downloads?
- Har andra medarbetare klickat på länken och/eller matat in sina uppgifter utan att rapportera det?

---

## 3. Tillgångar och händelseförlopp

### 3.1 Identifierade tillgångar
1. **Användaridentiteter/Domänkonton (Active Directory / Microsoft 365):** Kritiska för åtkomst till kommunens system och data.
2. **Kommunala IT-system och databaser:** Innehåller känsliga personuppgifter och kommunal information.
3. **E-postinfrastruktur (E-postserver/Gateway):** Nödvändig för kommunens dagliga kommunikation.
4. **Klientmaskiner (Medarbetarnas datorer):** Slutpunkter som används för att nå de interna systemen.

### 3.2 Händelseförlopp (5 steg)
1. **Initiering/Preparering:** Angriparen skapar en phishing-domän och formulerar nätfiskemejl som imiterar kommunens interna IT-support.
2. **Utskick:** Nätfiskemejl skickas ut till ett flertal medarbetare i kommunen.
3. **Exponering/Interaktion:** En medarbetare öppnar mejlet och klickar på den medföljande länken.
4. **Potentiell avläsning/Webbplatsbesök:** Medarbetarens webbläsare kopplar upp sig mot angriparens externa webbplats. Inga uppgifter matas in enligt användaren.
5. **Rapportering och upptäckt:** Händelsen identifieras och IT-avdelningen informeras för att påbörja verifiering och isolering.

---

## 4. CIA och enkel riskbedömning

### 4.1 Påverkan på CIA-triaden
- **Confidentiality (Konfidentialitet):** **MEDEL/RISK.** Om inloggningsuppgifter ändå läckts eller om skadlig kod installerats kan obehöriga få tillgång till känsliga kommunala handlingar och personuppgifter.
- **Integrity (Integritet):** **LÅG.** Ingen data har bekräftats ändrad eller förvanskats i dagsläget.
- **Availability (Tillgänglighet):** **LÅG.** Inga system eller tjänster har tagits ur drift till följd av klicket.

### 4.2 Kvalitativ riskbedömning
- **Sannolikhet:** **Medium (3/5).** Phishing-angrepp sker kontinuerligt och medarbetare klickar ibland på länkar.
- **Konsekvens:** **High (4/5).** Om ett administratörs- eller användarkonto komprometteras kan det leda til dataläckage och behörighetsklättring i kommunens nätverk.
- **Total Risknivå:** **MEDIUM / HÖG.** Även om ingen skada bekräftats krävs omedelbara skyddsåtgärder för att förhindra framtida fullbordade intrång.

---

## 5. CIS Controls v8.1-mappning

### 5.1 CIS 6: Access Control Management
- **Relaterad åtgärd:** Inför stark Multifaktorautentisering (MFA) för alla användarkonton och tillämpa principen om minsta behörighet (Least Privilege).
- **Relaterad verifiering:** Kontrollera via Identity Provider (t.ex. Entra ID / Active Directory) att MFA krävs för 100 % av användarna vid extern inloggning.

### 5.2 CIS 8: Audit Log Management
- **Relaterad åtgärd:** Centralisera och aktivera loggning för DNS-uppslag, webbtrafik/proxy och inloggningsförsök.
- **Relaterad verifiering:** Sök i SIEM/loggsystemet efter DNS-anrop mot den specifika phishing-domänen för att identifiera om fler datorer besökt länken.

### 5.3 CIS 14: Security Awareness and Skills Training
- **Relaterad åtgärd:** Etablera regelbunden utbildning i att identifiera socal engineering/nätfiske samt en enkel "Rapportera nätfiske"-knapp i e-postklienten.
- **Relaterad verifiering:** Genomföra kontrollerade phishing-simuleringar och mäta hur stor andel medarbetare som rapporterar respektive klickar på misstänkta länkar.

---

## 6. Prioriterade åtgärder (Högst tre)

1. **Aktivera strikt MFA (MFA Enforcement):** Tvinga multifaktorautentisering på alla konton så att stulna lösenord inte kan användas av angriparen från externa IP-adresser.
2. **Blockera domänen och genomför logganalys:** Lägg till den misstänkta webbadressen/IP-adressen i kommunens DNS-filter/brandvägg samt analysera proxy- och DNS-loggar för att se om fler enheter anslutit.
3. **Etablera snabb rapporteringsrutin:** Informera personalen om händelsen och påminn om rutinen för hur misstänkt e-post ska rapporteras till IT-supporten.

---

## 7. Teknisk koppling
Denna analys bygger på kursens moment kring **nätverksloggning och identitetshantering**:
- **DNS- och Proxy-loggar:** Genom att analysera DNS-förfrågningar (`UDP/53`) kan IT-avdelningen identifiera vilka interna IP-adresser som gjort uppslag mot den skadliga domänen vid tidpunkten för mejlutskicket.
- **HTTP/HTTPS-sessioner:** Även om HTTPS döljer innehållet i trafiken, kan TLS Server Name Indication (SNI) i proxy-loggen bekräfta vilka klienter som upprättat en anslutning till angriparens IP-adress.

---

## 8. English Security Summary
A potential phishing incident targeting a municipal administration was identified after several employees received fraudulent emails disguised as internal IT support. The emails urged recipients to log in via an external link to maintain system access. One employee clicked the link but reported no credentials were provided. Currently, there is no confirmed system compromise or data breach. AI involvement remains an unverified hypothesis. The overall risk is assessed as Medium due to the potential impact of credential theft. Recommended immediate mitigation actions include enforcing Multi-Factor Authentication (MFA) across all user accounts (CIS 6), analyzing DNS and proxy logs for additional exposures (CIS 8), and reinforcing security awareness reporting routines for staff (CIS 14).

---

## 9. AI- och källredovisning
- **Använda verktyg:** Generativ AI (Gemini) har använts som stöd för strukturering, språklig granskning och formulering av rapporfelement.
- **Verifiering & Korrigering:** Samtliga fakta har kontrollerats mot case-beskrivningen för Case A. AI-förslag som antydde bekräftad skadlig kod eller bekräftad AI-användning har tagits bort för att strikt hålla fakta separerade från antaganden.
- **Källor:** CIS Controls v8.1 officiella riktlinjer för kontroller 6, 8 och 14.

---

## 10. Slutsats
Incidenten utgör ett klassiskt nätfiskeansats där en snabb rapportering och avsaknad av inmatade uppgifter förhindrade ett omedelbart intrång. Genom att genomföra de tre rekommenderade åtgärderna höjs organisationens lägsta skyddsnivå avsevärt mot framtida och mer sofistikerade angrepp.
