# ABS_UC.prg

- Jobs: [7](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ABS-System E34 - M5 |
| ORIGIN | BMW TP-421 Hirsch |
| REVISION | 1.23 |
| AUTHOR | BMW TP-421 Hirsch |
| COMMENT | Keine Diagnose bei v &gt; 6km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [INFO](#job-info) - Information SGBD
- [ENDE](#job-ende) - Abbruch der Kommunikation
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose

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

<a id="job-ende"></a>
### ENDE

Abbruch der Kommunikation

_No arguments._

_No results._

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BB_NR | string | BB-Nummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_HFK | int | Haeufigkeit eines Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_ART3_NR | int | Textindex fuer Fehlerart 3 |
| F_ART3_TEXT | string | Text fuer Fehlerart 3 |
| F_ART4_NR | int | Textindex fuer Fehlerart 4 |
| F_ART4_TEXT | string | Text fuer Fehlerart 4 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_UW1_NR | int | Textindex der Umweltbedingung 1 |
| F_UW1_TEXT | string | Bedeutung der Umweltbedingung 1 |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_ECU_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x04 | Drehzahlfuehler Fehler hinten links |
| 0x05 | Drehzahlfuehler Fehler hinten rechts |
| 0x06 | Drehzahlfuehler Fehler vorne rechts |
| 0x07 | Drehzahlfuehler Fehler vorne links |
| 0x08 | ABS Ventil Fehler hinten links |
| 0x09 | ABS Ventil Fehler hinten rechts |
| 0x0A | ABS Ventil Fehler vorne rechts |
| 0x0B | ABS Ventil Fehler vorne links |
| 0x0E | Ventilrelais Fehler |
| 0x0F | Rueckfoerderpumpen Fehler |
| 0x15 | Steuergeraete-Fehler |
| 0x18 | Falsches Zahnrad an einem der 4 Raeder |
| 0x19 | Bremslichtschalter Leitungsunterbrechung |
| 0xFF | undefinierter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | statischer Fehler -- momentan vorhanden |
| 0x02 | sporadischer Fehler -- Zuendung ein &lt; 49mal |
| 0x03 | sporadischer Fehler -- Zuendung ein &gt;= 49mal |
| 0x04 | Kurzschluss nach U-Batt oder Unterbrechung |
| 0x05 | keine Fehlerart erkannt |
| 0x06 | BLS betaetigt |
| 0x07 | BLS nicht betaetigt |
| 0x08 | ABS Regelung aktiv |
| 0x09 | ABS Regelung passiv |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 2 columns

| UWNR | UWTEXT |
| --- | --- |
| 0x01 | Geschwindigkeit  km/h |
