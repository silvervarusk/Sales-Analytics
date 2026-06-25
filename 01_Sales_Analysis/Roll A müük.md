#  ROLL A
### Mitu rida on sales tabelis?   
-- Mitu toodet on kokku?

SELECT COUNT() AS ridade_arv FROM sales;    `
* 15234


###  Too välja esimesed 10 rida:
-- Millised veerud ja andmed tabelis on?    

SELECT  FROM sales LIMIT 10;        

<details>
  
<summary>📊 Sales  </summary>
  
![Sales Image](sales.png)
</details>

### Tallinna kaupluse tehingud (15)
   
SELECT  FROM sales    WHERE store_location = 'Tallinn'    ORDER BY sale_date DESC    LIMIT 15;    `


<details>
<summary> Tabeli vaade (click to expand)</summary>


| sale_id | invoice_id       | sale_date  | customer_id | product_id | qty | unit_price | total | channel | location | payment |
|--------|------------------|-----------|-------------|------------|-----|------------|-------|---------|----------|---------|
| 4387   | INV-202401-00095 | 2026-06-28 | 2739        | 1258       | 3   | 84.41      | 253.23 | pood    | Tallinn  | järelmaks |
| 3567   | INV-202311-00062 | 2026-06-27 | null        | 1198       | 2   | 291.72     | 583.44 | pood    | Tallinn  | kaart |
| 5609   | INV-202404-00255 | 2026-05-18 | 3279        | 1313       | 1   | 77.60      | 77.60  | pood    | Tallinn  | kaart |
| 8610   | INV-202411-00111 | 2026-04-26 | 4450        | 1217       | 3   | 34.04      | 102.12 | pood    | Tallinn  | järelmaks |
| 7057   | INV-202407-00366 | 2026-03-21 | 2221        | 1258       | 2   | 84.41      | 168.82 | pood    | Tallinn  | järelmaks |
| 4758   | INV-202402-00151 | 2026-03-20 | 3130        | 1224       | 1   | 222.10     | 222.10 | pood    | Tallinn  | sularaha |
| 7724   | INV-202409-00011 | 2026-03-18 | 4178        | 1274       | 1   | 234.79     | 234.79 | pood    | Tallinn  | kaart |
| 934    | INV-202304-00051 | 2026-03-17 | 4113        | 1082       | 3   | 100.93     | 302.79 | pood    | Tallinn  | kaart |
| 5802   | INV-202405-00035 | 2026-03-05 | 2619        | 1276       | 2   | 187.16     | 374.32 | pood    | Tallinn  | järelmaks |
| 8835   | INV-202411-00336 | 2026-01-25 | null        | 1092       | 3   | 144.20     | 432.60 | pood    | Tallinn  | kaart |
| 3816   | INV-202311-00311 | 2026-01-17 | 4404        | 1107       | 1   | 279.43     | 279.43 | pood    | Tallinn  | sularaha |
| 3595   | INV-202311-00090 | 2026-01-01 | 2997        | 1298       | 1   | 163.53     | 163.53 | pood    | Tallinn  | sularaha |
| 4520   | INV-202401-00228 | 2025-12-20 | null        | 1296       | 1   | 301.97     | 301.97 | pood    | Tallinn  | kaart |
| 276    | INV-202302-00015 | 2025-12-14 | 2221        | 1316       | 1   | 296.58     | 296.58 | pood    | Tallinn  | kaart |
| 4963   | INV-202403-00022 | 2025-12-10 | 4534        | 1095       | 4   | 140.64     | 562.56 | pood    | Tallinn  | järelmaks |

</details>


### -- 10 suurimat tehingut 
SELECT  FROM sales ORDER BY total_price DESC LIMIT 10;  
  
   <details>
<summary> 10 Suurimat tehingut (click to expand)</summary>
     
<img width="1156" height="399" alt="image" src="https://github.com/user-attachments/assets/a06ce05f-2882-4930-95f8-afdbfd2ab8ba" />
</details>


### -- 10 väikseimat tehingut   
SELECT  *FROM sales ORDER BY total_price ASC LIMIT 10;      
   <details>
<summary> 10 Väiksemat tehingut (click to expand)</summary>
     
<<img width="1158" height="388" alt="image" src="https://github.com/user-attachments/assets/ec0eb53b-b881-496c-993f-61d8e6d5a484" />
</details>  


  
## NULL väärtusi olulistes veergudes
--Mitu rida, kus kliendi info on puudu?    
SELECT COUNT() - COUNT(customer_id) AS puuduv_klient    FROM sales;    `

| puuduv_klient |
| ------------- |
| 1487          |

### --Kõik unikaalsed müügikanalid, mis müügitabelis esinevad  
SELECT DISTINCT channel FROM sales;   
| channel |
| ------- |
| online  |
| pood    |

### tehingute arv iga kaupluse kohta:
SELECT store_location, COUNT() AS tehinguid   FROM sales   GROUP BY store_location   ORDER BY tehinguid DESC;   
SELECT  *FROM sales ORDER BY total_price ASC LIMIT 10;      
   <details>
<summary> Tabel (click to expand)</summary>
     
<img width="200" height="168" alt="image" src="https://github.com/user-attachments/assets/2de7a202-cea3-4d06-990e-d498b7a9b186" />

</details> 

### Tehingud, kus summa on üle 100 EUR JA kauplus on Tallinnas:
sales   WHERE total_price > 100 AND store_location = 'Tallinn'   ORDER BY total_price DESC;   `
<details>
<summary>📊 Full Sales Dataset (click to expand)</summary>

