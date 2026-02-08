# RIP.prg

- Jobs: [11](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Remote Instrument Pack |
| ORIGIN | BMW TI-431 Lothar Dennert |
| REVISION | 1.4 |
| AUTHOR | Software-Style M.Rafferty |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Ident-Daten fuer Instrument Pack
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten lesen Read the coding data
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren Write and then verify the coding data
- [C_S_SCHREIBEN](#job-c-s-schreiben) - Codierdaten schreiben
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Read the Test Stamp Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Read the Test Stamp Beschreiben des Pruefstempels
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Herstellerdaten auslesen Read supplier specific data

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Instrument Pack

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_SW_NR | int | Softwarenummer |
| ID_CAN_INDEX | int | Can Index |
| ID_AENDERUNG_INDEX | int | Modification Index (minor software modifications) |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-s-lesen"></a>
### C_S_LESEN

Codierdaten lesen Read the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17,18,19,20:     Wortadresse (low/highbyte, low/highword) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-s-auftrag"></a>
### C_S_AUFTRAG

Codierdaten schreiben und verifizieren Write and then verify the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17,18,19,20:     Wortadresse (low/highbyte, low/highword) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write coding data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write coding data response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read coding data response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-s-schreiben"></a>
### C_S_SCHREIBEN

Codierdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Read the Test Stamp Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Pruefstempel Datenbyte1 |
| BYTE2 | int | Pruefstempel Datenbyte2 |
| BYTE3 | int | Pruefstempel Datenbyte3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Read the Test Stamp Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE2 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE3 | int | kann beliebig verwendet werden (0x00-0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Herstellerdaten auslesen Read supplier specific data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Blockadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKINHALT | binary | Daten des Blocks |
| LAENGE | int | Länge des Blocks |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [SUPPLIERDATA](#table-supplierdata) (2 × 2)

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

<a id="table-supplierdata"></a>
### SUPPLIERDATA

Dimensions: 2 rows × 2 columns

| INDEX | INFO |
| --- | --- |
| 0x00 | Additional Software Identification |
| 0x01 | Electronic / PCB Index |
