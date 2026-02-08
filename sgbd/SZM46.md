# SZM46.prg

- Jobs: [11](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Schaltzentrum Mittelkonsole E46 |
| ORIGIN | BMW TI-433 Zhang |
| REVISION | 1.06 |
| AUTHOR | BMW TI-430 Drexel, Alps Lo |
| COMMENT | N/A |
| PACKAGE | 1.00 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [STATUS_IO](#job-status-io) - Status lesen
- [STEUERN_IO](#job-steuern-io) - Status vorgeben

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table FArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table IOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table IArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string | 17 Codierbytes in Hex |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TASTE_SITZHEIZUNG_LINKS_EIN | int | Taste Sitzheizung links |
| STAT_TASTE_SITZHEIZUNG_RECHTS_EIN | int | Taste Sitzheizung rechts |
| STAT_TASTE_SONNENROLLO_EIN | int | Taste Sonnenrollo |
| STAT_TASTE_SURROUND_EIN | int | Taste SURROUND |
| STAT_LED_SURROUND_EIN | int | LED SURROUND |
| STAT_FUNKTION_SURROUND_EIN | int | Funktion SURROUND |
| STAT_KLEMME_R_EIN | int | Status Klemme R |
| STAT_KLEMME_15_EIN | int | Status Klemme 15 |
| STAT_KLEMME_50_EIN | int | Status Klemme 50 |
| STAT_KLEMME_30_WERT | real | Spannung Klemme 30 |
| STAT_KLEMME_30_EINH | string | Volt |
| STAT_SONNENROLLO_AUF | int | Sonnenrollo Verstellung nach oben aktiv |
| STAT_SONNENROLLO_AB | int | Sonnenrollo Verstellung nach unten aktiv |
| STAT_TIST_SITZHEIZUNG_LINKS_WERT | real | Isttemperatur Sitzheizung links |
| STAT_TIST_SITZHEIZUNG_LINKS_EINH | string | Grad C |
| STAT_TIST_SITZHEIZUNG_RECHTS_WERT | real | Isttemperatur Sitzheizung rechts |
| STAT_TIST_SITZHEIZUNG_RECHTS_EINH | string | Grad C |
| STAT_LEISTUNG_SITZHEIZUNG_LINKS_WERT | int | Heizleistung Sitzheizung links |
| STAT_LEISTUNG_SITZHEIZUNG_LINKS_EINH | string | % |
| STAT_LEISTUNG_SITZHEIZUNG_RECHTS_WERT | int | Heizleistung Sitzheizung rechts |
| STAT_LEISTUNG_SITZHEIZUNG_RECHTS_EINH | string | % |
| STAT_MOTORSTROM_SONNENROLLO_WERT | real | Motorstrom Sonnenrollo |
| STAT_MOTORSTROM_SONNENROLLO_EINH | string | Ampere |
| STAT_SITZHEIZUNG_LINKS_STUFE | int | Sitzheizungsstufe links |
| STAT_SITZHEIZUNG_RECHTS_STUFE | int | Sitzheizungsstufe rechts |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-steuern-io"></a>
### STEUERN_IO

Status vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_ID | string | table IOStatus IO_ID_TEXT |
| IO_BYTE | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| AUFTRAG | binary | Auftragstelegramm |
| ANTWORT | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [IOSTATUS](#table-iostatus) (16 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [FORTTEXTE](#table-forttexte) (12 × 2)
- [IORTTEXTE](#table-iorttexte) (9 × 2)

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

Dimensions: 69 rows × 2 columns

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
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
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

<a id="table-iostatus"></a>
### IOSTATUS

Dimensions: 16 rows × 2 columns

| IO_ID | IO_ID_TEXT |
| --- | --- |
| 0x00 | Left_side_seat_heater_switch |
| 0x01 | Right_side_seat_heater_switch |
| 0x02 | Sunblind_switch |
| 0x03 | Surround_switch |
| 0x06 | Day/Night_change over |
| 0x07 | Terminal_50_status |
| 0x08 | Terminal_15_status |
| 0x09 | Terminal_R_status  |
| 0x10 | Right_side_seat_heater_bottom_LED |
| 0x11 | Right_side_seat_heater_middle_LED |
| 0x12 | Right_side_seat_heater_top_LED |
| 0x13 | Left_side_seat_heater_bottom_LED |
| 0x14 | Left_side_seat_heater_middle_LED |
| 0x15 | Left_side_seat_heater_top_LED |
| 0x16 | Surround_sound_LED |
| 0x17 | Surround_sound_output |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0x?? | unbekannte Fehlerart |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0x?? | unbekannte Fehlerart |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 12 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x001 | Klemme 30 nicht vorhanden |
| 0x002 | Sitzheizung links Kurzschluss oder Leitungsunterbrechung |
| 0x003 | Sitzheizung rechts Kurzschluss oder Leitungsunterbrechung |
| 0x004 | Temperatursensor Sitzheizung links Leitungsunterbrechung |
| 0x005 | Temperatursensor Sitzheizung links Kurzschluss gegen Masse |
| 0x006 | Temperatursensor Sitzheizung rechts Leitungsunterbrechung |
| 0x007 | Temperatursensor Sitzheizung rechts Kurzschluss gegen Masse |
| 0x008 | Heizflaeche Sitzheizung links Leitungsunterbrechung |
| 0x009 | Heizflaeche Sitzheizung rechts Leitungsunterbrechung |
| 0x00A | Sonnenrollo Motor, Leitungsunterbrechung |
| 0x00B | Sonnenrollo Motor, Kurzschluss |
| 0x??? | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x001 | Taster Sitzheizung links dauernd betaetigt |
| 0x002 | Taster Sitzheizung rechts dauernd betaetigt |
| 0x003 | Taster Sonnenrollo dauernd betaetigt |
| 0x004 | Taster HiFi System dauernd betaetigt |
| 0x005 | Sitzheizung Unterspannung erkannt |
| 0x006 | Sonnenrollo Unterspannung erkannt |
| 0x007 | Sitzheizung Ueberspannung erkannt |
| 0x008 | Sonnenrollo Ueberspannung erkannt |
| 0x??? | unbekannter Fehlerort |
