# C_EKM.prg

- Jobs: [20](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD fuer EKM E31 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten schreiben und verifizieren
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Write and verify the Central code
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Read the ZCS record
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [C_CHECKSUM_VERIFY](#job-c-checksum-verify) - Ueberpruefung der Checksumme
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - letzten 7 Stellen der Fahrgestellnummer schreiben
- [C_FG_LESEN](#job-c-fg-lesen) - letzten 7 Stellen der Fahrgestellnummer lesen
- [C_FG_AUFTRAG2](#job-c-fg-auftrag2) - letzten 7 Stellen der Fahrgestellnummer schreiben
- [C_FG_LESEN2](#job-c-fg-lesen2) - letzten 7 Stellen der Fahrgestellnummer lesen
- [C_GEBRAUCHTBITS_LESEN](#job-c-gebrauchtbits-lesen) - Gebrauchtbits auslesen
- [C_GEBRAUCHT_SETZEN](#job-c-gebraucht-setzen) - Gebrauchtbits setzen FC 11xxxxxx FF xx00xxxx
- [C_GEBRAUCHT_SETZEN2](#job-c-gebraucht-setzen2) - Gebrauchtbits setzen FC 0xCF   FF 0xCF
- [C_KOMBI_GEBRAUCHTBITS_LESEN](#job-c-kombi-gebrauchtbits-lesen) - Gebrauchtbits auslesen
- [C_KOMBI_UNGEBRAUCHT_SETZEN](#job-c-kombi-ungebraucht-setzen) - Gebrauchtbits setzen FC xx00xxxx FF 11xxxxxx
- [C_KOMBI_GEBRAUCHT_SETZEN](#job-c-kombi-gebraucht-setzen) - Gebrauchtbits setzen FC xx11xxxx FF 00xxxxxx

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
| ID_GEN_NR | string | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_COD_INDEX | string | Codierindex |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_... |

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
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-checksum"></a>
### C_CHECKSUM

Berechnung und Speicherung der Checksumme

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-checksum-verify"></a>
### C_CHECKSUM_VERIFY

Ueberpruefung der Checksumme

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_VERIFY |

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

<a id="job-c-fg-auftrag2"></a>
### C_FG_AUFTRAG2

letzten 7 Stellen der Fahrgestellnummer schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | 7 oder 17 Stellen angeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen2"></a>
### C_FG_LESEN2

letzten 7 Stellen der Fahrgestellnummer lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string |  |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-gebrauchtbits-lesen"></a>
### C_GEBRAUCHTBITS_LESEN

Gebrauchtbits auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GEBRAUCHT | int |  |
| BIT_FC7 | int |  |
| BIT_FC6 | int |  |
| BIT_FF5 | int |  |
| BIT_FF4 | int |  |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-gebraucht-setzen"></a>
### C_GEBRAUCHT_SETZEN

Gebrauchtbits setzen FC 11xxxxxx FF xx00xxxx

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-gebraucht-setzen2"></a>
### C_GEBRAUCHT_SETZEN2

Gebrauchtbits setzen FC 0xCF   FF 0xCF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-kombi-gebrauchtbits-lesen"></a>
### C_KOMBI_GEBRAUCHTBITS_LESEN

Gebrauchtbits auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GEBRAUCHT | int |  |
| BIT_FC5 | int |  |
| BIT_FC4 | int |  |
| BIT_FF7 | int |  |
| BIT_FF6 | int |  |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-kombi-ungebraucht-setzen"></a>
### C_KOMBI_UNGEBRAUCHT_SETZEN

Gebrauchtbits setzen FC xx00xxxx FF 11xxxxxx

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-kombi-gebraucht-setzen"></a>
### C_KOMBI_GEBRAUCHT_SETZEN

Gebrauchtbits setzen FC xx11xxxx FF 00xxxxxx

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
