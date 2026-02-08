# ASCMK4G.prg

- Jobs: [25](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem u. Autom. Stabilitaets Controll MK4 Geschlossen E36 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.20 |
| AUTHOR | BMW TP-421 Hirsch, EF-73 Kusch |
| COMMENT | Keine Diagnose bei V &gt; 6 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ASCMK4G
- [IDENT](#job-ident) - Ident-Daten fuer ASC_MK4G
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ASC_MK4G
- [FS_LESEN_KB90](#job-fs-lesen-kb90) - Fehlerspeicher lesen fuer ASC_MK4G mit KB90
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ASC_MK4G
- [FS_INIT](#job-fs-init) - Fehlerspeicher initialisieren NVRAM-Loeschen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ASC_MK4G
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
- [ASC_SIM_HA](#job-asc-sim-ha) - Steuern_Digital ansteueren u. halten
- [STEUERN_ANALOG_ASC](#job-steuern-analog-asc) - Ansteuern MD_ASC
- [STEUERN_ANALOG_MSR](#job-steuern-analog-msr) - Ansteuern MD_MSR
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - HERSTELL_Daten fuer ASCMK4G
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Triggerschwellen der 4 Radsensoren
- [TAKTZAEHLER_LESEN](#job-taktzaehler-lesen) - Grenz- u. Istwert
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

Init-Job fuer ASCMK4G

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ASC_MK4G

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

Fehlerspeicher lesen fuer ASC_MK4G

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

Fehlerspeicher lesen fuer ASC_MK4G mit KB90

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

Fehlerspeicher loeschen fuer ASC_MK4G

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

Status Eingaenge ASC_MK4G

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
| STAT_ASC_TASTER_EIN | int | 0 oder 1 |
| STAT_EGS_SCHALTER_EIN | int | 0 oder 1 |
| STAT_MOMENTENEINGRIFF_EIN | int | 0 oder 1 |
| STAT_AD_WANDLER1_WERT | int | ohne Inhalt? |
| STAT_AD_WANDLER1_EINH | string | Volt |
| STAT_IGN_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| STAT_IGN_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_PUMPEN_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| STAT_PUMPEN_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_REFERENZ_SPANNUNG_EINH | string | Einheit = Volt |
| STAT_REFERENZ_SPANNUNG_WERT | int | 0.0 bis 5.00 Volt |
| STAT_MOTORDREHZAHL_WERT | int | Momentane Motordrehzahl in 1/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| STAT_CAN_STAND | string | DME oder DDE |
| STAT_MOTORMOMENT_WERT | long | Ind. Motormoment % |
| STAT_MOTORMOMENT_EINH | string | Einheit = % |
| STAT_FAHRERWUNSCH_WERT | long | Ind. Fahrerwunsch % |
| STAT_FAHRERWUNSCH_EINH | string | Einheit = % |
| STAT_REIBMOMENT_WERT | long | Ind. Motormoment % |
| STAT_REIBMOMENT_EINH | string | Einheit = % |
| STAT_NORMIERUNGSMOMENT_WERT | long | Ind. Motormoment % |
| STAT_NORMIERUNGSMOMENT_EINH | string | Einheit = % |
| STAT_CAN_INFO_1 | string | EGS |
| STAT_CAN_INFO_2 | string | DME oder DDE |
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

<a id="job-asc-sim-ha"></a>
### ASC_SIM_HA

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-analog-asc"></a>
### STEUERN_ANALOG_ASC

Ansteuern MD_ASC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| MD_ASC | int | gewuenschter wert in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-analog-msr"></a>
### STEUERN_ANALOG_MSR

Ansteuern MD_MSR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| MD_MSR | int | gewuenschter wert in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

HERSTELL_Daten fuer ASCMK4G

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
| _AUFTRAG | binary | anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-taktzaehler-lesen"></a>
### TAKTZAEHLER_LESEN

Grenz- u. Istwert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status OKAY oder FEHLER |
| TAKTZAEHLER_GRENZ_WERT | long |  |
| TAKTZAEHLER_IST_WERT | long | Wert der Triggerschwelle Sensor vorn rechts |

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
- [FORTTEXTE](#table-forttexte) (44 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (44 × 13)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 3)
- [STEUERN](#table-steuern) (13 × 3)
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

Dimensions: 44 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | Drehzahlfuehler vorne links Triggersignal |
| 0x12 | Drehzahlfuehler vorne links Kontinuitaet |
| 0x14 | Drehzahlfuehler vorne links Anfahrerkennung |
| 0x15 | Drehzahlfuehler vorne links ABS Ventil Auslass |
| 0x21 | Drehzahlfuehler vorne rechts Triggersignal |
| 0x22 | Drehzahlfuehler vorne rechts Kontinuitaet |
| 0x24 | Drehzahlfuehler vorne rechts Anfahrerkennung |
| 0x25 | Drehzahlfuehler vorne rechts ABS Ventil Auslass |
| 0x31 | Drehzahlfuehler hinten links Triggersignal |
| 0x32 | Drehzahlfuehler hinten links Kontinuitaet |
| 0x34 | Drehzahlfuehler hinten links Anfahrerkennung |
| 0x35 | Drehzahlfuehler hinten links ABS Ventil Auslass |
| 0x41 | Drehzahlfuehler hinten rechts Triggersignal |
| 0x42 | Drehzahlfuehler hinten rechts Kontinuitaet |
| 0x44 | Drehzahlfuehler hinten rechts Anfahrerkennung |
| 0x45 | Drehzahlfuehler hinten rechts ABS Ventil Auslass |
| 0x51 | ABS Ventil Einlass vorne links |
| 0x52 | ABS Ventil Einlass vorne rechts |
| 0x53 | ABS Ventil Einlass hinten links |
| 0x54 | ABS Ventil Einlass hinten rechts |
| 0x55 | ABS Ventil Auslass vorne links |
| 0x56 | ABS Ventil Auslass vorne rechts |
| 0x57 | ABS Ventil Auslass hinten links |
| 0x58 | ABS Ventil Auslass hinten rechts |
| 0x61 | ASC Sonderventil |
| 0x67 | Bremslichtschalter |
| 0x68 | Pumpenmotor Relais, Schaltzyklen |
| 0x71 | Pumpenmotor, Ventilblock, Kabelbaum |
| 0x73 | Steuergeraete Fehler |
| 0x76 | Drehzahlfuehler, -leitungen, Steuergeraet |
| 0x78 | Bordnetzspannung &gt; 16,5 Volt |
| 0x81 | Hauptrelais im Steuergeraet |
| 0x82 | Spannungsfehler |
| 0x83 | Ventilleckstrom |
| 0x85 | Ventilspule Ueberspannung |
| 0x91 | Interner IC-Fehler |
| 0x92 | CAN Bus Fehler |
| 0x93 | CAN Funktionsausfall |
| 0x94 | CAN Motordrehzahl |
| 0x95 | CAN Timeout DME/DDE |
| 0x96 | CAN Timeout EGS |
| 0x97 | Codierfehler |
| 0x98 | ASC Taster |
| 0xXY | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 44 rows × 13 columns

| ORT | UW_ANZ | UW1_NR | UW1_A | UW2_NR | UW2_A | UW2_B | UW3_NR | UW3_A | UW3_B | UW4_NR | UW4_A | UW4_B |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x11 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x12 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x14 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x15 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x21 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x22 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x24 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x25 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x31 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x32 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x34 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x35 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x41 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x42 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x44 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x45 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x51 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x52 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x53 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x54 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x55 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x56 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x57 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x58 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x61 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x67 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x68 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x71 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x73 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x76 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x78 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x81 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x82 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x83 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x85 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x91 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x92 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x93 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x94 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x95 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x96 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x97 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
| 0x98 | 0x04 | 0x00 | 10 | 0x01 | 0x01 | 0x02 | 0x02 | 0x03 | 0x04 | 0x03 | 0x05 | 0x06 |
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

Dimensions: 13 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHL | 0 | 0x10 |
| AVHL | 0 | 0x20 |
| EVHR | 0 | 0x40 |
| AVHR | 0 | 0x80 |
| Pumpe | 1 | 0x01 |
| SV | 1 | 0x02 |
| B_ASC | 1 | 0x04 |
| B_MSR | 1 | 0x08 |
| XYZ | 2 | 0xFF |

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
