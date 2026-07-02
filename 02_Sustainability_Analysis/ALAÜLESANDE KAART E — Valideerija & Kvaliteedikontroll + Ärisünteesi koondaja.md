# Valideerimis & Kvaliteedikontroll
##### Koostas: Silver Varusk

## Valideerimisraport
Praeguses raporti eesmärk on, kontrollida müügi-, kliendi- ja tooteandmete puhastamise tulemuste kvaliteeti ning hinnata, kas andmed on analüüsiks piisavalt usaldusväärsed.
Analüüsi käigus selgus, et suurimaks kvaliteediriskiks on duplikaatsed kirjed müügi-, kliendi- ja tooteandmetes, mis võivad mõjutada aruandlust ja KPI-sid. Täiendava kontrolli käigus ilmnesid ka müügisummade arvutusvead ning lojaalsusprogrammi loogikavead, mis vajavad enne lõppanalüüsi parandamist

## Kvaliteedikontrolli tulemused  

| Kontroll | Tulemus | Järgmine tegevus |
|-----------|----------|------------------|
| Testtabelid loodud (Sales, Customers, Products) | ✅ OK | Dokumenteerida muudatused ja üleviimine live versiooni. |
| NULL väärtuste kontroll |⚠️ Sales tabel vajab parandust NULL customer_id = E-Poe ost | Säilitada regulaarne kontroll, et uued puuduvad väärtused tuvastataks automaatselt.
| Duplikaatide kontroll | ⚠️ Duplikaadid Sales, Customers, Products andmetes | Eemaldada duplikaadid ning rakendada automaatne kontroll andmete sisestamisel. |
| Kuupäevade kontroll | ✅ OK | Jätkata tuleviku kuupäevade valideerimist andmete laadimise protsessis. |
| Hinnaloogika kontroll | 🔴 Vajab parandust | Uurida kirjeid, kus `quantity × unit_price ≠ total_price`, ning määratleda negatiivsete summade ärireeglid. |
| Loyalty Tier kontroll | 🔴 Vajab parandust | Täpsustada lojaalsusprogrammi loogika ning siduda kliendistaatus tegeliku ostuajalooga. |
|Kategooriate kontroll | ✅ OK | Ebapärasusi ei tuvastatud products_test-is|


## Ühised tähelepanekud
### Duplikaadid on peamine kvaliteediprobleem

✅ Müük
- 5 116 duplikaatset rida
- 4 013 duplikaatset invoice_id väärtust

✅ Kliendid
- 129 duplikaatset e-maili

✅ Tooted
- 12 duplikaatset tootenime

### Mõju ärile

Duplikaadid võivad põhjustada:

- ebatäpseid müügiaruandeid
- klientide topeltarvestust
- vale marginaali- ja kasumlikkusanalüüsi
- eksitavaid KPI-sid

---

# Kriitilised tähelepanekud

## 1. Müügisumma kontroll ei klapi

Leiti ligikaudu 200 kirjet, kus:

```text
quantity × product_price ≠ total_price
```
<img width="455" height="403" alt="image" src="https://github.com/user-attachments/assets/a1e2a074-50ef-4ea0-9e22-5811314b152e" />

## Loyalty Tier loogika ei ole äriliselt korrektne
Analüüs näitas juhtumeid, kus klient on märgitud Gold või Silver taseme kliendiks, kuigi tal puudub ostuajalugu.
Näide
<img width="1602" height="401" alt="image" src="https://github.com/user-attachments/assets/5ff4e2f5-14d8-46c3-bf6b-8ed006901d56" />
