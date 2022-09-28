---
layout: post
title:  "Cobra, un calculator românesc"
---

This post is in Romanian, but you can have Google Translate translate it into
the language of your choice by selecting it here:
<div id="google_translate_element"></div>
<script type="text/javascript" src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
<script type="text/javascript">
function googleTranslateElementInit() {
  new google.translate.TranslateElement({pageLanguage: 'ro'}, 'google_translate_element');
}
</script>

* TOC
{:toc}

## Fundal

Proiectele mele preferate se nasc din intersecția de pasiune multiple, și
acesta combină pasiune mea de-o viață pentru calculatoare și obsesia mea
ciudată cu România (sunt American).

Primul meu contact cu calculatoare româmești a fost acest [fascinant articol
din Ars Technica despre Cobra][1].  Voi încerca să las detaliile să fie
prezentate de surse mai autorizate, dar pe scurt, Cobra a fost un calculator
proiectat de cercetători din [Brașov, România][2] (de aceea COmputer BRAșov -
COBRA) în anii '80.  Doar câteva Cobra-uri oficiale a fost realizate, dar din
cauza dificultații de a obține calculatoare în acele vremuri, Cobra a dezvoltat
un cult printre studenți care le-au construit în privat cu utilizarea copii ale
schemelor și componente cumpărat din piața neagră.

[1]: https://arstechnica.com/gadgets/2017/11/the-underground-story-of-cobra-the-1980s-illicit-handmade-computer/
[2]: https://en.wikipedia.org/wiki/Brașov

Desigur, existau [multe alte calculatoare interesante din România
comunistă][3].  Mă ocup puțin cu colectare de calculatoare de epocă, deci
citând despre aceste, m-am întrebat cum aș putea să obțin unul în SUA.  În
lipsa acesteia, de ce să nu construie un Cobra de propria mea ca cum au făcut
pe vremuri?  Așa că asta am făcut.

[3]: https://retroit.ro/product-category/calculatoare-romanesti/

