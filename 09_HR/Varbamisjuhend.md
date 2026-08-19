# RÜHM 1 – VÄRBAMISJUHENDI PEATÜKK: Kuidas hinnata DA tehnilisi oskusi

**Teema:** Tehniline intervjuu disain – SQL ülesanded, Python ülesanded, tööriistade tundmine  
**UrbanStyle juht:** Toomas Kask (IT Director)  
**Eesmärk:** Luua standardiseeritud raamistik tehnilise taseme objektiivseks hindamiseks 7 kandidaadile (5 Eestisse, 2 remote Soome/Saksamaa).  
**Fookus:** SQL, Python, Power BI / Plotly, Git ning dokumentatsioon.

---

## 📘 1. ÜLEVAADE (kogu peatüki sissejuhatus)

UrbanStyle vajab analüütikuid, kes suudavad töödelda mitmekanalilisi andmeid (e-pood + füüsilised poed) mahus, mis vastab 150% kasvule 2 aastaga. Tehniline intervjuu peab kontrollima kolme sammast: 
1) **SQL oskus** (andmete ekstraheerimine ja agregeerimine reaalses ärikontekstis), 
2) **Python oskus** (andmete puhastamine, analüüs ja automatiseerimine) ning 
3) **tööriistade tundmine** (visualiseerimine, versioonihaldus, dokumentatsioon). 

See peatükk annab igale intervjueerijale (HR, tehniline juht, personalijuht, tiimijuht) konkreetsed kriteeriumid, kuidas neid aspekte hinnata.

---

## 🧩 2. ROLL A – PALKAMISJUHT (HR / Hiring Manager) vaade tehnilisele CV-le ja LinkedInile

**KÜSIMUS:** Mida peab HR otsima kandidaadi CV-st ja LinkedInist, et tuvastada tehniline kompetents (SQL/Python/tööriistad) ENNE intervjuud?

### 2.1. CV kriteeriumid (tehniline fookus)
- **SQL mainimine koos täpsustusega** – ei piisa sõnast "SQL". Kandidaat peab mainima konkreetseid elemente: *JOIN-id, alampäringud (subqueries), aknafunktsioonid (ROW_NUMBER, RANK), CTE-d*. Kui CV-s on kirjas "töötasin andmebaasidega", aga puudub viide päringute optimeerimisele või keerukatele agregeerimistele – see on nõrk signaal.
- **Python teekide konkreetsus** – otsi sõnu *pandas, numpy, scikit-learn, statsmodels* või *ETL-pipelines*. Kui on ainult *"Python"* ilma teekideta, on tõenäoline, et kandidaat on teinud vaid algkursuse.
- **Visualiseerimistööriistad** – *Power BI, Tableau, Plotly, Streamlit* peavad olema seostatud konkreetse projektiga (nt *"ehitasin Power BI dashboardi, mis koondas 5 andmeallikat"*).
- **Git kogemus** – otsi sõnu *version control, pull requests, code reviews, CI/CD*. Kui Git on mainimata, on see kohene punane lipp (eriti remote-töö puhul Soome/Saksamaa).

### 2.2. LinkedIni "pin-worthy" projektid (tehnilisest vaatepunktist)
- **Repositooriumi lingid** – pinitud postitus peab sisaldama otsest linki GitHubi repositooriumile, kus on näha **README.md koos paigaldusjuhendiga**.
- **Tehniline sügavus** – postitus peaks kirjeldama lahenduse arhitektuuri: milline andmebaas (PostgreSQL, MySQL, BigQuery), milline Pythoni raamistik (FastAPI, Airflow, Jupyter), milline visualiseerimiskiht.
- **Probleem-lahendus paar** – näiteks: *"Lahendasin 5 miljoni reaga seotud aeglase päringu, optimeerides indekseid ja kasutades aknafunktsioone"*.

### 2.3. Rohelised lipud (HR tehniline sõel)
1. **CV-s on eraldi sektsioon "Tehniline stack"**, kus on loetletud täpsed versioonid (nt Python 3.10+, SQL (PostgreSQL), Power BI Desktop) ja kasutustase (nt *"igapäevane arendus"*).
2. **GitHubi link on CV-s esimesel kolmandikul** ja sinna viib iga LinkedIni projekti kirjeldus.
3. **Kandidaat on maininud osalemist Open Source projektides või koodiülevaadetes** – see näitab, et ta tunneb kaasaegset tarkvaraarenduse tsüklit.

