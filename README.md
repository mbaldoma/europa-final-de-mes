# europa-final-de-mes
"Europa a final de mes" és un projecte de ...
## Dades

## Conjunt de dades mestre: `data/panel_mestre.csv`

Taula única que reuneix tots els indicadors descarregats d'Eurostat. Cada fila és **un país en un any**; cada columna és una variable. Les dades no es modifiquen: són els **valors originals**, sense rebasar ni fer cap càlcul derivat.

- **Files:** 480 (32 països × 15 anys, 2010-2024).
- **Columnes:** 30 (3 d'identificació + 27 variables).
- **Valors buits:** hi ha cel·les buides quan Eurostat no publica la dada per a aquell país i any. Els buits **no són zeros**: no s'han omplert ni interpolat.
- **Marques d'Eurostat** (`OBS_FLAG`, com ara dades provisionals o ruptures de sèrie): no s'inclouen en aquest fitxer. Es troben als CSV individuals de la carpeta `data/`.
- **Generació:** els CSV individuals es descarreguen amb `descarrega_eurostat.py` i el quadern `cobertura.ipynb` els combina i desa el fitxer mestre.

Aquest fitxer no s'utilitza directament a tots els gràfics. Cada visualització parteix d'un **subconjunt** amb només els països que tenen totes les variables necessàries durant el període mostrat. El nombre de països i els anys de cada gràfic s'indiquen al peu de la visualització.

### Columnes d'identificació

| Columna | Descripció |
|---|---|
| `pais` | Nom del país, en anglès (p. ex. `Spain`, `Türkiye`) |
| `geo` | Codi del país a Eurostat (p. ex. `ES`; Grècia és `EL` i el Regne Unit `UK`) |
| `any` | Any de la dada (2010-2024) |

### Salaris i preus

| Columna | Descripció | Unitat | Dataset | Observacions |
|---|---|---|---|---|
| `salari` | Salari net anual d'una persona soltera sense fills amb un sou igual al 100 % de la mitjana del país | euros per any, valors nominals | `earn_nt_net` | |
| `sal_min` | Salari mínim mensual | euros per mes | `earn_mw_cur` | Les dades són semestrals; aquí és la mitjana dels dos semestres de l'any. Només 24 països: vuit no tenen salari mínim legal nacional (Àustria, Dinamarca, Finlàndia, Islàndia, Itàlia, Noruega, Suècia i Suïssa) |
| `habitatge` | Índex de preus de l'habitatge (compra, total d'habitatges nous i existents), mitjana anual | índex, base 2015 = 100 | `prc_hpi_a` | No hi ha dades per a Grècia ni Suïssa |
| `ipc_CP00` | Índex de preus de consum harmonitzat (HICP): **tots els béns i serveis** | índex, base 2015 = 100 | `prc_hicp_aind` | Inflació general |
| `ipc_CP01` | HICP: **aliments i begudes no alcohòliques** | índex, base 2015 = 100 | `prc_hicp_aind` | |
| `ipc_CP04` | HICP: **habitatge, aigua, electricitat, gas i altres combustibles** | índex, base 2015 = 100 | `prc_hicp_aind` | Inclou el lloguer i els subministraments |

### Mercat de treball

| Columna | Descripció | Unitat | Dataset | Observacions |
|---|---|---|---|---|
| `vacants` | Taxa de vacants a la **construcció** (NACE F): llocs vacants respecte del total de llocs de treball, empreses de totes les mides | % | `jvs_a_rate_r2` | Mitjana anual. Algunes sèries comencen més tard (p. ex. Itàlia, Malta) |
| `atur_T`, `atur_M`, `atur_F` | Taxa d'atur de 15 a 74 anys: total, homes i dones | % de la població activa | `une_rt_a` | No hi ha dades per al Regne Unit |
| `ocupacio_T`, `ocupacio_M`, `ocupacio_F` | Taxa d'ocupació de 15 a 64 anys: total, homes i dones | % de la població d'aquesta edat | `lfsa_ergan` | Tota la ciutadania |
| `bretxa_B-N` | Bretxa salarial de gènere sense ajustar, a l'**economia empresarial** (NACE B-N) | % | `earn_gr_gpgr2` | Diferència entre els guanys per hora d'homes i dones, respecte dels dels homes. Prové de l'enquesta d'estructura salarial, que no es fa cada any a tots els països: té buits |
| `bretxa_F` | Bretxa salarial de gènere sense ajustar a la **construcció** (NACE F) | % | `earn_gr_gpgr2` | Mateix que l'anterior |

### Pobresa i desigualtat

| Columna | Descripció | Unitat | Dataset | Observacions |
|---|---|---|---|---|
| `pobresa_lab_T`, `pobresa_lab_M`, `pobresa_lab_F` | Taxa de risc de pobresa de les persones **ocupades** de 18 a 64 anys: total, homes i dones | % | `ilc_iw01` | Treballadors pobres |
| `sobrecarrega` | Població que viu en llars on la despesa en habitatge és excessiva respecte dels ingressos | % de la població | `ilc_lvho07a` | Població total |
| `arope_T`, `arope_M`, `arope_F` | Persones en risc de pobresa o d'exclusió social: total, homes i dones | % de la població | `ilc_peps01n` | **Només des de 2015** |
| `gini` | Coeficient de Gini de la renda disponible equivalent | escala de 0 a 100 (més alt, més desigualtat) | `ilc_di12` | **Només des de 2014** |

### Context econòmic i educatiu

| Columna | Descripció | Unitat | Dataset | Observacions |
|---|---|---|---|---|
| `pib_hab` | PIB per habitant, a preus corrents | euros per habitant | `nama_10_pc` | No hi ha dades per al Regne Unit |
| `estudis_sup_T`, `estudis_sup_M`, `estudis_sup_F` | Població de 25 a 34 anys amb estudis superiors (ISCED 2011, nivells 5-8): total, homes i dones | % de la població d'aquesta edat | `edat_lfse_03` | |

### Convencions dels noms

- El sufix `_T`, `_M` i `_F` indica el desglossament per sexe: **T**otal, **M**ales (homes) i **F**emales (dones).
- El sufix `_CP00`, `_CP01` i `_CP04` correspon al codi de la categoria de la classificació COICOP.
- Els indicadors derivats (índexs rebasats a 2010 = 100, salari real, etc.) no són en aquest fitxer: es calculen a cada subconjunt.

### Limitacions conegudes

- **Grècia i Suïssa** no tenen `habitatge`; el **Regne Unit** només té dades fins al 2019 i no en té d'atur ni de PIB per habitant (és un efecte del Brexit en la publicació d'Eurostat).
- **Islàndia, Noruega, Suïssa i Turquia** publiquen amb un any de retard per a algunes variables.
- **Turquia** té una inflació molt superior a la resta, així que els seus índexs de preus no són comparables en una mateixa escala.
- Els indicadors de **pobresa** (`arope`, `gini`) s'han d'interpretar només des de 2014-2015.
- Les conclusions es refereixen als països inclosos, majoritàriament de la Unió Europea, no a "Europa" en general.
