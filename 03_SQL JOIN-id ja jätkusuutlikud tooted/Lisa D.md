## Alaülesanne D – Müügikanalite ja klientide analüüs

### 1. Millistest linnadest kliendid kasutavad erinevaid müügikanaleid?

Selles päringus ühendan tabelid **sales** ja **customers**, et analüüsida, millistes linnades kasutatakse enim erinevaid müügikanaleid.

```sql
SELECT
    s.channel AS müügikanal,
    c.city AS linn,
    COUNT(DISTINCT c.customer_id) AS kliente,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY s.channel, c.city
ORDER BY müügikanal, kogumüük DESC;
```

<details>
<summary>Tulemus (click to expand)</summary>

<img width="287" height="444" alt="image" src="https://github.com/user-attachments/assets/b6d79427-3430-41bf-899e-47dc1516367d" />

</details>

---

### 2. Müügikanal ja tootekategooria (3 tabeli JOIN)

Selles päringus ühendan tabelid **sales**, **customers** ja **products**, et võrrelda müügikanalite tulemuslikkust erinevate tootekategooriate lõikes.

```sql
SELECT
    s.channel AS müügikanal,
    p.category AS tootekategooria,
    COUNT(DISTINCT c.customer_id) AS kliente,
    COUNT(s.sale_id) AS oste,
    SUM(s.total_price) AS kogumüük,
    ROUND(AVG(s.total_price), 2) AS keskmine_ost
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
INNER JOIN products p
    ON s.product_id = p.product_id
GROUP BY s.channel, p.category
ORDER BY müügikanal, kogumüük DESC;
```

<details>
<summary>Tulemus (click to expand)</summary>

<img width="496" height="450" alt="image" src="https://github.com/user-attachments/assets/46fbb5a1-52fb-4f97-9ae9-be84d90b41dd" />

</details>

---

### 3. Kõige efektiivsem müügikanal

Mõõdan müügikanali efektiivsust valemiga:

**Müük kliendi kohta = kogumüük ÷ klientide arv**

```sql
SELECT
    s.channel AS müügikanal,
    COUNT(DISTINCT s.customer_id) AS kliente,
    SUM(s.total_price) AS kogumüük,
    ROUND(
        SUM(s.total_price) /
        NULLIF(COUNT(DISTINCT s.customer_id), 0),
        2
    ) AS müük_per_klient
FROM sales s
GROUP BY s.channel
ORDER BY müük_per_klient DESC;
```

<details>
<summary>Tulemus (click to expand)</summary>

<img width="307" height="447" alt="image" src="https://github.com/user-attachments/assets/5435cc93-42b1-4a77-b583-77a862134ba8" />

</details>

---

## Tulemuste analüüs

### Milline kanal toob enim müüke?

✅ **Pood**

- Pood: **1 902 430,30 €**
- Online: **1 006 747,68 €**

Pood genereerib ligikaudu **89% rohkem käivet** kui online kanal.

---

### Milline kanal toob enim kliente?

✅ **Pood**

- Pood: **2 278 klienti**
- Online: **1 706 klienti**

Pood teenindab **572 klienti rohkem**, mis tähendab umbes **34% suuremat kliendibaasi**.

---

### Milline kanal on kõige efektiivsem?

✅ **Pood**

| Müügikanal | Kliente | Kogumüük (€) | Müük kliendi kohta (€) |
|------------|---------:|-------------:|----------------------:|
| Pood | 2278 | 1 902 430,30 | 835,13 |
| Online | 1706 | 1 006 747,68 | 590,12 |

Poe klient kulutab keskmiselt **245,01 € rohkem** kui online klient.

See tähendab, et poe kliendi väärtus on ligikaudu **41,5% kõrgem**.

---

## Linnade võrdlus

Linnade analüüs näitab, et müügikanalite kasutus erineb piirkonniti. Mõnes linnas domineerivad füüsilise poe ostud, samas kui teistes kasutatakse aktiivsemalt online kanalit.

Selline vahe võib olla seotud:

- klientide ostuharjumustega;
- poe asukohaga ja ligipääsetavusega;
- kohalike turunduskampaaniatega;
- toodete saadavusega.

Linnade detailsem analüüs võimaldab tuvastada piirkonnad, kus online müüki või poe külastatavust saab veel kasvatada.

---

## Järeldused

Analüüsi põhjal on **füüsiline pood kõige tugevam müügikanal**, sest:

- toob rohkem kliente;
- teenib suurema kogukäibe;
- saavutab kõrgema müügi kliendi kohta;
- on efektiivsem nii müügitulemuste kui ka kliendiväärtuse poolest.

Poe kliendid ostavad keskmiselt kallimaid või suurema väärtusega tooteid kui online kliendid.

---

## Soovitus

🎯 **Suurendada investeeringuid füüsilise poe arendamisse**, sest selle tasuvus on praeguste andmete põhjal kõige kõrgem.

Soovitatavad tegevused:

- suurendada poe külastatavust kampaaniate abil;
- tugevdada lojaalsusprogrammi;
- tõsta enim müüdud toodete nähtavust kaupluses;
- kasutada online kanalit uute klientide leidmiseks;
- suunata online kliendid soodustuste ja pakkumiste abil suurema ostukorvi väärtuseni.

---

## Kvaliteedikontroll

✅ Kasutatud on 3 tabeli JOIN-i (`sales`, `customers`, `products`)  
✅ Võrreldud on klientide arvu, kogumüüki ja kanali efektiivsust  
✅ Arvutatud on müük kliendi kohta  
✅ Tulemused on tõlgendatud ärilisest vaatenurgast  
✅ Esitatud on konkreetne ja põhjendatud soovitus  
✅ Analüüs vastab ülesande nõudele võrrelda müügikanaleid ning klientide käitumist



