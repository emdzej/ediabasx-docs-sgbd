# DSP2.prg

- Jobs: [24](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DSP2-Booster |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.9 |
| AUTHOR | TI-431 Spoljarec, TI-431 Krueger, TI-431 Mellersh, BMW TI-431 Rochal |
| COMMENT | DSP2 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer DSP-Booster E38
- [IDENT](#job-ident) - Ident-Daten fuer DSP
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STATUS_IO_LINES](#job-status-io-lines) - Auslesen einiger interner Statusleitungen
- [STATUS_SG](#job-status-sg) - Auslesen interner Stati
- [STATUS_DSP_ON](#job-status-dsp-on) - Auslesen DS on/off
- [STATUS_DSP_VOLUME](#job-status-dsp-volume) - Auslesen Lautstaerke
- [STATUS_QUELLE](#job-status-quelle) - Auslesen DSP Tonquelle
- [STATUS_LOUDNESS](#job-status-loudness) - Auslesen loudness on / off
- [STATUS_BALANCE](#job-status-balance) - Auslesen Einstellung Balance
- [STATUS_FADER](#job-status-fader) - Auslesen Einstellung Fader
- [STATUS_BASS](#job-status-bass) - Auslesen Einstellung Bass
- [STATUS_TREBLE](#job-status-treble) - Auslesen Einstellung Bass
- [STATUS_GAL](#job-status-gal) - Auslesen der GAL-Einstellung
- [RESET](#job-reset) - Loest einen Reset des Verstaerkers aus
- [STEUERN_DSP](#job-steuern-dsp) - DSP Einstellungen veraendern
- [DSP_SELBSTTEST](#job-dsp-selbsttest) - startet den Digitalteil selbsttest (!anschliessend FS-lesen notwendig)
- [LAUTSPRECHER_TEST_START](#job-lautsprecher-test-start) - startet die zyklische Ansteuerung aller 4 Kanaele mit verschiedenen Frequenzen
- [LAUTSPRECHER_TEST_ENDE](#job-lautsprecher-test-ende) - beendet die zyklische Ansteuerung aller 4 Kanaele
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FG_LESEN](#job-fg-lesen) - Auslesen der Fahrgestellnummer

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

Init-Job fuer DSP-Booster E38

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DSP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_TEXT | string | Lieferantenname |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart (entweder 0 oder 32) |
| F_ART1_TEXT | string | 1. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-io-lines"></a>
### STATUS_IO_LINES

Auslesen einiger interner Statusleitungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_CD_SS | int | 1-&gt; kein auswertbares Signal am CD-Eingang, sonst 0 |
| STAT_TEMP1 | int | 1-&gt; Temperaturschwelle 1 ueberschritten, sonst 0 |
| STAT_TEMP2 | int | 1-&gt; Temperaturschwelle 2 ueberschritten, sonst 0 |

<a id="job-status-sg"></a>
### STATUS_SG

Auslesen interner Stati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_TEMP_WERT | int | Temperatur am internen Kuehlkoerper |
| STAT_TEMP_EINH | string | Einheit der Kuehlkoerpertemperatur |
| STAT_HARDWAREVERSION | int | Hardwareversion |
| STAT_SOFTWAREVERSION | int | Softwareversion |
| STAT_DSP | int | ????? |

<a id="job-status-dsp-on"></a>
### STATUS_DSP_ON

Auslesen DS on/off

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_DSP_ON | int | 0:DSP aus, 1:DSP an |

<a id="job-status-dsp-volume"></a>
### STATUS_DSP_VOLUME

Auslesen Lautstaerke

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_VOLUME | int | Volume in dB (0 = maximum) |

<a id="job-status-quelle"></a>
### STATUS_QUELLE

Auslesen DSP Tonquelle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_QUELLE | int | Tonquelle |
| STAT_QUELLE_TEXT | string | Tonquelle table QUELLE ORT |

<a id="job-status-loudness"></a>
### STATUS_LOUDNESS

Auslesen loudness on / off

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LOUDNESS_ON | int | 0: loudness off, 1: loudness on |

<a id="job-status-balance"></a>
### STATUS_BALANCE

Auslesen Einstellung Balance

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BALANCE | int | Einstellung der Balance (-16 rechts...links +16) |

<a id="job-status-fader"></a>
### STATUS_FADER

Auslesen Einstellung Fader

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_FADER | int | Einstellung des Faders (-16 hinten...vorne +16) |

<a id="job-status-bass"></a>
### STATUS_BASS

Auslesen Einstellung Bass

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BASS | int | Einstellung des Basses (-16 ... +16) |

<a id="job-status-treble"></a>
### STATUS_TREBLE

Auslesen Einstellung Bass

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_TREBLE | int | Einstellung der Hoehen (-16 ... +16) |

<a id="job-status-gal"></a>
### STATUS_GAL

Auslesen der GAL-Einstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_GAL | int | Einstellung der GAL (1 ... 6) |

<a id="job-reset"></a>
### RESET

Loest einen Reset des Verstaerkers aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-dsp"></a>
### STEUERN_DSP

DSP Einstellungen veraendern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNCTION | string | Funktion die beeinflusst werden soll table STEUERN FUNKTION |
| PARAMETER | string | DSP: 0=Off  1=On VOLUME: 0(max)-255 QUELLE table QUELLE ORT LOUDNESS: 0=Off  1=On BALANCE: -16 - +16 FADER: -16 - +16 BASS: -16 - +16 TREBLE: -16 - +16 GAL: 1 - 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-dsp-selbsttest"></a>
### DSP_SELBSTTEST

startet den Digitalteil selbsttest (!anschliessend FS-lesen notwendig)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-lautsprecher-test-start"></a>
### LAUTSPRECHER_TEST_START

startet die zyklische Ansteuerung aller 4 Kanaele mit verschiedenen Frequenzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-lautsprecher-test-ende"></a>
### LAUTSPRECHER_TEST_ENDE

beendet die zyklische Ansteuerung aller 4 Kanaele

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-fg-lesen"></a>
### FG_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [FORTTEXTE](#table-forttexte) (12 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (9 × 2)
- [QUELLE](#table-quelle) (8 × 2)

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

Dimensions: 59 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 12 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Fehler DSP Funktion links |
| 0x02 | Fehler DSP Funktion rechts |
| 0x03 | Fehler externes RAM links |
| 0x04 | Fehler externes RAM rechts |
| 0x05 | DSP konnte nicht initialisiert werden |
| 0x06 | Unterspannung Klemme 30 bei Selbsttest erkannt |
| 0x07 | Unterspannung Radio ein bei Selbsttest erkannt |
| 0x08 | Uebertemperatur SW-Kanal abgeschaltet |
| 0x09 | Checksummenfehler im internen EEPROM (UTL) |
| 0x10 | Checksummenfehler im externen EEPROM (UTL) |
| 0x11 | Checksummenfehler im externen EEPROM (BMW) |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 9 rows × 2 columns

| FUNKTION | CTRL_BYTE |
| --- | --- |
| DSP | 0x00 |
| VOLUME | 0x01 |
| QUELLE | 0x02 |
| LOUDNESS | 0x03 |
| BALANCE | 0x04 |
| FADER | 0x05 |
| BASS | 0x06 |
| TREBLE | 0x07 |
| GAL | 0x08 |

<a id="table-quelle"></a>
### QUELLE

Dimensions: 8 rows × 2 columns

| ORT | CTRL_BYTE |
| --- | --- |
| CD | 0x00 |
| TUNER/TAPE | 0x01 |
| TMC | 0x07 |
| -- | 0x0F |
| NAVI | 0x02 |
| TV/VCR | 0x03 |
| GONG | 0x06 |
| unknown source | 0xXY |
