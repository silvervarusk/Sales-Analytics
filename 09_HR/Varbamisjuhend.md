# RÜHM 1 – VÄRBAMISJUHENDI PEATÜKK: Tehniline hindamine ja intervjuu stsenaarium

**Teemad:** 
1. Kuidas hinnata DA tehnilisi oskusi (SQL, Python, tööriistad)
2. DA intervjuu stsenaarium (küsimused, hindamiskriteeriumid, ajaplaan)

**Meeskond:** Sales Analytics  
**UrbanStyle juht:** Toomas Kask (IT Director) + juhatus

**Eesmärk:** Luua terviklik ja standardiseeritud tehnilise intervjuu raamistik 7 kandidaadile (5 Eestisse, 2 remote Soome/Saksamaa), mis hõlmab nii tehniliste oskuste hindamist kui ka intervjuu läbiviimise praktilist stsenaariumi.

---

## 1. ÜLEVAADE

See peatükk koondab UrbanStyle'i tehnilise värbamisprotsessi kahest olulisest aspektist: 
1) **Mida hinnata** – tehnilised oskused (SQL, Python, visualiseerimine, versioonihaldus, dokumentatsioon) ja 
2) **Kuidas hinnata** – intervjuu stsenaarium koos konkreetsete küsimuste, ajakava ja hindamiskriteeriumidega.

Kuna UrbanStyle kasvab kiiresti (150% 2 aastaga) ja värbab nii kohalikke kui ka remote-töötajaid Soomest ja Saksamaalt, on ühtne ja objektiivne hindamisraamistik kriitilise tähtsusega. See peatükk annab igale intervjueerijale (HR, tehniline juht, personalijuht, tiimijuht) konkreetsed tööriistad kandidaatide võrdlemiseks ja parima valiku tegemiseks.

---

## 2. ROLL A – PALKAMISJUHT (HR / Hiring Manager) – Irina

**KÜSIMUS:** Mida peab HR otsima kandidaadi CV-st ja LinkedInist, et tuvastada tehniline kompetents ENNE intervjuud? Kuidas disainida CV-sõelumise etappi?

### 2.1. CV kriteeriumid (tehniline fookus)

- **SQL-i konkreetsus** – otsi sõnu: *JOIN, subquery, CTE, window functions (ROW_NUMBER, RANK, LAG), query optimization, indexes*. Kui on vaid "SQL" ilma täpsustuseta – nõrk signaal.
- **Pythoni teegid** – *pandas, numpy, scikit-learn, statsmodels, matplotlib, seaborn, plotly*. Kui puuduvad teegid, on tõenäoline, et kandidaat on teinud vaid algkursuse.
- **Visualiseerimistööriistad** – *Power BI, Tableau, Looker, Streamlit, Dash* koos projektikirjeldusega.
- **Versioonihaldus** – *Git, GitHub, GitLab, branching, pull requests, code reviews*. Kui Git on mainimata – punane lipp.
- **Pilvetehnoloogiad** (boonusena) – *AWS, GCP, Azure, BigQuery, Snowflake* – eriti oluline remote-töötajatele.

### 2.2. LinkedIni "pin-worthy" projektid (tehnilisest vaatepunktist)

- **Repositooriumi link** – iga pinitud postitus peab sisaldama otsest linki GitHubi repositooriumile, kus on näha **README.md** koos paigaldus- ja kasutusjuhendiga.
- **Tehniline sügavus** – postitus kirjeldab lahenduse arhitektuuri: andmebaas (PostgreSQL/MySQL/BigQuery), Pythoni raamistik (FastAPI/Airflow/Jupyter), visualiseerimiskiht.
- **Probleem-lahendus paar** – *"Lahendasin 10 miljoni reaga seotud aeglase päringu, optimeerides indekseid ja kasutades aknafunktsioone, vähendades vastuseaja 45 sekundilt 2 sekundile"*.

### 2.3. Rohelised lipud (HR tehniline sõel)

