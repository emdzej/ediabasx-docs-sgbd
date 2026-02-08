# AIR_E36.PRG

- Jobs: [3](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | AIR_E36 |
| ORIGIN | BMW ET-421 Teepe |
| REVISION | 1.00 |
| AUTHOR | BMW ET-421 Teepe |
| COMMENT | Dummy-SGBD fuer Prufeung von Airbag-Ausloeseeinheiten bei E36 |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [NUMMERN_CHECK](#job-nummern-check) - Sachnummern Airbag-Ausloeseeinheit

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-nummern-check"></a>
### NUMMERN_CHECK

Sachnummern Airbag-Ausloeseeinheit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUREIHE | string | Variante des Fahrzeugs E34, E31, E38, E36 |
| VARIANTE | string | Variante des Fahrzeugs US, ECE |
| SACHNUMMER1 | string | Sachnummer der Ausloseeinheit 1 |
| SACHNUMMER2 | string | Sachnummer der Ausloseeinheit 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIRBAG_TYP1 | string | Typ-Zuordnung 1. Einheit |
| AIRBAG_TYP2 | string | Typ-Zuordnung 2. Einheit |
| AIRBAG_ART1 | string | Art-Zuordnung 1. Einheit (Fahrer/Beifahrer) |
| AIRBAG_ART2 | string | Art-Zuordnung 2. Einheit (Fahrer/Beifahrer) |
| MODELL1 | string | Variante des Fahrerairbags Cabrio, Coupe, Limousine, Compact, alle, nur bei E36 |
| MODELL2 | string | Variante des Beifahrerairbags Cabrio, Coupe, Limousine, Compact, alle, nur bei E36 |

## Tables

### Index

- [E38](#table-e38) (9 × 3)
- [E39](#table-e39) (3 × 3)
- [E31](#table-e31) (10 × 3)
- [E34](#table-e34) (10 × 3)
- [E36](#table-e36) (26 × 4)

<a id="table-e38"></a>
### E38

Dimensions: 9 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1162099 | ECE | F |
| 1162892 | ECE | F |
| 1162893 | ECE | F |
| 1162894 | ECE | F |
| 1162895 | ECE | F |
| 1162896 | ECE | F |
| 1162897 | ECE | F |
| 1161830 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e39"></a>
### E39

Dimensions: 3 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1162099 | ECE | F |
| 1162892 | ECE | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e31"></a>
### E31

Dimensions: 10 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1161008 | ECE | F |
| 1162743 | ECE | F |
| 1162744 | ECE | F |
| 2227855 | ECE | F |
| 1161755 | US | F |
| 1161756 | US | F |
| 1162090 | US | F |
| 1161757 | ECE_US | F |
| 1161758 | ECE_US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e34"></a>
### E34

Dimensions: 10 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1161008 | ECE | F |
| 1162743 | ECE | F |
| 1162744 | ECE | F |
| 2227855 | ECE | F |
| 1161756 | US | F |
| 1161757 | US | F |
| 1161758 | US | F |
| 1162090 | US | F |
| 2227755 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e36"></a>
### E36

Dimensions: 26 rows × 4 columns

| T_NR | TYP | ART | MODELL |
| --- | --- | --- | --- |
| 1092540 | ECE | F | F |
| 1093305 | ECE | F | F |
| 1092762 | ECE | F | F |
| 1093154 | US | F | B |
| 1093306 | US | F | B |
| 1161008 | ECE | F | 1 |
| 1162099 | ECE | F | F |
| 1162743 | ECE | F | 1 |
| 1162744 | ECE | F | 1 |
| 2227855 | ECE | F | F |
| 2228015 | ECE | F | F |
| 1162553 | US | F | 4 |
| 2227755 | US | F | 3 |
| 2228016 | US | F | 3 |
| 2227756 | US | F | 4 |
| 8146757 | LL | BF | 8 |
| 8146962 | RL | BF | 8 |
| 8162782 | LL | BF | 3 |
| 8182973 | RL | BF | 3 |
| 8209318 | LL | BF | 3 |
| 8209773 | RL | BF | 3 |
| 8162783 | LL | BF | 4 |
| 8182974 | RL | BF | 4 |
| 8209774 | LL | BF | 4 |
| 8209775 | RL | BF | 4 |
| XXXXXXX | unbekannt | Y | 0 |
