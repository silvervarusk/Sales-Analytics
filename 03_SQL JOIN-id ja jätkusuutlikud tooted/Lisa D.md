###  Alaülesanne D

### Millistest linnadest kliendid milliseid kanaleid kasutavad

```sql
SELECT
    s.channel AS müügikanal,
    c.city AS linn,
    COUNT(DISTINCT c.customer_id) AS kliente,
    SUM(s.total_price) AS kogumüük
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY s.channel, c.city
ORDER BY müügikanal, kogumüük DESC;
```

<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="287" height="444" alt="image" src="https://github.com/user-attachments/assets/b6d79427-3430-41bf-899e-47dc1516367d" />
</details> 

 
Ühenda 3 tabelit: `sales` + `customers` + `products

```sql
SELECT
    s.channel AS müügikanal,
    p.category AS tootekategooria,
    COUNT(DISTINCT c.customer_id) AS kliente,
    COUNT(s.sale_id) AS oste,
    SUM(s.total_price) AS kogumüük,
    ROUND(AVG(s.total_price), 2) AS keskmine_ost
FROM sales s
INNER JOIN customers c
    ON s.customer_id = c.customer_id
INNER JOIN products p
    ON s.product_id = p.product_id
GROUP BY s.channel, p.category
ORDER BY müügikanal, kogumüük DESC;
```
<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="496" height="450" alt="image" src="https://github.com/user-attachments/assets/46fbb5a1-52fb-4f97-9ae9-be84d90b41dd" />
</details


### Kõige efektiivsem kanal

```sql
SELECT
    s.channel AS müügikanal,
    COUNT(DISTINCT s.customer_id) AS kliente,
    SUM(s.total_price) AS kogumüük,
    ROUND(
        SUM(s.total_price) /
        NULLIF(COUNT(DISTINCT s.customer_id), 0),
        2
    ) AS müük_per_klient
FROM sales s
GROUP BY s.channel
ORDER BY müük_per_klient DESC;
```

<details>
<summary> Tulemus (click to expand)</summary>
  
<img width="307" height="447" alt="image" src="https://github.com/user-attachments/assets/5435cc93-42b1-4a77-b583-77a862134ba8" />
</details
