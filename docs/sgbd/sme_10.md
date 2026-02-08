# sme_10.prg

- Jobs: [40](#jobs)
- Tables: [131](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Speicher Management Elektronik der Gen2.0 |
| ORIGIN | BMW EA-412 Mellersh |
| REVISION | 3.004 |
| AUTHOR | BMW EA-412 Mellersh, Altran EA-412 Komposch |
| COMMENT | SME20 [6] |
| PACKAGE | 1.20 |
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
- [FS_LESEN_PERMANENT](#job-fs-lesen-permanent) - permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default
- [STATUS_BLOCK_LESEN](#job-status-block-lesen) - Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt
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
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)]
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [_STATUS_FS_LESEN_CSC](#job-status-fs-lesen-csc) - JobHeaderFormat UDS  : $22 ReadDataByIdentifier 0x650A _FS_LESEN_CSC

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

<a id="job-fs-lesen-permanent"></a>
### FS_LESEN_PERMANENT

permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers fuer UDS immer 3 |
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

<a id="job-status-block-lesen"></a>
### STATUS_BLOCK_LESEN

Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | long | Nummer des Blockes 0..255 |
| NEU_DEFINIEREN | string | Wenn 'JA' oder 'YES' wird der Block im SG gelöscht und neu ins SG geschrieben Wenn 'NEIN' oder 'NO' wird der Block im SG nicht gelöscht und nicht geschrieben Anschließend wird der Block gelesen |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige Result table SG_Funktionen ARG ID RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Antwort von SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Antwort von SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Antwort von SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |

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

<a id="job-status-fs-lesen-csc"></a>
### _STATUS_FS_LESEN_CSC

JobHeaderFormat UDS  : $22 ReadDataByIdentifier 0x650A _FS_LESEN_CSC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| _CSC_NUMBER | unsigned char | Nummer des CSCs 0..7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _NUMBER_OF_ENTRIES | unsigned char | Anzahl der eingetragenen CSC Fehlerspeichereinträge (max 10) |
| _CHECKSUM | unsigned int | Checksumme zum FS-Eintrag in der CSC |
| _F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| _F_ORT_NR | unsigned char | Index fuer Fehlerort |
| _FAULT_LOCATION | string | Fehlerort als Text (F_ORT_TEXT) table _FOrtTexte _ORTTEXT |
| _F_ART_NR | unsigned char | Index fuer Fehlerart |
| _FAULT_KIND | string | Fehlerart als Text (F_ART_TEXT) table _FArtTexte _ARTTEXT |
| _F_OPT_NR | unsigned char | Index fuer Fehleroption |
| _FAULT_OPTION | string | Fehleroption als Text table _FOptTexte _OPTTEXT |
| _FS_VERSION | unsigned char | Version des Fehlerspeichers der CSC |
| _TIME_SINCE_START | unsigned long | Zeit vom Applikationsstart bis FS-Eintrag in ms |
| _FAULT_MASK | unsigned long | Fehlermaske der aktiven CSC-Fehler |
| _FAULT_MASK_TEXT | string | table __FehlermaskenTexte _MASKTEXT aktive Fehler beim CSC |
| _MODULE_VOLTAGE | unsigned int | Modulspannung in mV |
| _SUM_VOLTAGE | unsigned int | Summe der Spannungen der Zellen in mV |
| _TEMPERATURE_1 | int | Temperatur vom SW1-Sensor in Grad Celcius |
| _TEMPERATURE_2 | int | Temperatur vom SW2-Sensor in Grad Celcius |
| _F_BAL_NR | unsigned int | Index fuer Balanciertext |
| _BALANCING_STATE | string | Balancierstatus als Text table _BalancierTexte _BALTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (126 × 2)
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
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FORTTEXTE](#table-forttexte) (283 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [DTCBEREICHE](#table-dtcbereiche) (20 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [IORTTEXTE](#table-iorttexte) (51 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (9 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (94 × 16)
- [TAB_HVIL_GENERATOR](#table-tab-hvil-generator) (3 × 2)
- [RES_0XDD64](#table-res-0xdd64) (1 × 10)
- [ARG_0XDD64](#table-arg-0xdd64) (1 × 12)
- [TAB_HVIL_GENERATOR_GEN2](#table-tab-hvil-generator-gen2) (3 × 2)
- [TAB_SYSTEM_STATUS](#table-tab-system-status) (6 × 2)
- [TAB_SCHUETZ_STATUS](#table-tab-schuetz-status) (5 × 2)
- [RDTCI_LEV_DOP](#table-rdtci-lev-dop) (9 × 2)
- [ARG_0XDD61](#table-arg-0xdd61) (1 × 12)
- [ARG_0XDD6E](#table-arg-0xdd6e) (2 × 12)
- [ARG_0XDD6F](#table-arg-0xdd6f) (1 × 12)
- [ARG_0XDD78](#table-arg-0xdd78) (1 × 12)
- [ARG_0XDD79](#table-arg-0xdd79) (2 × 12)
- [ARG_0XDD7B](#table-arg-0xdd7b) (1 × 12)
- [ARG_0XDDC1](#table-arg-0xddc1) (1 × 12)
- [ARG_0XDDC4](#table-arg-0xddc4) (2 × 12)
- [ARG_0XDDCC](#table-arg-0xddcc) (1 × 12)
- [ARG_0XDDCD](#table-arg-0xddcd) (1 × 12)
- [ARG_0XDF61](#table-arg-0xdf61) (2 × 12)
- [RES_0XAD61](#table-res-0xad61) (2 × 13)
- [RES_0XAD66](#table-res-0xad66) (2 × 13)
- [RES_0XDD61](#table-res-0xdd61) (1 × 10)
- [RES_0XDD63](#table-res-0xdd63) (2 × 10)
- [RES_0XDD6A](#table-res-0xdd6a) (4 × 10)
- [RES_0XDD6B](#table-res-0xdd6b) (8 × 10)
- [RES_0XDD6F](#table-res-0xdd6f) (1 × 10)
- [RES_0XDD7B](#table-res-0xdd7b) (1 × 10)
- [RES_0XDD7C](#table-res-0xdd7c) (26 × 10)
- [RES_0XDD7D](#table-res-0xdd7d) (2 × 10)
- [RES_0XDD7E](#table-res-0xdd7e) (2 × 10)
- [RES_0XDD8E](#table-res-0xdd8e) (28 × 10)
- [RES_0XDD90](#table-res-0xdd90) (28 × 10)
- [RES_0XDD91](#table-res-0xdd91) (12 × 10)
- [RES_0XDD94](#table-res-0xdd94) (70 × 10)
- [RES_0XDD95](#table-res-0xdd95) (70 × 10)
- [RES_0XDD96](#table-res-0xdd96) (70 × 10)
- [RES_0XDD97](#table-res-0xdd97) (70 × 10)
- [RES_0XDD98](#table-res-0xdd98) (70 × 10)
- [RES_0XDD99](#table-res-0xdd99) (70 × 10)
- [RES_0XDD9A](#table-res-0xdd9a) (70 × 10)
- [RES_0XDDAE](#table-res-0xddae) (12 × 10)
- [RES_0XDDAF](#table-res-0xddaf) (12 × 10)
- [RES_0XDDB0](#table-res-0xddb0) (12 × 10)
- [RES_0XDDB1](#table-res-0xddb1) (12 × 10)
- [RES_0XDDB2](#table-res-0xddb2) (12 × 10)
- [RES_0XDDB3](#table-res-0xddb3) (2 × 10)
- [RES_0XDDB9](#table-res-0xddb9) (12 × 10)
- [RES_0XDDBA](#table-res-0xddba) (12 × 10)
- [RES_0XDDBB](#table-res-0xddbb) (12 × 10)
- [RES_0XDDBC](#table-res-0xddbc) (3 × 10)
- [RES_0XDDBE](#table-res-0xddbe) (15 × 10)
- [RES_0XDDBF](#table-res-0xddbf) (2 × 10)
- [RES_0XDDC0](#table-res-0xddc0) (4 × 10)
- [RES_0XDDC1](#table-res-0xddc1) (8 × 10)
- [RES_0XDDC2](#table-res-0xddc2) (6 × 10)
- [RES_0XDDC4](#table-res-0xddc4) (2 × 10)
- [RES_0XDDC5](#table-res-0xddc5) (8 × 10)
- [RES_0XDDC6](#table-res-0xddc6) (8 × 10)
- [RES_0XDDC7](#table-res-0xddc7) (8 × 10)
- [RES_0XDDC8](#table-res-0xddc8) (5 × 10)
- [RES_0XDDC9](#table-res-0xddc9) (15 × 10)
- [RES_0XDDCB](#table-res-0xddcb) (2 × 10)
- [RES_0XDDCC](#table-res-0xddcc) (3 × 10)
- [RES_0XDDCF](#table-res-0xddcf) (2 × 10)
- [RES_0XDDE8](#table-res-0xdde8) (2 × 10)
- [RES_0XDDE9](#table-res-0xdde9) (24 × 10)
- [RES_0XDF60](#table-res-0xdf60) (2 × 10)
- [RES_0XDF64](#table-res-0xdf64) (4 × 10)
- [RES_0XDF65](#table-res-0xdf65) (5 × 10)
- [RES_0XDF66](#table-res-0xdf66) (6 × 10)
- [RES_0XDF67](#table-res-0xdf67) (2 × 10)
- [ARG_0X6500](#table-arg-0x6500) (2 × 12)
- [ARG_0X6501](#table-arg-0x6501) (2 × 12)
- [ARG_0X6502](#table-arg-0x6502) (2 × 12)
- [ARG_0X6503](#table-arg-0x6503) (2 × 12)
- [ARG_0X6504](#table-arg-0x6504) (2 × 12)
- [ARG_0X6506](#table-arg-0x6506) (2 × 12)
- [ARG_0X6507](#table-arg-0x6507) (2 × 12)
- [ARG_0X6508](#table-arg-0x6508) (2 × 12)
- [ARG_0X6509](#table-arg-0x6509) (2 × 12)
- [ARG_0X650B](#table-arg-0x650b) (2 × 12)
- [ARG_0X6511](#table-arg-0x6511) (2 × 12)
- [ARG_0X6512](#table-arg-0x6512) (2 × 12)
- [ARG_0X6515](#table-arg-0x6515) (2 × 12)
- [ARG_0X6519](#table-arg-0x6519) (2 × 12)
- [ARG_0X651B](#table-arg-0x651b) (2 × 12)
- [TAB_SCHUETZ_FREIGABE](#table-tab-schuetz-freigabe) (3 × 2)
- [TAB_KUEHLKREISLAUF_VENTIL_RUECKGABE](#table-tab-kuehlkreislauf-ventil-rueckgabe) (3 × 2)
- [TAB_AUFSTART_VERHINDERER](#table-tab-aufstart-verhinderer) (3 × 2)
- [TAB_KUEHLERKREISLAUF_VENTIL](#table-tab-kuehlerkreislauf-ventil) (4 × 2)
- [TAB_SYM_MODUS](#table-tab-sym-modus) (4 × 2)
- [TAB_SCHUETZ_SCHALTER](#table-tab-schuetz-schalter) (4 × 2)
- [TAB_ISOLATION_ISOLATIONSFEHLER](#table-tab-isolation-isolationsfehler) (4 × 2)
- [TAB_ISOLATION_ERFOLGREICH](#table-tab-isolation-erfolgreich) (4 × 2)
- [SVK_VERSION_DOP](#table-svk-version-dop) (2 × 2)
- [TAB_SME_ERMITTLUNG](#table-tab-sme-ermittlung) (4 × 2)
- [TAB_SME_SYMMETRIERUNG_FERTIG](#table-tab-sme-symmetrierung-fertig) (2 × 2)
- [DM_TAB_ROE_ACTIVATED_DOP](#table-dm-tab-roe-activated-dop) (2 × 2)
- [TAB_STATUS_HVIL](#table-tab-status-hvil) (3 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [TAB_ANST_SCHUETZ](#table-tab-anst-schuetz) (2 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [ENERGIESPARMODE_DOP](#table-energiesparmode-dop) (4 × 2)
- [PROG_DEP_DOP](#table-prog-dep-dop) (6 × 2)
- [EXTENDED_ENERGY_MODE_DOP](#table-extended-energy-mode-dop) (16 × 2)
- [_FORTTEXTE](#table-forttexte) (21 × 2)
- [_FARTTEXTE](#table-farttexte) (27 × 2)
- [_FOPTTEXTE](#table-fopttexte) (5 × 2)
- [_BALANCIERTEXTE](#table-balanciertexte) (5 × 2)
- [_FEHLERMASKENTEXTE](#table-fehlermaskentexte) (30 × 2)

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

Dimensions: 126 rows × 2 columns

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 6 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | Hier deaktivierte Funktionen gemäß FeTra-Liste festhalten |
| 0x01 | Spezieller Energiesparmode | - |
| 0x02 | ECOS-Mode | - |
| 0x03 | MOST-Mode | - |
| 0x04 | Rollenmode | - |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 283 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x020700 | Energiesparmode aktiv | 0 |
| 0x020708 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x020709 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02070A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02070B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 |
| 0x02070C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x02FF07 | Dummy-Fehlerspeichereintrag im Komponentenbereich nur für Testzwecke | 0 |
| 0x21F000 | HVS: Hauptschalter (K2): Kurzschluss nach Masse | 0 |
| 0x21F001 | HVS: Hauptschalter (K2): Kurzschluss nach Ubatt | 0 |
| 0x21F002 | HVS: Hauptschalter (K2): offene Leitung | 0 |
| 0x21F003 | HVS: Hauptschalter (K1): Kurzschluss nach Masse | 0 |
| 0x21F004 | HVS: Hauptschalter (K1): Kurzschluss nach Ubatt | 0 |
| 0x21F005 | HVS: Hauptschalter (K1): offene Leitung | 0 |
| 0x21F006 | HVS: Hauptschalter (K3): Kurzschluss nach Masse | 0 |
| 0x21F007 | HVS: Hauptschalter (K3): Kurzschluss nach Ubatt | 0 |
| 0x21F008 | HVS: Hauptschalter (K3): offene Leitung | 0 |
| 0x21F009 | HVS: Hauptschalter (K2): Treiberfehler | 0 |
| 0x21F00A | HVS: Hauptschalter (K1): Treiberfehler | 0 |
| 0x21F00B | HVS: Hauptschalter (K3): Treiberfehler | 0 |
| 0x21F00F | HVS: Hauptschalter (Lowside): Kurzschluss nach Masse | 0 |
| 0x21F011 | SME: EEPROM NV-Daten stehen auf Initialwerten | 0 |
| 0x21F015 | SME: Spannungsversorgung intern- - 5V Spannung zu niedrig | 0 |
| 0x21F016 | HVS: Stromversorgung CSC- - Kurzschluss nach Masse | 0 |
| 0x21F017 | HVS: Stromversorgung CSC- - Kurzschluss nach Ubatt | 0 |
| 0x21F018 | HVS: Stromversorgung CSC- - offene Leitung | 0 |
| 0x21F019 | HVS: CSC Treiberfehler | 0 |
| 0x21F01A | HVS: Stromversorgung U/i-Sensor- - Kurzschluss nach Masse | 0 |
| 0x21F01B | HVS: Stromversorgung U/i-Sensor- - Kurzschluss nach Ubatt | 0 |
| 0x21F01C | HVS: Stromversorgung U/i-Sensor- - offene Leitung | 0 |
| 0x21F01D | SME: Werte der Echtzeituhr unplausibel | 0 |
| 0x21F01E | SME: Wakeup der Echtzeituhr fehlerhaft | 0 |
| 0x21F020 | Kühlventil: Kurzschluss nach Masse | 1 |
| 0x21F021 | Kühlventil: Kurzschluss nach Ubatt | 1 |
| 0x21F022 | Kühlventil: offene Leitung | 1 |
| 0x21F023 | Kühlventil: Treiberfehler | 0 |
| 0x21F025 | HVS: Temp.-Sensor Kühlung: außerhalb Bereich (oben) | 0 |
| 0x21F026 | HVS: Temp.-Sensor Kühlung: außerhalb Bereich (unten) | 0 |
| 0x21F027 | HVS: Temp.-Sensor Kühlung: Kurzschluss nach Masse | 0 |
| 0x21F028 | HVS: Temp.-Sensor Kühlung: Kurzschluß nach Ubatt oder offene Leitung | 0 |
| 0x21F029 | SME: EEPROM, NV-Daten- - Lesefehler | 0 |
| 0x21F02A | SME: EEPROM, NV-Daten- - Schreibfehler | 0 |
| 0x21F02B | SME: unerwarteter Reset festgestellt | 0 |
| 0x21F02D | SME: RAM Defekt in Initialisierungsphase | 0 |
| 0x21F02E | SME: RAM Defekt in Laufzeitphase | 0 |
| 0x21F030 | SME: ROM Defekt in Laufzeitphase | 0 |
| 0x21F035 | HVS: U/i-Sensor -  CRC-Fehler bei Empfang auf Sensor | 0 |
| 0x21F037 | HVS: U/i-Sensor -  CRC-Fehler Programmspeicher | 0 |
| 0x21F038 | HVS: U/i-Sensor -  CRC-Fehler Kalibrierdaten auf dem Hauptcontroller | 0 |
| 0x21F039 | HVS: U/i-Sensor -  Fehler Spannungsversorgung Frontend Baustein | 0 |
| 0x21F03A | HVS: U/i-Sensor -  Fehler Referenzspannung Frontend Baustein | 0 |
| 0x21F03C | HVS: U/i-Sensor -  Fehler Kalibrierungsdaten Frontendbaustein | 0 |
| 0x21F03D | HVS: U/i-Sensor -  Leitungsbruch Strompfad | 0 |
| 0x21F041 | U/i-Sensor:  Fehler in der Konfiguration des Frontendbausteins | 0 |
| 0x21F042 | U/i-Sensor: Überlauf Strommessung | 0 |
| 0x21F043 | U/i-Sensor: Überlauf Messung Ubatt | 0 |
| 0x21F044 | U/i-Sensor: Überlauf Messung Uk2 | 0 |
| 0x21F045 | U/i-Sensor: Überlauf Messung Uq | 0 |
| 0x21F046 | U/i-Sensor: Meßbereichsüberschreitung Stromsensor (oben) | 0 |
| 0x21F047 | U/i-Sensor: Meßbereichsüberschreitung Stromsensor (unten) | 0 |
| 0x21F048 | U/i-Sensor: Messbereichsüberschreitung Ubatt (oben) | 0 |
| 0x21F049 | U/i-Sensor: Messbereichsüberschreitung Ubatt (unten) | 0 |
| 0x21F04A | U/i-Sensor: Messbereichsüberschreitung Uk2 (oben) | 0 |
| 0x21F04B | U/i-Sensor: Messbereichsüberschreitung Uk2 (unten) | 0 |
| 0x21F04C | U/i-Sensor: Messbereichsüberschreitung Uq (oben) | 0 |
| 0x21F04D | U/i-Sensor: Messbereichsüberschreitung Uq (unten) | 0 |
| 0x21F04E | HVS: U/i-Sensor - Steuerungsmodul BUS OFF | 0 |
| 0x21F04F | HVS: U/i-Sensor-Layer -  CRC-Fehler erkannt auf SME | 0 |
| 0x21F050 | HVS: U/i-Sensor -  Fehler Betriebsmodus | 0 |
| 0x21F052 | HVS: U/i-Sensor -  Treiberfehler | 0 |
| 0x21F054 | Crashsensor (Kl. 30C): Wert außerhalb Bereich oben | 0 |
| 0x21F055 | Klemme30F: Wert außerhalb Bereich oben | 0 |
| 0x21F056 | Klemme 15: Wert außerhalb Bereich oben | 0 |
| 0x21F057 | HVS: Ruhestromabschaltung HW-Peripherie -  nicht funktionsfähig | 0 |
| 0x21F058 | HVS: Ruhestromabschaltung SME -  Timeout für Nachlaufdiagnosen | 0 |
| 0x21F059 | HVS: Ruhestromabschaltung SME -  Timeout im Nachlauf | 0 |
| 0x21F05E | HVS: U/i-Sensor -  interner U/i-Sensorfehler | 0 |
| 0x21F06E | HVS: CSC CAN: CSC fehlt | 0 |
| 0x21F080 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 1 außerhalb Bereich (oben) | 0 |
| 0x21F081 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 1 außerhalb Bereich (unten) | 0 |
| 0x21F082 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 2 außerhalb Bereich (oben) | 0 |
| 0x21F083 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 2 außerhalb Bereich (unten) | 0 |
| 0x21F084 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 3 außerhalb Bereich (oben) | 0 |
| 0x21F085 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 3 außerhalb Bereich (unten) | 0 |
| 0x21F086 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 4 außerhalb Bereich (oben) | 0 |
| 0x21F087 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 4 außerhalb Bereich (unten) | 0 |
| 0x21F088 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 5 außerhalb Bereich (oben) | 0 |
| 0x21F089 | HVS: CSC Funktion: mind. eine Zellspannung im Modul 5 außerhalb Bereich (unten) | 0 |
| 0x21F08A | HVS: CSC Funktion: mind. eine Zellspannung im Modul 6 außerhalb Bereich (oben) | 0 |
| 0x21F08B | HVS: CSC Funktion: mind. eine Zellspannung im Modul 6 außerhalb Bereich (unten) | 0 |
| 0x21F08C | HVS: CSC Funktion: mind. eine Zellspannung im Modul 7 außerhalb Bereich (oben) | 0 |
| 0x21F08D | HVS: CSC Funktion: mind. eine Zellspannung im Modul 7 außerhalb Bereich (unten) | 0 |
| 0x21F08E | HVS: CSC Funktion: mind. eine Zellspannung im Modul 8 außerhalb Bereich (oben) | 0 |
| 0x21F08F | HVS: CSC Funktion: mind. eine Zellspannung im Modul 8 außerhalb Bereich (unten) | 0 |
| 0x21F090 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 1 außerhalb Bereich (oben) | 0 |
| 0x21F091 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 1 außerhalb Bereich (unten) | 0 |
| 0x21F092 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 2 außerhalb Bereich (oben) | 0 |
| 0x21F093 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 2 außerhalb Bereich (unten) | 0 |
| 0x21F094 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 3 außerhalb Bereich (oben) | 0 |
| 0x21F095 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 3 außerhalb Bereich (unten) | 0 |
| 0x21F096 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 4 außerhalb Bereich (oben) | 0 |
| 0x21F097 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 4 außerhalb Bereich (unten) | 0 |
| 0x21F098 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 5 außerhalb Bereich (oben) | 0 |
| 0x21F099 | HVS: CSC Funktion: mind. ein T-Sensor im Modul 5 außerhalb Bereich (unten) | 0 |
| 0x21F09A | HVS: CSC Funktion: mind. ein T-Sensor im Modul 6 außerhalb Bereich (oben) | 0 |
| 0x21F09B | HVS: CSC Funktion: mind. ein T-Sensor im Modul 6 außerhalb Bereich (unten) | 0 |
| 0x21F09C | HVS: CSC Funktion: mind. ein T-Sensor im Modul 7 außerhalb Bereich (oben) | 0 |
| 0x21F09D | HVS: CSC Funktion: mind. ein T-Sensor im Modul 7 außerhalb Bereich (unten) | 0 |
| 0x21F09E | HVS: CSC Funktion: mind. ein T-Sensor im Modul 8 außerhalb Bereich (oben) | 0 |
| 0x21F09F | HVS: CSC Funktion: mind. ein T-Sensor im Modul 8 außerhalb Bereich (unten) | 0 |
| 0x21F0A0 | HVS: CSC Funktion: Modulspannung 1 außerhalb Bereich (High) | 0 |
| 0x21F0A1 | HVS: CSC Funktion: Modulspannung 1 außerhalb Bereich (Low) | 0 |
| 0x21F0A2 | HVS: CSC Funktion: Modulspannung 2 außerhalb Bereich (High) | 0 |
| 0x21F0A3 | HVS: CSC Funktion: Modulspannung 2 außerhalb Bereich (Low) | 0 |
| 0x21F0A4 | HVS: CSC Funktion: Modulspannung 3 außerhalb Bereich (High) | 0 |
| 0x21F0A5 | HVS: CSC Funktion: Modulspannung 3 außerhalb Bereich (Low) | 0 |
| 0x21F0A6 | HVS: CSC Funktion: Modulspannung 4 außerhalb Bereich (High) | 0 |
| 0x21F0A7 | HVS: CSC Funktion: Modulspannung 4 außerhalb Bereich (Low) | 0 |
| 0x21F0A8 | HVS: CSC Funktion: Modulspannung 5 außerhalb Bereich (High) | 0 |
| 0x21F0A9 | HVS: CSC Funktion: Modulspannung 5 außerhalb Bereich (Low) | 0 |
| 0x21F0AA | HVS: CSC Funktion: Modulspannung 6 außerhalb Bereich (High) | 0 |
| 0x21F0AB | HVS: CSC Funktion: Modulspannung 6 außerhalb Bereich (Low) | 0 |
| 0x21F0AC | HVS: CSC Funktion: Modulspannung 7 außerhalb Bereich (High) | 0 |
| 0x21F0AD | HVS: CSC Funktion: Modulspannung 7 außerhalb Bereich (Low) | 0 |
| 0x21F0AE | HVS: CSC Funktion: Modulspannung 8 außerhalb Bereich (High) | 0 |
| 0x21F0AF | HVS: CSC Funktion: Modulspannung 8 außerhalb Bereich (Low) | 0 |
| 0x21F0B0 | HVS: CSC Funktion: offene Leitung einer Zellspannungsmessung aufgetreten | 0 |
| 0x21F0B1 | HVS: CSC Funktion: Symmetriereinheit defekt | 0 |
| 0x21F0B3 | HVS: CSC Funktion: thermisches Abschalten aufgetreten | 0 |
| 0x21F0B4 | HVS: CSC Funktion: Ungültige Anfrage empfangen | 0 |
| 0x21F0B5 | HVS: CSC Funktion: Symmetrierung nicht möglich, niedrigste Symmetrierspannung erreicht | 0 |
| 0x21F0B6 | HVS: CSC Funktion: CSC Wake-Up defekt | 0 |
| 0x21F0B7 | HVS: CSC Funktion: Kommunikation Frontend/CSC fehlgeschlagen | 0 |
| 0x21F0B8 | HVS: CSC Funktion: ungültige CAN DB | 0 |
| 0x21F0B9 | HVS: CSC Funktion: CAN Kommunikationsausfall detektiert | 0 |
| 0x21F0BA | HVS: CSC Funktion: ADC-Test 1 LTC6802 nicht bestanden | 0 |
| 0x21F0BB | HVS: CSC Funktion: ADC-Test 2 LTC6802 nicht bestanden | 0 |
| 0x21F0BC | HVS: CSC Funktion: LTC6801 Selbsttest nicht bestanden | 0 |
| 0x21F0BD | HVS: CSC Funktion: RAM Selbsttest nicht bestanden | 0 |
| 0x21F0BE | HVS: CSC Funktion: ROM Selbsttest nicht bestanden | 0 |
| 0x21F0BF | HVS: CSC Funktion: offene Leitung einer T-Messung aufgetreten | 0 |
| 0x21F0C0 | HVS: CSC Funktion: Plausibilitätsfehler Zellspannung | 0 |
| 0x21F0C1 | HVS: CSC Funktion: Plausibilitätsfehler Zelltemperatur | 0 |
| 0x21F0C2 | HVS: CSC Funktion: kritischer Hardwaredefekt | 0 |
| 0x21F100 | Service Disconnect: steckt nicht | 1 |
| 0x21F101 | Service Disconnect: Auswertung unplausibel | 0 |
| 0x21F102 | Crash: Crash I (ACAN, reversibel) festgestellt | 1 |
| 0x21F103 | Crash: Crash II (ACAN und KL30C, irreversibel) festgestellt | 1 |
| 0x21F104 | 12 V Versorgung (KL 30 F): Unterspannung | 1 |
| 0x21F105 | 12 V Versorgung (KL 30 F): Überspannung | 1 |
| 0x21F106 | Crashüberwachung (KL 30 C): Unterspannung | 1 |
| 0x21F107 | Kühlventil: Ventil lässt sich nicht schließen | 1 |
| 0x21F108 | Kühlventil: Ventil lässt sich nicht öffnen | 1 |
| 0x21F10A | HVS: Hauptschalter: Lebensdauerende erreicht | 0 |
| 0x21F10B | HVS: Hauptschalter: neg. Schütze kleben | 0 |
| 0x21F10C | HVS: Hauptschalter: neg. Schütze lassen sich nicht schließen | 0 |
| 0x21F10D | Stromüberwachung: Überstrom erkannt | 1 |
| 0x21F10E | HVS: Hauptschalter: pos. Schütze kleben | 0 |
| 0x21F10F | HVS: Hauptschalter: pos. Schütze lassen sich nicht schließen | 0 |
| 0x21F110 | Hauptschalter: Abschaltung unter Last festgestellt | 0 |
| 0x21F113 | Stromüberwachung: Toleranzüberschreitung untere Strombegrenzung | 1 |
| 0x21F114 | Stromüberwachung: Toleranzüberschreitung obere Strombegrenzung | 1 |
| 0x21F123 | Zellspannung -  Toleranzüberschreitung obere Spannungsbegrenzung | 1 |
| 0x21F124 | Zellspannung -  Toleranzüberschreitung untere Spannungsbegrenzung | 1 |
| 0x21F127 | Batteriespannung: Toleranzüberschreitung obere Spannungsbegrenzung | 1 |
| 0x21F128 | Batteriespannung: Toleranzüberschreitung untere Spannungsbegrenzung | 1 |
| 0x21F129 | HVS: HV-Interlock: kein Signal erzeugt | 0 |
| 0x21F12A | HV-Interlock: offene Leitung | 1 |
| 0x21F12B | HV-Interlock: Kurzschluss in Schleife | 1 |
| 0x21F12C | HV-Interlock: Kurzschluss nach Ubatt | 1 |
| 0x21F12D | HV-Interlock: Kurzschluss nach Masse | 1 |
| 0x21F130 | Isolationsüberwachung -  Isolationsfehler im Gesamtsystem (geschlossene Schütze) | 0 |
| 0x21F133 | Isolationsüberwachung -  Isolationswarnung im Gesamtsystem (geschlossene Schütze) | 0 |
| 0x21F138 | HVS: Isolationsüberwachung -  interner Isolationsfehler (offene Schütze) | 0 |
| 0x21F13A | HVS: Isolationsüberwachung -  Isolationsüberwachung deaktivert | 0 |
| 0x21F13B | HVS: Isolationsüberwachung -  interne Isolationwarnung (offene Schütze) | 0 |
| 0x21F13E | Vorladung -  Strom zu hoch | 1 |
| 0x21F140 | Vorladung -  Zeit zu lang | 1 |
| 0x21F141 | Vorladung -  Zeit zu kurz | 1 |
| 0x21F142 | Vorladung -  Kurzschluss im Zwischenkreis detektiert | 1 |
| 0x21F144 | Plausibilität Stromwert -  Strom unplausibel. Kein Ersatzwert vorhanden | 0 |
| 0x21F146 | HVS: Plausibilität Zwischenkreisspannung -  Spannung fehlerhaft, kein Ersatzwert vorhanden | 0 |
| 0x21F147 | HVS: Zellspannungsmessung -  eine oder mehrere Zellspannungen ungültig | 0 |
| 0x21F148 | HVS: Plausibilität Batteriespannung -  HV-Spannungsmessung unplausibel, Ersatzwert im Einsatz | 0 |
| 0x21F149 | HVS: Plausibilität Batteriespannung -  HV-Spannungsmessung unplausibel, kein Ersatzwert vorhanden | 0 |
| 0x21F150 | HVS: Plausibilität Batteriespannung -  Modulsummenspannung unplausibel | 0 |
| 0x21F151 | HVS: Plausibilität Batteriespannung -  Zellsummenspannung unplausibel | 0 |
| 0x21F152 | HVS: Plausibillität Spannungssensorik Modul 1 -  Spannung unplausibel | 0 |
| 0x21F153 | HVS: Plausibillität Spannungssensorik Modul 2 -  Spannung unplausibel | 0 |
| 0x21F154 | HVS: Plausibillität Spannungssensorik Modul 3 -  Spannung unplausibel | 0 |
| 0x21F155 | HVS: Plausibillität Spannungssensorik Modul 4 -  Spannung unplausibel | 0 |
| 0x21F156 | HVS: Plausibillität Spannungssensorik Modul 5 -  Spannung unplausibel | 0 |
| 0x21F157 | HVS: Plausibillität Spannungssensorik Modul 6 -  Spannung unplausibel | 0 |
| 0x21F158 | HVS: Plausibillität Spannungssensorik Modul 7 -  Spannung unplausibel | 0 |
| 0x21F159 | HVS: Plausibillität Spannungssensorik Modul 8 -  Spannung unplausibel | 0 |
| 0x21F15B | HVS: Zelltemperaturen -  Modultemperatur 1/8 unplausibel | 0 |
| 0x21F15C | HVS: Zelltemperaturen -  Modultemperatur 2/8 unplausibel | 0 |
| 0x21F15D | HVS: Zelltemperaturen -  Modultemperatur 3/8 unplausibel | 0 |
| 0x21F15E | HVS: Zelltemperaturen -  Modultemperatur 4/8 unplausibel | 0 |
| 0x21F15F | HVS: Zelltemperaturen -  Modultemperatur 5/8 unplausibel | 0 |
| 0x21F160 | HVS: Zelltemperaturen -  Modultemperatur 6/8 unplausibel | 0 |
| 0x21F161 | HVS: Zelltemperaturen -  Modultemperatur 7/8 unplausibel | 0 |
| 0x21F162 | HVS: Zelltemperaturen -  Modultemperatur 8/8 unplausibel | 0 |
| 0x21F163 | HVS: Zelltemperaturen: Zu viele Sensoren unplausibel | 0 |
| 0x21F167 | HVS: Zelltemperaturen -  Modultemperaturen 1/8 ausgefallen | 0 |
| 0x21F168 | HVS: Zelltemperaturen -  Modultemperaturen 2/8 ausgefallen | 0 |
| 0x21F169 | HVS: Zelltemperaturen -  Modultemperaturen 3/8 ausgefallen | 0 |
| 0x21F16A | HVS: Zelltemperaturen -  Modultemperaturen 4/8 ausgefallen | 0 |
| 0x21F16B | HVS: Zelltemperaturen -  Modultemperaturen 5/8 ausgefallen | 0 |
| 0x21F16C | HVS: Zelltemperaturen -  Modultemperaturen 6/8 ausgefallen | 0 |
| 0x21F16D | HVS: Zelltemperaturen -  Modultemperaturen 7/8 ausgefallen | 0 |
| 0x21F16E | HVS: Zelltemperaturen -  Modultemperaturen 8/8 ausgefallen | 0 |
| 0x21F16F | HVS: Zelltemperaturen: Hohe Temperatur, Leistungsbegrenzung aktiv | 0 |
| 0x21F170 | HVS: Zelltemperaturen: 1/8 Übertemperatur | 0 |
| 0x21F171 | HVS: Zelltemperaturen: 2/8 Übertemperatur | 0 |
| 0x21F172 | HVS: Zelltemperaturen: 3/8 Übertemperatur | 0 |
| 0x21F173 | HVS: Zelltemperaturen: 4/8 Übertemperatur | 0 |
| 0x21F174 | HVS: Zelltemperaturen: 5/8 Übertemperatur | 0 |
| 0x21F175 | HVS: Zelltemperaturen: 6/8 Übertemperatur | 0 |
| 0x21F176 | HVS: Zelltemperaturen: 7/8 Übertemperatur | 0 |
| 0x21F177 | HVS: Zelltemperaturen: 8/8 Übertemperatur | 0 |
| 0x21F17B | HVS: Batteriealterung: SOH niedrig (Fehlerschwelle) | 0 |
| 0x21F180 | Ladungszustand: kritische obere SoC-Grenze erreicht | 0 |
| 0x21F181 | Ladungszustand: kritische untere SoC-Grenze erreicht | 0 |
| 0x21F183 | HVS: Zellüberwachung: Zellen sind stark unsymmetriert | 0 |
| 0x21F186 | HVS: Zellüberwachung: Zelldefekt festgestellt | 0 |
| 0x21F187 | HVS: Zellüberwachung: Tiefentladung festgestellt | 0 |
| 0x21F18A | Deaktivierung Hauptschalter nach Fehler | 0 |
| 0x21F18C | Zuschaltung verhindert -  Überhitzungsschutz | 0 |
| 0x21F18D | Zuschaltung verhindert -  Maximale Anzahl Fehlversuche überschritten. | 0 |
| 0x21F18E | Zuschaltung verhindert -  Zwischenkreisspannung außerhalb des zulässigen Bereichs | 1 |
| 0x21F18F | Zuschaltung verhindert -  Sicherheitsmerkmale nicht erfüllt | 0 |
| 0x21F190 | HVS: Zuschaltung verhindert -  Transport-Bit gesetzt | 0 |
| 0x21F191 | HVS: Zuschaltung verhindert -  Entladeschutz aktiv, CSC im Standby | 0 |
| 0x21F192 | HVS: Zuschaltung verhindert -  NM nicht aktiv | 1 |
| 0x21F193 | HVS: Abschaltung der Hauptschütze -  Flashmode aktiv | 0 |
| 0x21F195 | HVS: Zuschaltung nicht möglich, Verdacht auf Kontaktunterbrechung durch Schmelzsicherung. Überstrom erkannt. | 0 |
| 0x21F1A0 | Sicherheitskonzept, Ebene 2: Hochvolt-Batterie, Temperatur zu hoch oder unbekannt | 0 |
| 0x21F1A1 | Sicherheitskonzept, Ebene 2: Hochvolt-Batterie, Spannung zu niedrig/hoch oder unbekannt | 1 |
| 0x21F1A2 | SME: Sicherheitskonzept  - Ebene 3 Schützöffner nach Timeout für Flashvorgang | 1 |
| 0x21F1A3 | Sicherheitskonzept, Ebene 2: Hochvolt-Batterie, Strom zu niedrig/hoch oder unbekannt | 1 |
| 0x21F1A4 | SME: Sicherheitskonzept -  Vorhalt 11 | 0 |
| 0x21F1A5 | SME: Sicherheitskonzept -  Vorhalt 12 | 0 |
| 0x21F1A6 | SME: Sicherheitskonzept -  Vorhalt 13 | 0 |
| 0x21F1A7 | Sicherheitskonzept, Ebene 2: SME, Abschaltpfadtest fehlgeschlagen | 0 |
| 0x21F1A8 | Sicherheitskonzept, Ebene 2: SME, Abschaltpfadtest Lowside fehlgeschlagen | 0 |
| 0x21F1A9 | HVS: Ebene1 -  Abschaltpfadtest K1 fehlgeschlagen | 0 |
| 0x21F1B0 | HVS: Ebene1 -  Abschaltpfadtest K2 fehlgeschlagen | 0 |
| 0x21F1B1 | HVS: Ebene1 -  Abschaltpfadtest K3 fehlgeschlagen | 0 |
| 0x21F1B2 | HVS: Ebene2 -  Abschalten detektiert | 0 |
| 0x21F1B3 | HVS: Ebene2 -  Timeout Abschaltpfadtest Sicherheitsrechner | 0 |
| 0x21F1B4 | SME: Sicherheitskonzept - Fehler in Laufzeitüberwachung | 0 |
| 0x21F1B5 | SME: Sicherheitskonzept - Prozessor-Test fehlgeschlagen | 0 |
| 0x21F1B6 | Sicherheitskonzept, Ebene 3: SME, Reset des Sicherheitsrechners | 0 |
| 0x21F1B7 | SME: Sicherheitskonzept - Reset Hauptrechner durch Watchdog | 0 |
| 0x21F1B8 | SME: Sicherheitskonzept - inkonsistentes RAM erkannt | 0 |
| 0x21F1B9 | Sicherheitskonzept, Ebene 3: SME, Maximale Anzahl an Resetzyklen erreicht | 0 |
| 0x21F1BA | SME: Sicherheitskonzept -  Abschaltung durch Ebene2 | 0 |
| 0x21F1BB | SME: Sicherheitskonzept - Speicher-ECC-Fehler | 0 |
| 0x21F1BC | SME: Sicherheitskonzept - nicht implementierter Interrupt | 0 |
| 0x21F1BD | SME: Sicherheitskonzept - Reset Hauptrechner durch Sicherheitsrechner | 0 |
| 0x21F1BE | SME: Sicherheitskonzept -  Core-Test kann nicht durchgeführt werden | 0 |
| 0x21F1F4 | HVS: CSC Version ungültig | 0 |
| 0xCAC486 | A-CAN: Steuerungsmodul BUS OFF | 1 |
| 0xCACBFF | Dummy-Fehlerspeichereintrag im Netzwerkfehler nur für Testzwecke | 0 |
| 0xCACC09 | HVS: CSC CAN: Steuerungsmodul BUS OFF | 0 |
| 0xCAD400 | CAN-Botschaft ungültig ST_MOT_1 | 1 |
| 0xCAD401 | CAN-Botschaft ungültig A_TEMP | 1 |
| 0xCAD405 | CAN-Botschaft ungültig DIAG_OBD_ENGMG_EL | 1 |
| 0xCAD406 | CAN-Botschaft ungültig TORQ_CRSH_1 | 1 |
| 0xCAD407 | CAN-Botschaft ungültig FAHRGESTELLNUMMER | 1 |
| 0xCAD408 | CAN-Botschaft ungültig FZZSTD | 1 |
| 0xCAD409 | CAN-Botschaft ungültig RLS_COOL_HVSTO | 1 |
| 0xCAD40A | CAN-Botschaft ungültig V_VEH | 1 |
| 0xCAD40B | CAN-Botschaft ungültig KILOMETERSTAND | 1 |
| 0xCAD40C | CAN-Botschaft ungültig KLEMMEN | 1 |
| 0xCAD40F | CAN-Botschaft ungültig ST_DCDC | 1 |
| 0xCAD410 | CAN-Botschaft ungültig ST_HYB_2 | 1 |
| 0xCAD411 | CAN-Botschaft ungültig CTR_CRASH_SWO_EKP | 1 |
| 0xCAD413 | CAN-Botschaft ungültig SPEC_HVSTO | 1 |
| 0xCAD414 | CAN-Botschaft ungültig STAT_ZV_KLAPPEN | 1 |
| 0xCAD416 | CAN-Signal ungültig RQ_CLO_DCSW_HVSTO | 1 |
| 0xCAF400 | Botschaft Relativzeit (0x328): Ausfall | 0 |
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

<a id="table-dtcbereiche"></a>
### DTCBEREICHE

Dimensions: 20 rows × 4 columns

| DTC-TYP | MINIMALWERT | MAXIMALWERT | BESCHREIBUNG |
| --- | --- | --- | --- |
| AllgemeinerDTC | 020000 | 02FFFF | Die zulässigen Bereiche sind für jedes Steuergerät festgelegt. Es können mehrere gültige Bereiche (Kacheln) definiert werden. |
| SystembusDTC | CAC415 | CAC41E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC40B | CAC414 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC47D | CAC486 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC469 | CAC472 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC501 | CAC50A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC41F | CAC43E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930000 | 930011 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC401 | CAC40A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930030 | 930055 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC50B | CAC514 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC43F | CAC449 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC45F | CAC468 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC473 | CAC47C | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | CAC487 | CAC48F | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SubbusDTC | CACC00 | CAD3FF | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SignalDTC | CAD400 | CB03FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | CAD400 | CB03FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | CACBFF | CACBFF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| KomponentenDTC | 21F000 | 21F1FF | Die zulässigen Bereiche sind für jedes Steuergerät festgelegt. Es können mehrere gültige Bereiche (Kacheln) definiert werden. |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x65E0 | Außentemperatur | Grad C | high | signed long | - | 1 | 2 | -40 |
| 0x65E1 | U-Batt, Kl. 30F | V | high | signed long | - | 1 | 1000 | 0 |
| 0x65E2 | Gesamtstrom HVS | A | high | signed long | - | 1 | 10 | -819.2 |
| 0x65E3 | U-Batt, HVS | V | high | signed long | - | 1 | 10 | 0 |
| 0x65E4 | U-Zwischenkreis | V | high | signed long | - | 4 | 1 | 0 |
| 0x65E5 | Batterietemperatur | Grad C | high | signed long | - | 1 | 1 | -50 |
| 0x65E6 | SOC (State of Charge) | Prozent | high | signed long | - | 1 | 10 | 0 |
| 0x65E7 | Systemstatus | 0-n | high | 0xFFFFFFFF | TAB_SYSTEM_STATUS | - | - | - |
| 0x65E8 | Schuetzstatus | 0-n | high | 0xFFFFFFFF | TAB_SCHUETZ_STATUS | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 51 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x070000 | DM_ZEITBOTSCHAFTTIMEOUT | 0 |
| 0x070003 | NVM_E_WRITE_FAILED | 0 |
| 0x070004 | NVM_E_READ_FAILED | 0 |
| 0x070005 | NVM_E_CONTROL_FAILED | 0 |
| 0x070006 | NVM_E_ERASE_FAILED | 0 |
| 0x070007 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x070008 | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x070009 | NVM_E_READ_ALL_FAILED | 0 |
| 0x07000A | VSM_EVENT_VEHICLESTATE | 0 |
| 0x070100 | Volle Queue des DARH von ROE | 0 |
| 0x070101 | Gelöschte Queue des DARH von ROE | 0 |
| 0x21F012 | SME: unerwarteter Powerdown festgestellt | 0 |
| 0x21F02C | SME: Temperatur zu hoch | 0 |
| 0x21F031 | HVS: Isolationsüberwachung -  Fehler des Iso Messkontakts | 0 |
| 0x21F032 | HVS: Isolationüberwachung -  Isolationsfehler im Gesamtsystem (geschlossene Schütze)  ungültig | 0 |
| 0x21F033 | HVS: Isolationsüberwachung -  Offsetspannung ungültig | 0 |
| 0x21F034 | HVS: Isolationsüberwachung -  HV Batteriespannung (Referenz) außerhalb Bereich | 0 |
| 0x21F036 | HVS: U/i-Sensor -  Sensortemperatur außerhalb Bereich | 0 |
| 0x21F03B | HVS: U/i-Sensor -  Fehler Messung Überstromerkennung | 0 |
| 0x21F03E | U/i-Sensor: Fehler in der Referenzspannung der Hardwarereissleine erkannt | 0 |
| 0x21F03F | U/i-Sensor: Fehler in den Kalibrierdaten der Hardwarereissleine erkannt | 0 |
| 0x21F040 | U/i-Sensor: Fehler im Programmspeicher der Hardwarereissleine erkannt | 0 |
| 0x21F051 | HVS: U/i-Sensor -  unerwarteter Reset | 0 |
| 0x21F053 | HVS: U/i-Sensor -  Diagnose Timeout | 0 |
| 0x21F06F | HVS: CSC CAN: unvollstaendige CAN Daten Modultemperaturen | 0 |
| 0x21F070 | HVS: CSC CAN: unvollstaendige CAN Daten Einzelzellspannungen | 0 |
| 0x21F071 | HVS: CSC CAN: unvollstaendige CAN Daten Modulspannungen | 0 |
| 0x21F072 | HVS: CSC Funktion: Opmode-Befehl nicht akzeptiert | 0 |
| 0x21F073 | HVS: U/i-Sensor -  falscher Messmodus eingestellt | 0 |
| 0x21F109 | HVS: Hauptschalter: Warnung Schützalterung | 0 |
| 0x21F116 | Stromüberwachung: Gewährleistungsüberschreitung Strombegrenzung Laden | 0 |
| 0x21F125 | Zellspannung -  Toleranzüberschreitung obere Spannungsbegrenzung (Gewährleistung) | 0 |
| 0x21F126 | Zellspannung -  Toleranzüberschreitung untere Spannungsbegrenzung (Gewährleistung) | 0 |
| 0x21F13C | Isolationsüberwachung -  Isolationsmessung im Gesamtsystem unplausibel (geschlossene Schütze) | 0 |
| 0x21F13D | HVS: Isolationsüberwachung -  interne Isolationsmessung unplausibel | 0 |
| 0x21F13F | Vorladung -  falsche Stromrichtung | 1 |
| 0x21F143 | Klemme 15: unplausibel / Fehler | 1 |
| 0x21F145 | Plausibilität Stromwert -  Prüfung nicht möglich | 0 |
| 0x21F179 | HVS: Batteriealterung: SOH zu hoch | 0 |
| 0x21F17A | HVS: Batteriealterung: SOH niedrig (Warnschwelle) | 0 |
| 0x21F182 | Ladungszustand:SoC unplausibel | 0 |
| 0x21F184 | HVS: Zellüberwachung: Zellspannungen stark unterschiedlich | 0 |
| 0x21F185 | HVS: Zellüberwachung: Zellwiderstände stark unterschiedlich | 0 |
| 0x21F188 | Drosselung -  Herabsetzung der Entladungsstromgrenze wegen Temperatur / SOC-Grenze | 0 |
| 0x21F189 | Drosselung -  Herabsetzung der Ladungsstromgrenze wegen Temperatur / SOC-Grenze | 0 |
| 0x21F194 | HVS: Aufstartdauer zu lang | 0 |
| 0x21F1F0 | FLS_E_ERASE_FAILED | 0 |
| 0x21F1F1 | FLS_E_WRITE_FAILED | 0 |
| 0x21F1F2 | FLS_E_READ_FAILED | 0 |
| 0x21F1F3 | FLS_E_COMPARE_FAILED | 0 |
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

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x65E0 | Außentemperatur | Grad C | high | signed long | - | 1 | 2 | -40 |
| 0x65E1 | U-Batt, Kl. 30F | V | high | signed long | - | 1 | 1000 | 0 |
| 0x65E2 | Gesamtstrom HVS | A | high | signed long | - | 1 | 10 | -819.2 |
| 0x65E3 | U-Batt, HVS | V | high | signed long | - | 1 | 10 | 0 |
| 0x65E4 | U-Zwischenkreis | V | high | signed long | - | 4 | 1 | 0 |
| 0x65E5 | Batterietemperatur | Grad C | high | signed long | - | 1 | 1 | -50 |
| 0x65E6 | SOC (State of Charge) | Prozent | high | signed long | - | 1 | 10 | 0 |
| 0x65E7 | Systemstatus | 0-n | high | 0xFFFFFFFF | TAB_SYSTEM_STATUS | - | - | - |
| 0x65E8 | Schuetzstatus | 0-n | high | 0xFFFFFFFF | TAB_SCHUETZ_STATUS | - | - | - |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 94 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ISOLATION | 0xAD61 | - | Ergebnis Isolationstest | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAD61 |
| KAPAZITAET_BESTIMMUNG | 0xAD66 | - | Bestimmung der Kapazität | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAD66 |
| SCHUETZ_SCHALTER | 0xDD60 | STAT_SCHUETZ_SCHALTER | Status der Schützschalter: geschlossen oder offen. Ergebnisse siehe Tabelle TAB_SCHUETZ_SCHALTER | 0-n | - | high | unsigned char | TAB_SCHUETZ_SCHALTER | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SCHUETZ_FREIGABE | 0xDD61 | - | Schreibt bzw. liest das Bit zur Freigabe oder Sperrung der Schützschalter. Job ist Klemmensicher | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDD61 | RES_0xDD61 |
| SCHUETZSCHALTUNGEN_ANZAHL | 0xDD63 | - | Anzahl der Schaltungen der Schützschalter (stromlos und unter Last)  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD63 |
| HVIL | 0xDD64 | STAT_GUELTIG | Ergebnis HVIL-Prüfung | 0-n | - | high | unsigned char | TAB_STATUS_HVIL | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| HV_SPANNUNG | 0xDD66 | STAT_HV_SPANNUNG_WERT | Zwischenkreisspannung vor den Schützen, unabhängig vom Schützzustand | V | - | high | unsigned int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| ANZAHL_KUEHLANFORDERUNG_DRINGEND | 0xDD67 | STAT_ANZAHL_KUEHLANFORDERUNG_DRINGEND_WERT | Anzahl der höheren T-Zustände in aufeinanderfolgenden Klemmenzyklen. | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| HV_SPANNUNG_BERECHNET | 0xDD68 | STAT_HV_SPANNUNG_BERECHNET_WERT | Batteriespannung hinter den Schützen, unabhängig vom Schützzustand | V | - | high | unsigned int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| HV_STROM | 0xDD69 | STAT_HV_STROM_WERT | HV-Strom in A | A | - | high | long | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| ISOLATIONSWIDERSTAND | 0xDD6A | - | Auslesen des aktuell anliegenden Isolationswiderstands | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD6A |
| TEMP_SENSOREN | 0xDD6B | - | Temperatur Zellen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD6B |
| KUEHLKREISLAUF_TEMP | 0xDD6C | STAT_TEMP_KUEHLKREISLAUF_WERT | Temperatur des Kühlmediums in °C | °C | - | high | int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| SCHUETZE_MAX_SOC_SICHERHEITABFRAGE | 0xDD6E | - | Hauptschütze schalten bei SOC &gt; 90 %, Passwort gesichert! | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDD6E | - |
| KUEHLKREISLAUF_VENTIL | 0xDD6F | - | Status / Steuern Kühlmittel-Ventil: Geschlossen oder offen / schliessen oder öffnen  | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD6F | RES_0xDD6F |
| AUFSTART_VERHINDERER | 0xDD72 | STAT_AUFSTART_VERHINDERER | Grund für nicht Aufstarten des HV-Systems | 0-n | - | high | unsigned char | TAB_AUFSTART_VERHINDERER | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| CUMULATIVE_LADUNG | 0xDD73 | STAT_LADUNG_AMP_STUNDEN_WERT | Die kumulierte Ladung für Ladevorgänge in Ah | Ah | - | low | unsigned long | - | 1.0 | 3600.0 | 0.0 | - | 22 | - | - |
| CUMULATIVE_ENTLADUNG | 0xDD74 | STAT_ENTLADUNG_AMP_STUNDEN_WERT | Die kumulierte Ladung für Entladevorgänge in Ah | Ah | - | low | unsigned long | - | 1.0 | 3600.0 | 0.0 | - | 22 | - | - |
| STATUS_KL30C_SPANNUNG | 0xDD76 | STAT_KL30C_SPANNUNG_WERT | Spannung Klemme 30C in V | V | - | high | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| SOC_REKALIBRIERUNG | 0xDD78 | - | Triggern der SOC Rekalibierungsprozedur (0 = nicht aktiv; 1 = aktiv) | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDD78 | - |
| SCHUETZE_MIN_SOC_SICHERHEITABFRAGE | 0xDD79 | - | Hauptschütze schalten bei min SOC (&lt; 5% SOC) Achtung!Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein. Nicht möglich während der Fahrt. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDD79 | - |
| REFERENZ_KAPAZITAET | 0xDD7B | - | Auslesen und Justieren Kapazität Batterie | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD7B | RES_0xDD7B |
| GW_INFO | 0xDD7C | - | Gewährleistungsdaten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7C |
| STROMGRENZEN | 0xDD7D | - | Stromgrenzen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7D |
| SPANNUNGSGRENZEN | 0xDD7E | - | Spannungsgrenzen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7E |
| HVB_HISTORIE_ZYKLEN | 0xDD8E | - | Ausgabe Anzahl der Lade- / Entladehübe (Ah-Durchsatz) in der jeweiligen Klasse und  Ausgabe der Strombelastung (Stromhistogram) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD8E |
| ZEIT_TEMP_HISTOGRAMM | 0xDD90 | - | Zeit in verschiedenen Temperaturklasse und Hauptschalterzuständen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD90 |
| ZEIT_SOC_KLASSE | 0xDD91 | - | Zeit seit Einbau in SOC-Klassen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD91 |
| HV_BATT_HIST_SOC_T1 | 0xDD94 | - | Dauer bei Temperatur &lt;-20°C und bei unterschiedlichen Werten von Strom und SOC | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD94 |
| HV_BATT_HIST_SOC_T2 | 0xDD95 | - | Dauer bei Temperatur -20°C &lt; T &lt; -13°C und bei unterschiedlichen Werten von Strom und SoC | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD95 |
| HV_BATT_HIST_SOC_T3 | 0xDD96 | - | Dauer bei Temperatur -13°C &lt; T &lt; -7°C und bei unterschiedlichen Werten von Strom und SoC. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD96 |
| HV_BATT_HIST_SOC_T4 | 0xDD97 | - | Dauer bei Temperatur -7°C &lt; T &lt; 0°C und bei unterschiedlichen Werten von Strom und SoC  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD97 |
| HV_BATT_HIST_SOC_T5 | 0xDD98 | - | Dauer bei Temperatur 0°C &lt; T &lt; 8°C und bei unterschiedlichen Werten von Strom und SoC.  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD98 |
| HV_BATT_HIST_SOC_T6 | 0xDD99 | - | Dauer bei Temperatur 8°C &lt; T &lt; 25°C und bei unterschiedlichen Werten von Strom und SoC | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD99 |
| HV_BATT_HIST_SOC_T7 | 0xDD9A | - | Dauer bei Temperatur 25°C &lt; T und bei unterschiedlichen Werten von Strom und SoC  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD9A |
| ZELLSPANNUNG_MODUL_4 | 0xDDAE | - | aktuell gemessene Zellspannungen Modul 4  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDAE |
| ZELLSPANNUNG_MODUL_5 | 0xDDAF | - | aktuell gemessene Zellspannungen Modul 5  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDAF |
| ZELLSPANNUNG_MODUL_6 | 0xDDB0 | - | aktuell gemessene Zellspannungen Modul 6  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDB0 |
| ZELLSPANNUNG_MODUL_7 | 0xDDB1 | - | aktuell gemessene Zellspannungen Modul 7 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDB1 |
| ZELLSPANNUNG_MODUL_8 | 0xDDB2 | - | aktuell gemessene Zellspannungen Modul 8  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDB2 |
| LADUNGSMENGE_HV_BOOST_RECUP | 0xDDB3 | - | Status entommene bzw. zugeführte Ladungsmenge | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDB3 |
| HV_SPANNUNG_BATTERIE | 0xDDB4 | STAT_HV_SPANNUNG_BATT_WERT | Batteriespannung hinter den Schützen, unabhängig vom Schützzustand | V | - | high | unsigned int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| ALTERUNG_INNENWIDERSTAND | 0xDDB6 | STAT_ALTERUNG_INNENWIDERSTAND_WERT | Alterung des Innenwiderstands in Prozent: Innenwiderstand des Speichers im Neuzustand auf den aktuellen Wert des Innenwiderstands bezogen  (R_neu /R_akt) *100   (100% = Neuzustand, sinkt mit Alterung) | % | - | high | unsigned int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| ALTERUNG_KAPAZITAET | 0xDDB7 | STAT_ALTERUNG_KAPAZITAET_WERT | Restkapazität des Speichers, prozentualer Wert: ( C_akt/C_nenn(neu) ) * 100, 0 = Lebensdauerende erreicht, 100 = Neuzustand | % | - | high | unsigned int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| ZELLSPANNUNG_MODUL_1 | 0xDDB9 | - | aktuell gemessene Zellspannungen in V Modul 1  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDB9 |
| ZELLSPANNUNG_MODUL_2 | 0xDDBA | - | aktuell gemessene Zellspannungen Modul 2  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDBA |
| ZELLSPANNUNG_MODUL_3 | 0xDDBB | - | aktuell gemessene Zellspannungen in V Modul 3  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDBB |
| ANZEIGE_SOC | 0xDDBC | - | aktueller Anzeige Soc | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDBC |
| SERVICE_DISCONNECT | 0xDDBD | STAT_SERVICE_DISCONNECT | Status Service Disconnect (0 = offen, 1 = geschlossen) | 0/1 | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| VORLADUNG | 0xDDBE | - | Info über Zeit, Strom und Temperaturen bei Vorladung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDBE |
| ZELLSPANNUNGEN_MIN_MAX | 0xDDBF | - | minimale und maximale Einzelzellspannungen werden ausgegeben | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDBF |
| TEMPERATUREN | 0xDDC0 | - | Ausgabe minimale Messtemperatur, maximale Messtemperatur, durchschnittliche Messtemperatur, maximale Zellkerntemperatur | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC0 |
| CSC_IDS | 0xDDC1 | - | Hardware IDs der einzelnen CSCs (Cell Supervisory Circuit) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDDC1 | RES_0xDDC1 |
| ALTERUNG_PARAMETER | 0xDDC2 | - | Korrekturfaktor des seriellen ohmischen Wiederstandes bei Entladung. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC2 |
| SOC | 0xDDC4 | - | Auslesen SOC Wert (in %) und Plausibilität oder Vorgabe des SOC Werts (0-100%) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDDC4 | RES_0xDDC4 |
| MODULSPANNUNG_UNPLAUSIBEL | 0xDDC5 | - | liefert die Modulnummer der CSCs zurück, in der ein unplausibler Spannungswert detektiert wurde (verknüpft mit DTC). Rückgabewert ist ein Komponentenvektor (Länge 8) mit der Belegung 0 = kein Fehler, 1 = Fehler erkannt. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC5 |
| HISTO_SYM_DAUER | 0xDDC6 | - | Auslesen der Anzahl von Symmetriervorgängen in den jeweiligen Zeitklassen (Soll-Zeit in der die Symmetrierwiderstände aktiv geschaltet werden sollen). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC6 |
| HISTO_SYM_ZELLANZAHL | 0xDDC7 | - | Auslesen der Anzahl der Einschlafvorgänge in denen die jeweiligen Zellzahl zur Symmetrierung angewiesen wurden. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC7 |
| SYM_DELTASOC | 0xDDC8 | - | Maximale SoC-Differenz in % über den gesamten HVS. Ringspeicher der letzten 5 Fahrten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC8 |
| MAX_SYM_DAUER | 0xDDC9 | - | Maximale Symmetriedauer des letzten Symmetriervorgangs | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDC9 |
| SERIENNUMMER_ECU | 0xDDCA | STAT_SERIENNUMMER_ECU_TEXT | Seriennummer des SME Steuergeräts | TEXT | - | high | string[10] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SOC_GRENZEN | 0xDDCB | - | Auslesen und Ändern der SOC Grenzen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDCB |
| SCHUETZ_RESTZAEHLER | 0xDDCC | - | Auslesen oder Rücksetzen (0 = kein Reset; 1 = Reset) des Zählers für die noch möglichen Schaltungen der Schütze K1, K2, K3 | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDDCC | RES_0xDDCC |
| CC_MELDUNG | 0xDDCD | - | Aktivieren / Deaktivierung des Sendens von CC-Meldung (0 = Senden nicht aktiv; 1 = Senden aktiv) | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDDCD | - |
| DIFFERENZ_SPANNUNGEN | 0xDDCF | - | Differenzspannung: Gesamtspannung Batterie - Summenzellspannung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDCF |
| ALTERUNG_KAPAZITAET_DEGRADATION | 0xDDE8 | - | Anzahl der alterungsbedingten Spannungsdegradationen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDE8 |
| ALTERUNG_KAPAZITAET_HISTOGRAMM_SOC_HUB | 0xDDE9 | - | Histogramm mit Häufigkeit einzelner aufgetretener SoC-Hübe im Betriebszeitraum | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDDE9 |
| BETRIEBSSTUNDEN | 0xDF60 | - | Zeit für geschlossene Hauptschalter und gesamte Batterielebensdauer (geschlossene + geöffnete Zeit der Hauptschalter) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF60 |
| SOC_GRENZE_OBEN | 0xDF61 | - | Öffnen/Rücksetzen der oberen SOC Grenze | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDF61 | - |
| COOL_DOWN | 0xDF62 | STAT_ANZAHL_KUEHLVORGAENGE_WERT | Anzahl der CoolDown Szenarios (Abfahrt mit heißem HV-Speicher) | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| KLEMMENZYKLEN | 0xDF63 | STAT_ANZAHL_KLEMMENZYKLEN_WERT | Anzahl der Klemmenzyklen | - | - | high | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| KUEHLDAUER | 0xDF64 | - | Kühldauer der HV-Batterie | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF64 |
| TEMP_SPREIZUNG_SYSTEM | 0xDF65 | - | Zeit in verschiedenen dT-Klassen bei aktiver Kühlung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF65 |
| TEMP_KUEHLMITTEL | 0xDF66 | - | Zeit in verschiedenen Temperaturklassen des Kühlmittels  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF66 |
| LADUNG_KUEHLUNG | 0xDF67 | - | Ladungsmengen bei eingeschalteter Kühlung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF67 |
| VIN | 0xF190 | STAT_FGNR17_WERT | 17-Stellige Fahrgestellnummer 00000000000000000 wenn keine Fahrgestellnummer vorhanden (jungfräuliches Steuergerät). Hinweis: Der Resultwert 00000000000000000 wird zurückgeliefert, falls das CAS 0xFF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF im Antworttelegramm liefert. | - | - | - | string[17] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| ALTERUNG_INNENWIDERSTAND_TS | 0x6334 | STAT_ALTERUNG_INNENWIDERSTAND_WERT | Alterung des Innenwiderstands in Prozent: Innenwiderstand des Speichers im Neuzustand auf den aktuellen Wert des Innenwiderstands bezogen  (R_neu /R_akt) *100   (100% = Neuzustand, sinkt mit Alterung) | % | - | high | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| ALTERUNG_KAPAZITAET_TS | 0x6335 | STAT_ALTERUNG_KAPAZITAET_WERT | Restkapazität des Speichers, prozentualer Wert: ( C_akt/C_nenn(neu) ) * 100, 0 = Lebensdauerende erreicht, 100 = Neuzustand | % | - | high | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _SOC_GRENZEN | 0x6500 | - | State of Charge Grenzwerte | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6500 | - |
| _ISOLATION | 0x6501 | - | Isolationsüberwachung | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6501 | - |
| _UEBERLAST_SCHWELLE | 0x6502 | - | Lade- und Entladestromgrenzen | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6502 | - |
| _KURZSCHLUSS_STROMGRENZE | 0x6503 | - | Kurzschluss Stromgrenze | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6503 | - |
| _LADE_SPANNUNGSGRENZE | 0x6504 | - | Lade Spannungsgrenze | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6504 | - |
| _SCHUETZ_K1 | 0x6506 | - | K1 Schütz | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6506 | - |
| _SCHUETZ_K2 | 0x6507 | - | K2 Schütz | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6507 | - |
| _SCHUETZ_K3 | 0x6508 | - | K3 Schütz | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6508 | - |
| _SERIENNUMMER | 0x6509 | - | Speicherseriennummer | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6509 | - |
| _ENTLADE_SPANNUNGSGRENZE | 0x650B | - | Entlade-Spannungsgrenze | - | - | - | - | - | - | - | - | - | 2E | ARG_0x650B | - |
| _SYM_MODUS | 0x6511 | - | Symmetriemodus der SEM | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6511 | - |
| _MESSBOTSCHAFTEN | 0x6512 | - | Messbotschaften ein/ausschalten | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6512 | - |
| _CSC_INDIZIERUNG | 0x6515 | - | CSCs werden mit den als Argument übergebenen Positionsindezes neu indiziert | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6515 | - |
| _ST_SYM_MODUS | 0x6516 | STAT_SYM_MODUS | Status der Symmetrierung | 0-n | - | high | unsigned char | TAB_SYM_MODUS | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _CSC_STANDBY | 0x6519 | - | CSCs in Standby-Mode setzen | - | - | - | - | - | - | - | - | - | 2E | ARG_0x6519 | - |
| _ANFORDERUNG_SCHUETZE_SCHLIESSEN | 0x651B | - | Schütze schließen | - | - | - | - | - | - | - | - | - | 2E | ARG_0x651B | - |

<a id="table-tab-hvil-generator"></a>
### TAB_HVIL_GENERATOR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ausschalten |
| 1 | einschalten |
| 255 | unbekannter Wert |

<a id="table-res-0xdd64"></a>
### RES_0XDD64

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GUELTIG | 0-n | - | unsigned int | - | TAB_STATUS_HVIL | - | - | - | Ergebnis HVIL-Prüfung |

<a id="table-arg-0xdd64"></a>
### ARG_0XDD64

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ANSTEUERUNG | 0-n | high | unsigned char | - | TAB_HVIL_GENERATOR_GEN2 | - | - | - | - | - | Stören/Abschalten des Interlockgenerators im BMS |

<a id="table-tab-hvil-generator-gen2"></a>
### TAB_HVIL_GENERATOR_GEN2

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUS |
| 1 | EIN |
| 2 | geregelt / Normalbetrieb |

<a id="table-tab-system-status"></a>
### TAB_SYSTEM_STATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | nicht definiert |
| 0x00000001 | nicht definiert |
| 0x00000002 | nicht definiert |
| 0x00000003 | nicht definiert |
| 0x000000FF | in Klärung |
| 0xFFFFFFFF | nicht definiert |

<a id="table-tab-schuetz-status"></a>
### TAB_SCHUETZ_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Trennschalter offen |
| 0x00000001 | Trennschalter auf Voraufladung |
| 0x00000002 | Trennschalter geschlossen |
| 0x00000003 | Signal ungültig |
| 0xFFFFFFFF | nicht definiert |

<a id="table-rdtci-lev-dop"></a>
### RDTCI_LEV_DOP

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 2 | reportDTCByStatusMask |
| 4 | reportDTCsnapshotRecordByDTCnumber |
| 6 | reportDTCextendedDataRecordByDTCnumber |
| 7 | reportNumberOfDTCbySeverityMaskRecord |
| 8 | reportDTCbySeverityMaskRecord |
| 9 | reportSeverityInformationOfDTC |
| 10 | reportSupportedDTC |
| 18 | reportNumberOfEmissionsRelatedOBDDTCByStatusMask |
| 19 | reportEmissionsRelatedOBDDTCByStatusMask |

<a id="table-arg-0xdd61"></a>
### ARG_0XDD61

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FREIGABE | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0 = nicht freigegeben; 1 = freigegeben |

<a id="table-arg-0xdd6e"></a>
### ARG_0XDD6E

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORD | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Sicherheitspasswort zur Schuetzschaltung |
| ANSTEUERUNG | 0-n | high | unsigned char | - | TAB_ANST_SCHUETZ | 1.0 | 1.0 | 0.0 | - | - | Achtung!Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein. Nicht möglich während der Fahrt. Auch bei hoher Ladung (90% SOC) noch möglich. |

<a id="table-arg-0xdd6f"></a>
### ARG_0XDD6F

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KUEHLKREISLAUF_VENTIL | 0-n | high | unsigned char | - | TAB_KUEHLERKREISLAUF_VENTIL | 1.0 | 1.0 | 0.0 | - | - | Steuern des Kühlmittel-Ventils: Geschlossen oder offen |

<a id="table-arg-0xdd78"></a>
### ARG_0XDD78

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTIVIERUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktivieren der SOC Rekalbieriung (0 = nicht aktiv; 1 = aktiv) |

<a id="table-arg-0xdd79"></a>
### ARG_0XDD79

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORD | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Sicherheitspasswort zur Schuetzschaltung |
| ANSTEUERUNG | 0-n | high | unsigned char | - | TAB_ANST_SCHUETZ | 1.0 | 1.0 | 0.0 | - | - | Achtung!Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein. Nicht möglich während der Fahrt. |

<a id="table-arg-0xdd7b"></a>
### ARG_0XDD7B

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KAPAZITAET_JUSTIERUNG | Ah | - | unsigned long | - | - | 3600.0 | 1.0 | 0.0 | - | - | Justierung Kapazität Batterie |

<a id="table-arg-0xddc1"></a>
### ARG_0XDDC1

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CSC_IDS | - | high | string[64] | - | - | 1.0 | 1.0 | 0.0 | - | - | String mit verketteten HW-IDs aller CSC (jede ID ist 8-stellig) |

<a id="table-arg-0xddc4"></a>
### ARG_0XDDC4

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORD | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Sicherheitspasswort für Veränderung des SOC Werts |
| SOC_VORGABE | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | SOC-Wert vorgeben ( 0 - 100%) |

<a id="table-arg-0xddcc"></a>
### ARG_0XDDCC

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0= kein Reset; 1= Reset durchführen |

<a id="table-arg-0xddcd"></a>
### ARG_0XDDCD

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZUSTAND_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktivieren / Deaktivierung des Sendens von CC-Meldung (0 = Senden nicht aktiv; 1 = Senden aktiv) |

<a id="table-arg-0xdf61"></a>
### ARG_0XDF61

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort für Verändern der SOC Grenzen |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0 = Grenze zurücksetzen; 1 = Grenze öffnen |

<a id="table-res-0xad61"></a>
### RES_0XAD61

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MESSUNG_ERFOLGREICH | - | - | + | 0-n | high | unsigned char | - | TAB_ISOLATION_ERFOLGREICH | 1.0 | 1.0 | 0.0 | aktueller Zustand Isolationsmessung |
| STAT_MESSUNG_ISOLATIONSFEHLER | - | - | + | 0-n | high | unsigned char | - | TAB_ISOLATION_ISOLATIONSFEHLER | 1.0 | 1.0 | 0.0 | aktueller Zustand des Isolationsfehlers |

<a id="table-res-0xad66"></a>
### RES_0XAD66

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KAPAZITAET_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Kapazitätsschätzwert in % (Wertebereich 0-100%) bezogen auf Nennkapazität |
| STAT_AKTUELLER_ZUSTAND_NR | - | - | + | 0-n | high | unsigned char | - | TAB_SME_ERMITTLUNG | - | - | - | Rückgabe Ermittlung läuft, erfolgreich oder mit Fehler beendet |

<a id="table-res-0xdd61"></a>
### RES_0XDD61

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHUETZ_FREIGABE | 0-n | high | unsigned char | - | TAB_SCHUETZ_FREIGABE | 1.0 | 1.0 | 0.0 | Liest das Bit zur Freigabe oder Sperrung der Schützschalter   |

<a id="table-res-0xdd63"></a>
### RES_0XDD63

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_SCHALTUNGEN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schaltungen der Schützschalter (ohne Last)  |
| STAT_ANZAHL_SCHALTUNGEN_LAST_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schaltungen der Schützschalter unter Last  |

<a id="table-res-0xdd6a"></a>
### RES_0XDD6A

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ISOWIDERSTAND_GESAMT_WERT | kOhm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Isolationswiderstands vom Gesamtsystem (geschlossene Schütze) |
| STAT_ISOWIDERSTAND_GESAMT_PLAUS | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gesamtsystem: 0 = Isolationswiderstand nicht plausibel, 1 = Isolationswiderstand plausibel |
| STAT_ISOWIDERSTAND_INTERN_WERT | kOhm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des internen Isolationswiderstands (offene Schütze) |
| STAT_ISOWIDERSTAND_INTERN_PLAUS | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intern:  0 = Isolationswiderstand nicht plausibel, 1 = Isolationswiderstand plausibel |

<a id="table-res-0xdd6b"></a>
### RES_0XDD6B

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_SENSOR_1_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 1 in °C |
| STAT_TEMP_SENSOR_2_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 2 in °C |
| STAT_TEMP_SENSOR_3_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 3 in °C |
| STAT_TEMP_SENSOR_4_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 4 in °C |
| STAT_TEMP_SENSOR_5_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 5 in °C |
| STAT_TEMP_SENSOR_6_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 6 in °C |
| STAT_TEMP_SENSOR_7_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 7 in °C |
| STAT_TEMP_SENSOR_8_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | mittlere Temperatur Modul 8 in °C |

<a id="table-res-0xdd6f"></a>
### RES_0XDD6F

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KUEHLKREISLAUF_VENTIL | 0-n | high | unsigned char | - | TAB_KUEHLKREISLAUF_VENTIL_RUECKGABE | 1.0 | 1.0 | 0.0 | Status Kühlmittel-Ventil: Geschlossen oder offen |

<a id="table-res-0xdd7b"></a>
### RES_0XDD7B

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KAPAZITAET_WERT | Ah | high | unsigned long | - | - | 1.0 | 36000.0 | 0.0 | Auslesen der Justierung Kapazität Batterie |

<a id="table-res-0xdd7c"></a>
### RES_0XDD7C

Dimensions: 26 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZEIT_POWER_DCHG_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -0.1 bis -100 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -100 bis -200 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -200 bis -300 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -300 bis -400 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -400 bis -500 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse -500 bis -600 W für Entladevorgänge |
| STAT_ZEIT_POWER_DCHG_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse &gt; 600 W für Entladevorgänge |
| STAT_ZEIT_POWER_CHG_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 0.1 bis 100 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 100 bis 200 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 200 bis 300 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 300 bis 400 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 400 bis 500 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse 500 bis 600 W für Ladevorgänge |
| STAT_ZEIT_POWER_CHG_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Leistungsklasse &gt; 600 W für Ladevorgänge |
| STAT_UCELLMAX_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | GW-Grenzverletzung der max. Einzelzellspannung eingetreten (1 = ja / 0 = nein). |
| STAT_UCELLMIN_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | GW-Grenzverletzung der min. Einzelzellspannung eingetreten (1 = ja / 0 = nein). |
| STAT_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand |
| STAT_IMAX_DCHG_WERT | A | high | unsigned long | - | - | 1.0 | 100.0 | 0.0 | maximal gemessener Entladestrom über Lebenszeit |
| STAT_IMAX_CHG_WERT | A | high | unsigned long | - | - | 1.0 | 100.0 | 0.0 | maximal gemessener Ladestrom über Lebenszeit |
| STAT_IMAX_LAD_ERROR_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | GW-Grenzverletzung des maximal erlaubten Ladestroms überschritten (1 = ja / 0 = nein) |
| STAT_TMAX_ERROR_OP_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | maximal erlaubte Temperatur während Betrieb überschritten (1 = ja, 0 = nein) |
| STAT_TMAX_ERROR_NO_OP_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | maximal erlaubte Temperatur ohne Betrieb überschritten (1 = ja, 0 = nein) |
| STAT_TMIN_ERROR_OP_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | minimal erlaubte Temperatur während Betrieb unterschritten (1 = ja, 0 = nein) |
| STAT_TMIN_ERROR_NO_OP_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | minimal erlaubte Temperatur ohne Betrieb unterschritten (1 = ja, 0 = nein) |
| STAT_CUMULATIVE_ENERGIE_LADUNG_WERT | Ws | high | unsigned long | - | - | 36.0 | 1.0 | 0.0 | Wert der kumulierten Energie für Ladevorgänge |
| STAT_CUMULATIVE_ENERGIE_ENTLADUNG_WERT | Ws | high | unsigned long | - | - | 36.0 | 1.0 | 0.0 | Wert der kumulierten Energie für Entladevorgänge |

<a id="table-res-0xdd7d"></a>
### RES_0XDD7D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADESTROMGRENZE_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | maximal erlaubter Ladestrom |
| STAT_ENTLADESTROMGRENZE_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | maximal erlaubter Entladesstrom |

<a id="table-res-0xdd7e"></a>
### RES_0XDD7E

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADESPANNUNGSGRENZE_WERT | V | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | maximal erlaubte Ladespannung |
| STAT_ENTLADESPANNUNGSGRENZE_WERT | V | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | maximal erlaubte Entladespannung |

<a id="table-res-0xdd8e"></a>
### RES_0XDD8E

Dimensions: 28 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SUM_OF_SOC_CHARGE_1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 0% &lt; x &lt;= 1% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 1% &lt; x &lt;= 3% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 3% &lt; x &lt;= 5% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 5% &lt; x &lt;= 10% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 10% &lt; x &lt;= 20% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 20% &lt; x &lt;= 30% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 30% &lt; x &lt;= 40% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 40% &lt; x &lt;= 60% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_9_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 60% &lt; x &lt;= 80% (Laden) |
| STAT_SUM_OF_SOC_CHARGE_10_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse            x &lt;= 80% (Laden) |
| STAT_SUM_OF_SOC_DISCHARGE_1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 0% &lt; x &lt;= 1% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 1% &lt; x &lt;= 3% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 3% &lt; x &lt;= 5% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 5% &lt; x &lt;= 10% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 10% &lt; x &lt;= 20% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 20% &lt; x &lt;= 30% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 30% &lt; x &lt;= 40% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 40% &lt; x &lt;= 60% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_9_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse 60% &lt; x &lt;= 80% (Entladen) |
| STAT_SUM_OF_SOC_DISCHARGE_10_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl SOC-Hübe (Ah-Durchsatz) der Klasse            x &lt;= 80% (Entladen) |
| STAT_I_HISTO_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in x&lt;=-160 A |
| STAT_I_HISTO_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in -160 A &lt;x&lt;=-80 A |
| STAT_I_HISTO_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in -80 A &lt;x&lt;= -5 A |
| STAT_I_HISTO_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in -5 A &lt;x&lt;=  0 A |
| STAT_I_HISTO_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in  0 A &lt;x&lt;= 5 A |
| STAT_I_HISTO_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in 5 A &lt;x&lt;= 80 A |
| STAT_I_HISTO_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in 80 A &lt;x&lt;= 160 A |
| STAT_I_HISTO_8_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Dauer Stromklasse in 160 A &lt;x |

<a id="table-res-0xdd90"></a>
### RES_0XDD90

Dimensions: 28 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZEIT_TEMP_TOTAL_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse &lt; -25°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse -25°C bis -10°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse -10°C bis 0°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 0°C bis 10°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 10°C bis 20°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 20°C bis 25°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 25°C bis 30°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_8_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 30°C bis 35°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_9_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 35°C bis 40°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_10_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 40°C bis 45°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_11_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 45°C bis 50°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_12_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 50°C bis 55°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_13_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 55°C bis 60°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_14_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse &gt; 60°C bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse &lt; -25°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse -25°C bis -10°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse -10°C bis 0°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 0°C bis 10°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 10°C bis 20°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 20°C bis 30°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 30°C bis 35°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_8_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 35°C bis 40°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_9_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 40°C bis 45°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_10_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 45°C bis 50°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_11_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 45°C till 50°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_12_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 50°C till 55°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_13_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse 55°C till 60°C bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_14_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Temperaturklasse &gt; 60°C bei geöffneten Hauptschaltern |

<a id="table-res-0xdd91"></a>
### RES_0XDD91

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZEIT_SOC_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 1 (x &lt; 15%) |
| STAT_ZEIT_SOC_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 2 (15% &lt;= x &lt; 25%) |
| STAT_ZEIT_SOC_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 3 (25% &lt;= x &lt; 30%) |
| STAT_ZEIT_SOC_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 4 (30% &lt;= x &lt; 40%) |
| STAT_ZEIT_SOC_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 5 (40% &lt;= x &lt; 50%) |
| STAT_ZEIT_SOC_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 6 (50% &lt;= x &lt; 55%) |
| STAT_ZEIT_SOC_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 7 (55% &lt;= x &lt; 60%) |
| STAT_ZEIT_SOC_8_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 8 (60% &lt;= x &lt; 65%) |
| STAT_ZEIT_SOC_9_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 9 (65% &lt;= x &lt; 70%) |
| STAT_ZEIT_SOC_10_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 10 (70% &lt;= x &lt; 75%) |
| STAT_ZEIT_SOC_11_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 11 (75% &lt;= x &lt; 90%) |
| STAT_ZEIT_SOC_12_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit seit Einbau in SOC-Klasse 12 (90% &lt;= x) |

<a id="table-res-0xdd94"></a>
### RES_0XDD94

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. Temperatur &lt; -20 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T1_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T1_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T1_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T1_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T1_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T1_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T1_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T1_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T1_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T1_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. Temperatur &lt; -20 °C.  200 A &lt; Strom |

<a id="table-res-0xdd95"></a>
### RES_0XDD95

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T2_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 80 % SoC. -20°C &lt; Temperatur &lt; -13 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T2_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T2_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T2_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T2_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T2_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T2_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T2_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T2_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T2_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -20°C &lt; Temperatur &lt; -13 °C.  200 A &lt; Strom |

<a id="table-res-0xdd96"></a>
### RES_0XDD96

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T3_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T3_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T3_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T3_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T3_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T3_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T3_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T3_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T3_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T3_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -13°C &lt; Temperatur &lt; -7 °C.  200 A &lt; Strom |

<a id="table-res-0xdd97"></a>
### RES_0XDD97

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T4_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T4_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T4_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T4_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T4_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T4_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T4_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T4_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T4_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T4_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. -7°C &lt; Temperatur &lt; 0 °C.  200 A &lt; Strom |

<a id="table-res-0xdd98"></a>
### RES_0XDD98

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A. |
| STAT_HV_BATT_HIST_SOC1_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T5_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T5_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T5_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T5_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T5_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T5_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T5_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T5_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T5_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T5_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 0°C &lt; Temperatur &lt; 8 °C.  200 A &lt; Strom |

<a id="table-res-0xdd99"></a>
### RES_0XDD99

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T6_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T6_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T6_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T6_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T6_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T6_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T6_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T6_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T6_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T6_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 8°C &lt; Temperatur &lt; 25 °C.  200 A &lt; Strom |

<a id="table-res-0xdd9a"></a>
### RES_0XDD9A

Dimensions: 70 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HV_BATT_HIST_SOC1_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC1_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC1_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC1_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC1_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC1_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC1_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC1_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC1_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC1_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei SoC &lt; 15 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC2_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC2_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC2_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC2_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC2_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC2_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC2_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC2_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC2_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC2_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 15 % &lt; SoC &lt; 25 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC3_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC3_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC3_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC3_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC3_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC3_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC3_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC3_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC3_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC3_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 25 % &lt; SoC &lt; 35 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC4_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC4_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC4_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC4_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC4_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC4_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC4_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC4_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC4_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC4_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 35 % &lt; SoC &lt; 45 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC5_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC5_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC5_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC5_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC5_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC5_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC5_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC5_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC5_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC5_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 45 % &lt; SoC &lt; 55 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC6_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC6_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC6_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC6_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC6_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC6_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC6_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC6_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC6_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC6_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 55 % &lt; SoC &lt; 65 %. 25°C &lt; Temperatur.  200 A &lt; Strom |
| STAT_HV_BATT_HIST_SOC7_T7_I1_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur. Strom &lt; -90 A |
| STAT_HV_BATT_HIST_SOC7_T7_I2_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  -90 A &lt; Strom &lt; -50 A |
| STAT_HV_BATT_HIST_SOC7_T7_I3_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  -50 A &lt; Strom &lt; -20 A |
| STAT_HV_BATT_HIST_SOC7_T7_I4_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  -20 A &lt; Strom &lt; -0.1 A |
| STAT_HV_BATT_HIST_SOC7_T7_I5_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  0.1 A &lt; Strom &lt; 20 A |
| STAT_HV_BATT_HIST_SOC7_T7_I6_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  20 A &lt; Strom &lt; 50 A |
| STAT_HV_BATT_HIST_SOC7_T7_I7_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  50 A &lt; Strom &lt; 100 A |
| STAT_HV_BATT_HIST_SOC7_T7_I8_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  100 A &lt; Strom &lt; 150 A |
| STAT_HV_BATT_HIST_SOC7_T7_I9_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  150 A &lt; Strom &lt; 200 A |
| STAT_HV_BATT_HIST_SOC7_T7_I10_WERT | ms | high | unsigned long | - | - | 100.0 | 1.0 | 0.0 | Dauer bei 65 % &lt; SoC. 25°C &lt; Temperatur.  200 A &lt; Strom |

<a id="table-res-0xddae"></a>
### RES_0XDDAE

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_37_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 37 |
| STAT_ZELLSPANNUNG_38_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 38 |
| STAT_ZELLSPANNUNG_39_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 39 |
| STAT_ZELLSPANNUNG_40_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 40 |
| STAT_ZELLSPANNUNG_41_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 41 |
| STAT_ZELLSPANNUNG_42_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 42 |
| STAT_ZELLSPANNUNG_43_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 43 |
| STAT_ZELLSPANNUNG_44_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 44 |
| STAT_ZELLSPANNUNG_45_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 45 |
| STAT_ZELLSPANNUNG_46_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 46 |
| STAT_ZELLSPANNUNG_47_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 47 |
| STAT_ZELLSPANNUNG_48_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 48 |

<a id="table-res-0xddaf"></a>
### RES_0XDDAF

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_49_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 49 |
| STAT_ZELLSPANNUNG_50_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 50 |
| STAT_ZELLSPANNUNG_51_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 51 |
| STAT_ZELLSPANNUNG_52_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 52 |
| STAT_ZELLSPANNUNG_53_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 53 |
| STAT_ZELLSPANNUNG_54_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 54 |
| STAT_ZELLSPANNUNG_55_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 55 |
| STAT_ZELLSPANNUNG_56_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 56 |
| STAT_ZELLSPANNUNG_57_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 57 |
| STAT_ZELLSPANNUNG_58_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 58 |
| STAT_ZELLSPANNUNG_59_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 59 |
| STAT_ZELLSPANNUNG_60_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 60 |

<a id="table-res-0xddb0"></a>
### RES_0XDDB0

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_61_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 61 |
| STAT_ZELLSPANNUNG_62_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 62 |
| STAT_ZELLSPANNUNG_63_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 63 |
| STAT_ZELLSPANNUNG_64_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 64 |
| STAT_ZELLSPANNUNG_65_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 65 |
| STAT_ZELLSPANNUNG_66_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 66 |
| STAT_ZELLSPANNUNG_67_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 67 |
| STAT_ZELLSPANNUNG_68_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 68 |
| STAT_ZELLSPANNUNG_69_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 69 |
| STAT_ZELLSPANNUNG_70_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 70 |
| STAT_ZELLSPANNUNG_71_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 71 |
| STAT_ZELLSPANNUNG_72_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 72 |

<a id="table-res-0xddb1"></a>
### RES_0XDDB1

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_73_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 73 |
| STAT_ZELLSPANNUNG_74_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 74 |
| STAT_ZELLSPANNUNG_75_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 75 |
| STAT_ZELLSPANNUNG_76_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 76 |
| STAT_ZELLSPANNUNG_77_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 77 |
| STAT_ZELLSPANNUNG_78_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 78 |
| STAT_ZELLSPANNUNG_79_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 79 |
| STAT_ZELLSPANNUNG_80_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 80 |
| STAT_ZELLSPANNUNG_81_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 81 |
| STAT_ZELLSPANNUNG_82_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 82 |
| STAT_ZELLSPANNUNG_83_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 83 |
| STAT_ZELLSPANNUNG_84_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 84 |

<a id="table-res-0xddb2"></a>
### RES_0XDDB2

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_85_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 85 |
| STAT_ZELLSPANNUNG_86_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 86 |
| STAT_ZELLSPANNUNG_87_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 87 |
| STAT_ZELLSPANNUNG_88_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 88 |
| STAT_ZELLSPANNUNG_89_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 89 |
| STAT_ZELLSPANNUNG_90_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 90 |
| STAT_ZELLSPANNUNG_91_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 91 |
| STAT_ZELLSPANNUNG_92_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 92 |
| STAT_ZELLSPANNUNG_93_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 93 |
| STAT_ZELLSPANNUNG_94_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 94 |
| STAT_ZELLSPANNUNG_95_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 95 |
| STAT_ZELLSPANNUNG_96_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 96 |

<a id="table-res-0xddb3"></a>
### RES_0XDDB3

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADUNGSMENGE_BOOST_WERT | Ah | high | unsigned long | - | - | 1.0 | 3600.0 | 0.0 | Im BOOST-Betrieb der HV-Batterie entnommene Ladungsmenge |
| STAT_LADUNGSMENGE_RECUP_WERT | Ah | high | unsigned long | - | - | 1.0 | 3600.0 | 0.0 | Während Rekuperation der HV-Batterie zugeführte Ladungsmenge |

<a id="table-res-0xddb9"></a>
### RES_0XDDB9

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_1_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 1 |
| STAT_ZELLSPANNUNG_2_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 2 |
| STAT_ZELLSPANNUNG_3_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 3 |
| STAT_ZELLSPANNUNG_4_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 4 |
| STAT_ZELLSPANNUNG_5_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 5 |
| STAT_ZELLSPANNUNG_6_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 6 |
| STAT_ZELLSPANNUNG_7_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 7 |
| STAT_ZELLSPANNUNG_8_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 8 |
| STAT_ZELLSPANNUNG_9_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 9 |
| STAT_ZELLSPANNUNG_10_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 10 |
| STAT_ZELLSPANNUNG_11_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 11 |
| STAT_ZELLSPANNUNG_12_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 12 |

<a id="table-res-0xddba"></a>
### RES_0XDDBA

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_13_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 13 |
| STAT_ZELLSPANNUNG_14_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 14 |
| STAT_ZELLSPANNUNG_15_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 15 |
| STAT_ZELLSPANNUNG_16_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 16 |
| STAT_ZELLSPANNUNG_17_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 17 |
| STAT_ZELLSPANNUNG_18_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 18 |
| STAT_ZELLSPANNUNG_19_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 19 |
| STAT_ZELLSPANNUNG_20_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 20 |
| STAT_ZELLSPANNUNG_21_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 21 |
| STAT_ZELLSPANNUNG_22_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 22 |
| STAT_ZELLSPANNUNG_23_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 23 |
| STAT_ZELLSPANNUNG_24_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 24 |

<a id="table-res-0xddbb"></a>
### RES_0XDDBB

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_25_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 25 |
| STAT_ZELLSPANNUNG_26_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 26 |
| STAT_ZELLSPANNUNG_27_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 27 |
| STAT_ZELLSPANNUNG_28_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 28 |
| STAT_ZELLSPANNUNG_29_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 29 |
| STAT_ZELLSPANNUNG_30_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 30 |
| STAT_ZELLSPANNUNG_31_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 31 |
| STAT_ZELLSPANNUNG_32_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 32 |
| STAT_ZELLSPANNUNG_33_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 33 |
| STAT_ZELLSPANNUNG_34_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 34 |
| STAT_ZELLSPANNUNG_35_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 35 |
| STAT_ZELLSPANNUNG_36_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuell gemessene Zellspannung in V von Zelle 36 |

<a id="table-res-0xddbc"></a>
### RES_0XDDBC

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZEIGE_SOC_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | aktueller Anzeige Soc |
| STAT_MAXIMALE_ANZEIGE_SOC_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | obere Grenze des Anzeige Soc |
| STAT_MINIMALE_ANZEIGE_SOC_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | untere Grenze des Anzeige Soc |

<a id="table-res-0xddbe"></a>
### RES_0XDDBE

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZEIT_VORLADUNG_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | zuletzt benötigte Vorladezeit |
| STAT_ZEIT_VORLADUNG_1_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | benötigte Vorladezeit (1 Vorgang zuvor) |
| STAT_ZEIT_VORLADUNG_2_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | benötigte Vorladezeit (2 Vorgänge zuvor) |
| STAT_ZEIT_VORLADUNG_3_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | benötigte Vorladezeit (3 Vorgänge zuvor) |
| STAT_ZEIT_VORLADUNG_4_WERT | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | benötigte Vorladezeit (4 Vorgänge zuvor) |
| STAT_MAX_STROM_VORLADUNG_WERT | A | high | int | - | - | 1.0 | 100.0 | 0.0 | maximaler Vorladestrom (letzte Vorladung) |
| STAT_MAX_STROM_VORLADUNG_1_WERT | A | high | int | - | - | 1.0 | 100.0 | 0.0 | maximaler Vorladestrom (1 Vorgang zuvor) |
| STAT_MAX_STROM_VORLADUNG_2_WERT | A | high | int | - | - | 1.0 | 100.0 | 0.0 | maximaler Vorladestrom (2 Vorgänge zuvor) |
| STAT_MAX_STROM_VORLADUNG_3_WERT | A | high | int | - | - | 1.0 | 100.0 | 0.0 | maximaler Vorladestrom (3 Vorgänge zuvor) |
| STAT_MAX_STROM_VORLADUNG_4_WERT | A | high | int | - | - | 1.0 | 100.0 | 0.0 | maximaler Vorladestrom (4 Vorgänge zuvor) |
| STAT_MAX_TEMP_VORLADUNG_WERT | °C | high | int | - | - | 1.0 | 10.0 | 0.0 | maximale Temperatur bei Vorladung (letzte Vorladung) |
| STAT_MAX_TEMP_VORLADUNG_1_WERT | °C | high | int | - | - | 1.0 | 10.0 | 0.0 | maximale Temperatur bei Vorladung (1 Vorgang zuvor) |
| STAT_MAX_TEMP_VORLADUNG_2_WERT | °C | high | int | - | - | 1.0 | 10.0 | 0.0 | maximale Temperatur bei Vorladung (2 Vorgänge zuvor) |
| STAT_MAX_TEMP_VORLADUNG_3_WERT | °C | high | int | - | - | 1.0 | 10.0 | 0.0 | maximale Temperatur bei Vorladung (3 Vorgänge zuvor) |
| STAT_MAX_TEMP_VORLADUNG_4_WERT | °C | high | int | - | - | 1.0 | 10.0 | 0.0 | maximale Temperatur bei Vorladung (4 Vorgänge zuvor) |

<a id="table-res-0xddbf"></a>
### RES_0XDDBF

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_UCELL_MIN_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | minimale Einzelzellspannung aller Einzelzellen |
| STAT_UCELL_MAX_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | maximale Einzelzellspannung aller Einzelzellen |

<a id="table-res-0xddc0"></a>
### RES_0XDDC0

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TMOD_MIN_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | minimale Messtemperatur |
| STAT_TMOD_MAX_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | maximale Messtemperatur |
| STAT_TMOD_MEAN_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | durchschnittliche Messtemperatur |
| STAT_TCORE_MAX_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | maximale Zellkerntemperatur |

<a id="table-res-0xddc1"></a>
### RES_0XDDC1

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CSC_ID0_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 1 |
| STAT_CSC_ID1_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 2 |
| STAT_CSC_ID2_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 3 |
| STAT_CSC_ID3_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 4 |
| STAT_CSC_ID4_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 5 |
| STAT_CSC_ID5_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 6 |
| STAT_CSC_ID6_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 7 |
| STAT_CSC_ID7_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware ID der CSC 8 |

<a id="table-res-0xddc2"></a>
### RES_0XDDC2

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAKTOR_RS_ENTLADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert des seriellen ohmschen Widerstandes bei Entladung |
| STAT_FAKTOR_RS_LADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert des seriellen ohmschen Widerstandes bei Ladung |
| STAT_FAKTOR_RP_ENTLADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert des parallelen ohmschen Widerstandes bei Entladung |
| STAT_FAKTOR_RP_LADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert des parallelen ohmschen Widerstandes bei Ladung |
| STAT_FAKTOR_CP_ENTLADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert der parallelen Kapazität (Doppelschicht-Kondensator) bei Entladung |
| STAT_FAKTOR_CP_LADE_WERT | - | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Wert der parallelen Kapazität (Doppelschicht-Kondensator) bei Ladung |

<a id="table-res-0xddc4"></a>
### RES_0XDDC4

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SOC_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | SOC der HV-Batterie |
| STAT_SOC_PLAUSIBILITAET_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Plausibilität des HV-Batterie SOC (0 = plausibel, 1 = unplausibel) |

<a id="table-res-0xddc5"></a>
### RES_0XDDC5

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_1_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 1 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_2_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 2 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_3_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 3 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_4_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 4 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_5_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 5 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_6_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 6 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_7_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 7 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |
| STAT_MODULSPANNUNG_UNPLAUSIBEL_8_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannungswert in Modul 8 als plausibel / unplausibel (0 = kein Fehler / 1 = Fehler) detektiert |

<a id="table-res-0xddc6"></a>
### RES_0XDDC6

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HISTO_SYM_DAUER_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 0 &lt; Zeit &lt; 15 |
| STAT_HISTO_SYM_DAUER_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 15 &lt; Zeit &lt; 75 |
| STAT_HISTO_SYM_DAUER_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 75 &lt; Zeit &lt; 135 |
| STAT_HISTO_SYM_DAUER_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 135 &lt; Zeit &lt; 195 |
| STAT_HISTO_SYM_DAUER_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 195 &lt; Zeit &lt; 255 |
| STAT_HISTO_SYM_DAUER_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 255 &lt; Zeit &lt; 315 |
| STAT_HISTO_SYM_DAUER_7_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 315 &lt; Zeit &lt; 375 |
| STAT_HISTO_SYM_DAUER_8_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl in Klasse 375 &lt; Zeit |

<a id="table-res-0xddc7"></a>
### RES_0XDDC7

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HISTO_SYM_ZELLANZAHL_1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 0 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 1 Zelle |
| STAT_HISTO_SYM_ZELLANZAHL_3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 2-8 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 9-48 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 49-87 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 88-94 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 95 Zellen |
| STAT_HISTO_SYM_ZELLANZAHL_8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Einschaltvorgänge bei 96 Zellen |

<a id="table-res-0xddc8"></a>
### RES_0XDDC8

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SYM_DELTASOC_1_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | aktueller dSOC (zuletzt bestimmt) |
| STAT_SYM_DELTASOC_2_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | dSOC vor einer Fahrt |
| STAT_SYM_DELTASOC_3_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | dSOC vor 2 Fahrten |
| STAT_SYM_DELTASOC_4_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | dSOC vor 3 Fahrten |
| STAT_SYM_DELTASOC_5_WERT | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | dSOC vor 4 Fahrten |

<a id="table-res-0xddc9"></a>
### RES_0XDDC9

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_SYM_DAUER_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximale Symmetrierdauer des zuletzt Symmetriervorgangs |
| STAT_MAX_SYM_ZEIT_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Beginn Symmetriervorgang zu 1 |
| STAT_BAL_COMPL_1_NR | 0-n | high | unsigned char | - | TAB_SME_SYMMETRIERUNG_FERTIG | - | - | - | Status Symmetrierung |
| STAT_MAX_SYM_DAUER_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximale Symmetrierdauer des Symmetriervorgangs vor 1 Fahrt |
| STAT_MAX_SYM_ZEIT_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Beginn Symmetriervorgang zu 2 |
| STAT_BAL_COMPL_2_NR | 0-n | high | unsigned char | - | TAB_SME_SYMMETRIERUNG_FERTIG | - | - | - | Status Symmetrierung |
| STAT_MAX_SYM_DAUER_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximale Symmetrierdauer des Symmetriervorgangs vor 2 Fahrt |
| STAT_MAX_SYM_ZEIT_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Beginn Symmetriervorgang zu 3 |
| STAT_BAL_COMPL_3_NR | 0-n | high | unsigned char | - | TAB_SME_SYMMETRIERUNG_FERTIG | - | - | - | Status Symmetrierung |
| STAT_MAX_SYM_DAUER_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximale Symmetrierdauer des Symmetriervorgangs vor 3 Fahrt |
| STAT_MAX_SYM_ZEIT_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Beginn Symmetriervorgang zu 4 |
| STAT_BAL_COMPL_4_NR | 0-n | high | unsigned char | - | TAB_SME_SYMMETRIERUNG_FERTIG | - | - | - | Status Symmetrierung |
| STAT_MAX_SYM_DAUER_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximale Symmetrierdauer des Symmetriervorgangs vor 4 Fahrten |
| STAT_MAX_SYM_ZEIT_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Beginn Symmetriervorgang zu 5 |
| STAT_BAL_COMPL_5_NR | 0-n | high | unsigned char | - | TAB_SME_SYMMETRIERUNG_FERTIG | - | - | - | Status Symmetrierung |

<a id="table-res-0xddcb"></a>
### RES_0XDDCB

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MIN_SOC_GRENZE_WERT | % | high | int | - | - | 1.0 | 100.0 | 0.0 | aktuell gültige minimale SOC Grenze |
| STAT_MAX_SOC_GRENZE_WERT | % | high | int | - | - | 1.0 | 100.0 | 0.0 | aktuell gültige maximale SOC Grenze |

<a id="table-res-0xddcc"></a>
### RES_0XDDCC

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHUETZ_K1_RESTZAEHLER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aktuell noch mögliche Schaltungen für Schütz K1 |
| STAT_SCHUETZ_K2_RESTZAEHLER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aktuell noch mögliche Schaltungen für Schütz K2 |
| STAT_SCHUETZ_K3_RESTZAEHLER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aktuell noch mögliche Schaltungen für Schütz K3 |

<a id="table-res-0xddcf"></a>
### RES_0XDDCF

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DIFF_SPANNUNG_STATISCH_WERT | V | high | int | - | - | 1.0 | 100.0 | 0.0 | Differenzspannung: Gesamtspannung HV-Batterie - Summenzellspannung (statische Ermittlung) |
| STAT_DIFF_SPANNUNG_DYNAMISCH_WERT | V | high | int | - | - | 1.0 | 100.0 | 0.0 | Differenzspannung: Gesamtspannung HV-Batterie - Summenzellspannung (dynamische Ermittlung) |

<a id="table-res-0xdde8"></a>
### RES_0XDDE8

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DEGRADATION_GESAMT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der alterungsbedingten Spannungsdegradationen der Hochvolt-Speicher über Gesamtzeit  |
| STAT_ANZAHL_DEGRADATION_LAUFENDES_JAHR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der alterungsbedingten Spannungsdegradationen der Hochvolt-Speicher im Mittel über letztes und laufendes Jahr |

<a id="table-res-0xdde9"></a>
### RES_0XDDE9

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HFK_GESAMT_SOC_HUB_15_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub von 15% über Gesamtzeit |
| STAT_HFK_GESAMT_SOC_HUB_15_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 15% und 20% über Gesamtzeit |
| STAT_HFK_GESAMT_SOC_HUB_20_25_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 20% und 25% über Gesamtzeit |
| STAT_HFK_GESAMT_SOC_HUB_25_30_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 25% und 30% über Gesamtzeit |
| STAT_HFK_GESAMT_SOC_HUB_30_35_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 30% und 35% über Gesamtzeit |
| STAT_HFK_GESAMT_SOC_HUB_35_40_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 35% und 40% über Gesamtzeit |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_15_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub von 15% im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_15_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 15% und 20%  im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_20_25_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 20% und 25%  im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_25_30_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 25% und 30%  im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_30_35_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 30% und 35%  im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_JAHR_SOC_HUB_35_40_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 35% und 40%  im Mittel über letztes und laufendes Jahr |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_15_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub von 15%  im Mittel über letzten und laufenden Monat |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_15_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 15% und 20% im Mittel über letzten und laufenden Monat |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_20_25_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 20% und 25% im Mittel über letzten und laufenden Monat |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_25_30_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 25% und 30% im Mittel über letzten und laufenden Monat |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_30_35_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 30% und 35% im Mittel über letzten und laufenden Monat |
| STAT_HFK_LAUFENDES_MONAT_SOC_HUB_35_40_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit bei SoC-Hub zwischen 35% und 40% im Mittel über letzten und laufenden Monat |
| STAT_ZEITSTEMPEL_SOC_HUB_15_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub von 15 % |
| STAT_ZEITSTEMPEL_SOC_HUB_15_20_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub zwischen 15% und 20% |
| STAT_ZEITSTEMPEL_SOC_HUB_20_25_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub zwischen 20% und 25% |
| STAT_ZEITSTEMPEL_SOC_HUB_25_30_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub zwischen 25% und 30% |
| STAT_ZEITSTEMPEL_SOC_HUB_30_35_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub zwischen 30% und 35% |
| STAT_ZEITSTEMPEL_SOC_HUB_35_40_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel bei letztem Auftreten des SoC-Hub zwischen 35% und 40% |

<a id="table-res-0xdf60"></a>
### RES_0XDF60

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIME_HV_ON_WERT | h | high | unsigned long | - | - | 1.0 | 100.0 | 0.0 | Die Gesamtzeit bei geschlossenen Hauptschalter |
| STAT_TIME_TOTAL_WERT | h | high | unsigned long | - | - | 1.0 | 100.0 | 0.0 | Die Gesamtzeit bei geschlossenen und geöffneten Hauptschalter |

<a id="table-res-0xdf64"></a>
### RES_0XDF64

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KUEHLDAUER_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Dauer Ventil geöffnet in der Klasse: 0 &lt; t &lt; 5 |
| STAT_KUEHLDAUER_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Dauer Ventil geöffnet in der Klasse: 6 &lt; t &lt; 10 |
| STAT_KUEHLDAUER_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Dauer Ventil geöffnet in der Klasse: 10 &lt; t &lt; 20 |
| STAT_KUEHLDAUER_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Dauer Ventil geöffnet in der Klasse: 20 &lt; t |

<a id="table-res-0xdf65"></a>
### RES_0XDF65

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_SPREIZUNG_SYS_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten bei Kühlung an Klasse 1 (x &lt;= 3°C) |
| STAT_TEMP_SPREIZUNG_SYS_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten bei Kühlung an Klasse 2 (3°C &lt; x &lt;= 6°C) |
| STAT_TEMP_SPREIZUNG_SYS_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten bei Kühlung an Klasse 3 (6°C &lt; x &lt;= 10°C) |
| STAT_TEMP_SPREIZUNG_SYS_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten bei Kühlung an Klasse 4 (10°C &lt; x &lt;= 15°C) |
| STAT_TEMP_SPREIZUNG_SYS_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten bei Kühlung an Klasse 5 (15°C &lt;= x) |

<a id="table-res-0xdf66"></a>
### RES_0XDF66

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_KUEHLMITTEL_1_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten in der Temperaturklasse 1: T &lt;= 0°C |
| STAT_TEMP_KUEHLMITTEL_2_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten in der Temperaturklasse 2: 0°C &lt; T &lt;= 5°C |
| STAT_TEMP_KUEHLMITTEL_3_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten in der Temperaturklasse 3:  5°C &lt; T &lt;= 10°C |
| STAT_TEMP_KUEHLMITTEL_4_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten in der Temperaturklasse 4:  10°C &lt; T &lt;= 15°C |
| STAT_TEMP_KUEHLMITTEL_5_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten in der Temperaturklasse 5:  15°C &lt; T &lt;= 20°C |
| STAT_TEMP_KUEHLMITTEL_6_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Minuten des Kühlmittels in der Temperaturklasse 6:  20°C &lt; T |

<a id="table-res-0xdf67"></a>
### RES_0XDF67

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADUNG_KUEHLUNG_WERT | Ah | high | unsigned long | - | - | 1.0 | 3600.0 | 0.0 | Ladungsmenge bei eingeschalteter Kühlung |
| STAT_ENTLADUNG_KUEHLUNG_WERT | Ah | high | unsigned long | - | - | 1.0 | 3600.0 | 0.0 | Entladungsmenge bei eingeschalteter Kühlung |

<a id="table-arg-0x6500"></a>
### ARG_0X6500

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6501"></a>
### ARG_0X6501

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6502"></a>
### ARG_0X6502

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6503"></a>
### ARG_0X6503

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6504"></a>
### ARG_0X6504

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6506"></a>
### ARG_0X6506

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6507"></a>
### ARG_0X6507

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6508"></a>
### ARG_0X6508

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6509"></a>
### ARG_0X6509

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| SERIENNUMMER | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Seriennummer |

<a id="table-arg-0x650b"></a>
### ARG_0X650B

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht ansteuern, 1=ansteuern |

<a id="table-arg-0x6511"></a>
### ARG_0X6511

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0-n | high | unsigned char | - | TAB_SYM_MODUS | 1.0 | 1.0 | 0.0 | - | - | 0=Normalbetrieb, 1=rein spannungsgesteuert |

<a id="table-arg-0x6512"></a>
### ARG_0X6512

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=nicht senden, 1=senden |

<a id="table-arg-0x6515"></a>
### ARG_0X6515

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| TABELLE | - | high | string[64] | - | - | 1.0 | 1.0 | 0.0 | - | - | Sendestring der HW-IDs |

<a id="table-arg-0x6519"></a>
### ARG_0X6519

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=kein Standby, 1=Standby |

<a id="table-arg-0x651b"></a>
### ARG_0X651B

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort zur Ausführung des Entwicklerjobs |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=geregelt/keine Anforderung, 1=Schütze schließen |

<a id="table-tab-schuetz-freigabe"></a>
### TAB_SCHUETZ_FREIGABE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht freigegeben |
| 0x01 | freigegeben |
| 0xFF | nicht definiert |

<a id="table-tab-kuehlkreislauf-ventil-rueckgabe"></a>
### TAB_KUEHLKREISLAUF_VENTIL_RUECKGABE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | geschlossen |
| 0x01 | offen |
| 0x02 | Fehler |

<a id="table-tab-aufstart-verhinderer"></a>
### TAB_AUFSTART_VERHINDERER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | interner Fehler |
| 0xFF | nicht definiert |

<a id="table-tab-kuehlerkreislauf-ventil"></a>
### TAB_KUEHLERKREISLAUF_VENTIL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | geschlossen |
| 0x01 | offen |
| 0x02 | geregelt |
| 0xFF | nicht definiert |

<a id="table-tab-sym-modus"></a>
### TAB_SYM_MODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalmodus |
| 1 | Spannungsgesteuerter Modus |
| 2 | Bitbalancing (Auswertung Cell-SOCs) |
| 3 | Zeitgesteuertes Balancing |

<a id="table-tab-schuetz-schalter"></a>
### TAB_SCHUETZ_SCHALTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | offen |
| 0x01 | geschlossen |
| 0x02 | verschweisste Kontakte |
| 0x03 | nicht definiert |

<a id="table-tab-isolation-isolationsfehler"></a>
### TAB_ISOLATION_ISOLATIONSFEHLER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Isolationswarnung liegt vor |
| 0x02 | Isolationsfehler liegt vor |
| 0xFF | nicht definiert |

<a id="table-tab-isolation-erfolgreich"></a>
### TAB_ISOLATION_ERFOLGREICH

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Isolationsmessung nicht erfolgreich |
| 0x01 | Isolationsmessung erfolgreich |
| 0x02 | Isolationsmessung läuft! |
| 0xFF | nicht definiert |

<a id="table-svk-version-dop"></a>
### SVK_VERSION_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | SVKVersion_01 |

<a id="table-tab-sme-ermittlung"></a>
### TAB_SME_ERMITTLUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ermittlung läuft: Entladungsphase bis SoC min |
| 0x01 | Ermittlung läuft: Ladungsphase |
| 0x02 | Ermittlung läuft: Entladungsphase bis mittleren SoC |
| 0x03 | Ermittlung erfolgreich beendet |

<a id="table-tab-sme-symmetrierung-fertig"></a>
### TAB_SME_SYMMETRIERUNG_FERTIG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | abgeschlossen |
| 0x01 | nicht abgeschlossen |

<a id="table-dm-tab-roe-activated-dop"></a>
### DM_TAB_ROE_ACTIVATED_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Aktive Fehlermeldung deaktiviert |
| 1 | Aktive Fehlermeldung aktiviert |

<a id="table-tab-status-hvil"></a>
### TAB_STATUS_HVIL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht ok |
| 0x01 | ok |
| 0xFF | nicht definiert |

<a id="table-rdbi-ads-dop"></a>
### RDBI_ADS_DOP

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ISOSAEReserved_00 |
| 1 | defaultSession |
| 2 | programmingSession |
| 3 | extendedDiagnosticSession |
| 4 | safetySystemDiagnosticSession |
| 64 | vehicleManufacturerSpecific_40 |
| 65 | codingSession |
| 66 | SWTSession |

<a id="table-tab-anst-schuetz"></a>
### TAB_ANST_SCHUETZ

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECUMehrmalsProgrammierbar |
| 1 | ECUMindestensEinmalVollstaendigProgrammierbar |
| 2 | ECUNichtMehrProgrammierbar |

<a id="table-energiesparmode-dop"></a>
### ENERGIESPARMODE_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalmode |
| 1 | Fertigungsmode |
| 2 | Transportmode |
| 3 | Flashmode |

<a id="table-prog-dep-dop"></a>
### PROG_DEP_DOP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | correctResult |
| 2 | incorrectResult |
| 3 | incorrectResult error SWE - HWE |
| 4 | incorrectResult error SWE - SWE |
| 255 | reserved |

<a id="table-extended-energy-mode-dop"></a>
### EXTENDED_ENERGY_MODE_DOP

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Erweiterter Betriebsmodus nicht gesetzt |
| 1 | Erweiterter Betriebsmodus 1 |
| 2 | Erweiterter Betriebsmodus 2 |
| 3 | Erweiterter Betriebsmodus 3 |
| 4 | Erweiterter Betriebsmodus 4 |
| 5 | Erweiterter Betriebsmodus 5 |
| 6 | Erweiterter Betriebsmodus 6 |
| 7 | Erweiterter Betriebsmodus 7 |
| 8 | Erweiterter Betriebsmodus 8 |
| 9 | Erweiterter Betriebsmodus 9 |
| 10 | Erweiterter Betriebsmodus 10 |
| 11 | Erweiterter Betriebsmodus 11 |
| 12 | Erweiterter Betriebsmodus 12 |
| 13 | Erweiterter Betriebsmodus 13 |
| 14 | Erweiterter Betriebsmodus 14 |
| 15 | Erweiterter Betriebsmodus 15 |

<a id="table-forttexte"></a>
### _FORTTEXTE

Dimensions: 21 rows × 2 columns

| _ORT | _ORTTEXT |
| --- | --- |
| 0x00 | System |
| 0x10 | CAN |
| 0x20 | Voltage of 12-cell module |
| 0x21 | Temperature of NTC_SW1 |
| 0x22 | Temperature of NTC_SW2 |
| 0x23 | Monitoring WUP signal of the SME |
| 0x24 | Reference voltage of the LTC6802-2 |
| 0x25 | Internal temperature of CSC |
| 0x26 | Voltage of the reference voltage divider |
| 0x27 | Voltage at WD |
| 0x28 | Configuration of HW version |
| 0x29 | Temperature of NTC_HW1 |
| 0x2A | 5V-Suppy |
| 0x30 | BSM |
| 0x31 | BSM: internal temp. |
| 0x32 | BSM: Temp.-Sens 1 |
| 0x33 | BSM: Temp.-Sens 2 |
| 0x34 | BSM: Monitor-Baustein |
| 0x40 | Versorgung |
| 0x50 | Balancing |
| 0xFF | unknown error |

<a id="table-farttexte"></a>
### _FARTTEXTE

Dimensions: 27 rows × 2 columns

| _ART | _ARTTEXT |
| --- | --- |
| 0x00 | generic |
| 0x01 | Out of Range Low |
| 0x02 | Out of Range High |
| 0x03 | Bus Off |
| 0x04 | Alive invalid |
| 0x05 | Under-voltage threshold reached |
| 0x06 | ADC self-test 1 |
| 0x07 | ADC self-test 2 |
| 0x08 | PEC-Error |
| 0x09 | VUV-Error |
| 0x0A | VOV-Error |
| 0x0B | Thermal shutdown |
| 0x0C | Over-temperature |
| 0x0D | Open connection |
| 0x0E | ROM |
| 0x0F | RAM |
| 0x10 | Bad request |
| 0x11 | Balancing unit defect |
| 0x12 | Compatibility |
| 0x13 | NVM |
| 0x14 | Plausibility check module voltage |
| 0x15 | Plausibility check temperature |
| 0x16 | Time-out communication to Front End |
| 0x17 | brief Plausibilitaet RAM |
| 0x18 | brief RAM Adressierung |
| 0x19 | brief Parameter im NVMS |
| 0xFF | unknown kind of error |

<a id="table-fopttexte"></a>
### _FOPTTEXTE

Dimensions: 5 rows × 2 columns

| _OPT | _OPTTEXT |
| --- | --- |
| 0x00 | no option |
| 0x01 | fault is active |
| 0x02 | fault may be reset by SME-Request |
| 0x80 | fault is permanent, reset only by SME-request |
| 0xFF | invalid option |

<a id="table-balanciertexte"></a>
### _BALANCIERTEXTE

Dimensions: 5 rows × 2 columns

| _BAL | _BALTEXT |
| --- | --- |
| 0x00 | inaktiv |
| 0x01 | aktiv, SME gibt Grenze vor |
| 0x02 | aktiv, SME gibt Bitmap vor |
| 0x03 | aktiv, keine Ansteuerung |
| 0xFF | unbekannte Balancierart |

<a id="table-fehlermaskentexte"></a>
### _FEHLERMASKENTEXTE

Dimensions: 30 rows × 2 columns

| _MASK | _MASKTEXT |
| --- | --- |
| 0x00000000 | no CSC error;  |
| 0x00000001 | cell overvoltage occurred;  |
| 0x00000002 | cell undervoltage occurred;  |
| 0x00000004 | temp. sensor 1 open to U_ref;  |
| 0x00000008 | temp. sensor 1 short to ground;  |
| 0x00000010 | temp. sensor 2 open to U_ref;  |
| 0x00000020 | temp. sensor 2 short to ground;  |
| 0x00000040 | module volt. out of range (high);  |
| 0x00000080 | module volt. out of range (low);  |
| 0x00000100 | open wire detected;  |
| 0x00000200 | balancing unit defective;  |
| 0x00000400 | CSC ECU-temperature too high;  |
| 0x00000800 | thermal shutdown occurred;  |
| 0x00001000 | invalid request received;  |
| 0x00002000 | lowest balancing voltage reached;  |
| 0x00004000 | Wake-up (WUP_ISO) defective;  |
| 0x00008000 | SPI defective, Alive-Counter defective;  |
| 0x00010000 | Invalid CAN-database;  |
| 0x00020000 | CAN-Bus off detected;  |
| 0x00040000 | ADC-Test 1 of LTC6802 failed;  |
| 0x00080000 | ADC-Test 2 of LTC6802 failed;  |
| 0x00100000 | Self-test of LTC6801 failed;  |
| 0x00200000 | RAM-Test failed;  |
| 0x00400000 | ROM-Test failed;  |
| 0x00800000 | T1 open wire detected;  |
| 0x01000000 | T2 open wire detected;  |
| 0x02000000 | Ucell plausibility error;  |
| 0x04000000 | T plausibility error;  |
| 0x08000000 | critical HW defect, shut-off required;  |
| 0xFFFFFFFF | unknown error |
