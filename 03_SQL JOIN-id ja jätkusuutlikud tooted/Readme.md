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


## 📊Tulemused
 

### 👥 Kliendid ja ostukäitumine
- Analüüsiti 3150 klienti, kellest 2551 (81%) olid aktiivsed ning 599 (19%) polnud kunagi ostu sooritanud.
- Leiti TOP 10 klienti kogumüügi põhjal ning tuvastati, et TOP 30% klientidest genereeris ligikaudu 65% kogu ettevõtte müügitulust.
- Tallinn oli suurima käibega linn, ületades 1 miljoni euro müügitulu.
- Silver-taseme kliendid genereerisid suurema kogukäibe kui Gold-taseme kliendid.

### 🎯 Mitteaktiivsed kliendid
- Tuvastati 599 klienti, kes polnud kunagi ostu teinud.
- Suurim osa mitteaktiivsetest klientidest paiknes Tallinnas ja Tartus.
- Analüüs näitas võimalust suurendada müüki sihitud taasaktiveerimiskampaaniate abil.

### 📦 Tooted ja inventuur
- Leiti 12 toodet, mida polnud kunagi müüdud.
- Müümata toodetel puudus inventuuri kirje või positiivne laoseis.
- Inventuuriandmetes tuvastati negatiivseid laoseise, mis viitavad andmekvaliteedi probleemidele ja vajavad täiendavat kontrolli.
- Jalanõud olid suurima käibega tootekategooria, aksessuaarid kõige nõrgema müügitulemusega kategooria.

### 🏪 Müügikanalid
- Füüsilised kauplused genereerisid ligikaudu 65% kogumüügist (€1,90M).
- Online-kanal moodustas umbes 35% kogumüügist (€1,01M).
- Poe kliendid kulutasid keskmiselt rohkem kui online-kanali kliendid.



## 🚀 Soovitused

- Keskenduda Tallinna piirkonna ja online-kanali edasisele arendamisele.
- Käivitada sihitud kampaaniad mitteaktiivsete klientide aktiveerimiseks.
- Tugevdada lojaalsusprogrammi ning keskenduda väärtuslike klientide hoidmisele.
- Parandada inventuuriandmete kvaliteeti ja lahendada negatiivsete laoseisude probleemid.
- Optimeerida nõrgemalt toimivate tootekategooriate sortimenti ja turundust.
