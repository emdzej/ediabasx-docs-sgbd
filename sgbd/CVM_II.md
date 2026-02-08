# CVM_II.prg

- Jobs: [19](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Cabrio-Verdeck-Modul II E46 |
| ORIGIN | BMW TI-431 Mellersh |
| REVISION | 1.7 |
| AUTHOR | BMW TI-431 Teepe, Mellersh, Krueger |
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
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [STATUS_LESEN](#job-status-lesen) - STATUS_LESEN job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [ANALYSE_VERDECKLAUF](#job-analyse-verdecklauf) - ANALYSE_VERDECKLAUF job
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern der Stellglieder
- [CODIERUNG_LESEN](#job-codierung-lesen) - Codierung lesen job
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers des CVM Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [LOGIN](#job-login) - Login job

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

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

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
| STAT_SWBUNT_EIN | int |  |
| STAT_V_SCHL_EIN | int |  |
| STAT_V_OEFF_EIN | int |  |
| STAT_CVM_II_EIN | int |  |
| STAT_VSW41_EIN | int | bei high: Windlauf geschlossen |
| STAT_VSW12_EIN | int | bei high: Verdeckklappe vollstaendig geoeffnet |
| STAT_VSW71_EIN | int | bei high: Verdeckklappe unten zum verriegeln rechts |
| STAT_VSW42_EIN | int | bei high: Windlauf geoeffnet |
| STAT_VSW8_EIN | int | bei high: Verdeck sicher am Windlauf verriegelt |
| STAT_SWHTOP_EIN | int | bei high: Hardtop aufgesetzt |
| STAT_VSW72_EIN | int | bei high: Verdeckklappe unten zum verriegeln links |
| STAT_V1KLAP_EIN | int | Ventil angesteuert |
| STAT_V2HAUPT_EIN | int | Ventil angesteuert |
| STAT_V3SBE_EIN | int | Ventil angesteuert |
| STAT_V4SBA_EIN | int | Ventil angesteuert |
| STAT_V5GO_EIN | int | Ventil angesteuert |
| STAT_VPUMPE_EIN | int | Druckpumpe angesteuert |
| STAT_VPSB_WERT | real | Spannungswert Spannbuegel |
| STAT_VPSB_EINH | string |  |
| STAT_SEG_ZUORD_SB_WERT | int | Wertebereich 0 bis 4 |
| STAT_SEG_ZUORD_SB_TEXT | string |  |
| STAT_SEG_ZUORD_SB_WINKEL | string | Winkelbereich |
| STAT_VPHS_WERT | real |  |
| STAT_VPHS_EINH | string |  |
| STAT_SEG_ZUORD_HSP_WERT | int |  |
| STAT_SEG_ZUORD_HSP_TEXT | string |  |
| STAT_SEG_ZUORD_HSP_WINKEL | string |  |
| STAT_VTEMP_WERT | int | Temperaturwert der Druckpumpe gemaess Umrechnungstabelle VTEMP |
| STAT_VTEMP_EINH | string | Grad C |
| STAT_LAUF_UNABHAENGIG_VON_P_TEMP_MOEGLICH_EIN | int |  |
| STAT_PRE_ALARM_AKTIV | int |  |
| STAT_TEMP_ABSCHALTUNG_AKTIV | int |  |
| STAT_TEMP_MESSUNG_DEFEKT_AKTIV | int |  |
| STAT_AUSSENTEMPERATUR_WERT | int | Wert der Aussentemperatur vom K-Bus |
| STAT_VERDECKKLAPPE_VERRIEGELT_EIN | int |  |
| STAT_HECKKLAPPE_GEOEFFNET_EIN | int |  |
| STAT_FAHRZEUG_FAEHRT_EIN | int |  |
| STAT_MIN_1_FENSTER_GESCHLOSSEN_EIN | int |  |
| STAT_VERDECKZAEHLER_ZU_WERT | int |  |
| STAT_VERDECKZAEHLER_AUF_WERT | int |  |
| _ANTWORT | binary | antworttelegramm |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| HERSTELLERDATEN | binary | Herstellerdaten Byte 1 bis 4 |

<a id="job-analyse-verdecklauf"></a>
### ANALYSE_VERDECKLAUF

ANALYSE_VERDECKLAUF job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATENBLOCK | binary | gesamte Daten aus allen gesendeten Telegrammen (Soll: 224) |
| ANZAHL_DATENBYTES | int | Anzahl der ausgelesenen Bytes |
| DATENBLOCK_TEXT | string | gesamte Daten aus allen gesendeten Telegrammen (Soll: 224) als String |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern der Stellglieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | anzusteuernder Ausgang (Ventil, Pumpe oder Heckscheibe) table Stellglieder STEUERN STEUER_I_O |

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

<a id="job-login"></a>
### LOGIN

Login job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORD | int | Passwort bei Verdeckbewegungen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (82 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [VTEMP](#table-vtemp) (256 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 3)
- [STEUERN](#table-steuern) (10 × 3)
- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 82 rows × 2 columns

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
| 0x16 | Poti Hauptsaeule, abgerissen |
| 0x17 | Poti Hauptsaeule, an Masse |
| 0x18 | Poti Spannbuegel, abgerissen |
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
| 0x47 | V4SBA, Kurzschluss nach Ub+ |
| 0x48 | V3SBE, nicht angeschlossen |
| 0x49 | V3SBE, Kurzschluss nach Masse |
| 0x4A | V3SBE, Kurzschluss nach Ub+ |
| 0x4B | V4SBA und V2_Haupt, Ausgang durch Kurzschluss verbunden |
| 0x4C | V2_Haupt, nicht angeschlossen |
| 0x4D | V2_Haupt, Kurzschluss nach Masse |
| 0x4E | V2_Haupt, Kurzschluss nach Ub+ |
| 0x50 | V5GO, nicht angeschlossen |
| 0x51 | V5GO, Kurzschluss nach Masse |
| 0x52 | V5GO, Kurzschluss nach Ub+ |
| 0x53 | VPUMPE, nicht angeschlossen |
| 0x54 | VPUMPE, Kurzschluss nach Masse |
| 0x55 | VPUMPE, Kurzschluss nach Ub+ |
| 0x56 | V5GO und VPUMPE, Ausgang durch Kurzschluss verbunden |
| 0x57 | V1KLAP, nicht angeschlossen |
| 0x58 | V1KLAP, Kurzschluss nach Masse |
| 0x59 | V1KLAP, Kurzschluss nach Ub+ |
| 0x5A | HECKS, nicht angeschlossen |
| 0x5B | HECKS, Kurzschluss nach Masse |
| 0x5C | HECKS, Kurzschluss nach Ub+ |
| 0x60 | Verdeckklappe wird nicht angehoben, Timeout |
| 0x61 | Verdeckklappe wird nicht geoeffnet, Timeout |
| 0x62 | Verdeckklappe wird nicht ausreichend geschlossen, Time? |
| 0x63 | Hauptsaeule zieht Spannbuegel nicht aus Verdeckkasten |
| 0x64 | Hauptsaeule drueckt Spannbuegel nicht in Verdeckkasten |
| 0x65 | Spannbuegel wird nicht vollstaendig angehoben |
| 0x66 | Spannbuegel findet Fangbereich nicht |
| 0x67 | Windlauf faehrt nicht auf |
| 0x68 | Windlauf faehrt nicht zu |
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

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x70 | Unterspannung an Klemme 30 |
| 0x71 | Ueberspannung an Klemme 30 |
| 0x72 | interne 5V-Versorgung ausserhalb Toleranz |
| 0x74 | keine ZKE-Antwort 'Tueren- / Klappenstatus' |
| 0x75 | Entriegeln Verdeckklappe nicht zurueckgemeldet |
| 0x76 | Verriegeln Verdeckklappe nicht zurueckgemeldet |
| 0x77 | Absenken Seitenscheiben nicht zurueckgemeldet |
| 0x78 | Anheben Seitenscheiben nicht zurueckgemeldet |
| 0x79 | kein Fahrstatus erhalten ,vom Kombi |
| 0x7A | Verdeckstecker nicht gesteckt |
| 0x7B | Hardwarefehler |
| 0x7C | unbekannte Verdeckstellung |
| 0x80 | keine Aussentemperatur erhalten |
| 0xFF | unbekannter Fehlerort |

<a id="table-vtemp"></a>
### VTEMP

Dimensions: 256 rows × 2 columns

| WERT | TEMP |
| --- | --- |
| 0x00 | 200 |
| 0x01 | 200 |
| 0x02 | 200 |
| 0x03 | 200 |
| 0x04 | 200 |
| 0x05 | 200 |
| 0x06 | 200 |
| 0x07 | 200 |
| 0x08 | 200 |
| 0x09 | 200 |
| 0x0A | 200 |
| 0x0B | 200 |
| 0x0C | 200 |
| 0x0D | 200 |
| 0x0E | 200 |
| 0x0F | 200 |
| 0x10 | 200 |
| 0x11 | 200 |
| 0x12 | 182 |
| 0x13 | 180 |
| 0x14 | 176 |
| 0x15 | 174 |
| 0x16 | 172 |
| 0x17 | 169 |
| 0x18 | 166 |
| 0x19 | 164 |
| 0x1A | 162 |
| 0x1B | 161 |
| 0x1C | 159 |
| 0x1D | 157 |
| 0x1E | 155 |
| 0x1F | 153 |
| 0x20 | 152 |
| 0x21 | 151 |
| 0x22 | 150 |
| 0x23 | 148 |
| 0x24 | 147 |
| 0x25 | 145 |
| 0x26 | 144 |
| 0x27 | 143 |
| 0x28 | 142 |
| 0x29 | 141 |
| 0x2A | 140 |
| 0x2B | 139 |
| 0x2C | 137 |
| 0x2D | 136 |
| 0x2E | 135 |
| 0x2F | 134 |
| 0x30 | 132 |
| 0x31 | 131 |
| 0x32 | 131 |
| 0x33 | 130 |
| 0x34 | 129 |
| 0x35 | 128 |
| 0x36 | 127 |
| 0x37 | 126 |
| 0x38 | 125 |
| 0x39 | 124 |
| 0x3A | 123 |
| 0x3B | 122 |
| 0x3C | 121 |
| 0x3D | 121 |
| 0x3E | 120 |
| 0x3F | 120 |
| 0x40 | 119 |
| 0x41 | 118 |
| 0x42 | 117 |
| 0x43 | 116 |
| 0x44 | 115 |
| 0x45 | 115 |
| 0x46 | 114 |
| 0x47 | 114 |
| 0x48 | 113 |
| 0x49 | 112 |
| 0x4A | 111 |
| 0x4B | 111 |
| 0x4C | 110 |
| 0x4D | 110 |
| 0x4E | 109 |
| 0x4F | 108 |
| 0x50 | 107 |
| 0x51 | 106 |
| 0x52 | 106 |
| 0x53 | 105 |
| 0x54 | 104 |
| 0x55 | 104 |
| 0x56 | 103 |
| 0x57 | 102 |
| 0x58 | 102 |
| 0x59 | 101 |
| 0x5A | 101 |
| 0x5B | 100 |
| 0x5C | 100 |
| 0x5D | 99 |
| 0x5E | 99 |
| 0x5F | 98 |
| 0x60 | 98 |
| 0x61 | 97 |
| 0x62 | 96 |
| 0x63 | 96 |
| 0x64 | 95 |
| 0x65 | 95 |
| 0x66 | 94 |
| 0x67 | 94 |
| 0x68 | 93 |
| 0x69 | 92 |
| 0x6A | 92 |
| 0x6B | 91 |
| 0x6C | 90 |
| 0x6D | 90 |
| 0x6E | 89 |
| 0x6F | 89 |
| 0x70 | 88 |
| 0x71 | 88 |
| 0x72 | 87 |
| 0x73 | 86 |
| 0x74 | 86 |
| 0x75 | 85 |
| 0x76 | 85 |
| 0x77 | 85 |
| 0x78 | 84 |
| 0x79 | 83 |
| 0x7A | 83 |
| 0x7B | 82 |
| 0x7C | 82 |
| 0x7D | 81 |
| 0x7E | 81 |
| 0x7F | 81 |
| 0x80 | 80 |
| 0x81 | 79 |
| 0x82 | 79 |
| 0x83 | 79 |
| 0x84 | 78 |
| 0x85 | 77 |
| 0x86 | 77 |
| 0x87 | 76 |
| 0x88 | 76 |
| 0x89 | 75 |
| 0x8A | 75 |
| 0x8B | 74 |
| 0x8C | 74 |
| 0x8D | 73 |
| 0x8E | 73 |
| 0x8F | 72 |
| 0x90 | 72 |
| 0x91 | 71 |
| 0x92 | 71 |
| 0x93 | 71 |
| 0x94 | 70 |
| 0x95 | 70 |
| 0x96 | 69 |
| 0x97 | 69 |
| 0x98 | 68 |
| 0x99 | 68 |
| 0x9A | 67 |
| 0x9B | 67 |
| 0x9C | 66 |
| 0x9D | 66 |
| 0x9E | 65 |
| 0x9F | 65 |
| 0xA0 | 65 |
| 0xA1 | 64 |
| 0xA2 | 64 |
| 0xA3 | 63 |
| 0xA4 | 63 |
| 0xA5 | 62 |
| 0xA6 | 62 |
| 0xA7 | 61 |
| 0xA8 | 60 |
| 0xA9 | 60 |
| 0xAA | 59 |
| 0xAB | 59 |
| 0xAC | 58 |
| 0xAD | 58 |
| 0xAE | 58 |
| 0xAF | 57 |
| 0xB0 | 56 |
| 0xB1 | 56 |
| 0xB2 | 55 |
| 0xB3 | 55 |
| 0xB4 | 54 |
| 0xB5 | 54 |
| 0xB6 | 53 |
| 0xB7 | 53 |
| 0xB8 | 52 |
| 0xB9 | 52 |
| 0xBA | 51 |
| 0xBB | 50 |
| 0xBC | 50 |
| 0xBD | 50 |
| 0xBE | 49 |
| 0xBF | 48 |
| 0xC0 | 48 |
| 0xC1 | 47 |
| 0xC2 | 47 |
| 0xC3 | 46 |
| 0xC4 | 46 |
| 0xC5 | 45 |
| 0xC6 | 44 |
| 0xC7 | 44 |
| 0xC8 | 43 |
| 0xC9 | 42 |
| 0xCA | 42 |
| 0xCB | 41 |
| 0xCC | 40 |
| 0xCD | 40 |
| 0xCE | 39 |
| 0xCF | 38 |
| 0xD0 | 37 |
| 0xD1 | 37 |
| 0xD2 | 36 |
| 0xD3 | 35 |
| 0xD4 | 35 |
| 0xD5 | 34 |
| 0xD6 | 34 |
| 0xD7 | 33 |
| 0xD8 | 32 |
| 0xD9 | 31 |
| 0xDA | 30 |
| 0xDB | 30 |
| 0xDC | 29 |
| 0xDD | 28 |
| 0xDE | 27 |
| 0xDF | 26 |
| 0xE0 | 25 |
| 0xE1 | 25 |
| 0xE2 | 24 |
| 0xE3 | 23 |
| 0xE4 | 23 |
| 0xE5 | 22 |
| 0xE6 | 21 |
| 0xE7 | 20 |
| 0xE8 | 19 |
| 0xE9 | 18 |
| 0xEA | 17 |
| 0xEB | 16 |
| 0xEC | 15 |
| 0xED | 15 |
| 0xEE | 14 |
| 0xEF | 13 |
| 0xF0 | 12 |
| 0xF1 | 11 |
| 0xF2 | 10 |
| 0xF3 | 10 |
| 0xF4 | 9 |
| 0xF5 | 9 |
| 0xF6 | 8 |
| 0xF7 | 7 |
| 0xF8 | 6 |
| 0xF9 | 5 |
| 0xFA | 5 |
| 0xFB | 4 |
| 0xFC | 3 |
| 0xFD | 2 |
| 0xFE | 1 |
| 0xFF | 0 |

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

Dimensions: 10 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| VENTIL1 | 1 | 0x01 |
| VENTIL2 | 1 | 0x02 |
| VENTIL3 | 1 | 0x04 |
| VENTIL4 | 1 | 0x08 |
| VENTIL5 | 1 | 0x10 |
| PUMPE | 1 | 0x20 |
| HHS | 1 | 0x40 |
| AUF | 3 | 0x01 |
| ZU | 3 | 0x02 |
| XXX | Y | Z |

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
