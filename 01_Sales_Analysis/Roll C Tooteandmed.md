### -- Mitu toodet on kokku?    
SELECT COUNT(*) AS toodete_arv FROM products;  
Vastus; 362 
<img width="940" height="533" alt="image" src="https://github.com/user-attachments/assets/4809625b-0802-40cf-8cb3-5601a1bc9631" />  


### -- Millised veerud ja andmed tabelis on?    SELECT  FROM products LIMIT 10;  
<img width="940" height="464" alt="image" src="https://github.com/user-attachments/assets/a348df19-8e77-40b4-9817-2b2199b338ef" />

### Uuri tootekategooriad. Milliseid kategooriaid UrbanStyle müüb?
-- Kõik unikaalsed tootekategooriad    
SELECT DISTINCT category FROM products;  

<img width="940" height="901" alt="image" src="https://github.com/user-attachments/assets/8b8f45c9-6710-4424-8ca2-1a17d584736c" />  

### Uuri hinnavahemikku. Leia kalleimad ja odavaimad tooted:
-- 10 kallemat toodet    
SELECT product_name, category, price    FROM products    ORDER BY price DESC    LIMIT 10;  
<img width="940" height="813" alt="image" src="https://github.com/user-attachments/assets/d58dcad0-464f-4fcb-ae29-476ae44b71f7" />  

-- 10 odavamat toodet    SELECT product_name, category, price    FROM products    ORDER BY price ASC    LIMIT 10;    
<img width="696" height="636" alt="image" src="https://github.com/user-attachments/assets/da03eb65-8643-46d2-b78c-bd2e0b6cc437" />  

### Filtreeri kategooria järgi. Vali üks kategooria ja uuri selle tooteid:  
-- Näite: kõik kindla kategooria tooted    
SELECT  FROM products    WHERE category = 'Kleidid'    ORDER BY price DESC;  
<img width="1090" height="690" alt="image" src="https://github.com/user-attachments/assets/705bd8ca-3824-4a50-b67f-90f9c7713150" />  

### 1. Kontrolli puuduvaid väärtusi:
-- Puuduvad hinnad    SELECT COUNT() - COUNT(price) AS puuduvad_hinnad    FROM products;  
<img width="843" height="502" alt="image" src="https://github.com/user-attachments/assets/6787f92c-3897-4bd3-85fa-48a1356a4108" />  

### Puuduvad kategooriad    SELECT COUNT() - COUNT(category) AS puuduvad_kategooriad    FROM products;  

<img width="1090" height="644" alt="image" src="https://github.com/user-attachments/assets/17fa5454-6548-4d8d-82d8-078357bec25e" />

### 1. Kirjuta kokkuvõte. Mitu toodet on? Millised kategooriad? Hinnavahemik? Puuduvad andmed?  
KVALITEEDIKONTROLL:  
☐ Vähemalt 3 SQL päringut töötavad ilma veata
☐ Kategooriad ja hinnavahemik on tuvastatud
☐ Kokkuvõte sisaldab konkreetseid numbreid (mitu toodet, min/max hind jne)


