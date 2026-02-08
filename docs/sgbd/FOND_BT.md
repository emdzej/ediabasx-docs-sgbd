# FOND_BT.prg

- Jobs: [14](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Fondmonitor Bedienteil |
| ORIGIN | BMW TI-431 Krueger |
| REVISION | 1.0 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-433 Helmich, BMW TI-433 Krueger |
| COMMENT | FOND_BT |
| PACKAGE | 0.05 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Bordmonitor Bedienteil-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Bordmonitor Bedienteil-Teil
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen 
- [Checksumme_abfragen](#job-checksumme-abfragen)
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern mehrerer digitaler Ausgaenge
- [Sonderjob](#job-sonderjob)
- [SELBSTTEST](#job-selbsttest) - Selbsttest Bordmonitor Bedien-Teils
- [STATUS_LESEN](#job-status-lesen) - Stati lesen am Bordmitor Bedien-Teil
- [Pruefstempel_lesen](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [Pruefstempel_schreiben](#job-pruefstempel-schreiben) - Daten in den Pruefstempel schreiben
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
| F_ART_ANZ | int | Anzahl der Fehlerarten, hier keine |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier keine |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-checksumme-abfragen"></a>
### Checksumme_abfragen

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
| TEL_LED_GELB | string | Ansteuerung gelbe LED |
| TEL_LED_ROT | string | Ansteuerung rote LED |
| TEL_LED_GRUEN | string | Ansteuerung gruene LED |
| LED_RADIO | string | Ansteuerung LED Radio |
| LED_HEIZ_UHR | string | Ansteuerun LED Heizung und Uhr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-sonderjob"></a>
### Sonderjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_SENDE | binary |  |
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
| STAT_KEYBOARD | int |  |
| STAT_MONITOR_DREHGEBER_SCHRITTE | int | -32 bis 31 |
| STAT_VOLUME_DREHGEBER_SCHRITTE | int | -32 bis 31 |
| STAT_LC_MONITOR_UEBERTEMP_WERT | int |  |
| STAT_SPANNUNG_UBATT_WERT | real |  |
| STAT_SPANNUNG_UBATT_EINH | string | Volt? |
| STAT_DIMMER_KL_58g_WERT | real |  |
| STAT_DIMMER_KL_58g_EINH | string | volt |
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
### Pruefstempel_lesen

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
### Pruefstempel_schreiben

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
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
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

Dimensions: 56 rows × 2 columns

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
| 0x55 | BHTC |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Watchdog Reset |
| 0x02 | PL-Leitung Kurzschluss gegen U-Batt |
| 0x03 | PL-Leitung Kurzschluss gegen Masse |
| 0x04 | PL-Leitung Leitungsunterbrechung |
| 0x05 | LC-Monitor Uebertemperatur |
| 0x06 | Radio Status Telegramm Timeout |
| 0x07 | Kurzschluss NF Leitung 1 |
| 0x08 | Kurzschluss NF Leitung 2 |
| 0x09 | Kurzschluss NF Leitung 3 |
| 0x0A | Kurzschluss NF Leitung 4 |
| 0x0B | I-Bus Fehler beim Senden |
| 0x0C | 25 Stunden Notabschaltung |
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
