# BMBTR50.prg

- Jobs: [14](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BMBTR50 |
| ORIGIN | BMW TI-431 Stephan Krueger |
| REVISION | 1.07 |
| AUTHOR | Software-Style M.Rafferty,BMW TI-430 Thomas Buboltz |
| COMMENT | Version ? |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identification data
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels Read the Test Stamp
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Write the Test Stamp
- [READ_SYSTEM_PARAMETERS](#job-read-system-parameters) - Auslesen verschiedener Geraetestati Read door status, dimmer position and LCD operation times
- [FS_LESEN](#job-fs-lesen) - Read all faults
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Clear error memory
- [STATUS_ANALOG](#job-status-analog) - Status der Analogsignale auslesen Read Analogue Input and Output States
- [STATUS_LESEN_DREHGEBER](#job-status-lesen-drehgeber) - Stati lesen am Bordmitor Bedien-Teil
- [SLEEP_MODE](#job-sleep-mode) - Steuergeraet in Sleep-Mode versetzen Power down ECU
- [READ_LCD_OFFSET](#job-read-lcd-offset) - LC helligkeit abgleich auflesen Read the LCD brightness offset value
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

Identification data

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
| AENDERUNGS_INDEX | int | Change index |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels Read the Test Stamp

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Test Stamp byte 1 Pruefstempel Datenbyte1 |
| BYTE2 | int | Test Stamp byte 2 Pruefstempel Datenbyte2 |
| BYTE3 | int | Test Stamp byte 3 Pruefstempel Datenbyte3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Write the Test Stamp

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden (0x00-0xFF) you can use any value you like (0x00-0xFF) |
| BYTE2 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE3 | int | kann beliebig verwendet werden (0x00-0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-system-parameters"></a>
### READ_SYSTEM_PARAMETERS

Auslesen verschiedener Geraetestati Read door status, dimmer position and LCD operation times

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TUER_STATUS | int | Door status |
| DIMMERSTELLUNG | int | Position of dimmer, 1 Byte |
| LC_ANZEIGE_BETRIEBSSTUNDENZAEHLER | string | in Sekunden hexadezimal, 4 Byte LCD display - time of operation in seconds hex |
| LC_ANZEIGE_DAUER_UEBERTEMPERATUR | string | in Sekunden hexadezimal, 4 Byte LCD display - time of over temperature in seconds hex |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-lesen"></a>
### FS_LESEN

Read all faults

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
| F_ART_ANZ | int | Anzahl der Fehlerarten Count of additional fault status information |
| F_ART1_NR | int | 1. (einzige) Fehlerart Fault status 1 - only returned for LC Monitor over temperature fault |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text Fault status text 1 - only returned for LC Monitor over temperature fault |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_SENDE | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Clear error memory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status der Analogsignale auslesen Read Analogue Input and Output States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response packet - block 0 |
| STAT_LCD_BRIGHTNESS_WERT | real | LC helligkeit LCD brightness |
| STAT_LCD_BRIGHTNESS_EINH | string |  |
| STAT_CLAMP_30_WERT | real | Clamp 30 |
| STAT_CLAMP_30_EINH | string |  |
| STAT_LCD_TEMPERATURE_WERT | real | LCD temperature (not used for Display low (Arrow) ) |
| STAT_LCD_TEMPERATURE_EINH | string |  |
| STAT_PHOTO_SENSOR_WERT | real | Photo sensor (not used for Display low (Arrow) ) |
| STAT_PHOTO_SENSOR_EINH | string |  |
| STAT_CLAMP_R_ON | int | Status clamp R  1=ON 0=OFF |

<a id="job-status-lesen-drehgeber"></a>
### STATUS_LESEN_DREHGEBER

Stati lesen am Bordmitor Bedien-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEYBOARD_WERT | int | Tasten status 255 = keine Taste gedrueckt, 254 = mehrere Tasten gedrueckt Key status 255 = No key pressed, 254 = 2 or more keys pressed |
| STAT_KEYBOARD_TEXT | string | Description of keyboard status |
| STAT_MONITOR_DREHGEBER_SCHRITTE | int | Rotary encoder steps |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

Steuergeraet in Sleep-Mode versetzen Power down ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-lcd-offset"></a>
### READ_LCD_OFFSET

LC helligkeit abgleich auflesen Read the LCD brightness offset value

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| OFFSET_TYPE | int | 0=offset value added. 1=offset value divided |
| OFFSET_WERT | int | Value of the LCD Brightness offset |
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
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [FORTTEXTE](#table-forttexte) (7 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [ANALOG](#table-analog) (8 × 4)

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

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 67 rows × 2 columns

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
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Energiesparmode aktiv |
| 0x01 | Reset |
| 0x02 | LC MONITOR übertemperatur |
| 0x08 | K-BUS Sendefehler |
| 0x09 | K-BUS Empfangsfehler |
| 0x16 | EEPROM Checksumfehler |
| 0xFF | Unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler inaktiv |
| 0x01 | Fehler aktiv |
| 0xFF | Unbekannter Fehlerort |

<a id="table-analog"></a>
### ANALOG

Dimensions: 8 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| AIP_EXT_5V_MON | 1.0 | 0.0 |  |
| KEY_STATUS | 1.0 | 0.0 |  |
| ROTARY_ENCODER | 1.0 | 0.0 |  |
| LCD_BRIGHTNESS | 1.0 | 0.0 |  |
| CLAMP_30 | 0.1 | 0.0 |  |
| LCD_TEMPERATURE | 1.0 | 0.0 |  |
| PHOTO_SENSOR | 1.0 | 0.0 |  |
| Unknown item | 0.0 | 0 |  |
