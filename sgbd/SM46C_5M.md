# SM46C_5M.prg

- Jobs: [17](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sitzmemory E46 Cabrio |
| ORIGIN | BMW TI-431 Krueger |
| REVISION | 1.0 |
| AUTHOR | BMW TI-433 Teepe, TI-433 Krueger |
| COMMENT | Info_Kommentar |
| PACKAGE | 0.05 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des internen Speichers
- [STATUS_1_LESEN](#job-status-1-lesen) - Stati des SM46_C
- [STATUS_2_LESEN](#job-status-2-lesen) - Stati des SM46
- [VARIANTE_LESEN](#job-variante-lesen) - SG-Variante aus Zelle 0x0124 auslesen
- [POSITIONEN_LESEN](#job-positionen-lesen) - 3 Speicher- und aktuelle Position aus EEPROM auslesen
- [STEUERN_IO](#job-steuern-io) - Ansteuern eines digitalen Einganges

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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

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

Stati des SM46_C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SCHALTER_SLV_VOR_EIN | int |  |
| STAT_SCHALTER_SLV_ZURUECK_EIN | int |  |
| STAT_SCHALTER_SHV_AUF_EIN | int |  |
| STAT_SCHALTER_SHV_AB_EIN | int |  |
| STAT_SCHALTER_SNV_AUF_EIN | int |  |
| STAT_SCHALTER_SNV_AB_EIN | int |  |
| STAT_SCHALTER_LEHNE_VOR_EIN | int |  |
| STAT_SCHALTER_LEHNE_ZURUECK_EIN | int |  |
| STAT_SCHALTER_KHV_AUF_EIN | int |  |
| STAT_SCHALTER_KHV_AB_EIN | int |  |
| STAT_TASTE_MEM_EIN | int |  |
| STAT_TASTE_POS1_EIN | int |  |
| STAT_TASTE_POS2_EIN | int |  |
| STAT_TASTE_POS3_EIN | int |  |
| STAT_EHV_EIN | int |  |
| STAT_EHZ_EIN | int |  |
| STAT_EE_SCHALTER_POS | int | 0=aus,1=vor,2=zurueck |
| STAT_RS_EIN | int |  |
| STAT_BC_EIN | int |  |
| STAT_KL30_EIN | int |  |
| STAT_LVK_EIN | int |  |
| STAT_LED_EIN | int |  |
| STAT_POS_SLV_WERT | long |  |
| STAT_POS_SHV_WERT | long |  |
| STAT_POS_SNV_WERT | long |  |
| STAT_POS_LNV_WERT | long |  |
| STAT_POS_KHV_WERT | long |  |
| STAT_SCHALTER_SITZLAENGE | int | 0=aus,1=vor,2=zurueck |
| STAT_SCHALTER_SITZHOEHE | int | 0=aus,1=auf,2=ab |
| STAT_SCHALTER_NEIGUNG | int | 0=aus,1=auf,2=ab |
| STAT_SCHALTER_SITZLEHNE | int | 0=aus,1=vor,2=zurueck |
| STAT_SCHALTER_KOPFSTUETZE | int | 0=aus,1=auf,2=ab |
| STAT_MEMORYSCHALTER | int | bitcodiert, Werte zwischen 0 und 15! bit 0=MEM-Taste bit 1=Taste 1 bit 2=Taste 2 bit 3=Taste 3 |

<a id="job-status-2-lesen"></a>
### STATUS_2_LESEN

Stati des SM46

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SPANNUNG_HALLS_LNV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SHV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SNV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SLV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_KHV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_LVK_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_KL30_WERT | real | Batterie-Spannung am SG |
| STAT_SPANNUNGEN_EINH | string | Einheit der Spannung |

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

<a id="job-positionen-lesen"></a>
### POSITIONEN_LESEN

3 Speicher- und aktuelle Position aus EEPROM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| POS_1_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 1 |
| POS_2_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 2 |
| POS_3_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 3 |
| POS_AKTUELL_SITZLAENGE_WERT | long | gespeicherte aktuelle Sitzlaengenposition |
| POS_1_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 1 |
| POS_2_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 2 |
| POS_3_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 3 |
| POS_AKTUELL_SITZHOEHE_WERT | long | gespeicherte aktuelle Sitzhoehenposition |
| POS_1_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 1 |
| POS_2_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 2 |
| POS_3_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 3 |
| POS_AKTUELL_SITZNEIGUNG_WERT | long | gespeicherte aktuelle Sitzneigungsposition |
| POS_1_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 1 |
| POS_2_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 2 |
| POS_3_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 3 |
| POS_AKTUELL_LEHNENNEIGUNG_WERT | long | gespeicherte aktuelle Lehnenneigungsposition |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (23 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (20 × 4)

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

Dimensions: 23 rows × 2 columns

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
| 0x0C | Hallsensor Kopfstuetze, Kurzschluss nach Masse |
| 0x0D | Hallsensor Kopfstuetze, Unterbrechung |
| 0x0E | Hallsensor Kopfstuetze, Kurzschluss nach Ubatt |
| 0x0F | Hallsensor Lehnenverriegelung, Kurzschluss nach Masse |
| 0x10 | Hallsensor Lehnenverriegelung, Unterbrechung |
| 0x11 | Hallsensor Lehnenverriegelung, Kurzschluss nach Ubatt |
| 0x12 | Hallsensor ST2 nicht aufgesteckt, Kurzschluss nach Masse |
| 0x13 | Steuergeraetefehler, Motorbruecke defekt |
| 0x14 | Sitzbedienschalter, Kurzschluss nach Ubatt |
| 0x15 | Sitzbedienschalter, Kurzschluss nach Masse |
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

Dimensions: 20 rows × 4 columns

| STEUER_I_O | BYTE1 | BYTE2 | BYTE3 |
| --- | --- | --- | --- |
| STOP | 0x01 | 0x00 | 0x00 |
| SLV_VOR | 0x01 | 0x01 | 0x00 |
| SLV_ZUR | 0x01 | 0x02 | 0x00 |
| SHV_AUF | 0x01 | 0x04 | 0x00 |
| SHV_AB | 0x01 | 0x08 | 0x00 |
| SNV_AUF | 0x01 | 0x10 | 0x00 |
| SNV_AB | 0x01 | 0x20 | 0x00 |
| LNV_VOR | 0x01 | 0x40 | 0x00 |
| LNV_ZUR | 0x01 | 0x80 | 0x00 |
| KHV_AB | 0x01 | 0x00 | 0x02 |
| KHV_AUF | 0x01 | 0x00 | 0x01 |
| POS_1 | 0x02 | 0x01 | 0x00 |
| POS_2 | 0x02 | 0x02 | 0x00 |
| POS_3 | 0x02 | 0x04 | 0x00 |
| LED_AN | 0x03 | 0x01 | 0x00 |
| LED_AUS | 0x03 | 0x00 | 0x00 |
| EH_STOP | 0x04 | 0x00 | 0x00 |
| EH_VOR | 0x04 | 0x01 | 0x00 |
| EH_ZUR | 0x04 | 0x02 | 0x00 |
| XXX | Y | Z | Z |
