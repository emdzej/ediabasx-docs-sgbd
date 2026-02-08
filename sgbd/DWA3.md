# DWA3.prg

- Jobs: [3](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Diebstahlwarnanlage DWA3 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.09 |
| AUTHOR | BMW TP-422 Teepe, BMW TP-421 Drexel |
| COMMENT | diese Version ist erforderlich fuer EDIABAS 4.0 |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job

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

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardware-Nummer |
| ID_VERSION | string | High/low-Version |
| ID_SW_NR | int | Software-Nummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int |  |
| ID_DATUM_JAHR | int |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (12 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 12 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | OKAY |
| 0x02 | OKAY |
| 0x05 | OKAY |
| 0x07 | OKAY |
| 0x0C | OKAY |
| 0x0D | OKAY |
| 0x0C | ERROR_ECU_FUNCTION |
| 0xAA | ERROR_ECU_REJECTED |
| 0x0A | ERROR_ECU_NACK |
| xxxx | OKAY |
| 0xFF | ERROR_ECU_UNKNOWN_STATUSBYTE |
