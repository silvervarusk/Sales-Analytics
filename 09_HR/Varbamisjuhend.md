# UrbanStyle Värbamisjuhend – Andmeanalüütiku (Data Analyst) hindamine

**Koostanud:** DACA meeskond (Nädal 9, Sessioon 2)  
**Sihtrühm:** UrbanStyle juhtkond (Liis Koppel, Toomas Kask, Kristi Tamm, Anna Mets, Marko Saar)  
**Eesmärk:** Ühtne raamistik 7 uue andmeanalüütiku värbamiseks (5 Eestisse, 2 remote Soome ja Saksamaa).

---

## 📘 1. Sissejuhatus – Liis Koppeli väljakutse

> "Meeskond, mul on teile oluline ülesanne. UrbanStyle kasvab kiiresti — investorite raha on tulemas ja meil on vaja palgata 7 uut andmeanalüütikut: 5 Eestisse (Tallinn, Tartu, Pärnu) ja 2 remote'i välismaale (Soome, Saksamaa). Aga ausalt? Ma ei tea, kuidas head analüütikut ära tunda! Te olete 8 nädalat siin töötanud. Te TEATE, mida hea analüütik peab oskama. Te TEATE, millised tööriistad on olulised. Te TEATE, kuidas andmeid ärile kasulikuks teha. Palun aidake mul luua värbamisjuhend, mida UrbanStyle'i juhid saavad kasutada."
>
> — Liis Koppel, Operations Manager, UrbanStyle.ltd

**Kristi lisab:**  
"Enne juhatuse koosolekut tahan ma veenduda, et teie portfooliod on valmis. Mitte ainult meie jaoks — vaid TEIE järgmise tööandja jaoks."

**Selles dokumendis esitame tervikliku värbamisjuhendi, mis katab:**

- CV ja LinkedIni hindamise (HR vaade)
- Tehnilise taseme hindamise (kood, GitHub, tööriistad)
- Pehmete oskuste ja kultuurilise sobivuse (personalijuht)
- Iseseisvuse, koostöö ja arengupotentsiaali (tiimijuht)
- Valideerimise ja ärisünteesi (kvaliteedikontroll)

---

## 🧩 2. Kuidas hinnata DA kandidaadi CV‑d ja LinkedIni profiili (Roll A – Palkamisjuht)

### 2.1. CV kriteeriumid – mis teeb DA CV tugevaks?

- **Kvantifitseeritud tulemused** – iga töökogemuse all vähemalt üks arvuline mõõdik (nt *“vähendasin aruandluse aega 4 tunnilt 20 minutini”*, *“tuvastasin hooajalisuse anomaalia, mis säästis 15% laokulusid”*).
- **Selge tehnoloogiapinge** – loetletud täpsed tööriistad (SQL, Python, Power BI/Tableau, Git) koos kasutustasemega (nt *“igapäevane”*, *“arendus”*).
- **Projektide struktuur** – iga projekt kirjeldatud skeemis: **probleem → minu roll → lahendus → tulemus**.
- **Kohandatus rollile** – esile tõstetud just andmeanalüüsiga seotud kogemus, mitte üldine töökirjeldus.

### 2.2. LinkedIn – mis projektid on "pin-worthy"?

- **Interaktiivne link** – projekt, millel on avalik link töötavale dashboardile (Power BI Service, Tableau Public, Streamlit) või interaktiivsele notebookile.
- **Mõju kirjeldus** – postituses selgelt välja toodud, millist äriprobleemi lahendati ja millist kasu see tõi.
- **Koostöö märge** – kui projekt on tehtud meeskonnas, on märgitud kaasautorid ja igaühe panus.

### 2.3. Rohelised lipud (tugev kandidaat)

1. CV‑s on **eraldi sektsioon “Business Impact”** või iga kogemuse all on numbriline tulemus.
2. LinkedInis on **vähemalt kaks “pinnitud” projekti**, kus on selgelt kirjeldatud andmeallikad, kasutatud meetodid ja saadud äriotsus.
3. Kandidaat on **ise loonud sisu** (artiklid, videod, töötoad) – näitab aktiivset õppimist ja jagamiskultuuri.

### 2.4. Punased lipud (hoiatusmärgid)

1. CV‑s puuduvad **arvulised tulemused** – ainult ülesannete loend (nt *“tegin SQL päringuid”*), mitte tulemuste kirjeldus.
2. LinkedIni profiilis pole **ühtegi projekti ega soovitust** – vähene nähtavus ja kogemuste tõendamine.

