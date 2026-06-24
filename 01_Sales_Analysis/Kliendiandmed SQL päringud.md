# Klientide arv kokku 
SELECT COUNT() AS klientide_arv FROM customers;  
  
3150 


# Andmete struktuur ülevaade
SELECT  *FROM customers LIMIT 10;    
![Customers Image](CUSTOMERS.jpg)

# Nimekiri linnadest
-- (Unikaalsed, Suure algustähega, tühikuteta)  
SELECT DISTINCT INITCAP(TRIM(city)) AS city
FROM customers;  

Tulemus
Kliendi ostud linnadest 12 erinvat asukohta:  
  
Pärnu
Paide
Jõhvi
Tallinn
Narva
Võru
Viljandi
Rakvere
Haapsalu
Valga
Tartu
Kuressaare  

# Tallinna kliendid (15 tükki)

SELECT *
FROM customers
WHERE city = 'Tallinn'
ORDER BY last_name ASC
LIMIT 15;  

# Registeerimine 
 SELECT MIN(registration_date) AS vanim,           MAX(registration_date) AS uusim    FROM customers;
   `  
Vanim 2020-01-02  
Uusim 2025-02-27

# -- Puuduvate väärtuste kontroll

--eesnimedede kontroll  
SELECT COUNT(*) - COUNT(first_name) AS puuduvad_eesnimed    FROM customers;
0 Kõigil on olemas eesnimi  

--E-post kontroll
SELECT COUNT(*) - COUNT(email) AS puuduvad_emailid    FROM customers;    `
Tulemus 380 puuduvad e-maili  

# Lühike kokkuvõte:
 * Anmdestikku tuleb puhastada  
 *Erinevates formaatides:  -City  Linna nimeded  algavad väikese või suurte tähtedega,   
 *Mõned andmestikud on puudulikud: Kõikidel klientidel pole e-mail aadressi registeeritud.  
 * Andmetes on duplikaat entrid  








