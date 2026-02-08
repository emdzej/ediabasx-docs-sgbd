# BC1.prg

- Jobs: [38](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BC1 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 2.5 |
| AUTHOR | SW-Style M.Rafferty, BMW TI-433 Robert Kuessel |
| COMMENT | Basierend auf V3.0/Datum 09.04.01 |
| PACKAGE | 0.08 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [START_DIAGNOSTICS](#job-start-diagnostics) - Obtain diagnostic seed and send key to begin diagnostics The ecu will lock if no diagnostic messages have been sent to it for 30 seconds
- [IDENT](#job-ident) - Identification data
- [READ_MANUFACTURER_DATA](#job-read-manufacturer-data) - Auslesen der Herstelldaten
- [READ_SIA_DATA](#job-read-sia-data) - Read Service information
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen FG-Nummer Read the VIN
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben der FG-Nummer Write the VIN
- [FS_LESEN](#job-fs-lesen) - Read internal and external faults
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [IS_LESEN](#job-is-lesen) - Read the alarm mislock and alarm trigger fault logs Auslesen der alarm Fehler speicher
- [READ_ALARM_MISLOCK](#job-read-alarm-mislock) - Read Alarm mislocks
- [READ_ALARM_TRIGGER](#job-read-alarm-trigger) - Read alarm triggers
- [SPEICHER_LESEN](#job-speicher-lesen) - Read memory by address Lesen des internen Speichers Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Write memory by address Schreiben des Speicherinhaltes
- [STEUERN_IOSTATES](#job-steuern-iostates) - Force Digital Output States
- [STEUERN_PWM_OUTPUTS](#job-steuern-pwm-outputs) - Force Digital Output States
- [STEUERN_STEPPER_MOTOR](#job-steuern-stepper-motor) - Force Stepper motor Output State
- [STEUERN_TILT_SENSOR](#job-steuern-tilt-sensor) - Force Tilt Sensor state
- [CLEAR_RF_BUFFERS](#job-clear-rf-buffers) - Clear the RF receive and status buffers
- [STATUS_ANALOG](#job-status-analog) - Read Analogue Input and Output States
- [STATUS_LIGHT_INPUTS](#job-status-light-inputs) - Read Lighting Digital Input States
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Read Digital Input States
- [STATUS_LIGHT_OUTPUTS](#job-status-light-outputs) - Read lighting Digital outputs
- [STATUS_DIGITAL_OUTPUTS](#job-status-digital-outputs) - Read Digital outputs
- [STATUS_RF](#job-status-rf) - Read the RF status
- [STATUS_TILT_SENSOR](#job-status-tilt-sensor) - Read the Tilt sensor status
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Ping message
- [SG_RESET](#job-sg-reset) - Reset the ECU
- [READ_PLIP_CODES](#job-read-plip-codes) - Read the codes and status for a specified plip location
- [WRITE_PLIP_CODES](#job-write-plip-codes) - Write the codes and status for a specified plip location
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and verify the coding data
- [LWR_ON](#job-lwr-on) - Switch on LWR2A
- [LWR_OFF](#job-lwr-off) - Switch on LWR2A
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden

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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-start-diagnostics"></a>
### START_DIAGNOSTICS

Obtain diagnostic seed and send key to begin diagnostics The ecu will lock if no diagnostic messages have been sent to it for 30 seconds

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Request seed response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Send key telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Send key response |

<a id="job-ident"></a>
### IDENT

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_SW_NR | int | Software version |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) 1, If AIF data is available |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-manufacturer-data"></a>
### READ_MANUFACTURER_DATA

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE5 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE6 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE7 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE8 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE9 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE10 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE11 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE12 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE13 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE14 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE15 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| SW_ID_NR | string | Software ID number in ROM |
| CHKSUM_RESULT | int | Checksum result |
| CHKSUM_BYTE_1 | unsigned char | Checksum byte 1 |
| CHKSUM_BYTE_2 | unsigned char | Checksum byte 2 |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read manufacturing data response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read software ID number response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read checksum result response |

<a id="job-read-sia-data"></a>
### READ_SIA_DATA

Read Service information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TOTAL_DISTANCE_WERT | long | Total Distance |
| TOTAL_DISTANCE_EINH | string | Total distance units km |
| CONSUMED_LITRES_SINCE_SERVICE_WERT | long | Count of litres |
| LAST_SERVICE_TYPE_OIL | int | 1 = Last service was an oil service, 0 = not |
| LAST_SERVICE_TYPE_INSPECTION | int | 1 = Last service was an inspection, 0 = not |
| TIME_SINCE_INSPECTION_SERVICE_WERT | long | Time count (at/since?) inspection |
| TIME_SINCE_INSPECTION_SERVICE_EINH | string | Einheit = Tage, days |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen FG-Nummer Read the VIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer Last digits of the VIN |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben der FG-Nummer Write the VIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Vehicle ID number Fahrgestellnummer 7 or 8 character string - if 8 characters the last is ignored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write VIN Telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write VIN response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read VIN response |

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
| F_ORT_TEXT | string | Fehlerort als Text Fault description See column "ORTTEXT" in table "FOrtTexte" |
| F_HFK | int | Fehlerhaeufigkeit Frequency |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Count of Environment Data Items per fault |
| F_ART_ANZ | int | Anzahl der Fehlerarten Count of additional fault status information |
| F_ART1_NR | int | 1. (einzige) Fehlerart Fault status 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text Fault status text 1 |
| F_LZ | int | Fehler alter Secondary frequency counter (age) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Clear block 0 response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Clear block 1 response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Clear block 2 response |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG Clear block 3 response |

<a id="job-is-lesen"></a>
### IS_LESEN

Read the alarm mislock and alarm trigger fault logs Auslesen der alarm Fehler speicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Infodaten pro Fehler als Hexcode Raw fault data from the ECU |
| F_ORT_NR | int | Index fuer Infoort Fault number = (raw fault code + block offset) |
| F_ORT_TEXT | string | Infoort als Text See table "IOrtTexte" column "ORTTEXT" |
| F_LZ | int | Fault age in AUX cycles Fehler alt |
| F_HFK | int | Fault age in AUX cycles Fehler alt |
| F_ART_ANZ | int | Anzahl der Infoarten Bereich: immer 0 Number of status strings = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 Number of environmental conditions = 0 |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read alarm mislocks response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read alarm triggers response |

<a id="job-read-alarm-mislock"></a>
### READ_ALARM_MISLOCK

Read Alarm mislocks

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MISLOCK_NR_1 | int | Mislock Fault number |
| MISLOCK_TEXT_1 | string | Mislock Fault description |
| MISLOCK_AGE_1 | int | Mislock Fault age |
| MISLOCK_NR_2 | int | Mislock Fault number |
| MISLOCK_TEXT_2 | string | Mislock Fault description |
| MISLOCK_AGE_2 | int | Mislock Fault age |
| MISLOCK_NR_3 | int | Mislock Fault number |
| MISLOCK_TEXT_3 | string | Mislock Fault description |
| MISLOCK_AGE_3 | int | Mislock Fault age |
| MISLOCK_NR_4 | int | Mislock Fault number |
| MISLOCK_TEXT_4 | string | Mislock Fault description |
| MISLOCK_AGE_4 | int | Mislock Fault age |
| MISLOCK_NR_5 | int | Mislock Fault number |
| MISLOCK_TEXT_5 | string | Mislock Fault description |
| MISLOCK_AGE_5 | int | Mislock Fault age |
| MISLOCK_NR_6 | int | Mislock Fault number |
| MISLOCK_TEXT_6 | string | Mislock Fault description |
| MISLOCK_AGE_6 | int | Mislock Fault age |
| MISLOCK_NR_7 | int | Mislock Fault number |
| MISLOCK_TEXT_7 | string | Mislock Fault description |
| MISLOCK_AGE_7 | int | Mislock Fault age |
| MISLOCK_NR_8 | int | Mislock Fault number |
| MISLOCK_TEXT_8 | string | Mislock Fault description |
| MISLOCK_AGE_8 | int | Mislock Fault age |
| MISLOCK_NR_9 | int | Mislock Fault number |
| MISLOCK_TEXT_9 | string | Mislock Fault description |
| MISLOCK_AGE_9 | int | Mislock Fault age |
| MISLOCK_NR_10 | int | Mislock Fault number |
| MISLOCK_TEXT_10 | string | Mislock Fault description |
| MISLOCK_AGE_10 | int | Mislock Fault age |
| MISLOCK_NR_11 | int | Mislock Fault number |
| MISLOCK_TEXT_11 | string | Mislock Fault description |
| MISLOCK_AGE_11 | int | Mislock Fault age |
| MISLOCK_NR_12 | int | Mislock Fault number |
| MISLOCK_TEXT_12 | string | Mislock Fault description |
| MISLOCK_AGE_12 | int | Mislock Fault age |
| MISLOCK_NR_13 | int | Mislock Fault number |
| MISLOCK_TEXT_13 | string | Mislock Fault description |
| MISLOCK_AGE_13 | int | Mislock Fault age |
| MISLOCK_NR_14 | int | Mislock Fault number |
| MISLOCK_TEXT_14 | string | Mislock Fault description |
| MISLOCK_AGE_14 | int | Mislock Fault age |
| MISLOCK_NR_15 | int | Mislock Fault number |
| MISLOCK_TEXT_15 | string | Mislock Fault description |
| MISLOCK_AGE_15 | int | Mislock Fault age |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-alarm-trigger"></a>
### READ_ALARM_TRIGGER

Read alarm triggers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ALARM_NR_1 | int | Alarm Fault number |
| ALARM_TEXT_1 | string | Alarm Fault description |
| ALARM_AGE_1 | int | Alarm Fault age |
| ALARM_NR_2 | int | Alarm Fault number |
| ALARM_TEXT_2 | string | Alarm Fault description |
| ALARM_AGE_2 | int | Alarm Fault age |
| ALARM_NR_3 | int | Alarm Fault number |
| ALARM_TEXT_3 | string | Alarm Fault description |
| ALARM_AGE_3 | int | Alarm Fault age |
| ALARM_NR_4 | int | Alarm Fault number |
| ALARM_TEXT_4 | string | Alarm Fault description |
| ALARM_AGE_4 | int | Alarm Fault age |
| ALARM_NR_5 | int | Alarm Fault number |
| ALARM_TEXT_5 | string | Alarm Fault description |
| ALARM_AGE_5 | int | Alarm Fault age |
| ALARM_NR_6 | int | Alarm Fault number |
| ALARM_TEXT_6 | string | Alarm Fault description |
| ALARM_AGE_6 | int | Alarm Fault age |
| ALARM_NR_7 | int | Alarm Fault number |
| ALARM_TEXT_7 | string | Alarm Fault description |
| ALARM_AGE_7 | int | Alarm Fault age |
| ALARM_NR_8 | int | Alarm Fault number |
| ALARM_TEXT_8 | string | Alarm Fault description |
| ALARM_AGE_8 | int | Alarm Fault age |
| ALARM_NR_9 | int | Alarm Fault number |
| ALARM_TEXT_9 | string | Alarm Fault description |
| ALARM_AGE_9 | int | Alarm Fault age |
| ALARM_NR_10 | int | Alarm Fault number |
| ALARM_TEXT_10 | string | Alarm Fault description |
| ALARM_AGE_10 | int | Alarm Fault age |
| ALARM_NR_11 | int | Alarm Fault number |
| ALARM_TEXT_11 | string | Alarm Fault description |
| ALARM_AGE_11 | int | Alarm Fault age |
| ALARM_NR_12 | int | Alarm Fault number |
| ALARM_TEXT_12 | string | Alarm Fault description |
| ALARM_AGE_12 | int | Alarm Fault age |
| ALARM_NR_13 | int | Alarm Fault number |
| ALARM_TEXT_13 | string | Alarm Fault description |
| ALARM_AGE_13 | int | Alarm Fault age |
| ALARM_NR_14 | int | Alarm Fault number |
| ALARM_TEXT_14 | string | Alarm Fault description |
| ALARM_AGE_14 | int | Alarm Fault age |
| ALARM_NR_15 | int | Alarm Fault number |
| ALARM_TEXT_15 | string | Alarm Fault description |
| ALARM_AGE_15 | int | Alarm Fault age |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Read memory by address Lesen des internen Speichers Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | length of data to read anzahl data lesen 1 - 32 bytes |
| ADRESSE | int | 16 bit ECU memory address EEPROM address range: 0x0C00 -&gt; 0x0FFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Write memory by address Schreiben des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_HIGH | int | gewuenschte Adresse high als Hexwert! Address high byte 0x00 -&gt; 0xFF |
| ADRESSE_LOW | int | gewuenschte Adresse low als Hexwert! Address low byte 0x00 -&gt; 0xFF |
| WERT | int | gewuenschter Wert als Hexwert! Single byte of data to write 0x00 -&gt; 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-iostates"></a>
### STEUERN_IOSTATES

Force Digital Output States

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Digital output to force, DOP_? Identifier "DOP_?" from "NAME" column in table "BITS" |
| EIN | int | 1 = ON, 0 = OFF 1 wenn einschalten / 0 wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read outputs response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Force outputs telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Force outputs response |

<a id="job-steuern-pwm-outputs"></a>
### STEUERN_PWM_OUTPUTS

Force Digital Output States

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | PWM output to force, AOP_? Identifier "AOP_?" from "NAME" column in table "Analog" Argument is case sensitive |
| EIN | int | 0 for OFF, any other value for ON '&gt; 0', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read PWM outputs response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Force PWM outputs telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Force PWM outputs response |

<a id="job-steuern-stepper-motor"></a>
### STEUERN_STEPPER_MOTOR

Force Stepper motor Output State

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN | int | 0 for START, any other value for STOP 0 fuer anfang, &gt;0 fuer halt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-tilt-sensor"></a>
### STEUERN_TILT_SENSOR

Force Tilt Sensor state

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN | int | 0 = OFF,      &gt;0 = ON '&gt;0', wenn ein / '0', wenn aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-clear-rf-buffers"></a>
### CLEAR_RF_BUFFERS

Clear the RF receive and status buffers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Read Analogue Input and Output States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read analogue inputs response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read PWM outputs response |
| STAT_AIP_EXT_5V_MON_WERT | real | Monitor the Switch 5V power |
| STAT_AIP_EXT_5V_MON_EINH | string |  |
| STAT_AIP_PASS_WIN_CURR_SENSE_WERT | real | Current sense to detect window stall |
| STAT_AIP_PASS_WIN_CURR_SENSE_EINH | string |  |
| STAT_AIP_WIN_RELAY_MON_WERT | real | Passenger and driver relay status |
| STAT_AIP_WIN_RELAY_MON_EINH | string |  |
| STAT_AIP_BLOWER_MOT_SENSE_WERT | real | Blower motor fault sense before A/C Switch on |
| STAT_AIP_BLOWER_MOT_SENSE_EINH | string |  |
| STAT_AIP_HEAD_LGT_LEVEL_SW_WERT | long | Switch to determine headlight level |
| STAT_AIP_HEAD_LGT_LEVEL_SW_EINH | string |  |
| STAT_AIP_MAIN_FLASH_SW_WERT | real | Switch to flash main beam |
| STAT_AIP_MAIN_FLASH_SW_EINH | string |  |
| STAT_AIP_MAIN_FLASH_SW_STATE | string | Switch to flash main beam |
| STAT_AIP_FT_WIPER_SENSE_WERT | real | Sense to detect fault in front wiper |
| STAT_AIP_FT_WIPER_SENSE_EINH | string |  |
| STAT_AIP_DRV_WIN_ANTITRAP_WERT | real | Anti trap monitoring of driver window lift |
| STAT_AIP_DRV_WIN_ANTITRAP_EINH | string |  |
| STAT_AIP_DRV_WIN_ANTITRAP_STATE | string | State of anti trap monitoring of driver window lift |
| STAT_AIP_DRV_WIN_CURR_SENSE_WERT | real | Current sense to detect window stall |
| STAT_AIP_DRV_WIN_CURR_SENSE_EINH | string |  |
| STAT_AIP_PASS_WIN_RELAY_MON_WERT | real | Diagnostic current monitor |
| STAT_AIP_PASS_WIN_RELAY_MON_EINH | string |  |
| STAT_AIP_LOCK_RELAY_MON_WERT | real | Central locking relay status |
| STAT_AIP_LOCK_RELAY_MON_EINH | string |  |
| STAT_AIP_EVAPORATOR_SENSE_WERT | real | Evaporation sensor |
| STAT_AIP_EVAPORATOR_SENSE_EINH | string |  |
| STAT_AIP_LOCK_RELAY_MON_2_WERT | real | Central locking status 2 |
| STAT_AIP_LOCK_RELAY_MON_2_EINH | string |  |
| STAT_AIP_INDICATOR_SW_WERT | real | Switch to change indicators |
| STAT_AIP_INDICATOR_SW_EINH | string |  |
| STAT_AIP_INDICATOR_SW_STATE | string | Indicator position |
| STAT_AIP_PASS_WIN_ANTITRAP_WERT | real | Anti trap monitoring of passenger window lift |
| STAT_AIP_PASS_WIN_ANTITRAP_EINH | string |  |
| STAT_AIP_PASS_WIN_ANTITRAP_STATE | string | State of anti trap monitoring of passenger window lift |
| STAT_AIP_BATT_VOLTS_MON_WERT | real | Main battery monitoring level |
| STAT_AIP_BATT_VOLTS_MON_EINH | string |  |
| STAT_AOP_MAP_READ_LGT_WERT | real | PWM output for map reading lights |
| STAT_AOP_MAP_READ_LGT_EINH | string |  |
| STAT_AOP_INTERIOR_LGT_WERT | real | PWM output for Interior lights |
| STAT_AOP_INTERIOR_LGT_EINH | string |  |
| STAT_AOP_MAIN_BEAM_WERT | real | PWM output for Main Beam |
| STAT_AOP_MAIN_BEAM_EINH | string |  |
| STAT_AOP_DIPPED_BEAM_WERT | real | PWM output for Dipped Beam |
| STAT_AOP_DIPPED_BEAM_EINH | string |  |

<a id="job-status-light-inputs"></a>
### STATUS_LIGHT_INPUTS

Read Lighting Digital Input States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIP_HAZARD_SW_ON | int | Switch input hazard switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_POSN_LGT_SW_ON | int | Switch input position lights 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_INT_LGT_SW_ON | int | Switch input interior light 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_FOG_SW_ON | int | Switch input rear fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_FOG_SW_ON | int | Switch input front fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DIPPED_BEAM_SW_ON | int | Switch input dipped beam 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_AUX_LGT_SW_ON | int | Switch input auxiliary lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_IND_SIGNAL_ON | int | Monitor the positive sense of indicator for sleep 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_IND_SIG_INVERTED_ON | int | Monitor the inverted sense of indicator for sleep 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LAMP_STATUS_ON | int | Indicator of the lamp status 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LH_DIR_IND_STATUS_ON | int | Monitor the left hand indicator 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RH_DIR_IND_STATUS_ON | int | Monitor the right hand indicator 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BRAKE_LAMP_STATUS_ON | int | Monitor the brake lamps 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Read Digital Input States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIP_DRV_KEY_SW_UNLK_ON | int | Driver key switch unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_KEY_SW_LK_ON | int | Driver key switch lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_DOOR_OPEN_ON | int | Driver door open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_DOOR_OPEN_ON | int | Passenger door open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_HT_FT_SCR_SW_ON | int | Heated front screen switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BONNET_SW_ON | int | Switch to detect the bonnet open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_OPEN_SW_ON | int | Switch to detect the boot open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_HANDLE_SW_ON | int | Switch input boot release motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_MASTER_LK_SW_ON | int | Switch input master lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_MASTER_UNLK_SW_ON | int | Switch input master unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_WIN_UP_SW_ON | int | Switch input driver window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_WIN_DOWN_SW_ON | int | Switch input driver window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_WIN_UP_SW_ON | int | Switch input passenger window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_WIN_DOWN_SW_ON | int | Switch input passenger window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_KEY_SW_LK_ON | int | Passenger key switch lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_KEY_SW_UNLK_ON | int | Passenger key switch unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_HT_RR_WIN_SW_ON | int | Switch input heated rear window 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_AUX_SW_ON | int | Auxiliary monitor from main ignition switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_POLL_SENSE_ON | int | Pollution sensor input, polluted air 1 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_ALARM_TILT_SW_ON | int | Alarm tilt sensor This output cannot be read from using read digital inputs command Use Tilt sensor status instead 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WASH_PUMP_ON | int | Switch for rear washer pump active 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_WASH_PUMP_ON | int | Switch input front washer pump active 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_INERTIA_SENSE_ON | int | Inertia sensor to detect unusual stop conditions 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_COL_SW_1_ON | int | Wiper switch 1 to activate front wipers 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_COL_SW_2_ON | int | Wiper switch 2 to activate front wipers 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WIPER_SW_ON | int | Rear wiper switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_AC_SWITCH_ON | int | Switch input air conditioning 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RECIRC_SW_ON | int | Toggles between recirc and fresh 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_WIPER_PARK_ON | int | Front wiper at the parked position 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WIPER_PARK_ON | int | Rear wiper at the parked position 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_KEY_IN_SW_ON | int | Switch input to detect key in ignition 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_POLICE_SW_ON | int | Switch input police functions 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LH_LATCH_ON | int | Switch input for left hand door latch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RH_LATCH_ON | int | Switch input for right hand door latch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RECIRC_MONITOR_ON | int | Recirc control monitor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_RELEASE_MONITOR_ON | int | Monitor the boot release 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BRAKE_SW_ON | int | Switch input brake pedal 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_ULTRASONIC_IN_ON | int | Ultrasonic alarm activated 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RF_CODE_LOGIC_ON | int | RF Code input 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RECIRC_ERROR_ON | int | Error with recirc control 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_REL_STATUS_ON | int | Monitor the boot release 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-light-outputs"></a>
### STATUS_LIGHT_OUTPUTS

Read lighting Digital outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DOP_RR_FOG_LED_ON | int | Rear fog LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_FOG_LGT_ON | int | Rear fog lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RH_INDICATOR_LGT_ON | int | Right hand indicator lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_LH_INDICATOR_LGT_ON | int | Left hand indicator lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RH_POSITION_LGT_ON | int | Right hand position lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_LH_POSITION_LGT_ON | int | Left hand position lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_FOG_LGT_RLY_ON | int | Front fog relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_NO_PLATE_LGT_ON | int | Number plate light 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-digital-outputs"></a>
### STATUS_DIGITAL_OUTPUTS

Read Digital outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DOP_DRV_LOCK_RLY_ON | int | Driver lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SUPER_LOCK_RLY_ON | int | Super lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_COMMON_LOCK_RLY_ON | int | Common relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_REST_LOCK_RLY_ON | int | Rest lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_DOWN_ON | int | Passenger window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_UP_ON | int | Passenger window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_DOWN_ON | int | Driver window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_UP_ON | int | Driver window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_RR_WIN_LED_ON | int | Heated rear window LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_FT_WIN_LED_ON | int | Heated front screen LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_AC_LED_ON | int | Air conditioning LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_LED_ON | int | Indicator for the recirc on 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_PARK_RUN_ON | int | Front wiper slow park run relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_RR_WIN_RLY_ON | int | Heated rear window relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_FT_WIN_RLY_ON | int | Heated front screen relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BBS_ARM_DISARM_ON | int | BBS arm/disarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SOUND_ALARM_ON | int | BBS version alarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_SLOW_FAST_ON | int | Front wiper slow fast relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BOOT_RELEASE_ON | int | Boot release motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_WATCHDOG_IN_ON | int | Handshake with hardware watchdog 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_CTL1_ON | int | Control 1 recirc operation 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_CTL2_ON | int | Control 2 recirc operation 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ROTARY_SUPPLY_ON | int | Supply to the rotary switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_AUX_RELAY_ON | int | Auxiliary relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PWR_WASH_RLY_ON | int | Powerwash relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_WIPER_RLY_ON | int | Rear wiper relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BLOWER_ENABLE_ON | int | Enable the blower motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_12V_EXT_PWR_ON | int | External switched 12V feed This output cannot be switched off via diagnostics 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ALARM_LED_ON | int | Alarm LED output 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-rf"></a>
### STATUS_RF

Read the RF status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LAST_RF_CODE | string | Last valid RF code received from plip |
| STAT_RF_REMOTE_OK_ROLLING_CODE_OK | int | Base and window code status 1 = Correct remote, correct rolling code (Correct base and window codes) |
| STAT_RF_REMOTE_OK_ROLLING_CODE_NOT_OK | int | Rolling code synchronisation status 1 = Rolling code out of synchronisation (Correct base code, incorrect window code) |
| STAT_RF_REMOTE_INCORRECT | int | Remote (Base) code status 1 = Incorrect remote (Incorrect base code), 0 = OK |
| STAT_RF_REMOTE_BATTERY_DEAD | int | Battery status 1 = Flat battery detected, 0 = OK |

<a id="job-status-tilt-sensor"></a>
### STATUS_TILT_SENSOR

Read the Tilt sensor status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TILT_SENSOR_PULSE_RECEIVED | int | Tilt sensor Pulse status 1 = Tilt sensor check pulse received, 0 = not received |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-plip-codes"></a>
### READ_PLIP_CODES

Read the codes and status for a specified plip location

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PLIP | unsigned int | Plip location to read 1 - 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CIPHER_KEY | string | Cipher code for required plip location |
| WINDOW_KEY | string | Window code for required plip location |
| BASE_CODE_KEY | string | Base code for required plip location |
| ENABLED | unsigned int | 0 = plip disabled, 1 = plip enabled |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-write-plip-codes"></a>
### WRITE_PLIP_CODES

Write the codes and status for a specified plip location

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PLIP | unsigned int | Plip location to write 1 - 4 |
| CIPHER_KEY | string | Cipher code for required plip location 16 characters ascii This is the ascii representation of the 8 hex characters used |
| WINDOW_KEY | string | Window code for required plip location 6 characters ascii This is the ascii representation of the 3 hex characters used |
| BASE_CODE_KEY | string | Base code for required plip location 6 characters ascii This is the ascii representation of the 3 hex characters used |
| ENABLE | unsigned int | 0 = plip disabled, 1 = plip enabled |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write PLIP telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write PLIP response packet |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read PLIP response packet |

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
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and verify the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write coding data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write coding data response cod_schreiben antwort |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read coding data response cod_lesen antwort |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-lwr-on"></a>
### LWR_ON

Switch on LWR2A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-lwr-off"></a>
### LWR_OFF

Switch on LWR2A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (63 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (58 × 2)
- [MORTTEXTE](#table-morttexte) (6 × 2)
- [AORTTEXTE](#table-aorttexte) (9 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [ANALOG](#table-analog) (21 × 5)
- [BITS](#table-bits) (98 × 5)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

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
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 63 rows × 2 columns

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
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
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

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 58 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | DATENBUS FEHLER |
| 0x01 | FAHRER-RELAIS NC FEHLER |
| 0x02 | GEMEINS. RELAIS NC FEHLER |
| 0x03 | RUHERELAIS NC FEHLER |
| 0x04 | SUPER-RELAIS NC FEHLER |
| 0x05 | FAH FEN HEBEN RELAIS NC FEHLER |
| 0x06 | FAH FEN HEBEN RELAIS NO FEHLER |
| 0x07 | FAH FEN SENKEN RELAIS NC FEHLER |
| 0x08 | FAH FEN SENKEN RELAIS NO FEHLER |
| 0x09 | BEIF FEN HEBEN RELAIS NC FEHLER |
| 0x0A | BEIF FEN HEBEN RELAIS NO FEHLER |
| 0x0B | BEIF FEN SENKEN RELAIS NC FEHLER |
| 0x0C | BEIF FEN SENKEN RELAIS NO FEHLER |
| 0x0D | FAHRER-RELAIS NO FEHLER |
| 0x0E | GEMEINS. RELAIS NO FEHLER |
| 0x0F | RUHERELAIS NO FEHLER |
| 0x10 | SUPER-RELAIS NO FEHLER |
| 0x80 | FAH FEN AUSGANG EIN FEHLER |
| 0x81 | BEIF FEN AUSGANG EIN FEHLER |
| 0x82 | FAH FEN AUSGANG AUS FEHLER |
| 0x83 | BEIF FEN AUSGANG AUS FEHLER |
| 0x84 | FRONTWISCHER EIN FEHLER |
| 0x85 | FRONTWISCHER GESCHW EIN FEHLER |
| 0x86 | FRISCHLUFT EIN FEHLER |
| 0x87 | UMLUFT EIN FEHLER O. FRISCHLUFT EIN FEHLER |
| 0x89 | HECKWISCHER EIN FEHLER |
| 0x8A | REGENSENSOR FEHLER |
| 0x8B | HHS EIN FEHLER |
| 0x8C | FRONTWISCHER AUS FEHLER |
| 0x8D | FRONTWISCHER GESCHW AUS FEHLER |
| 0x8E | FRISCHLUFT AUS FEHLER |
| 0x8F | UMLUFT AUS FEHLER |
| 0x91 | HECKWISCHER AUS FEHLER |
| 0x93 | HHS AUS FEHLER |
| 0x94 | FRONTWISCHER RÜCKMELD FEHLER |
| 0x95 | FRONTWISCHER BLOCKIERT FEHLER |
| 0x96 | HECKWISCHER BLOCKIERT FEHLER |
| 0x9A | KLIMAKOMPRESSOR FEHLER |
| 0x9B | HFS EIN FEHLER |
| 0x9C | HFS AUS FEHLER |
| 0xAA | BLINKER LINKS AUS FEHLER |
| 0xAC | BLINKER RECHTS AUS FEHLER |
| 0xB1 | NSW EIN FEHLER |
| 0xB2 | NSW AUS FEHLER |
| 0xB3 | ZUSATZLEUCHTE EIN FEHLER |
| 0xB4 | ZUSATZLEUCHTE AUS FEHLER |
| 0xB5 | GEBLÄSEMOTOR EIN FEHLER |
| 0xB6 | GEBLÄSEMOTOR AUS FEHLER |
| 0xBD | WASCHANLAGE EIN FEHLER |
| 0xBE | WASCHANLAGE AUS FEHLER |
| 0xBF | BBUS SCHÄRFEN ENTSCHÄRFEN EIN FEHLER |
| 0xC0 | BBUS SCHÄRFEN ENTSCHÄRFEN AUS FEHLER |
| 0xC1 | BBUS AKUST. ALARM EIN FEHLER |
| 0xC2 | BBUS AKUST. ALARM AUS FEHLER |
| 0xC4 | GEPÄCKR. ENTRIEG. AUS FEHLER |
| 0xC5 | FAH FEN EINKLEMMSCHUTZ FEHLER |
| 0xC6 | BEIF FEN EINKLEMMSCHUTZ FEHLER |
| 0xFF | Unbekannter Fehler |

<a id="table-morttexte"></a>
### MORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | FAH TÜR AUSL. |
| 0x01 | BEIF TÜR AUSL. |
| 0x02 | HAUBE AUSL. |
| 0x03 | GEPÄCKR. OFFEN AUSL. |
| 0x05 | ZV überbeanspr. |
| 0xFF | Unbekannter Fehler |

<a id="table-aorttexte"></a>
### AORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | NEBENVERBR.EIN AUSL. |
| 0x01 | ZÜNDG.EIN AUSL. |
| 0x02 | FAH TÜR AUSL. |
| 0x03 | BEIF TÜR AUSL. |
| 0x04 | ULTRASCHALL AUSL. |
| 0x05 | NEIG. AUSL. |
| 0x06 | HAUBE AUSL. |
| 0x07 | GEPÄCKR. OFFEN AUSL. |
| 0xFF | Unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler aktiv |
| 0x01 | Fehler inaktiv |
| 0xFF | Unbekannter Fehler |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x30 | Alarm-Fehlverriegelung - Fahrertür Eingang EIN |
| 0x31 | Alarm-Fehlverriegelung - Beifahrertür Eingang EIN |
| 0x32 | Alarm-Fehlverriegelung - Eingang Haube, Übergang EIN |
| 0x33 | Alarm-Fehlverriegelung - Gepäckraum-Entriegelungsschalter Eingang EIN |
| 0x35 | Alarm-Fehlverriegelung - Überhitzung ZV, Abschaltung ausgelöst |
| 0x40 | Alarmauslöser - Nebenverbraucher Eingang, Übergang auf EIN |
| 0x41 | Alarmauslöser - Zündung Eingang, Übergang auf EIN |
| 0x42 | Alarmauslöser - Fahrertür Eingang, Übergang auf EIN |
| 0x43 | Alarmauslöser - Beifahrertür Eingang, Übergang auf EIN |
| 0x44 | Alarmauslöser - Ultraschallzone 1 Eingang, Übergang auf EIN |
| 0x45 | Alarmauslöser - Neigung Eingang, Übergang auf EIN |
| 0x46 | Alarmauslöser - Haube Eingang, Übergang auf EIN |
| 0x47 | Alarmauslöser - Gepäckraum-Entriegelungsschalter Eingang, Übergang auf EIN |
| 0xXY | Unbekannter Fehler |

<a id="table-analog"></a>
### ANALOG

Dimensions: 21 rows × 5 columns

| NAME | FACT_A | FACT_B | EINH | DESCRIPTION |
| --- | --- | --- | --- | --- |
| AIP_EXT_5V_MON | 0.019607843 | 0.0 | V | Schalter Spannung 5V überwachen |
| AIP_PASS_WIN_CURR_SENSE | 0.171568627 | 0.0 | A | Stromfühler zum Erkennen einer Fensterblockierung |
| AIP_WIN_RELAY_MON | 1.0 | 0.0 |  | Status Fahrer-Relais |
| AIP_BLOWER_MOT_SENSE | 0.071568627 | 0.0 | V | Fehlerfühler Gebläsemotor vor A/C-Schalter EIN |
| AIP_HEAD_LGT_LEVEL_SW | 1.0 | 0.0 | Pos | Schalter Scheinwerferleuchtweite |
| AIP_MAIN_FLASH_SW | 0.019607843 | 0.0 | V | Schalter Lichthupe |
| AIP_FT_WIPER_SENSE | 0.080360012 | 0.0 | V | Geschwindigkeitserkennung Frontwischer |
| AIP_DRV_WIN_ANTITRAP | 0.019607843 | 0.0 | V | Überwachung Einklemmschutz Fensterheber |
| AIP_DRV_WIN_CURR_SENSE | 0.171568627 | 0.0 | A | Stromfühler zum Erkennen einer Fensterblockierung |
| AIP_PASS_WIN_RELAY_MON | 1.0 | 0.0 |  | Status Beifahrer-Relais |
| AIP_LOCK_RELAY_MON | 1.0 | 0.0 |  | Status 1 Relais/Zentralverriegelung |
| AIP_EVAPORATOR_SENSE | 0.356506238 | -29.3 | C | Verdampfertemperatursensor |
| AIP_LOCK_RELAY_MON_2 | 1.0 | 0.0 |  | Status 2 Relais/Zentralverriegelung |
| AIP_INDICATOR_SW | 0.019607843 | 0.0 | V | Blinkerschalter |
| AIP_PASS_WIN_ANTITRAP | 0.019607843 | 0.0 | V | Überwachung Einklemmschutz Fensterheber |
| AIP_BATT_VOLTS_MON | 0.072087658 | 0.0 | V | Überwachungsebene Hauptbatterie |
| AOP_MAP_READ_LGT | 1.0 | 0.0 |  | Kartenleseleuchten |
| AOP_INTERIOR_LGT | 1.0 | 0.0 |  | Innenlichtschalter |
| AOP_MAIN_BEAM | 1.0 | 0.0 |  | Fernlicht |
| AOP_DIPPED_BEAM | 1.0 | 0.0 |  | Abblendlicht |
| Unbekannter Gegenstand | 0.0 | 0 |  | Unbekannter Gegenstand |

<a id="table-bits"></a>
### BITS

Dimensions: 98 rows × 5 columns

| NAME | BYTE | MASK | VALUE | DESCRIPTION |
| --- | --- | --- | --- | --- |
| DIP_DRV_KEY_SW_UNLK | 4 | 0x02 | 0x02 | Schlüsselkontakt Fahrer entrieg. |
| DIP_DRV_KEY_SW_LK | 4 | 0x04 | 0x04 | Schlüsselkontakt Fahrer verrieg. |
| DIP_DRV_DOOR_OPEN | 4 | 0x08 | 0x08 | Fahrertür offen |
| DIP_PASS_DOOR_OPEN | 4 | 0x10 | 0x10 | Beifahrertür offen |
| DIP_HAZARD_SW | 4 | 0x20 | 0x20 | Schaltereingang Warnblinkschalter |
| DIP_HT_FT_SCR_SW | 4 | 0x40 | 0x40 | Schalter heizb. Frontscheibe |
| DIP_BONNET_SW | 4 | 0x80 | 0x80 | Schalter für offene Haube |
| DIP_BOOT_OPEN_SW | 5 | 0x02 | 0x02 | Schalter für offenen Gepäckraum |
| DIP_BOOT_HANDLE_SW | 5 | 0x04 | 0x04 | Schaltereingang Gepäckraum-Entriegelungsmotor |
| DIP_MASTER_LK_SW | 5 | 0x08 | 0x08 | Schaltereingang Hauptverriegelung |
| DIP_MASTER_UNLK_SW | 5 | 0x10 | 0x10 | Schaltereingang Hauptentriegelung |
| DIP_DRV_WIN_UP_SW | 5 | 0x20 | 0x20 | Schaltereingang Fenster/Fahrer heben |
| DIP_DRV_WIN_DOWN_SW | 5 | 0x40 | 0x40 | Schaltereingang Fenster/Fahrer senken |
| DIP_PASS_WIN_UP_SW | 5 | 0x80 | 0x80 | Schaltereingang Fenster/Beifahrer heben |
| DIP_PASS_WIN_DOWN_SW | 6 | 0x02 | 0x02 | Schaltereingang Fenster/Beifahrer senken |
| DIP_PASS_KEY_SW_LK | 6 | 0x04 | 0x04 | Schlüsselkontakt Beifahrer verrieg. |
| DIP_PASS_KEY_SW_UNLK | 6 | 0x08 | 0x08 | Schlüsselkontakt Beifahrer entrieg. |
| DIP_HT_RR_WIN_SW | 6 | 0x10 | 0x10 | Schaltereingang heizb. Heckscheibe |
| DIP_POSN_LGT_SW | 6 | 0x20 | 0x20 | Schaltereingang Standlicht |
| DIP_INT_LGT_SW | 6 | 0x40 | 0x40 | Schaltereingang Innenlicht |
| DIP_AUX_SW | 6 | 0x80 | 0x80 | Überwachung Nebenverbraucher von Hauptzündschalter |
| DIP_POLL_SENSE | 7 | 0x02 | 0x02 | Eingang Luftqualitätssensor, verschmutzte Luft 1 |
| DIP_RR_WASH_PUMP | 7 | 0x04 | 0x04 | Schalter für Heckscheibenwaschpumpe aktiv |
| DIP_ALARM_TILT_SW | 7 | 0x08 | 0x08 | Neigungsgeber Alarmanlage |
| DIP_INERTIA_SENSE | 7 | 0x40 | 0x40 | Trägheitssensor für ungewöhnliche Anhaltebedingungen |
| DIP_COL_SW_1 | 8 | 0x01 | 0x01 | Wischerschalter, zum Aktivieren der Frontwischer |
| DIP_COL_SW_2 | 8 | 0x02 | 0x02 | Wischerschalter, zum Aktivieren der Frontwischer |
| DIP_RR_WIPER_SW | 8 | 0x04 | 0x04 | Heckwischerschalter |
| DIP_AC_SWITCH | 8 | 0x08 | 0x08 | Schaltereingang Klimaanlage |
| DIP_RECIRC_SW | 8 | 0x10 | 0x10 | Umschalten zwischen Umluft und Frischluft |
| DIP_RR_FOG_SW | 8 | 0x20 | 0x20 | Schaltereingang Nebelschlussleuchten |
| DIP_FT_FOG_SW | 8 | 0x40 | 0x40 | Schaltereingang Nebelscheinwerfer |
| DIP_DIPPED_BEAM_SW | 8 | 0x80 | 0x80 | Schaltereingang Abblendlicht |
| DIP_FT_WIPER_PARK | 9 | 0x01 | 0x01 | Frontwischer in Parkstellung |
| DIP_RR_WIPER_PARK | 9 | 0x02 | 0x02 | Heckwischer in Parkstellung |
| DIP_KEY_IN_SW | 9 | 0x04 | 0x04 | Schalter nicht eingebaut |
| DIP_AUX_LGT_SW | 9 | 0x08 | 0x08 | Schalter nicht eingebaut |
| DIP_POLICE_SW | 9 | 0x10 | 0x10 | Schalter nicht eingebaut |
| DIP_LH_LATCH | 9 | 0x20 | 0x20 | Schalter nicht eingebaut |
| DIP_RH_LATCH | 9 | 0x40 | 0x40 | Schalter nicht eingebaut |
| DIP_FT_WASH_PUMP | 9 | 0x80 | 0x80 | Schaltereingang Frontscheibenwaschpumpe aktiv |
| DIP_LAMP_STATUS | 10 | 0x01 | 0x01 | Anzeige für Lampenstatus |
| DIP_RECIRC_MONITOR | 10 | 0x02 | 0x02 | Überwachung Umluftregler |
| DIP_BOOT_RELEASE_MONITOR | 10 | 0x04 | 0x04 | Überwachung der Gepäckraumentriegelung |
| DIP_BRAKE_SW | 10 | 0x08 | 0x08 | Schaltereingang Bremspedal |
| DIP_IND_SIGNAL | 10 | 0x10 | 0x10 | Überwachung des Plus-Fühlers für Sleep-Anzeige |
| DIP_IND_SIG_INVERTED | 10 | 0x20 | 0x20 | Überwachung des Invers-Fühlers für Sleep-Anzeige |
| DIP_ULTRASONIC_IN | 10 | 0x40 | 0x40 | Ultraschall-Alarm aktiviert |
| DIP_RF_CODE_LOGIC | 10 | 0x80 | 0x80 | Eingang Funksignalcode |
| DIP_BLOWER_MOTOR_STATUS | 11 | 0x01 | 0x01 | Anzeige für Gebläsemotorstatus |
| DIP_RECIRC_ERROR | 11 | 0x02 | 0x02 | Fehlfunktion des Umluftreglers |
| DIP_LH_DIR_IND_STATUS | 11 | 0x08 | 0x08 | Überwachung Blinker links |
| DIP_RH_DIR_IND_STATUS | 11 | 0x10 | 0x10 | Überwachung Blinker rechts |
| DIP_BRAKE_LAMP_STATUS | 11 | 0x40 | 0x40 | Überwachung Bremsleuchten |
| DIP_BOOT_REL_STATUS | 11 | 0x80 | 0x80 | Überwachung der Gepäckraumentriegelung |
| RF_REMOTE_OK_ROLLING_CODE_OK | 4 | 0x01 | 0x01 | Richtige Fernbedienung und richtige Codes |
| RF_REMOTE_OK_ROLLING_CODE_NOT_OK | 4 | 0x02 | 0x02 | Richtige Fernbedienung und ungültiger alternierender Code |
| RF_REMOTE_INCORRECT | 4 | 0x03 | 0x03 | Falsche Fernbedienung verwendet |
| RF_REMOTE_BATTERY_DEAD | 4 | 0x10 | 0x10 | Zu schwache oder keine Batterie in Fernbedienung |
| TILT_SENSOR_PULSE_RECEIVED | 4 | 0x01 | 0x01 | Vom Neigungsgeber empfangener Impuls i.O. |
| DOP_DRV_LOCK_RLY | 4 | 0x01 | 0x01 | Verriegelungsrelais Fahrer |
| DOP_SUPER_LOCK_RLY | 4 | 0x02 | 0x02 | Relais Entriegelungssperre |
| DOP_COMMON_LOCK_RLY | 4 | 0x04 | 0x04 | Gemeins. Relais |
| DOP_REST_LOCK_RLY | 4 | 0x08 | 0x08 | Relais Ruheverriegelung |
| DOP_PASS_WIN_DOWN | 4 | 0x10 | 0x10 | Fenster/Beifahrer senken |
| DOP_PASS_WIN_UP | 4 | 0x20 | 0x20 | Fenster/Beifahrer heben |
| DOP_DRV_WIN_DOWN | 4 | 0x40 | 0x40 | Fenster/Fahrer senken |
| DOP_DRV_WIN_UP | 4 | 0x80 | 0x80 | Fenster/Fahrer heben |
| DOP_HT_RR_WIN_LED | 5 | 0x04 | 0x04 | LED heizb. Heckscheibe |
| DOP_RR_FOG_LED | 5 | 0x08 | 0x08 | Anzeige Nebelschlussleuchte |
| DOP_HT_FT_WIN_LED | 5 | 0x10 | 0x10 | LED HFS |
| DOP_AC_LED | 5 | 0x20 | 0x20 | LED A/C |
| DOP_RR_FOG_LGT | 5 | 0x40 | 0x40 | Nebelschlussleuchten |
| DOP_RECIRC_LED | 5 | 0x80 | 0x80 | Anzeige für Umluft EIN |
| DOP_RH_INDICATOR_LGT | 6 | 0x20 | 0x20 | Blinker rechts |
| DOP_LH_INDICATOR_LGT | 6 | 0x40 | 0x40 | Blinker links |
| DOP_BBS_ARM_DISARM | 6 | 0x80 | 0x80 | BBS schärfen/entschärfen |
| DOP_LH_POSITION_LGT | 7 | 0x10 | 0x10 | Standlicht links |
| DOP_RH_POSITION_LGT | 7 | 0x20 | 0x20 | Standlicht rechts |
| DOP_FT_WIPER_PARK_RUN | 8 | 0x01 | 0x01 | Frontwischer, Relais, Langsamlauf in Parkstellung |
| DOP_PWR_WASH_RLY | 8 | 0x02 | 0x02 | Relaisspule, Waschanlage |
| DOP_HEATED_RR_WIN_RLY | 8 | 0x04 | 0x04 | Relaisspule, heizb. Heckscheibe |
| DOP_HEATED_FT_WIN_RLY | 8 | 0x08 | 0x08 | Relaisspule, HFS |
| DOP_FT_FOG_LGT_RLY | 8 | 0x10 | 0x10 | Relaisspule, Nebelscheinwerfer |
| DOP_AUX_RELAY | 8 | 0x20 | 0x20 | Relaisspule, Nebenverbraucher |
| DOP_FT_WIPER_SLOW_FAST | 8 | 0x40 | 0x40 | Langsam/Schnell-Relais Frontwischer |
| DOP_RR_WIPER_RLY | 8 | 0x80 | 0x80 | Relaisspule, Heckwischer |
| DOP_NO_PLATE_LGT | 9 | 0x01 | 0x01 | Kennzeichenleuchte |
| DOP_BOOT_RELEASE | 9 | 0x02 | 0x02 | Gepäckraum-Entriegelungsmotor |
| DOP_WATCHDOG_IN | 9 | 0x04 | 0x04 | Handshake mit Hardware-Watchdog |
| DOP_RECIRC_CTL1 | 9 | 0x08 | 0x08 | Steuerung Umluftbetrieb |
| DOP_RECIRC_CTL2 | 9 | 0x10 | 0x10 | Steuerung Umluftbetrieb |
| DOP_ROTARY_SUPPLY | 9 | 0x80 | 0x80 | Speisung an Drehschalter |
| DOP_SOUND_ALARM | 11 | 0x01 | 0x01 | BBS Version Alarm |
| DOP_BLOWER_ENABLE | 11 | 0x04 | 0x04 | Aktivieren des Gebläsemotors |
| DOP_12V_EXT_PWR | 11 | 0x20 | 0x20 | Extern geschaltete 12V-Speisung |
| DOP_ALARM_LED | 11 | 0x40 | 0x40 | Ausgang Alarm-LED |
| XY | XY | 0xXY | 0xXY | Unbekannter Gegenstand |
