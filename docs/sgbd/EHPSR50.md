# EHPSR50.prg

- Jobs: [29](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EHPSR50 |
| ORIGIN | BMW TI-431 Siegfried Helmich |
| REVISION | 1.1 |
| AUTHOR | Software-Style M.Rafferty |
| COMMENT | Basiert auf Spec Version A8 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EHPS
- [IDENT_EXTENDED](#job-ident-extended) - Read additional ECU Ident information
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Tester present message
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Begins a diagnostic session
- [SG_RESET](#job-sg-reset) - Reset the ECU
- [FS_LESEN](#job-fs-lesen) - Read internal and external faults
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [STATUS_FS_LESEN](#job-status-fs-lesen) - Read number of faults and earliest faults through snapshot
- [STATUS_IO_LESEN](#job-status-io-lesen) - Read Digital inputs/outputs
- [STATUS_ANALOG](#job-status-analog) - Read Analogue Input / Outputs
- [STEUERN_PWM](#job-steuern-pwm) - Force the Pulse Width Modulation from 0 to 100%
- [STEUERN_PWM_RESET](#job-steuern-pwm-reset) - Return PWM output control to the application software
- [READ_MEMORY](#job-read-memory) - Read ECU Memory by Address Speicher auslesen
- [READ_SIEMENS_SERIAL_NR](#job-read-siemens-serial-nr) - Read the Siemens serial number
- [READ_ZF_HW_NR](#job-read-zf-hw-nr) - Read the ZF ECU Hardware number
- [WRITE_MEMORY](#job-write-memory) - Write memory to a specified address Speicher schreiben
- [WRITE_ZF_HW_NR](#job-write-zf-hw-nr) - Write the ZF ECU Hardware Number
- [SEED_KEY](#job-seed-key) - Obtain security access to the ECU Schutzmechanismus SEED_KEY
- [CHECK_REPROG_DEPENDING](#job-check-reprog-depending) - Calculate the checksum and check the coherence system
- [REPORT_REPROG_STATUS](#job-report-reprog-status) - Get the status of reprogramming after a mistake
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Request download
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Transfer data to the ECU Data is transfered in blocks of 62 bytes (maximum 128 x 62 == 7936 bytes)
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Exit data transfer
- [PROG_DATUM_SCHREIBEN](#job-prog-datum-schreiben) - Schreiben der Programm datum Write the programming date
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer Read the VIN
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Schreiben der Fahrgestellnummer Write the VIN
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden Stop the diagnostic session

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

Ident-Daten fuer EHPS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_SYSTEM_NAME | int | BMW system name |
| ID_DATUM_TAG | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MON | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_SW_NR | int | Softwarenummer |
| ID_BUS_INDEX | int | Bus-Index |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-ident-extended"></a>
### IDENT_EXTENDED

Read additional ECU Ident information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SIEMENS_HW_NR | string | Siemens ECU hardware number |
| ID_SIEMENS_SW_NR | string | Siemens ECU software number |
| ID_SIEMENS_SW_VERSION_NR | string | Siemens ECU software version number |
| ID_PROG_DATUM_TAG | int | Programm tag Day of programming |
| ID_PROG_DATUM_MON | int | Programm monat Month of programming |
| ID_PROG_DATUM_JAHR | int | Programm jahr Year of programming |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read Siemens HW NR response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read Siemens SW NR response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read Siemens SW Version NR response |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG Read Siemens Programming date response |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Tester present message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Begins a diagnostic session

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Diagnostic mode: 0x81=Standard, 0x85=Programming |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-lesen"></a>
### FS_LESEN

Read internal and external faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode Raw fault data from the ECU |
| F_ORT_NR | int | Index fuer Fehlerort Fault number |
| F_ORT_TEXT | string | Fehlerort als Text Fault description |
| F_HFK | int | Fehlerhaeufigkeit Frequency |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Count of Environment Data Items per fault |
| F_ART_ANZ | int | Anzahl der Fehlerarten Count of additional fault status information per fault |
| F_ART1_NR | int | 1. (einzige) Fehlerart Fault status 1 number |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text Fault status 1 text |
| F_ART2_NR | int | 2. (einzige) Fehlerart Fault status 2 |
| F_ART2_TEXT | string | 2. (einzige) Fehlerart als Text Fault string 2 |
| F_ART3_NR | int | 3. (einzige) Fehlerart Fault status 3 |
| F_ART3_TEXT | string | 3. (einzige) Fehlerart als Text Fault string 3 |
| F_ART4_NR | int | 4. (einzige) Fehlerart Fault status 4 |
| F_ART4_TEXT | string | 4. (einzige) Fehlerart als Text Fault string 4 |
| F_ART5_NR | int | 5. (einzige) Fehlerart Fault status 5 |
| F_ART5_TEXT | string | 5. (einzige) Fehlerart als Text Fault string 5 |
| F_ART6_NR | int | 6. (einzige) Fehlerart Fault status 6 |
| F_ART6_TEXT | string | 6. (einzige) Fehlerart als Text Fault string 6 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-fs-lesen"></a>
### STATUS_FS_LESEN

Read number of faults and earliest faults through snapshot

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_FAULT_COUNT | int | Fehler zaehlen Count of all faults up to a maximum of 10 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode Raw fault data from the ECU |
| F_ORT_NR | int | Index fuer Fehlerort Fault number |
| F_ORT_TEXT | string | Fehlerort als Text Fault description |
| F_HFK | int | Fehlerhaeufigkeit Frequency |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Count of Environment Data Items per fault |
| F_ART_ANZ | int | Anzahl der Fehlerarten Count of additional fault status information per fault |
| F_ART1_NR | int | 1. (einzige) Fehlerart Fault status 1 number |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text Fault status 1 text |
| F_ART2_NR | int | 2. (einzige) Fehlerart Fault status 2 |
| F_ART2_TEXT | string | 2. (einzige) Fehlerart als Text Fault string 2 |
| F_ART3_NR | int | 3. (einzige) Fehlerart Fault status 3 |
| F_ART3_TEXT | string | 3. (einzige) Fehlerart als Text Fault string 3 |
| F_ART4_NR | int | 4. (einzige) Fehlerart Fault status 4 |
| F_ART4_TEXT | string | 4. (einzige) Fehlerart als Text Fault string 4 |
| F_ART5_NR | int | 5. (einzige) Fehlerart Fault status 5 |
| F_ART5_TEXT | string | 5. (einzige) Fehlerart als Text Fault string 5 |
| F_ART6_NR | int | 6. (einzige) Fehlerart Fault status 6 |
| F_ART6_TEXT | string | 6. (einzige) Fehlerart als Text Fault string 6 |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Read Digital inputs/outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_IGNITION_ON | int | 1 wenn einschalten / 0 wenn ausschalten 1=on, 0=off |
| STAT_ENGINE_RUNNING | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| STAT_APPLICATION_RUNNING | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| STAT_SPEED_CONTROL_ENABLED | int | 1 wenn activ / 0 wenn aus 1=enabled, 0=disabled |
| STAT_DIAGNOSTIC_CONTROL_MODE_ON | int | 1 wenn activ / 0 wenn aus 1=on, 0=off |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Read Analogue Input / Outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_BATTERY_VOLTS_WERT | real | 0 -&gt; 25.5 V |
| STAT_BATTERY_VOLTS_EINH | string |  |
| STAT_TEMPERATURE_WERT | real | -40 -&gt; 215 Deg C |
| STAT_TEMPERATURE_EINH | string |  |
| STAT_MOTOR_CURRENT_WERT | real | 0 -&gt; 127.5 A |
| STAT_MOTOR_CURRENT_EINH | string |  |
| STAT_MOTOR_SPEED_WERT | real | 0 -&gt; 5100 rpm |
| STAT_MOTOR_SPEED_EINH | string |  |
| STAT_MOTOR_VOLTAGE_WERT | real | 0 -&gt; 25.5 V |
| STAT_MOTOR_VOLTAGE_EINH | string |  |
| STAT_PWM_MOTOR_CONTROL_WERT | real | 0 -&gt; 100 % |
| STAT_PWM_MOTOR_CONTROL_EINH | string |  |
| STAT_MOTOR_SPEED_CONTROL_WERT | real | 0 -&gt; 5100 rpm |
| STAT_MOTOR_SPEED_CONTROL_EINH | string |  |
| STAT_PWM_OUT_WERT | real | 0 -&gt; 100 % |
| STAT_PWM_OUT_EINH | string |  |
| STAT_MOTOR_CURRENT_MAX_WERT | real | 0 -&gt; 127.5 A |
| STAT_MOTOR_CURRENT_MAX_EINH | string |  |
| STAT_BATTERY_CURRENT_MAX_WERT | real | 0 -&gt; 127.5 A |
| STAT_BATTERY_CURRENT_MAX_EINH | string |  |
| STAT_ENGINE_RUNNING_ANALOG_WERT | real | 0 -&gt; 20.4 V |
| STAT_ENGINE_RUNNING_ANALOG_EINH | string |  |
| STAT_MOTOR_RESISTANCE_WERT | real | 0 -&gt; 199 mOhms |
| STAT_MOTOR_RESISTANCE_EINH | string |  |
| STAT_EMF_COEF_WERT | real | 0 -&gt; 797 rpm/V |
| STAT_EMF_COEF_EINH | string |  |

<a id="job-steuern-pwm"></a>
### STEUERN_PWM

Force the Pulse Width Modulation from 0 to 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Value to set the PWM ( 0 -&gt; 100 % ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWM_WERT | int | New value for the PWM as % |
| STAT_PWM_EINH | string | Unit of PWM = % |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-pwm-reset"></a>
### STEUERN_PWM_RESET

Return PWM output control to the application software

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-memory"></a>
### READ_MEMORY

Read ECU Memory by Address Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MEM_ADDRESS | unsigned int | 16 bit ECU memory address 0x0000 -&gt; 0x00FF: DATA memory 0x9F80 -&gt; 0x9FBF: EEPROM memory used for Siemens logistic data 0x9FC0 -&gt; 0x9FFF: EEPROM memory used for ZF data area 0xFF00 -&gt; 0xFFFF: XDATA memory |
| MEM_LENGTH | int | Length of memory to read (1 -&gt; 20) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MEM_DATA | binary | ECU memory which is read |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-siemens-serial-nr"></a>
### READ_SIEMENS_SERIAL_NR

Read the Siemens serial number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIAL_NR | string | Siemens serial number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-zf-hw-nr"></a>
### READ_ZF_HW_NR

Read the ZF ECU Hardware number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZF_HW_NR | string | ZF ECU Hardware number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-write-memory"></a>
### WRITE_MEMORY

Write memory to a specified address Speicher schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | unsigned int | 16 bit ECU memory address 0x0000 -&gt; 0x00FF: DATA memory 0x9FC0 -&gt; 0x9FFF: EEPROM memory used for ZF data area 0xFF00 -&gt; 0xFFFF: XDATA memory |
| LENGTH | int | Length of memory to write (1 -&gt; 20) |
| MEMDATA | string | Data to write |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-write-zf-hw-nr"></a>
### WRITE_ZF_HW_NR

Write the ZF ECU Hardware Number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZF_NR | string | ZF ECU Hardware Number 12 characters |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-seed-key"></a>
### SEED_KEY

Obtain security access to the ECU Schutzmechanismus SEED_KEY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int | Security Access level 1=Dealer, 2=Programming |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE1 | binary | Sendetelegramm anzeigen Send key telegram to ECU - request seed |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Request seed response |
| _TEL_SENDE2 | binary | Sendetelegramm anzeigen Send key telegram to ECU - send key |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Send key response |

<a id="job-check-reprog-depending"></a>
### CHECK_REPROG_DEPENDING

Calculate the checksum and check the coherence system

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-report-reprog-status"></a>
### REPORT_REPROG_STATUS

Get the status of reprogramming after a mistake

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| REPROG_STATUS | unsigned int | Reprogramming status Bit0: checksum of ECU EEPROM software - if error then TRUE Bit1: ECU EEPROM software does not fit to ROM software - if error then TRUE Bit2: always FALSE Bit3: always FALSE Bit4: always FALSE Bit5: always FALSE Bit6: always FALSE Bit7: always FALSE |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Request download

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Transfer data to the ECU Data is transfered in blocks of 62 bytes (maximum 128 x 62 == 7936 bytes)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | Data to transfer to the ECU (62 bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Exit data transfer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-prog-datum-schreiben"></a>
### PROG_DATUM_SCHREIBEN

Schreiben der Programm datum Write the programming date

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROG_DATUM_TAG | int | Programm tag (1 -&gt; 31) Day of programming |
| PROG_DATUM_MON | int | Programm monat (1 -&gt; 12) Month of programming |
| PROG_DATUM_JAHR | int | Programm jahr - (2000 -&gt; 9999) Year of programming |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write program data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write program date response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read program date response |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer Read the VIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer VIN |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Schreiben der Fahrgestellnummer Write the VIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) VIN - stored as 17 ascii characters ( + 1 ascii checksum ) string can be 17 or 18 characters - if 18 the last character is ignored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write VIN telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write VIN response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read VIN response |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden Stop the diagnostic session

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (22 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [DIGITAL](#table-digital) (6 × 4)
- [ANALOG](#table-analog) (14 × 4)
- [FORTTEXTE](#table-forttexte) (8 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 22 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x11 | SERVICE NICHT UNTERSTÜTZT |
| 0x12 | SUB-FUNKTION NICHT UNTERSTÜTZT |
| 0x22 | Bedingung nicht korrekt |
| 0x31 | Anfrage außer Toleranz |
| 0x33 | Sicherheitszugang aberkannt / erforderlich |
| 0x35 | Ungültiger Schlüssel |
| 0x36 | Anzal der Versuche überschritten |
| 0x37 | Erforderliche Zeitverzögerung nicht abgelaufen |
| 0x40 | Hinunterladen nicht erlaubt |
| 0x41 | Unzulässiger Typ zum hinunterladen |
| 0x42 | Spezifizierte Adresse kann nicht hinuntergeladen werden |
| 0x50 | Hochladen nicht erlaubt |
| 0x52 | Hochladen von spezifizierte Adress nicht möglich |
| 0x53 | Die angefordrte Anzahl Bytes kann nicht hochgeladen werden |
| 0x78 | Anfoderung korrekt erhalten - Antwort noch offen |
| 0x79 | Inkorrekte BYTE Anzahl während Block Transfer |
| 0x80 | Service nicht unterstützt im aktuellen Diagnose Mode |
| 0x90 | Vorgang nicht ausgeführt |
| 0x91 | Ungültiges Nachrichten Format |
| 0xA0 | OKAY |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 56 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
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
| 0x28 | DODUCO =&gt; BERU |
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
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC |
| 0xFF | unbekannter Hersteller |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 6 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| IGNITION_ON | 13 | 0x01 | 0x01 |
| ENGINE_RUNNING | 13 | 0x02 | 0x02 |
| APPLICATION_RUNNING | 13 | 0x04 | 0x04 |
| SPEED_CONTROL_ENABLED | 13 | 0x08 | 0x08 |
| DIAGNOSTIC_CONTROL_MODE_ON | 13 | 0x10 | 0x10 |
| ?? | 0 | 0x00 | 0xFF |

<a id="table-analog"></a>
### ANALOG

Dimensions: 14 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| BATTERY_VOLTS | 0.1 | 0.0 | V |
| TEMPERATURE | 1.0 | -40.0 | Grad C |
| MOTOR_CURRENT | 0.5 | 0.0 | A |
| MOTOR_SPEED | 20.0 | 0.0 | min-1 |
| MOTOR_VOLTAGE | 0.1 | 0.0 | V |
| PWM_MOTOR_CONTROL | 0.39215686 | 0.0 | % |
| MOTOR_SPEED_CONTROL | 20.0 | 0.0 | min-1 |
| PWM_OUT | 0.39215686 | 0.0 | % |
| MOTOR_CURRENT_MAX | 0.5 | 0.0 | A |
| BATTERY_CURRENT_MAX | 0.5 | 0.0 | A |
| ENGINE_RUNNING_ANALOG | 0.08 | 0.0 | V |
| MOTOR_RESISTANCE | 0.78 | 0.0 | mOhms |
| EMF_COEF | 3.125 | 0.0 | min-1/V |
| Ungültige Ziffer | 0.0 | 0 |  |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 8 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5523 | Batterie Spannungsfehler |
| 0x5517 | Übertemperatur oder schlechtes Temperatursignal |
| 0x5531 | Verriegelungsschutz |
| 0x5550 | Motor Kurzschluß oder offener Stromkreis |
| 0x5529 | FET Kurzschluß oder offener Stromkreis |
| 0x5508 | Ungültiger Motorlauf |
| 0x5507 | Ungültige Motorspannung |
| 0xFFFF | Ungültiger Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | über max Schwellwert |
| 0x02 | unter min Schwellwert |
| 0x03 | kein siknal gefunden |
| 0x04 | ungültiges Signal |
| 0x05 | -- |
| 0x06 | Fehler momentan nicht vorhanden |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | -- |
| 0xFF | unbekannter Status |
