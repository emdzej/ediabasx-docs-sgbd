# t_scod.prg

- Jobs: [2](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | externe Tabelle PCodeTexte |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 0.001 |
| AUTHOR | BMW TI-430 Drexel |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerät im Klartext |
| ORIGIN | string | Steuergeräte-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

## Tables

### Index

- [SAECODETEXTE](#table-saecodetexte) (4 × 3)

<a id="table-saecodetexte"></a>
### SAECODETEXTE

Dimensions: 4 rows × 3 columns

| SCODE | STRING | TEXT |
| --- | --- | --- |
| 0x0000 | -- |  |
| SCODE | STRING | TEXT |
| 0x0000 | -- |  |
| 0xXYXYXY | ?? | unbekannter SAE-Code |
