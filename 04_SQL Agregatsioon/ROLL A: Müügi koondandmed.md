# 📊 SQL Müügikoondandmed

**Koostas:** Silver Varusk

## 📝 Projekti ülevaade

Analüüs hõlmab kuist müüki, tootekategooriate võrdlust ning müügitrendide uurimist kasutades CTE-sid ja aknafunktsioone.

### Kasutatud SQL tehnikad

- GROUP BY
- HAVING
- JOIN
- CTE (Common Table Expression)
- Window Functions (`LAG`)
- SUM, COUNT, AVG
- Protsentuaalse kasvu arvutamine

# 💡 Äriline kokkuvõte

### Peamised tähelepanekud

✅ Müügitulu kasvas aasta jooksul järjepidevalt.

✅ Aasta alguses jäi kuine käive vahemikku **85 000–110 000 €**.

✅ Teisel poolaastal ületas käive mitmel kuul **140 000 €**.

✅ Kõige edukam kuu oli **detsember 2024**, mille käive ulatus **170 623,28 euroni**.

✅ Kõige nõrgem kuu oli **jaanuar 2024**, mille käive oli **85 618,65 eurot**.

### Äriline järeldus

Ettevõtte müügitulemused paranesid aasta jooksul märkimisväärselt. Käibe kasv ning keskmise tellimuse väärtuse suurenemine viitavad tugevamale ostuaktiivsusele ja edukale müügistrateegiale. Tulemused toetavad optimistlike kasvueesmärkide seadmist järgmiseks perioodiks.

---

# ✅ Kvaliteedikontroll

- [x] GROUP BY kasutatud
- [x] HAVING kasutatud
- [x] JOIN kasutatud
- [x] CTE kasutatud
- [x] LAG() aknafunktsioon kasutatud
- [x] Äriline kokkuvõte lisatud

---



# SQL Päringud
---

# 📅 Müük kuude kaupa

See päring kuvab iga kuu tellimuste arvu, kogukäibe ja keskmise tellimuse väärtuse.

```sql
SELECT
    DATE_TRUNC('month', sale_date) AS kuu,
    COUNT(sale_id) AS tellimuste_arv,
    SUM(total_price) AS kogukäive,
    ROUND(AVG(total_price), 2) AS keskmine_tellimus
FROM sales
WHERE sale_date >= '2024-01-01'
GROUP BY DATE_TRUNC('month', sale_date)
ORDER BY kuu;
```

<details>
<summary>📈 Tulemus</summary>

<img width="329" height="550" alt="image" src="https://github.com/user-attachments/assets/1f513e6c-521d-4784-a395-da90e7fbb1ef" />

</details>

---

# 🛒 Müük kategooriate kaupa

Päring võrdleb erinevate tootekategooriate käivet ning kuvab ainult kategooriad, mille kogumüük ületab 1000 eurot.

```sql
SELECT
    p.category,
    COUNT(s.sale_id) AS toodete_arv,
    SUM(s.total_price) AS kogumüük,
    ROUND(AVG(s.total_price), 2) AS keskmine_hind
FROM sales s
JOIN products p
    ON s.product_id = p.product_id
GROUP BY p.category
HAVING SUM(s.total_price) > 1000
ORDER BY kogumüük DESC;
```

<details>
<summary>📈 Tulemus</summary>

<img width="299" height="195" alt="image" src="https://github.com/user-attachments/assets/14ab5cac-5013-485c-9a9e-61263805464d" />

</details>

---

# 📊 Kuised trendid CTE-ga

CTE abil arvutatakse kuine käive ning võrreldakse seda eelmise kuu tulemustega.

```sql
WITH kuu_myyk AS (
    SELECT
        DATE_TRUNC('month', sale_date) AS kuu,
        SUM(total_price) AS käive
    FROM sales
    WHERE sale_date >= '2024-01-01'
    GROUP BY DATE_TRUNC('month', sale_date)
)
SELECT
    kuu,
    käive,
    LAG(käive) OVER (ORDER BY kuu) AS eelmine_kuu,
    käive - LAG(käive) OVER (ORDER BY kuu) AS muutus
FROM kuu_myyk
ORDER BY kuu;
```

<details>
<summary>📈 Tulemus</summary>

<img width="346" height="552" alt="image" src="https://github.com/user-attachments/assets/3936830c-baa0-41db-84fd-6c9b9f7f5d56" />

</details>

---

# 📈 Kuised trendid koos kasvuprotsendiga

Selles analüüsis lisatakse kuisele muutusele ka protsentuaalne kasv võrreldes eelmise kuuga.

```sql
WITH kuu_myyk AS (
    SELECT
        DATE_TRUNC('month', sale_date) AS kuu,
        SUM(total_price) AS käive
    FROM sales
    WHERE sale_date >= '2024-01-01'
    GROUP BY DATE_TRUNC('month', sale_date)
)
SELECT
    kuu,
    käive,
    LAG(käive) OVER (ORDER BY kuu) AS eelmine_kuu,
    käive - LAG(käive) OVER (ORDER BY kuu) AS muutus,
    ROUND(
        (käive - LAG(käive) OVER (ORDER BY kuu))
        / LAG(käive) OVER (ORDER BY kuu) * 100,
        1
    ) AS kasvu_protsent
FROM kuu_myyk
ORDER BY kuu;
```

<details>
<summary>📈 Tulemus</summary>

<img width="401" height="558" alt="image" src="https://github.com/user-attachments/assets/591a0640-b019-41c9-93df-8956555177f1" />

</details>

---


