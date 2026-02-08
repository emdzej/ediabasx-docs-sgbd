# mraabs1.prg

- Jobs: [7](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ABS Steuergerät AB02.5 |
| ORIGIN | I+ME Actia R&D ABT, KA |
| REVISION | 1.004 |
| AUTHOR | I+ME R&D Axel Bäthge |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Fakeantwort notwendig wegen ISTA zur Steuerung SG-Baum
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler)
- [INIT_FS_LOESCHEN](#job-init-fs-loeschen) - Initialisierung und Kommunikationsparameter
- [FS_LOESCHEN](#job-fs-loeschen) - Initialisierung und Kommunikationsparameter
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Deinitialisierung

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

<a id="job-ident"></a>
### IDENT

Fakeantwort notwendig wegen ISTA zur Steuerung SG-Baum

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer NOTOKAY in ISTA wird damit Steuergerät gelb markiert |
| JOB_STATUS2 | string | immer OKAY in ISTA wird damit Steuergerät grün markiert |
| VARIANTE_IND | string | Name der SGBD |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HINWEIS | string | folgende Massnahmen |
| DONE | int | 1, wenn Okay |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers für KWP-2000 immer 2 |
| HINWEIS | string | folgende Massnahmen |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag als Zahl |
| F_READY_TEXT | string | Readyness Flag als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl Status Bit 7 |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-init-fs-loeschen"></a>
### INIT_FS_LOESCHEN

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HINWEIS | string | folgende Massnahmen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HINWEIS | string | folgende Massnahmen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Deinitialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | INITIALISIEREN VON ICOM_E FEHLGESCHLAGEN |
| 0x03 | LINIE SETZEN FEHLGESCHLAGEN |
| 0x04 | BLINKCODE LESEN FEHLGESCHLAGEN |
| 0x05 | INITIALISIEREN DER BLINKZAHLERFASSUNG FEHLGESCHLAGEN |
| 0x06 | BEENDEN DER BLINKZAHLERFASSUNG FEHLGESCHLAGEN |
| 0x07 | BEENDEN VON ICOM_E FEHLGESCHLAGEN |
| 0xFF | UNBEKANNTER FEHLER |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 10 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x01 | Druckmodulator vorn | 0 |
| 0x02 | Druckmodulator hinten | 0 |
| 0x03 | Sensor vorn | 0 |
| 0x04 | Sensor hinten | 0 |
| 0x05 | Batterie-Unterspannung | 0 |
| 0x06 | ABS-Relais | 0 |
| 0x07 | ABS-Steuergerät mit Druckmodulator | 0 |
| 0x08 | Störung durch äußere Einflüsse | 0 |
| 0x09 | Warnlampen-Bereich inkl. WL-Relais | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |
