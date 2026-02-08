# RLS_DS2.prg

- Jobs: [20](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Regen-/Fahrlichtsensor für DS2 |
| ORIGIN | BMW TI-430 Stübinger |
| REVISION | 1.04 |
| AUTHOR | KOSTAL AEK7 D.HAASE, BMW EE-201 Haas, BMW TI-431 Küssel |
| COMMENT | Serien-Version |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Sonder-Konzept (NICHT nach Lastenheft Codierung/Diagnose)
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden (DUMMY-Job)
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des internen Speichers
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten schreiben und verifizieren
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [AIC_INIT](#job-aic-init) - Initialisieren des Regensensors
- [STATUS_LESEN](#job-status-lesen) - Stati des Regensensors
- [STATUS_LESEN_VERSTAERKUNG](#job-status-lesen-verstaerkung) - Status Verstärkung des Regensensors
- [STATUS_LESEN_LICHT](#job-status-lesen-licht) - Status Verstärkung des Regensensors
- [STATUS_LESEN_MESSSTRECKEN](#job-status-lesen-messstrecken) - Streckensignale
- [STATUS_LESEN_HEIZUNG](#job-status-lesen-heizung) - Signal in dig

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
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Sonder-Konzept (NICHT nach Lastenheft Codierung/Diagnose)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit insbesondere fuer Fehlerort 3 bzw. 4 Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden (DUMMY-Job)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer OKAY |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZELLE | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE | binary | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| ZELLE | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-c-s-lesen"></a>
### C_S_LESEN

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-auftrag"></a>
### C_S_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-aic-init"></a>
### AIC_INIT

Initialisieren des Regensensors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Stati des Regensensors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RSK | int | Bit 0 = 1 wenn E46 Polarität Bit 7 = 1 wenn Polarität eingeschrieben |
| STAT_RSK_EINH | string | Digits |
| STAT_STRECKE_I1 | int | Stromwert der 1. Strecke in Dig Bereich 1 - 254 Dig |
| VERST_BEREICH | int | 0, wenn unterer Bereich 1, wenn hoher Bereich |
| VERST_BEREICH_EINH | string | Digits |
| STAT_UEBERWISCHZEITPUNKT_1 | int | Bereich: 0 bis 255 |
| STAT_UEBERWISCHZEITPUNKT_2 | int | Bereich: 0 bis 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-verstaerkung"></a>
### STATUS_LESEN_VERSTAERKUNG

Status Verstärkung des Regensensors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| stat_v_wert | int | Grundverstärkungsfaktor untere Stufe = 0 (kleine Verstärkung) obere Stufe  = 1 (große Verstärlung ) |
| stat_v_einh | string | Digits |
| stat_i1_wert | int | Sendestrom für die Strecke1 Bereich  : 0 bis 254 Grundverstärkungsfaktor 0 : Wert zwischen 10 und 254 Digits zulässig Grundverstärkungsfaktor 1 : Wert zwischen 10 und 200 Digits zulässig |
| stat_i1_einh | string | Digits |
| stat_i1_wert_gueltig | int | 1 für v_wert 0 und i1_wert zwischen 10 und 254 1 für v_wert 1 und i1_wert zwischen 10 und 200 0 wenn ungültig |
| stat_i2_wert | int | Sendestrom für die Strecke2 Bereich  : 0 bis 254 Grundverstärkungsfaktor 0 : Wert zwischen 10 und 254 Digits zulässig Grundverstärkungsfaktor 1 : Wert zwischen 10 und 200 Digits zulässig |
| stat_i2_einh | string | Digits |
| stat_i3_wert | int | Sendestrom für die Strecke3 Bereich  : 0 bis 254 Grundverstärkungsfaktor 0 : Wert zwischen 10 und 254 Digits zulässig Grundverstärkungsfaktor 1 : Wert zwischen 10 und 200 Digits zulässig |
| stat_i3_einh | string | Digits |
| stat_i4_wert | int | Sendestrom für die Strecke4 Bereich  : 0 bis 254 Grundverstärkungsfaktor 0 : Wert zwischen 10 und 254 Digits zulässig Grundverstärkungsfaktor 1 : Wert zwischen 10 und 200 Digits zulässig |
| stat_i4_einh | string | Digits |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-licht"></a>
### STATUS_LESEN_LICHT

Status Verstärkung des Regensensors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| stat_umli_wert | int | Umgebungslicht ungefiltert Bereich : 0 bis 255 |
| stat_umli_einh | string | Digits |
| stat_umlifilt_wert | int | Umgebungslicht gefiltert Bereich : 0 bis 255 |
| stat_umlifilt_einh | string | Digits |
| stat_froli_wert | int | Frontlicht ungefiltert Bereich : 0 bis 255 |
| stat_froli_einh | string | Digits |
| stat_frolifilt_wert | int | Frontlicht gefiltert Bereich : 0 bis 255 |
| stat_frolifilt_einh | string | Digits |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-messstrecken"></a>
### STATUS_LESEN_MESSSTRECKEN

Streckensignale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| stat_mess1_wert | int | gefilterte Messignalwert Strecke 1 Bereich: 150 bis 180 bei sauberer, trockener Scheibe |
| stat_mess1_einh | string | Digits |
| stat_mess2_wert | int | gefilterte Messignalwert Strecke 2 Bereich: 150 bis 180 bei sauberer, trockener Scheibe |
| stat_mess2_einh | string | Digits |
| stat_mess3_wert | int | gefilterte Messignalwert Strecke 3 Bereich: 150 bis 180 bei sauberer, trockener Scheibe |
| stat_mess3_einh | string | Digits |
| stat_mess4_wert | int | gefilterte Messignalwert Strecke 4 Bereich: 150 bis 180 bei sauberer, trockener Scheibe |
| stat_mess4_einh | string | Digits |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-heizung"></a>
### STATUS_LESEN_HEIZUNG

Signal in dig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| stat_heiztemp_wert | int | Heizungstemperatur typischer Wert im eingeschwungenen Zustand : 120 Digits |
| stat_heiztemp_einh | string | °C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (17 × 2)

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

Dimensions: 76 rows × 2 columns

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
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
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

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x10 | Licht Hardwarefehler |
| 0x20 | Sensor ist noch nicht codiert! |
| 0x30 | Fehler Lichtsensor |
| 0x40 | Keine optische Initialisierung möglich |
| 0x50 | Fehler optische Initialisierung und LichtHW |
| 0x60 | Fehler optische Initialisierung und nicht codiert! |
| 0x70 | Fehler optische Initialisierung und Lichtfehler |
| 0x80 | Hardwarefehler |
| 0x90 | Hardwarefehler und Lichthardwarefehler |
| 0xa0 | Hardwarefehler und nicht codiert! |
| 0xb0 | Hardwarefehler und Lichtplausibilitäts/hardwarefehler |
| 0xc0 | keine optische Init und Hardwarefehler |
| 0xd0 | Hardwarefehler Initialisierungsfehler Lichthardwarefehler |
| 0xe0 | Hardwarefehler Initialisierungsfehler Codierfehler |
| 0xf0 | Hardwarefehler Initialisierungsfehler Lichtfehler |
| 0xXY | Fehlerkombination |
