# JNAV_CE.prg

- Jobs: [25](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | I-Bus Navigationssystem Japan (JNAV-CE) |
| ORIGIN | BMW EE-42 Alexander Maier |
| REVISION | 3.07 |
| AUTHOR | ALPINE Electronics H.Nordalm |
| COMMENT | N/A |
| PACKAGE | 1.23 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete Reset ausloesen
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen low-Konzept (lower als Lastenheft Codierung/Diagnose)
- [SELBSTTEST](#job-selbsttest) - Ausloesen des Selbsttest
- [SELBSTTEST_2](#job-selbsttest-2) - Ausloesen des Selbsttest 2
- [POWER_DOWN](#job-power-down) - Ausloesen des Power Down
- [VERSION_INFO](#job-version-info) - Ident-Daten fuer das JNAV
- [STATUS_SW_CNS_BOOTLOADER](#job-status-sw-cns-bootloader) - SW Version des CNS2 Bootloaders
- [STATUS_SW_NAVI_IPL](#job-status-sw-navi-ipl) - SW Version des NAVI IPLs
- [STATUS_SW_NAVI_BIOS](#job-status-sw-navi-bios) - SW Version des NAVI BIOS
- [STATUS_SW_APL](#job-status-sw-apl) - SW Version der APL
- [STATUS_SW_NAVI](#job-status-sw-navi) - SW Version der Navigation
- [STATUS_SW_NK](#job-status-sw-nk) - SW Version des NK
- [STATUS_SW_CNS](#job-status-sw-cns) - SW Version des CNS
- [STATUS_SW_VICS](#job-status-sw-vics) - SW Version des VICS Receivers
- [STATUS_GPS_CONNECTION](#job-status-gps-connection) - Verbindungs-Status zw. GPS-Antenne und JNAV-CE Modus  : Default
- [STATUS_VICS_FM_CONNECTION](#job-status-vics-fm-connection) - Verbindungs-Status zw. internem VICS-Receiver und JNAV-CE und JNAV-CE Modus  : Default
- [STATUS_SPEEDPULSE](#job-status-speedpulse) - Geschwindigkeit vom SpeedPulse-Sensor Modus  : Default
- [STATUS_ETC](#job-status-etc) - ETC connection test Modus  : Default
- [STEUERN_VOICE_TEST](#job-steuern-voice-test) - starten der Sprach-Ausgabe Modus  : Default

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

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete Reset ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen low-Konzept (lower als Lastenheft Codierung/Diagnose)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_ART_ANZ | int | immer 0 |
| F_UW_ANZ | int | immer 0 |
| F_HFK | int | immer 1 |
| _TEL_ANTWORT | binary |  |

<a id="job-selbsttest"></a>
### SELBSTTEST

Ausloesen des Selbsttest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary |  |

<a id="job-selbsttest-2"></a>
### SELBSTTEST_2

Ausloesen des Selbsttest 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary |  |

<a id="job-power-down"></a>
### POWER_DOWN

Ausloesen des Power Down

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME_TO_WAIT | int | Einheit: 500 ms 0 = 0 s 1 = 0,5 s 2 = 1 s .... 40 = 20 s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-version-info"></a>
### VERSION_INFO

Ident-Daten fuer das JNAV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_SW_NR | string | Navigations-Software-Version |
| ID_MAP_NR | string | Map-Software-Version |

<a id="job-status-sw-cns-bootloader"></a>
### STATUS_SW_CNS_BOOTLOADER

SW Version des CNS2 Bootloaders

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-navi-ipl"></a>
### STATUS_SW_NAVI_IPL

SW Version des NAVI IPLs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-navi-bios"></a>
### STATUS_SW_NAVI_BIOS

SW Version des NAVI BIOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-apl"></a>
### STATUS_SW_APL

SW Version der APL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-navi"></a>
### STATUS_SW_NAVI

SW Version der Navigation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-nk"></a>
### STATUS_SW_NK

SW Version des NK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-cns"></a>
### STATUS_SW_CNS

SW Version des CNS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-vics"></a>
### STATUS_SW_VICS

SW Version des VICS Receivers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_SW | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-status-gps-connection"></a>
### STATUS_GPS_CONNECTION

Verbindungs-Status zw. GPS-Antenne und JNAV-CE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CONNECTION_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vics-fm-connection"></a>
### STATUS_VICS_FM_CONNECTION

Verbindungs-Status zw. internem VICS-Receiver und JNAV-CE und JNAV-CE Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENCY | int | z.B.: 0x2345 entspricht 23,45 MHz |
| SIGNAL_LEVEL | int | Einheit 3,2 mV z.B.: 0x01D0 entspricht 1495,3 mV |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CONNECTION_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-speedpulse"></a>
### STATUS_SPEEDPULSE

Geschwindigkeit vom SpeedPulse-Sensor Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPEEDPULSE | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-etc"></a>
### STATUS_ETC

ETC connection test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ETC | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-voice-test"></a>
### STEUERN_VOICE_TEST

starten der Sprach-Ausgabe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [JOBRESULT](#table-jobresult) (13 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (11 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)

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

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x02 | Interner VICS Empfaenger gestoert |
| 0x03 | I-Bus-Fehler |
| 0x04 | S-RAM-Fehler |
| 0x05 | V-RAM-Fehler |
| 0x06 | Interner GPS Empfaenger gestoert oder Anschluss zur GPS Antenne gestoert |
| 0x07 | DVD-Lese-Fehler |
| 0x08 | Gyro-Fehler |
| 0x09 | Fertigungs-Mode an |
| 0x0A | Transport-Mode an |
| 0x0B | Werkstatt-Mode an |
| 0xXY | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |
