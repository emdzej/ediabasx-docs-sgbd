# BIT2.prg

- Jobs: [22](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Basis-Interface Telefon 2 |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.1 |
| AUTHOR | BMW EE-430 Paeschke, TI-431 Krueger, TI-431 Holdsclaw, BMW TI-431 Rochal |
| COMMENT | BIT2 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
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
- [SELBSTTEST](#job-selbsttest) - Durchfuehrung des Selbsttests (Ermittlung Checksum SW)
- [SELBSTTEST_HW](#job-selbsttest-hw) - Durchfuehrung des hardwarespez. Selbsttests (Ports)
- [RESET](#job-reset) - Durchfuehrung eines resets ca. 2 Sek. nach senden von ACK erfolgt der Reset
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrecht erhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode beenden
- [IMEI_LESEN](#job-imei-lesen) - Identifikationsnummer (IMEI) der GSM Engine auslesen
- [RFPI_LESEN](#job-rfpi-lesen) - Identifikationsnummer (RFPI) der WDCT-Basis auslesen
- [SBDH_ANMELDEN](#job-sbdh-anmelden) - Anmelden eines SBDH an das S/E-Geraet
- [SBDH_ALLE_ABMELDEN](#job-sbdh-alle-abmelden) - Abmelden aller SBDHs vom S/E-Geraet
- [ECHO_CANC_DELAY_SETZEN](#job-echo-canc-delay-setzen) - Einstellen der Delay-Tap-Anzahl des Echo Cancellation Algorithmus der GSM Engine zur Optimierung des Freisprechbetriebes !!! Nur zu verwenden bei Problemen im Feld !!!
- [GERAETECODE_RUECKSETZEN](#job-geraetecode-ruecksetzen) - Ruecksetzen des Geraetecodes, falls der Kunde ihn vergessen hat

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| STAT_WDCOFFI_EIN | int | Status des WDCT-Schalters |
| STAT_TEL_ON1_DIAG_EIN | int | Schaltleitung fuer vordere Ejectbox |
| STAT_TEL_ON2_DIAG_EIN | int | Schaltleitung fuer hintere Ejectbox |
| STAT_DSP_DIAG_EIN | int |  |
| STAT_MUTE_DIAG_EIN | int | Radio-MUTE-Leitung |
| STAT_RXD_NAVI_EIN | int | DFUE-Schnittstelle - Empfangsleitung RxD |
| STAT_KL_R_EIN | int | Status Klemme R |
| STAT_CTS_NAVI_EIN | int | DFUE-Schnittstelle - Handshake-Leitung CTS |
| STAT_A20_SWAKTIV_EIN | int | Status der SW der GSM Engine |
| STAT_SBDH_SWAKTIV_EIN | int | Status der SW der WDCT-Basis |
| STAT_U_BATT | int | Messwert der Bordspannung in Deci-Volt |

<a id="job-status-lesen"></a>
### STATUS_LESEN

verschiedenen SG-Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_INTERNE_SW | string | interne Software-Versionen: A=GSM Engine, B=WDCT-Basis, C=Motherboard |
| STAT_INTERNE_HW | string | interne Hardware-Versionen: A, B und C wie oben |

<a id="job-selbsttest"></a>
### SELBSTTEST

Durchfuehrung des Selbsttests (Ermittlung Checksum SW)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| CHECKSUM | int | Checksumme Sollvorgabe abhaengig vom internen SW-Stand |

<a id="job-selbsttest-hw"></a>
### SELBSTTEST_HW

Durchfuehrung des hardwarespez. Selbsttests (Ports)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ERROR_TEL_ON1_SET | int | 1 -&gt; Fehler beim Setzen des Ports TEL_ON1 |
| ERROR_TEL_ON1_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports TEL_ON1 |
| ERROR_TEL_ON2_SET | int | 1 -&gt; Fehler beim Setzen des Ports TEL_ON2 |
| ERROR_TEL_ON2_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports TEL_ON2 |
| ERROR_DSP_SET | int | 1 -&gt; Fehler beim Setzen des Ports DSP |
| ERROR_DSP_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports DSP |
| ERROR_MUTE_SET | int | 1 -&gt; Fehler beim Setzen des Ports Mute |
| ERROR_MUTE_RESET | int | 1 -&gt; Fehler beim Ruecksetzen des Ports Mute |

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

<a id="job-imei-lesen"></a>
### IMEI_LESEN

Identifikationsnummer (IMEI) der GSM Engine auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_IMEI | string | IMEI der GSM Engine (15 Stellen ASCII) |

<a id="job-rfpi-lesen"></a>
### RFPI_LESEN

Identifikationsnummer (RFPI) der WDCT-Basis auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_RFPI | string | RFPI der WDCT-Basis (10 Stellen ASCII) |

<a id="job-sbdh-anmelden"></a>
### SBDH_ANMELDEN

Anmelden eines SBDH an das S/E-Geraet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-sbdh-alle-abmelden"></a>
### SBDH_ALLE_ABMELDEN

Abmelden aller SBDHs vom S/E-Geraet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-echo-canc-delay-setzen"></a>
### ECHO_CANC_DELAY_SETZEN

Einstellen der Delay-Tap-Anzahl des Echo Cancellation Algorithmus der GSM Engine zur Optimierung des Freisprechbetriebes !!! Nur zu verwenden bei Problemen im Feld !!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Anzahl der Delay Taps (0...28h) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-geraetecode-ruecksetzen"></a>
### GERAETECODE_RUECKSETZEN

Ruecksetzen des Geraetecodes, falls der Kunde ihn vergessen hat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)

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

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Fehler beim Einschalten der GSM Engine / interner Fehler |
| 0x02 | Fehler beim Einschalten der WDCT-Basis / interner Fehler |
| 0x03 | Fehler beim Einschalten von TEL_ON1 / KS Pin 1 nach Masse |
| 0x04 | Fehler beim Ausschalten von TEL_ON1 / KS Pin 1 nach Ubatt |
| 0x05 | Fehler beim Einschalten von TEL_ON2 / KS Pin 5 nach Masse |
| 0x06 | Fehler beim Ausschalten von TEL_ON2 / KS Pin 5 nach Ubatt |
| 0x07 | Fehler beim Einschalten von DSP / KS Pin 47 nach Masse |
| 0x08 | Fehler beim Ausschalten von DSP / KS Pin 47 nach Ubatt |
| 0x09 | Fehler beim Einschalten von MUTE / KS Pin 29 nach Ubatt |
| 0x0A | Fehler beim Ausschalten von MUTE / KS Pin 29 nach Masse |
| 0x10 | Allgemeiner I-Bus-Fehler |
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
