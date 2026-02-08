# edic_c.prg

- Jobs: [8](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | NPS 10  Sonderfunktionen für Bandendeprogramierung |
| ORIGIN | Softing GmbH Stadtmueller |
| REVISION | 1.00 |
| AUTHOR | Softing GmbH Stadtmueller |
| COMMENT | Ansteuerung der NPS-Hardware |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [ENDE](#job-ende) - Stoppen des wiederholten Senden und Empfangen
- [STATUS_LESEN](#job-status-lesen) - Holen des Status der Schlitten
- [SPANNUNG_SG_EIN](#job-spannung-sg-ein) - Spannungsversorgung ein
- [SPANNUNG_SG_AUS](#job-spannung-sg-aus) - Spannungsversorgung aus
- [AUFNAHME_AUS](#job-aufnahme-aus) - Schlitten abschalten
- [AUFNAHME_EIN](#job-aufnahme-ein) - Schlitten einschalten

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ende"></a>
### ENDE

Stoppen des wiederholten Senden und Empfangen

_No arguments._

_No results._

<a id="job-status-lesen"></a>
### STATUS_LESEN

Holen des Status der Schlitten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |
| LINKER_SCHLITTEN_AKTIV | int | Abfrage des linken Schlittens |
| RECHTER_SCHLITTEN_AKTIV | int | Abfrage des rechten Schlittens |
| KEIN_SCHLITTEN_AKTIV | int | Keiner der beiden Schlitten |

<a id="job-spannung-sg-ein"></a>
### SPANNUNG_SG_EIN

Spannungsversorgung ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-spannung-sg-aus"></a>
### SPANNUNG_SG_AUS

Spannungsversorgung aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-aufnahme-aus"></a>
### AUFNAHME_AUS

Schlitten abschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-aufnahme-ein"></a>
### AUFNAHME_EIN

Schlitten einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

## Tables

No tables found.
