# 08EMS2K.PRG

- Jobs: [29](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EMS2K |
| ORIGIN | Rover EE-R-45 John Longvill |
| REVISION | 0.8 |
| AUTHOR | Softing AG/BG5: AR,Le,Mw,Po |
| COMMENT | P-SGBD fuer EMS2K |
| PACKAGE | 0.40 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EMS2K
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Begins a diagnostic session
- [START_DIAGNOSTIC_SESSION_HIGHBAUD](#job-start-diagnostic-session-highbaud) - Begins a diagnostic session with fast baudrate
- [START_DIAGNOSTIC_SESSION_LOWBAUD](#job-start-diagnostic-session-lowbaud) - Begins a diagnostic session with low baudrate
- [STOP_DIAGNOSTIC_SESSION](#job-stop-diagnostic-session) - Ends a diagnostic session
- [SG_RESET](#job-sg-reset) - Reset the ECU
- [SEED_KEY](#job-seed-key) - Obtain security access to the ECU Schutzmechanismus SEED_KEY
- [ACCESS_TIMING_PARAMETERS](#job-access-timing-parameters) - Diagnosemode des SG beenden
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Request download
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Transfer data to the ECU
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Exit data transfer
- [AIF_SCHREIBEN](#job-aif-schreiben) - Beschreiben des Anwender-Info-Feldes
- [HWNR_SCHREIBEN](#job-hwnr-schreiben) - Write the current HwNr
- [STATUS_LESEN](#job-status-lesen) - Status
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Status
- [CHECK_REPROG_DEPENDING](#job-check-reprog-depending) - Status
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash  - Zellen loeschen
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [ZIF](#job-zif) - Job ZIF
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [UPROG_LESEN](#job-uprog-lesen) - Programmierspannung auslesen
- [BAUDRATEN_LESEN](#job-baudraten-lesen) - Baudratentabelle auslesen
- [TUNE_NR_SCHREIBEN](#job-tune-nr-schreiben) - Write the tune part number

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EMS2K

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_ORIG_BMW_NR | string | Urspruenglich BMW-Teilenummer Original BMW part number |
| ID_BMW_NR | string | Zurzeit BMW-Teilenummer Current BMW part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_TAG | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MON | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_SW_NR | int | Softwarenummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO Single or dual oxygen sensors |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung, sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_MOTOR | string | Parameter fuer MoTest Motorkennung |
| ID_PROD_NR | string | AR, Produktionsnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle |

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
| AIF_ANZ_FREI | int | Anzahl noch vorhandener (freier) AIF-Eintraege |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusammenbaunummer |
| AIF_SERIEN_NR | string | Seriennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_KM | string | Kilometerstand |
| AIF_PROG_NR | string | Programmstandsnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Begins a diagnostic session

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Diagnostic mode: 0x81=Standard, 0x83=EOL, 0x86=Development 0x85=Programming at 9.6k, 0xFF=Programming at 62.5k |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-start-diagnostic-session-highbaud"></a>
### START_DIAGNOSTIC_SESSION_HIGHBAUD

Begins a diagnostic session with fast baudrate

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-start-diagnostic-session-lowbaud"></a>
### START_DIAGNOSTIC_SESSION_LOWBAUD

Begins a diagnostic session with low baudrate

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-stop-diagnostic-session"></a>
### STOP_DIAGNOSTIC_SESSION

Ends a diagnostic session

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-seed-key"></a>
### SEED_KEY

Obtain security access to the ECU Schutzmechanismus SEED_KEY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Security access mode Typ zugang 1 = breakdown, 3 = dealer, 5 = End of line 7 = programming, 9 = development |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Request seed response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Send key response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-access-timing-parameters"></a>
### ACCESS_TIMING_PARAMETERS

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| P2_MIN | unsigned int | Minimum time between tester request and ECU response |
| P2_MAX | unsigned int | Maximum time between tester request and ECU response |
| P3_MIN | unsigned int | Minimum time between ECU response and tester request |
| P3_MAX | unsigned int | Maximum time between ECU response and tester request |
| P4_MIN | unsigned int | Minimum inter byte time for tester request |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Request download

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten: enthalten Adressinfo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Transfer data to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | Data to transfer to the ECU |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Exit data transfer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Beschreiben des Anwender-Info-Feldes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusammenbaunummer |
| AIF_SERIEN_NR | string | Seriennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_KM | string | Kilometerstand |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-hwnr-schreiben"></a>
### HWNR_SCHREIBEN

Write the current HwNr

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROG_HWNR | string | Fahrgestellnummer VIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SG_STATUS | int | nichts |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_CHECKSUMME_WERT | int | nichts |

<a id="job-check-reprog-depending"></a>
### CHECK_REPROG_DEPENDING

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash  - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROG_MODE | int | 1 = Daten, 2=Programm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_STATUS | int | nichts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten: enthalten Adressinfo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
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
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif"></a>
### ZIF

Job ZIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Programmstand |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string |  |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-uprog-lesen"></a>
### UPROG_LESEN

Programmierspannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | string | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-baudraten-lesen"></a>
### BAUDRATEN_LESEN

Baudratentabelle auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE_NUMMER | int | Nummer der zu lesenden Baudrate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | Baudrate 0....125000 "" heisst Tabellenende gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-tune-nr-schreiben"></a>
### TUNE_NR_SCHREIBEN

Write the tune part number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TUNE_NR | string | Tune part number - 8 characters |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write tune telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write tune response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write tune last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read tune response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (23 × 2)
- [LIEFERANTEN](#table-lieferanten) (45 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (15 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 23 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | @SERVICE NOT SUPPORTED@ |
| 0x12 | @SUB-FUNCTION NOT SUPPORTED@ |
| 0x22 | @CONDITION NOT CORRECT@ |
| 0x31 | @REQUEST OUT OF RANGE@ |
| 0x33 | @SECURITY ACCESS DENIED / REQUIRED@ |
| 0x35 | @INVALID KEY@ |
| 0x36 | @EXCEEDED NUMBER OF ATTEMPTS@ |
| 0x37 | @REQUIRED TIME DELAY NOT EXPIRED@ |
| 0x40 | @DOWNLOAD NOT ACCEPTED@ |
| 0x41 | @IMPROPER DOWNLOAD TYPE@ |
| 0x42 | @CANNOT DOWNLOAD TO SPECIFIED ADDRESS@ |
| 0x50 | @UPLOAD NOT ACCEPTED@ |
| 0x52 | @CANNOT UPLOAD FROM SPECIFIED ADDRESS@ |
| 0x53 | @CANNOT UPLOAD NUMBER OF BYTES REQUESTED@ |
| 0x78 | @REQUEST CORRECTLY RECEIVED - RESPONSE PENDING@ |
| 0x79 | @INCORRECT BYTE COUNT DURING BLOCK TRANSFER@ |
| 0x80 | @SERVICE NOT SUPPORTED IN CURRENT DIAGNOSTIC MODE@ |
| 0x90 | @OPERATION NOT PERFORMED@ |
| 0x91 | @INCORRECT MESSAGE FORMAT@ |
| 0xA0 | OKAY |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 45 rows × 2 columns

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
| 0xFF | @unbekannter Hersteller@ |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | EMS2K bereit, Startwert zu empfangen |
| 0x01 | kein freier Startwert mit Freigabe vorhanden |
| 0x02 | noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel (wie im DS2-LH definiert) |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 15 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Startwertprogrammierung bzw. -ruecksetzen war erfolgreich |
| 0x01 | falscher Startwert beim Ruecksetzen (EWS u. DME passen nicht zusammen)  |
| 0x02 | Telegramminhalt war kein Startwert (event. Wechselcode) |
| 0x03 | Schnittstellenfehler DWA: Frame o. Parity oder kein Signal (Timeout) |
| 0x04 | Prozess laeuft |
| 0x05 | Programmierung bzw. Ruecksetzen im Fahrzyklus noch nicht ausgefuehrt |
| 0x06 | gleiche Zufallszahl wie bei vorherigem Ruecksetzen trotz Weiterschaltung |
| 0x07 | noch kein Startwert programmiert |
| 0x10 | Startwert nicht korrekt in Flash programmiert |
| 0x11 | Wechselcode nicht korrekt in EEPROM-Spiegel programmiert |
| 0x12 | Zufallszahl nicht korrekt in EEPROM-Spiegel programmiert |
| 0x20 | Fehler bei Startwertprogrammierroutine |
| 0x21 | 2-aus-3-Startwertablage im Flash nicht in Ordnung |
| 0x22 | Ablage im EEPROM-Spiegel nicht in Ordnung |
| 0xXY | Fehlerhafter Status |
