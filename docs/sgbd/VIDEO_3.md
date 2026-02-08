# VIDEO_3.prg

- Jobs: [13](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Videomodul 3 |
| ORIGIN | BMW TI-431 Krueger |
| REVISION | 1.0 |
| AUTHOR | BMW TI-433 Helmich, BMW TI-431 Krueger |
| COMMENT | VIDEO_3 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Videomodul TV-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Videomodul TV-Teil
- [Pruefstempel_lesen](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Daten in den Pruefstempel schreiben
- [Speicher_lesen](#job-speicher-lesen) - Lesen, welche Parameter geladen sind
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Selbsttest des Videomoduls
- [SG_STATUS_LESEN](#job-sg-status-lesen) - Stati lesen am Videomodul 3
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen im Videomodul TV-Teil
- [STEUERN_SLEEP_MODE](#job-steuern-sleep-mode) - Steuergeraet in Sleep-Mode versetzen
- [MABIKI_MODE_SCHREIBEN](#job-mabiki-mode-schreiben) - Umschreiben eines Bytes
- [CODIERUNG_LAENDERVARIANTE_LESEN](#job-codierung-laendervariante-lesen) - Speicher lesen EEPROM
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum: Woche |
| ID_DATUM_JAHR | string | Herstelldatum: Jahr |
| ID_LIEF_NR | string | Lieferant-Nummer |
| ID_LIEF_TEXT | string | Lieferant im Klartext |
| ID_SW_NR | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-lesen"></a>
### Pruefstempel_lesen

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Daten in den Pruefstempel schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| _TEL_SENDE | binary |  |

<a id="job-speicher-lesen"></a>
### Speicher_lesen

Lesen, welche Parameter geladen sind

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT_AUSWAHL | int | Angabe, welches Speichermedium ausgelesen werden soll |
| START_ADRESSE_HIGH | int | Startadresse high als Hexwert |
| START_ADRESSE_MIDDLE | int | Startadresse middle als Hexwert |
| START_ADRESSE_LOW | int | Startadresse low als Hexwert |
| ANZAHL_BYTE | int | Angabe, wieviele Bytes ausgelesen werden sollen maximale Anzahl 32 Byte, entspricht 20 Hex |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| SEGMENT_TEXT | string | Text Segmentauswahl |
| DATEN | binary | angeforderter Datenblock |
| BYTE_ANZAHL | int | Eingabe, wieviel Byte ausgelesen werden sollen |
| EINGABEFEHLER | string | Fehlertextausgabe bei Eingabe &gt;32 Byte |
| _TEL_SENDE | binary | gesendetes Telegramm |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Selbsttest des Videomoduls

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-status-lesen"></a>
### SG_STATUS_LESEN

Stati lesen am Videomodul 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_ROT_1_OUT | string | Ausgabe Testergebnis |
| STAT_ROT_1_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_GRUEN_1_OUT | string | Ausgabe Testergebnis |
| STAT_GRUEN_1_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_BLAU_1_OUT | string | Ausgabe Testergebnis |
| STAT_BLAU_1_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_ROT_EXT_IN | string | Ausgabe Testergebnis |
| STAT_ROT_EXT_IN_WERT | int | Ausgabe Testergebnis |
| STAT_GRUEN_EXT_IN | string | Ausgabe Testergebnis |
| STAT_GRUEN_EXT_IN_WERT | int | Ausgabe Testergebnis |
| STAT_BLAU_EXT_IN | string | Ausgabe Testergebnis |
| STAT_BLAU_EXT_IN_WERT | int | Ausgabe Testergebnis |
| STAT_FS | string | Fernspeisung, nur mit Navi |
| STAT_FS_WERT | int | Fernspeisung, nur mit Navi |
| STAT_XSYNC | string | nur mit Navi |
| STAT_XSYNC_WERT | int | nur mit Navi |
| STAT_ROT_2_OUT | string | Ausgabe Testergebnis |
| STAT_ROT_2_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_GRUEN_2_OUT | string | Ausgabe Testergebnis |
| STAT_GRUEN_2_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_BLAU_2_OUT | string | Ausgabe Testergebnis |
| STAT_BLAU_2_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_CVBS_TUNER | string |  |
| STAT_CVBS_TUNER_WERT | int |  |
| STAT_AF_KH_L | string | Kopfhoerer links |
| STAT_AF_KH_L_WERT | int | Kopfhoerer links |
| STAT_AF_KH_R | string | Kopfhoerer rechts |
| STAT_AF_KH_R_WERT | int | Kopfhoerer rechts |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen im Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-steuern-sleep-mode"></a>
### STEUERN_SLEEP_MODE

Steuergeraet in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-mabiki-mode-schreiben"></a>
### MABIKI_MODE_SCHREIBEN

Umschreiben eines Bytes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FZG_TYP | string | E38 oder E39 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-codierung-laendervariante-lesen"></a>
### CODIERUNG_LAENDERVARIANTE_LESEN

Speicher lesen EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_LAENDERVARIANTE_TEXT | string | ECE, GB , US oder unbekannt |
| COD_LAENDERVARIANTE_WERT | int |  |
| ID_COD_INDEX | int | aus Id-lesen |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", als Dummy |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [SEGMENTAUSWAHL](#table-segmentauswahl) (6 × 2)

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

<a id="table-segmentauswahl"></a>
### SEGMENTAUSWAHL

Dimensions: 6 rows × 2 columns

| SEGMENT | AUSWAHLTEXT |
| --- | --- |
| 0x02 | EPROM |
| 0x03 | EEPROM |
| 0x04 | internes RAM DATA |
| 0x05 | externes RAM XDATA |
| 0x0B | internes RAM IDATA |
| 0xXY | Unbekanntes Segment |
