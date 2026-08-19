## UrbanStyle.ltd värbamisjuhend: (Roll B)

### 1. Koodi kvaliteet ja struktuur

Tehniline intervjueerija peab koodi vaadates nägema süsteemsust. Tehnilise intervjueerija eesmärk on hinnata, kas andmeanalüütiku (DA) kandidaat oskab kirjutada loetavat, struktureeritud ja taaskasutatavat koodi ning kasutada analüüsitööks sobivaid tööriistu. Lisaks tehnilistele oskustele näitab GitHubi repo kandidaadi töökorraldust, dokumenteerimisoskust ja võimet oma lahendusi teistele arusaadavalt esitleda.


**Loetavus:**


Muutujate ja funktsioonide nimed peaksid olema arusaadavad ning kood peaks olema loogiliselt üles ehitatud. Väiksemad funktsioonid on eelistatud väga pika ja keerulise koodiploki asemel. Kas kandidaat kasutab suuri tähti märksõnade jaoks (nt SELECT, FROM, JOIN)? 
Kas päringud on jaotatud ridadele nii, et loogika on jälgitav, mitte üks pikk tekstijada?
.

**Struktuur:** 

hea lahendus eraldab näiteks andmete laadimise, töötlemise ja visualiseerimise. UrbanStyle OÜ projekti puhul võiksid need olla näiteks eraldi moodulites data_fetcher.py, transform.py ja visualize_export.py, mida ühendab pipeline.py. 
.

**Kommentaarid ja docstring'id:**

kommentaarid peaksid selgitama miks midagi tehakse, mitte lihtsalt kordama koodi. Funktsioonidel võiks olla docstring, mis kirjeldab nende eesmärki, sisendit ja väljundit.
.

### 2. Tööriistade tundmine

Kandidaat peab tõestama, et ta valdab UrbanStyle'i tehnoloogilist stacki
:

**SQL:**
Peab valdama JOIN tüüpe, GROUP BY agregaatfunktsioone ja soovitavalt ka CTE (Common Table Expressions) kasutamist keerukama loogika puhul
.

**Python & pandas:**
oluline on pandas'e kasutamine andmete puhastamiseks (duplikaatide ja NULLide käsitlemine) ja analüüsimiseks, funktsioonide loomine, tingimuslaused, veakäsitlus ning vajadusel moodulite kasutamine. Tugev kandidaat oskab näiteks Supabase'ist andmeid pärida, neid pandas'ega töödelda ja tulemused failidesse eksportida.
.

**GitHub:** 
Portfoolio peab olema avalik ja hästi struktureeritud (iga nädal eraldi kaustas)
. 
Vaadata tuleks, kas kandidaat kasutab version control'i järjepidevalt, teeb loogilisi commit'e ja kirjutab commit-sõnumeid, millest on aru saada, mida muudeti.

**Power BI / Plotly:** 
kandidaat peaks oskama valida analüüsiküsimusele sobiva visualiseerimise ning esitada tulemusi selgelt. Näiteks UrbanStyle'i müügiandmete puhul võiks näidata nädalast müügitulu, KPI-sid või Top 10 toodet.


### 3. Dokumentatsioon ja GitHub

Hea GitHubi repo sisaldab README-d, mis selgitab projekti eesmärki, kasutatud tehnoloogiaid, andmete allikat, projekti struktuuri ja projekti käivitamise juhiseid. Vajadusel peaks README sisaldama ka näiteid väljunditest.
Kuna andmeanalüütik on sild tehnoloogia ja äri vahel, on dokumentatsioon kriitiline
.
README.md failid: Igal projektil peab olema kirjeldus: mis on äriprobleem, milliseid tööriistu kasutati ja mis oli peamine järeldus
.
Commit sõnumid: "Update" ei ole piisav. Commit-sõnumid peaksid olema konkreetsed, näiteks:

Add sales data cleaning function
Fix date filtering in data fetcher
Add weekly revenue visualization
Sellised sõnumid annavad intervjueerijale ülevaate projekti arengust.

**3 Rohelist lippu (Tugev kandidaat)**

Andmete valideerimise mentaliteet: Kandidaat ei hüppa kohe analüüsi juurde, vaid kontrollib esmalt ridade arvu, unikaalseid väärtuseid ja NULLide osakaalu
.

Äriliselt kvantifitseeritud tulemused: Ta ei ütle "leidsin VIPid", vaid "tuvastasin 424 VIP-klienti, kes annavad 42% UrbanStyle'i käibest"
.

Automatiseerimise huvi: Kandidaat on loonud skripte või pipeline'e, mis muudavad korduva töö (nt iganädalane RFM-analüüs) automaatseks
.


**2 Punast lippu (Hoiatusmärgid)**

Turvavead (Critical): API-võtmed või andmebaasi paroolid on jäetud otse koodi, mitte peidetud .env faili
.

"Must kast" analüüs: Koodis puuduvad selgitused ja README ei kirjelda, kuidas kandidaat tulemuseni jõudis. See tähendab, et teised meeskonnaliikmed ei saa tema tööd jätkata
.

Kood töötab ainult kandidaadi enda arvutis. Puuduvad juhised, sõltuvuste kirjeldus või korrektne projekti struktuur ning kandidaat ei oska selgitada, kuidas teine inimene projekti käivitaks.