1. **CV-s on eraldi sektsioon "Tehniline stack"** koos versioonide ja kasutustasemega (nt *"Python 3.10 – igapäevane arendus"*).
2. **GitHubi link on CV-s esimesel kolmandikul** ja kõik LinkedIni projektid viitavad sinna.
3. **Kandidaat on maininud osalemist Open Source projektides** või koodiülevaadetes – see näitab kaasaegse tarkvaraarenduse tsükli tundmist.

### 2.4. Punased lipud (HR hoiatused)

1. **CV-s on loetletud 15+ tehnoloogiat** (Excel, SPSS, R, Tableau, Qlik, Python, Java, C++...) – viitab pindmisele tundmisele. Keskendu 5-6 põhitehnoloogiale.
2. **LinkedInis puudub igasugune tehniline sisu** (artiklid, projektid, soovitused tehnilistelt juhtidelt) – kandidaat pole oma tehnilist kaubamärki ehitanud.

### 2.5. Mida HR esimesena vaatab (CV-sõelumise ajal – max 30 sekundit)

1. **Kas GitHubi link on olemas ja kas see on töökorras?** (kui link on vigane või puudub – lükka kohe kõrvale).
2. **Kas viimases töökohas on mainitud SQL-i ja Pythonit koos konkreetsete tulemustega?** (nt *"ehitasin ETL pipeline'i pandasiga, mis vähendas aruandluse aega 3 tunnilt 15 minutile"*).
3. **Kas hariduse ja kogemuse kombinatsioon on loogiline?** (nt matemaatika/informaatika taust + 2+ aastat kogemust).

---

## 3. ROLL B – TEHNILINE INTERVJUEERIJA (Technical Interviewer) – Tiiu

**KÜSIMUS:** Kuidas disainida tehniline intervjuu ja hinnata kandidaadi koodi/GitHubi nii, et see annaks objektiivse pildi tema oskustest?

### 3.1. Intervjuu stsenaarium – ülesehitus (75 minutit kokku)

| Aeg | Tegevus | Eesmärk |
|-----|---------|---------|
| 0:00–0:05 | Sissejuhatus + soojendusküsimus | Kandidaadi mugavustunde loomine |
| 0:05–0:20 | **SQL ülesanne (live-kood)** | Hinnata andmebaasioskust, optimeerimist, loogilist mõtlemist |
| 0:20–0:40 | **Pythoni ülesanne (live-kood)** | Hinnata andmetöötlusoskust, koodikvaliteeti, probleemilahendust |
| 0:40–0:55 | **Tööriistade arutelu** (Power BI/Plotly, Git, dokumentatsioon) | Hinnata laiemat tehnilist kirjaoskust ja kogemust |
| 0:55–1:10 | **Arhitektuuriline küsimus** | Hinnata süsteemset mõtlemist ja otsustusvõimet |
| 1:10–1:15 | Kandidaadi küsimused + lõpetus | Hinnata huvi ja ettevalmistust |

### 3.2. SQL ülesanne (15 min live-kood)

**Ülesande kirjeldus (UrbanStyle kontekst):**

> Sul on tabel `orders`:
> - `order_id` (int)
> - `customer_id` (int)
> - `order_date` (date)
> - `total_amount` (decimal)
> - `store_type` (varchar – 'online' või 'physical')
> - `country` (varchar – 'EE', 'FI', 'DE')
> 
> **1)** Kirjuta SQL-päring, mis arvutab **iga riigi kohta 2025. aasta esimese kvartali keskmise tellimuse summa**.
> 
> **2)** Kirjuta SQL-päring, mis leiab **kliendid, kes on ostnud vähemalt korra mõlemas kanalis (online ja physical)** ja arvuta nende koguostusumma.
> 
> **3)** Kuidas optimeeriksid neid päringuid, kui tabelis on 50 miljonit rida?

**Hindamiskriteeriumid:**
| Tase | Oskus |
|------|-------|
| **5 (suurepärane)** | Kasutab CTE-d, aknafunktsioone, selgitab indekseid ja partitsioone; kirjutab loetava ja optimeeritud koodi |
| **4 (hea)** | Kasutab JOIN-e, GROUP BY-d, HAVING-it; mõistab alampäringuid; oskab lisada WHERE-filtri |
| **3 (rahuldav)** | Kirjutab lihtsa päringu, mis töötab, kuid pole optimeeritud; vajab abi keerukamate konstruktsioonidega |
| **2 (nõrk)** | Ei oska JOIN-e või GROUP BY-d õigesti kasutada; päring ei tööta |
| **1 (puudulik)** | Ei oska SQL-i üldse |

