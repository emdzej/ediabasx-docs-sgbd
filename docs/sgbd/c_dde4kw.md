# c_dde4kw.prg

- Jobs: [10](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 4.0 for Freelander |
| ORIGIN | BMW TI-435 Matthew Bennett |
| REVISION | 0.03 |
| AUTHOR | Rover SSL M.Rafferty |
| COMMENT | DDE4 KW2000 only for Freelander - tested on ECU |
| PACKAGE | N/A |
| SPRACHE | english |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Auslesen des Zentralen Codierschluessels Read the ZCS
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Schreiben des Zentralen Codierschluessels Write the ZCS
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Status
- [SECURITY_ACCESS](#job-security-access) - Schutzmechanismus SEED_KEY Obtain security access via seed-key for programming
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_FG_LESEN](#job-c-fg-lesen) - Ident und AIF zusammen lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and verify coding data
- [IDENT](#job-ident) - Ident und AIF zusammen lesen

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

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

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Auslesen des Zentralen Codierschluessels Read the ZCS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GM | string | Zentralcode C1 - Grundmerkmal Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal Version information |

<a id="job-c-zcs-auftrag"></a>
### C_ZCS_AUFTRAG

Schreiben des Zentralen Codierschluessels Write the ZCS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal Basic features - 8 characters + chksm |
| SA | string | Zentralcode C2 - Sonderausstattung Particular equipment - 16 characters + chksm |
| VN | string | Zentralcode C3 - Versionsmerkmal Version information - 10 characters + chksm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| START_DIAGNOSTIC_SESSION_MODE | int | nichts |

<a id="job-security-access"></a>
### SECURITY_ACCESS

Schutzmechanismus SEED_KEY Obtain security access via seed-key for programming

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE_KEY | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| Z_ZAHL | int | Zufallszahl Random number |
| STAT_SEED_KEY | binary | Rueckgabewert Status |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Ident und AIF zusammen lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer VIN |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge Number of AIF records stored |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and verify coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident"></a>
### IDENT

Ident und AIF zusammen lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | ROVER assembly number |
| ID_HW_NR | string | ROVER-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | string | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | string | Lieferanten-Nummer Supplier number |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex Change index |
| ID_PROD_NR | string | Produktionsnummer |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (37 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 37 rows × 2 columns

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
| 0X80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIGNOSTICMODE |
| 0XF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0XFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0XFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| ?01? | OKAY |
| ?02? | BUSY |
| ?03? | AIF_NICHT_PROGRAMMIERT |
| ?04? | KEIN AIF MEHR FREI |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |
