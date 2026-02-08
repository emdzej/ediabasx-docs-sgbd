# KOMBI34L.prg

- Jobs: [10](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Kombi E34l |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.02 |
| AUTHOR | Softing Taubert, BMW TP-422 Zender, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [GWSZ_RESET](#job-gwsz-reset) - Ruecksetzen des Gesamtwegstreckenzaehlers
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [FG_NR_LESEN](#job-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [TACHO_A](#job-tacho-a) - liefert geschwindigkeitsproportionales Signal

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

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

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_GEN_NR | string | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ZAHL | int | Anzahl der Fehler |
| F_HEX_CODE | binary | HEX.Werte des Fehlers |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

Ruecksetzen des Gesamtwegstreckenzaehlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Oel/Weg/AG-Oel oder Zeit - Reset |
| ARG2 | string | Oel/Weg/AG-Oel oder Zeit - Reset |
| ARG3 | string | Oel/Weg/AG-Oel oder Zeit - Reset |
| ARG4 | string | Oel/Weg/AG-Oel oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-fg-nr-lesen"></a>
### FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FG_NR | string | Fahrgestellnummer |

<a id="job-tacho-a"></a>
### TACHO_A

liefert geschwindigkeitsproportionales Signal

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | int | Vorgabegeschwindigkeit in km/h, (2-240 km/h) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (16 × 3)
- [FARTTEXTE](#table-farttexte) (7 × 2)
- [SIARESET](#table-siareset) (4 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 16 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x00 | 0x01 | Interner Fehler (RAM) |
| 0x01 | 0x01 | Interner Fehler (ROM) |
| 0x05 | 0x02 | Codierstecker fehlerhaft |
| 0x06 | 0x03 | Codierstecker fehlerhaft |
| 0x07 | 0x04 | Codierstecker fehlerhaft |
| 0x08 | 0x05 | Codierstecker fehlerhaft |
| 0x09 | 0x06 | Codierstecker falsch programmiert |
| 0x0a | 0x07 | Ueberspannung an Klemme R |
| 0x0b | 0x08 | K-Zahl fehlerhaft |
| 0x10 | 0x09 | Tankgeber ohne Funktion |
| 0x11 | 0x0a | Temperaturanzeige fehlerhaft |
| 0x1a | 0x0e | EGS Stoerung |
| 0x1b | 0x0b | Bremsbelagfuehler |
| 0x1c | 0x0c | Tankreservekontakt fehlerhaft |
| 0x1d | 0x0d | Kombitaste fehlerhaft |
| 0xff | 0x00 | unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Kurzschluss nach UBatt |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Unterbrechung |
| 0x03 | ungueltiger Arbeitsbereich |
| 0x04 | sporadischer Fehler |
| 0x05 | statischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| AG_OEL_RESET | 0x03 |
| ZEIT_RESET | 0x04 |
