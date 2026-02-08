# NAVMK4_2.prg

- Jobs: [41](#jobs)
- Tables: [15](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Navigationsrechner MK3 / Roadrunner |
| ORIGIN | BMW EI-44 Bernd Biechele |
| REVISION | 2.000 |
| AUTHOR | BMW EI-44 Biechele |
| COMMENT | NAVMK4_2 fuer Diagnoseindex 06 |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Navigationsrechner
- [STATUS_LESEN](#job-status-lesen)
- [IDENT](#job-ident) - Ident-Daten fuer Navigationsrechner
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding
- [IS_LESEN](#job-is-lesen) - Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen, welche Software geladen ist
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben)
- [SPEICHER_LOESCHEN](#job-speicher-loeschen) - Sprachen loeschen
- [READ_CODING_DATA](#job-read-coding-data) - Auslesen der Codierdaten
- [WRITE_CODING_DATA](#job-write-coding-data) - Schreiben der configuration data
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Selbsttest Navigationsrechner
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen im Navigationsrechner
- [QUICK_ERASE](#job-quick-erase) - Fehlerspeicher loeschen ohne BUSY abzuwarten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [SYSTEM_PARAMETER_LESEN](#job-system-parameter-lesen)
- [SW_DEMAND_FLAG_SETZEN](#job-sw-demand-flag-setzen) - Herstellen des Auslieferzustandes
- [WRITE_CONFIGURATION_DATA](#job-write-configuration-data) - Schreiben der configuration data
- [READ_CONFIGURATION_DATA](#job-read-configuration-data) - Auslesen der configuration data
- [READ_PRODUCTION_STAMP_RECORD](#job-read-production-stamp-record) - Production stamp record lesen
- [WRITE_PRODUCTION_STAMP_RECORD](#job-write-production-stamp-record) - Schreiben der configuration data
- [READ_PRODUCTION_STAMP_TABLE](#job-read-production-stamp-table) - Production stamp table lesen
- [READ_PRODUCTION_STAMP_TABLE_QUICK_INFO](#job-read-production-stamp-table-quick-info) - Production stamp table lesen
- [SET_NO_SAVE_NVR](#job-set-no-save-nvr) - Speicherungs Verbot
- [REMOVE_NO_SAVE_NVR](#job-remove-no-save-nvr) - Speicherungs Freigabe
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben ohne Verifikation
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [STATUS_GPS_ANTENNA](#job-status-gps-antenna)
- [SPRACHAUSGABE](#job-sprachausgabe) - Sprachausgabe Navigationsrechner
- [FORCE_EJECT](#job-force-eject) - Freigabe der Eject Taste
- [SCHREIBEN_NAVDVDPIN](#job-schreiben-navdvdpin) - Freigabecode zum Eject
- [NAVDVDPIN_LESEN](#job-navdvdpin-lesen) - Auslesen der 4 Stellen des CD eject Freigabecodes
- [STEUERN_FLOTTENMODUS](#job-steuern-flottenmodus) - Flottenmodus Status
- [STATUS_FLOTTENMODUS](#job-status-flottenmodus) - Auslesen des Stati des Flottenmodus

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-status-lesen"></a>
### STATUS_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise A0 (Acknolage) |
| STAT_RADSENSOR | string | Bereich -1...3 |
| STAT_RADSENSOR_LINKS_WERT | int | Impulse pro Sekunde |
| STAT_RADSENSOR_RECHTS_WERT | int | Impulse pro Sekunde |
| STAT_RADSENSOR_EINH | string | Impulse/sec |
| STAT_GYRO | string | Bereich -1...3 |
| STAT_GYRO_WERT | int | Bereich 0...65535 |
| STAT_GYRO_EINH | string | Spannung in mV |
| STAT_5V | string | Bereich -1...3 |
| STAT_5V_WERT | int | 5V Stromversorgang digitale Schaltkreise Bereich 0...65535 |
| STAT_5V_EINH | string | Spannung in mV |
| STAT_12V | string | Bereich -1...3 |
| STAT_12V_WERT | int | Stromversorgung Batterie Bereich 0...6535 |
| STAT_12V_EINH | string | Spannung in mV |
| STAT_SPANNUNG_SENSOR | string | Bereich -1...3 |
| STAT_SPANNUNG_SENSOR_WERT | int | Spannungsversorgung Sensor Bereich 0...65535 |
| STAT_SPANNUNG_SENSOR_EINH | string | Spannung in mV |
| STAT_LUEFTER | string | Status-Abfrage Luefter,-1...3 |
| STAT_LUEFTER_WERT | int | Abfrage, ob Luefter eingeschaltet ist 0=Aus,1=Ein |
| STAT_LUEFTER_TEXT | string | Abfrage, ob Luefter eingeschaltet ist 0=Aus,1=Ein |
| STAT_CD_AUSWURFTASTE | string | Status -1...3 |
| STAT_CD_AUSWURFTASTE_WERT | int | Status-Abfrage, 0= nicht gedrueckt Status-Abfrage, 1= gedrueckt |
| STAT_CD_AUSWURFTASTE_TEXT | string | Status-Abfrage, 0= nicht gedrueckt Status-Abfrage, 1= gedrueckt |
| STAT_TEMPERATUR | string | Status -1...3 |
| STAT_SYSTEM_TEMPERATUR_WERT | int | Bereich -32768...32767 |
| STAT_SYSTEM_TEMPERATUR_EINH | string | Temperatur in Grad Celsius |
| STAT_GANGWAHL | string | Status -1...3 |
| STAT_GANGWAHL_WERT | int | Status 0= Vor, 1= Rueckwaerts |
| STAT_GANGWAHL_TEXT | string | Status 0= Vor, 1= Rueckwaerts |
| STAT_GPS | string | Status -1...3 |
| STAT_GPS_TEXT | string | Texte aus Spezifikation |
| STAT_GPS_WERT | int | Werte aus Spezifikation, 0x00-0x0C |
| _TEL_ANTWORT | binary |  |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY", aber hier zuerst "BUSY" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | string | BMW-Einkaufsnummer, Lieferant und Zielort enthalten |
| ID_LIEF_TEXT | string | Lieferant im Klartext |
| ID_SW_NR | int | Softwarenummer |
| ID_VARIANTE | string | Varianten Nav-Rechner: NAVMK4, NAVMK4? |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZAHL_GESAMT | int | Ausgabe der Fehleranzahl gesamt |
| F_ORT_NR | int | Fehlerortausgabe als Zahl |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Ausgabe der Fehlerarten als Zahl |
| F_ART1_NR | int | Index Fehlerart, 00 = nicht aktiv, hx40 = aktiv |
| _TEL_ANTWORT | binary | Antworttelegramm des Steuergeraetes |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-is-lesen"></a>
### IS_LESEN

Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZAHL_GESAMT | int | Ausgabe der Fehleranzahl gesamt |
| F_ORT_NR | int | Fehlerortausgabe als Zahl |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Ausgabe der Fehlerarten als Zahl |
| F_ART1_NR | int | Index Fehlerart, 00 = nicht aktiv, hx40 = aktiv |
| _TEL_ANTWORT | binary | Antworttelegramm des Steuergeraetes |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

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
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |
| _TEL_ANZAHL | int | Anzahl der Telegramme anzeigen |

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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen, welche Software geladen ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_SW_LADEN_WERT | int | Statusmeldung Software laden |
| STAT_SW_LADEN_TEXT | string | Text Status Software laden |
| SPRACHEN_MODIFIZIERT_CODE | binary | Ausgabecode der modifizierten Sprachen |
| SPRACHE_1_MOD_TEXT | string | 1.Sprache der Sprachmodifizierung |
| SPRACHE_2_MOD_TEXT | string | 2.Sprache der Sprachmodifizierung |
| SPRACHE_3_MOD_TEXT | string | 3.Sprache der Sprachmodifizierung |
| SPRACHEN_AKTUELL_CODE | binary | Ausgabecode der aktuellen Sprachen |
| SPRACHE_1_AKTUELL_TEXT | string | 1. geladene Sprache |
| SPRACHE_2_AKTUELL_TEXT | string | 2. geladene Sprache |
| SPRACHE_3_AKTUELL_TEXT | string | 3. geladene Sprache |
| _TEL_ANTWORT | binary |  |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPRACHE_1 | int | Sprache 1 der Sprachauswahl |
| SPRACHE_2 | int | Sprache 2 der Sprachauswahl |
| SPRACHE_3 | int | Sprache 3 der Sprachauswahl |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| SPRACHAUSWAHL_1 | string | Sprache 1 der Sprachauswahl |
| SPRACHAUSWAHL_2 | string | Sprache 2 der Sprachauswahl |
| SPRACHAUSWAHL_3 | string | Sprache 3 der Sprachauswahl |
| _TEL_SENDE | binary | Sendetelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-speicher-loeschen"></a>
### SPEICHER_LOESCHEN

Sprachen loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normal OKAY |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-read-coding-data"></a>
### READ_CODING_DATA

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_LAENDERVARIANTE_TEXT | string | Laendervariante ECE, US_CDN, AUS |
| COD_LAENDERVARIANTE_WERT | int | Wert des Bytes Laendervariante 0-2 |
| COD_SPEED_MAPS_WERT | int | Wert des Bytes SPEED_MAPS, derzeit unbenutzt |
| COD_SPEED_ROUTE_WERT | int | Wert des Bytes ROUTE_MAPS, derzeit unbenutzt |
| COD_USER_INPUT_WERT | int | Wert des Bytes USER_INPUT, derzeit unbenutzt |
| COD_VIN_WERT | int | Wert des Bytes VIN |
| COD_CAR_TYPE_TEXT | string | CAR_TYPE High Nibble = "Baureihe", Low Nibble = "Bauart" |
| COD_NOT_RUF | string | Wert des Bytes AUTO_EM_CALL, Telematik und automatischer Notruf |
| _TEL_ANTWORT | binary | Wert des Bytes _TEL_ANTWORT |

<a id="job-write-coding-data"></a>
### WRITE_CODING_DATA

Schreiben der configuration data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_LAENDERVARIANTE_WERT | string | Wert des Bytes Laendervariante 0-2 |
| COD_SPEED_MAPS_WERT | string | Wert des Bytes SPEED_MAPS, derzeit unbenutzt |
| COD_SPEED_ROUTE_WERT | string | Wert des Bytes ROUTE_MAPS, derzeit unbenutzt |
| COD_USER_INPUT_WERT | string | Wert des Bytes USER_INPUT, derzeit unbenutzt |
| COD_VIN_WERT | string | Vin Wert = 7 Byte lang |
| COD_CAR_TYPE_WERT | string | Wert des Bytes CAR_TYPE |
| COD_NOT_RUF | string | Wert des Bytes COD_NOT_RUF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | binary | OKAY, ERROR_.. |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary | Wert des Bytes _TEL_ANTWORT |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Selbsttest Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen im Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-quick-erase"></a>
### QUICK_ERASE

Fehlerspeicher loeschen ohne BUSY abzuwarten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. OKAY) |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-system-parameter-lesen"></a>
### SYSTEM_PARAMETER_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| _TEL_ANTWORT | binary |  |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-sw-demand-flag-setzen"></a>
### SW_DEMAND_FLAG_SETZEN

Herstellen des Auslieferzustandes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-write-configuration-data"></a>
### WRITE_CONFIGURATION_DATA

Schreiben der configuration data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KONFIG_CUSTOMER | string | Customer, z.B. BMW |
| KONFIG_SWDISPLAYTYPE | string | SW/Display type, z.B. C01 oder M01 |
| KONFIG_NAVIGATIONS_MODE | string | Navigation mode, z.B. S |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-read-configuration-data"></a>
### READ_CONFIGURATION_DATA

Auslesen der configuration data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| KONFIG_CUSTOMER | string | Customer im Klartext |
| KONFIG_SWDISPLAYTYPE | string | SW/Display type im Klartext |
| KONFIG_NAVIGATIONS_MODE | string | Navigation mode im Klartext |
| RESERVIERT | int | Return Value wird im Moment nicht gebraucht |
| _TEL_ANTWORT | binary |  |
| _TEL_ANZAHL | int | Anzahl der Telegramme anzeigen |

<a id="job-read-production-stamp-record"></a>
### READ_PRODUCTION_STAMP_RECORD

Production stamp record lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY", aber hier zuerst "BUSY" |
| GOOD_BAD_STATUS | string | Good/Bad Status |
| LAST_PRODUCT_PROCESS | int | Last product process |
| TYPE_SERIAL_NUMBER | string | Ty serial number |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-write-production-stamp-record"></a>
### WRITE_PRODUCTION_STAMP_RECORD

Schreiben der configuration data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GOOD_BAD_STATUS | string | Good/Bad Status |
| LAST_PRODUCT_PROCESS | string | Last product process |
| TYPE_SERIAL_NUMBER | string | Ty serial number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-read-production-stamp-table"></a>
### READ_PRODUCTION_STAMP_TABLE

Production stamp table lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGENR | string | Auswahl der Infopage |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_SENDE | binary |  |
| _1ST_RECORD_OF_PAGE | binary |  |
| _2ND_RECORD_OF_PAGE | binary |  |
| _3RD_RECORD_OF_PAGE | binary |  |
| _4TH_RECORD_OF_PAGE | binary |  |

<a id="job-read-production-stamp-table-quick-info"></a>
### READ_PRODUCTION_STAMP_TABLE_QUICK_INFO

Production stamp table lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | bestimmt die Anzahl der records |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary | Wert des Bytes _TEL_ANTWORT |
| RECORD_CONRTER | string | Anzahl der Records |

<a id="job-set-no-save-nvr"></a>
### SET_NO_SAVE_NVR

Speicherungs Verbot

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normal OKAY |
| DONE | int | 1 = OK |

<a id="job-remove-no-save-nvr"></a>
### REMOVE_NO_SAVE_NVR

Speicherungs Freigabe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normal OKAY |
| DONE | int | 1 = OK |

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

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben ohne Verifikation

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-status-gps-antenna"></a>
### STATUS_GPS_ANTENNA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise A0 (Acknolage) |
| STAT_GPS | string | Status -1...3 |
| STAT_GPS_TEXT | string | Werte aus Spezifikation |
| STAT_ANTENNA_TEXT | string | Antennenstatus aus Spezifikation |
| STAT_ANTENNA_WERT | int | 0 - verbunden, 1 - nicht verbunden, 2 - Kurzschluss, 3 - anderer GPS Status |
| _TEL_ANTWORT | binary |  |

<a id="job-sprachausgabe"></a>
### SPRACHAUSGABE

Sprachausgabe Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-force-eject"></a>
### FORCE_EJECT

Freigabe der Eject Taste

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-schreiben-navdvdpin"></a>
### SCHREIBEN_NAVDVDPIN

Freigabecode zum Eject

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | datenbereich 0x30 - 0x39 |
| BYTE2 | int | datenbereich 0x30 - 0x39 |
| BYTE3 | int | datenbereich 0x30 - 0x39 |
| BYTE4 | int | datenbereich 0x30 - 0x39 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-navdvdpin-lesen"></a>
### NAVDVDPIN_LESEN

Auslesen der 4 Stellen des CD eject Freigabecodes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CD_EJECT_PINNR | string | CD eject Freigabecodes |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-flottenmodus"></a>
### STEUERN_FLOTTENMODUS

Flottenmodus Status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | datenbereich 0x00 - 0x02 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | string | Flottenmodus |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-flottenmodus"></a>
### STATUS_FLOTTENMODUS

Auslesen des Stati des Flottenmodus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FLOTTEN_MODUS | string |  |
| FLOTTEN_MODUS_WERT | int |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (30 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [LAENDERCODEZIELLAND](#table-laendercodezielland) (10 × 2)
- [CODESPRACHEN](#table-codesprachen) (21 × 2)
- [CODESOFTWARELADENTEXT](#table-codesoftwareladentext) (3 × 2)
- [FLOTTENMODUS](#table-flottenmodus) (3 × 2)

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

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Navigationsrechner |
| 0x02 | Radsensor |
| 0x03 | Eingaenge Peripherie |
| 0x04 | GPS Receiver reagiert nicht auf Initialisierung von NavMk3 |
| 0x05 | Temperatur zu hoch |
| 0x06 | Anwendungs Software |
| 0x07 | Display |
| 0x08 | Audio |
| 0x09 | CD-Fehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 30 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x3B | CARIN CD in MK3 fehlt |
| 0x4B | Video |
| 0x4F | Audio |
| 0x51 | CD Lesen |
| 0x52 | Checksum Instruction EEPROM |
| 0x53 | Checksum Sprach EEPROM |
| 0x54 | Checksum Datei Verwaltung EEPROM |
| 0x55 | Kommunikation Display Bus |
| 0x62 | Gyro Wert nicht im Toleranzbereich |
| 0x63 | Schnittstelle Temperatur Sensor |
| 0x64 | Initialisierung GPS-Empfaenger |
| 0x65 | Luefterfuntion |
| 0x68 | 5V Spannungsversorgung CD-Player |
| 0x69 | 5V Spannungsversorgung |
| 0x6A | 12V Spannungsversorgung CD-Player |
| 0x6B | Spannungsversorgung Sensoren |
| 0x6C | Interne Temperatur zu hoch |
| 0x70 | Interne Temperatur CD-Player zu hoch |
| 0x71 | CD-Player |
| 0x72 | Slave memory |
| 0x73 | Bootcode memory |
| 0x74 | DRAM memory |
| 0x7C | CD-Player |
| 0x7D | CD-Player |
| 0x7E | CD-Player |
| 0x98 | Unerwartetes Software Ereignis, Reset Navigationsrechner |
| 0x99 | Unerwartetes Software Ereignis, Reset Navigationsrechner |
| 0xB5 | Busfehler, Reset Navigationsrechner |
| 0xB6 | Adressfehler, Reset Navigationsrechner |
| 0xFF | Unbekannter Fehlercode im Shadowspeicher |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x40 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-laendercodezielland"></a>
### LAENDERCODEZIELLAND

Dimensions: 10 rows × 2 columns

| CODE | ZIELLAND |
| --- | --- |
| 0x00 | Deutschland |
| 0x01 | englisch UK |
| 0x02 | englisch US |
| 0x03 | Italien |
| 0x04 | Spanien |
| 0x05 | englisch Japan |
| 0x06 | Frankreich |
| 0x07 | CDN |
| 0x08 | Aus/Golf/ZA |
| 0xFF | unbekanntes Land |

<a id="table-codesprachen"></a>
### CODESPRACHEN

Dimensions: 21 rows × 2 columns

| CODE | SPRACHEN |
| --- | --- |
| 0x00 | deutsch maennlich |
| 0x80 | deutsch weiblich |
| 0x01 | englisch UK maennlich |
| 0x81 | englisch UK weiblich |
| 0x02 | englisch US maennlich |
| 0x82 | englisch US weiblich |
| 0x03 | italienisch maennlich |
| 0x83 | italienisch weiblich |
| 0x04 | spanisch maennlich |
| 0x84 | spanisch weiblich |
| 0x05 | englisch UK maennlich |
| 0x85 | englisch UK weiblich |
| 0x06 | franzoesisch maennlich |
| 0x86 | franzoesisch weiblich |
| 0x07 | englisch US maennlich |
| 0x87 | englisch US weiblich |
| 0x08 | englisch UK maennlich |
| 0x88 | englisch UK weiblich |
| 0x89 | hollaendisch weiblich |
| 0x8A | russisch weiblich |
| 0xFF | keine Sprache |

<a id="table-codesoftwareladentext"></a>
### CODESOFTWARELADENTEXT

Dimensions: 3 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | Software erfolgreich geladen |
| 0x01 | Software laden erforderlich |
| 0xFF | unplausibler Wert |

<a id="table-flottenmodus"></a>
### FLOTTENMODUS

Dimensions: 3 rows × 2 columns

| CODE | FLOTTENMODUS |
| --- | --- |
| 0x00 | keine NAVI-DVD Sperrung |
| 0x01 | NAVI-DVD ist mit PIN-Code gesperrt |
| 0x02 | NAVI-DVD ist immer gesperrt |
