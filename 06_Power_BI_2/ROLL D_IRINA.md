# E-poe Lugu — UrbanStyle Ltd
### DACA · Nädal 6 · Andmelood ja Dashboard'i Valmistamine · Roll D

**Autor:** Irina
**Sihtrühm:** investorid, meeskond
**Tööriist:** Power BI Desktop
**Andmeallikas:** `sales.csv`, `products.csv` — filtreeritud `channel = 'online'`

---

## Ülesanne

E-pood on UrbanStyle'i kiiremini kasvav kanal ja investorite jaoks kõige huvitavam — skaleeritav, madalate püsikuludega, geograafiliselt piiramatu. Eesmärk on näidata kasvutempot ja digitaalse kanali potentsiaali.

## Andmete ettevalmistus

1. Page-level filter `channel = online` rakendatud kogu lehele.
2. Oluline erisus: online-tellimustel on `store_location` tühi (NULL) — see ei mõjuta seda lehte, kuna filtreerime `channel` järgi, mitte `store_location` järgi.
3. `sales` liidetud `products`-iga TOP-5 diagrammi jaoks.

## KPI-kaardid

| KPI | Väärtus |
|---|---|
| Kogukäive | 1 526 275,77 € |
| Tellimuste arv | 5204 |
| Keskmine tellimus | ≈ 293,32 € |
| Osakaal kogukäibest | 34,9% |
| Kasv H1 → H2 (2024) | [täienda `Kasv_H1_H2` mõõdiku tulemusega] |

**Metodoloogiline märkus:** aastane kasvuprotsent (YoY) ei ole arvutatav, kuna andmestik katab vaid 2024. aastat. Selle asemel kasutati ausamat, tegelikult mõõdetavat näitajat — kasv esimeselt poolaastalt teisele sama aasta sees.

**Äritõlgendus:** E-pood moodustab 34,9% kogukäibest — peaaegu sama palju kui Tallinna kauplus (37,2%), kuid ilma füüsilise kaupluse püsikuludeta. See teeb kanalist investorile atraktiivse: sarnane käive, tõenäoliselt madalam kulubaas.

## Diagrammid

### 1. Müügitrend kuude lõikes

Joondiagramm kuupäevahierarhiaga, näitab kasvukurvi kuju.

**Äritõlgendus:** [täienda pärast graafiku valmimist — kas kasv on ühtlane, hüppeline või lööb tagasi mingil perioodil]

### 2. TOP 5 toodet e-poes

Tulpdiagramm, Top N (5) filter, sorteeritud kahanevalt.

**Äritõlgendus:** [võrdle Roll A TOP-5 nimekirjaga — kas online-hitid erinevad Tallinna omadest? Kui jah, see on tugev leid turunduse jaoks]

### 3. Kanalite osakaal kogukäibest

Rõngasdiagramm: online vs pood (kasutatud sama `Osakaal_kogukaibest` mõõdikut, filtreeritud online'ile).

**Äritõlgendus:** Online moodustab 34,9% ja pood ülejäänu — vahe Tallinna suhtes on väike (2,3 protsendipunkti), mis näitab, et e-pood on juba peaaegu järgi jõudnud suurimale füüsilisele kauplusele.

## Annotatsioonid

1. [Kasvumoment trendigraafikul — kampaania mõju, kui nähtav]
2. [TOP-toote erinevus võrreldes Tallinnaga]

## Viitejoon

Tallinna keskmine kuukäive lisatud constant line'ina — näitab visuaalselt distantsi suurima füüsilise kaupluseni.

## Andmelugu

> UrbanStyle'i e-pood moodustab juba 34,9% kogukäibest (1,53M €, 5204 tehingut) — peaaegu võrdselt Tallinna kauplusega, kuid oluliselt madalama kulubaasiga. [Andmed: täienda H1→H2 kasvunumbriga]. Soovitame suurendada digitaalse turunduse eelarvet, kuna kanal on juba tõestanud end mahult võrdväärsena peakontori kauplusega, ilma füüsilise kaupluse püsikuludeta.

## Kvaliteedikontroll

- [x] Dashboard näitab ainult e-poe (`channel = online`) andmeid
- [x] Aastase kasvu asemel kasutatud ausat H1→H2 mõõdikut
- [ ] TOP 5 filter kontrollitud
- [ ] Annotatsioonid lisatud (min 2)
- [ ] Andmelugu lõplikult sõnastatud koos kasvunumbriga

---
*Osa DACA (Andmeanalüütiku Karjäärikiirendi) programmi nädala 6 ülesandest "Andmelood ja Dashboard'i Valmistamine".*
