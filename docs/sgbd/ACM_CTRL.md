# ACM_CTRL.prg

- Jobs: [11](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Spezial SGBD für die Flashabnahme |
| ORIGIN | BMW EE-73 Knöbl |
| REVISION | 1.7 |
| AUTHOR | BMW EE-73 Knöbl |
| COMMENT | N/A |
| PACKAGE | 1.09 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [UIF_GET_SIZE](#job-uif-get-size) - Ermitteln der Länge des AIFs Modus: Default
- [UIF_IDENT_READ](#job-uif-ident-read) - Auslesen des aktuellen AIFs KWP2000: $1a ReadEcuIdentification $86 CurrentUifDataTable Modus  : Default
- [UIF_MEM_READ](#job-uif-mem-read) - Auslesen des AIF-Speichers KWP2000: $23 ReadMemoryByAddress $hh Address $mm Address $ll Address $07 UIF Memory $nn Size Modus  : Default
- [FUNC_PHYS_HW_NR_READ](#job-func-phys-hw-nr-read) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) Modus  : Default
- [ACM_INIT_IDENT](#job-acm-init-ident) - Modus  : Default
- [ACM_SHOW_IDENT](#job-acm-show-ident) - Modus  : Default
- [ACM_FORCE_ERROR](#job-acm-force-error) - Modus  : Default
- [EDIABAS_SEND_JOB](#job-ediabas-send-job) - Modus  : Default
- [EDIABAS_WAIT_SEC](#job-ediabas-wait-sec) - Modus: Default

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

<a id="job-uif-get-size"></a>
### UIF_GET_SIZE

Ermitteln der Länge des AIFs Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ECU_ADDRESS | int | Steuergeräteadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| UIF_SIZE | int | ermittelte AIF Größe, evtl. korregiert |
| UIF_ORG_SIZE | int | direkte AIF Größe aus Telegrammlänge |
| UIF_DATA | binary | AIF Hex-Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-uif-ident-read"></a>
### UIF_IDENT_READ

Auslesen des aktuellen AIFs KWP2000: $1a ReadEcuIdentification $86 CurrentUifDataTable Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-uif-mem-read"></a>
### UIF_MEM_READ

Auslesen des AIF-Speichers KWP2000: $23 ReadMemoryByAddress $hh Address $mm Address $ll Address $07 UIF Memory $nn Size Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |
| AIF_GROESSE | int | AIF Länge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ANZAHL | int | Anzahl gelesener AIF-Einträge |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-func-phys-hw-nr-read"></a>
### FUNC_PHYS_HW_NR_READ

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräte- oder funktionale Adresse Default: $EF (alle SG) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ID_SG_ADR | long | Steuergeraeteadresse |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-acm-init-ident"></a>
### ACM_INIT_IDENT

Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-acm-show-ident"></a>
### ACM_SHOW_IDENT

Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ECU_ADDR | int | Optional: Steuergeräte Adresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-acm-force-error"></a>
### ACM_FORCE_ERROR

Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ERR_MODE | int | Fehlermodus 0..15 Default: 0 (AUS) |
| ERR_CNTR | int | Anzahl Durchläufe 0..255, 0 = endlos Default: 0 |
| ERR_WAIT | int | Warteblöcke 0..255 Default: 9 |
| ERR_KILL | int | Störblöcke 0..255 Default: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-ediabas-send-job"></a>
### EDIABAS_SEND_JOB

Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ECU_ADDR | int | Steuergeräte Adresse |
| ECU_DATA | string | Hex-Bytes Beispiel: 1a80 -&gt; 1a 80 oder: 23,0,0,0,7,0 -&gt; 23 00 00 07 00 oder: 22,2501 -&gt; 22 25 01 |
| ERROR_REPEAT_COUNTER | int | Wiederholungen im Fehlerfall (Default: 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ID_SG_ADR | long | Steuergeraeteadresse |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ediabas-wait-sec"></a>
### EDIABAS_WAIT_SEC

Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SECONDS | int | Wartezeit in Sekunden (max. 300 sec) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (86 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 86 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?03? | ERROR_ECU_INCORRECT_LEN |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?41? | ERROR_BAUDRATE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_DATA_OUT_OF_RANGE |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| ?73? | ERROR_NO_BIN_BUFFER |
| ?74? | ERROR_BIN_BUFFER |
| ?75? | ERROR_DATA_TYPE |
| ?76? | ERROR_CHECKSUM |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_NO_FREE_UIF |
| ?8B? | ERROR_MAX_UIF |
| ?8C? | ERROR_SIZE_UIF |
| ?8D? | ERROR_LEVEL |
| ?8E? | ERROR_KEY |
| ?8F? | ERROR_AUTHENTICATION |
| ?90? | ERROR_NO_DREF |
| ?91? | ERROR_CHECK_PECUHN |
| ?92? | ERROR_CHECK_PRGREF |
| ?93? | ERROR_AIF_NR |
| ?94? | ERROR_CHECK_DREF |
| ?95? | ERROR_CHECK_HWREF |
| ?96? | ERROR_CHECK_HWREF |
| ?97? | ERROR_CHECK_PRGREFB |
| ?98? | ERROR_CHECK_VMECUH*NB |
| ?99? | ERROR_CHECK_PRGREFB |
| ?9A? | ERROR_CHECK_VMECUH*N |
| ?A0? | ERROR_DIAG_PROT |
| ?A1? | ERROR_SG_ADRESSE |
| ?A2? | ERROR_SG_MAXANZAHL_AIF |
| ?A3? | ERROR_SG_GROESSE_AIF |
| ?A4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?A5? | ERROR_SG_AUTHENTISIERUNG |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |
