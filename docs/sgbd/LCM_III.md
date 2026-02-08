# LCM_III.prg

- Jobs: [30](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | LCM_III E38 / E39 / E52 / E53 |
| ORIGIN | BMW TI-430 Bendel |
| REVISION | 1.12 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-435 Drexel, BMW TI-433 Schaller |
| COMMENT | N/A |
| PACKAGE | 0.08 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [IS_LESEN](#job-is-lesen) - infospeicherlesen job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Default CODIERUNG_LESEN job
- [CODIERUNG_LESEN_ALLES](#job-codierung-lesen-alles) - Default CODIERUNG_LESEN_ALLES job
- [CODIERUNG_BLOCK_1_LESEN](#job-codierung-block-1-lesen) - Default CODIERUNG_BLOCK_1_LESEN job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [STATUS_LESEN_E52](#job-status-lesen-e52) - STATUS_LESEN_E52 job
- [STATUS_LENKSTOCKSCHALTER](#job-status-lenkstockschalter) - Default ident job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - STEUERN_SELBSTTEST job
- [STATUS_VORGEBEN](#job-status-vorgeben) - Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge
- [STATUS_VORGEBEN_E52](#job-status-vorgeben-e52) - Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreiben des Speicherinhaltes
- [STEUERN_DIMMER](#job-steuern-dimmer) - STEUERN_DIMMER job
- [STEUERN_LWR_POTI](#job-steuern-lwr-poti) - STEUERN_LWR_POTI job
- [FG_NR_LESEN](#job-fg-nr-lesen) - Default FG_NR_LESEN job
- [SIA_LESEN](#job-sia-lesen) - Default SIA_LESEN job
- [KALTABFRAGE_SCHREIBEN](#job-kaltabfrage-schreiben) - Default KALTABFRAGE_SCHREIBEN job
- [STATUS_BFD](#job-status-bfd) - Status der zusätzl. Brake-Force-Display - Lampen
- [STEUERN_BFD](#job-steuern-bfd) - Steuern der zusätzl. Brake-Force-Display - Lampen

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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
| F_ZAHL_BLOCK_11 | int | Anzahl der Fehler im Block 11 |
| F_ZAHL_BLOCK_12 | int | Anzahl der Fehler im Block 12 |

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
| COD_LICHTBEDIENEINHEIT_VERBAUT | int | 0 oder 1 |
| COD_ANALOGER_LENKSTOCKSCHALTER_VERBAUT | int | 0 oder 1 |
| COD_NSL_UND_NSW_TASTER_VERBAUT | int | 0 oder 1 |
| COD_STANDLICHT_VORNE_VERBAUT | int | 0 oder 1, invertiert! |
| COD_GEDIMMTES_BREMSLICHT_ALS_STANDLICHT_EINSCHALTEN | int | 0 oder 1 |
| COD_ACC_STEUERGERAET_VERBAUT | int | 0 oder 1 |
| COD_RUECKLICHT_INNEN_VERBAUT | int | 0 oder 1, invertiert! |
| COD_RUECKLICHT_AUSSEN_FEHLERMELDUNG_EIN | int | 0 oder 1 |
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
| COD_KEINE_KALTUEBERWACHUNG_BLK_HINTEN_EIN | int | 0 oder 1 |
| COD_KEINE_KALTUEBERWACHUNG_BLK_VORN_EIN | int | 0 oder 1 |
| COD_PERIODENDAUER_KALTUEBERWACHUNG_WERT | int | Bereich von 0 bis 71.12 Sekunden |
| COD_ENTPRELLZAHL_FEHLERERKENNUNG | int | 2-255 |
| COD_TASTVERHAELTNIS_SPANNUNG_KLEMME58g_BEI_MIN_DIMMER | int | 5-255, 2 bis 100% |
| COD_TASTVERHAELTNISZUWACHS_KLEMME58g_BEI_MAX_DIMMER | int | 32 bis 255, 12- 100 % |
| COD_MINIMALE_DIMMERSPANNUNG_WERT | real | in Volt |
| COD_DELTA_MIN_UND_MAX_DIMMERSPANNUNG_WERT | real | Differenz zwischen minimaler und maximaler Dimmerspannung in Volt |
| COD_SCHWELLE_AENDERUNG_DIMMER_AN_I_BUS | real | 1 bis 100, 255 entspricht 120 Grad drehwinkel |
| COD_EXPONENTIELLE_AUSWERTUNG_DIMMERSTELLUNG_EIN | int | hoechstes Bit |
| COD_FERNLICHT_DIMMUNG_TAG | real | 16 bis 127, 127 = 50% |
| COD_SPANNUNGSKOMPENSATION_FL_DIMMUNG_EIN | int | 0 oder 1 |
| COD_SPANNUNGSBEGRENZUNG_STANDLICHT_WERT | real |  |
| COD_SPANNUNGSBEGRENZUNG_GEDIMMTE_BREMSLICHTER_WERT | real | fuer Ersatzfunktion defektes Standlicht |
| COD_SPANNUNGSBEGRENZUNG_GEDIMMTE_BLK_VORNE_WERT | real | fuer Sidemarkerfunktion |
| COD_PERIODENDAUER_GEDIMMTE_LICHTER_WERT | real | Zeit in ms |
| COD_ERLAUBNIS_FL_UND_NSW_GLEICHZEITIG_EIN | int | 0 oder 1, invertiert |
| COD_TAGFAHRLICHT_EIN | int | 0 oder 1 |
| COD_AL_IST_TAGFAHRLICHT_EIN | int | 0 oder 1 |
| COD_GEDIMMTES_FL_IST_TAGFAHRLICHT_EIN | int | 0 oder 1 |
| COD_PARKLICHT_EINSCHALTBAR_EIN | int | 0 oder 1 |
| COD_BLK_VORN_ALS_SIDEMARKER_EIN | int | 0 oder 1 |
| COD_ALARMSCHALTER_SFZG_VERBAUT | int | 0 oder 1 |
| COD_ALARMSCHALTER_TAXI_VERBAUT | int | 0 oder 1 |
| COD_NSL_RECHTS_ANSTEUERBAR | int | 0 oder 1, invertiert! |
| COD_BL_UND_BLK_GEMEINSAM_ANSTEUERBAR | int | 0 oder 1 |
| COD_SL_VORN_HAT_ZUSATZBLINK_FUNKTION | int | 0 oder 1 |
| COD_SL_INNEN_HAT_TUERWARNLEUCHTEN_FUNKTION | int | 0 oder 1 |
| COD_E52_LINKSLENKER | int | 0 oder 1 |
| COD_E52_RECHTSLENKER | int | 0 oder 1 |
| COD_WARNBLINKER_HAT_VORRANG_VOR_BREMSLICHT | int | 0 oder 1 |
| COD_RICHTUNGSBLINKER_HAT_VORRANG_VOR_BREMSLICHT | int | 0 oder 1 |
| COD_GEDIMMTES_BL_ALS_SL_ERSATZ_EIN | int | 0 oder 1 |
| COD_BLK_VORN_ALS_AL_SL_ERSATZ_EIN | int | 0 oder 1 |
| COD_BLK_VORN_HAT_PARKLICHT_FUNKTION | int | 0 oder 1 |
| COD_BL_ALS_ERSATZFUNKTION_BEI_AHM | int | 0 oder 1 |
| COD_PIKTOGRAMMANZEIGE_WIE_E46_EIN | int | 0 oder 1 |
| COD_PIKTOGRAMM_BLINKT_BEI_DEFEKTEM_BL_EIN | int | 0 oder 1 |
| COD_BETRIEBSSTUNDENZAEHLER_WERDEN_AUTOMATISCH_GELOESCHT | int | 0 oder 1 |
| COD_DIMMUNG_BLINKER_VORN_OPTION_1 | int | 0 oder 1 |
| COD_DIMMUNG_BLINKER_VORN_OPTION_2 | int | 0 oder 1 |
| COD_DIMMUNG_BL_OPTION_1 | int | 0 oder 1 |
| COD_TAGFAHRLICHT_DAENEMARK | int | 0 oder 1 |
| COD_IMPULSLAENGE_FUER_LAMPENUEBERWACHUNG_AUS_RAM | int | 0 oder 1 |
| COD_ABFRAGEZEIT_AHM_IN_STOP_MODE | real | in ms |
| COD_FOLLOW_ME_HOME_ZEIT | int | in s |
| COD_FOLLOW_ME_HOME_MIT_AL_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_SL_HINTEN_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_SL_VORN_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_Kl58g_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_KZL_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_NSW_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_FL_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_BL_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_RFS_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_MIT_NSL_EIN | int | 0 oder 1 |
| COD_FOLLOW_ME_HOME_ABBRECHEN_MIT_LICHTSCHALTER | int | 0 oder 1 |

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
| BLOCK | int | angeforderte Blocknummer von 0 bis 18 |
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
| STAT_EINGANG_LOESCHANLAGE_EIN | int |  |
| STAT_EINGANG_VGLESP_EIN | int |  |
| STAT_EINGANG_CARB_EIN | int |  |
| STAT_KLEMME_R_EIN | int |  |
| STAT_KLEMME_30B_EIN | int |  |
| STAT_EINGANG_ZSK_EIN | int |  |
| STAT_EINGANG_GKFA_EIN | int |  |
| STAT_SCHALTER_LICHTHUPE_EIN | int |  |
| STAT_SCHALTER_WBL_EIN | int |  |
| STAT_EINGANG_KFN_EIN | int |  |
| STAT_EINGANG_PANZERTUER_EIN | int |  |
| STAT_EINGANG_BRFN_EIN | int |  |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter |
| STAT_SCHALTER_FL_EIN | int |  |
| STAT_SCHALTER_NSW_EIN | int |  |
| STAT_SCHALTER_NSL_EIN | int |  |
| STAT_SCHALTER_SL_EIN | int |  |
| STAT_SCHALTER_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER1_BLK_LINKS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_SCHALTER1_BLK_RECHTS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_SCHALTER1_SL_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_EINGANG1_BLS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_EINGANG_LUFTANLAGE_EIN | int |  |
| STAT_EINGANG_ALARM_EIN | int |  |
| STAT_EINGANG_WWN_EIN | int |  |
| STAT_SCHALTER2_AL_EIN | int |  |
| STAT_SCHALTER1_AL_EIN | int |  |
| STAT_SCHALTER_AUTO_AL_EIN | int | Schalter Automatikmodus: 0=AUS, 1=EIN, 2=nicht verbaut |
| STAT_KLEMME_15_EIN | int |  |
| STAT_EINGANG_MOTOR_NOTPROGRAMM_EIN | int |  |
| STAT_EINGANG_REIFEN_DEFEKT_EIN | int |  |
| STAT_AUSGANG_KZL_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_FL_RECHTS_EIN | int |  |
| STAT_AUSGANG_FL_LINKS_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_SL_INNEN_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSW_LINKS_EIN | int |  |
| STAT_AUSGANG_RFS_LINKS_EIN | int |  |
| STAT_AUSGANG_AL_LINKS_EIN | int |  |
| STAT_AUSGANG_AL_RECHTS_EIN | int |  |
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
| STAT_PARITY_AHM | int | odd ueber Bit 0 bis 6 von Byte 14 |
| STAT_KZL_LINKS_DEFEKT | int |  |
| STAT_BL_LINKS_DEFEKT | int |  |
| STAT_BL_RECHTS_DEFEKT | int |  |
| STAT_FL_RECHTS_DEFEKT | int |  |
| STAT_FL_LINKS_DEFEKT | int |  |
| STAT_SL_LINKS_VORN_DEFEKT | int |  |
| STAT_SL_INNEN_LINKS_HINTEN_DEFEKT | int |  |
| STAT_NSW_LINKS_DEFEKT | int |  |
| STAT_RFS_LINKS_DEFEKT | int |  |
| STAT_AL_LINKS_DEFEKT | int |  |
| STAT_AL_RECHTS_DEFEKT | int |  |
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
| STAT_EINGANGSSPANNUNG_DIMMER_EINH | string | Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_WERT | int | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_EINH | string | Volt |
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
| STAT_AL_DEFEKT_MELDUNG | string |  |
| STAT_SPANNUNG_AL_DEFEKT_WERT | real |  |
| STAT_SPANNUNG_AL_DEFEKT_EINH | string |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-lesen-e52"></a>
### STATUS_LESEN_E52

STATUS_LESEN_E52 job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLEMME_30A_EIN | int |  |
| STAT_NEON_BLK_VL_EIN | int | invertiertes Signal! |
| STAT_NEON_BLK_HL_EIN | int | invertiertes Signal! |
| STAT_NEON_BL_L_EIN | int | invertiertes Signal! |
| STAT_KLEMME_R_EIN | int |  |
| STAT_KLEMME_30B_EIN | int |  |
| STAT_EINGANG_ZSK_EIN | int |  |
| STAT_EINGANG_GKFA_EIN | int |  |
| STAT_SCHALTER_LICHTHUPE_EIN | int |  |
| STAT_SCHALTER_WBL_EIN | int |  |
| STAT_NEON_BLK_HR_EIN | int | invertiertes Signal! |
| STAT_EINGANG_PANZERTUER_EIN | int |  |
| STAT_EINGANG_BRFN_EIN | int |  |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter |
| STAT_SCHALTER_FL_EIN | int |  |
| STAT_SCHALTER_NSL_EIN | int |  |
| STAT_SCHALTER_SL_EIN | int |  |
| STAT_SCHALTER_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER1_BLK_LINKS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_SCHALTER1_BLK_RECHTS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_SCHALTER1_SL_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_EINGANG1_BLS_EIN | int | redundantes Signal wg. Rollenpruefstand |
| STAT_NEON_BLK_VR_EIN | int | invertiertes Signal! |
| STAT_EINGANG_ALARM_EIN | int |  |
| STAT_EINGANG_WWN_EIN | int |  |
| STAT_SCHALTER2_AL_EIN | int |  |
| STAT_SCHALTER1_AL_EIN | int |  |
| STAT_KLEMME_15_EIN | int |  |
| STAT_NEON_BL_R_EIN | int | invertiertes Signal! |
| STAT_EINGANG_REIFEN_DEFEKT_EIN | int |  |
| STAT_AUSGANG_KZL_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_FL_RECHTS_EIN | int |  |
| STAT_AUSGANG_FL_LINKS_EIN | int |  |
| STAT_AUSGANG_ZUSATZBLINKER_LINKS_EIN | int |  |
| STAT_AUSGANG_TUERWARNLEUCHTE_LINKS_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_SIGNAL_RFS_EIN | int |  |
| STAT_AUSGANG_AL_LINKS_EIN | int |  |
| STAT_AUSGANG_AL_RECHTS_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_LWR_EIN | int |  |
| STAT_AUSGANG_KZL_RECHTS_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int |  |
| STAT_AUSGANG_ZUSATZBLINKER_RECHTS_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSL_EIN | int |  |
| STAT_AUSGANG_TUERWARNLEUCHTE_RECHTS_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_RFS_EIN | int |  |
| STAT_NOTFUNKTION_PER_DIAGNOSE_AKTIV | int |  |
| STAT_DIMMUNG_KL58g_EIN | int |  |
| STAT_DIMMUNG_WBL_SUCHBELEUCHTUNG_EIN | int |  |
| STAT_DIMMUNG_LICHTSCHALTERBELEUCHTUNG_EIN | int |  |
| STAT_NSL_ANHAENGER_EIN | int | Nebelschlusslicht |
| STAT_RFS_ANHAENGER_EIN | int | Rueckfahrscheinwerfer |
| STAT_WARNBLINKEN_AKTIV | int |  |
| STAT_U_BATT_WERT | real | 0 bis 18 Volt |
| STAT_U_BATT_EINH | string | Volt |
| STAT_BLINKLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_BLINKLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_BREMSLICHT_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_NSL_RFS_ANHAENGER_EIN | int | Nebelschlussleuchte, Rueckfahrscheinwerfer |
| STAT_UNTERSPANNUNG_AHM_EIN | int |  |
| STAT_PARITY_AHM | int | odd ueber Bit 0 bis 6 von Byte 14 |
| STAT_BL_LINKS_DEFEKT | int |  |
| STAT_BL_RECHTS_DEFEKT | int |  |
| STAT_BLK_RECHTS_VORN_DEFEKT | int |  |
| STAT_BLK_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BLK_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_BLK_LINKS_VORN_DEFEKT | int |  |
| STAT_EINGANGSSPANNUNG_DIMMER_WERT | int | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_DIMMER_EINH | string | Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_WERT | int | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_EINH | string | Volt |
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
| STAT_FL_LH_SCHALTER_WERT | string |  |
| STAT_FL_LH_SCHALTER_POS | int | 0=aus, 1=LH, 2=FL,3=defekt |
| STAT_BLK_SCHALTER_WERT | string |  |
| STAT_BLK_SCHALTER_POS | int | 0=aus, 1=links, 2=rechts,3=defekt |
| STAT_SPANNUNG_AL_DEFEKT_WERT | real |  |
| STAT_SPANNUNG_AL_DEFEKT_EINH | string |  |
| STAT_AL_DEFEKT_MELDUNG | string |  |

<a id="job-status-lenkstockschalter"></a>
### STATUS_LENKSTOCKSCHALTER

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SPANNUNG_FL_LH_SCHALTER_WERT | real | 0 bis 5 Volt |
| STAT_SPANNUNG_BLK_SCHALTER_WERT | real | 0 bis 5 Volt |
| STAT_SPANNUNG_LWR_POTI_BEI_PU_LTG_HIGH_WERT | real | 0 bis 5 Volt |
| STAT_SPANNUNG_LWR_POTI_BEI_PU_LTG_LOW_WERT | real | 0 bis 5 Volt |
| STAT_SPANNUNG_DIMMER_POTI_BEI_PU_LTG_HIGH_WERT | real | 0 bis 5 Volt |
| STAT_SPANNUNG_DIMMER_POTI_BEI_PU_LTG_LOW_WERT | real | 0 bis 5 Volt |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Herstellerdaten Byte 1 bis 4 (oder 10?) |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

STEUERN_SELBSTTEST job

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

<a id="job-status-vorgeben-e52"></a>
### STATUS_VORGEBEN_E52

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

<a id="job-status-bfd"></a>
### STATUS_BFD

Status der zusätzl. Brake-Force-Display - Lampen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_AUSGANG_BFD_LINKS_EIN | int |  |
| STAT_AUSGANG_BFD_RECHTS_EIN | int |  |
| STAT_BFD_LINKS_DEFEKT | int |  |
| STAT_BFD_RECHTS_DEFEKT | int |  |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-steuern-bfd"></a>
### STEUERN_BFD

Steuern der zusätzl. Brake-Force-Display - Lampen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Ort der BFD-Lampe: "L" -&gt; links (left) "R" -&gt; rechts (right), "B" -&gt; beide (both) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _AUFTRAG | binary | Auftragtelegramm |
| _ANTWORT | binary | antworttelegramm |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (63 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (95 × 2)
- [IORTTEXTE](#table-iorttexte) (57 × 2)
- [STEUERN](#table-steuern) (62 × 3)
- [STEUERN_E52](#table-steuern-e52) (61 × 3)

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

Dimensions: 63 rows × 2 columns

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 95 rows × 2 columns

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
| 0x19 | BLK-Schalter / Leitung, Kurzschluss gegen Masse |
| 0x1A | FL-/LH-Schalter, Kurzschluss gegen Masse |
| 0x1B | Reserve Block 2 |
| 0x1C | Reserve Block 2 |
| 0x1D | Reserve Block 2 |
| 0x1E | Fehler am Treiberbaustein LWR |
| 0x1F | Ansteuerung Q21/Q22 LWR |
| 0x20 | Ansteuerung Q11/Q12 LWR |
| 0x21 | Reserve Block 3 |
| 0x28 | thermischer Oelsensor defekt |
| 0x29 | Reserve Block 4 |
| 0x2A | Reserve Block 4 |
| 0x32 | eine Klemme 30 fehlt |
| 0x33 | Klemme R fehlt |
| 0x34 | Klemme 15 fehlt |
| 0x35 | Reserve Block 5 |
| 0x36 | Reserve Block 5 |
| 0x3C | Reserve Block 6 |
| 0x3D | Reserve Block 6 |
| 0x3E | Reserve Block 6 |
| 0x3F | Reserve Block 6 |
| 0x40 | Reserve Block 6 |
| 0x46 | sporadischer Fehler beim Ansteuern des LWR-Treibers |
| 0x47 | Reserve Block 7 |
| 0x48 | Reserve Block 7 |
| 0x49 | Reserve Block 7 |
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
| 0x5E | Funkschluessel-Batterie |
| 0x5F | Kuehlwasser pruefen |
| 0x60 | Oelstand Motor, TOG |
| 0x61 | Reifen defekt |
| 0x62 | Reserve Block 9 |
| 0x63 | Reserve Block 9 |
| 0x64 | Reserve Block 9 |
| 0x65 | Reserve Block 9 |
| 0x66 | Reserve Block 9 |
| 0x67 | Reserve Block 9 |
| 0x68 | Reserve Block 9 |
| 0x69 | Reserve Block 9 |
| 0x6A | Reserve Block 9 |
| 0x6B | Reserve Block 9 |
| 0x6C | Reserve Block 9 |
| 0x6D | Reserve Block 9 |
| 0x6E | Reserve Block A |
| 0x78 | Abblendlicht links defekt |
| 0x79 | Abblendlicht rechts defekt |
| 0x7A | Standlicht vorne links defekt |
| 0x7B | Standlicht vorne rechts defekt |
| 0x7C | Blinker vorne links defekt |
| 0x7D | Blinker vorne rechts defekt |
| 0x7E | Nebelscheinwerfer rechts defekt |
| 0x7F | Nebelscheinwerfer links defekt |
| 0x80 | Fernlicht links defekt |
| 0x81 | Fernlicht rechts defekt |
| 0x8C | Ruecklicht links defekt |
| 0x8D | Ruecklicht rechts defekt |
| 0x8E | Ruecklicht innen links defekt |
| 0x8F | Ruecklicht innen rechts defekt |
| 0x90 | Blinker hinten links defekt |
| 0x91 | Blinker hinten rechts defekt |
| 0x92 | Bremslicht links defekt |
| 0x93 | Bremslicht rechts defekt |
| 0x94 | Nebelschlusslicht links defekt |
| 0x95 | Nebelschlusslicht rechts defekt |
| 0x96 | Rueckfahrscheinwerfer links defekt |
| 0x97 | Rueckfahrscheinwerfer rechts defekt |
| 0x98 | Bremslicht mitte defekt |
| 0x99 | Kennzeichenlicht defekt |
| 0xFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 57 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x3D | Energiesparmode aktiv |
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
| 0x5E | Funkschluessel-Batterie |
| 0x5F | Kuehlwasser pruefen |
| 0x60 | Oelstand Motor, TOG |
| 0x61 | Reifen defekt |
| 0x62 | Reserve Block 9 |
| 0x63 | Reserve Block 9 |
| 0x64 | Reserve Block 9 |
| 0x65 | Reserve Block 9 |
| 0x66 | Reserve Block 9 |
| 0x67 | Reserve Block 9 |
| 0x68 | Reserve Block 9 |
| 0x69 | Reserve Block 9 |
| 0x6A | Reserve Block 9 |
| 0x6B | Reserve Block 9 |
| 0x6C | Reserve Block 9 |
| 0x6D | Reserve Block 9 |
| 0x6E | Reserve Block A |
| 0x78 | Abblendlicht links defekt |
| 0x79 | Abblendlicht rechts defekt |
| 0x7A | Standlicht vorne links defekt |
| 0x7B | Standlicht vorne rechts defekt |
| 0x7C | Blinker vorne links defekt |
| 0x7D | Blinker vorne rechts defekt |
| 0x7E | Nebelscheinwerfer rechts defekt |
| 0x7F | Nebelscheinwerfer links defekt |
| 0x80 | Fernlicht links defekt |
| 0x81 | Fernlicht rechts defekt |
| 0x8C | Ruecklicht links defekt |
| 0x8D | Ruecklicht rechts defekt |
| 0x8E | Ruecklicht innen links defekt |
| 0x8F | Ruecklicht innen rechts defekt |
| 0x90 | Blinker hinten links defekt |
| 0x91 | Blinker hinten rechts defekt |
| 0x92 | Bremslicht links defekt |
| 0x93 | Bremslicht rechts defekt |
| 0x94 | Nebelschlusslicht links defekt |
| 0x95 | Nebelschlusslicht rechts defekt |
| 0x96 | Rueckfahrscheinwerfer links defekt |
| 0x97 | Rueckfahrscheinwerfer rechts defekt |
| 0x98 | Bremslicht mitte defekt |
| 0x99 | Kennzeichenlicht defekt |
| 0xFF | unbekannter Fehlerort |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 62 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| Kl30A | 0 | 0x01 |
| LOESCHAN | 0 | 0x02 |
| VGLESP | 0 | 0x04 |
| CARB | 0 | 0x10 |
| KlR | 0 | 0x40 |
| Kl30B | 0 | 0x80 |
| ZSK | 1 | 0x01 |
| GKFA | 1 | 0x02 |
| S_LH | 1 | 0x04 |
| WBL | 1 | 0x10 |
| KFN | 1 | 0x20 |
| PANZTUE | 1 | 0x40 |
| BRFN | 1 | 0x80 |
| S_BLS | 2 | 0x01 |
| S_FL | 2 | 0x02 |
| S_NSW | 2 | 0x04 |
| S_NSL | 2 | 0x10 |
| S_SL | 2 | 0x20 |
| S_BLK_R | 2 | 0x40 |
| S_BLK_L | 2 | 0x80 |
| LUFTAN | 3 | 0x01 |
| ALARM | 3 | 0x02 |
| WWN | 3 | 0x04 |
| S2_AL | 3 | 0x08 |
| S1_AL | 3 | 0x10 |
| Kl15 | 3 | 0x20 |
| MOTNOT | 3 | 0x40 |
| REIF_DEF | 3 | 0x80 |
| KZL_L | 4 | 0x04 |
| BL_L | 4 | 0x08 |
| BL_R | 4 | 0x10 |
| FL_R | 4 | 0x20 |
| FL_L | 4 | 0x40 |
| SL_LV | 5 | 0x01 |
| SL_LHI | 5 | 0x02 |
| NSW_L | 5 | 0x04 |
| RFS_L | 5 | 0x08 |
| AL_L | 5 | 0x10 |
| AL_R | 5 | 0x20 |
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
| SLEEPMODE | 8 | 0x40 |
| XXX | Y | Z |

<a id="table-steuern-e52"></a>
### STEUERN_E52

Dimensions: 61 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| Kl30A | 0 | 0x01 |
| NEON_BLK_VL | 0 | 0x02 |
| NEON_BLK_HL | 0 | 0x04 |
| NEON_BL_L | 0 | 0x10 |
| KlR | 0 | 0x40 |
| Kl30B | 0 | 0x80 |
| ZSK | 1 | 0x01 |
| GKFA | 1 | 0x02 |
| S_LH | 1 | 0x04 |
| WBL | 1 | 0x10 |
| NEON_BLK_RH | 1 | 0x20 |
| PANZTUE | 1 | 0x40 |
| BRFN | 1 | 0x80 |
| S_BLS | 2 | 0x01 |
| S_FL | 2 | 0x02 |
| S_NSW | 2 | 0x04 |
| S_NSL | 2 | 0x10 |
| S_SL | 2 | 0x20 |
| S_BLK_R | 2 | 0x40 |
| S_BLK_L | 2 | 0x80 |
| NEON_BLK_VR | 3 | 0x01 |
| ALARM | 3 | 0x02 |
| WWN | 3 | 0x04 |
| S2_AL | 3 | 0x08 |
| S1_AL | 3 | 0x10 |
| Kl15 | 3 | 0x20 |
| NEON_BL_R | 3 | 0x40 |
| REIF_DEF | 3 | 0x80 |
| KZL_L | 4 | 0x04 |
| BL_L | 4 | 0x08 |
| BL_R | 4 | 0x10 |
| FL_R | 4 | 0x20 |
| FL_L | 4 | 0x40 |
| Z_BLK_L | 5 | 0x01 |
| TWL_L | 5 | 0x02 |
| SL_LV | 5 | 0x04 |
| SIGNAL_RFS | 5 | 0x08 |
| AL_L | 5 | 0x10 |
| AL_R | 5 | 0x20 |
| BLK_RV | 5 | 0x40 |
| LWR | 6 | 0x02 |
| KZL_R | 6 | 0x04 |
| SL_LH | 6 | 0x08 |
| BL_M | 6 | 0x10 |
| Z_BLK_R | 6 | 0x20 |
| SL_RV | 6 | 0x40 |
| BLK_LH | 6 | 0x80 |
| BLK_RH | 7 | 0x02 |
| NSL_L | 7 | 0x04 |
| TWL_R | 7 | 0x08 |
| SL_RH | 7 | 0x10 |
| BLK_LV | 7 | 0x40 |
| RFS_R | 7 | 0x80 |
| NOTAKTIV | 8 | 0x01 |
| KL58_EIN | 8 | 0x02 |
| WBLSUCH_EIN | 8 | 0x04 |
| LSSUCH_EIN | 8 | 0x08 |
| NSL_AH_EIN | 8 | 0x10 |
| RFS_AH_EIN | 8 | 0x20 |
| SLEEPMODE | 8 | 0x40 |
| XXX | Y | Z |
