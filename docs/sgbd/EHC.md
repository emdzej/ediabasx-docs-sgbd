# EHC.prg

- Jobs: [24](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | 1-Achs-Luftfederung EHC |
| ORIGIN | BMW TI-431 Helmich |
| REVISION | 1.34 |
| AUTHOR | BMW TP-422 Teepe, Helmich |
| COMMENT | am Fahrzeug getestet |
| PACKAGE | 0.11 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EHC
- [FS_QUICK](#job-fs-quick) - Fehlerspeicher lesen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten des EHC
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - digitale Statis (Statusbytes) des EHC
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - analoge Stati des EHC
- [STATUS_ONLINE_LESEN](#job-status-online-lesen) - Online-Stati des EHC
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Timer-Stati des EHC
- [FAHRZEUG_HOEHE_ABGLEICHEN](#job-fahrzeug-hoehe-abgleichen) - Timer-Stati des EHC
- [STATUS_TIMER_LESEN](#job-status-timer-lesen) - Timer-Stati des EHC
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [STATUS_VORGEBEN](#job-status-vorgeben) - Ansteuern eines digitalen Ein- Ausgaenge
- [STEUERN_STATUS_VORGEBEN_LOOP](#job-steuern-status-vorgeben-loop) - Ansteuern eines digitalen Ein- Ausgaenge
- [KOMPRESSOR_STEUERN](#job-kompressor-steuern) - Ansteuern des Kompressors
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [MODUS_VORGEBEN](#job-modus-vorgeben) - EINSCHALTUNG des TRANSPORT oder MONTAGEMODUS
- [FASTFILTER_WERTE_LESEN_SCHREIBEN](#job-fastfilter-werte-lesen-schreiben) - Beschreiben des Pruefstempels
- [TIZKL15_SCHREIBEN](#job-tizkl15-schreiben) - Timerzeit fuer Meldung nach KL 15 verändern
- [IS_LESEN](#job-is-lesen) - Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose

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

Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EHC

_No arguments._

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

<a id="job-fs-quick"></a>
### FS_QUICK

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ZAHL | int | Anzahl der aktiven Fehler |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 255 |
| F_ART_ANZ | int | immer 8 |
| F_UW_ANZ | int | immer 1 |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_NR | int | Nr. der 1. Umweltbedingung |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | Fehler sporadisch? table FArtTexte ARTTEXT |
| F_ART2_NR | int | Fehlerart |
| F_ART2_TEXT | string | momentan vorhanden? table FArtTexte ARTTEXT |
| F_ART3_NR | int | Fehlerart |
| F_ART3_TEXT | string | Messbereich table FArtTexte ARTTEXT |
| F_ART4_NR | int | Fehlerart |
| F_ART4_TEXT | string | Schluss nach UBatt? table FArtTexte ARTTEXT |
| F_ART5_NR | int | Fehlerart |
| F_ART5_TEXT | string | Schluss nach Masse? table FArtTexte ARTTEXT |
| F_ART6_NR | int | Fehlerart |
| F_ART6_TEXT | string | Fehlerspezifisch table FArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerspezifische HEX-Daten |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_BLOCK0 | binary | die Codierbytes Block 0 |
| COD_KENNFELD | int | Datensatznummer |
| COD_CODIER_INDEX | int | Codierindex laut Codierdatensatz |
| COD_EINSCHALT_HYSTERESE | int |  |
| COD_AUSSCHALT_HYSTERESE | int |  |
| COD_AUFL_HOE_HL | int |  |
| COD_AUFL_HOE_HR | int |  |
| COD_DREHSINN_SENSOR_HL | string |  |
| COD_DREHSINN_SENSOR_HR | string |  |
| COD_NIV_OFFSET | int |  |
| COD_NIV_MIN | int |  |
| COD_NIV_BAHN | int |  |
| COD_FAHRT_AUF_TIME | int |  |
| COD_EINS_REG_TIME | int |  |
| COD_STAND_AUF_TIME | int |  |
| COD_TIME_ABREGEL | int |  |
| COD_P_SIKO_EIN | int |  |
| COD_P_ELEKTR_EIN | int |  |
| COD_P_PLAUSI_EIN | int |  |
| COD_P_DUMP_EIN | int |  |
| COD_DATEN_BLOCK1 | binary | die Codierbytes Block 1 |
| COD_SLOW_FILTER_KONSTANTEN | int |  |
| COD_FAST_FILTER_KONSTANTEN | int |  |
| COD_ANZ_HEBEN | int |  |
| COD_KURVE_VF | int |  |
| COD_DIFF_KURVE_E | int |  |
| COD_DIFF_KURVE_A | int |  |
| COD_TIME_KURVE_RES | int |  |
| COD_DIFF_SCHIEF_E | int |  |
| COD_DIFF_SCHIEF_A | int |  |
| COD_TIME_SCHIEF | int |  |
| COD_MAX_AUSFEDERWEG | int |  |
| COD_MAX_EINFEDERWEG | int |  |
| COD_V_RESET | int |  |
| COD_DATEN_BLOCK2 | binary | die Codierbytes Block 2 |
| COD_TIME_BATT | int |  |
| COD_U_BATT_MIN | int |  |
| COD_U_BATT_MAX | int |  |
| COD_TIME_VA | int |  |
| COD_TIME_KO | int |  |
| COD_TIME_KO_FAKT | int |  |
| COD_TIME_KO_EIN | int |  |
| COD_TIME_ABLVENT | int |  |
| COD_TIME_CCM_RES | int |  |
| COD_DATEN_BLOCK3 | binary | die Codierbytes Block 3 |
| COD_MAX_SENS | int |  |
| COD_MIN_SENS | int |  |
| COD_VDD_MAX | int |  |
| COD_VDD_MIN | int |  |
| COD_SENS_AKT_VF | int |  |
| COD_HOEHE_STAND_MAX | int |  |
| COD_HOEHE_STAND_MIN | int |  |
| COD_HOEHE_STAND_TIME | int |  |
| COD_U_GROUND | int |  |
| COD_U_BATT_OFF | int |  |
| COD_VERZOEG_TIME | int |  |
| COD_MAX_W | int |  |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

digitale Statis (Statusbytes) des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_HAND_HEBEN_HA_EIN | int |  |
| STAT_HAND_SENKEN_HA_EIN | int |  |
| STAT_HAND_HEBEN_HL_EIN | int |  |
| STAT_HAND_HEBEN_HR_EIN | int |  |
| STAT_HAND_SENKEN_HL_EIN | int |  |
| STAT_HAND_SENKEN_HR_EIN | int |  |
| STAT_HAND_HANDSTEUERUNG_ENDE_EIN | int |  |
| STAT_REG1_ABLASS_TO_EIN | int |  |
| STAT_REG1_KOMP_TO_EIN | int |  |
| STAT_REG1_UEBERSPANNUNG_EIN | int |  |
| STAT_REG1_UNTERSPANNUNG_EIN | int |  |
| STAT_REG1_DIAGNOSE_AKTIV | int |  |
| STAT_REG1_KLEMME15_ALT_EIN | int |  |
| STAT_REG1_MISSBRAUCH_EIN | int |  |
| STAT_REG2_FEHLER_AKTIV | int |  |
| STAT_REG2_MELDUNG_AKTIV | int |  |
| STAT_REG2_LAMPE_EIN | int |  |
| STAT_REG2_AD_FEHLER_AKTIV | int |  |
| STAT_REG2_EEPROM_AKTIV | int |  |
| STAT_REG2_ERSTE_MELDUNG_AKTIV | int |  |
| STAT_REG2_KL15_MELDUNG_AKTIV | int |  |
| STAT_FAHR_KURVE_AKTIV | int |  |
| STAT_FAHR_RADWECHSEL_AKTIV | int |  |
| STAT_FAHR_HEBEBUEHNE_AKTIV | int |  |
| STAT_FAHR_SCHIEFBELADUNG_AKTIV | int |  |
| STAT_FAHR_FAHRT_AKTIV | int |  |
| STAT_FAHR_BANDENDE_AKTIV | int |  |
| STAT_FAHR_BAHNVERLADUNG_AKTIV | int |  |
| STAT_FAHR_SCHIEFSTAND_AKTIV | int |  |
| STAT_STEUER_ERSTE_MESSUNG_AKTIV | int |  |
| STAT_STEUER_FILTER_INI_AKTIV | int |  |
| STAT_STEUER_NACH_HEBEN_AKTIV | int |  |
| STAT_STEUER_F_REGEL_LOS_AKTIV | int |  |
| STAT_STEUER_SCHIEFSTAND_REGEL_AKTIV | int |  |
| STAT_STEUER_REGEL_ABBRECHEN_AKTIV | int |  |
| STAT_STEUER_ERSTE_REGELUNG_AKTIV | int |  |
| STAT_SYS_OFFSET_OK_AKTIV | int |  |
| STAT_SYS_MOTOR_EIN | int |  |
| STAT_SYS_KLAPPENAENDERUNG_AKTIV | int |  |
| STAT_SYS_KLEMME15_EIN | int |  |
| STAT_SYS_KLAPPE_OFFEN_AKTIV | int |  |
| STAT_SYS_V_ABSCHALT_AKTIV | int |  |
| STAT_SYS_REGLE_NUR_AB_AKTIV | int |  |
| STAT_TOL_HR_SENKEN_AKTIV | int |  |
| STAT_TOL_HR_HEBEN_AKTIV | int |  |
| STAT_TOL_HL_SENKEN_AKTIV | int |  |
| STAT_TOL_HL_HEBEN_AKTIV | int |  |
| STAT_PORT_A_VENTIL_HR_AKTIV | int |  |
| STAT_PORT_A_VENTIL_HL_AKTIV | int |  |
| STAT_PORT_A_KOMP_RELAIS_AKTIV | int |  |
| STAT_PORT_A_ABLASS_VENTIL_AKTIV | int |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

analoge Stati des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SENSOR_HL_WERT | real | 0 - 5.1 Volt |
| STAT_EINHEITEN | string | Volt |
| STAT_SENSOR_HR_WERT | real | 0 - 5.1 Volt |
| STAT_VERSORGUNG_SENSOR_WERT | real | 0 - 25.5 Volt |
| STAT_VERSORGUNG_KOMPRESSOR_WERT | real | 0 - 25.5 Volt |
| STAT_VERSORGUNG_VENTIL_HL_WERT | real | 0 - 25.5 Volt |
| STAT_VERSORGUNG_VENTIL_HR_WERT | real | 0 - 25.5 Volt |
| STAT_VERSORGUNG_VENTIL_ABLASS_WERT | real | 0 - 25.5 Volt |
| STAT_U_BATT_WERT | real | 0 - 25.5 Volt |
| _TEL_ANTWORT | binary |  |

<a id="job-status-online-lesen"></a>
### STATUS_ONLINE_LESEN

Online-Stati des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SENSOR_HL_ROH_WERT | real | Rohwert Sensor HL in V |
| STAT_SENSOR_HR_ROH_WERT | real | Rohwert Sensor HR in V |
| STAT_SLOW_FILTER_HL_WERT | int |  |
| STAT_SLOW_FILTER_HR_WERT | int |  |
| STAT_FAST_FILTER_HL_WERT | int |  |
| STAT_FAST_FILTER_HR_WERT | int |  |
| STAT_FAHRGESCHW_WERT | int |  |
| STAT_TOL_HR_SENKEN_AKTIV | int |  |
| STAT_TOL_HR_HEBEN_AKTIV | int |  |
| STAT_TOL_HL_SENKEN_AKTIV | int |  |
| STAT_TOL_HL_HEBEN_AKTIV | int |  |
| STAT_PORT_A_VENTIL_HR_AKTIV | int |  |
| STAT_PORT_A_VENTIL_HL_AKTIV | int |  |
| STAT_PORT_A_KOMP_RELAIS_AKTIV | int |  |
| STAT_PORT_A_ABLASS_VENTIL_AKTIV | int |  |
| STAT_FAHR_KURVE_AKTIV | int |  |
| STAT_FAHR_RADWECHSEL_AKTIV | int |  |
| STAT_FAHR_HEBEBUEHNE_AKTIV | int |  |
| STAT_FAHR_SCHIEFBELADUNG_AKTIV | int |  |
| STAT_FAHR_FAHRT_AKTIV | int |  |
| STAT_FAHR_BANDENDE_AKTIV | int |  |
| STAT_FAHR_BAHNVERLADUNG_AKTIV | int |  |
| STAT_FAHR_SCHIEFSTAND_AKTIV | int |  |
| STAT_SYS_OFFSET_OK_AKTIV | int |  |
| STAT_SYS_MOTOR_EIN | int |  |
| STAT_SYS_KLAPPENAENDERUNG_AKTIV | int |  |
| STAT_SYS_KLEMME15_EIN | int |  |
| STAT_SYS_KLAPPE_OFFEN_AKTIV | int |  |
| STAT_SYS_V_ABSCHALT_AKTIV | int |  |
| STAT_SYS_REGLE_NUR_AB_AKTIV | int |  |
| STAT_REGELMODE_VORLAUF_NACHLAUF_AKTIV | int |  |
| STAT_REGELMODE_NORMAL_AKTIV | int |  |
| STAT_REGELMODE_KLAPPE_AKTIV | int |  |
| STAT_REGELMODE_SET_OFFSET_AKTIV | int |  |
| STAT_REGELMODE_FEHLERFALL_AKTIV | int |  |
| STAT_REGELMODE_BAHNVERLADUNG_AKTIV | int |  |
| STAT_REGELMODE_DIAGNOSE_AKTIV | int |  |
| STAT_FEHLERSTATUS_0_WERT | int |  |
| STAT_FEHLERSTATUS_1_WERT | int |  |
| STAT_FEHLERSTATUS_2_WERT | int |  |
| _TEL_ANTWORT | binary |  |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Timer-Stati des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| OFFSET_HL_WERT | int |  |
| OFFSET_HR_WERT | int |  |
| OFFSET_EINH | string | mm |
| _TEL_ANTWORT | binary |  |

<a id="job-fahrzeug-hoehe-abgleichen"></a>
### FAHRZEUG_HOEHE_ABGLEICHEN

Timer-Stati des EHC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELTA_HOEHE_LINKS | int | mm |
| DELTA_HOEHE_RECHTS | int | mm |
| MINDEST_DELTA | int | mm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| OFFSET_LINKS_ALT | int | alter offset |
| OFFSET_RECHTS_ALT | int | alter offset |
| OFFSET_LINKS_NEU | int | alter offset |
| OFFSET_RECHTS_NEU | int | alter offset |
| SG_HOEHE_LINKS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| SG_HOEHE_RECHTS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| AUFLOESUNG_LINKS_WERT | real | Sensoraufloesung links laut Kodierdaten |
| AUFLOESUNG_RECHTS_WERT | real | Sensoraufloesung rechts laut Kodierdaten |
| ABWEICHUNG_LINKS_WERT | int | Abweichung links |
| ABWEICHUNG_RECHTS_WERT | int | Abweichung rechts |
| TEL_ABGLEICH | binary | gesendetes Abgleichtelegramm |

<a id="job-status-timer-lesen"></a>
### STATUS_TIMER_LESEN

Timer-Stati des EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TIMER_KOMPRESSOR_WERT | real |  |
| STAT_TIMER_KOMPRESSOR_EINH | string |  |
| STAT_TIMER_KURVE_WERT | real |  |
| STAT_TIMER_KURVE_EINH | string |  |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-vorgeben"></a>
### STATUS_VORGEBEN

Ansteuern eines digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-status-vorgeben-loop"></a>
### STEUERN_STATUS_VORGEBEN_LOOP

Ansteuern eines digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente 1 |
| TIME | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-kompressor-steuern"></a>
### KOMPRESSOR_STEUERN

Ansteuern des Kompressors

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Ansteuerzeit in 100 ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | gewuenschtes Startsegment (0 bis 3) |
| MIDDLE | int | gewuenschte Startadresse midle als Hexwert! |
| LOW | int | gewuenschte Startadresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |
| DATEN | binary | angeforderter Datenblock (32 Bytes!) |

<a id="job-modus-vorgeben"></a>
### MODUS_VORGEBEN

EINSCHALTUNG des TRANSPORT oder MONTAGEMODUS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | TRANSPORT oder MONTAGE |
| SCHALT_WERT | string | EIN oder AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_EPROM_ALT | binary | alter Inhalt der EPROM-Zellen |
| _TEL_EPROM_SCHREIBEN | binary | Sendetelegram EPROM-Zellen |
| _TEL_STATUS_VORGEBEN | binary | Sendetelegram EPROM-Zellen |
| _TEL_EPROM_NEU | binary | neuer Inhalt der EPROM-Zellen |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-fastfilter-werte-lesen-schreiben"></a>
### FASTFILTER_WERTE_LESEN_SCHREIBEN

Beschreiben des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT_1 | binary | status online lesen |
| _TEL_ANTWORT_2 | binary | Pruefstempel lesen |
| _TEL_ANTWORT_3 | binary | nach Pruefstempel schreiben |
| STAT_FAST_FILTER_HL_WERT | int | Byte 1 vom Pruefstempel |
| BYTE2 | int | Pruefbyte vom Achsmessstand, Hex55 bei i.O. |
| STAT_FAST_FILTER_HR_WERT | int | Byte 3 vom Pruefstempel |

<a id="job-tizkl15-schreiben"></a>
### TIZKL15_SCHREIBEN

Timerzeit fuer Meldung nach KL 15 verändern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | gewuenschte Timerzeit (in Sekunden) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT_1 | binary |  |
| _TEL_ANTWORT_2 | binary |  |
| _TEL_ANTWORT_3 | binary |  |
| _TEL_ANTWORT_4 | binary |  |
| _TEL_SENDE_1 | binary |  |
| _TEL_SENDE_2 | binary |  |
| _TEL_SENDE_3 | binary |  |
| _TEL_SENDE_4 | binary |  |
| W1 | int |  |
| W2 | int |  |
| W3 | int |  |
| W4 | int |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 255 |
| F_ART_ANZ | int | immer 8 |
| F_UW_ANZ | int | immer 1 |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_NR | int | Nr. der 1. Umweltbedingung |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | Fehler sporadisch? table FArtTexte ARTTEXT |
| F_ART2_NR | int | Fehlerart |
| F_ART2_TEXT | string | momentan vorhanden? table FArtTexte ARTTEXT |
| F_ART3_NR | int | Fehlerart |
| F_ART3_TEXT | string | Messbereich table FArtTexte ARTTEXT |
| F_ART4_NR | int | Fehlerart |
| F_ART4_TEXT | string | Schluss nach UBatt? table FArtTexte ARTTEXT |
| F_ART5_NR | int | Fehlerart |
| F_ART5_TEXT | string | Schluss nach Masse? table FArtTexte ARTTEXT |
| F_ART6_NR | int | Fehlerart |
| F_ART6_TEXT | string | Fehlerspezifisch table FArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerspezifische HEX-Daten |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (11 × 2)
- [FARTTEXTE](#table-farttexte) (15 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 3)
- [STEUERN](#table-steuern) (12 × 3)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Sensor hinten links |
| 0x02 | Sensor hinten rechts |
| 0x03 | Kompressor-Relais |
| 0x04 | Magnetventil hinten links |
| 0x05 | Magnetventil hinten rechts |
| 0x06 | Ablassventil |
| 0x07 | Steuergeraet, EEPROM, A-/D-Wandler |
| 0x08 | Regelzeit, heben |
| 0x09 | Regelzeit, senken |
| 0x0A | Regelzeit, einseitig |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 15 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x02 | Kurzschluss gegen Masse |
| 0x05 | Kurzschluss gegen U-Batt oder Leitungsunterbrechung |
| 0x08 | ungueltiger Messbereich |
| 0x20 | Sensoraktivitaet |
| 0x21 | VDD oder beide defekt |
| 0x40 | Fehler momentan vorhanden |
| 0x70 | EEPROM defekt |
| 0x71 | A-/D-Wandler defekt |
| 0x80 | sporadischer Fehler |
| 0x90 | Fahrt |
| 0xA0 | rechte Seite |
| 0xA1 | linke Seite |
| 0xB0 | Stand |
| 0xB1 | Fahrt |
| 0xFF | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Sensor Versorgungsspannung | mV |
| 0x03 | minimale Spannung am Relais | mV |
| 0x04 | minimale Spannung am Ventil | mV |
| 0x07 | Checksumme | - |
| 0x17 | AD Wert | - |
| 0x08 | Hoehenstand hoehere Seite | mm |
| 0x09 | Hoehenstand tiefere Seite | mm |
| 0x10 | Hoehenstand rechts | mm |
| 0x11 | Hoehenstand links | mm |
| 0xXY | unbekannte Umweltbedingung | XY |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 12 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| HA_H | 0 | 0x01 |
| HA_S | 0 | 0x02 |
| HL_H | 0 | 0x04 |
| HR_H | 0 | 0x08 |
| HL_S | 0 | 0x10 |
| HR_S | 0 | 0x20 |
| HAND_ENDE | 0 | 0x80 |
| VERLADE_EIN | 1 | 0x01 |
| VERLADE_AUS | 1 | 0x02 |
| BAND_EIN | 1 | 0x10 |
| BAND_AUS | 1 | 0x20 |
| XXX | Y | Z |
