# RCC.prg

- Jobs: [13](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Funkuhrmodul - Radio Controlled Clock |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 1.00 |
| AUTHOR | BMW TP-422 Zender, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INFO](#job-info) - Information SGBD
- [EEPROM_LESEN](#job-eeprom-lesen) - Daten aus dem EEPROM auslesen
- [RAM_LESEN](#job-ram-lesen) - RAM-Daten auslesen
- [STATUS_FELDSTAERKE_LESEN](#job-status-feldstaerke-lesen) - gibt die aktuelle Feldstaerke des empfangenen Funkuhrsignals an
- [STATUS_ZEITSTEMPEL_LESEN](#job-status-zeitstempel-lesen) - gibt die Empfangshistorie wieder
- [STATUS_TESTINFO_LESEN](#job-status-testinfo-lesen) - Lieferantentestinformation auslesen
- [STEUERN_ANTENNENVERSTAERKER_EIN](#job-steuern-antennenverstaerker-ein) - Einschalten des Antennenverstaerkers
- [STEUERN_ANTENNENVERSTAERKER_AUS](#job-steuern-antennenverstaerker-aus) - Ausschalten des Antennenverstaerkers
- [STEUERN_ZEITINFO_SENDEN](#job-steuern-zeitinfo-senden) - Fordert RCC auf, die Zeitinfo auf dem I/K-Bus auszugeben
- [SOFT_RESET](#job-soft-reset) - Loest selbststaendig einen Reset aus

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Daten aus dem EEPROM auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00 - 0xFF) der Wortadresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der 2-Byte-Worte (max. 6 Worte = 12 Bytes), die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATEN | binary | Datenfeld |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM-Daten auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00 - 0xFF) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 12 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATEN | binary | Datenfeld |

<a id="job-status-feldstaerke-lesen"></a>
### STATUS_FELDSTAERKE_LESEN

gibt die aktuelle Feldstaerke des empfangenen Funkuhrsignals an

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STATUS_FELDSTAERKE | int | gibt die Staerke des empfangenen Funkuhrsignals in einer Skala von 0 bis 15 an |

<a id="job-status-zeitstempel-lesen"></a>
### STATUS_ZEITSTEMPEL_LESEN

gibt die Empfangshistorie wieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMMER | int | Nummer [1-5] des gewuenschten Zeitstempels, 1 = jung, 5 = alt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| ZEITSTEMPEL_NUMMER | int | Nummer [1-5] des Zeitstempels, 1 = jung, 5 = alt |
| ZEITSTEMPEL_STUNDE | int | Stundenangabe des Zeitstempels |
| ZEITSTEMPEL_MINUTE | int | Minutenangabe des Zeitstempels |
| ZEITSTEMPEL_TAG | int | Tagangabe des Zeitstempels |
| ZEITSTEMPEL_MONAT | int | Monatsangabe des Zeitstempels |

<a id="job-status-testinfo-lesen"></a>
### STATUS_TESTINFO_LESEN

Lieferantentestinformation auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STATUS_LIEFERANTENTESTINFO | int | gibt die Lieferantentestinformation aus |

<a id="job-steuern-antennenverstaerker-ein"></a>
### STEUERN_ANTENNENVERSTAERKER_EIN

Einschalten des Antennenverstaerkers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-steuern-antennenverstaerker-aus"></a>
### STEUERN_ANTENNENVERSTAERKER_AUS

Ausschalten des Antennenverstaerkers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-steuern-zeitinfo-senden"></a>
### STEUERN_ZEITINFO_SENDEN

Fordert RCC auf, die Zeitinfo auf dem I/K-Bus auszugeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |

<a id="job-soft-reset"></a>
### SOFT_RESET

Loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)

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

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
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
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0xFF | unbekannter Hersteller |
