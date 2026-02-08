# BM46WIDE.prg

- Jobs: [14](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Widescreen Bordmonitor E46 |
| ORIGIN | BMW TI-430 Buboltz |
| REVISION | 1.1 |
| AUTHOR | Alpine H. Weber, BMW TI-430 Buboltz, BMW TI-430 Gall |
| COMMENT | Widescreen E46 |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Bordmonitor Bedienteil-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Bordmonitor Bedienteil-Teil
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen 
- [CHECKSUMME_ABFRAGEN](#job-checksumme-abfragen)
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern mehrerer digitaler Ausgaenge
- [SELBSTTEST](#job-selbsttest) - Selbsttest Bordmonitor Bedien-Teils
- [STATUS_LESEN](#job-status-lesen) - Stati lesen am Bordmitor Bedien-Teil
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Daten in den Pruefstempel schreiben
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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
| JOB_STATUS | string | Normalerweise "OKAY") |
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
| ID_AI_INDEX | string | ALPINE Aenderungsindex Wird von ALPINE nicht aktualisiert NICHT BMW RELEVANT! |
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
| F_ART_ANZ | int | Anzahl der Fehlerarten, hier keine |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier keine |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-checksumme-abfragen"></a>
### CHECKSUMME_ABFRAGEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern mehrerer digitaler Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_RADIO | int | Ansteuerung LED Radio 0 := LED Radio aus 1 := LED Radio an jeder anderer Wert = LED aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-selbsttest"></a>
### SELBSTTEST

Selbsttest Bordmonitor Bedien-Teils

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Stati lesen am Bordmitor Bedien-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_KLEMME_R_EIN | int |  |
| STAT_LC_MONITOR_UEBERTEMP_WERT | int |  |
| STAT_SPANNUNG_UBATT_WERT | real |  |
| STAT_SPANNUNG_UBATT_EINH | string | Volt? |
| STAT_NFT2_WERT | int |  |
| STAT_NFT3_WERT | int |  |
| STAT_NFT4_WERT | int |  |
| STAT_NFT1_WERT | int |  |
| STAT_FOTOSENSOR_WERT | int |  |
| STAT_FOTOSENSOR_EINH | string | % |
| STAT_HELLIGKEITSWERT_LC_MONITOR | int | pulsweitenmodeliertes Signal, 0-255 keine Einheit |
| STAT_HEADROOMREGELUNG_KASSETTE | int | pulsweitenmodeliertes Signal, 0-255 keine Einheit |
| _TEL_ANTWORT | binary |  |

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

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [FORTTEXTE](#table-forttexte) (11 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN](#table-steuern) (8 × 3)

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

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 59 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Energiesparmode aktiv |
| 0x01 | Watchdog Reset |
| 0x02 | LC-Monitor Uebertemperatur |
| 0x03 | Radio Status Telegramm Timeout |
| 0x04 | Kurzschluss Audio Leitung 1 |
| 0x05 | Kurzschluss Audio Leitung 2 |
| 0x06 | Kurzschluss Audio Leitung 3 |
| 0x07 | Kurzschluss Audio Leitung 4 |
| 0x14 | Temperatursensor Fehler |
| 0x16 | EEPROM checksum Fehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 8 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| TEL_LED_GELB | 2 | 0x01 |
| TEL_LED_ROT | 2 | 0x02 |
| TEL_LED_GRUEN | 2 | 0x04 |
| LED_RADIO | 2 | 0x08 |
| LED_HEIZ_UHREVHL | 2 | 0x10 |
| Kassette | 1 | 0x01 |
| LED_FUNKTION | 1 | 0x02 |
| XYZ | 2 | 0xFF |
