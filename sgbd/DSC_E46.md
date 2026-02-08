# DSC_E46.prg

- Jobs: [54](#jobs)
- Tables: [10](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem u. Dynamisches Stabilitaets Controll E46 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.30 |
| AUTHOR | BMW TP-421 Hirsch, BMW TP-422 Teepe, BMW EF-73 Kusch, BMW TP-423 Pollmann |
| COMMENT | Keine Diagnose bei V &gt; 6 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer DSC3
- [IDENT](#job-ident) - Ident-Daten fuer DSC3
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer DSC3
- [FS_LESEN_KB90](#job-fs-lesen-kb90) - Fehlerspeicher lesen fuer DSC3 mit KB90
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer DSC3
- [FS_INIT](#job-fs-init) - Fehlerspeicher initialisieren NVRAM-Loeschen
- [STATUS_OFFSET_LESEN](#job-status-offset-lesen) - Status Offsetwerte DSC3
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge DSC3
- [STATUS_SENSOREN_LESEN](#job-status-sensoren-lesen) - Status SENSOREN DSC_E46, Signalgruppe 02
- [STATUS_SPANNUNGSWERTE_LESEN](#job-status-spannungswerte-lesen) - Status SPANNUNGSWERTE DSC_E46, Signalgruppe 01
- [STATUS_LWS](#job-status-lws) - Status LWS SENSOREN DSC_E46, Signalgruppe 03
- [STATUS_DME_DDE_1](#job-status-dme-dde-1) - Status DME_DDE_1 CAN-Botschaft, Signalgruppe 04
- [TRIG_SCHREIBEN](#job-trig-schreiben) - TRIGGERSCHWELLEN SCHREIBEN DSC_E46
- [STEUERN_DIGITAL](#job-steuern-digital) - Parameterliste: E oder W,EVVL,AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,Pumpe,SV1,SV2,EUV1,EUV2,V_PUMPE
- [STEUERN_ANALOG_ASC_LM](#job-steuern-analog-asc-lm) - Ansteuern MD_ASC und MD_LM
- [STEUERN_ANALOG_MSR](#job-steuern-analog-msr) - Ansteuern MD_MSR
- [DSC_SIM_VA](#job-dsc-sim-va) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_HA](#job-dsc-sim-ha) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_VA1](#job-dsc-sim-va1) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_HA1](#job-dsc-sim-ha1) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_VA2](#job-dsc-sim-va2) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_HA2](#job-dsc-sim-ha2) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_VA3](#job-dsc-sim-va3) - Steuern_Digital ansteueren u. halten
- [DSC_SIM_HA3](#job-dsc-sim-ha3) - Steuern_Digital ansteueren u. halten
- [DRUCKABBAU_VL](#job-druckabbau-vl) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_VR](#job-druckabbau-vr) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_VL](#job-druckaufbau-vl) - Steuern_Digital ansteuern u. ruecksetzen
- [DRUCKHALTEN](#job-druckhalten) - Steuern_Digital ansteueren u. ruecksetzen
- [PUMPENFOERDERLEISTUNG_VO](#job-pumpenfoerderleistung-vo) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKABBAU_HA](#job-druckabbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [DRUCKAUFBAU_HA](#job-druckaufbau-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [PUMPENFOERDERLEISTUNG_HA](#job-pumpenfoerderleistung-ha) - Steuern_Digital ansteueren u. ruecksetzen
- [ABS_REGELSIMULATION](#job-abs-regelsimulation) - Ansteuern mehrerer digitaler Ausgaenge
- [NA_ENTLUEFTUNG_LI](#job-na-entlueftung-li) - Steuern_Digital ansteueren u. ruecksetzen
- [NA_ENTLUEFTUNG_RE](#job-na-entlueftung-re) - Steuern_Digital ansteueren u. ruecksetzen
- [ENTLUEFTUNG_SERVICE](#job-entlueftung-service) - Steuern_Digital ansteueren u. ruecksetzen
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - HERSTELL_Daten fuer DSC3
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Triggerschwellen der 4 Radsensoren
- [STATUS_SENSOREN_LESEN_KOMP](#job-status-sensoren-lesen-komp) - Status SENSOREN DSC_E46, Signalgruppe 02
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [ID_SCHREIBEN](#job-id-schreiben) - Beschreiben des Pruefstempels Es muss ein Hex_String uebergeben werden: Adresse,Datenbyte: Bsp.: 0A,1B
- [LOGIN_DSC](#job-login-dsc) - Default init job
- [DRUCKSENSOR_DSC_ABGLEICHEN](#job-drucksensor-dsc-abgleichen) - Default init job
- [QUERBESCHLEUNIGUNGSSENSOR_DSC_ABGLEICHEN](#job-querbeschleunigungssensor-dsc-abgleichen) - Default init job
- [LENKWINKELSENSOR_ID_DSC_SCHREIBEN](#job-lenkwinkelsensor-id-dsc-schreiben) - Default init job
- [STATUS_LESEN_DDS](#job-status-lesen-dds)
- [DDS_RESET](#job-dds-reset)
- [DDS_EOL_PASSIV](#job-dds-eol-passiv)
- [COD_LESEN_CI_5](#job-cod-lesen-ci-5) - Codierdaten lesen DSC3 (120k Regler)
- [ABGLEICH_DSC_SENSOREN](#job-abgleich-dsc-sensoren) - LWS direkt ansprechen und O-Abgleich durchfuehren
- [ABGLEICH_LWS_AQ_SENSOREN](#job-abgleich-lws-aq-sensoren) - LWS direkt ansprechen und O-Abgleich durchfuehren
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

Init-Job fuer DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DSC3

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

Fehlerspeicher lesen fuer DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS_ASC_DSC = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS_ASC_DSC = 3 |
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
| PRUEFCODE | binary | alle Pruefcodes, max. 1024 Byte |

<a id="job-fs-lesen-kb90"></a>
### FS_LESEN_KB90

Fehlerspeicher lesen fuer DSC3 mit KB90

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

Fehlerspeicher loeschen fuer DSC3

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

<a id="job-status-offset-lesen"></a>
### STATUS_OFFSET_LESEN

Status Offsetwerte DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_OFFSET_LENKWINKEL_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_LENKWINKEL_EINH | string | Einheit des Offsetwerts des Lenkwinkels [Grad] |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_WERT | real | Offsetwert der Querbeschleunigung |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_EINH | string | Einheit des Offsetwerts der Querbeschleunigung [g] |
| STAT_OFFSET_DREHRATE_WERT | real | Offsetwert der Drehrate |
| STAT_OFFSET_DREHRATE_EINH | string | Einheit des Offsetwertes der Drehrate [Grad/sec] |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge DSC3

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
| STAT_BREMSFLUESSIGKEIT_EIN | int | 0 oder 1 |
| STAT_HANDBREMSSCHALTER_EIN | int | 0 oder 1 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-sensoren-lesen"></a>
### STATUS_SENSOREN_LESEN

Status SENSOREN DSC_E46, Signalgruppe 02

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_DREHRATENSENSOR_SPANNUNG_WERT | real | Spannungswert des Drehratensensor [Volt] |
| STAT_DREHRATENSENSOR_GESCHW_WERT | real | Geschwindigkeitswert des Drehratensensor [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_SPANNUNG_WERT | real | Spannungswert des Querbeschleunigungssensor [Volt] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_WERT | real | Beschleunigungswert des Querbeschleunigungssensor [g] |
| STAT_DRUCKSENSOR_DRUCKSTANGENKREIS_SPANNUNG_WERT | real | Spannungswert des Druckstangenkreissensors [Volt] |
| STAT_DRUCKSENSOR_DRUCKSTANGENKREIS_DRUCK_WERT | real | Druckwert des Druckstangenkreissensors [bar] |
| STAT_DRUCKSENSOR_SCHWIMMKREIS_SPANNUNG_WERT | real | Spannungswert des Druckstangenkreissensors [Volt] |
| STAT_DRUCKSENSOR_SCHWIMMKREIS_DRUCK_WERT | real | Druckwert des Druckstangenkreissensors [bar] |
| STAT_DREHRATENSENSOR_GESCHW_EINH | string | [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_EINH | string | [g] |
| STAT_SENSOR_DRUCK_EINH | string | bar |
| STAT_SENSOR_SPANNUNG_EINH | string | Volt |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_ASC_TASTER_EIN | int | 0 oder 1 |
| STAT_BREMSFLUESSIGKEIT_EIN | int | 0 oder 1 |
| STAT_HANDBREMSSCHALTER_EIN | int | 0 oder 1 |
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

<a id="job-status-lws"></a>
### STATUS_LWS

Status LWS SENSOREN DSC_E46, Signalgruppe 03

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_LENKWINKEL_WERT | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| STAT_LENKWINKEL_GESCHW_WERT | real | Geschwindigkeit Lenkeinschlag [Grad/sec] |
| STAT_LENKWINKEL_GESCHW_EINH | string | [Grad/sec] |
| STAT_ID_LWS | int | Identifikation LWS Sensor |
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

Parameterliste: E oder W,EVVL,AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,Pumpe,SV1,SV2,EUV1,EUV2,V_PUMPE

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

<a id="job-dsc-sim-va"></a>
### DSC_SIM_VA

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-ha"></a>
### DSC_SIM_HA

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-va1"></a>
### DSC_SIM_VA1

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-ha1"></a>
### DSC_SIM_HA1

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-va2"></a>
### DSC_SIM_VA2

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-ha2"></a>
### DSC_SIM_HA2

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-va3"></a>
### DSC_SIM_VA3

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-dsc-sim-ha3"></a>
### DSC_SIM_HA3

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

Steuern_Digital ansteuern u. ruecksetzen

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

<a id="job-entlueftung-service"></a>
### ENTLUEFTUNG_SERVICE

Steuern_Digital ansteueren u. ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

HERSTELL_Daten fuer DSC3

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
| STAT_OFFSET_DRUCKSENSOR_1_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_DRUCKSENSOR_1_EINH | string | Einheit des Offsetwerts des Drucksensors 1 [bar] |
| STAT_OFFSET_DRUCKSENSOR_2_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_DRUCKSENSOR_2_EINH | string | Einheit des Offsetwerts des Drucksensors 2 [bar] |
| _AUFTRAG | binary | anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-status-sensoren-lesen-komp"></a>
### STATUS_SENSOREN_LESEN_KOMP

Status SENSOREN DSC_E46, Signalgruppe 02

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_DREHRATENSENSOR_GESCHW_WERT | real | Geschwindigkeitswert des Drehratensensor [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_WERT | real | Beschleunigungswert des Querbeschleunigungssensor Messwert[g] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_KOMP | real | Beschleunigungswert des Querbeschleunigungssensor mit dem Offset kompensiert[g] |
| STAT_DRUCKSENSOR_DRUCKSTANGENKREIS_DRUCK_WERT | real | Druckwert des Druckstangenkreises Messwert[bar] |
| STAT_DRUCKSENSOR_DRUCKSTANGENKREIS_DRUCK_KOMP | real | Druckwert des Druckstangenkreises mit dem Offset kompensiert [bar] |
| STAT_DRUCKSENSOR_SCHWIMMKREIS_DRUCK_WERT | real | Druckwert des Schwimmkreissensors [bar] |
| STAT_DRUCKSENSOR_SCHWIMMKREIS_DRUCK_KOMP | real | Druckwert des Schwimmkreissensors mit dem Offset kompensiert [bar] |
| STAT_DREHRATENSENSOR_GESCHW_EINH | string | [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_EINH | string | [g] |
| STAT_SENSOR_DRUCK_EINH | string | bar |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

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
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |
| _TEL_ANTWORT | binary |  |
| _AUFTRAG1 | binary | Anforderungstelegramm |

<a id="job-id-schreiben"></a>
### ID_SCHREIBEN

Beschreiben des Pruefstempels Es muss ein Hex_String uebergeben werden: Adresse,Datenbyte: Bsp.: 0A,1B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_DATEN | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |
| _TEL_ANTWORT | binary |  |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |

<a id="job-login-dsc"></a>
### LOGIN_DSC

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder NACK |

<a id="job-drucksensor-dsc-abgleichen"></a>
### DRUCKSENSOR_DSC_ABGLEICHEN

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder NACK |

<a id="job-querbeschleunigungssensor-dsc-abgleichen"></a>
### QUERBESCHLEUNIGUNGSSENSOR_DSC_ABGLEICHEN

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder NACK |

<a id="job-lenkwinkelsensor-id-dsc-schreiben"></a>
### LENKWINKELSENSOR_ID_DSC_SCHREIBEN

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder NACK |
| _TEL_ANTWORT | binary |  |
| _TEL_ANTWORT_1 | binary |  |

<a id="job-status-lesen-dds"></a>
### STATUS_LESEN_DDS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STATUS_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| DRUCKSCHWELLE_GROB_15_75_KMH | int |  |
| DRUCKSCHWELLE_GROB_75_120_KMH | int |  |
| DRUCKSCHWELLE_GROB_120_165_KMH | int |  |
| DRUCKSCHWELLE_GROB_165_210_KMH | int |  |
| DRUCKSCHWELLE_GROB_210_245_KMH | int |  |
| DRUCKSCHWELLE_GROB_245_280_KMH | int |  |
| DRUCKSCHWELLE_FEIN_15_75_KMH | int |  |
| DRUCKSCHWELLE_FEIN_75_120_KMH | int |  |
| DRUCKSCHWELLE_FEIN_120_165_KMH | int |  |
| DRUCKSCHWELLE_FEIN_165_210_KMH | int |  |
| DRUCKSCHWELLE_FEIN_210_245_KMH | int |  |
| DRUCKSCHWELLE_FEIN_245_280_KMH | int |  |
| MOMENTENKOMPENSATION_1 | int |  |
| MOMENTENKOMPENSATION_2 | int |  |
| MOMENTENKOMPENSATION_3 | int |  |
| MOMENTENKOMPENSATION_4 | int |  |
| MOMENTENKOMPENSATION_5 | int |  |
| MOMENTENKOMPENSATION_6 | int |  |
| KURVENKOMPENSATION_LINKS_15_75_KMH | int |  |
| KURVENKOMPENSATION_LINKS_50_PROZ_15_75_KMH | int |  |
| KURVENKOMPENSATION_RECHTS_15_75_KMH | int |  |
| KURVENKOMPENSATION_RECHTS_50_PROZ_15_75_KMH | int |  |
| KURVENKOMPENSATION_LINKS_75_120_KMH | int |  |
| KURVENKOMPENSATION_LINKS_50_PROZ_75_120_KMH | int |  |
| KURVENKOMPENSATION_RECHTS_75_120_KMH | int |  |
| KURVENKOMPENSATION_RECHTS_50_PROZ_75_120_KMH | int |  |
| WARNUNG_AKTUELL | int |  |
| LERNZAEHLERSTAND | int |  |
| _AUFTRAG | binary | Anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-dds-reset"></a>
### DDS_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _AUFTRAG | binary | Anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-dds-eol-passiv"></a>
### DDS_EOL_PASSIV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _AUFTRAG | binary | Anforderungstelegramm |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-cod-lesen-ci-5"></a>
### COD_LESEN_CI_5

Codierdaten lesen DSC3 (120k Regler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_DAT_00 | string | Codierbyte 00 |
| COD_DAT_01_CS | string | Codierbyte 01 = Checksumme |
| COD_DAT_02 | string | Codierbyte 02 |
| COD_DAT_03 | string | Codierbyte 03 |
| COD_DAT_04_BUS | string | Codierbyte 04 = Busindex |
| COD_DAT_05 | string | Codierbyte 05 |
| COD_DAT_06 | string | Codierbyte 06 |
| COD_DAT_07 | string | Codierbyte 07 |
| COD_DAT_08 | string | Codierbyte 08 |
| COD_DAT_09 | string | Codierbyte 09 |
| COD_DAT_10 | string | Codierbyte 10 |
| COD_DAT_11 | string | Codierbyte 11 |
| COD_TYP_EINSPUR_PARAM | string | Einspurmodellparameter |
| COD_TYP_DRUCK_PARAM | string | Druckmodellparameter |
| COD_TYP_PRE_VLABS | string | verbesserte Lenkfaehigkeit ABS |
| COD_TYP_EBV_LAMPE | string | Warnlampe elektronische Bremskraftverteilung |
| COD_TYP_BREMSLICHTSCHALTER | string | aktiver/passiver Bremslichtschalter |
| COD_TYP_MOTOR_ART | string | Benzin/Diesel-Motor |
| COD_TYP_REIFENTOL_ABGLEICH_ASC | string | Reifentoleranzabgleich waehrend ASC-Regelung |
| COD_TYP_REIFENTOL_ABGLEICH | string | Reifentoleranzabgleich |
| COD_TYP_LOGIK_HA_SPERRE | string | Logik HA-Sperrdifferential aktiv/passiv |
| COD_TYP_GETRIEBE | string | Automatik/Schaltgetriebe |
| COD_TYP_DRUCKMOD_HA | string | Druckmodell Hinterachse |
| COD_TYP_DRUCKMOD_VA | string | Druckmodell Vorderachse |
| COD_TYP_DV_OFFSET | string | Schlupfschwellenoffset |
| COD_TYP_UEBERSTEUERN_MUE_0 | string | Uebersteuern Mue 0 |
| COD_TYP_UEBERSTEUERN_MUE_1 | string | Uebersteuern Mue 1 |
| COD_TYP_UNTERSTEUERN_MUE_0 | string | Untersteuern Mue 0 |
| COD_TYP_UNTERSTEUERN_MUE_1 | string | Untersteuern Mue 1 |
| COD_TYP_GRADIENT_MM_ZUGABE | string | Gradient Momentenzugabe |
| COD_TYP_DELTA_PSI_BETA_LIMIT_KORR | string | Delta Psi Beta Limit Korrektur |
| COD_TYP_UNTERSTEUERSCHWELLE | string | Untersteuerschwelle |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-abgleich-dsc-sensoren"></a>
### ABGLEICH_DSC_SENSOREN

LWS direkt ansprechen und O-Abgleich durchfuehren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FEHLER_URSACHE | string | OKAY, FEHLER |

<a id="job-abgleich-lws-aq-sensoren"></a>
### ABGLEICH_LWS_AQ_SENSOREN

LWS direkt ansprechen und O-Abgleich durchfuehren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FEHLER_URSACHE | string | OKAY, FEHLER |

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
- [FORTTEXTE](#table-forttexte) (65 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (62 × 6)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 3)
- [STEUERN](#table-steuern) (18 × 3)
- [SPANNUNGSWERTE](#table-spannungswerte) (16 × 4)
- [RAEDER](#table-raeder) (4 × 2)
- [FEHLERURSACHE](#table-fehlerursache) (5 × 2)
- [TRIGGERSCHWELLE](#table-triggerschwelle) (16 × 3)
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

Dimensions: 65 rows × 2 columns

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
| 0x62 | ASC Sonderventil 2 |
| 0x63 | EU Ventil 1 |
| 0x64 | EU Ventil 2 |
| 0x67 | Bremslichtschalter |
| 0x71 | Pumpenmotor, Ventilblock, Kabelbaum |
| 0x73 | Steuergeraete Fehler |
| 0x76 | Steuergeraete Fehler, Einstreuung Drehzahlfuehler |
| 0x78 | Bordnetzspannung &gt; 18 Volt |
| 0x81 | Hauptrelais im Steuergeraet |
| 0x82 | REF-Spannungsfehler |
| 0x83 | Ventilleckstrom |
| 0x85 | Ventilspule, Ueberspannung |
| 0x86 | CAN INSTR2 Botschaft nicht empfangen |
| 0x87 | DSC Taster laenger als 120sec gedrueckt oder Fehler |
| 0x88 | CAN DME4 Botschaft nicht empfangen |
| 0x91 | Interner Fehler CAN-Controller |
| 0x92 | CAN Bus Fehler |
| 0x93 | CAN DME/DDE Botschaft unplausibel |
| 0x94 | CAN DME/DDE, Motormoment nicht einstellbar |
| 0x95 | CAN Timeout DME/DDE |
| 0x96 | CAN Timeout EGS |
| 0x97 | Codierfehler |
| 0x98 | ASC Taster |
| 0xA1 | Gierraten Sensor elektrisch defekt |
| 0xA2 | Gierraten Sensor unplausibel |
| 0xA3 | Querbeschleunigung Sensor elektrisch defekt |
| 0xA4 | Querbeschleunigung Sensor unplausibel |
| 0xA5 | Druck Sensor 1 elektrisch defekt |
| 0xA6 | Druck Sensor 2 elektrisch defekt |
| 0xA7 | Druck Sensor unplausibel |
| 0xA8 | Spannungsversorgung Sensor |
| 0xB1 | Vorladepumpe elektrisch defekt |
| 0xB2 | Vorladepumpe mechanisch defekt |
| 0xB3 | Bremsfluessigkeit Niveau Sensor |
| 0xB4 | Lenkwinkel Sensor Signal unplausibel,offset |
| 0xB5 | Lenkwinkel Sensor Identifikation |
| 0xB6 | Lenkwinkel Sensor CAN Bus Fehler |
| 0xB7 | Lenkwinkel Sensor Intern |
| 0xB8 | Lenkwinkel Sensor keine Winkelposition |
| 0xXY | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 62 rows × 6 columns

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
| 0x62 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x63 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0x64 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
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
| 0xA1 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA2 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA3 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA4 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA5 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA6 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA7 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xA8 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB1 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB2 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB3 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB4 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB5 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB6 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB7 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
| 0xB8 | 0x03 | 0x00 | 10 | 0x01 | 0x02 |
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

Dimensions: 18 rows × 3 columns

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
| XYZ | 1 | 0x00 |
| SV1 | 2 | 0x01 |
| SV2 | 2 | 0x02 |
| EUV1 | 2 | 0x04 |
| EUV2 | 2 | 0x08 |
| V_Pumpe | 2 | 0x80 |
| XYZ | 2 | 0x00 |

<a id="table-spannungswerte"></a>
### SPANNUNGSWERTE

Dimensions: 16 rows × 4 columns

| HEX | U_IGN | U_REF | U_PUM |
| --- | --- | --- | --- |
| 0x00 | 0-0.8 | 0-0.8 | 0-1.1 |
| 0x01 | 0.5-1.4 | 0.5-1.4 | 0.7-2.1 |
| 0x02 | 1.1-2.1 | 1.1-2.1 | 1.6-3.0 |
| 0x03 | 1.8-2.7 | 1.8-2.7 | 2.6-3.9 |
| 0x04 | 2.4-3.4 | 2.4-3.4 | 3.5-4.8 |
| 0x05 | 3.1-4.0 | 3.1-4.0 | 4.4-5.8 |
| 0x06 | 3.7-4.6 | 3.7-4.6 | 5.3-6.7 |
| 0x07 | 4.3-5.3 | 4.3-5.3 | 6.3-7.6 |
| 0x08 | 5.0-5.9 | 5.0-5.9 | 7.2-8.5 |
| 0x09 | 5.6-6.6 | 5.6-6.6 | 8.1-9.5 |
| 0x0A | 6.3-7.2 | 6.3-7.2 | 9.0-10.4 |
| 0x0B | 6.9-7.8 | 6.9-7.8 | 10.0-11.3 |
| 0x0C | 7.5-8.5 | 7.5-8.5 | 10.9-12.2 |
| 0x0D | 8.2-9.1 | 8.2-9.1 | 11.8-13.2 |
| 0x0E | 8.8-9.8 | 8.8-9.8 | 12.7-14.7 |
| 0x0F | 9.5-10.3 | 9.5-10.3 | 13.7-14.8 |

<a id="table-raeder"></a>
### RAEDER

Dimensions: 4 rows × 2 columns

| RAD_NAME | ADRESSE |
| --- | --- |
| VL | 0x81 |
| VR | 0x82 |
| HL | 0x83 |
| HR | 0x84 |

<a id="table-fehlerursache"></a>
### FEHLERURSACHE

Dimensions: 5 rows × 2 columns

| FEHLER | URSACHE |
| --- | --- |
| Fehler_1 | Lenkwinkel_ECU meldet sich nicht |
| Fehler_2 | 0-Abgleich Lenkwinkel nicht o.k. |
| Fehler_3 | DSC3_ECU meldet sich nicht |
| Fehler_4 | 0-Abgleich Druck Sensor oder Querbeschleunigung Sensor nicht o.k. |
| Fehler_5 | Abgleich Lenkwinkel_ECU / DSC3_ECU nicht o.k. |

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
