#  ROLL A
### Mitu rida on sales tabelis?   
-- Mitu toodet on kokku?

SELECT COUNT() AS ridade_arv FROM sales;    `
* 15234


###  Too välja esimesed 10 rida:
-- Millised veerud ja andmed tabelis on?    

SELECT  FROM products LIMIT 10;    

<details>
  
<summary>📊 Sales  </summary>
  
![Sales Image](sales.png)
</details>



### Milliseid kategooriaid UrbanStyle müüb?  
-- Kõik unikaalsed tootekategooriad    

SELECT DISTINCT category FROM products; 
| 👟 Jalanõud | 👶 Laste riided | 🎒 Aksessuaarid | 👗 Naiste riided | 👔 Meeste riided |
|------------|----------------|----------------|-----------------|-----------------| 

### Kalleimad ja odavaimad tooted
-- 10 kallemat toodet    
SELECT product_name, category, price    FROM products    ORDER BY price DESC    LIMIT 10;


