# ASC_T.prg

- Jobs: [7](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem u. Autom. Stabilitaets Control E31 - M70 |
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

- [FORTTEXTE](#table-forttexte) (25 × 2)
- [FARTTEXTE](#table-farttexte) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 25 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x02 | Verb. zum EML gestoert |
| 0x03 | Verb. zur DME gestoert |
| 0x04 | Sensor hinten links |
| 0x05 | Sensor hinten rechts |
| 0x06 | Sensor vorne rechts |
| 0x07 | Sensor vorne links |
| 0x08 | ABS-Ventil hinten links |
| 0x09 | ABS-Ventil hinten rechts |
| 0x0A | ABS-Ventil vorne rechts |
| 0x0B | ABS-Ventil vorne links |
| 0x0C | Plunger-Ventil hinten li. |
| 0x0D | Plunger-Ventil hinten re. |
| 0x0E | Ventilrelaisfehler |
| 0x0F | ABS-Rueckfoerderpumpe |
| 0x10 | Plungerspeicherladeventil |
| 0x11 | Ladezeit Plungerspeicher |
| 0x12 | Leckage Plungerspeicher |
| 0x13 | Speicherwarndruckschwelle |
| 0x14 | Schnittstelle zum EGS |
| 0x15 | ABS/ASC-Steuergeraet def. |
| 0x16 | Drehzahlsignalfehler |
| 0x17 | Fehler Getriebecodierung |
| 0x18 | Falsches Impulsrad am Rad |
| 0x19 | Bremslichts. Leitungsunterbrechung |
| 0xFF | undefinierter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 6 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | statischer Fehler -- momentan vorhanden |
| 0x02 | sporadischer Fehler -- Zuendung ein &lt; 49mal |
| 0x03 | sporadischer Fehler -- Zuendung ein &gt;= 49mal |
| 0x04 | Kurzschluss nach U-Batt oder Unterbrechung |
| 0x05 | keine Fehlerart erkannt |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 2 columns

| UWNR | UWTEXT |
| --- | --- |
| 0x01 | Geschwindigkeit  km/h |
