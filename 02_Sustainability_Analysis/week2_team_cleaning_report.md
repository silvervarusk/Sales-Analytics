# Roll C Tooteandmete puhastamine
## 📌 Kiire ülevaade

✔ Test koopia loomine (products_test)  

#### Andmekvalideedi kontroll:
Duplikaatsed tootenimed (12 rida)  tuvastatud 
Null read puuduvad - Vähendab puhastamise vajadust  
✔Hinnainfo üldine kvaliteet on korralik → analüüsile suur mõju ei tekita.  

#### Tehtud tegevus:  
✔Ebajärjekindlad kategooriad puhastatud  - eemdaldatud potetsiaalne mõju Kategooriapõhiseid raportitele (Filteerimine, grupeerimine)



## Soovitus juhtkonnale

Kõige suurema mõjuga probleem:

👉 Duplikaatsed tootenimed

Riskid:
- Müügitulu võib olla üle hinnatud (double counting)
- TOP toodete analüüs on ebausaldusväärne
- Kasumlikkuse raportid moonutatud

Soovitus:  
✅ Rakendada unikaalsuse piirang (UNIQUE constraint) tootenimele või ID-le  
✅ Lisada andmesisestuse valideerimine  
✅ Kontrollprotsess enne BI raportite loomist
