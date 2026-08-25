# SQL Andmete Puhastamine ja Andmekvaliteedi Kontroll

## Projekti ülevaade

See projekt valmis DACA (Andmeanalüütiku Karjäärikiirendi) programmi raames.

Projekti eesmärk oli parandada andmekvaliteeti ning tuvastada kriitilised probleemid ettevõtte andmebaasis. Töö keskendus müügi-, kliendi- ja tooteandmete puhastamisele ning tabelitevahelisele ristvalideerimisele. Kõik analüüsid viidi läbi turvalistes testkoopiates, et vältida muudatusi originaalandmetes.

---

## Kasutatud tööriistad

- SQL
- PostgreSQL / Supabase
- GitHub
- Andmekvaliteedi kontrolli tehnikad
- Andmete puhastamine ja valideerimine

---

## Andmebaasi struktuur

Analüüs hõlmas kolme peamist tabelit:

- **sales** – müügitehingud
- **customers** – kliendiandmed
- **products** – tooteandmed

Lisaks viidi läbi ristvalideerimine kõigi tabelite vahel. 

---

# Müügiandmete puhastamine

## Teostatud kontrollid

- Duplikaatsete tellimuste leidmine
- NULL-väärtuste kontroll
- Tuleviku kuupäevade kontroll
- Külalisostude tuvastamine

## Tulemused

| Probleem | Kogus |
|-----------|--------:|
| Duplikaatseid invoice_id väärtusi | 4013 |
| Duplikaatseid ridu | 5116 |
| NULL customer_id | 1487 |
| NULL sale_date | 0 |
| NULL total_price | 0 |
| Tuleviku kuupäevi | 0 |

Kliendiviite puudumine (`customer_id IS NULL`) osutus äriloogika kohaselt külalisostuks ning seda ei käsitletud andmeveana. 

### Peamine järeldus

Kõige suurem probleem olid duplikaatsed müügikirjed, mis mõjutavad otseselt müügitulemusi, statistikat ja aruandlust. 

---

# Kliendiandmete puhastamine

## Teostatud kontrollid

- Duplikaatsete e-mailide kontroll
- Puuduvate nimede kontroll
- Linnanimede standardiseerimise vajaduse analüüs
- Kontaktandmete kvaliteedi hindamine

## Tulemused

| Probleem | Kogus |
|-----------|--------:|
| Duplikaatsed e-mailid | 129 |
| NULL eesnimi | 0 |
| NULL perenimi | 0 |
| Puuduvad kontaktandmed | 380 |
| Erinevat linnanime väärtust | 54 |

Analüüsi käigus standardiseeriti linnanimed ning e-mailid viidi ühtsesse väiketähtedel põhinevasse vormingusse. 

### Peamine järeldus

Kõige suurem äriline risk on puuduvad kontaktandmed, sest see takistab klientidega suhtlemist ja mõjutab otseselt müügi- ning tugiprotsesse. 

---

# Tooteandmete puhastamine

## Teostatud kontrollid

- Duplikaatsete toodete leidmine
- NULL-väärtuste kontroll
- Hinnaloogika kontroll
- Kategooriate järjepidevuse kontroll

## Tulemused

| Probleem | Kogus |
|-----------|--------:|
| Duplikaatsed tootenimed | 12 |
| NULL-väärtused kriitilistes väljades | 0 |
| Negatiivsed hinnad | 0 |
| Äärmuslikud hinnad | 0 |
| Kategooriate ebajärjekindlused | 0 |

Tooteandmed olid üldiselt väga hea kvaliteediga ning ainus märkimisväärne probleem oli duplikaatsete tootenimede olemasolu.

### Peamine järeldus

Duplikaatsed tootenimed võivad moonutada müügi-, kasumlikkuse- ja marginaalianalüüse. 

---

# Ristvalideerimine ja andmekvaliteedi kontroll

## Kontrollitud valdkonnad

- Müük viitab olemasolevatele klientidele
- Müük viitab olemasolevatele toodetele
- Müügihinna vastavus toote hinnale
- Kliendid, kes pole kunagi ostnud
- Tooted, mida pole kunagi müüdud

## Tulemused

| Probleem | Kogus |
|-----------|--------:|
| Orbid kliendid | 0 |
| Orbid tooted | 0 |
| Hinna ebakõlad | 664 |
| Vaimkliendid | 592 |
| Vaimtooted | 12 |

Kõik kliendi- ja tooteviited olid korrektsed, kuid märkimisväärne probleem ilmnes müügihindade kooskõlas tootehindadega.

### Peamine järeldus

664 müügikirjel ei vastanud müügihind toote hinnale, mis muudab marginaalianalüüsi ja müügitulemuste hindamise ebausaldusväärseks. 

---

# Soovitused

1. Eemaldada duplikaatsed müügikirjed.
2. Rakendada automaatne andmekvaliteedi kontroll.
3. Dokumenteerida külalisostude ärireeglid.
4. Standardiseerida kontaktandmete sisestamine.
5. Kasutada toodete analüüsis unikaalseid identifikaatoreid.
6. Rakendada müügihinna valideerimise reegel:
   - `total_price = retail_price × quantity`
7. Luua automaatsed teavitused hinnaloogika vigade tuvastamiseks. 

---

# Omandatud oskused

- SQL päringud
- Andmete puhastamine
- NULL-väärtuste analüüs
- Duplikaatide tuvastamine
- Andmekvaliteedi hindamine
- Ristvalideerimine tabelite vahel
- Äriliste soovituste koostamine
- PostgreSQL / Supabase kasutamine

---

# Projekti struktuur

```text
portfolio/
└── week-2/
    ├── individual/
    │   ├── week2_sales_cleaning.sql
    │   ├── week2_customers_cleaning.sql
    │   ├── week2_products_cleaning.sql
    │   └── week2_cross_validation.sql
    │
    ├── team/
    │   └── week2_team_cleaning_report.md
    │
    └── README.md
```

---

## Autorid

**Silver**
**Irina**
**Tiiu**

DACA – Andmeanalüütiku Karjäärikiirendi

GitHub Portfolio Project – SQL Andmete Puhastamine ja Andmekvaliteedi Kontroll
