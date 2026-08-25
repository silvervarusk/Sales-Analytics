Andmekvaliteedi ja Andmete Puhastamise Lõpparuanne

# Roll A – Müügiandmete puhastamine

## Eesmärk
Luua müügitabelist testkoopia, leida duplikaadid, NULL väärtused ja vigased kuupäevad ning dokumenteerida tulemused.

## Testkoopia loomine

```sql
CREATE TABLE sales_test AS
SELECT * FROM sales;
```

## NULL väärtuste kontroll

```sql
SELECT
    COUNT(*) FILTER (WHERE customer*id IS*NULL) AS null_customer_id,
    COUNT(*) FILTER (WHERE sale_date IS NULL) AS null_sale_date,
    COUNT(*) FILTER (WHERE*total*price IS NULL) AS null_total_price*FROM sales_test;
``*

*## Tulemus
- NULL customer_id = 14*7
* NULL sale_date = 0
- NULL total*price*= 0

Mär*us* customer_id NULL väärtused tähist*vad*külalisoste.

##*Tule*iku kuupäevade kontroll

```sql
SE*ECT COUNT**)*AS tuleviku_kuupaevad
FROM sales_t*st
*HERE*sale_date > CURRENT_DATE;
```

###*Tulemus
- Tule*iku kuupäevad = 0

## Duplika*t*de leidmine

```sql
SELECT invoice*id,
*     *COUNT(*) AS koopiate_arv
FROM sale*_test
GROUP BY*invoice*id
HAVING COUNT(*) > 1
ORDER BY ko*piate*ar* DESC;
```

### Tulemus
- 4013 du*l*kaatset invoice_id väärtust

## Du*l*ka*tsete ridade arv

```sql
SELECT CO*NT(*)*AS*duplikaat_read
FROM sales_test
WHE*E id NOT IN*(
*   SELECT MIN(id)
    FROM sales_t*st
    GROUP BY invoice*id*);
```

### Tulemus
- 5116 dupl*kaatset rida

## Külalisostude kon*roll

```sql
SELECT COUNT(*) AS ku*alisostud
FROM sales_test
WHERE cu*tomer_id IS NULL;
```

### Tulemus*- *487 külalisostu

## Duplikaatide e*mald*mine*
```sql
DELETE
FROM sales_test
WHE*E*id*NOT IN (
    SELECT MIN(id)
    FR*M sales_test
   *GROUP*BY invoice_id
);
```

## Kokkuvõte*
|*Probleem | Kogus |
|-----------|--*-----*
* Duplikaatsed read | 5116 |
| Dupl*kaatsed invoice_id | 4013 |
| NULL*customer_id | 1487 |
| NULL sale_d*te | 0 |
| NULL total_price | 0 |
* Tuleviku kuupäevad | 0 |

---

# *oll B – Kliendiandmete puhastamine*
## Testt*beli loomine

```sql
CREATE TABLE *ustomers_test AS
SELECT * FROM cus*omers;

SELECT*COUNT**) AS ridade_arv
FROM customers_te*t;
```

###*Tule*us
- 3150 rida

## Duplikaatsed e-*ailid

*``*sql
SELECT email,
       COUNT(*) A* koopiate_arv
*ROM*customers_test
GROUP BY email
HAVI*G COUNT(*) > 1**RDER BY koopiate_arv DESC;
```

##* Tulemus
**129 duplikaatset e-maili

## Puudu*ad nimed

```sql
SELECT
    COUNT(*) FILTER (WHERE first_name IS NULL*OR first_name = '') AS null_eesnim*,
    COUNT(*) FILTER (WHERE last_*ame IS NULL OR last_name = '') AS *ull_perenimi
FROM customers_test;
*``

### Tulemus
- Puuduvaid nimesi* ei leitud

## Linnade kontroll

`*`sql
SELECT city,
       COUNT(*) *S arv
FROM customers_test
GROUP BY*city
ORDER BY city;
```

### Tulem*s
- 54 erinevat linnanime varianti*
## Kontaktandmete kontroll

```sq*
SELECT
    COUNT(*) FILTER (WHERE*phone IS NULL OR phone = '') AS nu*l_telefon,
    COUNT(*) FILTER (WH*RE email IS NULL OR email = '') AS*null_email
FROM customers_test;
``*

### Tulemus
- 380 puuduvat e-mai*i*
## Linnanimede standardiseerimine*
```sql
UPDATE customers_test
*ET*city = INITCAP(TRIM(city))
WHERE c*ty != INITCAP(TR*M(city));
```

## E-mailide standa*diseerimine

```sql
UPDATE custome*s_test
SET email = LOWER(TRIM(emai*))
WHERE email != LOWER(TRIM(email*);
```

## Telefoninumbrite standa*diseerimine

```sql
SELECT phone,
*      CASE
           WHEN phone L*KE '+372%' THEN phone
           W*EN phone LIKE '372%' THEN '+' || p*one
           WHEN LENGTH(phone) * 7 THEN '+372' || phone
          *ELSE phone
       END AS standardn*_telefon
FROM customers_test
WHERE*phone IS NOT NULL
LIMIT 10;
```

#* Kokkuvõte

| Probleem | Kogus |
|*----------|--------|
| Duplikaatse* e-mailid | 129 |
| Puuduvad nimed*| 0 |
| Linnanimede ebajärjekindlu* | 54 |
| Puuduvad kontaktandmed |*380 |

---

# Roll C – Tooteandmet* puhastamine

## Testkoopia loomin*

```sql
CREATE TABLE IF NOT EXIST* products_test AS
SELECT * FROM pr*ducts;
```

## Ridade arv

```sql
*ELECT COUNT(*) AS ridade_arv
FROM *roducts_test;
```

### Tulemus
- 3*2 toodet

## Duplikaatsed tootenim*d

```sql
SELECT
    product_name,*    COUNT(*) AS koopiate_arv
FROM *roducts_test
GROUP BY product_name*HAVING COUNT(*) > 1
ORDER BY koopi*te_arv DESC;
```

### Tulemus
- 12*duplikaatset tootenime

## NULL-vä*rtuste kontroll

```sql
SELECT
   *COUNT(*) FILTER (WHERE product_nam* IS NULL OR product_name = '') AS *ull_nimi,
    COUNT(*) FILTER (WHE*E category IS NULL OR category = '*) AS null_kategooria,
    COUNT(*)*FILTER (WHERE retail_price IS NULL* AS null_jaehind,
    COUNT(*) FIL*ER (WHERE cost_price IS NULL) AS n*ll_omahind
FROM products_test;
```*
### Tulemus
- NULL väärtusi ei le*tud

## Negatiivsed hinnad

```sql*SELECT COUNT(*) AS negatiivne_hind*FROM products_test
WHERE retail_pr*ce < 0;
```

### Tulemus
- 0

## Ä*rmuslikud hinnad

```sql
SELECT pr*duct_name,
       retail_price
FRO* products_test
WHERE retail_price * 1000
ORDER BY retail_price DESC;
*``

### Tulemus
- 0

## Kategooria*e kontroll

```sql
SELECT category*
       COUNT(*) AS arv
FROM produ*ts_test
GROUP BY category
ORDER BY*category;
```

## Kategooriate üht*ustamine

```sql
UPDATE products_t*st
SET category = INITCAP(TRIM(cat*gory))
WHERE category != INITCAP(T*IM(category));
```

## CASE standa*diseerimine

```sql
UPDATE product*_test
SET category = CASE
    WHEN*LOWER(TRIM(category)) IN ('shoes',*'jalanõud', 'footwear') THEN 'Shoe*'
    WHEN LOWER(TRIM(category)) I* ('shirts', 'särgid', 'tops') THEN*'Shirts'
    WHEN LOWER(TRIM(categ*ry)) IN ('pants', 'püksid', 'trous*rs') THEN 'Pants'
    ELSE INITCAP*TRIM(category))
END;
```

## Lõpli* kontroll

```sql
SELECT category,*       COUNT(*) AS arv
FROM produc*s_test
GROUP BY category
ORDER BY *ategory;
```

## Kokkuvõte

| Prob*eem | Kogus |
|-----------|-------*|
| Duplikaatsed nimed | 12 |
| NU*L väärtused | 0 |
| Hinnavead | 0 *
| Kategooriavead | 0 |

---

# Ro*l D – Ristvalideerimine (Sales, Cu*tomers, Products)

## Orb-kliendid*
```sql
SELECT COUNT(*) AS orb_kli*nt
FROM sales s
LEFT JOIN customer* c
ON s.customer_id = c.customer_i*
WHERE c.customer_id IS NULL
AND s*customer_id IS NOT NULL;
```

### *ulemus
- 0

## Orb-tooted

```sql
*ELECT COUNT(*) AS orb_toode
FROM s*les s
LEFT JOIN products p
ON s.pr*duct_id = p.product_id
WHERE p.pro*uct_id IS NULL
AND s.product_id IS*NOT NULL;
```

### Tulemus
- 0

##*Hinna ebakõlad

```sql
SELECT
    *.sale_id,
    s.total_price,
    p*retail_price,
    s.quantity,
    *.total_price - (p.retail_price * s*quantity) AS erinevus
FROM sales s*JOIN products p
ON s.product_id = *.product_id
WHERE ABS(
    s.total*price - (p.retail_price * s.quanti*y)
) > 1
ORDER BY ABS(erinevus) DE*C;
```

### Tulemus
- 664 hinnavig*

## Vaimkliendid

```sql
SELECT C*UNT(*) AS vaimkliendid
FROM custom*rs c
LEFT JOIN sales s
ON c.custom*r_id = s.customer_id
WHERE s.custo*er_id IS NULL;
```

### Tulemus
- *92

## Vaimtooted

```sql
SELECT C*UNT(*) AS vaimtooted
FROM products*p
LEFT JOIN sales s
ON p.product_i* = s.product_id
WHERE s.product_id*IS NULL;
```

### Tulemus
- 12

--*

# Roll E – Valideerimis- ja kval*teedikontroll

## Peamised tulemus*d

### Duplikaadid

- Sales: 5116 *ida
- Invoice_ID duplikaadid: 4013*- Customers e-maili duplikaadid: 1*9
- Products duplikaatsed nimed: 1*

### Hinnaloogika

- 664 müüki, k*s:
  - total_price ≠ retail_price * quantity

###*Loja*lsusprogrammi probleemid

Leiti ju*tumeid, kus Gold või Silver taseme*klientidel puudus ostuajalugu.

##*Järeldused

Kõige suuremad kvalite*diprobleemid:

1. Müügiandmete dup*ikaadid
2. Hinnaloogika vead
3. Pu*duvad kontaktandmed
4. Duplikaatse* kliendikirjed
5. Duplikaatsed too*ekirjed

## Soovitused

- Rakendad* automaatne duplikaadikontroll.
- *isada valideerimised andmete sises*amisel.
- Kontrollida müügihinna a*vutamist.
- Täiendada kontaktandme*d.
- Dokumenteerida ärireeglid (kü*alisostud, lojaalsusprogramm jne).*
---

# Lõpphinnang

PHMT projekti*käigus puh*st*ti ja valideeriti müügi-, kliendi-*ja*tooteandmed. T*bel*tevahelised viited olid korrektsed* kuid tuvastati märkimisväärne hul* duplikaate ning hinn*loogika vigu. And*ed*on pärast puhastamist oluliselt us*ldusväärsemad ning sobivad edasiseks analüüsiks ja aruandluseks.
