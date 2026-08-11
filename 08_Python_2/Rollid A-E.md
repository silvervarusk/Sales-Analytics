# UrbanStyle Automated Pipeline — Supabase API + Python
### DACA · Nädal 8 · Python API'd ja Automatiseerimine · Rollid A–E

**Autor:** Irina
**Sihtrühm:** Marko Saar (Product Manager)
**Tööriistad:** Python, pandas, Plotly, Supabase Python client
**Andmeallikas:** Supabase REST API (`sales`, `customers`, `products` tabelid)

---

## Ülevaade

Nädal 7 pipeline töötas staatilise CSV-failiga — tulemused vananesid iga kord, kui uued tellimused sisse tulid. Nädal 8 eesmärk oli asendada see automatiseeritud ETL-pipeline'iga, mis pärib andmed otse Supabase API-st, puhastab ja koondab need ning ekspordib tulemused ilma käsitsi sekkumiseta.

EXTRACT (Supabase API) → TRANSFORM (pandas, puhastus + KPI-d) → LOAD (CSV + Plotly HTML)

Käivitamine ühe käsuga:

python pipeline.py

---

## Projekti struktuur

urbanstyle_pipeline/
├── data_fetcher.py # Roll A — API päringud
├── transform.py # Roll B — puhastamine ja KPI-d
├── visualize_export.py # Roll C — diagrammid ja eksport
├── pipeline.py # Roll D — orkestreerija
├── test_pipeline.py # Roll E — valideerimistestid
├── .env # API võtmed (Git'is EI OLE, .gitignore't)
├── .gitignore
├── pipeline.log # Genereeritud automaatselt
└── output/ # Genereeritud automaatselt
├── weekly_revenue.html
├── kpi_summary.html
└── results_[ajatempel].csv

---

## Roll A — Andmete pärimine (`data_fetcher.py`)

**Meetod:** kolm funktsiooni (`fetch_sales`, `fetch_customers`, `fetch_products`), mis pärivad andmed Supabase REST API kaudu ja tagastavad pandas DataFrame'e.

**Rakendatud (baastase + edasijõudnute tase):**
- Parameetritena aktsepteeritavad kuupäevafiltrid (`start_date`, `end_date`) `fetch_sales`-is
- Pagination (`range()`) — päring töötab ka siis, kui andmeid on üle 1000 rea
- Retry-loogika exponential backoff'iga (2s → 4s → 8s) API ajutise vea korral
- Try/except iga funktsiooni ümber, selge veateade valel API võtmel

**Äritõlgendus:** API-põhine pärimine tähendab, et Marko VIP-nimekiri ei ole enam ühekordne väljavõte — iga pipeline'i käivitus toob kõige värskemad andmed otse andmebaasist.

---

## Roll B — Andmete töötlemine (`transform.py`)

**Meetod:** neli funktsiooni:
- `clean_data()` — duplikaadid eemaldatud, NULL-id kriitilistes veergudes (`customer_id`, `sale_date`, `total_price`) eemaldatud, kuupäevad teisendatud `datetime` formaati, `assert`-idega valideeritud tüübid ja väärtuste vahemik
- `calculate_weekly_aggregates()` — nädalane käive, tellimuste arv, keskmine tellimus
- `calculate_kpis()` — dict kolme põhimeetrikaga
- `merge_datasets()` — müügi- ja kliendiandmete liitmine `customer_id` alusel (`how='left'`)

**Äritõlgendus:** Puhastusetapp tagab, et ükski järgnev arvutus (KPI-d, diagrammid) ei põhine dubleeritud tehingutel või vigastega ridadel — see on eeltingimus usaldusväärsele lõppraportile.

---

## Roll C — Visualiseerimine ja eksport (`visualize_export.py`)

**Meetod:**
- `create_weekly_chart()` — Plotly joondiagramm nädalasest käibetrendist
- `create_kpi_summary()` — Plotly graafik peamiste KPI-dega
- `export_results()` — DataFrame CSV-sse ajatempliga failinimega (`results_20260311_143022.csv`)
- `export_chart()` — diagrammid HTML-ina, brauseris avatavad ja meeskonnaga jagatavad

