# VIDEO_GT.prg

- Jobs: [22](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Videomodul, Graphik-Teil |
| ORIGIN | BMW TI-431 Rochal |
| REVISION | 1.8 |
| AUTHOR | BMW TI-431 Krueger, BMW TP-422 Helmich, BMW TP-422 Teepe, BMW TI-431 Rochal |
| COMMENT | VIDEO_GT |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Videomodul Graphik-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Videomodul Graphik-Teil
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Daten in den Pruefstempel schreiben
- [SOFTWARE_LOADING_LESEN](#job-software-loading-lesen) - Lesen, welche Software geladen ist
- [SOFTWARE_LOADING_SCHREIBEN](#job-software-loading-schreiben)
- [SELBSTTEST](#job-selbsttest) - Selbsttest des VM_GT
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen im VM_GT
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben ohne Verifikation
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [WRITE_CONFIGURATION_DATA](#job-write-configuration-data) - Schreiben der configuration data
- [READ_CONFIGURATION_DATA](#job-read-configuration-data) - Auslesen der configuration data
- [SW_DEMAND_FLAG_SETZEN](#job-sw-demand-flag-setzen) - Herstellen des Auslieferzustandes

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

Init-Job Videomodul Graphik-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Videomodul Graphik-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier 1 |
| F_ART1_NR | int | Index der ersten Fehlerart, 0 oder 40(nicht aktiv,aktiv) |
| F_ART1_TEXT | string | 1.Fehlerart als Text |
| F_UW_NR | int | Ausgabe der Fehlernummer aus Shadowspeicher |
| F_UW_TEXT | string | Ausgabe der Fehlernummer als Text |
| _TEL_ANTWORT | binary | Ausgabe des Telegramms |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| DATUM_1 | int | kann beliebig verwendet werden |
| DATUM_2 | int | kann beliebig verwendet werden |
| DATUM_3 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Daten in den Pruefstempel schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATUM_1 | int | kann beliebig verwendet werden |
| DATUM_2 | int | kann beliebig verwendet werden |
| DATUM_3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_SENDE | binary |  |

<a id="job-software-loading-lesen"></a>
### SOFTWARE_LOADING_LESEN

Lesen, welche Software geladen ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| SW_LADEN_STATUS | string | Statusmeldung Software laden |
| ZIEL_LAND | string | Zielland im Klartext |
| SPRACHE_1 | string | 1.Sprache der Sprachauswahl |
| SPRACHE_2 | string | 2.Sprache der Sprachauswahl |
| SPRACHE_3 | string | 3.Sprache der Sprachauswahl |
| FEHLERTEXT | string | Meldung, welches Subsystem den Fehler beim Software_laden verursacht hat |
| _TEL_ANTWORT | binary |  |

<a id="job-software-loading-schreiben"></a>
### SOFTWARE_LOADING_SCHREIBEN

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
| _TEL_SENDE | binary |  |

<a id="job-selbsttest"></a>
### SELBSTTEST

Selbsttest des VM_GT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen im VM_GT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_LAENDERVARIANTE_TEXT | string | Laendervariante ECE, US_CDN, AUS |
| COD_LAENDERVARIANTE_WERT | int | Wert des Bytes Laendervariante 0-2 |
| ID_COD_INDEX | int | Codierindex aus IDENT |
| COD_SPEED_MAPS_WERT | int | Wert des Bytes SPEED_MAPS, derzeit unbenutzt |
| COD_SPEED_ROUTE_WERT | int | Wert des Bytes ROUTE_MAPS, derzeit unbenutzt |
| COD_USER_INPUT_WERT | int | Wert des Bytes USER_INPUT, derzeit unbenutzt |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (7 × 2)
- [FARTTEXTE](#table-farttexte) (4 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (46 × 2)
- [LAENDERCODEZIELLAND](#table-laendercodezielland) (10 × 2)
- [CODESPRACHEN](#table-codesprachen) (10 × 2)
- [CODESOFTWARELADENTEXT](#table-codesoftwareladentext) (3 × 2)
- [ERRORCODETEXT](#table-errorcodetext) (5 × 2)

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

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Hardwarefehler im Videomodul |
| 0x02 | Hardwarefehler im Graphikteil oder TV-Teil |
| 0x03 | ARCNET-Fehler, keine Kommunikation mit NAV moeglich |
| 0x06 | Fehler Navigationsrechner |
| 0x07 | Fehler beim Beschreiben des EEPROMS |
| 0x08 | I2 C-Bus Fehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 4 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler in diesem Betriebszyklus erkannt |
| 0x40 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 46 rows × 2 columns

| UWNR | UWTEXT |
| --- | --- |
| 0x01 | EEPROM Fehler |
| 0x02 | Boot-ROM Checksummen Fehler |
| 0x03 | Boot-ROM Checksummen Fehler |
| 0x04 | Videoausgabe: Diagnoseschaltung mit staendigen High Pegel am RGB-Ausgang |
| 0x05 | Videoausgabe: Falscher Pegel am RGB Rot Ausgang |
| 0x06 | Videoausgabe: Falscher Pegel am RGB Gruen Ausgang |
| 0x07 | Videoausgabe: Falscher Pegel am RGB Blau Ausgang |
| 0x08 | Videoausgabe: Falscher Pegel am RGB Rot und Gruen Ausgang |
| 0x09 | Videoausgabe: Falscher Pegel am RGB Rot und Blau Ausgang |
| 0x0A | Videoausgabe: Falscher Pegel am RGB Gruen und Blau Ausgang |
| 0x0B | Videoausgabe: Falscher Pegel am RGB Rot Gruen und Blau Ausgang |
| 0x0C | Sprachausgabe: Falscher Pegel am Sprachausgang |
| 0x0D | Sprachausgabe: Keine Spracherzeugung |
| 0x0E | Sprachausgabe: Diagnose misst staendigen Low-Pegel am Sprachausgang |
| 0x0F | Sprachausgabe: Diagnose misst staendigen High-Pegel am Sprachausgang |
| 0x10 | Sprachausgabe: Keine Spracherzeugung |
| 0x11 | Read/write Fehler auf ARCNET chip |
| 0x12 | ARCNET Verbindung: Kein anderer ARCNET Knoten gefunden |
| 0x19 | CPU-DRAM read/write Fehler |
| 0x1A | Video-DRAM read/write Fehler |
| 0x1F | Kontrollprozess konnte nicht gestartet werden |
| 0x20 | Kontrollprozess konnte nicht gestoppt werden |
| 0x21 | Kontrollprozess: Kommunikationskanal konnte nicht eingerichtet werden |
| 0x22 | Kontrollprozess: Event konnte nicht eingerichtet werden |
| 0x23 | Kontrollprozess: Datenmodul konnte nicht eingerichtet werden |
| 0x24 | Kontrollprozess ist unvorhergesehen gestorben |
| 0x25 | Kontrollprozess: Die unteren 8 Bit koennen nicht erkannt werden |
| 0x26 | Kontrollprozess: Fehler beim Lesen des Kommunikationskanals |
| 0x27 | Kontrollprozess: Signal hat Adressaten nicht erreicht |
| 0x28 | Datamodul: Create/link Fehler beim Anlegen eines links |
| 0x29 | Datamodul: Create/link Fehler beim Anlegen eines links |
| 0x2A | Datamodul: Create/link Fehler beim Oeffnen eines Datenmoduls |
| 0x2B | Datamodul: Create/link Fehler beim Oeffnen eines Datenmoduls |
| 0x2C | Datamodul: Create/link Fehler beim Reservieren von Speicher fuer ein Datenmodul |
| 0x2D | Datamodul: Create/link Fehler beim Reservieren von Speicher fuer ein Datenmodul |
| 0x2E | Menue Steuerung: data_trigger Kommunikationskanal nicht verfuegbar |
| 0x2F | Menue Steuerung: Verbindung zum send_I-Bus konnte nicht geoeffnet werden |
| 0x30 | Menue Steuerung: Fehler beim BUILD_SCREEN Prozess |
| 0x31 | Menue Steuerung: Fehler beim SEND_IBUS Prozess |
| 0x32 | Menue Steuerung: Fehler ibus_trigger Kommunikationskanal |
| 0x33 | Menue Steuerung: Fehler beim Lesen des ibus_trigger Kommunikationskanals |
| 0x34 | Menue Steuerung: Datei fuer aktuelle Cursorposition kann nicht erzeugt werden |
| 0x35 | Menue Steuerung: Cursorposition konnte nicht abgespeichert werden |
| 0x36 | Menue Steuerung: Menue konnte nicht abgespeichert werden |
| 0x83 | I-Bus Sendefehler: Schreiben zum I2C-Treiber misslungen |
| 0xFF | unbekannter Fehlerort |

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
| 0x05 | engl. Japan |
| 0x06 | Frankreich |
| 0x07 | CDN |
| 0x08 | Aus/Golf/ZA |
| 0xFF | unbekanntes Land |

<a id="table-codesprachen"></a>
### CODESPRACHEN

Dimensions: 10 rows × 2 columns

| CODE | SPRACHEN |
| --- | --- |
| 0x00 | deutsch |
| 0x01 | englisch UK |
| 0x02 | englisch US |
| 0x03 | italienisch |
| 0x04 | spanisch |
| 0x05 | englisch UK |
| 0x06 | franzoesisch |
| 0x07 | englisch US |
| 0x08 | englisch UK |
| 0xFF | unbekannte Sprache |

<a id="table-codesoftwareladentext"></a>
### CODESOFTWARELADENTEXT

Dimensions: 3 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | Software erfolgreich geladen |
| 0x01 | Fehler beim Laden der Software |
| 0xFF | unbekannte Meldung |

<a id="table-errorcodetext"></a>
### ERRORCODETEXT

Dimensions: 5 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x01 | Fehler im Videomodul |
| 0x02 | Fehler im Navigationsrechner |
| 0x03 | Fehler Videomodul und im NAV-Rechner |
| 0x04 | CD Software-Fehler |
| 0xFF | unbekannter Fehlerort |
