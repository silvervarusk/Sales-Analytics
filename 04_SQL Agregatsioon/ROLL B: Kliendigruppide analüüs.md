# Kliendigruppide Analüüs (Customer Segmentation) IRINA
### Supabase — customers + sales

> "Segmenteeri kliendid kulutuse järgi (VIP / Regular / Uus), leia TOP kliendid ja koosta kliendiprofiili kokkuvõte Annale."

See projekt demonstreerib kliendigruppide analüüsi, kus kliendid segmenteeritakse kogukulutuse alusel.  
Eesmärk oli tuvastada kõige väärtuslikumad kliendid, mõista kliendikäitumist ja luua segmentide kaupa selge äriline ülevaade.

---

## 📌 1. Projekti eesmärk

Kliendigruppide analüüsi eesmärk oli:

- arvutada iga kliendi kogukäive  
- määrata kliendid segmentidesse (VIP / Regular / Uus)  
- tuvastada TOP kliendid  
- koostada kliendiprofiili kokkuvõte  
- anda juhatusele selge ülevaade kliendibaasi struktuurist  

Segmentide loogika:

- **VIP** — kogukäive > 20 000 €  
- **Regular** — kogukäive > 5 000 €  
- **Uus** — kogukäive ≤ 5 000 €

Kõik tulemused dokumenteeriti ning koostati kokkuvõte.

---

## 📊 2. Peamised avastused

### **2.1. VIP kliendid**
VIP‑kliendid moodustavad väikese, kuid äärmiselt väärtusliku segmendi.

**TOP 10 VIP kliendid:**

| Nimi | Linn | Tellimusi | Kogukäive | Segment |
|------|------|-----------|-----------|---------|
| Tiina Pärn | Tartu | 73 | 27 668.02 | VIP |
| Priit Rand | Pärnu | 76 | 26 286.10 | VIP |
| Kevin Org | Tallinn | 78 | 23 467.13 | VIP |
| Laura Tammik | Pärnu | 74 | 23 385.82 | VIP |
| Erkki Ilves | Tartu | 72 | 22 942.42 | VIP |
| Anu Kuusik | Tallinn | 77 | 21 626.10 | VIP |
| Kersti Lill | Tallinn | 71 | 21 137.47 | VIP |
| Riina Lill | Pärnu | 67 | 20 972.33 | VIP |
| Annika Saar | Viljandi | 66 | 20 726.79 | VIP |
| Ago Kull | Pärnu | 64 | 20 124.61 | VIP |

VIP‑kliendid ostavad tihti, suure summa eest ja on lojaalsed.

---

### **2.2. Regular kliendid**
Regular segment on lai ja moodustab suure osa kliendibaasist.

- Kogukäive 5 000–20 000 €  
- Stabiilne ostusagedus  
- Suur potentsiaal tõusta VIP‑segmenti  

Regular kliendid on ettevõtte kasvumootor.

---

### **2.3. Uus kliendid**
Uus segment on kõige suurem, kuid madala kogukäibega.

- Kogukäive < 5 000 €  
- Varajane kliendisuhe  
- Vajavad aktiveerimist  

Uus segment vajab turunduslikku toetust ja "onboarding" strateegiat.

---

## 🧭 3. Juhatuse kokkuvõte

### **3.1. Mis oli suurim üllatus?**

Suurim üllatus oli **VIP‑kliendi profiili tugevus**:

- VIP‑kliendid ostavad **kümneid kordi**  
- kulutavad **üle 20 000 €**  
- moodustavad väikese, kuid ülikõrge väärtusega segmendi  

Lisaks oli üllatav, et **Regular segment on väga lai**, mis tähendab suurt potentsiaali VIP‑segmenti kasvatamiseks.

---

### **3.2. Meie soovitus Kristile**

#### **1. Luua VIP‑programm**
- personaalne kliendihaldur  
- eksklusiivsed pakkumised  
- varajane ligipääs uutele toodetele  

#### **2. Aktiveerida Regular segmenti**
- kordusostu kampaaniad  
- ostusageduse tõstmise programmid  
- punktisüsteem  

