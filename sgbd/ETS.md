# ETS.prg

- Jobs: [19](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronischer Trennschalter |
| ORIGIN | BMW TP-421 Winkler H.-J. |
| REVISION | 1.00 |
| AUTHOR | BMW TP-421 Winkler H.-J. |
| COMMENT | Vorversion |
| PACKAGE | 1.26 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer ETS automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten fuer ETS
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Speichers
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Lesen der Codierdaten
- [CODIERDATEN_SCHREIBEN](#job-codierdaten-schreiben) - Schreiben der Codierdaten
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - Lesen der Digitalwerte
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Lesen der Analogwerte
- [STEUERN_DIGITAL](#job-steuern-digital) - Vorgeben eines Statuswertes (1 Signal)
- [ZYKLENZAEHLER_SCHREIBEN](#job-zyklenzaehler-schreiben) - Zaehlerstand des Zyklenzaehlers vorgeben
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [MODUL_INAKTIV](#job-modul-inaktiv) - Setzt das Modul temporaer inaktiv
- [MODUL_AKTIV](#job-modul-aktiv) - Setzt das Modul wieder aktiv
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
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

Initialisierung / Kommunikationsparameter fuer ETS automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ETS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table "JobResult" "STATUS_TEXT" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FEHLER_ANZAHL | int | Anzahl der Fehlerspeichereintraege |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 32 |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN | binary | ausgelesene Hex-Daten |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| WERT | int | Zu speicherder Wert Bereich: 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Lesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN | binary | Ausgelesene Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-schreiben"></a>
### CODIERDATEN_SCHREIBEN

Schreiben der Codierdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | Zu speichernde Daten (16 Byte, Bereich 0x00-0xFF), die einzelnen Bytes muessen durch Komma getrennt sein. Beispiel: "1,2,03,0x04,0x05..." |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

Lesen der Digitalwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| STAT_BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| STAT_BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| STAT_DIG_TEST | int | Start des Abgleichvorganges: 0 oder 1 SG-interner Status Bit 0 von STAT_BYTE1 |
| STAT_DIG_ZSK | int | Zuendschluesselkontakt: 0 oder 1 (= geschlossen) Bit 1 von STAT_BYTE1 |
| STAT_DIG_S_NOT | int | Schalter Notbetrieb: 0 oder 1 (= geschlossen) Bit 2 von STAT_BYTE1 |
| STAT_DIG_KBSTAT | int | K-Bus Status von BusIC: 0 oder 1 SG-interner Status Bit 3 von STAT_BYTE1 |
| STAT_DIG_E_KAT | int | E-Kat wird geheizt: 0 oder 1 (= geheizt) Bit 4 von STAT_BYTE1 |
| STAT_DIG_TD | int | Statischer Pegel Drehzahlsignal: 0 oder 1 (= liegt auf Masse) Bit 7 von STAT_BYTE1 |
| STAT_DIG_ST_ETS | int | Status Trennschalter: 0 oder 1 (= geschlossen) Bit 0 von STAT_BYTE2 |
| STAT_DIG_OSZ_EIN | int | Oszillator ein: 0 oder 1 SG-interner Status Bit 1 von STAT_BYTE2 |
| STAT_DIG_T_1 | int | SG-interner Status: 0 oder 1 Bit 2 von STAT_BYTE2 |
| STAT_DIG_T_3 | int | SG-interner Status: 0 oder 1 Bit 3 von STAT_BYTE2 |
| STAT_DIG_LP_OP_EIN | int | Ladungspumpe/OP-Versorgung ein: 0 oder 1 SG-interner Status Bit 4 von STAT_BYTE2 |
| STAT_DIG_S_EIN | int | Pullup fuer S_NOT/ZSK ein: 0 oder 1 SG-interner Status Bit 5 von STAT_BYTE2 |
| STAT_DIG_T_4 | int | SG-interner Status: 0 oder 1 Bit 6 von STAT_BYTE2 |
| STAT_DIG_DIAGMODE | int | Diagnosemode ein: 0 oder 1 (= Diagnosemode) Bit 0 von STAT_BYTE3 |
| STAT_DIG_MESSBEREICH | int | Messbereich fuer kleine Stroeme aktiv: 0 oder 1 (= aktiv) Bit 1 von STAT_BYTE3 |
| STAT_DIG_SWITCH | int | Trennschalter ein, geschuetzter Betrieb: 0 oder 1 (= ein, Batterien parallel) Bit 2 von STAT_BYTE3 |
| STAT_DIG_KL15 | int | KL.15 (HW oder K-Bus) ein: 0 oder 1 (= ein) Bit 3 von STAT_BYTE3 |
| STAT_DIG_KL15_HW | int | Kl.15 ueber Hardware ein: 0 oder 1 (= ein) Bit 4 von STAT_BYTE3 |
| STAT_DIG_MOTOR_ON | int | Motor laeuft: 0 oder 1 (=laeuft) Bit 7 von STAT_BYTE3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Lesen der Analogwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANA_UB_NTC_WERT | real | Versorgung Temperaturmessschaltung |
| STAT_ANA_UB_NTC_EINH | string | Einheit von Versorgung Temperaturmessschaltung |
| STAT_ANA_U_NTC_WERT | real | Spannung am Temperaturfuehler |
| STAT_ANA_U_NTC_EINH | string | Einheit von Spannung am Temperaturfuehler |
| STAT_ANA_U_MESS_G_WERT | real | Stromesswert grob |
| STAT_ANA_U_MESS_G_EINH | string | Einheit von Stromesswert grob |
| STAT_ANA_U_MESS_F_WERT | real | Stromesswert fein |
| STAT_ANA_U_MESS_F_EINH | string | Einheit von Stromesswert fein |
| STAT_ANA_U_KL15_WERT | real | Spannung KL15 Hardware |
| STAT_ANA_U_KL15_EINH | string | Einheit von Spannung KL15 Hardware |
| STAT_ANA_U_OP_WERT | real | Versorgung Messverstaerker |
| STAT_ANA_U_OP_EINH | string | Einheit von Versorgung Messverstaerker |
| STAT_ANA_U_BB_WERT | real | Spannung Bordbatterie |
| STAT_ANA_U_BB_EINH | string | Einheit von Spannung Bordbatterie |
| STAT_ANA_U_SB_WERT | real | Spannung Starterbatterie |
| STAT_ANA_U_SB_EINH | string | Einheit von Spannung Starterbatterie |
| STAT_ANA_R_DSON_WERT | real | Widerstand Halbleiterschalter |
| STAT_ANA_R_DSON_EINH | string | Einheit von Widerstand Halbleiterschalter |
| STAT_ANA_DREHZAHL_WERT | real | Drehzahl Hardware |
| STAT_ANA_DREHZAHL_EINH | string | Einheit von Drehzahl Hardware |
| STAT_ANA_TEMP_WERT | real | Temperatur Halbleiterschalter |
| STAT_ANA_TEMP_EINH | string | Einheit von Temperatur Halbleiterschalter |
| STAT_ANA_STROM_WERT | real | Strom ueber Halbleiterschalter |
| STAT_ANA_STROM_EINH | string | Einheit von Strom ueber Halbleiterschalter |
| STAT_ANA_SLOW_STROM_WERT | real | Mittlerer Strom ueber Halbleiterschalter |
| STAT_ANA_SLOW_STROM_EINH | string | Einheit von Mittlerer Strom ueber Halbleiterschalter |
| STAT_ANA_U_BB_SLOW_WERT | real | Mittlere Spannung Bordbatterie Ab SW-Stand 2.0 liefert SG immer den Wert Null |
| STAT_ANA_U_BB_SLOW_EINH | string | Einheit von Mittlere Spannung Bordbatterie |
| STAT_ANA_U_SB_SLOW_WERT | real | Mittlere Spannung Starterbatterie Ab SW-Stand 2.0 liefert SG immer den Wert Null |
| STAT_ANA_U_SB_SLOW_EINH | string | Einheit von Mittlere Spannung Starterbatterie |
| STAT_ANA_DREHZAHL_KB_WERT | real | Drehzahl K-Bus |
| STAT_ANA_DREHZAHL_KB_EINH | string | Einheit von Drehzahl K-Bus |
| STAT_ANA_ZYKLENZAEHLER_WERT | long | Zaehler der E-Kat-Zyklen |
| STAT_ANA_ZYKLENZAEHLER_EINH | string | Einheit von Zaehler der E-Kat-Zyklen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Vorgeben eines Statuswertes (1 Signal)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZELLE | int | Zellennummer (0-2 oder 4 oder 7-14 oder 16-20 oder 23) |
| WERT | int | Zu speichernder Wert (0 oder 1) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-zyklenzaehler-schreiben"></a>
### ZYKLENZAEHLER_SCHREIBEN

Zaehlerstand des Zyklenzaehlers vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | long | Zaehlerstand Bereich: 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-modul-inaktiv"></a>
### MODUL_INAKTIV

Setzt das Modul temporaer inaktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-modul-aktiv"></a>
### MODUL_AKTIV

Setzt das Modul wieder aktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)
- [FORTTEXTE](#table-forttexte) (20 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
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
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 20 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Interner Fehler: Interne Spannung |
| 0x01 | Interner Fehler: Ladungspumpe nicht abschaltbar |
| 0x10 | Interner Fehler: Prozessor Watchdog |
| 0x11 | Interner Fehler: Prozessor ROM |
| 0x12 | Interner Fehler: Taktgeber |
| 0x13 | Interner Fehler: Temperaturueberwachung defekt |
| 0x14 | Interner Fehler: EEPROM |
| 0x15 | Interner Fehler: Abgleichdaten fehlen |
| 0x16 | Interner Fehler: Codierdaten fehlen |
| 0x02 | Externer Fehler: Kl.15 Kurzschluss |
| 0x03 | Externer Fehler: Drehzahlsiganl am Eingang TD fehlt |
| 0x04 | Externer Fehler: E_KAT_EIN Masseschluss |
| 0x05 | Externer Fehler: Ueberspannung Starterbatterie |
| 0x17 | Externer Fehler: Generatorspannung zu niedrig |
| 0x18 | Externer Fehler: ZSK Kurzschluss |
| 0x19 | Externer Fehler: Stuetzen der Bordbatterie im Startbetrieb |
| 0x19 | Externer Fehler: Stuetzen der Bordbatterie im Fahrbetrieb |
| 0x1B | Externer Fehler: Batterien oder Modul wurden abgeklemmt |
| 0x1C | Externer Fehler: K-Bus- oder Kombisignal fehlt |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |
