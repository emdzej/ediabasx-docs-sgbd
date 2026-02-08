# ema_re.prg

- Jobs: [39](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektromotorischer Aufroller Rechts (fuer F01) |
| ORIGIN | BMW EI-620 Schuster,Erik |
| REVISION | 3.001 |
| AUTHOR | EDAG EI-620 Thieme_Arne |
| COMMENT | Standard-SGBD |
| PACKAGE | 1.09 |
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
- [POWER_DOWN_MODE](#job-power-down-mode) - SG in Power_Down-Mode versetzen UDS  : $11 ECUReset UDS  : $41 PowerDown Modus: Default
- [STATUS_LENKSEITE](#job-status-lenkseite) - IO Bytes des Steuergeraets UDS   : $22   ReadDataByIdentifier UDS   : $30   Codierdaten Block 3014 UDS   : $14   Codierdaten Block 3014 Lenkseite Linkslenker/Rechtslenker

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

<a id="job-power-down-mode"></a>
### POWER_DOWN_MODE

SG in Power_Down-Mode versetzen UDS  : $11 ECUReset UDS  : $41 PowerDown Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| POWER_DOWN_TIME | binary | Power Down Time in Seconds |

<a id="job-status-lenkseite"></a>
### STATUS_LENKSEITE

IO Bytes des Steuergeraets UDS   : $22   ReadDataByIdentifier UDS   : $30   Codierdaten Block 3014 UDS   : $14   Codierdaten Block 3014 Lenkseite Linkslenker/Rechtslenker

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKSEITE | int | Status nur gültig wenn SG codiert ist! Lenkseite Linkslenker/Rechtslenker 0= Linkslenker, 1= Rechtslenker, 2= Uncodiert |
| STAT_LENKSEITE_TEXT | string | Status nur gültig wenn SG codiert ist! Lenkseite Linkslenker/Rechtslenker 0= Linkslenker, 1= Rechtslenker, 2= Uncodiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (64 × 2)
- [LIEFERANTEN](#table-lieferanten) (115 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (9 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (113 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 9)
- [IORTTEXTE](#table-iorttexte) (67 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (10 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (11 × 16)
- [RES_0XD51A](#table-res-0xd51a) (4 × 10)
- [RES_0XD51C](#table-res-0xd51c) (12 × 10)
- [RES_0XA511](#table-res-0xa511) (1 × 13)
- [RES_0XD51B](#table-res-0xd51b) (3 × 10)
- [RES_0XD52B](#table-res-0xd52b) (6 × 10)
- [RES_0XA510](#table-res-0xa510) (2 × 13)
- [ARG_0XA510](#table-arg-0xa510) (1 × 14)
- [TAB_PRECRASH_GURTLOSE](#table-tab-precrash-gurtlose) (5 × 2)
- [TAB_EMA_MOTOR](#table-tab-ema-motor) (13 × 2)
- [RES_0XD521](#table-res-0xd521) (8 × 10)
- [RES_0XD522](#table-res-0xd522) (6 × 10)
- [TAB_EMA_RICHTUNG](#table-tab-ema-richtung) (4 × 2)
- [RES_0XD52A](#table-res-0xd52a) (6 × 10)
- [FAHRZEUG_STATUS_FZM](#table-fahrzeug-status-fzm) (17 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 64 rows × 2 columns

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

Dimensions: 115 rows × 2 columns

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
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

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

Dimensions: 24 rows × 3 columns

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

Dimensions: 9 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
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

Dimensions: 113 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x024E00 | Energiesparmode aktiv | 0 |
| 0x02FF4E | DM_DUMMY_APL | 0 |
| 0x481900 | Interner Fehler | 0 |
| 0x481903 | Software Fehler | 0 |
| 0x48190B | CODING_EVENT_NOT_CODED | 0 |
| 0x48190C | CODING_EVENT_TRANSACTION_FAILED | 0 |
| 0x48190D | CODING_EVENT_SIGNATURE_ERROR | 0 |
| 0x48190E | CODING_EVENT_WRONG_VEHICLE | 0 |
| 0x48190F | CODING_EVENT_INVALID_DATA | 0 |
| 0x481910 | CSM_E_ERROR_EVENT | 0 |
| 0x481914 | Maximale Anzahl Aktivierungen Pre-Crash erreicht | 0 |
| 0x481915 | Maximale Anzahl Aktivierungen Gurtlose-entfernen erreicht | 0 |
| 0x481919 | Retraktor-Motor blockiert | 0 |
| 0x48191A | Retraktor-Kupplung gebrochen | 0 |
| 0x481920 | Retraktor-Motor nicht angeschlossen | 0 |
| 0x481921 | Leitung 6 (Hallsensor Motor) Kurzschluss nach U_Batt | 0 |
| 0x481922 | Leitung 6 (Hallsensor Motor) Kurzschluss nach Masse | 0 |
| 0x481923 | Leitung 6 (Hallsensor Motor) Unterbrechung | 0 |
| 0x481924 | Hallsensor Motor - unplausible Signal-Sequenz | 0 |
| 0x481925 | Leitung 6 (Hallsensor Motor) unplausibler Messwert | 0 |
| 0x481926 | Leitungen 8 oder 9 (Motor) Kurzschluss nach U_Batt | 0 |
| 0x481927 | Leitungen 8 oder 9 (Motor) Kurzschluss nach Masse | 0 |
| 0x48192B | Leitung 3 (Hallsensor Gurt,Versorgung) Unterbrechung | 0 |
| 0x48192C | Leitung 2 (Hallsensor Gurt,Masse) Unterbrechung | 0 |
| 0x48192D | Leitungen 2 oder 3 (Hallsensor Gurt) Kurzschluss nach U_Batt | 0 |
| 0x48192E | Leitungen 2 oder 3 (Hallsensor Gurt) Kurzschluss nach Masse | 0 |
| 0x48192F | Leitung 4 (Hallsensor Gurtband,Geschwindigkeit) Unterbrechung | 0 |
| 0x481930 | Leitung 4 (Hallsensor Gurtband,Geschwindigkeit) Kurzschluss nach U_Batt | 0 |
| 0x481931 | Leitung 4 (Hallsensor Gurtband,Geschwindigkeit) Kurzschluss nach Masse | 0 |
| 0x481932 | Leitung 4 (Hallsensor Gurtband,Geschwindigkeit) unplausible Signal-Sequenz | 0 |
| 0x481933 | Leitung 5 (Hallsensor Gurtband,Richtung) Unterbrechung | 0 |
| 0x481934 | Leitung 5 (Hallsensor Gurtband,Richtung) Kurzschluss nach U_Batt | 0 |
| 0x481935 | Leitung 5 (Hallsensor Gurtband,Richtung) Kurzschluss nach Masse | 0 |
| 0x481936 | Hallsensor Gurtband  - unplausible Signal-Sequenz | 0 |
| 0x481937 | Interne Sensor-Versorgung fehlerhaft | 0 |
| 0xDC840A | FA-CAN : Control Module Bus OFF | 1 |
| 0xDC8BFF | DM_DUMMY_NW | 1 |
| 0xDC9400 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) : Timeout | 1 |
| 0xDC9401 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) Signal Prüfsumme (CRC_PCSH_RCOG) : Fehler | 1 |
| 0xDC9402 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) Signal Alive Zähler (ALIV_PCSH_RCOG) : Ungültig | 1 |
| 0xDC9403 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) Signal Alive Zähler (ALIV_PCSH_RCOG) : Fehler | 1 |
| 0xDC9405 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) Signal Qualifier (QU_FN_PCSH_RCOG) : Ungültig | 1 |
| 0xDC9406 | Botschaft PreCrash Erkennung (PCSH_RCOG, ID 0x104) Signal Zeit bis Kollision (T_COLI_PRD) : Ungültig | 1 |
| 0xDC9410 | Botschaft Gierrate (VYAW_VEH, 0x19F) : Timeout | 1 |
| 0xDC9411 | Botschaft Gierrate (VYAW_VEH, 0x19F) Signal Prüfsumme (CRC_VYAW_VEH) : Fehler | 1 |
| 0xDC9412 | Botschaft Gierrate (VYAW_VEH, 0x19F) Signal Alive Zähler (ALIV_VYAW_VEH) : Ungültig | 1 |
| 0xDC9413 | Botschaft Gierrate (VYAW_VEH, 0x19F) Signal Alive Zähler (ALIV_VYAW_VEH) : Fehler | 1 |
| 0xDC9414 | Botschaft Gierrate (VYAW_VEH, 0x19F) Signal Gierrate (VYAW_VEH) : Ungültig | 1 |
| 0xDC9416 | Botschaft Gierrate (VYAW_VEH, 0x19F) Signal Qualifier (QU_VYAW_VEH) : Ungültig | 1 |
| 0xDC9420 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) : Timeout | 1 |
| 0xDC9421 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) Signal Prüfsumme (CRC_ACLNX_COG) : Fehler | 1 |
| 0xDC9422 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) Signal Alive Zähler (ALIV_ACLNX_COG) : Ungültig | 1 |
| 0xDC9423 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) Signal Alive Zähler (ALIV_ACLNX_COG) : Fehler | 1 |
| 0xDC9424 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) Signal Längsbeschleunigung Schwerpunkt (ACLNX_COG): Ungültig | 1 |
| 0xDC9426 | Botschaft Längsbeschleunigung Schwerpunkt (ACLNX_MASSCNTR, ID 0x199) Signal Qualifier (QU_ACLNX_COG) : Ungültig | 1 |
| 0xDC9430 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) : Timeout | 1 |
| 0xDC9431 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) Signal Prüfsumme (CRC_ACLNY_COG) : Fehler | 1 |
| 0xDC9432 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) Signal Alive Zähler (ALIV_ACLNY_COG) : Ungültig | 1 |
| 0xDC9433 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) Signal Alive Zähler (ALIV_ACLNY_COG) : Fehler | 1 |
| 0xDC9434 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) Signal Querbeschleunigung Schwerpunkt (ACLNY_COG): Ungültig | 1 |
| 0xDC9436 | Botschaft Querbeschleunigung Schwerpunkt (ACLNY_MASSCNTR, ID 0x19A) Signal Qualifier (QU_ACLNY_COG) : Ungültig | 1 |
| 0xDC9440 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) : Timeout | 1 |
| 0xDC9441 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) Signal Prüfsumme (CRC_V_VEH) : Fehler | 1 |
| 0xDC9442 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) Signal Alive Zähler (ALIV_V_VEH) : Ungültig | 1 |
| 0xDC9443 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) Signal Alive Zähler (ALIV_V_VEH) : Fehler | 1 |
| 0xDC9445 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) Signal Fahrzeuggeschwindigkeit (V_VEH_COG) : Ungültig | 1 |
| 0xDC9446 | Botschaft Fahrzeuggeschwindigkeit (V_VEH, ID 0x1A1) Signal Qualifier (QU_V_VEH_COG) : Ungültig | 1 |
| 0xDC9450 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) : Timeout | 1 |
| 0xDC9451 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) Signal Prüfsumme (CRC_STEA_FTAX_EFFV) : Fehler | 1 |
| 0xDC9452 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) Signal Alive Zähler (ALIV_STEA_FTAX_EFFV) : Ungültig | 1 |
| 0xDC9453 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) Signal Alive Zähler (ALIV_STEA_FTAX_EFFV) : Fehler | 1 |
| 0xDC9454 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) Signal Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV) : Ungültig | 1 |
| 0xDC9455 | Botschaft Lenkwinkel Vorderachse effektiv (STEA_FTAX_EFFV, ID 0x302) Signal Qualifier (QU_STEA_FTAX_EFFV) : Ungültig | 1 |
| 0xDC9460 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) : Timeout | 1 |
| 0xDC9461 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Prüfsumme (CRC_AVL_BRTORQ_SUM) : Fehler | 1 |
| 0xDC9462 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Alive Zähler (ALIV_AVL_BRTORQ_SUM) : Ungültig | 1 |
| 0xDC9463 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Alive Zähler (ALIV_AVL_BRTORQ_SUM) : Fehler | 1 |
| 0xDC9465 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Summen-Bremsmoment (AVL_BRTORQ_SUM) : Ungültig | 1 |
| 0xDC9466 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Qualifier Summen-Bremsmoment (QU_AVL_BRTORQ_SUM) : Ungültig | 1 |
| 0xDC9468 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Summen-Bremsmoment Fahrerwunsch (AVL_BRTORQ_SUM_DVCH) : Ungültig | 1 |
| 0xDC9469 | Botschaft Bremsmoment (AVL_BRTORQ_SUM, ID 0xEF) Signal Qualifier Summen-Bremsmoment Fahrerwunsch (QU_AVL_BRTORQ_SUM_DVCH) : Ungültig | 1 |
| 0xDC9470 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) : Timeout | 1 |
| 0xDC9471 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) Signal Prüfsumme (CRC_ANG_ACPD) : Fehler | 1 |
| 0xDC9472 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) Signal Alive Zähler (ALIV_ANG_ACPD) : Ungültig | 1 |
| 0xDC9473 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) Signal Alive Zähler (ALIV_ANG_ACPD) : Fehler | 1 |
| 0xDC9475 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) Signal Winkel Fahrpedal (AVL_ANG_ACPD) : Ungültig | 1 |
| 0xDC9476 | Botschaft Winkel Fahrpedal (ANG_ACPD, ID 0xD9) Signal Qualifier Winkel Fahrpedal (QU_AVL_ANG_ACPD) : Ungültig | 1 |
| 0xDC9480 | Botschaft Klemmen (ID 0x12F) : Timeout | 1 |
| 0xDC9481 | Botschaft Klemmen (ID 0x12F) Signal Prüfsumme (CRC_KL CRC) : Fehler | 1 |
| 0xDC9482 | Botschaft Klemmen (ID 0x12F) Signal Alive Zähler (ALIV_COU_KL) : Ungültig | 1 |
| 0xDC9483 | Botschaft Klemmen (ID 0x12F) Signal Alive Zähler (ALIV_COU_KL) : Fehler | 1 |
| 0xDC9484 | Botschaft Klemmen (ID 0x12F) Signal Fahrzeugzustand (ST_VEH_CON)  : Ungültig | 1 |
| 0xDC9485 | Botschaft Klemmen (ID 0x12F) Signal Status Klemmen (ST_KL) : Ungültig | 1 |
| 0xDC9490 | Botschaft Gurtstatus/Sitzbelegung (ST_BLT_CT_SOCCU, ID 0x297) : Timeout | 1 |
| 0xDC9491 | Botschaft Gurtstatus/Sitzbelegung (ST_BLT_CT_SOCCU, ID 0x297) Signal Gurtstatus Fahrer (SW_BLTB_SW_DR) : Ungültig | 1 |
| 0xDC9492 | Botschaft Gurtstatus/Sitzbelegung (ST_BLT_CT_SOCCU, ID 0x297) Signal Gurtstatus Beifahrer (SW_BLTB_SW_PS) : Ungültig | 1 |
| 0xDC94A0 | Botschaft Türkontakte/Klappen/Zentralverriegelung (STAT_ZV_KLAPPEN, ID 0x2FC) : Timeout | 1 |
| 0xDC94A1 | Botschaft Türkontakte/Klappen/Zentralverriegelung (STAT_ZV_KLAPPEN, ID 0x2FC) Signal Türkontakt Fahrer (ST_DSW_DRD) : Ungültig | 1 |
| 0xDC94A2 | Botschaft Türkontakte/Klappen/Zentralverriegelung (STAT_ZV_KLAPPEN, ID 0x2FC) Signal Türkontakt Beifahrer (ST_DSW_PSD) : Ungültig | 1 |
| 0xDC94B1 | Botschaft CRASH (ID 0x1FE) Signal Überschreitung Beschleunigungsschwelle (ST_EXCE_THRV_ACLN) : Ungültig | 1 |
| 0xDC94B2 | Botschaft CRASH (ID 0x1FE) Signal Anzahl ausgelöste Zündpillen (QUAN_TRG_SQBS) : Ungültig | 1 |
| 0xDC94C0 | Botschaft Fahrzeugzustand (FZZSTD, ID 0x3A0) : Timeout | 1 |
| 0xDC94C2 | Botschaft Fahrzeugzustand (FZZSTD, ID 0x3A0) Signal Status Energieversorgung (ST_ENERG_FZM) : Ungültig | 1 |
| 0xDC94C3 | Botschaft Fahrzeugzustand (FZZSTD, ID 0x3A0) Signal Sperre Fehlerspeicher (ST_ILK_ERRM_FZM) : Ungültig | 1 |
| 0xDC94D0 | Botschaft Relativzeit (ID 0x328) : Timeout | 1 |
| 0xDC94D1 | Botschaft Relativzeit (ID 0x328) Signal Sekundenzähler relativ (T_SEC_COU_REL) : Ungültig | 1 |
| 0xDC94F0 | Botschaft Kilometerstand (ID 0x330) : Timeout | 1 |
| 0xDC94F1 | Botschaft Kilometerstand (ID 0x330) Signal Kilometerstand (MILE_KM) : Ungültig | 1 |
| 0xDC9500 | Botschaft Aussentemperatur (A_TEMP, ID 0x2CA) : Timeout | 1 |
| 0xDC9501 | Botschaft Aussentemperatur (A_TEMP, ID 0x2CA) Signal Aussentemperatur (TEMP_EX) : Ungültig | 1 |
| 0xDC9511 | Botschaft Status Stabilisierung DSC (ST_STAB_DSC, ID 0x173) : Signal Prüfsumme (CRC_ST_STAB_DSC) : Fehler | 1 |
| 0xDC9513 | Botschaft Status Stabilisierung DSC (ST_STAB_DSC, ID 0x173) : Signal Alive Zähler (ALIV_ST_STAB_DSC) : Fehler | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | System_Time_Start | hex | - | signed long | - | - | - | - |
| 0x4008 | System_Time_Begin_Offset | ms | high | unsigned char | - | 10 | - | - |
| 0x1727 | External_Temp | °C | - | unsigned char | - | - | 2 | -40 |
| 0x4002 | ECU_Internal_Temp | °C | - | unsigned char | - | - | 2 | -40 |
| 0x4003 | System_State | TEXT | - | 1 | - | - | - | - |
| 0x4004 | Time_After_POR | s | high | unsigned int | - | - | - | - |
| 0x4005 | PON_Counter | hex | - | signed long | - | - | - | - |
| 0x4006 | Batterie_KL_30b | V | - | unsigned char | - | - | 10 | - |
| 0x4007 | Batterie_KL_30 | V | - | unsigned char | - | - | 10 | - |
| 0x1728 | VSM_Status | 0-n | - | 0xFF | Fahrzeug_Status_FZM | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 67 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x4E0000 | KL30B_UNDERVOLTAGE | 0 |
| 0x4E0001 | KL30B_OVERVOLTAGE | 0 |
| 0x4E0002 | KL30_UNDERVOLTAGE | 0 |
| 0x4E0003 | KL30_OVERVOLTAGE | 0 |
| 0x4E0005 | DM_EVENT_ZEITBOTSCHAFT_TIMEOUT | 0 |
| 0x4E0006 | DM_QUEUE_FULL | 0 |
| 0x4E0007 | DM_QUEUE_DELETED | 0 |
| 0x4E0008 | VSM_EVENT_VEHICLESTATE | 0 |
| 0x4E000A | MCU_ILLEGAL_AD_RESET | 0 |
| 0x4E000B | MCU_CLOCK_FAILURE_RESET | 0 |
| 0x4E000C | MCU_INT_COP_RESET | 0 |
| 0x4E000D | MCU_EXT_COP_RESET | 0 |
| 0x4E000E | MCU_UNIMPLEMENTED_INSTRUCTION_TRAP | 0 |
| 0x4E000F | MCU_ADC_FAILURE | 0 |
| 0x4E0011 | MCU_INVALID_INTERRUPT | 0 |
| 0x4E0012 | MCU_SPURIOUS_INTERRUPT | 0 |
| 0x4E0013 | MCU_OSEK_EXCEPTION | 0 |
| 0x4E001A | ECU_OVERHEAT | 0 |
| 0x4E002C | MOT_HALF_BRIDGE_1_SELF_PROTECTION | 0 |
| 0x4E002D | MOT_HALF_BRIDGE_2_SELF_PROTECTION | 0 |
| 0x4E002E | MOT_HALF_BRIDGE_1_ENABLE_SIGNAL_KO | 0 |
| 0x4E002F | MOT_HALF_BRIDGE_2_ENABLE_SIGNAL_KO | 0 |
| 0x4E0032 | MOT_TENSIONNING_MOS_OPEN_CIRCUIT | 0 |
| 0x4E0033 | MOT_RELEASING_MOS_OPEN_CIRCUIT | 0 |
| 0x4E0034 | MOT_CURRENT_FAULT | 0 |
| 0x4E0035 | MOT_PWM_DUTY_CYCLE_FAULT | 0 |
| 0x4E004A | HSB_MUX_DEFAULT | 0 |
| 0x4E005A | ALG_SPEED_INPUT_ERROR | 0 |
| 0x4E005B | ALG_ACC_LAT_INPUT_ERROR | 0 |
| 0x4E005C | ALG_ACC_LONG_INPUT_ERROR | 0 |
| 0x4E005D | ALG_YAW_RATE_INPUT_ERROR | 0 |
| 0x4E005E | ALG_STEERING_ANGLE_INPUT_ERROR | 0 |
| 0x4E005F | ALG_BRAKE_INPUT_ERROR | 0 |
| 0x4E0060 | ALG_THROTTLE_INPUT_ERROR | 0 |
| 0x4E0061 | ALG_EMERGENCY_BRAKING_ERROR | 0 |
| 0x4E0062 | ALG_EVASIVE_MANOEUVRE_ERROR | 0 |
| 0x4E0063 | ALG_BODY_SLIP_ERROR | 0 |
| 0x4E0064 | ALG_OVER_UNDER_STEERING_ERROR | 0 |
| 0x4E0065 | ALG_UNDER_STEERING_DRIFT_ERROR | 0 |
| 0x4E0066 | ALG_TRBS_ERROR | 0 |
| 0x4E00AA | NVM_E_WRITE_FAILED | 0 |
| 0x4E00AB | NVM_E_READ_FAILED | 0 |
| 0x4E00AC | NVM_E_CONTROL_FAILED | 0 |
| 0x4E00AD | NVM_E_ERASE_FAILED | 0 |
| 0x4E00AE | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x4E00AF | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x4E00B0 | NVM_E_READ_ALL_FAILED | 0 |
| 0x4E00B1 | NVM_CODING_DATA_CORRUPTED | 0 |
| 0x4E00B2 | NVM_PROCESS_DATA_CORRUPTED | 0 |
| 0x4E00B3 | NVM_ECU_TIME_DATA_CORRUPTED | 0 |
| 0x4E00B4 | NVM_STATISTIC_DATA_CORRUPTED | 0 |
| 0x4E00B5 | NVM_CRASH_MEM_TO_WRITE_DATA_CORRUPTED | 0 |
| 0x4E00B6 | NVM_CRASH_MEM_1_DATA_CORRUPTED | 0 |
| 0x4E00B7 | NVM_CRASH_MEM_2_DATA_CORRUPTED | 0 |
| 0x4E00B8 | NVM_PROCESS_STATE_DATA_DATA_CORRUPTED | 0 |
| 0x4E00B9 | NVM_CALIBRATION_DATA_CORRUPTED | 0 |
| 0x4E00BA | NVM_CALIBRATION_DATA_MISSING | 0 |
| 0x4E00BB | NVM_HES_AUTOTEST_DATA_CORRUPTED | 0 |
| 0x4E00BC | NVM_OSEK_DATA_CORRUPTED | 0 |
| 0x4E00BD | NVM_ERROR_QUAL_INFO_CORRUPTED | 0 |
| 0x4E00C8 | PRECRASH_TENSION_FAILED_ST_ENERG_FZM | 0 |
| 0x4E00C9 | PRECRASH_TENSION_FAILED_UNDERVOLTAGE | 0 |
| 0x4E00CC | BELTSLACK_TENSION_FAILED_ST_ENERG_FZM | 0 |
| 0x4E00CD | BELTSLACK_TENSION_FAILED_UNDERVOLTAGE | 0 |
| 0x4E00D4 | PRECRASH_TENSION_FAILED_OVERVOLTAGE | 0 |
| 0x4E00D6 | BELTSLACK_TENSION_FAILED_OVERVOLTAGE | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | System_Time_Start | hex | - | signed long | - | - | - | - |
| 0x4008 | System_Time_Begin_Offset | ms | high | unsigned char | - | 10 | - | - |
| 0x1727 | External_Temp | °C | - | unsigned char | - | - | 2 | -40 |
| 0x4002 | ECU_Internal_Temp | °C | - | unsigned char | - | - | 2 | -40 |
| 0x4003 | System_State | TEXT | - | 1 | - | - | - | - |
| 0x4004 | Time_After_POR | s | high | unsigned int | - | - | - | - |
| 0x4005 | PON_Counter | hex | - | signed long | - | - | - | - |
| 0x4006 | Batterie_KL_30b | V | - | unsigned char | - | - | 10 | - |
| 0x4007 | Batterie_KL_30 | V | - | unsigned char | - | - | 10 | - |
| 0x1728 | VSM_Status | 0-n | - | 0xFF | Fahrzeug_Status_FZM | - | - | - |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 11 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STATUS_TUERKONTAKT | 0xD52B | - | Türkontakt: Status | bit | - | - | BITFIELD | RES_0xD52B | - | - | - | - | 22 | - | - |
| STEUERN_GURTLOSE | 0xA511 | - | Gurtlose entfernen: Steuern, Status | - | PRECRASH_EXTERNAL_ACTIVATION | - | - | - | - | - | - | - | 31 | - | RES_0xA511 |
| STEUERN_PRECRASH | 0xA510 | - | PreCrash-Straffung: Steuern, Status | - | STEUERN_PRECRASH | - | - | - | - | - | - | - | 31 | ARG_0xA510 | RES_0xA510 |
| STATUS_GURTKONTAKT | 0xD52A | - | Gurtkontakt: Status | bit | - | - | BITFIELD | RES_0xD52A | - | - | - | - | 22 | - | - |
| STATUS_CRASH_STATISTIK | 0xD51C | - | Crash-Statistik: Status | - | READ_CRASH_STATISTIC | - | - | - | - | - | - | - | 22 | - | RES_0xD51C |
| STATUS_PRECRASH_STATISTIK | 0xD51A | - | PreCrash-Statistik: Status | - | READ_PRECRASH_STATISTIC | - | - | - | - | - | - | - | 22 | - | RES_0xD51A |
| STATUS_ANALOGWERTE_EMA | 0xD521 | - | Analogwerte: Status | - | ANALOG_VALUE | - | - | - | - | - | - | - | 22 | - | RES_0xD521 |
| STEUERN_RETRAKTOR_AUSGETAUSCHT | 0xA51A | - | Retraktor: Steuern ACHTUNG: Dieser Diagnoseauftrag darf NUR ausgeführt werden, wenn zuvor der Retraktor getauscht wurde! Im Steuergerät wird ein Zähler zurückgesetzt, Diagnose wieder aktiviert und anschließend ein RESET ausgeführt. Erst nach Tausch und Ausführung dieses Jobs, wird der Fehlerspeichereintrag 0x48191A gelöscht. | - | - | - | - | - | - | - | - | - | 31 | - | - |
| STATUS_GURTLOSE_ENTFERNEN_STATISTIK | 0xD51B | - | Gurtlose entfernen-Statistik: Status | - | READ_BELTSLACK_REDUCTION_STATISTIC | - | - | - | - | - | - | - | 22 | - | RES_0xD51B |
| STATUS_GURTSENSOR | 0xD522 | - | Gurtsensor: Status | - | BELT_DISPLACEMENT_SENSOR | - | - | - | - | - | - | - | 22 | - | RES_0xD522 |
| STATUS_MOTORZUSTAND | 0xD528 | STAT_MOTORZUSTAND | Motorzustandsmanager Funktionsstatus | 0-n | - | - | char | TAB_EMA_MOTOR | - | - | - | - | 22 | - | - |

