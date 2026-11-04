# Mapa de visualitzacions: de la pregunta al gràfic

Cada visualització respon **una pregunta**, i cada bloc de la web n'explica una part de la història. Aquesta taula serveix per no perdre el fil. **No cal que tots els gràfics acabin a la web**: en cada bloc n'hi ha un d'**imprescindible** (⭐) i els altres són opcionals.

**La història en una frase:** treballar i cobrar no sempre arriba per final de mes, perquè les feines canvien, els sous creixen menys que alguns preus i la part de la despesa que es gasta en necessitats bàsiques aprieta.

## 0. Introducció: el cercle
| Pregunta | Gràfic | Estat |
|---|---|---|
| Què vol dir "arribar a final de mes"? | Cercle que es fa petit (cicle treballar-guanyar-gastar). Es fa amb D3, més endavant | pendent |

## 1. El treball: quines feines hi ha i quines desapareixen
| Pregunta | Plantilla de Flourish | Fitxer | Prioritat |
|---|---|---|---|
| Quines grans feines guanyen o perden treballadors? | *Bar chart race* | `flourish_cursa_isco1.csv` | ⭐ |
| I dins de cada gran grup? | *Bar chart race* (una per grup) | `flourish_cursa_isco2_OC*.csv` | opcional |
| On es fa cada feina? (països × ocupació) | *Heatmap* | `flourish_heatmap_isco.csv` | opcional |
| Com ha evolucionat una feina país per país? | *Projection map* amb filtre i temps | `flourish_mapa_isco.csv` | opcional |
| Quines feines tenen més dones i quines menys? | *Scatter* amb temps | `flourish_ocupacions_scatter.csv` | opcional |

## 2. Els salaris: quant es cobra i qui cobra menys
| Pregunta | Plantilla de Flourish | Fitxer | Prioritat |
|---|---|---|---|
| Quant ha pujat el salari comparat amb els preus? | *Line chart* | `flourish_linies_pais.csv` | ⭐ |
| Els homes cobren més que les dones? On i en quines feines? | *Scatter* (dumbbell) amb temps i filtre | `flourish_bretxa_ocupacio.csv`, `flourish_bretxa_sector.csv` | ⭐ |
| Com s'acosta el salari mínim al salari mitjà? | *Line chart* / *Scatter* (dumbbell) | `flourish_salari_minim_*.csv` | opcional |

## 3. Les despeses: en què es gasta
| Pregunta | Plantilla de Flourish | Fitxer | Prioritat |
|---|---|---|---|
| Ha pujat l'habitatge més que la resta de preus? | *Bar chart race* | `flourish_barchartrace_habitatge_real.csv` | ⭐ |
| Com ha canviat el repartiment de la despesa? | *Stacked bars* al 100 % | `flourish_despeses_apilat.csv` | ⭐ |
| En què gasta cada país? (països × categoria) | *Heatmap* | `flourish_heatmap_coicop.csv` | opcional |
| Evolució d'una despesa país per país | *Projection map* amb filtre i temps | `flourish_mapa_coicop.csv` | opcional |
| Els països rics gasten menys en menjar? | *Scatter* amb temps | `flourish_despeses_scatter.csv` | opcional |

## 4. La pobresa: qui no hi arriba
| Pregunta | Plantilla de Flourish | Fitxer | Prioritat |
|---|---|---|---|
| Els països més desiguals tenen més pobresa? | *Scatter* amb temps | `flourish_pobresa_scatter.csv` | ⭐ |
| Treballar protegeix de la pobresa? Homes i dones | *Scatter* (dumbbell) amb temps | `flourish_pobresa_laboral_genere.csv`, `flourish_pobresa_genere.csv` | ⭐ |
| Qui és més pobre: infants o gent gran? | *Scatter* (dumbbell) amb temps | `flourish_pobresa_edat.csv` | opcional |
| On és més alta la pobresa? | *Projection map* | `flourish_pobresa_mapa.csv` | opcional |

## Com es relacionen entre elles
```
FEINES (1)  →  quant es cobra (2)  →  en què es gasta (3)  →  qui queda a baix (4)
 quines hi ha     sou i bretxa         menjar i habitatge       pobresa i atur
```
Cada bloc acaba amb la pregunta del següent: *"i aquests sous, què permeten comprar?"*, *"i què queda, quan es paga l'habitatge?"*.

## Pendents
- **Quintils de renda:** les despeses són mitjanes. Falta saber què gasten les llars pobres (enquesta de pressupostos familiars d'Eurostat).
- **Introducció amb D3** (el cercle).
- **Revisió final** de totes les descàrregues i neteja del repositori.
