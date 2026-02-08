# mrarad.prg

- Jobs: [3](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | RAD Steuergeraet Motorrad  |
| ORIGIN | BMW Motorrad |
| REVISION | 1.000 |
| AUTHOR | Kufer |
| COMMENT | Nur fuer ISTA |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Fakeantwort notwendig wegen ISTA zur Steuerung SG-Baum

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

## Tables

No tables found.