<a id="table-res-0xd51a"></a>
### RES_0XD51A

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_PRECRASH_ALGO_WERT | - | high | unsigned int | - | - | - | - | - | Statistikzähler  PreCrash -Straffung durch Algorithmus |
| STAT_ZAEHLER_PRECRASH_EXTERN_WERT | - | high | unsigned int | - | - | - | - | - | Statistikzähler  PreCrash -Straffung durch externen Busteilnehmer |
| _STAT_ZAEHLER_PRECRASH_DIAGNOSE_WERT | - | high | unsigned int | - | - | - | - | - | Für Entwicklung: Statistikzähler  PreCrash -Straffung durch Diagnoseauslösung |
| _STAT_ZAEHLER_PRECRASH_RETRAKTOR_WERT | - | high | unsigned int | - | - | - | - | - | Für Entwicklung: Statistikzähler  PreCrash -Straffung, Retraktor |

<a id="table-res-0xd51c"></a>
### RES_0XD51C

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EINTRAG_1_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_ALGO_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 1: Systemzeit PreCrash-Straffung durch Algorithmus |
| STAT_EINTRAG_1_OFFSETZEIT_PRECRASH_AKTIVIERUNG_ALGO_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 1: Systemzeit-Offset PreCrash-Straffung durch Algorithmus |
| STAT_EINTRAG_1_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_EXTERN_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 1: Systemzeit PreCrash-Straffung: Aktivierung durch Diagnose |
| STAT_EINTRAG_1_OFFSETZEIT_PRECRASH_AKTIVIERUNG_EXTERN_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 1: Systemzeit-Offset PreCrash-Straffung: Aktivierung durch Diagnose |
| STAT_EINTRAG_1_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_CRASH_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 1: Systemzeit PreCrash-Straffung durch externen Busteilnehmer |
| STAT_EINTRAG_1_OFFSETZEIT_PRECRASH_AKTIVIERUNG_CRASH_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 1: Systemzeit-Offset PreCrash-Straffung durch externen Busteilnehmer |
| STAT_EINTRAG_2_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_ALGO_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 2: Systemzeit PreCrash-Straffung durch Algorithmus |
| STAT_EINTRAG_2_OFFSETZEIT_PRECRASH_AKTIVIERUNG_ALGO_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 2: Systemzeit-Offset PreCrash-Straffung durch Algorithmus |
| STAT_EINTRAG_2_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_EXTERN_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 2: Systemzeit PreCrash-Straffung Aktivierung durch Diagnose |
| STAT_EINTRAG_2_OFFSETZEIT_PRECRASH_AKTIVIERUNG_EXTERN_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 2: Systemzeit-Offset PreCrash-Straffung Aktivierung durch Diagnose |
| STAT_EINTRAG_2_SYSTEMZEIT_PRECRASH_AKTIVIERUNG_CRASH_WERT | s | high | unsigned long | - | - | - | - | - | Eintrag 2: Systemzeit PreCrash-Straffung durch externen Busteilnehmer |
| STAT_EINTRAG_2_OFFSETZEIT_PRECRASH_AKTIVIERUNG_CRASH_WERT | ms | high | char | - | - | 10 | - | - | Eintrag 2: Systemzeit-Offset PreCrash-Straffung durch externen Busteilnehmer |

<a id="table-res-0xa511"></a>
### RES_0XA511

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GURTLOSE | - | - | + | 0-n | high | unsigned char | - | TAB_PRECRASH_GURTLOSE | - | - | - | PreCrash-Straffung: Status  Tabelle: TAB_PRECRASH_GURTLOSE 0 = Beendet, n.i.O. 1 = Beendet, i.O. 2 = durch Benutzer abgebrochen 3 = läuft 4...255 reserviert Ansteuerbedingung: Gurt muss gesteckt sein |

<a id="table-res-0xd51b"></a>
### RES_0XD51B

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_GURTLOSE_ENTFERNEN_WERT | - | high | unsigned int | - | - | - | - | - | Statistikzähler: Gurtlose entfernen durch Algorithmus |
| _STAT_ZAEHLER_GURTLOSE_ENTFERNEN_DIAGNOSE_WERT | - | high | unsigned int | - | - | - | - | - | Für Entwicklung: Statistikzähler: Gurtlose entfernen durch Diagnose |
| _STAT_ZAEHLER_GURTLOSE_ENTFERNEN_RETRAKTOR_WERT | - | high | unsigned int | - | - | - | - | - | Für Entwicklung: Statistikzähler: Gurtlose entfernen, Retraktor |

<a id="table-res-0xd52b"></a>
### RES_0XD52B

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TUERKONTAKT_FA_OFFEN | 0/1 | - | char | 0x01 | - | - | - | - | Türkontakt Fahrerseite: Status 0 = Tür geschlossen, 1 = Tür offen |
| STAT_TUERKONTAKT_FA_PLAUSIBEL | 0/1 | - | char | 0x02 | - | - | - | - | Türkontakt Fahrerseite: Status 0 = plausibel, 1 = unplausibel |
| STAT_TUERKONTAKT_FA_UNGUELTIG | 0/1 | - | char | 0x03 | - | - | - | - | Türkontakt Fahrerseite: Status 0 = gültig, 1 = nicht gültig |
| STAT_TUERKONTAKT_BF_OFFEN | 0/1 | - | char | 0x04 | - | - | - | - | Türkontakt Beifahrerseite: Status 0 = Tür geschlossen, 1 = Tür offen |
| STAT_TUERKONTAKT_BF_PLAUSIBEL | 0/1 | - | char | 0x08 | - | - | - | - | Türkontakt Beifahrerseite: Status 0 = plausibel, 1 = unplausibel |
| STAT_TUERKONTAKT_BF_UNGUELTIG | 0/1 | - | char | 0x0C | - | - | - | - | Türkontakt Beifahrerseite: Status 0 = gültig, 1 = nicht gültig |