### 3.3. Pythoni ülesanne (20 min live-kood)

**Ülesande kirjeldus:**

> Sulle antakse CSV-fail (50 000 rida) UrbanStyle müügiandmetega:
> - `date`, `store`, `category`, `sales`, `cost`, `units_sold`
> 
> **1)** Loe fail pandasesse ja kuva esimesed 5 rida.
> 
> **2)** Arvuta iga kategooria marginaal (`(sales - cost) / sales * 100`).
> 
> **3)** Leia iga kuu keskmine marginaal ja salvesta see uude DataFramesse.
> 
> **4)** Kirjuta funktsioon, mis võtab sisendiks kuupäeva (string) ja tagastab selle kuu 3 parima marginaaliga kategooria koos marginaaliga.

**Hindamiskriteeriumid:**
| Tase | Oskus |
|------|-------|
| **5 (suurepärane)** | Kasutab vektoriseeritud operatsioone, type hints, dokstringe; kirjutab taaskasutatavaid funktsioone; käsitleb vigu (`try-except`) ja puuduvaid väärtusi |
| **4 (hea)** | Kasutab pandas groupby-d ja agg-funktsioone; kood on loetav; muutujanimed kirjeldavad |
| **3 (rahuldav)** | Kood töötab, kuid kasutab for-tsükleid; puuduvad kommentaarid; ei käsitle vigu |
| **2 (nõrk)** | Kood on segane; ei kasuta pandase tõhusalt; tulemus on vale |
| **1 (puudulik)** | Ei oska Pythonit üldse |

### 3.4. Tööriistade arutelu (15 min)

**Küsimused visualiseerimise kohta (Power BI / Plotly):**
- *"Kuidas ehitaksid dashboardi, mis näitab reaalajas online-müüki vs füüsilise poe müüki? Milliseid graafikuid kasutaksid ja miks?"*
- *"Kuidas selgitaksid mitte-tehnilisele juhile, miks interaktiivne dashboard on parem kui staatiline aruanne?"*

**Küsimused Git-i kohta:**
- *"Näita mulle oma GitHubi repo. Miks sa kasutasid just seda branchimise strateegiat?"*
- *"Kuidas lahendaksid konflikti, kui sinu feature branch on main-ist maha jäänud?"*
- *"Mis vahe on merge-l ja rebase-l? Millal kumbagi kasutada?"*

**Küsimused dokumentatsiooni kohta:**
- *"Mida peaks sisaldama hea README?"*
- *"Kuidas dokumenteeriksid keerulist SQL-päringut, mida teised analüütikud hakkavad kasutama?"*

**Hindamiskriteeriumid:**
| Tase | Oskus |
|------|-------|
| **5** | Oskab selgitada DAX-i põhimõtteid; teab Plotly express vs graph_objects erinevust; oskab rebase-d ja merge-i; README sisaldab installi, kasutust, näiteid ja andmeallikaid |
| **4** | Mõistab visualiseerimise põhimõtteid; oskab Git-is põhitoiminguid; README on olemas |
| **3** | Teab tööriistu, kuid ei oska neid süvitsi selgitada; Git-is teeb ainult commit ja push |
| **2** | Ei tea, mis on pull request; visualiseerimine piirdub Exceliga |

### 3.5. Arhitektuuriline küsimus (15 min)

**Küsimus:** 
> *"Kujuta ette, et UrbanStyle'il on andmed kolmes erinevas süsteemis: e-poe andmebaas (PostgreSQL), füüsiliste poodide kassaandmed (CSV-failid) ja turundusandmed (Google Analytics API). Kuidas kavandaksid lahenduse, mis koondab need andmed ühtsesse analüüsiplatvormi?"*

