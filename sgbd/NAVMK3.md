# NAVMK3.prg

- Jobs: [30](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Navigationsrechner MK3/Roadrunner |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.02 |
| AUTHOR | BMW TI-431 Helmich, BMW TI-431 Krueger, BMW TI-431 Holdsclaw, Bernd Woell S-VDO, BMW TI-431 Rochal |
| COMMENT | NAVMK3 |
| PACKAGE | 0.09 |
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
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes

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
| TEST_STAT_RADSENSOR | string | Bereich -1...3 |
| STAT_RADSENSOR_LINKS_WERT | int | Impulse pro Sekunde |
| STAT_RADSENSOR_RECHTS_WERT | int | Impulse pro Sekunde |
| STAT_RADSENSOR_EINH | string | Impulse/sec |
| TEST_STATUS_GYRO | string | Bereich -1...3 |
| STAT_GYRO_WERT | int | Bereich 0...65535 |
| STAT_GYRO_EINH | string | Spannung in mV |
| TEST_STAT_5V | string | Bereich -1...3 |
| STAT_5V_WERT | int | 5V Stromversorgang digitale Schaltkreise Bereich 0...65535 |
| STAT_5V_EINH | string | Spannung in mV |
| TEST_STAT_12V | string | Bereich -1...3 |
| STAT_12V_WERT | int | Stromversorgung Batterie Bereich 0...6535 |
| STAT_12V_EINH | string | Spannung in mV |
| TEST_STAT_SPANNUNG_SENSOR | string | Bereich -1...3 |
| STAT_SPANNUNG_SENSOR_WERT | int | Spannungsversorgung Sensor Bereich 0...65535 |
| STAT_SPANNUNG_SENSOR_EINH | string | Spannung in mV |
| TEST_STAT_LUEFTER | string | Status-Abfrage Luefter,-1...3 |
| STAT_LUEFTER_WERT | int | Abfrage, ob Luefter eingeschaltet ist 0=Aus,1=Ein |
| STAT_LUEFTER_TEXT | string | Abfrage, ob Luefter eingeschaltet ist 0=Aus,1=Ein |
| TEST_STAT_CD_AUSWURFTASTE | string | Status -1...3 |
| STAT_CD_AUSWURFTASTE_WERT | int | Status-Abfrage, 0= nicht gedrueckt Status-Abfrage, 1= gedrueckt |
| STAT_CD_AUSWURFTASTE_TEXT | string | Status-Abfrage, 0= nicht gedrueckt Status-Abfrage, 1= gedrueckt |
| TEST_STAT_TEMPERATUR | string | Status -1...3 |
| STAT_SYSTEM_TEMPERATUR_WERT | int | Bereich -32768...32767 |
| STAT_SYSTEM_TEMPERATUR_EINH | string | Temperatur in Grad Celsius |
| TEST_STAT_GANGWAHL | string | Status -1...3 |
| STAT_GANGWAHL_WERT | int | Status 0= Vor, 1= Rueckwaerts |
| STAT_GANGWAHL_TEXT | string | Status 0= Vor, 1= Rueckwaerts |
| TEST_STATUS_GPS | string | Status -1...3 |
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
| ID_VARIANTE | string | Varianten Nav-Rechner: NAVMK3_LOW, NAVMK3_HIGH, NAVMK3? |
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
| KONFIG_CUSTOMER | string | Customer im Klartext |
| KONFIG_SWDISPLAYTYPE | string | SW/Display type im Klartext |
| KONFIG_NAVIGATIONS_MODE | string | Navigation mode im Klartext |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| RESERVIERT | int | Return Value wird im Moment nicht gebraucht |
| TERMINATOR | int | Return Value wird im Moment nicht gebraucht |
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
| _1st_record_of_page | binary |  |
| _2nd_record_of_page | binary |  |
| _3rd_record_of_page | binary |  |
| _4th_record_of_page | binary |  |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (30 × 2)
- [LAENDERCODEZIELLAND](#table-laendercodezielland) (10 × 2)
- [CODESPRACHEN](#table-codesprachen) (19 × 2)
- [CODESOFTWARELADENTEXT](#table-codesoftwareladentext) (3 × 2)

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

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x40 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

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
| 0x62 | Gyro Wert nicht im Toleranzbereich  |
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

Dimensions: 19 rows × 2 columns

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
| 0xFF | keine Sprache |

<a id="table-codesoftwareladentext"></a>
### CODESOFTWARELADENTEXT

Dimensions: 3 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | Software erfolgreich geladen |
| 0x01 | Software laden erforderlich |
| 0xFF | unplausibler Wert |