Din ferecire pentru mine, există o resursă fantastică despre Cobra:
[cobrasov.com](http://cobrasov.com).  Fără asta aș fi renunțat cu siguranță.
Are istorie, manualele originale, scheme, software, și documentație de
construirea autorului unor Cobra-uri în anii '90 precum și 2016.  Eforturi de
conservare așa sunt atât de important, și vă încurajez să te uiți la site-ul.
De fapt, e mult mai interesant decât acest articol de blog.

Site-ul e internaționalizată în limbile engleză și română, și de aceea
documentez construirea mea în ambele limbile de asemenea.  În plus, dacă citiți
asta în română, puteți vedea că am nevoie de practica.

![Cobra](/assets/posts/cobra/cobra.jpg){:height="50%" width="50%"}
*Replica mea a Cobra*

## Un pic despre Cobra

Cobra este o clonă a [ZX Spectrum][4], un calculator din Regatul Unit.  A fost
realizat destul de ieftin și prin urmare a fost omniprezent în întreaga Europa.
În multe țări au fost clone inclusiv SUA cu [Timex Sinclair][5].

Spectrum are procesor [Z80][6] care rulează la 3.5 MHz, 16K sau 48K de RAM,
grafice bitmap, și sunet beeper.  Nu există nici un cip elegant pentru grafice
sau sunet ca VIC II sau SID - CPU-ul trebuie să face totul.  Interfața
periferică este implementată de către un cip dedicat numită ULA.  Spectrum are
un ROM cu un interpret BASIC, și alte programe software au fost distribute pe
bande audio.

Cobra include toate acestea într-un mod compatabil.  Chiar și implementază
funcțiile a ULA folosind cipuri logice din seria 74.  De asemenea, Cobra are
mai multă memorie - 64K (sau 80K cu modificări) - și o interfață de disc
floppy.  Are diferite moduri de adresare care nu sunt compatibile cu Spectrum
dar permite utilizarea [CP/M][7] și alte sisteme.  Deci, e mai mult decât doar
o clonă.

[4]: https://en.wikipedia.org/wiki/ZX_Spectrum
[5]: https://en.wikipedia.org/wiki/Timex_Sinclair
[6]: https://en.wikipedia.org/wiki/Zilog_Z80
[7]: https://en.wikipedia.org/wiki/CP/M

## Construcția

### Plăci de circuite

La început, am folosit imaginile a plăcilor din cobrasov.com și le-am avut
produs de un productor de placă de circuite imprimate.:

(de la stânga la dreapta în imnaginea)

* Interfaţa de floppy disk v.1.0
* Modulul cu modificări rev.0.4a
* Codor PAL v.0
* Placa de bază v.0.2 (rev.3.16a)
* Tastatura v.1.0

![Plăci de circuite](/assets/posts/cobra/boards.jpg)

### Componente și surselor lor

Blocul răsăritean a avut o întreagă industriei semiconductorilor proprie, și în
scopul de a face Cobra meu un pic mai autentic, am decis să folesesc doar
IC-uri antichitate din acel moment și din acel loc.  În mare parte, ei sunt din
URSS dar cu niște excepții:  CPU-ul este U880 din Germania de Est, DRAM e din
Cehoslovacia, și câteva IC-uri sunt din Băneasă în România pentru a numi doar
câteva.  Din păcate, n-am găsit înlocuitori răsăriteni pentru două PROM-uri,
dar orice altceva este autentic.

(Acest lucru a fost un proiect pe termen lung.  Deși multe dintre componente am
cumpărat din Rusia, asta a avut loc la începutul anului 2021, deci eu nu am
spargat blocada.)

Am citit că componente din piața neagră pe vremuri nu a fost foarte fiabile,
deci am testat cu migală funcțiile logice a fiecărui IC-uri înainte de a le
instala.  Aceasta s-a dovedit nenecesar, deoarece fiecare dintre ei au trecut
proba.

Pentru componente pasive, eu am folosit componente moderne.

### Sursa de alimentare

Am avut norocul să găsesc [o sursă de alimentare existentă][8] care avea deja
tensiunile corecte și conector corect, dar pinii conectorului nu a fost corect.
Tot ce a trebuit să fac a fost să schimb firele pe placa de circuit a sursei de
alimentare.

[8]: https://www.digikey.com/en/products/detail/mean-well-usa-inc/GP25A13A-R1B/7703336

### Placa de bază

![Pregătirea placii de bază](/assets/posts/cobra/preparing.jpg){:height="50%" width="50%"}
*Pregătirea placii de bază și sursei de alimentare*

![Programarea EEPROM](/assets/posts/cobra/eeprom.jpg){:height="30%" width="30%"}
*Programarea unui EEPROM*

Cu sursa de alimentare gata, și după am terminat lipirea și instalarea
componentelor și programat EEPROM-uri, am fost surprins să văd logo-ul de boot.

![Programarea EEPROM](/assets/posts/cobra/firstboot.jpg){:height="50%" width="50%"}
*Calculatorul este viu!*

La început, a fost a problemă ciudată grafică care îmbunătățit după ce
calculatorul a mers o vreme - zone umplute pe ecranul, ca litere de logo-ul de
boot, ar completa treptat.  Variația în timp m-a făcut să mă întreb dacă de
asemenea a existat o variație corespunzătoare în temperatură, deci am atins
fiecare IC în circuitul video și am găsit unul fierbinte.  Destul de sigur,
după înlocuirea IC-ului, problema a fost rezolvată.

Dar chiar și așa, mă așteptam la mai multe dificultăți în obținerea pixelilor
pe ecran.  Puțin știam câtă muncă mai a rămas de făcut...

ROM-ul de boot permite utilizatorilor să alege să încărca din bandă audio, din
dischete, sau din ROM-ul de BASIC.  Încărcarea din ROM-ul de BASIC e metoda cea
mai simplă, deci acesta a fost următorul pas, dar n-a mers.

Una dintre problemele a fost timing-uri memoriei.  ROM-ul de boot în sine merge
din EEPROM, nu din RAM, deci nu este afectat de această problemă.  Dar din
cauză variație timpurilor de acces memoriilor și de asemenea diferențe de
viteză dintre tehnologiile utilizate în IC-uri pentru logica interfeței, este
necesar să se întarzie unele dintre semnale astfel încât ajung la memoria la
timpul potrivit.  Acest lucru se face prin ajustarea valorilor (înlocuirea,
cu alte cuvinte) a cinci condensatoare.  Aceasta a necesitat o grămadă de
încercare și eroare, dar în sfârșit am reușit să încărc ROM-ul de BASIC în RAM
și îl pornesc de acolo.

Dar încă BASIC nu ar termina pornire, deci am scos analizorul logic și
emulatorul EEPROM și, în sfârșit, după o seară întreagă de depanare, am
urmărit problema la un jumper cu setarea incorectă.  În fapt, dacă aș fi
petrecut cinci minute în timpul asamblării să înțeleg setările jumperilor în
loc să mă grăbesc, toate astea puteau fi evitate.  Aș vrea să pot spune că a
fost singura dată când s-a întâmplat asta.

![Depanarea](/assets/posts/cobra/troubleshooting.jpg){:height="50%" width="50%"}
*Depanarea CPU-ului*

În cele din urmă, eu am ajuns la BASIC!  Reușeam chiar să încărc niște software
Spectrum din audio (folisând fișiere WAV pe laptop în loc de un reportofon).

![BASIC](/assets/posts/cobra/basic.jpg){:height="50%" width="50%"}
*Ecran de BASIC*

Următoarea provocare a fost încărcarea CP/M-ului din dischete.   Nici asta nu a
mers de la început.  Încă o dată, am adus analizorul logic și emualtorul EEPROM
și am petrecut o seară întreagă de depanare să aflu care setările jumperilor
le-am ignorat în timpul asemblării.  Dar totuși, chiar și cu setările corecte,
nu a mers.

Până acum am folosit Cobra în modul 64K, și am observat că au fost multe
diferențe între ROM-ul de boot pentru 64K și ROM-ul de boot pentru 80K.  Am
decis să încerc reconfigurarea calculatorului în modul 80K.  Acest lucru se
face prin modificarea setărilor jumperilor, dar din păcate, am aflat că
timing-uri memoriei nu mai era corect pentru că modul 80K a modificat căile
semnalelor memoriei.  Deci, a fost necesar să reglez memoria peste tot din nou.

Dar cu modul 80K de lucru, am reușit să rulez CP/M!

![CP/M](/assets/posts/cobra/cpm.jpg){:height="50%" width="50%"}
*Ecran de CP/M*

A fost o problemă ultimă, care nu am observat până am început să folosesc mai
multe din memoria - nu am putut face uz de o parte din spațiul superior de
adrese.  Am urmărit problema la poarta cu diode compusă din D19, D20, și D21.
S-a dovedit că autorul de cobrasov.com a avut și aceeași problema și a
documentat-o.  Nu știu de ce nu funcționează, dar am înlocuit poarta cu 7411
care a rezolvat-o.

![Diode](/assets/posts/cobra/diodegate.jpg){:height="20%" width="20%"}
![Cip](/assets/posts/cobra/bodgegate.jpg){:height="20%" width="20%"}
*Înlocuirea diodelor cu cip*

### Tastatura

Am lucrat la tastatură în timp ce construirea placa de bază.  În primele etape,
am angajat o tastă (ca 'B'-ul la ecranul de boot pentru a porni BASIC) prin
scurtcircuitarea gaure corespunzătoare pe placa de tastatură.  După ce l-am
făcut să meargă BASIC, asta nu mai era suficient.

Curând am aflat că n-aș reuși să folosesc placa de tastatură din cobrasov.com
pentru că comutatoarelor acestuia sunt orientate la un inghi de 90 de grade, și
tastele perzonalizate (din [WASD Keyboards][9]) care am planificat să-l
utilizez sunt direcțional.  Mi-ar trebuie să proiectez [propria mea placa de
tastatură][10].  Am adaptat placa din cobrasov.com să se rotească comutatoarele
și să se potrivească dimensiunile tastelor WASD-ului.

[9]: https://www.wasdkeyboards.com/
[10]: https://github.com/tsowell/cobra-keyboard

#### Legende tastelor

Am vrut tastele să includă legende pentru fiecare dintre funcțiile tastelor pe
tastatura ZX Spectrum.  Am știut că asta ar fi nevoie de mult ajustări, deci am
creat [un singur șablon SVG și am scris un script Python][11] să genereze
automat toate tastele pe baza șablonului și le introduce în șablonul WASD-ului.
Această metodă economisit foarte mult timp și asigurat consistența tastelor.

![Procesul pentru keycaps](/assets/posts/cobra/keycaps.png){:height="50%" width="50%"}

Designul este un omagiu a ZX Spectrum 48K.

![Tastatura de ZX Spectrum](/assets/posts/cobra/zxspectrum.jpg){:height="50%" width="50%"}
*Tastatura de ZX Spectrum*

![Tastatura mea pentru Cobra](/assets/posts/cobra/keycaps.jpg){:height="70%" width="70%"}
*Tastatura mea Cobra*

[11]: https://github.com/tsowell/cobra-keycaps

### Unități de Disc

Unitați de disc sunt necesare pentru CP/M, deci a trebuit să le fac să
funcționeze pentru asta.  Unități floppy de 3.5" poate fi folosit cu Cobra
atâta timp cât au fost modificat să ofere un semnal READY conform standardului
Shugart.  Ca de obiciei, [cobrasov.com are informații detaliate][12].  Totuși,
am sărit peste soluția descrisă acolo și am optat să adaug un comutator READY
pentru fiecare unitatea.  Pe lângă faptul că este mai ușor de implementat,
abilitatea de a dezactiva unității cu comutator poate fi utilă.

![Comutatorile](/assets/posts/cobra/switches.jpg){:height="30%" width="30%"}
*Comutatorile*

[ZX Spectrum 128K][13] a avut un cip de sunet [AY-3-8912][14] care se intâmplat
să fie la aceeași adresă cu interfața de disc Cobra-ului.  Plăcile de extensie
AY-3, ca [Melodik][15] din Polonia, au fost făcute pentru ZX Spectrum 48K
folosind aceeași adresă.  Rezultatul este că programe pentru Spectrum care
utilizează AY-3 poate provoca accese parazite la disc, și cu o ocazie am
pierdut date din cauza asta.  Acum, de regulă, folosesc comutatoarele READY să
dezactivez unitățiile în timpul utilizării software-ului Spectrum.

[12]: http://cobrasov.com/CoBra%20Project/left-fdd.html
[13]: https://en.wikipedia.org/wiki/ZX_Spectrum#ZX_Spectrum_128
[14]: https://en.wikipedia.org/wiki/General_Instrument_AY-3-8910
[15]: https://spectrumcomputing.co.uk/entry/1001155/Hardware/Melodik

### Carcasa

Pe vremuri, oameni a instalat Cobra-uri în carcase tradiționale în formă de
wedge.

![Cobra în carcasa originală](/assets/posts/cobra/originalcobra.jpg){:height="30%" width="30%"}
*Cobra în carcasa originală*

Pentru simplitatea, am luat o abordare diferită și am făcut o carcasă simplă
din acril cu un design deschis.  Placa de bază și placa de tastatură conectarea
spre un panou inferior, și un panou superior acoperă placă de bază.  De
asemenea, panoul superior are orificii pentru montarea de a două unitați de
disc vertical, și are un loc pentru a pune un ecran.  Am folosit acril
transparent pentru panoul superior în scopul de a afișa placa de bază și
IC-urile antichitate.

![Carcasa mea](/assets/posts/cobra/case.jpg){:height="50%" width="50%"}

*Panoul inferior pe stânga și panoul superior pe dreapta, ambii afișat cu componentele montate*

### Video

Inițial, calitatea video a fost slabă, și am luptat timp de luni pentru a
rezolva asta.  La început, text negru pe fundal alb a fost ilizibil, dar l-am
îmbunătățit prin optimizarea valorilor componentelor pe codorul PAL.  Dar apoi
nu a putut să citesc text alb pe fundal negru.  După multă muncă și mai multe
modificări la circuitele video le-am echilibrat cât de bine am putut.

cobrasov.com documentează diferite modele de codori PAL de pe vremuri, și
foloseam [cel care autor a folosit în anii '90 cu prima placă sa de bază][16].
Am decis să încerc [un alt design][17], pentru care există scheme pe site, în
speranța că ar avea calitatea mai bine.  Am proiectat [o placă pentru această
versiune][18].  Cred că a ajutat un pic, și cu siguranță are culori mai
precise, dar încă nu eram satisfăcut.

![Codorul PAL meu](/assets/posts/cobra/palcoder.jpg){:height="30%" width="30%"}
*Codorul PAL meu*

În sfârșit, într-o zi când am fost lucrând pe o altă parte de calculatorul, am
decis să aplic depanare termică din nou.  Până la urmă, calitatea video s-a
imbunătătit cu timp de funcționare (sună cunoscut?).  Destul de sigur, am găsit
un cip cald și l-am înlocuit, după care video a fost foarte clar!

[16]: http://cobrasov.com/CoBra%20Project/pal0.html
[17]: http://cobrasov.com/CoBra%20Project/pal2.html
[18]: https://github.com/tsowell/cobra-palcoder-21

## Proiectele

În afara de construirea calculatorului, am lucrat la niște proiecte
hardware/software care gravitează în jurul Cobra-ului.  Un cuplu de repere sunt
o placă de sunet AY-3 și programul RUNZ80, un încărcător de snapshot-uri .z80
pentru CP/M.

În viitor aș vrea să cercetez portarea a CP/M 3, să scrie un player de muzică
[AY][19] pentru CP/M, și să scrie [un demo][20] Spectrum.

[19]: http://www.vgmpf.com/Wiki/index.php?title=AY
[20]: https://en.wikipedia.org/wiki/Demoscene

### Placa de Sunet AY-3

Cobra, la fel ca Spectrum 48K, are doar beeper pentru sunet.  În ciuda multor
utilizări ingenioase de către scena demo, înca e cam limitat beeper-ul.  O
placă de sunet cu cipuri [AY-3][21] a fost un plus destul de popular pentru
Spectrum 48K și calculatoare compatibile, și mulțime de software face uz de ea.
Am un interes în muzică de calculator și am vrut să experimentez asta, deci am
făcut [o astfel de plăcă pentru Cobra][22].

Este o îmbunătățire utilă.  Un aspect amuzant e că din cauza coliziunii de
adrese cu interfața de disc, indicatoare luminoase unităților de disc clipesc
în ritm cu muzică.

![Placa de sunet AY-3](/assets/posts/cobra/ay3.jpg){:height="50%" width="50%"}
*Placa de sunet AY-3*

[21]: https://en.wikipedia.org/wiki/General_Instrument_AY-3-8910
[22]: https://github.com/tsowell/cobra-ay-3-8192

### RUNZ80

Software pentru Spectrum 48K a fost distribuit pe bandă audio, și în prezent
[înregistrări digitale ale benzilor][23] pot fi găsite pe internet.  Încărcarea
din bandă durează aproximativ 3-5 minute, și procesul nu este de încredere.
Chiar și atunci când încărcarea reușeste, des decopăr că programul a fost de
fapt scris pentru Spectrum 128K (deși nu a fost etichetate ca atare) și nu va
funcționa pe Cobra.  Am crescut obosit de asta.

cobrasov.com documentează [o metodă genială pentru backupul software-ului][24]
în care un program e încărcată din bandă, și apoi starea completă a
calculatorului e scris înapoi la bandă.  Atunci de la CP/M, starea e scris pe
disc și se adaugă o rutină loader.  În acest punct, programul poate fi încărcat
din disc de la CP/M, și rapid.

Am vrut să fac și eu la fel, dar am vrut să trișez un pic.  Emulatoare Spectrum
pe hardware modern pot încărcare din bandă virtuală într-o clipă și pot să crea
ușor snapshot-uri de memorie.  Și în plus, astăzi, snapshot-uri preexistente
sunt disonibile pe internet în formate standard [ca .z80][25].

Deci, soluția mea este [RUNZ80][26], un program independent pentru CP/M care
analizează fișiere .z80 nemodificate în scopul de a restaura starile CPU-ului
și memoriei din ei și a le execută.  Durează în jur de 12 secunde pentru RUNZ80
să pornească un program din un snapshot, și susține compresia a conținutului
memoriei pentru a economi spațiu pe disc.

De asemenea, am modificat [emulatorul Fuse][27] astfel încât să încărce un
fișier de bandă audio și să creeze un snapshot pentru RUNZ80 imediat în un mod
fără cap.  În acest fel, atunci când s-au lansat la începutul acestui an
[traduceri ale jocurilor slovace din anii '80][28], am reușit să rulez-le pe
calculatoarea mea comunistă cu efort minim.

[23]: https://worldofspectrum.org/faq/reference/formats.htm#Tape
[24]: http://cobrasov.com/CoBra%20Project/basic+nmi.html
[25]: https://worldofspectrum.org/faq/reference/z80format.htm
[26]: https://github.com/tsowell/runz80-cobra
[27]: http://fuse-emulator.sourceforge.net/
[28]: https://scd.sk/clanky/playable-english-localizations-of-slovak-digital-games-from-the-late-80s-period/

## Impresii

Când eram copil, primul calculator familiei mele a fost 286, deci calculatoare
de 8 biți ca Cobra și Spectrum au fost puțin înainte de vremea mea.  Cu toată
sinceritatea, întotdeauna am crezut că ei sunt prea limitate să fie de interes.
Nici măcar nu au MMU!

Dimpotrivă, m-am distrat atât de mult cu Cobra.  În privința compatibilitatea
cu Spectrum, acel calculator e puțin cunoscut în SUA, deci software-ul său e o
lume nouă pentru mine.  Mi-a plăcut în special demo-uri din [scena demo][29]
pentru programarea genială și artistica.  Nu am planuri pentru programarea în
Spectrum BASIC pe Cobra, dar am învățat să programez în copilărie cu
[QBasic][30] pentru MS-DOS, și văd acum cum QBasic a reușit să satisfacă nevoia
unei mediu de programare mai simplu, cum a făcut BASIC cu calculatoarele de 8
biți.

[29]: https://en.wikipedia.org/wiki/Demoscene
[30]: https://en.wikipedia.org/wiki/QBasic

Chiar mi-a depășit așteptările CP/M-ul.  Nu mi-am închipuit vreodată cum un
sistem de operare mai primitiv decât MS-DOS ar putea fi foarte util, dar am
fost surprins de cat de repede am devenit productiv în CP/M.  Și am surprins de
cât de ușor a fost să învăț cum să folosesc [ED][31], un editor care lucrează
linie cu linie la fel ca [editorul pentru Unix cu același nume][32].  Am fost
mereu intimidată de editoare de acest tip, dar curând am fost făcând modificări
complexe fără măcar să uit mai întâi la fișierele.

Și am fost uimit de cât de deschis se simțe CP/M.  Prin utilizarea de un
debugger și disassembler, este foarte ușor să se uite în jurul codul mașină în
memoria pentru a vedea cum funcționează.  Probabil ajută că spațiul de adrese e
atât de mic.  Chiar dacă nu a fost open source, cred că sistemul încă mai
transparent decât MS-DOS-ul sau Windows-ul copilăriei mele.

[31]: http://www.gaby.de/cpm/manuals/archive/cpm22htm/ch2.htm
[32]: https://en.wikipedia.org/wiki/Ed_(text_editor)

### Concluziile

În primul rând, dacă aveți vreun interes, constriuirea propriului calculator de
8 biți recomand din toată inima.  Există multe kituri bazat pe Z80, 6502, etc.
care sunt de asemenea moduri grozave de a începe.  Îmi incipui că dacă aș fi
cumpărat un calculator existent mi-aș fi pierdut interesul foarte repede, dar
prin murdărirea mâinilor am învățat mai mult și am format o conexiune de durată
cu mașina.

Cred că am reușit în mică măsură să capturez sentimentul acestei epoc de
calcul.  Am constatat chiar că am preferat să imprim documentația în loc să o
caut online.  Există o puritate în o mașină atât de simplă și a avea toate
cunoștințele care aveți nevoie la îndemană.

De asemenea, am putut să se angajez cu istoria unică a Cobra-ului.  Am
construit replica mea în modul ușor - în prezent, pot avea făcute plăci de
circuit la celălalt capăt al lumii făra măcar să vorbesc cu nimeni, dar pentru
persoana tipică în românia anilor '80, astfel de lucruri nu a putut fi obținute
fără sacrificiu.  În plus au avut componente ne-fiabile, și adesea n-au avut
osciloscop nici analizor logic, și cu siguranță nici internet.  Nu-mi pot
imagina circumstanțele lor, dar pot să admir determinarea lor, și poate că eu
pot să se refere la necesitatea lor fundamentală de computing.  Sunt foarte
norocos să avea povestea lor să mă inspire.

![Cobra](/assets/posts/cobra/conclusion.jpg){:height="60%" width="60%"}
*Programare pe Cobra*

## Linkurile de pe Github

Cod și fișiere de design pentru piesele personalizate sunt pe Github:

* Carcasa: [cobra-case](https://github.com/tsowell/cobra-case)
* Tastatura: [cobra-keyboard](https://github.com/tsowell/cobra-keyboard)
* Taste: [cobra-keycaps](https://github.com/tsowell/cobra-keycaps)
* Codorul PAL: [cobra-palcoder-21](https://github.com/tsowell/cobra-palcoder-21)
* Placa de sunet AY-3: [cobra-ay-3-8192](https://github.com/tsowell/cobra-ay-3-8192)
* RUNZ80: [runz80-cobra](https://github.com/tsowell/runz80-cobra)

## Galeria foto

[Galeria foto Cobra]({% post_url 2022-09-27-cobra-gallery %})
