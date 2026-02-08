# c_shd_s.prg

- Jobs: [8](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD fuer HO-Servicemassnahmen |
| ORIGIN | BMW VS-22 Wittelsberger |
| REVISION | 1.00 |
| AUTHOR | BMW VS-22 Wittelsberger, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | N/A |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer GM III
- [TESTEN_SHD_PATCH](#job-testen-shd-patch) - ACHTUNG: nur E38,E39,E39/2 mit SW02,SW03,SW05 Testen der Daten des SHD bzgl. Uebernahme eins SW-Patch
- [SCHREIBEN_BCS_PATCH](#job-schreiben-bcs-patch) - ACHTUNG: nur fuer E38,E39, E39/2 SW 02, SW 03  SW 05! Zusaetzlicher Patch wegen Feldproblemen ab 9/97
- [PATCH_INFO_LESEN](#job-patch-info-lesen) - Auslesen der Patch Info 
- [PATCH_DATEN_LESEN](#job-patch-daten-lesen) - Auslesen der Patch Daten 
- [SHD_INITIALISIERUNG_NACH_PATCH](#job-shd-initialisierung-nach-patch) - Initialisierung nach Patch Daten schrieben 

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer GM III

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| P_MODUL | string | gewuenschtes Peripheriemodul table PeripherieModule PM_ABK PM_TEXT |

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

<a id="job-testen-shd-patch"></a>
### TESTEN_SHD_PATCH

ACHTUNG: nur E38,E39,E39/2 mit SW02,SW03,SW05 Testen der Daten des SHD bzgl. Uebernahme eins SW-Patch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| PATCH_OK | int | 1: Patch = IO / 0: Patch = NIO |
| _TEL_ANTWORT | binary |  |

<a id="job-schreiben-bcs-patch"></a>
### SCHREIBEN_BCS_PATCH

ACHTUNG: nur fuer E38,E39, E39/2 SW 02, SW 03  SW 05! Zusaetzlicher Patch wegen Feldproblemen ab 9/97

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-patch-info-lesen"></a>
### PATCH_INFO_LESEN

Auslesen der Patch Info 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| PATCH_NR | string | Auslesen der Speicherzelle 0xb661 |
| CHECKSUMME1 | string | Auslesen der Speicherzelle 0xb689 |
| CHECKSUMME2 | string | Auslesen der Speicherzelle 0xb68A |
| PATCH_SOURCE | string | zur Bestimmung wer den Patch geschrieben hat (Speicherzelle 0xB65D) |

<a id="job-patch-daten-lesen"></a>
### PATCH_DATEN_LESEN

Auslesen der Patch Daten 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-shd-initialisierung-nach-patch"></a>
### SHD_INITIALISIERUNG_NACH_PATCH

Initialisierung nach Patch Daten schrieben 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [PERIPHERIEMODULE](#table-peripheriemodule) (9 × 3)
- [PERIPHERIEMODULE_HD](#table-peripheriemodule-hd) (5 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-peripheriemodule"></a>
### PERIPHERIEMODULE

Dimensions: 9 rows × 3 columns

| PM_NR | PM_ABK | PM_TEXT |
| --- | --- | --- |
| 0x00 | GM3 | @Grundmodul@ III |
| 0x01 | FT | @Fahrertuer@ |
| 0x02 | BT | @Beifahrertuer@ |
| 0x03 | SHD | @Schiebehebedach@ |
| 0x04 | SB | @Schalterblock@ |
| 0x05 | SM_LSM | @Sitz/Lenksaeulenmemory@ @Fahrer@ |
| 0x08 | SM_BF | @Sitzmemory@ @Beifahrer@ |
| 0x09 | SM_SFB | @Sitzmemory@ @Fernbedienung@ @Beifahrersitz@ |
| 0xXY | XY | ERROR_PM_UNBEKANNT |

<a id="table-peripheriemodule-hd"></a>
### PERIPHERIEMODULE_HD

Dimensions: 5 rows × 3 columns

| PM_NR | PM_ABK | PM_TEXT |
| --- | --- | --- |
| 0x00 | GM3 | @Grundmodul@ III |
| 0x01 | FT | @Fahrertuer@ |
| 0x02 | BT | @Beifahrertuer@ |
| 0x03 | SHD | @Schiebehebedach@ |
| 0xXY | XY | ERROR_PM_NICHT_ERLAUBT |

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

Dimensions: 27 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
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
| 0xXY | @unbekannter Hersteller@ |
