# UrbanStyle müügi- ja kliendianalüüsi projekt

**Autorid:** Irina, Silver ja Tiiu  
**Projekti kestus:** 10 nädalat  
**Eesmärk:** Aidata UrbanStyle’il ehitada andmepõhine müügi- ja kliendipilt alates andmekvaliteedist kuni automatiseeritud raportiteni.

---

## 📌 Projekti ülevaade

UrbanStyle on jaemüügiettevõte, kes soovis paremat arusaama oma müügist, klientidest ja laoseisust. Meie meeskond viis läbi täieliku andmeauditi, puhastas andmed, lõi visualiseeringud ja esitas juhatusele kolm andmepõhist soovitust.

---

## 📊 Andmeallikad

Analüüsisime nelja peamist andmeallikat:

- **Müük (sales)** – kõik müügitehingud
- **Kliendid (customers)** – kliendiandmed
- **Tooted (products)** – tootekataloog
- **Inventuur (inventory)** – laoseisud
- **Turunduskanalid** – Google Organic, TikTok, Google Ads jt

---

## 🧹 Andmete puhastamine

| Mõõdik | Tulemus |
|--------|---------|
| Algne müügiridade arv | 15 234 |
| Eemaldatud duplikaate | 5 116 |
| Pärast puhastamist | ~10 118 rida |

---

## 🔍 Peamised leiud

### 📈 Müük ja käive
- Aasta käive kasvas stabiilselt
- Tippkuu: **detsember (~170 623 €)**
- Suurim kategooria: **jalanõud (774 034 €)**
- Järgnevad: meeste- ja naisteriided

### 👥 Kliendid
- Kokku **3 150 klienti**
- **595 (19%)** pole kunagi ostnud
- Väike **VIP-grupp (~10–20 klienti)** toob ebaproportsionaalselt suure osa käibest (igaüks >20 000 €)

### 🧥 Tooted ja inventuur
- **362 toodet**, **5 kategooriat**
- **12 toodet** pole kunagi müüdud
- Jalanõud, meeste- ja naisteriided on edukaimad
- Aksessuaarid ja lasteriided seovad kapitali, kuid liiguvad aeglaselt

### 📣 Turunduskanalid
- Juhtiv kanal: **Google Organic (~8,6 mln € auditeeritud käive)**
- TikTok ja Google Ads kasvavad, kuid ei ole veel põhivedurid

### ⚠️ Suurim üllatus
Näiv "müügilangus" aastatel 2025–2026 osutus **andmelüngaks** (9 kuud andmeid puudu), mitte päris äriprobleemiks.

---

## 📊 Visualiseeringud

### 1. Müügitrend kuude kaupa (2024–2025)
![Müügitrend](link_graafikule)

**So what?**  
Otsuseid ei tohi teha ainult 2025. aasta graafiku põhjal – enne tuleb andmed korrastada. Fookus peab jääma 2024. aasta tõestatud kasvule.

---

### 2. Kategooriate käive
![Kategooriate käive](link_graafikule)

**So what?**  
Juhatus saab selge ülevaate, kuhu suunata laovaru ja turunduseelarve. Aksessuaarid ja lasteriided vajavad optimeerimist.

---

### 3. Kliendisegmendid (RFM)
![Kliendisegmendid](link_graafikule)

**So what?**  
Näha on väike, kuid väga väärtuslik VIP-klientide grupp ja suur At-Risk/Uus segment, kus peitub ettevõtte kiireim kasvupotentsiaal.

---

## 💡 Soovitused juhatusele

### 1️⃣ VIP ja At-Risk kliendid fookusesse
**Tegevus:** Käivitage VIP-lojaalsusprogramm ja sihitud win-back kampaania At-Risk klientidele.  
**Põhjendus:** Väike VIP-grupp toob väga suure osa käibest, samal ajal 595 klienti pole kunagi ostnud – siin on kiireim lisatulu potentsiaal.

---

