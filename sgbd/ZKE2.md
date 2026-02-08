# ZKE2.prg

- Jobs: [19](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zentrale Karosserie-Elektronik II |
| ORIGIN | BMW ET-421 Gerd Huber |
| REVISION | 1.12 |
| AUTHOR | Pioneer Martin Moll, BMW ET-421 Teepe, BMW ET-421 Gerd Huber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FEHLERZAEHLER_LESEN](#job-fehlerzaehler-lesen) - Auslesen des Fehlerzaehlers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Abbruch der Diagnose-Kommunikation
- [STATUS_GRUPPE_0_LESEN](#job-status-gruppe-0-lesen) - Auslesen des Statusfelds Gruppe 0
- [STATUS_GRUPPE_1_LESEN](#job-status-gruppe-1-lesen) - Auslesen des Statusfelds Gruppe 1
- [STATUS_GRUPPE_2_LESEN](#job-status-gruppe-2-lesen) - Auslesen des Statusfelds Gruppe 2
- [STATUS_GRUPPE_3_LESEN](#job-status-gruppe-3-lesen) - Auslesen des Statusfelds Gruppe 3
- [STATUS_GRUPPE_4_LESEN](#job-status-gruppe-4-lesen) - Auslesen des Statusfelds Gruppe 4
- [STATUS_GRUPPE_5_LESEN](#job-status-gruppe-5-lesen) - Auslesen des Statusfelds Gruppe 5
- [STATUS_GRUPPE_6_LESEN](#job-status-gruppe-6-lesen) - Auslesen des Statusfelds Gruppe 6
- [STATUS_GRUPPE_7_LESEN](#job-status-gruppe-7-lesen) - Auslesen des Statusfelds Gruppe 7
- [STATUS_GRUPPE_8_LESEN](#job-status-gruppe-8-lesen) - Auslesen des Statusfelds Gruppe 8
- [STATUS_GRUPPE_9_LESEN](#job-status-gruppe-9-lesen) - Auslesen des Statusfelds Gruppe 9
- [CODIERUNG_LESEN](#job-codierung-lesen) - Codierdaten
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern der Ausgaenge

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| ID_GEN_NR | string | Generationsnummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |

<a id="job-fehlerzaehler-lesen"></a>
### FEHLERZAEHLER_LESEN

Auslesen des Fehlerzaehlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| F_ZAHL | int | Anzahl der Fehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 ( Werte: 0 bis 3 ) |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 ( Werte: 0 oder 1 ) |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_HFK | int | Haeufigkeit des Einzelfehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Abbruch der Diagnose-Kommunikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |

<a id="job-status-gruppe-0-lesen"></a>
### STATUS_GRUPPE_0_LESEN

Auslesen des Statusfelds Gruppe 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_RS_AKTIV | int | Status von RS, 0 oder 1 |
| STAT_NS_AKTIV | int | Status von NS, 0 oder 1 |
| STAT_RSK_AKTIV | int | Status von RSK, 0 oder 1 |
| STAT_SSSSHK_AKTIV | int | Status von SSSSHK, 0 oder 1 |
| STAT_SSSHK_AKTIV | int | Status von SSSHK, 0 oder 1 |
| STAT_SSPHK_AKTIV | int | Status von SSPHK, 0 oder 1 |
| STAT_SSOHK_AKTIV | int | Status von SSOHK, 0 oder 1 |
| STAT_WWNM_VOLL | int | Status von WWNM, 0 oder 1 |
| STAT_KL15_AKTIV | int | Status von Kl.15, 0 oder 1 |
| STAT_KLR_AKTIV | int | Status von Kl.R, 0 oder 1 |
| STAT_KL50_AKTIV | int | Status von Kl.50, 0 oder 1 |
| STAT_SWA_AKTIV | int | Status von SWA, 0 oder 1 |
| STAT_SWI_AKTIV | int | Status von SWI, 0 oder 1 |
| STAT_SWS1_AKTIV | int | Status von SWS1, 0 oder 1 |
| STAT_SWS2_AKTIV | int | Status von SWS2, 0 oder 1 |
| STAT_SIRS_AKTIV | int | Status von SIRS, 0 oder 1 |
| STAT_SW_AKTIV | int | Status von SW, 0 oder 1 |
| STAT_NSW_AKTIV | int | Status von NSW, 0 oder 1 |
| STAT_TKBH_OFFEN | int | Status von TKBH, 0 oder 1 |
| STAT_TKFH_OFFEN | int | Status von TKFH, 0 oder 1 |
| STAT_TKBT_OFFEN | int | Status von TKBT, 0 oder 1 |
| STAT_TKFT_OFFEN | int | Status von TKFT, 0 oder 1 |
| STAT_FKBH_ZU | int | Status von FKBH, 0 oder 1 |
| STAT_FKFH_ZU | int | Status von FKFH, 0 oder 1 |
| STAT_IRFB_AKTIV | int | Status von IRFB, 0 oder 1 |
| STAT_IRFA_AKTIV | int | Status von IRFA, 0 oder 1 |
| STAT_VRHK_AKTIV | int | Status von VRHK, 0 oder 1 |
| STAT_ERHK_AKTIV | int | Status von ERHK, 0 oder 1 |
| STAT_TBH_AKTIV | int | Status von TBH, 0 oder 1 |

<a id="job-status-gruppe-1-lesen"></a>
### STATUS_GRUPPE_1_LESEN

Auslesen des Statusfelds Gruppe 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_FBHZ_ZU | int | Status von FBHZ, 0 oder 1 |
| STAT_FBHA_AUF | int | Status von FBHA, 0 oder 1 |
| STAT_TFH_AKTIV | int | Status von TFH, 0 oder 1 |
| STAT_FFHZ_ZU | int | Status von FFHZ, 0 oder 1 |
| STAT_FFHA_AUF | int | Status von FFHA, 0 oder 1 |
| STAT_DSRA_AKTIV | int | Status von DSRA, 0 oder 1 |
| STAT_DSIR_AKTIV | int | Status von DSIR, 0 oder 1 |
| STAT_DWP_AKTIV | int | Status von DWP, 0 oder 1 |
| STAT_DWI3_AKTIV | int | Status von DWI3, 0 oder 1 |
| STAT_DWI2_AKTIV | int | Status von DWI2, 0 oder 1 |
| STAT_DWI1_AKTIV | int | Status von DWI1, 0 oder 1 |
| STAT_DKS_AKTIV | int | Status von DKS, 0 oder 1 |
| STAT_DADV_AKTIV | int | Status von DADV, 0 oder 1 |
| STAT_FSTBH_AKTIV | int | Status von FSTBH, 0 oder 1 |
| STAT_FSZBH_ZU | int | Status von FSZBH, 0 oder 1 |
| STAT_FSABH_AUF | int | Status von FSABH, 0 oder 1 |
| STAT_FSTFH_AKTIV | int | Status von FSTFH, 0 oder 1 |
| STAT_FSZFH_ZU | int | Status von FSZFH, 0 oder 1 |
| STAT_FSAFH_AUF | int | Status von FSAFH, 0 oder 1 |
| STAT_FSKS_AKTIV | int | Status von FSKS, 0 oder 1 |
| STAT_FSTFT_AKTIV | int | Status von FSTFT, 0 oder 1 |
| STAT_FSZFT_ZU | int | Status von FSZFT, 0 oder 1 |
| STAT_FSAFT_AUF | int | Status von FSAFT, 0 oder 1 |
| STAT_FSTBT_AKTIV | int | Status von FSTBT, 0 oder 1 |
| STAT_FSZBT_ZU | int | Status von FSTBT, 0 oder 1 |
| STAT_FSABT_AUF | int | Status von FSABT, 0 oder 1 |

<a id="job-status-gruppe-2-lesen"></a>
### STATUS_GRUPPE_2_LESEN

Auslesen des Statusfelds Gruppe 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_RADVA_AKTIV | int | Status von RADVA, 0 oder 1 |
| STAT_RADVZ_AKTIV | int | Status von RADVZ, 0 oder 1 |
| STAT_WPK_AKTIV | int | Status von WPK, 0 oder 1 |
| STAT_RKSA_AUF | int | Status von RKSA, 0 oder 1 |
| STAT_RKSZ_ZU | int | Status von RKSZ, 0 oder 1 |
| STAT_RWI1_AKTIV | int | Status von RWI1, 0 oder 1 |
| STAT_RWI2_AKTIV | int | Status von RWI2, 0 oder 1 |
| STAT_RWI3_AKTIV | int | Status von RWI3, 0 oder 1 |
| STAT_RWP_AKTIV | int | Status von RWP, 0 oder 1 |
| STAT_RSIR_AKTIV | int | Status von RSIR, 0 oder 1 |
| STAT_RSRA1_AKTIV | int | Status von RSRA1, 0 oder 1 |
| STAT_RSRA2_AKTIV | int | Status von RSRA2, 0 oder 1 |
| STAT_RMFFA_AUF | int | Status von RMFFA, 0 oder 1 |
| STAT_RMFFZ_ZU | int | Status von RMFFZ, 0 oder 1 |
| STAT_RMFFHA_AUF | int | Status von RMFFHA, 0 oder 1 |
| STAT_RMFFHZ_ZU | int | Status von RMFFHZ, 0 oder 1 |
| STAT_RMFBA_AUF | int | Status von RMFBA, 0 oder 1 |
| STAT_RMFBZ_ZU | int | Status von RMFBZ, 0 oder 1 |
| STAT_RMFBHA_AUF | int | Status von RMFBHA, 0 oder 1 |
| STAT_RMFBHZ_ZU | int | Status von RMFBHZ, 0 oder 1 |
| STAT_RMZS_AKTIV | int | Status von RMZS, 0 oder 1 |
| STAT_RMVR_AKTIV | int | Status von RMVR, 0 oder 1 |
| STAT_RMER_AKTIV | int | Status von RMER, 0 oder 1 |
| STAT_RMSFT_AKTIV | int | Status von RMSFT, 0 oder 1 |
| STAT_RMSFTR_AKTIV | int | Status von RMSFTR, 0 oder 1 |
| STAT_RMSR_AKTIV | int | Status von RMSR, 0 oder 1 |
| STAT_RMSBT_AKTIV | int | Status von RMSBT, 0 oder 1 |
| STAT_RMSFH_AKTIV | int | Status von RMSFH, 0 oder 1 |
| STAT_RMSBH_AKTIV | int | Status von RMSBH, 0 oder 1 |
| STAT_RMSHK_AKTIV | int | Status von RMSHK, 0 oder 1 |

<a id="job-status-gruppe-3-lesen"></a>
### STATUS_GRUPPE_3_LESEN

Auslesen des Statusfelds Gruppe 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_RHKA_AKTIV | int | Status von RHKA, 0 oder 1 |
| STAT_RVA_AKTIV | int | Status von RVA, 0 oder 1 |
| STAT_RESL_AKTIV | int | Status von RESL, 0 oder 1 |
| STAT_RESR_AKTIV | int | Status von RESR, 0 oder 1 |
| STAT_ZS1_AKTIV | int | Status von ZS1, 0 oder 1 |
| STAT_ZS1N_AKTIV | int | Status von ZS1N, 0 oder 1 |
| STAT_RWB_AKTIV | int | Status von RWB, 0 oder 1 |
| STAT_RIB_AKTIV | int | Status von RIB, 0 oder 1 |
| STAT_SSHDA_AUF | int | Status von SSHDA, 0 oder 1 |
| STAT_SSHDZ_ZU | int | Status von SSHDZ, 0 oder 1 |
| STAT_SSHDH_AKTIV | int | Status von SSHDH, 0 oder 1 |
| STAT_RSHDA_AUF | int | Status von RSHDA, 0 oder 1 |
| STAT_RSHDZ_ZU | int | Status von RSHDZ, 0 oder 1 |
| STAT_MSHDA_AUF | int | Status von MSHDA, 0 oder 1 |
| STAT_MSHDZ_ZU | int | Status von MSHDZ, 0 oder 1 |
| STAT_QZSHD_ZU | int | Status von QZSHD, 0 oder 1 |
| STAT_SFHAFH_AUF | int | Status von SFHAFH, 0 oder 1 |
| STAT_SFHZFH_ZU | int | Status von SFHZFH, 0 oder 1 |
| STAT_SFHTFH_AKTIV | int | Status von SFHTFH, 0 oder 1 |

<a id="job-status-gruppe-4-lesen"></a>
### STATUS_GRUPPE_4_LESEN

Auslesen des Statusfelds Gruppe 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_MAFAFH_AUF | int | Status von MAFAFH, 0 oder 1 |
| STAT_MAFZFH_ZU | int | Status von MAFZFH, 0 oder 1 |
| STAT_SSPFH_AKTIV | int | Status von SSPFH, 0 oder 1 |
| STAT_SSSSFH_AKTIV | int | Status von SSSSFH, 0 oder 1 |
| STAT_TGIFH_AKTIV | int | Status von TGIFH, 0 oder 1 |
| STAT_QZFH_ZU | int | Status von QZFH, 0 oder 1 |
| STAT_ZVERFH_AKTIV | int | Status von ZVERFH, 0 oder 1 |
| STAT_ZVVRFH_AKTIV | int | Status von ZVVRFH, 0 oder 1 |
| STAT_TGAFH_AKTIV | int | Status von TGAFH, 0 oder 1 |
| STAT_SFHABH_AUF | int | Status von SFHABH, 0 oder 1 |
| STAT_SFHZBH_ZU | int | Status von SFHZBH, 0 oder 1 |
| STAT_SFHTBH_AKTIV | int | Status von SFHTBH, 0 oder 1 |
| STAT_MAFABH_AUF | int | Status von MAFABH, 0 oder 1 |
| STAT_MAFZBH_ZU | int | Status von MAFZBH, 0 oder 1 |
| STAT_SSPBH_AKTIV | int | Status von SSPBH, 0 oder 1 |
| STAT_SSSSBH_AKTIV | int | Status von SSSSBH, 0 oder 1 |
| STAT_TGIBH_AKTIV | int | Status von TGIBH, 0 oder 1 |

<a id="job-status-gruppe-5-lesen"></a>
### STATUS_GRUPPE_5_LESEN

Auslesen des Statusfelds Gruppe 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_QZBH_ZU | int | Status von QZBH, 0 oder 1 |
| STAT_ZVERBH_AKTIV | int | Status von ZVERBH, 0 oder 1 |
| STAT_ZVVRBH_AKTIV | int | Status von ZVVRBH, 0 oder 1 |
| STAT_TGKBH_AKTIV | int | Status von TGKBH, 0 oder 1 |
| STAT_SFHAFT_AUF | int | Status von SFHAFT, 0 oder 1 |
| STAT_SFHZFT_ZU | int | Status von SFHZFT, 0 oder 1 |
| STAT_SFHTFT_AKTIV | int | Status von SFHTFT, 0 oder 1 |
| STAT_TSHFT_AKTIV | int | Status von TSHFT, 0 oder 1 |
| STAT_MAFAFT_AUF | int | Status von MAFAFT, 0 oder 1 |
| STAT_MAFZFT_ZU | int | Status von MAFZFT, 0 oder 1 |
| STAT_SSPFT_AKTIV | int | Status von SSPFT, 0 oder 1 |
| STAT_SSSSFT_AKTIV | int | Status von SSSSFT, 0 oder 1 |
| STAT_TGIFT_AKTIV | int | Status von TGIFT, 0 oder 1 |
| STAT_QZFT_ZU | int | Status von QZFT, 0 oder 1 |
| STAT_ZVERFT_AKTIV | int | Status von ZVERFT, 0 oder 1 |
| STAT_ZVVRFT_AKTIV | int | Status von ZVVRFT, 0 oder 1 |
| STAT_TGKFT_AKTIV | int | Status von TGKFT, 0 oder 1 |
| STAT_TSAFT_AKTIV | int | Status von TSAFT, 0 oder 1 |
| STAT_TSBFT_AKTIV | int | Status von TSBFT, 0 oder 1 |
| STAT_TSBNFT_AKTIV | int | Status von TSBNFT, 0 oder 1 |
| STAT_TSCFT_AKTIV | int | Status von TSCFT, 0 oder 1 |
| STAT_SFHABT_AUF | int | Status von SFHABT, 0 oder 1 |
| STAT_SFHZBT_ZU | int | Status von SFHZBT, 0 oder 1 |

<a id="job-status-gruppe-6-lesen"></a>
### STATUS_GRUPPE_6_LESEN

Auslesen des Statusfelds Gruppe 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_SFHTBT_AKTIV | int | Status von SFHTBT, 0 oder 1 |
| STAT_MAFABT_AUF | int | Status von MAFABT, 0 oder 1 |
| STAT_MAFZBT_ZU | int | Status von MAFZBT, 0 oder 1 |
| STAT_SSPBT_AKTIV | int | Status von SSPBT, 0 oder 1 |
| STAT_SSSSBT_AKTIV | int | Status von SSSSBT, 0 oder 1 |
| STAT_TGIBT_AKTIV | int | Status von TGIBT, 0 oder 1 |
| STAT_QZBT_ZU | int | Status von QZBT, 0 oder 1 |
| STAT_ZVERBT_AKTIV | int | Status von ZVERBT, 0 oder 1 |
| STAT_ZVVRBT_AKTIV | int | Status von ZVVRBT, 0 oder 1 |
| STAT_TGKBT_AKTIV | int | Status von TGKBT, 0 oder 1 |
| STAT_TSABT_AKTIV | int | Status von TSABT, 0 oder 1 |
| STAT_TSBBT_AKTIV | int | Status von TSBBT, 0 oder 1 |
| STAT_TSBNBT_AKTIV | int | Status von TSBNBT, 0 oder 1 |
| STAT_TSCBT_AKTIV | int | Status von TSCBT, 0 oder 1 |

<a id="job-status-gruppe-7-lesen"></a>
### STATUS_GRUPPE_7_LESEN

Auslesen des Statusfelds Gruppe 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_STDCON_AKTIV | int | Status von STDCON, 0 oder 1 |
| STAT_SLP_AKTIV | int | Status von SLP, 0 oder 1 |

<a id="job-status-gruppe-8-lesen"></a>
### STATUS_GRUPPE_8_LESEN

Auslesen des Statusfelds Gruppe 8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| STAT_FHPF_WERT | int | Status von FHPF, E 31: 0 bis 120, E 32: 0 bis 178 |
| STAT_FHPB_WERT | int | Status von SLP, E 31: 0 bis 120, E 32: 0 bis 178 |
| STAT_FHPFH_WERT | int | Status von FHPFH, E 32: 0 bis 178 |
| STAT_FHPBH_WERT | int | Status von FHPBH, E 32: 0 bis 178 |

<a id="job-status-gruppe-9-lesen"></a>
### STATUS_GRUPPE_9_LESEN

Auslesen des Statusfelds Gruppe 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_SG_NACK |
| STAT_SHDP_WERT | int | Status von SHDP, 0 (Heb.) bis 23 (zu) bis 193 (auf) |
| STAT_ADVP_WERT | int | Status von ADVP, 0 bis 4 |
| STAT_SSS_WERT | int | Status von SSS, 0 bis 255 |
| STAT_V_WERT | int | Status von V, 0 bis 6 |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| FAHRZEUGTYP_TEXT | string | Liefert: E31 oder E32 |
| SHD_VORHANDEN | int | Liefert: 0 oder 1 |
| SERVOSCHLIESSUNG_VORHANDEN | int | Liefert: 0 oder 1 |
| TSH_VORHANDEN | int | Liefert: 0 oder 1 |
| SCHEINWERFERREINIGUNG_VORHANDEN | int | Liefert: 0 oder 1 |
| LENKERTYP_TEXT | string | Liefert: Linkslenker oder Rechtslenker |
| SIR_VORHANDEN | int | Liefert: 0 oder 1 |
| ADV_VORHANDEN | int | Liefert: 0 oder 1 |
| FENSTERABSENKUNG_VORHANDEN | int | Liefert: 0 oder 1 |
| WISCHERMECHANIKPARKSTELLUNG_VORHANDEN | int | Liefert: 0 oder 1 |
| LAENDERVARIANTE_BYTE | string | Liefert: Laendervariante (original Byte) |
| LAENDERVARIANTE_TEXT | string | Liefert: Laendervariante Klartext (vgl. Tabelle Laender) |
| EINKLEMMSCHUTZ_FH_WERT | int | FH Schwelle Einklemmschutz FT und BT |
| IMPULSZAHL_FH_WERT | int | FH Impulszahl Absenkung (Hex) |
| SHD_IMPULSZAHL_POS_ZU | int | SHD Impulszahl Geschlossen Position * 2 (Hex) |
| SHD_IMPULSZAHL_ENDPOS_SCHIEBEN | int | SHD Impulszahl Schieben Endposition (Hex) |
| HW_NR | int | Liefert: 0 oder 1 |
| HW_NR_TEXT | string | Liefert: Standardcodierung oder Serienanlauf |
| HERSTELLER_NR | int | Liefert: 0 oder 1 |
| HERSTELLER_NR_TEXT | string | Liefert: Standardcodierung oder Reinshagen |
| DATUM_KW | int | Liefert: 1 bis 52 |
| DATUM_JAHR | int | Liefert 1980 bis 2079 |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern der Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table SteuerParameter AUSGANG |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY od. ERROR_SG_NACK od. ERROR_SG_UNBEKANNTES_STATUSBYTE |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (70 × 2)
- [FARTTEXTE](#table-farttexte) (5 × 2)
- [STEUERPARAMETER](#table-steuerparameter) (161 × 2)
- [LAENDER](#table-laender) (6 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 70 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | GM II |
| 0x01 | TM FT, Verbindung zu GM II |
| 0x02 | TM BT, Verbindung zu GM II |
| 0x03 | TM FTH, Verbindung zu GM II |
| 0x04 | TM BTH, Verbindung zu GM II |
| 0x05 | SHDM, Verbindung zu GM II |
| 0x06 | TM FT |
| 0x07 | TM BT |
| 0x08 | TM FTH |
| 0x09 | TM BTH |
| 0x0A | SHDM |
| 0x0B | RM1, Verbindung zu GM II |
| 0x0C | RM2, Verbindung zu GM II |
| 0x0D | FH Schalter FA, Verbindung zu GM II |
| 0x3E | Klemme R an GM II fehlerhaft |
| 0x0E | Wischerschalter, Zuleitung |
| 0x0F | Wischermotor, Zuleitung, Rueckstellkontakte |
| 0x10 | ADV-Motor, Zuleitung, Nockenschalter |
| 0x11 | Relais Wischermotor I, Zuleitung, Sicherung, RM1 |
| 0x12 | Relais Wischermotor II, Zuleitung, Sicherung, RM1 |
| 0x13 | Relais Wischermotor III, Zuleitung, Sicherung, RM1 |
| 0x14 | Relais Wasserpumpe, Zuleitung, Sicherung, RM1 |
| 0x15 | Relais SIR, Zuleitung, Sicherung, RM1 |
| 0x16 | DRM 2 ADV, Zuleitung, Sicherung, RM1 |
| 0x17 | DRM 2 SRA, Zuleitung, Sicherung, RM1 |
| 0x27 | TM FT, TSH, Zuleitung |
| 0x1E | Schlossschalter FT, Zuleitung |
| 0x1F | Schlossschalter BT, Zuleitung |
| 0x20 | Antrieb ZV FT, Schalter ZV FT, Zuleitung |
| 0x21 | Antrieb ZV BFT, Schalter ZV BFT, Zuleitung |
| 0x22 | Antrieb ZV Heckklappe, Schalter ZV Heckklappe, Zuleitung |
| 0x23 | RM1 (Relais ZS), Sicherungsrelais I |
| 0x24 | RM1 (Relais VR), Sicherungsrelais I |
| 0x25 | RM1 (Relais ER), Sicherungsrelais I |
| 0x26 | CRASH-Stromschalter, Zuleitung |
| 0x28 | FH Schalter FT, Zuleitung |
| 0x29 | FH Schalter BT, Zuleitung |
| 0x2A | FH Schalter FTH,Zuleitung |
| 0x2B | FH Schalter BTH, Zuleitung |
| 0x2C | FH Motor FT, Zuleitung, Inkrementgeber |
| 0x2D | FH Motor BT, Zuleitung, Inkrementgeber |
| 0x2E | FH Motor BTH, Fensterkontakt FAH, Zuleitung, RM1 |
| 0x2F | FH Motor BTH, Fensterkontakt BFH, Zuleitung, RM1 |
| 0x18 | RM1 (Relais Fensterheber FT auf, FFA), Sicherungsrelais I |
| 0x19 | RM1 (Relais Fensterheber BT auf, FBA), Sicherungsrelais II |
| 0x1A | RM1 (Relais Fensterheber FTH auf, FFHA), Sicherungsrelais I |
| 0x1B | RM1 (Relais Fensterheber BTH auf, FBHA), Sicherungsrelais II |
| 0x1C | RM1 (Relais Fensterheber FT zu, FFZ), Sicherungsrelais I |
| 0x1D | RM1 (Relais Fensterheber BT zu, FBZ), Sicherungsrelais II |
| 0x3C | RM1 (Relais Fensterheber FTH zu, FFHZ), Sicherungsrelais I |
| 0x3D | RM1 (Relais Fensterheber BTH zu, FBHZ), Sicherungsrelais II |
| 0x41 | FT Verbindungsleitung RM1 - FH Motor |
| 0x42 | BT Verbindungsleitung RM1 - FH Motor |
| 0x43 | FTH Verbindungsleitung RM1 - FH Motor |
| 0x44 | BTH Verbindungsleitung RM1 - FH Motor |
| 0x30 | SHD Schalter, Zuleitung |
| 0x31 | SHD Motor, SHD-Modul (Inkrementgeber) |
| 0x32 | SHD Motor (Relais), Sicherungsrelais I, Dachzuleitung |
| 0x33 | Positionsgeber Motor, Zuleitung, Sicherung FT |
| 0x34 | Positionsgeber Motor, Zuleitung, Sicherung BT |
| 0x35 | Positionsgeber Motor, Zuleitung, Sicherung FTH |
| 0x36 | Positionsgeber Motor, Zuleitung, Sicherung BTH |
| 0x37 | Positionsgeber Motor, Zuleitung, Sicherung Heckklappe |
| 0x38 | RM 2 (Relais 1-2), Sicherung FT |
| 0x39 | RM 2 (Relais 3 - 7), Sicherung, BT, BHT, FHT, Heckklappe |
| 0x3A | Ueberstromzaehler Sicherungsrelais I, zu hoher Strom an MFFA, MFFZ, MFFHA, MFFHZ, MER, MVR, MZS, 3OESL |
| 0x3B | Ueberstromzaehler Sicherungsrelais II, zu hoher Strom an MFBA, MFBZ, MFBHZ, MFBHA |
| 0x3F | zu hoher Strom an GMII RESL, RESR, IB, GRA, GRB, WB, RA1 - RA5, DTX, RMDA, RMLD, RMTR |
| 0x40 | zu hoher Strom an RM1 WI1, WI2, WI3, WP, SIR, VA, ERHK |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 5 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Kurzschluss gegen U-Batt |
| 0x01 | Kurzschluss gegen Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | ungueltiger Arbeitsbereich |
| 0xFF | unbekannte Fehlerart |

<a id="table-steuerparameter"></a>
### STEUERPARAMETER

Dimensions: 161 rows × 2 columns

| ZELLE | AUSGANG |
| --- | --- |
| 0x00 | RS |
| 0x01 | NS |
| 0x03 | RSK |
| 0x04 | SSSSHK |
| 0x05 | SSSHK |
| 0x06 | SSPHK |
| 0x07 | SSOHK |
| 0x08 | WWNM |
| 0x0A | KL15 |
| 0x0B | KLR |
| 0x0C | KL50 |
| 0x0D | SWA |
| 0x0E | SWI |
| 0x0F | SWS1 |
| 0x10 | SWS2 |
| 0x11 | SIRS |
| 0x12 | SW |
| 0x13 | NSW |
| 0x14 | TKBH |
| 0x15 | TKFH |
| 0x16 | TKBT |
| 0x17 | TKFT |
| 0x18 | FKBH |
| 0x19 | FKFH |
| 0x1B | IRFB |
| 0x1C | IRFA |
| 0x1D | VRHK |
| 0x1E | ERHK |
| 0x1F | TBH |
| 0x20 | FBHZ |
| 0x21 | FBHA |
| 0x22 | TFH |
| 0x23 | FFHZ |
| 0x24 | FFHA |
| 0x25 | DSRA |
| 0x26 | DSIR |
| 0x27 | DWP |
| 0x28 | DWI3 |
| 0x29 | DWI2 |
| 0x2A | DWI1 |
| 0x2B | DKS |
| 0x2D | DADV |
| 0x31 | FSTBH |
| 0x32 | FSZBH |
| 0x33 | FSABH |
| 0x35 | FSTFH |
| 0x36 | FSZFH |
| 0x37 | FSAFH |
| 0x38 | FSKS |
| 0x39 | FSTFT |
| 0x3A | FSZFT |
| 0x3B | FSAFT |
| 0x3D | FSTBT |
| 0x3E | FSZBT |
| 0x3F | FSABT |
| 0x40 | RADVA |
| 0x41 | RADVZ |
| 0x43 | WPK |
| 0x44 | RKSA |
| 0x45 | RKSZ |
| 0x46 | RWI1 |
| 0x47 | RWI2 |
| 0x48 | RWI3 |
| 0x49 | RWP |
| 0x4A | RSIR |
| 0x4B | RSRA1 |
| 0x4C | RSRA2 |
| 0x4D | RMFFA |
| 0x4E | RMFFZ |
| 0x4F | RMFFHA |
| 0x50 | RMFFHZ |
| 0x51 | RMFBA |
| 0x52 | RMFBZ |
| 0x53 | RMFBHA |
| 0x54 | RMFBHZ |
| 0x55 | RMZS |
| 0x56 | RMVR |
| 0x57 | RMER |
| 0x59 | RMSFT |
| 0x5A | RMSFTR |
| 0x5B | RMSR |
| 0x5C | RMSBT |
| 0x5D | RMSFH |
| 0x5E | RMSBH |
| 0x5F | RMSHK |
| 0x60 | RHKA |
| 0x61 | RVA |
| 0x62 | RESL |
| 0x63 | RESR |
| 0x67 | ZS1 |
| 0x68 | ZS1N |
| 0x69 | RWB |
| 0x6F | RIB |
| 0x70 | SSHDA |
| 0x71 | SSHDZ |
| 0x72 | SSHDH |
| 0x73 | RSHDA |
| 0x74 | RSHDZ |
| 0x75 | MSHDA |
| 0x76 | MSHDZ |
| 0x79 | QZSHD |
| 0x7C | SFHAFH |
| 0x7D | SFHZFH |
| 0x7E | SFHTFH |
| 0x81 | MAFAFH |
| 0x82 | MAFZFH |
| 0x83 | SSPFH |
| 0x84 | SSSSFH |
| 0x8B | TGIFH |
| 0x8C | QZFH |
| 0x8D | ZVERFH |
| 0x8E | ZVVRFH |
| 0x8F | TGAFH |
| 0x90 | SFHABH |
| 0x91 | SFHZBH |
| 0x92 | SFHTBH |
| 0x95 | MAFABH |
| 0x96 | MAFZBH |
| 0x97 | SSPBH |
| 0x98 | SSSSBH |
| 0x9F | TGIBH |
| 0xA0 | QZBH |
| 0xA1 | ZVERBH |
| 0xA2 | ZVVRBH |
| 0xA3 | TGKBH |
| 0xA4 | SFHAFT |
| 0xA5 | SFHZFT |
| 0xA6 | SFHTFT |
| 0xA8 | TSHFT |
| 0xA9 | MAFAFT |
| 0xAA | MAFZFT |
| 0xAB | SSPFT |
| 0xAC | SSSSFT |
| 0xB5 | TGIFT |
| 0xB6 | QZFT |
| 0xB7 | ZVERFT |
| 0xB8 | ZVVRFT |
| 0xB9 | TGKFT |
| 0xBA | TSAFT |
| 0xBB | TSBFT |
| 0xBC | TSBNFT |
| 0xBD | TSCFT |
| 0xBE | SFHABT |
| 0xBF | SFHZBT |
| 0xC0 | SFHTBT |
| 0xC3 | MAFABT |
| 0xC4 | MAFZBT |
| 0xC5 | SSPBT |
| 0xC6 | SSSSBT |
| 0xCF | TGIBT |
| 0xD0 | QZBT |
| 0xD1 | ZVERBT |
| 0xD2 | ZVVRBT |
| 0xD3 | TGKBT |
| 0xD4 | TSABT |
| 0xD5 | TSBBT |
| 0xD6 | TSBNBT |
| 0xD7 | TSCBT |
| 0xE6 | STDCON |
| 0xF0 | SLP |
| 0xFF | ERROR_UNBEKANNTER_PARAMETER |

<a id="table-laender"></a>
### LAENDER

Dimensions: 6 rows × 2 columns

| LV | LAENDERVARIANTE |
| --- | --- |
| 0x00 | ECE |
| 0x01 | US |
| 0x02 | Australien |
| 0x03 | Finnland |
| 0x04 | Reserve 1 |
| 0x05 | Reserve 2 |
