# FBZV.prg

- Jobs: [13](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Funkfernbedienung fuer Zentralverriegelung E38 |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.14 |
| AUTHOR | BMW TP-421 Penzenstadler, BMW TP-421 Mehringer, BMW TP-421 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default Initialisierung der Kommunikation via EDIC
- [IDENT](#job-ident) - Identifizierung SG lesen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher Sg lesen und auswerten Pro Fehler wird ein Ergenbissatz gebildet
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STATUS_KLEMME_R_EIN](#job-status-klemme-r-ein) - Status Klemme R abfragen
- [STEUERN_TEST_EMPFANG](#job-steuern-test-empfang) - Steuern Selbsttestfunktion HF-Empfang
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [CODE_SCHREIBEN](#job-code-schreiben) - Schreiben der Codierdaten
- [CODE_LESEN](#job-code-lesen) - Auslesen der Codierdaten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beendet Kommuniktion mit SG DUMMY
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Aufrechterhalten Kommuniktion mit SG

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

Default Initialisierung der Kommunikation via EDIC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done/true |

<a id="job-ident"></a>
### IDENT

Identifizierung SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn Fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher Sg lesen und auswerten Pro Fehler wird ein Ergenbissatz gebildet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn erfolgreich |
| F_ORT_NR | int | Fehlerort Index |
| F_ORT_TEXT | string | Text des Fehlers |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn erfolgreich |

<a id="job-status-klemme-r-ein"></a>
### STATUS_KLEMME_R_EIN

Status Klemme R abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLEMME_R_EIN_WERT | int | 1=true / 0=false |
| STAT_KLEMME_R_EIN_TEXT | string | "EIN" / "AUS" |

<a id="job-steuern-test-empfang"></a>
### STEUERN_TEST_EMPFANG

Steuern Selbsttestfunktion HF-Empfang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_RX_OKAY_WERT | int | 1 = true / 0 = false |
| STAT_RX_OKAY_TEXT | string | 'korrekter Empfang','fehlerhafter Empfang' |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE2 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE3 | int | kann beliebig verwendet werden 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-code-schreiben"></a>
### CODE_SCHREIBEN

Schreiben der Codierdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMFORT_OPEN | int | "1", wenn Komfortoeffnen aktiv |
| PANIC_ACTIVE | int | "1", Panik-Mode-Aktivierung |
| ZS_MODE | int | "1", wenn Zentralsicherung sofort "0", wenn Zentralsicherung nach zweiter Betaetigung |
| PANIC_DELAY | int | "0", delta t = 2sec "1", delta t = 3sec "2", delta t = 4sec "3", delta t = 5sec |
| RANGE_OPEN | int | "1", wenn Reichweiten Oeffnen reduziert |
| RANGE_CLOSE | int | "1", wenn Reichweite Schliessen reduziert |
| KOMFORT_CLOSE | int | "1", wenn Komfortschliessen aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn erfolgreich |

<a id="job-code-lesen"></a>
### CODE_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn erfolgreich |
| KOMFORT_OPEN | int | "1", wenn Komfortoeffnen aktiv |
| PANIC_ACTIVE | int | "1", Panik-Mode-Aktivierung gesetzt |
| ZS_MODE | int | "1", wenn Zentralsicherung sofort "0", wenn Zentralsicherung nach zweiter Betaetigung |
| PANIC_DELAY | int | "2", delta t = 2sec "3", delta t = 3sec "4", delta t = 4sec "5", delta t = 5sec |
| RANGE_OPEN | int | "1", wenn Reichweiten Oeffnen reduziert |
| RANGE_CLOSE | int | "1", wenn Reichweite Schliessen reduziert |
| KOMFORT_CLOSE | int | "1", wenn Komfortschliessen aktiv |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beendet Kommuniktion mit SG DUMMY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Aufrechterhalten Kommuniktion mit SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (4 × 2)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 4 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Batteriefehler in Transmitter 1 |
| 0x02 | Batteriefehler in Transmitter 2 |
| 0x03 | Batteriefehler in Transmitter 3 |
| 0x04 | Batteriefehler in Transmitter 4 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |
