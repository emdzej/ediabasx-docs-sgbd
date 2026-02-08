# DLE.prg

- Jobs: [14](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Download Engine |
| ORIGIN | BMW VS-43 Rowedder |
| REVISION | 1.000 |
| AUTHOR | VS-43 Rowedder |
| COMMENT | Steuer-SGBD für Download Engine im Interface |
| PACKAGE | 1.37 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung)
- [STATUS_DLE_VERSION](#job-status-dle-version) - Feststellen, ob eine DLE vorhanden ist und Versionsstring zurückliefern Diese Funktion ist die Einzige, die mit einem Interface ohne DLE aufgerufen werden darf, alle Anderen bewirken ohne DLE einen Abbruch von EDIABAS
- [STEUERN_DLE_RESET](#job-steuern-dle-reset) - DLE Rücksetzen: Senden und DNMT/TP stoppen, Ringpuffer löschen
- [STEUERN_TP_INTERVALL](#job-steuern-tp-intervall) - Intervall für Tester Present setzen
- [STEUERN_DLE_HEADER](#job-steuern-dle-header) - Headerinformationen setzen
- [STEUERN_DLE_IOANTWORT](#job-steuern-dle-ioantwort) - Vergleichstelegramm  setzen
- [STEUERN_DLE_TP](#job-steuern-dle-tp) - Tester Present ein / ausschalten
- [STEUERN_DLE_LADEN](#job-steuern-dle-laden) - Daten in den Ringpuffer laden
- [STEUERN_DLE_BUFFERCLEAR](#job-steuern-dle-bufferclear) - Ringpuffer löschen
- [STATUS_DLE](#job-status-dle) - DLE Status holen
- [WAIT_FOR_DLE](#job-wait-for-dle) - Warten bis die DLE alle Blocks geschrieben hat
- [STEUERN_DLE_ODP](#job-steuern-dle-odp) - Datenverbindung für DLE II öffnen
- [STEUERN_DLE_SID](#job-steuern-dle-sid) - Service ID für DLE II setzen Der Service ID String wird von der DLE II automatisch Header und Daten eingefügt

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

<a id="job-status-dle-version"></a>
### STATUS_DLE_VERSION

Feststellen, ob eine DLE vorhanden ist und Versionsstring zurückliefern Diese Funktion ist die Einzige, die mit einem Interface ohne DLE aufgerufen werden darf, alle Anderen bewirken ohne DLE einen Abbruch von EDIABAS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| PRESENT | string | "TRUE" wenn DLE vorhanden, sonst "FALSE" |
| VERSION | string | Versionsstring in der Form &lt;MAJOR&gt;.&lt;MINOR&gt; |
| _TEL_ANTWORT | binary | Antwort des OPPS |

<a id="job-steuern-dle-reset"></a>
### STEUERN_DLE_RESET

DLE Rücksetzen: Senden und DNMT/TP stoppen, Ringpuffer löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-tp-intervall"></a>
### STEUERN_TP_INTERVALL

Intervall für Tester Present setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INTERVALL | int | zeitlicher Abstand zwischen denn Tester Present Telegrammen in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-header"></a>
### STEUERN_DLE_HEADER

Headerinformationen setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOURCE | int | Adresse des Testers |
| LENGTH | int | Programmierblocklänge /mit/ Service-ID, /ohne/ Prüfsumme |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DLE_KOMMANDO | binary | Kommando an OPPS |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-ioantwort"></a>
### STEUERN_DLE_IOANTWORT

Vergleichstelegramm  setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IOANTWORT | string | Antwort, die das SG sendet, wenn Daten akzeptiert sind |
| MASKE | string | Maske, die angibt, welche Bits der IOANTWORT mit der SG Antwort verglichen werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_KOMMANDOT | binary | Auftrag für Vergleichstelegramm |
| _TEL_KOMMANDOM | binary | Auftrag für Maske |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-tp"></a>
### STEUERN_DLE_TP

Tester Present ein / ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE | int | 1 = DNMT senden, TP zyklisch senden starten 0 = TP zyklisch senden stoppen, ENMT senden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-laden"></a>
### STEUERN_DLE_LADEN

Daten in den Ringpuffer laden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PUFFER | binary | Daten für den Ringpuffer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FREI | unsigned long | Anzahl der freien Bytes im Ringpuffer |
| FIFO_STATUS | string | Zustand des Ringpuffers {EMPTY, FILLED, OVERFLOW} |
| DLE_STATUS | string | Zustand der Download Engine {RUN, STOP, TIMEOUT, IFERR, COMERR, MISMATCH} |
| BLOCKS | unsigned long | Anzahl der fehlerfrei gesendeten Datentelegramme |
| SG_ANTWORT | binary | Letzte Antwort des SG bei Fehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-bufferclear"></a>
### STEUERN_DLE_BUFFERCLEAR

Ringpuffer löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des OPPS |

<a id="job-status-dle"></a>
### STATUS_DLE

DLE Status holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FREI | unsigned long | Anzahl der freien Bytes im Ringpuffer |
| FIFO_STATUS | string | Zustand des Ringpuffers {EMPTY, FILLED, OVERFLOW} |
| DLE_STATUS | string | Zustand der Download Engine {RUN, STOP, TIMEOUT, IFERR, COMERR, MISMATCH} |
| BLOCKS | unsigned long | Anzahl der fehlerfrei gesendeten Datentelegramme |
| SG_ANTWORT | binary | Letzte Antwort des SG bei Fehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-wait-for-dle"></a>
### WAIT_FOR_DLE

Warten bis die DLE alle Blocks geschrieben hat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FREI | unsigned long | Anzahl der freien Bytes im Ringpuffer |
| FIFO_STATUS | string | Zustand des Ringpuffers {EMPTY, FILLED, OVERFLOW} |
| DLE_STATUS | string | Zustand der Download Engine {RUN, STOP, TIMEOUT, IFERR, COMERR, MISMATCH} |
| BLOCKS | unsigned long | Anzahl der fehlerfrei gesendeten Datentelegramme |
| SG_ANTWORT | binary | Letzte Antwort des SG bei Fehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antworten des OPPS |

<a id="job-steuern-dle-odp"></a>
### STEUERN_DLE_ODP

Datenverbindung für DLE II öffnen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PORT | int | Portnummer, an der das Interface hört |
| STAT_IPADDR | string | IP-Adresse des Interfaces in "Dotted Notation" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des OPPS |

<a id="job-steuern-dle-sid"></a>
### STEUERN_DLE_SID

Service ID für DLE II setzen Der Service ID String wird von der DLE II automatisch Header und Daten eingefügt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SID | string | Service ID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Auftrag an das OPPS |
| _TEL_ANTWORT | binary | Antwort des OPPS |

## Tables

No tables found.
