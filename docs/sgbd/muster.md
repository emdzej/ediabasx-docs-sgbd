# muster.prg

- Jobs: [10](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MUSTER SGBD |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.08 |
| AUTHOR | BMW TP-421 Drexel |
| COMMENT | MUSTER SGBD |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten fuer MUSTER
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Fehlerspeicher quick lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten fuer MUSTER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_LZ | int | Logistikzaehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_UW_SATZ | int | Anzahl der Umweltbedingungssaetze |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string |  |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string |  |
| F_UW1_NR | int |  |
| F_UW1_TEXT | string |  |
| F_UW1_WERT | int |  |
| F_UW1_EINH | string |  |
| F_UW2_NR | int |  |
| F_UW2_TEXT | string |  |
| F_UW2_WERT | int |  |
| F_UW2_EINH | string |  |
| F_UW3_NR | int |  |
| F_UW3_TEXT | string |  |
| F_UW3_WERT | int |  |
| F_UW3_EINH | string |  |
| F_UW4_NR | int |  |
| F_UW4_TEXT | string |  |
| F_UW4_WERT | int |  |
| F_UW4_EINH | string |  |
| F_HEX_CODE | binary |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Fehlerspeicher quick lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ANZ | int | Fehleranzahl |
| F_BSZ_AKT | real | Betriebsstundenzaehler aktuell |
| F_BSZ_ALT | real | Betriebsstundenzaehler bei letztem FS loeschen |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Datenfeld |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [JOBRESULTKWP2000](#table-jobresultkwp2000) (32 × 2)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (30 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (13 × 3)

<a id="table-jobresultkwp2000"></a>
### JOBRESULTKWP2000

Dimensions: 32 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0X00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0X10 | ERROR_ECU_GENERAL_REJECT |
| 0X11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0X12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED_INVALID_FORMAT |
| 0X21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0X22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0X23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0X31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0X33 | ERROR_ECU_SECURITY_ACCESS_DENIED_SECURITY_ACCESS_REQUESTED |
| 0X35 | ERROR_ECU_INVALID_KEY |
| 0X36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0X37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0X40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0X41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0X42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0X43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0X50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0X51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0X52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0X53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0X71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0X72 | ERROR_ECU_TRANSFER_ABORTED |
| 0X74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0X75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0X76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0X77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0X78 | ERROR_ECU_REQ_CORRECTLY_RCVD_RSP_PENDING |
| 0X79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0XF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0XFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0XFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

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

Dimensions: 30 rows × 2 columns

| LIEF_NR | LIEF_NAME |
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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Fehler 1 |
| 0x02 | Fehler 2 |
| 0x03 | Fehler 3 |
| 0x04 | Fehler 4 |
| 0x05 | Fehler 5 |
| 0x06 | Fehler 6 |
| 0x07 | Fehler 7 |
| 0x08 | Fehler 8 |
| 0x09 | Fehler 9 |
| 0x0A | Fehler 10 |
| 0x0B | Fehler 11 |
| 0x0C | Fehler 12 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Kurzschluss gegen U-Batt |
| 0x01 | Kurzschluss gegen Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | ungueltiger Arbeitsbereich |
| 0x04 | sporadischer Fehler |
| 0x05 | statischer Fehler |
| 0x06 | Fehler momentan nicht vorhanden |
| 0x07 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 13 rows × 3 columns

| UWNR | UWTEXT | UWEINH |
| --- | --- | --- |
| 0x01 | Umwelt Text 1 | Umwelt Einheit 1 |
| 0x02 | Umwelt Text 2 | Umwelt Einheit 2 |
| 0x03 | Umwelt Text 3 | Umwelt Einheit 3 |
| 0x04 | Umwelt Text 4 | Umwelt Einheit 4 |
| 0x05 | Umwelt Text 5 | Umwelt Einheit 5 |
| 0x06 | Umwelt Text 6 | Umwelt Einheit 6 |
| 0x07 | Umwelt Text 7 | Umwelt Einheit 7 |
| 0x08 | Umwelt Text 8 | Umwelt Einheit 8 |
| 0x09 | Umwelt Text 9 | Umwelt Einheit 9 |
| 0x0A | Umwelt Text 10 | Umwelt Einheit 10 |
| 0x0B | Umwelt Text 11 | Umwelt Einheit 11 |
| 0x0C | Umwelt Text 12 | Umwelt Einheit 12 |
| 0xFF | unbekannte Umweltbedingung | unbekannte Umweltbedingung |
