# Ristvalideerimine ja Andmekvaliteedi Kontroll (sales, customers, products)

> "Valideeri andmete terviklikkust TABELITE VAHEL — kas sales viitab olemasolevatele klientidele ja toodetele?"  
> "Leia orbid ja ebakõlad."

See dokument annab juhatuse‑tasemel kokkuvõtte ristvalideerimise tulemustest kolme tabeli vahel: **sales**, **customers**, **products**.  
Fookus oli viidete terviklikkusel, hinnaloogika kontrollil ja äriliste ebakõlade tuvastamisel.

---

## 📌 1. Ülevaade tehtud tegevustest

Analüüsiti Supabase’i kolme tabelit ning kontrolliti:

- kas müügid viitavad olemasolevatele klientidele  
- kas müügid viitavad olemasolevatele toodetele  
- kas müügihind klapib toote jaehinnaga  
- kas on kliente, kes pole kunagi ostnud  
- kas on tooteid, mida pole kunagi müüdud  

Kõik sammud dokumenteeriti ning koostati ristvalideerimise raport koos SQL‑skriptiga.

---

## 📊 2. Peamised tulemused

### **2.1. Orbid kliendid**
```sql
SELECT COUNT(*) AS orb_klient
FROM sales s
LEFT JOIN customers c ON s.customer_id = c.customer_id
WHERE c.customer_id IS NULL AND s.customer_id IS NOT NULL;

