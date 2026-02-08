# c_ews.prg

- Jobs: [11](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD EWS 2 |
| ORIGIN | BMW TI-433 Mario Spoljarec |
| REVISION | 1.01 |
| AUTHOR | BMW TI-433 Mario Spoljarec |
| COMMENT | Verifiziert |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EWS
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STATUS_LESEN](#job-status-lesen) - Stati der EWS
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer aus der EWS
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Schreiben der 17-stelligen Fahrgestellnummer (incl. Pruefziffer)
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Auslesen des Zentralen Codierschluessels aus KD-Daten
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Schreiben des Zentralen Codierschluessels in die KD-Daten (incl. verify)
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren

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

Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Stati der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DME_LEITUNG_FREI | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_DREHZAHL | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_P_N | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_EEPROM_TRANSPONDER_WC_DEFEKT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_EWS_JUNGFRAEULICH | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_P_N_EINGANG | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WFSI_EINGANG | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_BC_EINGANG | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_MOTORDREHZAHL | real | (5 bis 254)/0.3 1/s |
| STAT_AKTUELLE_SCHLUESSELNUMMER | int | 0 bis 9 |
| STAT_SE_MODUL_SENDET | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KLEMME_R_EIN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_WC | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_ID | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_PW | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_GESPERRT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_AKTUELLE_SCHLUESSEL_ID | binary | 8 Byte |
| STAT_AKTUELLE_SCHLUESSEL_ID_TEXT | string | 8 Byte |
| STAT_AKTUELLER_WC | binary | 8 Byte |
| STAT_AKTUELLER_WC_TEXT | string | 8 Byte |
| STAT_VORGABE_DME | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ANLASSERRELAIS | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ENTRIEGELN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_DME_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ANLASSERRELAIS_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ENTRIEGELN_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Schreiben der 17-stelligen Fahrgestellnummer (incl. Pruefziffer)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Auslesen des Zentralen Codierschluessels aus KD-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| GM | string | Zentralcode C1 - Grundmerkmal |
| SA | string | Zentralcode C2 - Sonderausstattung |
| VN | string | Zentralcode C3 - Versionsnummer |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-c-zcs-auftrag"></a>
### C_ZCS_AUFTRAG

Schreiben des Zentralen Codierschluessels in die KD-Daten (incl. verify)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal |
| SA | string | Zentralcode C2 - Sonderausstattung |
| VN | string | Zentralcode C3 - Versionsmerkmal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

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
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0xFF | unbekannter Hersteller |
