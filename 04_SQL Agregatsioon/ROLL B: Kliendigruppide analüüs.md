##ROLL B — KLIENDIGRUPPIDE ANALÜÜS (IRINA)

# Kliendigruppide Analüüs (Customer Segmentation)  
### Supabase — customers + sales

> "Segmenteeri kliendid kulutuse järgi (VIP / Regular / Uus), leia TOP kliendid ja koosta kliendiprofiili kokkuvõte Annale."

See projekt demonstreerib kliendigruppide analüüsi, kus kliendid segmenteeritakse kogukulutuse alusel.  
Töö sisaldab:  
- kliendi kogukäibe arvutamist  
- segmentide määramist (VIP / Regular / Uus)  
- TOP klientide leidmist  
- kliendiprofiili kokkuvõtet  
- SQL‑põhist analüüsi, mis sobib andmeanalüütiku portfooliosse

---

## 📌 1. Projekti eesmärk

Eesmärk oli luua selge kliendisegmenteerimise mudel, mis toetab:

- müügi- ja turundusotsuseid  
- VIP‑klientide tuvastamist  
- kliendikäitumise mõistmist  
- personaalse kommunikatsiooni loomist  
- kliendihalduse prioriseerimist

Segmentide loogika:

- **VIP** — kogukäive > 20 000 €  
- **Regular** — kogukäive > 5 000 €  
- **Uus** — kogukäive ≤ 5 000 €

---

## 📊 2. Kasutatud SQL‑loogika (CTE)

```sql
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
