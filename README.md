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

## Dades noves: ocupacions, sectors i enquesta salarial

Aquests tres fitxers es descarreguen amb `descarrega_eurostat.py` (`python descarrega_eurostat.py ses_ocupacio assalariats_sector ocupats_isco2`) i es troben a [`data/`](data/). Tenen el mateix format que la resta de descàrregues de l'script: `geo` (codi de país), `pais` (nom), `TIME_PERIOD`, `OBS_VALUE` i `OBS_FLAG`, més les columnes de les dimensions. Inclouen la **UE-27** (`EU27_2020`) com a agregat de referència.

| Fitxer | Indicador | Dataset d'Eurostat | Anys | Files |
|---|---|---|---|---|
| `assalariats_sector.csv` | Assalariats per sector i sexe | `lfsa_eegan2` | 2010-2025 | 32.518 |
| `ocupats_isco2.csv` | Ocupats per ocupació i sexe | `lfsa_egai2d` | 2011-2025 | 72.166 |
| `ses_ocupacio.csv` | Sou per hora per ocupació, sector i sexe | `earn_ses_hourly` | 2010, 2014, 2018, 2022 | 35.003 |

### `assalariats_sector.csv`: assalariats per sector
- **Opcions triades:** unitat en milers de persones; edat de 15 a 64 anys; sexe total, homes i dones.
- **Sectors:** 23 valors de la classificació NACE Rev. 2 (A-U, més `TOTAL` i `NRP`, sense resposta). Cada lletra és una secció (p. ex. `F` = construcció, `J` = informació i comunicacions, `Q` = sanitat).
- **Font:** enquesta de població activa de la UE.
- **Observacions:** les xifres de països petits són poc fiables (marca `u`).

### `ocupats_isco2.csv`: ocupats per ocupació
- **Opcions triades:** unitat en milers de persones; edat de 15 a 64 anys; sexe total, homes i dones.
- **Ocupacions:** 55 codis de la classificació **ISCO-08**: 9 grans grups (`OC1`-`OC9`), les forces armades (`OC0`), els subgrups de dos dígits (p. ex. `OC71`, treballadors de la construcció) i dos codis especials (`TOTAL`, `NRP`).
- **Observacions:** hi ha ruptures de sèrie (marca `b`), de manera que un canvi gran entre dos anys pot venir d'un canvi de classificació.

### `ses_ocupacio.csv`: enquesta d'estructura salarial
- **Dataset:** *Structure of Earnings Survey* (`earn_ses_hourly`), que es fa **cada quatre anys**.
- **Opcions triades:** jornada total, totes les edats, sexe total/homes/dones; tres indicadors (`SAL` assalariats, `MEAN_E_EUR` sou brut per hora en euros i `MEAN_E_PPS` en PPS); onze ocupacions (total, `OC1`-`OC9` i `OC0`) i quatre agrupacions de sectors (`B-S_X_O`, `B-F`, `G-N`, `P-S`).
- **Cobertura:** empreses de 10 o més assalariats, seccions B a S sense l'administració pública (O).
- **Observacions:**
  - El **2022 només té el total per ocupació**, no el desglossament per sector (excepte Xipre).
  - Els agregats de la UE-27 del 2010 i del 2014 són inconsistents: cal calcular-los a partir dels països o usar-ne proporcions.
  - `SAL` és en **persones**, no en milers.
  - Els valors són bruts, a diferència del salari net de `salari.csv`.

### Taules mestres i fitxers de sortida

El quadern `crea_mestre_i_exploracio.ipynb` combina tots els fitxers de `data/` en **tres taules**, perquè no tenen les mateixes dimensions. Substitueix el panell que generava `cobertura.ipynb`.

| Fitxer | Una fila és... | Columnes |
|---|---|---|
| `data/panel_mestre.csv` | un país en un any | 71 (7 dimensions i 64 fets, 11 dels quals calculats) |
| `data/ocupacions_mestre.csv` | un país, un any i una ocupació | 14 |
| `data/ses_mestre.csv` | un país, un any, una ocupació i un sector | 19 |
| `data/diccionari_variables.csv` | una columna del panell | descripció, unitat, font i rol (dimensió o fet) |

Les cel·les buides **no són zeros**: vol dir que Eurostat no publica la dada. No s'omplen ni s'interpolen.

Les columnes `regio`, `zona_euro_2024`, `te_sal_min_legal` i `periode` són de **classificació pròpia**, no d'Eurostat. Les columnes calculades (índexs a base 2010 = 100, pressió de l'habitatge, salari real, % de dones, bretxes) es documenten al diccionari amb la font *Calculada*.

La carpeta `data_sortida/` conté fitxers CSV ja preparats per pujar a Flourish. Es poden regenerar executant la secció D del quadern.