**Hindamiskriteeriumid:**
| Tase | Oskus |
|------|-------|
| **5** | Kirjeldab ETL-pipeline'i (extract, transform, load), mainib Airflow't või Prefect'i, andmeladu (data warehouse), andmemudeli kujundust |
| **4** | Mainib API-päringuid, pandas CSV lugemist, SQL-i andmete ühendamist |
| **3** | Pakub lihtsa lahenduse (käsitsi andmete ühendamine), kuid ei arvesta automatiseerimist |
| **2** | Ei osa andmeallikaid ühendada |

---

## 4. ROLL C – PERSONALIJUHT (People Manager) – Silver

**KÜSIMUS:** Kuidas hinnata kandidaadi pehmeid oskusi tehnilises intervjuus? Kuidas näevad pehmed oskused välja koodis ja GitHubis?

### 4.1. Kommunikatsioon (tehniline selgitamine)

- **Kuidas kandidaat kaitseb oma tehnilist valikut?** Näiteks: *"Miks sa valisid pandas, mitte SQL-i selle andmete puhastamiseks?"* – hea kandidaat toob välja pandas flexibility ja data type handling.
- **Kas ta oskab rääkida MITTE-tehnilisele inimesele?** Proovi: *"Seleta mulle, mis on SQL-i aknafunktsioon, nii et ma saaksin aru kui marketingijuht."*
- **Dokumentatsioonioskus** – kas README-s on selgelt kirjas, kuidas keskkonda püstitada, kust andmeid saada ja milline on väljundi struktuur?

### 4.2. Probleemilahendus (loogiline mõtlemine)

- **Kas ta selgitab oma mõttekäiku enne koodi kirjutamist?** (nt *"Ma lähenen nii: kõigepealt puhastan andmed, siis grupeerin, siis visualiseerin"*).
- **Kuidas ta reageerib, kui seisab silmitsi veaga?** (debugimisoskus – kas ta loeb veateadet, kasutab print/im-ga kontrolli, kontrollib andmetüüpe).
- **Kas ta toob välja alternatiivsed lahendused?** (nt *"Võiks ka regressiooni kasutada, aga aegridade puhul sobib ARIMA paremini"*).

### 4.3. Meeskonnatöö (koostöö märgid)

- **Kas GitHubis on näha koostööd?** (mitme autori commit-id, pull requestid, kommentaarid teiste koodile).
- **Kas ta mainib projektides koostööd?** (nt *"töötasin koos turundusmeeskonnaga"*, *"kogusin nõudeid müügiosakonnalt"*).
- **Kuidas ta suhtub tagasisidesse?** (kas ta on avatud kriitikale ja teeb kohe parandusi).

### 4.4. Kultuuriline sobivus (UrbanStyle kontekst)

UrbanStyle väärtused: **kasv, koostöö, kliendikesksus, andmepõhisus, paindlikkus**.