<a id="table-res-0xa510"></a>
### RES_0XA510

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PRECRASH | - | - | + | 0-n | high | unsigned char | - | TAB_PRECRASH_GURTLOSE | - | - | - | PreCrash-Straffung: Status  Tabelle: TAB_PRECRASH_GURTLOSE 0 = Beendet, n.i.O. 1 = Beendet, i.O. 2 = durch Benutzer abgebrochen 3 = läuft Ansteuerbedingung: Gurt muss gesteckt sein |
| STAT_AKTIVIERUNGSZEIT_WERT | + | - | - | ms | high | unsigned int | - | - | 10 | - | - | Dauer der Aktivierung in ms |

<a id="table-arg-0xa510"></a>
### ARG_0XA510

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTIVIERUNGSZEIT | + | - | ms | high | unsigned int | - | - | 10 | - | - | - | 1000 | Dauer der Aktivierung Argument: 500 entspricht 5s (typischer Wert) |

<a id="table-tab-precrash-gurtlose"></a>
### TAB_PRECRASH_GURTLOSE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Beendet n.i.O. |
| 0x01 | Beendet i.O. |
| 0x02 | Durch Benutzer abgebrochen |
| 0x03 | Vorgang läuft |
| 0xFFFF | nicht definiert |

<a id="table-tab-ema-motor"></a>
### TAB_EMA_MOTOR

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Überprüfung aktiv |
| 0x01 | Aufstarten aktiv |
| 0x02 | Leerlauf |
| 0x03 | Funktion PreCrash, Straffung aktiv |
| 0x04 | Funktion PreCrash, Entriegelung aktiv |
| 0x05 | Funktion Gurtlose entfernen, aktiv |
| 0x06 | Funktion Gurtlose entfernen, Entriegelung aktiv |
| 0x07 | Fehler (Überlastschutz Gurtlose Entfernen) |
| 0x08 | Fehler (Überlastschutz) |
| 0x09 | Fehler (Status 9) |
| 0x0A | Fehler (Status 10) |
| 0x0B | Fehler (Status 11) |
| 0xFF | undefiniert |

