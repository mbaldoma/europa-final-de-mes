## Taules mestres: columnes, significat i unitats

El quadern `crea_mestre_i_exploracio.ipynb` genera tres taules mestres a [`data/`](data/). Hi ha una per cada nivell de detall de les dades. Les cel·les buides vol dir que Eurostat no publica la dada; **no són zeros** i no s'han omplert ni interpolat. Els sufixos `_T`, `_M` i `_F` indiquen sexe: **T**otal, **M**ales (homes) i **F**emales (dones).

| Taula | Una fila és... | Files | Columnes |
|---|---|---|---|
| [`panel_mestre.csv`](data/panel_mestre.csv) | un país en un any | 480 | 71 |
| [`ocupacions_mestre.csv`](data/ocupacions_mestre.csv) | un país, un any i una ocupació | _(segons les teves dades)_ | 14 |
| [`ses_mestre.csv`](data/ses_mestre.csv) | un país, un any, una ocupació i un sector | _(segons les teves dades)_ | 19 |

Els fets i les dimensions de `panel_mestre.csv` també són a [`diccionari_variables.csv`](data/diccionari_variables.csv).

---

### `panel_mestre.csv`: un país en un any (2010-2024)


#### Identificació i dimensions

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `pais` | Nom del país, en anglès tal com el dona Eurostat | text | Eurostat |
| `geo` | Codi de país d'Eurostat (EL = Grècia, UK = Regne Unit) | text, 2 lletres | Eurostat |
| `any` | Any de la dada | any | Eurostat |
| `regio` | Grup regional: Nord, Oest, Est, Sud o Altres (classificació pròpia, basada en l'esquema geogràfic de l'ONU) | categòrica | Pròpia |
| `zona_euro_2024` | El país formava part de la zona euro el 2024 | sí / no | Pròpia |
| `te_sal_min_legal` | El país té salari mínim legal nacional en algun any de les dades | sí / no | Pròpia (a partir d'earn_mw_cur) |
| `periode` | Etapa econòmica de l'any: crisi del deute (2010-2013), recuperació (2014-2019), pandèmia i inflació (2020-2024) | categòrica | Pròpia |

#### Salaris i preus

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `salari` | Salari net anual d'una persona soltera sense fills amb un sou igual a la mitjana del país | euros per any (nominals) | Eurostat earn_nt_net |
| `sal_min` | Salari mínim mensual brut (mitjana dels dos semestres de l'any) | euros per mes | Eurostat earn_mw_cur |
| `habitatge` | Índex de preus de l'habitatge (compra, nou i de segona mà) | índex, 2015 = 100 | Eurostat prc_hpi_a |
| `ipc_CP00` | Índex de preus de consum harmonitzat (HICP): tots els béns i serveis | índex, 2015 = 100 | Eurostat prc_hicp_aind |
| `ipc_CP01` | HICP: aliments i begudes no alcohòliques | índex, 2015 = 100 | Eurostat prc_hicp_aind |
| `ipc_CP04` | HICP: habitatge, aigua, electricitat, gas i altres combustibles | índex, 2015 = 100 | Eurostat prc_hicp_aind |

#### Mercat de treball

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `vacants` | Taxa de vacants a la construcció | % dels llocs de treball | Eurostat jvs_a_rate_r2 |
| `bretxa_B-N` | Bretxa salarial de gènere sense ajustar, economia empresarial | % del sou per hora dels homes | Eurostat earn_gr_gpgr2 |
| `bretxa_F` | Bretxa salarial de gènere sense ajustar, construcció | % del sou per hora dels homes | Eurostat earn_gr_gpgr2 |
| `atur_T` | Taxa d'atur de 15 a 74 anys, total | % de la població activa | Eurostat une_rt_a |
| `atur_M` | Taxa d'atur de 15 a 74 anys, homes | % de la població activa | Eurostat une_rt_a |
| `atur_F` | Taxa d'atur de 15 a 74 anys, dones | % de la població activa | Eurostat une_rt_a |
| `ocupacio_T` | Taxa d'ocupació de 15 a 64 anys, total | % de la població de 15 a 64 | Eurostat lfsa_ergan |
| `ocupacio_M` | Taxa d'ocupació de 15 a 64 anys, homes | % de la població de 15 a 64 | Eurostat lfsa_ergan |
| `ocupacio_F` | Taxa d'ocupació de 15 a 64 anys, dones | % de la població de 15 a 64 | Eurostat lfsa_ergan |

#### Pobresa i desigualtat

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `pobresa_lab_T` | Risc de pobresa de les persones ocupades de 18 a 64 anys, total | % dels ocupats | Eurostat ilc_iw01 |
| `pobresa_lab_M` | Risc de pobresa de les persones ocupades de 18 a 64 anys, homes | % dels ocupats | Eurostat ilc_iw01 |
| `pobresa_lab_F` | Risc de pobresa de les persones ocupades de 18 a 64 anys, dones | % dels ocupats | Eurostat ilc_iw01 |
| `sobrecarrega` | Població que viu en llars on el cost de l'habitatge supera el 40 % de la renda disponible | % de la població | Eurostat ilc_lvho07a |
| `arope_T` | Risc de pobresa o d'exclusió social (AROPE), total | % de la població | Eurostat ilc_peps01n |
| `arope_M` | Risc de pobresa o d'exclusió social (AROPE), homes | % de la població | Eurostat ilc_peps01n |
| `arope_F` | Risc de pobresa o d'exclusió social (AROPE), dones | % de la població | Eurostat ilc_peps01n |
| `gini` | Coeficient de Gini de la renda disponible equivalent | escala de 0 a 100 | Eurostat ilc_di12 |

#### Context econòmic i educatiu

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `pib_hab` | PIB per habitant a preus corrents | euros per habitant | Eurostat nama_10_pc |
| `estudis_sup_T` | Població de 25 a 34 anys amb estudis superiors, total | % de la població de 25 a 34 | Eurostat edat_lfse_03 |
| `estudis_sup_M` | Població de 25 a 34 anys amb estudis superiors, homes | % de la població de 25 a 34 | Eurostat edat_lfse_03 |
| `estudis_sup_F` | Població de 25 a 34 anys amb estudis superiors, dones | % de la població de 25 a 34 | Eurostat edat_lfse_03 |

#### Assalariats per sector

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `assal_total` | Assalariats de 15 a 64 anys, tots els sectors | milers de persones | Eurostat lfsa_eegan2 |
| `assal_industria` | Assalariats a la indústria manufacturera (NACE C) | milers de persones | Eurostat lfsa_eegan2 |
| `assal_construccio` | Assalariats a la construcció (NACE F) | milers de persones | Eurostat lfsa_eegan2 |
| `assal_tic` | Assalariats a informació i comunicacions (NACE J) | milers de persones | Eurostat lfsa_eegan2 |
| `assal_sanitat` | Assalariats a sanitat i serveis socials (NACE Q) | milers de persones | Eurostat lfsa_eegan2 |
| `dones_total_pct` | Dones sobre el total d'assalariats, tots els sectors | % (calculada) | Eurostat lfsa_eegan2 |
| `dones_industria_pct` | Dones sobre el total d'assalariats a la indústria manufacturera | % (calculada) | Eurostat lfsa_eegan2 |
| `dones_construccio_pct` | Dones sobre el total d'assalariats a la construcció | % (calculada) | Eurostat lfsa_eegan2 |
| `dones_tic_pct` | Dones sobre el total d'assalariats a informació i comunicacions | % (calculada) | Eurostat lfsa_eegan2 |
| `dones_sanitat_pct` | Dones sobre el total d'assalariats a sanitat i serveis socials | % (calculada) | Eurostat lfsa_eegan2 |

#### Ocupats per ocupació

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `ocup_total` | Ocupats de 15 a 64 anys, totes les ocupacions | milers de persones | Eurostat lfsa_egai2d |
| `ocup_directius` | Ocupats com a directius i gerents (ISCO 1) | milers de persones | Eurostat lfsa_egai2d |
| `ocup_oficis` | Ocupats com a artesans i treballadors d'oficis (ISCO 7) | milers de persones | Eurostat lfsa_egai2d |
| `ocup_paletes` | Ocupats en oficis de la construcció, excepte electricistes: paletes i similars (ISCO 71) | milers de persones | Eurostat lfsa_egai2d |
| `ocup_electricistes` | Ocupats com a electricistes i electrònics (ISCO 74) | milers de persones | Eurostat lfsa_egai2d |
| `ocup_proftic` | Ocupats com a professionals de les TIC (ISCO 25) | milers de persones | Eurostat lfsa_egai2d |
| `dones_directius_pct` | Dones sobre el total d'ocupats com a directius i gerents | % (calculada) | Eurostat lfsa_egai2d |
| `dones_oficis_pct` | Dones sobre el total d'ocupats en oficis | % (calculada) | Eurostat lfsa_egai2d |
| `dones_paletes_pct` | Dones sobre el total d'ocupats en oficis de la construcció (ISCO 71) | % (calculada) | Eurostat lfsa_egai2d |
| `dones_electricistes_pct` | Dones sobre el total d'electricistes i electrònics | % (calculada) | Eurostat lfsa_egai2d |
| `dones_proftic_pct` | Dones sobre el total de professionals de les TIC | % (calculada) | Eurostat lfsa_egai2d |

#### Sou per hora (enquesta d'estructura salarial)

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `sou_hora_T` | Sou brut mitjà per hora, tots els assalariats | euros per hora | Eurostat earn_ses_hourly |
| `sou_hora_M` | Sou brut mitjà per hora, homes | euros per hora | Eurostat earn_ses_hourly |
| `sou_hora_F` | Sou brut mitjà per hora, dones | euros per hora | Eurostat earn_ses_hourly |
| `sou_hora_pps_T` | Sou brut mitjà per hora, tots els assalariats, ajustat pel nivell de preus del país | PPS per hora | Eurostat earn_ses_hourly |
| `bretxa_hora_pct` | Bretxa salarial calculada a partir del sou per hora: 1 - sou dones / sou homes | % (calculada) | Eurostat earn_ses_hourly |

#### Indicadors calculats

| Columna | Significat | Unitat | Font |
|---|---|---|---|
| `salari_idx2010` | Salari net, rebasat: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `habitatge_idx2010` | Preus de l'habitatge, rebasats: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `ipc_CP00_idx2010` | Preus de consum en general, rebasats: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `ipc_CP01_idx2010` | Preus dels aliments, rebasats: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `ipc_CP04_idx2010` | Preus d'habitatge i subministraments, rebasats: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `pib_hab_idx2010` | PIB per habitant, rebasat: 2010 = 100 | índex, 2010 = 100 | Calculada |
| `pressio_habitatge` | Pressió de l'habitatge: preu de l'habitatge dividit pel salari (ambdós a base 2010 = 100) | índex, 2010 = 100 | Calculada |
| `pressio_menjar` | Pressió dels aliments: preu dels aliments dividit pel salari (ambdós a base 2010 = 100) | índex, 2010 = 100 | Calculada |
| `salari_real_idx2010` | Salari real: salari net dividit pels preus de consum generals (ambdós a base 2010 = 100) | índex, 2010 = 100 | Calculada |
| `bretxa_atur_pp` | Diferència d'atur entre dones i homes (atur dones - atur homes) | punts percentuals | Calculada |
| `bretxa_ocupacio_pp` | Diferència d'ocupació entre homes i dones (ocupació homes - ocupació dones) | punts percentuals | Calculada |

Notes sobre el panell:
- `habitatge`, `ipc_*` són índexs amb 2015 = 100: serveixen per comparar **evolucions**, no nivells.
- Els indicadors calculats es basen en els valors de 2010 de cada país; si un país no té dada el 2010, queden buits.
- `regio`, `zona_euro_2024`, `te_sal_min_legal` i `periode` són de classificació pròpia, no d'Eurostat.
- Grècia i Suïssa no tenen `habitatge`, i el Regne Unit no té atur ni PIB per habitant.

---

### `ocupacions_mestre.csv`: un país, un any i una ocupació (2011-2025)

Parteix de `ocupats_isco2.csv` (classificació ISCO-08). Inclou la UE-27 com a agregat.

| Columna | Significat | Unitat |
|---|---|---|
| `pais` | Nom del país o agregat (en anglès) | text |
| `geo` | Codi d'Eurostat (`EU27_2020` per a la UE-27) | text |
| `tipus` | `pais` o `agregat` | text |
| `any` | Any de la dada | any |
| `isco08` | Codi de l'ocupació (p. ex. `OC71`) o `TOTAL`/`NRP` (sense resposta) | text |
| `nivell` | 0 = total, 1 = gran grup (`OC7`), 2 = subgrup (`OC71`) | 0, 1 o 2 |
| `grup` | Gran grup del qual penja l'ocupació (`OC71` → `OC7`) | text |
| `ocupacio` | Nom de l'ocupació en català | text |
| `ocupats_T` | Ocupats de 15 a 64 anys, total | milers de persones |
| `ocupats_M` | Ocupats de 15 a 64 anys, homes | milers de persones |
| `ocupats_F` | Ocupats de 15 a 64 anys, dones | milers de persones |
| `dones_pct` | Dones sobre homes + dones (calculada) | % |
| `pes_pct` | Pes de l'ocupació sobre el total d'ocupats del país i any (calculada) | % |
| `ocupats_idx2011` | Ocupats respecte del 2011 del mateix país i ocupació (calculada) | índex, 2011 = 100 |

Limitació: hi ha ruptures de sèrie (marca `b` als CSV originals), de manera que un canvi gran entre dos anys pot venir d'un canvi de classificació.

---

### `ses_mestre.csv`: un país, un any, una ocupació i un sector (2010, 2014, 2018 i 2022)

Parteix de `ses_ocupacio.csv` (enquesta d'estructura salarial, cada quatre anys, empreses de 10 o més assalariats, sense administració pública). Inclou la UE-27.

| Columna | Significat | Unitat |
|---|---|---|
| `pais` | Nom del país o agregat (en anglès) | text |
| `geo` | Codi d'Eurostat (`EU27_2020` per a la UE-27) | text |
| `tipus` | `pais` o `agregat` | text |
| `any` | Any de l'enquesta | 2010, 2014, 2018 o 2022 |
| `isco08` | Codi de l'ocupació (`TOTAL`, `OC1`-`OC9`, `OC0`) | text |
| `ocupacio` | Nom de l'ocupació en català | text |
| `nace_r2` | Codi del sector: `B-S_X_O` (tota l'economia sense administració pública), `B-F`, `G-N` o `P-S` | text |
| `sector` | Nom del sector en català | text |
| `sou_hora_eur_T`, `_M`, `_F` | Sou brut mitjà per hora: total, homes, dones | euros per hora |
| `sou_hora_pps_T`, `_M`, `_F` | El mateix, ajustat pel nivell de preus del país | PPS per hora |
| `assalariats_T`, `_M`, `_F` | Nombre d'assalariats: total, homes, dones | **persones** (no milers) |
| `dones_pct` | Dones sobre homes + dones (calculada) | % |
| `bretxa_pct` | 1 - sou de les dones / sou dels homes (calculada) | % |

Limitacions: el 2022 només té el total per ocupació (no el desglossament per sector, excepte Xipre). Els agregats de la UE-27 del 2010 i 2014 són inconsistents, així que convé calcular-los a partir dels països.
