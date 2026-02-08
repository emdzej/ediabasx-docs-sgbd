# LSZ.prg

- Jobs: [30](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Lichtschaltzentrum E46 |
| ORIGIN | BMW TI-430 Bendel |
| REVISION | 1.25 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-433 Drexel, BMW TI-433 Schaller |
| COMMENT | LSZ E46 |
| PACKAGE | 0.09 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Default CODIERUNG_LESEN job
- [CODIERUNG_LESEN_ALLES](#job-codierung-lesen-alles) - Default CODIERUNG_LESEN_ALLES job
- [CODIERUNG_BLOCK_1_LESEN](#job-codierung-block-1-lesen) - Default CODIERUNG_BLOCK_1_LESEN job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - DIAGNOSE_WEITER job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - DIAGNOSE_ENDE job
- [STEUERN_IO](#job-steuern-io) - Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreiben des Speicherinhaltes
- [STEUERN_DIMMER](#job-steuern-dimmer) - STEUERN_DIMMER job
- [STEUERN_LWR_POTI](#job-steuern-lwr-poti) - STEUERN_LWR_POTI job
- [STEUERN_SCHALTERSPANNUNG_FL_LH](#job-steuern-schalterspannung-fl-lh) - STEUERN_SCHALTERSPANNUNG_FL_LH job
- [STEUERN_SCHALTERSPANNUNG_BLINKER](#job-steuern-schalterspannung-blinker) - STEUERN_SCHALTERSPANNUNG_BLINKER job
- [STEUERN_FOTOZELLE](#job-steuern-fotozelle) - STEUERN_FOTOZELLE job
- [STEUERN_BELADUNGSSENSOR_VORN](#job-steuern-beladungssensor-vorn) - STEUERN_BELADUNGSSENSOR_VORN job
- [FG_NR_LESEN](#job-fg-nr-lesen) - Default FG_NR_LESEN job
- [SIA_LESEN](#job-sia-lesen) - Default SIA_LESEN job
- [BETRIEBSSTUNDENZAEHLER_LESEN](#job-betriebsstundenzaehler-lesen) - Default BETRIEBSSTUNDENZAEHLER_LESEN job
- [BETRIEBSSTUNDENZAEHLER_LOESCHEN](#job-betriebsstundenzaehler-loeschen) - Default BETRIEBSSTUNDENZAEHLER_LOESCHEN job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Default pruefstempel_setzen job
- [POWER_DOWN](#job-power-down) - Default POWER_DOWN

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

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int | Anzahl gespeicherter Fehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ALL_BLOCKS | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string | Fehlerort |
| F_ORT_NR | int | Nummer des Fehler |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 1 |
| F_ART1_NR | int | Fehlerartnummer |
| F_ART1_TEXT | string | Fehlerarttext |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_1 | int | Anzahl der Fehler im Block 1 |
| F_ZAHL_BLOCK_2 | int | Anzahl der Fehler im Block 2 |
| F_ZAHL_BLOCK_3 | int | Anzahl der Fehler im Block 3 |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |
| F_ZAHL_BLOCK_5 | int | Anzahl der Fehler im Block 5 |
| F_ZAHL_BLOCK_6 | int | Anzahl der Fehler im Block 6 |
| F_ZAHL_BLOCK_7 | int | Anzahl der Fehler im Block 7 |
| F_ZAHL_BLOCK_8 | int | Anzahl der Fehler im Block 8 |
| F_ZAHL | int | Anzahl der Gesamtfehler der Bloecke 1 bis 3 (schwere Fehler) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-lesen"></a>
### IS_LESEN

is_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 1 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |
| F_ZAHL_BLOCK_5 | int | Anzahl der Fehler im Block 5 |
| F_ZAHL_BLOCK_6 | int | Anzahl der Fehler im Block 6 |
| F_ZAHL_BLOCK_7 | int | Anzahl der Fehler im Block 7 |
| F_ZAHL_BLOCK_8 | int | Anzahl der Fehler im Block 8 |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Default CODIERUNG_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| COD_BL_LI_RE_KALTUEBERWACHUNG_EIN | int | 0 oder 1, Kaltueberwachung fuer Bremslicht |
| COD_SL_VORN_KALTUEBERWACHUNG_EIN | int | 0 oder 1 Kaltueberwachung fuer Standlicht vorne |
| COD_SL_HINTEN_KALTUEBERWACHUNG_EIN | int | 0 oder 1 Kaltueberwachung fuer standlicht hinten |
| COD_KZL_KALTUEBERWACHUNG_EIN | int | 0 oder 1 Kaltueberwachung fuer Kennzeichenlicht |
| COD_NSL_KALTUEBERWACHUNG_EIN | int | 0 oder 1 Kaltueberwachung fuer Nebelschlusslicht |
| COD_SL_HINTEN_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Standlicht hinten |
| COD_SL_VORN_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Standlicht vorn |
| COD_AL_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Abblendlicht |
| COD_FL_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Fernlicht |
| COD_BSZ_LOESCHUNG_BEI_LAMPENWECHSEL_EIN | int | 0 oder 1 Betriebsstundenzaehlerloeschung bei Lampenwechsel |
| COD_NSL_L_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Nebelschlusslicht links |
| COD_NSL_R_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Nebelschlusslicht rechts |
| COD_BL_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Bremslicht |
| COD_BL_MITTE_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Bremslicht mitte |
| COD_KZL_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Kennzeichenlicht |
| COD_ZYKLUSZEIT_STATUSTELEGRAMM_WIE_E38_E39_EIN | int | 0 oder 1 Zykluszeit wie E38/E39 |
| COD_ANHAENGERLICHT_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Anhaengerlicht |
| COD_GEDIMMTE_BLINKER_FUER_STANDLICHT_EIN | int | 0 oder 1 Ersatzfunktion bedimmte Blinker bei Standlichtausfall |
| COD_BLS2_ABFRAGE_EIN | int | 0 oder 1, 2. Bremslichtschalter wird abgefragt |
| COD_BLS_FEHLERMELDUNG_EIN | int | 0 oder 1 Fehlermeldung fuer Bremslichtschalter |
| COD_BLS_B_SCHWELL_WERT | int | Schwellwert in km/h/s |
| COD_T_WARTE_FEHLER_BLS_WERT | int | Wartezeit bis Meldung Bremslichtschalter kommt [s] |
| COD_WERT_ABSCHALTUNG_STAND_PARKLICHT | real | Spannung [Volt] bei der Stand/Parklicht abschaltet |
| COD_WARNBLINKEN_ENABLE | int | 0 oder 1 |
| COD_AL_KALTUEBERWACHUNG_EIN | int | 0 oder 1 |
| COD_FL_KALTUEBERWACHUNG_EIN | int | 0 oder 1 |
| COD_BLK_HINTEN_KALTUEBERWACHUNG_EIN | int | 0 oder 1 |
| COD_BLK_VORN_KALTUEBERWACHUNG_EIN | int | 0 oder 1 |
| COD_PERIODENDAUER_KALTUEBERWACHUNG_WERT | int | Bereich von 0 bis 71.12 Sekunden |
| COD_ENTPRELLZAHL_FEHLERERKENNUNG | int | 4-255 |
| COD_TASTVERHAELTNIS_SPANNUNG_KLEMME58g_BEI_MIN_DIMMER | real | 5-255, 2 bis 100% |
| COD_TASTVERHAELTNISZUWACHS_KLEMME58g_BEI_MAX_DIMMER | real | 32 bis 255, 12- 100 % |
| COD_ABFRAGEZEIT_AHM_IN_LOW_POWER_MODE | real | in ms |
| COD_SCHWELLE_AENDERUNG_DIMMER_AN_K_BUS | real | 1 bis 100, 255 entspricht 120 Grad drehwinkel |
| COD_DAUER_FOLLOW_ME_HOME_SCHALTUNG | int | 0 bis 255 sec |
| COD_EINSCHALTZEIT_GEDIMMTE_BLK_VORN | real | 0 bis 255 |
| COD_EINSCHALTZEIT_GEDIMMTES_BREMSLICHT | real | 0 bis 255 |
| COD_PERIODENDAUER_DIMMUNG_BLK_BL | real | 0 bis 255 |
| COD_EINSCHALTZEIT_GEDIMMTES_AL | real | 0 bis 255 |
| COD_PERIODENDAUER_DIMMUNG_AL | real | 0 bis 255 |
| COD_MINIMALE_AUSTASTZEIT_FUER_SL | real | 0 bis 255 |
| _ANTWORT | binary | Antwort-Telegramm |
| COD_LWR_AUTOMATISCH_CODIERT | int | 0 oder 1 |

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
| BLOCK | int | angeforderte Blocknummer von 0 bis 16 |
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
| STAT_KLEMME_15_EIN | int |  |
| STAT_SCHALTER_WBL_EIN | int | Warnblinklicht |
| STAT_SCHALTER_BLS2_EIN | int | 2. Bremslichtschalter |
| STAT_SCHALTER2_AL_EIN | int | 2. Abblendlichtschalterkontakt |
| STAT_SCHALTER_SL_EIN | int | Standlicht |
| STAT_SCHALTER_AL_EIN | int | Abblendlicht |
| STAT_LICHTSCHALTER_POS_NR | int | vercodeter Wert der Lichtschalterposition, 0=aus, 1=SL, 2=AL, 3=SL+AL |
| STAT_TASTER_NSW_EIN | int |  |
| STAT_TASTER_NSL_EIN | int |  |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter |
| STAT_KLEMME_R_EIN | int |  |
| STAT_FL_LH_POS_NR | int | vercodeter Wert der FL_LH-Schalterposition, 0=aus, 1=LH, 2=FL, 3=Kurzschluss |
| STAT_SCHALTER_FL_LH_KURZSCHLUSS_MASSE_EIN | int |  |
| STAT_SCHALTER_FL_EIN | int |  |
| STAT_SCHALTER_LH_EIN | int | Lichthupe |
| STAT_SCHALTER_FL_LH_RUHE_EIN | int |  |
| STAT_SCHALTER_FL_LH_WERT | real |  |
| STAT_SCHALTER_FL_LH_EINH | string | Volt |
| STAT_BLK_POS_NR | int | vercodeter Wert der Blinker-Schalterposition, 0=aus, 1=rechts, 2=links, 3=Kurzschluss |
| STAT_SCHALTER_BLK_KURZSCHLUSS_MASSE_EIN | int |  |
| STAT_SCHALTER_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER_BLK_RUHE_EIN | int |  |
| STAT_SCHALTER_BLK_WERT | real |  |
| STAT_SCHALTER_BLK_EINH | string | Volt |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_LWR_EIN | int | Leuchtweitenregulierung |
| STAT_AUSGANG_AL_RECHTS_EIN | int | bis Codierindex 24 (Funktionsbau) FL_RECHTS |
| STAT_AUSGANG_AL_LINKS_EIN | int | bis Codierindex 24 (Funktionsbau) FL_LINKS |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_FL_LINKS_EIN | int | bis Codierindex 24 (Funktionsbau) AL_LINKS |
| STAT_AUSGANG_FL_RECHTS_EIN | int | bis Codierindex 24 (Funktionsbau) AL_RECHTS |
| STAT_AUSGANG_SL_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSW_RELAIS_EIN | int |  |
| STAT_AUSGANG_KZL_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_NSL_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_HINTEN_EIN | int |  |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | 0.0 bis 5.0 Volt |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_EINH | string |  |
| STAT_NOTFUNKTION_PER_DIAGNOSE_AKTIV | int |  |
| STAT_DIMMUNG_KL58g_EIN | int |  |
| STAT_DIMMUNG_WBL_SUCHBELEUCHTUNG_EIN | int |  |
| STAT_DIMMUNG_LICHTSCHALTERBELEUCHTUNG_EIN | int |  |
| STAT_NSL_ANHAENGER_EIN | int | Nebelschlusslicht |
| STAT_WARNBLINKEN_AKTIV | int |  |
| STAT_U_BATT_WERT | real | 0 bis 18 Volt |
| STAT_U_BATT_EINH | string | Volt |
| STAT_BLINKLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_BLINKLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_BREMSLICHT_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_NSL_RFS_ANHAENGER_EIN | int | Nebelschlussleuchte, Rueckfahrscheinwerfer |
| STAT_PARITY_AHM | int | odd ueber Bit 0 bis 6 von Byte 14 |
| STAT_BL_MITTE_DEFEKT | int |  |
| STAT_SL_RECHTS_VORN_DEFEKT | int |  |
| STAT_BL_LINKS_DEFEKT | int |  |
| STAT_BL_RECHTS_DEFEKT | int |  |
| STAT_BLK_LINKS_VORN_DEFEKT | int |  |
| STAT_BLK_RECHTS_VORN_DEFEKT | int |  |
| STAT_AL_RECHTS_DEFEKT | int |  |
| STAT_AL_LINKS_DEFEKT | int |  |
| STAT_SL_LINKS_VORN_DEFEKT | int |  |
| STAT_FL_LINKS_DEFEKT | int |  |
| STAT_FL_RECHTS_DEFEKT | int |  |
| STAT_SL_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BLK_ZUSATZ_LINKS_DEFEKT | int |  |
| STAT_KZL_DEFEKT | int |  |
| STAT_BLK_ZUSATZ_RECHTS_DEFEKT | int |  |
| STAT_SL_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_NSL_DEFEKT | int |  |
| STAT_BLK_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BLK_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_EINGANGSSPANNUNG_DIMMER_WERT | real | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_DIMMER_EINH | string | Volt |
| STAT_EINGANGSSPANNUNG_LWR_POTI_WERT | real | 0 bis 5 Volt, bei Xenon-Licht hinterer Beladungssensor |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | 0.0 bis 5.0 Volt = LWR_POTI |
| STAT_EINGANGSSPANNUNG_LWR_POTI_EINH | string | Volt |
| STAT_CRASH_WARNBLINKEN_AKTIV | int |  |
| STAT_DWA_WARNBLINKEN_AKTIV | int |  |
| STAT_DWA_AL_BLINKEN_AKTIV | int |  |
| STAT_DWA_FL_BLINKEN_AKTIV | int |  |
| STAT_CRASHSENSOR_AKTIV | int |  |
| STAT_DWA_AUSGELOEST | int |  |
| STAT_EINGANGSSPANNUNG_FOTOZELLE_WERT | real | 0 bis 5 Volt |
| STAT_EINGANGSSPANNUNG_FOTOZELLE_EINH | string | 0 bis 5 Volt |
| STAT_TEST_SCHALTER_SL_EIN | int |  |
| STAT_TEST_SCHALTER_AL_EIN | int |  |
| STAT_TEST_TASTER_NSW_EIN | int |  |
| STAT_TEST_TASTER_NSL_EIN | int |  |
| STAT_TEST_DIMMER_POTI_EIN | int |  |
| STAT_TEST_LWR_POTI_EIN | int |  |
| STAT_TEST_SCHALTER_FL_EIN | int |  |
| STAT_TEST_SCHALTER_LH_EIN | int |  |
| STAT_TEST_SCHALTER_BLK_LINKS_EIN | int |  |
| STAT_TEST_SCHALTER_BLK_RECHTS_EIN | int |  |
| STAT_TEST_EINGANG_BLS_EIN | int | Bremslichtschalter |
| STAT_TEST_SCHALTER_WBL_EIN | int |  |
| _ANTWORT | binary | antworttelegramm |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ICT_TEILENUMMER_PLATINE | int | Teilnummer der Hauptleiterplatine |
| ICT_SERIENNUMMER_PLATINE | long | Seriennummer der Hauptleiterplatine |
| ICT_INDEX | int | ICT-Seriennummer Gehaeuse-Index |
| GERAETE_VARIANTE | string | Name der Variante |
| GERAETE_VARIANTE_NR | int | Nummer der Variante |
| GEH_SERIENNUMMER_KOMPLETTBAUGRUPPE | long |  |
| GEH_INDEXNUMMER | int |  |
| HERSTELLERDATEN_STRING | string | Herstellerdaten Byte 1 bis 10 |

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

<a id="job-steuern-io"></a>
### STEUERN_IO

Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente 1 moeglich sind bis  zu 15 Argumente, Liste: 'KLR' = Klemme R aktivieren (Radio-Stellung) 'Kl15' = Klemme 15 aktivieren (Zuendung ein) 'KL58_EIN' = Klemme 58 ein (Suchbeleuchtung) 'NOTAKTIV' = Notfunktion aktivieren 'WBLSUCH_EIN' = Suchbeleuchtung am Warnblinkschalter aktivieren 'LSSUCH_EIN' = Suchbeleuchtung am Lenkstockschalter aktivieren 'SLEEP_MODE' = Steruergeraet in Sleepmode versetzen 'START_PRUEF' = Start des Selbsttestmodes 'QUICK_NACHF' = schnelle Scheinwerfernachfuehrung (nur SW2.0, CI29) 'S_WBL' = Schalter Warnblinklicht 'S2_BLS' = 2.Bremslichtschalter 'S2_AL' = 2.Schalter Abblendlicht 'S_SL' = Schalter Standlicht 'S_AL' = Schalter Abblendlicht 'T_NSW' = Taster Nebelscheinwerfer 'T_NSL' = Taster Nebelschlusslicht 'S_BLS' = Bremslichtschalter 'S_FL' = Schalter Fernlicht 'S_LH' = Schalter Lichthupe, 'S_F_AUS' = Schalter Fernlicht aus 'S_BLK_L' = Schalter Blinker links 'S_BLK_R' = Schalter Blinker rechts 'S_BLK_AUS' = Schalter Blinker aus 'BL_M' = Ausgang Bremslicht mitte 'SL_RV' = Ausgang Standlicht rechts vorn 'BL_L' = Ausgang Bremslicht links 'BL_R' = Ausgang Bremslicht rechts 'BLK_LV' = Ausgang Blinker links vorn 'BLK_RV' = Ausgang Blinker rechts vorn 'LWR' = Ausgang Leuchtweitenregulierung 'AL_R' = Ausgang Abblendlicht rechts 'AL_L' = Ausgang Abblendlicht links 'SL_LV' = Ausgang Standlicht links vorn 'FL_L' = Ausgang Fernlicht links 'FL_R' = Ausgang Fernlicht rechts 'SL_LH' = Ausgang Standlicht links hinten 'REL_NSW' = Relais Nebelscheinwerfer 'KZL' = Kennzeichenbeleuchtung, 'SL_RH' = Ausgang Standlicht rechts hinten 'NSL' = Ausgang Nebelschlusslicht 'BLK_LH' = Ausgang Blinker links hinten (schaltet Dauerlicht) 'BLK_RH' = Ausgang Blinker rechts hinten (schaltet Dauerlicht) 'NSL_AH_EIN' = Nebelschlusslicht am Anhaenger einschalten Argumente koennen sich gegenseitig over-rulen Rueckkehr in den normalen Betriebszustand mit Job 'DIAGNOSE_ENDE' |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 moegliche Argumente: |
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
| DIMMWERT | int | gewuenschter Spannungswert in Volt |

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
| POTI_WERT | int | gewuenschter Wert in Volt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-schalterspannung-fl-lh"></a>
### STEUERN_SCHALTERSPANNUNG_FL_LH

STEUERN_SCHALTERSPANNUNG_FL_LH job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | gewuenschter Wert in [Volt] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-schalterspannung-blinker"></a>
### STEUERN_SCHALTERSPANNUNG_BLINKER

STEUERN_SCHALTERSPANNUNG_BLINKER job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | gewuenschter Wert in [Volt] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-fotozelle"></a>
### STEUERN_FOTOZELLE

STEUERN_FOTOZELLE job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FOTO_WERT | int | gewuenschter Wert in Volt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-beladungssensor-vorn"></a>
### STEUERN_BELADUNGSSENSOR_VORN

STEUERN_BELADUNGSSENSOR_VORN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | gewuenschter Wert in [Volt] |

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
| GESAMTWEGSTRECKE_WERT | long | Zaehlerstand Gesamtwegstrecke (nur 100er Einheiten!) |
| GESAMTWEGSTRECKE_EINH | string | 100 km |
| SI_WEGZAEHLER_EINH | string | SI-km |
| SI_WEGZAEHLER_WERT | string |  |
| SI_LITERZAEHLER_WERT | long |  |
| SI_LETZTER_SERVICE_WAR_OELSERVICE | int |  |
| SI_LETZTER_SERVICE_WAR_INSPEKTION | int |  |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_WERT | string | SI-Wegstrecke beim letzten Oelservice |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_EINH | string | SI-km |
| SI_ZEITINSPEKTIONSZAEHLER_WERT | long |  |
| SI_ZEITINSPEKTIONSZAEHLER_EINH | string | Tage |

<a id="job-betriebsstundenzaehler-lesen"></a>
### BETRIEBSSTUNDENZAEHLER_LESEN

Default BETRIEBSSTUNDENZAEHLER_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BETRIEBSZEIT_LSZ_WERT | long | Gesamtbetriebszeit des LSZ [h] |
| BETRIEBSZEIT_AL_LINKS_WERT | long | Gesamtbetriebszeit des Abblendlichts links [h] |
| BETRIEBSZEIT_AL_RECHTS_WERT | long | Gesamtbetriebszeit des Abblendlichts rechts [h] |
| BETRIEBSZEIT_BL_L_WERT | long | Gesamtbetriebszeit des Bremslichts links [h] |
| BETRIEBSZEIT_BL_R_WERT | long | Gesamtbetriebszeit des Bremslichts rechts [h] |
| BETRIEBSZEIT_SL_LH_WERT | long | Gesamtbetriebszeit des Standlichts links hinten [h] |
| BETRIEBSZEIT_SL_RH_WERT | long | Gesamtbetriebszeit des Standlichts rechts hinten [h] |
| BETRIEBSZEIT_BLK_L_WERT | long | Gesamtbetriebszeit des Blinkers links [h] |
| BETRIEBSZEIT_BLK_R_WERT | long | Gesamtbetriebszeit des Blinkers rechts [h] |
| BETRIEBSZEIT_NSL_WERT | long | Gesamtbetriebszeit des Nebelschlusslichts [h] |
| BETRIEBSZEIT_NSW_RELAIS_WERT | long | Gesamtbetriebszeit des Nebelscheinwerferrelais [h] |
| BETRIEBSZEIT_EINH | string | Stunden [h] |
| ANZAHL_BETAETIGUNGEN_BLS_WERT | long | Anzahl Betaetigungen des Bremslichtschalters, wird in 100er Einheiten gespeichert! |

<a id="job-betriebsstundenzaehler-loeschen"></a>
### BETRIEBSSTUNDENZAEHLER_LOESCHEN

Default BETRIEBSSTUNDENZAEHLER_LOESCHEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZAEHLER | int | 0x01 bis 0x0b zum loeschen einzelner Zaehler 0xFF zum loeschen aller Zaehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BYTE1 | int |  |
| BYTE2 | int |  |
| BYTE3 | int |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Default pruefstempel_setzen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0x00 bis 0xFF |
| BYTE2 | int | 0x00 bis 0xFF |
| BYTE3 | int | 0x00 bis 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-power-down"></a>
### POWER_DOWN

Default POWER_DOWN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (63 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (65 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (43 × 3)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 65 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0A | RAM-Fehler des Mikro-Prozessors |
| 0x0B | ROM-Fehler des Mikro-Prozessors |
| 0x0C | EEPROM-Fehler des Mikro-Prozessors |
| 0x0D | PowerMOS-Statusleitung 2 staendig aktiv |
| 0x0E | PowerMOS-Statusleitung 3 staendig aktiv |
| 0x0F | PowerMOS-Statusleitung 4 staendig aktiv |
| 0x10 | PowerMOS-Statusleitung 5 staendig aktiv |
| 0x11 | Reserve Block 1 |
| 0x12 | Reserve Block 1 |
| 0x13 | Reserve Block 1 |
| 0x14 | Leitung Bremslichtschalter, Unterbrechung |
| 0x15 | Leitung Bremslichtschalter, Kurzschluss gegen Masse |
| 0x16 | Leitung / Schalter Blinker, Kurzschluss gegen Masse |
| 0x17 | Leitung / Schalter Fernlicht/Lichthupe, Kurzschluss gegen Masse |
| 0x18 | Verbindung zum AHM ist gestoert |
| 0x19 | Reserve Block 2 |
| 0x1A | Reserve Block 2 |
| 0x1B | Reserve Block 2 |
| 0x1E | Steuergeraetefehler im LWR-Teil |
| 0x1F | Ansteuerung Motor fuer LWR 1 |
| 0x20 | Ansteuerung Motor fuer LWR 2 |
| 0x21 | LWR, vorderer Beladungssensor Unterbrechung |
| 0x22 | LWR, vorderer Beladungssensor Kurzschluss nach Masse |
| 0x23 | LWR, hinterer Beladungssensor Unterbrechung |
| 0x24 | LWR, hinterer Beladungssensor Kurzschluss nach Masse |
| 0x25 | Reserve Block 3 |
| 0x28 | Klemme R fehlt |
| 0x29 | Klemme 15 fehlt |
| 0x2A | Reserve Block 4 |
| 0x2B | Reserve Block 4 |
| 0x2C | Reserve Block 4 |
| 0x2D | Reserve Block 4 |
| 0x2E | Reserve Block 4 |
| 0x2F | Reserve Block 4 |
| 0x32 | Bremslicht mitte defekt |
| 0x33 | Standlicht rechts vorn defekt |
| 0x34 | Bremslicht links defekt |
| 0x35 | Bremslicht rechts defekt |
| 0x36 | Blinker links vorn defekt |
| 0x37 | Blinker rechts vorn defekt |
| 0x38 | Standlicht links vorn defekt |
| 0x39 | Fernlicht links defekt |
| 0x3A | Fernlicht rechts defekt |
| 0x3B | Standlicht links hinten defekt |
| 0x3C | Kennzeichenlicht defekt |
| 0x3D | Standlicht rechts hinten defekt |
| 0x3E | Nebelschlusslicht defekt |
| 0x3F | Blinker links hinten defekt |
| 0x40 | Blinker rechts hinten defekt |
| 0x41 | Abblendlicht rechts defekt |
| 0x42 | Abblendlicht links defekt |
| 0x43 | Zusatzblinker links defekt |
| 0x44 | Zusatzblinker rechts defekt |
| 0x45 | Fehlercode reserviert |
| 0x46 | Fehlercode reserviert |
| 0x47 | Fehlercode reserviert |
| 0x48 | Fehlercode reserviert |
| 0x49 | Fehlercode reserviert |
| 0x4A | Anhaenger, Blinker links defekt |
| 0x4B | Anhaenger, Blinker rechts defekt |
| 0x4C | Reserve Block 7 |
| 0x4D | Reserve Block 7 |
| 0x50 | sporadischer Fehler bei Ansteuerung LWR-Treiber |
| 0x51 | Reserve Block 8 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 43 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| Kl15 | 0 | 0x10 |
| S_WBL | 0 | 0x20 |
| S2_BLS | 0 | 0x40 |
| S2_AL | 0 | 0x80 |
| S_SL | 1 | 0x01 |
| S_AL | 1 | 0x02 |
| T_NSW | 1 | 0x04 |
| T_NSL | 1 | 0x08 |
| S_BLS | 1 | 0x10 |
| KLR | 1 | 0x40 |
| S_FL | 2 | 0x50 |
| S_LH | 2 | 0x80 |
| S_F_AUS | 2 | 0xFF |
| S_BLK_L | 3 | 0x50 |
| S_BLK_R | 3 | 0x80 |
| S_BLK_AUS | 3 | 0xFF |
| BL_M | 4 | 0x01 |
| SL_RV | 4 | 0x02 |
| BL_L | 4 | 0x08 |
| BL_R | 4 | 0x10 |
| BLK_LV | 4 | 0x20 |
| BLK_RV | 4 | 0x40 |
| AL_R | 5 | 0x02 |
| AL_L | 5 | 0x04 |
| SL_LV | 5 | 0x08 |
| FL_L | 5 | 0x10 |
| FL_R | 5 | 0x20 |
| SL_LH | 5 | 0x40 |
| REL_NSW | 6 | 0x01 |
| KZL | 6 | 0x02 |
| SL_RH | 6 | 0x08 |
| NSL | 6 | 0x10 |
| BLK_LH | 6 | 0x20 |
| BLK_RH | 6 | 0x80 |
| NOTAKTIV | 8 | 0x01 |
| KL58_EIN | 8 | 0x02 |
| WBLSUCH_EIN | 8 | 0x04 |
| LSSUCH_EIN | 8 | 0x08 |
| NSL_AH_EIN | 8 | 0x10 |
| SLEEP_MODE | 8 | 0x20 |
| START_PRUEF | 8 | 0x40 |
| QUICK_NACHF | 8 | 0x80 |
| XXX | Y | Z |