<a id="table-res-0xd521"></a>
### RES_0XD521

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL30_WERT | V | high | unsigned int | - | - | - | 1000 | - | Spannung Klemme 30 (0V .. 16V) |
| STAT_KL30B_WERT | V | high | unsigned int | - | - | - | 1000 | - | Spannung Klemme 30b (0V .. 16V) |
| STAT_MOTORSPANNUNG1_WERT | V | high | unsigned int | - | - | - | 1000 | - | Spannung Motorsteuerleitung 1 (0V .. 16V) |
| STAT_MOTORSPANNUNG2_WERT | V | high | unsigned int | - | - | - | 1000 | - | Spannung Motorsteuerleitung 2 (0V .. 16V) |
| STAT_MOTORSTROM1_WERT | A | high | unsigned int | - | - | - | 100 | - | Stromstärke Motorsteuerleitung 1 (0A .. 60A) |
| STAT_MOTORSTROM2_WERT | A | high | unsigned int | - | - | - | 100 | - | Stromstärke Motorsteuerleitung 2 (0A .. 60A) |
| _STAT_TESTSPANNUNG_WERT | - | high | unsigned int | - | - | - | - | - | Result nur für Entwicklung relevant |
| _STAT_SENSOR_LEVEL_WERT | - | high | unsigned int | - | - | - | - | - | Result nur für Entwicklung relevant |

