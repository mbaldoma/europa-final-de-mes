# europa-final-de-mes
"Europa a final de mes" és un projecte de ...
## Dades

Totes les dades provenen d'**Eurostat** (Data Browser, <https://ec.europa.eu/eurostat/databrowser/>) i s'han descarregat en format **SDMX-CSV 1.0**, sense comprimir. Es troben a la carpeta [`data/`](data/). Els enllaços de l'API de cada descàrrega estan guardats a [`data/fonts.txt`](data/fonts.txt).

Data de descàrrega: _(escriu-hi la data)_

| Fitxer | Indicador | Dataset d'Eurostat | Anys | Països | Files |
|---|---|---|---|---|---|
| `salari.csv` | Salari net anual | `earn_nt_net` | 2000-2025 | 33 | 784 |
| `habitatge.csv` | Preu de l'habitatge | `prc_hpi_a` | 2005-2025 | 31 | 639 |
| `menjar.csv` | Preu dels aliments | `prc_hicp_aind` | 1996-2025 | 38 | 1.040 |
| `vacants.csv` | Vacants a la construcció | `jvs_a_rate_r2` | 2008-2025 | 34 | 533 |

Els quatre fitxers comparteixen les columnes `geo` (país), `TIME_PERIOD` (any), `OBS_VALUE` (valor), `OBS_FLAG` (marca d'Eurostat) i `CONF_STATUS` (confidencialitat), de manera que es poden creuar per país i any.

### `salari.csv`: salari net anual

- **Dataset:** *Annual net earnings* (`earn_nt_net`).
- **Opcions triades:**
  - Freqüència: anual.
  - Moneda: euro.
  - Tipus de salari: net (després d'impostos i cotitzacions).
  - Tipus de llar: persona soltera sense fills amb un salari igual al 100 % de la mitjana.
- **Unitat:** euros per any, en valors nominals (no ajustats per la inflació).
- **Què representa:** el que s'enduu a casa, en un any, un treballador amb el sou mitjà del seu país.
- **Observacions:** la columna `OBS_FLAG` marca 28 files amb la lletra `b` (ruptura de sèrie).

### `habitatge.csv`: preu de l'habitatge

- **Dataset:** *House price index (2015 = 100) - annual data* (`prc_hpi_a`).
- **Opcions triades:**
  - Tipus de compra: total (habitatge nou i existent).
  - Unitat: índex de la mitjana anual, amb base 2015 = 100.
- **Unitat:** índex (2015 = 100). No són euros: un valor de 130 vol dir que els preus són un 30 % més alts que el 2015.
- **Observacions:** hi ha 38 valors buits, amb `CONF_STATUS = N` (dada no publicada o confidencial). Per exemple, Àustria no té dades abans de 2010.

### `menjar.csv`: preu dels aliments

- **Dataset:** *HICP - annual data (average index and rate of change)* (`prc_hicp_aind`). L'HICP és l'índex de preus de consum harmonitzat, que Eurostat fa servir per comparar la inflació entre països.
- **Opcions triades:**
  - Categoria (COICOP): *Food and non-alcoholic beverages* (aliments i begudes no alcohòliques).
  - Unitat: índex de la mitjana anual (no la taxa de canvi).
- **Unitat:** índex amb base 2015 = 100 (tots els països valen 100 el 2015).
- **Observacions:** inclou països candidats (Albània, Sèrbia, Kosovo, Montenegro, Macedònia del Nord) i les sèries comencen en anys diferents. Algunes files porten la marca `d` (definició diferent de l'estàndard).

### `vacants.csv`: vacants a la construcció

- **Dataset:** *Job vacancy rate by NACE Rev. 2 activity, annual data* (`jvs_a_rate_r2`).
- **Opcions triades:**
  - Activitat econòmica: *Construction* (secció F de NACE Rev. 2).
  - Mida d'empresa: total.
  - Unitat: mitjana anual.
- **Unitat:** percentatge. La taxa de vacants és el nombre de llocs de treball vacants dividit per la suma de llocs ocupats i vacants. Una taxa alta indica que les empreses no troben personal.
- **Observacions:** les sèries comencen en anys diferents segons el país (França el 2012, Alemanya el 2011, Itàlia el 2016, Malta el 2017, Islàndia el 2019, Turquia el 2021) i el Regne Unit s'acaba el 2019. Marques presents: `p` (provisional), `u` (poc fiable) i `b` (ruptura de sèrie).

### Marques d'Eurostat (`OBS_FLAG`)

| Marca | Significat |
|---|---|
| `b` | Ruptura de sèrie |
| `p` | Provisional |
| `e` | Estimat |
| `d` | Definició diferent de l'estàndard |
| `u` | Poc fiable |

### Tractament previst

1. Mantenir només les columnes `geo`, `TIME_PERIOD` i `OBS_VALUE`.
2. Treure els agregats (com *European Union - 27 countries*) i els països sense dades als altres fitxers.
3. Restringir el període a partir de 2010.
4. Fusionar els quatre fitxers per país i any.
5. Rebasar salari, habitatge i menjar a **2010 = 100**, per poder comparar-ne l'evolució. Les vacants es deixen en percentatge.

Els càlculs es fan al quadern de Jupyter del repositori.

### Fonts

Eurostat. Base de dades en línia, datasets `earn_nt_net`, `prc_hpi_a`, `prc_hicp_aind` i `jvs_a_rate_r2`.
