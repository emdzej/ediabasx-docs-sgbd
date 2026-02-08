# 04BMSC2.prg

- Jobs: [34](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BMSC2 |
| ORIGIN | Softing AG |
| REVISION | 1.6 |
| AUTHOR | Softing AG, Roman Marziw |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [Initialisierung](#job-initialisierung) - Dieser Job wird vom EDIABAS automatisch beim ersten Zugriff auf eine SGBD aufgerufen. Bei weiteren Zugriffen auf dieselbe SGBD wird dieser Job nicht mehr aufgerufen. Ausnahme: nach einem EDIABAS-Fehler wird dieser Auftrag erneut aufgerufen In der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit dem SG notwendig sind, z.B. -  Verbindung zum Interface aufbauen -  Setzen des Wiederholungszaehlers -  Setzen der Kommunikationsparameter 
- [NEU_REIZEN](#job-neu-reizen) - Dieser Job wird immer dann aufgerufen, wenn das SG resettet wurde, die Steuergeraetekommunikation aber weitergefuehrt werden soll ohne dass das EDIC einen Timeout-Fehler meldet. Der Job bewirkt, dass das EDIC die Kommunikation abbricht und wieder neu aufsetzt (wie im JOB Initi- alisierung.
- [Ende](#job-ende) - Dieser Job wird vom EDIABAS automatisch bei einem Wechsel der SGBD aufgerufen. Job dient der Beendigung der KWP2000 Kommunikation
- [INFO](#job-info) - Information SGBD
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [ZIF](#job-zif) - Job Zulieferer Infofeld lesen
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender-Info-Feldes nach einer Programmierung
- [START_PROGRAMMING_SESSION](#job-start-programming-session) - Status
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Status
- [STOP_DIAGNOSTIC_SESSION](#job-stop-diagnostic-session) - Status
- [STATUS_LESEN](#job-status-lesen) - Status
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash  - Zellen loeschen
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben (RequestDownload)
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen beschreiben
- [FLASH_LESEN](#job-flash-lesen) - Job Flash lesen
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Programmiersitzung schliessen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [IDENT](#job-ident) - Liest Identifikationsdaten aus dem Steuergeraet aus
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [POWER_DOWN_MODE](#job-power-down-mode) - Nachlaufzyklus initiieren nichtfluechtige Daten werden ins EEPROM geschrieben
- [UPROG_LESEN](#job-uprog-lesen) - Programmierspannung auslesen
- [LOESCH_DAUER_LESEN](#job-loesch-dauer-lesen) - Loeschdauer aus SG auslesen
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus
- [ECU_RESET](#job-ecu-reset) - PowerOn-Reset per Software
- [ECU_RESET_STATUS](#job-ecu-reset-status) - Abfrage der letzten Reset-Ursache
- [ADAPTION_LESEN_SETZEN](#job-adaption-lesen-setzen) - Status
- [IO_STATUS_VORGEBEN](#job-io-status-vorgeben) - Status
- [PARK_POS_LL_STEPPER](#job-park-pos-ll-stepper) - Status
- [SONDEN_SPANNUNG_LESEN](#job-sonden-spannung-lesen) - Auslesen der Sondenspannung aus Messwerteblock 1

<a id="job-initialisierung"></a>
### Initialisierung

Dieser Job wird vom EDIABAS automatisch beim ersten Zugriff auf eine SGBD aufgerufen. Bei weiteren Zugriffen auf dieselbe SGBD wird dieser Job nicht mehr aufgerufen. Ausnahme: nach einem EDIABAS-Fehler wird dieser Auftrag erneut aufgerufen In der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit dem SG notwendig sind, z.B. -  Verbindung zum Interface aufbauen -  Setzen des Wiederholungszaehlers -  Setzen der Kommunikationsparameter 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | DONE ist ein obligatorisches Ergebnis, das von EDIABAS ausgewertet wird. Es duerfen nur folgende Werte zugewiesen werden: =  0 : Fehler bei der Initialisierung &lt;&gt; 0 : Initialisierung erfolgreich durchgefuehrt Fehlerbehandlung: DONE=0: Fehler 100, INITIALIZATION ERROR Auftrag nicht gefunden in SGBD: Fehler  90, NO INITIALIZATION JOB |

<a id="job-neu-reizen"></a>
### NEU_REIZEN

Dieser Job wird immer dann aufgerufen, wenn das SG resettet wurde, die Steuergeraetekommunikation aber weitergefuehrt werden soll ohne dass das EDIC einen Timeout-Fehler meldet. Der Job bewirkt, dass das EDIC die Kommunikation abbricht und wieder neu aufsetzt (wie im JOB Initi- alisierung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ende"></a>
### Ende

Dieser Job wird vom EDIABAS automatisch bei einem Wechsel der SGBD aufgerufen. Job dient der Beendigung der KWP2000 Kommunikation

_No arguments._

_No results._

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BOSCH |
| DATEN_REF_PROJEKT | string | Projektkennzeichnung |
| DATEN_REF_PROGRAMM_STAND | string | Programmstand |
| DATEN_REF_DATENSATZ | string | Datensatzkennung |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hw-referenz"></a>
### HW_REFERENZ

Job HW-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BOSCH |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif"></a>
### ZIF

Job Zulieferer Infofeld lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BOSCH |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Projektkennzeichnung |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | Nummer des zu lesenden AIF's &gt;=1. 0 bedeutet aktuelles AIF, auf das ein freies AIF folgt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE_HIGH | int | AIF Adresse, naechste (freie), high-word |
| AIF_ADRESSE_LOW | int | AIF Adresse, naechste (freie), low-word |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Datum der Programmierung |
| AIF_SW_NR | string | Softwarenummer |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusbaunummer |
| AIF_SERIEN_NR | string | Seriennummer (Programmiergeraet) |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_KM | string | km-Stand |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener (freier) AIF-Eintraege |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender-Info-Feldes nach einer Programmierung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | BMW-Fertigungsdatum |
| AIF_SW_NR | string | Softwarenummer |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | ZusBaunummer |
| AIF_SERIEN_NR | string | Seriennummer (Programmiergeraet) |
| AIF_HAENDLER_NR | int | Haendlernummer |
| AIF_KM | long | km-Stand |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_SCHREIBEN_ADRESSE | binary | Adresse des aktuell beschriebenen AIFs |
| AIF_SCHREIBEN_STATUS | int | Status in Positive Response 1=ok/2=nok |
| AIF_SCHREIBEN_ANZAHL | int | Anzahl der geschriebenen Bytes = 46 bei AIF_SCHREIBEN_STATUS == 1 &lt; 46 bei AIF_SCHREIBEN_STATUS == 2 |
| JOB_STATUS | string |  |

<a id="job-start-programming-session"></a>
### START_PROGRAMMING_SESSION

Status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMMING_MODE | long | PROGRAMMING_MODE 85 = ProgProg, 88 = DatProg |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAGNOSTIC_MODE | long | DIAGNOSTIC_MODE 84 = EOLSSM, 87 =ECUAdjustmentMode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-stop-diagnostic-session"></a>
### STOP_DIAGNOSTIC_SESSION

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SG_STATUS | int | nichts |
| SG_STATUS_STRING | binary | nichts |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash  - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten: enthalten Adressinfo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_ADR | long | Segment-Basisadresse |
| FLASH_LOESCHEN_ANZAHL | long | Anzahl der geloeschten Bytes |
| FLASH_LOESCHEN_STATUS | int | nichts |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Vorbereitung fuer Flash schreiben (RequestDownload)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten: enthalten Adressinfo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_ADR | long | Adresse des zuletzt programmierten Bytes |
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl der programmierten Bytes |
| FLASH_SCHREIBEN_STATUS | int | Statusbyte fuer Prog o.k./nicht o.k. |

<a id="job-flash-lesen"></a>
### FLASH_LESEN

Job Flash lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LESEN_ADR | long | Adresse des ersten zu lesenden Bytes |
| FLASH_LESEN_ANZAHL | int | Anzahl der zu lesenden Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LESEN_INHALT | binary |  |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Programmiersitzung schliessen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACCESS_MODE | int | fuer die Uebergabe des Access-Modes 0x01, 0x03 oder 0x05 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |

<a id="job-ident"></a>
### IDENT

Liest Identifikationsdaten aus dem Steuergeraet aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index - bei MKB_C nicht benutzt |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_DIAG_INDEX_DBYT2 | int | Diagnose-Index |
| ID_DIAG_INDEX_DBYT1 | int | Diagnose-Index |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_BSV | string | Softwarenummer (boot software version) |
| ID_SW_NR_DSV | string | Softwarenummer (data software version) |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_PRUEF_BYTE | int | Pruefstatusbyte fuer alle Segmente |
| STAT_BOOT_SEG | int | Pruefergebnis fuer Bootsoftware |
| STAT_PROG_SEG | int | Pruefergebnis fuer Betriebssoftware |
| STAT_DAT_SEG | int | Pruefergebnis fuer Datensegment |

<a id="job-power-down-mode"></a>
### POWER_DOWN_MODE

Nachlaufzyklus initiieren nichtfluechtige Daten werden ins EEPROM geschrieben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-uprog-lesen"></a>
### UPROG_LESEN

Programmierspannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | real | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-loesch-dauer-lesen"></a>
### LOESCH_DAUER_LESEN

Loeschdauer aus SG auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| LOESCH_DAUER | int | Loeschdauer in Sekunden |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION_STATUS | int | gewaehlter StatusOfDTC (0/1) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer MKBC 0-(identified DTCs) oder 1-(supported DTCs) |
| F_ANZ_NR | int | Anzahl der vom ECU uebergebenen Fehler |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |

<a id="job-ecu-reset"></a>
### ECU_RESET

PowerOn-Reset per Software

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ecu-reset-status"></a>
### ECU_RESET_STATUS

Abfrage der letzten Reset-Ursache

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RESET_STATUS_REG | int | Inhalt des Reset-Status-Registers |
| RESET_STATUS_RES | int | Reset-Status-2 reserved |

<a id="job-adaption-lesen-setzen"></a>
### ADAPTION_LESEN_SETZEN

Status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IOCP_ADAPTION | int | Adaption lesen = 0x09, selektiv setzen = 0x04 |
| CS1_ADAPTION | int | Adaption Auswahlbyte1 |
| CS2_ADAPTION | int | Adaption Auswahlbyte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| R_CS1_STATUS | int | Ergebnis CS1 Status bei setzen und lesen |
| R_CS2_STATUS | int | Ergebnis CS2 Status bei setzen und lesen |
| R_CS3_STATUS | int | Ergebnis CS3 Status bei setzen und lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-io-status-vorgeben"></a>
### IO_STATUS_VORGEBEN

Status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_IO_STATUS | int |  |
| IOCP_IO_STATUS | int |  |
| CS1_IO_STATUS | int | IO_STATUS Auswahlbyte1 |
| CS2_IO_STATUS | int | IO_STATUS Auswahlbyte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| R_CS1_IO_STATUS | int | result IO_STATUS Auswahlbyte1 |
| R_CS2_IO_STATUS | int | result IO_STATUS Auswahlbyte2 |

<a id="job-park-pos-ll-stepper"></a>
### PARK_POS_LL_STEPPER

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-sonden-spannung-lesen"></a>
### SONDEN_SPANNUNG_LESEN

Auslesen der Sondenspannung aus Messwerteblock 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SONDEN_SPANNUNG | real | Sondenspannung |

## Tables

### Index

- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [JOBRESULT](#table-jobresult) (43 × 2)
- [FORTTEXTE](#table-forttexte) (26 × 2)

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 43 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?01? | BUSY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?10? | ERROR_F_CODE |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 26 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0105 | Umgebungsdrucksensor |
| 0x0110 | Ansauglufttemperaturfühler |
| 0x0115 | Motortemperaturfühler |
| 0x0120 | Drosselklappenpotentiometer |
| 0x0121 | schnelle Drosselklappenadaption |
| 0x0130 | Lambdasonde |
| 0x0135 | Lambdasondenheizung |
| 0x0201 | Einspritzventil |
| 0x0230 | Elektrische Kraftstoffpumpe |
| 0x0335 | KW-Signal |
| 0x0412 | Sekundärluftventil |
| 0x0443 | Tankentlüftungsventil |
| 0x0480 | Elektrischer Lüfter |
| 0x0500 | Geschwindigkeitssignal |
| 0x0505 | Leerlaufregler |
| 0x0560 | Ubatt-Signal |
| 0x0561 | Wackelkontakt |
| 0x0601 | E2-Emulation |
| 0x0603 | Steuergerätetest (SGS) |
| 0x0608 | UEXT Spannungsversorgung DKP |
| 0x0655 | Übertemperatur LED |
| 0x1510 | Elektrischer Lüfter |
| 0x1600 | Steuergerätetest (SGS) |
| 0x9997 | schnelle Drosselklappenadaption |
| 0x9999 | Übertemperatur LED |
| 0x???? | unbekannter Fehler |
