# C_LWR.prg

- Jobs: [6](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Codierbeschreibungsdatei Leuchtweitenregulierung E38, E39, E46, E53, R50 |
| ORIGIN | BMW TP-421 Thomas Hirsch |
| REVISION | 1.02 |
| AUTHOR | BMW TP-421 Thomas Hirsch |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer LWR
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

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

Ident-Daten fuer LWR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |

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

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
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

| LIEF_NR | LIEF_TEXT |
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
| 0xXY | unbekannter Hersteller |
