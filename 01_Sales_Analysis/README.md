# 📊 WEEK 1 — Müügiosakond

## 🛍️ Kategooriad
| 👟 Jalanõud | 👶 Laste riided | 🎒 Aksessuaarid | 👗 Naiste riided | 👔 Meeste riided |
|------------|----------------|----------------|-----------------|-----------------|

---
## 🧱 Table view Andmestruktuuridest 


<details>  
<summary>📊  Customers</summary>
  
![Customers Image](CUSTOMERS.jpg)  
  
</details>  


<details>
  
<summary>📊 Sales  </summary>
  
![Sales Image](sales.png)
</details>



<details>
  
<summary>📊 Products</summary>
  
<img width="1209" height="323" alt="image" src="https://github.com/user-attachments/assets/70afaff2-e1b7-473e-8ae1-11d24bf98181" />
</details>

## 🔍 Müük (A)
On olemas NULL väärtused (nt customer_id)  
- 
<details>
  
<summary> Esineb loogikavigu (nt kanal vs makse)</summary>
  
<img width="1132" height="56" alt="image" src="https://github.com/user-attachments/assets/d0a9a698-c444-4554-b30d-37c0516998b6" />
</details>

- Leidub nii väga suuri kui väga väikseid tehinguid  
- Puuduvad kliendiandmed: **1487 rida**

  **Järeldus**  
Sales tabel sisaldab piisavalt andmeid analüüsiks,  
kuid vajab **andmete puhastamist ja valideerimist*  



## 🔍 Kliendiandmed (B)

⚠️ **Andmete kvaliteet**
- Linnanimed ebajärjekindlad (väike/suur algustäht)
- Puuduvad e-mailid osadel klientidel  !!!! **Targeting AD VIP klienditdele PUUDULIK**

⚠️ **Duplikaadid**
- Kokku e-maile: **3150**
- Unikaalseid: **2640**
- ❗ Duplikaate: **510**


## 🌍 Müügikanalid ja asukohad (D)

- 🛒 Müügikanalid: **online**, **pood**
- 📍 Linnad: **Tallinn, Tartu, Pärnu**
- ❗ NULL väärtus = e-poe tellimus

💳 **Makseviisid:**
- järelmaks  
- kaart  
- sularaha  

⚠️ **Leitud probleem**
- 5204 tehingut ilma asukohata  
- ❗ E-poes on kasutatud *sularaha* → loogikaviga  

---


# Kokkuvõte
## 🚨 Suurimad üllatused
- 🔴 **Müük**
- Ostud ei saa olla NEGATIIVSES summas kui tegemist ei ole tagastusega.
- 🔴 **Kliendiandmed**
  - Duplikaadid e-mailides → vajab puhastamist  

- ✅ **Müügikanalid ja asukohad**
  - Puuduvad NULL väärtused (hea kvaliteet)  
  - Channel vs payment mismatch  
  - e-poe maksed ≠ sularaha  
---

## 💡 Soovitused

- Standardiseerida linnanimed (LOWER / UPPER)  Kasutadaes INITCAP (capitalizes)  ja TRIM (Tühikute eemaldamiseks) funktsioone.
- Eemaldada e-mail duplikaadid
- Lisa validatsioon:
  - `online → ainult kaart/järelmaks`
- Kontrollida NULL asukohad 
- Kontrollida üle negatiivsed maksed


## 🔗 SQL & Audit Logid 
  
  

* Roll A Müügiandmed  

  👉[Müük](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/Roll%20A%20m%C3%BC%C3%BCk.md)  
  
* Roll B Kliendiandmed (customers)  
  
  👉 [Kliendiandmed](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/Kliendiandmed%20SQL%20päringud.md)  

* Roll C  Tooteandmed (products)  

* ROll D  Müügikanalid (sales: kanalid, asukohad  
  
  👉[Müügikanalid ja asukohad](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/myygikanalid%20ja%20asukohad.md)  

 * Lisa  
   👉 [SQL Week 01 – Andmete import](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/SQL%20WEEK%2001%20CODE%20andmete%20import)
   
   👉 [Uuemad Kliendid viimased 6 kuud ](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/uuemad_kliendid)
   

## 📚 Kasutatud materjalid

- N1_0_1_P_IT_SQL_pohi_v2.9  
- N1_2_1_P_GT_SQL_pohi_v2.9




















