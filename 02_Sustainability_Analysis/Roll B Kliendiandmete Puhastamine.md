# Kliendiandmete Puhastamine
##### Koostas: Silver Varusk

## Test tabeli loomine
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

| Kategooria                  | Leitud probleeme |
|---------------------------|------------------|
| Duplikaatsed e-mailid     | 129              |
| NULL eesnimi              | 0                |
| NULL perenimi             | 0                |
| Ebajärjekindlad linnanimed| 54 (unikaalsed)  |
| NULL telefon/e-mail       | 380              |
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

## Null väärtuste puhastamine

```sql
UPDATE customers_test
SET first_name = 'Tundmatu'
WHERE first_name IS NULL OR first_name = 
```

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="219" height="43" alt="image" src="https://github.com/user-attachments/assets/bb98376a-ba9b-40e4-b206-f7538166b6d8" />

</details> 

### Linnanimede ühtlustamine INITCAP + TRIM abil

```sql
UPDATE customers_test
SET city = INITCAP(TRIM(city))
WHERE city != INITCAP(TRIM(city));
```
<details>
<summary> Tulemus (click to expand)</summary>   
<img width="231" height="67" alt="image" src="https://github.com/user-attachments/assets/351bfa5e-da62-41a8-87a7-cd6f507ac186" />

</details> 

## E-Mailide standardiseerimine väiketähtedeks

```sql
UPDATE customers_test
SET email = LOWER(TRIM(email))
WHERE email != LOWER(TRIM(email));
```
<details>
<summary> Tulemus (click to expand)</summary>   
<img width="237" height="49" alt="image" src="https://github.com/user-attachments/assets/2e1c4f6a-7a89-4dc9-9417-28a4463ade3a" />
</details> 

## Tulemuste kontroll ja vaatlemine Vana vs UUS

```sql
SELECT city, COUNT(*) AS arv
FROM customers_test
GROUP BY city ORDER BY city;
```
<details>
<summary>Tulemus (click to expand)</summary>

<table>
  <tr>
    <td align="center">
      <strong>Vana</strong><br>
      <img width="157" height="404" src="https://github.com/user-attachments/assets/f277c8f3-640d-44d3-ada5-50c9ee548f08" />
    </td>
    <td align="center">
      <strong>Uus</strong><br>
      <img width="168" height="414" src="https://github.com/user-attachments/assets/c3ab6972-d795-4542-9245-64776ae08b3a" />
    </td>
  </tr>
</table>

</details>

## Telefoni numbrite standardiseerimine:
```sql
SELECT phone,
    CASE
        WHEN phone LIKE '+372%' THEN phone
        WHEN phone LIKE '372%' THEN '+' || phone
        WHEN LENGTH(phone) = 7 THEN '+372' || phone
        ELSE phone
    END AS standardne_telefon
FROM customers_test
WHERE phone IS NOT NULL
LIMIT 10;
```
Tulemus:

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="246" height="289" alt="image" src="https://github.com/user-attachments/assets/1e294ccd-2421-4bc1-96d3-71e6152650cc" />

</details>  

## Muudatuse kontroll, kas midagi muutus:
```sql
SELECT 
    phone AS vana,
    CASE
        WHEN phone LIKE '+372%' THEN phone
        WHEN phone LIKE '372%' THEN '+' || phone
        WHEN LENGTH(phone) = 7 THEN '+372' || phone
        ELSE phone
    END AS uus
FROM customers
WHERE phone IS NOT NULL
AND phone !=
    CASE
        WHEN phone LIKE '+372%' THEN phone
        WHEN phone LIKE '372%' THEN '+' || phone
        WHEN LENGTH(phone) = 7 THEN '+372' || phone
        ELSE phone
    END;
```

<details>
<summary> Tulemus (click to expand)</summary>   
<img width="346" height="117" alt="image" src="https://github.com/user-attachments/assets/71b2cf47-6cfa-4caf-899f-b105b226e53e" />

</details> 


