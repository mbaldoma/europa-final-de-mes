## Glossari

Termes i classificacions que apareixen a les dades. Si una columna et sembla estranya, mira primer `data/diccionari_variables.csv` i després aquest glossari.

### Mercat de treball

**Població activa, ocupada, aturada i inactiva.** De tota la població en edat de treballar, unes persones **treballen** (ocupades), unes altres **busquen feina** i n'estarien disponibles (aturades), i la resta **ni treballa ni en busca** (inactives): estudiants, jubilats, persones que cuiden la família, persones amb una malaltia llarga... Les ocupades més les aturades formen la **població activa**.

**`atur_T` i `ocupacio_T` no sumen 100 %.** Tenen dos denominadors diferents:

| | Es calcula com | Edats | Fonts |
|---|---|---|---|
| Taxa d'atur | aturats / **població activa** | 15-74 anys | `une_rt_a` |
| Taxa d'ocupació | ocupats / **població total** d'aquesta edat | 15-64 anys | `lfsa_ergan` |

Les inactives només són a la taxa d'ocupació, i les edats són diferents. Per això un 70 % d'ocupació amb un 8 % d'atur és perfectament coherent. Les dues mesuren coses relacionades però no redundants: l'**atur** diu quanta gent busca feina i no en troba, i l'**ocupació** diu quanta gent treballa en total. Un país pot tenir poc atur i poca ocupació si molta gent ni tan sols busca feina, i això passa sovint amb les dones en alguns països.

**Bretxa salarial de gènere sense ajustar.** Diferència entre el sou per hora dels homes i el de les dones, en % del dels homes. No descompta que treballin en sectors o jornades diferents, i per això no és "cobrar menys per la mateixa feina".

**Vacant.** Lloc de treball obert que l'empresa vol cobrir i encara no ha cobert. La **taxa de vacants** és vacants / (llocs ocupats + vacants).

### Renda, pobresa i desigualtat

**Salari net.** El que s'emporta el treballador un cop descomptats impostos i cotitzacions. `salari` és el d'una persona soltera, sense fills i amb un sou igual al mitjà del país (és una persona tipus, no la mitjana de tothom).

**Nominal i real.** Un valor **nominal** és en euros del seu any, sense tenir en compte que els preus pugen. Un valor **real** descompta la inflació. `salari_real_idx2010` és el salari amb la inflació treta.

**Índex amb base.** Un índex amb 2015 = 100 (o 2010 = 100) compara cada any amb l'any base. Un 130 vol dir un 30 % més que aquell any. Serveix per comparar evolucions, no nivells: tots els països valen 100 l'any base.

**PPS** (*Purchasing Power Standard*, estàndard de poder adquisitiu). Una unitat artificial que elimina les diferències de preus entre països, de manera que 1 PPS compra el mateix a tot arreu. `sou_hora_pps_T` és el sou per hora en aquesta unitat.

