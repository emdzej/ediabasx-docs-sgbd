# LME38.prg

- Jobs: [20](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Lichtmodul E38 |
| ORIGIN | BMW, TP-422, Teepe |
| REVISION | 1.99 |
| AUTHOR | BMW, TP-422, Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Default ident job
- [FG_NR_LESEN](#job-fg-nr-lesen) - Default FG_NR_LESEN job
- [KALTABFRAGE_SCHREIBEN](#job-kaltabfrage-schreiben) - Default KALTABFRAGE_SCHREIBEN job
- [SIA_LESEN](#job-sia-lesen) - Default SIA_LESEN job
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Default CODIERUNG_LESEN job
- [CODIERUNG_LESEN_ALLES](#job-codierung-lesen-alles) - Default CODIERUNG_LESEN_ALLES job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs
- [STEUERN_MEHRERE](#job-steuern-mehrere) - Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge
- [STEUERN_DIMMER](#job-steuern-dimmer) - STEUERN_DIMMER job
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreiben des Speicherinhaltes
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - DIAGNOSE_WEITER job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - DIAGNOSE_ENDE job

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

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

<a id="job-fg-nr-lesen"></a>
### FG_NR_LESEN

Default FG_NR_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| FG_NR | string | Fahrgestellnummer 7-stellig |

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

<a id="job-sia-lesen"></a>
### SIA_LESEN

Default SIA_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| GESAMTWEGSTRECKE_WERT | string | Zaehlerstand Gesamtwgstrecke (nur 100er Einheiten!) |
| GESAMTWEGSTRECKE_EINH | string | 100 km |
| SI_WEGZAEHLER_EINH | string | SI-km |
| SI_WEGZAEHLER_WERT | string |  |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_WERT | string | SI-Wegstrecke beim letzten Oelservice |
| SI_WEGSTRECKE_LETZTER_OELSERVICE_EINH | string | SI-km |
| SI_ZEITINSPEKTIONSZAEHLER_WERT | string |  |
| SI_ZEITINSPEKTIONSZAEHLER_EINH | string | Tage |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |

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
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

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
| JOB_STATUS | string |  |
| COD_STANDLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_ABBLENDLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_FERNLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_NEBELSCHEINWERFER_FEHLERMELDUNG_EIN | int |  |
| COD_RUECKLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_RUECKFAHRSCHEINWERFER_FEHLERMELDUNG_EIN | int |  |
| COD_NSL_LINKS_FEHLERMELDUNG_EIN | int |  |
| COD_NSL_RECHTS_FEHLERMELDUNG_EIN | int |  |
| COD_KEINE_BREMSLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_BREMSLICHT_MITTE_FEHLERMELDUNG_EIN | int |  |
| COD_KENNZEICHENLICHT_FEHLERMELDUNG_EIN | int |  |
| COD_ANHAENGER_FEHLERMELDUNG_EIN | int |  |
| COD_BLS_FEHLERMELDUNG_EIN | int |  |
| COD_WARNBLINKEN_ENABLE | int |  |
| COD_WERT_ABSCHALTUNG_STAND_PARKLICHT | int |  |
| COD_GASENTLADUNG_IN_ABBLENDLICHT_KREIS_EIN | int |  |
| COD_GASENTLADUNG_IN_NSW_KREIS_EIN | int |  |
| COD_GASENTLADUNG_IN_FERNLICHT_KREIS_EIN | int |  |
| COD_PERIODENDAUER_KALTUEBERWACHUNG_WERT | int | Bereich von 0 bis 166 Sekunden |
| COD_PERIODENDAUER_KALTUEBERWACHUNG_EINH | string | s |
| COD_ENTPRELLZAHL_FEHLERERKENNUNG | int |  |
| COD_MINIMALE_SPANNUNG_KLEMME58g | int |  |
| COD_SPANNUNGSHUB_AN_KLEMME58g | int |  |
| COD_VERHAELTNIS_HELLIGKEIT_WBL_DIMMER | int |  |
| COD_ABFRAGEZEIT_AHM_IN_STOP_MODE | int |  |
| COD_SCHWELLE_AENDERUNG_DIMMER_AN_I_BUS | int |  |
| COD_FERNLICHT_DIMMUNG_TAG | int |  |
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
| BLOCK | int | angeforderte Blocknummer |
| CODIERDATEN | binary | CODIERDATENFELD |

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SCHALTER_BLINKLICHT_LINKS_EIN | int |  |
| STAT_SCHALTER_BLINKLICHT_RECHTS_EIN | int |  |
| STAT_SCHALTER_ABBLENDLICHT_EIN | int |  |
| STAT_SCHALTER_STANDLICHT_EIN | int |  |
| STAT_SCHALTER_RES_M1_EIN | int |  |
| STAT_SCHALTER_WARNBLINKLICHT_EIN | int |  |
| STAT_SCHALTER_FERNLICHT_EIN | int |  |
| STAT_SCHALTER_LICHTHUPE_EIN | int |  |
| STAT_SCHALTER_BREMSLICHT_EIN | int |  |
| STAT_SCHALTER_NEBELSCHEINWERFER_EIN | int |  |
| STAT_SCHALTER_NEBELSCHLUSSLICHT_EIN | int |  |
| STAT_SCHALTER_RES_M2_EIN | int |  |
| STAT_KLEMME15_EIN | int |  |
| STAT_KLEMME30B_EIN | int |  |
| STAT_KLEMME30A_EIN | int |  |
| STAT_SCHALTER_RES_P3_EIN | int |  |
| STAT_AUSGANG_AL_LINKS_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_SL_INNEN_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_KZL_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_VORN_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_BLK_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_BLK_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_LWR_EIN | int |  |
| STAT_AUSGANG_SL_INNEN_RECHTS_HINTEN_EIN | int |  |
| STAT_AUSGANG_SL_LINKS_HINTEN_EIN | int |  |
| STAT_AUSGANG_SL_RECHTS_VORN_EIN | int |  |
| STAT_AUSGANG_AL_RECHTS_EIN | int |  |
| STAT_AUSGANG_FERNLICHT_LINKS_EIN | int |  |
| STAT_AUSGANG_FERNLICHT_RECHTS_EIN | int |  |
| STAT_AUSGANG_NSW_LINKS_EIN | int |  |
| STAT_AUSGANG_NSW_RECHTS_EIN | int |  |
| STAT_AUSGANG_NSL_LINKS_EIN | int |  |
| STAT_AUSGANG_NSL_RECHTS_EIN | int |  |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int |  |
| STAT_AUSGANG_RFS_EIN | int |  |
| STAT_DIMMUNG_KL58g_EIN | int |  |
| STAT_DIMMUNG_WBL_SUCHBELEUCHTUNG_EIN | int |  |
| STAT_AHM_KOMMUNIKATION_ANSTOSS_EIN | int |  |
| STAT_NSL_ANHAENGER_EIN | int | Nebelschlusslicht |
| STAT_RFS_ANHAENGER_EIN | int | Rueckfahrscheinwerfer |
| STAT_U_BATT_WERT | int |  |
| STAT_U_BATT_EINH | string |  |
| STAT_SPANNUNG_NOTBETRIEB_WERT | int |  |
| STAT_SPANNUNG_NOTBETRIEB_EINH | string |  |
| STAT_BLINKLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_BLINKLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_BREMSLICHT_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_LINKS_ANHAENGER_EIN | int |  |
| STAT_STANDLICHT_RECHTS_ANHAENGER_EIN | int |  |
| STAT_NSL_RFS_ANHAENGER_EIN | int | Nebelschlussleuchte, Rueckfahrscheinwerfer |
| STAT_UNTERSPANNUNG_AHM_EIN | int |  |
| STAT_PARITY_AHM | int | even ueber Bit 0 bis 6 von Byte 12 |
| STAT_NOTFUNKTION_PER_DIAGNOSE_AKTIV | int |  |
| STAT_DWA_ALARM_AKTIV | int |  |
| STAT_AL_LINKS_DEFEKT | int |  |
| STAT_SL_LINKS_VORN_DEFEKT | int |  |
| STAT_SL_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_SL_INNEN_LINKS_HINTEN_DEFEKT | int |  |
| STAT_KZL_DEFEKT | int |  |
| STAT_BLK_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_BLK_LINKS_VORN_DEFEKT | int |  |
| STAT_BREMSLICHT_LINKS_DEFEKT | int |  |
| STAT_BREMSLICHT_RECHTS_DEFEKT | int |  |
| STAT_BLK_LINKS_HINTEN_DEFEKT | int |  |
| STAT_BLK_RECHTS_VORN_DEFEKT | int |  |
| STAT_LWR_DEFEKT | int |  |
| STAT_SL_INNEN_RECHTS_HINTEN_DEFEKT | int |  |
| STAT_SL_LINKS_HINTEN_DEFEKT | int |  |
| STAT_SL_RECHTS_VORN_DEFEKT | int |  |
| STAT_AL_RECHTS_DEFEKT | int |  |
| STAT_FERNLICHT_LINKS_DEFEKT | int |  |
| STAT_FERNLICHT_RECHTS_DEFEKT | int |  |
| STAT_NSW_LINKS_DEFEKT | int |  |
| STAT_NSW_RECHTS_DEFEKT | int |  |
| STAT_NSL_LINKS_DEFEKT | int |  |
| STAT_NSL_RECHTS_DEFEKT | int |  |
| STAT_BREMSLICHT_MITTE_DEFEKT | int |  |
| STAT_RFS_DEFEKT | int |  |
| STAT_KLEMME58g_DEFEKT | int |  |
| STAT_EINGANGSSPANNUNG_DIMMER_WERT | int |  |
| STAT_EINGANGSSPANNUNG_DIMMER_EINH | string | Volt |
| STAT_NOTEINGANG_BLINKER_LINKS_EIN | int |  |
| STAT_NOTEINGANG_BLINKER_RECHTS_EIN | int |  |
| STAT_NOTEINGANG_ABBLENDLICHT_EIN | int |  |
| STAT_NOTEINGANG_STANDLICHT_EIN | int |  |
| STAT_NOTEINGANG_BREMSLICHT_EIN | int |  |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Herstellerdaten Byte 1 bis 4 (oder 10?) |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-mehrere"></a>
### STEUERN_MEHRERE

Ansteuern mehrerer (maximal 15) digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZAHL | int | gewuenschte Anzahl Komponenten (maximal 15) |
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

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (9 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [STEUERN](#table-steuern) (46 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Bremslichtschalter defekt |
| 0x01 | Leitung Dimmerpoti, Unterbrechung |
| 0x02 | Klemme 15 |
| 0x03 | Klemme 30, A oder B fehlt |
| 0x04 | Kommunikation Anhaengermodul unterbrochen |
| 0x05 | LM-interner Datenbus defekt |
| 0x06 | LM-interne Schalterabfrageschaltung defekt |
| 0x07 | LM-interne Versorgungsspannung fehlerhaft |
| 0xFF | unbekannte Fehlerart |

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

Dimensions: 46 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| S_BLK_L | 0 | 0x01 |
| S_BLK_R | 0 | 0x02 |
| S_AL | 0 | 0x04 |
| S_SL | 0 | 0x08 |
| S_RES_M1 | 0 | 0x10 |
| S_WBL | 0 | 0x20 |
| S_FL | 0 | 0x40 |
| S_LH | 0 | 0x80 |
| S_BL | 1 | 0x01 |
| S_NSW | 1 | 0x02 |
| S_NSL | 1 | 0x04 |
| S_RES_M2 | 1 | 0x08 |
| KLEMME15 | 1 | 0x10 |
| KLEMME30B | 1 | 0x20 |
| KLEMME30A | 1 | 0x40 |
| S_RES_P3 | 1 | 0x80 |
| AL_L | 2 | 0x01 |
| SL_L_V | 2 | 0x02 |
| SL_R_H | 2 | 0x04 |
| SL_I_L | 2 | 0x08 |
| KZL | 2 | 0x10 |
| BLK_R_V | 2 | 0x20 |
| BLK_L_H | 2 | 0x40 |
| BL_L | 2 | 0x80 |
| BL_R | 3 | 0x01 |
| BLK_L_V | 3 | 0x02 |
| BLK_R_H | 3 | 0x04 |
| LWR | 3 | 0x08 |
| SL_I_R | 3 | 0x10 |
| SL_L_H | 3 | 0x20 |
| SL_R_V | 3 | 0x40 |
| AL_R | 3 | 0x80 |
| FL_L | 4 | 0x01 |
| FL_R | 4 | 0x02 |
| NSW_L | 4 | 0x04 |
| NSW_R | 4 | 0x08 |
| NSL_L | 4 | 0x10 |
| NSL_R | 4 | 0x20 |
| BL_M | 4 | 0x40 |
| RFS | 4 | 0x80 |
| KL_58g_EIN | 5 | 0x01 |
| WBL_SUCH | 5 | 0x02 |
| AHM_KOM | 5 | 0x04 |
| NSL_A | 5 | 0x08 |
| RFS_A | 5 | 0x10 |
| NOT_AKTIV | 6 | 0x02 |

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