### 2.5. Mida palkamisjuht esimesena vaatab?

- **Esimene vaade** – kas kandidaadi praegune/viimane roll vastab otsitavale profiilile (andmeanalüütik, BI arendaja, data engineer).
- **Teine vaade** – kas esimese 5 sekundi jooksul on näha **arvulisi tulemusi** (protsendid, rahalised summad, ajasääst).
- **Kolmas vaade** – kas GitHubi või portfolio link on **esile tõstetud** ja töökorras.

---

## 🛠️ 3. Kuidas hinnata DA tehnilist taset koodi ja GitHubi alusel (Roll B – Tehniline intervjueerija)

### 3.1. Koodi kvaliteet – loetavus, kommentaarid, struktuur

- **Loetavus** – muutujanimed kirjeldavad (mitte `x`, `df1`), funktsioonid lühikesed ja täidavad üht ülesannet.
- **Kommentaarid** – ei ole liigselt, aga oluliste otsuste juures on selgitus (miks just see meetod, milline on äri loogika).
- **Struktuur** – projekt jagatud selgetesse kaustadesse (`src/`, `notebooks/`, `tests/`, `data/`) ning on olemas `requirements.txt` või `environment.yml`.

### 3.2. Tööriistade tundmine (SQL, Python, Power BI/Plotly, Git)

- **SQL** – kandidaat oskab kirjutada keerukamaid päringuid (JOIN‑id, alampäringud, aknafunktsioonid), kasutab CTE‑sid, oskab optimeerida (indeksid, `EXPLAIN`). Näidisülesanne: arvutada kliendi eluea väärtus (LTV) müügiandmetest.
- **Python** – kasutab pandaseid ja numpy’t tõhusalt (vektoriseeritud operatsioonid), oskab kirjutada **taaskasutatavaid** ja **testitavaid** funktsioone. Eelistatavalt näha ka ETL‑voogu (Airflow, Prefect) või API‑päringuid.
- **Visualiseerimine** – Power BI või Plotly kasutamine interaktiivsete dashboardide loomiseks; oskus valida õige graafik tüüp andmete olemusest lähtudes.
- **Git** – regulaarsed commit’id (mitte üks suur commit), commit‑sõnumid informatiivsed (nt Conventional Commits). Kasutusel on branches (feature‑branchid, pull requestid).

### 3.3. Dokumentatsioon – README, commit‑sõnumid

- **README** – sisaldab:
  - Projekti eesmärki (äriprobleem).
  - Juhendit keskkonna püstitamiseks.
  - Näidiskäivitust.
  - Andmeallikate kirjeldust.
  - Tulemuste kokkuvõtet ja järeldusi.
- **Commit‑sõnumid** – loetavad ja kirjeldavad, nt *“fix: parandati kuupäevaformaadi tõrge”* või *“feat: lisati LTV arvutuse funktsioon”*.

### 3.4. Rohelised lipud

1. Repos on **testid** (vähemalt lihtsad unittestid või pytest) – professionaalne suhtumine.
2. Koodis on **tüüpihinnangud (type hints)** ja funktsioonide dokstringid (Google või NumPy stiilis).
3. On olemas **eraldi kaust `docs/`** , kus on kirjeldatud arhitektuurilised otsused ja põhjendused.

### 3.5. Punased lipud

1. Repos on **ainult üks suur Jupyteri notebook**, millel puudub struktuur, koodi korratakse, muutujad segased.
2. Puudub **README** või see on tühi – kandidaat ei oska oma tööd teistele selgitada.

---

## 🤝 4. Kuidas hinnata DA kandidaadi pehmeid oskusi ja sobivust meeskonda (Roll C – Personalijuht)

### 4.1. Kommunikatsioon – kuidas hea kandidaat projekte kirjeldab?

- **Selge struktuur** – kirjelduses eraldi lõigud: probleem, meetod, tulemus, järeldus.
- **Keel on mitte‑tehniline** – oskab selgitada keerulisi analüüse ka ilma andmeteaduse žargoonita. Kasutab ärimõisteid.
- **Visualiseerimine** – oskab valida ja selgitada sobivat graafikut, et oma sõnumit toetada.

### 4.2. Probleemilahendus – mis näitab loogilist mõtlemist?

- Portfoolios näha **tervet analüüsitsüklit** – äriküsimuse sõnastusest andmete korrastamise, analüüsi ja soovitusteni.
- Toodud **alternatiivsed lahendused** ja põhjendus, miks üks neist valiti.

