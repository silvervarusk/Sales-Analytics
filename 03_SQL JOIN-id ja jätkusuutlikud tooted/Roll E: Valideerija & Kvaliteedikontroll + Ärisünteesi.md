✅ Valideerimisraport (Roll E)
1. Roll A – Müük + Kliendid
Kontrollitud
INNER JOIN päringud töötavad korrektselt.
TOP 10 klientide tulemused on loogilised.
Linnade müügitulemused on kooskõlas klientide ja ostude arvuga.
Loyalty Tier analüüs sisaldab kõiki tasemeid.
Tulemus

✅ Klientide, ostude ja müügiandmete vahelised seosed on korrektsed.
 ✅ Linnade müügitulemused on realistlikud.
 ✅ TOP kliendid ja üle keskmise kulutajad on üheselt tuvastatud.
 ✅ Ärilised soovitused põhinevad tulemustel.

Tähelepanek

⚠️ Loyalty Tier tulemustes on suurim käive märgitud väärtuse NULL alla (1 071 805 €). See viitab sellele, et osal klientidest puudub lojaalsustase ning andmekvaliteeti võiks parandada.

2. Roll B – Kliendid ilma ostudeta
Kontrollitud
LEFT JOIN kasutus on korrektne.
WHERE sale_id IS NULL loogika töötab õigesti.
Kadunud klientide arv on tuvastatud.
Aktiivsete ja mitteaktiivsete klientide võrdlus tehtud.
Tulemus

✅ Leiti 599 klienti, kes pole kunagi ostu teinud.
 ✅ Kadunud klientide jaotus linnade kaupa on analüüsitud.
 ✅ Registreerimisperioodide analüüs on tehtud.
 ✅ Esitatud on konkreetne turundussoovitus klientide aktiveerimiseks.

Ristkontroll

✅ Aktiivseid kliente 2551 + kadunud kliente 599 = kokku 3150 klienti. Numbrid on omavahel kooskõlas.

3. Roll C – Tooted ja inventuur
Kontrollitud
Müümata toodete leidmiseks kasutati korrektset LEFT JOIN lahendust.
Inventuuriandmed ühendati toodetega.
Kontrolliti laoseisu ning müümata toodete olemasolu.
Tulemus

✅ Leiti 12 toodet, mida pole kunagi müüdud.
 ✅ Ühelgi müümata tootel puudus positiivne laoseis.
 ✅ Raha ei ole kinni täielikult müümata toodetes.
 ✅ Enim müüdud toodete analüüs on tehtud.

Tähelepanek

⚠️ Inventuuris esines negatiivseid laoseise, mis viitab võimalikule andme- või protsessiveale ning vajab täiendavat kontrolli.

4. Roll D – Müügikanalid
Kontrollitud
3 tabeli JOIN (sales, customers, products) töötab korrektselt.
Võrreldud on klientide arvu, käivet ja kanali efektiivsust.
Arvutatud on müük kliendi kohta.
Analüüsitud on linnade ja kanalite erinevusi.
Tulemus

✅ Pood on suurima käibega kanal (1 902 430 €).
 ✅ Online-kanal teenib üle 1 miljoni euro käivet.
 ✅ Poe klient on keskmiselt väärtuslikum kui online klient.
 ✅ Tallinna piirkond on ettevõtte tugevaim müügikeskus.

Tähelepanek

✅ Kanalite võrdlus, kliendiarvud ja käibenumbrid on omavahel kooskõlas ning ärilised soovitused on põhjendatud.

🔄 Ristkontroll (A–D)
Kontroll	TulemusMüügitulemused linnade kaupa ühtivad Roll D järeldustega	✅
Tallinn on suurima käibega piirkond nii Roll A kui Roll D järgi	✅
Aktiivsete klientide arv Roll B analüüsis toetab Roll A klientide müügianalüüsi	✅
Müümata toodete analüüs Roll C ei näita vastuolu müügiandmetega	✅
Kanalite müüginumbrid on loogilises vahemikus	✅
Andmete põhjal tehtud soovitused on põhjendatud	✅
🎯 Ühtne ärikokkuvõte Toomasele ja Annale

Analüüs näitas, et UrbanStyle suurimad tuluallikad on Tallinna piirkond, füüsilised poed ning aktiivsed lojaalsed kliendid. Samal ajal tuvastati 599 klienti, kes on registreerunud, kuid pole kunagi ostu sooritanud, mis kujutab endast olulist kasvuvõimalust. Toodete analüüsist selgus, et müümata toodetes ei ole hetkel kinni märkimisväärset kapitali, kuid inventuuriandmetes esineb negatiivseid laoseise, mis vajavad korrastamist. Kõige suurem üllatus oli see, et Silver-taseme kliendid genereerivad rohkem kogukäivet kui Gold-taseme kliendid ning Tallinn üksi annab üle miljoni euro müügitulu. Soovitame suunata turundusressursid Tallinna piirkonda, online-kanali arendamisse ning 599 mitteaktiivse kliendi taasaktiveerimisse personaalse kampaania abil.

✅ Kvaliteedikontroll
 Kõigi rollide (A–D) väljundid on üle vaadatud
 Ristkontroll tehtud — numbrid klapivad omavahel
 Valideerimisraport kirjas
 Ühtne ärisoovitus stakeholderitele koostatud
 Soovitused põhinevad tegelikel analüüsitulemustel, mitte oletustel
