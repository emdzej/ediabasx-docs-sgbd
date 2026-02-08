# C_KMB34.prg

- Jobs: [11](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD fuer KMBL E34 |
| ORIGIN | BMW TI-431 Michael Nau |
| REVISION | 1.00 |
| AUTHOR | Softing AEC Daniel Frey |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Identifikation
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten schreiben und verifizieren
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Write and verify the Central code
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Read the ZCS record
- [C_CHECKSUM1](#job-c-checksum1) - Berechnung und Speicherung der Checksumme fuer Codierindex 25
- [C_CHECKSUM2](#job-c-checksum2) - Berechnung und Speicherung der Checksumme fuer Codierindex 27
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - letzten 7 Stellen der Fahrgestellnummer schreiben
- [C_FG_LESEN](#job-c-fg-lesen) - letzten 7 Stellen der Fahrgestellnummer lesen

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Identifikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_COD_INDEX | string | Codierindex |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-zcs-auftrag"></a>
### C_ZCS_AUFTRAG

Write and verify the Central code

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Read the ZCS record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos) Version information |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-checksum1"></a>
### C_CHECKSUM1

Berechnung und Speicherung der Checksumme fuer Codierindex 25

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-checksum2"></a>
### C_CHECKSUM2

Berechnung und Speicherung der Checksumme fuer Codierindex 27

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

letzten 7 Stellen der Fahrgestellnummer schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | 7 oder 17 Stellen angeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

letzten 7 Stellen der Fahrgestellnummer lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string |  |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (2 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 2 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |
