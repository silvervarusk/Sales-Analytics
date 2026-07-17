/* ---------------------------------------------------------
   ROLL B — KLIENDIGRUPPIDE ANALÜÜS (KOONDSKRIPT)
   Autor: Irina
   Kirjeldus: Ühtne skript, mis arvutab kliendi kogukäibe,
   määrab segmendi, tagastab segmentide jaotuse, TOP kliendid
   ja üle keskmise kulutajad.
--------------------------------------------------------- */

-----------------------------------------------------------
-- 1. Loo CTE: kliendi kogukäive + tellimuste arv + segment
-----------------------------------------------------------
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
),

segmenteeritud AS (
    SELECT
        customer_id,
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
)

-----------------------------------------------------------
-- 2. Tagasta segmenteeritud kliendid (põhitulemus)
-----------------------------------------------------------
SELECT *
FROM segmenteeritud
ORDER BY kogukäive DESC;


-----------------------------------------------------------
-- 3. Segmentide jaotus (VIP / Regular / Uus)
-----------------------------------------------------------
SELECT
    segment,
    COUNT(*) AS kliendiarv
FROM segmenteeritud
GROUP BY segment
ORDER BY kliendiarv DESC;


-----------------------------------------------------------
-- 4. TOP 10 klienti kogukäibe järgi
-----------------------------------------------------------
SELECT
    nimi,
    city,
    tellimuste_arv,
    kogukäive,
    segment
FROM segmenteeritud
ORDER BY kogukäive DESC
LIMIT 10;


-----------------------------------------------------------
-- 5. Üle keskmise kulutajad (subquery)
-----------------------------------------------------------
SELECT
    s.nimi,
    s.city,
    s.kogukäive,
    s.segment
FROM segmenteeritud s
WHERE s.kogukäive > (
    SELECT AVG(kogukäive)
    FROM segmenteeritud
)
ORDER BY s.kogukäive DESC;

