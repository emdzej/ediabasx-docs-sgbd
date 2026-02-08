# MFLR50.prg

- Jobs: [8](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Multifunktionslenkrad R50 |
| ORIGIN | BMW TI-431 Stadlhofer |
| REVISION | 1.2 |
| AUTHOR | Software-Style M.Rafferty |
| COMMENT | Version Spec 1.2 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Read the ECU Identification data
- [IDENT_SCHREIBEN](#job-ident-schreiben) - Write the ECU Ident
- [STEUERN_IOSTATES](#job-steuern-iostates) - Force Digital Output States
- [STATUS_LESEN](#job-status-lesen) - alle Stati des MFL lesen Read all input/outputs
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten Continue Diagnostics - Send ping message
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden End diagnostics

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-ident"></a>
### IDENT

Read the ECU Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

Write the ECU Ident

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part number 7 character string if BMW format, 9 character string if Rover encoded |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |

<a id="job-steuern-iostates"></a>
### STEUERN_IOSTATES

Force Digital Output States

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente Control name From NAME column in table "Digital" |
| EIN | int | 1 wenn einschalten  0 wenn ausschalten Forcing value: 1=on 0=off |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |

<a id="job-status-lesen"></a>
### STATUS_LESEN

alle Stati des MFL lesen Read all input/outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUXILIARY_VOLTAGE_WERT | real | Voltage of auxiliary |
| STAT_AUXILIARY_VOLTAGE_EINH | string | Unit = V |
| STAT_SEARCH_UP_ACTIVE | int | Search up switch |
| STAT_SEARCH_DOWN_ACTIVE | int | Search down switch |
| STAT_VOLUME_UP_ACTIVE | int | Volume up switch |
| STAT_VOLUME_DOWN_ACTIVE | int | Volume down switch |
| STAT_MODE_ACTIVE | int | Mode switch |
| STAT_PHONE_SEND_END_ACTIVE | int | Phone send/end switch |
| STAT_SPEED_UP_ACTIVE | int | Speed up switch |
| STAT_SPEED_DOWN_ACTIVE | int | Speed down switch |
| STAT_CRUISE_ON_OFF_ACTIVE | int | Cruise on/off switch |
| STAT_CRUISE_RESUME_ACTIVE | int | Cruise resume switch |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten Continue Diagnostics - Send ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden End diagnostics

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (45 × 2)
- [ROVERPARTPREFIX](#table-roverpartprefix) (22 × 2)
- [DIGITAL](#table-digital) (11 × 5)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 45 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartprefix"></a>
### ROVERPARTPREFIX

Dimensions: 22 rows × 2 columns

| CODE | PREFIX |
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
| 0xB6 | YUW |
| 0xFF | ??? |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 11 rows × 5 columns

| NAME | BYTE | MASK | VALUE | ID_NR |
| --- | --- | --- | --- | --- |
| SEARCH_UP | 3 | 0x01 | 0x01 | 0x00 |
| SEARCH_DOWN | 3 | 0x02 | 0x02 | 0x01 |
| VOLUME_UP | 3 | 0x04 | 0x04 | 0x02 |
| VOLUME_DOWN | 3 | 0x08 | 0x08 | 0x03 |
| MODE | 3 | 0x10 | 0x10 | 0x04 |
| PHONE_SEND_END | 3 | 0x20 | 0x20 | 0x05 |
| SPEED_UP | 3 | 0x40 | 0x40 | 0x06 |
| SPEED_DOWN | 3 | 0x80 | 0x80 | 0x07 |
| CRUISE_ON_OFF | 4 | 0x01 | 0x01 | 0x08 |
| CRUISE_RESUME | 4 | 0x02 | 0x02 | 0x09 |
| ?? | FF | 0x00 | 0xFF | 0xFF |