<a id="table-res-0xd522"></a>
### RES_0XD522

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| _STAT_GURTSENSOR_WERT | - | high | unsigned char | - | - | - | - | - | Result nur für Entwicklung relevant |
| STAT_GURTSENSOR_POSITION_WINKEL_WERT | Grad | high | int | - | - | - | - | - | Gurtsensor:  Position: -6000 ° .. 6000 ° |
| STAT_GURTSENSOR_RICHTUNG | 0-n | high | unsigned char | - | TAB_EMA_RICHTUNG | - | - | - | Gurtsensor : Bewegungsrichtung |
| STAT_GURTSENSOR_GESCHWINDIGKEIT_WERT | °/s | high | unsigned int | - | - | - | - | - | Gurtsensor : Geschwindigkeit: 0 °/s .. 47000 °/s |
| _STAT_MOTOR_SENSOR_WERT | - | high | unsigned char | - | - | - | - | - | Result nur für Entwicklung relevant |
| STAT_MOTOR_SENSOR_POSITION_WERT | Grad | high | long | - | - | - | - | - | Motorsensor : Position: 0 ° .. 4500000 ° |

<a id="table-tab-ema-richtung"></a>
### TAB_EMA_RICHTUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 85 | Straffrichtung |
| 170 | Loeserichtung |
| 0 | Ruhezustand |
| 0xFFFF | Nicht definiert |

