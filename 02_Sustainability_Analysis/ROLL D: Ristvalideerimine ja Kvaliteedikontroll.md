# Ristvalideerimine ja Andmekvaliteedi Kontroll  
### (sales, customers, products — Supabase)

> "Valideeri andmete terviklikkust TABELITE VAHEL — kas sales viitab olemasolevatele klientidele ja toodetele?"  
> "Leia orbid ja ebakõlad."

See projekt demonstreerib ristvalideerimise protsessi kolme põhitabeli vahel: **sales**, **customers**, **products**.  
Eesmärk oli tuvastada viidete terviklikkust, hinnaloogika ebakõlasid ja ärilisi anomaaliaid, mis mõjutavad müügi- ja kliendianalüüsi kvaliteeti.

---

## 📌 1. Projekti eesmärk

Ristvalideerimise eesmärk oli kontrollida:

- kas müügid viitavad olemasolevatele klientidele  
- kas müügid viitavad olemasolevatele toodetele  
- kas müügihind klapib toote jaehinnaga  
- kas on kliente, kes pole kunagi ostnud  
- kas on tooteid, mida pole kunagi müüdud  

Kõik tulemused dokumenteeriti ning koostati juhatuse‑tasemel kokkuvõte.

---

## 📊 2. Peamised avastused

### **2.1. Orbid kliendid**
**Tulemus:** 0 müüki viitab olematule kliendile  
→ kliendiviited on täielikud ja korrektsed.

### **2.2. Orbid tooted**
**Tulemus:** 0 müüki viitab olematule tootele  
→ tooteviited on täielikud.

### **2.3. Hinna ebakõlad**
**Tulemus:** 664 müügil ei klapi müügihind toote jaehinnaga  
→ see on kõige kriitilisem avastatud probleem.

### **2.4. Vaimkliendid (pole kunagi ostnud)**
**Tulemus:** 592 klienti pole kunagi ostnud  
→ võimalikud testandmed, vanad kirjed või mittetäielik kliendi elutsükkel.

### **2.5. Vaimtooted (pole kunagi müüdud)**
**Tulemus:** 12 toodet pole kunagi müüdud  
→ võimalikud uued tooted, lõpetatud tooted või vigased kirjed.

---

## 🧭 3. Juhatuse kokkuvõte

### **3.1. Mis oli suurim üllatus?**

Suurim üllatus oli **hinnaloogika massiivne ebakõla**:  
**664 müüki** ei klapi toote jaehinnaga.

See näitab, et:

- müügiarvestus ei ole usaldusväärne  
- marginaaliarvutused on valed  
- kampaaniate mõju ei ole mõõdetav  
- analüütika ei saa tugineda müügihindadele  

Kõik viited klientidele ja toodetele olid korrektsed — üllatavalt tugev andmekvaliteet selles osas.

---

### **3.2. Meie soovitus Toomasele**

Kõige kriitilisem probleem Toomase jaoks on **hinnaloogika ebakõla**.

Soovitame:

1. **Rakendada müügihinna valideerimise reegel**  
   - total_price = retail_price * quantity  
   - lubatud kõrvalekalle: ±1 EUR (allahindlused, ümardamine)

2. **Lisada allahindluse struktuur**  
   - discount_amount  
   - discount_percentage  
   - campaign_id  

3. **Luua automaatne kvaliteedikontroll (cron job / trigger)**  
   - tuvastab valed hinnad  
   - logib need eraldi tabelisse  
   - saadab alerti analüütikule

4. **Analüütikas kasutada ainult valideeritud müüke**  
   - vältida vigaste ridade sattumist KPI‑desse

---

### **3.3. Milliseid andmeid meil puudus?**

Analüüsi käigus selgus, et järgmised andmed oleksid andnud sügavama ja täpsema kvaliteedikontrolli:

- **Allahindluse info** (discount_amount, discount_percentage)  
- **Kampaaniate info** (campaign_id)  
- **Toote hinnalugu** (retail_price ajas)  
- **Müügi tüüp** (täishind, kampaania, hulgi, tagastus)  
- **Toote olek** (aktiivne / arhiveeritud)  
- **Kliendi segment** (B2C, B2B, VIP, uus klient)

Ilma nendeta ei saa hinnaloogika ebakõlasid äriliselt selgitada.

---

## 📈 4. Ristvalideerimise raport (kokkuvõte)

| Kategooria         | Probleeme | Kirjeldus                                   |
|--------------------|----------:|---------------------------------------------|
| Orbid kliendid     | 0         | Müük viitab olematule kliendile            |
| Orbid tooted       | 0         | Müük viitab olematule tootele              |
| Hinna ebakõlad     | 664       | Müügihind ei klapi toote jaehinnaga        |
| Vaimkliendid       | 592       | Klient ei ole kunagi ostnud                |
| Vaimtooted         | 12        | Toodet pole kunagi müüdud                  |
| **Kokku probleeme**| **1268**  |                                            |

---

## 🛠️ 5. SQL‑skript (täielik)

```sql
-- 1. Orbid kliendid
SELECT COUNT(*) AS orb_klient
FROM sales s
LEFT JOIN customers c ON s.customer_id = c.customer_id
WHERE c.customer_id IS NULL AND s.customer_id IS NOT NULL;

-- 2. Orbid tooted
SELECT COUNT(*) AS orb_toode
FROM sales s
LEFT JOIN products p ON s.product_id = p.product_id
WHERE p.product_id IS NULL AND s.product_id IS NOT NULL;

-- 3. Hinna ebakõlad
SELECT s.sale_id, s.total_price, p.retail_price, s.quantity,
s.total_price - (p.retail_price * s.quantity) AS erinevus
FROM sales s
JOIN products p ON s.product_id = p.product_id
WHERE ABS(s.total_price - (p.retail_price * s.quantity)) > 1
ORDER BY ABS(erinevus) DESC;

-- 4. Vaimkliendid
SELECT COUNT(*) AS vaimkliendid
FROM customers c
LEFT JOIN sales s ON c.customer_id = s.customer_id
WHERE s.customer_id IS NULL;

-- 5. Vaimtooted
SELECT COUNT(*) AS vaimtooted
FROM products p
LEFT JOIN sales s ON p.product_id = s.product_id
WHERE s.product_id IS NULL;


