# asc_l22.prg

- Jobs: [16](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Automatische Stabilitaets Control plus Traktion, ASC+T L22 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.0 |
| AUTHOR | BMW EF-73 Kusch |
| COMMENT | Conti_Teves MK25, 10400Bd, LANDROVER Freelander |
| PACKAGE | 1.14 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter KWP
- [START_COMMUNICATION](#job-start-communication) - Kap. 5.1
- [STOP_COMMUNICATION](#job-stop-communication) - Kommunikation beenden, Kap. 5.2 Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - Starten eines Diagnose-Modus
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Stop des aktuellen Diagnose-Modus
- [DIAGNOSE_WEITER](#job-diagnose-weiter)
- [SEED](#job-seed) - Status Eingaenge ASC_MK20
- [IDENT](#job-ident) - Ident-Daten des SG ... Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit)
- [STEUERN_DIGITAL](#job-steuern-digital) - Parameterliste:EVVL,AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,Pumpe,SV1,SV2,EUV1,EUV2
- [DIAG_MODE_SEED](#job-diag-mode-seed) - Status Eingaenge ASC_MK20
- [NA_ENTLUEFTUNG_LI](#job-na-entlueftung-li) - Steuern_Digital ansteueren u. ruecksetzen
- [NA_ENTLUEFTUNG_RE](#job-na-entlueftung-re) - Steuern_Digital ansteueren u. ruecksetzen

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

Initialisierung und Kommunikationsparameter KWP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-start-communication"></a>
### START_COMMUNICATION

Kap. 5.1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANSWER | binary | Hex-Antwort vom SG |
| _TEL_REQUEST | binary | Anforderung ans SG |
| KEY_BYTE | string | Key-Byte SG |

<a id="job-stop-communication"></a>
### STOP_COMMUNICATION

Kommunikation beenden, Kap. 5.2 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Anforderung ans SG |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

Starten eines Diagnose-Modus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MODE_TEXT | string | Mode als Textausgabe |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Stop des aktuellen Diagnose-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-seed"></a>
### SEED

Status Eingaenge ASC_MK20

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODE_TEXT | string | Mode als Textausgabe |
| _TEL_REQUEST_1 | binary | Anforderungstelegramm |
| _TEL_REQUEST_2 | binary | Anforderungstelegramm |
| _TEL_ANSWER_1 | binary | Antworttelegramm |
| _TEL_ANSWER_2 | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, oder FEHLER |

<a id="job-ident"></a>
### IDENT

Ident-Daten des SG ... Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Fehlercode(dec) |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ZAHL | int | Anzahl Fehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 3 |
| F_ART1_NR | int | 1. Fehlerart Bereich: |
| F_ART1_TEXT | string | 1. Fehlerart als Text table FArtTexte ARTTEXT |
| F_ART2_NR | int | 2. Fehlerart Bereich: |
| F_ART2_TEXT | string | 2. Fehlerart als Text table FArtTexte ARTTEXT |
| F_ART3_NR | int | 3. Fehlerart Bereich: |
| F_ART3_TEXT | string | 3. Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Antworttelegramm |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Parameterliste:EVVL,AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,Pumpe,SV1,SV2,EUV1,EUV2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_REQUEST | binary | Anforderungstelegramm |
| _TEL_ANSWER | binary | Antworttelegramm |

<a id="job-diag-mode-seed"></a>
### DIAG_MODE_SEED

Status Eingaenge ASC_MK20

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODE_TEXT | string | Mode als Textausgabe |
| _TEL_REQUEST_1 | binary | Anforderungstelegramm |
| _TEL_REQUEST_2 | binary | Anforderungstelegramm |
| _TEL_ANSWER_1 | binary | Antworttelegramm |
| _TEL_ANSWER_2 | binary | Antworttelegramm |
| _TEL_REQUEST_3 | binary | Antworttelegramm |
| _TEL_ANSWER_3 | binary | Antworttelegramm |
| _TEL_REQUEST_4 | binary | Antworttelegramm |
| _TEL_ANSWER_4 | binary | Antworttelegramm |
| JOB_STATUS_1 | string | OKAY, oder FEHLER |
| JOB_STATUS_2 | string | OKAY, oder FEHLER |
| JOB_STATUS_3 | string | OKAY, oder FEHLER |
| JOB_STATUS_4 | string | OKAY, oder FEHLER |

<a id="job-na-entlueftung-li"></a>
### NA_ENTLUEFTUNG_LI

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-re"></a>
### NA_ENTLUEFTUNG_RE

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [DIAGMODE](#table-diagmode) (5 × 4)
- [JOBRESULT](#table-jobresult) (33 × 2)
- [LIEFERANTEN](#table-lieferanten) (33 × 2)
- [FORTTEXTE](#table-forttexte) (50 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [STEUERN](#table-steuern) (15 × 3)

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 5 rows × 4 columns

| NR | ACCESS_NR | MODE | MODE_TEXT |
| --- | --- | --- | --- |
| 0x81 | 3 | SI | Service |
| 0x83 | 5 | MAN | Rover_Manufacture |
| 0x85 | 7 | PRG | Reprogramming |
| 0x86 | 9 | DEV | Rover_Development |
| 0xXY | - | --- | unknown Diagnostic-Mode |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 33 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED_INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED_SECURITY_ACCESS_REQUESTED |
| 0x35 | ERROR_ECU_INVALID_KEY |
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
| 0x78 | ERROR_ECU_REQ_CORRECTLY_RCVD_RSP_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIGNOSTICMODE |
| 0xF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0xFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0xFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 33 rows × 2 columns

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
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 50 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D90 | wheel speed sensor front left monitoring trigger signal |
| 0x5D91 | wheel speed sensor front left continuity (extrapolation) |
| 0x5D93 | wheel speed sensor front left start up detection (comparison) |
| 0x5D94 | monitoring ABS outlet valve by wheel speed sensor front left (long term detection) |
| 0x5DA0 | wheel speed sensor front right monitoring trigger signal |
| 0x5DA1 | wheel speed sensor front right continuity  (extrapolation) |
| 0x5DA3 | wheel speed sensor front right start up detection (comparison) |
| 0x5DA4 | monitoring ABS outlet valve by wheel speed sensor front right (long term detection) |
| 0x5DB0 | wheel speed sensor rear left monitoring trigger signal |
| 0x5DB1 | wheel speed sensor rear left continuity (extrapolation) |
| 0x5DB3 | wheel speed sensor rear left start up detection (comparison) |
| 0x5DB4 | monitoring ABS outlet valve by wheel speed sensor rear left (long term detection) |
| 0x5DC0 | wheel speed sensor rear right monitoring trigger signal |
| 0x5DC1 | wheel speed sensor rear right continuity (extrapolation) |
| 0x5DC3 | wheel speed sensor rear right start up detection (comparison) |
| 0x5DC4 | monitoring ABS outlet valve by wheel speed sensor rear right (long term detection) |
| 0x5DD0 | ABS inlet valve front left |
| 0x5DD1 | ABS inlet valve front right |
| 0x5DD2 | ABS inlet valve rear left |
| 0x5DD3 | ABS inlet valve rear right |
| 0x5DD4 | ABS outlet valve front left |
| 0x5DD5 | ABS outlet valve front right |
| 0x5DD6 | ABS outlet valve rear left |
| 0x5DD7 | ABS outlet valve rear right |
| 0x5DE0 | ASC extra valve 1 |
| 0x5DE1 | ASC extra valve 2 |
| 0x5DE2 | EU valve 1 |
| 0x5DE3 | EU valve 2 |
| 0x5DE4 | redundant brake light switch (electrical failure) |
| 0x5DE5 | brake light switch (signal not plausible) |
| 0x5DE6 | longitudinal acceleration Sensor not plausible |
| 0x5DE7 | longitudinal acceleration Sensor electrical failure |
| 0x5DF0 | monitoring of pump supply voltage during pump motor actuation |
| 0x5DF2 | control unit error |
| 0x5DF4 | operating voltage &lt; 9 Volt |
| 0x5DF5 | leakage current detection, passive valve test, failure detection via active test pulse, electromagnetic interference  wheel speed sensor |
| 0x5DF6 | Parameter Error (datas detected in first loop did not correspond to datas stored in EEPROM |
| 0x5DF7 | operating voltage &gt; 18 Volt |
| 0x5E00 | main relay inside control unit (kl30) |
| 0x5E10 | internal error CAN-Controller (RAM check error) |
| 0x5E11 | CAN Bus Off Error |
| 0x5E12 | CAN DME/DDE/2 datas not plausible |
| 0x5E13 | CAN DME/DDE/1 datas not plausible |
| 0x5E14 | CAN Timeout DME/DDE |
| 0x5E15 | CAN Timeout EGS |
| 0x5E16 | CAN Timeout INSTR4 |
| 0x5E17 | CAN EGS Error (datas not plausible) |
| 0x5E32 | Brake light switch Relay |
| 0x5E36 | gear plausibility gear |
| 0xXYXY | Unknown error location |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Testbedingungen erfuellt |
| 0x10 | Testbedingungen noch nicht erfuellt |
| 0x00 | Fehler bisher nicht aufgetreten |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x40 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x60 | Fehler momentan vorhanden und bereits gespeichert |
| 0x00 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x80 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xXY | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 15 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHL | 0 | 0x10 |
| AVHL | 0 | 0x20 |
| EVHR | 0 | 0x40 |
| AVHR | 0 | 0x80 |
| SV1 | 1 | 0x01 |
| SV2 | 1 | 0x02 |
| EUV1 | 1 | 0x04 |
| EUV2 | 1 | 0x08 |
| Pump | 1 | 0x10 |
| BLS | 1 | 0x20 |
| XYZ | 1 | 0x00 |
