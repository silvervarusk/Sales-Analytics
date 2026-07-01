# Müügiandmete puhastamine
## Roll A :müügiandmete puhastaja
Koostas: Tiiu Kumar
## Ülesanne :luua müügitabelist testkoopia, leida duplikaatsed kirjed, NULL väärtused ja vigased kuupäevad sales-tabelis.
## Puhasta ja dokumenteeri kõik probleemid ja tehtud muudatused

## Testkoopia loomine :

CREATE TABLE sales_test AS SELECT * FROM sales;

## Kõik puhastamisega seotud tegevused viiakse läbi tabelis sales_test
# Andmekvaliteedi kontroll

## NULL väärtustekontroll: kontrollitakse olulisi veerge customer_id, sale_date, total_price

SELECT
    COUNT(*) FILTER (WHERE customer_id IS NULL) AS null_customer_id,
    COUNT(*) FILTER (WHERE sale_date IS NULL) AS null_sale_date,
    COUNT(*) FILTER (WHERE total_price IS NULL) AS null_total_price
FROM sales_test;


Tulemus: 1487 NULL customer_id, 0 NULL sale_date, 0 NULL total_price
Customer_id NULL väärtused - tegemist on külalisostudega (äriloogika kohaselt lubatud)


## Tuleviku kuupäevade kontroll
Kontrolliti, kas tabelis leidub müügikuupäevi, mis on hilisemad kui tänane kuupäev.

SELECT COUNT(*) AS tuleviku_kuupaevad
FROM sales_test
WHERE sale_date > CURRENT_DATE;

Tulemus: 0 tuleviku kuupäeva. Vigaseid kuupäevi ei leitud.

## Duplikaatide leidmine
duplikaadid tuvastatakse välja invoice_id järgi

SELECT  invoice_id, COUNT(*) AS koopiate_arv
FROM sales_test
GROUP BY invoice_id
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;

Tulemus: duplikaatseid invoice_id väärtusi on 4013 tk

<img width="239" height="454" alt="duplikaadid_nimekiri" src="https://github.com/user-attachments/assets/a3d93e75-f98b-447a-a0a8-1d5052445ab3" />


## Loe kokku duplikaatsete ridade arv:

SELECT COUNT(*) AS duplikaat_read
FROM sales_test
WHERE id NOT IN (
    SELECT MIN(id)
    FROM sales_test
    GROUP BY invoice_id
);


Tulemus: 5116 rida on duplikaadid
<img width="767" height="301" alt="invoice283" src="https://github.com/user-attachments/assets/660f65e7-d1de-4d20-8b33-f45aca8a0690" />




## Kui customer_id IS NULL siis pole mitte andmeviga vaid nö külalisost - kehtiv äriloogika
selliseid oste on :

SELECT COUNT(*) AS külalisostud FROM sales_test WHERE customer_id IS NULL;


Tulemus: selliseid on 1487 tk 

## Puhastamisraport : kustutan duplikaadid:
Duplikaatread eemaldatakse , säilitades igast tellimusest kõige varasem kirje (MIN(id))

delete
--SELECT *
FROM sales_test
WHERE id NOT IN (
    SELECT MIN(id) FROM sales_test GROUP BY invoice_id
);

# Puhastamisraport

| Kategooria                 | Probleeme | Kirjeldus                                   |
|---------------------------|----------:|---------------------------------------------|
| Duplikaadid               | 5116      | Korduvad read mis tuleks eemaldada         |
| Duplikaatsed invoice_id väärtused|4013| Korduvad tellimuse numbrid                 |
| NULL customer_id          | 1487      | ärireegel lubab külalisoste                |
| NULL sale_date            | 0         | Kõigil ridadel on kuupäev olemas           |
| NULL total_price          | 0         | Kõigil ridadel on summa olemas             |
| Tuleviku kuupäevad        | 0         | Tuleviku kuupäevad puuduvad                |
| **Kokku probleeme**       |           |       

# Soovitused
Esmalt tuleks eemaldada duplikaatsed tellimused, sest need mõjutavad otseselt müügitulemusi, aruandeid ja statistikat.
Dokumenteerida süsteemi ärireeglites, et customer_id = NULL tähendab külalisostu. See aitab vältida nende kirjete ekslikku käsitlemist andmevigadena.
Rakendada regulaarne andmekvaliteedi kontroll, mis tuvastab automaatselt:
•	duplikaatsed tellimused;
•	puuduvad väärtused;
•	vigased kuupäevad.
Selline kontroll aitab hoida andmebaasi kvaliteeti ka tulevikus