| sale_id | invoice_id       | sale_date  | customer_id | product_id | quantity | unit_price | total_price | channel | store_location | payment_method |
| ------- | ---------------- | ---------- | ----------- | ---------- | -------- | ---------- | ----------- | ------- | -------------- | -------------- |
| 8379    | INV-202410-00273 | 2024-10-06 | 2712        | 1210       | 5        | 374.54     | 1872.70     | pood    | Tallinn        | kaart          |
| 8379    | INV-202410-00273 | 2024-10-06 | 2712        | 1210       | 5        | 374.54     | 1872.70     | pood    | Tallinn        | kaart          |
| 3441    | INV-202310-00264 | 2023-10-03 | 2707        | 1134       | 5        | 371.79     | 1858.95     | pood    | Tallinn        | sularaha       |
| 7543    | INV-202408-00341 | 2024-08-06 | 2961        | 1042       | 5        | 347.84     | 1739.20     | pood    | Tallinn        | kaart          |
| 9684    | INV-202501-00242 | 2025-01-15 | 2288        | 1031       | 4        | 434.08     | 1736.32     | pood    | Tallinn        | kaart          |
| 9684    | INV-202501-00242 | 2025-01-15 | 2288        | 1031       | 4        | 434.08     | 1736.32     | pood    | Tallinn        | kaart          |
| 3644    | INV-202311-00139 | 2023-11-03 | 3166        | 1009       | 5        | 332.55     | 1662.75     | pood    | Tallinn        | kaart          |
| 144     | INV-202301-00144 | 2023-01-07 | 3446        | 1009       | 5        | 332.55     | 1662.75     | pood    | Tallinn        | järelmaks      |
| 2503    | INV-202308-00080 | 2023-08-27 | 2397        | 1069       | 4        | 402.62     | 1610.48     | pood    | Tallinn        | järelmaks      |
| 9588    | INV-202501-00146 | 2025-01-13 | 2687        | 1049       | 5        | 308.84     | 1544.20     | pood    | Tallinn        | järelmaks      |
| 4470    | INV-202401-00178 | 2024-01-20 | 4791        | 1049       | 5        | 308.84     | 1544.20     | pood    | Tallinn        | sularaha       |
| 9001    | INV-202412-00109 | 2024-12-01 | 3367        | 1149       | 5        | 304.14     | 1520.70     | pood    | Tallinn        | järelmaks      |
| 9212    | INV-202412-00320 | 2024-12-04 | 4178        | 1295       | 4        | 375.34     | 1501.36     | pood    | Tallinn        | järelmaks      |
| 9212    | INV-202412-00320 | 2024-12-04 | 4178        | 1295       | 4        | 375.34     | 1501.36     | pood    | Tallinn        | järelmaks      |
| 9212    | INV-202412-00320 | 2024-12-04 | 4178        | 1295       | 4        | 375.34     | 1501.36     | pood    | Tallinn        | järelmaks      |
| 8239    | INV-202410-00133 | 2024-10-05 | 4368        | 1210       | 4        | 374.54     | 1498.16     | pood    | Tallinn        | kaart          |
| 2822    | INV-202308-00399 | 2023-08-20 | 2629        | 1134       | 4        | 371.79     | 1487.16     | pood    | Tallinn        | sularaha       |
| 2822    | INV-202308-00399 | 2023-08-20 | 2629        | 1134       | 4        | 371.79     | 1487.16     | pood    | Tallinn        | sularaha       |
| 209     | INV-202301-00209 | 2023-01-19 | null        | 1108       | 4        | 371.05     | 1484.20     | pood    | Tallinn        | sularaha       |
| 209     | INV-202301-00209 | 2023-01-19 | null        | 1108       | 4        | 371.05     | 1484.20     | pood    | Tallinn        | sularaha       |
| 1038    | INV-202304-00155 | 2023-04-20 | 4505        | 1281       | 5        | 292.61     | 1463.05     | pood    | Tallinn        | järelmaks      |
| 4921    | INV-202402-00314 | 2024-02-19 | 2327        | 1240       | 4        | 356.57     | 1426.28     | pood    | Tallinn        | järelmaks      |
| 4921    | INV-202402-00314 | 2024-02-19 | 2327        | 1240       | 4        | 356.57     | 1426.28     | pood    | Tallinn        | järelmaks      |
| 9056    | INV-202412-00164 | 2024-12-11 | null        | 1338       | 5        | 282.29     | 1411.45     | pood    | Tallinn        | sularaha       |
| 4221    | INV-202312-00388 | 2023-12-05 | 2412        | 1293       | 4        | 351.33     | 1405.32     | pood    | Tallinn        | kaart          |
| 9792    | INV-202502-00022 | 2025-02-10 | null        | 1150       | 5        | 280.02     | 1400.10     | pood    | Tallinn        | sularaha       |

</details>





