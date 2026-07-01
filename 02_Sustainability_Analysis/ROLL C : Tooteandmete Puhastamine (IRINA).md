# Tooteandmete Puhastamise Kokkuvõte (Supabase / SQL)

> "Leia duplikaadid, NULL väärtused ja ebajärjekindlused products tabelis."  
> "Loo test koopia ja dokumenteeri probleemid."

See dokument annab juhatuse‑tasemel ülevaate tooteandmete puhastamise tulemustest, tuvastatud probleemidest ja soovitustest andmekvaliteedi tõstmiseks.

---

## 📌 1. Ülevaade tehtud tegevustest

Analüüsiti Supabase'i tabelit **products**, loodi turvaline testkoopia ning viidi läbi täielik andmekvaliteedi kontroll neljal kriitilisel tasemel:

- duplikaatsed tootenimed  
- NULL‑väärtused  
- hinnaloogika vead  
- kategooriate järjekindlus  

Kõik sammud dokumenteeriti ning koostati puhastamisraport koos SQL‑skriptiga.

---

## 📊 2. Peamised tulemused

### **2.1. Testtabel**
- Loodi: `products_test`  
- Ridade arv: **362**

### **2.2. Duplikaatsed tootenimed**
- Leitud: **12 duplikaati**  
- Kõige olulisem avastus, mis mõjutab analüüsi täpsust.

### **2.3. NULL‑väärtused**
- Kõik kriitilised väljad olid täidetud  
- **0 NULL‑i** (nimi, kategooria, jaehind, omahind)

### **2.4. Hinnaloogika**
- Negatiivseid hindu: **0**  
- Äärmuslikke hindu (>1000€): **0**

### **2.5. Kategooriate järjekindlus**
Leitud **5 kategooriat**:

- aksessuaarid  
- jalanõusid  
- laste_riided  
- meeste_riided  
- naiste_riided  

Kategooriate kirjapilt oli ühtlane — ei esinenud “Shoes vs shoes” tüüpi probleeme.

---

## 🧭 3. Juhatuse kokkuvõte

### **3.1. Mis oli suurim üllatus?**

Suurim üllatus oli see, et **kriitilisi vigu ei olnud üldse**:  
- ei olnud NULL‑väärtusi  
- ei olnud hinnavigu  
- kategooriad olid ühtlased  

Ainus oluline probleem oli **12 duplikaatset tootenime**, mis mõjutab otseselt müügi‑ ja marginaalianalüüsi.

---

### **3.2. Meie soovitus Toomasele**

**Rakendada duplikaatide ennetamise ja puhastamise protsess**, mis sisaldab:

- unikaalse `product_id` kasutamist analüütikas  
- duplikaatide automaatset tuvastamist (trigger / cron job)  
- tootenimede standardiseerimist (bränd + mudel + variatsioon)  
- reegel: *üks toode = üks kirje*

Lisasoovitus:  
Rakendada kategooriate standardiseerimise CASE‑loogika:

**[CASE‑standardiseerimine](ca://s?q=Selgita_kategooriate_CASE_standardiseerimist)**

---

### **3.3. Milliseid andmeid meil puudus?**

Analüüsi käigus selgus, et järgmised andmed oleksid andnud sügavama kvaliteedikontrolli:

- **product_id** (unikaalne identifikaator)  
- **hinnamuutuste ajalugu**  
- **ametlik kategooriate taksonoomia**  
- **toote olek (aktiivne/arhiveeritud)**  
- **bränd / mudel / variatsioonid**

Need andmed võimaldaksid tulevikus luua automaatse kvaliteedikontrolli ja täpsema analüüsi.

---

## 📈 4. Puhastamisraport (kokkuvõte)

| Kategooria                 | Probleeme | Kirjeldus                                   |
|---------------------------|----------:|---------------------------------------------|
| Duplikaatsed nimed        | 12        | Sama tootenimi esineb mitu korda           |
| NULL nimi/hind            | 0         | Kõik kriitilised väljad olemas             |
| Loogilised vead           | 0         | Pole negatiivseid ega äärmuslikke hindu    |
| Ebajärjekindlad kategooriad | 0       | Pole juhtumeid stiilis Shoes vs shoes      |
| NULL omahind/kategooria   | 0         | Klassifitseerimine olemas                  |
| **Kokku probleeme**       | **12**    |                                            |

---

## 🛠️ 5. SQL‑skript (täielik)

```sql
-- 1. Loo test koopia
CREATE TABLE IF NOT EXISTS products_test AS
SELECT * FROM products;

-- 2. Ridade arv
SELECT COUNT(*) AS ridade_arv
FROM products_test;

-- 3. Duplikaatsete tootenimede leidmine
SELECT
    product_name,
    COUNT(*) AS koopiate_arv
FROM products_test
GROUP BY product_name
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;

-- 4. NULL-väärtuste kontroll
SELECT
    COUNT(*) FILTER (WHERE product_name IS NULL OR product_name = '') AS null_nimi,
    COUNT(*) FILTER (WHERE category IS NULL OR category = '') AS null_kategooria,
    COUNT(*) FILTER (WHERE retail_price IS NULL) AS null_jaehind,
    COUNT(*) FILTER (WHERE cost_price IS NULL) AS null_omahind
FROM products_test;

-- 5. Loogilised hinnavead
SELECT COUNT(*) AS negatiivne_hind
FROM products_test
WHERE retail_price < 0;

SELECT product_name, retail_price
FROM products_test
WHERE retail_price > 1000
ORDER BY retail_price DESC;

-- 6. Kategooriate jaotus
SELECT category, COUNT(*) AS arv
FROM products_test
GROUP BY category
ORDER BY category;

-- 7. Vormingu ühtlustamine
UPDATE products_test
SET category = INITCAP(TRIM(category))
WHERE category != INITCAP(TRIM(category));

-- 8. Standardiseerimine CASE abil
UPDATE products_test
SET category = CASE
    WHEN LOWER(TRIM(category)) IN ('shoes', 'jalanõud', 'footwear') THEN 'Shoes'
    WHEN LOWER(TRIM(category)) IN ('shirts', 'särgid', 'tops')      THEN 'Shirts'
    WHEN LOWER(TRIM(category)) IN ('pants', 'püksid', 'trousers')   THEN 'Pants'
    ELSE INITCAP(TRIM(category))
END;

-- 9. Lõplik kategooriate kontroll
SELECT category, COUNT(*) AS arv
FROM products_test
GROUP BY category
ORDER BY category;