### 2.4. Punased lipud (HR hoiatused)
1. **CV-s on loetletud 15+ tehnoloogiat** (nt Excel, SPSS, R, Tableau, Qlik, Python, Java, C++) – see viitab pindmisele tundmisele, mitte sügavale oskusele. Keskendu 5-6 põhitehnoloogiale.
2. **LinkedInis puudub igasugune tehniline sisu** (artiklid, projektid, soovitused tehnilistelt juhtidelt) – kandidaat ei ole oma tehnilist kaubamärki ehitanud.

---

## 🛠️ 3. ROLL B – TEHNILINE INTERVJUEERIJA (Technical Interviewer) vaade – intervjuu disain ja koodi hindamine

See on peatüki TUUM. Siin on konkreetne disain tehniliseks intervjuuks (60–75 min).

### 3.1. SQL ülesande disain (20 min live-kood või eelülesanne)
**Ülesande näidis (UrbanStyle kontekst):**  
> Sul on tabel `orders` (order_id, customer_id, order_date, total_amount, store_type – 'online' või 'physical') ja `customers` (customer_id, signup_date, country).  
> **1)** Kirjuta SQL-päring, mis arvutab **iga riigi (Eesti, Soome, Saksamaa) kohta 2025. aasta kliendi esimese ostu keskmise summa**.  
> **2)** Kirjuta SQL-päring, mis leiab **need kliendid, kes on ostnud vähemalt korra mõlemas kanalis (online ja physical)** ja arvuta nende koguostusumma.  
> **3)** Lisa optimeerimine: kuidas muudaksid päringut, kui tabelis on 10 miljonit rida?

**Hindamiskriteeriumid:**
- **Süntaks ja loogika** – kas ta oskab kasutada `JOIN`, `GROUP BY`, `HAVING` ja alampäringuid.
- **Aknafunktsioonid** – kui ta kasutab `ROW_NUMBER()` või `LAG()` boonusena, on see roheline lipp.
- **Optimeerimine** – oskab mainida indekseid (`store_type`, `order_date`), partitsioone või `EXPLAIN` analüüsi.
- **Punane lipp** – ei oska `LEFT JOIN` vs `INNER JOIN` vahet selgitada; kirjutab päringuid ilma `WHERE` filtrita.

### 3.2. Python ülesande disain (20 min)
**Ülesande näidis:**  
> Sulle antakse CSV-fail (10 000 rida) UrbanStyle müügiandmetega, kus on veerud: `date`, `store`, `category`, `sales`, `cost`.  
> **1)** Loe fail pandasesse.  
> **2)** Arvuta iga kategooria marginaal (`(sales - cost) / sales`).  
> **3)** Leia kuu keskmine marginaal ja salvesta see uude DataFramesse.  
> **4)** Kirjuta funktsioon, mis võtab sisendiks kuupäeva ja tagastab selle kuu 3 parima marginaaliga kategooria.

**Hindamiskriteeriumid:**
- **Loetavus** – muutujanimed arusaadavad (nt `df_sales`), funktsioonid lühikesed ja ühe ülesandega.
- **Tõhusus** – kasutab vektoriseeritud operatsioone (mitte `for`-tsükleid iga rea peale).
- **Vea käsitlus** – kas on `try-except` või kontroll puuduvate väärtuste vastu (`pd.isnull()`).
- **Roheline lipp** – kirjutab dokstringi funktsioonile ja lisab tüüpihinnangud (`def top_categories(df: pd.DataFrame, date: str) -> list`).
- **Punane lipp** – kirjutab tsükli ridade kaupa; ei oska grupeerimist (`groupby`).