### 4.3. Meeskonnatöö – mis märgid näitavad koostööd?

- Projekti kirjelduses mainitud **koostööd** (nt *“töötasin koos turundusmeeskonnaga”*).
- Repos näha **mitme autori kommitte** või viide ühiselt tehtud projektile.
- Kandidaat osalenud **koodiülevaadetes** (pull requestid, kommentaarid).

### 4.4. Kultuuriline sobivus – mis sobib UrbanStyle väärtustega?

UrbanStyle väärtused: **kasv, koostöö, kliendikesksus, andmepõhisus, paindlikkus**.

- Kandidaat on varem töötanud **kiirelt kasvavas keskkonnas**.
- Tema projektid näitavad **algatusvõimet** – ta on ise probleeme tuvastanud.
- Ta on **valmis õppima uusi tööriistu** (nt kui ettevõte kasutab Power BI‑d, aga ta on varem kasutanud Tableau’d, siis ta on ise õppinud Power BI‑d demo tegemiseks).

### 4.5. Rohelised lipud

1. README‑s on eraldi sektsioon **“Kuidas see projekt aitas äri”** – selge seos äri‑eesmärgiga.
2. Kandidaat on oma portfoolios **toonud välja tagasiside**, mida ta on saanud kolleegidelt või juhendajatelt.
3. Ta on **loonud kasutusjuhendi** või video oma dashboardi kasutamiseks – hoolivus teiste kasutajate vastu.

### 4.6. Punased lipud

1. Projektikirjeldus on **ainult tehniline** (loetelu funktsioonidest), puudub selgitus, miks see üldse tehti.
2. Kandidaat ei ole **kunagi teinud koostööd** ega maini meeskonnatööd – võib viidata raskustele tiimis töötamisel.

---

## 🚀 5. Kuidas hinnata DA kandidaadi iseseisvust, koostööd ja kasvupotentsiaali (Roll D – Tiimijuht)

### 5.1. Iseseisvus – mis näitab, et kandidaat lahendab ise?

- Repos on näha **algatusi** – ta ei ole lihtsalt täitnud etteantud ülesandeid, vaid on ise lisanud täiendavaid analüüse, visualiseeringuid või dokumentatsiooni.
- Ta on **ise püstitanud hüpoteese** ja neid testinud.
- On olemas **tõend**, et ta on lahendanud andmetega seotud probleeme ilma juhendamiseta.

### 5.2. Kommunikatsioon – mis näitab selget selgitust?

- Oma projektides on ta **kirjeldanud otsuseid** – miks ta valis just selle agregeerimise, miks ta eemaldas kõrvalekalded, miks ta kasutas just seda graafikut.
- Ta on **kirjutanud kokkuvõtte** (executive summary), mis sobib esitamiseks juhtkonnale – lühidalt, arusaadavalt, tulemustele keskendudes.

### 5.3. Koostöö – mis näitab panust meeskonnatöösse?

- GitHubis näha, et ta on **teinud pull requeste**, osalenud aruteludes (kommentaarid), aidanud kaaslastel koodi parandada.
- Projektikirjelduses mainitud, et ta on **kogunud nõudeid** teistelt osakondadelt (müük, turundus, logistika) ja integreerinud nende tagasisidet.

### 5.4. Arengupotentsiaal – mille järgi hinnata kasvuruumi?

- Vaadata **ajalist arengut** – kui kandidaadil on mitu projekti, siis kas hilisemad on keerukamad, hõlmavad uusi tehnikaid, suuremat andmemahtu või täpsemat ärianalüüsi.
- Kas ta on **õppinud uusi tööriistu** (nt alustas Excelist, liikus SQL‑i, seejärel Pythoni ja pilveteenusteni) – näitab kohanemisvõimet.
- Kas ta on **jaganud teadmist** – kirjutanud blogipostituse, juhendanud kolleege või pidanud töötuba.

### 5.5. Rohelised lipud

1. Kandidaat on oma portfoolios **toonud välja vead** ja nende lahendused – enesekriitiline ja arengule orienteeritud suhtumine.
2. Tal on **vähemalt üks projekt**, mis on tehtud **koostöös** (näha kaasautorid, jagatud repo).
3. Ta on **kasutanud versioonihaldust** professionaalselt (feature branchid, pull requestid, koodiülevaated).

### 5.6. Punased lipud

1. Kõik projektid on **üksikud** ja väga sarnased – pole märke koostööst ega arengust.
2. Kandidaat ei oska **õigustada** oma tehnilisi valikuid (vastab vaid “see tundus sobiv”) – viitab madalale sügavusele.

