# HKM.prg

- Jobs: [13](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Heckklappen-Modul fuer E38 |
| ORIGIN | BMW TI-430 Stefan Bendel |
| REVISION | 1.01 |
| AUTHOR | BMW TI-430 Gerd Huber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer Heckklappen-Modul automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer HKM
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_IO](#job-status-io) - Stati aller Signale des Heckklappen-Moduls
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs v. HKM
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten des HKM

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer Heckklappen-Modul automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer HKM

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

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT | binary |  |

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
| JOB_STATUS | string | OKAY, ERROR_.. |
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

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-status-io"></a>
### STATUS_IO

Stati aller Signale des Heckklappen-Moduls

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TOEHKK | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKNG2 | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_STATV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_TOEHK | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKNG1 | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_UBL | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_EN_L | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKVENT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKPA | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKPZ | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WDSP | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KL50 | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKK | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_TOEHKI | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_HKFUNK | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_BEWEGUNGSZAEHLER_WERT | long | aktueller Wert des Bewegungszaehlers Bereich: 0 bis 65535 |
| STAT_WIEDERHOLSPERRE_WERT | long | aktueller Zaehlwert der Wiederholsperre Bereich: 0 bis 65535 |
| STAT_ZAEHLER_EINH | string | Einheit: 1 |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs v. HKM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten des HKM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN | binary | alle Codierdaten als reine Datenbytes |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [BITS](#table-bits) (12 × 6)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
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
| 0x28 | DODUCO |
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x90 | Interner Fehler im Heckklappen-Modul: Prozessor |
| 0x91 | Interner Fehler im Heckklappen-Modul: Prozessor ROM |
| 0x92 | Interner Fehler im Heckklappen-Modul: Taktgeber |
| 0x93 | Ansteuerung: Relais klebt bei Oeffnen |
| 0x94 | Ansteuerung: Relais versagt bei Oeffnen |
| 0x95 | Ansteuerung: Relais klebt bei Schliessen |
| 0x96 | Ansteuerung: Relais versagt bei Schliessen |
| 0xA0 | Ventil 1: Kurzschluss oder Leerlauf |
| 0xA1 | Neigungsschalter oder Leitung Neigungsschalter |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-bits"></a>
### BITS

Dimensions: 12 rows × 6 columns

| ZELLE | BYTE | MASK | VALUE | NAME | TEXT |
| --- | --- | --- | --- | --- | --- |
| 0 | 1 | 0x01 | 0x01 | TOEHKK | Taster fuer Heckklappe Innenseite |
| 1 | 1 | 0x02 | 0x02 | HKNG2 | Heckklappen-Neigungsschalter 2 |
| 3 | 1 | 0x08 | 0x08 | TOEHK | Taster Oeffnen Heckklappe |
| 4 | 1 | 0x10 | 0x10 | HKNG1 | Heckklappen-Neigungsschalter 1 |
| 21 | 3 | 0x20 | 0x20 | HKVENT | Heckklappe Hydraulikventil |
| 22 | 3 | 0x40 | 0x40 | HKPA | Heckklappe Hydraulikpumpe Richtung auf |
| 23 | 3 | 0x80 | 0x80 | HKPZ | Heckklappe Hydraulikpumpe Richtung zu |
| 34 | 5 | 0x04 | 0x04 | KL50 | Klemme 50 |
| 35 | 5 | 0x08 | 0x08 | HKK | Heckklappenkontakt |
| 36 | 5 | 0x10 | 0x10 | TOEHKI | Taster Oeffnen Heckklappe Innenraum |
| 38 | 5 | 0x40 | 0x40 | HKFUNK | Funkschluessel Heckklappen-Taste |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