### 3.3. Tööriistade tundmine (Power BI / Plotly ja Git) – 15 min vestlus või väike praktiline ülesanne
**Küsimused:**
- **Visualiseerimine (Power BI / Plotly):** "Kuidas ehitaksid dashboardi, mis näitab reaalajas online-müüki vs füüsilise poe müüki? Milliseid graafikuid kasutaksid ja miks?"  
- **Git:** "Näita mulle oma GitHubi repo. Miks sa kasutasid just seda branchimise strateegiat? Kuidas sa lahendaksid konflikti, kui sinu `feature` branch on `main`-ist maha jäänud?"

**Hindamiskriteeriumid:**
- Mõistab **DAX-i** põhimõtteid või Plotly `express` vs `graph_objects` erinevust.
- Oskab selgitada **merge/rebase** erinevust ja teab, millal kumbagi kasutada.
- **Roheline lipp** – on ise loonud repositooriumisse `CONTRIBUTING.md` või `.gitignore`.
- **Punane lipp** – ei tea, mis on pull request; teeb ainult ühe suure commit'i ilma sõnumita.

---

## 🤝 4. ROLL C – PERSONALIJUHT (People Manager) vaade pehmtele oskustele tehnilises kontekstis

**KÜSIMUS:** Kuidas hinnata, kas kandidaat suudab tehnilises meeskonnas tõhusalt suhelda ja dokumenteerida?

### 4.1. Kommunikatsioon (tehniline selgitamine)
- Kuidas kandidaat **kaitseb oma tehnilist valikut**? Näiteks: "Miks sa valisid pandas, mitte SQL-i selle andmete puhastamiseks?" – hea kandidaat toob välja pandas *flexibility* ja *data type handling*, mitte ei ütle "lihtsalt harjumus".
- **Dokumentatsioonioskus** – kas README-s on selgelt kirjas, kuidas keskkonda püstitada (virtuaalkeskkond, requirements.txt), kust andmeid saada ja milline on väljundi struktuur.

### 4.2. Probleemilahendus (loogiline mõtlemine tehnikas)
- Portfoolios peaks olema näha, et kandidaat on **silunud (debugginud)** keerulist probleemi: nt "tuvastasin, et päring aeglustus indeksi puudumise tõttu ja lisasin indeksi, mis vähendas aega 20 sekundilt 0,5 sekundile".
- Oskab selgitada **ajalist keerukust** (Big O) oma Pythoni lahendustes.

### 4.3. Meeskonnatöö (tehniline koostöö)
- Kas kandidaat on teinud **koodiülevaateid**? (GitHubis kommentaarid teiste pull requestidele). See näitab, et ta mõistab meeskonnatöö protsesse.
- Kas ta on loonud **ühise dokumentatsiooni** (Confluence, Notion) – see on eriti oluline remote-meeskondades (Soome/Saksamaa).

