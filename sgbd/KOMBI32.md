# KOMBI32.prg

- Jobs: [11](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Kombi E32 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.00 |
| AUTHOR | Softing, BMW ET-421 Teepe, BMW TI-433 Dennert |
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
- [AGS_COD_LESEN](#job-ags-cod-lesen) - Auslesen der AGS-Codierung
- [AGS_COD_SCHREIBEN](#job-ags-cod-schreiben) - Schreiben der AGS-Codierung

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
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_TABELLE |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_HFK | int | Haeufigkeit eines Fehlers |

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
| JOB_STATUS | string | Liefert: OKAY |

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

<a id="job-ags-cod-lesen"></a>
### AGS_COD_LESEN

Auslesen der AGS-Codierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| AGS_COD | string | Liefert: AGS_CODIERT od. AGS_NICHT_CODIERT |

<a id="job-ags-cod-schreiben"></a>
### AGS_COD_SCHREIBEN

Schreiben der AGS-Codierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (6 × 3)
- [SIARESET](#table-siareset) (4 × 2)
- [AGS_COD](#table-ags-cod) (2 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 6 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x00 | 0x00 | unbekannter Fehlerort |
| 0x02 | 0x01 | Kodierstecker fehlerhaft |
| 0x01 | 0x02 | Programmierung fehlerhaft |
| 0x04 | 0x03 | K-Zahl fehlerhaft |
| 0x03 | 0x04 | Tachoprogrammierung |
| 0x05 | 0x05 | Geschwindigkeitslimit |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| AG_OEL_RESET | 0x03 |
| ZEIT_RESET | 0x04 |

<a id="table-ags-cod"></a>
### AGS_COD

Dimensions: 2 rows × 2 columns

| AGSCOD | AGSCODTEXT |
| --- | --- |
| 0x00 | AGS_NICHT_CODIERT |
| 0xFF | AGS_CODIERT |
