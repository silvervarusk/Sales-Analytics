# Roll C Tooted + Inventuur 
##### Koostas Silver Varusk

### LEFT JOIN: kõik tooted, ka need mis pole müüdud 

```sql
SELECT
    p.product_name,
    p.category,
    p.subcategory,
    p.retail_price,
    s.sale_id
FROM products p
LEFT JOIN sales s 
    ON p.product_id = s.product_id
WHERE s.sale_id IS NULL; 
```

<details>
<summary> Tulemus (click to expand)</summary>
     
<img width="459" height="412" alt="image" src="https://github.com/user-attachments/assets/2bb0100c-2bba-4f8d-968a-20544c7ad677" />
</details> 

### Müümata tooted kokku:
```sql
SELECT COUNT(*) AS müümata_tooteid    FROM products p    LEFT JOIN sales s ON p.product_id = s.product_id    WHERE s.sale_id IS NULL;
```

<details>
<summary> Tulemus (click to expand)</summary>
     
<img width="158" height="104" alt="image" src="https://github.com/user-attachments/assets/cde4b6bb-73d2-4979-8878-105a5509d34b" />
</details> 

### Enim müüdud tooted:
```sql
SELECT        p.product_name,        p.category,        p.subcategory,        COUNT(s.sale_id) AS müüdud_kordi,        SUM(s.total_price) AS kogumüük    FROM products p    INNER JOIN sales s ON p.product_id = s.product_id    GROUP BY p.product_id, p.product_name, p.category, p.subcategory    ORDER BY kogumüük DESC    LIMIT 10;    
```
<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="539" height="438" alt="image" src="https://github.com/user-attachments/assets/d5c8bfc5-a887-4f26-84a2-d647af270831" />
</details> 

### Analüüsi kategooriate kaupa:
```sql
SELECT
    p.category,
    COUNT(DISTINCT p.product_id) AS tooteid,
    COUNT(s.sale_id) AS müüke,
    SUM(s.total_price) AS kogumüük
FROM products p
LEFT JOIN sales s ON p.product_id = s.product_id
GROUP BY p.category
ORDER BY kogumüük DESC;
```

<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="381" height="452" alt="image" src="https://github.com/user-attachments/assets/5a33109f-8caa-4914-8853-3e165163e2e7" />
</details> 

### Ühenda inventuuriga — millised tooted on laos?
```sql
SELECT
    p.product_name,
    p.category,
    i.location,
    i.quantity_available,
    i.reorder_point,
    CASE
        WHEN i.quantity_available <= i.reorder_point THEN 'TELLI JUURDE'
        ELSE 'OK'
    END AS staatus
FROM products p
LEFT JOIN inventory i ON p.product_id = i.product_id
ORDER BY i.quantity_available ASC;
```

<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="562" height="440" alt="image" src="https://github.com/user-attachments/assets/447c2866-6282-407b-bb45-ed30ef9ce732" />
</details> 
Tähelepanek: Laoseisus on negatiivsed numbrid - Pole loogiline

### Ühenda kolm tabelit: leia tooted, mis on laos, aga pole kunagi müüdud — topelt kahju (laoseis + müümata):

SELECT
    p.product_name,
    p.category,
    p.retail_price,
    i.quantity_available,
    (p.retail_price * i.quantity_available) AS kinni_olev_raha
FROM products p
LEFT JOIN sales s
    ON p.product_id = s.product_id
LEFT JOIN inventory i
    ON p.product_id = i.product_id
WHERE s.sale_id IS NULL
  AND i.quantity_available > 0
ORDER BY kinni_olev_raha DESC;

Järeldus: Selliseid tooteid praegu puudub




<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="552" height="388" alt="image" src="https://github.com/user-attachments/assets/96c93c4f-13d0-4b77-82f7-a9b2f3cdcd4a" />


</details> 










