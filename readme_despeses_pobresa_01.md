## Dades noves: despeses de les llars i pobresa per edat

Es descarreguen amb `descarrega_eurostat.py` (`descarrega("despeses_cp")`, etc.) i es troben a [`data/`](data/). Tenen el mateix format que la resta de descàrregues: `geo`, `pais`, `TIME_PERIOD`, `OBS_VALUE`, `OBS_FLAG` i les columnes de les dimensions. Inclouen la UE-27 (`EU27_2020`) com a agregat.

| Fitxer | Indicador | Dataset d'Eurostat | Unitat |
|---|---|---|---|
| `despeses_cp.csv` | Despesa de consum de les llars per finalitat (COICOP) | `tec00134` | % del total de la despesa |
| `consum_habitant.csv` | Consum final de les llars per habitant | `nama_10_pc` (`P31_S14_S15`) | euros corrents per habitant |
| `arope_edat.csv` | Risc de pobresa o exclusió social (AROPE) per edat | `ilc_peps01n` | % de la població d'aquesta edat |

### `despeses_cp.csv`: en què gasten els diners les llars
- **Classificació COICOP** (*Classification of Individual Consumption by Purpose*): divideix la despesa en 12 o 13 finalitats (`CP01` aliments, `CP04` habitatge i subministraments, `CP07` transport, etc.). La llista és a `despeses_mestre.csv`.
- **Pes:** cada valor és el tant per cent de la despesa total que va a la categoria. Per a cada país i any, la suma és 100.
- **Observacions:** `CP04` inclou el **lloguer imputat** dels propietaris, per això pesa molt. Són mitjanes del país: les llars pobres gasten proporcionalment més en menjar i habitatge, i això no es veu aquí.

### `consum_habitant.csv`
- Multiplicat pel pes, dona la despesa en **euros per habitant** de cada categoria.
- Els valors són **nominals** (no descompten la inflació).

### `arope_edat.csv`
- Tres franges: menors de 18 anys (`Y_LT18`), de 18 a 64 (`Y18-64`) i 65 o més (`Y_GE65`). Només des del 2015.

### Taules mestres noves

El quadern `exploracio_2_despeses_pobresa.ipynb` continua el quadern de les taules mestres i en crea de noves. **No substitueix** `panel_mestre.csv`: el completa.

| Fitxer | Una fila és... | Contingut |
|---|---|---|
| `data/panel_ampliat.csv` | un país en un any | El panell original més les despeses (`desp_CP01`…, `desp_basica_pct`), el consum per habitant (`consum_hab`) i el risc de pobresa per edats (`arope_menors18`, `arope_18_64`, `arope_65mes`) |
| `data/despeses_mestre.csv` | un país, un any i una categoria de despesa | `pes_pct`, `pes_dif_2010_pp` (canvi respecte del 2010, en punts percentuals) i `despesa_hab_eur` (despesa en euros per habitant) |
| `data/diccionari_panel_ampliat.csv` | una columna del panell ampliat | descripció, unitat, font i rol |

| Columna nova | Significat | Unitat |
|---|---|---|
| `desp_CP01` … `desp_CP13` | Pes de cada categoria de despesa (`CP13` només a la classificació nova) | % de la despesa |
| `desp_basica_pct` | Despesa bàsica: aliments (`CP01`) + habitatge i subministraments (`CP04`) | % de la despesa |
| `consum_hab` | Consum final de les llars per habitant | euros per habitant |
| `arope_menors18` | AROPE, menors de 18 anys | % |
| `arope_18_64` | AROPE, de 18 a 64 anys | % |
| `arope_65mes` | AROPE, 65 anys o més | % |

### Fitxers de sortida per a Flourish
A `data_sortida/`:
- **`flourish_cursa_isco1.csv`** i **`flourish_cursa_isco1_idx.csv`**: cursa dels grans grups d'ocupació (en milers i en índex 2011 = 100).
- **`flourish_cursa_isco2_OC0.csv` … `OC9.csv`**: una cursa per cada gran grup, amb els seus subgrups.
- **`flourish_despeses_*.csv`**: cursa, barres apilades, scatter i mapa de les despeses.
- **`flourish_pobresa_*.csv`**: scatter, mapa, pobresa per edats i per sexe.

### Limitacions conegudes
- **Ruptures de sèrie** a les ocupacions de la UE-27 el 2011 i el 2021 (a tots els grans grups): els canvis d'aquests anys poden ser d'enquesta i no reals.
- Les despeses són **mitjanes nacionals**, no de les llars pobres.
- Si Eurostat ha canviat la classificació COICOP, les categories de l'any nou poden no ser comparables amb les antigues.

### Glossari: COICOP
Classificació internacional que ordena la despesa de les llars segons **per a què** es gasta. No indica on es compra, sinó la finalitat: `CP01` aliments i begudes sense alcohol, `CP04` habitatge, aigua, electricitat i gas, `CP06` salut, `CP07` transport, `CP11` restaurants i allotjament… El mateix codi `CP` (amb `CP00` el total) s'usa a l'índex de preus (`ipc_CP01`), de manera que **es pot comparar el que puja el preu d'una categoria amb el pes que té a la despesa**.

### Ampliació: salari mínim i noves visualitzacions

**`salari_minim_relatiu.csv`** (`earn_mw_avgr2`): salari mínim mensual com a % del salari brut mitjà mensual. Només països amb salari mínim legal. Té dues dimensions que es filtren al quadern: el sector (`nace_r2`) i si és sobre la mitjana o la mediana (`indic_se`).

Columnes noves al `panel_ampliat.csv`:

| Columna | Significat | Unitat |
|---|---|---|
| `min_sobre_mitjana_pct` | Salari mínim mensual com a % del salari brut mitjà mensual (indicador oficial) | % |
| `salari_sobre_min` | Salari net anual de la persona tipus dividit pel salari mínim brut anual (12 mensualitats). **Aproximació**: compara net amb brut | ràtio (1 = igual) |

Fitxers nous de sortida a `data_sortida/`:
- `flourish_heatmap_isco.csv`, `flourish_heatmap_coicop.csv`: mapes de calor països × categoria.
- `flourish_mapa_isco.csv`, `flourish_mapa_coicop.csv` (i versions `_ample`): mapes amb filtre per codi i temps.
- `flourish_bretxa_ocupacio.csv`, `flourish_bretxa_sector.csv`: dumbbell de la bretxa salarial amb filtre i temps.
- `flourish_salari_minim_linies.csv`, `flourish_salari_minim_dumbbell.csv`: salari mínim.
- Els dumbbell de pobresa (`flourish_pobresa_genere.csv`, `flourish_pobresa_laboral_genere.csv`, `flourish_pobresa_edat.csv`) ara inclouen la columna `any`, per fer-hi servir el slider de temps.
