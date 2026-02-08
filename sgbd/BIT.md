# BIT.prg

- Jobs: [17](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Basis-Interface Telefon |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.3 |
| AUTHOR | BMW TI-433 Spoljarec, BMW TI-431 Rochal |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer BMW-TELEFON
- [IDENT](#job-ident) - Ident-Daten fuer das BIT
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [STATUS_IO_LESEN](#job-status-io-lesen) - verschiedenen Status IO-Ports
- [STATUS_LESEN](#job-status-lesen) - verschiedenen SG-Status lesen
- [STEUERN_DIGITAL](#job-steuern-digital) - Ports im Bit setzen
- [SELBSTTEST](#job-selbsttest) - Durchfuehrung des Selbsttests (Ermittlung Checksum SW)
- [SELBSTTEST_HW](#job-selbsttest-hw) - Durchfuehrung des hardwarespez. Selbsttests (Ports)
- [SLEEP_MODE](#job-sleep-mode) - versetzen des SGs in den sleepmode ca. 2 Sek. nach senden von ACK geht das SG in dne Power down Aufwecken nur durch einen Reset
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

Ident-Daten fuer das BIT

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
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart (entweder 0 oder 32) |
| F_ART1_TEXT | string | 1. Fehlerart als Text table FArtTexte ARTTEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |

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
| STAT_DATA1 | int | Inhalt Datenbyte 1 der Portzustaende |
| STAT_DATA2 | int | Inhalt Datenbyte 2 der Portzustaende |
| STAT_DATA3 | int | Inhalt Datenbyte 3 der Portzustaende |
| STAT_KOMPENSOR_DIAG_EIN | int |  |
| STAT_IGNITION_DIAG | int |  |
| STAT_CHARGE_DIAG_EIN | int |  |
| STAT_DSP_DIAG_EIN | int |  |
| STAT_MUTE_DIAG_EIN | int |  |
| STAT_CRASHSENSOR_EIN | int |  |
| STAT_KL_R_EIN | int |  |
| STAT_PANIK_TASTE_EIN | int |  |
| STAT_VOLUME | int |  |
| STAT_STANDBY_EIN | int |  |
| STAT_NOK_SIE | int |  |
| STAT_MOIS | int |  |
| STAT_DATA_TO_MOBILE | int |  |
| STAT_DATA_TO_BIT | int |  |
| STAT_CLK_A | int |  |
| STAT_KLINGEL_INPUT | int |  |
| STAT_TIMER_TST | int |  |
| STAT_ENABLE_RESET | int |  |
| STAT_ENABLE_RESET_TIMER | int |  |
| STAT_RX1_BIT | int |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

verschiedenen SG-Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_WARMSTART | int | Warmstart erfolgt? |
| STAT_KLEMME_R | int | Warmstart durch Klemme R erfolgt? |
| STAT_I_BUS | int | Warmstart durch ein I-BUS-Telegraqmm erfolgt? |
| STAT_TELEFONBUS | int | Warmstart durch den Telefonbus erfolgt? |
| STAT_ZUBEHOERBUS | int | Warmstart durch den Zubehoerbus erfolgt? |
| STAT_RESET_TIMER | int | Warmstart durch den Reset-timer erfolgt? |
| STAT_HANDY_TYP | string | Handy Typ (Nokia oder Siemens) |
| STAT_INTERNE_SW | string | interne SW z.B. 01.00 |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ports im Bit setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL | int | 00 -&gt; Ports, 01 -&gt; Freisprechlautstaerke |
| DATA1 | int | Auswahl 00 -&gt; diverse Prots, 01 -&gt; Freisprechlautstaerke |
| DATA2 | int | Auswahl 00 -&gt; diverse Prots, 01 -&gt; Freisprechlautstaerke |

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
| CHK_1 | int | Checksumme ueber den Adressbereich 0x00000-0x03FFF Sollvorgabe abhaengig vom internen SW-Stand |
| CHK_2 | int | Checksumme ueber den Adressbereich 0x08000-0x7FEFF Sollvorgabe abhaengig vom internen SW-Stand |

<a id="job-selbsttest-hw"></a>
### SELBSTTEST_HW

Durchfuehrung des hardwarespez. Selbsttests (Ports)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ERROR_SUPPLY_SET | int | 1 -&gt; Fehler beim Setzen des Ports Supply |
| ERROR_SUPPLY_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports Supply |
| ERROR_IGNITION_SET | int | 1 -&gt; Fehler beim Setzen des Ports Ignition |
| ERROR_IGNITION_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports Ignition |
| ERROR_CHARGE_SET | int | 1 -&gt; Fehler beim Setzen des Ports Charge |
| ERROR_CHARGE_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports Charge |
| ERROR_DSP_SET | int | 1 -&gt; Fehler beim Setzen des Ports DSP |
| ERROR_DSP_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports DSP |
| ERROR_MUTE_SET | int | 1 -&gt; Fehler beim Setzen des Ports Mute |
| ERROR_MUTE_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports Mute |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

versetzen des SGs in den sleepmode ca. 2 Sek. nach senden von ACK geht das SG in dne Power down Aufwecken nur durch einen Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

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

- [JOBRESULT](#table-jobresult) (6 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Fehler beim Einschalten von SUPPLY / KS Pin 38 nach Masse |
| 0x02 | Fehler beim Ausschalten von SUPPLY / KS Pin 38 nach Ubatt |
| 0x03 | Fehler beim Einschalten von IGNITION / KS Pin 39 nach Masse |
| 0x04 | Fehler beim Ausschalten von IGNITION / KS Pin 39 nach Ubatt |
| 0x05 | Fehler beim Einschalten von CHARGE / KS Pin 37 nach Masse |
| 0x06 | Fehler beim Ausschalten von CHARGE / KS Pin 37 nach Ubatt |
| 0x07 | Fehler beim Einschalten von DSP / KS Pin 5 nach Masse |
| 0x08 | Fehler beim Ausschalten von DPS / KS Pin 5 nach Ubatt |
| 0x09 | Fehler beim Einschalten von MUTE / KS Pin 4 nach Ubatt |
| 0x0A | Fehler beim Ausschalten von MUTE / KS Pin 4 nach Masse |
| 0x10 | Allgemeiner I-Bus-Fehler |
| 0x11 | Akku Ladezustand |
| 0x12 | GSM Pegel |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |
