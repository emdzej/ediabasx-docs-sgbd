# LCM.prg

- Jobs: [22](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | LCM E38 / E39 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.06 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [IS_LESEN](#job-is-lesen) - infospeicherlesen job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Default CODIERUNG_LESEN job
- [CODIERUNG_LESEN_ALLES](#job-codierung-lesen-alles) - Default CODIERUNG_LESEN_ALLES job
- [CODIERUNG_BLOCK_1_LESEN](#job-codierung-block-1-lesen) - Default CODIERUNG_BLOCK_1_LESEN job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - DIAGNOSE_WEITER job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - DIAGNOSE_ENDE job
- [STATUS_VORGEBEN](#job-status-vorgeben) - Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreiben des Speicherinhaltes
- [STEUERN_DIMMER](#job-steuern-dimmer) - STEUERN_DIMMER job
- [STEUERN_LWR_POTI](#job-steuern-lwr-poti) - STEUERN_LWR_POTI job
- [FG_NR_LESEN](#job-fg-nr-lesen) - Default FG_NR_LESEN job
- [SIA_LESEN](#job-sia-lesen) - Default SIA_LESEN job
- [KALTABFRAGE_SCHREIBEN](#job-kaltabfrage-schreiben) - Default KALTABFRAGE_SCHREIBEN job

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |

<a id="job-is-lesen"></a>
### IS_LESEN

infospeicherlesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_5 | int | Anzahl der Fehler im Block 5 |
| F_ZAHL_BLOCK_6 | int | Anzahl der Fehler im Block 6 |
| F_ZAHL_BLOCK_7 | int | Anzahl der Fehler im Block 7 |
| F_ZAHL_BLOCK_8 | int | Anzahl der Fehler im Block 8 |
| F_ZAHL_BLOCK_9 | int | Anzahl der Fehler im Block 9 |
| F_ZAHL_BLOCK_10 | int | Anzahl der Fehler im Block 10 |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_1 | int | Anzahl der Fehler im Block 1 |
| F_ZAHL_BLOCK_2 | int | Anzahl der Fehler im Block 2 |
| F_ZAHL_BLOCK_3 | int | Anzahl der Fehler im Block 3 |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |
| F_ZAHL | int | Anzahl der Gesamtfehler der Bloecke 1 bis 4 (schwere Fehler) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Default CODIERUNG_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| COD_STANDLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_ABBLENDLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_FERNLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_NEBELSCHEINWERFER_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_RUECKLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_RUECKFAHRSCHEINWERFER_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_NSL_LINKS_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_NSL_RECHTS_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_KEINE_BREMSLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_BREMSLICHT_MITTE_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_KENNZEICHENLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_ANHAENGER_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_BLS_FEHLERMELDUNG_EIN | int | 0 oder 1 |
| COD_BLS_B_SCHWELL_WERT | int | Schwellwert in km/h/s |
| COD_T_WARTE_FEHLER_BLS_WERT | int | Wartezeit bis Meldung Bremslichtschalter kommt [s] |
| COD_WERT_ABSCHALTUNG_STAND_PARKLICHT | int | 0 oder 1 |
| COD_WARNBLINKEN_ENABLE | int | 0 oder 1 |
| COD_KEINE_KALTUEBERWACHUNG_ABBLENDLICHT_EIN | int | 0 oder 1 |
| COD_KEINE_KALTUEBERWACHUNG_NSW_EIN | int | 0 oder 1 |
| COD_KEINE_KALTUEBERWACHUNG_FERNLICHT_EIN | int | 0 oder 1 |
| COD_PERIODENDAUER_KALTUEBERWACHUNG_WERT | int | Bereich von 0 bis 71.12 Sekunden |
| COD_ENTPRELLZEIT_FEHLERERKENNUNG_BLS_BEI_KLR | int | in ms (gueltiger Bereich 13 bis 325ms) |
| COD_ENTPRELLZAHL_FEHLERERKENNUNG | int | 2-255 |
| COD_TASTVERHAELTNIS_SPANNUNG_KLEMME58g_BEI_MIN_DIMMER | int | 5-255, 2 bis 100% |
| COD_TASTVERHAELTNISZUWACHS_KLEMME58g_BEI_MAX_DIMMER | int | 32 bis 255, 12- 100 % |
| COD_VERHAELTNIS_HELLIGKEIT_WBL_DIMMER | int | 50 - 128 |
| COD_ABFRAGEZEIT_AHM_IN_STOP_MODE | int | in ms |
| COD_SCHWELLE_AENDERUNG_DIMMER_AN_I_BUS | int | 1 bis 100, 255 entspricht 120 Grad drehwinkel |
| COD_FERNLICHT_DIMMUNG_TAG | int | 16 bis 255, 255 = 100% |
| COD_ZYKLUSZEIT_WERT | int | in Sekunden (50 bis 255)*20ms |
| _ANTWORT | binary | Antwort-Telegramm |

<a id="job-codierung-lesen-alles"></a>
### CODIERUNG_LESEN_ALLES

Default CODIERUNG_LESEN_ALLES job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNUMMER | int | angeforderter Datenblock |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BLOCK | int | angeforderte Blocknummer von 0 bis 17 |
| CODIERDATEN | binary | CODIERDATENFELD |

<a id="job-codierung-block-1-lesen"></a>
### CODIERUNG_BLOCK_1_LESEN

Default CODIERUNG_BLOCK_1_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LAENDERVARIANTE | string | codierte Laendervariante |
| CODIER_INDEX | int | Codierindex |
| CODIER_VARIANTE | int | Codierdatenvariante |

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLEMME_30A_EIN | int |  |
| STAT_KLEMME_30B_EIN | int |  |
| STAT_KLEMME_15_EIN | int |  |
| STAT_KLEMME_R_EIN | int |  |
| STAT_SCHALTER2_AL_EIN | int |  |
| STAT_SCHALTER2_SL_EIN | int |  |
| STAT_SCHALTER2_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER2_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER1_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER1_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER1_SL_EIN | int |  |
| STAT_SCHALTER1_AL_EIN | int |  |
| STAT_SCHALTER_NSL_EIN | int |  |
| STAT_SCHALTER_NSW_EIN | int |  |
| STAT_SCHALTER_FL_EIN | int |  |
| STAT_EINGANG1_BLS_EIN | int | Bremslichtschalter 1 |
| STAT_EINGANG_ZSK_EIN | int |  |
| STAT_EINGANG_GKFA_EIN | int |  |
| STAT_SCHALTER_LICHTHUPE_EIN | int |  |
| STAT_SCHALTER_WBL_EIN | int |  |
| STAT_EINGANG2_BLS_EIN | int |  |
| STAT_EINGANG_KFN_EIN | int |  |
| STAT_EINGANG_PANZERTUER_EIN | int |  |
| STAT_EINGANG_BRFN_EIN | int |  |
| STAT_EINGANG_LUFTANLAGE_EIN | int |  |
| STAT_EINGANG_LOESCHANLAGE_EIN | int |  |
| STAT_EINGANG_VGLESP_EIN | int |  |
| STAT_EINGANG_CARB_EIN | int |  |
| STAT_EINGANG_MOTOR_NOTPROGRAMM_EIN | int |  |
| STAT_EINGANG_ALARM_EIN | int |  |
| STAT_EINGANG_WWN_EIN | int |  |
| STAT_EINGANG_OELSTAND_STATISCH_EIN | int |  |
| STAT_AUSGANG_KZL_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_AL_RECHTS_EIN | int |  |
| STAT_AUSGANG_AL_LINKS_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_SL_INNEN_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSW_LINKS_EIN | int |  |
| STAT_AUSGANG_RFS_LINKS_EIN | int |  |
| STAT_AUSGANG_FL_LINKS_EIN | int |  |
| STAT_AUSGANG_FL_RECHTS_EIN | int |  |
| STAT_AUSGANG_NSW_RECHTS_EIN | int |  |
| STAT_AUSGANG_NSL_RECHTS_EIN | int |  |
| STAT_AUSGANG_LWR_EIN | int |  |
| STAT_AUSGANG_KZL_RECHTS_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSL_LINKS_EIN | int |  |
| STAT_AUSGANG_SL_INNEN_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_RFS_RECHTS_EIN | int |  |
| STAT_NOTFUNKTION_PER_DIAGNOSE_AKTIV | int |  |
| STAT_DIMMUNG_KL58g_EIN | int |  |
| STAT_DIMMUNG_WBL_SUCHBELEUCHTUNG_EIN | int |  |
| STAT_DIMMUNG_LICHTSCHALTERBELEUCHTUNG_EIN | int |  |
| STAT_NSL_ANHAENGER_EIN | int | Nebelschlusslicht |
| STAT_RFS_ANHAENGER_EIN | int | Rueckfahrscheinwerfer |
| STAT_WARNBLINKEN_AKTIV | int |  |
| STAT_U_BATT_WERT | int | 0 bis 18 Volt |
| STAT_U_BATT_EINH | string | Volt |
| STAT_BLINKLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_BLINKLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_BREMSLICHT_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_NSL_RFS_ANHAENGER_EIN | int | Nebelschlussleuchte, Rueckfahrscheinwerfer |
| STAT_UNTERSPANNUNG_AHM_EIN | int |  |
| STAT_PARITY_AHM | int | even ueber Bit 0 bis 6 von Byte 14 |
| STAT_KZL_LINKS_DEFEKT | int |  |
| STAT_BL_LINKS_DEFEKT | int |  |
| STAT_BL_RECHTS_DEFEKT | int |  |
| STAT_AL_RECHTS_DEFEKT | int |  |
| STAT_AL_LINKS_DEFEKT | int |  |
| STAT_SL_LINKS_VORN_DEFEKT | int |  |
| STAT_SL_INNEN_LINKS_HINTEN_DEFEKT | int |  |
| STAT_NSW_LINKS_DEFEKT | int |  |
| STAT_RFS_LINKS_DEFEKT | int |  |
| STAT_FL_LINKS_DEFEKT | int |  |
| STAT_FL_RECHTS_DEFEKT | int |  |
| STAT_NSW_RECHTS_DEFEKT | int |  |
| STAT_NSL_RECHTS_DEFEKT | int |  |
| STAT_KZL_RECHTS_DEFEKT | int |  |
| STAT_SL_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BREMSLICHT_MITTE_DEFEKT | int |  |
| STAT_SL_RECHTS_VORN_DEFEKT | int |  |
| STAT_BLK_RECHTS_VORN_DEFEKT | int |  |
| STAT_BLK_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BLK_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_NSL_LINKS_DEFEKT | int |  |
| STAT_SL_INNEN_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_SL_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_BLK_LINKS_VORN_DEFEKT | int |  |
| STAT_RFS_RECHTS_DEFEKT | int |  |
| STAT_EINGANGSSPANNUNG_DIMMER_WERT | int | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_WERT | int | 0 bis 5 Volt |
| STAT_CRASH_WARNBLINKEN_AKTIV | int |  |
| STAT_DWA_WARNBLINKEN_AKTIV | int |  |
| STAT_DWA_AL_BLINKEN_AKTIV | int |  |
| STAT_DWA_FL_BLINKEN_AKTIV | int |  |
| STAT_CRASHSENSOR_AKTIV | int |  |
| STAT_DWA_AUSGELOEST | int |  |
| STAT_OELSTAND_WARNUNG1_AUSGELOEST | int |  |
| STAT_OELSTANDSSENSOR_DEFEKT | int |  |
| STAT_OELSTAND_KATASTROPHE_AUSGELOEST | int |  |
| STAT_EINGANG_TOG_EIN | int |  |
| STAT_TOG_HEIZZEIT_WERT | real | in 50 mikrosekunden Schritten |
| STAT_TOG_HEIZZEIT_EINH | string | Sekunden |
| STAT_TOG_ABKUEHLZEIT_WERT | real | in 50 mikrosekunden Schritten |
| STAT_TOG_ABKUEHLZEIT_EINH | string | Sekunden |
| _ANTWORT | binary | antworttelegramm |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Herstellerdaten Byte 1 bis 4 (oder 10?) |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

DIAGNOSE_WEITER job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

DIAGNOSE_ENDE job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-vorgeben"></a>
### STATUS_VORGEBEN

Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIGH | int | gewuenschte Startadresse high als Hexwert! |
| LOW | int | gewuenschte Startadresse low als Hexwert! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | angeforderter Datenblock (32 Bytes!) |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Schreiben des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_HIGH | int | gewuenschte Adresse high als Hexwert! |
| ADRESSE_LOW | int | gewuenschte Adresse low als Hexwert! |
| WERT | int | gewuenschter Wert als Hexwert! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-dimmer"></a>
### STEUERN_DIMMER

STEUERN_DIMMER job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIMMWERT | int | gewuenschter Wert der Helligkeit [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-lwr-poti"></a>
### STEUERN_LWR_POTI

STEUERN_LWR_POTI job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POTI_WERT | int | gewuenschter Wert in [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-fg-nr-lesen"></a>
### FG_NR_LESEN

Default FG_NR_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| FG_NR | string | Fahrgestellnummer 7-stellig |

<a id="job-sia-lesen"></a>
### SIA_LESEN

Default SIA_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| GESAMTWEGSTRECKE_WERT | long | Zaehlerstand Gesamtwgstrecke (nur 100er Einheiten!) |
| GESAMTWEGSTRECKE_EINH | string | 100 km |
| SI_WEGZAEHLER_EINH | string | SI-km |
| SI_WEGZAEHLER_WERT | long |  |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_WERT | long | SI-Wegstrecke beim letzten Oelservice |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_EINH | string | SI-km |
| SI_ZEITINSPEKTIONSZAEHLER_WERT | long |  |
| SI_ZEITINSPEKTIONSZAEHLER_EINH | string | Tage |

<a id="job-kaltabfrage-schreiben"></a>
### KALTABFRAGE_SCHREIBEN

Default KALTABFRAGE_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KALTABFRAGE_BYTE | int | gewuenschter Wert der Kaltabfrage (0 bis 255) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _ANTWORT1 | binary | Antwort-Telegramm1 |
| _ANTWORT2 | binary | Antwort-Telegramm2 |
| _SENDEN | binary | Sendetelegramm |
| KALTABFRAGEZEIT_ALT_BYTE | int | alte Kaltabfragezeit als Byte |
| KALTABFRAGEZEIT_ALT_WERT | int | alte Kaltabfragezeit in Sekunden |
| KALTABFRAGEZEIT_ALT_EINH | string | "s" |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (37 × 2)
- [IORTTEXTE](#table-iorttexte) (32 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [STEUERN](#table-steuern) (65 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 37 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0A | RAM-Fehler des Mikro-Prozessors |
| 0x0B | ROM-Fehler des Mikro-Prozessors |
| 0x0C | EEPROM-Fehler des Mikro-Prozessors |
| 0x0D | redundante Eingaenge melden Widerspruch |
| 0x0E | PowerMOS-Statusleitung 1 staendig aktiv |
| 0x0F | PowerMOS-Statusleitung 2 staendig aktiv |
| 0x10 | PowerMOS-Statusleitung 3 staendig aktiv |
| 0x11 | Reserve Block 1 |
| 0x14 | Bremslichtschalter, Leitung offen |
| 0x15 | Bremslichtschalter, Kurzschluss gegen Masse |
| 0x16 | LWR-Potentiometer offen |
| 0x17 | Dimmer-Potentiometer offen |
| 0x18 | Verbindung zum AHM ist gestoert |
| 0x19 | Reserve Block 2 |
| 0x1E | Fehler am Treiberbaustein LWR |
| 0x1F | Ansteuerung Q21/Q22 LWR |
| 0x20 | Ansteuerung Q11/Q12 LWR |
| 0x21 | Reserve Block 3 |
| 0x28 | thermischer Oelsensor defekt |
| 0x29 | Fehler ?????, Block 4 |
| 0x2A | Fehler ?????, Block 4 |
| 0x32 | eine Klemme 30 fehlt |
| 0x33 | Klemme R fehlt |
| 0x34 | Klemme 15 fehlt |
| 0x35 | Fehler ?????, Block 5 |
| 0x36 | Fehler ?????, Block 5 |
| 0x3C | Fehler ?????, Block 6 |
| 0x3D | Fehler ?????, Block 6 |
| 0x3E | Fehler ?????, Block 6 |
| 0x3F | Fehler ?????, Block 6 |
| 0x40 | Fehler ?????, Block 6 |
| 0x46 | sporadischer Fehler beim Ansteuern des LWR-Treibers |
| 0x47 | Fehler ?????, Block 7 |
| 0x48 | Fehler ?????, Block 7 |
| 0x49 | Fehler ?????, Block 7 |
| 0x4A | Fehler ?????, Block 7 |
| 0xFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 32 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x50 | EEPROM CCM |
| 0x51 | Panzertuer offen |
| 0x52 | Bremsfluessigkeit pruefen |
| 0x53 | Oeldruck Motor |
| 0x54 | Kuehlwassertemperatur |
| 0x55 | Katalysator zu heiss |
| 0x56 | Einspritzanlage |
| 0x57 | Niveauregulierung |
| 0x58 | Motornotprogramm |
| 0x59 | Getriebenotprogramm |
| 0x5A | Bremsbelaege |
| 0x5B | Waschwasserstand |
| 0x5C | Luftanlage pruefen |
| 0x5D | Feuerloeschanlage pruefen |
| 0x5E | Funkschluessel Batterie |
| 0x5F | Kuehlwasser pruefen |
| 0x60 | Oelstand Motor TOG |
| 0x61 | Reifen defekt |
| 0x62 | Fehler ?????, Block 9 |
| 0x63 | Fehler ?????, Block 9 |
| 0x64 | Fehler ?????, Block 9 |
| 0x65 | Fehler ?????, Block 9 |
| 0x66 | Fehler ?????, Block 9 |
| 0x67 | Fehler ?????, Block 9 |
| 0x68 | Fehler ?????, Block 9 |
| 0x69 | Fehler ?????, Block 9 |
| 0x6A | Fehler ?????, Block 9 |
| 0x6B | Fehler ?????, Block 9 |
| 0x6C | Fehler ?????, Block 9 |
| 0x6D | Fehler ?????, Block 9 |
| 0x6E | Fehler ?????, Block A |
| 0xFF | unbekannter Fehlerort |

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

<a id="table-steuern"></a>
### STEUERN

Dimensions: 65 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| Kl30A | 0 | 0x01 |
| Kl30B | 0 | 0x02 |
| Kl15 | 0 | 0x04 |
| KlR | 0 | 0x08 |
| S2_AL | 0 | 0x10 |
| S2_SL | 0 | 0x20 |
| S2_BLK_R | 0 | 0x40 |
| S2_BLK_L | 0 | 0x80 |
| S1_BLK_L | 1 | 0x01 |
| S1_BLK_R | 1 | 0x02 |
| S1_SL | 1 | 0x04 |
| S1_AL | 1 | 0x08 |
| S_NSL | 1 | 0x10 |
| S_NSW | 1 | 0x20 |
| S_FL | 1 | 0x40 |
| S1_BLS | 1 | 0x80 |
| ZSK | 2 | 0x01 |
| GKFA | 2 | 0x02 |
| S_LH | 2 | 0x04 |
| WBL | 2 | 0x08 |
| S2_BLS | 2 | 0x10 |
| KFN | 2 | 0x20 |
| PANZTUE | 2 | 0x40 |
| BRFN | 2 | 0x80 |
| LUFTAN | 3 | 0x01 |
| LOESCHAN | 3 | 0x02 |
| VGLESP | 3 | 0x04 |
| CARB | 3 | 0x08 |
| MOTNOT | 3 | 0x10 |
| ALARM | 3 | 0x20 |
| WWN | 3 | 0x40 |
| REIF_DEF | 3 | 0x80 |
| KZL_L | 4 | 0x04 |
| BL_L | 4 | 0x08 |
| BL_R | 4 | 0x10 |
| AL_R | 4 | 0x20 |
| AL_L | 4 | 0x40 |
| SL_LV | 5 | 0x01 |
| SL_LHI | 5 | 0x02 |
| NSW_L | 5 | 0x04 |
| RFS_L | 5 | 0x08 |
| FL_L | 5 | 0x10 |
| FL_R | 5 | 0x20 |
| NSW_R | 5 | 0x40 |
| NSL_R | 5 | 0x80 |
| LWR | 6 | 0x02 |
| KZL_R | 6 | 0x04 |
| SL_LH | 6 | 0x08 |
| BL_M | 6 | 0x10 |
| SL_RV | 6 | 0x20 |
| BLK_RV | 6 | 0x40 |
| BLK_LH | 6 | 0x80 |
| BLK_RH | 7 | 0x02 |
| NSL_L | 7 | 0x04 |
| SL_RHI | 7 | 0x08 |
| SL_RH | 7 | 0x10 |
| BLK_LV | 7 | 0x40 |
| RFS_R | 7 | 0x80 |
| NOTAKTIV | 8 | 0x01 |
| KL58_EIN | 8 | 0x02 |
| WBLSUCH_EIN | 8 | 0x04 |
| LSSUCH_EIN | 8 | 0x08 |
| NSL_AH_EIN | 8 | 0x10 |
| RFS_AH_EIN | 8 | 0x20 |
| XXX | Y | Z |

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
