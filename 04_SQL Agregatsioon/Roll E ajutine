✅ VALIDEERIMISRAPORT

Roll: Valideerija & Kvaliteedikontroll + Ärisünteesi koondaja

Analüüsitud rollid:

A: Müügi koondandmed
B: Kliendisegmendid ja väärtuslikud kliendid
C: Inventuuristatistika
D: Turunduskanalite analüüs
1. ROLL A – Müügi koondandmed
Kontrollitud
Kuupõhine müügianalüüs olemas
GROUP BY, HAVING, JOIN, CTE ja LAG() kasutatud
Numbrilised tulemused on loogilised
Käibe trend liigub kasvavas suunas
Tulemus

✅ OK

Kõrgeim kuu: detsember 2024 (170 623 €)
Madalaim kuu: jaanuar 2024 (85 619 €)
Käive kasvab aasta jooksul järjepidevalt.
Märkus

⚠ Kategooriate müügitulemustes kasutatakse SUM(total_price) kategooria kaupa. Kui müügitabelis on üks tellimus seotud ühe tootega, on loogika korrektne. Kui tellimuses võib olla mitu toodet, tuleks kontrollida võimalikku topeltarvestust.

2. ROLL B – Kliendisegmendid
Kontrollitud
CTE kasutatud õigesti
Segmentide loogika arusaadav
Klientide arvud on realistlikud
Segmentide koguarv klapib
Tulemus

✅ OK

Segmendid:

VIP: 19 klienti
Regular: 917 klienti
Uus: 1615 klienti

Kokku:

19 + 917 + 1615 = 2551 klienti ✔️
Äriline tähelepanek

✅ VIP-kliente on alla 1% kliendibaasist, kuid nende keskmine käive on 18 227 €.

3. ROLL C – Inventuuristatistika
Kontrollitud
GROUP BY töötab korrektselt
HAVING kasutatud õigesti
ROW_NUMBER() kasutatud õigesti
TOP 3 toodete leidmise loogika korrektne
Tulemus

✅ OK

Peamised tulemused:

Kõige tugevam müügikategooria: Meesteriided (4121 ühikut)
Kõrgeima väärtusega kategooria: Jalanõud (keskmine hind 214,10 €)
Nõrgim kategooria: Aksessuaarid (3231 ühikut)
Märkus

⚠ Müügimahud ja käibenumbrid võiks järgmises versioonis siduda Roll A kategooriakäibetega, et näha lisaks kogusele ka tegelikku kasumipotentsiaali.

4. ROLL D – Turunduskanalite analüüs
Kontrollitud
GROUP BY kasutatud
CTE kasutatud
DATE_TRUNC kasutatud
LAG() kasutatud
Kanalite võrdlus arusaadav
Tulemus

✅ OK

Peamised tulemused:

Google Organic suurim käive: 863 240 €
Direct liiklus teine: 599 438 €
Facebook Ads: 504 811 €
Kõrgeim käive kliendi kohta: E-mail (4542 € kliendi kohta)
PARANDA

⚠ Autor märgib ise olulise kvaliteediriski:

Turunduskanalite nimed ei ole standardiseeritud:

Google
google
Google Organic
google_organic

See võib moonutada kanalite tulemusi. Enne juhtimisotsuseid tuleb kanalid normaliseerida.

PARANDA

⚠ Võimalik topeltarvestus tabelis web_logs, kui ühel kliendil on mitu kirjet. Autor on selle riski õigesti välja toonud.

RISTKONTROLL ROLLIDE VAHEL
Kontroll	TulemusMüügi üldine kasv (A) toetub tugevatele kanalitele (D)	✅
Kõrge väärtusega kliendid (B) sobituvad tugeva käibekasvuga (A)	✅
Kõrge hinnaga jalanõud (C) toetavad suuremat tellimuse väärtust (A)	✅
Turunduskanalid toovad piisavalt kliente võrreldes kliendibaasi suurusega (B vs D)	✅
Leitud kriitilised andmekvaliteedi riskid dokumenteeritud	✅
