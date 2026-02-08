# sme_04.prg

- Jobs: [35](#jobs)
- Tables: [49](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Speicher Management Elektronik Hybrid Gen. 1.5 |
| ORIGIN | BMW EA-411 Markus_Fuchs |
| REVISION | 2.003 |
| AUTHOR | CAS DHS-F Jörg_Scheiner, CAS DHS-F Sven_Kasner |
| COMMENT | **I-500** |
| PACKAGE | 1.15 |
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
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (12 × 9)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (29 × 16)
- [FORTTEXTE](#table-forttexte) (203 × 3)
- [TAB_SCHUETZ_SCHALTER](#table-tab-schuetz-schalter) (4 × 2)
- [RES_0XDD61](#table-res-0xdd61) (1 × 10)
- [ARG_0XDD61](#table-arg-0xdd61) (1 × 12)
- [TAB_SCHUETZ_FREIGABE](#table-tab-schuetz-freigabe) (3 × 2)
- [TAB_STATUS_HVIL](#table-tab-status-hvil) (3 × 2)
- [RES_0XDD6A](#table-res-0xdd6a) (2 × 10)
- [RES_0XDD6B](#table-res-0xdd6b) (4 × 10)
- [RES_0XDD6D](#table-res-0xdd6d) (2 × 10)
- [RES_0XDD6F](#table-res-0xdd6f) (1 × 10)
- [ARG_0XDD6F](#table-arg-0xdd6f) (1 × 12)
- [TAB_KUEHLERKREISLAUF_VENTIL](#table-tab-kuehlerkreislauf-ventil) (4 × 2)
- [RES_0XDD70](#table-res-0xdd70) (5 × 10)
- [RES_0XDD71](#table-res-0xdd71) (35 × 10)
- [TAB_AUFSTART_VERHINDERER](#table-tab-aufstart-verhinderer) (3 × 2)
- [RES_0XDD77](#table-res-0xdd77) (18 × 10)
- [ARG_0XDD79](#table-arg-0xdd79) (2 × 12)
- [TAB_ANST_SCHUETZ](#table-tab-anst-schuetz) (2 × 2)
- [RES_0XDD7B](#table-res-0xdd7b) (1 × 10)
- [ARG_0XDD7B](#table-arg-0xdd7b) (1 × 12)
- [RES_0XDD7C](#table-res-0xdd7c) (52 × 10)
- [RES_0XDD7D](#table-res-0xdd7d) (2 × 10)
- [RES_0XDD7E](#table-res-0xdd7e) (2 × 10)
- [RES_0XDD7F](#table-res-0xdd7f) (21 × 10)
- [ARG_0XDD7F](#table-arg-0xdd7f) (21 × 12)
- [RES_0XAD60](#table-res-0xad60) (6 × 13)
- [ARG_0XAD60](#table-arg-0xad60) (1 × 14)
- [RES_0XAD61](#table-res-0xad61) (1 × 13)
- [TAB_STATUS_ISOLATION](#table-tab-status-isolation) (5 × 2)
- [RES_0XAD62](#table-res-0xad62) (4 × 13)

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

Dimensions: 118 rows × 2 columns

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

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

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

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM-Stand                         (3 Bytes 1Bit=1km) | km | - | unsigned int | - | - | - | - |
| 0x1701 | Systemzeit                       (1Bit=1sec) | sec | - | signed long | - | - | - | - |
| 0x1702 | SAE-Code                        (3 Bytes) | - | - | unsigned int | - | - | - | - |
| 0x4000 | Außentemperatur | °C | - | signed char | - | - | - | - |
| 0x4001 | Spannung 12V-Batterie | V | - | unsigned char | - | - | 8 | - |
| 0x4002 | Strom HV-Curcuit | A | - | unsigned int | - | - | 10 | -819,2 |
| 0x4003 | Spannung HV-Batterie | V | - | unsigned int | - | - | 64 | - |
| 0x4004 | Spannung auf Zwischenkreisseite | V | - | unsigned int | - | - | 64 | - |
| 0x4005 | Temperatur HV-Batterie | °C | - | signed char | - | - | - | - |
| 0x4006 | SOC HV-Batterie | % | - | unsigned int | - | - | 10 | - |
| 0x4007 | Systemstatus | - | - | unsigned char | - | - | - | - |
| 0x4008 | Contactor State Machine FSM | - | - | unsigned char | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 29 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHUETZ_SCHALTER | 0xDD60 | STAT_SCHUETZ_SCHALTER | Status Schützschalter: geschlossen oder offen | 0-n | - | - | unsigned int | TAB_SCHUETZ_SCHALTER | - | - | - | - | 22 | - | - |
| SCHUETZ_FREIGABE | 0xDD61 | - | Schreibt bzw. liest das Bit zur Freigabe oder Sperrung der Schützschalter. Job ist Klemmensicher | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD61 | RES_0xDD61 |
| SCHUETZSCHALTUNGEN_ANZAHL | 0xDD63 | STAT_ANZAHL_SCHALTUNGEN_WERT | Anzahl der Schaltungen der Schützschalter (stromlos und unter Last) | - | - | - | unsigned long | - | - | - | - | - | 22 | - | - |
| HVIL | 0xDD64 | STAT_GUELTIG | Stören/Abschalten des Interlockgenerators im BMS / Ergebnis HVIL-Prüfung | 0-n | - | - | unsigned int | TAB_STATUS_HVIL | - | - | - | - | 22 | - | - |
| HV_SPANNUNG | 0xDD66 | STAT_HV_SPANNUNG_WERT | HV-Spannung Zwischenkreisspannung vor den Schützen | V | - | - | int | - | - | - | - | - | 22 | - | - |
| HV_SPANNUNG_BERECHNET | 0xDD68 | STAT_HV_SPANNUNG_BERECHNET_WERT |  HV-Spannung berechnet aus einzelnen Zellen  Batteriespannung hinter den Schützen   | V | - | - | int | - | - | - | - | - | 22 | - | - |
| HV_STROM | 0xDD69 | STAT_HV_STROM_WERT | HV-Strom | A | - | - | long | - | - | 1024.0 | - | - | 22 | - | - |
| ISOLATIONSWIDERSTAND | 0xDD6A | - | Auslesen des aktuell anliegenden Isolationswiderstands | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD6A |
| TEMP_SENSOREN | 0xDD6B | - | Temperatur Zellen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD6B |
| KUEHLKREISLAUF_TEMP | 0xDD6C | STAT_TEMP_KUEHLKREISLAUF_WERT | Temperatur Kühlkreislauf | °C | - | - | int | - | - | - | - | - | 22 | - | - |
| KAPAZITAETSVERLUST | 0xDD6D | - | HV-Batterie Kapazitätsverlust | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD6D |
| KUEHLKREISLAUF_VENTIL | 0xDD6F | - | Status / Steuern Kühlmittel-Ventil: Geschlossen oder offen | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD6F | RES_0xDD6F |
| AUSLIEFERUNGSDATEN | 0xDD70 | - | Auslesen Herstellerdaten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD70 |
| ZELLSPANNUNG | 0xDD71 | - | Zellenspannungen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD71 |
| AUFSTART_VERHINDERER | 0xDD72 | STAT_AUFSTART_VERHINDERER | Grund für nicht Aufstarten des HV-Systems | 0-n | - | - | int | TAB_AUFSTART_VERHINDERER | - | - | - | - | 22 | - | - |
| CUMULATIVE_LADUNG | 0xDD73 | STAT_LADUNG_AMP_STUNDEN_WERT | Status kumulierte Ladung | Ah | - | low | int | - | - | - | - | - | 22 | - | - |
| CUMULATIVE_ENTLADUNG | 0xDD74 | STAT_ENTLADUNG_AMP_STUNDEN_WERT | Status kumulierte Entladung | Ah | - | low | int | - | - | - | - | - | 22 | - | - |
| SERIENNUMMER | 0xDD75 | STAT_SERIENNUMMER_WERT | Schreiben/Auslesen Seriennummer | - | - | - | string[10] | - | - | - | - | - | 22 | - | - |
| STATUS_KL30C_SPANNUNG | 0xDD76 | STAT_KL30C_SPANNUNG_WERT | Spannung Klemme30C | V | - | - | unsigned int | - | - | 100.0 | - | - | 22 | - | - |
| HISTOGRAM | 0xDD77 | - | Zeit/Temperatur Histogramm SoC 1-3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD77 |
| SCHUETZE_MIN_SOC_SICHERHEITABFRAGE | 0xDD79 | - | Hauptschütze schalten bei min SOC (&lt; 5% SOC) Achtung!Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein Nicht möglich während der Fahrt. Auch bei tiefer Entladung (5% SOC) noch möglich. Achtung! Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein, um sicher zu stellen, dass ein Ladegerät bereits angeschlossen ist! | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDD79 | - |
| REFERENZ_KAPAZITAET | 0xDD7B | - | Auslesen und Justieren Kapazität Batterie | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD7B | RES_0xDD7B |
| GW_INFO | 0xDD7C | - | Gewährleistungsdaten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7C |
| STROMGRENZEN | 0xDD7D | - | Stromgrenzen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7D |
| SPANNUNGSGRENZEN | 0xDD7E | - | Spannungsgrenzen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDD7E |
| OCV_KENNLINIE | 0xDD7F | - | SoC-abhängige Leerlaufspannung | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD7F | RES_0xDD7F |
| ZELLAUSGLEICHSENTLADESPANNUNG | 0xAD60 | - | Zellausgleichsentladespannung | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAD60 | RES_0xAD60 |
| ISOLATION | 0xAD61 | - | Ergebnis Isolationstest | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAD61 |
| SOC | 0xAD62 | - | HV-Batterie SOC (state of charge) | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAD62 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 203 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x020700 | Energiesparmode aktiv | 0 |
| 0x02FF07 | Dummy-DTC: Applikationsfehler zum Testen | 0 |
| 0x21F000 | Interlock Leitung unterbrochen | 0 |
| 0x21F001 | Interlock Leitung: Kurzschluss auf Versorgung 12V | 0 |
| 0x21F002 | Interlock Leitung: Kurzschluss nach Masse | 0 |
| 0x21F003 | Interlock Wechselsignal wird nicht generiert | 0 |
| 0x21F004 | Interlock Leitung: Allgemeiner Fehler | 0 |
| 0x21F005 | Interlock Leitung: Durchführungsfehler | 0 |
| 0x21F006 | VCC_5V ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F007 | VCC_5V ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F008 | VCC_3.3V ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F009 | VCC_3.3V ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F00A | VCC_2.5V ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F00B | VCC_2.5V ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F00C | VCC_1.5V ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F00D | VCC_1.5V ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F011 | Klemme15 unplausibel/fehlerhaft | 0 |
| 0x21F012 | Klemme30C unplausibel | 0 |
| 0x21F013 | Klemme30C Unterspannung | 0 |
| 0x21F018 | EME, interner Fehler: ROM-Initialisierung fehlgeschlagen | 0 |
| 0x21F019 | EME, interner Fehler: ROM-Fehler im Betrieb | 0 |
| 0x21F01A | EME, interner Fehler: RAM-Initialisierung fehlgeschlagen | 0 |
| 0x21F01B | EME, interner Fehler: RAM-Fehler im Betrieb | 0 |
| 0x21F01C | EME, interner Fehler: EEPROM defekt | 0 |
| 0x21F030 | EME, Versorgungsspannung: Spannung zu hoch / interner Sensor defekt | 0 |
| 0x21F032 | EME, Versorgungsspannung: Spannung zu niedrig / interner Sensor defekt / Masseanschluss fehlt | 0 |
| 0x21F034 | EME, Software: Inkompatible Softwareversion programmiert | 0 |
| 0x21F035 | EME, interner Fehler: HW-Identifikation aus EEPROM nicht lesbar | 0 |
| 0x21F038 | Vorladung kann nicht in max. Vorladezeit ausgeführt werden | 0 |
| 0x21F039 | I_BATT_Precharge liegt ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F03A | I_BATT_Precharge liegt ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F03C | Schütz(e) auf Batt Plus läßt sich nicht schließen | 0 |
| 0x21F03D | Schütz(e) auf Batt Minus läßt sich nicht schließen | 0 |
| 0x21F03E | Schütz(e) auf Batt Plus läßt sich nicht öffnen | 0 |
| 0x21F03F | Schütz(e) auf Batt Minus läßt sich nicht öffnen | 0 |
| 0x21F040 | Hauptschütz (Plus) ist demnächst funktionsunfähig | 0 |
| 0x21F041 | Hauptschütz (Minus) ist demnächst funktionsunfähig | 0 |
| 0x21F042 | Vorladeschütz ist demnächst funktionsunfähig | 0 |
| 0x21F043 | Hauptschütz (Plus) ist funktionsunfähig | 0 |
| 0x21F044 | Hauptschütz (Minus) ist funktionsunfähig | 0 |
| 0x21F045 | Vorladeschütz ist funktionsunfähig | 0 |
| 0x21F046 | Schützefunktion gesperrt da Transportbit gesetzt | 0 |
| 0x21F047 | Kühlventil kann nicht geöffnet werden | 0 |
| 0x21F048 | Initialisierung fehlgeschlagen | 0 |
| 0x21F049 | Oscillator AUS | 0 |
| 0x21F04A | Periodic Time fehlgeschlagen | 0 |
| 0x21F04B | Kühlventil kann nicht geschlossen werden | 0 |
| 0x21F04C | ISA-ASIC interface nicht initialisiert | 0 |
| 0x21F04D | Konfigurations- oder Arbeitsregister des Controllers fehlerhaft | 0 |
| 0x21F04E | Startup Interrupt Test fehlerhaft | 0 |
| 0x21F04F | Startup Register Test fehlerhaft | 0 |
| 0x21F053 | Kommunikation konnte nicht gestartet werden | 0 |
| 0x21F056 | HW Kommunikation fehlerhaft | 0 |
| 0x21F059 | Kommunikation zwischen BMC und CSC gestört | 0 |
| 0x21F05A | CSC Konfiguration nicht kompatibel | 0 |
| 0x21F05C | Kühlmitteltemperatur am Einlauf in die Batterie kritisch | 0 |
| 0x21F060 | Interner Isolationswiderstand ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F061 | Isolationswiderstand Messeinheit defekt | 0 |
| 0x21F062 | Isolation Plus Bereichsfehler | 0 |
| 0x21F063 | Isolation Minus Bereichsfehler | 0 |
| 0x21F064 | Externer Isolationswiderstand ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F068 | Isolation Dc Link Plus | 0 |
| 0x21F069 | Isolation Dc Link Minus | 0 |
| 0x21F06A | Isolation Batt Plus Bereichsfehler | 0 |
| 0x21F06B | Isolation Batt Minus Bereichsfehler | 0 |
| 0x21F06C | Isolation Contactor Plus Bereichsfehler | 0 |
| 0x21F06D | Isolation Contactor Minus Bereichsfehler | 0 |
| 0x21F070 | BCC: berechneter EOL erreicht | 0 |
| 0x21F071 | BCC: Battery ist extrem unausgewogen | 0 |
| 0x21F072 | BCC: einige Zellen sind defekt | 0 |
| 0x21F073 | BCC: EEPROM Lesefehler (InternalData Listed) | 0 |
| 0x21F074 | BCC: EEPROM Lesefehler (InternalData IntegrityFailed) | 0 |
| 0x21F075 | BCC: EEPROM Lesefehler (Bal Listed) | 0 |
| 0x21F076 | BCC: EEPROM Lesefehler (Bal IntegrityFailed) | 0 |
| 0x21F077 | BCC: JCS/NV-Daten unplaussibel (SOH, Warranty Information) | 0 |
| 0x21F07E | BCC: Alterungsbestimmung notwendig | 0 |
| 0x21F084 | Ersatzwert für Batteriespannung muss gebildet werden | 0 |
| 0x21F085 | Batteriespannung kann nicht ermittelt werden, d.h. auch keine Ersatzwertbildung möglich | 0 |
| 0x21F086 | Ersatzwert für Zwischenkreisspannung muss gebildet werden | 0 |
| 0x21F087 | Zwischenkreisspannung kann nicht ermittelt werden, d.h. auch keine Ersatzwertbildung möglich | 0 |
| 0x21F088 | Ersatzwert für Batterietemperatur muss gebildet werden | 0 |
| 0x21F089 | Batterietemperatur kann nicht ermittelt werden, d.h. auch keine Ersatzwertbildung möglich | 0 |
| 0x21F08A | BCC: derating maximum charge voltage | 0 |
| 0x21F08B | BCC: derating minimum discharge voltage | 0 |
| 0x21F0A0 | &lt;Critical Close&gt; ist gesetzt | 0 |
| 0x21F0A1 | &lt;Critical Close&gt; ist nicht möglich | 0 |
| 0x21F0A2 | &lt;Critical Close&gt; ist nicht möglich im aktuellen Fahrzyklus | 0 |
| 0x21F0A3 | EME, interner Fehler, Ebene 2: Programmablauffehler | 0 |
| 0x21F0A4 | EME, interner Fehler, Ebene 2: Resetursachenermittelung konnte nicht aus dem EEPROM lesen | 0 |
| 0x21F0A5 | Resetursachenermittelung konnte die Überwachungsmodul-Resetinformationen nicht lesen | 0 |
| 0x21F0A8 | EME, interner Fehler, Ebene 2:  Watchdog CY320 kann nicht konfiguriert werden | 0 |
| 0x21F0A9 | EME, interner Fehler, Ebene 2:  Fehlerzähler des Überwachungsmoduls ist größer 4 | 0 |
| 0x21F0AA | EME, interner Fehler, Ebene 2:  Fehlerzähler des Überwachungsmoduls verändert sich trotz Fehler nicht | 0 |
| 0x21F0AB | Level 1: Irregulärer Powerdown detektiert | 0 |
| 0x21F0AC | Klemme30 außerhalb des gültigen Bereichs (zu hoch) für CAN | 0 |
| 0x21F0AD | Klemme30 außerhalb des gültigen Bereichs (zu niedrig) für CAN | 0 |
| 0x21F0AE | CSC Ausgleichseinheit defekt | 0 |
| 0x21F0AF | CSC Zellverbindung defekt | 0 |
| 0x21F0B0 | CSC Messhardware defekt | 0 |
| 0x21F0B1 | SEH: Trotz bestätigtem, sicherheitsrelevantem Fehlerzustand ist die Leistungsendstufe nicht abgeschaltet | 0 |
| 0x21F0B2 | es wurde ein Reset aufgrund eines Überwachungsfehlers ausgeführt | 0 |
| 0x21F0B3 | Crash Ereignis ermittelt (EKP via CAN signalisiert) | 0 |
| 0x21F0B4 | EME, interner Fehler, Ebene 3: die maximales Resetanzahl eines spezifischen Fehlers erreicht | 0 |
| 0x21F0B5 | Ebene 3: Interlock Check wird nicht mehr korrekt durchgefuehrt | 0 |
| 0x21F0B6 | Ebene 3: Isolationsueberwachung wird nicht mehr korrekt durchgefuehrt | 0 |
| 0x21F0B7 | Ebene 3: Safety-relevante ISO Daten sind korumpiert | 0 |
| 0x21F0B8 | Ebene 3: Safety-relevante Interlock Daten sind korumpiert | 0 |
| 0x21F0B9 | Ebene 3: Safety-relevante Daten der Batterielast-Uberwachung sind korumpiert | 0 |
| 0x21F0BA | Ebene 3: Batterielastueberwachung wird nicht mehr korrekt durchgefuehrt | 0 |
| 0x21F0BB | EME, interner Fehler, Ebene 3: Reset durch externes Überwachungsmodul | 0 |
| 0x21F0D1 | Kühlkreislauf Temperatur Sensor Rohwert außerhalb des gültigen Bereichs (unten) | 0 |
| 0x21F0D2 | Kühlkreislauf Temperatur Sensor Rohwert außerhalb des gültigen Bereichs (oben) | 0 |
| 0x21F0E0 | Batterie Temperatur Sensor 1 unplausibel / fehlerhaft | 0 |
| 0x21F0E3 | Batterie Übertemperatur Sensor 1 (1.Schwelle) | 0 |
| 0x21F0E4 | CSE Temperatur Sensor 1 ungültig | 0 |
| 0x21F0E5 | Batterie Temperatur Sensor 1 außerhalb gültiger Bereich (oben) | 0 |
| 0x21F0E6 | Batterie Temperatur Sensor 1 außerhalb gültiger Bereich (unten) | 0 |
| 0x21F0E8 | Batterie Temperatur Sensor2 unplausibel / fehlerhaft | 0 |
| 0x21F0EB | Batterie Übertemperatur Sensor2 (1.Schwelle) | 0 |
| 0x21F0EC | Wert der 2.Batterietemperatur ungültig | 0 |
| 0x21F0ED | Batterie Temperatur Sensor2 außerhalb gültiger Bereich (oben) | 0 |
| 0x21F0EE | Batterie Temperatur Sensor2 außerhalb gültiger Bereich (unten) | 0 |
| 0x21F0F0 | Batterie Temperatur Sensor3 unplausibel / fehlerhaft | 0 |
| 0x21F0F3 | Batterie Übertemperatur Sensor3 (1.Schwelle) | 0 |
| 0x21F0F4 | Wert der 3.Batterietemperatur ungültig | 0 |
| 0x21F0F5 | Batterie Temperatur Sensor3 außerhalb gültiger Bereich (oben) | 0 |
| 0x21F0F6 | Batterie Temperatur Sensor3 außerhalb gültiger Bereich (unten) | 0 |
| 0x21F0F8 | Batterie Temperatur Sensor4 unplausibel / fehlerhaft | 0 |
| 0x21F0FB | Batterie Übertemperatur Sensor4 (1.Schwelle) | 0 |
| 0x21F0FC | Wert der 4.Batterietemperatur ungültig | 0 |
| 0x21F0FD | Batterie Temperatur Sensor4 außerhalb gültiger Bereich (oben) | 0 |
| 0x21F0FE | Batterie Temperatur Sensor4 außerhalb gültiger Bereich (unten) | 0 |
| 0x21F118 | dynamischer Stromgrenzwert für Batterieladen fehlerhaft (Wertabweichung) | 0 |
| 0x21F119 | dynamischer Stromgrenzwert für Batterieentladen (Wertabweichung) | 0 |
| 0x21F11A | dynamischer Spannungsgrenzwert für Batterieladen fehlerhaft (Wertabweichung) | 0 |
| 0x21F11B | dynamischer Spannungsgrenzwert für Batterieentladen (Wertabweichung) | 0 |
| 0x21F11C | SOC sehr klein | 0 |
| 0x21F11D | SOC klein | 0 |
| 0x21F11E | SOC sehr hoch | 0 |
| 0x21F11F | Überstrom gemessen | 0 |
| 0x21F120 | CSC_Volt kritische Schwelle (oben) | 0 |
| 0x21F121 | CSC_Volt kritische Unterspannung (1.Schwelle) | 0 |
| 0x21F123 | CSC_Volt kritische Unterspannung (2.Schwelle) | 0 |
| 0x21F124 | Wert der Zellspannung ungültig  | 0 |
| 0x21F125 | Summe der Einzelzellspannungen unplausibel | 0 |
| 0x21F12A | Schütze wurden unter Last geöffnet | 0 |
| 0x21F12B | Vorladen zum Schutz der Elektronik temporär gesperrt | 0 |
| 0x21F12C | Verschlissenes Schütz(e) auf Batt Plus läßt sich nicht öffnen | 0 |
| 0x21F12D | Verschlissenes Schütz(e) auf Batt Minus läßt sich nicht öffnen | 0 |
| 0x21F138 | HW Überstrom Test des Sensors | 0 |
| 0x21F139 | HW Abschaltlogik freigegeben (Schütze geöffnet) | 0 |
| 0x21F13B | HW Overcurrent gesetzt | 0 |
| 0x21F13C | HW Übertemperatur, Überspannung oder Unterspannung ausgelöst | 0 |
| 0x21F13D | Takt-Signal wird nicht erzeugt | 0 |
| 0x21F13F | HW-Abschaltung fehlerhaft | 0 |
| 0x21F148 | Externer Crashsensor: Crash detektiert (KL30C) | 0 |
| 0x21F150 | HV_Spannung_ZK ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F151 | HV_Spannung_ZK ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F152 | HV_Spannung unplausibel / fehlerhaft | 0 |
| 0x21F160 | I_BATT ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F161 | I_BATT ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F162 | I_BATT unplausibel / fehlerhaft | 0 |
| 0x21F168 | Singel CSC Package Voltage ausserhalb des gültigen Bereichs  | 0 |
| 0x21F169 | Summe der CSC-Pack-Spannungen unplausibel | 0 |
| 0x21F16A | Interne ISO-Spannung unplausibel | 0 |
| 0x21F16B | Externe ISO-Spannung unplausibel | 0 |
| 0x21F170 | ISO Referenzspannung PLUS ausserhalb des gültigen Bereichsbands (oben) | 0 |
| 0x21F171 | ISO Refernzspannung MINUS ausserhalb des gültigen Bereichsbands (oben) | 0 |
| 0x21F172 | VCC_12V ausserhalb des gültigen Bereichs (oben) | 0 |
| 0x21F173 | VCC_12V ausserhalb des gültigen Bereichs (unten) | 0 |
| 0x21F174 | ISO Referenzspannung PLUS ausserhalb des gültigen Bereichsbands (unten) | 0 |
| 0x21F175 | ISO Referenzspannung MINUS ausserhalb des gültigen Bereichsbands (unten) | 0 |
| 0x21F178 | Stromplausibilisierung nicht möglich | 0 |
| 0x21F179 | Spannungsplausibilisierung nicht möglich | 0 |
| 0x21F180 | Temperaturplausibilisierung nicht möglich | 0 |
| 0x21F181 | Kl30C-Plausibilisierung nicht möglich | 0 |
| 0x21F182 | Sicherheitsprüfung noch nicht beendet | 0 |
| 0x21F183 | Zwischenkreisspannung liegt oberhalb der Batteriespannung | 0 |
| 0x21F184 | Momentaner Isolationswiderstand unterhalb des kritischen Grenzwertes. | 0 |
| 0x21F185 | Überwachung von Strom- und Zeitgenzen während   Kommandiert Stromlos   | 0 |
| 0x21F186 | Langzeitüberwachung von   Kommandiert Stromlos   | 0 |
| 0x21F187 | Level 3: Safety-relevante Daten der Uberwachung sind korumpiert | 0 |
| 0x21F189 | HV Strom Datenübertragung fehlerhaft | 0 |
| 0x21F18A | HV Spannung Datenübertragung fehlerhaft | 0 |
| 0xCAC400 | Botschaft (Steuerung Crashabschaltung EKP, FA-CAN, 0x135): Ausfall | 0 |
| 0xCAC401 | Botschaft (Fahrzeugzustand, FA-CAN, 0x3A0): Ausfall | 0 |
| 0xCAC402 | Botschaft (Klemmen, FA-CAN, 0x12F): Ausfall | 0 |
| 0xCAC403 | Botschaft (Relativzeit, FA-CAN, 0x328): Ausfall | 0 |
| 0xCAC404 | Botschaft (Freigabe Kühlung Hochvoltspeicher, FA-CAN, 0x37B): Ausfall | 0 |
| 0xCAC405 | Botschaft (ZV und Klappenzustand, FA-CAN, 0x2FC): Ausfall | 0 |
| 0xCAC406 | Zeitüberschreitung von CAN-Botschaft KILOMETERSTAND | 0 |
| 0xCAC407 | Botschaft (Geschwindigkeit Fahrzeug, FA-CAN, 0x1A1): Ausfall | 0 |
| 0xCAC40A | Zeitüberschreitung von CAN-Botschaft ST_MOT_1 | 0 |
| 0xCAC40C | Botschaft (Außentemperatur, FA-CAN, 0x2CA): Ausfall | 0 |
| 0xCAC40D | Zeitüberschreitung von CAN-Botschaft DT_PT_1 | 0 |
| 0xCAC40E | Zeitüberschreitung von CAN-Botschaft DT_PT_2 | 0 |
| 0xCAC40F | Zeitüberschreitung von CAN-Botschaft TORQ_CRSH_1 | 0 |
| 0xCAC410 | CRC der Nutzdaten von CAN-Botschaft ST_MOT_1 fehlerhaft | 0 |
| 0xCAC411 | Zähler von CAN-Botschaft ST_MOT_1 fehlerhaft | 0 |
| 0xCAC412 | Zeitüberschreitung von CAN-BotschaftST_DCDC | 0 |
| 0xCAC486 | Sub-Hybrid CAN Bus Off | 0 |
| 0xCACBFF | Dummy-DTC: Netzwerkfehler zum Testen | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-tab-schuetz-schalter"></a>
### TAB_SCHUETZ_SCHALTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | offen |
| 0x01 | geschlossen |
| 0x02 | verschweisste Kontakte |
| 0x03 | nicht definiert |

<a id="table-res-0xdd61"></a>
### RES_0XDD61

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHUETZ_FREIGABE | 0-n | - | unsigned int | - | TAB_SCHUETZ_FREIGABE | - | - | - | Liest das Bit zur Freigabe oder Sperrung der Schützschalter   |

<a id="table-arg-0xdd61"></a>
### ARG_0XDD61

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FREIGABE | 0/1 | - | unsigned int | - | - | - | - | - | - | - | 0 = nicht freigegeben 1 = freigegeben |

<a id="table-tab-schuetz-freigabe"></a>
### TAB_SCHUETZ_FREIGABE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht freigegeben |
| 0x01 | freigegeben |
| 0xFF | nicht definiert |

<a id="table-tab-status-hvil"></a>
### TAB_STATUS_HVIL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht ok |
| 0x01 | ok |
| 0xFF | nicht definiert |

<a id="table-res-0xdd6a"></a>
### RES_0XDD6A

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ISOWIDERSTAND_WERT | kOhm | - | int | - | - | - | - | - | Isolationswiderstand |
| STAT_ISOWIDERSTAND_PLAUSIBILITAET_EIN | 0/1 | - | char | - | - | - | - | - | Plausibilität des Isolationswiderstand  |

<a id="table-res-0xdd6b"></a>
### RES_0XDD6B

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_SENSOR_1_WERT | °C | - | int | - | - | - | - | - | - |
| STAT_TEMP_SENSOR_2_WERT | °C | - | int | - | - | - | - | - | - |
| STAT_TEMP_SENSOR_3_WERT | °C | - | int | - | - | - | - | - | - |
| STAT_TEMP_SENSOR_4_WERT | °C | - | int | - | - | - | - | - | - |

<a id="table-res-0xdd6d"></a>
### RES_0XDD6D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KAPAZITAETSVERLUST_WERT | % | - | int | - | - | - | 16.0 | - | HV-Batterie Kapazitätsverlust |
| STAT_KAPAZITAETSVERLUST_PLAUSIBILITAET_EIN | 0/1 | - | char | - | - | - | - | - | Plausibilität des Kapazitätsverlustes der HV-Batterie |

<a id="table-res-0xdd6f"></a>
### RES_0XDD6F

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KUEHLKREISLAUF_VENTIL | 0-n | - | unsigned int | - | TAB_KUEHLERKREISLAUF_VENTIL | - | - | - | Status Kühlmittel-Ventil: Geschlossen oder offen  |

<a id="table-arg-0xdd6f"></a>
### ARG_0XDD6F

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KUEHLKREISLAUF_VENTIL | 0-n | - | unsigned int | - | TAB_KUEHLERKREISLAUF_VENTIL | - | - | - | - | - | Steuern Kühlmittel-Ventil: Geschlossen oder offen |

<a id="table-tab-kuehlerkreislauf-ventil"></a>
### TAB_KUEHLERKREISLAUF_VENTIL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | geschlossen |
| 0x01 | offen |
| 0x02 | geregelt |
| 0xFF | nicht definiert |

<a id="table-res-0xdd70"></a>
### RES_0XDD70

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSLIEFERUNG_JAHR_WERT | - | - | char | - | - | - | - | - | Auslieferungsdaten Jahr |
| STAT_AUSLIEFERUNG_KALENDERWOCHE_WERT | - | - | char | - | - | - | - | - | Auslieferungsdaten Kalenderwoche |
| STAT_AUSLIEFERUNG_TAG_WERT | - | - | char | - | - | - | - | - | Auslieferungsdaten Tag Kalenderwoche |
| STAT_AUSLIEFERUNG_OK | 0/1 | - | char | - | - | - | - | - | Auslieferungsdaten Bandende OK 1: OK 0: nicht OK |
| STAT_AUSLIEFERUNG_SOC_WERT | % | - | int | - | - | - | 16.0 | - | Auslieferungsdaten Ladung Batterie SOC (Prozent) |

<a id="table-res-0xdd71"></a>
### RES_0XDD71

Dimensions: 35 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZELLSPANNUNG_1_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 1 |
| STAT_ZELLSPANNUNG_2_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 2 |
| STAT_ZELLSPANNUNG_3_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 3 |
| STAT_ZELLSPANNUNG_4_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 4 |
| STAT_ZELLSPANNUNG_5_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 5 |
| STAT_ZELLSPANNUNG_6_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 6 |
| STAT_ZELLSPANNUNG_7_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 7 |
| STAT_ZELLSPANNUNG_8_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 8 |
| STAT_ZELLSPANNUNG_9_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 9 |
| STAT_ZELLSPANNUNG_10_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 10 |
| STAT_ZELLSPANNUNG_11_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 11 |
| STAT_ZELLSPANNUNG_12_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 12 |
| STAT_ZELLSPANNUNG_13_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 13 |
| STAT_ZELLSPANNUNG_14_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 14 |
| STAT_ZELLSPANNUNG_15_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 15 |
| STAT_ZELLSPANNUNG_16_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 16 |
| STAT_ZELLSPANNUNG_17_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 17 |
| STAT_ZELLSPANNUNG_18_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 18 |
| STAT_ZELLSPANNUNG_19_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 19 |
| STAT_ZELLSPANNUNG_20_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 20 |
| STAT_ZELLSPANNUNG_21_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 21 |
| STAT_ZELLSPANNUNG_22_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 22 |
| STAT_ZELLSPANNUNG_23_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 23 |
| STAT_ZELLSPANNUNG_24_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 24 |
| STAT_ZELLSPANNUNG_25_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 25 |
| STAT_ZELLSPANNUNG_26_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 26 |
| STAT_ZELLSPANNUNG_27_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 27 |
| STAT_ZELLSPANNUNG_28_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 28 |
| STAT_ZELLSPANNUNG_29_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 29 |
| STAT_ZELLSPANNUNG_30_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 30 |
| STAT_ZELLSPANNUNG_31_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 31 |
| STAT_ZELLSPANNUNG_32_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 32 |
| STAT_ZELLSPANNUNG_33_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 33 |
| STAT_ZELLSPANNUNG_34_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 34 |
| STAT_ZELLSPANNUNG_35_WERT | mV | - | unsigned int | - | - | - | - | - | Spannung Zelle 35 |

<a id="table-tab-aufstart-verhinderer"></a>
### TAB_AUFSTART_VERHINDERER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | interner Fehler |
| 0xFF | nicht definiert |

<a id="table-res-0xdd77"></a>
### RES_0XDD77

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HISTOGRAMM_SOC1_1_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.1 |
| STAT_HISTOGRAMM_SOC1_2_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.2 |
| STAT_HISTOGRAMM_SOC1_3_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.3 |
| STAT_HISTOGRAMM_SOC1_4_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.4 |
| STAT_HISTOGRAMM_SOC1_5_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.5 |
| STAT_HISTOGRAMM_SOC1_6_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 1.6 |
| STAT_HISTOGRAMM_SOC2_1_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.1 |
| STAT_HISTOGRAMM_SOC2_2_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.2 |
| STAT_HISTOGRAMM_SOC2_3_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.3 |
| STAT_HISTOGRAMM_SOC2_4_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.4 |
| STAT_HISTOGRAMM_SOC2_5_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.5 |
| STAT_HISTOGRAMM_SOC2_6_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 2.6 |
| STAT_HISTOGRAMM_SOC3_1_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.1 |
| STAT_HISTOGRAMM_SOC3_2_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.2 |
| STAT_HISTOGRAMM_SOC3_3_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.3 |
| STAT_HISTOGRAMM_SOC3_4_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.4 |
| STAT_HISTOGRAMM_SOC3_5_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.5 |
| STAT_HISTOGRAMM_SOC3_6_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen SoC gelesen wird SoC 3.6 |

<a id="table-arg-0xdd79"></a>
### ARG_0XDD79

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ANSTEUERUNG | 0-n | - | unsigned int | - | TAB_ANST_SCHUETZ | - | - | - | - | - | Achtung!Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein Nicht möglich während der Fahrt. Auch bei tiefer Entladung (5% SOC) noch möglich. Achtung! Dieser Job muss in allen Folgetools mit Security Abfrage gesichert sein, um sicher zu stellen, dass ein Ladegerät bereits angeschlossen ist! |
| PASSWORD | - | - | string[5] | - | - | - | - | - | - | - | Sicherheitspasswort zur Schuetzschaltung |

<a id="table-tab-anst-schuetz"></a>
### TAB_ANST_SCHUETZ

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |

<a id="table-res-0xdd7b"></a>
### RES_0XDD7B

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KAPAZITAET_WERT | Ah | - | unsigned int | - | - | - | 3600.0 | - | Auslesen Justierung Kapazität Batterie |

<a id="table-arg-0xdd7b"></a>
### ARG_0XDD7B

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KAPAZITAET_JUSTIERUNG | Ah | - | unsigned int | - | - | 3600.0 | - | - | - | - | Justierung Kapazität Batterie |

<a id="table-res-0xdd7c"></a>
### RES_0XDD7C

Dimensions: 52 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZEIT_UMAX_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die maximale Einzelspannung über der zulässigen Maximalgrenze lag |
| STAT_ZEIT_UMIN_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die minimale Einzelspannung unter der zulässigen Minimalgrenze lag |
| STAT_ZEIT_BETRIEB_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in der der Speicher im Betrieb ist |
| STAT_ZEIT_THIGH_BETRIEB_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur im Betrieb über 80°C lag |
| STAT_ZEIT_TMAX_BETRIEB_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur im Betrieb über 60°C lag |
| STAT_ZEIT_TMIN_BETRIEB_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur im Betrieb unter -40°C lag |
| STAT_ZEIT_PARKEN_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in der der Speicher im Parkzustand betrieben wird |
| STAT_ZEIT_THIGH_PARKEN_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur während des Parkens über 80°C lag |
| STAT_ZEIT_TMAX_PARKEN_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur während des Parkens über 60°C lag |
| STAT_ZEIT_TMIN_PARKEN_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der die Zelltemperatur während des Parkens unter -40°C lag |
| STAT_ZEIT_IMAX_LADUNG_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der der Strom länger als 2 Sekunden oder 20 A über der zulässigen Ladestromgrenze lag |
| STAT_ZEIT_IMAX_ENTLADUNG_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden in der der Strom länger als 2 Sekunden oder 20 A unter der zulässigen Entladestromgrenze lag  |
| STAT_CUMULATIVE_ENERGIE_LADUNG_WERT | Ws | low | unsigned long | - | - | - | - | - | Wert der kumulierten Energie in Ws für Ladevorgänge |
| STAT_CUMULATIVE_ENERGIE_ENTLADUNG_WERT | Ws | low | unsigned long | - | - | - | - | - | Wert der kumulierten Energie in Ws für Entladevorgänge |
| STAT_CUMULATIVE_LADUNG_WERT | Ah | low | unsigned long | - | - | - | 3600.0 | - | Wert der kumulierten Ladung in Ah |
| STAT_CUMULATIVE_ENTLADUNG_WERT | Ah | low | unsigned long | - | - | - | 3600.0 | - | Wert der kumulierten Entladung in Ah |
| STAT_ANZAHL_WECKVORGAENGE_WERT | - | low | unsigned long | - | - | - | - | - | Anzahl der Übergänge vom Parken in den Betrieb |
| STAT_ZEIT_BALANCING_1_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_2_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_3_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_4_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_5_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_6_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_7_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_8_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_9_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_10_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_11_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_12_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_13_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_14_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_15_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_16_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_17_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_18_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_19_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_20_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_21_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_22_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_23_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_24_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_25_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_26_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_27_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_28_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_29_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_30_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_31_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_32_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_33_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_34_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |
| STAT_ZEIT_BALANCING_35_WERT | s | low | unsigned long | - | - | - | - | - | Zeit in Sekunden, in denen die Zelle gezielt entladen wurde |

<a id="table-res-0xdd7d"></a>
### RES_0XDD7D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADESTROMGRENZE_WERT | A | - | unsigned int | - | - | - | 32.0 | - | maximal erlaubter Ladestrom, Umrechnung 1/32 |
| STAT_ENTLADESTROMGRENZE_WERT | A | - | unsigned int | - | - | - | 32.0 | - | maximal erlaubter Entladesstrom, Umrechnung 1/32 |

<a id="table-res-0xdd7e"></a>
### RES_0XDD7E

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADESPANNUNGSGRENZE_WERT | V | - | unsigned int | - | - | - | 64.0 | - | maximal erlaubte Ladespannung, Umrechnung 1/64 |
| STAT_ENTLADESPANNUNGSGRENZE_WERT | V | - | unsigned int | - | - | - | 64.0 | - | maximal erlaubte Entladespannung, Umrechnung 1/64 |

<a id="table-res-0xdd7f"></a>
### RES_0XDD7F

Dimensions: 21 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNGSKENNLINIE_1_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_2_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_3_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_4_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_5_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_6_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_7_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_8_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_9_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_10_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_11_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_12_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_13_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_14_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_15_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_16_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_17_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_18_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_19_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_20_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |
| STAT_SPANNUNGSKENNLINIE_21_21_WERT | V | - | unsigned int | - | - | - | 100.0 | - | Spannungsgrenze, Umrechnung 1/100 |

<a id="table-arg-0xdd7f"></a>
### ARG_0XDD7F

Dimensions: 21 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNGSKENNLINIE_1_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_2_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_3_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_4_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_5_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_6_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_7_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_8_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_9_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_10_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_11_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_12_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_13_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_14_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_15_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_16_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_17_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_18_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_19_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_20_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |
| STAT_SPANNUNGSKENNLINIE_21_21_WERT | V | - | unsigned int | - | - | 100.0 | - | - | - | - | OCV Spannungskennlinie, Umrechnung 100/1 |

<a id="table-res-0xad60"></a>
### RES_0XAD60

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGLEICHSENTLADESPANNUNG_EIN | - | - | + | 0/1 | - | char | - | - | - | - | - | Status Ausgleichsentladespannung; 0 = aus, 1 = ein |
| STAT_MAX_ZELLSPANNUNG_START_ENTLADUNG_WERT | - | - | + | mV | - | int | - | - | - | - | - | max. Zellspannung beim Start der letzten Ausgleichsentladung |
| STAT_MIN_ZELLSPANNUNG_START_ENTLADUNG_WERT | - | - | + | mV | - | int | - | - | - | - | - | min. Zellspannung beim Start der letzten Ausgleichsentladung |
| STAT_MAX_ZELLSPANNUNG_ENDE_ENTLADUNG_WERT | - | - | + | mV | - | int | - | - | - | - | - | max. Zellspannung beim Ende der letzten Ausgleichsentladung |
| STAT_MIN_ZELLSPANNUNG_ENDE_ENTLADUNG_WERT | - | - | + | mV | - | int | - | - | - | - | - | min. Zellspannung beim Ende der letzten Ausgleichsentladung |
| STAT_ISTGRENZE_AUSGLEICHSENTLADESPANNUNG_WERT | - | - | + | mV | - | int | - | - | - | - | - | Ist-Grenze Ausgleichsentladespannung |

<a id="table-arg-0xad60"></a>
### ARG_0XAD60

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ENTLADESPANNUNG | + | - | mV | - | int | - | - | - | - | - | - | - | Balanciert die Spannung der Zellen aus. |

<a id="table-res-0xad61"></a>
### RES_0XAD61

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ISOLATION | - | + | + | 0-n | - | unsigned int | - | TAB_STATUS_ISOLATION | - | - | - | Ergebnis Isolationstest |

<a id="table-tab-status-isolation"></a>
### TAB_STATUS_ISOLATION

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fehler |
| 0x01 | Warnung |
| 0x10 | i.O. |
| 0x11 | ungültig |
| 0xFF | nicht definiert |

<a id="table-res-0xad62"></a>
### RES_0XAD62

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SOC_WERT | - | + | + | % | - | unsigned int | - | - | - | 16.0 | - | HV-Batterie SOC |
| STAT_SOC_PLAUSIBILITAET_EIN | - | + | + | 0/1 | - | char | - | - | - | - | - | Plausibilität des HV-Batterie SOC |
| STAT_SOC_MAX_WERT | - | + | + | % | - | unsigned int | - | - | - | 16.0 | - | Maximalwert SOC |
| STAT_SOC_MIN_WERT | - | + | + | % | - | unsigned int | - | - | - | 16.0 | - | Minimalwert SOC |
