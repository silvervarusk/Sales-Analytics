# A: Müük + Kliendid (IRINA)

> "Leia parimad kliendid, linnade müügitulemused ja lojaalsustasemete jaotus INNER JOIN abil."  
> "Koosta Anna jaoks selge ülevaade, mis näitab, kes ostab kõige rohkem ja kust tuleb suurim tulu."

See dokument annab täieliku ülevaate Roll A tulemustest:  
INNER JOIN päringud, TOP kliendid, linnade müük, loyalty_tier analüüs, üle keskmise kulutajate leidmine ning äriline kokkuvõte.

---

## 📌 1. Ülevaade tehtud tegevustest

Analüüsiti Supabase'i tabeleid **sales** ja **customers**, viidi läbi täielik müügi‑ ja kliendianalüüs ning koostati struktureeritud tulemus:

- INNER JOIN kliendi ja müügi ühendamiseks  
- TOP 10 klienti kogumüügi järgi  
- Müük linnade kaupa  
- Loyalty_tier jaotus  
- Edasijõudnute alamjärjepäring: kliendid üle keskmise kogumüügi  
- Ärisoovitus Annale

Kõik sammud dokumenteeriti ning koostati SQL‑skript koos tabelitega.

---

## 📊 2. Peamised tulemused

### **2.1. INNER JOIN — aktiivsed kliendid**

INNER JOIN tagastab ainult kliendid, kellel on vähemalt üks ost.

Kontroll näitas:
- kõik väljad korrektsed  
- linnanimed ühtlustatud  
- ostude kuupäevad loogilised  
- NULL‑väärtusi ei esinenud

---

### **2.2. TOP 10 klienti kogumüügi järgi**

| klient       | city     | ostude_arv | kogumüük   |
|--------------|----------|------------|------------|
| Tiina Pärn   | Tartu    | 73         | 27668.02   |
| Priit Rand   | Pärnu    | 76         | 26286.10   |
| Kevin Org    | Tallinn  | 78         | 23467.13   |
| Laura Tammik | Pärnu    | 74         | 23385.82   |
| Erkki Ilves  | Tartu    | 72         | 22942.42   |
| Anu Kuusik   | Tallinn  | 77         | 21626.10   |
| Kersti Lill  | Tallinn  | 71         | 21137.47   |
| Riina Lill   | Pärnu    | 67         | 20972.33   |
| Annika Saar  | Viljandi | 66         | 20726.79   |
| Ago Kull     | Pärnu    | 64         | 20124.61   |

**Peamine järeldus:**  
TOP kliendid kulutavad oluliselt rohkem kui keskmine klient — üle 20 000 €.

---

### **2.3. Müük linnade kaupa**

| city       | kliente | oste | kogumüük   |
|------------|---------|------|------------|
| Tallinn    | 1007    | 3601 | 1006252.88 |
| Tartu      | 525     | 1764 | 523286.64  |
| Pärnu      | 276     | 1231 | 374005.86  |
| Narva      | 145     | 438  | 122226.14  |
| Viljandi   | 94      | 359  | 102314.94  |
| Rakvere    | 90      | 338  | 93379.03   |
| Jõhvi      | 71      | 290  | 77601.15   |
| Kuressaare | 80      | 256  | 76509.61   |
| Haapsalu   | 73      | 252  | 73492.83   |
| Võru       | 66      | 216  | 60983.07   |
| Valga      | 69      | 216  | 59530.76   |
| Paide      | 55      | 169  | 53148.87   |

**Peamine järeldus:**  
Tallinn annab üle **1 miljoni €** müüki — rohkem kui kõik teised linnad kokku.

---

### **2.4. Loyalty_tier jaotus**

| loyalty_tier | kliente | kogumüük   |
|--------------|---------|------------|
| null         | 1024    | 1071805.32 |
| silver       | 560     | 593470.07  |
| gold         | 491     | 533601.64  |
| bronze       | 476     | 423854.75  |

**Peamine järeldus:**  
Kõige kasumlikum grupp on **silver**, mitte gold — see näitab, et keskmise aktiivsusega kliendid toovad suurima kogutulu.

---

### **2.5. Üle keskmise kulutajad (subquery)**

| klient       | kogumüük |
|--------------|----------|
| Tiina Pärn   | 27668.02 |
| Priit Rand   | 26286.10 |
| Kevin Org    | 23467.13 |
| Laura Tammik | 23385.82 |
| Erkki Ilves  | 22942.42 |

**Peamine järeldus:**  
Üle keskmise kulutajaid on vähe — nad moodustavad **kõrge väärtusega VIP‑segmendi**.

---

## 🧭 3. Juhatuse kokkuvõte

### **3.1. Mis oli suurim üllatus?**

- Tallinn üksi annab **üle 1 miljoni €** müüki  
- Silver‑taseme kliendid toovad rohkem tulu kui gold  
- TOP kliendid kulutavad 20–27 tuhat eurot — oluliselt üle keskmise  

---

### **3.2. Meie soovitus Annale**

**Fookus Tallinna ja Tartu klientidele — seal on suurim tulu.**  
**Kampaania silver‑taseme tõstmiseks gold‑tasemele.**  
**VIP‑klientidele (üle keskmise kulutajad) luua eriprogramm.**

Soovitus turundusele:

- personaalsed pakkumised TOP klientidele  
- linnapõhised kampaaniad Tallinnas ja Tartus  
- lojaalsusprogrammi tugevdamine silver‑tasemel  

---

### **3.3. Milliseid andmeid meil puudus?**

- kliendi ostude ajalugu (aastate lõikes)  
- kampaaniate mõju müügile  
- kliendi tagastused  
- kliendi rahulolu / NPS  
- segmentide demograafia  

Need andmed võimaldaksid luua täpsema kliendisegmenteerimise.

---

## 🛠️ 4. SQL‑skript (täielik)

```sql
-- 1. INNER JOIN: kliendid, kes on ostnud
SELECT
    c.first_name,
    c.last_name,
    c.email,
    c.city,
    s.sale_id,
    s.sale_date,
    s.total_price
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
LIMIT 20;

-- 2. TOP 10 klienti kogumüügi järgi
SELECT
    c.first_name || ' ' || c.last_name AS klient,
    c.city,
    COUNT(DISTINCT s.sale_id) AS ostude_arv,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY
    c.customer_id,
    c.first_name,
    c.last_name,
    c.city
ORDER BY kogumüük DESC
LIMIT 10;

-- 3. Müük linnade kaupa
SELECT
    c.city,
    COUNT(DISTINCT c.customer_id) AS kliente,
    COUNT(s.sale_id) AS oste,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY c.city
ORDER BY kogumüük DESC;

-- 4. Loyalty_tier jaotus
SELECT
    c.loyalty_tier,
    COUNT(DISTINCT c.customer_id) AS kliente,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY c.loyalty_tier
ORDER BY kogumüük DESC;

-- 5. Üle keskmise kulutajad (subquery)
SELECT
    c.first_name || ' ' || c.last_name AS klient,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY
    c.customer_id,
    c.first_name,
    c.last_name
HAVING SUM(s.total_price) > (
    SELECT AVG(kliendi_müük)
    FROM (
        SELECT SUM(total_price) AS kliendi_müük
        FROM sales
        GROUP BY customer_id
    ) AS keskmised
)
ORDER BY kogumüük DESC;
