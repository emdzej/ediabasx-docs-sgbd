# CVM_IV.prg

- Jobs: [28](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Cabrio-Verdeck-Modul IV E85 |
| ORIGIN | BMW EI-61 Kluge |
| REVISION | 1.03 |
| AUTHOR | HELBAKO E2 Spanner, BMW Drexel TI-433, Huber TI-433, Spoljarec TP-421, Dennert TI-431 |
| COMMENT | SGBD fuer E85 Cabrioverdeckmodul ab SW 2.3 |
| PACKAGE | 1.00 |
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
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes FE-TRA-MODE Es muss immer das Argument "0" uebergeben werden
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers des CVM Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreibzugriff auf einzelne RAM-Zellen Als Argumente wird die Adresse der zu aendernden Zelle sowie deren Soll-Inhalt uebergeben.
- [CODIERUNG_LESEN](#job-codierung-lesen) - Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben
- [STATUS_LESEN](#job-status-lesen) - es werden die Eingangs- und Ausgangsstati aus dem Steuergeraet gelesen Die Auflistung der Statusbits erfolgt von LSB nach MSB
- [STEUERN_VERDECK](#job-steuern-verdeck) - Default ident job
- [HERSTELLER_SCHREIBEN](#job-hersteller-schreiben) - Default ident job
- [HERSTELLER_LESEN](#job-hersteller-lesen) - Default ident job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [IS_LESEN](#job-is-lesen) - is_lesen job
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [RESET](#job-reset) - Steuergeraet in RESET-Zustand versetzen
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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes FE-TRA-MODE Es muss immer das Argument "0" uebergeben werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| fe_tra_mode | int | nur 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argument nicht uebergeben oder ausser Bereich |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers des CVM Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| ADRESSE | long | 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Schreibzugriff auf einzelne RAM-Zellen Als Argumente wird die Adresse der zu aendernden Zelle sowie deren Soll-Inhalt uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | RAM   : 0x1000 - 0x1EFF EEPROM: 0x0800 - 0x0BFF |
| DATA | int | 0x00 - 0xFF, neuer Inhalt der Zelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Lesezugriff auf die einzelnen Codierdatenbloecke Als Argument wird die Nummer des zu lesenden Codierdatenblockes uebergeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNUMMER | int | zulaessige Blocknummern liegen i Bereich 0x0000 - 0x0004 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Es werden jeweils die 16 Byte des angesprochenen Codierdatenblockes ausgegeben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-status-lesen"></a>
### STATUS_LESEN

es werden die Eingangs- und Ausgangsstati aus dem Steuergeraet gelesen Die Auflistung der Statusbits erfolgt von LSB nach MSB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME_R_EIN | int | gesetztes Bit heisst Signal liegt vor |
| STAT_KLEMME_30_EIN | int | gesetztes Bit heisst Signal liegt vor |
| STAT_VERDECKKASTENBODEN_UNTEN | int | gesetztes Bit heisst Signal liegt vor |
| STAT_V_SCHL_BETAETIGT | int | gesetztes Bit heisst Signal liegt vor |
| STAT_V_OEFF_BETAETIGT | int | gesetztes Bit heisst Signal liegt vor |
| STAT_HARDTOP_MONTIERT | int | gesetztes Bit heisst Signal liegt vor |
| STAT_KLEMME_15_EIN | int | gesetztes Bit heisst Signal liegt vor |
| STAT_POSITION_WINDLAUF_TEXT | string | Signal enthaelt kombinierte Info ueber Windlaufposition moegliche Zustaende sind: VERRIEGELT - Hall VERRIEGELT ist bedaempft ENTRIEGELT - Hall ENTRIEGELT ist bedaempft ZWISCHENPOSITION -  kein Hall ist bedaempft UNPLAUSIBEL - Hall ENTRIEGELT und Hall VERRIEGELT sind bedaempft |
| STAT_POSITION_VERDECK_TEXT | string | Signal enthaelt kombinierte Info ueber Verdeckposition moegliche Zustaende sind: OFFEN - Hall ABGELEGT ist bedaempft ZU    - Hall VORNE ist bedaempft ZWISCHENPOSITION -  kein Hall ist bedaempft UNPLAUSIBEL - Hall ABGELEGT und Hall VORNE sind bedaempft |
| STAT_HALL_RESERVE_ERREGT | int | gesetztes Bit heisst Signal liegt vor |
| STAT_RELAIS_PUMPE_TEXT | string | Signal enthaelt kombinierte Info ueber Ansteuerung der Pumpe moegliche Zustaende sind: STOP - beide Signale LOW OEFFNEN - Anstuerung ABLEGEN ist HIGH SCHLIESSEN - Ansteuerung  SCHLIESSEN ist HIGH UNPLAUSIBEL - beide Ansteuerungen sind HIGH |
| STAT_MOTOR_WINDLAUF_TEXT | string | Signal enthaelt kombinierte Info ueber Ansteuerung des Windlaufmotors moegliche Zustaende sind: AUS - beide Signale LOW OEFFNEN - Anstuerung ENTRIEGELN ist HIGH SCHLIESSEN - Ansteuerung  VERRIEGELN ist HIGH MOTORBREMSE - beide Ansteuerungen sind HIGH |
| STAT_SPANNUNG_KL30_WERT | real | am Spannungsteiler gemessene Spannung |
| STAT_SPANNUNG_KL30_EINH | string |  |
| STAT_GESCHW_WERT | int | ueber KBus empfangene FZG-Geschwindigkeit |
| STAT_GESCHW_EINH | string |  |
| STAT_STATENO_WERT | int | Nummer des in der SW abgearbeiteten States |
| STAT_AUSSENTEMPERATUR_WERT | int |  |
| STAT_AUSSENTEMPERATUR_EINH | string |  |
| STAT_TUEREN_GESCHLOSSEN | int | gesetztes Bit heisst, dass alle Tueren geschlossen sind |
| STAT_FAHRZEUG_FAEHRT | int | gesetztes Bit heisst Fahrzeug faehrt |
| STAT_MINDESTENS_1_FENSTER_GESCHLOSSEN | int | gesetztes Bit heisst mindestens ein Fenster ist geschl. |
| STAT_FREIGABE_HECKSCHEIBENHEIZUNG | int | gesetztes Bit heisst Freigabe liegt vor |
| STAT_VERDECKZAEHLER_ZU_NR | int | Gibt Anzahl der Verdecklaeufe in Richtung zu an |
| STAT_VERDECKZAEHLER_AUF_NR | int | gibt Anzahl der Verdecklaeufe in Richtung auf an |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-steuern-verdeck"></a>
### STEUERN_VERDECK

Default ident job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTER | string | Signal Taster vorgeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| TEL | binary |  |

<a id="job-hersteller-schreiben"></a>
### HERSTELLER_SCHREIBEN

Default ident job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Byte 1 der Herstellerdaten: 0x00...0xFF |
| BYTE2 | int | Byte 2 der Herstellerdaten: 0x00...0xFF |
| BYTE3 | int | Byte 3 der Herstellerdaten: 0x00...0xFF |
| BYTE4 | int | Byte 4 der Herstellerdaten: 0x00...0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-hersteller-lesen"></a>
### HERSTELLER_LESEN

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BYTE1 | int | Herstellerdaten Byte 1: 0x00...0xFF |
| BYTE2 | int | Herstellerdaten Byte 2: 0x00...0xFF |
| BYTE3 | int | Herstellerdaten Byte 3: 0x00...0xFF |
| BYTE4 | int | Herstellerdaten Byte 4: 0x00...0xFF |

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
| ANZ | int | DEBUG |
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
| TEL | binary |  |

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
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-reset"></a>
### RESET

Steuergeraet in RESET-Zustand versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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
| TEL | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (53 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 3)
- [STEUERN](#table-steuern) (3 × 3)

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

Dimensions: 69 rows × 2 columns

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
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
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

Dimensions: 53 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | reserviert |
| 0x01 | Codierdatensatz ungültig, Modul nicht codiert |
| 0x02 | Codierung ungültig |
| 0x03 | Checksummenfehler ROM |
| 0x04 | reserviert |
| 0x05 | Checksummenfehler in den Codierdaten |
| 0x06 | RAM-Fehler |
| 0x07 | Watchdog-Reset |
| 0x08 | ungültiger Opcode |
| 0x09 | Clock-Monitor-Fehler |
| 0x0A | Fehler im Programmfluß |
| 0x10 | reserviert |
| 0x11 | Versorgung der HALL-Sensoren n.i.O. |
| 0x12 | Bedientaster 'Öffnen' permanent auf GND |
| 0x13 | Bedientaster 'Schliessen' permanent auf GND |
| 0x14 | reserviert |
| 0x15 | reserviert |
| 0x16 | reserviert |
| 0x17 | reserviert |
| 0x18 | reserviert |
| 0x19 | reserviert |
| 0x1A | VSW V_VORNE, Kurzschluss nach UB |
| 0x1B | VSW V_VORNE, undefinierter Spannungsbereich |
| 0x1C | VSW V_VORNE, Kurzschluss nach GND |
| 0x1D | VSW 4.1, Kurzschluss nach UB |
| 0x1E | VSW 4.1, undefinierter Spannungsbereich |
| 0x1F | VSW 4.1, Kurzschluss nach GND |
| 0x20 | VSW 4.2, Kurzschluss nach UB |
| 0x21 | VSW 4.2, undefinierter Spannungsbereich |
| 0x22 | VSW 4.2, Kurzschluss nach GND |
| 0x23 | VSW V_ABGEL, Kurzschluss nach UB |
| 0x24 | VSW V_ABGEL, undefinierter Spannungsbereich |
| 0x25 | VSW V_ABGEL, Kurzschluss nach GND |
| 0x26 | reserviert |
| 0x27 | reserviert |
| 0x28 | reserviert |
| 0x40 | Antrieb Fanghaken: Strom beim Entriegeln zu hoch |
| 0x41 | Antrieb Fanghaken: Strom beim Verriegeln zu hoch |
| 0x42 | Antrieb Fanghaken: Kurzschluss Ub+ |
| 0x43 | Antrieb Fanghaken: Offene Last beim Entriegeln |
| 0x44 | Antrieb Fanghaken: Offene Last beim Verriegeln |
| 0x62 | Fertigungsmode/Transportmode aktiv |
| 0x63 | Verdeck fährt nicht zu |
| 0x64 | Verdeck fährt nicht auf |
| 0x67 | Fanghaken fahren nicht auf |
| 0x68 | Fanghahen fahren nicht zu |
| 0x69 | RPUMPEA, offene Last |
| 0x6A | RPUMPEA, Kurzschluss nach Masse |
| 0x6B | reserviert |
| 0x6C | RPUMPEZ, offene Last |
| 0x6D | RPUMPEZ, Kurzschluss nach Masse |
| 0x6E | reserviert |
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
| 0x6F | Kommunikationsfehler K-Bus-Schnittstelle |
| 0x70 | Unterspannung an Klemme 30 |
| 0x71 | Ueberspannung an Klemme 30 |
| 0x72 | Hall-Versorgung zeigt Unterspannung |
| 0x73 | Spannungseinbruch |
| 0x74 | Grundmodul sendet nicht 'Tueren- / Klappenstatus' |
| 0x75 | Power-On-Reset |
| 0x76 | reserviert |
| 0x77 | Absenken Seitenscheiben nicht gemeldet |
| 0x78 | Anheben Seitenscheiben nicht gemeldet |
| 0x79 | kein Status vom Kombiinstrument erhalten |
| 0x7A | reserviert |
| 0x7B | Fehler bei Aktivierung HHS |
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

Dimensions: 3 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| AUF | 1 | 0xE3 |
| ZU | 1 | 0x27 |
| STOPP | 1 | 0x00 |
