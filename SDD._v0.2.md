Solution Design Document (SDD korábban MVT)
ID2619_6-DBOS-EDMNET-756-[NET#029].4.SDD-kapcsolattartási_email_cím_megtekintése_módosítása

| Mező  | Leírás                 |
|-------|------------------------|
|SDD elfogadásának és lezárásának dátuma: |	YYYY.MM.DD. |



A dokumentum célja az Üzleti követelmény specifikáció (BRS) - és ha rendelkezésre áll akkor az architekturális leírás (SAD) - alapján, a megoldás magas szintű kidolgozása. A különböző technológiai területek igényeinek és szempontjainak egységbe foglalása. 
Ha az SDD elfogadása és lezárásra megtörtént, de a fejlesztés 3 hónapon belül nem került megvalósításra, akkor az SDD kötelezően felülvizsgálandó.


| Specifikáció készítője |
|-------|------------------------|
| Név: |	Balogh István |
| Szervezeti egység: |	IT Megoldástervezés és Teszttámogatás |
| Beosztás: |	Solution Architect |
| Telefonszám: |	+36 20 746 3731 |
| E-mail cím:	| balogh.istvan2@mbhbank.hu |


 
Tartalom	
1	Változáskövetés	4
2	Hivatkozások	4
3	Fogalomtár	5
4	Üzleti igény	5
4.1	Bevezetés - Üzleti igény röviden	6
4.2	Scope elemek	6
4.3	Out of Scope elemek	6
5	Eltérések az üzleti igényhez képest	6
6	Érintett rendszerek	6
6.1	Internetbank Frontend (Csatorna)	7
6.1.1	Fejlesztési / Paraméterezési igény	7
6.1.2	Folyamatok	8
6.1.3	Jogosultság	9
6.1.4	Riport igény	9
6.1.5	Ősfeltöltés/Adattisztítás	9
6.2	Backend / Middleware / Omnichannel szolgáltatások	9
6.2.1	Fejlesztési / Paraméterezési igény	9
6.2.2	Folyamatok	10
6.2.3	Jogosultság	10
6.2.4	Riport igény	10
6.2.5	Ősfeltöltés/Adattisztítás	10
6.3	Ügyfél törzsadat (Customer Master)	10
6.3.1	Fejlesztési / Paraméterezési igény	10
6.4	Email Service	11
6.4.1	Fejlesztési igény	11
6.4.2	Paraméterezési igény	11
6.5	Authentication / Signing service	11
6.5.1	Fejlesztési igény	11
6.6	Audit / Logging / Analytics	11
6.6.1	Fejlesztési igény	11
6.7	Email megerősítés – hibakezelés	11
6.8	Kill / Hide switch	12
7	Bank által elvégzendő feladatok	12
8	Mellékletek	12
9	Egyéb megjegyzések (hiányosságok)	12
10	Véleményezés	13

 
1	Változáskövetés
Növekvő sorszám, ami 0.1-el indul. Változás esetén a tizedesjegyet növeld az előző verziószámhoz képest (pl. 0.9 után 0.10), és a Módosítás rövid leírása mezőbe röviden vázold, hogy mi és/vagy miért változott az anyagban.
Amíg csak az SA dolgozik rajta, addig 0.valami a verziószám, első körös véleményezésre küldésre az 1.0 verzió kerül. Ezután már mindenképpen legyen vagy a változáskövetés bekapcsolva a dokumentumon, vagy színezve a változás. Ez utóbbi esetben a törlendő rész csak áthúzott betűtípussal jelenjen meg.
A vélemények átvezetése növeli a tizedesjegyet (v1.1, v1.2, stb.) Az összes vélemény átvezetése után v.2.0 verzió kerül kiküldésre, mint következő véleményezendő vagy végleges jóváhagyandó verzió.
Minden kiküldött verzió, csak az előző kiküldött verzióhoz képest való eltéréseket tartalmazza.
A változást a címben is le kell követni.
Verziószám	Módosítva 
(dátum)	Változásban érintett rendszerek	Módosítás rövid leírása
v.0.1	2026.06.10.	Internetbank, Backend, Email service	Első (draft) verzió -
v.0.2	2026.06.10.	Internetbank, Backend, Email service	Első (draft) verzió - javítások
v.1.0	YYYY.MM.DD.		Első verzió -

SDD visszanyitása:
-	Ha a SAD módosításra kerül, akkor az SDD visszanyitható
-	IDD visszajelzés alapján:
o	Visszanyitandó: új rendszert kell felvenni az érintett rendszerek közé, mert annak kezelnie / tárolnia / feldolgoznia kell új adatot, és ezt a rendszert az SDD véleményezett és lezárt verziója nem tartalmazza. 
o	Nem visszanyitandó: Ha a rendszer érintettség úgy merül fel, hogy kezelnie / tárolnia / feldolgozni nem kell az új adatot. (pl. a rendszer igénybe veszi azt a szolgáltatást, ami adatbővítéssel érintett, de ez nem okoz fejlesztést a rendszerben, mert az új adatot figyelmen kívül hagyja, működésében nem okoz fennakadást)
-	Ha SRS készítése közben derül ki, hogy az SDD-ben leírtaktól eltérő megvalósítás lesz, de ez nem okoz SAD módosítást, akkor az eltérés dokumentálásának az SRS-ben kell megtörténnie, emiatt az SDD visszanyitásra nem kerül. Az SRS-t véleményezésre vissza kell küldeni az SA-nak is, aki ezt a ’Project’ mappa alá a megfelelő helyre csatolja.
2	Hivatkozások
Mindig legyen beírva a BRS (vagy az Magas szintű üzleti specifikáció, ami a QBR-on elfogadásra került) és ha van akkor a SAD is.
Amennyiben CR vagy Hibajegy alapján új SDD készül egy anyaghoz abban hivatkozni kell az eredeti SDD-t, és az új SDD címét vissza kell vezetni az eredeti anyag Hivatkozások táblázatba. Emiatt az eredeti SDD nem vált verziót.

A következő dokumentumok kerültek meghivatkozásra ebben az anyagban:
Dokumentum neve	Leírás
Kapcsolattartás e-mail cím megtekintése, módosítása - DBOS és MBH Netbank implementáció - Confluence
BRQ/Confluence üzleti specifikáció
dokumentum - Kapcsolattartás e-mail cím megtekintése, módosítása (BRS (Business Requirement Specification) helyettesítő)
https://www.figma.com/design/OlIkuaosm6gRBh9Ryc8ySj/%F0%9F%9F%A4-Kapcsolattart%C3%A1s-e-mail-c%C3%ADm-megtekint%C3%A9se--m%C3%B3dos%C3%ADt%C3%A1sa?node-id=0-1&p=f&t=79J1fU58XkDdAkR9-0	Figma link – UI/UX terv (Sajnos, a link nem működik!)
MBH_Üzleti_követelmény_Spacifikáció_PROJECTNEVE.docx	BRS (Business Requirement Specification)
SAD_PROJECTNEVE.docx	SAD (Solution Architektúra Dokumentum)
Eredeti MVT/SDD	Eredeti MVT/SDD nincs
	

3	Fogalomtár
OPCIONÁLIS: Ebben a pontban azokat a fogalmakat és rendszereket kell feltüntetni, amelyek segítik a megértést, hogy a dokumentumot olvasó is értse a rövidítéseket, kifejezéseket.
Ha van SAD, akkor a rendszer neveket és rövidítéseket az alapján használjuk.
Kifejezés/Rövidítés	Magyarázat
Email confirmation/ validation link	JWT alapú megerősítő/érvényesítési (Validációs) link
Internetbank	Felhasználói frontend
JWT token	Email validációhoz használt token
Hide switch	A Hide switch esetében a menüpont elérhető (ellentétben a kill switch beállítással) viszont aktív műveletet nem végezhet a felhasználó.
Kill switch, Hide switch - DBOS és MBH Netbank implementáció - Confluence

Kill switch	A Kill switch esetében a paraméterek lehetséges állapotai és azok hatása:
-	funkció elérhető
-	funkció nem elérhető. Ilyenkor a menüben a funkció látszik, de inaktív. 
Kill switch, Hide switch - DBOS és MBH Netbank implementáció - Confluence

Signing	OTP / mobilapp aláírás
4	Üzleti igény
Az üzleti igény leírása pár mondatban.
4.1	Bevezetés - Üzleti igény röviden
A felhasználó módosítani tudja az Internetbank regisztráció során megadott kapcsolattartási e-mail címét , amely az ügyfél törzsadat része.

4.2	Scope elemek
BRS-ben szereplő igények közül azok felsorolása, amik az SDD készítése közben Scope-ban maradtak.
•	Email cím megjelenítés 
•	Email cím módosítás 
•	Validáció (formai és üzleti) 
•	Email megerősítés (linkes) 
•	Tranzakció aláírás 
•	Visszaigazolás 
•	Audit log, Analitika 
•	Kill/Hide switch 
•	Admin paraméterezés

4.3	Out of Scope elemek
BRS-ben szereplő igények közül azok felsorolása, amik az SDD készítése közben Out of Scope-ba kerültek.
•	Egyéb ügyfél kapcsolattartási adatok módosítása 
•	Több e-mail kezelése

5	Eltérések az üzleti igényhez képest
Ha a BRS már le van zárva, akkor az üzleti igénytől eltérő tervezett megvalósítást ebben a táblázatban kell feltüntetni, a BRS nem kerül se visszanyitásra se módosításra. Amennyiben az Üzleti igény fejezetben a BRS-ben szereplő igényhez képest scope változás történt, azt ennek a fejezetnek a táblázatában is fel kell tüntetni. Üzleti igény Scope és Out of Scope fejezete legyen összhangban az Eltérések az üzleti igényhez képest fejezet táblázatával.
Ha BRS még nincs lezárva, akkor lehet a BA-t kérni, hogy egyeztessen az üzlettel és módosítson a BRS-en. Amennyiben üzlettől kapott magas szintű BRS alapján dolgozik az SA, akkor neki kell egyeztetnie a változásokat az üzlettel.
BRS azonosító	Eredeti igény	Tervezett megvalósítás	Indoklás
BRS-ben megadott azonosító	Eredeti üzleti igény rövid leírása	Tényleges megvalósítás rövid leírása	Indoklás röviden
N/A	BRS nincs	BRQ, illetve Confluence dokumentum alapján készült SDD	BRS nem készült
			

6	Érintett rendszerek
Egy egyszerűsített ábra készíthető az érintett rendszerek és a közöttük lévő kapcsolatokról (interface), ha az segíti a folyamat megértését. Amennyiben van SAD, akkor arra az 2. pontban hivatkozunk.
Feltételezett rendszerek (High-level)
•	Internetbank Frontend 
•	Channel Backend / Middleware 
•	Customer Master (törzsadat) 
•	Notification / Email service 
•	Authentication / Signing service 
•	Config/Param rendszer 
•	Audit / Logging 
•	Analytics

Ábrák…

1. ábra SDD szintű példa ábra, ha van SAD és abban szerepelnek szolgáltatás ID-k
Amennyiben nem állnak rendelkezésre szoltáltatás ID-k, akkor azokat el kell hagyni a fenti ábráról.

2. ábra SRS szintű példa ábra, SDD-ben NEM használandó
6.1	Internetbank Frontend (Csatorna)
Miért érintett a rendszer? (röviden) Jelenlegi működés leírása, amennyiben az a fejlesztési igény megértéséhez szükséges. Egy rendszerhez tartozhat [Fejlesztési igény és/vagy Paraméterezési igény] vagy ha egyik sincs akkor Tájékoztatás fejezet. 
Flexcube esetén SDD készítésekor a Flexadapter; Link; SIA; FIA stb. nem kezelendő külön. Ettől eltérni akkor kell, ha a SAD ábráján külön megjelenik.
6.1.1	Fejlesztési / Paraméterezési igény
OPCIONÁLIS - BRS-ben megadott azonosító - Fejlesztés specifikálása.
•	Új menüpont: Kapcsolattartási e-mail
•	Képernyők: 
o	Megtekintés
o	Módosítás (2 mező)
o	Megerősítés várakozás
o	Visszaigazolás
•	Validációk: 
o	E-mail formátum hibák
o	egyezés (két e-mail eltérés)
o	új ≠ régi (új = régi tiltása)
•	Input korlátozás:
o	Beillesztés (Paste) tiltás megerősítő mezőnél
o	Üres mező tiltása

6.1.1.1	Adattartalom
OPCIONÁLIS
Mindig azokat az adatokat kell feltüntetni a táblában, amelyekre az adott SDD szerint igény van. Nem kell nyomozni, hogy az esetlegesen meglévő szolgáltatásnak mi az adatszettje. A rendszerszervező feladata lesz eldönteni, hogy az EA által megadott szolgáltatásban, az SDD-ben megadott adattartalom alapján kell-e bármilyen módosítást végezni.
Ha a SAD meghatároz egy interfészt két rendszer között, akkor ezzel azt is meghatározza, hogy a szükséges adatok megtalálhatóak a forrásrendszerben.
Ha az SDD-ben meg van határozva egy szolgáltatás meghívásához az adatkör, de az SRS készítése közben kiderül hogy ez nem elégséges, akkor a rendszerszervező kideríti, hogy a szükséges adat a hívó oldalon rendelkezésre áll-e (hívó oldali rendszerszervező segítségével)
-	Ha rendelkezésre áll, akkor az SRS-ben pontosan meghatározza a híváshoz szükséges adatkört
-	Ha nem áll rendelkezésre, akkor megvizsgálja, hogy másik szolgáltatás igénybevételével be tudja-e szerezni a szükséges adatot
-	Ha egyik sem, akkor ettől a ponttól már témafüggő a további megoldás.
Az adattartalmon kívül minden egyéb integrációs adat, amiket a korábbi Üzenetek/Interfészek fejezet tartalmazott, a továbbiakban nem képezik az SDD részét. Azt az Integrációs Architect / Szakértő fogja feltüntetni az IDD-ben. Minden olyan esetben, ahol integrációs feladat van kell, hogy készüljön SAD és IDD is.
Interface azonosító: SAD-ban feltüntetett ID
Online/Batch: 
Mezőnév	Adattípus	Hossz / Méret	Kötelezőség	Előfordulás*	Értékkészlet	Alapértelmezett érték	Validációs szabály	Kapcsolódás más mezőkhöz	Üzleti jelentés / példaérték
Az adat logikai neve (pl. Születési dátum)	pl. szöveg, szám, dátum	Maximális hossz / méret	Kötelező
1..1	Értékkészlet / Kódlista elemeinek felsorolása pl. PIROS, ZÖLD, KÉK	Ha van pl. státusz = „AKTÍV”	Formai / Üzleti érvényességi szabályok pl. nem lehet jövőbeli dátum	pl csak akkor kötelező, ha más mező értéke = X	Rövid leírás, hogy mire szolgál
									

*Előfordulás mezőben megadható értékek:
-	Kötelező, egyszeri [1..1]
-	Opcionális egyszeri [0..1]
-	Kötelező, többszörös [1..n]
-	Opcionális, többszörös [0..n]
-	Min. X, max. Y előfordulás [X..Y], ahol X és Y behelyettesítendő adat, pl: 1..2 Jelentése, hogy az adott adat minimum egyszer, de maximum kétszer fordul elő pl: kapcsolattartó neve
-	Pontos többszörös előfordulás [X..X] ahol X behelyettesítendő adat, pl: 3..3 Jelentése, hogy az adott adat pontosan háromszor fog előfordulni pl: biztonsági kérdésre adott válasz

6.1.2	Folyamatok
OPCIONÁLIS - End-to-End folyamat adott rendszerre vonatkozó része, amennyiben a fejlesztés megértéséhez szükséges.
1.	Email megjelenítése 
2.	Módosítás indítása 
3.	Új email megadás 
4.	Validáció 
5.	Backend hívás → email küldés 
6.	Várakozás validációra 
7.	Signing indítás 
8.	Eredmény képernyő
6.1.3	Jogosultság
OPCIONÁLIS - Ha az adott rendszerhez kapcsolódóan új jogosultság szükséges vagy a meglévő jogosultság változik.
•	Nem jogosultságfüggő
6.1.4	Riport igény
OPCIONÁLIS
Ha az adott rendszerből kell riportot generálni (pl. Flex, DW stb. esetén). Ha van BRS-ben MEGFELELŐ üzleti riport igény, akkor azt nem kell átmásolni, de hivatkozni kell a BRS megfelelő pontját. Ha az kiegészítésre/módosításra szorul akkor azt az SDD-ben kell teljeskörűen megjeleníteni.
6.1.5	Ősfeltöltés/Adattisztítás
OPCIONÁLIS - Ha az adott rendszerben erre szükség van, akkor az érintett ügyfélkör és az ősfeltöltés/adattisztítás specifikálása

6.2	Backend / Middleware / Omnichannel szolgáltatások
Jelen pont és az alatta lévő alpontok másolása az érintett rendszerek darabszáma alapján.
6.2.1	Fejlesztési / Paraméterezési igény
BRS-ben megadott azonosító
Fejlesztési igény
•	API-k:
o	GET email
o	INIT email change
o	CONFIRM token
o	COMPLETE change (sign után)
•	Token kezelés (JWT)
•	State/Flow kezelés:
o	pending
o	validated (email_confirmed)
o	signed
o	failed
Paraméterezési igény
•	Email link TTL (default 5 perc)
•	Resend delay
•	Kill switch / Hide switch
6.2.1.1	Adattartalom (logikai szint)
Mező	Típus	Kötelező	Validáció
customerId	string	igen	existing
currentEmail	string	igen	email
newEmail	string	igen	email format
confirmEmail	string	igen	egyezés
token	string	igen	JWT
status	string	igen	PENDING / VALIDATED / DONE
timestamp	datetime	igen	

6.2.2	Folyamatok
1.	Email módosítás indítás (mentése pending státuszba)
2.	Token generálás (JWT) 
3.	Email küldés
4.	Token validáció (Confirmation endpoint)
5.	Signing indítás (trigger)
6.	E-mail frissítés véglegesítve 
7.	Notification küldés

6.2.3	Jogosultság

6.2.4	Riport igény
•	Módosítások listája 
•	Sikertelen próbálkozások 
•	Timestamp
6.2.5	Ősfeltöltés/Adattisztítás

6.3	Ügyfél törzsadat (Customer Master)
6.3.1	Fejlesztési / Paraméterezési igény
•	Email update 
•	Historikus tárolás

6.3.1.1	Adattartalom / Adattárolás (új)
•	oldEmail 
•	newEmail 
•	modifiedAt 
•	status 
•	failureReason

6.4	Email Service
6.4.1	Fejlesztési igény
•	Template alapú email 
o	Magyar (HU) + angol (EN) (+ később német (DE)) tartalom 
•	Token link kezelése

6.4.2	Paraméterezési igény
•	Email template adminból
•	link TTL (default 5 perc) 
o	resend delay 

6.5	Authentication / Signing service
6.5.1	Fejlesztési igény
•	Signing flow integráció:
o	SMS OTP
o	Mobil app (biometria/mPIN)

6.6	Audit / Logging / Analytics
6.6.1	Fejlesztési igény
•	Audit log: 
o	régi email
o	új email
o	timestamp
o	státusz
•	Analytics: 
o	menüpont megnyitás
o	módosítás indítás
o	sikeres / sikertelen
6.7	Email megerősítés – hibakezelés
Hiba (Error)	Leírás
invalid token	hibás JWT
expired	lejárt link
reused	már használt
technical error	backend hiba
success	validált

6.8	Kill / Hide switch
Kill
•	Menü látszik
•	Funkció hívás → popup
Hide
•	Funkció teljes eltűnés

7	Bank által elvégzendő feladatok
OPCIONÁLIS
Ebben a pontban azokat a bank vagy üzlet által elvégzendő feladatokat szükséges meghatározni, amelyek elengedhetetlenek a jelen SDD-ben leírt fejlesztések megvalósításához. Ezek a feladatok a fejlesztés szempontjából nélkülözhetetlenek, és hiányuk akadályozná a teljeskörű kivitelezést. 
•	Email template-ek feltöltése 
•	Paraméterek beállítása (admin): 
o	TTL
o	resend delay
•	Analitika riportok definiálása

8	Mellékletek
OPCIONÁLIS
•	Figma link (kijavítva)
•	Email templatek (később)

9	Egyéb megjegyzések (hiányosságok)
•	Nincs BRS → traceability limitált
•	Nincs SAD → interfészek hiányoznak  
•	Email service konkrét rendszer nincs definiálva 
•	Token formátum (JWT vs custom) kérdése 
•	Pending email storage nincs konkretizálva
•	Edge case-k vizsgálata:
o	user nem kattint linkre 
o	link lejár 
o	többszöri resend 
o	signing fail után retry

10	Véleményezés
Érintett rendszerek szervezőit szükséges felsorolni, valamint azokat a területeket/rendszereket, akik csak tájékoztatást kapnak. Utóbbi esetben az ‘Elfogadva (dátum)’ mezőbe elég annyit írni, hogy ‘Tájékoztatás’. Amennyiben jóváhagyáskor plusz információ is érkezik a jóváhagyótól, azt be kell másolni a ‘Megjegyzések’ mezőbe.
A dokumentum az egyeztetéseket követően az alábbi kollegák véleményezésével / tájékoztatásával készült el:
Elfogadva (dátum)	Terület / Rendszer	Illetékes/Szervező	Megjegyzések
Tájékoztatás	Enterprise Architect/	?	Amennyiben készült SAD akkor az SDD-t EA-val kötelező véleményeztetni
Tájékoztatás	Integrációs Architect	Második körben integrációs architekt, akit Erdős Bélától kell kérni	Amennyiben készült SAD akkor az SDD-t Integrációs szakértővel vagy Integrációs Architect-el kötelező véleményeztetni
Tájékoztatás	Integrációs Szakértő	Első körben integrációs szakértő: Pikó Csaba	Amennyiben készült SAD akkor az SDD-t Integrációs szakértővel vagy Integrációs Architect-el kötelező véleményeztetni
Tájékoztatás	Business Analyst	Lengyel Kornél	Amennyiben BA készítette a BRS-t (vagy BRQ/Confluence dokumentáció van)
Tájékoztatás	Adattárház	Gönczi Gergő	Kötelezően tájékoztatandó
Tájékoztatás	Adattárház		Amennyiben fejlesztés is van, akkor kötelező véleményeztetni
	Üzleti megrendelő		
	Rendszer1		
	Rendszer2		
Tájékoztatás	Törzsadat	Fehér Zsuzsa, Hortobágyi Helga	Amennyiben FlexCube ügyfél / számla érintett, akkor Törzsadat tájékoztatandó.
Tájékoztatás	Adattisztítás	Horváth Andrea	Amennyiben FlexCube ügyfél / számla érintett, akkor tájékoztatandó.
Tájékoztatás	Bankbiztonság/IT sec		ajánlott (token + email security)
Tájékoztatás	Bankkártya Operáció	Takács Mónika	Amennyiben a Bankkártya érintett
Tájékoztatás	Adózási osztály	Csiszár Ottó	Amennyiben tran kód jön létre az SDD-benj
Tájékoztatás	Tesztautomatizáció	Priskin István	
Tájékoztatás	Tesztmenedzsment	Püspöki Lajos Szabolcs	
Tájékoztatás	Tesztelés	Polcsik Szilvia	
Tájékoztatás	Lakossági és Vállalati csatornák fejlesztése	Schrenk Richárd	Kötelezően tájékoztatandó