---

## 📊 6. Valideerimine, kvaliteedikontroll ja ärisüntees (Roll E)

### 6.1. Valideerimisraport (kontroll rollide A–D väljundite üle)

| Roll | Kontrollitud aspekt | Otsus | Märkus |
|------|----------------------|-------|--------|
| A    | Kriteeriumid konkreetsed, mitte üldsõnalised | **OK** | Kõik punktid mõõdetavad – arvulised tulemused, projektide struktuur, pinitud projektid. |
| A    | Vähemalt 3 rohelist + 2 punast lippu | **OK** | Nõutud arv täidetud. |
| B    | Kriteeriumid viitavad konkreetsetele tehnilistele aspektidele | **OK** | SQL, Python, Git, dokumentatsioon selgelt lahti kirjutatud. |
| B    | Kaetud vähemalt 3 tehnilist aspekti + lipud | **OK** | SQL, Python, visualiseerimine, Git – 4 aspekti. |
| C    | Kriteeriumid konstruktiivsed ja konkreetsed | **OK** | Kommunikatsioon, probleemilahendus, koostöö, kultuur – kõik ärikesksed. |
| C    | Vähemalt 2 pehmet oskust koos näidetega | **OK** | Kommunikatsioon ja meeskonnatöö toodud koos konkreetsete portfoolionäidetega. |
| D    | Kriteeriumid tasakaalustatud (rohelised+punased) | **OK** | 3 rohelist, 2 punast. |
| D    | Kaetud koostöö, kommunikatsioon, iseseisvus | **OK** | Kõik kolm kajastatud. |

**PARANDA ettepanekud:**

- **Roll A** – soovitan lisada selgituse, et LinkedInis tuleks kontrollida ka **soovitusi** (recommendations) kolleegidelt.
- **Roll B** – lisada konkreetne näidisülesanne (nt “kirjuta SQL‑päring, mis arvutab 30‑päevase aktiivsete klientide osakaalu”).
- **Roll C** – täpsustada, et kultuurilise sobivuse puhul tuleb arvestada ka **regionaalseid erisusi** (Soome – madal hierarhia, Saksamaa – struktureeritus).
- **Roll D** – lisada soovitus hinnata ka **viisi, kuidas kandidaat suhtub tagasisidesse** – kas ta on avatud kriitikale ja kohaneb kiiresti.

**Ristkontroll:** Kõikide rollide kriteeriumid on omavahel kooskõlas – CV ja LinkedIni hinnangud toetavad tehnilist hinnangut, pehmed oskused ja koostöövõime on omavahel seotud. Vastuolusid ei leitud.

### 6.2. Ühtne ärikokkuvõte (stakeholderile – tööandja vaade)

1. **Peamine järeldus** – UrbanStyle vajab andmeanalüütikuid, kes ei oska mitte ainult SQL‑i ja Pythonit, vaid suudavad **tõlkida andmed äriotsusteks** ning suhelda nii tehniliste kui ka mitte‑tehniliste osapooltega.
2. **Mis otsus muutub?** – Värbamisprotsessi tuleb lisada **ärijuhtumi ülesanne** (business case), kus kandidaat peab reaalse müügiandmete põhjal soovitama hinnakujunduse muudatust või turunduskanali optimeerimist. See eristab oskajad teoreetikutest.
3. **Mis üllatas?** – Kõige suurem üllatus oli, et **enamik kandidaate** ei suuda oma varasemaid projekte siduda **mõõdetava rahalise või efektiivsuse kasvuga** – nad kirjeldavad tehnilisi detaile, kuid ärimõju jääb häguseks.

---

## 📝 7. KOKKUVÕTE – vastused kolmele sünteesiküsimusele

### 7.1. Mis oli kõige üllatavam – mida tööandjad TEGELIKULT hindavad?

> **Tööandjad hindavad kõige rohkem kandidaadi võimet tõlkida andmetest tulenevad teadmised praktilisteks äriotsusteks ning seda oskust näitab kõige paremini varasemate projektide kirjeldus koos kvantifitseeritud tulemustega – mitte puhtalt tehniline nutikus.**

### 7.2. Millist soovitust annaksime Liisile värbamisprotsessi parandamiseks?

> **Soovitame lisada igasse vooru (CV‑sõel, tehniline intervjuu, personaliintervjuu) konkreetse ärikonteksti, kus kandidaat peab lahendama UrbanStyle’le tüüpilise probleemi (nt kampaania ROI analüüs, lao täiendamise ennustus). Samuti tuleks luua ühtne hindamiskaart (scorecard), et kõik intervjueerijad hindaksid samadel kriteeriumidel.**

