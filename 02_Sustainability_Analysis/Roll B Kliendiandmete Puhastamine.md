# Kliendiandmete Puhastamine
##### Koostas: Silver Varusk

```sql
CREATE TABLE customers_test AS SELECT * FROM customers;
SELECT COUNT(*) AS ridade_arv FROM customers_test;
```
Tulemis:3150 rida

<details>
<summary> Tulemus (click to expand)</summary>
     
<img width="89" height="52" alt="image" src="https://github.com/user-attachments/assets/7d618a24-7405-46bf-ac90-ac125e6c9fc8" />
</details> 

## Duplikaatsed e-mailid.

Tulemus: 129 duplikaatset e-maili.
```sql

SELECT email, COUNT(*) AS koopiate_arv
FROM customers_test
GROUP BY email
HAVING COUNT(*) > 1
ORDER BY koopiate_arv DESC;
```

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="257" height="405" alt="image" src="https://github.com/user-attachments/assets/dc9bcf49-7290-417f-8ab6-bc56ece37dc4" />
</details> 

## Puuduvad nimed

```sql
SELECT
    COUNT(*) FILTER (WHERE first_name IS NULL OR first_name = '') AS null_eesnimi,
    COUNT(*) FILTER (WHERE last_name IS NULL OR last_name = '') AS null_perenimi
FROM customers_test;
```
Tulemus: Puuduvaid nimesi ei esinenud
<details>
<summary> Tulemus (click to expand)</summary>   
<img width="181" height="63" alt="image" src="https://github.com/user-attachments/assets/545dbf7a-074b-431c-8acd-da27ce7b3831" />
</details> 

 ## Linnade kirjapildi kontroll
 
```sql
SELECT city, COUNT(*) AS arv
FROM customers_test
GROUP BY city
ORDER BY city;
```
Kirjapildis on ebajärjekindlusi, vajab puhastamist. Hetkel 54 erinevat linna.

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="173" height="411" alt="image" src="https://github.com/user-attachments/assets/f47ade35-b6d8-474d-a2ab-c5cc92d9acb1" />

</details> 

## Kontakt andmete kontroll

```sql
SELECT
    COUNT(*) FILTER (WHERE phone IS NULL OR phone = '') AS null_telefon,
    COUNT(*) FILTER (WHERE email IS NULL OR email = '') AS null_email
FROM customers_test;
```

Tulemus: Esineb 380 e-maili null väärtusega.

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="163" height="58" alt="image" src="https://github.com/user-attachments/assets/477704b7-e1a5-4d02-a6ba-3576965aed61" />
</details> 


## Puhastamisraport:Andmekvaliteedi probleemid

| Kategooria                  | Leitud probleeme | Kirjeldus                                   |
|---------------------------|------------------|---------------------------------------------|
| Duplikaatsed e-mailid     | ?                | Sama e-mail mitmel kliendil                 |
| NULL eesnimi              | ?                | Puuduv kliendi eesnimi                      |
| NULL perenimi             | ?                | Puuduv kliendi perenimi                     |
| Ebajärjekindlad linnanimed| ?                | Erinevad nimekujud (nt tallinn vs Tallinn)  |
| NULL telefon/e-mail       | ?                | Puuduvad kontaktandmed                      |
| **KOKKU probleeme**       | ?                |                                             |

---

## Soovitus

Kõige rohkem mõjutab igapäevast tööd **NULL telefon/e-mail**, sest:
- kliendiga ei saa ühendust  
- müük ja klienditugi katkeb  
- protsessid jäävad seisma  

Teiseks kriitiline probleem on **duplikaatsed e-mailid**, mis võivad põhjustada:
- valeandmeid aruandluses  
- dubleeritud suhtlust  
- segadust kliendihalduses
