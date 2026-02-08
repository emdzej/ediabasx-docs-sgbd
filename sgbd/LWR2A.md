# LWR2A.prg

- Jobs: [16](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | automatische Leuchtweitenregulierung E38 |
| ORIGIN | BMW TI-431 Nau |
| REVISION | 2.18 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-430 Drexel, BMW TI-431 Schaller, BMW TI-431 Kuessel |
| COMMENT | N/A |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [IS_LESEN](#job-is-lesen) - Default IS_LESEN job
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Default CODIERDATEN_LESEN job
- [SPEICHER_LESEN](#job-speicher-lesen) - Default SPEICHER_LESEN job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [STATUS_SENSOR_LESEN](#job-status-sensor-lesen) - STATUS_SENSOR_LESEN job
- [STEUERN_ANTRIEBE](#job-steuern-antriebe) - STEUERN_ANTRIEBE job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default hersteller_lesen job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Default pruefstempel_setzen job
- [DREHSINN_SENSOREN_LESEN](#job-drehsinn-sensoren-lesen) - DIAGNOSE_ENDE job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - DIAGNOSE_ENDE job

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_UW1_NR | int | Nummer der Umwltbedingung, hier immer 1 |
| F_UW1_EINH | string | Aussentemperatur in Grad C |
| F_UW1_WERT | int | Wert der Umweltbedingung |
| F_UW1_TEXT | string | "Aussentemperatur" |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | Bit 0 aus Infospeicher |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string | Bit 1 aus Infospeicher |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string | Bit 2 aus Infospeicher |
| F_ART4_NR | int |  |
| F_ART4_TEXT | string | Bit 3 aus Infospeicher |
| F_ART5_NR | int |  |
| F_ART5_TEXT | string | Bit 4 aus Infospeicher |
| F_ART6_NR | int |  |
| F_ART6_TEXT | string | Bit 5 aus Infospeicher |
| F_ART7_NR | int |  |
| F_ART7_TEXT | string | Bit 6 aus Infospeicher |
| F_ART8_NR | int |  |
| F_ART8_TEXT | string | Fehler momentan vorhanden J/N |
| F_HFK | int |  |
| F_HEX_CODE | binary | Hex-Daten des Fehlers |
| _INFOSPEICHER | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Default IS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _ANTWORT | binary | Inhalt Antworttelegramm |
| INFOSPEICHER | binary | Inhalt Infospeicher |
| FEHLER_KLEMME30_AKTIV | int | Byte1, Bit0 |
| FEHLER_IRQ_AKTIV | int | Byte1, Bit1 |
| FEHLER_RESET_AKTIV | int | Byte1, Bit2 |
| FEHLER_SENSORVERSORGUNG_AKTIV | int | Byte1, Bit3 |
| FEHLER_DREHZAHLFUEHLER_VORN_RECHTS_SPRUNG_AKTIV | int | Byte1, Bit4 |
| FEHLER_DREHZAHLFUEHLER_VORN_RECHTS_UEBERLAUF_AKTIV | int | Byte1, Bit5 |
| DIAGNOSE_ODER_TELEGRAMMFEHLER_AKTIV | int | Byte1, Bit6 |
| FEHLER_SENSORVERSORGUNG_ZU_GROSS_AKTIV | int | Byte2, Bit0 |
| FEHLER_SENSORSIGNAL_VORNE_ZU_KLEIN_AKTIV | int | Byte2, Bit1 |
| FEHLER_SENSORSIGNAL_ZU_GROSS_AKTIV | int | Byte2, Bit2 |
| FEHLER_SENSORSIGNAL_HINTEN_ZU_KLEIN_AKTIV | int | Byte2, Bit4 |
| FEHLER_SENSORSIGNAL_HINTEN_ZU_GROSS_AKTIV | int | Byte2, Bit5 |
| FEHLER_MOTOR_RECHTS_KURZSCHLUSS_WICKLUNG_1_AKTIV | int | Byte3, Bit0 |
| FEHLER_MOTOR_RECHTS_KURZSCHLUSS_WICKLUNG_2_AKTIV | int | Byte3, Bit1 |
| FEHLER_MOTOR_RECHTS_OPEN_LOAD_WICKLUNG_1_AKTIV | int | Byte3, Bit2 |
| FEHLER_MOTOR_RECHTS_OPEN_LOAD_WICKLUNG_2_AKTIV | int | Byte3, Bit3 |
| FEHLER_MOTOR_RECHTS_TEMPERATUR_PREALARM_AKTIV | int | Byte3, Bit4 |
| FEHLER_MOTOR_LINKS_KURZSCHLUSS_WICKLUNG_1_AKTIV | int | Byte4, Bit0 |
| FEHLER_MOTOR_LINKS_KURZSCHLUSS_WICKLUNG_2_AKTIV | int | Byte4, Bit1 |
| FEHLER_MOTOR_LINKS_OPEN_LOAD_WICKLUNG_1_AKTIV | int | Byte4, Bit2 |
| FEHLER_MOTOR_LINKS_OPEN_LOAD_WICKLUNG_2_AKTIV | int | Byte4, Bit3 |
| FEHLER_MOTOR_LINKS_TEMPERATUR_PREALARM_AKTIV | int | Byte4, Bit4 |
| ZAEHLER_SG_FEHLER | int | Byte5, Bit0 und 1 |
| ZAEHLER_MOTOR_RECHTS_FEHLER | int | Byte5, Bit2 und 3 |
| ZAEHLER_MOTOR_LINKS_FEHLER | int | Byte5, Bit4 und 5 |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Default CODIERDATEN_LESEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | auszulesender Codierdatenblock |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATENFELD | binary | Inhalt Codierdatenblock |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Default SPEICHER_LESEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speicher-Segment (0 bis ??) |
| HIGH | int | high-Adresse (0 bis ff) |
| MIDDLE | int | middle-Adresse (0 bis ff) |
| LOW | int | low-Adresse (0 bis ff) |
| BYTES | int | Anzahl Bytes (maximal 31) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATENFELD | binary | Inhalt Speicherblock |

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_REGELUNG_SCHNELL_AKTIV | int | Wert Statusbyte 1, Bit 0, schnelle Regelung |
| STAT_VERSORGUNGSSPANNUNG_ZU_KLEIN_AKTIV | int | Wert Statusbyte 1, Bit 1, Versorgungsspannung &lt;11,3V |
| STAT_IRQ_FEHLER_AKTIV | int | Wert Statusbyte 1, Bit 2, Interrupt |
| STAT_RESET_AKTIV | int | Wert Statusbyte 1, Bit 3, SG Reset |
| STAT_SENSORVERSORGUNG_AKTIV | int | Wert Statusbyte 1, Bit 4, Sensorversorung |
| STAT_TACHO_A_SIGNAL_SPRINGT_AKTIV | int | Wert Statusbyte 1, Bit 5 |
| STAT_TACHO_A_SIGNAL_UEBERLAUF_AKTIV | int | Wert Statusbyte 1, Bit 6 |
| STAT_DIAGNOSEFEHLER_AKTIV | int | Wert Statusbyte 1, Bit 7 |
| STAT_FAHRLICHT_EIN | int | Wert Statusbyte 2, Bit 1 |
| STAT_FERNLICHT_EIN | int | Wert Statusbyte 2, Bit 2 |
| STAT_REGELUNGSSTOP_MOTORFEHLER_AKTIV | int | Wert Statusbyte 2, Bit 4 |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-status-sensor-lesen"></a>
### STATUS_SENSOR_LESEN

STATUS_SENSOR_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SENSOR_VORN_WERT | int | Status Sensor vorn |
| STAT_SENSOR_VORN_EINH | string | [Volt] |
| STAT_SENSOR_HINTEN_WERT | int | Status Sensor hinten |
| STAT_SENSOR_HINTEN_EINH | string | [Volt] |

<a id="job-steuern-antriebe"></a>
### STEUERN_ANTRIEBE

STEUERN_ANTRIEBE job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZIELWERT1 | int | anzusteuernder ZIELWERT 1 (Bereich 0 bis 1024) |
| ZIELWERT2 | int | anzusteuernder Zielwert 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default hersteller_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Daten des Herstellerfeldes |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BYTE1 | int |  |
| BYTE2 | int |  |
| BYTE3 | int |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Default pruefstempel_setzen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0x00 bis 0xFF |
| BYTE2 | int | 0x00 bis 0xFF |
| BYTE3 | int | 0x00 bis 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-drehsinn-sensoren-lesen"></a>
### DREHSINN_SENSOREN_LESEN

DIAGNOSE_ENDE job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| COD_DREHSINN_SENSOR_VORN_POSITIV | int |  |
| COD_DREHSINN_SENSOR_HINTEN_POSITIV | int |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

DIAGNOSE_ENDE job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (6 × 2)
- [FARTTEXTE](#table-farttexte) (26 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Signalfehler |
| 0x02 | Sensorfehler vorn |
| 0x03 | Sensorfehler hinten |
| 0x04 | Antrieb Scheinwerfer links |
| 0x05 | Antrieb Scheinwerfer rechts |
| 0xFF | unbekannter Fehlercode |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 26 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan vorhanden |
| 0x01 | Fehler momentan nicht vorhanden |
| 0x02 | -- |
| 0x10 | Ueberwachung Versorgung Ub &lt; 11,3 Volt |
| 0x11 | Interrupt im Steuergeraet |
| 0x12 | Reset im Steuergeraet |
| 0x13 | Sensorversorgung: PE0 &lt; 2,5 Volt im Steuergeraet |
| 0x14 | DFAVR hat zu grosse Spruenge (extern) |
| 0x15 | DFAVR Ueberlauf (extern) |
| 0x16 | Telegrammfehler (extern) |
| 0x20 | Sensorversorgung: PE0 &gt; 4,9 Volt |
| 0x21 | Sensorsignal vorne: PE1 &lt; 0,5 Volt |
| 0x22 | Sensorsignal vorne: PE1 &gt; 4,7 Volt |
| 0x30 | Sensorsignal hinten: PE3 &lt; 0,5 Volt |
| 0x31 | Sensorsignal hinten: PE3 &gt; 4,7 Volt |
| 0x40 | Kurzschluss Wicklung 1 |
| 0x41 | Kurzschluss Wicklung 2 |
| 0x42 | Open load Wicklung 1 |
| 0x43 | Open load Wicklung 2 |
| 0x44 | Temperatur prealarm |
| 0x50 | Kurzschluss Wicklung 1 |
| 0x51 | Kurzschluss Wicklung 2 |
| 0x52 | Open load Wicklung 1 |
| 0x53 | Open load Wicklung 2 |
| 0x54 | Temperatur prealarm |
| 0xFF | unbekannte Fehlerart |

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