#### **3. Kasvatada Uut segmenti**
- esmaostu soodustused  
- automaatne onboarding  
- personaalsed soovitused  

VIP‑kliendid toovad kõige suurema tulu, Regular kliendid kõige suurema kasvupotentsiaali.

---

### **3.3. Milliseid andmeid meil puudus?**

Analüüsi käigus selgus, et järgmised andmed oleksid andnud veel täpsema kliendiprofiili:

- kliendi **vanus**  
- kliendi **sugu**  
- kliendi **registreerimise kuupäev**  
- kliendi **kanal** (veeb, pood, kampaania)  
- kliendi **segmendi muutused ajas**  
- kliendi **toote-eelistused**  
- kliendi **tagastuste info**

Need andmed võimaldaksid luua:

- täpsemaid segmente  
- personaalseid pakkumisi  
- kliendi elutsükli analüüsi  

---

## 📈 4. Segmentide kokkuvõtte tabel

| Segment | Kogukäive | Tellimuste arv | Profiil |
|--------|-----------|----------------|---------|
| **VIP** | > 20 000 € | Väga kõrge | lojaalsed, suur tulu |
| **Regular** | 5 000–20 000 € | Keskmine | kasvupotentsiaal |
| **Uus** | < 5 000 € | Madal | vajab aktiveerimist |

---

## 🧩 5. Lühike juhatuse kokkuvõte ühes lõigus

Kliendigruppide analüüs näitas, et VIP‑kliendid moodustavad väikese, kuid äärmiselt väärtusliku segmendi, mis toob kõige suurema tulu. Regular segment on lai ja pakub suurt kasvupotentsiaali, samas kui Uus segment vajab aktiivset kaasamist. Soovitame Toomasele luua VIP‑programmi, tugevdada Regular segmenti kordusostu kampaaniatega ning arendada Uus segmenti onboarding‑pakkumistega. Täiendavad demograafilised ja käitumuslikud andmed võimaldaksid segmente veelgi täpsemaks muuta.

---

## 🛠️ 6. SQL‑skriptid (kõik rolli B päringud)

```sql
-- 1. Kliendi kogukäibe arvutamine + segmentide määramine (CTE)
WITH kliendi_kokkuvote AS (
    SELECT
        c.customer_id,
        c.first_name || ' ' || c.last_name AS nimi,
        c.city,
        COUNT(o.sale_id) AS tellimuste_arv,
        SUM(o.total_price) AS kogukäive
    FROM customers c
    JOIN sales o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id, c.first_name, c.last_name, c.city
)
SELECT
    nimi,
    city,
    tellimuste_arv,
    kogukäive,
    CASE
        WHEN kogukäive > 20000 THEN 'VIP'
        WHEN kogukäive > 5000 THEN 'Regular'
        ELSE 'Uus'
    END AS segment
FROM kliendi_kokkuvote
ORDER BY kogukäive DESC;

-- 2. TOP VIP kliendid (kui eraldi vaja)
WITH kliendi_kokkuvote AS (
    SELECT
        c.customer_id,
        c.first_name || ' ' || c.last_name AS nimi,
        c.city,
        COUNT(o.sale_id) AS tellimuste_arv,
        SUM(o.total_price) AS kogukäive
    FROM customers c
    JOIN sales o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id, c.first_name, c.last_name, c.city
)
SELECT *
FROM kliendi_kokkuvote
WHERE SUM(total_price) > 20000
ORDER BY kogukäive DESC
LIMIT 10;

-- 3. Segmentide jaotuse kokkuvõte
WITH kliendi_kokkuvote AS (
    SELECT
        c.customer_id,
        SUM(o.total_price) AS kogukäive
    FROM customers c
    JOIN sales o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id
)
SELECT
    CASE
        WHEN kogukäive > 20000 THEN 'VIP'
        WHEN kogukäive > 5000 THEN 'Regular'
        ELSE 'Uus'
    END AS segment,
    COUNT(*) AS klientide_arv
FROM kliendi_kokkuvote
GROUP BY segment
ORDER BY klientide_arv DESC;
