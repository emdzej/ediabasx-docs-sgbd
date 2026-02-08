# ASCMK20.prg

- Jobs: [35](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ABS/ASC, ITT_Industries, MK20E_I, E36,E46 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.16 |
| AUTHOR | BMW TP-421 Hirsch, EF-73 Kusch |
| COMMENT | Keine Diagnose bei V &gt; 6 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ASCMK20
- [IDENT](#job-ident) - Ident-Daten fuer ASC_MK20
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ASC_MK20
- [FS_LESEN_KB90](#job-fs-lesen-kb90) - Fehlerspeicher lesen fuer ASC_MK20 mit KB90
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ASC_MK20
- [FS_INIT](#job-fs-init) - Fehlerspeicher initialisieren NVRAM-Loeschen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ASC_MK20
- [STATUS_SPANNUNGSWERTE_LESEN](#job-status-spannungswerte-lesen) - Status SPANNUNGSWERTE DSC_E46, Signalgruppe 01
- [STATUS_DME_DDE_1](#job-status-dme-dde-1) - Status DME_DDE_1 CAN-Botschaft, Signalgruppe 04
- [TRIG_SCHREIBEN](#job-trig-schreiben) - TRIGGERSCHWELLEN SCHREIBEN DSC_E46
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern mehrerer digitaler Ausgaenge
- [STEUERN_ANALOG_ASC_LM](#job-steuern-analog-asc-lm) - Ansteuern MD_ASC und MD_LM
- [STEUERN_ANALOG_MSR](#job-steuern-analog-msr) - Ansteuern MD_MSR
- [PUMPENFOERDERLEISTUNG_VO](#job-pumpenfoerderleistung-vo) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_HA](#job-druckabbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_HA](#job-druckaufbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [PUMPENFOERDERLEISTUNG_HA](#job-pumpenfoerderleistung-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [ABS_REGELSIMULATION](#job-abs-regelsimulation) - Ansteuern mehrerer digitaler Ausgaenge
- [NA_ENTLUEFTUNG_LI](#job-na-entlueftung-li) - Steuern_Digital ansteueren u. ruecksetzen
- [NA_ENTLUEFTUNG_RE](#job-na-entlueftung-re) - Steuern_Digital ansteueren u. ruecksetzen
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - HERSTELL_Daten fuer ASCMK4G
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Triggerschwellen der 4 Radsensoren
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen fuer ASC_MK20
- [ASC_SIM_HA6](#job-asc-sim-ha6) - Steuern_Digital ansteueren u. halten
- [ASC_SIM_HA8](#job-asc-sim-ha8) - Steuern_Digital ansteueren u. halten
- [ASC_SIM_HA9](#job-asc-sim-ha9) - Steuern_Digital ansteueren u. halten
- [ASC_SIM_HA10](#job-asc-sim-ha10) - Steuern_Digital ansteueren u. halten
- [DRUCKABBAU_VL](#job-druckabbau-vl) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_VR](#job-druckabbau-vr) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_VL](#job-druckaufbau-vl) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKHALTEN](#job-druckhalten) - Steuern_Digital ansteueren u. ruecksetzen
- [COD_LESEN](#job-cod-lesen) - Codierdaten lesen MK20E_I
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

Init-Job fuer ASCMK20

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ASC_MK20

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

Fehlerspeicher lesen fuer ASC_MK20

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS_ASC_MK20 = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS_ASC_MK20 = 3 |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit = km/h |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Text der 2. Umweltbedingung |
| F_UW2_WERT | int | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string |  |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Text der 3. Umweltbedingung |
| F_UW3_WERT | int | Wert der 3. Umweltbedingung |
| F_UW3_EINH | string |  |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen-kb90"></a>
### FS_LESEN_KB90

Fehlerspeicher lesen fuer ASC_MK20 mit KB90

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

Fehlerspeicher loeschen fuer ASC_MK20

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

Status Eingaenge ASC_MK20

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
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-spannungswerte-lesen"></a>
### STATUS_SPANNUNGSWERTE_LESEN

Status SPANNUNGSWERTE DSC_E46, Signalgruppe 01

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_CAN_STAND_WERT | int | CAN-Stand |
| STAT_IND_NORMIERUNGSMOMENT_WERT | real | Induziertes Normierungsmoment [Nm] |
| STAT_IGN_SPANNUNG_WERT | string | IGN_Spannungswert [Volt] |
| STAT_RUECKFOERDERPUMPE_WERT | string | Spannungswert der Rueckfoerderpumpe [Volt] |
| STAT_REF_SPANNUNG_WERT | string | Referenz-Spannungswert [Volt] |
| STAT_SPANNUNG_VORLADEPUMPE_WERT | real | Spannungsversorgung der Vorladepumpe [Volt] |
| STAT_SPANNUNG_DSC_SENSOREN_WERT | real | Spannungsversorgung der DSC_3 Sensoren [Volt] |
| STAT_SPANNUNG_EINH | string | Volt |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-dme-dde-1"></a>
### STATUS_DME_DDE_1

Status DME_DDE_1 CAN-Botschaft, Signalgruppe 04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl [U/Min] |
| STAT_MOTORDREHZAHL_EINH | string | [U/Min] |
| STAT_MD_IND_NE_WERT | real | indiziertes Motormoment nach Momenteneingriff [% von MD-Norm] |
| STAT_MD_IND_NE_EINH | string | [% von MD_NORM] |
| STAT_MD_IND_WERT | real | indiziertes Motormoment [% von MD-Norm] |
| STAT_MD_IND_EINH | string | [% von MD_NORM] |
| STAT_MD_REIB_WERT | real | Reibmoment des Motors [% von MD-Norm] |
| STAT_MD_REIB_EINH | string | [% von MD_NORM] |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-trig-schreiben"></a>
### TRIG_SCHREIBEN

TRIGGERSCHWELLEN SCHREIBEN DSC_E46

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
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |
| ORT14 | string | gewuenschte Komponente 14 |
| ORT15 | string | gewuenschte Komponente 15 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-analog-asc-lm"></a>
### STEUERN_ANALOG_ASC_LM

Ansteuern MD_ASC und MD_LM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| MD_ASC | int | gewuenschter wert in % |
| MD_LM | int | gewuenschter wert in % |

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

<a id="job-na-entlueftung-li"></a>
### NA_ENTLUEFTUNG_LI

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-re"></a>
### NA_ENTLUEFTUNG_RE

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

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
| TRIGGERHYSTERESE_VL | long | Wert der Triggerschwelle Sensor vorn links |
| TRIGGERHYSTERESE_VR | long | Wert der Triggerschwelle Sensor vorn rechts |
| TRIGGERHYSTERESE_HL | long | Wert der Triggerschwelle Sensor hinten links |
| TRIGGERHYSTERESE_HR | long | Wert der Triggerschwelle Sensor hinten rechts |
| TRIGGERHYSTERESE_EINH | string | Einheit Triggerhysterese |
| _AUFTRAG | binary | anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen-sar"></a>
### FS_LESEN_SAR

Fehlerspeicher lesen fuer ASC_MK20

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text oder unbekannter Fehlerort liefert Leerstring, wenn F_ORT_NR = 0 |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-asc-sim-ha6"></a>
### ASC_SIM_HA6

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-asc-sim-ha8"></a>
### ASC_SIM_HA8

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-asc-sim-ha9"></a>
### ASC_SIM_HA9

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-asc-sim-ha10"></a>
### ASC_SIM_HA10

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

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

<a id="job-cod-lesen"></a>
### COD_LESEN

Codierdaten lesen MK20E_I

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_DAT_00 | string | Codierbyte 00 |
| COD_DAT_CS | string | Codierbyte 01 = Checksumme |
| COD_DAT_02 | string | Codierbyte 02 |
| COD_DAT_03 | string | Codierbyte 03 |
| COD_DAT_BUS | string | Codierbyte 04 = Busindex |
| COD_TYP_AMR | string | Antriebsmomentenregelung, Motorvariante |
| COD_TYP_BMR | string | Bremsmomentenregelung |
| COD_TYP_BREMSKRAFTVERTEILUNG | string | hydraulische Bremskraftverteilung |
| COD_TYP_BREMSLICHTSCHALTER | string | aktiver/passiver Bremslichtschalter |
| COD_TYP_MOTOR | string | Benzin/Diesel-Motor |
| COD_TYP_SPERRE | string | HA-Sperrdifferential |
| COD_TYP_GETRIEBE | string | Automatik/Schaltgetriebe |
| COD_TYP_RTA_ASC | string | Reifentoleranzabgleich_ASC |
| COD_TYP_RTA | string | Reifentoleranzabgleich |
| COD_TYP_CBC | string | Cornering_Brake_Control |
| COD_TYP_PRE_CBC | string | Cornering_Brake_Control |
| COD_TYP_BREMSWARNLEUCHTE | string | Ausgabe der Bremswarnleuchte |
| COD_TYP_DV_OFFSET | string | Schlupfschwellenoffset |
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
- [FORTTEXTE](#table-forttexte) (43 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (43 × 6)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 3)
- [STEUERN](#table-steuern) (14 × 3)
- [RAEDER](#table-raeder) (4 × 2)
- [TRIGGERSCHWELLE](#table-triggerschwelle) (16 × 3)
- [SPANNUNGSWERTE](#table-spannungswerte) (16 × 4)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)

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

Dimensions: 43 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | Drehzahlfuehler vorne links Triggersignal |
| 0x12 | Drehzahlfuehler vorne links Kontinuitaet |
| 0x14 | Drehzahlfuehler vorne links Anfahrerkennung |
| 0x15 | Ueberwachung ABS Auslass Ventil ueber Drehzahlfuehler vorne links |
| 0x21 | Drehzahlfuehler vorne rechts Triggersignal |
| 0x22 | Drehzahlfuehler vorne rechts Kontinuitaet |
| 0x24 | Drehzahlfuehler vorne rechts Anfahrerkennung |
| 0x25 | Ueberwachung ABS Auslass Ventil ueber Drehzahlfuehler vorne rechts |
| 0x31 | Drehzahlfuehler hinten links Triggersignal |
| 0x32 | Drehzahlfuehler hinten links Kontinuitaet |
| 0x34 | Drehzahlfuehler hinten links Anfahrerkennung |
| 0x35 | Ueberwachung ABS Auslass Ventil ueber Drehzahlfuehler hinten links |
| 0x41 | Drehzahlfuehler hinten rechts Triggersignal |
| 0x42 | Drehzahlfuehler hinten rechts Kontinuitaet |
| 0x44 | Drehzahlfuehler hinten rechts Anfahrerkennung |
| 0x45 | Ueberwachung ABS Auslass Ventil ueber Drehzahlfuehler hinten rechts |
| 0x51 | ABS Einlass Ventil vorne links |
| 0x52 | ABS Einlass Ventil vorne rechts |
| 0x53 | ABS Einlass Ventil hinten links |
| 0x54 | ABS Einlass Ventil hinten rechts |
| 0x55 | ABS Auslass Ventil vorne links |
| 0x56 | ABS Auslass Ventil vorne rechts |
| 0x57 | ABS Auslass Ventil hinten links |
| 0x58 | ABS Auslass Ventil hinten rechts |
| 0x61 | ASC Sonderventil 1 |
| 0x67 | Bremslichtschalter |
| 0x71 | Pumpenmotor, Ventilblock, Kabelbaum |
| 0x73 | Steuergeraete Fehler |
| 0x76 | Steuergeraete Fehler, Einstreuung Drehzahlfuehler |
| 0x78 | Bordnetzspannung &gt; 18 Volt |
| 0x81 | Hauptrelais im Steuergeraet |
| 0x82 | REF-Spannungsfehler |
| 0x83 | Ventilleckstrom |
| 0x85 | Ventilspule, Ueberspannung |
| 0x91 | Interner Fehler CAN-Controller |
| 0x92 | CAN Bus Fehler |
| 0x93 | CAN DME/DDE unplausible Daten |
| 0x94 | CAN DME/DDE, Motormoment nicht einstellbar |
| 0x95 | CAN Timeout DME/DDE |
| 0x96 | CAN Timeout EGS |
| 0x97 | Codierfehler |
| 0x98 | ASC Taster |
| 0xXY | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 43 rows × 6 columns

| ORT | UW_ANZ | UW1_NR | UW1_A | UW2_NR | UW3_NR |
| --- | --- | --- | --- | --- | --- |
| 0x11 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x12 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x14 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x15 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x21 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x22 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x24 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x25 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x31 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x32 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x34 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x35 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x41 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x42 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x44 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x45 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x51 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x52 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x53 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x54 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x55 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x56 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x57 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x58 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x61 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x67 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x71 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x73 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x76 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x78 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x81 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x82 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x83 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x85 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x91 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x92 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x93 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x94 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x95 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x96 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x97 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x98 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xXY | 0x03 | 0x00 | 10 | 0x01 | 0x02 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | Fahrzeuggeschwindigkeit | km/h |
| 0x01 | Regelung | - |
| 0x02 | BLS | - |
| 0xXY | unbekannte Umweltbedingung | XY |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 14 rows × 3 columns

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
| B_ASC | 1 | 0x04 |
| B_MSR | 1 | 0x08 |
| XYZ | 1 | 0xFF |
| SV1 | 2 | 0x01 |
| XYZ | 2 | 0xFF |

<a id="table-raeder"></a>
### RAEDER

Dimensions: 4 rows × 2 columns

| RAD_NAME | ADRESSE |
| --- | --- |
| VL | 0x81 |
| VR | 0x82 |
| HL | 0x83 |
| HR | 0x84 |

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
| D | 0x0D | 1450 |
| E | 0x0E | 1450 |
| F | 0x0F | 1450 |

<a id="table-spannungswerte"></a>
### SPANNUNGSWERTE

Dimensions: 16 rows × 4 columns

| HEX | U_IGN | U_REF | U_PUM |
| --- | --- | --- | --- |
| 0x00 | 0-1.5 | 0-0.8 | 0-1.2 |
| 0x01 | 0.9-2.6 | 0.5-1.4 | 0.8-2.2 |
| 0x02 | 2.1-3.8 | 1.1-2.0 | 1.8-3.3 |
| 0x03 | 3.2-5.0 | 1.7-2.7 | 2.8-4.3 |
| 0x04 | 4.4-6.1 | 2.4-3.3 | 3.8-5.3 |
| 0x05 | 5.6-7.3 | 3.0-3.9 | 4.8-6.3 |
| 0x06 | 6.8-8.5 | 3.6-4.5 | 5.8-7.3 |
| 0x07 | 7.9-9.7 | 4.2-5.2 | 6.8-8.3 |
| 0x08 | 9.1-10.8 | 4.9-5.8 | 7.8-9.3 |
| 0x09 | 10.3-12.0 | 5.5-6.4 | 8.8-10.3 |
| 0x0A | 11.4-13.2 | 6.1-7.0 | 9.8-11.3 |
| 0x0B | 12.6-14.3 | 6.7-7.7 | 10.8-12.3 |
| 0x0C | 13.8-15.5 | 7.4-8.3 | 11.8-13.3 |
| 0x0D | 15.0-16.7 | 8.0-8.9 | 12.8-14.3 |
| 0x0E | 16.1-17.9 | 8.6-9.5 | 13.8-15.3 |
| 0x0F | 17.3-18.8 | 9.2-10.0 | 14.8-16.1 |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

| LIEF_NR | LIEF_NAME |
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
| 0xFF | unbekannter Hersteller |
