# EKP2DS2.prg

- Jobs: [25](#jobs)
- Tables: [12](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EKPM2 |
| ORIGIN | BMW EF61 Schönherr |
| REVISION | 1.000 |
| AUTHOR | Helbako GmbH ES Gerd Meyering |
| COMMENT | N/A |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete Reset ausloesen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob
- [STATUS_MESSWERTE](#job-status-messwerte) - es werden die Messwerte des AD-Umsetzers ausgelesen
- [STATUS_REGELUNGSWERTE](#job-status-regelungswerte) - es werden die Regelungsdaten gelesen
- [STEUERN_FOERDERMENGE](#job-steuern-foerdermenge)
- [STEUERN_PWM_VORGEBEN](#job-steuern-pwm-vorgeben)
- [STATUS_SOLL_IST](#job-status-soll-ist)
- [STATUS_EINREGELZEIT](#job-status-einregelzeit) - die Einregelzeit wird gelesen
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [IS_LESEN](#job-is-lesen) - fs_lesen job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [SET_NULL_CODIERUNG](#job-set-null-codierung) - Codierung in den Auslieferungszustand (ID=0)

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete Reset ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | die letzten vier Stellen der Fahrgestellnummer |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

es werden die Messwerte des AD-Umsetzers ausgelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_UEBER_HIGHSIDE_WERT | real | Uebertemperatur des Highside-Treibers |
| STAT_TEMP_UEBER_HIGHSIDE_EINH | string |  |
| STAT_TEMP_UEBER_LOWSIDE_WERT | real | Uebertemperatur des Lowside-Treibers |
| STAT_TEMP_UEBER_LOWSIDE_EINH | string |  |
| STAT_MOTORSPANNUNG_WERT | real | Spannung am Pumpenmotor |
| STAT_MOTORSPANNUNG_EINH | string |  |
| STAT_MOTORSTROM_WERT | real | Stromfluss durch Pumpenmotor |
| STAT_MOTORSTROM_EINH | string |  |
| STAT_SPANNUNG_KL30_WERT | real | Spannung an Klemme 30 |
| STAT_SPANNUNG_KL30_EINH | string |  |
| STAT_SPANNUNG_KL15_WERT | real | Spannung an Klemme 15 |
| STAT_SPANNUNG_KL15_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-regelungswerte"></a>
### STATUS_REGELUNGSWERTE

es werden die Regelungsdaten gelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTUELLE_DREHZAHL_WERT | int | Ist-Drehzahl des Motors |
| STAT_AKTUELLE_DREHZAHL_EINH | string |  |
| STAT_SOLL_FOERDERMENGE_WERT | int | Soll-Foerdermenge der Pumpe |
| STAT_SOLL_FOERDERMENGE_EINH | string |  |
| STAT_SOLL_DREHZAHL_WERT | int | Soll-Drehzahl des Pumpenmotors |
| STAT_SOLL_DREHZAHL_EINH | string |  |
| STAT_PWM_REGISTER_WERT | int | Wert des SFR-Registers in der CPU zur PWM-Vorgabe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-foerdermenge"></a>
### STEUERN_FOERDERMENGE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLLFOERDERMENGE | int | Wert der vorzugebenden Soll-Foerdermenge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-pwm-vorgeben"></a>
### STEUERN_PWM_VORGEBEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLL_PWM | int | Wert der vorzugebenden Soll-PWM 0%...100% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-soll-ist"></a>
### STATUS_SOLL_IST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VORGABE_SOLLFOERDERMENGE | int | Wert der vorzugebenden Soll-Foerdermenge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLFOERDERMENGE_WERT | int | zurueckgelesene Sollfoerdermenge, sollte gleich Vorgabe sein |
| STAT_SOLLFOERDERMENGE_EINH | string |  |
| STAT_SOLLDREHZAHL_WERT | int | Drehzahl, die sich aus Soll-Foerdermenge ergibt |
| STAT_SOLLDREHZAHL_EINH | string |  |
| STAT_ISTDREHZAHL_WERT | int | tatsaechliche EKP-Drehzahl |
| STAT_ISTDREHZAHL_EINH | string |  |
| STAT_DELTA_DREHZAHL_WERT | long | Soll-Drehzahl minus Ist-Drehzahl |
| STAT_DELTA_DREHZAHL_EINH | string |  |
| JOB_STATUS | string |  |

<a id="job-status-einregelzeit"></a>
### STATUS_EINREGELZEIT

die Einregelzeit wird gelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EINREGELZEIT_WERT | unsigned int | Wert der Einregelzeit |
| STAT_EINREGELZEIT_EINH | string |  |
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
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier 9 |
| F_UW1_NR | int | Index der Umweltbedingung 1 |
| F_UW1_TEXT | string | Spannung KL30 |
| F_UW1_WERT | real | Wert der Spannung an KL30 |
| F_UW1_EINH | string | Einheit V |
| F_UW2_NR | int | Index der Umweltbedingung 2 |
| F_UW2_TEXT | string | Sollfoerdermenge |
| F_UW2_WERT | int | Wert der Sollfoerdermenge |
| F_UW2_EINH | string | Einheit l/h |
| F_UW3_NR | int | Index der Umweltbedingung 3 |
| F_UW3_TEXT | string | Kilometerstand |
| F_UW3_WERT | long | Wert des Kilometerstandes |
| F_UW3_EINH | string | Einheit km |
| F_UW4_NR | int | Index der Umweltbedingung 4 |
| F_UW4_TEXT | string | Fahrzeuggeschwindigkeit |
| F_UW4_WERT | long | Wert der Fahrzeuggeschwindigkeit |
| F_UW4_EINH | string | Einheit km/h |
| F_UW5_NR | int | Index der Umweltbedingung 5 |
| F_UW5_TEXT | string | FZG-Motordrehzahl |
| F_UW5_WERT | long | Wert der FZG-Motordrehzahl |
| F_UW5_EINH | string | Einheit 1/min |
| F_UW6_NR | int | Index der Umweltbedingung 6 |
| F_UW6_TEXT | string | Aussentemperatur |
| F_UW6_WERT | long | Wert der Aussentemperatur |
| F_UW6_EINH | string | Einheit °C |
| F_UW7_NR | int | Index der Umweltbedingung 7 |
| F_UW7_TEXT | string | Motorspannung EKP |
| F_UW7_WERT | long | Wert der Motorspannung EKP |
| F_UW7_EINH | string | Einheit V |
| F_UW8_NR | int | Index der Umweltbedingung 8 |
| F_UW8_TEXT | string | Motorstrom EKP |
| F_UW8_WERT | long | Wert des Motorstroms EKP |
| F_UW8_EINH | string | Einheit A |
| F_UW9_NR | int | Index der Umweltbedingung 9 |
| F_UW9_TEXT | string | Drehzahl der EKP |
| F_UW9_WERT | long | Wert der Drehzahl der EKP |
| F_UW9_EINH | string | Einheit 1/min |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-is-lesen"></a>
### IS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier 9 |
| F_UW1_NR | int | Index der Umweltbedingung 1 |
| F_UW1_TEXT | string | Spannung KL30 |
| F_UW1_WERT | real | Wert der Spannung an KL30 |
| F_UW1_EINH | string | Einheit V |
| F_UW2_NR | int | Index der Umweltbedingung 2 |
| F_UW2_TEXT | string | Sollfoerdermenge |
| F_UW2_WERT | int | Wert der Sollfoerdermenge |
| F_UW2_EINH | string | Einheit l/h |
| F_UW3_NR | int | Index der Umweltbedingung 3 |
| F_UW3_TEXT | string | Kilometerstand |
| F_UW3_WERT | long | Wert des Kilometerstandes |
| F_UW3_EINH | string | Einheit km |
| F_UW4_NR | int | Index der Umweltbedingung 4 |
| F_UW4_TEXT | string | Fahrzeuggeschwindigkeit |
| F_UW4_WERT | long | Wert der Fahrzeuggeschwindigkeit |
| F_UW4_EINH | string | Einheit km/h |
| F_UW5_NR | int | Index der Umweltbedingung 5 |
| F_UW5_TEXT | string | FZG-Motordrehzahl |
| F_UW5_WERT | long | Wert der FZG-Motordrehzahl |
| F_UW5_EINH | string | Einheit 1/min |
| F_UW6_NR | int | Index der Umweltbedingung 6 |
| F_UW6_TEXT | string | Aussentemperatur |
| F_UW6_WERT | long | Wert der Aussentemperatur |
| F_UW6_EINH | string | Einheit °C |
| F_UW7_NR | int | Index der Umweltbedingung 7 |
| F_UW7_TEXT | string | Motorspannung EKP |
| F_UW7_WERT | long | Wert der Motorspannung EKP |
| F_UW7_EINH | string | Einheit V |
| F_UW8_NR | int | Index der Umweltbedingung 8 |
| F_UW8_TEXT | string | Motorstrom EKP |
| F_UW8_WERT | long | Wert des Motorstroms EKP |
| F_UW8_EINH | string | Einheit A |
| F_UW9_NR | int | Index der Umweltbedingung 9 |
| F_UW9_TEXT | string | Drehzahl der EKP |
| F_UW9_WERT | long | Wert der Drehzahl der EKP |
| F_UW9_EINH | string | Einheit 1/min |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNUMMER | int | zulaessige Blocknummern liegen i Bereich 0x0000 - 0x000B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Es werden jeweils die 16 Byte des angesprochenen Codierdatenblockes ausgegeben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

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

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-set-null-codierung"></a>
### SET_NULL_CODIERUNG

Codierung in den Auslieferungszustand (ID=0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (93 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (18 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (8 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 3)
- [FARTTEXTE](#table-farttexte) (3 × 2)

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

Dimensions: 93 rows × 2 columns

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
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
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
| F_UWB_ERW | ja |
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

Dimensions: 18 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x91 | EKP-Motor: Spannung zu hoch |
| 0x92 | EKP-Motor: Spannung zu niedrig |
| 0x93 | EKP-Motor: Strom zu hoch |
| 0x94 | EKP-Motor: Strom zu niedrig |
| 0x95 | EKP-Motor: Strom fehlt |
| 0x96 | EKP-Motor: Drehzahl fehlt |
| 0x97 | EKP-Motor: Drehzahl zu hoch |
| 0x98 | EKP-Motor: Drehzahl zu niedrig |
| 0x99 | Endstufe (high-side): Übertemperatur Stufe 2 |
| 0x9A | Endstufe (high-side): Übertemperatur Stufe 1 |
| 0x9B | Kodierdaten: Notlauf-Datensatz |
| 0x9C | EEPROM: CRC-Fehler |
| 0x9D | Kodierdaten: Nicht kodiert |
| 0x9E | Externer Fehler: CRASH/+Batterie-Abschaltung |
| 0x9F | ASIC: Abschaltung |
| 0xD4 | Externer Fehler: CAN-ID 0xAA (TORQUE_3) fehlt(e) |
| 0xC7 | Externer Fehler: CAN-Bus-Off |
| 0xFF | unbekannter Fehlecode |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 8 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA1 | KL_WakeUp: Spannung zu hoch |
| 0xA2 | KL_WakeUp: Fehlt |
| 0xA3 | KL30: Fehlt |
| 0xA4 | KL30: Spannung zu hoch |
| 0xA5 | EKP-Motor: Drehz. zu niedrig wg. KL30-Unterspann. |
| 0xA6 | Ext. Fehler: FLASHEN abgelehnt (Geschw./Motordrehz. nicht 0) |
| 0xA7 | ASIC: Warnung |
| 0xFF | unbekannter Infocode |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | --- | --- |
| 0x01 | Spannung KL30 | V |
| 0x02 | Sollfoerdermenge | l/h |
| 0x03 | Kilometerstand | km |
| 0x04 | Fahrzeuggeschwindigkeit | km/h |
| 0x05 | Motordrehzahl | 1/min |
| 0x06 | Aussentemperatur | °C |
| 0x07 | EKP Motorspannung | V |
| 0x08 | EKP Motorstrom | A |
| 0x09 | EKP Motordrehzahl | 1/min |
| 0xXY | unbekannte Umweltbedingung | --- |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |
