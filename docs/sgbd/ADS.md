# ADS.PRG

- Jobs: [6](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Aktiver Diagnose Stecker |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.02 |
| AUTHOR | BMW TP-421 Drexel, BMW TP-421 Huber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [POWER_BREAK](#job-power-break) - Abschalten des ADS fuer Ruhestrommessung ECOS
- [POWER_OFF](#job-power-off) - Abschalten des ADS
- [POWER_ON](#job-power-on) - Einschalten des ADS (Klemme 15 muss EIN sein!)
- [LOOPTEST](#job-looptest) - Testschleife fuer RxD und TxD Vorher RxD mit TxD verbinden

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-power-break"></a>
### POWER_BREAK

Abschalten des ADS fuer Ruhestrommessung ECOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-power-off"></a>
### POWER_OFF

Abschalten des ADS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-power-on"></a>
### POWER_ON

Einschalten des ADS (Klemme 15 muss EIN sein!)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-looptest"></a>
### LOOPTEST

Testschleife fuer RxD und TxD Vorher RxD mit TxD verbinden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| CHECK | string | Ergebnis des Leitungstests |

## Tables

No tables found.
