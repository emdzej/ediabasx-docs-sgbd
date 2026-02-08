# ABSMK4.prg

- Jobs: [8](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem MK4 E36 |
| ORIGIN | BMW TP-421 Hirsch |
| REVISION | 1.09 |
| AUTHOR | BMW TP-421 Hirsch |
| COMMENT | Keine Diagnose bei V &gt; 2.5 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ABS_ASC_MK4
- [IDENT](#job-ident) - Ident-Daten fuer ABS_MK4
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ABS_MK4
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ABS_MK4
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ABS_MK4
- [STEUERN_DIGITAL](#job-steuern-digital) - Steuern_Digital mit mehreren Ausgaenge fuer ABS_MK4
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer ABS_ASC_MK4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ABS_MK4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_SW_NR | int | BMW-Softwarenummer |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen fuer ABS_MK4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS_MK4 = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS_MK4 = 0 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer ABS_MK4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge ABS_MK4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_PEDALWEGSENSOR_WERT | int | 0 bis 7 |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Steuern_Digital mit mehreren Ausgaenge fuer ABS_MK4

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [FORTTEXTE](#table-forttexte) (30 × 2)
- [STEUERN](#table-steuern) (8 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xFA | ERROR_ECU_FUNCTION |
| 0xFB | ERROR_ECU_FUNCTION |
| 0xF7 | ERROR_ECU_FUNCTION |
| 0xF8 | ERROR_ECU_FUNCTION |
| 0xF2 | ERROR_ECU_FUNCTION |
| 0x0A | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 30 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | ABS Ventil Einlass vorne links |
| 0x12 | ABS Ventil Auslass vorne links |
| 0x14 | ABS Ventil Einlass vorne rechts |
| 0x18 | ABS Ventil Auslass vorne rechts |
| 0x21 | ABS Ventil Einlass Hinter Achse |
| 0x22 | ABS Ventil Auslass Hinter Achse |
| 0x44 | Bus od. Busprozessor |
| 0x48 | Interner IC-Fehler |
| 0x51 | Drehzahlfuehler Fehler VL, Triggersignal |
| 0x52 | Drehzahlfuehler Fehler VR, Triggersignal |
| 0x54 | Drehzahlfuehler Fehler HL, Triggersignal |
| 0x58 | Drehzahlfuehler Fehler HR, Triggersignal |
| 0x61 | Drehzahlfuehler Fehler VL, Kontinuitaet |
| 0x62 | Drehzahlfuehler Fehler VR, Kontinuitaet |
| 0x64 | Drehzahlfuehler Fehler HL, Kontinuitaet |
| 0x68 | Drehzahlfuehler Fehler HR, Kontinuitaet |
| 0x71 | Drehzahlfuehler Fehler VL, Anfahrerkennung |
| 0x72 | Drehzahlfuehler Fehler VR, Anfahrerkennung |
| 0x74 | Drehzahlfuehler Fehler HL, Anfahrerkennung |
| 0x78 | Drehzahlfuehler Fehler HR, Anfahrerkennung |
| 0x84 | Pedalwegsensor |
| 0x88 | Hydraulikpumpe |
| 0x91 | Pumpenmotor |
| 0x98 | Hydraulikkreislauf |
| 0xA1 | ABS Ventil Auslass vorne links |
| 0xA2 | ABS Ventil Auslass vorne rechts |
| 0xA4 | ABS Ventil Auslass Hinter Achse |
| 0xA8 | ABS Ventil Auslass Hinter Achse |
| 0xFF | NV-RAM |
| 0xXY | unbekannter Fehlerort |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 8 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHA | 0 | 0x10 |
| AVHA | 0 | 0x20 |
| Pumpe | 1 | 0x01 |
| XYZ | 2 | 0xFF |