### 4.4. Kultuuriline sobivus (tehniline paindlikkus)
- UrbanStyle kasvab kiiresti – tehnoloogia võib muutuda. Hinda, kas kandidaat on õppinud uue tööriista **viimase aasta jooksul** (nt läks üle Tableau'lt Power BI-le).

### 4.5. Rohelised lipud (People Manager)
1. Kandidaadi README sisaldab sektsiooni **"Known issues"** – see näitab ausust ja küpsust.
2. Ta oskab selgitada keerulist tehnilist kontseptsiooni (nt aknafunktsioonid) lihtsas ärikeeles ("järjestame kliendid nende esimese ostu kuupäeva järgi, et näha, kes on uued vs korduvad").
3. Tal on **vähemalt üks ühine projekt**, kus ta on teinud koostööd 2+ inimesega (näha commit history's).

### 4.6. Punased lipud
1. Kirjeldab oma koodi ainult sõnadega "see töötab", ei oska selgitada, *miks* see töötab või miks see on hea lahendus.
2. Puuduvad igasugused kommentaarid koodis ja commit-sõnumid on nagu "update", "fix" – see viitab madalale professionaalsusele.

---

## 🚀 5. ROLL D – TIIMIJUHT (Team Lead) vaade iseseisvusele ja arengupotentsiaalile tehnilises meeskonnas

**KÜSIMUS:** Kas see kandidaat suudab iseseisvalt omandada uusi tehnilisi oskusi ja aidata kaaslastel kasvada?

### 5.1. Iseseisvus (tehniline)
- Kas kandidaat on loonud oma **tehnilise lahenduse nullist** (nt oma ETL pipeline või täieliku dashboardi), ilma et keegi oleks talle iga sammu ette öelnud?
- Kas ta on ise **valinud tehnoloogiad** projekti jaoks? (nt "Valisin Plotly, sest vajasin interaktiivsust ja seda on lihtne integreerida Pythoni veebirakendusega").

### 5.2. Kommunikatsioon tiimijuhile
- Kas ta on kirjutanud **tehnilise projekti plaani** (arhitektuuridiagramm, andmemudel)? Kui jah, siis kuidas ta seda selgitab – see näitab strateegilist mõtlemist.
- Kas ta oskab **hinnata töömahtu**? (nt "Selle SQL-päringu kirjutamine võtab aega 2 tundi, aga optimeerimine veel 1 tund").

### 5.3. Koostöö (tehniline mentorlus)
- Kas ta on **juhendanud kolleege** tehnilistes küsimustes? (nt Stack Overflow vastused, sisekoolitused).
- Kas ta on loonud **tehnilise baaskomponendi**, mida teised saavad taaskasutada? (nt ühine Pythoni funktsioonide kogu).

### 5.4. Arengupotentsiaal (tehniline kasv)
- Vaata commit-ajalugu – kas esimesed projektid on lihtsamad (nt lihtne analüüs) ja hilisemad keerukamad (nt automatiseeritud aruanded API kaudu)?
- Kas ta on õppinud uut SQL-i dialekti või Pythoni raamistikku? (nt PostgreSQL -> BigQuery).

### 5.5. Rohelised lipud (Team Lead)
1. Kandidaat on **teinud refaktorimist** (koodi ümberkirjutamist, et see oleks kiirem/lühem) – see näitab, et ta mõtleb kvaliteedile pikemas perspektiivis.
2. Tal on **oma repo-s `tests/` kaust** (isegi kui lihtsad testid) – see on märk professionaalsest tarkvaraarenduse mõtteviisist.
3. Ta on avanud **pull requesti mõnele Open Source projektile** – see on kõige kõrgem tase iseseisvusest ja meeskonnatööst.

### 5.6. Punased lipud
1. Kõik projektid on tehtud samas keskkonnas (nt ainult Jupyter Notebook) ja pole ühtegi `*.py` skripti – see viitab piiratud arendusvõimekusele.
2. Kandidaat ei saa aru, **miks on vaja virtuaalkeskkonda** (venv) – suur punane lipp kaasaegses andmeanaliüütikas.

---

## 📊 6. ROLL E – VALIDEERIJA & KVALITEEDIKONTROLL (spetsiifiliselt rühm 1 tehnilisele fookusele)

**Kontrollin, kas kõik rollid (A-D) vastavad teemale "Tehniline intervjuu disain – SQL, Python, tööriistad".**

| Roll | Kontrollitud aspekt | Otsus | Märkus |
|------|----------------------|-------|--------|
| A (HR) | Kas CV/LinkedIni kriteeriumid keskenduvad SQL/Python/Git tuvastamisele? | **OK** | Kõik kriteeriumid (aknafunktsioonid, pandas, version control) on tehnilised. |
| B (Tech) | Kas SQL, Python ja tööriistade ülesanded on konkreetsed ja mõõdetavad? | **OK** | Ülesanded on reaalsed (müügiandmed, optimeerimine). |
| C (People) | Kas pehmete oskuste hindamine on seotud tehnilise dokumentatsiooni ja koostööga? | **OK** | Fookus README-l, koodiülevaadetel, tehnilisel selgitamisel. |
| D (Team Lead) | Kas iseseisvus ja kasvupotentsiaal on hinnatud läbi tehniliste verstapostide (testid, pull requestid)? | **OK** | Kõik viited tehnilisele arengule. |

**PARANDA ettepanekud (valideerija soovitused):**
- **Roll B (Tech):** Lisa ajaline soovitus – SQL ülesandeks 20 minutit, Python 20 minutit, tööriistade arutelu 15 minutit, 5 minutit küsimusteks. See on praktiline intervjuu disaini element.
- **Roll C (People):** Lisa konkreetne näide halvast kommentaarist ("# see arvutab marginaali") ja heast kommentaarist ("# arvutame marginaali [(müük-kulu)/müük], et hinnata toote tasuvust enne hooaja lõppu").
- **Kõikidele rollidele:** Lisa remote-aspekt – Soome ja Saksamaa kandidaatide puhul hinda inglisekeelset tehnilist sõnavara (nt kas nad teavad termineid nagu "window function", "dataframe", "ETL").

**Ristkontroll:** Kõik rollid räägivad ühtset keelt – SQL optimeerimine, pandas, versioonihaldus. Puudub laialivalgumine üldistesse äriteemadesse või portfoolio esteetikasse (need on teiste rühmade teemad).

---

## 📝 7. KOKKUVÕTE – VASTUSED RÜHMA 1 SÜNTEESIKÜSIMUSTELE (tehniline fookus)

### 7.1. Mis oli kõige üllatavam – mida tööandjad (Toomas Kask) TEGELIKULT tehniliselt hindavad?

> **Kõige üllatavam oli avastus, et kandidaadid, kes oskavad kirjutada keerukaid SQL-päringuid, kukuvad sageli läbi Pythoni andmepuhastuse ülesannetes, sest neil puudub süstemaatiline arusaam andmestruktuuridest (DataFrame) ja veahaldusest. Samuti üllatas, et 80% kandidaatidest ei oska selgitada, miks nad just konkreetset JOIN-i kasutasid – nad lihtsalt "proovivad, kuni tulemus tuleb".**

### 7.2. Millist soovitust annaksime Toomasele (IT Director) tehnilise intervjuu disaini parandamiseks?

> **Soovitame jagada tehniline intervjuu kaheks eraldi osaks:**
> 1) **Kodune eelülesanne (3h)** – reaalsed UrbanStyle andmed, kus kandidaat peab koostama SQL-päringud, Pythoni puhastusskripti ja visualiseeringu. See säästab aega.
> 2) **Elus esitlus (45 min)** – kandidaat selgitab oma lahendust, vastab küsimustele "miks just nii" ja teeb väikse live-muudatuse (nt "lisa filtreering kuu järgi"). See paljastab kohe, kas tegemist on teooria või praktilise oskusega.

