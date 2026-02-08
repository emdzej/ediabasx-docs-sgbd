# d_most.grp

- Jobs: [2](#jobs)
- Tables: [1](#tables)

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENTIFIKATION](#job-identifikation) - Auslesen des Fahrzeugauftrags aus dem CAS Ermitteln der Baureihe 

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-identifikation"></a>
### IDENTIFIKATION

Auslesen des Fahrzeugauftrags aus dem CAS Ermitteln der Baureihe 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE | string | Name der MOST SGBD (in Abhängigkeit von der Baureihe) |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 5 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x10 | D-CAN |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |
