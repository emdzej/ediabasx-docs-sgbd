# EASY_E_F.prg

- Jobs: [17](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Einstiegshilfe Fahrerseite E46 |
| ORIGIN | BMW TI-431 Krueger |
| REVISION | 1.0 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-431 Krueger |
| COMMENT | Information |
| PACKAGE | 0.05 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer SM46 automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer das SM46
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrechterhalten
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des internen Speichers
- [STATUS_1_LESEN](#job-status-1-lesen) - Stati der Easy-Entry
- [STATUS_2_LESEN](#job-status-2-lesen) - Stati des SM46
- [STEUERN_IO](#job-steuern-io) - Ansteuern eines digitalen Einganges
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [VARIANTE_LESEN](#job-variante-lesen) - SG-Variante aus Zelle 0x0124 auslesen
- [SG_STATUS_LESEN](#job-sg-status-lesen) - auslesen der Systemstati aus dem Steuergeraet

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

Init-Job fuer SM46 automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer das SM46

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
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
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ | int | Gesamtzahl Fehler |
| F_ORT_NR | int | identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int |  |
| F_ART_ANZ | int | immer 1 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| F_UW_ANZ | int | immer 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers (2 Bytes) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_HIGH | int |  |
| ADRESSE_LOW | int |  |
| ANZAHL | int | 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATENFELD | binary | Ergebnisfeld mit 1 bis 16 Bytes |
| _TEL_ANTWORT | binary |  |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ZELLE | int | immer nur 1 Speicherzelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary |  |

<a id="job-status-1-lesen"></a>
### STATUS_1_LESEN

Stati der Easy-Entry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SCHALTER_SLV_VOR_EIN | int |  |
| STAT_SCHALTER_SLV_ZURUECK_EIN | int |  |
| STAT_EASY_ENTRY_EIN | int |  |
| STAT_RS_EIN | int |  |
| STAT_EE_SCHALTER_POS | int | 0=aus,1=vor,2=zurueck |
| STAT_POS_SLV_WERT | long |  |
| STAT_SCHALTER_SITZLAENGE | int | 0=aus,1=vor,2=zurueck |

<a id="job-status-2-lesen"></a>
### STATUS_2_LESEN

Stati des SM46

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SPANNUNG_HALLS_SLV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_KL30_WERT | real | Batterie-Spannung am SG |
| STAT_SPANNUNGEN_EINH | string | Einheit der Spannung |

<a id="job-steuern-io"></a>
### STEUERN_IO

Ansteuern eines digitalen Einganges

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| LOESCHDATUM_JAHR | int | letzte Stelle Jahreszahl fuer Loeschdatum Kundendienst |
| LOESCHDATUM_KW | int | KW der Fehlerspeicherloeschung fuer Kundendienst |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-variante-lesen"></a>
### VARIANTE_LESEN

SG-Variante aus Zelle 0x0124 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| SG_VARIANTE | string | Variante im Klartext |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-status-lesen"></a>
### SG_STATUS_LESEN

auslesen der Systemstati aus dem Steuergeraet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| SOFTSTOP_FAND_STATT | int | bei letzter Verstellung fand Softstop statt |
| BLOCKABSCHALTUNG_FAND_STATT | int | bei letzter Verstellung fand Blockabschaltung statt |
| TIPPTASTEN_BETRIEB_MOEGLICH | int |  |
| SLEEPMODE_MOEGLICH | int |  |
| BEIFAHRERTUER_OFFEN | int |  |
| FAHRERTUER_OFFEN | int |  |
| KLEMME_15_AKTIV | int |  |
| KLEMME_R_AKTIV | int |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (15 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (4 × 3)

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

Dimensions: 15 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Hallsensor Lehnenneigung, Kurzschluss nach Masse |
| 0x01 | Hallsensor Lehnenneigung, Unterbrechung |
| 0x02 | Hallsensor Lehnenneigung, Kurzschluss nach Ubatt |
| 0x03 | Hallsensor Sitzhoehe, Kurzschluss nach Masse |
| 0x04 | Hallsensor Sitzhoehe, Unterbrechung |
| 0x05 | Hallsensor Sitzhoehe, Kurzschluss nach Ubatt |
| 0x06 | Hallsensor Sitzneigung, Kurzschluss nach Masse |
| 0x07 | Hallsensor Sitzneigung, Unterbrechung |
| 0x08 | Hallsensor Sitzneigung, Kurzschluss nach Ubatt |
| 0x09 | Hallsensor Sitzschlitten, Kurzschluss nach Masse |
| 0x0A | Hallsensor Sitzschlitten, Unterbrechung |
| 0x0B | Hallsensor Sitzschlitten, Kurzschluss nach Ubatt |
| 0x0C | Versorgungsspannung Hallsensoren, Kurzschluss nach Ubatt |
| 0x0D | Steuergeraetefehler, Motorbruecke defekt |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 4 rows × 3 columns

| STEUER_I_O | BYTE1 | BYTE2 |
| --- | --- | --- |
| STOP | 1 | 0x00 |
| SLV_VOR | 1 | 0x01 |
| SLV_ZUR | 1 | 0x02 |
| XXX | Y | Z |
