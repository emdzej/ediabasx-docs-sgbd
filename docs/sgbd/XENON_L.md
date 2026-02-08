# XENON_L.prg

- Jobs: [11](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Xenon links E46 / Mini |
| ORIGIN | BMW TI-431 Lodde |
| REVISION | 1.00 |
| AUTHOR | BMW TI-431 Schaller, BMW TI-431 Lodde, BMW TI-432 Pichler |
| COMMENT | Version von BMW TP-422 Teepe ueberarbeitet |
| PACKAGE | 1.00 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - DIAGNOSE_WEITER job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - DIAGNOSE_ENDE job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [ADAPTIVWERT_LOESCHEN](#job-adaptivwert-loeschen) - loeschen eines Adaptivwerte Es muss immer ein Argument mit drei moeglichen Werten (WECHSEL_LAMPE, WECHSEL_ZUENDMODUL, WECHSEL_STEUERGERAET) uebergeben werden.

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SPANNUNG_KLEMME15_WERT | real | Spannung Klemme 15, Aufloesung 0,1 Volt |
| STAT_SPANNUNG_KLEMME56b_WERT | real | Spannung Klemme 56b, Aufloesung 0,1 Volt |
| STAT_LAMPENBRENNSPANNUNG_WERT | int | Lampenbrennspannung, Aufloesung 1 Volt |
| STAT_SPANNUNG_EINH | string | Einheit aller Spannungen = Volt |
| STAT_LAMPEN_BRENNT_SEIT_3_MINUTEN_EIN | int | Lampe hat ihre 3-minuetige Startphase hinter sich damit ist die Brennspannung stabilisiert |
| STAT_LAMPENWECHSEL_HAT_STATTGEFUNDEN | int | Lampe wurde gewechselt |
| STAT_ZUENDMODUL_WURDE_GEWECHSELT | int | Zuendmodul wurde ausgetauscht |
| STAT_STEUERGERAET_WURDE_GEWECHSELT | int | Steuergeraet wurde ausgetauscht |
| STAT_SYSTEMBRENNDAUER_WERT | real | Systembrenndauer [h] |
| STAT_ANZAHL_SYSTEMEINSCHALTUNGEN_WERT | long | Anzahl der Systemeinschaltungen |
| STAT_LAMPENBRENNDAUER_WERT | real | Lampenbrenndauer [h] |
| STAT_LAMPENBRENNDAUER_EINH | string | Lampenbrenndauer [h] |
| STAT_ANZAHL_LAMPENEINSCHALTUNGEN | long | Anzahl der Lampeneinschaltungen |
| STAT_BRENNSPANNUNG_NEUE_LAMPE_WERT | int | Brennspannung der neuen Lampe [Volt] wird erst nach 3 Minuten ununterbrochenen Betriebs gespeichert |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

DIAGNOSE_WEITER job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

DIAGNOSE_ENDE job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-adaptivwert-loeschen"></a>
### ADAPTIVWERT_LOESCHEN

loeschen eines Adaptivwerte Es muss immer ein Argument mit drei moeglichen Werten (WECHSEL_LAMPE, WECHSEL_ZUENDMODUL, WECHSEL_STEUERGERAET) uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTIVWERT | string | WECHSEL_LAMPE, WECHSEL_ZUENDMODUL, WECHSEL_STEUERGERAET table JobResult STATUS_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (14 × 2)
- [LIEFERANTEN](#table-lieferanten) (34 × 2)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [ADAPTIVWERTE](#table-adaptivwerte) (4 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0A | Ul &lt;65 Volt, Brennspannung ausserhalb des zulaessigen Bereichs |
| 0x0B | Ul &gt;115 Volt, Brennspannung ausserhalb des zulaessigen Bereichs |
| 0x0C | D2S/R-Lampe ist erloschen |
| 0x0D | D2S/R-Lampe mehrmals erloschen |
| 0x14 | Zuendung erfolglos |
| 0x15 | Zuendgeraet nicht angeschlossen oder defekt |
| 0x1E | µC-interner Fehler |
| 0x1F | Hardwarefehler im Steuergeraet |
| 0x20 | Kurzschluss am Ausgang des Steuergeraetes (ZG-Pins) |
| 0x21 | Zuendhilfsspannung fehlerhaft |
| 0x28 | Ueberspannungsabschaltung, Klemme 56b &gt; 19 Volt |
| 0x29 | SW-Kabelbaum oder Zuleitung zum SW zu hochohmig |
| 0x2A | Klemme 15 &lt; 7,5 Volt |
| 0xFF | unbekannter Fehlerort |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 34 rows × 2 columns

| LIEF_NR | LIEF_NAME |
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
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Melco/ZKW |
| 0xFF | unbekannter Hersteller |

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

<a id="table-adaptivwerte"></a>
### ADAPTIVWERTE

Dimensions: 4 rows × 2 columns

| ADAPTIVWERT | BITWERT |
| --- | --- |
| WECHSEL_LAMPE | 0x01 |
| WECHSEL_ZUENDMODUL | 0x02 |
| WECHSEL_STEUERGERAET | 0x03 |
| FALSCHES_ARGUMENT | 0x00 |
