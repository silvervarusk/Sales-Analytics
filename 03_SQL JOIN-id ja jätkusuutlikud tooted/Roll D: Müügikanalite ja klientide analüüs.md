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

### 4. Iga kaupluse müügikanalite jaotus

Selles analüüsis võrdlen Tallinna, Tartu ja Pärnu kaupluste müügitulemusi ning online-kanalit.

```sql
SELECT
    s.store_location AS kauplus,
    s.channel AS müügikanal,
    COUNT(s.sale_id) AS oste,
    SUM(s.total_price) AS kogumüük,
    ROUND(SUM(s.total_price) / COUNT(s.sale_id), 2) AS keskmine_ost
FROM sales s
GROUP BY s.store_location, s.channel
ORDER BY kauplus, kogumüük DESC;
```

<details>
<summary>Tulemus (click to expand)</summary>

<img width="307" height="447" alt="image" src="https:://github.com/user-attachments/assets/2ebe6286-e870-4c29-b181-8afa5670dca1" />

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

## Kaupluste müügikanalite võrdlus

| Kauplus | Müügikanal | Oste | Kogumüük (€) | Keskmine ost (€) |
|----------|------------|------:|-------------:|-----------------:|
| Tallinn | Pood | 3801 | 1 092 003,15 | 287,31 |
| Tartu | Pood | 1797 | 521 603,11 | 290,26 |
| Pärnu | Pood | 1058 | 298 744,04 | 272,91 |
| Online | Online | 3462 | 1 006 747,68 | 290,80 |

### Tähelepanekud

✅ **Tallinn on ettevõtte tugevaim müügipiirkond**

- üle 1 miljoni euro kogukäivet;
- rohkem kui pool kogu poe käibest;
- suurim klientide ja ostude arv.

✅ **Tartu näitab tugevat tulemust**

- üle 520 000 € käivet;
- kõrge keskmine ostusumma (290,26 €);
- väga lähedal online-kanali tulemustele.

✅ **Pärnu jääb teistest maha**

- ainult 298 744 € käivet;
- madalaim keskmine ostusumma (272,91 €);
- väikseim ostude arv.

✅ **Online-kanal on väga konkurentsivõimeline**

- üle 1 miljoni euro müüki;
- keskmine ostusumma 290,80 €;
- kõrgeim keskmine ost kõigi kanalite seas.

---

## Ärilised järeldused

### Kas Tallinna, Tartu ja Pärnu kauplused kasutavad kanaleid erinevalt?

Jah.

Tallinn on ettevõtte peamine müügikeskus ning füüsilise poe tähtsus on seal väga suur. Tartu saavutab samuti häid tulemusi, kuid väiksemas mahus. Pärnu müügitulemused jäävad oluliselt tagasihoidlikumaks.

See viitab sellele, et piirkondade ostukäitumine erineb ning turunduseelarvet ei ole mõistlik jagada kõigi linnade vahel võrdselt.

### Kas mõni kauplus peaks rohkem online-müügile panustama?

✅ **Pärnu**

Pärnu keskmine ost (272,91 €) jääb alla online-kanali keskmisele ostule (290,80 €).

Seetõttu võiks Pärnus rohkem investeerida:

- veebireklaami;
- sotsiaalmeedia kampaaniatesse;
- e-poe eripakkumistesse;
- click-and-collect lahenduste turundamisse.

---

## Kuhu peaks Anna turunduseelarvet suunama?

🎯 Soovituslik prioriteet:

### 1. Tallinn

- suurim müügimaht;
- suurim kliendibaas;
- kõrgeim potentsiaal täiendava käibe kasvatamiseks.

### 2. Online-kanal

- üle 1 miljoni euro käivet;
- kõrgeim keskmine ost;
- võimaldab jõuda klientideni üle kogu Eesti.

### 3. Pärnu

- suurim kasvupotentsiaal;
- online-müügi osakaalu saab suurendada.

### 4. Tartu

- stabiilne ja tugev tulemus;
- keskenduda olemasolevate klientide hoidmisele ja lojaalsuse kasvatamisele.

---

## Lõplik soovitus

Analüüsi põhjal on ettevõtte kõige tugevamad müügikanalid **Tallinna füüsiline kauplus ja online-müük**.

Kõige suurema arengupotentsiaaliga piirkond on **Pärnu**, kus turundusinvesteeringud võiksid keskenduda online-müügi kasvatamisele.

Anna võiks suunata suurema osa turunduseelarvest:

- Tallinna poe nähtavuse suurendamisse;
- online-kanali arendamisse;
- Pärnu digiturunduse tugevdamisse.

See aitaks maksimeerida müügitulu ning kasvatada klientide arvu kõige suurema potentsiaaliga kanalites.

---

## Kvaliteedikontroll

✅ Kasutatud on 3 tabeli JOIN-i (`sales`, `customers`, `products`)  
✅ Võrreldud on klientide arvu, kogumüüki ja kanali efektiivsust  
✅ Arvutatud on müük kliendi kohta  
✅ Analüüsitud on kaupluste ja online-kanali erinevusi  
✅ Esitatud on ärilised järeldused ning turundussoovitused  
✅ Vastatud on küsimustele müügikanalite efektiivsuse ja piirkondlike erinevuste kohta  
✅ Esitatud on konkreetsed ning andmetel põhinevad soovitused


