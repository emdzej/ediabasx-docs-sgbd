# C_SEC.prg

- Jobs: [12](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sicherheits-Steuergeraet E38/3 |
| ORIGIN | BMW TI-433 Gerd Huber |
| REVISION | 0.02 |
| AUTHOR | BMW TI-433 Gerd Huber, remes B. Bloechl |
| COMMENT | Prototyp |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information bzgl. SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen DS2-Low-Konzept mit Abweichungen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer beide Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [KODIERDATEN_LESEN](#job-kodierdaten-lesen) - Auslesen des Kodierdatenblocks1 2 Byte fuer Ausstattung & Sprache
- [KODIERDATEN_SCHREIBEN](#job-kodierdaten-schreiben) - Schreiben des Kodierdatenblocks1 2 Byte fuer Ausstattung & Sprache
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren

<a id="job-info"></a>
### INFO

Information bzgl. SGBD

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen DS2-Low-Konzept mit Abweichungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 255 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antworten vom SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer beide Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-kodierdaten-lesen"></a>
### KODIERDATEN_LESEN

Auslesen des Kodierdatenblocks1 2 Byte fuer Ausstattung & Sprache

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-kodierdaten-schreiben"></a>
### KODIERDATEN_SCHREIBEN

Schreiben des Kodierdatenblocks1 2 Byte fuer Ausstattung & Sprache

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF ist eigentlich bitweise zu lesen |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF ist eigentlich bitweise zu lesen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (9 × 2)
- [FARTTEXTE](#table-farttexte) (20 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
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
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Magnetventile FH Fahrertuer auf/zu |
| 0x02 | Magnetventile FH Beifahrertuer auf/zu |
| 0x03 | Magnetventile FH Fahrertuer hinten auf/zu |
| 0x04 | Magnetventile FH Beifahrertuer hinten auf/zu |
| 0x05 | Frontscheibenheizung Fahrerseite |
| 0x06 | Frontscheibenheizung Beifahrerseite |
| 0x07 | Seitenscheibenheizung Fahrerseite |
| 0x08 | Seitenscheibenheizung Beifahrerseite |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 20 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x01 | statischer Fehler |
| 0x02 | sporadischer Fehler |
| 0x04 | Unterbrechung |
| 0x05 | statischer Fehler: Unterbrechung |
| 0x06 | sporadischer Fehler: Unterbrechung |
| 0x08 | Kurzschluss |
| 0x09 | statischer Fehler: Kurzschluss |
| 0x0A | sporadischer Fehler: Kurzschluss |
| 0x0D | statischer Fehler: Unterbrechung/Kurzschluss |
| 0x0E | sporadischer Fehler: Unterbrechung/Kurzschluss |
| 0x10 | Kurzschluss nach plus |
| 0x11 | statischer Fehler: Kurzschluss nach plus |
| 0x12 | sporadischer Fehler: Kurzschluss nach plus |
| 0x15 | statischer Fehler: Unterbrechung/Kurzschluss nach plus |
| 0x16 | sporadischer Fehler: Unterbrechung/Kurzschluss nach plus |
| 0x19 | statischer Fehler: Kurzschluss nach Masse/nach plus |
| 0x1A | sporadischer Fehler: Kurzschluss nach Masse/nach plus |
| 0x1D | statischer Fehler: Unterbrechung/Kurzschluss nach Masse/nach plus |
| 0x1E | sporadischer Fehler: Unterbrechung/Kurzschluss nach Masse/nach plus |
| 0xXY | unbekannte Fehlerart |
