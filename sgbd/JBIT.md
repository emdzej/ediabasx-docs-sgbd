# JBIT.prg

- Jobs: [13](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | JBIT |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.1 |
| AUTHOR | BMW EE-43 Groene, BMW TI-431 Krueger, S&S E.Genseleiter, BMW TI-431 Rochal |
| COMMENT | JBIT |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer BMW-TELEFON
- [IDENT](#job-ident) - Ident-Daten fuer das JBIT
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [STATUS_IO_LESEN](#job-status-io-lesen) - verschiedenen Status IO-Ports
- [STEUERN_DIGITAL](#job-steuern-digital) - Ports im JBIT setzen
- [SELBSTTEST](#job-selbsttest) - Durchfuehrung des Selbsttests (Ermittlung Checksum SW)
- [RESET](#job-reset) - Durchfuehrung eines resets ca. 2 Sek. nach senden von ACK erfolgt der Reset
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrecht erhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode beenden

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

Init-Job fuer BMW-TELEFON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer das JBIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_CODE | int | Fehlercode |
| F_TEXT | string | Fehlertext |
| F_COUNTER | int | Fehlerhaeufigkeit des jeweiligen Fehlers |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

verschiedenen Status IO-Ports

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_MOBILE_PHONE | int | mobile phone switched off (0) or on (1)? |
| STAT_EBX_LID_SW | int | eject-box lid is down (0) or up (1) |
| STAT_EBX_TRAY_SW | int | eject-box tray is down (0) or up (1) |
| STAT_TALK_VOLUME_WERT | int | talking volume level, 0 &lt;= vol &lt;= 11 |
| STAT_TALK_VOLUME_EINH | string |  |
| STAT_RING_VOLUME_WERT | int | ringing volume level, 0 &lt;= vol &lt;= 11 |
| STAT_RING_VOLUME_EINH | string |  |
| STAT_RADIO_MUTE | int | muting if off (0) or on (1) |
| STAT_EBX_TEMP | int | eject-box temperature allows phone battery charing: no (0) or yes (1) |
| STAT_DSP_TEL_ON | int | TEL_ON signal for DSP: off (0) or on (1) |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ports im JBIT setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SWITCH_MOBILE_PHONE | int | switch mobile phone off (00h) or on (01h) |
| TALK_VOLUME | int | talking volume: 0...11 |
| RING_VOLUME | int | ringing volume: 0...11 |
| RAD_MUTE | int | radio mute signal off (00h) or on (01h) |
| DSP_TEL_ON | int | TEL_ON signal for DSP off (00h) or on (01h) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-selbsttest"></a>
### SELBSTTEST

Durchfuehrung des Selbsttests (Ermittlung Checksum SW)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TOTAL_CHECK | int | OK = 00h, Not OK = 01h |
| SRAM_CHECK | int | OK = 00h, Not OK = 01h |
| FLASH_ROM_CHECK | int | OK = 00h, Not OK = 01h |
| EEPROM_CHECK | int | OK = 00h, Not OK = 01h |
| COMM_WITH_PHONE_CHECK | int | communication with mobile phone check OK = 00h , Not OK = 01h |

<a id="job-reset"></a>
### RESET

Durchfuehrung eines resets ca. 2 Sek. nach senden von ACK erfolgt der Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose aufrecht erhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (5 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Fehler in der Spannungsversorgung |
| 0x01 | Fehler EEPROM Checksumme |
| 0x02 | Fehler Checksumme I-bus Telegramm |
| 0x03 | Ausserhalb des Temperaturbereich fuer laden |
| 0xFF | unbekannte Fehler Nummer |
