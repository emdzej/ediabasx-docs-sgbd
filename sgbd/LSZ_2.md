# LSZ_2.prg

- Jobs: [43](#jobs)
- Tables: [16](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | LSZ_2  |
| ORIGIN | BMW EI-63 Herrling (BMW-Partner) |
| REVISION | 4.000 |
| AUTHOR | BMW TI-431 Schaller, LEAR DCS Scheler, BMW TI-430 Bendel, LEAR DCS Schmidt |
| COMMENT | LSZ fuer E46 PU 09 / 2001, E85, E83 bis MÜ 09 / 2006  |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [CODIERUNG_LESEN_ALLES](#job-codierung-lesen-alles) - Default CODIERUNG_LESEN_ALLES job
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
- [XENON_VORHANDEN](#job-xenon-vorhanden) - Default XENON_VORHANDEN job
- [LWR_VORHANDEN](#job-lwr-vorhanden) - Default LWR_VORHANDEN job
- [LAENDERCODIERUNG](#job-laendercodierung) - Default CODIERUNG_BLOCK_5_LESEN job
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen Gueltiger Adressblockbereich: 0x00 - 0x0D (219 Bytes in total)
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben der red. Datenablage mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben mit Gegenverifikation Gueltiger Adressblockbereich: 0x00 - 0x11 (288 Bytes in total)
- [C_FA_LOESCHEN](#job-c-fa-loeschen) - Fahrzeugauftrag Löschen mit Gegenverifikation Gueltiger Adressblockbereich: 0x00 - 0x11 (288 Bytes in total)
- [STEUERN_BFD_LED](#job-steuern-bfd-led) - E46/2,C - Steuern des Brake-Force-Display
- [STEUERN_DYN_LWR](#job-steuern-dyn-lwr) - Fertigungsmodus schnelle Scheinwerfernachregelung
- [SLEEPINSTRUCTION_IHKA](#job-sleepinstruction-ihka) - PD-Telegramm über K-Bus vom LSZ an IHKA
- [FS_LESEN_GESAMT](#job-fs-lesen-gesamt) - fs_lesen_gesamt job

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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

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

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | siehe table LeuchtkammerStati |
| STAT_LH_1 | int | Links hinten Kammer 1 |
| STAT_LH_2 | int | Links hinten Kammer 2 |
| STAT_LH_3 | int | Links hinten Kammer 3 |
| STAT_LH_4 | int | Links hinten Kammer 4 |
| STAT_LH_5 | int | Links hinten Kammer 5 |
| STAT_LH_6 | int | Links hinten Kammer 6 |
| STAT_RH_1 | int | Rechts hinten Kammer 1 |
| STAT_RH_2 | int | Rechts hinten Kammer 2 |
| STAT_RH_3 | int | Rechts hinten Kammer 3 |
| STAT_RH_4 | int | Rechts hinten Kammer 4 |
| STAT_RH_5 | int | Rechts hinten Kammer 5 |
| STAT_RH_6 | int | Rechts hinten Kammer 6 |
| STAT_RS_1 | int | Rechts seitlich Kammer 1 |
| STAT_MH_1 | int | Mitte hinten Kammer 1 |
| STAT_MH_2 | int | Mitte hinten Kammer 2 |
| STAT_LV_1 | int | Links vorne Kammer 1 |
| STAT_LV_2 | int | Links vorne Kammer 2 |
| STAT_LV_3 | int | Links vorne Kammer 3 |
| STAT_LV_4 | int | Links vorne Kammer 4 |
| STAT_LV_5 | int | Links vorne Kammer 5 |
| STAT_LV_6 | int | Links vorne Kammer 6 |
| STAT_RV_1 | int | Rechts vorne Kammer 1 |
| STAT_RV_2 | int | Rechts vorne Kammer 2 |
| STAT_RV_3 | int | Rechts vorne Kammer 3 |
| STAT_RV_4 | int | Rechts vorne Kammer 4 |
| STAT_RV_5 | int | Rechts vorne Kammer 5 |
| STAT_RV_6 | int | Rechts vorne Kammer 6 |
| STAT_LS_1 | int | Links seitlich Kammer 1 |
| STAT_KLEMME_15_EIN | int |  |
| STAT_SCHALTER_WBL_EIN | int | Warnblinklicht |
| STAT_SCHALTER_BLS2_EIN | int | 2. Bremslichtschalter |
| STAT_SCHALTER2_AL_EIN | int | 2. Abblendlichtschalterkontakt |
| STAT_SCHALTER_SL_EIN | int | Standlicht |
| STAT_SCHALTER_AL_EIN | int | Abblendlicht |
| STAT_LICHTSCHALTER_POS_NR | int | Lichtschalterposition: 0=aus, 1=SL, 2=FLC, 3=AL |
| STAT_TASTER_NSW_EIN | int |  |
| STAT_TASTER_NSL_EIN | int | PIN 49, SL2_LINKS_HINTEN |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter |
| STAT_KLEMME_R_EIN | int |  |
| STAT_FL_LH_POS_NR | int | vercodeter Wert der FL_LH-Schalterposition, 0=aus, 1=LH, 2=FL, 3=Kurzschluss |
| STAT_SCHALTER_FL_LH_KURZSCHLUSS_MASSE_EIN | int |  |
| STAT_SCHALTER_FL_EIN | int | Fernlicht |
| STAT_SCHALTER_LH_EIN | int | Lichthupe |
| STAT_SCHALTER_FL_LH_RUHE_EIN | int |  |
| STAT_SCHALTER_FL_LH_WERT | real | (0V-1V)Kurzschluss/(1V-2,5V)Fernlicht/(2,5V-4V)Lichthupe/(4V-5V)Aus |
| STAT_SCHALTER_FL_LH_EINH | string | Volt |
| STAT_BLK_POS_NR | int | vercodeter Wert der Blinker-Schalterposition, 0=aus, 1=rechts, 2=links, 3=Kurzschluss |
| STAT_SCHALTER_BLK_KURZSCHLUSS_MASSE_EIN | int |  |
| STAT_SCHALTER_BLK_LINKS_EIN | int |  |
| STAT_SCHALTER_BLK_RECHTS_EIN | int |  |
| STAT_SCHALTER_BLK_RUHE_EIN | int |  |
| STAT_SCHALTER_BLK_WERT | real | (0V-1V)Kurzschluss/(1V-2,5V)Blk.links/(2,5V-4V)Blk.rechts/(4V-5V)Aus |
| STAT_SCHALTER_BLK_EINH | string | Volt |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | 0.0 bis 5.0 Volt |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_EINH | string | Volt |
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
| _VARIANTE | string |  |
| _VARIANTE_FZG | int | Vercodete Fzg-Variante des LSZ_2 aus Codierblock 0, Byte 30 siehe table VarianteFzg WERT INT_VARIANTE VARIANTE_FZG |
| _LAENDERVARIANTE_FZG | int | Vercodete Fzg-Laendervariante des LSZ_2 aus Codierblock 0, Byte 30 siehe table LaenderVarianteFzg WERT INT_L_VARIANTE L_VARIANTE_FZG |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! |
| STAT_AUSGANG_SL_RECHTS_VORN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_SL3_LINKS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! |
| STAT_AUSGANG_BLK_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_VORN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! |
| STAT_AUSGANG_BLINKER_ZUSATZ_RECHTS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_SL3_RECHTS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! PIN 38 |
| STAT_AUSGANG_SL2_RECHTS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! PIN37 |
| STAT_AUSGANG_AL_RECHTS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! bis Codierindex 24 (Funktionsbau) FL_RECHTS |
| STAT_AUSGANG_AL_LINKS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! bis Codierindex 24 (Funktionsbau) FL_LINKS |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_FL_LINKS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! bis Codierindex 24 (Funktionsbau) AL_LINKS |
| STAT_AUSGANG_FL_RECHTS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! bis Codierindex 24 (Funktionsbau) AL_RECHTS |
| STAT_AUSGANG_SL_LINKS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_NSW_RELAIS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_KZL_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_BLINKER_ZUSATZ_LINKS_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_SL_RECHTS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!! PIN 29 |
| STAT_AUSGANG_NSL_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_BLK_LINKS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_BIXENON | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AUSGANG_BLK_RECHTS_HINTEN_EIN | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BL_MITTE_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL_RECHTS_VORN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL3_LINKS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BL_LINKS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BL_RECHTS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_LINKS_VORN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_RECHTS_VORN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL3_RECHTS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AL_RECHTS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_AL_LINKS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL_LINKS_VORN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_FL_LINKS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_FL_RECHTS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL_LINKS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL2_RECHTS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_ZUSATZ_LINKS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_KZL_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_ZUSATZ_RECHTS_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_SL_RECHTS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_NSL_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_LINKS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |
| STAT_BLK_RECHTS_HINTEN_DEFEKT | int | LSZ-RESULT NICHT MEHR GÜLTIG FÜR LSZ-2 !!!  |

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
| ORT1 | string | gewuenschte Komponente 1 moeglich sind bis  zu 15 Argumente, Liste: 'KLR' = Klemme R aktivieren (Radio-Stellung) 'Kl15' = Klemme 15 aktivieren (Zuendung ein) 'KL58_EIN' = Klemme 58 ein (Suchbeleuchtung) 'NOTAKTIV' = Notfunktion aktivieren 'WBLSUCH_EIN' = Suchbeleuchtung am Warnblinkschalter aktivieren 'LSSUCH_EIN' = Suchbeleuchtung am Lenkstockschalter aktivieren 'SLEEP_MODE' = Steruergeraet in Sleepmode versetzen 'START_PRUEF' = Start des Selbsttestmodes 'QUICK_NACHF' = schnelle Scheinwerfernachfuehrung (nur SW2.0, CI29) 'S_WBL' = Schalter Warnblinklicht 'S2_BLS' = 2.Bremslichtschalter 'S2_AL' = 2.Schalter Abblendlicht 'S_SL' = Schalter Standlicht 'S_AL' = Schalter Abblendlicht 'T_NSW' = Taster Nebelscheinwerfer 'T_NSL' = Taster Nebelschlusslicht 'S_BLS' = Bremslichtschalter 'S_FL' = Schalter Fernlicht 'S_LH' = Schalter Lichthupe, 'S_F_AUS' = Schalter Fernlicht aus 'S_BLK_L' = Schalter Blinker links 'S_BLK_R' = Schalter Blinker rechts 'S_BLK_AUS' = Schalter Blinker aus 'BL_M' = Ausgang Bremslicht mitte 'SL_RV' = Ausg. Positionsl. vorn (E85US: Sidemarker hinten, E83US: AHM Blink-Bremslicht) rechts 'SL2_LH' = Ausgang Schlusslicht 3 (E85: Blinker 2 vorn) links 'BL_L' = Ausgang Bremslicht (E46/5&gt;09/01: Schlusslicht) links 'BL_R' = Ausgang Bremslicht (E46/5&gt;09/01: Schlusslicht) rechts 'BLK_LV' = Ausgang Blinker links vorn (schaltet Dauerlicht) 'BLK_RV' = Ausgang Blinker rechts vorn (schaltet Dauerlicht) 'BLK_ZU_R' = Ausgang seitl. Blinker rechts (schaltet Dauerlicht) 'SL2_RH' = Ausgang Schlusslicht 3 rechts 'AL_R' = Ausgang Abblendlicht rechts 'AL_L' = Ausgang Abblendlicht links 'SL_LV' = Ausg. Positionsl. vorn (E85US: Sidemarker hinten, E83US: AHM Blink-Bremsl.) links 'FL_L' = Ausgang Fernlicht links 'FL_R' = Ausgang Fernlicht rechts 'SL_LH' = Ausgang Schlusslicht 1 (E46/5&gt;09/01: Bremslicht) links 'SL1_RH' = Ausgang Schlusslicht 2 (E85: Blinker 2 vorn) rechts 'REL_NSW' = Relais Nebelscheinwerfer 'KZL' = Kennzeichenbeleuchtung 'BLK_ZU_L' = Ausgang seitl. Blinker links (schaltet Dauerlicht) 'SL_RH' = Ausgang Schlusslicht 1 (E46/5&gt;09/01: Bremslicht) rechts 'NSL' = Ausgang Nebelschlusslicht (E46/4&gt;09/01: Schlusslicht 2 links) 'BLK_LH' = Ausgang Blinker links hinten (schaltet Dauerlicht) 'BIXENON' = Ausgang BiXenonklappe 'BLK_RH' = Ausgang Blinker rechts hinten (schaltet Dauerlicht) 'NSL_AH_EIN' = Nebelschlusslicht am Anhaenger einschalten Argumente koennen sich gegenseitig over-rulen Rueckkehr in den normalen Betriebszustand mit Job 'DIAGNOSE_ENDE' |
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

<a id="job-xenon-vorhanden"></a>
### XENON_VORHANDEN

Default XENON_VORHANDEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| XENON | string | Xenonlicht |

<a id="job-lwr-vorhanden"></a>
### LWR_VORHANDEN

Default LWR_VORHANDEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LWR | string | Leuchtweitenregulierung |

<a id="job-laendercodierung"></a>
### LAENDERCODIERUNG

Default CODIERUNG_BLOCK_5_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _FZG_LAENDERVARIANTE | string | codierte Laendervariante |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen Gueltiger Adressblockbereich: 0x00 - 0x0D (219 Bytes in total)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben der red. Datenablage mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben mit Gegenverifikation Gueltiger Adressblockbereich: 0x00 - 0x11 (288 Bytes in total)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fa-loeschen"></a>
### C_FA_LOESCHEN

Fahrzeugauftrag Löschen mit Gegenverifikation Gueltiger Adressblockbereich: 0x00 - 0x11 (288 Bytes in total)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-bfd-led"></a>
### STEUERN_BFD_LED

E46/2,C - Steuern des Brake-Force-Display

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Ort der BFD-Lampen: "L" -&gt; links (left) "R" -&gt; rechts (right) "B" -&gt; beide (both) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _AUFTRAG | binary | Auftragtelegramm |
| _ANTWORT | binary | antworttelegramm |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-dyn-lwr"></a>
### STEUERN_DYN_LWR

Fertigungsmodus schnelle Scheinwerfernachregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GERAETE_VARIANTE | string | Name der Variante |
| _VARIANTE_FZG | string | Vercodete Fzg-Variante des LSZ_2 aus Codierblock 0, Byte 30 siehe table VarianteFzg WERT INT_VARIANTE VARIANTE_FZG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-sleepinstruction-ihka"></a>
### SLEEPINSTRUCTION_IHKA

PD-Telegramm über K-Bus vom LSZ an IHKA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IHKA_SOFTWARE_VERSION | string | Softwareversion der IHKA |
| PATCH_INSTALL | string | gibt an, ob der Patch im LSZ installiert ist |
| PATCH_ACTIVATION | string | gibt an, ob der Patch aktiviert ist |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-fs-lesen-gesamt"></a>
### FS_LESEN_GESAMT

fs_lesen_gesamt job

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
| F_ZAHL_BLOCK_1 | int | Anzahl der Fehler im Block 1 |
| F_ZAHL_BLOCK_2 | int | Anzahl der Fehler im Block 2 |
| F_ZAHL_BLOCK_3 | int | Anzahl der Fehler im Block 3 |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |
| F_ZAHL_BLOCK_5 | int | Anzahl der Fehler im Block 5 |
| F_ZAHL_BLOCK_6 | int | Anzahl der Fehler im Block 6 |
| F_ZAHL_BLOCK_7 | int | Anzahl der Fehler im Block 7 |
| F_ZAHL_BLOCK_8 | int | Anzahl der Fehler im Block 8 |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (65 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (49 × 3)
- [LEUCHTKAMMERSTATI](#table-leuchtkammerstati) (27 × 3)
- [VARIANTEFZG](#table-variantefzg) (9 × 3)
- [LAENDERVARIANTEFZG](#table-laendervariantefzg) (3 × 3)

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

Dimensions: 77 rows × 2 columns

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
| 0x18 | Continental Teves |
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
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
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

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 65 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0A | RAM-Fehler des Mikro-Prozessors |
| 0x0B | ROM-Fehler des Mikro-Prozessors |
| 0x0C | EEPROM-Fehler des Mikro-Prozessors |
| 0x0D | Diagnose-Leitung U12/2 defekt |
| 0x0E | Diagnose-Leitung U12/1 defekt |
| 0x0F | Diagnose-Leitung U11/2 defekt |
| 0x10 | Kl. 30 A fehlerhaft |
| 0x11 | Kl. 30 B fehlerhaft |
| 0x12 | Diagnose-Leitung U11/1 defekt |
| 0x13 | Diagnose-Leitung U10 defekt |
| 0x14 | Leitung Bremslichtschalter, Unterbrechung |
| 0x15 | Leitung Bremslichtschalter, Kurzschluss gegen Masse |
| 0x16 | Leitung / Schalter Blinker, Kurzschluss gegen Masse |
| 0x17 | Leitung / Schalter Fernlicht/Lichthupe, Kurzschluss gegen Masse |
| 0x18 | Verbindung zum AHM ist gestoert |
| 0x19 | Abblendlichtschalter- Eingaenge widerspruechlich |
| 0x1A | Reserve Block 2 |
| 0x1B | Reserve Block 2 |
| 0x1E | Steuergeraetefehler im LWR-Teil |
| 0x1F | Spulen Schrittmotoren defekt |
| 0x20 | Reserve Block 3 |
| 0x21 | LWR, vorderer Beladungssensor Unterbrechung |
| 0x22 | LWR, vorderer Beladungssensor Kurzschluss nach Masse |
| 0x23 | LWR, hinterer Beladungssensor Unterbrechung |
| 0x24 | LWR, hinterer Beladungssensor Kurzschluss nach Masse |
| 0x25 | Reserve Block 3 |
| 0x28 | Klemme R fehlt |
| 0x29 | Klemme 15 fehlt |
| 0x2A | LWR-Poti defekt |
| 0x2B | Dimmer-Poti defekt |
| 0x2C | Reserve Block 4 |
| 0x2D | Reserve Block 4 |
| 0x2E | Reserve Block 4 |
| 0x2F | Reserve Block 4 |
| 0x32 | Bremslicht Mitte defekt |
| 0x33 | Positionslicht rechts vorn defekt |
| 0x34 | Bremslicht (E46/5 &gt; 09/01: Schlusslicht) links defekt |
| 0x35 | Bremslicht (E46/5 &gt; 09/01: Schlusslicht) rechts defekt |
| 0x36 | Blinker links vorn defekt |
| 0x37 | Blinker rechts vorn defekt |
| 0x38 | Positionslicht links vorn defekt |
| 0x39 | Fernlicht  (E85 &gt; 01/06: Positionslicht vorn) links defekt |
| 0x3A | Fernlicht  (E85 &gt; 01/06: Positionslicht vorn) rechts defekt |
| 0x3B | Schlusslicht (E46/5 &gt; 09/01: Bremslicht) links defekt |
| 0x3C | Kennzeichenlicht defekt |
| 0x3D | Schlusslicht (E46/5 &gt; 09/01: Bremslicht) rechts defekt |
| 0x3E | Nebelschlusslicht (E46/4 &gt; 09/01: Schlusslicht 2 links,  E85US &gt; 01/06: zweistufiges Bremslicht links) defekt |
| 0x3F | Blinker links hinten defekt |
| 0x40 | Blinker rechts hinten defekt |
| 0x41 | Abblendlicht rechts defekt |
| 0x42 | Abblendlicht links defekt |
| 0x43 | Zusatzblinker links defekt |
| 0x44 | Zusatzblinker rechts defekt |
| 0x45 | Schlusslicht 2 (E85: Blinker vorn) rechts defekt |
| 0x46 | Schlusslicht 3 (E85: Blinker vorn) links defekt |
| 0x47 | Schlusslicht 3 (E85 &gt; 01/06: zweistufiges Bremslicht) rechts defekt |
| 0x48 | ein Scheinwerfer nicht aktiviert wegen Blendgefahr durch Kurvenlicht |
| 0x49 | Reserve Block 7 |
| 0x4A | Anhaenger, Blinker links defekt |
| 0x4B | Anhaenger, Blinker rechts defekt |
| 0x4C | Reserve Block 7 |
| 0x4D | Reserve Block 7 |
| 0x50 | sporadischer Fehler bei Ansteuerung LWR-Treiber |
| 0x51 | FWT-Mode |
| 0xFF | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

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

Dimensions: 49 rows × 3 columns

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
| SL2_LH | 4 | 0x04 |
| BL_L | 4 | 0x08 |
| BL_R | 4 | 0x10 |
| BLK_LV | 4 | 0x20 |
| BLK_RV | 4 | 0x40 |
| BLK_ZU_R | 4 | 0x80 |
| SL2_RH | 5 | 0x01 |
| AL_R | 5 | 0x02 |
| AL_L | 5 | 0x04 |
| SL_LV | 5 | 0x08 |
| FL_L | 5 | 0x10 |
| FL_R | 5 | 0x20 |
| SL_LH | 5 | 0x40 |
| SL1_RH | 5 | 0x80 |
| REL_NSW | 6 | 0x01 |
| KZL | 6 | 0x02 |
| BLK_ZU_L | 6 | 0x04 |
| SL_RH | 6 | 0x08 |
| NSL | 6 | 0x10 |
| BLK_LH | 6 | 0x20 |
| BIXENON | 6 | 0x40 |
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

<a id="table-leuchtkammerstati"></a>
### LEUCHTKAMMERSTATI

Dimensions: 27 rows × 3 columns

| STATUS | ABKUERZUNG | BEDEUTUNG |
| --- | --- | --- |
| 0 | AUS | AUS |
| 1 | SL | Stand-/Schlusslicht |
| 2 | BL | Bremslicht |
| 3 | FRA | Fahrtrichtungsanzeiger |
| 4 | NSL | Nebelschlusslicht |
| 5 | RFSW | Rückfahrscheinwerfer |
| 6 | BL+SL | Bremslicht+Stand-/Schlusslicht |
| 7 | FRA+BL | Fahrtrichtungsanzeiger+Bremslicht |
| 8 | FRA+SL | Fahrtrichtungsanzeiger+Stand-/Schlusslicht |
| 9 | FRA+BL+SL | Fahrtrichtungsanzeiger+Bremslicht+Stand-/Schlusslicht |
| 10 | NSL+SL | Nebelschlusslicht+Stand-/Schlusslicht |
| 11 | SM_US | Sidemarker US |
| 12 | AL | Abblendlicht |
| 13 | AL+BiX | Abblendlicht+BiXenon-Fernlicht |
| 14 | FL | Halogen-Fernlicht |
| 15 | LH | Lichthupe |
| 16 | DRL_US | Daytime-Running-Light US |
| 17 | NSW | Nebelscheinwerfer |
| 18 | SM_US+FRA | Sidemarker US+Fahrtrichtungsanzeiger |
| 19 | KZL | Kennzeichenlicht |
| 20 | SL+BFD | Schlusslicht+BrakeForceDisplay |
| 21 | BFD | BrakeForceDisplay |
| 22 | NSL+BFD | Nebelschlusslicht+BrakeForceDisplay |
| 90 | uncodiert | Uncodiert bzw. Auslieferungszustand |
| 95 | unbenutzt | Leuchtkammer ohne LSZ-Funktion |
| 99 | defekt | defekt |
| 0xXY | unbekannt | unbekannter Leuchtkammerstatus |

<a id="table-variantefzg"></a>
### VARIANTEFZG

Dimensions: 9 rows × 3 columns

| WERT | INT_VARIANTE | VARIANTE_FZG |
| --- | --- | --- |
| 0x00 | 0 | nicht kodiert bzw. Auslieferzustand |
| 0x01 | 1 | E46/4 &gt; PU 09.01 |
| 0x02 | 2 | E46/2,3,C + (E46/4 + !PU 09.01) |
| 0x03 | 3 | E46/5 + !PU 09.01 |
| 0x04 | 4 | E46/5 &gt; PU 09.01 |
| 0x05 | 5 | E85 |
| 0x06 | 6 | E83 |
| 0x07 | 7 | E85 &gt;PU 01/06 |
| 0xXY | 255 | unbekannte Fahrzeug-Variante |

<a id="table-laendervariantefzg"></a>
### LAENDERVARIANTEFZG

Dimensions: 3 rows × 3 columns

| WERT | INT_L_VARIANTE | L_VARIANTE_FZG |
| --- | --- | --- |
| 0x00 | 1 | ECE |
| 0x01 | 2 | US |
| 0xXY | 255 | unbekannte Fahrzeug-Laendervariante |
