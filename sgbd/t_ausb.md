# t_ausb.prg

- Jobs: [2](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | externe Tabelle ZuordnungsTabelle |
| ORIGIN | BMW EE-24 Gase |
| REVISION | 1.005 |
| AUTHOR | BMW TI-430 Schnelle, EE-24 Gase |
| COMMENT | N/A |
| PACKAGE | 1.35 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

## Tables

### Index

- [AUSB_VORAB](#table-ausb-vorab) (40 × 5)

<a id="table-ausb-vorab"></a>
### AUSB_VORAB

Dimensions: 40 rows × 5 columns

| DTC | FORTTEXT | PQM | AUSBLENDDATUM | COMMENT |
| --- | --- | --- | --- | --- |
| 0xA048 | P-Fehler Speichertest MMI-Rechner |  |  |  |
| 0xA5E8 | P-Fehler Speichertest MMI-Rechner |  |  |  |
| 0xD550 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD551 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD590 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD591 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD650 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD651 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD690 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD691 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD6D0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD6D1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD790 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD791 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD7D0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD7D1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD810 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD811 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD850 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD851 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xD8D0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xD8D1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xDAD0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xDAD1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xDBD0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xDBD1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xDDD0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xDDD1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xDE10 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xDE11 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xDE50 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose). |  |  |  |
| 0xDE51 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long). |  |  |  |
| 0xDFD0 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xDFD1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xE110 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xE111 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xE150 | P-Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |  |  |  |
| 0xE151 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xE191 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
| 0xE1D1 | P-Lange und/oder haeufige Unlocks (Error_Unlock_Long) |  |  |  |