<a id="table-res-0xd52a"></a>
### RES_0XD52A

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GURTKONTAKT_FA_GESTECKT | 0/1 | - | char | 0x01 | - | - | - | - | Gurtkontakt Fahrerseite: Status 0 = nicht gesteckt,  1 = gesteckt |
| STAT_GURTKONTAKT_FA_VERBAUT | 0/1 | - | char | 0x02 | - | - | - | - | Gurtkontakt Fahrerseite: Status 0 = verbaut, 1 = nicht verbaut |
| STAT_GURTKONTAKT_FA_UNGUELTIG | 0/1 | - | char | 0x03 | - | - | - | - | Gurtkontakt Fahrerseite: Status 0 = gültig, 1 = nicht gültig |
| STAT_GURTKONTAKT_BF_GESTECKT | 0/1 | - | char | 0x04 | - | - | - | - | Gurtkontakt Beifahrerseite: Status 0 = nicht gesteckt,  1 = gesteckt |
| STAT_GURTKONTAKT_BF_VERBAUT | 0/1 | - | char | 0x08 | - | - | - | - | Gurtkontakt Beifahrerseite: Status 0 = verbaut, 1 = nicht verbaut |
| STAT_GURTKONTAKT_BF_UNGUELTIG | 0/1 | - | char | 0x0C | - | - | - | - | Gurtkontakt Beifahrerseite: Status 0 = gültig, 1 = nicht gültig |

<a id="table-fahrzeug-status-fzm"></a>
### FAHRZEUG_STATUS_FZM

Dimensions: 17 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Initial |
| 0x01 | Standby, Fahrer abwesend |
| 0x02 | Basisbetrieb, Fahrer anwesend |
| 0x03 | Basisbetrieb, Fahrzeug rollt |
| 0x04 | Motornachlauf |
| 0x05 | Zündung ein |
| 0x06 | Zündung ein, Fahrzeug rollt |
| 0x07 | Motor an, Fahrzeug steht |
| 0x08 | Fahrt |
| 0x09 | Bevorstehender Motorstart |
| 0x0A | Bevorstehender Motorstart, Fahrzeug rollt |
| 0x0B | Motorstart |
| 0x0C | Motorstart, Fahrzeug rollt |
| 0x0D | Waschstrassenbetrieb |
| 0x0E | Fehler |
| 0x0F | Signal ungültig |
| 0xFF | Unbekannt |
