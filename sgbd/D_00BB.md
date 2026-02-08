# D_00BB.grp

- Jobs: [2](#jobs)
- Tables: [1](#tables)

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Einstellen der Kommunikationsparameter
- [IDENTIFIKATION](#job-identifikation) - Ermittlung der SG Variante Zur Gruppe gehoerende Varianten: NAV_JAP  : DS2 NAV_JAP2 : BMW_FAST

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Einstellen der Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-identifikation"></a>
### IDENTIFIKATION

Ermittlung der SG Variante Zur Gruppe gehoerende Varianten: NAV_JAP  : DS2 NAV_JAP2 : BMW_FAST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE | string | Der zurueckgelieferte Name entspricht dem Namen der Datei fuer die Varianten-SGBD |

## Tables

### Index

- [DI_TABELLE](#table-di-tabelle) (4 × 2)

<a id="table-di-tabelle"></a>
### DI_TABELLE

Dimensions: 4 rows × 2 columns

| DI | VARIANTE |
| --- | --- |
| 00 | NAV_JAP |
| 01 | NAV_JAP |
| 02 | JNAV_CE |
| 03 | JNAV_CE2 |
