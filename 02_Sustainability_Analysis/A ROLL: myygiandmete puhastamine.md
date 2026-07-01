# Müügiandmete puhastamine
## Roll A :müügiandmete puhastaja
Koostas: Tiiu Kumar
## Ülesanne :leida duplikaadid, NULL väärtused ja vigased kuupäevad sales-tabelis.
## Puhasta ja dokumenteeri kõik muudatused
'''sql
CREATE TABLE sales_test AS SELECT * FROM sales;
'''sql

##Leia NULL väärtused kriitilistes väljades:
'''sql
SELECT
    COUNT(*) FILTER (WHERE customer_id IS NULL) AS null_customer_id,
    COUNT(*) FILTER (WHERE sale_date IS NULL) AS null_sale_date,
    COUNT(*) FILTER (WHERE total_price IS NULL) AS null_total_price
FROM sales_test;
'''sql

Tulemus: 1487 NULL customer_id, 0 NULL sale_date, 0 NULL total_price

##Kontrolli kuupäevade formaati — kas on tuleviku kuupäevi?
'''sql
SELECT COUNT(*) AS tuleviku_kuupaevad
FROM sales_test
WHERE sale_date > CURRENT_DATE;
'''sql
Tulemus: 0 tuleviku kuupäeva.

##Leia duplikaadid — millised tellimused korduvad?
duplikaadid invoice_id järgi
'''sql
SELECT  invoice_id, COUNT(*) AS koopiate_arv
FROM sales_test
GROUP BY invoice_id
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;
'''sql
duplikaatseid invoice_id on 4013 tk

##Loe kokku duplikaatsete ridade arv:
'''sql
SELECT COUNT(*) AS duplikaat_read
FROM sales_test
WHERE id NOT IN (
    SELECT MIN(id)
    FROM sales_test
    GROUP BY invoice_id
);
'''sql

Tulemus: 5116 rida on duplikaadid

##Kui customer_id IS NULL siis pole mitte andmeviga vaid nö külalisost - kehtiv äriloogika
selliseid oste on :
'''sql
SELECT COUNT(*) AS külalisostud FROM sales_test WHERE customer_id IS NULL;
'''sql

Tulemus: selliseid on 1487 tk 

## Puhastamisraport : kustutan duplikaadid:
'''sql

delete
--SELECT *
FROM sales_test
WHERE id NOT IN (
    SELECT MIN(id) FROM sales_test GROUP BY invoice_id
);

'''sql

| Kategooria                 | Probleeme | Kirjeldus                                   |
|---------------------------|----------:|---------------------------------------------|
| Duplikaadid               | 5116      | Korduvad invoice_id väärtused              |
| NULL customer_id          | 0         | ärireegel lubab külalisoste                |
| NULL sale_date            | 0         | Kõigil ridadel on kuupäev olemas           |
| NULL total_price          | 0         | Kõigil ridadel on summa olemas             |
| Tuleviku kuupäevad        | 0         | Tuleviku kuupäevad puuduvad                |
| **Kokku probleeme**       |           |       

##Soovitus
Eemaldada duplikaat tellimusread (5116 tk)
Kui kliendi id on puudu võib raportitesse lisada selle asemel ajutise sildi 'külalisost'
