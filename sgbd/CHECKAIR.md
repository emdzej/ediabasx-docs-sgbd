# CHECKAIR.PRG

- Jobs: [3](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DUMMY |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.04 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | Dummy SGBD fuer Airbag-Ausloseeinheiten |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [NUMMERN_CHECK](#job-nummern-check) - Sachnummern Airbag-Ausloeseeinheit
- [INFO](#job-info) - Information SGBD

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
| AIRBAG_ART1 | string | Art-Zuordnung 1. Einheit (Fahrer/Beifahrer/Cabrio) |
| AIRBAG_ART2 | string | Art-Zuordnung 2. Einheit (Fahrer/Beifahrer/Cabrio) |

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

## Tables

### Index

- [E38](#table-e38) (20 × 3)
- [E39](#table-e39) (20 × 3)
- [E31](#table-e31) (16 × 3)
- [E34](#table-e34) (13 × 3)
- [E36](#table-e36) (17 × 3)

<a id="table-e38"></a>
### E38

Dimensions: 20 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1162099 | ECE | F |
| 1162892 | ECE | F |
| 1162893 | ECE | F |
| 1162894 | ECE | F |
| 1162895 | ECE | F |
| 1162896 | ECE | F |
| 1162897 | ECE | F |
| 1094446 | ECE | F |
| 1094447 | ECE | F |
| 1094448 | ECE | F |
| 1094449 | ECE | F |
| 1161830 | US | F |
| 1093311 | US | F |
| 1093310 | US | F |
| 1093246 | US | F |
| 1094256 | US | F |
| 1094258 | US | F |
| 1095510 | US | F |
| 1095512 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e39"></a>
### E39

Dimensions: 20 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1094255 | US | F |
| 1094257 | US | F |
| 1094444 | ECE | F |
| 1094446 | ECE | F |
| 1094447 | ECE | F |
| 1094448 | ECE | F |
| 1094449 | ECE | F |
| 1094823 | US | F |
| 1094824 | US | F |
| 1094454 | US | F |
| 1094455 | US | F |
| 1094843 | US | F |
| 1094844 | US | F |
| 1162099 | ECE | F |
| 1162892 | ECE | F |
| 1095509 | US | F |
| 1095510 | US | F |
| 1095511 | US | F |
| 1095512 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e31"></a>
### E31

Dimensions: 16 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1161008 | ECE | F |
| 1162743 | ECE | F |
| 1162744 | ECE | F |
| 2227855 | ECE | F |
| 1161755 | US | F |
| 1161756 | US | F |
| 1161757 | ECE_US | F |
| 1161758 | ECE_US | F |
| 1162090 | US | F |
| 2227755 | US | F |
| 1093308 | US | F |
| 2228016 | US | F |
| 1093307 | US | F |
| 1094444 | ECE | F |
| 1093306 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e34"></a>
### E34

Dimensions: 13 rows × 3 columns

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
| 1092539 | US | F |
| 1093306 | US | F |
| 2228016 | US | F |
| XXXXXXX | unbekannt | Y |

<a id="table-e36"></a>
### E36

Dimensions: 17 rows × 3 columns

| T_NR | TYP | ART |
| --- | --- | --- |
| 1161008 | ECE | F |
| 1162743 | ECE | F |
| 1162744 | ECE | F |
| 2227855 | ECE | F |
| 1161756 | US | F |
| 1161757 | US | F |
| 1161758 | US | F |
| 1162553 | US | F |
| 2227755 | US | F |
| 2227756 | US | F |
| 8146757 | LL | BF |
| 8146962 | RL | BF |
| 8162782 | LL | BF |
| 8162783 | LL_CABRIO | BF |
| 8182973 | RL | BF |
| 8182974 | RL_CABRIO | BF |
| XXXXXXX | unbekannt | Y |
