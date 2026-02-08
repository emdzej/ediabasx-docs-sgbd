# CVM_III.prg

- Jobs: [16](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Cabrio-Verdeck-Modul III E52 |
| ORIGIN | BMW TI-431 Mellersh |
| REVISION | 1.2 |
| AUTHOR | BMW TI-431 Teepe, Mellersh |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [STEUERN_DIGITAL](#job-steuern-digital) - STEUERN_DIGITAL job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Codierung lesen job
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers des CVM Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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
| F_LOESCHDATUM_KW | int |  |
| F_LOESCHDATUM_JAHR | int |  |
| F_ORT_NR | int |  |
| F_ORT_TEXT | string |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_UW1_NR | int | Nummer der Umweltbedingung, immer 1 |
| F_UW1_TEXT | string | Text der Umweltbedingung, immer 'Aussentemperatur' |
| F_UW1_EINH | string | Einheit Grad C |
| F_UW1_WERT | int | Wert |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-is-lesen"></a>
### IS_LESEN

is_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_NR | int |  |
| F_ORT_TEXT | string |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-status-lesen"></a>
### STATUS_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLEMME_R_EIN | int |  |
| STAT_KLEMME_30_EIN | int |  |
| STAT_V_SCHL_EIN | int |  |
| STAT_V_OEFF_EIN | int |  |
| STAT_V_SPERR_EIN | int | zur Hardtoperkennung |
| STAT_CVM_III_EIN | int | Stati gelten fuer CVM_III |
| STAT_VSW41_EIN | int | bei high: Windlauf geschlossen |
| STAT_VSW12_EIN | int | bei high: Verdeckklappe vollstaendig geoeffnet |
| STAT_VSW71_EIN | int | bei high: Verdeckklappe unten zum verriegeln rechts |
| STAT_VSW42_EIN | int | bei high: Windlauf geoeffnet |
| STAT_VSW8_EIN | int | bei high: Verdeck sicher am Windlauf verriegelt |
| STAT_SWHTOP_EIN | int | bei high: Hardtop aufgesetzt |
| STAT_VSW9_EIN | int | bei high: Sensor fuer Griffschale |
| STAT_RPUMPEA_EIN | int | bei high: Pumpenrelais fuer auf angesteuert |
| STAT_RPUMPEZ_EIN | int | bei high: Pumpenrelais fuer zu angesteuert |
| STAT_V_WM1_EIN | int | bei high: Windlaufmotor oeffnet Windlauf |
| STAT_V_WM2_EIN | int | bei high: Windlaufmotor schliesst Windlauf |
| STAT_AUSSENTEMPERATUR_WERT | int | Wert der Aussentemperatur vom K-Bus |
| STAT_FAHRZEUG_FAEHRT_EIN | int |  |
| STAT_MIN_1_FENSTER_GESCHLOSSEN_EIN | int |  |
| STAT_FREIGABE_HECKSCHEIBENHEIZUNG_EIN | int | oder HiFi |
| STAT_VERDECKZAEHLER_ZU_WERT | int |  |
| STAT_VERDECKZAEHLER_AUF_WERT | int |  |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Herstellerdaten Byte 1 bis 4 |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

STEUERN_DIGITAL job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | anzusteuerndes Ventil |
| PASSWORD | string | Passwort bei Verdeckbewegungen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Codierung lesen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATENBLOCK | binary | Netto Hex-Daten von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers des CVM Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| ADRESSE | int | 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (71 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (11 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 3)
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

Dimensions: 71 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Codierdatensatz ungueltig, nicht codiert |
| 0x02 | Codierung unplausibel, Zuordnung CVM II oder III |
| 0x03 | Checksummenfehler ROM |
| 0x04 | Checksummenfehler EEPROM |
| 0x05 | Checksummenfehler in den Codierdaten |
| 0x06 | RAM-Check fehlerhaft |
| 0x07 | Watchdog-Fehler |
| 0x08 | Opcode-Fehler |
| 0x09 | Clock-Monitor-Fehler |
| 0x0A | Kommunikationsfehler K-Bus-Schnittstelle |
| 0x10 | Versorgung der VSW im Fahrzeug ausser Toleranz |
| 0x11 | Versorgung der VSW am Verdeck ausser Toleranz |
| 0x12 | Bedientaster 'Oeffnen' permanent aktiv |
| 0x13 | Bedientaster 'Schliessen' permanent aktiv |
| 0x14 | Temperaturfuehlereingang, permanent auf Masse |
| 0x15 | Temperaturfuehlereingang, kein Sensor angeschlossen |
| 0x16 | Poti Hauptsaeule, abgerissene |
| 0x17 | Poti Hauptsaeule, an Masse |
| 0x18 | Poti Spannbuegel, abgerissene |
| 0x19 | Poti Spannbuegel, an Masse |
| 0x1A | VSW 1.2, Eingangsspannung &gt;5 Volt |
| 0x1B | VSW 1.2, Eingangsspannung undefiniert |
| 0x1C | VSW 1.2, Eingang an Masse |
| 0x1D | VSW 4.1, Eingangsspannung &gt;5 Volt |
| 0x1E | VSW 4.1, Eingangsspannung undefiniert |
| 0x1F | VSW 4.1, Eingang an Masse |
| 0x20 | VSW 4.2, Eingangsspannung &gt;5 Volt |
| 0x21 | VSW 4.2, Eingangsspannung undefiniert |
| 0x22 | VSW 4.2, Eingang an Masse |
| 0x23 | VSW 7.1, Eingangsspannung &gt;5 Volt |
| 0x24 | VSW 7.1, Eingangsspannung undefiniert |
| 0x25 | VSW 7.1, Eingang an Masse |
| 0x26 | VSW 7.2, Eingangsspannung &gt;5 Volt |
| 0x27 | VSW 7.2, Eingangsspannung undefiniert |
| 0x28 | VSW 7.2, Eingang an Masse |
| 0x29 | VSW 8, Eingangsspannung &gt;5 Volt |
| 0x2A | VSW 8, Eingangsspannung undefiniert |
| 0x2B | VSW 8, Eingang an Masse |
| 0x2C | VSW 9, Eingangsspannung &gt;5 Volt |
| 0x2D | VSW 9, Eingangsspannung undefiniert |
| 0x2E | VSW 9, Eingang an Masse |
| 0x2F | VSW HTOP, Eingangsspannung &gt;5 Volt |
| 0x30 | VSW HTOP, Eingangsspannung undefiniert |
| 0x31 | VSW HTOP, Eingang an Masse |
| 0x40 | Entriegeln, Motorstrom H-Bruecke zu hoch, Kurzschluss |
| 0x41 | Verriegeln, Motorstrom H-Bruecke zu hoch, Kurzschluss |
| 0x42 | Kurzschluss Motorbruecke oder Motor nach Ub+ |
| 0x43 | Offene Last beim Entriegeln |
| 0x44 | Offene Last beim Verriegeln |
| 0x45 | V4SBA, nicht angeschlossen |
| 0x46 | V4SBA, Kurzschluss nach Masse |
| 0x47 | V4SBA, Kurzschluss nach UBatt |
| 0x48 | V3SBE, nicht angeschlossen |
| 0x49 | V3SBE, Kurzschluss nach Masse |
| 0x4A | V3SBE, Kurzschluss nach UBatt |
| 0x4B | Ausgaenge V4SBA und V2_HAUPT, durch Kurzschluss verbunden |
| 0x4C | V2_HAUPT, nicht angeschlossen |
| 0x4D | V2_HAUPT, Kurzschluss nach Masse |
| 0x4E | V2_HAUPT, Kurzschluss nach UBatt |
| 0x50 | V5GO, nicht angeschlossen |
| 0x51 | V5GO, Kurzschluss nach Masse |
| 0x52 | V5GO, Kurzschluss nach UBatt |
| 0x67 | Windlauf faehrt nicht auf |
| 0x68 | Windlauf faehrt nicht zu |
| 0x69 | RPUMPEA, nicht angeschlossen |
| 0x6A | RPUMPEA, Kurzschluss nach Masse |
| 0x6B | RPUMPEA, Kurzschluss nach UBatt |
| 0x6C | RPUMPEZ, nicht angeschlossen |
| 0x6D | RPUMPEZ, Kurzschluss nach Masse |
| 0x6E | RPUMPEZ, Kurzschluss nach UBatt |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x70 | Unterspannung an Klemme 30 |
| 0x71 | Ueberspannung an Klemme 30 |
| 0x72 | interne 5V-Versorgung ausserhalb Toleranz |
| 0x74 | keine ZKE-Antwort 'Tueren- / Klappenstatus' |
| 0x77 | Absenken Seitenscheiben nicht zurueckgemeldet |
| 0x78 | Anheben Seitenscheiben nicht zurueckgemeldet |
| 0x79 | kein Kombistatus erhalten |
| 0x7A | Verdeckstecker nicht gesteckt |
| 0x7B | SW in undefiniertem Zustand, Hardwarefehler |
| 0x7C | SW in undefiniertem Zustand, unbekannte Verdeckstellung |
| 0xFF | unbekannter Fehlerort |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | ----   | ---- |
| 0x01 | Aussentemperatur | Grad C |
| 0xXY | unbekannte Umweltbedingung | -- |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 8 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| VENTIL1 | 1 | 0x01 |
| VENTIL2 | 1 | 0x02 |
| VENTIL3 | 1 | 0x04 |
| VENTIL4 | 1 | 0x08 |
| VENTIL5 | 1 | 0x10 |
| PUMPE | 1 | 0x20 |
| HHS | 1 | 0x40 |
| XXX | Y | Z |
