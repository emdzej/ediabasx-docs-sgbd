# A-SITZ_F.prg

- Jobs: [6](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Aktivsitz Fahrer |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 1.0 |
| AUTHOR | BMW TI-430 Drexel |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen ZKE 3 Fehlerspeicher wird geloescht!
- [STATUS_IO](#job-status-io) - Status lesen

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

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit = 1 |
| F_ART_ANZ | int | Anzahl der Fehlerarten = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen = 0 |
| F_HEX_CODE | binary | Fehlerspeicherdaten |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen ZKE 3 Fehlerspeicher wird geloescht!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FUNKTION_EIN | int | Funktion ein |
| STAT_BESCHLEUNIGUNGSABSCHALTUNG_EIN | int | Beschleunigungsabschaltung ein |
| STAT_GESCHWINDIGKEITSABSCHALTUNG_EIN | int | Geschwindigkeitsabschaltung ein |
| STAT_UNTERSPANNUNGSABSCHALTUNG_EIN | int | Unterspannungsabschaltung ein |
| STAT_KLEMME_15_EIN | int | Klemme 15 |
| STAT_KLEMME_R_EIN | int | Klemme R |
| STAT_PUMPENSTATUS_WERT | int | Interner Pumpenstatus als Nummer 0 - 12 |
| STAT_PUMPENSTATUS_EINH | string | -- |
| STAT_PUMPENSTATUS_TEXT | string | Interner Pumpenstatus als Text table PumpenStatus STATUS_TEXT |
| TELEGRAMM | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)
- [PUMPENSTATUS](#table-pumpenstatus) (14 × 2)

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

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Motortreiber defekt |
| 0x01 | Ventiltreiber defekt |
| 0x02 | Beschleunigungssensor kein Signal |
| 0x03 | EEPROM defekt |
| 0x04 | Hallsensor oder Pumpenmotor defekt |
| 0x05 | Drucksensor 1 defekt |
| 0x06 | Drucksensor 2 defekt |
| 0x07 | Systemfehler Not-Aus |
| 0x08 | interner Systemfehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-pumpenstatus"></a>
### PUMPENSTATUS

Dimensions: 14 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Pumpe steht |
| 0x01 | Pumpe startet von Mittelstellung nach Anschlag 1 |
| 0x02 | Pumpe faehrt nach Anschlag 1 |
| 0x03 | Pumpe wartet bei Anschlag 1 |
| 0x04 | Pumpe startet von Anschlag 1 nach Mittelstellung |
| 0x05 | Pumpe faehrt von Anschlag 1 nach Mittelstellung |
| 0x06 | Pumpe wartet in Mittelstellung |
| 0x07 | Pumpe startet von Mittelstellung nach Anschlag 2 |
| 0x08 | Pumpe faehrt nach Anschlag 2 |
| 0x09 | Pumpe wartet bei Anschlag 2 |
| 0x0A | Pumpe startet von Anschlag 2 nach Mittelstellung |
| 0x0B | Pumpe faehrt von Anschlag 2 nach Mittelstellung |
| 0x0C | Pumpe wartet in Mittelstellung |
| 0xFF | unbekannter Zustand |
