# IRIS.prg

- Jobs: [10](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integriertes Radio Informations-System IRIS E39 |
| ORIGIN | BMW TP-421 Spoljarec |
| REVISION | 1.04 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer IRIS E39
- [IDENT](#job-ident) - Ident-Daten fuer IRIS
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen)
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Default pruefstempel_setzen job
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen)
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

Init-Job fuer IRIS E39

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer IRIS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ANZ | int | Anzahl der Gesamtfehler |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart (entweder 0 oder 32) |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_HEX_CODE | binary | Hex-Werte des Einzelfehlers |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE_1 | int | Byte 1 des Pruefstempels |
| BYTE_2 | int | Byte 2 des Pruefstempels |
| BYTE_3 | int | Byte 3 des Pruefstempels |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Default pruefstempel_setzen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0x00 bis 0xFF |
| BYTE2 | int | 0x00 bis 0xFF |
| BYTE3 | int | 0x00 bis 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _ANTWORT | binary |  |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary |  |
| _ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _ANTWORT | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [FORTTEXTE](#table-forttexte) (3 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 3 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Keine gueltige Statusrueckmeldung IKE |
| 0x02 | Keine gueltige Statusrueckmeldung AUDIO |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x01 | Fehler momentan vorhanden |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |
