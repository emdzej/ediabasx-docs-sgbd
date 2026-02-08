# DDSHD.prg

- Jobs: [8](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDSHD E34/2 |
| ORIGIN | BMW ET-421 Teepe |
| REVISION | 1.34 |
| AUTHOR | BMW ET-421 Teepe |
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
- [STATUS_IO_LESEN](#job-status-io-lesen) - Auslesen der Ein- Ausgaenge
- [STATUS_POS_LESEN](#job-status-pos-lesen) - Auslesen der Deckelpositionen

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
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Nr der Fehlerart 1 |
| F_ART1_TEXT | string | Fehlerart 1 Text |
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

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Auslesen der Ein- Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_E_IMPULSGEBER_VORN1_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_IMPULSGEBER_VORN2_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_IMPULSGEBER_HINTEN1_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_IMPULSGEBER_HINTEN2_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_RESERVE_1_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_RESERVE_2_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_MOTOR_SHD_FAHRERSEITE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_MOTOR_SHD_KOMFORT_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_SCHALTER_V_SCHIEBEN_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_SCHALTER_H_SCHIEBEN_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_SCHALTER_SCHLIESSEN_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DIAG_REL_SHDV_AUF_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DIAG_REL_SHDV_ZU_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DIAG_REL_SHDH_AUF_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DIAG_REL_SHDH_ZU_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_REL_SHDV_AUF_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_REL_SHDV_ZU_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_REL_SHDH_AUF_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_REL_SHDH_ZU_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_VERSORGUNG_IMPLUSGEBER_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_ENABLE_BAUSTEIN1_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_ENABLE_BAUSTEIN2_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_BETRIEBSART_BAUSTEINE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_SPANNUNG_U_BATT_WERT | int | Liefert: 0 der 1 |

<a id="job-status-pos-lesen"></a>
### STATUS_POS_LESEN

Auslesen der Deckelpositionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_POS_V_DECKEL_WERT | int | Liefert: Position in Inkrementen |
| STAT_POS_H_DECKEL_WERT | int | Liefert: Position in Inkrementen |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (17 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Relais 1 zieht nicht an |
| 0x02 | Relais 2 zieht nicht an |
| 0x03 | Relais 3 zieht nicht an |
| 0x04 | Relais 4 zieht nicht an |
| 0x05 | Relais 1 klebt |
| 0x06 | Relais 2 klebt |
| 0x07 | Relais 3 klebt |
| 0x08 | Relais 4 klebt |
| 0x09 | Zuleitung HD Motor verpolt |
| 0x0a | Zuleitung VD Motor verpolt |
| 0x0b | Hinterer Motor / Geber |
| 0x0c | Vorderer Motor / Geber |
| 0x0d | Spannungs-Versorgung |
| 0x0e | Impulsgeber VD /HD |
| 0x0f | SHD-Schalter |
| 0x10 | DDSHD_Modul |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0 | sporadischer Fehler |
| 1 | statischer Fehler |
