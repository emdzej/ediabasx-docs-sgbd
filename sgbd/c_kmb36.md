# c_kmb36.prg

- Jobs: [13](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD fuer Kombi E36 DSII |
| ORIGIN | BMW TI-431 Michael Nau |
| REVISION | 0.04 |
| AUTHOR | BMW TI-431 Lothar Dennert, Michael Nau |
| COMMENT | N/A |
| PACKAGE | 1.03 |
| SPRACHE | @sprache@ |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Identifikation
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [SG_RESET](#job-sg-reset) - Beenden der Diagnose
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer
- [C_FG_LESEN_2](#job-c-fg-lesen-2) - Auslesen der Fahrgestellnummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Schreiben der 7-stelligen Fahrgestellnummer
- [C_FG_AUFTRAG_2](#job-c-fg-auftrag-2) - Schreiben der 7-stelligen Fahrgestellnummer
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten schreiben und verifizieren
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Wortadr. 34-3D auslesen

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
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-sg-reset"></a>
### SG_RESET

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FG_NR | string | Fahrgestellnummer |

<a id="job-c-fg-lesen-2"></a>
### C_FG_LESEN_2

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FG_NR | string | zweite Fahrgestellnummer aus Kombi nur CI 27 |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Schreiben der 7-stelligen Fahrgestellnummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (7-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-auftrag-2"></a>
### C_FG_AUFTRAG_2

Schreiben der 7-stelligen Fahrgestellnummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (7-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Anwenderinfofeld Wortadr. 34-3D auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VN | string | C3 Zifferncode fuer Versionsnummer |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (11 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 11 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x09 | OKAY |
| 0x0c | OKAY |
| 0x0d | OKAY |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0xFF | unbekannter Hersteller |