- **Kiire kasv** – kandidaat on töötanud kiirelt kasvavas keskkonnas (startup, skaleeruv ettevõte).
- **Andmepõhisus** – ta otsustab andmete põhjal, mitte intuitsiooni järgi.
- **Paindlikkus** – ta on õppinud viimase aasta jooksul uue tööriista (nt läks üle Tableau'lt Power BI-le).

### 4.5. Rohelised lipud (People Manager)

1. **README-s on sektsioon "Kuidas see projekt aitas äri"** – selge seos äri-eesmärgiga.
2. **Kandidaat selgitab keerulisi kontseptsioone lihtsalt** (nt *"aknafunktsioon võimaldab arvutada jooksva keskmise ilma andmeid grupeerimata"*).
3. **Ta on teinud koodiülevaateid või osalenud paaris programmeerimises** (pair programming).

### 4.6. Punased lipud

1. **Kirjeldab oma koodi ainult sõnadega "see töötab"** – ei oska selgitada, miks see on hea lahendus.
2. **Puuduvad kommentaarid koodis ja commit-sõnumid on "update", "fix"** – viitab madalale professionaalsusele.

---

## 5. ROLL D – TIIMIJUHT (Team Lead) – Irina

**KÜSIMUS:** Kas kandidaat suudab iseseisvalt omandada uusi tehnilisi oskusi, aidata kaaslastel kasvada ja olla tiimi väärtuslik liige?

### 5.1. Iseseisvus (tehniline)

- **Kas kandidaat on loonud lahenduse nullist?** (nt oma ETL-pipeline või täieliku dashboardi).
- **Kas ta on ise valinud tehnoloogiad?** (nt *"Valisin Plotly, sest vajasin interaktiivsust ja seda on lihtne integreerida Pythoni veebirakendusega"*).
- **Kuidas ta lahendas takistusi?** (nt *"Otsisin lahendust Stack Overflow'st ja kohandasin selle meie andmetele"*).

### 5.2. Kommunikatsioon tiimijuhile

- **Kas ta on kirjutanud tehnilise projekti plaani?** (arhitektuuridiagramm, andmemudel).
- **Kas ta oskab hinnata töömahtu?** (nt *"Selle SQL-päringu kirjutamine võtab aega 2 tundi, optimeerimine veel 1 tund"*).
- **Kas ta toob välja riske?** (nt *"Andmete kvaliteediga võib olla probleeme – peame kontrollima puuduvaid väärtusi"*).

### 5.3. Koostöö (mentorlus ja teadmiste jagamine)

- **Kas ta on juhendanud kolleege?** (nt Stack Overflow vastused, sisekoolitused).
- **Kas ta on loonud tehnilise baaskomponendi, mida teised saavad taaskasutada?** (nt ühine Pythoni funktsioonide kogu).
- **Kas tema pull requestid sisaldavad konstruktiivset tagasisidet?** (ei ole lihtsalt "LGTM").

### 5.4. Arengupotentsiaal

- **Vaata commit-ajalugu** – kas esimesed projektid on lihtsamad ja hilisemad keerukamad?
- **Kas ta on õppinud uut tehnoloogiat?** (nt läks PostgreSQL-ilt BigQuery-le).
- **Kas ta on loonud sisu?** (blogipostitus, töötuba, videoõpetus).

### 5.5. Rohelised lipud (Team Lead)

1. **Repos on tests/ kaust** – professionaalne tarkvaraarenduse mõtteviis.
2. **Ta on avanud pull requesti mõnele Open Source projektile** – kõrgeim iseseisvuse tase.
3. **Ta on teinud refaktorimist** – mõtleb kvaliteedile pikemas perspektiivis.

### 5.6. Punased lipud

1. **Kõik projektid on tehtud ainult Jupyter Notebook'is** – pole ühtegi `.py` skripti.
2. **Kandidaat ei saa aru, miks on vaja virtuaalkeskkonda (venv)** – suur punane lipp.

---

## 6. ROLL E – VALIDEERIJA & KVALITEEDIKONTROLL + ÄRISÜNTEES

**Valideerimisraport**

| Roll | Kontrollitud aspekt | Otsus | Märkus |
|------|----------------------|-------|--------|
| A (Irina) | Kas CV/LinkedIni kriteeriumid on tehnilised ja konkreetsed? | **OK** | SQL-i aknafunktsioonid, Pythoni teegid, Git on mainitud |
| A (Irina) | Kas HR-i esmavaate kriteeriumid on selged? | **OK** | GitHubi link, kvantifitseeritud tulemused, haridus+kogemus |
| B (Tiiu) | Kas SQL-i, Pythoni ja tööriistade ülesanded on konkreetsed? | **OK** | Reaalsed UrbanStyle andmed, optimeerimisülesanded |
| B (Tiiu) | Kas intervjuu stsenaarium on praktiline? | **OK** | 75-minutine ajakava iga etapiga |
| C (Silver) | Kas pehmete oskuste hindamine on seotud tehnilise kontekstiga? | **OK** | Kommunikatsioon koodis, dokumentatsioon, koostöö märgid |
| C (Silver) | Kas kultuuriline sobivus on hinnatud? | **OK** | Kiire kasv, paindlikkus, andmepõhisus |
| D (Irina) | Kas iseseisvus ja arengupotentsiaal on hinnatud läbi tehniliste verstapostide? | **OK** | Testid, Open Source, refaktorimine |

**PARANDA ettepanekud:**
- **Roll B (Tiiu):** Lisa SQL-i ülesandesse ka `HAVING` näide – paljud kandidaadid unustavad selle ära.
- **Roll D (Irina):** LISA konkreetne küsimus remote-töö kohta: *"Kuidas hoiad sidet kaugmeeskonnaga, kui oled Soomes/Saksamaal?"*
- **Kõik rollid:** LISA punkt "Remote-spetsiifilised oskused" – eriti oluline Soome ja Saksamaa kandidaatidele.

**Ristkontroll:** Kõik rollid on omavahel kooskõlas – HR sõelub tehnilist kompetentsi, tehniline intervjuu seda süvitsi kontrollib, personalijuht hindab suhtlust ja kultuuri, tiimijuht vaatab iseseisvust ja kasvupotentsiaali.

---

## 7. KOKKUVÕTE – VASTUSED KOLMELE SÜNTEESIKÜSIMUSELE

### 7.1. Mis oli kõige üllatavam – mida tööandjad TEGELIKULT tehniliselt hindavad?

> **Kõige üllatavam oli avastus, et kandidaadid, kes oskavad kirjutada keerukaid SQL-päringuid, kukuvad sageli läbi Pythoni andmepuhastuse ülesannetes, sest neil puudub süstemaatiline arusaam DataFrame'i struktuurist ja veahaldusest. Samuti üllatas, et enamik kandidaate ei oska selgitada, miks nad just konkreetset JOIN-i või visualiseerimisviisi kasutasid – nad lihtsalt "teevad, nagu harjunud".**

### 7.2. Millist soovitust annaksime Liisile värbamisprotsessi parandamiseks?

> **Soovitame jagada tehniline hindamine kaheks etapiks:**
> 1) **Kodune eelülesanne (3–4 tundi)** – reaalsed UrbanStyle andmed, kus kandidaat peab koostama SQL-päringud, Pythoni puhastusskripti ja visualiseeringu. See säästab intervjuuaega.
> 2) **Intervjuu (75 minutit)** – kandidaat esitleb oma lahendust, vastab küsimustele "miks just nii" ja teeb väikse live-muudatuse (nt "lisa filtreering kuu järgi"). See paljastab kohe, kas tegemist on teooria või praktilise oskusega.
> 
> **Lisa igasse vooru konkreetne ärikontekst** – kandidaat peab lahendama UrbanStyle'le tüüpilise probleemi (nt kampaania ROI analüüs, lao täiendamise ennustus).

