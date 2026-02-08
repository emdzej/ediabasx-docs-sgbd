# ABSMK4G.prg

- Jobs: [22](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem MK4 Geschlossen E36 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.18 |
| AUTHOR | BMW TP-421 Hirsch, BMW EF-73 Kusch |
| COMMENT | Keine Diagnose bei V &gt; 2.5 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ABSMK4G
- [IDENT](#job-ident) - Ident-Daten fuer ABS_MK4G
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ABS_MK4G
- [FS_LESEN_KB90](#job-fs-lesen-kb90) - Fehlerspeicher lesen fuer ABS_MK4G mit KB90
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ABS_MK4G
- [FS_INIT](#job-fs-init) - Fehlerspeicher initialisieren NVRAM-Loeschen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ABS_MK4G
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern mehrerer digitaler Ausgaenge
- [DRUCKABBAU_VL](#job-druckabbau-vl) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_VR](#job-druckabbau-vr) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_VL](#job-druckaufbau-vl) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKHALTEN](#job-druckhalten) - Steuern_Digital ansteueren u. ruecksetzen
- [PUMPENFOERDERLEISTUNG_VO](#job-pumpenfoerderleistung-vo) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_HA](#job-druckabbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_HA](#job-druckaufbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [PUMPENFOERDERLEISTUNG_HA](#job-pumpenfoerderleistung-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [ABS_REGELSIMULATION](#job-abs-regelsimulation) - Ansteuern mehrerer digitaler Ausgaenge
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - HERSTELL_Daten fuer ABSMK4G
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Triggerschwellen der 4 Radsensoren
- [TRIG_SCHREIBEN](#job-trig-schreiben) - TRIGGERSCHWELLEN SCHREIBEN ABS_MK4G
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

Init-Job fuer ABSMK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ABS_MK4G

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
| ID_DATUM_TAG | string | Herstelldatum Tag |
| ID_DATUM_MONAT | int | Herstelldatum Monat |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | BMW-Softwarenummer |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen fuer ABS_MK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS_ASC_MK4G = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS_ASC_MK4G = 4 |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit = km/h |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Text der 2. Umweltbedingung |
| F_UW2_EINH | string |  |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Text der 3. Umweltbedingung |
| F_UW3_EINH | string |  |
| F_UW4_NR | int | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | Text der 4. Umweltbedingung |
| F_UW4_EINH | string |  |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen-kb90"></a>
### FS_LESEN_KB90

Fehlerspeicher lesen fuer ABS_MK4G mit KB90

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ZAHL | int | Fehlergesamtzahl |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer ABS_MK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-init"></a>
### FS_INIT

Fehlerspeicher initialisieren NVRAM-Loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge ABS_MK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_AD_WANDLER1_WERT | int | ohne Inhalt? |
| STAT_AD_WANDLER1_EINH | string | Volt |
| STAT_IGN_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| STAT_IGN_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_PUMPEN_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| STAT_PUMPEN_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_REFERENZ_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_REFERENZ_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern mehrerer digitaler Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-druckabbau-vl"></a>
### DRUCKABBAU_VL

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-druckabbau-vr"></a>
### DRUCKABBAU_VR

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-druckaufbau-vl"></a>
### DRUCKAUFBAU_VL

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-druckhalten"></a>
### DRUCKHALTEN

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-pumpenfoerderleistung-vo"></a>
### PUMPENFOERDERLEISTUNG_VO

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-druckabbau-ha"></a>
### DRUCKABBAU_HA

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-druckaufbau-ha"></a>
### DRUCKAUFBAU_HA

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-pumpenfoerderleistung-ha"></a>
### PUMPENFOERDERLEISTUNG_HA

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-abs-regelsimulation"></a>
### ABS_REGELSIMULATION

Ansteuern mehrerer digitaler Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_WARTESCHLEIFEN | int | Anzahl Warteschleifen, wenn nicht angegeben == 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

HERSTELL_Daten fuer ABSMK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status OKAY oder FEHLER |
| SCHREIBSCHUTZ_BYTES_1_BIS_14 | int | Schreibschutzbit fuer Datenbytes |
| SERIENNUMMER | long | Laufende Tages Seriennummer |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_TAG | int | Herstelldatum Tag |
| ID_DATUM_MONAT | int | Herstelldatum Monat |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| DATENBYTES | binary | zusammengestoepselte Antwort |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Triggerschwellen der 4 Radsensoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status OKAY oder FEHLER |
| TRIGGERHYSTERESE_VL | string | Wert der Triggerschwelle Sensor vorn links |
| TRIGGERHYSTERESE_VR | string | Wert der Triggerschwelle Sensor vorn rechts |
| TRIGGERHYSTERESE_HL | string | Wert der Triggerschwelle Sensor hinten links |
| TRIGGERHYSTERESE_HR | string | Wert der Triggerschwelle Sensor hinten rechts |
| TRIGGERHYSTERESE_EINH | string | Einheit Triggerhysterese |
| _AUFTRAG | binary | anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-trig-schreiben"></a>
### TRIG_SCHREIBEN

TRIGGERSCHWELLEN SCHREIBEN ABS_MK4G

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| RAD_ADRESSE | string | Adresse des betreffenden Rades |
| TRIG_WERT | string | Wert der Triggerschwelle [mVolt] |
| TRIG_WERT_EINH | string | Einheit=mVolt |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [FORTTEXTE](#table-forttexte) (32 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (32 × 13)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 3)
- [STEUERN](#table-steuern) (8 × 3)
- [RAEDER](#table-raeder) (4 × 2)
- [TRIGGERSCHWELLE](#table-triggerschwelle) (16 × 3)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 32 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | ABS Ventil Einlass vorne links |
| 0x12 | ABS Ventil Auslass vorne links |
| 0x14 | ABS Ventil Einlass vorne rechts |
| 0x18 | ABS Ventil Auslass vorne rechts |
| 0x21 | ABS Ventil Einlass hinten |
| 0x22 | ABS Ventil Auslass hinten |
| 0x44 | Bus od. Busprozessor |
| 0x48 | Interner IC Fehler |
| 0x51 | Drehzahlfuehler vorne links Triggersignal |
| 0x52 | Drehzahlfuehler vorne rechts Triggersignal |
| 0x54 | Drehzahlfuehler hinten links Triggersignal |
| 0x58 | Drehzahlfuehler hinten rechts Triggersignal |
| 0x61 | Drehzahlfuehler vorne links Kontinuitaet |
| 0x62 | Drehzahlfuehler vorne rechts Kontinuitaet |
| 0x64 | Drehzahlfuehler hinten links Kontinuitaet |
| 0x68 | Drehzahlfuehler hinten rechts Kontinuitaet |
| 0x71 | Drehzahlfuehler vorne links Anfahrerkennung |
| 0x72 | Drehzahlfuehler vorne rechts Anfahrerkennung |
| 0x74 | Drehzahlfuehler hinten links Anfahrerkennung |
| 0x78 | Drehzahlfuehler hinten rechts Anfahrerkennung |
| 0x91 | Pumpenmotor |
| 0x94 | Bordnetzspannung &gt;16,5 Volt |
| 0xA1 | Ventil Auslass / Sensor vorne links |
| 0xA2 | Ventil Auslass / Sensor vorne rechts |
| 0xA4 | Ventil Auslass / Sensor hinten links |
| 0xA8 | Ventil Auslass / Sensor hinten rechts |
| 0xB1 | Versorgung ABS-Aggregat |
| 0xB2 | Ventilfehler Hauptrelais |
| 0xB4 | Ventilblock, Stecker abgezogen |
| 0xB8 | Hardware-gesteuertes Abschalten |
| 0xFF | NVRAM intern |
| 0xXY | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 32 rows × 13 columns

| ORT | UW_ANZ | UW1_NR | UW1_A | UW2_NR | UW2_A | UW2_B | UW3_NR | UW3_A | UW3_B | UW4_NR | UW4_A | UW4_B |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x11 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x12 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x14 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x18 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x21 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x22 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x44 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x48 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x51 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x52 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x54 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x58 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x61 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x62 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x64 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x68 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x71 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x72 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x74 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x78 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x91 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x94 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xA1 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xA2 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xA4 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xA8 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xB1 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xB2 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xB4 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xB8 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xFF | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0xXY | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 8 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | Fahrzeuggeschwindigkeit | km/h |
| 0x01 | ABS Regelung aktiv | - |
| 0x02 | ABS Regelung nicht aktiv | - |
| 0x03 | BLS betaetigt | - |
| 0x04 | BLS nicht betaetigt | - |
| 0x05 | Unterspannungserkennung | - |
| 0x06 | keine Unterspannungserkennung | - |
| 0xXY | unbekannte Umweltbedingung | XY |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 8 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHA | 0 | 0x10 |
| AVHA | 0 | 0x20 |
| Pumpe | 1 | 0x01 |
| XYZ | 2 | 0xFF |

<a id="table-raeder"></a>
### RAEDER

Dimensions: 4 rows × 2 columns

| RAD_NAME | ADRESSE |
| --- | --- |
| VL | 0x81 |
| VR | 0x82 |
| HR | 0x83 |
| HL | 0x84 |

<a id="table-triggerschwelle"></a>
### TRIGGERSCHWELLE

Dimensions: 16 rows × 3 columns

| TRIG_WERT | TRIG_HEX | USS |
| --- | --- | --- |
| 0 | 0x00 | 100 |
| 1 | 0x01 | 125 |
| 2 | 0x02 | 150 |
| 3 | 0x03 | 200 |
| 4 | 0x04 | 250 |
| 5 | 0x05 | 300 |
| 6 | 0x06 | 375 |
| 7 | 0x07 | 475 |
| 8 | 0x08 | 600 |
| 9 | 0x09 | 750 |
| A | 0x0A | 925 |
| B | 0x0B | 1175 |
| C | 0x0C | 1450 |
| D | 0x0D | 1825 |
| E | 0x0E | 2275 |
| F | 0x0F | 2850 |

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
