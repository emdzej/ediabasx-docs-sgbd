# gws_i01.prg

- Jobs: [42](#jobs)
- Tables: [46](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Gangwahlschalter |
| ORIGIN | BMW EI-60 Uzun |
| REVISION | 1.003 |
| AUTHOR | ZF_Friedrichshafen_AG OTEI1 DiMaio |
| COMMENT | - |
| PACKAGE | 1.34 |
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)]
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [READ_SWE_DEVELOPMENT_INFO](#job-read-swe-development-info) - ReadSWEDevelopmentInfo ansteuern UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0205 ReadSWEDevelopmentInfo Modus: Default
- [GWS_SERIENNUMMER_LESEN](#job-gws-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [GWS_SERIENNUMMER_SCHREIBEN](#job-gws-seriennummer-schreiben) - Seriennummer des Steuergeraets UDS  : $2E   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber
- [REQUEST_SEED_PARAMETER_ACCESS](#job-request-seed-parameter-access) - SGBD-Job für Parameter-Seed fragen UDS  : $27 SecurityAccess UDS  : $61 RequestSeed
- [SEND_KEY_PARAMETER_ACCESS](#job-send-key-parameter-access) - SGBD-Job für Parameter-Key freischalten UDS  : $27 SecurityAccess UDS  : $62 RequestSeed
- [FERTIGUNGSDATUM_LESEN](#job-fertigungsdatum-lesen) - Fertigungsdatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18B ECUManufactoringData Modus: Default
- [FERTIGUNGSDATUM_SCHREIBEN](#job-fertigungsdatum-schreiben) - Beschreiben des Fertigungsdatum Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $F18B
- [PARAMETERBLOCK_LESEN](#job-parameterblock-lesen) - ZF Codierdatenblock lesen UDS  : $22   ReadDataByIdentifier UDS  : $5100 PARAMETERBLOCK_LESEN Modus: Default
- [LED_PARAMETERBLOCK_LESEN](#job-led-parameterblock-lesen) - ZF LED Codierdatenblock lesen UDS  : $22   ReadDataByIdentifier UDS  : $5104 LED_PARAMETERBLOCK_LESEN Modus: Default

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
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
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
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
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

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF  = Status der aktiven Fehlermeldung nicht feststellbar |
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

<a id="job-read-swe-development-info"></a>
### READ_SWE_DEVELOPMENT_INFO

ReadSWEDevelopmentInfo ansteuern UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0205 ReadSWEDevelopmentInfo Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROZESSKLASSE | unsigned char | 0x06: BTLD 0x08: SWFL |
| LID | unsigned long | 0x000019ca: BTLD 0x000019cb: SWFL |
| HAUPTVERSION | unsigned char | HV |
| NEBENVERSION | unsigned char | NV |
| PATCHVERSION | unsigned char | PV |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROZESSKLASSE_WERT | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| PROZESSKLASSE_TEXT | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| PROZESSKLASSE_KURZTEXT | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| VERSION | string | Angabe der Version der Prozessklasse |
| SGBM_ID | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| SWE_DEVELOPMENT_INFO | string | SWE Development Info |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-gws-seriennummer-lesen"></a>
### GWS_SERIENNUMMER_LESEN

Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-gws-seriennummer-schreiben"></a>
### GWS_SERIENNUMMER_SCHREIBEN

Seriennummer des Steuergeraets UDS  : $2E   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0x30-0x39 |
| BYTE2 | int | Bereich: 0x30-0x39 |
| BYTE3 | int | Bereich: 0x30-0x39 |
| BYTE4 | int | Bereich: 0x30-0x39 |
| BYTE5 | int | Bereich: 0x30-0x39 |
| BYTE6 | int | Bereich: 0x30-0x39 |
| BYTE7 | int | Bereich: 0x30-0x39 |
| BYTE8 | int | Bereich: 0x30-0x39 |
| BYTE9 | int | Bereich: 0x30-0x39 |
| BYTE10 | int | Bereich: 0x30-0x39 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-request-seed-parameter-access"></a>
### REQUEST_SEED_PARAMETER_ACCESS

SGBD-Job für Parameter-Seed fragen UDS  : $27 SecurityAccess UDS  : $61 RequestSeed

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Is not being used |
| BYTE2 | int | Is not being used |
| BYTE3 | int | Is not being used |
| BYTE4 | int | Is not being used |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-send-key-parameter-access"></a>
### SEND_KEY_PARAMETER_ACCESS

SGBD-Job für Parameter-Key freischalten UDS  : $27 SecurityAccess UDS  : $62 RequestSeed

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fertigungsdatum-lesen"></a>
### FERTIGUNGSDATUM_LESEN

Fertigungsdatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18B ECUManufactoringData Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_DATUM | string | Fertigungsdatum (DD.MM.YY) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fertigungsdatum-schreiben"></a>
### FERTIGUNGSDATUM_SCHREIBEN

Beschreiben des Fertigungsdatum Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $F18B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| YEAR | int | Bereich: 0-99 |
| MONTH | int | Bereich: 1-12 |
| DAY | int | Bereich: 1-31 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-parameterblock-lesen"></a>
### PARAMETERBLOCK_LESEN

ZF Codierdatenblock lesen UDS  : $22   ReadDataByIdentifier UDS  : $5100 PARAMETERBLOCK_LESEN Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_FSP_LIMIT_U_LOW | string | Unterer Schwellwert zum Ausblenden der Fehlerspeicherung |
| COD_FSP_LIMIT_U_HIGH | string | Oberer Schwellwert zum Ausblenden der Fehlerspeicherung |
| COD_POS_DEB_TIME_1 | string | Entprellzeit fuer die Sensorrohwerterfassung |
| COD_POS_DEB_TIME_2_INV | string | Entprellzeit fuer die Sensorrohwerterfassung invers (2 aus 3) |
| COD_POS_DEB_TIME_3 | string | Entprellzeit fuer die Sensorrohwerterfassung (2 aus 3) |
| COD_POS_DEB_COD_IDENTIFIER | string | Festwert 0x43 |
| COD_PBUTT_DEB_TIME_1 | string | Entprellzeit fuer die Parktastererfassung |
| COD_PBUTT_DEB_TIME_2_INV | string | Entprellzeit fuer die Parktastererfassung invers (2 aus 3) |
| COD_PBUTT_DEB_TIME_3 | string | Entprellzeit fuer die Parktastererfassung (2 aus 3) |
| COD_PBUTT_DEB_COD_IDENTIFIER | string | Festwert 0xEA |
| COD_THRESHOLD_ILL_CUT_OFF | string | Schwellwert ADC zur Beleuchtungsabschaltung (Temperaturthematik) |
| COD_POS_DEB_NA_CNT_1 | string | Zeit in ms für die, die Drehklinke in NA stehen muss, damit es nicht um ein Schnippen handelt |
| COD_POS_DEB_NA_CNT_2_INV | string | Zeit in ms für die, die Drehklinke in NA stehen muss, damit es nicht um ein Schnippen handelt. Invers (2 aus 3) |
| COD_POS_DEB_NA_CNT_3 | string | Zeit in ms für die, die Drehklinke in NA stehen muss, damit es nicht um ein Schnippen handelt |
| COD_POS_DEB_NA_COD_IDENTIFIER | string | Festwert 0xAD |
| COD_DTC_SWITCH_OFF_1 | string | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich |
| COD_DTC_SWITCH_OFF_2 | string | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich |
| COD_DTC_SWITCH_OFF_3 | string | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich |
| COD_DTC_SWITCH_OFF_4 | string | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich |
| COD_RES_32 | string | Codierbyte Reserve 32 |
| COD_CORONA_TIMEOUT | string | Timeout, nach der das blaue Atmen der Corona im Stand ausgeschalten wird |
| COD_CORONA_PERIOD | string | Blinkfrequenz der Korona (Periodendauer in ms) |
| COD_CORONA_BREATH_IN_TIME | string | Abstimmung Corona State "Corona atmet blau (hell)": Zeitpunkt Ende der Phase "ausatmen" |
| COD_CORONA_BREATH_OUT_TIME | string | Abstimmung Corona State "Corona atmet blau (hell)": Zeitpunkt Ende der Phase "ausatmen" |
| COD_CORONA_DARK_BREATH_IN_TIME | string | Abstimmung Corona State "Corona atmet blau (dunkel)": Zeitpunkt Ende der Phase "einatmen" |
| COD_CORONA_DARK_BREATH_OUT_TIME | string | Abstimmung Corona State "Corona atmet blau (dunkel)": Zeitpunkt Ende der Phase "ausatmen" |
| COD_LED_DIAG_ADC_TRIGGER_DELAY | string | LED Diagnose ADC Trigger Delay |
| COD_FNC_LED_OFF_LOWER_LIMIT | string | Untere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| COD_FNC_LED_OFF_UPPER_LIMIT | string | Obere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| COD_FNC_LED_ON_LOWER_LIMIT | string | Untere Diagnoseschwelle Funktionsausleuchtung - LED an |
| COD_FNC_LED_ON_UPPER_LIMIT | string | Obere Diagnoseschwelle Funktionsausleuchtung - LED an |
| COD_BKG_LED_OFF_LOWER_LIMIT | string | Untere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| COD_BKG_LED_OFF_UPPER_LIMIT | string | Obere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| COD_BKG_LED_ON_LOWER_LIMIT | string | Untere Diagnoseschwelle Funktionsausleuchtung - LED an |
| COD_BKG_LED_ON_UPPER_LIMIT | string | Obere Diagnoseschwelle Funktionsausleuchtung - LED an |
| COD_BREATH_MIN_DUTY_CYCLE | string | Start- und Endtastverhaeltnis der Atmung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-led-parameterblock-lesen"></a>
### LED_PARAMETERBLOCK_LESEN

ZF LED Codierdatenblock lesen UDS  : $22   ReadDataByIdentifier UDS  : $5104 LED_PARAMETERBLOCK_LESEN Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_SYM_P_L_MIN | string | Dimmwert Funktionsanzeige LED P Symbol - Lmin gem. BMW GS 95010 [% in Counts] |
| COD_SYM_P_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED P Symbol - ST/N gem. BMW GS 95010 |
| COD_SYM_P_L_MAX | string | Dimmwert Funktionsanzeige LED P Symbol - Lmax gem. BMW GS 95010 |
| COD_SYM_R_L_MIN | string | Dimmwert Funktionsanzeige LED R Symbol - Lmin gem. BMW GS 95010 |
| COD_SYM_R_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED R Symbol - ST/N gem. BMW GS 95010 |
| COD_SYM_R_L_MAX | string | Dimmwert Funktionsanzeige LED R Symbol - Lmax gem. BMW GS 95010 |
| COD_SYM_N_L_MIN | string | Dimmwert Funktionsanzeige LED N Symbol - Lmin gem. BMW GS 95010 |
| COD_SYM_N_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED N Symbol - ST/N gem. BMW GS 95010 |
| COD_SYM_N_L_MAX | string | Dimmwert Funktionsanzeige LED N Symbol - Lmax gem. BMW GS 95010 |
| COD_SYM_D_L_MIN | string | Dimmwert Funktionsanzeige LED D Symbol - Lmin gem. BMW GS 95010 |
| COD_SYM_D_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED D Symbol - ST/N gem. BMW GS 95010 |
| COD_SYM_D_L_MAX | string | Dimmwert Funktionsanzeige LED D Symbol - Lmax gem. BMW GS 95010 |
| COD_SQUARE_P_L_MIN | string | Dimmwert Funktionsanzeige LED P Quadrat - Lmin gem. BMW GS 95010 |
| COD_SQUARE_P_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED P Quadrat - ST/N gem. BMW GS 95010 |
| COD_SQUARE_P_L_MAX | string | Dimmwert Funktionsanzeige LED P Quadrat - Lmax gem. BMW GS 95010 |
| COD_SQUARE_R_L_MIN | string | Dimmwert Funktionsanzeige LED R Quadrat - Lmin gem. BMW GS 95010 |
| COD_SQUARE_R_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED R Quadrat - ST/N gem. BMW GS 95010 |
| COD_SQUARE_R_L_MAX | string | Dimmwert Funktionsanzeige LED R Quadrat - Lmax gem. BMW GS 95010 |
| COD_SQUARE_N_L_MIN | string | Dimmwert Funktionsanzeige LED N Quadrat - Lmin gem. BMW GS 95010 |
| COD_SQUARE_N_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED N Quadrat - ST/N gem. BMW GS 95010 |
| COD_SQUARE_N_L_MAX | string | Dimmwert Funktionsanzeige LED N Quadrat - Lmax gem. BMW GS 95010 |
| COD_SQUARE_D_L_MIN | string | Dimmwert Funktionsanzeige LED D Quadrat - Lmin gem. BMW GS 95010 |
| COD_SQUARE_D_STN_BOUNDARY | string | Dimmwert Funktionsanzeige LED D Quadrat - ST/N gem. BMW GS 95010 |
| COD_SQUARE_D_L_MAX | string | Dimmwert Funktionsanzeige LED D Quadrat - Lmax gem. BMW GS 95010 |
| COD_BKG_P_L_MIN | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmin gem BMW GS 95010 |
| COD_BKG_P_L_MAX | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmax gem BMW GS 95010 |
| COD_BKG_R_L_MIN | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmin gem BMW GS 95010 |
| COD_BKG_R_L_MAX | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmax gem BMW GS 95010 |
| COD_BKG_N_L_MIN | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmin gem BMW GS 95010 |
| COD_BKG_N_L_MAX | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmax gem BMW GS 95010 |
| COD_BKG_D_L_MIN | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmin gem BMW GS 95010 |
| COD_BKG_D_L_MAX | string | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmax gem BMW GS 95010 |
| COD_CORONA_ORANGE_DARK_BREATH_L_MIN | string | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - Lmin gem. BMW GS 95010 |
| COD_CORONA_ORANGE_DARK_BREATH_STN_BOUNDARY | string | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - ST/N gem. BMW GS 95010 |
| COD_CORONA_ORANGE_DARK_BREATH_L_MAX | string | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - Lmax gem. BMW GS 95010 |
| COD_CORONA_ORANGE_BREATH_L_MIN | string | Dimmwert Funktionsanzeige Corona atmet orange (hell) - Lmin gem. BMW GS 95010 |
| COD_CORONA_ORANGE_BREATH_STN_BOUNDARY | string | Dimmwert Funktionsanzeige Corona atmet orange (hell) - ST/N gem. BMW GS 95010 |
| COD_CORONA_ORANGE_BREATH_L_MAX | string | Dimmwert Funktionsanzeige Corona atmet orange (hell) - Lmax gem. BMW GS 95010 |
| COD_CORONA_ORANGE_L_MIN | string | Dimmwert Funktionsanzeige Corona orange (hell) - Lmin gem. BMW GS 95010 |
| COD_CORONA_ORANGE_STN_BOUNDARY | string | Dimmwert Funktionsanzeige Corona orange (hell) - ST/N gem. BMW GS 95010 |
| COD_CORONA_ORANGE_L_MAX | string | Dimmwert Funktionsanzeige Corona orange (hell) - Lmax gem. BMW GS 95010 |
| COD_EBAND_BLUE_L_MIN | string | Dimmwert Funktionsanzeige E-Band blau (hell) - Lmin gem. BMW GS 95010 |
| COD_EBAND_BLUE_STN_BOUNDARY | string | Dimmwert Funktionsanzeige E-Band blau (hell) - ST/N gem. BMW GS 95010 |
| COD_EBAND_BLUE_L_MAX | string | Dimmwert Funktionsanzeige E-Band blau (hell) - Lmax gem. BMW GS 95010 |
| COD_EBAND_ORANGE_L_MIN | string | Dimmwert Suchbeleuchtung E-Band orange - Lmin gem. BMW GS 95010 |
| COD_EBAND_ORANGE_STN_BOUNDARY | string | Dimmwert Suchbeleuchtung E-Band orange - ST/N gem. BMW GS 95010 |
| COD_EBAND_ORANGE_L_MAX | string | Dimmwert Suchbeleuchtung E-Band orange - Lmax gem. BMW GS 95010 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (133 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (45 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [DTCBEREICHE](#table-dtcbereiche) (21 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (30 × 9)
- [IORTTEXTE](#table-iorttexte) (66 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (15 × 16)
- [ARG_0XD202](#table-arg-0xd202) (3 × 12)
- [ARG_0XD203](#table-arg-0xd203) (1 × 12)
- [ARG_0XD204](#table-arg-0xd204) (1 × 12)
- [RES_0XD5AE](#table-res-0xd5ae) (2 × 10)
- [ARG_0X5101](#table-arg-0x5101) (2 × 12)
- [ARG_0X5102](#table-arg-0x5102) (2 × 12)
- [ARG_0X5103](#table-arg-0x5103) (1 × 12)
- [ARG_0X5105](#table-arg-0x5105) (2 × 12)
- [ARG_0X5106](#table-arg-0x5106) (2 × 12)
- [ARG_0X5107](#table-arg-0x5107) (1 × 12)
- [ARG_0X5108](#table-arg-0x5108) (1 × 12)
- [ARG_0X5109](#table-arg-0x5109) (1 × 12)
- [RES_0X5100](#table-res-0x5100) (36 × 10)
- [RES_0X5104](#table-res-0x5104) (81 × 10)
- [TAB_POSITION_DREHSTELLER](#table-tab-position-drehsteller) (6 × 2)
- [TAB_CORONA_FARBE](#table-tab-corona-farbe) (2 × 2)
- [TAB_ENTR_TASTER](#table-tab-entr-taster) (4 × 2)
- [TAB_FUNKTIONSBELEUCHTUNG](#table-tab-funktionsbeleuchtung) (5 × 2)
- [TAB_0X4100](#table-tab-0x4100) (1 × 9)
- [TAB_0X4101](#table-tab-0x4101) (1 × 9)
- [TAB_0X4102](#table-tab-0x4102) (1 × 7)
- [TAB_0X4103](#table-tab-0x4103) (1 × 3)
- [PROZESSKLASSEN_GWS](#table-prozessklassen-gws) (24 × 3)
- [UDS_TAB_HEX2ASCII](#table-uds-tab-hex2ascii) (89 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 76 rows × 2 columns

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
| ?19? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_IDENTIFIER |
| ?1A? | ERROR_ECU_RESPONSE_INCORRECT_RESET_TYPE |
| ?1B? | ERROR_ECU_RESPONSE_INCORRECT_SERIAL_NUMBER_FORMAT |
| ?1C? | ERROR_ECU_RESPONSE_INCORRECT_DTC_BY_STATUS_MASK |
| ?1D? | ERROR_ECU_RESPONSE_INCORRECT_DTC_STATUS_AVAILABILITY_MASK |
| ?1E? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_IDENTIFIER |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_VERIFY |
| ?61? | ERROR_ECU_RESPONSE_ZGW |
| ?62? | ERROR_ECU_RESPONSE_BACKUP |
| ?70? | ERROR_CALID_CVN_INCORRECT_LEN |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 133 rows × 2 columns

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
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive World Headquarters |
| 0x0000B6 | Hans Widmaier |
| 0x0000B7 | SB LiMotive Germany GmbH |
| 0x0000B8 | KYOCERA Display Corporation |
| 0x0000B9 | MAGNA Powertrain AG & Co KG |
| 0x0000BA | BorgWarner |
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

Dimensions: 26 rows × 3 columns

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
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0x04 | GWTB | Gateway-Tabelle |
| 0x0D | SWFK | BEGU: Detaillierung auf SWE-Ebene |
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

Dimensions: 12 rows × 3 columns

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
| 0x5F | ECUGDM | ECUGarageDiagnoseMode |
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

Dimensions: 45 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xE0AC26 | Schnittstelle DME (Daten Antriebsstrang 2, A-CAN): Signal ungültig | 1 |
| 0xE09402 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) nicht aktuell, Empfänger GWS (FA-CAN), Sender EGS (FA-CAN) | 1 |
| 0xE0942B | Botschaft (Stabilisierung DSC, 0x173) nicht aktuell, Empfänger GWS (FA-CAN), Sender (DSC) | 1 |
| 0xE08486 | A-CAN Control Module Bus OFF | 0 |
| 0xE0AC28 | Schnittstelle LIM (Status Ladeleitung Steckt, FA-CAN): Signal ungültig | 1 |
| 0xE09424 | Botschaft (Daten Antriebsstrang 2, 0x3F9) fehlt, Empfänger GWS (FA-CAN), Sender (DME) | 1 |
| 0x8026FB | Interner Steuergerätefehler Software | 0 |
| 0xE09426 | Botschaft (Daten Antriebsstrang 2, 0x3F9) Prüfsummer falsch, Empfänger GWS (FA-CAN), Sender (DME) | 1 |
| 0xE09412 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) nicht aktuell, Empfänger GWS (A-CAN), Sender EGS (A-CAN) | 1 |
| 0xE08BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0x802694 | Hall-Sensoren Zweifachfehler | 0 |
| 0x8026E0 | Parktaster fehlerhaft | 1 |
| 0xE0AC06 | Schnittstelle FRM (Dimmung): Signal ungültig | 1 |
| 0xE0942D | Botschaft (Status Ladeschnittstelle, 0x3B4) fehlt, Empfänger GWS (FA-CAN), Sender (LIM) | 1 |
| 0xE09410 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) fehlt, Empfänger GWS (A-CAN), Sender EGS (A-CAN) | 1 |
| 0xE09425 | Botschaft (Daten Antriebsstrang 2, 0x3F9) nicht aktuell, Empfänger GWS (FA-CAN), Sender (DME) | 1 |
| 0x80268E | Parktaster: Taste klemmt | 0 |
| 0x025E00 | Energiesparmode aktiv | 0 |
| 0xE09429 | Botschaft (Daten Antriebsstrang 2, 0x3F9) Prüfsummer falsch, Empfänger GWS (A-CAN), Sender (DME) | 1 |
| 0x802698 | Überspannung erkannt | 1 |
| 0x8026FA | Interner Steuergerätefehler Hardware | 0 |
| 0xE09400 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) fehlt, Empfänger GWS (FA-CAN), Sender EGS (FA-CAN) | 1 |
| 0xE09404 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) Prüfsumme falsch, Empfänger GWS (FA-CAN), Sender EGS (FA-CAN) | 1 |
| 0xE09428 | Botschaft (Daten Antriebsstrang 2, 0x3F9) nicht aktuell, Empfänger GWS (A-CAN), Sender (DME) | 1 |
| 0xE0942A | Botschaft (Stabilisierung DSC, 0x173) fehlt, Empfänger GWS (FA-CAN), Sender (DSC) | 1 |
| 0xE0AC08 | Schnittstelle KOMBI (LCD Helligkeit Regelung): Signal ungültig | 1 |
| 0xE0AC20 | Schnittstelle EGS (Daten Anzeige Getriebestrang, A-CAN): Signal ungültig | 1 |
| 0x02FF5E | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x802692 | Hall-Sensoren Einfachfehler | 0 |
| 0xE0AC00 | Schnittstelle EGS (Daten Anzeige Getriebestrang, FA-CAN): Signal ungültig | 1 |
| 0x8026F8 | Coronabeleuchtung fehlerhaft | 0 |
| 0xE09414 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) Prüfsumme falsch, Empfänger GWS (A-CAN), Sender EGS (A-CAN) | 1 |
| 0x802696 | Unterspannung erkannt | 1 |
| 0xE0AC27 | Schnittstelle DSC (Stabilisierung DSC, FA-CAN): Signal ungültig | 1 |
| 0xE0AC04 | Schnittstelle CAS (Klemmen): Signal ungültig | 1 |
| 0xE09408 | Botschaft (Klemmen, 0x12F) fehlt, Empfänger GWS (FA-CAN), Sender CAS (FA-CAN) | 1 |
| 0xE0942C | Botschaft (Stabilisierung DSC, 0x173) Prüfsummer falsch, Empfänger GWS (FA-CAN), Sender (DSC) | 1 |
| 0xE0840A | FA-CAN Control Module Bus OFF | 0 |
| 0x802680 | Funktionsanzeige fehlerhaft | 0 |
| 0xE0AC25 | Schnittstelle DME (Daten Antriebsstrang 2, FA-CAN): Signal ungültig | 1 |
| 0x80268C | Suchbeleuchtung fehlerhaft | 0 |
| 0xE0940A | Botschaft (Dimmung, 0x202) fehlt, Empfänger GWS (FA-CAN), Sender FRM (FA-CAN) | 1 |
| 0xE09427 | Botschaft (Daten Antriebsstrang 2, 0x3F9) fehlt, Empfänger GWS (A-CAN), Sender (DME) | 1 |
| 0xE0940C | Botschaft (LCD Helligkeit Regelung, 0x393) fehlt, Empfänger GWS (FA-CAN), Sender KOMBI (FA-CAN) | 1 |
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
| F_HLZ_VIEW | nein |

<a id="table-dtcbereiche"></a>
### DTCBEREICHE

Dimensions: 21 rows × 4 columns

| DTC-TYP | MINIMALWERT | MAXIMALWERT | BESCHREIBUNG |
| --- | --- | --- | --- |
| AllgemeinerDTC | 020000 | 02FFFF | Die zulässigen Bereiche sind für jedes Steuergerät festgelegt. Es können mehrere gültige Bereiche (Kacheln) definiert werden. |
| SystembusDTC | E0841F | E0843E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08469 | E08472 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930030 | 930055 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E0843F | E08449 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08501 | E0850A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08415 | E0841E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08600 | E086FF | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930000 | 930011 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08487 | E0848F | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E0850B | E08514 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E0840B | E08414 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08401 | E0840A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E08473 | E0847C | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E0845F | E08468 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | E0847D | E08486 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SubbusDTC | E08C00 | E093FF | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SignalDTC | E09400 | E0C3FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | E08BFF | E08BFF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | E09400 | E0C3FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| KomponentenDTC | 802680 | 8026FF | Die zulässigen Bereiche sind für jedes Steuergerät festgelegt. Es können mehrere gültige Bereiche (Kacheln) definiert werden. |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 30 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x170C | Batteriespannung | mV | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | TEMP | °C | High | unsigned char | - | 1.0 | 1.0 | -70.0 |
| 0x4100 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x0001 | FEHLERORT_HALLSENSOR_VV_1 | 0/1 | High | 0x01 | - | - | - | - |
| 0x0002 | FEHLERORT_HALLSENSOR_VV_2 | 0/1 | High | 0x02 | - | - | - | - |
| 0x0003 | FEHLERORT_HALLSENSOR_VO_1 | 0/1 | High | 0x04 | - | - | - | - |
| 0x0004 | FEHLERORT_HALLSENSOR_VO_2 | 0/1 | High | 0x08 | - | - | - | - |
| 0x0005 | FEHLERORT_HALLSENSOR_NA_1 | 0/1 | High | 0x10 | - | - | - | - |
| 0x0006 | FEHLERORT_HALLSENSOR_NA_2 | 0/1 | High | 0x20 | - | - | - | - |
| 0x0007 | FEHLERORT_HALLSENSOR_HI_1 | 0/1 | High | 0x40 | - | - | - | - |
| 0x0008 | FEHLERORT_HALLSENSOR_HI_2 | 0/1 | High | 0x80 | - | - | - | - |
| 0x4101 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x0009 | FEHLERORT_FKT_LED_P_KS_MASSE | 0/1 | High | 0x01 | - | - | - | - |
| 0x000A | FEHLERORT_FKT_LED_P_KS_UBATT_OPEN | 0/1 | High | 0x02 | - | - | - | - |
| 0x000B | FEHLERORT_FKT_LED_R_SYMBOL_KS_MASSE | 0/1 | High | 0x04 | - | - | - | - |
| 0x000C | FEHLERORT_FKT_LED_R_SYMBOL_KS_UBATT_OPEN | 0/1 | High | 0x08 | - | - | - | - |
| 0x000D | FEHLERORT_FKT_LED_R_QUADRAT_KS_MASSE | 0/1 | High | 0x10 | - | - | - | - |
| 0x000E | FEHLERORT_FKT_LED_R_QUADRAT_KS_UBATT_OPEN | 0/1 | High | 0x20 | - | - | - | - |
| 0x000F | FEHLERORT_FKT_LED_N_SYMBOL_KS_MASSE | 0/1 | High | 0x40 | - | - | - | - |
| 0x0010 | FEHLERORT_FKT_LED_N_SYMBOL_KS_UBATT_OPEN | 0/1 | High | 0x80 | - | - | - | - |
| 0x4102 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x0011 | FEHLERORT_FKT_LED_N_QUADRAT_KS_MASSE | 0/1 | High | 0x01 | - | - | - | - |
| 0x0012 | FEHLERORT_FKT_LED_N_QUADRAT_KS_UBATT_OPEN | 0/1 | High | 0x02 | - | - | - | - |
| 0x0013 | FEHLERORT_FKT_LED_D_SYMBOL_KS_MASSE | 0/1 | High | 0x04 | - | - | - | - |
| 0x0014 | FEHLERORT_FKT_LED_D_SYMBOL_KS_UBATT_OPEN | 0/1 | High | 0x08 | - | - | - | - |
| 0x0015 | FEHLERORT_FKT_LED_D_QUADRAT_KS_MASSE | 0/1 | High | 0x10 | - | - | - | - |
| 0x0016 | FEHLERORT_FKT_LED_D_QUADRAT_KS_UBATT_OPEN | 0/1 | High | 0x20 | - | - | - | - |
| 0x4103 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x0017 | FEHLERORT_HALLSENSOR_HH_1 | 0/1 | High | 0x01 | - | - | - | - |
| 0x0018 | FEHLERORT_HALLSENSOR_HH_2 | 0/1 | High | 0x02 | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 66 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x8026DB | CANNM_E_CANIF_TRANSMIT_ERROR_1 | 0 |
| 0x8026D5 | SPI_E_TIMEOUT | 1 |
| 0x8026E3 | ECC ROM Check fehlerhaft | 1 |
| 0x8026C4 | COMM_E_START_Tx_TIMEOUT_C0 | 0 |
| 0x8026D3 | WDGM_E_SET_MODE | 0 |
| 0x8026C1 | CNM_E_NETWORK_TIMEOUT | 0 |
| 0x8026E6 | Fehlererkennung Programablaufkontrolle | 1 |
| 0x8026AD | MCU_E_HCLOCK_1_FAILURE | 1 |
| 0x8026B1 | MCU_E_TIMEOUT_OSC_STABILITY | 1 |
| 0x8026D2 | WDGM_E_ALIVE_SUPERVISION | 0 |
| 0x8026C5 | ECUM_E_ALL_RUN_REQUESTS_KILLED | 0 |
| 0x8026AA | MCU_E_LOCK_0_FAILURE | 1 |
| 0x8026CB | MCU_E_CLOCK_FAILURE | 0 |
| 0x8026A1 | CANNM_E_NETWORK_TIMEOUT_0 | 1 |
| 0x8026F9 | Abschaltung wegen Übertemperatur | 1 |
| 0x8026CD | NVM_E_INTEGRITY_FAILED | 0 |
| 0x8026B2 | WDG_E_MISS_TRIGGER | 1 |
| 0x8026BF | CANNM_E_INIT_FAILED | 0 |
| 0x8026E5 | Fehlererkennung Core Self Test | 1 |
| 0x5E1003 | Puffer für ausgehende Fehlermeldungen ist voll | 1 |
| 0x8026D0 | WDG_E_DISABLE_REJECTED | 0 |
| 0x8026D4 | PWM_E_UNEXPECTED_IRQ | 1 |
| 0x8026CA | FLS_E_WRITE_FAILED | 0 |
| 0x8026B5 | COMM_E_STOP_Tx_TIMEOUT_C1 | 0 |
| 0x8026AF | MCU_E_LOCK_1_FAILURE | 1 |
| 0x8026E1 | Zyklischer ROM Check fehlerhaft | 1 |
| 0x8026E8 | Fehlererkennung WD Reset | 1 |
| 0x8026DC | CANNM_E_NETWORK_TIMEOUT_1 | 1 |
| 0x8026B0 | MCU_E_TIMEOUT_TRANSITION | 1 |
| 0x8026BC | CANIF_E_FULL_TX_BUFFER | 0 |
| 0x8026C2 | CNM_E_TX_PATH_FAILED | 0 |
| 0x8026C6 | FEE_E_WRITE_FAILED | 1 |
| 0x5E1002 | Botschaft (Fahrzeugzustand, 0x3A0) fehlt | 1 |
| 0x8026BA | ADC_E_TIMEOUT | 1 |
| 0x8026CE | NVM_E_REQ_FAILED | 0 |
| 0x8026AC | MCU_E_LCLOCK_1_FAILURE | 1 |
| 0x8026A8 | MCU_E_LCLOCK_0_FAILURE | 1 |
| 0x8026C3 | COMM_E_NET_START_IND_CHANNEL_0 | 0 |
| 0x8026AB | MCU_E_RCCLOCK_0_FAILURE | 1 |
| 0x8026E2 | Zyklischer RAM Check fehlerhaft | 1 |
| 0x8026A2 | COMM_E_STOP_Tx_TIMEOUT_C0 | 0 |
| 0x8026D1 | WDG_E_MODE_SWITCH_FAILED | 0 |
| 0x8026C7 | FLS_E_COMPARE_FAILED | 0 |
| 0x8026B4 | FLS_E_UNEXPECTED_FLASH_ID | 1 |
| 0x8026BB | CAN_E_TIMEOUT | 0 |
| 0x8026CC | MCU_E_LOCK_FAILURE | 0 |
| 0x8026E7 | Fehlererkennung Stack Check | 1 |
| 0x8026B3 | MCU_E_RC_MEASURE | 1 |
| 0x8026A9 | MCU_E_HCLOCK_0_FAILURE | 1 |
| 0x8026C8 | FLS_E_ERASE_FAILED | 0 |
| 0x8026B9 | CANIF_E_INVALID_RXPDUID | 0 |
| 0x8026BD | CANIF_E_STOPPED | 0 |
| 0x8026C9 | FLS_E_READ_FAILED | 0 |
| 0x8026CF | PIA_E_IO_ERROR | 1 |
| 0x8026E4 | ECC RAM Check fehlerhaft | 1 |
| 0x8026A6 | IPDUM_E_TRANSMIT_FAILED | 0 |
| 0x8026B7 | COMM_E_NET_START_IND_CHANNEL_1 | 0 |
| 0x8026A0 | CANNM_E_TX_PATH_FAILED | 1 |
| 0x8026B6 | COMM_E_START_Tx_TIMEOUT_C1 | 0 |
| 0x5E1004 | Fehler konnte nach maximaler Anzahl von Versuchen nicht gesendet werden | 1 |
| 0x8026A7 | MCU_E_QUARTZ_FAILURE | 1 |
| 0x8026BE | CANNM_E_CANIF_TRANSMIT_ERROR | 0 |
| 0x8026B8 | CANIF_E_INVALID_TXPDUID | 0 |
| 0x8026AE | MCU_E_RCCLOCK_1_FAILURE | 1 |
| 0x8026C0 | CANTP_E_COMM | 0 |
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

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x170C | Batteriespannung | mV | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | TEMP | °C | High | unsigned char | - | 1.0 | 1.0 | -70.0 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 15 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION_DREHSTELLER | 0xD200 | STAT_POSITION_DREHSTELLER | Position Drehsteller:siehe Tabelle TAB_POSITION_DREHSTELLER | 0-n | - | high | unsigned char | TAB_POSITION_DREHSTELLER | - | - | - | - | 22 | - | - |
| CORONA_BELEUCHTUNG | 0xD202 | - | Coronabeleuchtung | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD202 | - |
| FUNKTIONSBELEUCHTUNG_DREHSTELLER | 0xD203 | - | Funktionsbeleuchtung vom Drehsteller | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD203 | - |
| SUCHBELEUCHTUNG_DREHSTELLER | 0xD204 | - | Suchbeleuchtung Drehsteller | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD204 | - |
| STATUS_GWS_PARKTASTER_1_UND_2 | 0xD5AE | - | Status Parktaster Kontake 1 und 2; 0= nicht gedrückt 1= gedrückt 2= klemmt | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5AE |
| PARAMETERBLOCK_LESEN | 0x5100 | - | Read ZF-Codierdatenblocks | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x5100 |
| PARAMETERBLOCK_SCHREIBEN_1_BYTE | 0x5101 | - | Write 1 Byte in ZF-Codierdatenblock | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5101 | - |
| PARAMETERBLOCK_SCHREIBEN_2_BYTES | 0x5102 | - | Write 2 Bytes in ZF-Codierdatenblock | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5102 | - |
| WRITE_BLOCK_IN_NVM | 0x5103 | - | Write the 64 bytes block in the non volatile memory. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5103 | - |
| LED_PARAMETERBLOCK_LESEN | 0x5104 | - | LED Parameterblock lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x5104 |
| LED_PARAMETERBLOCK_SCHREIBEN_1_BYTE | 0x5105 | - | LED Parameterblock schreiben 1 Byte | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5105 | - |
| LED_PARAMETERBLOCK_SCHREIBEN_2_BYTES | 0x5106 | - | Write 2 bytes in array | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5106 | - |
| WRITE_LED_BLOCK_IN_NVM | 0x5107 | - | Write LED block in NvM | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5107 | - |
| SET_PARAMETERBLOCK_TO_INIT_VALUES | 0x5108 | - | Set Param Block 1 to the initial ROM default values | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5108 | - |
| SET_LED_PARAMETERBLOCK_TO_INIT_VALUES | 0x5109 | - | Set Param Block 2 (LED params) to the ROM default values. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5109 | - |

<a id="table-arg-0xd202"></a>
### ARG_0XD202

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FARBE | 0-n | high | unsigned char | - | TAB_CORONA_FARBE | - | - | - | - | - | Farbe der Coronabeleuchtung |
| PULSIEREND | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Pulsierend: 0x00 = nicht pulsierend 0x01 = pulsierend |
| ZEIT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Dauer der Ansteuerung |

<a id="table-arg-0xd203"></a>
### ARG_0XD203

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STUFE | 0-n | high | unsigned char | - | TAB_FUNKTIONSBELEUCHTUNG | - | - | - | - | - | Angesteuerte Stufe der Funktionsbeleuchtung |

<a id="table-arg-0xd204"></a>
### ARG_0XD204

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | high | unsigned char | - | TAB_FUNKTIONSBELEUCHTUNG | - | - | - | - | - | Anzusteuerndes Element der Suchbeleuchtung Siehe Tabelle TAB_FUNKTIONSBELEUCHTUNG |

<a id="table-res-0xd5ae"></a>
### RES_0XD5AE

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PARKTASTER_1_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | - | - | - | Status Parktaster Kontakt 1; siehe TAB_ENTR_TASTER   |
| STAT_PARKTASTER_2_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | - | - | - | Status Parktaster Kontakt 2; siehe TAB_ENTR_TASTER   |

<a id="table-arg-0x5101"></a>
### ARG_0X5101

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX_IN_ARRAY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 63.0 | Schreibt 1 Byte auf dem Tabellenindex INDEX_IN_ARRAY |
| VALUE | HEX | high | unsigned char | - | - | - | - | - | - | - | Wert der geschrieben werden soll - 1 Byte |

<a id="table-arg-0x5102"></a>
### ARG_0X5102

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX_IN_ARRAY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 63.0 | Schreibt 2 Bytes auf dem Tabellenindex INDEX_IN_ARRAY |
| VALUE | HEX | high | unsigned int | - | - | - | - | - | - | - |  Wert der geschrieben werden soll - 2 Bytes |

<a id="table-arg-0x5103"></a>
### ARG_0X5103

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| UPDATE_BLOCK | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Update des 64 Bytes großen Speicherbereiches: 0: Kein Update ins NvM durchführen 1:  Update ins NvM durchführen |

<a id="table-arg-0x5105"></a>
### ARG_0X5105

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX_IN_ARRAY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 127.0 | Scheibt 1 Byte auf dem Tabellenindex INDEX_IN_ARRAY |
| VALUE | HEX | high | unsigned char | - | - | - | - | - | - | - | Wert - 1 Byte |

<a id="table-arg-0x5106"></a>
### ARG_0X5106

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX_IN_ARRAY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 127.0 | Schreibt 2 Bytes auf den Tabellenindex INDEX_IN_ARRAY |
| VALUE | HEX | high | unsigned int | - | - | - | - | - | - | - | Wert - 2 Bytes |

<a id="table-arg-0x5107"></a>
### ARG_0X5107

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| UPDATE_LED_BLOCK | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Update des LED-Parameterblocks: 0: kein Update des LED-Blocks im NvM 1: Update des LED-Blocks im NvM |

<a id="table-arg-0x5108"></a>
### ARG_0X5108

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SET_TO_ROM_VALUES | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Parameterblock wird auf die initial ROM-Werte zurückgesetzt, wenn der Übergabeparameter 1 ist. |

<a id="table-arg-0x5109"></a>
### ARG_0X5109

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SET_TO_ROM_VALUES | 0/1 | high | unsigned char | - | - | - | - | - | - | - | LED Parameterblock wird auf die initial ROM Werte zurückgesetzt, wenn der Übergabeparameter 1 ist. |

<a id="table-res-0x5100"></a>
### RES_0X5100

Dimensions: 36 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_COD_FSP_LIMIT_U_LOW_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Unterer Schwellwert zum Ausblenden der Fehlerspeicherung |
| STAT_COD_FSP_LIMIT_U_HIGH_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Oberer Schwellwert zum Ausblenden der Fehlerspeicherung |
| STAT_COD_POS_DEB_TIME_1_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Sensorrohwerterfassung |
| STAT_COD_POS_DEB_TIME_2_INV_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Sensorrohwerterfassung invers (2 aus 3) |
| STAT_COD_POS_DEB_TIME_3_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Sensorrohwerterfassung (2 aus 3) |
| STAT_COD_POS_DEB_COD_IDENTIFIER_WERT | HEX | high | unsigned char | - | - | - | - | - | Festwert 0x43 |
| STAT_COD_PBUTT_DEB_TIME_1_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Parktastererfassung |
| STAT_COD_PBUTT_DEB_TIME_2_INV_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Parktastererfassung invers (2 aus 3) |
| STAT_COD_PBUTT_DEB_TIME_3_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Entprellzeit für die Parktastererfassung (2 aus 3) |
| STAT_COD_PBUTT_DEB_COD_IDENTIFIER_WERT | HEX | high | unsigned char | - | - | - | - | - | Festwert 0xEA |
| STAT_COD_THRESHOLD_ILL_CUT_OFF_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Schwellwert ADC zur Beleuchtungsabschaltung (Temperaturthematik) |
| STAT_COD_POS_DEB_NA_CNT_1_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in ms für die, die Drehklinke in NA stehen muß, damit es sich nicht um ein Schnippen handelt. |
| STAT_COD_POS_DEB_NA_CNT_2_INV_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in ms für die, die Drehklinke in NA stehen muß, damit es nicht um ein Schnippen handelt. invers (2 aus 3) |
| STAT_COD_POS_DEB_NA_CNT_3_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in ms für die, die Drehklinke in NA stehen muß, damit es nicht um ein Schnippen handelt (2 aus 3) |
| STAT_COD_POS_DEB_NA_COD_IDENTIFIER_WERT | HEX | high | unsigned char | - | - | - | - | - | Festwert 0xAD |
| STAT_COD_DTC_SWITCH_OFF_1_WERT | HEX | high | unsigned long | - | - | - | - | - | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich. |
| STAT_COD_DTC_SWITCH_OFF_2_WERT | HEX | high | unsigned long | - | - | - | - | - | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich |
| STAT_COD_DTC_SWITCH_OFF_3_WERT | HEX | high | unsigned long | - | - | - | - | - | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich. |
| STAT_COD_DTC_SWITCH_OFF_4_WERT | HEX | high | unsigned long | - | - | - | - | - | DTC-Code der ausgeblendet wird für die Fehlerspeicherung. (Erkennung, Feherqualifizierung und Fehlerbehandlung bleiben erhalten). Primärer Speicher oder Infospeicher möglich. |
| STAT_COD_RES_32_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Codierbyte Reserve 32 = frei |
| STAT_COD_CORONA_TIMEOUT_WERT | ms | high | unsigned char | - | - | 100.0 | 1.0 | 0.0 | Timeout, nach der das blaue Atmen der Corona im Stand ausgeschalten wird |
| STAT_COD_CORONA_PERIOD_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Blinkfrequenz der Korona (Periodendauer in ms) |
| STAT_COD_CORONA_BREATH_IN_TIME_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abstimmung Corona State  Corona atmet blau hell : Zeitpunkt Ende der Phase  einatmen  |
| STAT_COD_CORONA_BREATH_OUT_TIME_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abstimmung Corona State  Corona atmet blau hell : Zeitpunkt Start der Phase  ausatmen  |
| STAT_COD_CORONA_DARK_BREATH_IN_TIME_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abstimmung Corona State  Corona atmet blau dunkel : Zeitpunkt Ende der Phase  einatmen  |
| STAT_COD_CORONA_DARK_BREATH_OUT_TIME_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abstimmung Corona State  Corona atmet blau dunkel : Zeitpunkt Start der Phase  ausatmen  |
| STAT_COD_LEDDIAG_ADC_TRIGGER_DELAY_WERT | HEX | high | unsigned int | - | - | - | - | - | LED Diagnose ADC Trigger Delay |
| STAT_COD_FNC_LED_OFF_LOWER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Untere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| STAT_COD_FNC_LED_OFF_UPPER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Obere Diagnoseschwelle Funktionsausleuchtung - LED aus |
| STAT_COD_FNC_LED_ON_LOWER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Untere Diagnoseschwelle Funktionsausleuchtung - LED an |
| STAT_COD_FNC_LED_ON_UPPER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Obere Diagnoseschwelle Funktionsausleuchtung - LED an |
| STAT_COD_BKG_LED_OFF_LOWER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Untere Diagnoseschwelle Suchbeleuchtung - LED aus |
| STAT_COD_BKG_LED_OFF_UPPER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Obere Diagnoseschwelle Suchbeleuchtung - LED aus |
| STAT_COD_BKG_LED_ON_LOWER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Untere Diagnoseschwelle Suchbeleuchtung - LED an |
| STAT_COD_BKG_LED_ON_UPPER_LIMIT_WERT | HEX | high | unsigned int | - | - | - | - | - | Obere Diagnoseschwelle Suchbeleuchtung - LED an |
| STAT_COD_BREATH_MIN_DUTY_CYCLE_WERT | HEX | high | unsigned int | - | - | - | - | - | Start und Endtastverhältnis der Corona Atmung |

<a id="table-res-0x5104"></a>
### RES_0X5104

Dimensions: 81 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_COD_SYM_P_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Symbol - Lmin gem. BMW GS 95010 [% in Counts] |
| STAT_COD_SYM_P_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Symbol - ST/N gem. BMW GS 95010 |
| STAT_COD_SYM_P_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Symbol - Lmax gem. BMW GS 95010 |
| STAT_COD_SYM_R_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Symbol - Lmin gem. BMW GS 95010 |
| STAT_COD_SYM_R_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Symbol - ST/N gem. BMW GS 95010 |
| STAT_COD_SYM_R_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Symbol - Lmax gem. BMW GS 95010 |
| STAT_COD_SYM_N_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Symbol - Lmin gem. BMW GS 95010 |
| STAT_COD_SYM_N_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Symbol - ST/N gem. BMW GS 95010 |
| STAT_COD_SYM_N_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Symbol - Lmax gem. BMW GS 95010 |
| STAT_COD_SYM_D_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Symbol - Lmin gem. BMW GS 95010 |
| STAT_COD_SYM_D_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Symbol - ST/N gem. BMW GS 95010 |
| STAT_COD_SYM_D_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Symbol - Lmax gem. BMW GS 95010 |
| STAT_COD_SQUARE_P_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Quadrat - Lmin gem. BMW GS 95010 |
| STAT_COD_SQUARE_P_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Quadrat - ST/N gem. BMW GS 95010 |
| STAT_COD_SQUARE_P_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED P Quadrat - Lmax gem. BMW GS 95010 |
| STAT_COD_SQUARE_R_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Quadrat - Lmin gem. BMW GS 95010 |
| STAT_COD_SQUARE_R_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Quadrat - ST/N gem. BMW GS 95010 |
| STAT_COD_SQUARE_R_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED R Quadrat - Lmax gem. BMW GS 95010 |
| STAT_COD_SQUARE_N_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Quadrat - Lmin gem. BMW GS 95010 |
| STAT_COD_SQUARE_N_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Quadrat - ST/N gem. BMW GS 95010 |
| STAT_COD_SQUARE_N_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED N Quadrat - Lmax gem. BMW GS 95010 |
| STAT_COD_SQUARE_D_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Quadrat - Lmin gem. BMW GS 95010 |
| STAT_COD_SQUARE_D_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Quadrat - ST/N gem. BMW GS 95010 |
| STAT_COD_SQUARE_D_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige  LED D Quadrat - Lmax gem. BMW GS 95010 |
| STAT_COD_BKG_P_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmin gem BMW GS 95010 |
| STAT_COD_BKG_P_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED P Hintergrund - Lmax gem BMW GS 95010 |
| STAT_COD_BKG_R_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED R Hintergrund - Lmin gem BMW GS 95010 |
| STAT_COD_BKG_R_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED R Hintergrund - Lmax gem BMW GS 95010 |
| STAT_COD_BKG_N_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED N Hintergrund - Lmin gem BMW GS 95010 |
| STAT_COD_BKG_N_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED N Hintergrund - Lmax gem BMW GS 95010 |
| STAT_COD_BKG_D_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED D Hintergrund - Lmin gem BMW GS 95010 |
| STAT_COD_BKG_D_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Suchbeleuchtung LED D Hintergrund - Lmax gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_DARK_BREATH_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - Lmin gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_DARK_BREATH_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - ST/N gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_DARK_BREATH_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (dunkel) - Lmax gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_BREATH_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (hell) - Lmin gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_BREATH_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (hell) - ST/N gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_BREATH_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona atmet orange (hell) - Lmax gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona orange (hell) - Lmin gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona orange (hell) - ST/N gem BMW GS 95010 |
| STAT_COD_CORONA_ORANGE_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige Corona orange (hell) - Lmax gem BMW GS 95010 |
| STAT_COD_EBAND_BLUE_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band (hell) - Lmin gem BMW GS 95010 |
| STAT_COD_EBAND_BLUE_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band (hell) - ST/N gem BMW GS 95010 |
| STAT_COD_EBAND_BLUE_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band (hell) - Lmax gem BMW GS 95010 |
| STAT_COD_EBAND_ORANGE_L_MIN_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band orange - Lmin gem BMW GS 95010 |
| STAT_COD_EBAND_ORANGE_STN_BOUNDARY_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band orange - ST/N gem BMW GS 95010 |
| STAT_COD_EBAND_ORANGE_L_MAX_WERT | HEX | high | unsigned int | - | - | - | - | - | Dimmwert Funktionsanzeige E-Band orange - Lmax gem BMW GS 95010 |
| STAT_COD_RES1_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES2_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES3_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES4_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES5_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES6_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES7_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES8_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES9_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES10_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES11_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES12_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES13_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES14_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES15_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES16_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES17_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES18_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES19_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES20_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES21_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES22_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES23_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES24_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES25_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES26_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES27_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES28_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES29_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES30_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES31_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES32_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES33_WERT | HEX | high | unsigned char | - | - | - | - | - | - |
| STAT_COD_RES34_WERT | HEX | high | unsigned char | - | - | - | - | - | - |

<a id="table-tab-position-drehsteller"></a>
### TAB_POSITION_DREHSTELLER

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ruhestellung |
| 0x01 | Tippen nach vorn |
| 0x02 | Überdrücken nach vorn |
| 0x03 | Tippen nach hinten |
| 0x04 | Überdrücken nach hinten |
| 0xFF | nicht definiert |

<a id="table-tab-corona-farbe"></a>
### TAB_CORONA_FARBE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | BLAU |
| 0x02 | ORANGE |

<a id="table-tab-entr-taster"></a>
### TAB_ENTR_TASTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht gedrueckt |
| 0x01 | gedrueckt |
| 0x02 | klemmt |
| 0xFF | unbekannnter Fehlerort |

<a id="table-tab-funktionsbeleuchtung"></a>
### TAB_FUNKTIONSBELEUCHTUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | ALLE |
| 0x02 | P |
| 0x03 | N |
| 0x04 | D |
| 0x05 | R |

<a id="table-tab-0x4100"></a>
### TAB_0X4100

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x0001 | 0x0002 | 0x0003 | 0x0004 | 0x0005 | 0x0006 | 0x0007 | 0x0008 |

<a id="table-tab-0x4101"></a>
### TAB_0X4101

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x0009 | 0x000A | 0x000B | 0x000C | 0x000D | 0x000E | 0x000F | 0x0010 |

<a id="table-tab-0x4102"></a>
### TAB_0X4102

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0011 | 0x0012 | 0x0013 | 0x0014 | 0x0015 | 0x0016 |

<a id="table-tab-0x4103"></a>
### TAB_0X4103

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0017 | 0x0018 |

<a id="table-prozessklassen-gws"></a>
### PROZESSKLASSEN_GWS

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

<a id="table-uds-tab-hex2ascii"></a>
### UDS_TAB_HEX2ASCII

Dimensions: 89 rows × 2 columns

| HEX | ASCII |
| --- | --- |
| 0x21 | ! |
| 0x23 | # |
| 0x24 | $ |
| 0x25 | % |
| 0x26 | & |
| 0x27 | ' |
| 0x28 | ( |
| 0x29 | ) |
| 0x2A | * |
| 0x2B | + |
| 0x2C | , |
| 0x2D | - |
| 0x2E | . |
| 0x2F | / |
| 0x30 | 0 |
| 0x31 | 1 |
| 0x32 | 2 |
| 0x33 | 3 |
| 0x34 | 4 |
| 0x35 | 5 |
| 0x36 | 6 |
| 0x37 | 7 |
| 0x38 | 8 |
| 0x39 | 9 |
| 0x3A | : |
| 0x3B | ; |
| 0x3C | &lt; |
| 0x3D | = |
| 0x3E | &gt; |
| 0x3F | ? |
| 0x41 | A |
| 0x42 | B |
| 0x43 | C |
| 0x44 | D |
| 0x45 | E |
| 0x46 | F |
| 0x47 | G |
| 0x48 | H |
| 0x49 | I |
| 0x4A | J |
| 0x4B | K |
| 0x4C | L |
| 0x4D | M |
| 0x4E | N |
| 0x4F | O |
| 0x50 | P |
| 0x51 | Q |
| 0x52 | R |
| 0x53 | S |
| 0x54 | T |
| 0x55 | U |
| 0x56 | V |
| 0x57 | W |
| 0x58 | X |
| 0x59 | Y |
| 0x5A | Z |
| 0x5B | [ |
| 0x5D | ] |
| 0x5E | ^ |
| 0x5F | _ |
| 0x60 | ` |
| 0x61 | a |
| 0x62 | b |
| 0x63 | c |
| 0x64 | d |
| 0x65 | e |
| 0x66 | f |
| 0x67 | g |
| 0x68 | h |
| 0x69 | i |
| 0x6A | j |
| 0x6B | k |
| 0x6C | l |
| 0x6D | m |
| 0x6E | n |
| 0x6F | o |
| 0x70 | p |
| 0x71 | q |
| 0x72 | r |
| 0x73 | s |
| 0x74 | t |
| 0x75 | u |
| 0x76 | v |
| 0x77 | w |
| 0x78 | x |
| 0x79 | y |
| 0x7A | z |
| 0x7C | \| |
| 0x7E | ~ |
