# tpl.prg

- Jobs: [41](#jobs)
- Tables: [76](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Telematic Plattform Low |
| ORIGIN | BMW EI-71 Hr.Kaindl |
| REVISION | 8.005 |
| AUTHOR | PIXIDAGmbH EI-71 Lindner, BMW_AG EI-71 Kaindl |
| COMMENT | - |
| PACKAGE | 1.49 |
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
- [STATUS_BETRIEBSMODE](#job-status-betriebsmode) - Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default
- [STEUERN_BETRIEBSMODE](#job-steuern-betriebsmode) - Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [_STEUERN_TELESERVICE_LOGGING](#job-steuern-teleservice-logging) - Auslesen der gespeicherten internen teleservice Loggings 
- [_STEUERN_REMOTESERVICE_LOGGING](#job-steuern-remoteservice-logging) - Auslesen der gespeicherten internen remote service Loggings 
- [STATUS_POWERMANAGEMENT_NAD](#job-status-powermanagement-nad) - Auslesen der gespeicherten internen Powermanagement Transitionen 
- [STATUS_ECALL_LOGGING](#job-status-ecall-logging) - Auslesen der gespeicherten internen EU ecall Loggings 
- [STEUERN_PROVISIONING_DATA](#job-steuern-provisioning-data) - Schreiben der Provisionierungsdaten

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

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IGNORIERE_EREIGNIS_DTC | string | 'IGNORIERE_EREIGNIS_DTC': Alle Ereignis DTC-Fehlereinträge werden ignoriert sonst: alle Fehlereinträge werden ausgegeben |

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

Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9

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

Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-stop"></a>
### STEUERN_ROE_PERSISTENT_STOP

Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-start"></a>
### STEUERN_ROE_PERSISTENT_START

Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)

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

<a id="job-steuern-teleservice-logging"></a>
### _STEUERN_TELESERVICE_LOGGING

Auslesen der gespeicherten internen teleservice Loggings 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | teleservice logging session number requested Range: 1-20 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIMESTAMP | string | Timestamp as hex string |
| STAT_EVENT_TEXT | string | values from table TEventTsLog |
| STAT_CC_NOTIFICATION | int | CALL_CONTROL_NOTIFI Event - Call Control Notification |
| STAT_CC_REQUEST | int | CALL_CONTROL_REQUEST Event - Call Control Request |
| STAT_HTTP_RES_APP_TYPE | string | HTTP_RESPONSE Event - values from table THttpResponseType |
| STAT_HTTP_RESULT | int | HTTP_RESPONSE Event - Http Result |
| STAT_HTTP_REQ_APP_TYPE | string | HTTP_REQUEST Event - values from table THttpRequestType |
| STAT_HTTP_METHOD | string | HTTP_REQUEST Event - Http method |
| STAT_JSESSION_ID | string | HTTP_REQUEST / HTTP_RESPONSE Event - Jsession ID |
| STAT_VIN | string | HTTP_REQUEST Event - VIN |
| STAT_URL | string | HTTP_REQUEST Event - Url |
| STAT_POSITION_DATA | string | HTTP_REQUEST Event - Position data |
| STAT_WAKEUP_MASK | string | PINGUIN_TRIGGER Event - Wakeup Mask |
| STAT_BEARER | string | PINGUIN_TRIGGER Event - Bearer - values from table TBearer |
| STAT_DS_SPEED | int | RPC_REQUEST Event - Drive State : Speed |
| STAT_DS_HANDBRAKE_LOCKED | char | RPC_REQUEST Event - Drive State : Handbrake Locked |
| STAT_DS_VEH_MOVING | char | RPC_REQUEST Event - Drive State : Vehicle Moving |
| STAT_RPC_ERROR_CAUSE | string | RPC_REQUEST Event - RPC Error Cause - values from table TRpcErrorCause |
| STAT_RPC | char | RPC_INDICATION / RPC_REQUEST / RPC_TRIGGER Event - RPC |
| STAT_CELL_ID | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Cell ID |
| STAT_CLAMP_STATE | string | PINGUIN_TRIGGER / RPC_TRIGGER / VEHICLE_CLAMP_STATE_EVENT Event - Clamp State - values from table TClampState |
| STAT_COD_TEL_DISABLE | char | PINGUIN_TRIGGER / RPC_TRIGGER Event - Coding Telematic Disable |
| STAT_ENGINE_STATE | char | PINGUIN_TRIGGER / RPC_TRIGGER Event - Engine state |
| STAT_MILEAGE | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Mileage |
| STAT_NMCC | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - NMCC |
| STAT_NMNC | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - NMNC |
| STAT_POWER_STATE | string | PINGUIN_TRIGGER / RPC_TRIGGER Event - Power State - values from table TPowerMode |
| STAT_SIGNAL_STRENGTH | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Signal strength |
| STAT_VEH_BUS_STATE | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Vehicle bus state |
| STAT_VEH_EVENT | string | VEHICLE_EVENT Event - values from table TVehicleEvent |
| STAT_AVAIL_TS | int | TS_CALL_STATES Event - Available Teleservice |
| STAT_CALL_ST | string | TS_CALL_STATES Event  - Call status - values from table TCallStatus |
| STAT_DATA_SERVICE_TYPE | string | TS_CALL_STATES Event  - Data service type - values from table TDataServiceType |
| STAT_DATA_CALL_ST | string | TS_CALL_STATES Event  - Data Call status - values from table TDataCallStatus |
| STAT_LANG_CALL_ST | string | TS_CALL_STATES Event  - Language Call Status - values from table TCallStatus |
| STAT_ERROR_MESS | string | TS_CALL_STATES Event  - Error Message - values from table TErrorMessage |
| STAT_BLOCK_CALL_ST | string | TS_CALL_STATES Event  -  Block Call status - values from table TBlockCallState |
| STAT_TELE_EVENT_TYPE | string | START_TS_TRIGGER Event  -  Teleservice Event type - values from table TTeleEventType |
| STAT_CATEGORIES_TEXT | string | values from table TCategoriesTsLog |
| STAT_CONTEXT_TYPE_TEXT | string | values from table TContextTypeTsLog |
| STAT_TS_CALL_STATE | int | Basic Log - CAN TEleservice Call State |
| STAT_CALL_TYPES | int | Extended Log - Call Types |
| STAT_HOTLINE_CALL_NUMBER | string | Extended Log - Hotline Call Number |
| STAT_MAX_TS_SPEED | int | Extended Log - Max Teleservice Speed |
| STAT_SAVED_TS_TRIGGER | int | Extended Log - Saved Teleservice Trigger |
| STAT_TD_CALL_NUMBER | string | Extended Log - Telediagnostic Call Number |
| STAT_TS_ACTIVE | int | Extended Log - Teleservice Active |
| STAT_TS_DATE | int | Extended Log - Teleservice Date |
| STAT_TS_DISTANCE_INT | int | Extended Log - Teleservice Distance Interval |
| STAT_TS_TIME_INT | int | Extended Log - Teleservice Time Interval |
| STAT_TS_URL | string | Extended Log - Teleservice Url |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-remoteservice-logging"></a>
### _STEUERN_REMOTESERVICE_LOGGING

Auslesen der gespeicherten internen remote service Loggings 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | remote service logging session number requested Range: 1-20 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIMESTAMP | string | Timestamp as hex string |
| STAT_EVENT_TEXT | string | values from table TEventRsLog |
| STAT_CC_NOTIFICATION | int | CALL_CONTROL_NOTIFI Event - Call Control Notification |
| STAT_CC_REQUEST | int | CALL_CONTROL_REQUEST Event - Call Control Request |
| STAT_HTTP_RES_APP_TYPE | string | HTTP_RESPONSE Event - values from table THttpResponseType |
| STAT_HTTP_RESULT | int | HTTP_RESPONSE Event - Http Result |
| STAT_HTTP_REQ_APP_TYPE | string | HTTP_REQUEST Event - values from table THttpRequestType |
| STAT_HTTP_METHOD | string | HTTP_REQUEST Event - Http method |
| STAT_JSESSION_ID | string | HTTP_REQUEST / HTTP_RESPONSE Event - Jsession ID |
| STAT_VIN | string | HTTP_REQUEST Event - VIN |
| STAT_URL | string | HTTP_REQUEST Event - Url |
| STAT_POSITION_DATA | string | HTTP_REQUEST Event - Position data |
| STAT_WAKEUP_MASK | string | PINGUIN_TRIGGER Event - Wakeup Mask |
| STAT_BEARER | string | PINGUIN_TRIGGER Event - Bearer - values from table TBearer |
| STAT_DS_SPEED | int | RPC_REQUEST Event - Drive State : Speed |
| STAT_DS_HANDBRAKE_LOCKED | char | RPC_REQUEST Event - Drive State : Handbrake Locked |
| STAT_DS_VEH_MOVING | char | RPC_REQUEST Event - Drive State : Vehicle Moving |
| STAT_RPC_ERROR_CAUSE | string | RPC_REQUEST Event - RPC Error Cause - values from table TRpcErrorCause |
| STAT_RPC | char | RPC_INDICATION / RPC_REQUEST / RPC_TRIGGER Event - RPC |
| STAT_CELL_ID | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Cell ID |
| STAT_CLAMP_STATE | string | PINGUIN_TRIGGER / RPC_TRIGGER / VEHICLE_CLAMP_STATE_EVENT Event - Clamp State - values from table TClampState |
| STAT_COD_TEL_DISABLE | char | PINGUIN_TRIGGER / RPC_TRIGGER Event - Coding Telematic Disable |
| STAT_ENGINE_STATE | char | PINGUIN_TRIGGER / RPC_TRIGGER Event - Engine state |
| STAT_MILEAGE | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Mileage |
| STAT_NMCC | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - NMCC |
| STAT_NMNC | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - NMNC |
| STAT_POWER_STATE | string | PINGUIN_TRIGGER / RPC_TRIGGER Event - Power State - values from table TPowerMode |
| STAT_SIGNAL_STRENGTH | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Signal strength |
| STAT_VEH_BUS_STATE | int | PINGUIN_TRIGGER / RPC_TRIGGER Event - Vehicle bus state |
| STAT_VEH_EVENT | string | VEHICLE_EVENT Event - values from table TVehicleEvent |
| STAT_CATEGORIES_TEXT | string | values from table TCategoriesRTsLog |
| STAT_CONTEXT_TYPE_TEXT | string | values from table TContextTypeRsLog |
| STAT_EVENT_CREATION_TIME | long | Basic Log - Event creation time |
| STAT_RS_ACTIVE | char | Extended Log - Remote Service Active |
| STAT_RCC_ACTIVE | char | Extended Log - Remote Climate Control Active |
| STAT_RDL_ACTIVE | char | Extended Log - Remote Door Lock Active |
| STAT_RDU_ACTIVE | char | Extended Log - Remote Door Unlock Active |
| STAT_RHB_ACTIVE | char | Extended Log - Remote Horn Blow Active |
| STAT_RLF_ACTIVE | char | Extended Log - Remote Light Flash Active |
| STAT_VF_ACTIVE | char | Extended Log - Vehicle Finder Active |
| STAT_DOWNLINK_URL | string | Extended Log - Downlink Url |
| STAT_UPLINK_URL | string | Extended Log - Uplink Url |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-powermanagement-nad"></a>
### STATUS_POWERMANAGEMENT_NAD

Auslesen der gespeicherten internen Powermanagement Transitionen 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | Dataset number requested Range: 1 (Only one dataset supported) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIMESTAMP_TEXT | string | Timestamp as hex string |
| STAT_STM | string | Values from table TPowerStmNAD |
| STAT_STATUS | string | Values from table TPowerStateNAD |
| STAT_TRIGGER | string | Values from table TPowerTriggerNAD |
| STAT_GUARD | string | Values from table TPowerGuardNAD |
| STAT_GUARD_VALUE_TEXT | string | Guard value as hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-ecall-logging"></a>
### STATUS_ECALL_LOGGING

Auslesen der gespeicherten internen EU ecall Loggings 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | eCall logging session number requested Range: 1-20 Disable/Enable logging session: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_TEXT | string | values from table TStateEcallLog |
| STAT_EVENT_TEXT | string | values from table TEventEcallLog |
| STAT_TIMESTAMP | string | Timestamp as hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-provisioning-data"></a>
### STEUERN_PROVISIONING_DATA

Schreiben der Provisionierungsdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TYPE | unsigned char | Welche Daten geschrieben werden sollen 0x01 DPAS, 0x03 OTA |
| ARG_PATH | string | absolute and complete path to file that shall be written |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Rückmeldungen, Fehlercodes z.B. OK 0x00 oder NOTOK 0x01 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XA020_R](#table-arg-0xa020-r) (2 × 14)
- [ARG_0XA05F_R](#table-arg-0xa05f-r) (1 × 14)
- [ARG_0XA086_R](#table-arg-0xa086-r) (3 × 14)
- [ARG_0XA089_R](#table-arg-0xa089-r) (1 × 14)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (40 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (93 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (2 × 2)
- [RES_0XA020_R](#table-res-0xa020-r) (1 × 13)
- [RES_0XA05E_R](#table-res-0xa05e-r) (4 × 13)
- [RES_0XA05F_R](#table-res-0xa05f-r) (2 × 13)
- [RES_0XA079_R](#table-res-0xa079-r) (1 × 13)
- [RES_0XA07A_R](#table-res-0xa07a-r) (3 × 13)
- [RES_0XA089_R](#table-res-0xa089-r) (1 × 13)
- [RES_0XD029_D](#table-res-0xd029-d) (8 × 10)
- [RES_0XD035_D](#table-res-0xd035-d) (4 × 10)
- [RES_0XD0CE_D](#table-res-0xd0ce-d) (13 × 10)
- [RES_0XD0D3_D](#table-res-0xd0d3-d) (3 × 10)
- [RES_0XD0E1_D](#table-res-0xd0e1-d) (9 × 10)
- [RES_0XD0E3_D](#table-res-0xd0e3-d) (3 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (21 × 16)
- [TAB_ANTENNE_ECALL](#table-tab-antenne-ecall) (4 × 2)
- [TAB_BUB_LADUNG_ART](#table-tab-bub-ladung-art) (6 × 2)
- [TAB_NO_YES](#table-tab-no-yes) (3 × 2)
- [TAB_RET_STATUS](#table-tab-ret-status) (4 × 2)
- [TAB_SOS_CAN_BOTSCHAFT](#table-tab-sos-can-botschaft) (2 × 2)
- [TAB_SOS_DEAKTIVIERUNG](#table-tab-sos-deaktivierung) (2 × 2)
- [TAB_TASTER_STATUS](#table-tab-taster-status) (4 × 2)
- [TAB_TDAACTIVATIONSTATE](#table-tab-tdaactivationstate) (5 × 2)
- [TAB_TESTSTATUS](#table-tab-teststatus) (6 × 2)
- [TANTENNEFEHLERART](#table-tantennefehlerart) (6 × 2)
- [TGPSSTATUS](#table-tgpsstatus) (14 × 2)
- [TPROVISIONINGSTATUS](#table-tprovisioningstatus) (5 × 2)
- [TPROVISIONINGSTATUSECALL](#table-tprovisioningstatusecall) (6 × 2)
- [TRESETSTATUS](#table-tresetstatus) (6 × 2)
- [TSIMSTATUS](#table-tsimstatus) (8 × 2)
- [TVERBAUCECALL](#table-tverbaucecall) (13 × 2)
- [TSTATEECALLLOG](#table-tstateecalllog) (60 × 2)
- [TEVENTECALLLOG](#table-teventecalllog) (98 × 2)
- [TEVENTRTSLOG](#table-teventrtslog) (14 × 2)
- [TCATEGORIESRTSLOG](#table-tcategoriesrtslog) (5 × 2)
- [TCONTEXTTYPERTSLOG](#table-tcontexttypertslog) (5 × 2)
- [THTTPREQUESTTYPE](#table-thttprequesttype) (18 × 2)
- [THTTPRESPONSETYPE](#table-thttpresponsetype) (16 × 2)
- [TBEARER](#table-tbearer) (3 × 2)
- [TCLAMPSTATE](#table-tclampstate) (16 × 2)
- [TPOWERMODE](#table-tpowermode) (5 × 2)
- [TRPCERRORCAUSE](#table-trpcerrorcause) (4 × 2)
- [TVEHICLEEVENT](#table-tvehicleevent) (3 × 2)
- [TCALLSTATUS](#table-tcallstatus) (9 × 2)
- [TDATASERVICETYPE](#table-tdataservicetype) (4 × 2)
- [TDATACALLSTATUS](#table-tdatacallstatus) (10 × 2)
- [TLANGCALLSTATUS](#table-tlangcallstatus) (9 × 2)
- [TERRORMESSAGE](#table-terrormessage) (15 × 2)
- [TBLOCKCALLSTATE](#table-tblockcallstate) (6 × 2)
- [TTELEEVENTTYPE](#table-tteleeventtype) (7 × 2)
- [TPOWERGUARDNAD](#table-tpowerguardnad) (16 × 2)
- [TPOWERSTATENAD](#table-tpowerstatenad) (75 × 2)
- [TPOWERTRIGGERNAD](#table-tpowertriggernad) (73 × 2)
- [TPOWERSTMNAD](#table-tpowerstmnad) (5 × 2)

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

Dimensions: 137 rows × 2 columns

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
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | KYOCERA Display Corporation |
| 0x0000B9 | MAGNA Powertrain AG & Co KG |
| 0x0000BA | BorgWarner |
| 0x0000BB | BMW - Fahrzeugsimulator |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin |
| 0x0000BE | Schaeffler Technologies |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 35 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x21 | Fehler momentan vorhanden und bereits gespeichert |
| 0x24 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x25 | Fehler momentan vorhanden und bereits gespeichert |
| 0x28 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x29 | Fehler momentan vorhanden und bereits gespeichert |
| 0x2C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x2D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x60 | Fehler gespeichert |
| 0x61 | Fehler gespeichert |
| 0x64 | Fehler gespeichert |
| 0x65 | Fehler gespeichert |
| 0x68 | Fehler gespeichert |
| 0x69 | Fehler gespeichert |
| 0x6C | Fehler gespeichert |
| 0x6D | Fehler gespeichert |
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

<a id="table-arg-0xa020-r"></a>
### ARG_0XA020_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_TYPE | + | - | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | There can only have two Values for the argument: BMW or BROWSER ARG_TYPE =  BMW  or  BROWSER  |
| ARG_PATH | + | - | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | path of the certificate |

<a id="table-arg-0xa05f-r"></a>
### ARG_0XA05F_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_VERBAU_ROUTINE | + | - | 0-n | - | unsigned long | - | TVerbauCECALL | - | - | - | - | - | Routinen, die getestet werden sollen Tabelle TVerbauCECALL |

<a id="table-arg-0xa086-r"></a>
### ARG_0XA086_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_FREQUENZ | + | - | Hz | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Frequenz in Hertz. Bereich 400 bis 3400 Hz. Sonst Request out of range |
| ARG_LAUTSTAERKE | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Lautstaerke von 0-15. Minimal- und Maximalbereich eincodiert. Bei ungueltigen Einganben kommt Request out of range |
| ARG_DAUER | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 255.0 | Dauer des Tons. Wertebereich von 0 bis 255 |

<a id="table-arg-0xa089-r"></a>
### ARG_0XA089_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SOS_DEAKTIVIERUNG | + | - | 0-n | high | unsigned char | - | TAB_SOS_DEAKTIVIERUNG | - | - | - | - | - | 0x00 aktiviert und 0x01 deaktiviert das Senden von SOS-Botschaften über CAN |

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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 40 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x026100 | Energiesparmode aktiv | 0 |
| 0x026108 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x026109 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02610A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02610B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 |
| 0x02610C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x02FF61 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0xB7F30D | Keine Kommunikation mit GPS-Empfänger | 0 |
| 0xB7F311 | Kein Zugriff auf interne SIM-Karte | 0 |
| 0xB7F313 | SIM-Karte gesperrt | 0 |
| 0xB7F318 | Notruf-LED Fehler | 0 |
| 0xB7F319 | Notruf-Taster: Kurzschluss | 0 |
| 0xB7F31A | Notruf-Taster: Unterbrechung | 0 |
| 0xB7F31B | Mikrofon 1: Kurzschluss nach Plus | 0 |
| 0xB7F320 | Hardware Reset | 0 |
| 0xB7F321 | Software Reset | 0 |
| 0xB7F323 | Alive Signal Airbag fehlerhaft | 1 |
| 0xB7F324 | Notruf-Lautsprecher: Kurzschluss nach Plus | 0 |
| 0xB7F325 | Notruf-Lautsprecher: Unterbrechung | 0 |
| 0xB7F326 | Notruf-Lautsprecher: Kurzschluss nach Masse | 0 |
| 0xB7F327 | Mikrofon 1: Kurzschluss nach Masse | 0 |
| 0xB7F328 | Mikrofon 1: Unterbrechung | 0 |
| 0xB7F32E | Mikrofon 1: Leitungen kurzgeschlossen | 0 |
| 0xB7F335 | Interner Steuergerätefehler Hardware | 0 |
| 0xB7F336 | Interner Steuergerätefehler Software | 0 |
| 0xB7F338 | Alive Signal Airbag fehlt | 1 |
| 0xB7F339 | Unterspannung erkannt | 1 |
| 0xB7F33A | Überspannung erkannt | 1 |
| 0xB7F33E | Automatischer Notruf häufig ausgelöst | 1 |
| 0xB7F33F | Notruf durch Diagnose deaktiviert | 0 |
| 0xB7F341 | Backup-Batterie: Hardware defekt | 0 |
| 0xB7F342 | Notruf-Lautsprecher: Leitungen kurzgeschlossen | 0 |
| 0xB7F343 | Backup-Batterie:  Before end of life | 0 |
| 0xB7F347 | Provisionierung ohne Signatur Diagnose | 0 |
| 0xB7F348 | Provisionierung ohne Signatur OTA | 0 |
| 0xB7F349 | Zertifikat ohne Signatur | 0 |
| 0xE14415 | IuK- oder Body-CAN Physikalischer Busfehler | 0 |
| 0xE1441E | IuK- oder Body-CAN Control Module Bus OFF | 0 |
| 0xE14BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | Text | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 93 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x101772 | CANTP_E_OPER_NOT_SUPPORTED | 0 |
| 0x101773 | CANSM_E_MODE_CHANGE_NETWORK_0 | 0 |
| 0x101774 | CANSM_E_SETTRSCVMODE_NETWORK_0 | 0 |
| 0x230004 | Kommunikation Einschlafkoordinator: Zeitüberschreitung | 1 |
| 0x610002 | Puffer für ausgehende Fehlermeldungen ist voll | 1 |
| 0x610003 | Fehler konnte nach maximaler Anzahl von Versuchen nicht gesendet werden | 1 |
| 0x610004 | Ungültiges Signal in CAN-Botschaft RELATIVZEIT | 0 |
| 0x610005 | Botschaft (Fahrzeugzustand, 0x3A0) fehlt | 1 |
| 0x610006 | CANIF_E_FULL_TX_BUFFER | 0 |
| 0x610007 | CANIF_E_STOPPED | 0 |
| 0x610008 | CANNM_E_CANIF_TRANSMIT_ERROR | 0 |
| 0x610009 | CAN NM Zeitüberschreitung | 0 |
| 0x61000A | CANNM_E_INIT_FAILED | 0 |
| 0x61000B | CANTP_E_COMM | 0 |
| 0x61000C | CAN Transceiver ungültiger Zustand | 0 |
| 0x61000E | CAN_E_TIMEOUT | 0 |
| 0x610011 | COMM_E_NET_START_IND_CHANNEL_0 | 0 |
| 0x610012 | ECUM_E_ALL_RUN_REQUESTS_KILLED | 0 |
| 0x610015 | WDG_E_DISABLE_REJECTED | 0 |
| 0x610016 | WDGM_E_SET_MODE | 0 |
| 0x610019 | NVM_E_INTEGRITY_FAILED | 0 |
| 0x61001A | NVM_E_REQ_FAILED | 0 |
| 0x61001B | MCU_E_CLOCK_FAILURE | 0 |
| 0x61001C | WDGM_E_ALIVE_SUPERVISION | 0 |
| 0x61001D | IPDUM_E_TRANSMIT_FAILED | 0 |
| 0x610021 | Backup-Batterie: Kurzschluss nach 12 Volt | 0 |
| 0x610022 | Backup-Batterie: Kurzschluss nach Masse | 0 |
| 0x610023 | Backup-Batterie: Unterbrechung | 0 |
| 0x610025 | Backup-Batterie: End of life | 0 |
| 0x610026 | EEPROM Kommunikationsfehler | 0 |
| 0x610028 | RAM Test fehlgeschlagen | 0 |
| 0x610029 | CAN-Interface - DLC ungültig | 0 |
| 0x61002A | Zeitüberschreitung CAN-Botschaft CON_VEH | 0 |
| 0x61002B | Ungültiges Signal in CAN-Botschaft CON_VEH | 0 |
| 0x61002C | Ungültiges Signal in CAN-Botschaft DWA_ALARM | 0 |
| 0x61002D | Ungültiges Signal in CAN-Botschaft TELM_FN_TR | 0 |
| 0x61002E | Ungültiges Signal in CAN-Botschaft TS_CALL_TR | 0 |
| 0x61002F | Ungültiges Signal in CAN-Botschaft TS_TR_ST | 0 |
| 0x610030 | ECall deaktiviert | 0 |
| 0x610031 | HW Version oder Variantenfehler | 0 |
| 0x610032 | Keine Kommunikation mit NAD nach Startup | 0 |
| 0x610033 | Kommunikation mit NAD dauerhaft gestört | 0 |
| 0x610034 | Falsche NGTP Keytable | 0 |
| 0x610036 | ROM Test fehlgeschlagen | 0 |
| 0x610037 | Interner Spannungsfehler 9V0 | 0 |
| 0x610038 | Interner Spannungsfehler 4V5 | 0 |
| 0x610039 | Interner Spannungsfehler 3V8 | 0 |
| 0x61003A | Interner Spannungsfehler 5V0 | 0 |
| 0x61003B | Fehlerhafte Referenzspannung 2,5 Volt | 0 |
| 0x930000 | Alive Signal Airbag: Prüfsummenfehler | 1 |
| 0xB7F305 | MCU_E_LOCK_FAILURE | 0 |
| 0xB7F314 | SIM-Karte nicht freigeschaltet | 0 |
| 0xB7F322 | Alive Signal Airbag fehlt beim Aufstart | 1 |
| 0xB7F337 | Alive Signal Airbag fehlerhaft beim Aufstart | 1 |
| 0xB7F33B | Interner Steuergerätefehler | 0 |
| 0xB7F346 | WDG_E_MODE_SWITCH_FAILED | 0 |
| 0xE14400 | Zeitüberschreitung CAN-Botschaft A_TEMP | 1 |
| 0xE14401 | Zeitüberschreitung CAN-Botschaft BEDIENUNG_AUDIO_TEL | 1 |
| 0xE14402 | Zeitüberschreitung CAN-Botschaft DT_PT_2 | 1 |
| 0xE14403 | Zeitüberschreitung CAN-Botschaft EINHEITEN | 1 |
| 0xE14404 | Zeitüberschreitung CAN-Botschaft FLLUPT_GPWSUP | 1 |
| 0xE14405 | Zeitüberschreitung CAN-Botschaft MILE_VEH | 1 |
| 0xE14408 | Zeitüberschreitung CAN-Botschaft KILOMETERSTAND | 1 |
| 0xE14409 | Zeitüberschreitung CAN-Botschaft KLEMMEN | 1 |
| 0xE1440C | Zeitüberschreitung CAN-Botschaft POWERMGMT_CTR_COS | 1 |
| 0xE1440D | Zeitüberschreitung CAN-Botschaft STEA_FTAX_EFFV | 1 |
| 0xE1440E | Zeitüberschreitung CAN-Botschaft UHRZEIT_DATUM | 1 |
| 0xE1440F | Zeitüberschreitung CAN-Botschaft VYAW_VEH | 1 |
| 0xE14411 | Zeitüberschreitung CAN-Botschaft V_VEH | 1 |
| 0xE14412 | Zeitüberschreitung CAN-Botschaft LAMPENZUSTAND | 1 |
| 0xE14413 | Zeitüberschreitung CAN-Botschaft STAT_GANG_RUECKWAERTS | 1 |
| 0xE14414 | Zeitüberschreitung CAN-Botschaft STAT_ZV_KLAPPEN | 1 |
| 0xE14420 | Ungültiges Signal in CAN-Botschaft BEDIENUNG_AUDIO_TEL | 1 |
| 0xE14421 | Ungültiges Signal in CAN-Botschaft CRASH | 1 |
| 0xE14422 | Ungültiges Signal in CAN-Botschaft CTR_CR | 1 |
| 0xE14423 | Ungültiges Signal in CAN-Botschaft DT_PT_2 | 1 |
| 0xE14424 | Ungültiges Signal in CAN-Botschaft EINHEITEN | 1 |
| 0xE14425 | Ungültiges Signal in CAN-Botschaft FLLUPT_GPWSUP | 1 |
| 0xE14427 | Ungültiges Signal in CAN-Botschaft KLEMMEN | 1 |
| 0xE1442A | Ungültiges Signal in CAN-Botschaft OP_ROCO_AVOL | 1 |
| 0xE1442B | Ungültiges Signal in CAN-Botschaft POWERMGMT_CTR_COS | 1 |
| 0xE1442C | Ungültiges Signal in CAN-Botschaft STAT_ZV_KLAPPEN | 1 |
| 0xE1442D | Ungültiges Signal in CAN-Botschaft STEA_FTAX_EFFV | 1 |
| 0xE1442E | Ungültiges Signal in CAN-Botschaft TELM_SER_CTR | 1 |
| 0xE1442F | Ungültiges Signal in CAN-Botschaft UHRZEIT_DATUM | 1 |
| 0xE14430 | Ungültiges Signal in CAN-Botschaft VYAW_VEH | 1 |
| 0xE14431 | Ungültiges Signal in CAN-Botschaft V_VEH | 1 |
| 0xE14432 | Ungültiges Signal in CAN-Botschaft DT_BAT | 1 |
| 0xE14433 | Ungültiges Signal in CAN-Botschaft STAT_GANG_RUECKWAERTS | 1 |
| 0xE14434 | Ungültiges Signal in CAN-Botschaft A_TEMP | 1 |
| 0xE14438 | Ungültiges Signal in CAN-Botschaft KILOMETERSTAND | 1 |
| 0xE1443A | Ungültiges Signal in CAN-Botschaft MILE_VEH | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 2 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 01 | ERROR_MISSING_ARGUMENT |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0xa020-r"></a>
### RES_0XA020_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RET_STATUS | + | - | + | 0-n | high | unsigned char | - | TAB_RET_STATUS | - | - | - | Status message |

<a id="table-res-0xa05e-r"></a>
### RES_0XA05E_R

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANTENNE | - | - | + | 0-n | high | unsigned char | - | TAB_ANTENNE_ECALL | - | - | - | gibt an, welche Antenne getestet wurden |
| STAT_TEST_ANTENNE | - | - | + | 0-n | high | unsigned char | - | TAB_TESTSTATUS | - | - | - | Gibt den Status des gesamten Tests der entsprechenden Antenne wieder Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt |
| STAT_FEHLERART_ANTENNE | - | - | + | 0-n | high | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet |
| STAT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | der auf der fehlerhaften Antenne gemessene Widerstand in 0.1 kOhm. |

<a id="table-res-0xa05f-r"></a>
### RES_0XA05F_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAU_ROUTINE | - | - | + | 0-n | - | unsigned long | - | TVerbauCECALL | - | - | - | Ausgeführte Testroutine(n) |
| STAT_TEST_VERBAU | - | - | + | 0-n | - | unsigned char | - | TAB_TESTSTATUS | - | - | - | Gibt den Status des Verbautests wieder Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt |

<a id="table-res-0xa079-r"></a>
### RES_0XA079_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PROVISIONING_RESET | - | - | + | 0-n | - | unsigned char | - | TResetStatus | - | - | - | Status Reset Werte gemäß Tabelle TResetStatus 0 UNKNOWN - unbekannt 1 ACTIVE - läuft noch 2 SUCCESS - alles OK 3 FAILED - mit Fehler beendet 4 IDLE - wurde nicht gestartet |

<a id="table-res-0xa07a-r"></a>
### RES_0XA07A_R

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PROVISIONING | - | - | + | 0-n | - | unsigned char | - | TProvisioningStatusEcall | - | - | - | Status des Provisionierungsprozess Werte gemäß Tabelle TProvisioningStatusEcall |
| STAT_ECALL_OTA_ID_TEXT | - | - | + | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | Version von den aktuellen OTA Daten |
| STAT_ECALL_DAS_ID_TEXT | - | - | + | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | Version von den aktuellen DAS Daten |

<a id="table-res-0xa089-r"></a>
### RES_0XA089_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SOS_CAN_BOTSCHAFT | - | - | + | 0-n | high | unsigned char | - | TAB_SOS_CAN_BOTSCHAFT | 1.0 | 1.0 | 0.0 | Auslesen des aktuellen Status des Signalmodus (siehe Job STEUERN_SIGNAL_MODE) |

<a id="table-res-0xd029-d"></a>
### RES_0XD029_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BUB_SPANNUNG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batteriespannung als Wert in Millivolt |
| STAT_BUB_TEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Batterietemperatur in C° |
| STAT_BUB_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Status gibt an ob Steuergerät auf Betrieb mit BUB oder ohne codiert ist. 0 = nicht verbaut 1 = verbaut |
| STAT_BUB_SOH_WERT | % | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Relative Health der Backup-Batterie (State of Health) |
| STAT_BUB_JAHR_HEALTH_MESSUNG_WERT | - | high | int | - | - | 1.0 | 1000.0 | 0.0 | Datum der Relative Health Messung der Backup-Batterie. Ergebnis Jahr (Format: JJJJ) |
| STAT_BUB_MONAT_HEALTH_MESSUNG_WERT | - | high | int | - | - | 1.0 | 1000.0 | 0.0 | Datum der Relative Health Messung der Backup-Batterie. Ergebnis Monat (Format: MM) |
| STAT_BUB_TAG_HEALTH_MESSUNG_WERT | - | high | int | - | - | 1.0 | 1000.0 | 0.0 | Datum der Relative Health Messung der Backup-Batterie. Ergebnis Tag (Format: TT) |
| STAT_BUB_LADUNG_ART | 0-n | high | unsigned char | - | TAB_BUB_LADUNG_ART | - | - | - | Gibt das aktuelle Ladungsverfahren an. |

<a id="table-res-0xd035-d"></a>
### RES_0XD035_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SIM_STATUS | 0-n | high | unsigned char | - | TSimStatus | - | - | - | Status der SIM-Karte |
| STAT_IP_ADRESSE_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | IP-Adresse z.B. 192.168.0.1 |
| STAT_AKTUELLES_NETZ_TEXT | TEXT | high | string[6] | - | - | 1.0 | 1.0 | 0.0 | Status des aktuell verfügbaren Netzwerks 000 000 = NMCC NMNC Nmcc= network mobile country code (Land) Nmnc= network mobile network code (Network provider) |
| STAT_SIGNAL_STAERKE_TEXT | TEXT | high | string[1] | - | - | 1.0 | 1.0 | 0.0 | Empfangsstärke des verfügbaren Netzwerks im Bereich von 0-5 0 = kein Signal 5 = volles Signal |

<a id="table-res-0xd0ce-d"></a>
### RES_0XD0CE_D

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHORT_VIN_TEXT | TEXT | high | string[7] | - | - | 1.0 | 1.0 | 0.0 | 7-stellige Fahrgestellnummer |
| STAT_SMCC_TEXT | TEXT | high | string[3] | - | - | 1.0 | 1.0 | 0.0 | SIM Mobile Länderkode |
| STAT_SMNC_TEXT | TEXT | high | string[3] | - | - | 1.0 | 1.0 | 0.0 | SIM Mobile Netzwerkkode |
| STAT_NMCC_TEXT | TEXT | high | string[3] | - | - | 1.0 | 1.0 | 0.0 | Netzwerk Mobile Länderkode |
| STAT_NMNC_TEXT | TEXT | high | string[3] | - | - | 1.0 | 1.0 | 0.0 | Netzwerk Mobile Netzwerkkode |
| STAT_VERSION_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Version des Steuergerätes und des Provisionierungsmanagers |
| STAT_OTA_ID_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | OTA - ID |
| STAT_DAS_ID_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | DAS - ID |
| STAT_CAUSE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Cause Wert Der Wert gibt den Auslöser der Provisionierung an. 0: Required access data is missing in the DASAS data 1: A required OTAAS is expired 2: Update request by user via the HMI  3: Application trigger 4: The PINGUIN triggered the provisioning  5: ACM triggered provisioning on DPAS Mode 6: Provisioning via Diagnosis |
| STAT_DPAS_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Provisionierungszustand |
| STAT_ICC_ID_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | ICC - ID |
| STAT_IMEI_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | IMEI |
| STAT_SERIAL_NUMBER_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Seriennummer des Steuergeräts |

<a id="table-res-0xd0d3-d"></a>
### RES_0XD0D3_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHORT_VIN_TEXT | TEXT | high | string[7] | - | - | 1.0 | 1.0 | 0.0 | 7-stellige Fahrgestellnummer |
| STAT_DOWNLOAD_ID_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Download ID |
| STAT_PROVISIONING | 0-n | high | unsigned char | - | TProvisioningStatus | - | - | - | Status vom Schreibvorgang der Provisionierungsdaten. |

<a id="table-res-0xd0e1-d"></a>
### RES_0XD0E1_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GPS_RECEIVER_SW_VERSION_TEXT | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | Auslesen der Software Versionsnummer des GPS Receivers |
| STAT_GPS | 0-n | - | unsigned char | - | TGpsStatus | - | - | - | Liest den GPS Status. Siehe Tabelle TGpsStatus. |
| STAT_GPS_LONG_WERT | - | high | long | - | - | 1.0 | 1.0 | 0.0 | Längengrad |
| STAT_GPS_LAT_WERT | - | high | long | - | - | 1.0 | 1.0 | 0.0 | Breitengrad |
| STAT_GPS_HEADING_WERT | ° | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Richtung in Grad |
| STAT_GPS_SPEED_WERT | m/s | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Geschwindigkeit in m pro Sekunde. Steuergerät sendet in cm/s, in der SGBD wird auf m/s umgerechnet |
| STAT_GPS_HEIGHT_WERT | m | high | int | - | - | 1.0 | 1.0 | 0.0 | Höhe in Meter |
| STAT_GPS_DATE_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum TTMMJJJJ |
| STAT_GPS_TIME_TEXT | TEXT | high | string[6] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit HHMMSS |

<a id="table-res-0xd0e3-d"></a>
### RES_0XD0E3_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GPS_DISTANCE_1_WERT | m | high | long | - | - | 1.0 | 1.0 | 0.0 | Gibt die zurückgelegte Strecke (GPS) seit dem letzten Auslesen des Jobs aus. |
| STAT_GPS_DISTANCE_2_WERT | m | high | long | - | - | 1.0 | 1.0 | 0.0 | Gibt die zurückgelegte Strecke (GPS) seit dem zweitletzten Auslesen des Jobs aus. |
| STAT_GPS_DISTANCE_3_WERT | m | high | long | - | - | 1.0 | 1.0 | 0.0 | Gibt die zurückgelegte Strecke (GPS) seit dem drittletzten Auslesen des Jobs aus. |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 21 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| UNIVERSAL_TRANSPORT_LAYER | 0xA020 | - | Dummy für UTL Transport-Schicht | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA020_R | RES_0xA020_R |
| TEST_ANTENNE_ECALL | 0xA05E | - | Startet und bewertet die Prüfung für eine definierte Antenne | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA05E_R |
| TEST_VERBAU_ECALL | 0xA05F | - | Test Verbau CECALL | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA05F_R | RES_0xA05F_R |
| PROVISIONING_RESET | 0xA079 | - | Setzt die standard Telematik Konfigurationswerte zurück und löscht die OTA (Over The Air) Daten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA079_R |
| PROVISIONING_ECALL | 0xA07A | - | Startet die Provisionierung der Telematikdienste OTA | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA07A_R |
| SOS_SPEAKER_TEST | 0xA086 | - | Spielt einen Ton mit parametrierbarer Frequenz, Dauer, Lautstärke auf dem SOS-Lautsprecher ab | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA086_R | - |
| SIGNAL_MODE_ECALL | 0xA089 | - | Aktiviert bzw. deaktiviert das Senden von SOS-Botschaften (via CAN) zu Testzwecken des SOS-Tasters | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA089_R | RES_0xA089_R |
| BACKUP_BATTERIE | 0xD029 | - | Backup-Batterie | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD029_D |
| LAST_CONNECTION_TEL | 0xD035 | - | Auslesen des SIM Status und IP Adresse der letzte Verbindung Argument beschreibt welches Gerät für das die letze Verbindung abgefragt wird | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD035_D |
| ICC_ID_LESEN | 0xD05A | STAT_ICC_ID_TEXT | Auslesen des ICC (Integrated Circuit Card) -ID des internen Telefonmoduls | TEXT | - | - | string | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| IMEI_LESEN | 0xD06B | STAT_IMEI_TEXT | Auslesen des IMEI (International Mobile Equipment Identity) des internen Telefonmoduls | TEXT | - | - | string | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NAD_FIRMWARE_VERSION | 0xD06D | STAT_NAD_FIRMWARE_VERSION_TEXT | Auslesen der Firmware Version des NAD (Network Access Module) | TEXT | - | - | string | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NAD_USERWARE_VERSION | 0xD06E | STAT_NAD_USERWARE_VERSION_TEXT | Auslesen der Userware Version des NAD (Network Access Module) | TEXT | - | - | string | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_TDA_AKTIVIERUNG | 0xD091 | STAT_DIENSTE_AKTIVIERUNG | Status TDA BMW Dienste | 0-n | - | - | unsigned char | TAB_TDAActivationState | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SOS_TASTER | 0xD09B | STAT_SOS_TASTER | Gibt an, ob der SOS-Taster gedrückt (0x01) oder nicht gedrückt (0x00) ist. | 0-n | - | high | unsigned char | TAB_TASTER_STATUS | - | - | - | - | 22 | - | - |
| PROVISIONING_PARAMETER | 0xD0CE | - | Liest die Parameter der Provisionierung aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD0CE_D |
| PROVISIONING_DATA | 0xD0D3 | - | Liest Status des Schreibens der Provisionierungsdatei. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD0D3_D |
| SELBSTTEST | 0xD0D7 | STAT_SELBSTTEST | Gibt den Status des Tests wieder. | 0-n | - | - | unsigned char | TAB_TESTSTATUS | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_GPS_ECALL | 0xD0E1 | - | GPS Status des Telematiksteuergeräts. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD0E1_D |
| STATUS_GPS_DISTANCE | 0xD0E3 | - | Zurückgelegte Strecke gemessen über GPS. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD0E3_D |
| PROVISIONING_FORMAT | 0xD0EB | STAT_STAT_SIGNATURE | dient dazu, eine signierte Bereitstellungsdatei zu verstehen  | 0-n | - | high | unsigned char | TAB_NO_YES | - | - | - | - | 22 | - | - |

<a id="table-tab-antenne-ecall"></a>
### TAB_ANTENNE_ECALL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | GSM_Telematik |
| 0x02 | GSM_Backup |
| 0x04 | GPS_Antenne |
| 0xFF | Ungültig |

<a id="table-tab-bub-ladung-art"></a>
### TAB_BUB_LADUNG_ART

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ladung BUB aus |
| 0x01 | Normale Ladung |
| 0x02 | Erhaltungsladung |
| 0x03 | Keine Ladung: Voll geladen |
| 0x04 | Keine Ladung: Temperatur |
| 0x05 | Keine Ladung: BUB Betrieb |

<a id="table-tab-no-yes"></a>
### TAB_NO_YES

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | no |
| 0x01 | yes |
| 0xFF | not defined |

<a id="table-tab-ret-status"></a>
### TAB_RET_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | prepostprocessing neg. response |
| 0x02 | prepostprocessing timeout |
| 0x03 | ret_data exceeds 0xF000 bytes |

<a id="table-tab-sos-can-botschaft"></a>
### TAB_SOS_CAN_BOTSCHAFT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SOS-Botschaften werden gesendet |
| 0x01 | SOS-Botschaften werden nicht gesendet |

<a id="table-tab-sos-deaktivierung"></a>
### TAB_SOS_DEAKTIVIERUNG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Senden von SOS-Nachrichten aktivieren |
| 0x01 | Senden von SOS-Nachrichten deaktivieren |

<a id="table-tab-taster-status"></a>
### TAB_TASTER_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Taste nicht betätigt |
| 0x01 | Taste betätigt |
| 0x02 | nicht verbaut oder codiert |
| 0xFF | Ungültig |

<a id="table-tab-tdaactivationstate"></a>
### TAB_TDAACTIVATIONSTATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Leerlauf, derzeit nicht aktiv |
| 0x02 | Aktivierung läuft |
| 0x03 | Aktivierung fehlgeschlagen |
| 0x04 | Aktivierung erfolgreich |
| 0xFF | nicht definiert |

<a id="table-tab-teststatus"></a>
### TAB_TESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tantennefehlerart"></a>
### TANTENNEFEHLERART

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | AntennaDisconnectedFromAntennaAmplifier |
| 0x03 | Falscher Antennfuß oder Diversity |
| 0x04 | Antenne nicht gesteckt ( nur für BT- Antenne 12-07) |
| 0xFF | Nicht definiert |

<a id="table-tgpsstatus"></a>
### TGPSSTATUS

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht unterstuetzt: Kein GPS |
| 0x01 | Nicht unterstuetzt: Kommunikationsfehler |
| 0x02 | Receiverfehler |
| 0x03 | Kein almanac |
| 0x04 | Suche Satelliten |
| 0x05 | Ortung Satellit 1 |
| 0x06 | Ortung Satellit 2 |
| 0x07 | Ortung Satellit 3 |
| 0x08 | Ortung Satellit 4 |
| 0x09 | Ortung Satellit 5 |
| 0x0A | Ortung Satellit 6 |
| 0x0B | 2D Position |
| 0x0C | 3D Position |
| 0xFF | Nicht definiert |

<a id="table-tprovisioningstatus"></a>
### TPROVISIONINGSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | IDLE wurde nicht gestartet |
| 0x01 | ACTIVE laeuft noch |
| 0x02 | SUCCESS alles OK |
| 0x03 | mit Fehler beendet |
| 0xFF | Nicht definiert |

<a id="table-tprovisioningstatusecall"></a>
### TPROVISIONINGSTATUSECALL

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | unbekannt |
| 0x01 | läuft noch |
| 0x02 | alles OK |
| 0x03 | mit Fehler beendet |
| 0x04 | wurde nicht gestartet |
| 0xFF | nicht definiert |

<a id="table-tresetstatus"></a>
### TRESETSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | unbekannt |
| 0x01 | läuft noch |
| 0x02 | alles OK |
| 0x03 | mit Fehler |
| 0x04 | wurde nicht gestartet |
| 0xFF | undefinierter Zustand |

<a id="table-tsimstatus"></a>
### TSIMSTATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xff | undefinierter Status |
| 0x00 | nicht eingebucht, sucht kein Netz |
| 0x01 | eingebucht |
| 0x02 | nicht eingebucht, sucht ein Netz |
| 0x03 | einbuchen verweigert |
| 0x04 | eingebucht und roaming |
| 0x05 | eingebucht und roaming off-net |
| 0x10 | Emergency Call bereit |

<a id="table-tverbaucecall"></a>
### TVERBAUCECALL

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle |
| 0x00000001 | GSM-Telematik |
| 0x00000002 | GSM-Backup |
| 0x00000004 | GPS-Antenne |
| 0x00000008 | Backup-Lautsprecher |
| 0x00000010 | E-Call-Button |
| 0x00000020 | E-Call-LED |
| 0x00000040 | E-Batterie |
| 0x00000080 | Airbag-Leitung |
| 0x00000100 | Wakeup-Leitung-CAS |
| 0x00000200 | Mikrophon1 |
| 0x00000400 | Mikrophon2 |
| 0xFFFFFFFF | nicht definiert |

<a id="table-tstateecalllog"></a>
### TSTATEECALLLOG

Dimensions: 60 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | DEFAULT |
| 0x7D00 | ECALL_SOURCE_UNKNOWN |
| 0x7D01 | ECALL_SOURCE_HARDKEY |
| 0x7D02 | ECALL_SOURCE_AIRBAG |
| 0x7D03 | ECALL_SOURCE_EXTERNAL |
| 0x7D04 | ECALL_SOURCE_MOST |
| 0x7D05 | ECALL_SOURCE_CAN_CRASH |
| 0x7D06 | ECALL_SOURCE_USER_ABORT |
| 0x7E01 | CLAMP_RESERVE |
| 0x7E02 | CLAMP_30 |
| 0x7E03 | CLAMP_30F_CHANGE |
| 0x7E04 | CLAMP_30_ON |
| 0x7E05 | CLAMP_30B_CHANGE |
| 0x7E06 | CLAMP_30B_ON |
| 0x7E07 | CLAMP_R_CHANGE |
| 0x7E08 | CLAMP_R_ON |
| 0x7E09 | CLAMP_15_CHANGE |
| 0x7E0A | CLAMP_15_ON |
| 0x7E0B | CLAMP_50_DELAY |
| 0x7E0C | CLAMP_50_CHANGE |
| 0x7E0D | CLAMP_50_ON |
| 0x7E0E | CLAMP_ERROR |
| 0x7E0F | CLAMP_INVALID |
| 0x7F00 | MOVEMENT_NO |
| 0x7F01 | MOVEMENT_YES |
| 0x8000 | WAKEUP_REASON_UNKNOWN |
| 0x8001 | WAKEUP_REASON_REGULAR |
| 0x8002 | WAKEUP_REASON_REMOTE |
| 0x8100 | ENGINE_OFF |
| 0x8101 | ENGINE_ON |
| 0x8200 | ANTENNA_UNKNOWN |
| 0x8201 | ANTENNA_MAIN |
| 0x8202 | ANTENNA_BACKUP |
| 0x8300 | TERM_SOURCE_UNKNOWN |
| 0x8301 | TERM_SOURCE_MFL |
| 0x8302 | TERM_SOURCE_MMI |
| 0x8400 | TERM_REASON_UNKNOWN |
| 0x8401 | TERM_REASON_NETWORK |
| 0x8402 | TERM_REASON_HANGUP |
| 0x8500 | BEARER_UNKNOWN |
| 0x8501 | BEARER_SMS |
| 0x8502 | BEARER_INBAND |
| 0x8503 | BEARER_DTMF |
| 0x8600 | BATT_RELIABLE_NO |
| 0x8601 | BATT_RELIABLE_YES |
| 0x8700 | BUS_ACTIVE_NO |
| 0x8701 | BUS_ACTIVE_YES |
| 0x8800 | POWER_SOURCE_UNKNONW |
| 0x8801 | POWER_SOURCE_VEHICLE |
| 0x8802 | POWER_SOURCE_BACKUP_BATTERY |
| 0x8900 | REASON_PROVISIONING |
| 0x8901 | REASON_DIAG |
| 0x8902 | REASON_CODING |
| 0x8903 | REASON_MMI |
| 0x8904 | REASON_MMI_STARTUP |
| 0x8A00 | AUTO_ENABLED_ANY_NETWORK_NO |
| 0x8A01 | AUTO_ENABLED_ANY_NETWORK_YES |
| 0x8B00 | MAN_ENABLED_ANY_NETWORK_NO |
| 0x8B01 | MAN_ENABLED_ANY_NETWORK_YES |
| 0xFFFF | Nicht definiert |

<a id="table-teventecalllog"></a>
### TEVENTECALLLOG

Dimensions: 98 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DEFAULT |
| 0x01 | TIME_UPDATE_1 |
| 0x02 | TIME_UPDATE_2 |
| 0x03 | MILAGE_1 |
| 0x04 | MILAGE_2 |
| 0x05 | MILAGE_3 |
| 0x06 | MILAGE_4 |
| 0x07 | GPS_QUALITY_1 |
| 0x08 | GPS_QUALITY_2 |
| 0x09 | GPS_POS_LONGITUDE_1 |
| 0x0A | GPS_POS_LONGITUDE_2 |
| 0x0B | GPS_POS_LONGITUDE_3 |
| 0x0C | GPS_POS_LONGITUDE_4 |
| 0x0D | GPS_POS_LATITUDE_1 |
| 0x0E | GPS_POS_LATITUDE_2 |
| 0x0F | GPS_POS_LATITUDE_3 |
| 0x10 | GPS_POS_LATITUDE_4 |
| 0x11 | AIRBAG_CONTEXT |
| 0x12 | NETWORK_MCC_1 |
| 0x13 | NETWORK_MCC_2 |
| 0x14 | NETWORK_MCC_3 |
| 0x15 | NETWORK_MCC_4 |
| 0x16 | NETWORK_MNC_1 |
| 0x17 | NETWORK_MNC_2 |
| 0x18 | NETWORK_MNC_3 |
| 0x19 | NETWORK_MNC_4 |
| 0x1A | NETWORK_CELL_ID_1 |
| 0x1B | NETWORK_CELL_ID_2 |
| 0x1C | NETWORK_SIGNAL_STRENGTH_1 |
| 0x1D | NETWORK_SIGNAL_STRENGTH_2 |
| 0x1E | PHONE_NUMBER_DIGIT_1 |
| 0x1F | PHONE_NUMBER_DIGIT_2 |
| 0x20 | PHONE_NUMBER_DIGIT_3 |
| 0x21 | PHONE_NUMBER_DIGIT_4 |
| 0x22 | PHONE_NUMBER_DIGIT_5 |
| 0x23 | PHONE_NUMBER_DIGIT_6 |
| 0x24 | PHONE_NUMBER_DIGIT_7 |
| 0x25 | PHONE_NUMBER_DIGIT_8 |
| 0x26 | PHONE_NUMBER_DIGIT_9 |
| 0x27 | PHONE_NUMBER_DIGIT_10 |
| 0x28 | PHONE_NUMBER_DIGIT_11 |
| 0x29 | PHONE_NUMBER_DIGIT_12 |
| 0x2A | PHONE_NUMBER_DIGIT_13 |
| 0x2B | PHONE_NUMBER_DIGIT_14 |
| 0x2C | PHONE_NUMBER_DIGIT_15 |
| 0x2D | PHONE_NUMBER_DIGIT_16 |
| 0x2E | PHONE_NUMBER_DIGIT_17 |
| 0x2F | PHONE_NUMBER_DIGIT_18 |
| 0x30 | PHONE_NUMBER_DIGIT_19 |
| 0x31 | PHONE_NUMBER_DIGIT_20 |
| 0x32 | PHONE_NUMBER_DIGIT_21 |
| 0x33 | PHONE_NUMBER_DIGIT_22 |
| 0x34 | PHONE_NUMBER_DIGIT_23 |
| 0x35 | PHONE_NUMBER_DIGIT_24 |
| 0x36 | PHONE_NUMBER_DIGIT_25 |
| 0x37 | PHONE_NUMBER_DIGIT_26 |
| 0x38 | PHONE_NUMBER_DIGIT_27 |
| 0x39 | PHONE_NUMBER_DIGIT_28 |
| 0x3A | SUPPORTED_TYPE_PROVISIONING |
| 0x3B | SUPPORTED_TYPE_CODING |
| 0x4B | TIME_ECALL_TRIGGER_UPDATE |
| 0x4C | TIME_ECALL_ACTIVE |
| 0x4D | TIME_ECALL_ABORTED |
| 0x4E | TIME_NETWORK_REGISTRATION |
| 0x4F | TIME_ANTENNA_SWITCHED |
| 0x50 | TIME_FIRE_FORGET_SMS_STARTED |
| 0x51 | TIME_FIRE_FORGET_SMS_DELIVERED |
| 0x52 | TIME_VOICE_CALL_DIALING |
| 0x53 | TIME_VOICE_CALL_ESTABLISHED |
| 0x54 | TIME_VOICE_CALL_TERMINATED_USER |
| 0x55 | TIME_VOICE_CALL_TERMINATED_COMMAND |
| 0x56 | TIME_VOICE_CALL_TERMINATED_REMOTE |
| 0x57 | TIME_INCOMING_VOICE_CALL_ACCEPTED |
| 0x58 | TIME_EU_ECALL_DATA_TRANSMISSION_STARTED |
| 0x59 | TIME_EU_ECALL_DATA_TRANSMISSION_SUCCESS |
| 0x5A | TIME_ASSIST_ECALL_DATA_SEND_STARTED |
| 0x5B | TIME_ASSIST_ECALL_DATA_SEND_SUCCESS |
| 0x5C | TIME_ASSIST_ECALL_DATA_TRANSMISSION_SUCCESS |
| 0x5D | TIME_ECALL_INACTIVE |
| 0x5E | TIME_ECALL_STANDBY_STARTED |
| 0x5F | TIME_ECALL_STANDBY_ENDED |
| 0x60 | TIME_SWITCH_POWER_SUPPLY |
| 0x7D | TRIGGER_SOURCE |
| 0x7E | CLAMP_STATUS |
| 0x7F | VEH_MOVEMENT |
| 0x80 | LAST_WAKEUP_REASON |
| 0x81 | ENGINE_STATUS |
| 0x82 | SELECTED_ANTENNA |
| 0x83 | TERMINATION_SOURCE |
| 0x84 | TERMINATION_REASON |
| 0x85 | BEARER |
| 0x86 | VEH_BATTERY_STATUS |
| 0x87 | VEH_BUS_STATUS |
| 0x88 | NEW_POWER_SOURCE |
| 0x89 | DISABLE_ENABLE_REASON |
| 0x8A | NEW_STATUS_ECALL_AUTOMATIC |
| 0x8B | NEW_STATUS_ECALL_MANUAL |
| 0xFF | Nicht definiert |

<a id="table-teventrtslog"></a>
### TEVENTRTSLOG

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | CALL_CONTROL_NOTIFI |
| 0x01 | CALL_CONTROL_REQUEST |
| 0x02 | HTTP_REQUEST |
| 0x03 | HTTP_RESPONSE |
| 0x04 | PINGUIN_TRIGGER |
| 0x05 | RPC_INDICATION |
| 0x06 | RPC_REQUEST |
| 0x07 | RPC_TRIGGER |
| 0x08 | VEHICLE_EVENT |
| 0x09 | VEHICLE_CLAMPSTATE_EVENT |
| 0x0A | TS_CALL_STATES |
| 0x0B | START_RS_TRIGGER |
| 0x0C | START_TS_TRIGGER |
| 0xFF | Nicht definiert |

<a id="table-tcategoriesrtslog"></a>
### TCATEGORIESRTSLOG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | INVALID |
| 0x01 | INCOMING_TRIGGER |
| 0x02 | INCOMING_EVENT |
| 0x03 | OUTGOING_EVENT |
| 0xFF | Nicht definiert |

<a id="table-tcontexttypertslog"></a>
### TCONTEXTTYPERTSLOG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RS_EXTENDED |
| 0x01 | RS_BASIC |
| 0x02 | TS_EXTENDED |
| 0x03 | TS_BASIC |
| 0xFF | Nicht definiert |

<a id="table-thttprequesttype"></a>
### THTTPREQUESTTYPE

Dimensions: 18 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RS_GET_JOB |
| 0x01 | RS_GET_FINISH |
| 0x02 | RS_DOOR_UNLOCK |
| 0x03 | RS_DOOR_LOCK |
| 0x04 | RS_VEHICLEFINDER_POSITION |
| 0x05 | RS_VEHICLEFINDER_BLOWHORN |
| 0x06 | RS_VEHICLEFINDER_LIGHTFLASH |
| 0x07 | RS_CLIMATECONTROL |
| 0x08 | TS_AUTH_SERVER_CHALL |
| 0x09 | TS_AUTH_CLIENT_CHALL |
| 0x0A | TS_AUTH_ERROR |
| 0x0B | TS_START_SESSION |
| 0x0C | TS_PDM_RESULT |
| 0x0D | TS_DIAG_RESPONSE |
| 0x0E | TS_TERMINATE_SESSION_ERROR |
| 0x0F | TS_TERMINATE_SESSION_OK |
| 0x10 | TS_PROTOCOL_MESSAGE_ERROR |
| 0xFF | Nicht definiert |

<a id="table-thttpresponsetype"></a>
### THTTPRESPONSETYPE

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RS_DOOR_JOB |
| 0x01 | RS_VEHICLEFINDER_JOB |
| 0x02 | RS_CLIMATECONTROL_JOB |
| 0x03 | RS_FINISH |
| 0x04 | TS_AUTH_SERVER_RESP |
| 0x05 | TS_AUTH_CLIENT_OK |
| 0x06 | TS_AUTH_ERROR |
| 0x07 | TS_START_SESSION_OK |
| 0x08 | TS_TERMINATE_SESSION |
| 0x09 | TS_TERMINATE_SEESION_ERROR |
| 0x0A | TS_PROTOCOL_MESSAGE_ERROR |
| 0x0B | TS_SESSION_STATUS |
| 0x0C | TS_DIAG_REQUEST |
| 0x0D | TS_EXECUTE_PDM |
| 0x0E | TS_PDM_DOWNLOAD |
| 0xFF | Nicht definiert |

<a id="table-tbearer"></a>
### TBEARER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | BEARER_SMS |
| 0x01 | BEARER_HTTP |
| 0xFF | Nicht definiert |

<a id="table-tclampstate"></a>
### TCLAMPSTATE

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | INIT |
| 0x01 | RESERVE |
| 0x02 | KL30 |
| 0x03 | KL30F_CHANGE |
| 0x04 | KL30F_ON |
| 0x05 | KL30B_CHANGE |
| 0x06 | KL30B_ON |
| 0x07 | KLR_CHANGE |
| 0x08 | KLR_ON |
| 0x09 | KL15_CHANGE |
| 0x0A | KL15_ON |
| 0x0B | KL50_DELAY |
| 0x0C | KL50_CHANGE |
| 0x0D | KL50_ON |
| 0x0E | ERROR |
| 0xFF | INVALID |

<a id="table-tpowermode"></a>
### TPOWERMODE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SLEEP |
| 0x01 | NORMAL_OPERATION |
| 0x02 | NAD_ALWAYS_ON |
| 0x03 | NAD_ALWAYSON_DEBUG |
| 0xFF | INVALID |

<a id="table-trpcerrorcause"></a>
### TRPCERRORCAUSE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO_ERROR |
| 0x01 | NAO_ON_RPC_REJECTED |
| 0x02 | ANSWER_QUEUE_FULL |
| 0xFF | INVALID |

<a id="table-tvehicleevent"></a>
### TVEHICLEEVENT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | PROVISOINING_EVENT |
| 0x01 | CLAMPSTATE_EVENT |
| 0xFF | INVALID |

<a id="table-tcallstatus"></a>
### TCALLSTATUS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ABORT |
| 0x01 | DATA_CALL |
| 0x02 | ERROR |
| 0x03 | FINISHED |
| 0x04 | IDLE |
| 0x05 | PROVISIONING |
| 0x07 | VOICE_CALL |
| 0x08 | WAITING |
| 0xFF | INVALID |

<a id="table-tdataservicetype"></a>
### TDATASERVICETYPE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NONE |
| 0x01 | TELEDIAGNOSTICS |
| 0x02 | REMOTE_HELP |
| 0xFF | INVALID |

<a id="table-tdatacallstatus"></a>
### TDATACALLSTATUS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ABORT |
| 0x01 | AUTHENTICATION |
| 0x02 | CLOSING_CONNECTION |
| 0x03 | CONNECTING |
| 0x04 | DIAGNOSTICS |
| 0x05 | ERROR |
| 0x06 | FINISHED |
| 0x07 | IDLE |
| 0x08 | INITIAL_DATA |
| 0xFF | INVALID |

<a id="table-tlangcallstatus"></a>
### TLANGCALLSTATUS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ABORT |
| 0x01 | CLOSING_CONNECTION |
| 0x02 | CONNECTED |
| 0x03 | CONNECTING |
| 0x04 | DATA_TRANSFER |
| 0x05 | ERROR |
| 0x06 | FINISHED |
| 0x07 | IDLE |
| 0xFF | INVALID |

<a id="table-terrormessage"></a>
### TERRORMESSAGE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | NO_MESSAGE |
| 0x02 | ERROR_DATA_CONNECTION |
| 0x03 | ERROR_VOICE_CONNECTION |
| 0x04 | CONNECTION_LOST |
| 0x05 | NO_NETWORK |
| 0x06 | LINE_BUSY |
| 0x07 | NO_DEVICE |
| 0x08 | ERROR_DATA_TRANSFER |
| 0x09 | CONDITION_VIOLATION |
| 0x0A | ERROR_AUTHENTIFICATION |
| 0x0B | INTERNAL_ERROR |
| 0x0C | ERROR_PROVISIONING |
| 0x0D | USER_CHANNEL |
| 0x0E | PSIM_EXPIRED |
| 0xFF | INVALID |

<a id="table-tblockcallstate"></a>
### TBLOCKCALLSTATE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEIN_CALL_BLOCK |
| 0x01 | BLOCK_MO_CALLS |
| 0x02 | BLOCK_MT_CALLS |
| 0x03 | BLOCK_MO_AND_MT_CALLS |
| 0x0F | SIGNAL_UNGUELTIG |
| 0xFF | INVALID |

<a id="table-tteleeventtype"></a>
### TTELEEVENTTYPE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | CAN_TRIGGER |
| 0x01 | PINGUIN_TRIGGER |
| 0x02 | MILAGE_TRIGGER |
| 0x03 | TIME_TRIGGER |
| 0x04 | CALENDAR_TRIGGER |
| 0x05 | SAVED_TRIGGER |
| 0xFF | INVALID |

<a id="table-tpowerguardnad"></a>
### TPOWERGUARDNAD

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00FF | N/A |
| 0x0100 | isRunningOnBubGr5s |
| 0x0101 | isNeedCanMcu |
| 0x0102 | isRemoteService |
| 0x0103 | isNetworkReg |
| 0x0104 | doWakeupVehicle |
| 0x0105 | NaoCountDown |
| 0x0106 | isECall |
| 0x0107 | CanMcuShutdownTargetNao |
| 0x0108 | isRapidPowerDown |
| 0x0109 | isTeleservice |
| 0x010A | CP_NaoTrace |
| 0x01FF | N/A |
| 0x02FF | N/A |
| 0x03FF | N/A |
| 0xFFFF | Nicht definiert |

<a id="table-tpowerstatenad"></a>
### TPOWERSTATENAD

Dimensions: 75 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Sleep Power Off |
| 0x0001 | Normal Operation |
| 0x0002 | Nad Always On |
| 0x0003 | Nad Always On Debug |
| 0x0004 | MTS |
| 0x0005 | MTS Sleep |
| 0x0006 | Temperature Shutdown |
| 0x0100 | IpcActivity |
| 0x0101 | BubPowerDown |
| 0x0102 | ECall |
| 0x0103 | IpcShutdown |
| 0x0104 | IpcDeinit |
| 0x0105 | IpcDeinitNoteStart |
| 0x0106 | IpcStart |
| 0x0107 | IpcInit |
| 0x0108 | IpcInitNoteShutdown |
| 0x0109 | IpcStartApplications |
| 0x010A | IpcInitApps |
| 0x010B | IpcInitAppsNoteSd |
| 0x010C | IpcWait |
| 0x010D | Nao |
| 0x010E | NaoIdleLowPower |
| 0x010F | NaoLowPower |
| 0x0110 | IpcWaitLowPower |
| 0x0111 | LowPowerCanMcu |
| 0x0112 | LowPowerTraceDelay |
| 0x0113 | IsNaDe |
| 0x0114 | IsNeCaMc |
| 0x0115 | NoNetworkReg |
| 0x0116 | WakeupCanMcuNao |
| 0x0117 | IsNaoDebug |
| 0x0118 | NormalOperation |
| 0x0119 | NoService |
| 0x011A | NoServiceWait |
| 0x011B | RapidPowerDown |
| 0x011C | RemoteService |
| 0x011D | Teleservice |
| 0x011E | IpcOff |
| 0x011F | NaoExit |
| 0x0120 | NaoTimerOff |
| 0x0121 | NaoTimerLastMinute |
| 0x0122 | NaoTimerStopped |
| 0x0123 | NaoTimerRunning |
| 0x0200 | Init |
| 0x0201 | BB Powerup |
| 0x0202 | BB Startup |
| 0x0203 | Normal |
| 0x0204 | Prepare Shutdown |
| 0x0205 | BB Powerdown |
| 0x0206 | Shutdown |
| 0x0207 | BB Error |
| 0x0208 | Uninit |
| 0x0310 | Startup |
| 0x0311 | Startup One |
| 0x0312 | Startup Two |
| 0x0320 | Wakeup |
| 0x0321 | Wakeup One |
| 0x0322 | Wakeup Validation |
| 0x0323 | Wakeup Reaction |
| 0x0324 | Wakeup Two |
| 0x0325 | Wakeup Wake Sleep |
| 0x0326 | Wakeup TTII |
| 0x0330 | Run |
| 0x0332 | App Run |
| 0x0333 | App Post Run |
| 0x0340 | Shutdown |
| 0x0344 | Prepare Shutdown |
| 0x0349 | Go Sleep |
| 0x034D | Go Off One |
| 0x034E | Go Off Two |
| 0x0350 | Sleep |
| 0x0390 | Reset |
| 0x0380 | Off |
| 0x03FF | Error |
| 0xFFFF | Nicht definiert |

<a id="table-tpowertriggernad"></a>
### TPOWERTRIGGERNAD

Dimensions: 73 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Initial Power Up |
| 0x0001 | CAN Bus Off |
| 0x0002 | CAN Bus On |
| 0x0003 | NAO Maximum Time Expired |
| 0x0004 | No Network Registration |
| 0x0100 | EVTGUARD32 |
| 0x0101 | trgMTSModeUpdate |
| 0x0102 | trgCanMcuConnectionStartup |
| 0x0103 | EVTGUARD31 |
| 0x0104 | trgRemoteServiceStart |
| 0x0105 | EVTGUARD30 |
| 0x0106 | trgNeedVehicle |
| 0x0107 | trgCanMcuConnectionShutdown |
| 0x0108 | Wait_Nao_60s |
| 0x0109 | trgCodingUpdate |
| 0x010A | trgNetworkReg |
| 0x010B | trgECallFinished |
| 0x010C | EVTGUARD24 |
| 0x010D | EVTGUARD23 |
| 0x010E | EVTGUARD22 |
| 0x010F | EVTGUARD21 |
| 0x0110 | EVTGUARD20 |
| 0x0111 | EVTGUARD29 |
| 0x0112 | EVTGUARD28 |
| 0x0113 | NotRunningOnBub |
| 0x0114 | EVTGUARD27 |
| 0x0115 | EVTGUARD26 |
| 0x0116 | trgLatBufferEmpty |
| 0x0117 | EVTGUARD25 |
| 0x0118 | WaitLPTDelay_1s |
| 0x0119 | trgTeleserviceStart |
| 0x011A | trgStartNaoTimer |
| 0x011B | trgTeleserviceFinished |
| 0x011C | trgRemoteServiceFinished |
| 0x011D | EVTGUARD14 |
| 0x011E | EVTGUARD15 |
| 0x011F | EVTGUARD16 |
| 0x0120 | EVTGUARD17 |
| 0x0121 | EVTGUARD18 |
| 0x0122 | EVTGUARD19 |
| 0x0123 | trgNoNetworkReg |
| 0x0124 | trgLatBufferNonEmpty |
| 0x0125 | trgNotNeedCanMcu |
| 0x0126 | EVTGUARD10 |
| 0x0127 | EVTGUARD11 |
| 0x0128 | EVTGUARD12 |
| 0x0129 | EVTGUARD13 |
| 0x012A | Wait_NoNetworkReg_10s |
| 0x012B | trgCanMcuConnectedWakeup |
| 0x012C | runninggOnBubGr5s |
| 0x012D | trgRapidPowerDown |
| 0x012E | trgProvisioningUpdate |
| 0x012F | trgIpcDeinitialized |
| 0x0130 | trgNaoTimerExpired |
| 0x0131 | trgVehicleIgnitionOn |
| 0x0132 | trgIpcInitialized |
| 0x0133 | trgECallStart |
| 0x0134 | trgNaoOff |
| 0x0135 | EVTGUARD6 |
| 0x0136 | EVTGUARD5 |
| 0x0137 | EVTGUARD8 |
| 0x0138 | EVTGUARD7 |
| 0x0139 | EVTGUARD9 |
| 0x013A | EVTGUARD0 |
| 0x013B | trgNeedCanMcu |
| 0x013C | EVTGUARD1 |
| 0x013D | EVTGUARD2 |
| 0x013E | EVTGUARD3 |
| 0x013F | EVTGUARD4 |
| 0x0140 | Wait_NoService_1s |
| 0x02FF | N/A |
| 0x03FF | N/A |
| 0xFFFF | Nicht definiert |

<a id="table-tpowerstmnad"></a>
### TPOWERSTMNAD

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | System |
| 0x01 | BB LCM |
| 0x02 | CAN MCU |
| 0x03 | CAN MCU EcuM |
| 0xFF | Nicht definiert |
