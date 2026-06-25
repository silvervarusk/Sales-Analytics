# WEEK 1 Müügiosakond
| 👟 Jalanõud | 👶 Laste riided | 🎒 Aksessuaarid | 👗 Naiste riided | 👔 Meeste riided |
|------------|----------------|----------------|-----------------|-----------------| 

### Andme struktuurid:


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





# Olulised tähelepanekud kliendiandmetel
* Anmdestikku tuleb puhastada: Erinevates formaatides: -City Linna nimeded algavad väikese või suure tähega  
* Mõned andmestikud on puudulikud: Kõikidel klientidel pole e-mail aadressi registeeritud.  
* KAHLTUS andmetes esinevad duplikaat entrid  näide e-mail aadresid
  
  Kokku e-maile: 3150  
  Kokku e-maile unikaalseid: 2640  
   **Vahe** 510

 # Kokkuvõte Müügikanalid ja asukohad
 Müügikanaleid on 2 : online ja pood Poed asuvad kolmes linnas : Tallinn, Tartu, Pärnu. Poe asukoht ei ole alati määratud (NULL e. siis on tegemist e-poe ostuga) Makseviise on kasutusel 3 erinevad: järelmaks, kaart, sularaha Ilma asukohata tehinguid oli 5204 Leidsin vastuolu - e-poe ostul on makseviisiks märgitud sularaha

# AUDIT LOG-ID.  
  
👉 [SQL Week 01 – Andmete import](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/SQL%20WEEK%2001%20CODE%20andmete%20import)

👉 [Kliendiandmed SQL päringud](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/Kliendiandmed%20SQL%20päringud.md)

👉 [Uuemad Kliendid viimased 6 kuud ](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/uuemad_kliendid)  
  
👉[Müügikanalid ja asukohad](https://github.com/silvervarusk/Sales-Analytics/blob/main/01_Sales_Analysis/myygikanalid%20ja%20asukohad.md)  


# Suurim üllatus:  
* Customers Andmed on vigased, esinevad duplikaate e-posti aadressidel. Vajavad töötlemist!  
* Sales:Müügikanalid ja asukohad - Payment method ja channel nimed ei klappi. Veebipoe maksed ei saa ola sularahas.   
* Products (üheskis lahtris polnud null väärtusi) 
# Soovitus Toomasele  
  
# Puuduvad andmestikud  
## Kasutatud juhendid:

N1_0_1_P_IT_SQL_pohi_v2.9  
N1_2_1_P_GT_SQL_pohi_v2.9  



