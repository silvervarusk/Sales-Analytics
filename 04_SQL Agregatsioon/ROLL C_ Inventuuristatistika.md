# C: Inventuuristatstika 
Koostas : Tiiu Kumar

> "Ülesanne :Analüüsi tootekategooriaid, laoseisu ja müüdud vs laos suhteid."  

Sisend:
Tabelid: products, sales,inventory_movements

---

## 📌 1. Ülevaade tehtud tegevustest

- Tootekategooriate koondandmed .Koosta ülevaade kategooriate kaupa:
- müüdud vs laos: päring mis leiab kategooriad mis on müünud üle 100 ühiku
- Kõige suurem kogus tooteid on müüdud meesteriiete katefoorias: 4121 toodet
- Toodete järjestus kategooria sees 
 
---

## 📊 2. Peamised tulemused

### **2.1. Kõige rohkem tooteid on meesteriiete kategoorias (erinevaid tooteid 82), toote keskmine hind on kõige kallim jalanõude kategoorias.**
- näide
 <img width="516" height="233" alt="image" src="https://github.com/user-attachments/assets/0d5c2b31-7f49-4592-a1a9-b3b45c6b7e5c" />
 
  



### **2.2.  müüdud vs laos**
Kõige suurem kogus tooteid on müüdud meesteriiete katefoorias: 4121 toodet

-  näide

<img width="524" height="309" alt="image" src="https://github.com/user-attachments/assets/be22a78b-1412-42c5-9e14-f3a3b3d2694d" />

  


### **2.3. Toodete järjestus kategooria sees**
-  näide
  
<img width="699" height="342" alt="image" src="https://github.com/user-attachments/assets/a97b001f-e25a-48d5-9929-e804f932d162" />

iga kategooria top 3 tooted:

<img width="670" height="381" alt="image" src="https://github.com/user-attachments/assets/72b1877a-4dd3-4ff7-a5fa-ed4f1243f9de" />

### **2.4. Kvaliteedikontroll: kas toodete fail (products) ei sisalda tuplikaatkirjeid**
- tooteid kokku : **362**  


### **2.5. Päring 2.2.lisa tuvastas et on hulk tooteid, mida on laos palju, kuid viimase 6 kuu jooksul pole müüdud**



## 🧭 3. Kokkuvõte Annale


- Tuvastasime andmete analüüsi käigus, et teatud toodete laovarud on ebaloomulikult kõrged 
võrreldes tegeliku müügitempoga. 

---

### **3.2. Meie soovitus Annale**




## 🛠️ 4. SQL‑skript 
```sql
-- nädal 4 ROLL C 
 --Koosta ülevaade kategooriate kaupa:
SELECT      
p.category,      
COUNT(DISTINCT p.product_id) AS tooteid,      
ROUND(AVG(p.retail_price), 2) AS keskmine_hind,      
MIN(p.retail_price) AS min_hind,      
MAX(p.retail_price) AS max_hind    
FROM products p    
GROUP BY p.category    
ORDER BY tooteid DESC;


---kirjuta ise päring mis leiab kategooriad mis on müünud üle ... ühiku
SELECT
category,
SUM(quantity) AS kogus,
ROUND(AVG(quantity),2) AS keskmine_kogus_toote_kohta,
COUNT(DISTINCT p.product_id) AS toodete_arv
FROM   products p
JOIN sales s ON p.product_id = s.product_id
GROUP BY p.category
HAVING SUM(quantity) > 100
ORDER BY kogus DESC;

--Toodete järjestus kategooria sees — kasuta window function'i:
-- etteantud select , järjestus hinna järgi
SELECT      
p.product_name,      
p.category,      
p.retail_price,      
ROW_NUMBER() OVER (        
  PARTITION BY p.category        
  ORDER BY p.retail_price DESC     
  ) AS koht_kategoorias   
  FROM products p;    
---
--Lisa lisaküsimus: millised tooted on TOP 3 igas kategoorias ja kuidas nende müük on jaotunud?
--top tooted müüdud koguse järgi
WITH toote_myyk AS (
    SELECT
        category,
        product_name,
        SUM(quantity) AS müüdud_kogus,
        ROW_NUMBER() OVER (
            PARTITION BY p.category
            ORDER BY SUM(s.quantity) DESC
        ) AS koht
    FROM products p
    JOIN sales s ON p.product_id = s.product_id
    GROUP BY category, product_name
)
SELECT category, product_name, müüdud_kogus, koht
FROM toote_myyk
WHERE koht <= 3
ORDER BY category, koht;

  -- kontroll
  select COUNT(DISTINCT product_id) from products;
  --tulemus on 362
  select COUNT(product_id) from products;
  -- tulemus on samuti 362 - s.t. et tuplikaatseid tooteid ei ole  

--see päring leiab tooted, mida on laos üle 200 , kuid mida pole viimase 6  kuu jooksul müüdud
  SELECT 
  p.category,
  p.product_name, 
  i.location,
    i.quantity_available, 
    COALESCE(SUM(s.quantity), 0) AS myydud_viimase_6kuuga
FROM products p
JOIN inventory i ON p.product_id = i.product_id
-- Kasutame LEFT JOIN-i, et näha ka müümata tooteid
LEFT JOIN sales s ON p.product_id = s.product_id 
    AND s.sale_date > CURRENT_DATE - INTERVAL '6 month'
WHERE i.quantity_available > 200
GROUP BY p.category, p.product_name, i.location, i.quantity_available
-- HAVING filtreerib grupeeritud tulemust (summat)
HAVING COALESCE(SUM(s.quantity), 0) = 0
ORDER BY quantity_available DESC;

--sellisedi tooteid on 218 tk mida onüle 200 tk ja mida pole müüdud viimase 6 kuu jooksul

```