### 7.3. Mis info puudub, mida peaksime veel uurima?

> **Puudub põhjalikum arusaam kandidaatide varasemast töökeskkonnast – kas nad on töötanud hajutatud meeskonnas, kuidas nad on toime tulnud ebaselgete nõuetega ja kuidas nad on kohanenud kiiresti muutuvas ärikeskkonnas. Soovitame lisada käitumuslikud küsimused, mis puudutavad just neid aspekte (nt “Räägi korrast, kus sa pidid muutma analüüsi suunda poole pealt”).**

---

## 📚 8. Lõplik koondpeatükk – täielik värbamisjuhendi peatükk

**PEATÜKK:** Kuidas hinnata andmeanalüütiku kandidaati terviklikult (CV, tehnilised oskused, pehmed oskused, koostöö)  
**Meeskond:** DACA rühm 9  
**UrbanStyle juht:** Liis Koppel (Operations Manager)

### 8.1. ÜLEVAADE
See peatükk annab UrbanStyle juhtkonnale ühtse raamistiku, kuidas hinnata andmeanalüütiku kandidaate CV, GitHubi portfoolio, tehniliste ja pehmete oskuste ning meeskonnasobivuse alusel. Terviklik lähenemine aitab vältida ühekülgset hindamist ja leida kandidaadid, kes toovad tehnilise kompetentsi kõrval ka reaalset ärikasu.

### 8.2. HINDAMISKRITEERIUMID (kõigi rollide vaatepunktist koondatud)
- **HR (roll A)** – kvantifitseeritud tulemused CV‑s, pinitud projektid LinkedInis, selge tehnoloogiapinge.
- **Tehniline (roll B)** – loetav ja testitud kood, dokumentatsioon, optimeeritud SQL ja Python, Git‑i head tavad.
- **Personalijuht (roll C)** – selge ärikommunikatsioon, loogiline probleemilahendus, koostöö märgid, kultuuriline sobivus (kasvav, paindlik keskkond).
- **Tiimijuht (roll D)** – iseseisvus, selgituste kvaliteet, panus meeskonda, arengupotentsiaal (nähtav progress portfoolios).

### 8.3. KONKREETSED NÄITED (UrbanStyle kontekst)
- Näiteks meie meeskonnas paistis silma analüütik, kes tuvastas müügiandmetes mustri, et teatud tootekategooriate müük langeb pärast hinnalangust 3 nädalat hiljem uuesti, ja soovitas hinnakujundust kohandada – see tõi kord kvartalis 12% kasvu. Tema kood oli hästi struktureeritud, README‑s oli selge ärikirjeldus ja ta oli kaasanud turundusmeeskonna koostöösse.
- Teine kandidaat demonstreeris iseseisvust, ehitades ise Power BI dashboardi, mis ühendas andmed nii veebipoest kui füüsilistest kassadest – ja lisas juhendi, kuidas seda igapäevaselt kasutada.

### 8.4. 3 VÕTMESOOVITUST JUHILE
1. **Lisa CV‑sõelumisse kohustuslik väli “Saavutused”** – iga töökogemuse juures peab olema vähemalt üks arvuline tulemus. Kui seda pole, lükka CV kohe kõrvale.
2. **Tehnilises voorus kasuta reaalseid UrbanStyle andmeid** (anonüümseks muudetud) ja lase kandidaadil koostada lühike analüüs 60 minuti jooksul – see annab kõige täpsema pildi tema pärisoskusest.
3. **Loo ühtne hindamistabel (scorecard)** kõigile intervjueerijatele, kus on 5‑pallised skaalad tehniliste, äri‑, suhtlus‑ ja koostöökriteeriumide alusel – see muudab otsuse objektiivsemaks ja võrreldavaks.

### 8.5. ÜLLATAV AVASTUS
> **Kõige üllatavam oli see, et kandidaadid, kellel oli silmapaistev tehniline GitHub, kukkusid sageli läbi ärikonteksti selgitamisel, samas kui mõõduka tehnilise tasemega kandidaadid, kes oskasid oma tööd selgelt ja tulemustele fokusseeritult esitleda, osutusid UrbanStyle’i jaoks edukamaks valikuks.**

---

**Dokumendi lõpp.**  
*Koostatud Nädala 9 sessiooni 2 raames. Kõik õigused kuuluvad meeskonnale ja UrbanStyle’ile.*