**Risc de pobresa.** Viure en una llar amb una renda per sota del **60 % de la renda mediana del país** (la mediana és el valor del mig: la meitat de la població cobra més i l'altra meitat menys). Es calcula per a cada llar, tenint en compte quanta gent hi viu, i per això és un llindar **relatiu**: mesura desigualtat dins d'un país, no pobresa absoluta.

**`pobresa_lab_*` (pobresa laboral).** No es mesura el sou de la persona, sinó la renda de la **seva llar**. Una persona ocupada és "en risc de pobresa" quan, tot i treballar, els ingressos de la seva llar queden per sota del llindar. Passa quan el sou és baix, quan es treballa poques hores, quan hi ha moltes persones a càrrec amb un sol sou o quan la llar només té un sol ingrés.

**AROPE** (*At Risk Of Poverty or social Exclusion*). Persones que compleixen almenys una d'aquestes tres condicions: renda de la llar per sota del 60 % de la mediana, privació material i social severa (per exemple no poder pagar la calefacció), o llar amb molt poca feina (els adults van treballar menys del 20 % del seu potencial).

**Coeficient de Gini.** Mesura la desigualtat de la renda en una escala de 0 a 100. El 0 és igualtat perfecta, i el 100 que una persona té tots els ingressos. A Europa els valors són al voltant de 25-35. Mesura la renda, no el patrimoni.

**Sobrecàrrega de l'habitatge.** Persones que viuen en llars que dediquen més del 40 % de la renda disponible a l'habitatge.

### PIB per habitant no és "el que es paga als treballadors"

`pib_hab` i `salari` no es poden comparar en valor absolut, i **que el PIB per habitant sigui més gran que el salari no vol dir que es pagui poc**. Hi ha diverses raons:

- El **PIB per habitant** divideix el valor produït per **tota la població**, també per infants, jubilats i persones aturades. El `salari` és el d'**un sol treballador**.
- El PIB inclou coses que no són salari: **beneficis de les empreses**, impostos, amortitzacions i rendes del capital. A països com Irlanda o Luxemburg, el PIB s'infla per la presència de les seus de multinacionals, i no es reflecteix en la renda de la gent.
- El `salari` és **net** (després d'impostos), i el PIB és **brut**.

Per tant, el que té sentit mirar és com **evolucionen** les dues coses, o la relació entre països (si els països rics tenen sous més alts). Si volguessis saber quina part de la producció va als treballadors, caldria un altre indicador (la *part salarial* del PIB), que no tenim.

### Classificació de sectors: NACE Rev. 2

Classifica **on treballa** l'empresa. Els sectors són pocs: 21 lletres.

| Lletra | Sector |
|---|---|
| A | Agricultura, silvicultura i pesca |
| B | Indústries extractives |
| C | Indústria manufacturera |
| D | Energia elèctrica, gas i vapor |
| E | Aigua, sanejament i residus |
| F | Construcció |
| G | Comerç i reparació de vehicles |
| H | Transport i emmagatzematge |
| I | Hostaleria |
| J | Informació i comunicacions |
| K | Activitats financeres i assegurances |
| L | Activitats immobiliàries |
| M | Activitats professionals, científiques i tècniques |
| N | Activitats administratives i serveis auxiliars |
| O | Administració pública i defensa |
| P | Educació |
| Q | Sanitat i serveis socials |
| R | Arts, entreteniment i oci |
| S | Altres serveis |
| T | Llars com a ocupadors |
| U | Organitzacions extraterritorials |

Un codi amb guió és un **rang**: `B-F` de la B a la F, `G-N` de la G a la N, `P-S` de la P a la S i `B-N` de la B a la N. `B-S_X_O` és de la B a la S **excepte** la O, és a dir, tota l'economia sense l'administració pública.

### Classificació d'ocupacions: ISCO-08

Classifica **quina feina fa** la persona, sigui quin sigui el sector de l'empresa. Té **nivells**, i cada dígit afegeix detall:

| Nivell | Exemple | Quantitat |
|---|---|---|
| Gran grup (1 dígit) | `OC7` Artesans i treballadors d'oficis | 10 |
| Subgrup (2 dígits) | `OC71` Treballadors de la construcció (excepte electricistes) | 43 |

(També existeixen nivells de 3 i 4 dígits, que no tenim.)

| Gran grup | Ocupació |
|---|---|
| `OC0` | Forces armades |
| `OC1` | Directius i gerents |
| `OC2` | Professionals científics i intel·lectuals |
| `OC3` | Tècnics i professionals de suport |
| `OC4` | Personal administratiu |
| `OC5` | Treballadors de serveis i vendes |
| `OC6` | Treballadors qualificats agrícoles, forestals i pesquers |
| `OC7` | Artesans i treballadors d'oficis |
| `OC8` | Operadors d'instal·lacions i maquinària i muntadors |
| `OC9` | Ocupacions elementals |

`TOTAL` és la suma de totes les ocupacions i `NRP` vol dir "sense resposta".

### Com es creuen NACE i ISCO a `ses_mestre.csv`

Són **dues maneres independents de classificar la mateixa persona**. Una persona té una **ocupació** (què fa: paleta, administrativa, directora) i treballa en un **sector** (en què s'hi dedica l'empresa: construcció, sanitat). El mateix ofici es troba en molts sectors: hi ha administratius a la construcció, a la sanitat i a l'hostaleria. I a la construcció hi ha paletes, però també enginyers i administratius.

Cada fila de `ses_mestre.csv` és una **cel·la d'aquesta taula creuada**: una ocupació dins d'un sector, per a un país i un any. Per exemple, per a Espanya el 2018, els artesans i treballadors d'oficis (`OC7`) són:

| `nace_r2` | Sector | Assalariats | Sou per hora |
|---|---|---|---|
| `B-F` | Indústria i construcció | 774.108 | 10,80 € |
| `G-N` | Serveis empresarials | 217.466 | 10,12 € |
| `P-S` | Educació, sanitat i altres serveis | 31.705 | 10,17 € |
| `B-S_X_O` | Tota l'economia sense administració pública | 1.023.279 | 10,64 € |

Les tres primeres files **sumen** la quarta (`B-F` + `G-N` + `P-S` = `B-S_X_O`), per això la quarta és el total. **Compte de no sumar-les totes juntes**: es duplicaria.

A `ses_mestre.csv` només hi ha el **primer nivell d'ISCO** (`OC0`-`OC9` i `TOTAL`), i només els **quatre sectors agregats**. Això és així perquè l'enquesta, en aquest dataset d'Eurostat, no dona més detall. Els subgrups de dos dígits (`OC71`...) són només a `ocupacions_mestre.csv`, però **allà no hi ha sectors** ni sous. Per tant, no es pot saber el sou dels paletes (`OC71`), sinó només el dels artesans en general (`OC7`).

### Marques d'Eurostat (`OBS_FLAG`)

| Marca | Significat |
|---|---|
| `b` | Ruptura de sèrie |
| `p` | Provisional |
| `e` | Estimat |
| `d` | Definició diferent de l'estàndard |
| `u` | Poc fiable |
| `i` | Marca específica del dataset (se'n mostra el significat a Eurostat) |
