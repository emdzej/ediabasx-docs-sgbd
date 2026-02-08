# NAVIGAT.prg

- Jobs: [16](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Navigationsrechner |
| ORIGIN | BMW TP-422 Helmich |
| REVISION | 2.06 |
| AUTHOR | BMW TP-422 Helmich, BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Navigationsrechner
- [STATUS_LESEN](#job-status-lesen) - Spezielle Eingaenge lesen
- [IDENT](#job-ident) - Ident-Daten fuer Navigationsrechner
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High Konzept nach LH Codierung/Diagnose mit Umweltbeding
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SPEICHER_LESEN](#job-speicher-lesen) - "System Configuration lesen"
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - RDS und GPS Configuration schreiben
- [SELBSTTEST](#job-selbsttest) - Selbsttest Navigationsrechner
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen im Navigationsrechner
- [QUICK_ERASE](#job-quick-erase) - Fehlerspeicher loeschen ohne BUSY abzuwarten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [KALIBRIERUNG_LOESCHEN](#job-kalibrierung-loeschen) - Loeschen der Kalibrierung ds NAV-Systems
- [KALIBRIERUNG_LESEN](#job-kalibrierung-lesen) - Loeschen der Kalibrierung ds NAV-Systems

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

Init-Job Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Spezielle Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_RADSENSOR_LINKS_WERT | real | V-Wert in km/h |
| STAT_RADSENSOR_RECHTS_WERT | real | V-Wert in km/h |
| STAT_RADSENSOREN_EINH | string | km/h |
| STAT_COMPASS_A_WERT | int | Spannung in mV vom Kompass A gemessen |
| STAT_COMPASS_A_EINH | string | Spannung in mV vom Kompass A gemessen |
| STAT_COMPASS_B_WERT | int | Spannung in mV, vom Kompass B gemessen |
| STAT_COMPASS_B_EINH | string | Spannung in mV, vom Kompass B gemessen |
| STAT_DIFFERENZ_COMPASS_A_B_WERT | int | absolute Differenz-Spannung in mV, zwischen Kompass A und B |
| STAT_RUECKWAERTSGANG | int | Abfrage, ob Rueckwaertsgang eingelegt ist |
| STAT_CD_Auswurf_Taste | int | Status-Abfrage CD-Auswurf-Taste |
| STAT_GPS_STATUS_WERT | int | 1 n.i.O, &gt;1 bis 12 i.O. |
| STAT_GPS_DATA_OK | int | 0 n.i.O, 1 i.O. |
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
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |
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
| F_UW_ANZ | int | Ausgabe Anzahl der Umweltbedingen, hier 1 |
| F_ART1_NR | int | Index Fehlerart, 00 = nicht aktiv, hx40 = aktiv |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_UW1_NR | int | Ausgabe Fehlercode vom Shadowspeicher |
| F_UW1_TEXT | string | Ausgabe Fehlercode als Text |
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

"System Configuration lesen"

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| RDS_SPEZIFIKATION | string | Kennung, ob RDS benutzt wird oder nicht,"0" oder"R" |
| GPS_SPEZIFIKATION | string | Kennung, ob GPS angeschlossen ist und Welches 0: kein GPS, M: Magnavox GPS, T: Trimble GPS |
| _TEL_ANTWORT | binary | Antworttelegramm anzeigen |
| _TEL_ANZAHL | int | Anzahl der Telegramme anzeigen |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

RDS und GPS Configuration schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RDS_CONFIGURATION | string | Nach Telegrammspezifikation "0" oder "R" 0: ohne RDS, R: mit RDS |
| GPS_CONFIGURATION | string | Nach Telegrammspezifikation "0","M" oder "T" 0: ohne GPS, M: Magnavox, T: Trimble |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| _TEL_SENDE | binary | Telegramm anzeigen |

<a id="job-selbsttest"></a>
### SELBSTTEST

Selbsttest Navigationsrechner

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

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

<a id="job-kalibrierung-loeschen"></a>
### KALIBRIERUNG_LOESCHEN

Loeschen der Kalibrierung ds NAV-Systems

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| _TEL_ANTWORT | binary |  |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

<a id="job-kalibrierung-lesen"></a>
### KALIBRIERUNG_LESEN

Loeschen der Kalibrierung ds NAV-Systems

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| _TEL_ANTWORT | binary |  |
| STAT_KALIBRIERUNG_OK | int | Datenbyte 0 |
| STAT_SENSOR_INTERFACE_BOARD | string | Datenbyte 1 high nibble |
| STAT_R_GANG_CODIERUNG_HIGH | int | Datenbyte 1 low nibble |
| STAT_SCHALTER1_CODIERUNG_HIGH | int | Datenbyte 2 high nibble |
| STAT_SCHALTER2_CODIERUNG_HIGH | int | Datenbyte 2 low nibble |
| STAT_RADSENSOR_TYP | string | Datenbyte 3 high nibble |
| STAT_SENSOR_POSITION | string | Datenbyte 3 low nibble |
| STAT_SPURWEITE_WERT | int | Datenbytes 4+5 |
| STAT_SPURWEITE_EINH | string | in mm |
| STAT_RADSTAND_EINH | string | in mm |
| STAT_RADSTAND_WERT | int | Datenbytes 6+7 |
| STAT_DISTANZ_PRO_PULSE_WERT | real | Datenbytes 8+9 |
| STAT_DISTANZ_PRO_PULSE_EINH | string | cm |
| STAT_KORREKTURFAKTOR_LINKES_RAD | real | Datenbytes 10+11 absolut-Wert |
| STAT_KOMPASS_OFFSET_WERT | real | Datenbytes 12+13 |
| STAT_KOMPASS_OFFSET_EINH | string | Grad |
| STAT_X_VERSCHIEBUNG_KOMPASS_HW_WERT | int | Datenbytes 14+15 |
| STAT_Y_VERSCHIEBUNG_KOMPASS_HW_WERT | int | Datenbytes 16+17 |
| STAT_X_VERSCHIEBUNG_KOMPASS_HW_EINH | string | mm? |
| STAT_Y_VERSCHIEBUNG_KOMPASS_HW_EINH | string | mm?? |
| STAT_MAGNETISCHE_DEKLINATION_WERT | real | Datenbytes 18+19 |
| STAT_MAGNETISCHE_DEKLINATION_EINH | string | Grad |
| STAT_MAGNETISCHE_INTENSITAET_WERT | real | Datenbytes 20+21 |
| STAT_MAGNETISCHE_INTENSITAET_EINH | string | Datenbytes"nT" |
| STAT_X_KOORDINATE_MITTELPUNKT_WERT | real | Datenbytes 22+23 |
| STAT_X_KOORDINATE_MITTELPUNKT_EINH | string | mm? |
| STAT_Y_KOORDINATE_MITTELPUNKT_WERT | real | Datenbytes 24+25 |
| STAT_Y_KOORDINATE_MITTELPUNKT_EINH | string | mm?? |
| STAT_LAENGE_A_ACHSE_WERT | int | Datenbytes 26 |
| STAT_LAENGE_A_ACHSE_EINH | string | Datenbytes 27 |
| STAT_LAENGE_B_ACHSE_WERT | int | Datenbytes |
| STAT_LAENGE_B_ACHSE_EINH | string | ?? |
| STAT_X_VERSCHIEBUNG_HSS_WERT | real | Datenbytes 28+29 |
| STAT_X_VERSCHIEBUNG_HSS_EINH | string | ?? |
| STAT_Y_VERSCHIEBUNG_HSS_WERT | real | Datenbytes 30+31 |
| STAT_Y_VERSCHIEBUNG_HSS_EINH | string | ?? |
| _TEL_ANZAHL | int | Anzahl der gesendeten Telegramme |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (8 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (45 × 2)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 8 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x10 | Hardwarefehler im Navigationsrechner |
| 0x11 | Hardwarefehler im Kompass-System |
| 0x13 | Hardwarefehler im Radsensor-System |
| 0x14 | Temperatur im Navigationsrechner zu hoch |
| 0x15 | CD-Fehler |
| 0x16 | Fehler in der Navigations-Software |
| 0x17 | Kalibrierfehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x40 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 45 rows × 2 columns

| UWNR | UWTEXT |
| --- | --- |
| 0x00 | Kein Eintrag im Shadowspeicher |
| 0x60 | Rad-Sensor interface defekt |
| 0x61 | Hardwarefehler im Kompass-System |
| 0x64 | Fehler im GPS-Senor interface |
| 0x65 | Luefter ist defekt |
| 0x66 | Fehler beim Programmiern der EEPROMs durch die Spannungsvers. |
| 0x68 | 5V Versorgung fuer CD-player defekt |
| 0x69 | 5V Versorgung fuer NAV-Rechner defekt |
| 0x6A | 12V Versorgung fuer CD-player defekt |
| 0x6B | Spannungsversorgung fuer Sensor defekt |
| 0x6C | Temperatur im NAV-Rechner zu hoch |
| 0x70 | Temperatur im CD-player zu hoch |
| 0x71 | CD-player interner Fehler |
| 0x73 | Fehler im Boot-ROM |
| 0x74 | Fehler im DRAM |
| 0x75 | Fehler im FEPROM |
| 0x77 | Fehler im EEPROM |
| 0x78 | Fehler Vorwaerts-/Rueckwaertsgang Erkennung |
| 0x79 | Interner Fehler, kann ingnoriert werden |
| 0x7A | Interner Fehler, kann ingnoriert werden |
| 0x7B | GPS ein/aus Fehlfunktion |
| 0x7C | CD-player interner Fehler |
| 0x7D | CD-player interner Fehler |
| 0x7E | CD-player interner Fehler |
| 0x80 | Status Heckscheibenheizung falsch |
| 0x85 | Keine Impulse an beiden Raedern |
| 0x86 | Keine Impulse vom linken Rad |
| 0x87 | Keine Impulse vom rechten Rad |
| 0x89 | Negative Impulse vom linken Rad |
| 0x8A | Negative Impulse vom rechten Rad |
| 0x8B | Sensoranschluss falsch |
| 0x8C | Kompassanschluss falsch |
| 0x8D | Keine Linkskurve durchgefuehrt |
| 0x8E | Kompass ausserhalb Bereich |
| 0x8F | Kompass nahe am Grenzbereich |
| 0x95 | Zu wenig Messwerte |
| 0x96 | Zu wenig Messwerte in einigen Richtungen |
| 0x97 | Falsche Ellipsen-Achse |
| 0x98 | Falsche Ellipsen-Groesse |
| 0x99 | Zu viele gestoerte Messwerte |
| 0x9A | Alle Kompasswerte gleich |
| 0x9B | Alle Kompass X-Werte gleich |
| 0x9C | Alle Kompass Y-Werte gleich |
| 0x9F | Fahrgeschwindidkeit zu hoch |
| 0xFF | Unbekannter Fehler im Shadowspeicher |
