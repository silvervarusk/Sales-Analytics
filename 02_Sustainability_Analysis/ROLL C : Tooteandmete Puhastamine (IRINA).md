# Tooteandmete Puhastamine (Supabase / SQL)

## Ülevaade

See projekt demonstreerib tooteandmete kvaliteedikontrolli ja puhastamise protsessi Supabase'i tabelis `products`.  
Fookus on duplikaatide leidmisel, NULL‑väärtuste kontrollimisel, loogiliste vigade tuvastamisel ja kategooriate ühtlustamisel.

> "Leia duplikaadid, NULL väärtused ja ebajärjekindlused products tabelis."  
> "Loo test koopia ja dokumenteeri probleemid."

## Andmeallikas

- **Sisendtabel:** `products`
- **Testtabel:** `products_test` (turvaline koopia puhastamiseks)

```sql
CREATE TABLE products_test AS
SELECT * FROM products;

SELECT COUNT(*) AS ridade_arv
FROM products_test;
-- 362 rida

1. Duplikaatsete tootenimede leidmine

SELECT
    product_name,
    COUNT(*) AS koopiate_arv
FROM products_test
GROUP BY product_name
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;
-- Leitud: 12 duplikaatset tootenime

Mõju analüütikale:  
Duplikaadid moonutavad müügi-, marginaali- ja SKU‑analüüsi ning tekitavad segadust aruandluses.

2. NULL‑väärtuste kontroll kriitilistes väljadest

SELECT
    COUNT(*) FILTER (WHERE product_name IS NULL OR product_name = '') AS null_nimi,
    COUNT(*) FILTER (WHERE category IS NULL OR category = '') AS null_kategooria,
    COUNT(*) FILTER (WHERE retail_price IS NULL) AS null_jaehind,
    COUNT(*) FILTER (WHERE cost_price IS NULL) AS null_omahind
FROM products_test;
-- Kõik väärtused olemas (0 NULL)

3. Loogiliste hinnavigade kontroll

-- Negatiivsed hinnad
SELECT COUNT(*) AS negatiivne_hind
FROM products_test
WHERE retail_price < 0;

-- Äärmuslikud hinnad (> 1000 EUR)
SELECT product_name, retail_price
FROM products_test
WHERE retail_price > 1000
ORDER BY retail_price DESC;
-- Leitud: 0 negatiivset ja 0 äärmuslikku hinda

4. Kategooriate järjekindlus

SELECT category, COUNT(*) AS arv
FROM products_test
GROUP BY category
ORDER BY category;

Leitud 5 kategooriat:

aksessuaarid
jalanõusid
laste_riided
meeste_riided
naiste_riided

5. Puhastamisraport

| Kategooria | Probleeme | Kirjeldus |
| --- | --- | --- |
| Duplikaatsed nimed | 12 | Sama tootenimi esineb mitu korda |
| NULL nimi/hind | 0 | Kõik kriitilised väljad olemas |
| Loogilised vead | 0 | Pole negatiivseid ega äärmuslikke hindu |
| Ebajärjekindlad kategooriad | 0 | Pole juhtumeid stiilis Shoes vs shoes |
| NULL omahind/kategooria | 0 | Klassifitseerimine olemas |
| **Kokku probleeme** | **12** |  |

Kõige olulisem probleem
Duplikaatsed tootenimed mõjutavad analüüsi kõige rohkem, sest moonutavad müügi- ja marginaaliarvutusi ning tekitavad segadust SKU tasemel.

6. Edasijõudnud puhastamine (valikuline)

6.1. Kategooriate vormingu ühtlustamine

UPDATE products_test
SET category = INITCAP(TRIM(category))
WHERE category != INITCAP(TRIM(category));

6.2. Kategooriate standardiseerimine CASE‑lausete abil

UPDATE products_test
SET category = CASE
    WHEN LOWER(TRIM(category)) IN ('shoes', 'jalanõud', 'footwear') THEN 'Shoes'
    WHEN LOWER(TRIM(category)) IN ('shirts', 'särgid', 'tops')      THEN 'Shirts'
    WHEN LOWER(TRIM(category)) IN ('pants', 'püksid', 'trousers')   THEN 'Pants'
    ELSE INITCAP(TRIM(category))
END;

7. Kvaliteedikontroll

[x] Testtabel loodud
[x] Duplikaadid tuvastatud
[x] NULL‑väärtused kontrollitud
[x] Loogilised hinnavead kontrollitud
[x] Kategooriad analüüsitud
[x] Raport sisaldab konkreetseid numbreid






