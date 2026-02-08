# JNAV_CE2.prg

- Jobs: [30](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Japan Navigation 2 I-Bus |
| ORIGIN | BMW EI-44 Eva Kroll |
| REVISION | 6.000 |
| AUTHOR | ALPINE AOEUR H.Nordalm, ALPINE AOGE-MN G.Grieser, ALPINE AOGE-MN P.Dünzelmann, ALPINE AOGE-MN J.Schmöller |
| COMMENT | N/A |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete Reset ausloesen
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen low-Konzept (lower als Lastenheft Codierung/Diagnose)
- [SELFTEST](#job-selftest) - Start of the selftest
- [SELFTEST_2](#job-selftest-2) - Start of Selftest 2
- [STATUS_MAP_VERSION](#job-status-map-version) - Ident-Daten of the JNAV
- [STATUS_SW_CNS_IPL](#job-status-sw-cns-ipl) - SW Version of the CNS2 Bootloader
- [STATUS_SW_MAIN_IPL](#job-status-sw-main-ipl) - SW Version of the NAVI IPLs
- [STATUS_SW_APL](#job-status-sw-apl) - SW Version of the APL
- [STATUS_SW_NAVI](#job-status-sw-navi) - SW Version of Navigation
- [STATUS_SW_KERNEL](#job-status-sw-kernel) - SW Version of Kernel
- [STATUS_SW_CNS2](#job-status-sw-cns2) - SW Version of the CNS
- [STATUS_SW_VICS](#job-status-sw-vics) - SW Version of the VICS Receivers
- [STATUS_GPS_CONNECTION](#job-status-gps-connection) - Connection-status between GPS-Antenna and JNAV-CE Modus  : Default
- [STATUS_VICS_FM_CONNECTION](#job-status-vics-fm-connection) - Connection-Status between internal VICS-Receiver and JNAV-CE Modus  : Default
- [STATUS_ETC](#job-status-etc) - ETC connection test Modus  : Default
- [STEUERN_VOICE_TEST](#job-steuern-voice-test) - starten der Sprach-Ausgabe Modus  : Default
- [STATUS_SPEEDPULSE](#job-status-speedpulse) - Geschwindigkeit vom SpeedPulse-Sensor Modus  : Default
- [STEUERN_FLASHING_FROM_PCMCIA](#job-steuern-flashing-from-pcmcia) - starten des Flashvorgangs über PCMCIA-Interface Modus  : Default
- [STEUERN_VIN_WRITE](#job-steuern-vin-write) - Write VIN into ECU DS2: 	   $1F SweepingTechnologies $E5 SWTSetFZG
- [STATUS_VIN](#job-status-vin) - Read VIN in ECU DS2: 	   $1F SweepingTechnologies $E6 SWTGetFZG
- [STATUS_SERIALNUMBER_READ](#job-status-serialnumber-read) - Serial number of the JNAV
- [STATUS_FREISCHALTUNG](#job-status-freischaltung) - SWT Enable status of JNav DS2: 	   $1F SweepingTechnologies $F6 SWTGetStatus
- [STATUS_FLASHING_FROM_PCMCIA](#job-status-flashing-from-pcmcia) - Status of the flashing procsess

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

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-selftest"></a>
### SELFTEST

Start of the selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR |
| _TEL_ANTWORT | binary |  |

<a id="job-selftest-2"></a>
### SELFTEST_2

Start of Selftest 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR |
| _TEL_ANTWORT | binary |  |

<a id="job-status-map-version"></a>
### STATUS_MAP_VERSION

Ident-Daten of the JNAV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (e.g. ACK) |
| STAT_MAP_NR | string | Map-Software-Version |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sw-cns-ipl"></a>
### STATUS_SW_CNS_IPL

SW Version of the CNS2 Bootloader

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (e.g. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW Version of the CNS2 Bootloader |

<a id="job-status-sw-main-ipl"></a>
### STATUS_SW_MAIN_IPL

SW Version of the NAVI IPLs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW Version of the NAVI IPLs |

<a id="job-status-sw-apl"></a>
### STATUS_SW_APL

SW Version of the APL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW Version of the APL |

<a id="job-status-sw-navi"></a>
### STATUS_SW_NAVI

SW Version of Navigation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW version of navigation |

<a id="job-status-sw-kernel"></a>
### STATUS_SW_KERNEL

SW Version of Kernel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW Version of Kernel |

<a id="job-status-sw-cns2"></a>
### STATUS_SW_CNS2

SW Version of the CNS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of the Communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW-Version of the CNS |

<a id="job-status-sw-vics"></a>
### STATUS_SW_VICS

SW Version of the VICS Receivers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of the Communication (z.B. ACK) |
| STAT_SW | string | Softwarenumber |
| _TEL_ANTWORT | binary | SW Version of the CICS Receivers |

<a id="job-status-gps-connection"></a>
### STATUS_GPS_CONNECTION

Connection-status between GPS-Antenna and JNAV-CE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error table JobResult STATUS_TEXT |
| STAT_CONNECTION_STATUS | string | Connection Status between GPS-Antenna and JNAV-CE |
| STAT_CONNECTION_STATUS_WERT | int | Information of status from GPS-connection 0 = GPS Antenne nicht angeschlossen (offen) 1 = GPS Antenne Kurzschluss 2 = GPS Antenne angeschlossen &gt;2 = Unblausible Werte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vics-fm-connection"></a>
### STATUS_VICS_FM_CONNECTION

Connection-Status between internal VICS-Receiver and JNAV-CE Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENCY | int | e.g.: 0x2345 correspond to 23,45 MHz |
| SIGNAL_LEVEL | int | Unit 3,2 mV e.g.: 0x01D0 correspond to 1495,3 mV |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error table JobResult STATUS_TEXT |
| STAT_ANTENNE_STATUS | string | Connection-Status between internal VICS-Receiver and JNAV-CE |
| STAT_ANTENNE_STATUS_WERT | int | Information of status from FM-connection 0 = FM Antenne nicht gesteckt 1 = FM Antenne gesteckt &gt;1 = Unblausible Werte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-etc"></a>
### STATUS_ETC

ETC connection test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ETC | string | Status of GPS connection |
| STAT_ETC_WERT | int | Information of status from GPS-connection 0 = Keine Verbindung zum ETC 1 = ETC Verbindung ok &gt;1 = Unblausible Werte |
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

<a id="job-status-speedpulse"></a>
### STATUS_SPEEDPULSE

Geschwindigkeit vom SpeedPulse-Sensor Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPEEDPULSE_WERT | int | Geschwindigkeit vom SpeedPulse-Sensor |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flashing-from-pcmcia"></a>
### STEUERN_FLASHING_FROM_PCMCIA

starten des Flashvorgangs über PCMCIA-Interface Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vin-write"></a>
### STEUERN_VIN_WRITE

Write VIN into ECU DS2: 	   $1F SweepingTechnologies $E5 SWTSetFZG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | 7 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs table SwtFehler_Tab STATUS_TEXT possible error codes UNKNOWN ERROR |
| JOB_STATUS_CODE | string | 1 Byte Hex Format Entrypoint in table SwtFehler |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-answer of ECU |

<a id="job-status-vin"></a>
### STATUS_VIN

Read VIN in ECU DS2: 	   $1F SweepingTechnologies $E6 SWTGetFZG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, i fno error occurs table SwtFehler_Tab STATUS_TEXT Possible errorcodes UNKNOWN ERROR |
| STAT_JOB_STATUS_CODE | string | 1 Byte Hex Format Entrypoint in table SwtFehler |
| STAT_VIN | string | VIN 17 Bytes or 7 Bytes |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-serialnumber-read"></a>
### STATUS_SERIALNUMBER_READ

Serial number of the JNAV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (e.g. ACK) |
| STAT_SN | string | Serial number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-freischaltung"></a>
### STATUS_FREISCHALTUNG

SWT Enable status of JNav DS2: 	   $1F SweepingTechnologies $F6 SWTGetStatus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error Possible Error Codes UNKNOWN ERROR SW NOT ACTIVATED |
| STAT_JOB_STATUS_CODE | int | 0x00, if no error |
| STAT_FSCENABLER | int | FSC-Status of SW-ID "00100001" |
| STAT_FSCENABLER_TEXT | string | FSC-Status of SW-ID "00100001" |
| STAT_FSCSHORT | int | FSC-Status of SW-ID "0008xxxx" |
| STAT_FSCSHORT_TEXT | string | FSC-Status of SW-ID "0008xxxx" |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flashing-from-pcmcia"></a>
### STATUS_FLASHING_FROM_PCMCIA

Status of the flashing procsess

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status of Communication (z.B. ACK) |
| STAT_FLASHING_FROM_PCMCIA | string | Status of flashing process |
| STAT_FLASHING_FROM_PCMCIA_WERT | int | Information of status of flashing from PCMCIA |
| _TEL_ANTWORT | binary | answer of ECU (hex value) |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (100 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (11 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)

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

Dimensions: 100 rows × 2 columns

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
| 0x18 | Continental Teves |
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
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
| 0x93 | TPO Display Corp. |
| 0x94 | KÜSTER Automotive Control |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental Automotive |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls |
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

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x02 | Interner VICS Empfänger gestört |
| 0x03 | I-Bus-Fehler |
| 0x04 | S-RAM-Fehler |
| 0x05 | V-RAM-Fehler |
| 0x06 | Interner GPS Empfänger gestört oder Verbindung zur GPS Antenne gestört |
| 0x07 | HDD-Lese-Fehler |
| 0x08 | Gyro-Fehler |
| 0x09 | Produktions-Mode an |
| 0x0A | Transport-Mode an |
| 0x0B | Werkstatt-Mode an |
| 0xXY | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |
