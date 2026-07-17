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
```sql

##🥇 3. TOP kliendid (VIP)
VIP‑kliendid on need, kelle kogukäive ületab 20 000 €.
TOP‑10 kliendid:

Nimi	Linn	Tellimusi	Kogukäive	Segment
Tiina Pärn	Tartu	73	27 668.02	VIP
Priit Rand	Pärnu	76	26 286.10	VIP
Kevin Org	Tallinn	78	23 467.13	VIP
Laura Tammik	Pärnu	74	23 385.82	VIP
Erkki Ilves	Tartu	72	22 942.42	VIP
Anu Kuusik	Tallinn	77	21 626.10	VIP
Kersti Lill	Tallinn	71	21 137.47	VIP
Riina Lill	Pärnu	67	20 972.33	VIP
Annika Saar	Viljandi	66	20 726.79	VIP
Ago Kull	Pärnu	64	20 124.61	VIP


VIP‑kliendid moodustavad kõige väärtuslikuma kliendisegmendi — nad ostavad tihti ja suure summaga.

##📈 4. Segmentide jaotus
VIP kliendid
Väga kõrge ostusagedus

Väga suur kogukäive

Tugev lojaalsus

Soovitus: personaalne pakkumine, lojaalsusprogramm

Regular kliendid
Stabiilne ostusagedus

Keskmine kogukäive

Potentsiaal tõusta VIP‑segmenti

Soovitus: kampaaniad, kordusostude soodustamine

Uus kliendid
Madal kogukäive

Varajane kliendisuhe

Vajavad aktiveerimist

Soovitus: onboarding, esmaostu pakkumised

##🧭 5. Juhatuse kokkuvõte
5.1. Mis oli suurim üllatus?
Suurim üllatus oli VIP‑kliendi profiili tugevus:
VIP‑kliendid ostavad kümneid kordi ja kulutavad üle 20 000 €, mis näitab väga kõrget lojaalsust ja stabiilset ostukäitumist.

Lisaks oli üllatav, et Regular segment on väga lai, mis tähendab suurt potentsiaali VIP‑segmenti kasvatamiseks.

5.2. Meie soovitus Toomasele
Toomasele soovitame:

Luua VIP‑programm

personaalne kliendihaldur

eksklusiivsed pakkumised

varajane ligipääs uutele toodetele

Regular segmenti aktiveerida

kordusostu kampaaniad

ostusageduse tõstmise programmid

punktisüsteem

Uus segmenti kasvatada

esmaostu soodustused

automaatne onboarding

personaalsed soovitused

VIP‑kliendid toovad kõige suurema tulu, Regular kliendid kõige suurema kasvupotentsiaali.

5.3. Milliseid andmeid meil puudus?
Analüüsi käigus selgus, et järgmised andmed oleksid andnud veel täpsema kliendiprofiili:

kliendi vanus

kliendi sugu

kliendi registreerimise kuupäev

kliendi kanal (veeb, pood, kampaania)

kliendi segmendi muutused ajas

kliendi toote-eelistused

kliendi tagastuste info

Need andmed võimaldaksid luua:

täpsemaid segmente

personaalseid pakkumisi

kliendi elutsükli analüüsi

churn‑prognoose

##📊 6. Segmentide kokkuvõtte tabel
Segment	Kogukäive	Tellimuste arv	Profiil
VIP	> 20 000 €	Väga kõrge	lojaalsed, suur tulu
Regular	5 000–20 000 €	Keskmine	kasvupotentsiaal
Uus	< 5 000 €	Madal	vajab aktiveerimist


##🛠️ 7. SQL‑skript (täielik)
sql
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

##🧩 8. Lühike juhatuse kokkuvõte ühes lõigus
Kliendigruppide analüüs näitas, et VIP‑kliendid moodustavad väikese, kuid äärmiselt väärtusliku segmendi, mis toob kõige suurema tulu. Regular segment on lai ja pakub suurt kasvupotentsiaali, samas kui Uus segment vajab aktiivset kaasamist. Soovitame Toomasele luua VIP‑programmi, tugevdada Regular segmenti kordusostu kampaaniatega ning arendada Uus segmenti onboarding‑pakkumistega. Täiendavad demograafilised ja käitumuslikud andmed võimaldaksid segmente veelgi täpsemaks muuta.
