# UTILITY.PRG

- Jobs: [10](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | allgemeine Funktionen |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 1.14 |
| AUTHOR | Softing Taubert, BMW TI-430 Drexel, BMW TP-421 Teepe, BMW TI-430 Haase |
| COMMENT | N/A |
| PACKAGE | 1.36 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung)
- [STATUS_UBATT](#job-status-ubatt) - Auslesen der Spannungsversorgung
- [STATUS_ZUENDUNG](#job-status-zuendung) - Auslesen der Klemme 15
- [ABS_RELAIS](#job-abs-relais) - Schalten des Relais am ABS-STAND
- [INTERFACE](#job-interface) - Rueckgabe des Interfaces
- [IF_RESET](#job-if-reset) - Interface-Reset Rücksetzen der Kommunikationsparameter
- [TIME_AND_DATE](#job-time-and-date) - Zeit- und Datumsangaben
- [PARALLELE_CODIERUNG_EIN](#job-parallele-codierung-ein) - Setzt das angeschlossene Interface auf bestätigte Kommunikation
- [OGW_CAN_TEST](#job-ogw-can-test) - JOB für OGW (E65) Funktionstest

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

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Auslesen der Spannungsversorgung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_UBATT | int |  |

<a id="job-status-zuendung"></a>
### STATUS_ZUENDUNG

Auslesen der Klemme 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY","ERROR_UBATT" |
| STAT_ZUENDUNG | int |  |

<a id="job-abs-relais"></a>
### ABS_RELAIS

Schalten des Relais am ABS-STAND

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS | string | "EIN","AUS" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY","ERROR_PARAMETER","ERROR_INTERFACE" ERROR_INTERFACE bedeutet, dass ein falsches Interface angeschlossen ist (PICO, EIDBSS=EDIC muss sein) |

<a id="job-interface"></a>
### INTERFACE

Rueckgabe des Interfaces

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TYP | string | Interface Name |
| VERSION | int | Versionsnummer |
| BATTERIE | long | Spannung in mV |
| ANTWORT | binary | Interface Name als Data |
| JOB_STATUS | string | Status immer OKAY! |

<a id="job-if-reset"></a>
### IF_RESET

Interface-Reset Rücksetzen der Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-time-and-date"></a>
### TIME_AND_DATE

Zeit- und Datumsangaben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TIME | string | aktuelle Systemzeit |
| DATE | string | aktuelles Systemdatum |
| JAHR | int | Jahr als integer |
| MONAT | int | Monat integer |
| TAG | int | Tag als integer |
| STUNDE | int | Stunde als integer |
| MINUTE | int | Minute als integer |
| SEKUNDE | int | Sekunde als integer |
| KW | int | Kalenderwoche als integer |
| WOCHENTAG | string | Wochentag als Text |
| JOB_STATUS | string | Status immer OKAY! |

<a id="job-parallele-codierung-ein"></a>
### PARALLELE_CODIERUNG_EIN

Setzt das angeschlossene Interface auf bestätigte Kommunikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TYP | string | Interface Name |
| JOB_STATUS | string | Status immer OKAY! |

<a id="job-ogw-can-test"></a>
### OGW_CAN_TEST

JOB für OGW (E65) Funktionstest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TYP | string | Interface Name |
| OUT | binary |  |
| JOB_STATUS | string | Status immer OKAY! |

## Tables

No tables found.
