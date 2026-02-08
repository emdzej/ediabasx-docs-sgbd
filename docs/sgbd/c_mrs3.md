# c_mrs3.prg

- Jobs: [13](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD MRS3 |
| ORIGIN | BMW TI-433 Lothar Dennert |
| REVISION | 1.07 |
| AUTHOR | BMW TI-433 Mario Spoljarec, BMW TI-433 Lothar Dennert |
| COMMENT | Verifiziert |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG MRS 3
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG MRS 3
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [C_FS_LOESCHEN](#job-c-fs-loeschen) - Fehlerspeicher loeschen
- [C_LOGIN](#job-c-login)
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_PRUEFSTEMPEL_LESEN](#job-c-pruefstempel-lesen) - Auslesen des Pruefstempels
- [C_PRUEFSTEMPEL_SETZEN](#job-c-pruefstempel-setzen) - Verriegeln des SGs
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen der Verriegelung (= Pruefstempel)
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen

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

Init-Job fuer AIRBAG MRS 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG MRS 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-c-fs-loeschen"></a>
### C_FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-c-login"></a>
### C_LOGIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOGIN_CODE | binary | Login Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY, wenn fehlerfrei" |
| TELEGRAMM | binary | antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

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

<a id="job-c-pruefstempel-lesen"></a>
### C_PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| PRUEFSTEMPEL | binary |  |

<a id="job-c-pruefstempel-setzen"></a>
### C_PRUEFSTEMPEL_SETZEN

Verriegeln des SGs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRUEFSTEMPEL | binary | Pruefstempel zum verriegeln des SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen der Verriegelung (= Pruefstempel)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | Datenbyte 1 |
| BYTE2 | int | Datenbyte 2 |
| BYTE3 | int | Datenbyte 3 |

<a id="job-verriegelung-schreiben"></a>
### VERRIEGELUNG_SCHREIBEN

Verriegelungsbytes setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ERROR_CODE | string | OKAY, FEHLER |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xB2 | ERROR_ECU_NUMBER |
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
| 0x19 | @Elektromatik Suedafrika@ |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0xFF | @unbekannter Hersteller@ |
