# BMBT46TN.prg

- Jobs: [27](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Bordmonitor Topnavigation |
| ORIGIN | BMW TI-433 Helmich |
| REVISION | 1.01 |
| AUTHOR | BMW TI-433 Helmich, BMW TI-433 Holdsclaw |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Bordmonitor Bedienteil-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Bordmonitor Bedienteil-Teil
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen 
- [STEUERN_SELBSTHALTUNG](#job-steuern-selbsthaltung)
- [STEUERN_MONITOR_HELLIGKEIT](#job-steuern-monitor-helligkeit)
- [STEUERN_NF_TEST](#job-steuern-nf-test)
- [STEUERN_HEADROOM](#job-steuern-headroom)
- [STEUERN_MUTE](#job-steuern-mute)
- [STEUERN_POWER_CASSETTE](#job-steuern-power-cassette)
- [STEUERN_POWER_DISPLAY](#job-steuern-power-display)
- [STEUERN_NTSC_PAL](#job-steuern-ntsc-pal)
- [STEUERN_HEIZUNG](#job-steuern-heizung)
- [STEUERN_CASSETTE](#job-steuern-cassette)
- [TESTTON_AUSGEBEN](#job-testton-ausgeben)
- [CASSETTENDECK_BETRIEBSSTUNDENZAEHLER_LOESCHEN](#job-cassettendeck-betriebsstundenzaehler-loeschen)
- [LC_ANZEIGE_BETRIEBSSTUNDENZAEHLER_LOESCHEN](#job-lc-anzeige-betriebsstundenzaehler-loeschen)
- [SELBSTTEST](#job-selbsttest) - Selbsttest Bordmonitor Bedien-Teil
- [Status_lesen_SG](#job-status-lesen-sg)
- [STATUS_LESEN_DREHGEBER](#job-status-lesen-drehgeber) - Stati lesen am Bordmitor Bedien-Teil
- [STATUS_LESEN_DISPLAY](#job-status-lesen-display) - Stati lesen Bordmitor u. Display
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job Bordmonitor Bedienteil-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Bordmonitor Bedienteil-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferant-Nummer |
| ID_LIEF_TEXT | string | Lieferant im Klartext |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_INDEX | string | Aenderungsindex |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | Ausgabe Fehlernummer |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | hier 1, vorhanden/ nicht vorhanden |
| F_ART1_TEXT | string | momentan vorhanden/ sporadisch(momentan nicht vorhanden) |
| F_ART1_NR | int | Nummer der Fahlerart |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier keine |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-selbsthaltung"></a>
### STEUERN_SELBSTHALTUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-monitor-helligkeit"></a>
### STEUERN_MONITOR_HELLIGKEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-nf-test"></a>
### STEUERN_NF_TEST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-headroom"></a>
### STEUERN_HEADROOM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-mute"></a>
### STEUERN_MUTE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-power-cassette"></a>
### STEUERN_POWER_CASSETTE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-power-display"></a>
### STEUERN_POWER_DISPLAY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-ntsc-pal"></a>
### STEUERN_NTSC_PAL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-heizung"></a>
### STEUERN_HEIZUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERCODE | int | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-steuern-cassette"></a>
### STEUERN_CASSETTE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERTEXT | string | DATENBYTE 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-testton-ausgeben"></a>
### TESTTON_AUSGEBEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-cassettendeck-betriebsstundenzaehler-loeschen"></a>
### CASSETTENDECK_BETRIEBSSTUNDENZAEHLER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-lc-anzeige-betriebsstundenzaehler-loeschen"></a>
### LC_ANZEIGE_BETRIEBSSTUNDENZAEHLER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-selbsttest"></a>
### SELBSTTEST

Selbsttest Bordmonitor Bedien-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| _TEL_SENDE | binary | Sendetelegramm anzeigen |
| _TEL_ANTWORT | binary | Antworttelegramm anzeigen |

<a id="job-status-lesen-sg"></a>
### Status_lesen_SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| TUER_STATUS | int | ????????? |
| CASSETTEN_STATUS_WERT | int | 0= Cassetenlaufwerk in Eject, Standby, FFW, FRW oder Pause 1= Cassetenlaufwerk in Play |
| CASSETTEN_STATUS_TEXT | string | 0= Cassetenlaufwerk in Eject, Standby, FFW, FRW oder Pause 1= Cassetenlaufwerk in Play |
| DIMMERSTELLUNG | int | ?????????, 1 Byte |
| CASSETTENDECK_BETRIEBSSTUNDENZAEHLER | string | in Sekunden hexadezimal, 4 Byte |
| LC_ANZEIGE_BETRIEBSSTUNDENZAEHLER | string | in Sekunden hexadezimal, 4 Byte |
| LC_ANZEIGE_DAUER_UEBERTEMPERATUR | string | in Sekunden hexadezimal, 4 Byte |
| MONITORTYP_WERT | int | Monitortyp, 0=kein Monitor 1= Philips, 2= Alpine |
| MONITORTYP_TEXT | string | s.o. |
| _TEL_ANTWORT | binary | Antworttelegramm anzeigen |

<a id="job-status-lesen-drehgeber"></a>
### STATUS_LESEN_DREHGEBER

Stati lesen am Bordmitor Bedien-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_KEYBOARD_WERT | int | 254 oder 255 |
| STAT_KEYBOARD_TEXT | string | 255= keine Taste gedrueckt,254= mehrere Tasten gedrueckt |
| STAT_MONITOR_DREHGEBER_SCHRITTE | int | -32 bis 31 |
| STAT_VOLUME_DREHGEBER_SCHRITTE | int | -32 bis 31 |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-status-lesen-display"></a>
### STATUS_LESEN_DISPLAY

Stati lesen Bordmitor u. Display

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_KLEMME_R_EIN | int | 1= Ein, 0= Aus |
| STAT_HEADROOMREGELUNG_KASSETTE | int | Pulsweitenmodeliertes Signal(PWM), 0-255 Berechnete Verstaerkung |
| STAT_HELLIGKEITSWERT_LC_MONITOR | int | Pulsweitenmodeliertes Signal(PWM), 0-255 Berechnete Helligkeit |
| STAT_SPANNUNG_UBATT_WERT | real |  |
| STAT_SPANNUNG_UBATT_EINH | string | Volt |
| STAT_NFT1_WERT | int |  |
| STAT_NFT2_WERT | int |  |
| STAT_NFT3_WERT | int |  |
| STAT_NFT4_WERT | int |  |
| STAT_LCD_TEMPERATUR_WERT | int | nur Ausgabe ADC-Wert, 0-255 |
| STAT_FOTOSENSOR_WERT | int | nur Ausgabe ADC-Wert, 0-255 |
| STAT_LAMPENHEIZUNG_WERT | int | nur TN BM, 1=Ein, 0=Aus |
| _TEL_ANTWORT | binary | Antworttelegramm anzeigen |

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (17 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [CASSETTE](#table-cassette) (14 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

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

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Reset |
| 0x02 | LC-Monitor Uebertemperatur |
| 0x03 | Radio Status Telegramm Timeout |
| 0x04 | Kurzschluss NF Leitung 1 |
| 0x05 | Kurzschluss NF Leitung 2 |
| 0x06 | Kurzschluss NF Leitung 3 |
| 0x07 | Kurzschluss NF Leitung 4 |
| 0x08 | K-Bus Senden |
| 0x09 | K-Bus Empfangen |
| 0x0A | Monitor Heizung Kurzschluss gegen U-Batt |
| 0x0B | Stecker Monitor UB Leitungsunterbrechung |
| 0x0C | Stecker Monitor Ub Heiz Leitungsunterbrechung |
| 0x14 | Temperatursensor Monitor unplausibler Wert |
| 0x15 | Monitorheizung oder Sicherung |
| 0x16 | EEPROM Checksumme stimmt nicht mit programmierten Wert ueberein |
| 0x17 | Programm Versionsnummer stimmt nicht mit der im EEPROM programmierten ueberein |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-cassette"></a>
### CASSETTE

Dimensions: 14 rows × 2 columns

| FUNKTIONTEXT | HEXCODE |
| --- | --- |
| EJECT | 0x40 |
| PLAY | 0x41 |
| FFW | 0x42 |
| FRW | 0x43 |
| MSS_FW | 0x44 |
| MSS_RW | 0x45 |
| STANDBY | 0x48 |
| PAUSE_EIN | 0x4A |
| PAUSE_AUS | 0x4B |
| WIEDERGABE_NORMAL | 0x5A |
| WIEDERGABE_REVERSE | 0x5B |
| DOLBY_B | 0x5D |
| DOLBY_C | 0x5E |
| DOLBY_AUS | 0x5F |

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
