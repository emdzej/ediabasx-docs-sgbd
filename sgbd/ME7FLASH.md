# ME7FLASH.PRG

- Jobs: [30](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ME 7.X M62  |
| ORIGIN | BMW TP-421 Weber |
| REVISION | 1.40 |
| AUTHOR | BMW TP-421 Weber |
| COMMENT | Master - Datei fuer Flashprog. |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [ZIF](#job-zif) - Job ZIF
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [GET_CURRAIFADR](#job-get-curraifadr) - ermittelt die Adresse des Momentan gültigen AIF-Eintrags
- [AIF_SCHREIBEN](#job-aif-schreiben) - ermittelt die Adresse des Momentan gültigen AIF-Eintrags
- [FLASH_LESEN](#job-flash-lesen) - Beliebige FLASH - Zellen auslesen
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Status
- [FLASH_PROG_STATUS](#job-flash-prog-status) - Status
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash  - Zellen loeschen
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Beliebige Flash Zellen mit 02 beschreiben
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen  beschreiben
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Beliebige EPROM - Zellen auslesen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [FS_LESEN_STATUS](#job-fs-lesen-status) - Auslesen des Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode)
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - Wechselcodesynchronisation EWS 3 - DME anstossen
- [STATUS_SYNC_MODE](#job-status-sync-mode)

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-initialisierung"></a>
### initialisierung

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

<a id="job-uprog-ein"></a>
### UPROG_EIN

Programmierspannung einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | real | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-uprog-aus"></a>
### UPROG_AUS

Programmierspannung ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| DATEN_REF_PROJEKT | string | Projektkennzeichnung |
| DATEN_REF_PROGRAMM_STAND | string | Programmstand |
| DATEN_REF_DATENSATZ | string | Datensatzkennung |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hw-referenz"></a>
### HW_REFERENZ

Job HW-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif"></a>
### ZIF

Job ZIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Programmstand |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-get-curraifadr"></a>
### GET_CURRAIFADR

ermittelt die Adresse des Momentan gültigen AIF-Eintrags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE | long | AIF Basisadresse |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

ermittelt die Adresse des Momentan gültigen AIF-Eintrags

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRGESTELLNR | string |  |
| BMW_FERTIGUNGSDAT | string |  |
| BMW_SWNR | string |  |
| BMW_TYPPRUEFNR | long |  |
| BMW_ZBNR | long |  |
| PRG_GERAET_SER_NR | string |  |
| WERKSCODE | int |  |
| KM | int |  |
| PRG_STANDSNR | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| VERIFYBYTE | int |  |

<a id="job-flash-lesen"></a>
### FLASH_LESEN

Beliebige FLASH - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low HEX |
| FLASH_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LESEN_WERT | binary | nichts |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| START_DIAGNOSTIC_SESSION_MODE | int | nichts |

<a id="job-flash-prog-status"></a>
### FLASH_PROG_STATUS

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_PROG_STATUS | int | nichts |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash  - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_STATUS | int | nichts |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Beliebige Flash Zellen mit 02 beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ADRESSE_ANFANG | long | Uebergabeparameter, Startadresse High-Middle-Low und Daten |
| FLASH_SCHREIBEN_ADRESSE_ENDE | long | Uebergabeparameter, Endadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_STATUS | int | nichts |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen  beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_STATUS | int | nichts |
| FLASH_SCHREIBEN_ANZAHL | int | nichts |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Beliebige EPROM - Zellen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |

<a id="job-fs-lesen-status"></a>
### FS_LESEN_STATUS

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_CODEHEX | binary | alle Fehlerbyte |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_CODEHEX | binary | alle Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-sync-mode"></a>
### STEUERN_SYNC_MODE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STEUERN_SYNC_MODE_STATUS | int | Statusflag |
| STEUERN_SYNC_MODE_TEXT | string | Statustext |

<a id="job-wechselcode-sync-dme"></a>
### WECHSELCODE_SYNC_DME

Wechselcodesynchronisation EWS 3 - DME anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (33 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 33 rows × 2 columns

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
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |
