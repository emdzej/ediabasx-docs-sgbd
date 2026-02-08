# ZKE3_PM1.prg

- Jobs: [30](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: Memorymodule E38, E39 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.00 |
| AUTHOR | BMW TI-433 Gerd Huber, BMW TP-422 Frank Fannasch |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 1.00 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer GM III
- [STATUS_DIGITAL_SM_LSM](#job-status-digital-sm-lsm) - Status der Digitalsignale des SM/LSM (Ein-/Ausgaenge) nur bei E38 / nicht bei E39
- [STATUS_ANALOG_SM](#job-status-analog-sm) - Status der Achsenposition des SM
- [STATUS_ANALOG_SMBF](#job-status-analog-smbf) - Status der Achsenposition des SMBF
- [STATUS_ANALOG_LSM](#job-status-analog-lsm) - Status der Achsenposition des LSM
- [STATUS_ANALOG_SM_LAENGS_MIN_MAX](#job-status-analog-sm-laengs-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_HOEHE_MIN_MAX](#job-status-analog-sm-hoehe-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_NEIGUNG_MIN_MAX](#job-status-analog-sm-neigung-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_LEHNE_MIN_MAX](#job-status-analog-sm-lehne-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_KOPF_MIN_MAX](#job-status-analog-sm-kopf-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_SITZTIEFE_MIN_MAX](#job-status-analog-sm-sitztiefe-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SM_LEHNENKOPF_MIN_MAX](#job-status-analog-sm-lehnenkopf-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_LSM_NEIGUNG_MIN_MAX](#job-status-analog-lsm-neigung-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_LSM_LAENGS_MIN_MAX](#job-status-analog-lsm-laengs-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_LAENGS_MIN_MAX](#job-status-analog-smbf-laengs-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_HOEHE_MIN_MAX](#job-status-analog-smbf-hoehe-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_NEIGUNG_MIN_MAX](#job-status-analog-smbf-neigung-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_LEHNE_MIN_MAX](#job-status-analog-smbf-lehne-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_KOPF_MIN_MAX](#job-status-analog-smbf-kopf-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_SITZTIEFE_MIN_MAX](#job-status-analog-smbf-sitztiefe-min-max) - Status des Schleppzeigerwertes der Achse
- [STATUS_ANALOG_SMBF_LEHNENKOPF_MIN_MAX](#job-status-analog-smbf-lehnenkopf-min-max) - Status des Schleppzeigerwertes der Achse
- [STEUERN_DIGITAL_SM_LSM](#job-steuern-digital-sm-lsm) - Ansteuern eines digitalen Ein- oder Ausgangs des SM_LSM nur bei E38 / nicht bei E39
- [STATUS_DIGITAL_SMBF](#job-status-digital-smbf) - Status der Digitalsignale des SMBF (Ein-/Ausgaenge) nur bei E38 / nicht bei E39
- [STEUERN_DIGITAL_SMBF](#job-steuern-digital-smbf) - Ansteuern eines digitalen Ein- oder Ausgangs des SMBF nur bei E38 / nicht bei E39
- [STATUS_DIGITAL_SMSFB](#job-status-digital-smsfb) - Status der Digitalsignale des SMSFB (Ein-/Ausgaenge) nur bei E38 / nicht bei E39
- [STEUERN_DIGITAL_SMSFB](#job-steuern-digital-smsfb) - Ansteuern eines digitalen Ein- oder Ausgangs des SMSFB nur bei E38 / nicht bei E39
- [STEUERN_DIGITAL_NACHEINANDER](#job-steuern-digital-nacheinander) - Ansteuern maximal 5 digitaler Signale des GM3 oder eines Peripheriemoduls NACHEINANDER
- [IDENT_SW_NR_TUEREN](#job-ident-sw-nr-tueren) - Vergleich der Softwarenummern der Tuermodule FT und BT

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

Ident-Daten fuer GM III

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| P_MODUL | string | gewuenschtes Peripheriemodul table PeripherieModule PM_ABK PM_TEXT |

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

<a id="job-status-digital-sm-lsm"></a>
### STATUS_DIGITAL_SM_LSM

Status der Digitalsignale des SM/LSM (Ein-/Ausgaenge) nur bei E38 / nicht bei E39

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_MSLFAVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSLFAZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHFAAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHFAAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNFAAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNFAAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNFAVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNFAZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKFAAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKFAAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOFAV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOFAZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKVFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKZFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLSNAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLSNAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLSLVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLSLZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm"></a>
### STATUS_ANALOG_SM

Status der Achsenposition des SM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE0_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH | string | Einheit: '1' |
| STAT_ACHSE1_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH | string | Einheit: '1' |
| STAT_ACHSE2_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH | string | Einheit: '1' |
| STAT_ACHSE3_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH | string | Einheit: '1' |
| STAT_ACHSE4_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH | string | Einheit: '1' |
| STAT_ACHSE5_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH | string | Einheit: '1' |
| STAT_ACHSE6_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf"></a>
### STATUS_ANALOG_SMBF

Status der Achsenposition des SMBF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE0_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH | string | Einheit: '1' |
| STAT_ACHSE1_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH | string | Einheit: '1' |
| STAT_ACHSE2_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH | string | Einheit: '1' |
| STAT_ACHSE3_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH | string | Einheit: '1' |
| STAT_ACHSE4_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH | string | Einheit: '1' |
| STAT_ACHSE5_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH | string | Einheit: '1' |
| STAT_ACHSE6_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-lsm"></a>
### STATUS_ANALOG_LSM

Status der Achsenposition des LSM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE7_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE7_EINH | string | Einheit: '1' |
| STAT_ACHSE8_WERT | int | aktuelle Achsenposition Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE8_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-laengs-min-max"></a>
### STATUS_ANALOG_SM_LAENGS_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE0_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE0_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-hoehe-min-max"></a>
### STATUS_ANALOG_SM_HOEHE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE1_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE1_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-neigung-min-max"></a>
### STATUS_ANALOG_SM_NEIGUNG_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE2_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE2_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-lehne-min-max"></a>
### STATUS_ANALOG_SM_LEHNE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE3_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE3_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-kopf-min-max"></a>
### STATUS_ANALOG_SM_KOPF_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE4_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE4_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-sitztiefe-min-max"></a>
### STATUS_ANALOG_SM_SITZTIEFE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE5_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE5_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-sm-lehnenkopf-min-max"></a>
### STATUS_ANALOG_SM_LEHNENKOPF_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE6_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE6_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-lsm-neigung-min-max"></a>
### STATUS_ANALOG_LSM_NEIGUNG_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE7_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE7_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE7_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE7_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-lsm-laengs-min-max"></a>
### STATUS_ANALOG_LSM_LAENGS_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE8_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE8_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE8_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE8_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-laengs-min-max"></a>
### STATUS_ANALOG_SMBF_LAENGS_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE0_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE0_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE0_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-hoehe-min-max"></a>
### STATUS_ANALOG_SMBF_HOEHE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE1_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE1_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE1_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-neigung-min-max"></a>
### STATUS_ANALOG_SMBF_NEIGUNG_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE2_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE2_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE2_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-lehne-min-max"></a>
### STATUS_ANALOG_SMBF_LEHNE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE3_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE3_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE3_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-kopf-min-max"></a>
### STATUS_ANALOG_SMBF_KOPF_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE4_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE4_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE4_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-sitztiefe-min-max"></a>
### STATUS_ANALOG_SMBF_SITZTIEFE_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE5_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE5_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE5_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-smbf-lehnenkopf-min-max"></a>
### STATUS_ANALOG_SMBF_LEHNENKOPF_MIN_MAX

Status des Schleppzeigerwertes der Achse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ACHSE6_WERT_MAX | int | aktueller min Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH_MAX | string | Einheit: '1' |
| STAT_ACHSE6_WERT_MIN | int | aktueller max Wert der Achse Bereich: 0 bis 0xFFFF (mit Vorzeichen) |
| STAT_ACHSE6_EINH_MIN | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-sm-lsm"></a>
### STEUERN_DIGITAL_SM_LSM

Ansteuern eines digitalen Ein- oder Ausgangs des SM_LSM nur bei E38 / nicht bei E39

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_SM_LSM NAME ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-smbf"></a>
### STATUS_DIGITAL_SMBF

Status der Digitalsignale des SMBF (Ein-/Ausgaenge) nur bei E38 / nicht bei E39

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_MSLBFVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSLBFZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNBFVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNBFZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOBFV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOBFZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKVBF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKZBF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-smbf"></a>
### STEUERN_DIGITAL_SMBF

Ansteuern eines digitalen Ein- oder Ausgangs des SMBF nur bei E38 / nicht bei E39

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_SMBF NAME ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-smsfb"></a>
### STATUS_DIGITAL_SMSFB

Status der Digitalsignale des SMSFB (Ein-/Ausgaenge) nur bei E38 / nicht bei E39

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_MSLBFVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSLBFZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSHBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSNBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNBFVO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MLNBFZU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKBFAF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MKBFAB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOBFV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MSOBFZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKVBF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_LKZBF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-smsfb"></a>
### STEUERN_DIGITAL_SMSFB

Ansteuern eines digitalen Ein- oder Ausgangs des SMSFB nur bei E38 / nicht bei E39

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_SMBF NAME ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-nacheinander"></a>
### STEUERN_DIGITAL_NACHEINANDER

Ansteuern maximal 5 digitaler Signale des GM3 oder eines Peripheriemoduls NACHEINANDER

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| P_MODUL | string | Name des gewuenschten Peripherie-Moduls table PeripherieModule PM_ABK PM_TEXT |
| SEKUNDEN | int | Pausenzeit am Ende in Sekunden ACHTUNG: Zeitangabe funktioniert nicht bei EDIABAS im EDIC |
| ORT1 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT2 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT3 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT4 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT5 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG1 | binary |  |
| _TEL_AUFTRAG2 | binary |  |
| _TEL_AUFTRAG3 | binary |  |
| _TEL_AUFTRAG4 | binary |  |
| _TEL_AUFTRAG5 | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-ident-sw-nr-tueren"></a>
### IDENT_SW_NR_TUEREN

Vergleich der Softwarenummern der Tuermodule FT und BT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| SW_NR_IDENTISCH | int | 1 wenn gleich - 0 wenn verschieden |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [PERIPHERIEMODULE](#table-peripheriemodule) (9 × 3)
- [BITS_SM_LSM](#table-bits-sm-lsm) (19 × 6)
- [BITS_SMBF](#table-bits-smbf) (15 × 6)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 69 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
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
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-peripheriemodule"></a>
### PERIPHERIEMODULE

Dimensions: 9 rows × 3 columns

| PM_NR | PM_ABK | PM_TEXT |
| --- | --- | --- |
| 0x00 | GM3 | Grundmodul III |
| 0x01 | FT | Fahrertuer |
| 0x02 | BT | Beifahrertuer |
| 0x03 | SHD | Schiebehebedach |
| 0x04 | SB | Schalterblock |
| 0x05 | SM_LSM | Sitz/Lenksaeulenmemory Fahrer |
| 0x08 | SM_BF | Sitzmemory Beifahrer |
| 0x09 | SM_SFB | Sitzmemory Fernbedienung Beifahrersitz |
| 0xXY | XY | ERROR_PM_UNBEKANNT |

<a id="table-bits-sm-lsm"></a>
### BITS_SM_LSM

Dimensions: 19 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| MSLFAVO | 1 | 0x01 | 0x01 | E | Sitzschlitten vor |
| MSLFAZU | 1 | 0x02 | 0x02 | E | Sitzschlitten zurueck |
| MSHFAAF | 1 | 0x04 | 0x04 | E | Sitzhoehe auf |
| MSHFAAB | 1 | 0x08 | 0x08 | E | Sitzhoehe ab |
| MSNFAAF | 1 | 0x10 | 0x10 | E | Sitzneigung auf |
| MSNFAAB | 1 | 0x20 | 0x20 | E | Sitzneigung ab |
| MLNFAVO | 1 | 0x40 | 0x40 | E | Sitzlehne vor |
| MLNFAZU | 1 | 0x80 | 0x80 | E | Sitzlehne zurueck |
| MKFAAF | 2 | 0x01 | 0x01 | E | Kopfstuetze auf |
| MKFAAB | 2 | 0x02 | 0x02 | E | Kopfstuetze ab |
| MSOFAV | 2 | 0x04 | 0x04 | E | Sitztiefe vor |
| MSOFAZ | 2 | 0x08 | 0x08 | E | Sitztiefe zurueck |
| LKVFA | 2 | 0x10 | 0x10 | E | Lehnenkopf vor |
| LKZFA | 2 | 0x20 | 0x20 | E | Lehnenkopf zurueck |
| MLSNAF | 2 | 0x40 | 0x40 | E | Lenksaeule auf |
| MLSNAB | 2 | 0x80 | 0x80 | E | Lenksaeule ab |
| MLSLVO | 3 | 0x01 | 0x01 | E | Lenksaeule vor |
| MLSLZU | 3 | 0x02 | 0x02 | E | Lenksaeule zurueck |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |

<a id="table-bits-smbf"></a>
### BITS_SMBF

Dimensions: 15 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| MSLBFVO | 1 | 0x01 | 0x01 | E | Sitzschlitten vor |
| MSLBFZU | 1 | 0x02 | 0x02 | E | Sitzschlitten zurueck |
| MSHBFAF | 1 | 0x04 | 0x04 | E | Sitzhoehe auf |
| MSHBFAB | 1 | 0x08 | 0x08 | E | Sitzhoehe ab |
| MSNBFAF | 1 | 0x10 | 0x10 | E | Sitzneigung auf |
| MSNBFAB | 1 | 0x20 | 0x20 | E | Sitzneigung ab |
| MLNBFVO | 1 | 0x40 | 0x40 | E | Sitzlehne vor |
| MLNBFZU | 1 | 0x80 | 0x80 | E | Sitzlehne zurueck |
| MKBFAF | 2 | 0x01 | 0x01 | E | Kopfstuetze auf |
| MKBFAB | 2 | 0x02 | 0x02 | E | Kopfstuetze ab |
| MSOBFV | 2 | 0x04 | 0x04 | E | Sitztiefe vor |
| MSOBFZ | 2 | 0x08 | 0x08 | E | Sitztiefe zurueck |
| LKVBF | 2 | 0x10 | 0x10 | E | Lehnenkopf vor |
| LKZBF | 2 | 0x20 | 0x20 | E | Lehnenkopf zurueck |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
