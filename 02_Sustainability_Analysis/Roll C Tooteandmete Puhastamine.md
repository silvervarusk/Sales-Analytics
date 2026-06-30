<img width="135" height="48" alt="image" src="https://github.com/user-attachments/assets/5d4fd798-cd95-4137-a223-0e21131755bb" />
# Roll C Tooteandmete Puhastamine
#####  Koostas: Silver Varusk

## Test koopia ja ridade arvu kontroll:

```sql
CREATE TABLE products_test AS SELECT * FROM products;
SELECT COUNT(*) AS ridade_arv FROM products_test;
```

<details>
<summary> Tulemus (click to expand)</summary>
     
<img width="103" height="69" alt="image" src="https://github.com/user-attachments/assets/ffe0a1f9-db96-46b9-93d5-4e32fc4799f1" />
</details> 

## Duplikaadid: Korduvad tootenimed

```sql
SELECT product_name, COUNT(*) AS koopiate_arv
FROM products_test
GROUP BY product_name
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;

```
##### Kokku on 12 rida, kus on korduv tootenime.

<details>
  <summary>Vaata tabelit (click to expand)</summary>

<img width="285" height="345" alt="image" src="https://github.com/user-attachments/assets/5e5582a1-8ddc-4703-a5a0-f859934bc06b" />

</details>

## NULL väärtused kriitilistes väljades:

```sql
SELECT
    COUNT(*) FILTER (WHERE product_name IS NULL OR product_name = '') AS null_nimi,
    COUNT(*) FILTER (WHERE category IS NULL OR category = '') AS null_kategooria,
    COUNT(*) FILTER (WHERE retail_price IS NULL) AS null_jaehind,
    COUNT(*) FILTER (WHERE cost_price IS NULL) AS null_omahind
FROM products_test;
```
Kriitilistes väljades ei ole praeguse andmete järgi null andmeid.

<details>
  <summary>Supabase vaade (click to expand)</summary>
<img width="307" height="52" alt="image" src="https://github.com/user-attachments/assets/1661d99d-1cb2-48a9-bbb3-da90bc79e990" />


</details>

# Andmete loogika kontroll: Ebareaalsed hinnad 
  
##### -- Kas on negatiivseid hindu?
```sql

SELECT COUNT(*) AS negatiivne_hind
FROM products_test
WHERE retail_price < 0;
```
Tulemus:  Negatiivsed hinnad puuduvad

<details>
  <summary>Supabase vaade (click to expand)</summary>
<img width="135" height="48" alt="image" src="https://github.com/user-attachments/assets/4398ce5d-d634-490b-a7fb-6b9c64fd3c27" />

</details>





##### -- Kas on äärmuslikke hindu (> 1000€)?

Tulemus: Toodete seal pole hindu mis on rohkem kui 1000 EUR
```sql

SELECT product_name, retail_price
FROM products_test
WHERE retail_price > 1000
ORDER BY retail_price DESC;
```

<details>
  <summary>Supabase vaade (click to expand)</summary>
<img width="349" height="248" alt="image" src="https://github.com/user-attachments/assets/64fd13c7-68b0-4d5f-afd9-b40d8e2767f6" />>

</details>


##### Kategooriate järjekindlus
Tulemus: 

```sql
SELECT category, COUNT(*) AS arv
FROM products_test
GROUP BY category
ORDER BY category;
```
<details>
  <summary>Supabase vaade (click to expand)</summary>
<img width="159" height="159" alt="image" src="https://github.com/user-attachments/assets/a108b10f-852f-4c0a-8821-7c6f5bf2a147" />


</details>


## Puhastamisraport:
KVALITEEDIKONTROLL:
☐ Test koopia on loodud (mitte production tabelil!)
☐ Duplikaadid ja NULL-id on tuvastatud
☐ Raport sisaldab konkreetseid numbreid
Hetkeseiguga: probleem mõjutab tooteanalüüsi kõige rohkem  

| Kategooria                     | Leitud probleeme | Kirjeldus                                   |
|--------------------------------|------------------|---------------------------------------------|
| Duplikaatsed nimed             | ?                | Sama tootenimi mitu korda                   |
| NULL nimi/hind                 | ?                | Puuduvad kriitilised väljad                 |
| Loogilised vead                | ?                | Negatiivne või äärmuslik jaehind            |
| Ebajärjekindlad kategooriad    | ?                | Erinevad nimekujud (Shoes vs shoes)         |
| NULL omahind/kategooria        | ?                | Puuduv klassifitseerimine                  |
| KOKKU probleeme               | ?                |                                             |



##  Andmete puhastamine

##### Ühtlusta kategooriate nime
```sql
UPDATE products_test
SET category = INITCAP(TRIM(category))
WHERE category != INITCAP(TRIM(category));
```

#####  Kontrolli tulemust
```sql
SELECT category, COUNT(*) AS arv
FROM products_test
GROUP BY category ORDER BY category;
```
<details>

  <summary> Tulemuse võrdlemine </summary>   
<p align="center">
  <b>Enne</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <b>Pärast</b>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/a108b10f-852f-4c0a-8821-7c6f5bf2a147" width="200"/>
  <img src="https://github.com/user-attachments/assets/3c0b0982-c325-4011-9475-329b8682e1ce" width="200"/>
</p>

</details>

##### Kategooriate standardiseerimine kasutades CASE WHEN

```sql
UPDATE products_test
SET category = CASE
    WHEN LOWER(TRIM(category)) IN ('shoes', 'jalanõud', 'footwear') THEN 'Shoes'
    WHEN LOWER(TRIM(category)) IN ('shirts', 'särgid', 'tops') THEN 'Shirts'
    WHEN LOWER(TRIM(category)) IN ('pants', 'püksid', 'trousers') THEN 'Pants'
    ELSE INITCAP(TRIM(category))
END;
```
Kontroll visuaalne:
Vana:

### Kontroll visuaalne

<details>
     
 <summary> Vana vs uus </summary>   
 
**Vana**  

<img width="955" height="384" alt="image" src="https://github.com/user-attachments/assets/fc643c78-6669-415a-8d75-3ea2078e48e6" />

**Uus**  
<img width="963" height="376" alt="image" src="https://github.com/user-attachments/assets/2e32a3a1-d5e8-4c05-bc3a-0b2b5abb4730" />


</details>

