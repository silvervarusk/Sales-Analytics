# Valideerimisraport ja ärisüntees

## Eesmärk

Roll E ülesanne oli kontrollida meeskonna analüüside kvaliteeti, valideerida tulemuste korrektsus ning koondada kõikidest analüüsidest üks terviklik äriline ülevaade UrbanStyle juhtkonnale.

---

## Valideerimise tulemused

### Roll A – Müük ja kliendid

- Kontrollitud on kliendi- ja müügiandmete ühendamine INNER JOIN abil.
- TOP klientide analüüs on loogiline ja tulemused vastavad müügiandmetele.
- Linnade müügitulemused on korrektsed ning toetavad ärilisi järeldusi.
- Lojaalsustasemete analüüsis selgus, et osa klientidest on ilma lojaalsustasemeta, mis viitab võimalikule andmekvaliteedi probleemile.

### Roll B – Kliendid ilma ostudeta

- LEFT JOIN lahendus on korrektselt realiseeritud.
- Tuvastati 599 klienti, kes pole kunagi ostu sooritanud.
- Aktiivsete ja mitteaktiivsete klientide arvud on omavahel kooskõlas.
- Esitatud soovitused põhinevad analüüsitulemustel.

### Roll C – Tooted ja inventuur

- Leiti 12 toodet, mida pole kunagi müüdud.
- Müümata toodete tõttu ei ole laos märkimisväärset kapitali kinni.
- Inventuuriandmetes esines negatiivseid laoseise, mis vajavad täiendavat kontrolli.

### Roll D – Müügikanalid

- Kanalite võrdlus ning 3 tabeli JOIN analüüs on korrektselt teostatud.
- Füüsiline pood on suurima käibega müügikanal.
- Online-kanal näitab tugevat potentsiaali ning saavutab kõrge keskmise ostusumma.

---

## Ristkontroll

Valideerimise käigus võrreldi erinevate rollide tulemusi omavahel.

✅ Müügitulemused linnade lõikes kattuvad nii kliendi- kui müügikanalite analüüsides.

✅ Aktiivsete klientide arv on kooskõlas kliendi- ja ostuanalüüside tulemustega.

✅ Müümata toodete analüüs ei ole vastuolus müügiandmetega.

✅ Müügikanalite käibe- ja kliendinumbrid jäävad loogilistesse vahemikesse.

✅ Kõik peamised järeldused põhinevad andmetel ning toetavad üksteist.

---

## Ärikokkuvõte juhtkonnale

Analüüs näitas, et UrbanStyle suurimad tugevused on Tallinna piirkond, füüsilised kauplused ning aktiivsed lojaalsed kliendid. Samal ajal leiti 599 registreeritud klienti, kes pole veel ühtegi ostu teinud ning kujutavad endast märkimisväärset kasvuvõimalust. Müümata toodete arv on väike ning nende tõttu ei ole ettevõttel laos märkimisväärset kapitali kinni, kuid inventuuriandmete kvaliteet vajab parandamist. Kõige suurema üllatusena selgus, et Silver-taseme kliendid genereerivad rohkem kogukäivet kui Gold-taseme kliendid ning Tallinna piirkond ületab müügitulemuste poolest oluliselt teisi linnu.

---

## Soovitused

1. Suurendada fookust Tallinna piirkonna klientidele ja kampaaniatele.
2. Investeerida online-müügikanali arendamisse ja turundamisse.
3. Käivitada sihitud kampaania 599 mitteaktiivse kliendi aktiveerimiseks.
4. Arendada lojaalsusprogrammi ning keskenduda kõrge väärtusega klientide hoidmisele.
5. Parandada inventuuriandmete kvaliteeti ja uurida negatiivsete laoseisude põhjuseid.
