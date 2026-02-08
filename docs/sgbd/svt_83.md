# svt_83.prg

- Jobs: [27](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SVT E83 |
| ORIGIN | Helbako A. Spanner, Stefan Fleck, magnasteyr |
| REVISION | 1.01 |
| AUTHOR | HELBAKO E2 Spanner |
| COMMENT | SGBD fuer E83 Servotronic |
| PACKAGE | 0.11 |
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
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers der SVT Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [STATUS_IO_LESEN](#job-status-io-lesen) - es werden die Eingangs- und Ausgangsstati aus dem Steuergeraet gelesen Die Auflistung der Statusbits erfolgt von LSB nach MSB
- [STEUERN_WANDLERSTROM](#job-steuern-wandlerstrom) - Default ident job
- [RESET](#job-reset) - Steuergeraet in RESET-Zustand versetzen
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LOESCHEN](#job-fs-loeschen) - modifizierter Default-Job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [IDENT_ERWEITERT](#job-ident-erweitert) - Identdaten lesen
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreibzugriff auf einzelne RAM-Zellen Als Argumente wird die Adresse der zu aendernden Zelle sowie deren Soll-Inhalt uebergeben.
- [STATUS_SERIENNUMMER](#job-status-seriennummer) - Seriennummer des Moduls
- [STATUS_AD_WERTE](#job-status-ad-werte) - Register der AD-Umsetzer auslesen
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [STATUS_CPCBO](#job-status-cpcbo) - Meßwert der Stromplausibilisierung vor Wandlerbestromung
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers der SVT Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| ADRESSE | int | 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| TELEGRAMM | binary | das Anfragetelegramm |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

es werden die Eingangs- und Ausgangsstati aus dem Steuergeraet gelesen Die Auflistung der Statusbits erfolgt von LSB nach MSB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLSTROM_KENNLINIE_WERT | unsigned int | Wert des Sollstromes gemäß Kennlinie |
| STAT_SOLLSTROM_KENNLINIE_EINH | string | Einheit dieses Signals ist mA |
| STAT_SOLLSTROM_PT1_WERT | unsigned int | Wert der Sollstromes nach dem PT1-Sollwert Regler |
| STAT_SOLLSTROM_PT1_EINH | string | Einheit dieses Signals ist mA |
| STAT_ISTSTROM_WERT | unsigned int | Wert der Ist-Strom-Messung, umgerechnet in mA |
| STAT_ISTSTROM_EINH | string | Einheit dieses Signals ist mA |
| STAT_PWM_REGISTER_WERT | int | Wert des PWM-Registers |
| STAT_CAN_GESCHWINDIGKEIT_WERT | int | Geschwindigkeit, die vom CAN-Bus kommt |
| STAT_CAN_GESCHWINDIGKEIT_EINH | string | Einheit dieses Signals ist km/h |
| STAT_KENNLINIE_GESCHWINDIGKEIT_WERT | int | Geschwindigkeit mit der in der Kennlinie interpoliert wird |
| STAT_KENNLINIE_GESCHWINDIGKEIT_EINH | string | Einheit dieses Signals ist km/h |
| STAT_SPANNUNG_KLEMME_30_WERT | int | gemittelte Spannung an Klemme 30 |
| STAT_SPANNUNG_KLEMME_30_EINH | string | Einheit dieses Signals ist Volt |
| STAT_STATE_NUMMER_WERT | int | Nummer des aktuellen States in der State Maschine |
| STAT_FEHLER_LASTKREIS | int | aktiver Fehler im Lastkreis detektiert |
| STAT_UNTERSPANNUNG | int | Unterspannung aktiv |
| STAT_UEBERSPANNUNG | int | Überspannung aktiv |
| STAT_SPANNUNGSEINBRUCH | int | ELMOS 100.26 hat über Hardware Spannungseinbruch gemeldet |
| STAT_V_ERSATZWERT | int | Ersatzwertberechnung der Geschwindigkeit ist wegen zu großer Beschleunigung aktiv |
| STAT_KLEMME_R | int | Klemme R im Klemmenstatus-Telegramm ist gesetzt |
| STAT_KLEMME_15 | int | Klemme 15 im Klemmenstatus-Telegramm ist gesetzt |
| STAT_KLEMME_50 | int | Klemme 50 im Klemmenstatus-Telegramm ist gesetzt |
| STAT_STATUS_FLAGS2_WERT | int | Sammlung diverser  Statusflags |
| _TEL_ANTWORT | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-steuern-wandlerstrom"></a>
### STEUERN_WANDLERSTROM

Default ident job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_IN_PROZENT | unsigned char | PWM-Duty-Cycle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_ISTSTROM_WERT | unsigned int | Strom auf Grund der PWM-Vorgabe |
| STAT_ISTSTROM_EINH | string | Einheit des Stromes ist natürlich mA |
| _TEL_AUFTRAG | binary | Anfragetelegrammdaten |
| _TEL_ANTWORT | binary | Antworttelegrammdaten |

<a id="job-reset"></a>
### RESET

Steuergeraet in RESET-Zustand versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |
| TEL | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

modifizierter Default-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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
| F_ART1_TEXT | string | aktiv oder sporadisch |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string | weiterführende Informationen |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier 3 |
| F_UW1_NR | int | Index der Umweltbedingung 1 |
| F_UW1_TEXT | string | Kilometerstand |
| F_UW1_WERT | long | Wert des Kilometerstandes |
| F_UW1_EINH | string | Einheit km |
| F_UW2_NR | int | Index der Umweltbedingung 2 |
| F_UW2_TEXT | string | Spannung an Klemme 30 |
| F_UW2_WERT | real | Wert der Spannung an Klemme 30 |
| F_UW2_EINH | string | Einheit V |
| F_UW3_NR | int | Index der Umweltbedingung 3 |
| F_UW3_TEXT | string | Fahrzeuggeschwindigkeit |
| F_UW3_WERT | long | Wert der Fahrzeuggeschwindigkeit |
| F_UW3_EINH | string | Einheit km/h |
| F_ZAHL | int | Anzahl der Gesamtfehler |
| HELP | int |  |
| TEL | binary |  |

<a id="job-ident-erweitert"></a>
### IDENT_ERWEITERT

Identdaten lesen

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
| ID_CAN_INDEX | int | Can-Index |
| ID_AI | int | Änderungsindex |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Schreibzugriff auf einzelne RAM-Zellen Als Argumente wird die Adresse der zu aendernden Zelle sowie deren Soll-Inhalt uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | RAM   : 0x0000 - 0x07FF EEPROM: 0x0800 - 0x0BFF |
| DATA | int | 0x00 - 0xFF, neuer Inhalt der Zelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-status-seriennummer"></a>
### STATUS_SERIENNUMMER

Seriennummer des Moduls

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SERIENNUMMER | string | Seriennummer als String |

<a id="job-status-ad-werte"></a>
### STATUS_AD_WERTE

Register der AD-Umsetzer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_AD_KLEMME30_WERT | int | Kanal der Betriebsspannungsmessung |
| STAT_AD_U_MESS_WERT | int | Kanal der Strommessung |
| STAT_AD_U_WANDLER_WERT | int | Kanal der Spannungsmessung am Wandler |
| STAT_AD_U_SHUNT_WERT | int | Kanal der Spannungsmessung am Shunt |
| _TEL_ANTWORT | binary |  |

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
| BINAER_BUFFER | binary | Codierdaten Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DWord) Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3:               Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary |  |
| TELEGRAMM | binary |  |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-status-cpcbo"></a>
### STATUS_CPCBO

Meßwert der Stromplausibilisierung vor Wandlerbestromung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_CPCBO_WERT | unsigned int | Strom als 16Bit Wert |
| STAT_CPCBO_EINH | string | Einheit des Stromes ist mA |
| _TEL_ANTWORT | binary |  |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte  21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| CHECKSUMME | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FARTTEXTE](#table-farttexte) (59 × 2)
- [FARTBIT](#table-fartbit) (6 × 2)
- [FARTOFFSET](#table-fartoffset) (12 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 3)

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

Dimensions: 67 rows × 2 columns

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
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
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

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Klemme 30 |
| 0x01 | Lastkreis |
| 0x02 | Messpfad |
| 0x03 | ECU intern |
| 0x04 | CAN low |
| 0x05 | CAN high |
| 0x06 | ASC1 |
| 0x07 | DME2_DDE2 |
| 0x08 | INSTR2 |
| 0x09 | Strommmessung |
| 0x0A | KBus-Kommunikation |
| 0x0B | Codierdaten |
| 0xXY | unbekannter Fehlecode |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 59 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | statischer Fehler |
| 0x02 | sporadischer Fehler |
| 0x10 | Unterspannung Klemme 30 |
| 0x11 | Überspannung Klemme 30 |
| 0x12 | Unterbrechung Klemme 30 |
| 0x13 | Symptom unbekannt |
| 0x14 | Symptom unbekannt |
| 0x15 | Symptom unbekannt |
| 0x20 | Leitungsunterbrechung |
| 0x21 | Kurzschluss Servo1 gegen Klemme 31 |
| 0x22 | Kurzschluss Servo1/Servo2 gegen Klemme 30 |
| 0x23 | Kurzschluss Servo2 gegen Klemme 31 |
| 0x24 | Symptom unbekannt |
| 0x25 | Kurzschluss Servo1 gegen Servo2 = KS-Ventil |
| 0x30 | Symptom unbekannt |
| 0x31 | Symptom unbekannt |
| 0x32 | Symptom unbekannt |
| 0x33 | Symptom unbekannt |
| 0x34 | Symptom unbekannt |
| 0x35 | Messpfad defekt |
| 0x40 | Takt Fehler |
| 0x41 | Programmfluß Fehler |
| 0x42 | Watchdog Reset |
| 0x43 | EEPROM-Fehler |
| 0x44 | ROM-Fehler |
| 0x45 | RAM-Fehler |
| 0x50 | Symptom unbekannt |
| 0x51 | Symptom unbekannt |
| 0x52 | Symptom unbekannt |
| 0x53 | Leitungsunterbrechung = kein Signal |
| 0x54 | Kurzschluss gegen Klemme 31 |
| 0x55 | Kurzschluss gegen Klemme 30 |
| 0x60 | fehlerhaft |
| 0x61 | Timeout |
| 0x62 | Symptom unbekannt |
| 0x63 | Symptom unbekannt |
| 0x64 | Symptom unbekannt |
| 0x65 | Symptom unbekannt |
| 0x70 | Symptom unbekannt |
| 0x71 | Symptom unbekannt |
| 0x72 | Symptom unbekannt |
| 0x73 | nicht kalibriert |
| 0x74 | unplausibel bei Initialisierung |
| 0x75 | unplausibel im Betrieb |
| 0x80 | Symptom unbekannt |
| 0x81 | Symptom unbekannt |
| 0x82 | Symptom unbekannt |
| 0x83 | Symptom unbekannt |
| 0x84 | Klemmenstatus unplausibel |
| 0x85 | kein Klemmenstatus vom Kombi |
| 0x90 | Modul nicht codiert |
| 0x91 | Codierdaten fehlerhaft |
| 0x92 | Symptom unbekannt |
| 0x93 | Symptom unbekannt |
| 0x94 | Symptom unbekannt |
| 0x95 | Symptom unbekannt |
| 0xFF | nicht belegt |
| 0xXY | unbekannte Fehlerart |

<a id="table-fartbit"></a>
### FARTBIT

Dimensions: 6 rows × 2 columns

| BIT | VALUE |
| --- | --- |
| 0x01 | 5 |
| 0x02 | 4 |
| 0x04 | 3 |
| 0x08 | 2 |
| 0x10 | 1 |
| 0x20 | 0 |

<a id="table-fartoffset"></a>
### FARTOFFSET

Dimensions: 12 rows × 2 columns

| ORT | OFFSET |
| --- | --- |
| 0x00 | 0x10 |
| 0x01 | 0x20 |
| 0x02 | 0x30 |
| 0x03 | 0x40 |
| 0x04 | 0x50 |
| 0x05 | 0x50 |
| 0x06 | 0x60 |
| 0x07 | 0x60 |
| 0x08 | 0x60 |
| 0x09 | 0x70 |
| 0x0A | 0x80 |
| 0x0B | 0x90 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | ----   | ---- |
| 0x01 | Kilometerstand | km |
| 0x02 | Geschwindigkeit | km/h |
| 0x03 | Versorgungsspannung KL30 | V |
| 0xXY | unbekannte Umweltbedingung | -- |