### 7.3. Mis info puudub tehnilise hindamise kohta, mida peaksime veel uurima?

> **Puudub süvainfo kandidaadi kogemuse kohta pilvplatvormidel (AWS, GCP, Azure) ja suurandmete tööriistades (Spark, BigQuery).** Kuna UrbanStyle kasvab kiiresti, võivad andmemahud peagi nõuda pilvelahendusi. Soovitame lisada ühe lisaküsimuse:
> *"Kuidas töötleksid 100 GB andmeid, kui pandas jääb aeglaseks?"*
> See eristab kandidaate, kes on valmis tuleviku väljakutseteks.

---

## 8. 3 VÕTMESOOVITUST TOOMASELE (IT Director) + JUHATUSELE

1. **Loo ühtne "tech task" repo** – laadi sinna näidisandmed ja täpsed juhised. Kõik kandidaadid saavad sama ülesande, mis võimaldab objektiivset võrdlust. Lisa automaatne testimisskript, et kontrollida, kas SQL-päringud tagastavad õige tulemuse.

2. **Kasuta paarishindamist (pair-coding)** – lase kandidaadil kirjutada SQL/Python koos sinu meeskonna vanemanalüütikuga. See annab kohe pildi koostööoskusest ja viisist, kuidas ta probleemile läheneb (kas ta küsib abi, kas ta kommenteerib tegevusi).

3. **Loo ühtne hindamiskaart (scorecard)** kõigile intervjueerijatele, kus on 5-pallised skaalad:
   - SQL-i oskus (süntaks, optimeerimine, keerukus)
   - Pythoni oskus (loetavus, tõhusus, veakäsitlus)
   - Tööriistade tundmine (visualiseerimine, Git, dokumentatsioon)
   - Kommunikatsioon (tehniline selgitamine, ärikesksus)
   - Koostöö ja iseseisvus
   - Arengupotentsiaal

   See muudab otsuse objektiivsemaks ja võrreldavaks.