### 2️⃣ Sortimendi ja laovaru korrastamine
**Tegevus:** Vaadake kriitiliselt üle aksessuaaride ja lasteriiete sortiment ning likvideerige 12 müümata toodet.  
**Põhjendus:** Need kategooriad seovad kapitali, kuid ei anna proportsionaalset käivet – optimeerimine vabastab sularaha ja lihtsustab inventuuri.

---

### 3️⃣ Automatiseeritud aruandlus
**Tegevus:** Võtke kasutusele loodud Python-pipeline, mis jookseb kord nädalas (API → puhastus → RFM → raport).  
**Põhjendus:** Praegune käsitöö võtab ~4 tundi nädalas. Automatiseerimine säästab aega, vähendab inimlike vigade riski ja annab juhatusele alati värsked numbrid.

---

## 🤖 AI kasutamine meeskonna töös

AI oli meie tiimi jaoks praktiline tööriist, mitte "maagiline lahendus".

| Valdkond | Kuidas AI aitas |
|----------|-----------------|
| **SQL ja Python debugimine** | Kontrollis keerulisemaid päringuid (duplikaadid, RFM kvintiilid, window-funktsioonid) – vähendas vigade arvu |
| **Aruannete struktureerimine** | Aitas sõnastada raportite tehnilist teksti, kuid ärisoovitused sõnastasime ise |
| **Arhitektuuri valideerimine** | API-päringute ja veakäsitluse parimate praktikate kontroll |

**Õppetund:**  
> *"AI on suurepärane partner tehnilistes detailides, aga vastutus numbrite, ärikonteksti ja otsuste eest jääb alati meile."*

---

## 🛠️ Kasutatud tehnoloogiad

- **SQL** – andmete pärimine ja puhastamine
- **Python** – RFM-analüüs, puhastus, automatiseerimine
- **Power BI / Plotly** – visualiseeringud
- **GitHub** – koodihaldus ja koostöö
- **AI-assistent** – debugimine ja struktureerimine

---

## 📁 Repositooriumi struktuur

|UrbanStyle_Analytics/|
|├── data/|
|│ ├── raw/ # algandmed|
|│ └── cleaned/ # puhastatud andmed|
|├── notebooks/|
|│ ├── 01_data_cleaning.ipynb|
|│ ├── 02_eda.ipynb|
|│ └── 03_rfm_analysis.ipynb|
|├── reports/|
|│ └── urbanstyle_juhatuse_aruanne.pdf|
|├── pipeline/|
|│ ├── data_fetcher.py|
|│ ├── transform.py|
|│ └── main.py|
|├── visuals/|
|│ └── dashboard.pbix|
|└── README.md|


---

## 👥 Meeskond

- **Irina** – andmete puhastamine, SQL, Python
- **Silver** – visualiseeringud, Power BI, dashboardid
- **Tiiu** – RFM-analüüs, kliendisegmenteerimine, esitlus

---

## 📅 Projekti ajatelg

| Nädal | Tegevus |
|-------|---------|
| 1–2 | Andmete audit ja puhastamine |
| 3–4 | JOIN-analüüs ja andmete rikastamine |
| 5–6 | RFM-segmentatsioon ja kliendianalüüs |
| 7–8 | Visualiseeringud ja dashboardid |
| 9–10 | Automatiseerimine ja juhatuse esitlus |

---

## 🏁 Kokkuvõte

UrbanStyle’i projekt andis meile väärtusliku kogemuse töötada reaalsete andmetega alates toorandmetest kuni äriotsusteni. Tuvastasime andmelüngad, puhastasime kvaliteedi, lõime visualiseeringud ja esitasime kolm mõõdetavat soovitust.

> **"Andmed on väärtuslikud alles siis, kui nende põhjal tehakse paremaid otsuseid."**

---

📧 **Kontakt:** urbanstyle.analytics@gmail.com  
🔗 **GitHub:** https://github.com/urbanstyle-analytics
