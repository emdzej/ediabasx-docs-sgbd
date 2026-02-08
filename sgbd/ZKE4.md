# ZKE4.prg

- Jobs: [16](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zentrale Karosserie-Elektronik IV  fuer E36 |
| ORIGIN | BMW TP-421 Gerd Huber |
| REVISION | 1.06 |
| AUTHOR | BMW TP-421 Gerd Huber |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer Grundmodul IV automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer GM IV
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_DIGITAL](#job-status-digital) - Status der Digitalsignale des GM IV (Ein-/Ausgaenge)
- [STATUS_ANALOG](#job-status-analog) - Status der Analogsignale des GM IV
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs v. GM4
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten des GM IV (Block 0)
- [INFOSPEICHER_LESEN](#job-infospeicher-lesen) - Infospeicher lesen Info-Speicher ist im Aufbau identisch dem Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose
- [STEUERN_SIMULTAN](#job-steuern-simultan) - Gleichzeitiges Ansteuern maximal 5 digitaler Signale des GM4 !!! ACHTUNG: ZKE IV antwortet nicht !!! ??? !!!

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

Init-Job fuer Grundmodul IV automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer GM IV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_BMW_NR_KURZ | string | letzte 2 Stellen der BMW-Teilenummer |
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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| F_LOESCHDATUM_KW | int | Loeschdatum des Fehlerspeichers (KW) |
| F_LOESCHDATUM_JAHR | int | Loeschdatum des Fehlerspeichers (Jahr) |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOESCHDATUM_KW | int | aktuelle Kalenderwoche beim Loeschen des Fehlerspeichers |
| LOESCHDATUM_JAHR | int | aktuelles Kalemderjahr beim Loeschen des Fehlerspeichers |

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
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
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
| FG_ZIFFERN | string | Ziffern der FG-Nummer, die in den Pruefstempel geschrieben werden |
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

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status der Digitalsignale des GM IV (Ein-/Ausgaenge)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_VR1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ER1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_VR2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ER2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_VR3_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ER3_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_IRA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_IRB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL15_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL58_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL50_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL30ZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL30IB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRVR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL30FH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KISI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES3_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES4_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES5_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHA2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHZ2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHA2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHZ2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HKK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HFK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TGFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKFH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_NGEG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEBH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RES6_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ZS22_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEFH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEHS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRDWA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DRFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DOA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DDWAL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DNGAG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_IGFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_IGBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_CS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DIB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DVA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DTSH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RDWA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DWAL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_NGAG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MVR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WFSI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_IB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_VA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_TSH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_KOE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_IGV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RXD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_TXD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_KS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_FSHD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RESA1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_CSMODE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DIAGMOD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status der Analogsignale des GM IV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_V30E_WERT | long | Spannung an Klemme 30E Bereich: ? bis ? |
| STAT_V30E_EINH | string | Einheit: 'Volt' |
| STAT_VIGV_WERT | long | Spannung IGFV, IGBV Bereich: ? bis ? |
| STAT_VIGV_EINH | string | Einheit: 'Volt' |
| STAT_IFFH_WERT | long | Strom FH Fahrer hinten Bereich: ? bis ? |
| STAT_IFFH_EINH | string | Einheit: 'Ampere' |
| STAT_IFBH_WERT | long | Strom BH Beifahrer hinten Bereich: ? bis ? |
| STAT_IFBH_EINH | string | Einheit: 'Ampere' |
| STAT_IFFHMAX_WERT | long | Anlauf-Strom FH Fahrer hinten Bereich: ? bis ? |
| STAT_IFFHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_IFBHMAX_WERT | long | Anlauf-Strom FH Beifahrer hinten Bereich: ? bis ? |
| STAT_IFBHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_VMFFZ_WERT | long | Spannung FH Fahrer zu Bereich: ? bis ? |
| STAT_VMFFZ_EINH | string | Einheit: 'Volt' |
| STAT_VMFBZ_WERT | long | Spannung FH Beifahrer zu Bereich: ? bis ? |
| STAT_VMFBZ_EINH | string | Einheit: 'Volt' |
| STAT_V31L_WERT | long | Spannung Last-Masse Klemme 31L Bereich: ? bis ? |
| STAT_V31L_EINH | string | Einheit: 'Volt' |
| STAT_FFPOS_WERT | long | FT aktuelle Fensterposition Bereich: ? bis ? |
| STAT_FFPOS_EINH | string | Einheit: 'Milli-Meter' |
| STAT_FBPOS_WERT | long | BT aktuelle Fensterposition Bereich: ? bis ? |
| STAT_FBPOS_EINH | string | Einheit: 'Milli-Meter' |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs v. GM4

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten des GM IV (Block 0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_FH_DEAKTIV_NACH_KLR_AUS_EIN | int | 0 oder 1 |
| COD_FH_DEAKTIV_NACH_TUER_AUF_EIN | int | 0 oder 1 |
| COD_FH_NICHT_ABSENKEN_BEI_VK_AUF_EIN | int | 0 oder 1 |
| COD_FH_DEAKTIV_NACH_TUER_ZU_EIN | int | 0 oder 1 |
| COD_FH_AKTIV_NACH_TUER_AUF_EIN | int | 0 oder 1 |
| COD_MIT_FH_HINTEN_EIN | int | 0 oder 1 |
| COD_CABRIO_FUNKTIONEN_EIN | int | 0 oder 1 |
| COD_SCHEIBENABSENKUNG_SPERREN_EIN | int | 0 oder 1 |
| COD_KOMFORTSCHLIESSEN_SPERREN_EIN | int | 0 oder 1 |
| COD_FH_TIPP_AUF_FT_EIN | int | 0 oder 1 |
| COD_FH_TIPP_ZU_FT_EIN | int | 0 oder 1 |
| COD_FH_TIPP_AUF_BT_EIN | int | 0 oder 1 |
| COD_FH_TIPP_ZU_BT_EIN | int | 0 oder 1 |
| COD_FH_TIPP_AUF_HINTEN_EIN | int | 0 oder 1 |
| COD_FH_TIPP_ZU_HINTEN_EIN | int | 0 oder 1 |
| COD_FH_TIPP_AUF_ZENTRAL_EIN | int | 0 oder 1 |
| COD_FH_TIPP_ZU_ZENTRAL_EIN | int | 0 oder 1 |
| COD_MIT_DWA_EIN | int | 0 oder 1 |
| COD_MIT_NGAG_EIN | int | 0 oder 1 |
| COD_MIT_IR_SCHUTZ_EIN | int | 0 oder 1 |
| COD_MIT_SCHEIBENUEBERWACHUNG_EIN | int | 0 oder 1 |
| COD_RES_E6_AKTIV | int | 0 oder 1 |
| COD_RES_E1_AKTIV | int | 0 oder 1 |
| COD_SCHAERFEN_ENTSCHAERFEN_NUR_MIT_FB_EIN | int | 0 oder 1 |
| COD_ALARM_INTERVALLTON_EIN | int | 0 oder 1 |
| COD_OPTISCHER_ALARM_EIN | int | 0 oder 1 |
| COD_LED_BLITZT_EIN | int | 0 oder 1 |
| COD_HK_WIE_IR_EIN | int | 0 oder 1, Signale Heckklappe wie Fernbedienung |
| COD_ENTSICHERN_UEBER_HK_EIN | int | 0 oder 1 |
| COD_QUITTUNGSDAUER_AKUSTISCHER_ALARM_WERT | int | Dauer in ms (0 bis 150) |
| COD_QUITTIERUNG_BEIM_ENTSCHAERFEN_EIN | int | 0 oder 1 |
| COD_QUITTIERUNG_MIT_OPTISCHEM_ALARM_EIN | int | 0 oder 1 |
| COD_MIT_TSH_EIN | int | Tuerschlossheizung j/n |
| COD_IB_AUS_BEI_KL15_EIN | int | Innenbeleuchtung aus bei Kl 15 (1)/ R (0) ein |
| COD_IB_EIN_BEI_KLR_AUS_OHNE_KL58_EIN | int | 0 oder 1 |
| COD_IB_SOFT_ON_OFF_EIN | int | 0 oder 1 |
| COD_IB_NICHT_EIN_BEI_TGFT_EIN | int | 0 oder 1 |
| COD_IB_NICHT_EIN_BEI_IR_ENTRIEGELN_EIN | int | 0 oder 1 |
| COD_IB_GENERELL_EIN_BEI_ENTRIEGELN_EIN | int | 0 oder 1 |
| COD_EKS_EMPFINDLICHKEIT_FH_VORN_WERT | int | Empfindlichkeit EKS in Inkrementen |
| COD_ANLAUF_UNTERDR_GLEICHE_RICHTUNG_FH_VORN_WERT | int | in Inkrementen |
| COD_ANLAUF_UNTERDR_GEGEN_RICHTUNG_FH_VORN_WERT | int | in Inkrementen |
| COD_ABSCHALTUNG_SCHEIBENABSENKUNG_BEIM_SCHLIESSEN_WERT | int | in Inkrementen |
| COD_ABSCHALTUNG_SCHEIBENABSENKUNG_BEIM_OEFFNEN_WERT | int | in Inkrementen |
| COD_POS_FH_VORN_EKS_MIN_WERT | int | Min-Pos EKS in Inkrementen |
| COD_POS_FH_VORN_EKS_MAX_WERT | int | Max-Pos EKS in Inkrementen |
| COD_GESAMTWEG_FH_VORN_WERT | int | Gesamtweg FH vorn in Inkrementen |
| COD_DATEN | binary | alle Codierdaten vorerst als reine Datenbytes |
| DATENSICHERUNG_BLOCK_0 | string | Datensicherungsbyte fuer Block 0 |
| _TEL_ANTWORT | binary |  |

<a id="job-infospeicher-lesen"></a>
### INFOSPEICHER_LESEN

Infospeicher lesen Info-Speicher ist im Aufbau identisch dem Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| F_LOESCHDATUM_KW | int | Loeschdatum des Infospeichers (KW) |
| F_LOESCHDATUM_JAHR | int | Loeschdatum des Infospeichers (Jahr) |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

<a id="job-steuern-simultan"></a>
### STEUERN_SIMULTAN

Gleichzeitiges Ansteuern maximal 5 digitaler Signale des GM4 !!! ACHTUNG: ZKE IV antwortet nicht !!! ??? !!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT2 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT3 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT4 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT5 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (63 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [IORTTEXTE](#table-iorttexte) (31 × 2)
- [BITS](#table-bits) (100 × 6)

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

| LIEF_NR | LIEF_TEXT |
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
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 63 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Sicherung Innenbeleuchtung, Verbraucherabschaltung, Tuerschlossheizung |
| 0x02 | Sicherung Zentralverriegelung |
| 0x03 | Sicherung Fensterheber vorne |
| 0x04 | Leitung Klemme R fehlt |
| 0x05 | Leitung Klemme 15 fehlt |
| 0x06 | Leitung Klemme 31L fehlt |
| 0x28 | Codierung GM IV EEPROM |
| 0x29 | GM IV EEPROM |
| 0x2A | Kurzschluss oder Leitung Innenraumbeleuchtung |
| 0x2B | Unterbrechung oder Leitung Verbraucherabschaltung |
| 0x2C | Kurzschluss oder Leitung Verbraucherabschaltung |
| 0x2D | Unterbrechung oder Leitung Tuerschlossheizung |
| 0x2E | Kurzschluss oder Leitung Tuerschlossheizung |
| 0x08 | Crash-Sensor oder Verbindung ZAE2 |
| 0x09 | ZS-Kontakt |
| 0x0A | FT: Aggregat oder Kurzschluss gegen U-Batt |
| 0x0B | FT: Aggregat oder Leitungsunterbrechung |
| 0x0C | BT: Aggregat oder Kurzschluss gegen U-Batt |
| 0x0D | BT: Aggregat oder Leitungsunterbrechung |
| 0x0E | HK: Aggregat oder Kurzschluss gegen U-Batt |
| 0x0F | HK: Aggregat oder Leitungsunterbrechung |
| 0x30 | Relaiskleber Signal MER nach Masse |
| 0x31 | Relaiskleber Signal MER nach U-Batt |
| 0x32 | Relaiskleber Signal MVR nach Masse |
| 0x33 | Relaiskleber Signal MVR nach U-Batt |
| 0x34 | Relaiskleber Signal MZS nach Masse |
| 0x35 | Relaiskleber Signal MZS nach U-Batt |
| 0x11 | Leitungen IGFV, IGBV Kurzschluss nach Masse oder Impulsgeber FH-Motor |
| 0x36 | GM IV: Relaiskleber Signal MFFA nach Masse |
| 0x37 | GM IV: Relaiskleber Signal MFFA nach U-Batt |
| 0x38 | GM IV: Relaiskleber Signal MFFZ nach Masse |
| 0x39 | GM IV: Relaiskleber Signal MFFZ nach U-Batt |
| 0x3A | GM IV: Relaiskleber Signal MFBA nach Masse |
| 0x3B | GM IV: Relaiskleber Signal MFBA nach U-Batt |
| 0x3C | GM IV: Relaiskleber Signal MFBZ nach Masse |
| 0x3D | GM IV: Relaiskleber Signal MFBZ nach U-Batt |
| 0x3E | Thermoschalter FH FT angesprochen oder Motor Impulsgeber |
| 0x3F | Thermoschalter FH BT angesprochen oder Motor Impulsgeber |
| 0x12 | FH-Motor Fahrer hinten: Thermo-Sicherung, FH-Motor oder Leitungen |
| 0x13 | Leitung IFFH Kurzschluss gegen Masse oder RM IV |
| 0x14 | RM IV Relaiskleber nach U-Batt oder Leitung IFFH Kurzschluss gegen Masse |
| 0x15 | FH-Motor Beifahrer hinten: Thermo-Sicherung, FH-Motor oder Leitungen |
| 0x16 | Leitung IFBH Kurzschluss gegen Masse oder RM IV |
| 0x17 | RM IV Relaiskleber nach U-Batt oder Leitung IFBH Kurzschluss gegen Masse |
| 0x18 | RM IV oder Leitung RFFHA Unterbrechung oder Kurzschluss gegen Masse |
| 0x19 | RM IV oder Leitung RFFHA Kurzschluss gegen U-Batt |
| 0x1A | RM IV oder Leitung RFBHA Unterbrechung oder Kurzschluss gegen Masse |
| 0x1B | RM IV oder Leitung RFBHA Kurzschluss gegen U-Batt |
| 0x1C | RM IV oder Leitung RFFHZ Unterbrechung oder Kurzschluss gegen Masse |
| 0x1D | RM IV oder Leitung RFFHZ Kurzschluss gegen U-Batt |
| 0x1E | RM IV oder Leitung RFBHZ Unterbrechung oder Kurzschluss gegen Masse |
| 0x1F | RM IV oder Leitung RFBHZ Kurzschluss gegen U-Batt |
| 0x42 | FH-Motor Fahrer hinten blockiert oder Mechanik schwergaengig |
| 0x43 | FH-Motor Beifahrer hinten blockiert oder Mechanik schwergaengig |
| 0x22 | CVM oder Leitung SFBHA2, SFBHZ2 Kurzschluss gegen Masse &gt; 0,5 sec |
| 0x23 | Crash-Alarm-Geber oder Leitung OA Kurzschluss gegen U-Batt |
| 0x24 | DWA-LED oder Leitung DWAL Kurzschluss gegen U-Batt |
| 0x25 | DWA-LED oder Leitung DWAL Unterbrechung oder Kurzschluss gegen Masse |
| 0x26 | DWA-Relais oder Leitung RDWA Kurzschluss gegen U-Batt |
| 0x27 | Neigungsgeber oder Innenraumschutz oder Leitung NGAG/ISAG Kurzschluss gegen U-Batt |
| 0x44 | Neigungsgeber, Sicherung oder Leitung |
| 0x45 | Innenraumschutz, Sicherung oder Leitung |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 31 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x80 | Klemme R |
| 0x81 | Klemme 15 |
| 0x82 | Klemme 50 |
| 0x83 | Tuerkontakt FT |
| 0x84 | Tuerkontakt BT |
| 0x85 | Tuerkontakt FTH |
| 0x86 | Tuerkontakt BTH / Entriegelung Verdeck |
| 0x87 | Heckklappenkontakt |
| 0x88 | Handschuhfachkontakt |
| 0x89 | Motorhaubenkontakt |
| 0x8A | Neigungsgeber |
| 0x8B | Heckscheibe |
| 0x8C | Scheibenueberwachung FT |
| 0x8D | Scheibenueberwachung BT |
| 0x8E | Scheibenueberwachung FTH |
| 0x8F | Scheibenueberwachung BTH |
| 0x90 | Innenraumschutz |
| 0x91 | Manipulation Aggregat FT |
| 0x92 | Manipulation Aggregat BT |
| 0x93 | Manipulation Aggregat HK |
| 0x94 | Reserve-Eingang RES6 |
| 0x95 | Reserve-Eingang RES1 |
| 0x96 | Panik-Mode |
| 0xA0 | Wiederholsperre ZV angesprochen |
| 0xA1 | Crash wurde ausgeloest |
| 0xA2 | BC hat DWA-Horn angesteuert / Leitung RDWA oder Relais fehlt |
| 0xA3 | Power-On-Reset (Batterie oder GM IV abgeklemmt) |
| 0xB0 | Watchdog-Reset (Software GM IV oder EMV-Stoerung) |
| 0xB1 | Illegal Opcode-Reset (EMV-Stoerung oder ROM GM IV defekt) |
| 0xB2 | Clock-Monitor-Reset (GM IV Oszillator defekt oder GM IV Platine verschmutzt/feucht) |
| 0xXY | unbekannter Info-Ort |

<a id="table-bits"></a>
### BITS

Dimensions: 100 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| VR1 | 0 | 0x01 | 0x01 | E | Verriegeln FT |
| ER1 | 0 | 0x02 | 0x02 | E | Entriegeln FT |
| VR2 | 0 | 0x04 | 0x04 | E | Verriegeln BT |
| ER2 | 0 | 0x08 | 0x08 | E | Entriegeln BT |
| VR3 | 0 | 0x10 | 0x10 | E | Verriegeln HK |
| ER3 | 0 | 0x20 | 0x20 | E | Entriegeln HK |
| IRA | 0 | 0x40 | 0x40 | E | ZV-Fernbedienung Signal A |
| IRB | 0 | 0x80 | 0x80 | E | ZV-Fernbedienung Signal B |
| ZS | 1 | 0x01 | 0x01 | E | Zentralsichern |
| KL15 | 1 | 0x02 | 0x02 | E | Klemme 15 |
| KL58 | 1 | 0x04 | 0x04 | E | Klemme 58 |
| KL50 | 1 | 0x08 | 0x08 | E | Klemme 50 |
| KLR | 1 | 0x10 | 0x10 | E | Klemme R |
| TZV | 1 | 0x20 | 0x20 | E | Taster ZV (Reserve) |
| RES1 | 1 | 0x40 | 0x40 | E | Reserve 1 |
| RES2 | 1 | 0x80 | 0x80 | E | Reserve 2 |
| DRFA | 2 | 0x01 | 0x01 | E | Diagnose-Relais FH Fahrer auf |
| KL30ZV | 2 | 0x02 | 0x02 | E | Klemme 30 Zentralverriegelung |
| DRBA | 2 | 0x04 | 0x04 | E | Diagnose-Relais FH Beifahrer auf |
| KL30IB | 2 | 0x08 | 0x08 | E | Klemme 30 Innenlicht |
| DRVR | 2 | 0x10 | 0x10 | E | Diagnose-Relais ZV verriegeln |
| DRER | 2 | 0x20 | 0x20 | E | Diagnose-Relais ZV entriegeln |
| DRZS | 2 | 0x40 | 0x40 | E | Diagnose-Relais ZV sichern |
| KL30FH | 2 | 0x80 | 0x80 | E | Klemme 30 Fensterheber |
| SFFA | 3 | 0x01 | 0x01 | E | FH-Schalter Fahrer auf |
| SFFZ | 3 | 0x02 | 0x02 | E | FH-Schalter Fahrer zu |
| SFBA | 3 | 0x04 | 0x04 | E | FH-Schalter Beifahrer auf |
| SFBZ | 3 | 0x08 | 0x08 | E | FH-Schalter Beifahrer zu |
| KISI | 3 | 0x10 | 0x10 | E | Kindersicherung FH-Schalter hinten |
| RES3 | 3 | 0x20 | 0x20 | E | Reserve 3 (EKS-Leiste Fahrer hinten) |
| RES4 | 3 | 0x40 | 0x40 | E | Reserve 4 (EKS-Leiste Beifahrer hinten) |
| RES5 | 3 | 0x80 | 0x80 | E | Reserve 5 |
| SFFHA | 4 | 0x01 | 0x01 | E | FH-Schalter Fahrer hinten auf |
| SFFHZ | 4 | 0x02 | 0x02 | E | FH-Schalter Fahrer hinten zu |
| SFBHA | 4 | 0x04 | 0x04 | E | FH-Schalter Beifahrer hinten auf |
| SFBHZ | 4 | 0x08 | 0x08 | E | FH-Schalter Beifahrer hinten zu |
| SFFHA2 | 4 | 0x10 | 0x10 | E | SFFH hinten auf (E36/C: FH Zentral auf) |
| SFFHZ2 | 4 | 0x20 | 0x20 | E | SFFH hinten zu (E36/C: FH Zentral zu) |
| SFBHA2 | 4 | 0x40 | 0x40 | E | SFBH hinten auf (E36/C: CVM: alle FH auf) |
| SFBHZ2 | 4 | 0x80 | 0x80 | E | SFBH hinten zu (E36/C: CVM: alle FH zu) |
| HKK | 5 | 0x01 | 0x01 | E | Heckklappenkontakt |
| MHK | 5 | 0x02 | 0x02 | E | Motorhaubenkontakt |
| HFK | 5 | 0x04 | 0x04 | E | Handschuhfachkontakt |
| TGFT | 5 | 0x08 | 0x08 | E | Tuergriff Fahrertuer |
| TKFT | 5 | 0x10 | 0x10 | E | Tuerkontakt Fahrertuer |
| TKBT | 5 | 0x20 | 0x20 | E | Tuerkontakt Beifahrertuer |
| TKFH | 5 | 0x40 | 0x40 | E | Tuerkontakt Fahrertuer hinten (E36/C: Verdeckklappe) |
| TKBH | 5 | 0x80 | 0x80 | E | Tuerkontakt Beifahrertuer hinten (E36/C: Verdeck entriegeln) |
| NGEG | 6 | 0x01 | 0x01 | E | Eingang Neigungsgeber |
| SUEF | 6 | 0x02 | 0x02 | E | Scheibenueberwachung Fahrer bzw. INRS |
| SUEB | 6 | 0x04 | 0x04 | E | Scheibenueberwachung Beifahrer |
| SUEBH | 6 | 0x08 | 0x08 | E | Scheibenueberwachung Beifahrer hinten |
| RES6 | 6 | 0x10 | 0x10 | E | Reserve 6 |
| ZS22 | 6 | 0x20 | 0x20 | E | zusaetzliches Signal Ferbedienung (Panik) |
| SUEFH | 6 | 0x40 | 0x40 | E | Scheibenueberwachung Fahrer hinten |
| SUEHS | 6 | 0x80 | 0x80 | E | Scheibenueberwachung Heckscheibe |
| DRDWA | 7 | 0x01 | 0x01 | E | Diagnose-Relais DWA-Horn |
| DRFFHA | 7 | 0x02 | 0x02 | E | Diagnose-Relais FFH auf |
| DRFBHA | 7 | 0x04 | 0x04 | E | Diagnose-Relais FBH auf |
| DRFFHZ | 7 | 0x08 | 0x08 | E | Diagnose-Relais FFH zu |
| DRFBHZ | 7 | 0x10 | 0x10 | E | Diagnose-Relais FBH zu |
| DOA | 7 | 0x20 | 0x20 | E | Diagnose Optischer Alarm |
| DDWAL | 7 | 0x40 | 0x40 | E | Diagnose DWA-LED |
| DNGAG | 7 | 0x80 | 0x80 | E | Diagnose Neigungsgeber |
| IGFA | 8 | 0x01 | 0x01 | E | Impulsgeber FH-Motor Fahrer A |
| IGBA | 8 | 0x04 | 0x04 | E | Impulsgeber FH-Motor Beifahrer A |
| CS | 8 | 0x80 | 0x80 | E | Crash-Sensor |
| DIB | 9 | 0x01 | 0x01 | E | Diagnose IB |
| DVA | 9 | 0x02 | 0x02 | E | Diagnose VA |
| DTSH | 9 | 0x04 | 0x04 | E | Diagnose TSH |
| RDWA | 10 | 0x01 | 0x01 | A | Relais DWA-Horn |
| RFFHA | 10 | 0x02 | 0x02 | A | FH-Relais Fahrer hinten auf |
| RFBHA | 10 | 0x04 | 0x04 | A | FH-Relais Beifahrer hinten auf |
| RFFHZ | 10 | 0x08 | 0x08 | A | FH-Relais Fahrer hinten zu |
| RFBHZ | 10 | 0x10 | 0x10 | A | FH-Relais Beifahrer hinten zu |
| OA | 10 | 0x20 | 0x20 | A | DWA: Optischer Alarm |
| DWAL | 10 | 0x40 | 0x40 | A | DWA-LED |
| NGAG | 10 | 0x80 | 0x80 | A | Ausgang Neigungsgeber |
| MFFA | 11 | 0x01 | 0x01 | A | FH-Motor Fahrer auf |
| MFFZ | 11 | 0x02 | 0x02 | A | FH-Motor Fahrer zu |
| MFBA | 11 | 0x04 | 0x04 | A | FH-Motor Beifahrer auf |
| MFBZ | 11 | 0x08 | 0x08 | A | FH-Motor Beifahrer zu |
| MVR | 11 | 0x10 | 0x10 | A | ZV-Motor verriegeln |
| MER | 11 | 0x20 | 0x20 | A | ZV-Motor entriegeln |
| MZS | 11 | 0x40 | 0x40 | A | ZV-Motor sichern |
| WFSI | 11 | 0x80 | 0x80 | A | Wegfahrsicherung Motronic |
| IB | 12 | 0x01 | 0x01 | A | Innenlicht |
| VA | 12 | 0x02 | 0x02 | A | Verbraucherabschaltung EIN |
| TSH | 12 | 0x04 | 0x04 | A | Tuerschlossheizung |
| KOE | 12 | 0x08 | 0x08 | A | Komfortoeffnen Verdeck |
| IGV | 12 | 0x10 | 0x10 | A | Versorgung Impulsgeber |
| RXD | 13 | 0x01 | 0x01 | A | Leitung RxD |
| TXD | 13 | 0x02 | 0x02 | A | Leitung TxD |
| KS | 13 | 0x04 | 0x04 | A | Komfortschliessen FH, SHD, Verdeck |
| WB | 13 | 0x08 | 0x08 | A | Crash-Warnblinken |
| FSHD | 13 | 0x10 | 0x10 | A | Freigabe SHD (Komfortrelais) |
| RESA1 | 13 | 0x20 | 0x20 | A | Reserve-Ausgang 1 |
| CSMODE | 14 | 0x01 | 0x01 | A | System im Crash-Mode |
| DIAGMOD | 14 | 0x02 | 0x02 | A | System im Diagnose-Mode |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
