# PDCE38.prg

- Jobs: [12](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Parkdistanz Kontrolle E34 E36 E38 E39 |
| ORIGIN | BMW TP-421 Spoljarec |
| REVISION | 1.11 |
| AUTHOR | BMW TP-421 Spoljarec |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer PDC
- [IDENT](#job-ident) - Ident-Daten fuer PDC
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status der I/O Ports lesen
- [STEUERN_IO_STATUS](#job-steuern-io-status) - Ansteuern von den I/O Stati
- [STATUS_WEG_V_MODE_LESEN](#job-status-weg-v-mode-lesen) - Status des Steuergeraets lesen
- [STATUS_AUSSCHWINGZEIT_LESEN](#job-status-ausschwingzeit-lesen) - AUSSCHWINGZEIT lesen
- [STEUERN_WEG_V](#job-steuern-weg-v) - Ansteuern der Abstaende und der Geschwindigkeit
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job fuer PDC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer PDC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_TEXT | string | Lieferantenname |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | Index der 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | Index der 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |
| F_ART5_NR | int | Index der 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_ART6_NR | int | Index der 6. Fehlerart |
| F_ART6_TEXT | string | 6. Fehlerart als Text |
| F_ART7_NR | int | Index der 7. Fehlerart |
| F_ART7_TEXT | string | 7. Fehlerart als Text |
| F_ART8_NR | int | Index der 8. Fehlerart |
| F_ART8_TEXT | string | 8. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status der I/O Ports lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_RGANG_EIN | int | 1: Rueckwaertsgang eingelegt |
| STAT_KONTROLLSIGNAL_EIN | int | 1: Kotrollsignal ein |
| STAT_UBATT_12V | int | 1: U_Batt liegt an |
| STAT_ANHAENGER_JA | int | 1: Anhaenger vorhanden |

<a id="job-steuern-io-status"></a>
### STEUERN_IO_STATUS

Ansteuern von den I/O Stati

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Diagnosemode, Tongeber, Kontrollsignal, System steuern siehe table IO_STATUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-weg-v-mode-lesen"></a>
### STATUS_WEG_V_MODE_LESEN

Status des Steuergeraets lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_V_WERT | int | Geschwindigkeit des Fahrzeugs |
| STAT_V_EINH | string | Einheit km/h |
| STAT_WEG_HL_WERT | int | Abstand hinten links |
| STAT_WEG_HR_WERT | int | Abstand hinten rechts |
| STAT_WEG_HML_WERT | int | Abstand hinten in der Mitte links |
| STAT_WEG_HMR_WERT | int | Abstand hinten in der Mitte rechts |
| STAT_WEG_VL_WERT | int | Abstand vorne links |
| STAT_WEG_VR_WERT | int | Abstand vorne rechts |
| STAT_WEG_VML_WERT | int | Abstand vorne in der Mitte links |
| STAT_WEG_VMR_WERT | int | Abstand vorne in der Mitte rechts |
| STAT_WEG_EINH | string | Einheit cm fuer Abstaende |
| STAT_MELDUNG_DISPLAY | int | 1: Meldung auf Display |
| STAT_GONG_HINTEN | int | 1: BC-GONG hinten statt Lautsprecher |
| STAT_GONG_VORNE | int | 1: BC-GONG vorne statt Lautsprecher |
| STAT_4_WANDLER | int | 1: 4-Kanal PDC |
| STAT_PDC_TASTER_VORHANDEN | int | 1: Taster Parkhilfe vorhanden |
| STAT_ANHAENGER | int | 1: Anhaengerbetrieb |
| STAT_I_BUS_SG | int | 1: I-BUS Steuergeraet anstatt D-BUS |
| STAT_PARKHILFE_AKTIV | int | 1: Parkhilfe aktiv |

<a id="job-status-ausschwingzeit-lesen"></a>
### STATUS_AUSSCHWINGZEIT_LESEN

AUSSCHWINGZEIT lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_AUSSCHWING_T_EINH | string | Einheit Ausschwingzeit usec |
| STAT_AUSSCHWING_T_HL_WERT | int | Ausschwingzeit hinten links |
| STAT_AUSSCHWING_T_HR_WERT | int | Ausschwingzeit hinten rechts |
| STAT_AUSSCHWING_T_HML_WERT | int | Ausschwingzeit hinten mitte links |
| STAT_AUSSCHWING_T_HMR_WERT | int | Ausschwingzeit hinten mitte rechts |
| STAT_AUSSCHWING_T_VL_WERT | int | Ausschwingzeit vorne links |
| STAT_AUSSCHWING_T_VR_WERT | int | Ausschwingzeit vorne rechts |
| STAT_AUSSCHWING_T_VML_WERT | int | Ausschwingzeit vorne mitte links |
| STAT_AUSSCHWING_T_VMR_WERT | int | Ausschwingzeit vorne mitte rechts |

<a id="job-steuern-weg-v"></a>
### STEUERN_WEG_V

Ansteuern der Abstaende und der Geschwindigkeit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| V_WERT | int | Geschwindigkeit des Fahrzeugs |
| HL_WERT | int | Abstand hinten links |
| HR_WERT | int | Abstand hinten rechts |
| HML_WERT | int | Abstand hinten in der Mitte links |
| HMR_WERT | int | Abstand hinten in der Mitte rechts |
| VL_WERT | int | Abstand vorne links |
| VR_WERT | int | Abstand vorne rechts |
| VML_WERT | int | Abstand vorne in der Mitte links |
| VMR_WERT | int | Abstand vorne in der Mitte rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (5 × 2)
- [SG_STATUS](#table-sg-status) (9 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [FARTMATRIX](#table-fartmatrix) (13 × 17)
- [IO_STATUS](#table-io-status) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 5 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-sg-status"></a>
### SG_STATUS

Dimensions: 9 rows × 2 columns

| SG_ORT | SG_TEXTE |
| --- | --- |
| 0x01 | Rueckwaertsgang eingelegt |
| 0x02 | BC-Gong hinten statt Lautsprecher |
| 0x04 | BC-Gong vorne statt Lautsprecher |
| 0x08 | Nur 4 Wandler hinten |
| 0x10 | Taster Parkhilfe vorhanden |
| 0x20 | Anhaengerbetrieb |
| 0x40 | I-Bus |
| 0x80 | Parkhilfe aktiv |
| 0x00 | unbekannter Status |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Wandler vorne Mitte rechts |
| 0x02 | Wandler vorne Mitte links |
| 0x04 | Wandler vorne rechts |
| 0x05 | Weggeber |
| 0x06 | Wandler vorne links |
| 0x08 | Wandler hinten Mitte rechts |
| 0x09 | Tongeber vorne |
| 0x0A | Wandler hinten Mitte links |
| 0x0C | Wandler hinten rechts |
| 0x0D | Wandler hinten links |
| 0x13 | Taste |
| 0x15 | Tongeber hinten |
| 0x16 | Kontrollsignal |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x02 | Wandlerleitung: Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Ausschwingfehler (Wandler schwingt zu lange nach) |
| 0x05 | Schirm: Kurzschluss gegen Masse |
| 0x06 | Kurzschluss Schirm Wandlerleitung |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0x10 | Kurzschluss gegen U-Batt |
| 0x20 | Kurzschluss gegen Masse |
| 0x30 | Leitungsunterbrechung |
| 0x70 | Fehler momentan vorhanden |
| 0x80 | sporadischer Fehler |
| 0xFF | -- |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 13 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0D | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x0C | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x0A | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x08 | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x06 | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x04 | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x02 | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x01 | 0xFF | 0xFF | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x15 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x30 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x00 | 0x70 | 0x00 | 0x80 |
| 0x09 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x30 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x00 | 0x70 | 0x00 | 0x80 |
| 0x16 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x30 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x00 | 0x70 | 0x00 | 0x80 |
| 0x05 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x30 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x00 | 0x70 | 0x00 | 0x80 |
| 0x13 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x30 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x00 | 0x70 | 0x00 | 0x80 |

<a id="table-io-status"></a>
### IO_STATUS

Dimensions: 8 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| DTAUS | 0x01 |
| DTVEIN | 0x02 |
| DTHEIN | 0x04 |
| DKSAUS | 0x08 |
| DKSEIN | 0x10 |
| DEIN | 0x20 |
| SAUS | 0x40 |
| SEIN | 0x80 |

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
