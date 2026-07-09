# 📊 Nädal 3 – SQL JOIN Analüüs

## 🎯 Eesmärk

Kasutasime SQL JOIN-lauseid UrbanStyle andmebaasi tabelite ühendamiseks, et analüüsida klientide ostukäitumist, toodete müügitulemusi, inventuuri seisu ning müügikanalite efektiivsust.
## 💡 Äriline fookus
Analüüside eesmärk oli toetada UrbanStyle juhtkonda andmepõhiste otsuste tegemisel kliendisuhete arendamise, müügitulemuste parandamise, inventuuri optimeerimise ning efektiivsemate müügikanalite tuvastamise kaudu.  

## 🛠 Käsitletud SQL teemad

- INNER JOIN
- LEFT JOIN
- Multi-table JOIN
- GROUP BY
- ORDER BY
- COUNT(), SUM(), AVG()
- CASE WHEN
- Subqueries

## 📌 Ülesanded

### 👤 Roll A – Kliendianalüüs
- TOP kliendid kogumüügi järgi
- Klientide ostukäitumise analüüs
- Müügitulemused linnade lõikes
- Lojaalsustasemete mõju müügitulemustele

### 👤 Roll B – Klientide aktiveerimine
- Kliendid, kes pole kunagi ostu sooritanud
- Aktiivsete ja mitteaktiivsete klientide võrdlus
- Klientide jaotus linnade ning registreerimisperioodide kaupa
- Soovitused klientide taasaktiveerimiseks

### 👤 Roll C – Tooted ja inventuur
- Müüdud ja müümata toodete analüüs
- Enim müüdud toodete tuvastamine
- Tootekategooriate võrdlus
- Inventuuri ja laoseisu analüüs
- Juurde tellimise vajaduse hindamine

### 📈 Müük, müügikanalid ja ärisüntees
- Müügikanalite võrdlus ja efektiivsuse analüüs
- Tootekategooriate müük kanalite kaupa
- Tulemuste valideerimine ja ristkontroll
- Andmepõhiste soovituste koostamine UrbanStyle juhtkonnale
- Presentatsioon

## 📊 Tulemused

### 👥 Kliendid
- Leiti TOP 10 klienti kogumüügi põhjal.
- Tallinn oli suurima käibega linn, ületades 1 miljoni euro müügitulu.
- Silver-taseme kliendid genereerisid suuremat kogukäivet kui Gold-taseme kliendid.

### 🔍 Kliendid ilma ostudeta
- Tuvastati 599 klienti, kes pole kunagi ostu sooritanud.
- Suurim osa mitteaktiivsetest klientidest asus Tallinnas ja Tartus.
- Leiti võimalus aktiveerida need kliendid sihitud kampaaniate abil.

### 📦 Tooted ja inventuur
- Leiti 12 toodet, mida pole kunagi müüdud.
- Müümata toodete hulgas puudus positiivne laoseis.
- Inventuuriandmetes esines negatiivseid laoseise, mis vajavad täiendavat kontrolli.

### 🏪 Müügikanalid
- Füüsilised kauplused genereerisid suurima käibe.
- Online-kanal ületas 1 miljoni euro müügitulu.
- Poe kliendid kulutasid keskmiselt rohkem kui online-kanali kliendid.


### 🚀 Soovitused

- Keskenduda Tallinna piirkonna ja online-kanali arendamisele.
- Käivitada kampaaniad mitteaktiivsete klientide aktiveerimiseks.
- Tugevdada lojaalsusprogrammi ja VIP-klientide hoidmist.
- Parandada inventuuriandmete kvaliteeti.
