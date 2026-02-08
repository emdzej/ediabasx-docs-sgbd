# c_video2.prg

- Jobs: [14](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD fuer Video-Flashprogrammierung |
| ORIGIN | BMW VS-22 Wittelsberger |
| REVISION | 1.00 |
| AUTHOR | BMW VS-22 Wittelsberger, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Videomodul TV-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Videomodul TV-Teil
- [CS_BILDEN](#job-cs-bilden)
- [DATEN_EEPROM_UEBERNEHMEN](#job-daten-eeprom-uebernehmen)
- [EEPROM_KENNUNG_LESEN](#job-eeprom-kennung-lesen)
- [RESET_VM](#job-reset-vm)
- [FLASH_LOESCHEN](#job-flash-loeschen)
- [BOOT_MODUS_AKTIVIEREN](#job-boot-modus-aktivieren)
- [BLOCKCHECKSUMME_LESEN](#job-blockchecksumme-lesen)
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten lesen
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen beschreiben
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum: Woche |
| ID_DATUM_JAHR | string | Herstelldatum: Jahr |
| ID_LIEF_NR | string | Lieferant-Nummer |
| ID_LIEF_TEXT | string | Lieferant im Klartext |
| ID_SW_NR | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-cs-bilden"></a>
### CS_BILDEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-daten-eeprom-uebernehmen"></a>
### DATEN_EEPROM_UEBERNEHMEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-eeprom-kennung-lesen"></a>
### EEPROM_KENNUNG_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-reset-vm"></a>
### RESET_VM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-boot-modus-aktivieren"></a>
### BOOT_MODUS_AKTIVIEREN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-blockchecksumme-lesen"></a>
### BLOCKCHECKSUMME_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| B0B1 | int | Byte fuer unterscheidung Block 0 oder Block 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation(ACK..) |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |
| CHKSUMME | string |  |

<a id="job-c-s-auftrag"></a>
### C_S_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-lesen"></a>
### C_S_LESEN

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

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", als Dummy |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (2 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [SEGMENTAUSWAHL](#table-segmentauswahl) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 2 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | IBus Dauerhigh Abschaltung |
| 0x02 | Watchdog ausgeloest |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | I-Bus-Pufferueberlauf |
| 0x02 | I2 C Fehler zum Graphikteil |
| 0x03 | I2 C Fehler vom Graphikteil |
| 0x04 | Uebertemperatur im Videomodul |
| 0x05 | Audio-Fehler |
| 0x06 | RGB-Fehler |
| 0x07 | Video-Fehler |
| 0x08 | Sonstige-Fehler |
| 0x09 | EEPROM read Fehler |
| 0x0A | EEPROM write Fehler |
| 0x0B | EEPROM Checksumfehler |
| 0x0C | EEPROM Neuinitialisierung |
| 0x0D | Kein RGB Telegramm vom Graphikteil |
| 0xXY | unbekannte Fehlerart |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler nicht aktiv |
| 0x20 | Fehler aktiv |
| 0xXY | unbekannte Fehlerart |

<a id="table-segmentauswahl"></a>
### SEGMENTAUSWAHL

Dimensions: 6 rows × 2 columns

| SEGMENT | AUSWAHLTEXT |
| --- | --- |
| 0x02 | EPROM |
| 0x03 | EEPROM |
| 0x04 | internes RAM DATA |
| 0x05 | externes RAM XDATA |
| 0x0B | internes RAM IDATA |
| 0xXY | Unbekanntes Segment |

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
