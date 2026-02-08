# BC_IV.prg

- Jobs: [9](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Bordcomputer BC4 E32 / E34 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.04 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [STATUS_LESEN](#job-status-lesen) - Auslesen der I-O-Ports
- [RAM_LESEN](#job-ram-lesen) - Lesen des RAM-Speichers
- [EPROM_LESEN](#job-eprom-lesen) - Lesen des EPROM-Speichers

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

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

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_VERSION_NR | int | Generationsnummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten hier 2 |
| F_ART1_NR | int | Nr der Fehlerart 1 |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Nr der Fehlerart 2 |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen hier 0 |
| F_HFK | int | Haeufigkeit des Einzelfehlers (1 oder 2) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Auslesen der I-O-Ports

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY oder Error-Nack |
| STAT_E_JET_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_RADSENSOR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_LCD_BELEUCHTUNG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_LUEFTUNG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_VERSORGUNG_TYPSTECKER_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_KOMBISCHNITTSTELLE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_DIAGNOSE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DAC_LEITUNG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_GONG_T1_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_GONG_T2_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_HORN_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_CODE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_ZEIT2_LED_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_CODE_LED_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_LIMIT_LED_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_ZEIT1_LED_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_HEIZUNG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_IO_DATA_TYPSTECKER_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SPALTE_1_TASTATUR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SPALTE_2_TASTATUR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SPALTE_3_TASTATUR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SPALTE_4_TASTATUR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_CLOCK_LTG_TYPSTECKER_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_LATCH_ENABLE_LCD_TREIBER_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_EMPFANGSLTG_KOMBI_DIAG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SENDELTG_KOMBI_DIAG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_SERIAL_IN_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_SERIAL_OUT_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_CLOCK_SERIAL_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_LTG_BRUCH_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_STROBE_A_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_STROBE_B_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_TEMPSENSOR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_KLEMME_R_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_KLEMME_15_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_TANK_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_ETVG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_KLEMME_58g_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_AD_PHOTOTRANSISTOR_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_INV_TASTE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_CODE_TASTE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_GESCHW_TASTE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_DISTANZ_TASTE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_HAUBE_RADIO_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_KLEMME_50_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_KLEMME_15_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_KLEMME_R_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_LSS_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_RES_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_RD_LTG_AKTIV | int | Liefert: 0 oder 1 |
| STAT_E_CC_TASTE_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_DAC_AKTIV | int | Liefert: 0 oder 1 |
| STAT_A_TD_AKTIV | int | Liefert: 0 oder 1 |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Lesen des RAM-Speichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| RAM_DATA | binary | Liefert: 256Bytes RAM |

<a id="job-eprom-lesen"></a>
### EPROM_LESEN

Lesen des EPROM-Speichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| EPROM_DATA | binary | Liefert: 512 Bytes EPROM |
| EPROM_DATA1 | binary | Liefert: 256 Bytes EPROM |
| EPROM_DATA2 | binary | Liefert: 256 Bytes EPROM |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (13 × 3)
- [FARTTEXTE](#table-farttexte) (7 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x01 | 0x15 | Luefterausgang |
| 0x02 | 0x14 | Zusatzheizung |
| 0x03 | 0x17 | Alarmhorn |
| 0x04 | 0x18 | Wegfahrsicherung |
| 0x05 | 0x12 | Warngong-Temperatur |
| 0x06 | 0x13 | Warngong-Zeit |
| 0x07 | 0x05 | Temperaturfuehler |
| 0x08 | 0x0f | Datenleitung |
| 0x09 | 0x08 | Klemme R |
| 0x0A | 0x06 | Klemme 15 |
| 0x0B | 0x0B | Tacho A Signal |
| 0x0C | 0x0c | Tauchrohrgeber |
| 0xFF | 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Kurzschluss gegen Masse |
| 0x04 | Fehler momentan nicht vorhanden |
| 0x05 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |
