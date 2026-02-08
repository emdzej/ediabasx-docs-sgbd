# EKP_III.PRG

- Jobs: [11](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EKP III |
| ORIGIN | BMW |
| REVISION | 0.02 |
| AUTHOR | HELBAKO E2 Spanner |
| COMMENT | SGBD fuer EKP III |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [CODIERUNG_LESEN](#job-codierung-lesen) - Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten schreiben und verifizieren
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [ADU_WERTE_LESEN](#job-adu-werte-lesen) - es werden die Messwerte des AD-Umsetzers ausgelesen
- [EKP_DATEN_LESEN](#job-ekp-daten-lesen) - es werden die Messwerte des AD-Umsetzers ausgelesen

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

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNUMMER | int | zulaessige Blocknummern liegen i Bereich 0x0000 - 0x0004 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Es werden jeweils die 16 Byte des angesprochenen Codierdatenblockes ausgegeben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DWord) Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3:               Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TELEGRAMM | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier 3 |
| F_UW1_NR | int | Index der Umweltbedingung 1 |
| F_UW1_TEXT | string | Spannung KL30 |
| F_UW1_WERT | real | Wert der Spannung an KL30 |
| F_UW1_EINH | string | Einheit Grad C |
| F_UW2_NR | int | Index der Umweltbedingung 2 |
| F_UW2_TEXT | string | Sollfoerdermenge |
| F_UW2_WERT | int | Wert der Sollfoerdermenge |
| F_UW2_EINH | string | Einheit l/h |
| F_UW3_NR | int | Index der Umweltbedingung 3 |
| F_UW3_TEXT | string | Kilometerstand |
| F_UW3_WERT | long | Wert des Kilometerstandes |
| F_UW3_EINH | string | Einheit km |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-is-lesen"></a>
### IS_LESEN

is_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier 3 |
| F_UW1_NR | int | Index der Umweltbedingung 1 |
| F_UW1_TEXT | string | Spannung KL30 |
| F_UW1_WERT | real | Wert der Spannung an KL30 |
| F_UW1_EINH | string | Einheit Grad C |
| F_UW2_NR | int | Index der Umweltbedingung 2 |
| F_UW2_TEXT | string | Sollfoerdermenge |
| F_UW2_WERT | int | Wert der Sollfoerdermenge |
| F_UW2_EINH | string | Einheit l/h |
| F_UW3_NR | int | Index der Umweltbedingung 3 |
| F_UW3_TEXT | string | Kilometerstand |
| F_UW3_WERT | long | Wert des Kilometerstandes |
| F_UW3_EINH | string | Einheit km |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-adu-werte-lesen"></a>
### ADU_WERTE_LESEN

es werden die Messwerte des AD-Umsetzers ausgelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_HIGHSIDE_WERT | real |  |
| SENSOR_HIGHSIDE_EINH | string |  |
| SENSOR_LOWSIDE_WERT | real |  |
| SENSOR_LOWSIDE_EINH | string |  |
| MOTORSPANNUNG_WERT | real |  |
| MOTORSPANNUNG_EINH | string |  |
| MOTORSTROM_WERT | real |  |
| MOTORSTROM_EINH | string |  |
| SPANNUNG_KL30_WERT | real |  |
| SPANNUNG_KL30_EINH | string |  |
| SPANNUNG_KL15_WERT | real |  |
| SPANNUNG_KL15_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-ekp-daten-lesen"></a>
### EKP_DATEN_LESEN

es werden die Messwerte des AD-Umsetzers ausgelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL_PUMPE_WERT | int |  |
| DREHZAHL_PUMPE_EINH | string |  |
| SOLL_FOERDERMENGE_WERT | int |  |
| SOLL_FOERDERMENGE_EINH | string |  |
| SOLL_DREHZAHL_WERT | int |  |
| SOLL_DREHZAHL_EINH | string |  |
| PWM_REGISTER_WERT | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (55 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (5 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

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
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 55 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
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
| 0x28 | DODUCO =&gt; BERU |
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
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC1 | MOTORSPANNUNG_ZU_HOCH    0xC1 |
| 0xC2 | MOTORSTROM_ZU_HOCH       0xC2 |
| 0xC3 | DREHZAHL_FEHLT           0xC3 |
| 0xC4 | DREHZAHL_ZU_HOCH         0xC4 |
| 0xC5 | DREHZAHL_ZU_NIEDRIG      0xC5 |
| 0xC6 | UEBERTEMP_HIGH_SIDE      0xC6 |
| 0xC7 | UEBERTEMP_LOW_SIDE       0xC7 |
| 0xC8 | CAN_ANST_TIMEOUT         0xC8 |
| 0xC9 | UC_UEBERTEMP             0xC9 |
| 0xCA | MOTORSTROM_ZU_NIEDRIG    0xCA |
| 0xCB | MOTORSTROM_FEHLT         0xCB |
| 0xCC | MOTORSPANNUNG_ZU_NIEDRIG 0xCC |
| 0xFF | unbekannter Fehlecode |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xD1 | KL15_ZU_HOCH               0xD1 |
| 0xD2 | KL30_FEHLT                 0xD2 |
| 0xD3 | KL30_ZU_HOCH               0xD3 |
| 0xD4 | DREHZAL_ZU_NIEDRIG_UNTERSP 0xD4 |
| 0xFF | unbekannter Infocode |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | ----   | ---- |
| 0x01 | Aussentemperatur | Grad C |
| 0x02 | Sollfoerdermenge | l/h |
| 0x03 | Kilometerstand | km |
| 0xXY | unbekannte Umweltbedingung | -- |