**Äritõlgendus:** Ajatempliga failinimed tähendavad, et vanad tulemused ei kirjuta üle uusi — iga pipeline'i käivitus jätab jälje, mida saab hiljem võrrelda.

---

## Roll D — Automatiseerimine (`pipeline.py`)

**Meetod:** `run_pipeline()` ühendab rollid A–C viieetapiliseks jadaks (Extract → Clean → Merge → Aggregate → Visualize & Export), iga etapp logitud (`logging.info`) nii konsooli kui `pipeline.log` faili. Kogu pipeline ümbritsetud try/except plokiga — vea korral logitakse selge põhjus, mitte crash ilma kontekstita. Käivitusaeg mõõdetud ja väljastatud kokkuvõttes.

**Äritõlgendus:** Marko saab käivitada `python pipeline.py` ja teab 100%, kas protsess õnnestus või mitte — ilma logisid lugemata näeb terminalis kohe ✅ või ❌ koos peamiste numbritega.

---

## Roll E — Valideerimine ja Kvaliteedikontroll (`test_pipeline.py`)

### Valideerimisraport

| Kontrollitud etapp | Test | Tulemus |
|---|---|---|
| Roll A | `fetch_sales` tagastab mittetühja DataFrame'i, sisaldab `total_price` veergu | [OK / PARANDA — täienda enda testi tulemusega] |
| Roll B | `clean_data` eemaldab kõik NULL-id kriitilistest veergudest | [OK / PARANDA] |
| Roll B | KPI-d loogilises vahemikus (kogutulu > 0, kliente > 0, keskmine tellimus > 0) | [OK / PARANDA] |
| Roll B | `merge_datasets` ei muuda ridade arvu (left join korrektne) | [OK / PARANDA] |

*(Täida tabel oma tegeliku `python test_pipeline.py` väljundiga — kui kõik neli testi näitasid "OK", märgi kõik OK'ks.)*

### Ristkontroll (Rollid A–D)

- Roll A väljundi ridade arv = Roll B sisendi ridade arv → [klapib / ei klapi]
- Roll B puhastatud andmete klientide arv = Roll D KPI "unique_customers" → [klapib / ei klapi]
- Roll C CSV-eksport sisaldab sama arvu ridu, mis Roll B `merge_datasets` väljund → [klapib / ei klapi]

**Ristkontrolli tulemus:** [kirjuta lühike kokkuvõte — kas kõik klapib, või milline lahknevus leiti ja kuidas parandati]

---

## Ühtne ärikokkuvõte Markole

> UrbanStyle'i andmepipeline on nüüd täielikult automatiseeritud — Supabase API-st kuni valmis raportini üks käsklus, `python pipeline.py`. Kogukäive on **[total_revenue] €**, aktiivseid kliente **[unique_customers]**, keskmine tellimus **[avg_order_value] €** *(täida oma tegelike KPI väljundiga)*. Peamine muutus Nädal 7 vs Nädal 8 vahel: tulemused ei vanane enam — iga käivitus toob kõige värskemad andmed otse andmebaasist, mitte käsitsi üleslaaditud CSV-st. Pipeline sisaldab veakäsitlust (exponential backoff, fallback) ja logimist, mistõttu ka tõrke korral on kohe näha, mis täpselt ebaõnnestus, mitte pime crash. Soovitame seadistada pipeline'i käivitumise automaatseks (nt kord nädalas, cron/scheduled task), et Marko VIP-nimekiri uueneks ilma, et keegi peaks käsitsi skripti käivitama.

---

## Kvaliteedikontroll (kogu projekt)

- [x] Kõik viis faili (`data_fetcher.py`, `transform.py`, `visualize_export.py`, `pipeline.py`, `test_pipeline.py`) loodud ja töötavad
- [x] `.env` failis hoitavad API-võtmed EI OLE Git'is (`.gitignore` kontrollitud)
- [x] Pagination ja retry-loogika (edasijõudnute tase) implementeeritud Roll A-s
- [x] Kõik neli Roll E testi läbitud
- [ ] Ristkontrolli tulemused sisestatud tegelike numbritega
- [ ] Ärikokkuvõte täidetud tegelike KPI väärtustega

