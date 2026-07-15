# ROLL D: TURUNDUSKANALITE ANALÜÜS

## Metoodika

Analüüs põhines:

- turunduskanalite koondnäitajatel (GROUP BY)
- kanalite efektiivsusel (CTE)
- kuistel trendidel (DATE_TRUNC)
- kuust-kuusse kasvuanalüüsil (LAG() window function)

##### Tulemus annab hea ülevaate sellest, millised turunduskanalid toovad kõige rohkem käivet, kliente ja tellimusi ning kuidas nende tulemuslikkus ajas muutub.

---

## 📊 Turunduskanalite koondandmed

```sql
SELECT
    w.source AS turunduskanal,
    COUNT(DISTINCT c.customer_id) AS kliente,
    COUNT(DISTINCT o.sale_id) AS tellimusi,
    SUM(o.total_price) AS kogukäive,
    ROUND(AVG(o.total_price), 2) AS keskmine_tellimus
FROM sales o
JOIN customers c
    ON o.customer_id = c.customer_id
LEFT JOIN web_logs w
    ON c.customer_id = w.customer_id
GROUP BY w.source
ORDER BY kogukäive DESC;
```

<img width="362" height="415" alt="image" src="https://github.com/user-attachments/assets/a061681e-4aef-4e2a-a9e9-92100de80940" />

**Eesmärk:** võrrelda erinevate turunduskanalite klientide arvu, tellimusi ja käivet.

---

## 🎯 Kanali efektiivsus CTE-ga

```sql
WITH kanali_muuk AS (
    SELECT
        w.source AS turunduskanal,
        SUM(o.total_price) AS kogumuuk,
        COUNT(DISTINCT o.sale_id) AS tellimusi
    FROM sales o
    JOIN customers c
        ON o.customer_id = c.customer_id
    LEFT JOIN web_logs w
        ON c.customer_id::text = w.customer_id
    GROUP BY w.source
),
kanali_kliendid AS (
    SELECT
        w.source AS turunduskanal,
        COUNT(DISTINCT c.customer_id) AS kliente
    FROM customers c
    LEFT JOIN web_logs w
        ON c.customer_id::text = w.customer_id
    GROUP BY w.source
)
SELECT
    m.turunduskanal,
    k.kliente,
    m.tellimusi,
    m.kogumuuk,
    ROUND(
        m.kogumuuk / NULLIF(k.kliente, 0),
        2
    ) AS muuk_kliendi_kohta
FROM kanali_muuk m
JOIN kanali_kliendid k
    ON m.turunduskanal = k.turunduskanal
WHERE m.tellimusi > 100
ORDER BY muuk_kliendi_kohta DESC;
```

<img width="353" height="412" alt="image" src="https://github.com/user-attachments/assets/7a8f6f81-99ff-40fb-9348-4c8e763652cb" />

**Eesmärk:** leida kõige efektiivsem turunduskanal müügi kohta kliendi lõikes.

---

## 📈 Kampaaniate kuised trendid

```sql
SELECT
    w.source AS turunduskanal,
    DATE_TRUNC('month', o.sale_date) AS kuu,
    SUM(o.total_price) AS kogukaive,
    COUNT(DISTINCT o.customer_id) AS kliente,
    COUNT(DISTINCT o.sale_id) AS tellimusi
FROM sales o
JOIN customers c
    ON o.customer_id = c.customer_id
LEFT JOIN web_logs w
    ON c.customer_id::text = w.customer_id
GROUP BY
    w.source,
    DATE_TRUNC('month', o.sale_date)
HAVING COUNT(DISTINCT o.sale_id) > 20
ORDER BY
    kuu,
    kogukaive DESC;
```

<img width="399" height="411" alt="image" src="https://github.com/user-attachments/assets/f9289853-2d07-4453-8a78-07af6e6309da" />

**Eesmärk:** jälgida kanalite tulemuslikkust kuude lõikes.

---

## 🏆 Window Function kuust-kuusse kasvu leidmiseks

```sql
SELECT
    w.source AS turunduskanal,
    DATE_TRUNC('month', o.sale_date) AS kuu,
    SUM(o.total_price) AS kogukaive,
    LAG(
        SUM(o.total_price)
    ) OVER (
        PARTITION BY w.source
        ORDER BY DATE_TRUNC('month', o.sale_date)
    ) AS eelmise_kuu_kaive
FROM sales o
JOIN customers c
    ON o.customer_id = c.customer_id
LEFT JOIN web_logs w
    ON c.customer_id = w.customer_id
GROUP BY
    w.source,
    DATE_TRUNC('month', o.sale_date)
ORDER BY
    w.source,
    kuu;
```

<img width="337" height="412" alt="image" src="https://github.com/user-attachments/assets/58259a40-730a-49fe-aca0-8b758c723a6f" />

**Eesmärk:** võrrelda iga kanali käivet eelmise kuuga.

---

# Kokkuvõte

## Turunduskanalite tulemuslikkus 2023–2024

### 1. Google Organic on suurima käibega turunduskanal

- Käive: **863 240 €**
- Kliendid: **1 580**
- Tellimused: **3 378**
- Keskmine tellimus: **286 €**

### 2. Direct-liiklus toob stabiilselt tugevat müüki

- Käive: **599 438 €**
- Kliendid: **1 173**
- Tellimused: **3 864**
- Keskmine tellimus: **280 €**

### 3. Facebook Ads on üks olulisemaid tasulisi kanaleid

- Käive: **504 811 €**
- Kliendid: **1 016**
- Tellimused: **3 864**
- Keskmine tellimus: **284 €**

### 4. E-maili kampaaniad paistavad silma kliendi väärtuse poolest

- Käive kliendi kohta: **4 542 €**
- Kliendid: **878**
- Tellimused: **2 787**

### 5. Kuine trendianalüüs näitab, et Google Organic ja Direct on kõige järjepidevamad käivet loovad kanalid

- Google Organic oli vaadeldud perioodil enamasti suurima kuise käibega kanal.
- Direct säilitas stabiilse müügitaseme ning näitas mitmel kuul märkimisväärset kasvu võrreldes eelneva kuuga.

---

# Juhtkonna peamised järeldused

## Mis töötab hästi?

✅ Google'i orgaaniline liiklus on peamine käibeallikas.

✅ Direct-liiklus näitab tugevat brändi tuntust ja korduvostude osakaalu.

✅ Facebook Ads ja e-maili kampaaniad annavad tugeva panuse müüki ning on efektiivsed kliendikanalid.

## Millele tähelepanu pöörata?

⚠ Turunduskanalite nimetused ei ole andmetes ühtlustatud (näiteks Google, google, Google Organic, google_organic). See võib moonutada kanalite tegelikku võrdlust.

⚠ Mõnel kliendil võib olla mitu kirjet tabelis `web_logs`, mis võib põhjustada käibe topeltarvestust. Enne lõplike strateegiliste otsuste tegemist tuleks kontrollida atribuutsiooniloogikat.

⚠ Osa müügist võib olla seotud kanaliga `NULL`, mis tähendab, et tellimust ei saanud ühegi turundusallikaga seostada. See viitab võimalikule puudulikule jälgimisele.