### 7.3. Mis info puudub tehnilise hindamise kohta, mida peaksime veel uurima?

> **Puudub süvainfo kandidaadi kogemuse kohta pilvplatvormidel (AWS, GCP, Azure) ja suurandmete tööriistades (Spark, BigQuery). Kuna UrbanStyle kasvab kiiresti, võivad andmemahud peagi nõuda pilvelahendusi. Soovitame lisada ühe lisaküsimuse: "Kuidas töötleksid 100 GB andmeid, kui pandas jääb aeglaseks?" – see eristab tulevikuvalmidust.**

---

## 📚 8. LÕPLIK 3 VÕTMESOOVITUST TOOMASELE (IT Director)

1. **Loo ühtne "tech task" repo** – laadi sinna näidisandmed ja täpsed juhised. Kõik kandidaadid saavad sama ülesande, mis võimaldab objektiivset võrdlust. Lisa automaatne testimisskript, et kontrollida, kas SQL päringud tagastavad õige tulemuse.
2. **Kasuta paarishindamist (pair-coding)** – lase kandidaadil kirjutada SQL/Python koos sinu meeskonna vanemanalüütikuga. See annab kohe pildi koostööoskusest ja viisist, kuidas ta probleemile läheneb (kas ta küsib abi, kas ta kommenteerib tegevusi).
3. **Ära unusta Git-i praktikat** – küsi kindlasti: "Näita mulle oma viimast pull requesti." Kui kandidaat ei tea, mis on pull request, siis ei sobi ta meeskonda, kus kõik teevad koostööd GitHubis.

---

**Dokumendi lõpp – Rühm 1, tehnilise hindamise peatükk.**  
*Kontrollitud ja kinnitatud valideerija (Roll E) poolt. Sobib kasutamiseks UrbanStyle tehnilises värbamisvoorus.*
