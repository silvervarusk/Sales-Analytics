# 📊 SQL Andmeanalüüsi Projekt

**Autor:** Silver Varusk

## 📌 Projekti eesmärk

Selle projekti eesmärk oli analüüsida ettevõtte müügi-, kliendi-, toote- ja turundusandmeid SQL-i abil ning koostada juhtkonnale andmepõhised soovitused.

Projekt viidi läbi nelja analüütilise rolli koostöös:

- ROLL A – Müügi koondandmed
- ROLL B – Kliendisegmendid ja väärtuslikud kliendid
- ROLL C – Inventuuristatistika
- ROLL D – Turunduskanalite analüüs
- Valideerija – Kvaliteedikontroll ja ärisüntees

---

# 🛠 Kasutatud SQL Tehnikad

Projektis kasutati järgmisi SQL funktsioone ja kontseptsioone:

✅ JOIN

✅ GROUP BY

✅ HAVING

✅ Aggregate Functions
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

✅ Common Table Expressions (CTE)

✅ Window Functions
- LAG()
- ROW_NUMBER()
- RANK()

✅ DATE_TRUNC()

✅ CASE WHEN

---

# 📈 ROLL A – Müügi Koondanalüüs

### Analüüsiti

- Kuist müüki
- Müügikäivet
- Keskmist tellimuse väärtust
- Kuust-kuusse kasvu

### Peamised leiud

- Müük kasvas 2024. aasta jooksul järjepidevalt.
- Kõige edukam kuu oli detsember 2024.
- Kõige nõrgem kuu oli jaanuar 2024.
- Teisel poolaastal ületas käive mitmel kuul 140 000 €.

### Äriline järeldus

Ettevõtte müügitulemused paranesid aasta jooksul märkimisväärselt ning toetavad edasiste kasvueesmärkide seadmist.

---

# 👥 ROLL B – Kliendisegmendid ja Väärtuslikud Kliendid

### Analüüsiti

- Kliendisegmente
- Kogukäivet kliendi kohta
- VIP-kliente
- Linnapõhist kliendirankingu analüüsi

### Tulemused

| Segment | Kliente |
|----------|----------:|
| VIP | 19 |
| Regular | 917 |
| Uus | 1615 |
| Kokku | 2551 |

### Peamised leiud

- VIP-kliente on alla 1% kogu kliendibaasist.
- VIP-klientide keskmine käive on 18 227 €.
- Regular-segment moodustab tugeva ja stabiilse kliendibaasi.

### Äriline järeldus

Kõige suuremat väärtust loob väike hulk VIP-kliente, mistõttu kliendilojaalsus ja korduvostude suurendamine on kriitilise tähtsusega.

---

# 🏆 ROLL C – Inventuuristatistika

### Analüüsiti

- Tootekategooriaid
- Hinnatasemeid
- Müügimahtusid
- TOP-tooteid

### Peamised leiud

✅ Kõige tugevam müügikategooria:

**Meesteriided**
- 4121 müüdud ühikut

✅ Kõrgeima väärtusega kategooria:

**Jalanõud**
- Keskmine hind 214,10 €

✅ Kõige nõrgem kategooria:

**Aksessuaarid**
- 3231 müüdud ühikut

### Äriline järeldus

Jalanõud ja meesteriided pakuvad ettevõttele suurimat äripotentsiaali ning vajavad täiendavat tähelepanu toodete ja kampaaniate planeerimisel.

---

# 📢 ROLL D – Turunduskanalite Analüüs

### Analüüsiti

- Turunduskanalite efektiivsust
- Käivet kanalite lõikes
- Kliendiväärtust
- Kuiseid kampaaniatrende

## Tulemused

| Kanal | Käive |
|---------|----------:|
| Google Organic | 863 240 € |
| Direct | 599 438 € |
| Facebook Ads | 504 811 € |

### Kõrgeim müük kliendi kohta

**E-mail Marketing**
- 4542 € kliendi kohta

### Äriline järeldus

Google Organic ja Direct on kõige tugevamad käibeallikad.

E-maili kampaaniad loovad kõige väärtuslikumaid kliente.

---

# ✅ Kvaliteedikontroll ja Valideerimine

Kontrolliti:

- Andmete loogilisust
- Summade kooskõla
- Segmentide jaotust
- Tulemuste ristkontrolli rollide vahel

### Valideerimise tulemus

✅ Rollide A–D tulemused olid omavahel kooskõlas

✅ Kriitilisi vastuolusid ei tuvastatud

### Leitud kvaliteediriskid

⚠ Turunduskanalite nimed ei olnud täielikult standardiseeritud

Näited:

- Google
- google
- Google Organic
- google_organic

⚠ Võimalik topeltarvestus tabelis `web_logs`, kui kliendil on mitu kirjet.

---

# 🎯 Lõplik Ärikokkuvõte

Analüüs näitab, et ettevõtte kasvu toetavad kolm peamist tegurit:

1. Tugev müügikasv 2024. aastal
2. Kõrge väärtusega VIP-kliendid
3. Efektiivsed turunduskanalid

Google Organic on ettevõtte peamine käibeallikas ning VIP-kliendid loovad ebaproportsionaalselt suure osa kogutulust. Kõrgeima väärtusega tootekategooriaks osutusid jalanõud ning suurima müügimahuga kategooriaks meesteriided.

## Soovitus juhtkonnale

- Suurendada investeeringuid orgaanilisse nähtavusse (SEO)
- Hoida ja arendada VIP-kliente
- Keskenduda premium-tootekategooriatele
- Standardiseerida turunduskanalite andmed parema raportite kvaliteedi saavutamiseks

---

# 📚 Õpitulemused

Projekti käigus harjutati:

- SQL päringute kirjutamist
- Andmete puhastamist ja valideerimist
- CTE kasutamist
- Window Functions kasutamist
- Ärianalüüsi ja andmepõhist otsustamist
- Tulemuste esitlust stakeholderitele

---

**Projekt valminud SQL andmeanalüüsi õppeprojekti raames.**
