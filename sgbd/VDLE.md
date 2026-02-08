# VDLE.prg

- Jobs: [8](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Virtuelle Download Engine |
| ORIGIN | BMW VS-43 Rowedder |
| REVISION | 1.001 |
| AUTHOR | VS-43 Frank Wegener, VS-43 Michael Rowedder |
| COMMENT | Steuer-SGBD für Virtuelle Download Engine Emulation |
| PACKAGE | 1.40 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung)
- [INIT_VDLE](#job-init-vdle) - Segment aus IntelHex in ECU laden
- [START_TESTERPRESENT](#job-start-testerpresent) - Start TesterPresent
- [STOP_TESTERPRESENT](#job-stop-testerpresent) - Stop TesterPresent
- [REQUEST_SEGMENTINFO](#job-request-segmentinfo) - SegmentAddr und SegmentSize in Buf vereitstellen
- [SEND_SEGMENT](#job-send-segment) - Segment aus IntelHex in ECU laden
- [EXIT_VDLE](#job-exit-vdle) - Beenden VDLE Sitzung ggf. temporäre Dateien entfernen

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

<a id="job-init-vdle"></a>
### INIT_VDLE

Segment aus IntelHex in ECU laden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |
| DLL_NR_OF_SEGMENTS | int | Anzahl der Segemente des IntelHexFiles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| NR_OF_SEGMENTS | int | Anzahl der Segemente des IntelHexFiles |

<a id="job-start-testerpresent"></a>
### START_TESTERPRESENT

Start TesterPresent

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-stop-testerpresent"></a>
### STOP_TESTERPRESENT

Stop TesterPresent

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-request-segmentinfo"></a>
### REQUEST_SEGMENTINFO

SegmentAddr und SegmentSize in Buf vereitstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |
| DLL_SEGMENT_ADDR | unsigned long |  |
| DLL_SEGMENT_SIZE | unsigned long |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| REQUESTDOWNLOADBUFFER | binary | Buffer for Segment Adress and Size Infos |

<a id="job-send-segment"></a>
### SEND_SEGMENT

Segment aus IntelHex in ECU laden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |
| DLL_FLASH_SCHREIBEN_STATUS | int |  |
| DLL_ERROR_MSG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| FLASH_SCHREIBEN_STATUS | int | +1, wenn fehlerfrei |
| ERROR_MSG | string |  |

<a id="job-exit-vdle"></a>
### EXIT_VDLE

Beenden VDLE Sitzung ggf. temporäre Dateien entfernen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DLL_JOB_STATUS | string | JobStatus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

No tables found.
