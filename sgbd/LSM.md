# LSM.prg

- Jobs: [8](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Lenksaeulenmemory E31 / E32 / E34 |
| ORIGIN | BMW, TP-422, Teepe |
| REVISION | 1.52 |
| AUTHOR | BMW, TP-422, Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [MODELL_COD_LESEN](#job-modell-cod-lesen) - Auslesen der MODELL-Codierung -- aus RAM und EEPROM
- [MODELL_COD_SCHREIBEN](#job-modell-cod-schreiben) - Schreiben der MODELL-Codierung

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |

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
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-modell-cod-lesen"></a>
### MODELL_COD_LESEN

Auslesen der MODELL-Codierung -- aus RAM und EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| MODELL_COD | string | Liefert: E31_CODIERT od. E32_34_CODIERT |

<a id="job-modell-cod-schreiben"></a>
### MODELL_COD_SCHREIBEN

Schreiben der MODELL-Codierung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Modell-Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (32 × 3)
- [MODELL_COD](#table-modell-cod) (2 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 32 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x02 | 0x01 | Arbeitsbereich Neigung |
| 0x03 | 0x02 | Arbeitsbereich laengs |
| 0x04 | 0x03 | Kalibrierung Verstellogik |
| 0x05 | 0x03 | Kalibrierung Verstellogik |
| 0x06 | 0x03 | Kalibrierung Verstellogik |
| 0x07 | 0x03 | Kalibrierung Verstellogik |
| 0x08 | 0x03 | Kalibrierung Verstellogik |
| 0x09 | 0x03 | Kalibrierung Verstellogik |
| 0x0A | 0x03 | Kalibrierung Verstellogik |
| 0x0B | 0x03 | Kalibrierung Verstellogik |
| 0x0C | 0x04 | Relaisueberwachung Neigung |
| 0x0D | 0x05 | Relaisueberwachung laengs |
| 0x0E | 0x04 | Relaisueberwachung Neigung |
| 0x0F | 0x05 | Relaisueberwachung laengs |
| 0x10 | 0x04 | Relaisueberwachung Neigung |
| 0x11 | 0x05 | Relaisueberwachung laengs |
| 0x12 | 0x04 | Relaisueberwachung Neigung |
| 0x13 | 0x05 | Relaisueberwachung laengs |
| 0x14 | 0x06 | WZUe Neigung |
| 0x15 | 0x07 | WZUe laengs |
| 0x16 | 0x06 | WZUe Neigung |
| 0x17 | 0x07 | WZUe laengs |
| 0x18 | 0x08 | Signal Lenkstockhebel Zurueck |
| 0x19 | 0x09 | Signal Lenkstockhebel Vor |
| 0x1A | 0x0A | Signal Lenkstockhebel Ab |
| 0x1B | 0x0B | Signal Lenkstockhebel Auf |
| 0x1C | 0x0C | Tastenfeld |
| 0x1D | 0x0D | Klemme R |
| 0x1E | 0x0E | Memory-LED |
| 0x20 | 0x0F | Relaisueberwachung |
| 0x21 | 0x10 | Relaisueberwachung |
| 0x00 | 0x00 | unbekannte Fehlerart |

<a id="table-modell-cod"></a>
### MODELL_COD

Dimensions: 2 rows × 2 columns

| MODELLCOD | MODELLCODTEXT |
| --- | --- |
| 0x00 | E31_CODIERT |
| 0x80 | E32_34_CODIERT |
