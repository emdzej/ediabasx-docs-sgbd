# rse_01.prg

- Jobs: [70](#jobs)
- Tables: [96](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Rear Seat Entertainment MID |
| ORIGIN | BMW EI-41 Röttgerman,Uwe |
| REVISION | 4.005 |
| AUTHOR | LEAR DCS Neubauer |
| COMMENT | N/A |
| PACKAGE | 1.19 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $F150 Sub-Parameter SGBD-Index Modus: Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [SVK_LESEN](#job-svk-lesen) - Informationen zur Steuergeraete-Verbau-Kennung UDS  : $22   ReadDataByIdentifier UDS  : $F1xx Sub-Parameter fuer SVK UDS  : $F101 SVK_AKTUELL (Default) Modus: Default
- [STATUS_LESEN](#job-status-lesen) - Lesen eines oder mehrerer Stati UDS  : $22 ReadDataByIdentifier
- [STEUERN](#job-steuern) - Vorgeben eines Status UDS  : $2E WriteDataByIdentifier
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [STEUERN_IO](#job-steuern-io) - Vorgeben eines Status UDS  : $2F InputOutputControlByIdentifier
- [STEUERN_ROUTINE](#job-steuern-routine) - Vorgeben eines Status UDS  : $31 RoutineControl
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers UDS  : $85 ControlDTCSetting UDS  : $?? Sperren ($02) / Freigabe ($01) Modus: Default
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default
- [HERSTELLINFO_LESEN](#job-herstellinfo-lesen) - Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default
- [STATUS_BETRIEBSMODE](#job-status-betriebsmode) - Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default
- [STEUERN_BETRIEBSMODE](#job-steuern-betriebsmode) - Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STATUS_VERSION_MOST_CONTROLLER](#job-status-version-most-controller) - Return Version of MOST Controller
- [STATUS_VERSORGUNGSSPANNUNG](#job-status-versorgungsspannung) - Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_WAKEUP_STATUS](#job-status-wakeup-status) - Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Gibt an ob SG Most Ring wecken darf
- [STATUS_AVERAGE_MESSAGE_RECEPTION_RATE](#job-status-average-message-reception-rate) - Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein
- [STATUS_FOT_TEMPERATUR](#job-status-fot-temperatur) - Temperatur am FOT
- [STEUERN_SENSOR_TEMP](#job-steuern-sensor-temp) - Simulates the temperature of a definite sensor.
- [STEUERN_WATCHDOG_TRIGGER_STOP](#job-steuern-watchdog-trigger-stop) - Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.
- [STATUS_SENSOR_TEMP](#job-status-sensor-temp) - Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [DEBUG_DMCLIENT_SYSTIME](#job-debug-dmclient-systime) - Systemzeit UDS  : $22   ReadDataByIdentifier UDS  : $1701 Sub-Parameter Systemzeit Modus: Default
- [STATUS_WAKEUP_ABSTIME](#job-status-wakeup-abstime) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $171B Wakeup absolute time Modus: Default
- [STATUS_DEBUG_DMCLIENT_IS_DTCACTIVERESPONSE](#job-status-debug-dmclient-is-dtcactiveresponse) - Fehlerspeicher lesen (DTC an DM) UDS  : $22   ReadDataByIdentifier UDS  : $1723 DMClient_isDTCActiveResponse Modus: Default
- [STATUS_DEBUG_DMCLIENT_IS_DTCLOCKABLE](#job-status-debug-dmclient-is-dtclockable) - Fehlerspeicher lesen (DTC an DM) UDS  : $22   ReadDataByIdentifier UDS  : $1724 DMClient_isDTCLockable Modus: Default
- [STATUS_BOOTLOADERVERSION](#job-status-bootloaderversion) - Nachrichtenabnahmerate bei Flashvorgang UDS  : $22   ReadDataByIdentifier UDS  : $4001 Sub-Parameter Nachrichtenabnahmerate Modus: Default
- [STATUS_SOFTWARENAME](#job-status-softwarename) - Build Softwarename UDS  : $22   ReadDataByIdentifier UDS  : $4002 Softwarename Modus: Default
- [STATUS_CPU_AUSLASTUNG](#job-status-cpu-auslastung) - Nachrichtenabnahmerate bei Flashvorgang UDS  : $22   ReadDataByIdentifier UDS  : $4006 Sub-Parameter CPU-Auslastung Modus: Default
- [STATUS_TEMP_VERTEILUNG_FOT](#job-status-temp-verteilung-fot) - FOT Temperaturverteilung UDS  : $22   ReadDataByIdentifier UDS  : $D054 Sub-Parameter FOT Temperaturverteilung Modus: Default
- [STATUS_TEMP_VERTEILUNG_DVD_DRIVE](#job-status-temp-verteilung-dvd-drive) - DVD-Drive Temperaturverteilung UDS  : $22   ReadDataByIdentifier UDS  : $D055 Sub-Parameter DVD Temperaturverteilung Modus: Default
- [STATUS_ACTIVE_SESSION](#job-status-active-session) - Active Session UDS  : $22   ReadDataByIdentifier UDS  : $F186 Active Session Modus: Default
- [STATUS_HW_NR](#job-status-hw-nr) - HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F192 Sub-Parameter HW-NR Modus: Default
- [DEBUG_DMCLIENT_TRIGGERDTCENTRY](#job-debug-dmclient-triggerdtcentry) - Debug DMClient UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0304 Debug DMClient UDS   : $??   Parameter  1:NW DTC, 0:Apllication Modus : Default
- [STEUERN_CLEAR_TEMP_VERTEILUNG](#job-steuern-clear-temp-verteilung) - temp histogram to be deleted UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A034 Steuern Clear Tempereturverteiling UDS   : $??   Parameter Modus : Default
- [STEUERN_INTERNAL_RESET](#job-steuern-internal-reset) - Internal Reset UDS   : $31   RoutineControlRequestServiceID UDS   : $01   Steuern UDS   : $A023 Steuern internal reset Modus : Default
- [STATUS_APPLICATION](#job-status-application) - Reads out applications stati if they are coded and their availability
- [STATUS_DRIVE_TEMPERATUR](#job-status-drive-temperatur) - Drive Temperatur UDS  : $22   ReadDataByIdentifier UDS  : $D00B Sub-Parameter Drive Temperatur Modus: Default
- [STATUS_VIN](#job-status-vin) - HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F190 Sub-Parameter VIN Modus: Default
- [STATUS_VOLTAGES](#job-status-voltages) - Spannungen am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_IR_FREQ](#job-status-ir-freq) - Build Softwarename UDS  : $22   ReadDataByIdentifier UDS  : $D056 IR_FREQ Modus: Default
- [STEUERN_DEBUG_COMMAND](#job-steuern-debug-command) - Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A040 Steuern Debug UDS   : $??   Parameter Modus : Default
- [STEUERN_FIRMWARE_UPDATE](#job-steuern-firmware-update) - Update Firmware UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A041 Steuern update UDS   : $??   Parameter UDS   : $1234  -  Atmel firmware UDS   : $5678  -  UIC Starter firmware UDS   : $1111  -  INIC firmware Modus : Default
- [STATUS_FIRMWARE](#job-status-firmware) - Status der Firmware versionen ATMEL, INIC und UIC Starter auslesen UDS   : $31   RoutineControlRequestServiceID UDS   : $03   Result UDS   : $A041 Status firmware Modus : Default
- [STATUS_DVD_FIRMWARE](#job-status-dvd-firmware) - version of DVD firmware UDS  : $22   ReadDataByIdentifier UDS  : $D057 DVD FW Version Modus: Default
- [RESCUE_HW_DATA](#job-rescue-hw-data) - Gerätehardware-Daten wiederherstellen Modus: Default

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $F150 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SG_ADR | long | Steuergeraeteadresse |
| ID_SGBD_INDEX | long | Index zur Erkennung der SG-Variante |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_SNAPSHOT | binary | Hex-Antwort von SG |
| _RESPONSE_EXTENDED_DATA | binary | Hex-Antwort von SG |
| _RESPONSE_SEVERITY | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | 0x??????: Angabe eines einzelnen Fehlers Default: 0xFFFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default

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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-svk-lesen"></a>
### SVK_LESEN

Informationen zur Steuergeraete-Verbau-Kennung UDS  : $22   ReadDataByIdentifier UDS  : $F1xx Sub-Parameter fuer SVK UDS  : $F101 SVK_AKTUELL (Default) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SVK | string | table SVK_ID BEZEICHNUNG WERT default SVK_AKTUELL |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_TEST | int | Programmierabhaengigkeiten (ProgrammingDependenciesChecked) 1: IO : Signaturpruefung und ProgrammingDependenciesCheck erfolgreich 2: NIO: mindestens eine SWE fehlerhaft oder ProgrammingDependenciesCheck nicht durchgefuehrt 3: NIO: mindestens eine SWE passt nicht mit einer HWE zusammen 4: NIO: mindestens eine SWE passt nicht mit einer anderen SWE zusammen sonst: reserviert |
| ANZAHL_EINHEITEN | int | Anzahl der xWEn |
| PROG_DATUM | string | Programmierdatum (DD.MM.YY) |
| PROG_KM | long | KM-Stand bei Programmierung (10 KM bis 655350 KM) Inkrement sind 10 KM -1: KM-Stand wird nicht unterstuetzt |
| PROZESSKLASSE_WERT | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| PROZESSKLASSE_TEXT | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| PROZESSKLASSE_KURZTEXT | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| VERSION | string | Angabe der Version der Prozessklasse |
| SGBM_ID | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Lesen eines oder mehrerer Stati UDS  : $22 ReadDataByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige result erzeugt table SG_Funktionen ARG ID RESULTNAME RES_TABELLE ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern"></a>
### STEUERN

Vorgeben eines Status UDS  : $2E WriteDataByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID LABEL ARG_TABELLE |
| WERT | string | Es muss mindestens ein Argument übergeben werden Argumente siehe table SG_Funktionen ARG ID ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-io"></a>
### STEUERN_IO

Vorgeben eines Status UDS  : $2F InputOutputControlByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID RES_TABELLE ARG_TABELLE |
| STEUERPARAMETER | string | 'RCTECU' = returnControlToECU 'RTD'    = resetToDefault 'FCS'    = freezeCurrentState 'STA'    = shortTermAdjustment optionales Argument Wenn nicht angegeben, dann kein InputOutputControlParameter im Request |
| WERT | string | Argumente siehe table SG_Funktionen ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-routine"></a>
### STEUERN_ROUTINE

Vorgeben eines Status UDS  : $31 RoutineControl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID RES_TABELLE ARG_TABELLE |
| STEUERPARAMETER | string | 'STR'  = startRoutine 'STPR' = stopRoutine 'RRR'  = requestRoutineResults |
| WERT | string | Argumente siehe table SG_Funktionen ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers UDS  : $85 ControlDTCSetting UDS  : $?? Sperren ($02) / Freigabe ($01) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT Default: "ja" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_2000 | binary | Hex-Antwort von SG |
| _RESPONSE_200X | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-herstellinfo-lesen"></a>
### HERSTELLINFO_LESEN

Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_LIEF_NR | long | Lieferantennummer 0xFFFFFF, falls nicht vorhanden |
| ID_LIEF_TEXT | string | Text zu ID_LIEF_NR table Lieferanten LIEF_TEXT unbekannter Hersteller, falls nicht vorhanden |
| ID_DATUM | string | Herstelldatum (DD.MM.YY) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | 0x00: Normalmode 0x01: Fertigungsmode 0x02: Transportmode 0x03: Flashmode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_WERT | int | Ausgabe des Energiesparmodes 0: Kein Energiesparmode gesetzt 1: Produktionsmode gesetzt 2: Transportmode gesetzt 3: Flashmode gesetzt -1: Mode ungueltig |
| STAT_ENERGIESPARMODE_TEXT | string | Text zu STAT_ENERGIESPARMODE_WERT |
| STAT_PRODUKTIONSMODE_EIN | int | 0: Produktionsmode nicht aktiv 1: Produktionsmode aktiv |
| STAT_TRANSPORTMODE_EIN | int | 0: Transportmode nicht aktiv 1: Transportmode aktiv |
| STAT_FLASHMODE_EIN | int | 0: Flashmode nicht aktiv 1: Flashmode aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-betriebsmode"></a>
### STATUS_BETRIEBSMODE

Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSMODE_WERT | int | Aktueller Betriebsmode table Betriebsmode WERT 0     : Kein Betriebsmode gesetzt 1 - 16: Erweiterter Betriebsmode (Bedeutung siehe Tabelle) |
| STAT_BETRIEBSMODE_TEXT | string | Textausgabe STAT_BETRIEBSMODE_WERT table Betriebsmode TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-betriebsmode"></a>
### STEUERN_BETRIEBSMODE

Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BETRIEBSMODE | int | Betriebsmode setzen table Betriebsmode WERT 0     : Kein Betriebsmode gesetzt 1 - 16: Erweiterter Betriebsmode (Bedeutung siehe Tabelle) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-version-most-controller"></a>
### STATUS_VERSION_MOST_CONTROLLER

Return Version of MOST Controller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRANSCEIVER_VERSION | string | Transceiver Version Format DDMMYY |
| STAT_NETSERVICES_VERSION | string | 3 Bytes Netservices Version |
| STAT_NETSERVICES_REVISION | string | 4 Byte Netservices Revision |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-versorgungsspannung"></a>
### STATUS_VERSORGUNGSSPANNUNG

Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MILLI_VOLT_WERT | unsigned int | Spannung in milliVolt |
| STAT_MILLI_VOLT_EINH | string | unit of the result |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-wakeup-status"></a>
### STATUS_WAKEUP_STATUS

Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_STATUS | int | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus WERT |
| STAT_WAKEUP_STATUS_TEXT | string | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Gibt an ob SG Most Ring wecken darf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABILITY_TO_WAKE | int | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| STAT_ABILITY_TO_WAKE_TEXT | string | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-average-message-reception-rate"></a>
### STATUS_AVERAGE_MESSAGE_RECEPTION_RATE

Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSG_CMS_SYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des Kontrollkanals [0-1000] |
| STAT_MSG_CMS_ASYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des async. Kanals. Sollte dieses Gerät nicht Async geflasht werden muss dieser Parameter auf 0 gesetzt sein [0-10000] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fot-temperatur"></a>
### STATUS_FOT_TEMPERATUR

Temperatur am FOT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FOT_TEMP_CELSIUS | char | Temperatur am FOT des SG in Celsius -128 C bis +127 C hierbei -128 C bedeutet ungültig (0xFF) |
| STAT_FOT_TEMP_FAHRENHEIT | real | Temperatur am FOT des SG in Fahrenheit -196.6 F bis +260.6 F hierbei bedeutet -198.4 F ungültig ( -128 C) Dieses this result is calculated inside the SGBD-Job Fahrenheit = (( Celsius × 9 ) / 5 ) + 32 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-temp"></a>
### STEUERN_SENSOR_TEMP

Simulates the temperature of a definite sensor.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be simulated |
| ARG_TEMPERATURE | char | Temperature that must be simulated |
| ARG_DURATION | unsigned char | Duration of the temperature simulation |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-watchdog-trigger-stop"></a>
### STEUERN_WATCHDOG_TRIGGER_STOP

Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TIME_WATCHDOG | unsigned int | Beschreibung: z.B. ARG_TIME_WATCHDOG = 4 bedeutet Abschalten des Watchdog-Triggers nach 4 Sekunden. nur positiven Zahlen und die 0. Skalierung: 1 entspricht 1 Sekunde |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-sensor-temp"></a>
### STATUS_SENSOR_TEMP

Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_WERT | char | Temperature of the selected sensor |
| STAT_DURATION_WERT | unsigned char | Remaining duration for the simulated temperature |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-stop"></a>
### STEUERN_ROE_STOP

Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF = Status der aktiven Fehlermeldung nicht feststellbar |
| STAT_ROE_AKTIV_TEXT | string | Interpretation von STAT_ROE_AKTIV table UDS_TAB_ROE_AKTIV TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-start"></a>
### STEUERN_ROE_START

Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-stop"></a>
### STEUERN_ROE_PERSISTENT_STOP

Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-start"></a>
### STEUERN_ROE_PERSISTENT_START

Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cps-lesen"></a>
### CPS_LESEN

Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPS | string | Codierpruefstempel 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diag-session-lesen"></a>
### DIAG_SESSION_LESEN

Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_SESSION_WERT | int | Diagnose-Session (1 Byte) |
| DIAG_SESSION_TEXT | string | Diagnose-Session als Text |
| DIAG_DETAIL_WERT | int | Details zur Diagnose-Session (1 Byte) |
| DIAG_DETAIL_TEXT | string | Details zur Diagnose-Session als Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-flash-tp-lesen"></a>
### FLASH_TP_LESEN

Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN | int | EraseMemoryTime (2 Byte) |
| FLASH_TEST | int | CheckMemoryTime (2 Byte) |
| FLASH_BOOT | int | BootloaderInstallationTime (2 Byte) |
| FLASH_AUTHENT | int | AuthenticationTime (2 Byte) |
| FLASH_RESET | int | ResetTime (2 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-prog-zaehler-lesen"></a>
### PROG_ZAEHLER_LESEN

Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_ZAEHLER_STATUS_WERT | int | Status, wie oft das SG programmierbar ist |
| PROG_ZAEHLER_STATUS_TEXT | string | Status, wie oft das SG programmierbar ist |
| PROG_ZAEHLER | int | Programmierzaehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-prog-max-lesen"></a>
### PROG_MAX_LESEN

Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_MAX | long | maximal mögliche Programmiervorgänge Sonderfall 0xFFFF: Anzahl der Programmiervorgänge unbegrenzt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-debug-dmclient-systime"></a>
### DEBUG_DMCLIENT_SYSTIME

Systemzeit UDS  : $22   ReadDataByIdentifier UDS  : $1701 Sub-Parameter Systemzeit Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTIME | long | Status Systemzeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-wakeup-abstime"></a>
### STATUS_WAKEUP_ABSTIME

Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $171B Wakeup absolute time Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_ABSTIME | string | Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-debug-dmclient-is-dtcactiveresponse"></a>
### STATUS_DEBUG_DMCLIENT_IS_DTCACTIVERESPONSE

Fehlerspeicher lesen (DTC an DM) UDS  : $22   ReadDataByIdentifier UDS  : $1723 DMClient_isDTCActiveResponse Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| STAT_F_HEX_CODE_TEXT | string | Fehlerdaten pro Fehler als Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-debug-dmclient-is-dtclockable"></a>
### STATUS_DEBUG_DMCLIENT_IS_DTCLOCKABLE

Fehlerspeicher lesen (DTC an DM) UDS  : $22   ReadDataByIdentifier UDS  : $1724 DMClient_isDTCLockable Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| STAT_F_HEX_CODE_TEXT | string | Fehlerdaten pro Fehler als Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bootloaderversion"></a>
### STATUS_BOOTLOADERVERSION

Nachrichtenabnahmerate bei Flashvorgang UDS  : $22   ReadDataByIdentifier UDS  : $4001 Sub-Parameter Nachrichtenabnahmerate Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BOOTLOADER_UIC | string | Bootloaderversion UIC |
| STAT_BOOTLOADER_VGC | string | Bootloaderversion VGC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-softwarename"></a>
### STATUS_SOFTWARENAME

Build Softwarename UDS  : $22   ReadDataByIdentifier UDS  : $4002 Softwarename Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOFTWARENAME | string | Build Softwarename |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cpu-auslastung"></a>
### STATUS_CPU_AUSLASTUNG

Nachrichtenabnahmerate bei Flashvorgang UDS  : $22   ReadDataByIdentifier UDS  : $4006 Sub-Parameter CPU-Auslastung Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CPU_AUSLASTUNG_UIC | char | CPU Auslastung UIC |
| STAT_CPU_AUSLASTUNG_VGC | char | CPU Auslastung VGC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-fot"></a>
### STATUS_TEMP_VERTEILUNG_FOT

FOT Temperaturverteilung UDS  : $22   ReadDataByIdentifier UDS  : $D054 Sub-Parameter FOT Temperaturverteilung Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_VERTEILUNG_FOT | unsigned long | FOT Temperaturverteilung |
| STAT_TEMP_RANGE | string | Zuordnung der Temperaturverterilung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-dvd-drive"></a>
### STATUS_TEMP_VERTEILUNG_DVD_DRIVE

DVD-Drive Temperaturverteilung UDS  : $22   ReadDataByIdentifier UDS  : $D055 Sub-Parameter DVD Temperaturverteilung Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_VERTEILUNG_DVD_DRIVE | char | DVD Temperaturverteilung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-active-session"></a>
### STATUS_ACTIVE_SESSION

Active Session UDS  : $22   ReadDataByIdentifier UDS  : $F186 Active Session Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ACT_SESS | long | Status aktive Session |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hw-nr"></a>
### STATUS_HW_NR

HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F192 Sub-Parameter HW-NR Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_NR | string | HW-Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-debug-dmclient-triggerdtcentry"></a>
### DEBUG_DMCLIENT_TRIGGERDTCENTRY

Debug DMClient UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0304 Debug DMClient UDS   : $??   Parameter  1:NW DTC, 0:Apllication Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TRIGGERDTCENTRY | int | Parameter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-temp-verteilung"></a>
### STEUERN_CLEAR_TEMP_VERTEILUNG

temp histogram to be deleted UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A034 Steuern Clear Tempereturverteiling UDS   : $??   Parameter Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_CLEAR_TEMP | char | Selects the desired temp histogram to be deleted: 0x00  FOT 0x01  DVD 0x02  HDD |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-internal-reset"></a>
### STEUERN_INTERNAL_RESET

Internal Reset UDS   : $31   RoutineControlRequestServiceID UDS   : $01   Steuern UDS   : $A023 Steuern internal reset Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-application"></a>
### STATUS_APPLICATION

Reads out applications stati if they are coded and their availability

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_APPL | unsigned char | ID of application |
| STAT_APPL_TEXT | string | Name of application from table TApplication |
| STAT_APPL_ENABLED | unsigned char | Status if application x is running or not values from table TApplicationRunningStatus |
| STAT_APPL_ENABLED_TEXT | string | Status if application x is running or not text values from table TApplicationRunningStatus |
| STAT_APPL_CODED | unsigned char | Status if application x is activated via coding or SWT or not values from table TApplicationActivationStatus |
| STAT_APPL_CODED_TEXT | string | Status if application x is activated via coding or SWT or not text values from table TApplicationActivationStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-drive-temperatur"></a>
### STATUS_DRIVE_TEMPERATUR

Drive Temperatur UDS  : $22   ReadDataByIdentifier UDS  : $D00B Sub-Parameter Drive Temperatur Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DRIVE_TEMP_CELSIUS | unsigned char | Drive Temperatur Celsius |
| STAT_DRIVE_TEMP_FAHRENHEIT | unsigned char | Drive Temperatur Fahrenheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vin"></a>
### STATUS_VIN

HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F190 Sub-Parameter VIN Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VIN | string | VIN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-voltages"></a>
### STATUS_VOLTAGES

Spannungen am SG. Darstellung mit Millivolt-Auflösung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_WERT | unsigned int | Spannung in milliVolt |
| STAT_KL30_EINH | string | unit of the result |
| STAT_1_2_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_1_2_V_EINH | string | unit of the result |
| STAT_1_3_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_1_3_V_EINH | string | unit of the result |
| STAT_1_8_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_1_8_V_EINH | string | unit of the result |
| STAT_2_5_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_2_5_V_EINH | string | unit of the result |
| STAT_3_3_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_3_3_V_EINH | string | unit of the result |
| STAT_5_V_WERT | unsigned int | Spannung in milliVolt |
| STAT_5_V_EINH | string | unit of the result |
| STAT_MINUS_5_V_WERT | int | Spannung in milliVolt |
| STAT_MINUS_5_V_EINH | string | unit of the result |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ir-freq"></a>
### STATUS_IR_FREQ

Build Softwarename UDS  : $22   ReadDataByIdentifier UDS  : $D056 IR_FREQ Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IR_FREQ | unsigned long | IR_Frequenz |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-debug-command"></a>
### STEUERN_DEBUG_COMMAND

Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A040 Steuern Debug UDS   : $??   Parameter Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_DEBUG_COMMAND | string | debug |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-firmware-update"></a>
### STEUERN_FIRMWARE_UPDATE

Update Firmware UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $A041 Steuern update UDS   : $??   Parameter UDS   : $1234  -  Atmel firmware UDS   : $5678  -  UIC Starter firmware UDS   : $1111  -  INIC firmware Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_FIRMWARE_TYP | unsigned int | kein Kommentar |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-firmware"></a>
### STATUS_FIRMWARE

Status der Firmware versionen ATMEL, INIC und UIC Starter auslesen UDS   : $31   RoutineControlRequestServiceID UDS   : $03   Result UDS   : $A041 Status firmware Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FIRMWARE_PMC_ROM | char | version of PMC firmware |
| STAT_FIRMWARE_PMC_ROM_COPY | char | version of PMC firmware copy |
| STAT_FIRMWARE_UIC_STARTER | string | version of UIC starter |
| STAT_FIRMWARE_UIC_STARTER_COPY | string | Version of uic starter copy |
| STAT_FIRMWARE_INIC_HW | char | INIC hardware version |
| STAT_FIRMWARE_INIC_FW | string | version of INIC FW |
| STAT_FIRMWARE_INIC_FW_COPY | string | version of INIC FW copy |
| STAT_FIRMWARE_INIC_CS | string | version of INIC CS |
| STAT_FIRMWARE_INIC_CS_COPY | string | version of INIC CS copy |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dvd-firmware"></a>
### STATUS_DVD_FIRMWARE

version of DVD firmware UDS  : $22   ReadDataByIdentifier UDS  : $D057 DVD FW Version Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DVD_FIRMWARE | string | DVD firmware version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-rescue-hw-data"></a>
### RESCUE_HW_DATA

Gerätehardware-Daten wiederherstellen Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STATUS | int | 0, DATEN IN ORDNUNG 1, DATEN ERFOLGREICH WIEDERHERGESTELLT 2, DATEN KORRUPT, NICHT REPARABEL 3, DATEN KORRUPT, FEHLER BEIM WIEDERHERSTELLEN |
| STATUS_TEXT | string | STATUS in Textform |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (125 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (25 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (85 × 2)
- [TWAKEUPSTATUS](#table-twakeupstatus) (3 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (40 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 9)
- [IORTTEXTE](#table-iorttexte) (46 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (8 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (31 × 16)
- [TCONNECTIONTABLE](#table-tconnectiontable) (132 × 2)
- [TCONNECTIONSTATUS](#table-tconnectionstatus) (4 × 2)
- [TAPPLICATION](#table-tapplication) (4 × 2)
- [TAPPLICATIONRUNNINGSTATUS](#table-tapplicationrunningstatus) (3 × 2)
- [TAPPLICATIONACTIVATIONSTATUS](#table-tapplicationactivationstatus) (6 × 2)
- [TKEYNR](#table-tkeynr) (16 × 2)
- [TAUXVERBINDUNG](#table-tauxverbindung) (10 × 2)
- [TVERBINDUNGFEHLERART](#table-tverbindungfehlerart) (4 × 2)
- [TETHERNETCONNECTION](#table-tethernetconnection) (4 × 2)
- [TETHERNETACTIVATIONSTATE](#table-tethernetactivationstate) (3 × 2)
- [TTEMPERATURVERTEILUNG](#table-ttemperaturverteilung) (37 × 1)
- [RES_0XD025](#table-res-0xd025) (8 × 10)
- [T_UWB_ERWEITERT](#table-t-uwb-erweitert) (1 × 2)
- [RES_0XD020](#table-res-0xd020) (1 × 10)
- [ARG_0XD020](#table-arg-0xd020) (1 × 12)
- [RES_0XD02C](#table-res-0xd02c) (2 × 10)
- [TTASTE](#table-ttaste) (11 × 2)
- [ARG_0XA006](#table-arg-0xa006) (1 × 14)
- [ARG_0XA037](#table-arg-0xa037) (1 × 14)
- [ARG_0XA001](#table-arg-0xa001) (3 × 14)
- [RES_0XD003](#table-res-0xd003) (1 × 10)
- [ARG_0XD003](#table-arg-0xd003) (1 × 12)
- [TAUDIOKANAL](#table-taudiokanal) (26 × 2)
- [RES_0XA022](#table-res-0xa022) (2 × 13)
- [ARG_0XA022](#table-arg-0xa022) (1 × 14)
- [ARG_0XA007](#table-arg-0xa007) (1 × 14)
- [RES_0XA04D](#table-res-0xa04d) (1 × 13)
- [RES_0XD014](#table-res-0xd014) (2 × 10)
- [ARG_0XD014](#table-arg-0xd014) (2 × 12)
- [TDEMUTESTATUS](#table-tdemutestatus) (3 × 2)
- [TDEMUTESOURCE](#table-tdemutesource) (5 × 2)
- [TSOURCEDEMUTESTATUS](#table-tsourcedemutestatus) (7 × 2)
- [RES_0XA01E](#table-res-0xa01e) (2 × 13)
- [ARG_0XA01E](#table-arg-0xa01e) (1 × 14)
- [TVERBAUROUTINE](#table-tverbauroutine) (24 × 2)
- [RES_0XD02A](#table-res-0xd02a) (8 × 10)
- [RES_0XA03C](#table-res-0xa03c) (2 × 13)
- [ARG_0XA03C](#table-arg-0xa03c) (1 × 14)
- [TLUEFTERSTATUS](#table-tluefterstatus) (5 × 2)
- [RES_0XA01D](#table-res-0xa01d) (83 × 13)
- [ARG_0XA01D](#table-arg-0xa01d) (1 × 14)
- [TTESTSTATUS](#table-tteststatus) (6 × 2)
- [TVIDEOQUELLE](#table-tvideoquelle) (15 × 2)
- [TVIDEOEINGANGFEHLERART](#table-tvideoeingangfehlerart) (4 × 2)
- [TFBASEINGANG](#table-tfbaseingang) (11 × 2)
- [TEINGANGVIDEOSWITCH](#table-teingangvideoswitch) (11 × 2)
- [TAUSGANGVIDEOSWITCH](#table-tausgangvideoswitch) (11 × 2)
- [RES_0XA024](#table-res-0xa024) (2 × 13)
- [ARG_0XA024](#table-arg-0xa024) (2 × 14)
- [RES_0XD026](#table-res-0xd026) (6 × 10)
- [RES_0XD04E](#table-res-0xd04e) (3 × 10)
- [THWVARIANTE](#table-thwvariante) (62 × 2)
- [THWLIEFERANT](#table-thwlieferant) (7 × 2)
- [THWEINHEIT](#table-thweinheit) (1 × 2)
- [RES_0XA039](#table-res-0xa039) (1 × 13)
- [ARG_0XA039](#table-arg-0xa039) (1 × 14)
- [TINITIALISIERUNG](#table-tinitialisierung) (3 × 2)
- [RES_0XA025](#table-res-0xa025) (1 × 13)
- [ARG_0XA025](#table-arg-0xa025) (1 × 14)
- [TLANGUAGE](#table-tlanguage) (24 × 2)
- [ARG_0XA036](#table-arg-0xa036) (2 × 14)
- [TAUDIOSIGNAL](#table-taudiosignal) (11 × 2)
- [TINSERTEDMEDIUM](#table-tinsertedmedium) (6 × 2)
- [RES_0XD00C](#table-res-0xd00c) (22 × 10)
- [TLAUFWERK](#table-tlaufwerk) (19 × 2)
- [ARG_0XA01A](#table-arg-0xa01a) (3 × 14)
- [TSIGNALART](#table-tsignalart) (9 × 2)
- [TVIDEOAUSGANG](#table-tvideoausgang) (11 × 2)
- [RES_0XA00B](#table-res-0xa00b) (2 × 13)
- [ARG_0XA00B](#table-arg-0xa00b) (1 × 14)
- [TENTSOURCE](#table-tentsource) (27 × 2)
- [TENTSOURCESTATUS](#table-tentsourcestatus) (4 × 2)
- [TSELBSTTESTROUTINE](#table-tselbsttestroutine) (2 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 66 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED |
| 0x13 | ERROR_ECU_INCORRECT_MESSAGE_LENGTH_OR_INVALID_FORMAT |
| 0x14 | ERROR_ECU_RESPONSE_TOO_LONG |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT |
| 0x24 | ERROR_ECU_REQUEST_SEQUENCE_ERROR |
| 0x25 | ERROR_ECU_NO_RESPONSE_FROM_SUBNET_COMPONENT |
| 0x26 | ERROR_ECU_FAILURE_PREVENTS_EXECUTION_OF_REQUESTED_ACTION |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x70 | ERROR_ECU_UPLOAD_DOWNLOAD_NOT_ACCEPTED |
| 0x71 | ERROR_ECU_TRANSFER_DATA_SUSPENDED |
| 0x72 | ERROR_ECU_GENERAL_PROGRAMMING_FAILURE |
| 0x73 | ERROR_ECU_WRONG_BLOCK_SEQUENCE_COUNTER |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x7E | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x7F | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x81 | ERROR_ECU_RPM_TOO_HIGH |
| 0x82 | ERROR_ECU_RPM_TOO_LOW |
| 0x83 | ERROR_ECU_ENGINE_IS_RUNNING |
| 0x84 | ERROR_ECU_ENGINE_IS_NOT_RUNNING |
| 0x85 | ERROR_ECU_ENGINE_RUN_TIME_TOO_LOW |
| 0x86 | ERROR_ECU_TEMPERATURE_TOO_HIGH |
| 0x87 | ERROR_ECU_TEMPERATURE_TOO_LOW |
| 0x88 | ERROR_ECU_VEHICLE_SPEED_TOO_HIGH |
| 0x89 | ERROR_ECU_VEHICLE_SPEED_TOO_LOW |
| 0x8A | ERROR_ECU_THROTTLE_PEDAL_TOO_HIGH |
| 0x8B | ERROR_ECU_THROTTLE_PEDAL_TOO_LOW |
| 0x8C | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_NEUTRAL |
| 0x8D | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_GEAR |
| 0x8F | ERROR_ECU_BRAKE_SWITCH_NOT_CLOSED |
| 0x90 | ERROR_ECU_SHIFTER_LEVER_NOT_IN_PARK |
| 0x91 | ERROR_ECU_TORQUE_CONVERTER_CLUTCH_LOCKED |
| 0x92 | ERROR_ECU_VOLTAGE_TOO_HIGH |
| 0x93 | ERROR_ECU_VOLTAGE_TOO_LOW |
| ?00? | OKAY |
| ?01? | ERROR_ECU_NO_RESPONSE |
| ?02? | ERROR_ECU_INCORRECT_LEN |
| ?03? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?04? | ERROR_ECU_TA_RESPONSE_NOT_SA_REQUEST |
| ?05? | ERROR_ECU_SA_RESPONSE_NOT_TA_REQUEST |
| ?06? | ERROR_ECU_RESPONSE_INCORRECT_DATA_IDENTIFIER |
| ?07? | ERROR_ECU_RESPONSE_TOO_MUCH_DATA |
| ?08? | ERROR_ECU_RESPONSE_TOO_LESS_DATA |
| ?09? | ERROR_ECU_RESPONSE_VALUE_OUT_OF_RANGE |
| ?0A? | ERROR_TABLE |
| ?10? | ERROR_F_CODE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?14? | ERROR_ECU_RESPONSE_INCORRECT_IO_CONTROL_PARAMETER |
| ?15? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_TYPE |
| ?16? | ERROR_ECU_RESPONSE_INCORRECT_SUB_FUNCTION |
| ?17? | ERROR_ECU_RESPONSE_INCORRECT_DYNAMICALLY_DEFINED_DATA_IDENTIFIER |
| ?18? | ERROR_ECU_RESPONSE_NO_STRING_END_CHAR |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 125 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen =&gt; Delphi |
| 0x000002 | Kostal |
| 0x000003 | Hella |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako |
| 0x000008 | Bosch |
| 0x000009 | Loewe =&gt; Lear |
| 0x000010 | VDO |
| 0x000011 | Valeo |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine |
| 0x000018 | Continental Teves |
| 0x000019 | Elektromatik Suedafrika |
| 0x000020 | Becker |
| 0x000021 | Preh |
| 0x000022 | Alps |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi PHI |
| 0x000028 | DODUCO =&gt; BERU |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer |
| 0x000033 | Jatco |
| 0x000034 | Fuba |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE |
| 0x000041 | Megamos |
| 0x000042 | TRW |
| 0x000043 | Wabco |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC (Hella Electronics Corporation) |
| 0x000046 | Gemel |
| 0x000047 | ZF |
| 0x000048 | GMPT |
| 0x000049 | Harman Kardon |
| 0x000050 | Remes |
| 0x000051 | ZF Lenksysteme |
| 0x000052 | Magneti Marelli |
| 0x000053 | Borg Instruments |
| 0x000054 | GETRAG |
| 0x000055 | BHTC (Behr Hella Thermocontrol) |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon |
| 0x000058 | Autoliv |
| 0x000059 | Haberl |
| 0x000060 | Magna Steyr |
| 0x000061 | Marquardt |
| 0x000062 | AB-Elektronik |
| 0x000063 | Siemens VDO Borg |
| 0x000064 | Hirschmann Electronics |
| 0x000065 | Hoerbiger Electronics |
| 0x000066 | Thyssen Krupp Automotive Mechatronics |
| 0x000067 | Gentex GmbH |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steering Europe |
| 0x000071 | NSI B.V |
| 0x000072 | AISIN AW CO.LTD |
| 0x000073 | Shorlock |
| 0x000074 | Schrader |
| 0x000075 | BERU Electronics GmbH |
| 0x000076 | CEL |
| 0x000077 | Audio Mobil |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | AKsys GmbH |
| 0x000086 | META System |
| 0x000087 | Hülsbeck & Fürst GmbH & Co KG |
| 0x000088 | Mann & Hummel Automotive GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.A. |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp. |
| 0x000094 | KÜSTER Automotive Control |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental Automotive |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls |
| 0x00009A | Takata- Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN-Driveline |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | PEIKER acustics GmbH |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | ADC Automotive Distance Control Systems GmbH |
| 0x0000A5 | Funkwerk Dabendorf GmbH |
| 0x0000A6 | Lame |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Wanyu |
| 0x0000A9 | Thyssen Krupp Presta |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA |
| 0x0000AF | Alfmeier |
| 0x0000B0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0x0000B1 | Omron Automotive Electronics Europe Group |
| 0x0000B2 | ASK |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 19 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-prozessklassen"></a>
### PROZESSKLASSEN

Dimensions: 25 rows × 3 columns

| WERT | PROZESSKLASSE | BEZEICHNUNG |
| --- | --- | --- |
| 0x00 | - | ungueltig |
| 0x01 | HWEL | Hardware (Elektronik) |
| 0x02 | HWAP | Hardwareauspraegung |
| 0x03 | HWFR | Hardwarefarbe |
| 0x05 | CAFD | Codierdaten |
| 0x06 | BTLD | Bootloader |
| 0x08 | SWFL | Software ECU Speicherimage |
| 0x09 | SWFF | Flash File Software |
| 0x0A | SWPF | Pruefsoftware |
| 0x0B | ONPS | Onboard Programmiersystem |
| 0x0F | FAFP | FA2FP |
| 0x1A | TLRT | Temporaere Loeschroutine |
| 0x1B | TPRG | Temporaere Programmierroutine |
| 0x07 | FLSL | Flashloader Slave |
| 0x0C | IBAD | Interaktive Betriebsanleitung Daten |
| 0x10 | FCFA | Freischaltcode Fahrzeug-Auftrag |
| 0x1C | BLUP | Bootloader-Update Applikation |
| 0x1D | FLUP | Flashloader-Update Applikation |
| 0x04 | GWTB | Gateway-Tabelle |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xFF | - | ungueltig |

<a id="table-svk-id"></a>
### SVK_ID

Dimensions: 65 rows × 2 columns

| WERT | BEZEICHNUNG |
| --- | --- |
| 0x01 | SVK_AKTUELL |
| 0x02 | SVK_SUPPLIER |
| 0x03 | SVK_WERK |
| 0x04 | SVK_BACKUP_01 |
| 0x05 | SVK_BACKUP_02 |
| 0x06 | SVK_BACKUP_03 |
| 0x07 | SVK_BACKUP_04 |
| 0x08 | SVK_BACKUP_05 |
| 0x09 | SVK_BACKUP_06 |
| 0x0A | SVK_BACKUP_07 |
| 0x0B | SVK_BACKUP_08 |
| 0x0C | SVK_BACKUP_09 |
| 0x0D | SVK_BACKUP_10 |
| 0x0E | SVK_BACKUP_11 |
| 0x0F | SVK_BACKUP_12 |
| 0x10 | SVK_BACKUP_13 |
| 0x11 | SVK_BACKUP_14 |
| 0x12 | SVK_BACKUP_15 |
| 0x13 | SVK_BACKUP_16 |
| 0x14 | SVK_BACKUP_17 |
| 0x15 | SVK_BACKUP_18 |
| 0x16 | SVK_BACKUP_19 |
| 0x17 | SVK_BACKUP_20 |
| 0x18 | SVK_BACKUP_21 |
| 0x19 | SVK_BACKUP_22 |
| 0x1A | SVK_BACKUP_23 |
| 0x1B | SVK_BACKUP_24 |
| 0x1C | SVK_BACKUP_25 |
| 0x1D | SVK_BACKUP_26 |
| 0x1E | SVK_BACKUP_27 |
| 0x1F | SVK_BACKUP_28 |
| 0x20 | SVK_BACKUP_29 |
| 0x21 | SVK_BACKUP_30 |
| 0x22 | SVK_BACKUP_31 |
| 0x23 | SVK_BACKUP_32 |
| 0x24 | SVK_BACKUP_33 |
| 0x25 | SVK_BACKUP_34 |
| 0x26 | SVK_BACKUP_35 |
| 0x27 | SVK_BACKUP_36 |
| 0x28 | SVK_BACKUP_37 |
| 0x29 | SVK_BACKUP_38 |
| 0x2A | SVK_BACKUP_39 |
| 0x2B | SVK_BACKUP_40 |
| 0x2C | SVK_BACKUP_41 |
| 0x2D | SVK_BACKUP_42 |
| 0x2E | SVK_BACKUP_43 |
| 0x2F | SVK_BACKUP_44 |
| 0x30 | SVK_BACKUP_45 |
| 0x31 | SVK_BACKUP_46 |
| 0x32 | SVK_BACKUP_47 |
| 0x33 | SVK_BACKUP_48 |
| 0x34 | SVK_BACKUP_49 |
| 0x35 | SVK_BACKUP_50 |
| 0x36 | SVK_BACKUP_51 |
| 0x37 | SVK_BACKUP_52 |
| 0x38 | SVK_BACKUP_53 |
| 0x39 | SVK_BACKUP_54 |
| 0x3A | SVK_BACKUP_55 |
| 0x3B | SVK_BACKUP_56 |
| 0x3C | SVK_BACKUP_57 |
| 0x3D | SVK_BACKUP_58 |
| 0x3E | SVK_BACKUP_59 |
| 0x3F | SVK_BACKUP_60 |
| 0x40 | SVK_BACKUP_61 |
| 0xXY | ERROR_UNKNOWN |

<a id="table-dtcextendeddatarecordnumber"></a>
### DTCEXTENDEDDATARECORDNUMBER

Dimensions: 5 rows × 3 columns

| WERT | TEXT | ANZ_BYTE |
| --- | --- | --- |
| 0x00 | ISO_RESERVED | 0 |
| 0x01 | CONDITION_BYTE | 1 |
| 0x02 | HFK | 1 |
| 0x03 | HLZ | 1 |
| 0xFF | RECORD_UNKNOWN | 0 |

<a id="table-dtcsnapshotidentifier"></a>
### DTCSNAPSHOTIDENTIFIER

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0xFFFF | IDENTIFIER_UNKNOWN | - | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |

<a id="table-fehlerklasse"></a>
### FEHLERKLASSE

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Keine Fehlerklasse verfuegbar |
| 0x01 | Ueberpruefung bei naechstem Werkstattbesuch |
| 0x02 | Ueberpruefung bei naechstem Halt |
| 0x04 | Ueberpruefung sofort erforderlich ! |
| 0xFF | unbekannte Fehlerklasse |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 11 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x04 | ECUSSDS | ECUSafetySystemDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
| 0x43 | ECUHDD | ECUHDDDownloadSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-uds-tab-roe-aktiv"></a>
### UDS_TAB_ROE_AKTIV

Dimensions: 3 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Aktive Fehlermeldung deaktiviert |
| 0x01 | Aktive Fehlermeldung aktiviert |
| 0xFF | Status der aktiven Fehlermeldung nicht feststellbar |

<a id="table-tfblockidtexte"></a>
### TFBLOCKIDTEXTE

Dimensions: 85 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | NetBlock |
| 0x02 | NetworkMaster |
| 0x03 | ConnectionMaster |
| 0x04 | PowerMaster |
| 0x05 | Vehicle |
| 0x06 | Diagnosis |
| 0x07 | VideoSwitch |
| 0x0F | EnhancedTestability |
| 0x10 | MMI |
| 0x11 | SVS |
| 0x14 | BCStatistic |
| 0x15 | ControlElements |
| 0x20 | AudioMaster |
| 0x22 | AudioAmplifier / AudioAmplifier_HU |
| 0x23 | HeadPhoneAmplifier |
| 0x24 | AuxiliaryInput |
| 0x26 | MicrophoneInput |
| 0x2E | AudioSinkRouter |
| 0x2F | AudioSourceRouter |
| 0x30 | AudioTapePlayer |
| 0x31 | AudioDiskPlayer |
| 0x32 | MultiMediaPlayer |
| 0x40 | AmFmTuner |
| 0x41 | TMCTuner |
| 0x42 | TVTuner |
| 0x43 | DABTuner |
| 0x44 | SatRadio |
| 0x50 | Telephone |
| 0x51 | GeneralPhoneBook / MobileOffice |
| 0x52 | Navigation / NavigationStd |
| 0x54 | Bluetooth |
| 0x6F | Monitor |
| 0x70 | PDC |
| 0x71 | Climate |
| 0x74 | EBA/Services |
| 0x80 | MMI_Terminal |
| 0x81 | Kombi_Terminal |
| 0x82 | HUD_Terminal |
| 0x90 | Telematik |
| 0x91 | InternalAudioSource |
| 0x92 | InternalAudioSink |
| 0xA0 | WLAN |
| 0xA1 | Kleer |
| 0xAB | TollCollect |
| 0xBE | Browser |
| 0xC0 | CANDevices |
| 0xC1 | MPEG-TS_Decoder |
| 0xC9 | Services |
| 0xCA | KombiMiscFKts |
| 0xCB | BordComputer |
| 0xCC | ADASInterface |
| 0xCD | NavigationInfo |
| 0xCE | iSpeech |
| 0xCF | HMIControl |
| 0xD0 | Security |
| 0xD1 | SystemFunction |
| 0xD2 | MultiMediaServer |
| 0xD3 | MassStorageControl |
| 0xD4 | SWUpdate |
| 0xD5 | VirtualControlElements |
| 0xD6 | Vehicle2 |
| 0xD7 | VideoConnectionMaster |
| 0xD8 | VideoSink |
| 0xD9 | EarlyVideoControl |
| 0xDA | MapControl |
| 0xDB | Titelematics |
| 0xDC | DataComIP |
| 0xDD | DUMM |
| 0xDE | TelematikTCU / jetzt TelematicAssist |
| 0xDF | TeleX |
| 0xE0 | KombiInterface |
| 0xE1 | HUDInterface |
| 0xE2 | Camera |
| 0xE3 | MOSTFileSystem |
| 0xE4 | XFCD / Jingle / SoundApplications |
| 0xE5 | CentralControlUnit / CentralControlSystem |
| 0xE6 | TripMemory |
| 0xE7 | RemoteApplication |
| 0xE8 | VideoOutSettings |
| 0xE9 | SoundSignalService |
| 0xEA | PDC |
| 0xEB | DebugApplication |
| 0xED | PIM |
| 0xEE | DataCommunication |
| 0xFF | Nicht definiert |

<a id="table-twakeupstatus"></a>
### TWAKEUPSTATUS

Dimensions: 3 rows × 3 columns

| WERT | TEXT | TEXT2 |
| --- | --- | --- |
| 0 | not initialised | off |
| 1 | SG will be waked up | on |
| 2 | SG are waked up | critical |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 40 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x022600 | Energiesparmode aktiv | 0 |
| 0xB7FC04 | Verbindung RSE zum Infrarot Sender 1 (links): offene Leitung | 0 |
| 0xB7FC05 | Verbindung RSE zum Infrarot Sender 1 (links): Kurzschluss | 0 |
| 0xB7FC06 | Verbindung RSE zum Infrarot Sender 2 (rechts): offene Leitung | 0 |
| 0xB7FC07 | Verbindung RSE zum Infrarot Sender 2 (rechts): Kurzschluss | 0 |
| 0xB7FC08 | Video Eingang 1 (FBAS): kein Video- oder Sync-Signal vorhanden | 1 |
| 0xB7FC09 | Video Eingang 2 (FBAS oder Y von YC): kein Video- oder Synch-Signal vorhanden | 1 |
| 0xB7FC0A | Video Eingang 1 (FBAS): Signal außerhalb Torleranz | 1 |
| 0xB7FC0B | Video Eingang 2 (FBAS oder Y von YC): Signal außerhalb Torleranz | 1 |
| 0xB7FC0D | Video Eingang(gelb) von AV-in links: Signal außerhalb Toleranz | 1 |
| 0xB7FC10 | Video Eingang gelb von AV-in rechts: Signal außerhalb Toleranz | 1 |
| 0xB7FC16 | DVD Laufwerk: Hardware Fehler | 0 |
| 0xB7FC17 | DVD Laufwerk: Software Fehler | 0 |
| 0xB7FC18 | DVD Medium Fehler | 1 |
| 0xB7FC19 | ATC Test negativ: DVD Laufwerk defekt | 0 |
| 0xB7FC1A | Ausfall der Kommunikation der linken hinteren Bildschirm | 1 |
| 0xB7FC1B | Ausfall der Kommunikation der rechten hinteren Bildschirm | 1 |
| 0xB7FC1C | Blende: Kommunikationsfehler | 0 |
| 0xB7FC1D | Blende: Hardware Fehler | 0 |
| 0xB7FC1E | Lüfter Fehler | 0 |
| 0xB7FC1F | Interner Spannungsfehler | 0 |
| 0xB7FC20 | Interner Temperaturfehler | 0 |
| 0xB7FC23 | Externe Unterspannung | 1 |
| 0xB7FC24 | Externe Überspannung | 1 |
| 0xB7FC28 | Codierungsfehler nicht codiert | 0 |
| 0xB7FC29 | Codierungsfehler falsches Fahrzeug | 0 |
| 0xB7FC2A | Codierungsereignis Datenübertragung fehlgeschlagen | 0 |
| 0xB7FC2B | Codierungsereignis Signatur Fehler | 0 |
| 0xB7FC2C | Codierungsereignis ungültige Daten | 0 |
| 0xB7FC2D | Hauptplatine: Hardware Fehler | 0 |
| 0xB7FC2E | Flash File System: fehlerhaft | 0 |
| 0xB7FC2F | Software Fehler (SWE  x ) | 0 |
| 0xD2843F | Empfängerknoten: hat Nachricht nicht abgenommen, Puffer voll | 0 |
| 0xD28440 | Überwachungsschaltung hat Reset ausgelöst | 0 |
| 0xD28442 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt kritische Schwelle | 0 |
| 0xD28444 | MOST: Ring wacht nicht auf | 0 |
| 0xD28445 | Host hat bei fatalem Fehler vom INIC einen Reset ausgelöst | 0 |
| 0x02FF26 | Diagnosemastertest: Dummy Applikation-DTC | 0 |
| 0xD28BFF | Diagnosemastertest: Dummy Netzwerk-DTC | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 3 |
| F_HLZ_VIEW | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1709 | MOST Nachrichten Kopf | text | - | 6 | - | 1 | 1 | 0 |
| 0x170A | FOT Temperatur | Grad_C | high | signed int | - | - | 200 | - |
| 0x170B | Node Position Register | text | - | 1 | - | - | - | - |
| 0x170C | Versorgungsspannung | mVolt | high | unsigned int | - | - | - | - |
| 0x7F00 | ReferenzspannungIR | mVolt | high | unsigned int | - | - | - | - |
| 0x7F01 | Aktuelle SpannungIR | mVolt | high | unsigned int | - | - | - | - |
| 0x7F02 | NVM Block | text | - | 1 | - | 1 | 1 | 0 |
| 0x7F03 | Resetgrund | text | - | 2 | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 46 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x100600 | Ursache DVD Laufwerk Fehler | 0 |
| 0x100601 | Ursache DVD Laufwerk Initianilisierungsfehler | 0 |
| 0x100602 | Ursache Lade-/Auswurffehler | 0 |
| 0x100603 | DVD drive medium RC detection fehler | 0 |
| 0x100700 | Blende: Protokollfehler | 0 |
| 0x100701 | Blende: Alive Fehler | 0 |
| 0x100702 | Blende: Versionsfehler | 0 |
| 0x100703 | Blende: Softwarefehler | 0 |
| 0x100901 | EEPROM CRC Fehler | 0 |
| 0x100902 | HW Videodecoder Fehler | 0 |
| 0x100905 | ASP - Bootfehler | 0 |
| 0x100906 | FPGA - Bootfehler | 0 |
| 0x100908 | INIC is in fail safe mode - Programcode Fehler | 0 |
| 0x100909 | PMC - falsche Softwareversion | 0 |
| 0x10090A | VGC Lifecycle - Bootfehler | 0 |
| 0x10090B | VGC Lifecycle - Watchdog wurde ausgelöst | 0 |
| 0x10090C | VGC: Life Cycle Fehler | 0 |
| 0x10090D | IR Frequenz Fehler | 0 |
| 0x100C01 | ASP - Watchdog wurde ausgelöst | 0 |
| 0x100D00 | Diagnose-Master-Client: Fehler konnte nach max. Anzahl an Versuchen nicht gesendet werden | 0 |
| 0x100D01 | Fehler in FZM-Botschaft | 0 |
| 0x100F00 | Ursache Medium Detektierungsfehler | 1 |
| 0x930000 | Timing-Master: kann Kanal nicht reservieren; Ergebnistabelle (RAT) voll | 0 |
| 0x930001 | Versorgungsspannung: Mindestwert unterschritten | 0 |
| 0x930002 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt Schwelle 1 | 0 |
| 0x930003 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt Schwelle 2 | 0 |
| 0x930004 | Diagnose-Master-Client: Datenzwischenablage im Active Response Handler übergelaufen | 0 |
| 0x930005 | Diagnose-Master-Client: Telegramm Systemzeit nicht fristgerecht erkannt | 0 |
| 0x930006 | MOST: Licht geht unerwartet aus | 0 |
| 0x930007 | MOST: Synchronisation (PLL) arbeitet nicht korrekt | 0 |
| 0x930008 | Systemzustand Ok nicht fristgerecht erkannt | 0 |
| 0x930011 | MOST: Ringbruch | 0 |
| 0x930030 | Timing-Master: kann Audiokanal nicht reservieren; beschäftigt | 0 |
| 0x930031 | Timing-Master: kann Kanal nicht freigeben; beschäftigt | 0 |
| 0x930032 | Timing-Master: kann Kanal nicht freigeben; falsches Label | 0 |
| 0x930033 | Empfängerknoten: hat Nachricht nicht abgenommen; Empfänger existiert nicht | 0 |
| 0x930034 | Empfängerknoten: hat Nachricht nicht abgenommen; fehlerhafte Check-Summe am Empfänger erkannt | 0 |
| 0x930035 | Übertragungsfehler im Hardware Abstraction Layer | 0 |
| 0x930036 | Empfängerknoten: Segmentierungsfehler in Nachricht erkannt | 0 |
| 0x930037 | Senderknoten: Segmentierungsfehler in Nachricht erkannt | 0 |
| 0x930038 | Empfängerknoten: Fehler in Nachrichtenwarteschlange erkannt | 0 |
| 0x930039 | Senderknoten: Fehler in Nachrichtenwarteschlange erkannt | 0 |
| 0x93003A | Empfängerknoten: Kommandointerpreter kennt Nachricht nicht | 0 |
| 0x93003B | Empfängerknoten: mindestens eine Nachricht (Group/Broadcast) nicht abgenommen | 0 |
| 0x93003C | MOST: Ring unerlaubt geweckt | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1709 | MOST Nachrichten Kopf | text | - | 6 | - | 1 | 1 | 0 |
| 0x170A | FOT Temperatur | Grad_C | high | signed int | - | - | 200 | - |
| 0x170B | Node Position Register | text | - | 1 | - | 1 | 1 | 0 |
| 0x170C | Versorgungsspannung | mVolt | high | unsigned int | - | - | - | - |
| 0x7F00 | ReferenzspannungIR | mVolt | high | unsigned int | - | - | - | - |
| 0x7F01 | Aktuelle SpannungIR | mVolt | high | unsigned int | - | - | - | - |
| 0x7F02 | NVM Block | text | - | 1 | - | 1 | 1 | 0 |
| 0x7F03 | Resetgrund | text | - | 2 | - | 1 | 1 | 0 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 31 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_EMERGENCY_EJECT | 0xA007 | - | Notauswurf | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA007 | - |
| STATUS_LESEN_LAUFWERK | 0xD00C | - | Liest aus, welche Laufwerke verbaut sind. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD00C |
| TEST_VIDEOEINGANG | 0xA01D | - | Testet die Videoeingänge durch Analyse der dort anliegenden Sinale | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA01D | RES_0xA01D |
| STEUERN_EJECT | 0xA006 | - | Steuern des Auswurfs der Medien aus den Laufwerken. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA006 | - |
| LANGUAGE | 0xA025 | - | Liest und setzt die aktuelle MMI Sprache. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA025 | RES_0xA025 |
| STATUS_DRIVE_DVD | 0xD006 | STAT_MEDIUM_INSERTED | Liest aktuelle Werte des DVD-Laufwerks aus. | 0-n | - | - | unsigned char | TInsertedMedium | - | - | - | - | 22 | - | - |
| LUEFTER | 0xA03C | - | Steuerung und Status des Lüfters. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA03C | RES_0xA03C |
| SELBSTTEST | 0xA022 | - | Selbsttests des Steuergerätes Sie sollen einen evtl. notwendigen Tausch von Software/Hardware erkennen. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA022 | RES_0xA022 |
| STEUERN_VOLUMEAUDIO | 0xA036 | - | Verstellt die ausgewählte Lautstärke | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA036 | - |
| SIGNALAUSGABE | 0xA01A | - | Steuert die Videosignalausgabe eines Steuergerätes (Videoquelle). | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA01A | - |
| STATUS_INITIALISIERUNG | 0xD004 | STAT_INITIALISIERUNG | Gibt den Gesamt-Initialisierungsstatus des Steuergerätes wieder. | 0-n | - | - | unsigned char | TInitialisierung | - | - | - | - | 22 | - | - |
| STATUS_ANALOG_TEMPERATUR | 0xD026 | - | Abfrage der Temperaturen des Steuergerätes. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD026 |
| AUDIOKANAELE | 0xD003 | - | Verstellt und liest den aktuell eingestellten Lautsprecherkanal. | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD003 | RES_0xD003 |
| NEXT_ENTSOURCE | 0xA00B | - | Steuerung Entertainmentquellen | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA00B | RES_0xA00B |
| TEST_VERBAU | 0xA01E | - | Startet die Verbauprüfung der externen Anschlüsse. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA01E | RES_0xA01E |
| STEUERN_LINEAR | 0xA004 | - | Zurücksetzen der Fader und Lautstärke auf Default-Werte | - | - | - | - | - | - | - | - | - | 31 | - | - |
| STATUS_CD_MD_CDC | 0xD02C | - | Reads out the disc identifier and the quality level of the digital playback. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD02C |
| STATUS_FAN_HISTORY | 0xD02A | - | Reads out the fan histogram. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD02A |
| STATUS_VOLUMEAUDIO | 0xA039 | - | Liest die ausgewählte Lautstärke aus | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA039 | RES_0xA039 |
| STEUERN_VOLUMEAUDIO_DEFAULT | 0xA002 | - | Zurücksetzen aller Lautstärkewerte auf Default-Werte | - | - | - | - | - | - | - | - | - | 31 | - | - |
| MENU | 0xA024 | - | Einstellen eines MMI Menüs. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA024 | RES_0xA024 |
| DEMUTE | 0xD014 | - | Steuert und liest die Mute-Funktion aus | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD014 | RES_0xD014 |
| STEUERN_TRACK_NUMBER | 0xA037 | - | Auswahl der Tracknummer | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA037 | - |
| EXTERNAL_ILLUMINATION | 0xD018 | STAT_EXTERNAL_ILLUMIONATION_WERT | Liefert den Wert der Beleuchtungsstärke des Displays | - | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_TASTE | 0xD013 | STAT_TASTE | Test aller Tasten außer der Functional Bookmarks und des Drehknopfs. | 0-n | - | - | unsigned char | TTaste | - | - | - | - | 22 | - | - |
| SINUSGENERATOR | 0xA001 | - | Gibt einen Sinuston auf einen oder mehrere Kanäle aus. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA001 | - |
| STATUS_HW_VARIANTE | 0xD04E | - | Liefert die HW-Variante der Headunit bzw. von TV/Video-Steuergeräten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD04E |
| LOGISTIC_NR | 0xD020 | - | Schreibt und liest die Logistik Nummer der Auslieferungsvariante. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD020 | RES_0xD020 |
| SER_NR_DOM_LESEN | 0xD019 | STAT_SER_NR_DOM_WERT | liest die 14stellige Car Radio Identification Number(CRIN). | - | - | - | string[14] | - | - | - | - | - | 22 | - | - |
| STATUS_VOLTAGES | 0xD025 | - | - | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD025 |
| STATUS_COUNTER_REGION_CODE | 0xA04D | - | Auslesen des Werts Änderungszähler DVD Ländercode | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA04D |

<a id="table-tconnectiontable"></a>
### TCONNECTIONTABLE

Dimensions: 132 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | AmFmTuner/AudioAmplifier = 0x01  |
| 2 | AmFmTuner/HeadPhoneAmplifier = 0x02  |
| 3 | AmFmTuner/HeadPhoneAmplifier = 0x03  |
| 8 | Null device/AudioAmplifier = 0x08  |
| 9 | Null device/HeadPhoneAmplifier = 0x09  |
| 16 | AmFmTuner/HeadPhoneAmplifier = 0x10  |
| 24 | AudioDiscPlayer/AudioAmplifier = 0x18  |
| 25 | AudioDiscPlayer/HeadPhoneAmplifier = 0x19  |
| 32 | AudioDiscPlayer/AudioAmplifier = 0x20  |
| 33 | AudioDiscPlayer/HeadPhoneAmplifier = 0x21  |
| 34 | AudioDiscPlayer/HeadPhoneAmplifier = 0x22  |
| 40 | MultiMediaPlayer/AudioAmplifier = 0x28  |
| 48 | SVS/AudioAmplifier = 0x30  |
| 64 | Telephone/AudioAmplifier = 0x40  |
| 106 | DABTuner/HeadPhoneAmplifier = 0x6A |
| 80 | TVTuner/AudioAmplifier = 0x50  |
| 81 | TVTuner/HeadPhoneAmplifier = 0x51  |
| 82 | TVTuner/HeadPhoneAmplifier = 0x52  |
| 88 | Navigation/AudioAmplifier = 0x58  |
| 114 | Browser/HeadPhoneAmplifier = 0x72  |
| 56 | AmFmTuner/AudioAmplifier = 0x38  |
| 72 | TelematikTCU/AudioAmplifier = 0x48 |
| 117 | AuxilaryInput/HeadPhoneAmplifier = 0x75  |
| 118 | AuxilaryInput/HeadPhoneAmplifier = 0x76  |
| 119 | AuxilaryInput/AudioAmplifier = 0x77  |
| 120 | AuxilaryInput/HeadPhoneAmplifier = 0x78  |
| 121 | AuxilaryInput/HeadPhoneAmplifier = 0x79  |
| 128 | AuxilaryInput/AudioAmplifier = 0x80  |
| 129 | AuxilaryInput/HeadPhoneAmplifier = 0x81  |
| 130 | AuxilaryInput/HeadPhoneAmplifier = 0x82  |
| 134 | MultiMediaPlayer/AudioAmplifier = 0x86  |
| 132 | PDC/AudioAmplifier = 0x84 |
| 133 | Jingle/AudioAmplifier = 0x85  |
| 4 | AmFmTuner/AudioAmplifier = 0x04  |
| 5 | AmFmTuner/HeadPhoneAmplifier = 0x05  |
| 6 | AmFmTuner/HeadPhoneAmplifier = 0x06  |
| 36 | MultiMediaPlayer/AudioAmplifier = 0x24  |
| 37 | MultiMediaPlayer/HeadPhoneAmplifier = 0x25  |
| 38 | MultiMediaPlayer/HeadPhoneAmplifier = 0x26  |
| 39 | MultiMediaPlayer/AudioAmplifier = 0x27  |
| 41 | MultiMediaPlayer/HeadPhoneAmplifier = 0x29  |
| 67 | Telephone/HeadPhoneAmplifier = 0x43  |
| 68 | Telephone/HeadPhoneAmplifier = 0x44  |
| 69 | Telephone/AudioAmplifier = 0x45  |
| 70 | Telephone/HeadPhoneAmplifier = 0x46  |
| 71 | Telephone/HeadPhoneAmplifier = 0x47  |
| 73 | TelematikTCU/HeadPhoneAmplifier = 0x49  |
| 83 | TVTuner/AudioAmplifier = 0x53  |
| 84 | TVTuner/HeadPhoneAmplifier = 0x54  |
| 85 | TVTuner/HeadPhoneAmplifier = 0x55  |
| 112 | DABTuner/HeadPhoneAmplifier = 0x70  |
| 113 | Browser/AudioAmplifier = 0x71  |
| 115 | Browser/HeadPhoneAmplifier = 0x73  |
| 116 | AuxilaryInput/AudioAmplifier = 0x74  |
| 10 | Null device/HeadPhoneAmplifier = 0x0A  |
| 11 | AmFmTuner/AudioAmplifier = 0x0B  |
| 12 | AmFmTuner/HeadPhoneAmplifier = 0x0C  |
| 14 | AmFmTuner/AudioAmplifier = 0x0E  |
| 15 | AmFmTuner/HeadPhoneAmplifier = 0x0F  |
| 26 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1A  |
| 28 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1C  |
| 29 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1D  |
| 42 | MultiMediaPlayer/HeadPhoneAmplifier = 0x2A  |
| 44 | MicrophoneInput/SVS = 0x2C  |
| 45 | MicrophoneInput/Telephone = 0x2D  |
| 74 | TelematikTCU/HeadPhoneAmplifier = 0x4A  |
| 107 | SatRadio/AudioAmplifier = 0x6B  |
| 108 | SatRadio/HeadPhoneAmplifier = 0x6C  |
| 109 | SatRadio/HeadPhoneAmplifier = 0x6D  |
| 110 | DABTuner/AudioAmplifier = 0x6E  |
| 111 | DABTuner/HeadPhoneAmplifier = 0x6F  |
| 122 | AuxilaryInput/AudioAmplifier = 0x7A  |
| 123 | AuxilaryInput/HeadPhoneAmplifier = 0x7B  |
| 124 | AuxilaryInput/HeadPhoneAmplifier = 0x7C  |
| 125 | AuxilaryInput/AudioAmplifier = 0x7D  |
| 126 | AuxilaryInput/HeadPhoneAmplifier = 0x7E  |
| 127 | AuxilaryInput/HeadPhoneAmplifier = 0x7F  |
| 154 | AuxilaryInput/AudioAmplifier = 0x9A  |
| 155 | AuxilaryInput/HeadPhoneAmplifier = 0x9B  |
| 156 | AuxilaryInput/HeadPhoneAmplifier = 0x9C  |
| 157 | AuxilaryInput/AudioAmplifier = 0x9D  |
| 158 | AuxilaryInput/HeadPhoneAmplifier = 0x9E  |
| 159 | AuxilaryInput/HeadPhoneAmplifier = 0x9F  |
| 160 | AuxilaryInput/AudioAmplifier = 0xA0  |
| 161 | AuxilaryInput/HeadPhoneAmplifier = 0xA1  |
| 162 | AuxilaryInput/HeadPhoneAmplifier = 0xA2  |
| 163 | AuxilaryInput/AudioAmplifier = 0xA3  |
| 164 | AuxilaryInput/HeadPhoneAmplifier = 0xA4  |
| 165 | AuxilaryInput/HeadPhoneAmplifier = 0xA5  |
| 166 | AuxilaryInput/AudioAmplifier = 0xA6  |
| 167 | AuxilaryInput/HeadPhoneAmplifier = 0xA7  |
| 168 | AuxilaryInput/HeadPhoneAmplifier = 0xA8  |
| 169 | AuxilaryInput/AudioAmplifier = 0xA9  |
| 170 | AuxilaryInput/HeadPhoneAmplifier = 0xAA  |
| 171 | AuxilaryInput/HeadPhoneAmplifier = 0xAB  |
| 172 | EntertainmentServer/AudioAmplifier = 0xAC  |
| 173 | EntertainmentServer/HeadPhoneAmplifier = 0xAD  |
| 174 | EntertainmentServer/HeadPhoneAmplifier = 0xAE  |
| 176 | EntertainmentServer/AudioAmplifier = 0xB0  |
| 177 | EntertainmentServer/HeadPhoneAmplifier = 0xB1  |
| 178 | EntertainmentServer/HeadPhoneAmplifier = 0xB2  |
| 179 | EntertainmentServer/AudioAmplifier = 0xB3  |
| 180 | MultiMediaPlayer/AudioAmplifier = 0xB4  |
| 181 | MultiMediaPlayer/HeadPhoneAmplifier = 0xB5  |
| 182 | MultiMediaPlayer/HeadPhoneAmplifier = 0xB6  |
| 183 | MultiMediaPlayer/AudioAmplifier = 0xB7  |
| 184 | Browser/AudioAmplifier = 0xB8  |
| 185 | Browser/HeadPhoneAmplifier = 0xB9  |
| 13 | AmFmTuner/HeadPhoneAmplifier = 0x0D  |
| 27 | AudioDiscPlayer/AudioAmplifier = 0x1B  |
| 18 | Null device/AudioAmplifier = 0x12 |
| 19 | Null device/HeadPhoneAmplifier = 0x13 |
| 20 | Null device/HeadPhoneAmplifier = 0x14 |
| 49 | iSpeechl/AudioAmplifier = 0x31 |
| 50 | iSpeech/AudioAmplifier = 0x32 |
| 104 | DABTuner/AudioAmplifier = 0x68 |
| 105 | DABTuner/HeadPhoneAmplifier = 0x69 |
| 187 | AuxilaryInput/AudioAmplifier = 0xBB |
| 188 | AuxilaryInput/HeadPhoneAmplifier = 0xBC |
| 189 | AuxilaryInput/HeadPhoneAmplifier = 0xBD |
| 46 | MicrophoneInput/iSpeech = 0x2E |
| 47 | MicrophoneInput/iSpeech = 0x2F |
| 186 | Browser/HeadPhoneAmplifier = 0xBA |
| 190 | AuxilaryInput/AudioAmplifier = 0xBE |
| 191 | AuxilaryInput/HeadPhoneAmplifier = 0xBF |
| 192 | AuxilaryInput/HeadPhoneAmplifier = 0xC0 |
| 193 | AuxilaryInput/AudioAmplifier = 0xC1 |
| 194 | AuxilaryInput/HeadPhoneAmplifier = 0xC2 |
| 195 | AuxilaryInput/HeadPhoneAmplifier = 0xC3 |
| 196 | AuxilaryInput/AudioAmplifier = 0xC4 |
| 197 | AuxilaryInput/HeadPhoneAmplifier = 0xC5 |
| 198 | AuxilaryInput/HeadPhoneAmplifier = 0xC6 |

<a id="table-tconnectionstatus"></a>
### TCONNECTIONSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Demuted |
| 0x01 | All.a.Con.a.SAPause.OR.Con.In.Mem. |
| 0x07 | Connection doest exist |
| 0xFF | Unknown |

<a id="table-tapplication"></a>
### TAPPLICATION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RSE Hauptapplikatio |
| 0x01 | Video Applikation |
| 0x02 | Audio Applikation |
| 0xFF | Nicht definiert |

<a id="table-tapplicationrunningstatus"></a>
### TAPPLICATIONRUNNINGSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Applikation nicht gestartet |
| 0x01 | Applikation gestartet |
| 0xFF | Nicht definiert |

<a id="table-tapplicationactivationstatus"></a>
### TAPPLICATIONACTIVATIONSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Deaktiviert durch Codierung |
| 0x02 | Aktiviert durch Codierung |
| 0x04 | Deaktiviert durch SWT |
| 0x08 | Aktiviert durch SWT |
| 0x10 | Teilweise Aktiviert durch SWT |
| 0xFF | Nicht definiert |

<a id="table-tkeynr"></a>
### TKEYNR

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Schlüssel 1 |
| 0x02 | Schlüssel 2 |
| 0x03 | Schlüssel 3 |
| 0x04 | Schlüssel 4 |
| 0x05 | Schlüssel 5 |
| 0x06 | Schlüssel 6 |
| 0x07 | Schlüssel 7 |
| 0x08 | Schlüssel 8 |
| 0x09 | Schlüssel 9 |
| 0x0A | Schlüssel 10 |
| 0x0B | Schlüssel 11 |
| 0x0C | Schlüssel 12 |
| 0x0D | Schlüssel 13 |
| 0x0E | Schlüssel 14 |
| 0x0F | Schlüssel 15 |
| 0xFF | Alle Schlüssel |

<a id="table-tauxverbindung"></a>
### TAUXVERBINDUNG

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Aux Verbindungen |
| 0x0001 | Aux In Audio |
| 0x0100 | Aux In RSE links |
| 0x0200 | Aux In RSE rechts |
| 0x0300 | Aux In RSE links und rechts |
| 0x0400 | Aux In RSE BMW Individual |
| 0x0500 | Aux In RSE links und BMW Individual |
| 0x0600 | Aux In RSE rechts und BMW Individual |
| 0x0700 | Aux In RSE links, rechts und BMW Individual |
| 0xFFFF | Nicht definiert |

<a id="table-tverbindungfehlerart"></a>
### TVERBINDUNGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-tethernetconnection"></a>
### TETHERNETCONNECTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Alle |
| 0x01 | Ethernet Verbindung für den Flash-Prozess |
| 0x02 | Ethernet Verbindung zum RSE |
| 0xFF | Nicht definiert |

<a id="table-tethernetactivationstate"></a>
### TETHERNETACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Deaktiviert |
| 0x01 | Aktiviert |
| 0xFF | Nicht definiert |

<a id="table-ttemperaturverteilung"></a>
### TTEMPERATURVERTEILUNG

Dimensions: 37 rows × 1 columns

| TEMPERATURERANGE |
| --- |
| -40°C to -35°C |
| -35°C to -30°C |
| -30°C to -25°C |
| -25°C to -20°C |
| -20°C to -15°C |
| -15°C to -10°C |
| -10°C to -5°C |
| -5°C to 0°C |
| 0°C to 5°C |
| 5°C to 10°C |
| 10°C to 15°C |
| 15°C to 20°C |
| 20°C to 25°C |
| 25°C to 30°C |
| 30°C to 35°C |
| 35°C to 40°C |
| 40°C to 45°C |
| 45°C to 50°C |
| 50°C to 55°C |
| 55°C to 60°C |
| 60°C to 65°C |
| 65°C to 70°C |
| 70°C to 75°C |
| 75°C to 80°C |
| 80°C to 85°C |
| 85°C to 90°C |
| 90°C to 95°C |
| 95°C to 100°C |
| 100°C to 105°C |
| 105°C to 110°C |
| 110°C to 115°C |
| 115°C to 120°C |
| 120°C to 125°C |
| 125°C to 130°C |
| 130°C to 135°C |
| 135°C to 140°C |
| Maximale Temperatur |

<a id="table-res-0xd025"></a>
### RES_0XD025

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_3.3V_SW1_WERT | V | - | unsigned int | - | - | - | - | - | - |
| STAT_3.3V_SW2_WERT | V | - | unsigned int | - | - | - | - | - | - |
| STAT_3V_SW_WERT | V | - | unsigned int | - | - | - | - | - | - |
| STAT_5V_SW_WERT | V | - | unsigned int | - | - | - | - | - | - |
| STAT_BATTERY_VOLTAGE_WERT | V | - | unsigned int | - | - | - | - | - | Numerische Ausgabe der Batteriespannung |
| STAT_SPG_BOARD_WERT | mV | - | unsigned int | - | - | - | - | - | - |
| STAT_SPG_FPGA_WERT | mV | - | unsigned int | - | - | - | - | - | - |
| STAT_SPG_SH3_WERT | mV | - | unsigned int | - | - | - | - | - | - |

<a id="table-t-uwb-erweitert"></a>
### T_UWB_ERWEITERT

Dimensions: 1 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0xFFFFFFF | Nachrichten Kopf |

<a id="table-res-0xd020"></a>
### RES_0XD020

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LOGISTIC_NR_WERT | - | - | string[7] | - | - | - | - | - | Auslesen der Logistik-Nummer. ACHTUNG: RESULT wird von _WERT auf _TEXT gewandelt! |

<a id="table-arg-0xd020"></a>
### ARG_0XD020

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_LOGISTIC_NR | - | - | string[7] | - | - | - | - | - | - | - | die zu schreibende Logistiknummer |

<a id="table-res-0xd02c"></a>
### RES_0XD02C

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DISC_IDENT_WERT | - | - | string | - | - | - | - | - | Disk Identifier für das beinhaltete Medium. ACHTUNG: RÜCKGABE wird von _WERT zu _TEXT! |
| STAT_DIGITAL_PLAYBACK_QUALITY_WERT | - | - | unsigned char | - | - | - | - | - | Quality level of the digital playback Range: 0-15 0-1: Media not readable (drive not ok) 2-8: Mutes or distortion which is customer related (drive not ok) 9-14: Media readable, no customer related distortion (drive ok) 15: Media quality 100%, e.g. BLER 0 (drive ok) |

<a id="table-ttaste"></a>
### TTASTE

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Taste gedrückt |
| 0x01 | Auswurf CD |
| 0x02 | Auswurf DVD |
| 0x03 | Entertainment Knopf |
| 0x04 | Suchlauf abwärts - Skip links |
| 0x05 | Suchlauf aufwärts - Skip rechts |
| 0x10 | RSE Einschaltknopf links |
| 0x11 | RSE Einschaltknopf rechts |
| 0x12 | RSE Auswurf DVD |
| 0x13 | MIODE-Taste |
| 0xFF | Nicht definiert |

<a id="table-arg-0xa006"></a>
### ARG_0XA006

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DRIVE | + | - | - | - | unsigned int | - | - | - | - | - | - | - | gibt an, auf welchem Laufwerk der  Eject ausgeführt werden soll. Default 4 Tabelle TLaufwerk |

<a id="table-arg-0xa037"></a>
### ARG_0XA037

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_TRACK | + | - | - | - | unsigned int | - | - | - | - | - | - | - | Wählt die CD/DVD-Tracknummer die abgespielt werden soll. |

<a id="table-arg-0xa001"></a>
### ARG_0XA001

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_FREQUENZ | + | - | Hz | - | unsigned int | - | - | - | - | - | 20 | 20000 | Frequenzeinstellung: 20..20 000 Hz |
| ARG_LEVEL | + | - | - | - | char | - | - | - | - | - | -96 | 127 | Bei Headunits:  Hex-Wert, von 0x00 lückenlos bis 0x7F, Nicht unterstützte Werte (Stereo: 0x3F) dürfen nicht zu Fehlermeldungen führen. Sondern die für das Lautsprechersystem nächstmöglich kleinere verfügbare Lautstärke wird eingestellt.    Bei Verstärkern: Integer, -96..0 [dB] |
| ARG_KANAL | + | - | - | - | unsigned long | - | - | - | - | - | - | - | bezeichnet den Kanal, auf dem ausgegeben werden soll. |

<a id="table-res-0xd003"></a>
### RES_0XD003

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KANAL | 0-n | - | unsigned long | - | TAudioKanal | - | - | - | Kanalnummer |

<a id="table-arg-0xd003"></a>
### ARG_0XD003

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_KANAL | - | - | unsigned long | - | - | - | - | - | - | - | Kanalnummer |

<a id="table-taudiokanal"></a>
### TAUDIOKANAL

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Kanäle |
| 0x00000001 | Links vorne (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000002 | Rechts vorne (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000004 | Center vorne (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000008 | Seite links (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000010 | Seite rechts (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000020 | Links hinten (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000040 | Rechts hinten (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000080 | Links vorne Bass (Erweiterter Kanal) |
| 0x00000100 | Rechts vorne Bass (Erweiterter Kanal) |
| 0x00000200 | Links hinten Bass (Erweiterter Kanal) |
| 0x00000400 | Rechts hinten Bass (Erweiterter Kanal) |
| 0x00000800 | Center hinten (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00001000 | Linker Kopfhörer links |
| 0x00002000 | Linker Kopfhörer rechts |
| 0x00004000 | Rechter Kopfhörer links |
| 0x00008000 | Rechter Kopfhörer rechts |
| 0x00010000 | Links vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00020000 | Rechts vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00040000 | Center vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00080000 | Seite links (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00100000 | Seite rechts (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00200000 | Links hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00400000 | Rechts hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00800000 | Center hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-res-0xa022"></a>
### RES_0XA022

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SELBSTTEST_ROUTINE | - | - | + | 0-n | - | unsigned long | - | TSelbsttestRoutine | - | - | - | Routine(n), die getestet wurde(n). Tabelle  TSelbsttestRoutine |
| STAT_SELBSTTEST | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des Tests wieder. |

<a id="table-arg-0xa022"></a>
### ARG_0XA022

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SELBSTTEST_ROUTINE | + | - | - | - | unsigned long | - | - | - | - | - | - | - | Routinen, die getestet werden sollen. Die Tabelle TSelbsttestRoutine wird in der SGBD von der Entwicklung bzw. vom Zulieferer befüllt und gepflegt. |

<a id="table-arg-0xa007"></a>
### ARG_0XA007

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DRIVE | + | - | - | - | unsigned int | - | - | - | - | - | - | - | gibt an, auf welchem Laufwerk der  Eject ausgeführt werden soll. Default: 4 Tabelle TLaufwerk |

<a id="table-res-0xa04d"></a>
### RES_0XA04D

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_COUNTER_REGION_CODE_WERT | - | - | + | - | - | unsigned char | - | - | - | - | - | Wert Änderugszähler DVD Ländercode |

<a id="table-res-0xd014"></a>
### RES_0XD014

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DEMUTE_SOURCE1 | 0-n | - | unsigned char | - | TSourceDemuteStatus | - | - | - | Gibt den eingestellten Mute-Modus zurück: Für Source1 sind nur die Werte 0-3 gültig. |
| STAT_DEMUTE_SOURCE2 | 0-n | - | unsigned char | - | TSourceDemuteStatus | - | - | - | Gibt den eingestellten Mute-Modus zurück: Für Source2 sind nur die Werte 4-5 gültig. Bei Headunits wird hier 255 zurückgeliefert. |

<a id="table-arg-0xd014"></a>
### ARG_0XD014

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DEMUTE | 0-n | - | unsigned char | - | TDemuteStatus | - | - | - | - | - | - |
| ARG_HEADPHONES | 0-n | - | unsigned char | - | TDemuteSource | - | - | - | - | - | - |

<a id="table-tdemutestatus"></a>
### TDEMUTESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stummschaltung ein |
| 0x01 | Stummschaltung aus |
| 0xFF | Nicht definiert |

<a id="table-tdemutesource"></a>
### TDEMUTESOURCE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht benutzt(Default in Headunit) |
| 0x01 | Kopfhörer links |
| 0x02 | Kopfhörer rechts |
| 0x03 | Beide Kopfhörer |
| 0xFF | Nicht definiert |

<a id="table-tsourcedemutestatus"></a>
### TSOURCEDEMUTESTATUS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Head-Unit aus |
| 0x01 | Head-Unit ein |
| 0x02 | RSE Kopfhörer links aus |
| 0x03 | RSE Kopfhörer links ein |
| 0x04 | RSE Kopfhörer rechts aus |
| 0x05 | RSE Kopfhörer rechts ein |
| 0xFF | Nicht definiert |

<a id="table-res-0xa01e"></a>
### RES_0XA01E

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAU_ROUTINE | - | - | + | 0-n | - | unsigned long | - | TVerbauRoutine | - | - | - | Ausgeführte Testroutine(n). |
| STAT_TEST_VERBAU | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des Verbautests wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. |

<a id="table-arg-0xa01e"></a>
### ARG_0XA01E

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_VERBAU_ROUTINE | + | - | - | - | unsigned long | - | - | - | - | - | - | - | Routinen, die getestet werden sollen. Tabelle TVerbauRoutine |

<a id="table-tverbauroutine"></a>
### TVERBAUROUTINE

Dimensions: 24 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Routinen |
| 0x00000001 | Verbindung Head-Unit zum Diversity |
| 0x00000002 | Verbindung Diversity zu den Antennen |
| 0x00000004 | Verbindung Head-Unit zum DAB L-Band Antennenfuß |
| 0x00000008 | Verbindung Head-Unit zum DAB Band III Antennenfuß |
| 0x00000010 | Verbindung Head-Unit zum GPS-Antennenfuß |
| 0x00000020 | Verbindung Head-Unit zum Aux-In Box |
| 0x00000040 | Lautsprecherausgangsleitungen (Stereo System) |
| 0x00000080 | Ausgangsleitungen zum HiFi Verstärker |
| 0x00000100 | RAD ON Leitung |
| 0x00000200 | Verbindung Head-Unit zum Mikrofon 1 |
| 0x00000400 | Verbindung Head-Unit zum Mikrofon 2 |
| 0x00000800 | Verbindung Head-Unit zum VICS FM Antennenfuß |
| 0x00001000 | Verbindung Head-Unit zum VICS Beacon Antennenfuß |
| 0x00002000 | Verbindung Head-Unit zum ETC-Spiegel |
| 0x00004000 | Ethernet-Verbindung Head-Unit zum ZGW |
| 0x00008000 | Ethernet-Verbindung Head-Unit zum RSE High |
| 0x00010000 | Verbindung Head-Unit zur USB Kunden-Schnittstelle |
| 0x00020000 | Verbindungen zu IR-Sendeeinheit |
| 0x00040000 | Verbindung Head-Unit zum SDARS Antennenfuß |
| 0x00080000 | Verbindung Head-Unit zur Bluetooth Antenne |
| 0x00100000 | Ethernet-Verbindung Head-Unit zur Combox |
| 0x00200000 | Ethernet-Verbindung RSE High zur Combox |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-res-0xd02a"></a>
### RES_0XD02A

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIME_FAN_ALL_WERT | s | - | unsigned long | - | - | - | - | - | Whole operating time of the fan in seconds. |
| STAT_OCCURENCES_FAN_SWITCH_ON_WERT | - | - | unsigned long | - | - | - | - | - | Number of switch ON occurrences |
| STAT_TIME_FAN_OFF_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is not running |
| STAT_TIME_FAN_MIN_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is running at its minimal rotation speed (quietmode) |
| STAT_TIME_FAN_INTERMEDIATE1_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is running at an intermediate rotation speed for which the voltage v1 is: minimal rotation speed &lt; v1 &lt;= 6V |
| STAT_TIME_FAN_INTERMEDIATE2_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is running at an intermediate rotation speed for which the voltage v2 is: 6V &lt; v2 &lt; = 8V |
| STAT_TIME_FAN_INTERMEDIATE3_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is running at an intermediate rotation speed for which the voltage v3 is: 8V &lt; v3 &lt; = 10V |
| STAT_TIME_FAN_MAX_WERT | s | - | unsigned long | - | - | - | - | - | Time in seconds the fan is running at its maximal rotation speed |

<a id="table-res-0xa03c"></a>
### RES_0XA03C

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LUEFTER | - | - | + | 0-n | - | unsigned char | - | TLuefterStatus | - | - | - | Status des Lüfters. |
| STAT_LUEFTER_DREHZAHL_WERT | - | - | + | Hz | - | unsigned int | - | - | - | - | - | Aktuelle Frequenz des Lüfters in Hz. (Wenn nicht abfragbar, wird 0xFFFF zurückgegeben) |

<a id="table-arg-0xa03c"></a>
### ARG_0XA03C

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DURATION | + | - | - | - | unsigned char | - | - | - | - | - | 0 | 30 | legt die Dauer in Sekunden fest, die der Lüfter auf Maximum läuft. |

<a id="table-tluefterstatus"></a>
### TLUEFTERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Lüfter steht |
| 0x01 | Lüfter läuft, aber nicht mit der erwarteteten Drehzahl |
| 0x02 | Lüfter läuft mit der erwarteteten Drehzahl |
| 0xFE | Lüfter läuft mit unbekannter Drehzahl |
| 0xFF | Nicht definiert |

<a id="table-res-0xa01d"></a>
### RES_0XA01D

Dimensions: 83 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt nach Tabelle TVideoQuelle bzw. TEingangVideoSwitch an, welche Quelle(n) getestet wurde(n). |
| STAT_TEST_VIDEOEINGANG | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des gesamten Tests oder der entsprechenden Quelle(n) wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. |
| STAT_ANZAHL_FEHLERHAFTE_SIGNALE_WERT | - | - | + | - | - | unsigned char | - | - | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 2 oder 3 meldet. Gibt wieder, wie vielen Fehler während des Test gefunden wurden. |
| STAT_FEHLER_1_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_1_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. X ist kleiner gleich der Anzahl der auf das Steuergerät schaltbaren Quellen. Für den Videoswitch und Monitore sind die schaltbaren Quellen gleich der Anzahl der Eingänge. Bei  N theoretisch verbaubaren und schaltbaren Quellen muss dieses Result N-mal implementiert werden. Beispiel falls es nur möglichen Quellen gäbe: STAT_FEHLER_1_ FEHLERART, STAT_FEHLER_2_ FEHLERART |
| STAT_FEHLER_1_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_1_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_1_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_2_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_2_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_2_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_2_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_2_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_3_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_3_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_3_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_3_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_3_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_4_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_4_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_4_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_4_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_4_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_5_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_5_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_5_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_5_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_5_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_6_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_6_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_6_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_6_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_6_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_7_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_7_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_7_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_7_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_7_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_8_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_8_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_8_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_8_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_8_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_9_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_9_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_9_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_9_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_9_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_10_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_10_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_10_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_10_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_10_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_11_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_11_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_11_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_11_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_11_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_12_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_12_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_12_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_12_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_12_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_13_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_13_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_13_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_13_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_13_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_14_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_14_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_14_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_14_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_14_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_15_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_15_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_15_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_15_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_15_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_16_QUELLE | - | - | + | 0-n | - | unsigned long | - | TVideoQuelle | - | - | - | Gibt die Videoquelle wieder, bei der der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_16_FEHLERART_SIGNAL | - | - | + | 0-n | - | unsigned char | - | TVideoeingangFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Test: 0 kein Video- oder Sync-Signal vor-handen, 1 Signal außerhalb der Toleranz, & & 255 Nicht definiert. Gibt wieder, als Integer, welcher Art der X. Fehler war. |
| STAT_FEHLER_16_EINGANG | - | - | + | 0-n | - | unsigned long | - | TFBasEingang | - | - | - | Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet.  Gibt wieder, als Integer, auf welchem Eingang der X. Fehler gefunden wurde. |
| STAT_FEHLER_16_VIDEOSWITCH_EINGANG | - | - | + | 0-n | - | unsigned int | - | TEingangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Eingang des Videoswitches geroutet wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_16_VIDEOSWITCH_AUSGANG | - | - | + | 0-n | - | unsigned int | - | TAusgangVideoSwitch | - | - | - | Wertet die durch STEUERN_TEST_VIDEOEINGANG ausgeführten Tests aus. Gibt an, welcher Ausgang des Videoswitches geroutet wurde. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. |

<a id="table-arg-0xa01d"></a>
### ARG_0XA01D

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_QUELLE | + | - | - | - | unsigned long | - | - | - | - | - | 0 | - | Wertet das Signal von einer oder mehreren Quellen aus. Legt die Videoquelle fest, von der aus das Signal auf die Senke geroutet wird: Tabelle TVideoQuelle bzw. TEingangVideoSwitch |

<a id="table-tteststatus"></a>
### TTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tvideoquelle"></a>
### TVIDEOQUELLE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Quellen |
| 0x00000001 | MMC |
| 0x00000002 | NiVi |
| 0x00000004 | RFK |
| 0x00000008 | TV |
| 0x00000010 | TopView |
| 0x00000020 | Entertainmentserver |
| 0x00000040 | Headunit |
| 0x00000080 | RearSeatEntertainment |
| 0x00000100 | SideView |
| 0x00000200 | AUX1 |
| 0x00000400 | AUX2 |
| 0x00000800 | AUX3 |
| 0x00001000 | AUX4 |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tvideoeingangfehlerart"></a>
### TVIDEOEINGANGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Video- oder Sync-Signal vorhanden |
| 0x01 | Signal außerhalb der Toleranz |
| 0x02 | Verbindung konnte nicht hergestellt werden |
| 0xFF | Nicht definiert |

<a id="table-tfbaseingang"></a>
### TFBASEINGANG

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Eingänge |
| 0x00000001 | FBAS-Eingang 1 |
| 0x00000002 | FBAS-Eingang 2 |
| 0x00000004 | FBAS-Eingang 3 |
| 0x00000008 | FBAS-Eingang 4 |
| 0x00000010 | FBAS-Eingang 5 |
| 0x00000020 | FBAS-Eingang 6 |
| 0x00000040 | FBAS-Eingang 7 |
| 0x00000080 | FBAS-Eingang 8 |
| 0x00000100 | FBAS-Eingang 9 |
| 0xFFFFFFFF | nicht definiert |

<a id="table-teingangvideoswitch"></a>
### TEINGANGVIDEOSWITCH

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Kein VideoSwitch vorhanden bzw. verwendet |
| 0x0001 | Eingang 1 |
| 0x0002 | Eingang 2 |
| 0x0004 | Eingang 3 |
| 0x0008 | Eingang 4 |
| 0x0010 | Eingang 5 |
| 0x0020 | Eingang 6 |
| 0x0040 | Eingang 7 |
| 0x0080 | Eingang 8 |
| 0x0100 | Eingang 9 |
| 0xFFFF | Nicht definiert |

<a id="table-tausgangvideoswitch"></a>
### TAUSGANGVIDEOSWITCH

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Kein VideoSwitch vorhanden bzw. verwendet |
| 0x0001 | Ausgang 1 |
| 0x0002 | Ausgang 2 |
| 0x0004 | Ausgang 3 |
| 0x0008 | Ausgang 4 |
| 0x0010 | Ausgang 5 |
| 0x0020 | Ausgang 6 |
| 0x0040 | Ausgang 7 |
| 0x0080 | Ausgang 8 |
| 0x0100 | Ausgang 9 |
| 0xFFFF | Nicht definiert |

<a id="table-res-0xa024"></a>
### RES_0XA024

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MENU_WERT | - | - | + | - | - | unsigned long | - | - | - | - | - | ID des Menüs. |
| STAT_MENU_RSE_RIGHT_WERT | - | - | + | - | - | unsigned long | - | - | - | - | - | ID des Menü der zweiten MMI, z.B. RSE rechter Bildschirm. |

<a id="table-arg-0xa024"></a>
### ARG_0XA024

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_MENU | + | - | - | - | unsigned long | - | - | - | - | - | - | - | Einstellen eines MMI Menüs. |
| ARG_MENU_RSE_RIGHT | + | - | - | - | unsigned long | - | - | - | - | - | - | - | ID des Menüs der zweiten MMI, z.B. RSE rechter Bildschirm. |

<a id="table-res-0xd026"></a>
### RES_0XD026

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_FOT_WERT | °C | - | char | - | - | - | - | - | liefert die Temperatur des Fibre Optical Transceivers (FOT). Bereich: -127,&,127 |
| STAT_TEMP_ENDSTU_WERT | °C | - | int | - | - | - | - | - | liefert die Temperatur der Endstufe. Bereich: -32767,&, 32767 |
| STAT_TEMP_GYRO_WERT | °C | - | char | - | - | - | - | - | liefert die Temperatur des Gyro. Bereich: -127,&,127 |
| STAT_TEMP_MOD_WERT | °C | - | char | - | - | - | - | - | liefert die Temperatur des Moduls (normalerweise prozessornah). Bereich: -127,&,127 |
| STAT_TEMP_HDD_WERT | °C | - | char | - | - | - | - | - | liefert die Temperatur des HDD-Laufwerks. Bereich: -127,&,127 |
| STAT_TEMP_DVD_WERT | °C | - | char | - | - | - | - | - | liefert die Temperatur des DVD-Laufwerks. Bereich: -127,&,127 |

<a id="table-res-0xd04e"></a>
### RES_0XD04E

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HW_VARIANTE | 0-n | - | unsigned long | - | THwVariante | - | - | - | liefert nach Tabelle THwVariante(Bitkombination) eindeutig, welche Variante vorliegt.  Z.B. liefert ein CIC HIGH mit IBOC den Wert 0x10004 (=0x4+0x10000) |
| STAT_HW_VARIANTE_LIEFERANT | 0-n | - | unsigned char | - | THwLieferant | - | - | - | gibt den Lieferanten nach Tabelle THwLieferant aus. |
| STAT_HW_EINHEIT | 0-n | - | unsigned long | - | THwEinheit | - | - | - | liefert eine eindeutige ID der Hardwarevariante. Die Tabelle THwEinheit ist von der Entwicklung in der SGBD zu pflegen. 0xFFFFFFFF bedeutet  nicht definiert |

<a id="table-thwvariante"></a>
### THWVARIANTE

Dimensions: 62 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Headunit Stufe 1 (Radio Business) |
| 0x00000001 | Headunit Stufe 2 (Radio Professional) |
| 0x00000002 | Headunit Stufe 3 (Navigation Business) |
| 0x00000004 | Headunit Stufe 4 (Navigation Professional) |
| 0x00000008 | RearSeatEntertainment Mid |
| 0x00000010 | RearSeatEntertainment High |
| 0x00000020 | TV-Modul DVB-T |
| 0x00000040 | TV-Modul DVB-T RSE |
| 0x00000080 | TV-Modul ISDB-T |
| 0x00000100 | VideoSwitch Mid |
| 0x00000200 | VideoSwitch High |
| 0x00010000 | mit Funktion IBOC |
| 0x00020000 | mit Funktion DAB |
| 0x00040000 | mit Funktion Video-in |
| 0x00080000 | mit Funktion SDARS |
| 0x00100000 | mit Funktion Telefon |
| 0x00200000 | mit Funktion I-Speech |
| 0x00400000 | mit Funktion CD-Laufwerk |
| 0xFFFFFFF1 | --- Bitkombinationen Headunit Stufe 1 (Radio Business) --- |
| 0x00010001 | Headunit Stufe 1 (Radio Business) mit Funktion IBOC |
| 0x00020001 | Headunit Stufe 1 (Radio Business) mit Funktion DAB |
| 0x00080001 | Headunit Stufe 1 (Radio Business) mit Funktion SDARS |
| 0xFFFFFFF2 | --- Bitkombinationen Headunit Stufe 2 (Radio Professional) --- |
| 0x00410002 | Headunit Stufe 2 (Radio Professional) mit Funktion IBOC und CD-Laufwerk |
| 0x00490002 | Headunit Stufe 2 (Radio Professional) mit Funktion IBOC, SDARS und CD-Laufwerk |
| 0x006D0002 | Headunit Stufe 2 (Radio Professional) mit Funktion IBOC, SDARS, Video-In, I-Speech und CD-Laufwerk |
| 0x002D0002 | Headunit Stufe 2 (Radio Professional) mit Funktion IBOC, SDARS, Video-In und I-Speech |
| 0x00500002 | Headunit Stufe 2 (Radio Professional) mit Funktion Telefon und CD-Laufwerk |
| 0x00640002 | Headunit Stufe 2 (Radio Professional) mit Funktion Video-In, I-Speech und CD-Laufwerk |
| 0x00760002 | Headunit Stufe 2 (Radio Professional) mit Funktion DAB, Video-In, Telefon, I-Speech und CD-Laufwerk |
| 0x00020002 | Headunit Stufe 2 (Radio Professional) mit Funktion Video-In, Telefon, I-Speech |
| 0xFFFFFFF3 | --- Bitkombinationen Headunit Stufe 3 (Navigation Business) --- |
| 0x00340003 | Headunit Stufe 3 (Navigation Business) mit Funktion Video-in, Telefon und I-Speech |
| 0x00360003 | Headunit Stufe 3 (Navigation Business) mit Funktion DAB, Video-in, Telefon und I-Speech |
| 0x00090003 | Headunit Stufe 3 (Navigation Business) mit Funktion IBOC und SDARS |
| 0x004B0003 | Headunit Stufe 3 (Navigation Business) mit Funktion IBOC,Video-In, SDARS, I-Speech |
| 0xFFFFFFF4 | --- Bitkombinationen Headunit Stufe 4 (Navigation Professional) --- |
| 0x00040004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in |
| 0x00050004 | Headunit Stufe 4 (Navigation Professional) mit Funktion IBOC und Video-in |
| 0x00060004 | Headunit Stufe 4 (Navigation Professional) mit Funktion DAB und Video-in |
| 0x000D0004 | Headunit Stufe 4 (Navigation Professional) mit Funktion IBOC, SDARS und Video-in |
| 0x01040004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in als Japan-Variante |
| 0x02040004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in als China/Korea-Variante |
| 0x00140004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in und Telefon |
| 0x00150004 | Headunit Stufe 4 (Navigation Professional) mit Funktion IBOC und Video-in und Telefon |
| 0x00160004 | Headunit Stufe 4 (Navigation Professional) mit Funktion DAB und Video-in und Telefon |
| 0x001D0004 | Headunit Stufe 4 (Navigation Professional) mit Funktion IBOC, SDARS und Video-in und Telefon |
| 0x01140004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in und Telefon als Japan-Variante |
| 0x02140004 | Headunit Stufe 4 (Navigation Professional) mit Funktion Video-in und Telefon als China/Korea-Variante |
| 0xFFFFFFF5 | --- Bitkombinationen RearSeatEntertainment Mid --- |
| 0x00040008 | RearSeatEntertainment Mid mit Funktion Video-in |
| 0x01000008 | RearSeatEntertainment Mid als Japan-Variante |
| 0x02000008 | RearSeatEntertainment Mid als China/Korea-Variante |
| 0x01040008 | RearSeatEntertainment Mid mit Funktion Video-in als Japan-Variante |
| 0x02040008 | RearSeatEntertainment Mid mit Funktion Video-in als China/Korea-Variante |
| 0xFFFFFFF6 | --- Bitkombinationen RearSeatEntertainment High --- |
| 0x00040010 | RearSeatEntertainment High mit Funktion Video-in |
| 0x01000010 | RearSeatEntertainment High als Japan-Variante |
| 0x02000010 | RearSeatEntertainment High als China/Korea-Variante |
| 0x01040010 | RearSeatEntertainment High mit Funktion Video-in als Japan-Variante |
| 0x02040010 | RearSeatEntertainment High mit Funktion Video-in als China/Korea-Variante |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-thwlieferant"></a>
### THWLIEFERANT

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Harman Becker |
| 0x01 | Siemens VDO |
| 0x02 | Visteon |
| 0x03 | Alpine |
| 0x04 | Lear |
| 0x05 | Fuba |
| 0xFF | Nicht definiert |

<a id="table-thweinheit"></a>
### THWEINHEIT

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xFF | Nicht definiert |

<a id="table-res-0xa039"></a>
### RES_0XA039

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LEVEL_WERT | + | - | - | - | - | char | - | - | - | - | - | Bei Headunits:  Hex-Wert, von 0x00 lückenlos bis 0x7F, Nicht unterstützte Werte (Stereo: 0x3F) dürfen nicht zu Fehlermeldungen führen. Sondern die für das Lautsprechersystem nächstmöglich kleinere verfügbare Lautstärke wird eingestellt.   Bei manchen sekundären Lautstärken wie Navi-Out wird die Lautstärke relativ angegeben, z.B: [-11;11]  Bei Verstärkern: Integer, -96..0 [dB] |

<a id="table-arg-0xa039"></a>
### ARG_0XA039

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_AUDIO_SIGNAL | + | - | 0-n | - | unsigned char | - | TAudioSignal | - | - | - | - | - | Gibt an, welche Lautstärke ausgelesen werden soll. Default: 0 |

<a id="table-tinitialisierung"></a>
### TINITIALISIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | IO initialisiert |
| 0xFF | NIO initialisiert |

<a id="table-res-0xa025"></a>
### RES_0XA025

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LANGUAGE | - | - | + | 0-n | - | unsigned char | - | TLanguage | - | - | - | Die derzeit eingestellte MMI Sprache. |

<a id="table-arg-0xa025"></a>
### ARG_0XA025

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_LANGUAGE | + | - | 0-n | - | unsigned char | - | TLanguage | - | - | - | - | - | legt die Sprache fest. |

<a id="table-tlanguage"></a>
### TLANGUAGE

Dimensions: 24 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | codierte Sprache |
| 0x01 | Deutsch |
| 0x02 | Englisch (UK) |
| 0x03 | Englisch (US) |
| 0x04 | Spanisch |
| 0x05 | Italienisch |
| 0x06 | Französisch |
| 0x07 | Flämisch |
| 0x08 | Niederländisch |
| 0x09 | Arabisch |
| 0x0A | Chinesisch Traditionell |
| 0x0B | Chinesisch Simpel |
| 0x0C | Koreanisch |
| 0x0D | Japanisch |
| 0x0E | Russisch |
| 0x0F | Portugisisch |
| 0x10 | Schwedisch |
| 0x11 | Griechisch |
| 0x12 | Türkisch |
| 0x13 | Polnisch |
| 0x14 | Ungarisch |
| 0x15 | Arabisch |
| 0xFE | Kein Sprachpaket aktiv |
| 0xFF | Nicht definiert |

<a id="table-arg-0xa036"></a>
### ARG_0XA036

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_LEVEL | + | - | - | - | char | - | - | - | - | - | - | - | Bei Headunits:  Hex-Wert, von 0x00 lückenlos bis 0x7F Bei manchen sekundären Lautstärken wie Navi-Out wird die Lautstärke relativ angegeben, z.B: [-11;11]  Bei Verstärkern: Integer, -96..0 [dB] |
| ARG_AUDIO_SIGNAL | + | - | 0-n | - | unsigned char | - | TAudioSignal | - | - | - | - | - | Gibt an, welche Lautstärke verstellt oder ausgelesen werden soll. Default: 0 |

<a id="table-taudiosignal"></a>
### TAUDIOSIGNAL

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Entertainment |
| 0x01 | Offset Verkehrsmeldungen |
| 0x02 | Offset Navigation |
| 0x03 | Telefon |
| 0x04 | Spracherkennung |
| 0x05 | PDC |
| 0x06 | Gong |
| 0x07 | AUX-IN |
| 0x10 | nur für RSE: Entertainment Kopfhörer linke Seite |
| 0x20 | nur für RSE: Entertainment Kopfhörer rechte Seite |
| 0xFF | Nicht definiert |

<a id="table-tinsertedmedium"></a>
### TINSERTEDMEDIUM

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Medium eingelegt |
| 0x01 | Medium Erkennung wird durchgeführt |
| 0x02 | CD Medium ist eingelegt |
| 0x03 | DVD Medium ist eingelegt |
| 0x04 | Flashspeicher Medium ist eingelegt |
| 0xFF | Nicht definiert |

<a id="table-res-0xd00c"></a>
### RES_0XD00C

Dimensions: 22 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAUTE_LAUFWERKE | 0-n | - | unsigned int | - | TLaufwerk | - | - | - | Liest aus, welche Laufwerke verbaut sind. |
| STAT_VENDORID_TAPE_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_TAPE_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_TAPE_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_VENDORID_CD_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_CD_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_CD_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_VENDORID_DVD_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_DVD_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_DVD_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_VENDORID_MD_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_MD_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_MD_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_VENDORID_HDD_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_HDD_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_HDD_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_VENDORID_USB_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_USB_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. |
| STAT_FIRMWARE_USB_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. |
| STAT_VENDORID_FLASHSPEICHER_WERT | - | - | string | - | - | - | - | - | Gibt die VENDORID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_PRODUCTID_FLASHSPEICHER_WERT | - | - | string | - | - | - | - | - | Gibt die PRODUCTID des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |
| STAT_FIRMWARE_FLASHSPEICHER_WERT | - | - | string | - | - | - | - | - | Gibt die Firmware-Version des Laufwerks aus. ACHTUNG: Result wird dynamisch zu ..._TEXT statt _WERT. |

<a id="table-tlaufwerk"></a>
### TLAUFWERK

Dimensions: 19 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Kein Laufwerk |
| 0x00000001 | Kassette |
| 0x00000002 | CD |
| 0x00000004 | DVD |
| 0x00000008 | MD |
| 0x00000010 | HDD |
| 0x00000012 | CD und HDD |
| 0x00000014 | DVD und HDD |
| 0x00000020 | USB |
| 0x00000022 | CD und USB |
| 0x00000024 | DVD und USB |
| 0x00000032 | CD, HDD und USB |
| 0x00000034 | DVD, HDD und USB |
| 0x00000040 | Flash Speicher |
| 0x00000042 | CD und Flash Speicher |
| 0x00000044 | DVD und Flash Speicher |
| 0x00000062 | CD, USB und Flash Speicher |
| 0x00000064 | DVD, USB und Flash Speicher |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-arg-0xa01a"></a>
### ARG_0XA01A

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SIGNALART | + | - | 0-n | - | unsigned char | - | TSignalArt | - | - | - | - | - | Art der Signalausgabe. |
| ARG_AUSGANG | + | + | - | - | unsigned int | - | - | - | - | - | - | - | Default: 0 Alle Ausgänge des Steuergerätes müssen einzeln und kombiniert anwählbar sein. |
| ARG_TIMEOUT | + | - | - | - | unsigned char | - | - | - | - | - | - | - | Wertebereich: 0-30,255 0 schaltet wieder auf Normalbetrieb. 255 schaltet das Signal ohne einen TIMEOUT. Ansonsten legt dies Zahl die Sekunden fest, die das Testbild ausgegeben wird. Default: 255 Wird dieser Parameter nicht angegeben, erfolgt eine Ausgabe, bis: -der Job erneut mit Parameter 0 aufgerufen wird -das Steuergerät neu startet (Aufwachen, Reset, &) |

<a id="table-tsignalart"></a>
### TSIGNALART

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Realbild |
| 0x02 | Testbild |
| 0x03 | Signal abschalten |
| 0x04 | Testbild mit Alive Counter (ACNT) |
| 0x05 | Testbild mit stehendem ACNT |
| 0x06 | Testbild mit leicht gestörtem ACNT |
| 0x07 | Testbild mit stark gestörtem ACNT |
| 0x08 | Testbild mit leicht springendem ACNT |
| 0x09 | Testbild mit stark springendem ACNT |

<a id="table-tvideoausgang"></a>
### TVIDEOAUSGANG

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Ausgänge |
| 0x0001 | Ausgang 1 |
| 0x0002 | Ausgang 2 |
| 0x0004 | Ausgang 3 |
| 0x0008 | Ausgang 4 |
| 0x0010 | Ausgang 5 |
| 0x0020 | Ausgang 6 |
| 0x0040 | Ausgang 7 |
| 0x0080 | Ausgang 8 |
| 0x0100 | Ausgang 9 |
| 0xFFFF | Nicht definiert |

<a id="table-res-0xa00b"></a>
### RES_0XA00B

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ENTSOURCE | - | - | + | 0-n | - | unsigned char | - | TEntSource | - | - | - | die eingestellte Entertainmentquelle |
| STAT_DESIRED_ENTSOURCE | - | - | + | 0-n | - | unsigned char | - | TEntSourceStatus | - | - | - | gibt zurück, ob die letzte einzustellende Entertainmentquelle verfügbar war. |

<a id="table-arg-0xa00b"></a>
### ARG_0XA00B

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_ENTSOURCE | + | - | 0-n | - | unsigned char | - | TEntSource | - | - | - | - | - | die auszuwählende Entertainmentquelle |

<a id="table-tentsource"></a>
### TENTSOURCE

Dimensions: 27 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nächste |
| 0x01 | FM |
| 0x02 | AM |
| 0x03 | internes CD Laufwerk |
| 0x04 | CDC |
| 0x05 | internes MD Laufwerk |
| 0x06 | WB (Weatherband) |
| 0x07 | SDARS |
| 0x08 | unbenutzt (vorher IBOC) |
| 0x09 | AUX IN intern oder extern |
| 0x0A | internes DVD Laufwerk |
| 0x0B | TV |
| 0x0C | unbenutzt (vorher VIDEOTXT) |
| 0x0D | Reserviert für AV-AUX IN |
| 0x0E | DAB |
| 0x0F | TRF |
| 0x10 | RSE-DVD |
| 0x11 | RSE-AVIN-LEFT |
| 0x12 | RSE-AVIN-RIGHT |
| 0x13 | USB extern 1 (USB Audio der MULF2 High/ComBox) |
| 0x14 | USB extern 2 (USB Telefon der MULF2 High/ComBox) |
| 0x15 | RSE analog (Audio) |
| 0x16 | MMC |
| 0x17 | Mono analog IN |
| 0x18 | USB intern |
| 0x19 | Entertainment server |
| 0xFF | Entertainmentquelle nicht definiert |

<a id="table-tentsourcestatus"></a>
### TENTSOURCESTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Entertainmentquelle war nicht verfügbar |
| 0x01 | Entertainmentquelle war verfügbar |
| 0x02 | Entertainmentquelle wird gesucht |
| 0xFF | Nicht definiert |

<a id="table-tselbsttestroutine"></a>
### TSELBSTTESTROUTINE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Routinen |
| 0xFFFFFFFF | Nicht definiert |
