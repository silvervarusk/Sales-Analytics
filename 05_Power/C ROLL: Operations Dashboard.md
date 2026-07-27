# Operations Dashboard — UrbanStyle Ltd
### DACA · Nädal 5 · Visualiseerimise disain · Roll C

**Autor:** Irina
**Sihtrühm:** Liis (Operations)
**Tööriist:** Power BI Desktop
**Andmeallikad:** `sales.csv`, `inventory.csv`, `products.csv`

---

## Ülesanne

Liis vajab ühe pilguga ülevaadet laoseisude olukorrast ja müügi jaotusest kaupluste lõikes, et teha kiireid operatiivseid otsuseid — kus on tugev müük, kus on riskid laoseisus.

## Andmete ettevalmistus

Enne visualiseerimist läbis toorandmestik kolm puhastusetappi Power Query'is:

1. **Puuduv kaupluse asukoht.** Online-tellimustel (`channel = online`) oli väli `store_location` tühi (NULL), mitte märgitud kui "Online". Loodi arvutatud veerg `store_final`, mis asendab tühjad väärtused sõnaga "Online" — ilma selleta oleks diagrammil tekkinud eksitav "(Blank)" sektor.
2. **Negatiivsed laoseisud.** `inventory` tabelis leidus 10 rida negatiivse `quantity_available` väärtusega — need eemaldati enne agregeerimist, kuna tegemist on ilmselge andmeveaga, mitte reaalse laoseisuga.
3. **Andmetüüpide kontroll.** Kinnitati, et arvväljad (`total_price`, `quantity_available`) on korrektselt Decimal/Whole Number tüüpi, mitte tekst.

## Diagrammid

### 1. Müük kaupluste lõikes

Sektordiagramm, mis näitab müügitulu jaotust nelja kanali vahel: Tallinn, Tartu, Pärnu, Online.

| Kauplus | Osakaal | Tulu (€) | Tehinguid |
|---|---|---|---|
| Tallinn | 38% | 1 626 304 | 5704 |
| Online | 35% | 1 526 276 | 5204 |
| Tartu | 18% | 783 469 | 2708 |
| Pärnu | 10% | 438 183 | 1618 |

**Äritõlgendus:** Tallinn moodustab suurima osa müügitulust (38%), kuid Online-kanal on sellele väga lähedal (35%) — koos toovad need kaks kanalit üle 70% kogu käibest. Pärnu ja Tartu on väiksema mahuga ning nende arengut tasub jälgida eraldi, et mõista, kas tegemist on strateegilise valikuga (väiksem turg) või kasutamata potentsiaaliga.

### 2. Laoseis toote kategooria järgi

Tulpdiagramm, sorteeritud suurimast väikseimani, näitab saadaolevat laokogust tükkides viies tootekategoorias (pärast negatiivsete väärtuste eemaldamist).

| Kategooria | Kogus (tk) |
|---|---|
| meeste_riided | 101 277 |
| jalanõud | 86 352 |
| laste_riided | 75 222 |
| naiste_riided | 64 055 |
| aksessuaarid | 50 125 |

**Äritõlgendus:** Suurim laovaru on meeste riiete kategoorias, väikseim aksessuaaride kategoorias. Kategooriate vaheline erinevus (üle kahe korra) võib viidata kas erinevale nõudlusele või erinevale tellimispoliitikale — see väärib täpsemat läbivaatust koos müügikiiruse andmetega, et vältida nii ülevaru kui ka otsalõppemist.

## Dashboard'i vaade

![Operations Dashboard](./operations_dashboard.png)

*(lisa siia oma salvestatud ekraanipilt Power BI dashboard'ist — pilt peaks kajastama mõlemat diagrammi ühel ekraanil)*

## Kvaliteedikontroll

- [x] Mõlemad diagrammid vastavad Liis'i operatiivsele vajadusele (kauplused + laoseis)
- [x] Kauplused ja kategooriad on värvide ja siltide kaudu selgelt eristatavad
- [x] Andmed on puhastatud (NULL-väärtused ja negatiivsed kogused käsitletud enne visualiseerimist)
- [x] Sektordiagrammil täpselt 4 osa, tulpdiagramm sorteeritud kahanevalt

---
*Osa DACA (Andmeanalüütiku Karjäärikiirendi) programmi nädala 5 ülesandest "Visualiseerimise disain".*
