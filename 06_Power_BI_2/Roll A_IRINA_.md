# Tallinna Kaupluse Lugu — UrbanStyle Ltd
### DACA · Nädal 6 · Andmelood ja Dashboard'i Valmistamine · Roll A

**Autor:** Irina
**Sihtrühm:** Kristi (CEO), meeskond
**Tööriist:** Power BI Desktop
**Andmeallikas:** `sales.csv`, `products.csv` — filtreeritud `store_location = 'Tallinn'`

---

## Ülesanne

Tallinn on UrbanStyle'i peakontor ja suurim kauplus. Eesmärk on näidata ühe dashboard'i peal nii tugevusi kui kasvuvõimalusi, mida teised kauplused saaksid kopeerida.

## Andmete ettevalmistus

1. Page-level filter `store_location = Tallinn` rakendatud kogu lehele — kõik visuaalid näitavad automaatselt ainult Tallinna andmeid.
2. `sales` tabel liidetud `products` tabeliga `product_id` kaudu, et saada tootenimesid TOP-5 diagrammi jaoks.
3. Kuupäevaväljal (`sale_date`) kasutusel Power BI vaikimisi kuupäevahierarhia (Year → Quarter → Month → Day) drill-down'i võimaldamiseks.

## KPI-kaardid

| KPI | Väärtus |
|---|---|
| Kogukäive | 1 626 303,81 € |
| Tellimuste arv | 5704 |
| Keskmine tellimus | ≈ 285,15 € |
| Osakaal kogukäibest | 37,2% |

**Äritõlgendus:** Tallinn on selgelt ettevõtte suurim kauplus, moodustades üle kolmandiku (37,2%) kogu käibest. See tähendab, et Tallinna toimimise kvaliteet mõjutab otseselt ettevõtte tervikpilti — iga muster, mis siin töötab, väärib kaalumist teistes kauplustes.

## Diagrammid

### 1. Müügitrend kuude lõikes

Joondiagramm kuupäevahierarhiaga (drill-down Year → Month → Day).

**Äritõlgendus:** [täienda pärast graafiku valmimist — nt "Käive kasvas ühtlaselt kuni detsembrini, mil toimus X% hüpe jõulukampaania tõttu"]

### 2. TOP 5 toodet Tallinnas

Tulpdiagramm, sorteeritud suurimast väikseimani, Top N filtriga (Top 5, by Sum of total_price).

| Koht | Toode | Ligikaudne käive (€) |
|---|---|---|
| 1 | Vintage tweed kampsun | ≈ 7500 |
| 2 | Moodne merino villane triiksärk | ≈ 6500 |
| 3 | Sportlik villane tossud | ≈ 5200 |
| 4 | Boheemlaslik puuvillane tuulejope | ≈ 5200 |
| 5 | Minimalistlik džersii polo särk | ≈ 5000 |

*(täpsed numbrid tuleks üle kontrollida otse Power BI's — ülal olevad on ligikaudsed, loetud graafikult)*

**Äritõlgendus:** Kudumitooted (kampsun, triiksärk) domineerivad Tallinna TOP-5 nimekirjas — see viitab tugevale nõudlusele soojemate rõivaste järele, mis võib olla hooajaline signaal teistele kauplustele sortimenti planeerides.

### 3. Kliendisegmentide jaotus

Rõngasdiagramm — registreeritud kliendid vs külalisostud (Tallinna kaupluses).

**Äritõlgendus:** [täienda tegeliku jaotusega, kui diagramm valmis]

## Annotatsioonid

1. [Trendigraafiku kõrgeim/madalaim punkt — selgita PÕHJUST, mitte ainult numbrit]
2. [TOP-toote diagrammil — miks see toode domineerib]

## Viitejoon

Keskmine kuukäive (Analytics pane → Average line) lisatud trendigraafikule, et visualiseerida kõikumist keskmise suhtes.

## Andmelugu

> Tallinn on UrbanStyle'i peakontor ja suurim kauplus, moodustades 37,2% kogukäibest (1,63M € 5704 tehingust). [Andmed: täienda trendi ja TOP-toote leiuga pärast graafikute valmimist]. Soovitame [konkreetne tegevussoovitus TOP-toote või hooajalisuse põhjal].

## Kvaliteedikontroll

- [x] Dashboard näitab ainult Tallinna andmeid (page-level filter kontrollitud)
- [x] KPI "Osakaal kogukäibest" vormindatud protsendina (37,2%, mitte 0,37)
- [ ] TOP 5 filter kontrollitud — algselt kuvas 6 toodet, parandamisel
- [ ] Annotatsioonid lisatud (min 2)
- [ ] Andmelugu lõplikult sõnastatud

---
*Osa DACA (Andmeanalüütiku Karjäärikiirendi) programmi nädala 6 ülesandest "Andmelood ja Dashboard'i Valmistamine".*
