# nivi2.prg

- Jobs: [38](#jobs)
- Tables: [76](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Night Vision |
| ORIGIN | BMW EI-611 King |
| REVISION | 3.008 |
| AUTHOR | Autoliv AS Vahlberg |
| COMMENT | NiVi [16] |
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
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default
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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) oder VERBAUORT eines bestimmten Sensors (table VerbauortTabelle ORT) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_VERBAUORT_NR | long | Verbauort-Nummer des Sensors |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn Teilenummer vom Sensor nicht verfuegbar dann '--' |
| SENSOR_LIN_2_0_FORMAT | int | 1: Die optionalen Daten des Sensors (Hersteller, Seriennummer, ...) werden in LIN_2_Format geliefert 0: Optionale Daten nicht im LIN_2_Format (nur Defaultwerte werden ausgegeben) |
| SENSOR_HERSTELLER_NR | long | Lieferantennummer des Herstellers wenn Hersteller-Nummer nicht verfuegbar, dann 0 |
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann 'Information nicht verfuegbar' |
| SENSOR_FUNKTIONS_NR | long | Funktionsnummer des Sensors wenn Funktions-Nummer nicht verfuegbar, dann 0 |
| SENSOR_VARIANTEN_NR | long | Variantennummer des Sensors wenn Varianten-Nummer nicht verfuegbar, dann 0 |
| SENSOR_PROD_DATUM | string | Produnktionsdatum (DD.MM.YY) des Sensors wenn Produktions-Datum nicht verfuegbar, dann '--' |
| SENSOR_SERIEN_NR | string | Seriennummer des Sensors wenn Serien-Nummer nicht verfuegbar, dann '--' |
| SENSOR_SW_RELEASE_NR | string | Softwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| SENSOR_HW_RELEASE_NR | string | Hardwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (127 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (25 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (175 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (99 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (5 × 3)
- [FORTTEXTE](#table-forttexte) (70 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [DTCBEREICHE](#table-dtcbereiche) (20 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 9)
- [IORTTEXTE](#table-iorttexte) (12 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (10 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (33 × 16)
- [STATUS_FZM](#table-status-fzm) (5 × 2)
- [SW_ERROR](#table-sw-error) (14 × 2)
- [ARG_0XA01A](#table-arg-0xa01a) (3 × 14)
- [ARG_0XA380](#table-arg-0xa380) (1 × 14)
- [ARG_0XA381](#table-arg-0xa381) (3 × 14)
- [ARG_0XA383](#table-arg-0xa383) (1 × 14)
- [ARG_0XD384](#table-arg-0xd384) (3 × 12)
- [ARG_0XD385](#table-arg-0xd385) (1 × 12)
- [ARG_0XD3AC](#table-arg-0xd3ac) (1 × 12)
- [ARG_0XD3AE](#table-arg-0xd3ae) (1 × 12)
- [ARG_0XD3AF](#table-arg-0xd3af) (1 × 12)
- [ARG_0XD3B1](#table-arg-0xd3b1) (3 × 12)
- [RES_0XA380](#table-res-0xa380) (3 × 13)
- [RES_0XD384](#table-res-0xd384) (3 × 10)
- [RES_0XD385](#table-res-0xd385) (1 × 10)
- [RES_0XD38A](#table-res-0xd38a) (9 × 10)
- [RES_0XD38C](#table-res-0xd38c) (3 × 10)
- [RES_0XD3CF](#table-res-0xd3cf) (3 × 10)
- [ARG_0X4000](#table-arg-0x4000) (1 × 12)
- [ARG_0X4002](#table-arg-0x4002) (2 × 12)
- [ARG_0X4004](#table-arg-0x4004) (2 × 12)
- [ARG_0X410B](#table-arg-0x410b) (1 × 14)
- [RES_0X4001](#table-res-0x4001) (21 × 10)
- [RES_0X4003](#table-res-0x4003) (4 × 10)
- [RES_0X4005](#table-res-0x4005) (4 × 10)
- [RES_0X4007](#table-res-0x4007) (18 × 10)
- [RES_0X4008](#table-res-0x4008) (18 × 10)
- [RES_0X4009](#table-res-0x4009) (18 × 10)
- [RES_0X400A](#table-res-0x400a) (18 × 10)
- [RES_0X410B](#table-res-0x410b) (1 × 13)
- [RES_0X41F1](#table-res-0x41f1) (9 × 10)
- [TSIGNALART](#table-tsignalart) (9 × 2)
- [TAB_BLENDE](#table-tab-blende) (4 × 2)
- [TAB_INIT](#table-tab-init) (3 × 2)
- [TAB_MODUS_PERSONENERKENNUNG](#table-tab-modus-personenerkennung) (4 × 2)
- [TAB_KALIBRIERUNG_NIVI](#table-tab-kalibrierung-nivi) (3 × 2)
- [TAB_DIEBSTAHLSCHUTZ](#table-tab-diebstahlschutz) (6 × 2)
- [TAB_NIVI_PIXELTEST](#table-tab-nivi-pixeltest) (4 × 2)
- [SEITE](#table-seite) (2 × 2)
- [TAB_LINSENHEIZUNG](#table-tab-linsenheizung) (4 × 2)
- [TAB_RICHTUNG](#table-tab-richtung) (2 × 2)
- [TAB_STAT_NIVI_CAM](#table-tab-stat-nivi-cam) (9 × 2)
- [PIXELTEST_MODUS](#table-pixeltest-modus) (2 × 2)
- [TAB_NIVI_STATUS](#table-tab-nivi-status) (5 × 2)
- [TAB_MODE_JUSTAGELINIEN](#table-tab-mode-justagelinien) (3 × 2)
- [VP_CAN_TRACE](#table-vp-can-trace) (3 × 2)
- [TAB_MODUS_BLENDE](#table-tab-modus-blende) (5 × 2)
- [VP__39391829841500](#table-vp-39391829841500) (12 × 2)
- [TVIDEOAUSGANG](#table-tvideoausgang) (11 × 2)
- [TAB_PERSONENERKENNUNG](#table-tab-personenerkennung) (5 × 2)
- [TAB_ARG_LINSENHEIZUNG](#table-tab-arg-linsenheizung) (3 × 2)

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

Dimensions: 127 rows × 2 columns

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 175 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
| 0x03A0 | Druck- Temperatursensor Tank | 1 |
| 0x03C0 | EAC-Sensor | - |
| 0x0400 | Schaltzentrum Lenksäule | - |
| 0x0500 | DSC Sensor-Cluster | - |
| 0x0600 | Nahbereichsradarsensor links | - |
| 0x0700 | Nahbereichsradarsensor rechts | - |
| 0x0800 | Funkempfänger | - |
| 0x0900 | Elektrische Lenksäulenverriegelung | - |
| 0x0A00 | Regen- Lichtsensor | - |
| 0x290A00 | DSC Hydraulikblock | - |
| 0x0B00 | Nightvision Kamera | - |
| 0x0C00 | TLC Kamera | - |
| 0x0D00 | Spurwechselradarsensor hinten links | - |
| 0x0E00 | Heckklima Bedienteil rechts | 1 |
| 0x0F00 | Rearview Kamera hinten | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A20 | Schalterblock Sitzheizung hinten links | 1 |
| 0x1A40 | Schalterblock Sitzheizung hinten rechts | 1 |
| 0x1A60 | Sitzheizung Fahrer | 1 |
| 0x1A80 | Sitzheizung Beifahrer | 1 |
| 0x1AA0 | Sitzheizung Fahrer hinten | 1 |
| 0x1AC0 | Sitzheizung Beifahrer hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1C80 | Sitzverstellschalter Beifahrer über Fond | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1E40 | Heckklappenemblem | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2110 | DWA Mikrowellensensor vorne rechts | 1 |
| 0x2120 | DWA Mikrowellensensor hinten rechts | 1 |
| 0x2130 | DWA Mikrowellensensor hinten links | 1 |
| 0x2140 | DWA Mikrowellensensor vorne links | 1 |
| 0x2150 | DWA Mikrowellensensor hinten | 1 |
| 0x2180 | DWA Ultraschallsensor | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
| 0x2D00 | Smart Opener | 1 |
| 0x2E00 | LED-Hauptlicht-Modul links | 1 |
| 0x2F00 | LED-Hauptlicht-Modul rechts | 1 |
| 0x0910 | Elektrische Lenksäulenverriegelung | 1 |
| 0x3200 | Funkempfänger | 1 |
| 0x3300 | Funkempfänger 2 | 1 |
| 0x3400 | Türgriffelektronik Fahrer | - |
| 0x3500 | Türgriffelektronik Beifahrer | - |
| 0x3600 | Türgriffelektronik Fahrer hinten | - |
| 0x3700 | Türgriffelektronik Beifahrer hinten | - |
| 0x3800 | Telestart-Handsender 1 | - |
| 0x3900 | Telestart-Handsender 2 | - |
| 0x3A00 | Fond-Fernbedienung | - |
| 0x3B00 | Elektrische Wasserpumpe | 1 |
| 0x3B10 | Elektrische Wasserpumpe 1 | 1 |
| 0x3B20 | Elektrische Wasserpumpe 2 | 1 |
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4600 | Nackenwärmer | 1 |
| 0x4700 | Nackenwärmer Bedienschalter | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
| 0x5710 | Satellit Tür links | 0 |
| 0x5718 | Satellit Tür rechts | 0 |
| 0x5720 | Satellit B-Säule links X | 0 |
| 0x5728 | Satellit B-Säule rechts X | 0 |
| 0x5730 | Satellit B-Säule links Y | 0 |
| 0x5738 | Satellit B-Säule rechts Y | 0 |
| 0x5740 | Satellit Zentralsensor X | 0 |
| 0x5748 | Satellit Zentralsensor Y | 0 |
| 0x5750 | Satellit Zentralsensor Low g Y | 0 |
| 0x5758 | Satellit Zentralsensor Low g Z | 0 |
| 0x5760 | Satellit Zentralsensor Roll Achse | 0 |
| 0x5768 | Fussgängerschutz Sensor links | 0 |
| 0x5770 | Fussgängerschutz Sensor rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0x5A00 | Innenlichtelektronik | 1 |
| 0x5B00 | Zentralinstrument | - |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Fahrertür vorne oben | 1 |
| 0x5E06 | Innenbeleuchtung Fahrertür vorne Mitte | 1 |
| 0x5E07 | Innenbeleuchtung Fahrertür vorne unten | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Fahrertür hinten oben | 1 |
| 0x5E0A | Innenbeleuchtung Fahrertür hinten unten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Beifahrertür vorne oben | 1 |
| 0x5E0D | Innenbeleuchtung Beifahrertür vorne Mitte | 1 |
| 0x5E0E | Innenbeleuchtung Beifahrertür vorne unten | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Beifahrertür hinten oben | 1 |
| 0x5E11 | Innenbeleuchtung Beifahrertür hinten unten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung I-Tafel Fahrer oben | 1 |
| 0x5E14 | Innenbeleuchtung I-Tafel Fahrer unten | 1 |
| 0x5E15 | Innenbeleuchtung I-Tafel oben Mitte | 1 |
| 0x5E16 | Innenbeleuchtung I-Tafel unten Mitte | 1 |
| 0x5E17 | Innenbeleuchtung I-Tafel oben Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung I-Tafel unten Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 99 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | DaimlerChrysler |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars (Ford Group) |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis |
| 0x0014 | Microchip |
| 0x0015 | CRF |
| 0x0016 | Renesas Technology Europe GmbH |
| 0x0017 | Atmel |
| 0x0018 | Magnet Marelli |
| 0x0019 | NEC |
| 0x001A | Fujitsu |
| 0x001B | Opel |
| 0x001C | Infineon |
| 0x001D | AMI Semiconductor |
| 0x001E | Vector Informatik |
| 0x001F | Brose |
| 0x0020 | ZMD |
| 0x0021 | ihr |
| 0x0022 | Visteon |
| 0x0023 | ELMOS |
| 0x0024 | ON Semi |
| 0x0025 | Denso |
| 0x0026 | c&s |
| 0x0027 | Renault |
| 0x0028 | Renesas Technology Europe Limited |
| 0x0029 | Yazaki |
| 0x002A | Trinamic Microchips |
| 0x002B | Allegro Microsystems |
| 0x002C | Toyota |
| 0x002D | PSA Peugeot Citroën |
| 0x002E | Westsächsische Hochschule Zwickau |
| 0x002F | Micron AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt Ingenierbüro GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA Hueck & Co. |
| 0x0037 | Continental Temic microelectronic GmbH |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electric Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies |
| 0x0055 | Lear Corporation  |
| 0x0056 | KOSTAL Ireland GmbH |
| 0x0057 | LIPOWSKY Industrie-Elektronik GmbH  |
| 0x0058 | Sanken Electric Co.,Ltd |
| 0x0059 | Elektrobit Automotive GmbH |
| 0x005A | VIMERCATI S.p.A. |
| 0x005B | AB Volvo |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic |
| 0x0061 | Flextronics / Sidler Automotive |
| 0x0062 | EAO Automotive |
| 0x0063 | helag-electronic |
| 0x0064 | Magna International |
| 0x0065 | ARVINMERITOR |
| 0x0066 | Valeo SA |
| 0x0067 | Defond Holding / BJAutomotive |
| 0x0068 | Industrie Saleri S. p. A. |
| 0x0069 | ROHM Semiconductor GmbH |
| 0x0070 | Alfmeier AG |
| 0x0071 | Sanden Corporation |
| 0x0072 | Huf Hülsbeck & Fürst GmbH&Co KG |
| 0x0073 | ebm-papst St. Georgen GmbH&Co. KG |
| 0xFFFF | unbekannter Hersteller |

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

Dimensions: 5 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | kein Betriebsmode |
| 0x01 | Spezieller Energiesparmode | Night Vision 2 deaktiviert |
| 0x02 | ECOS-Mode | Night Vision 2 deaktiviert |
| 0x04 | MOST-Mode | Night Vision 2 deaktiviert |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 70 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x025700 | Energiesparmodus aktiv | 0 |
| 0x02FF57 | Test-DTC für Diagnose-Master-Client, DM_TEST_APPL | 0 |
| 0x800480 | NiVi-Steuergerät, FBAS-Ausgang (+): Kurzschluss nach Plus | 0 |
| 0x800481 | NiVi-Steuergerät, FBAS-Ausgang (-): Kurzschluss nach Plus | 0 |
| 0x800484 | LVDS-Leitungen: Defekt erkannt | 0 |
| 0x800486 | NiVi-Steuergerät, Video-Eingangssignal: Kein Sync-Signal oder Video-Signal von Kamera | 0 |
| 0x800487 | NiVi-Kamera: Unterspannung erkannt | 0 |
| 0x800488 | NiVi-Steuergerät: Stromaufnahme der Kamera zu hoch | 0 |
| 0x80048A | NiVi-Steuergerät: Unterspannung erkannt | 0 |
| 0x80048B | NiVi-Steuergerät: Überspannung erkannt | 0 |
| 0x80048C | NiVi-Kamera: Abschaltung wegen Übertemperatur | 0 |
| 0x80048E | NiVi-Kamera: Heizwendel der Linse defekt | 0 |
| 0x800490 | NiVi-Kamera: Kamera dejustiert | 1 |
| 0x800491 | NiVi-Kamera: IR-Sensor defekt | 0 |
| 0x800492 | NiVi-Kamera: Blendenmotor defekt | 0 |
| 0x800493 | NiVi-Kamera: Maximale Anzahl defekter Pixel überschritten | 0 |
| 0x800494 | NiVi-Kamera: Interner Softwarefehler | 0 |
| 0x800495 | Diebstahlschutz: falsche Zuordnung der Komponenten | 0 |
| 0x800496 | Diebstahlschutz: Freischaltcode für Steuergerät ungültig | 0 |
| 0x800497 | Diebstahlschutz: Freischaltcode für Kamera ungültig | 0 |
| 0x800498 | NiVi-Kamera: Eingefrorenes Bild | 0 |
| 0x800499 | NiVi-Steuergerät: Unzulässige Softwarekonfiguration; Codierung nicht durchgeführt | 0 |
| 0x80049A | NiVi-Steuergerät: Interner Softwarefehler | 0 |
| 0x80049B | NiVi-Steuergerät: Abschaltung wegen Übertemperatur | 0 |
| 0x80049C | NiVi-Steuergerät: Interner Hardwarefehler | 0 |
| 0x80049D | NiVi-Taster: Unzulässigen Tastenstatus erkannt (bei E70) | 1 |
| 0x80049E | NiVi-Steuergerät: Eingefrorenes Bild | 0 |
| 0x8004B0 | Codierung: Steuergerät nicht codiert | 0 |
| 0x8004B1 | Codierung: Fehler bei Codierung aufgetreten | 0 |
| 0x8004B2 | Codierung: Signatur für Daten nicht gültig | 0 |
| 0x8004B3 | Codierung: Codierung passt nicht zum Fahrzeug | 0 |
| 0x8004B4 | Codierung: unplausible Daten während der Transaktion | 0 |
| 0x8004B5 | Gezieltes Anleuchten konnte nicht ausgeführt werden | 0 |
| 0x8004B6 | Blindheit erkannt | 1 |
| 0xDEC40A | FA-CAN Control Module Bus OFF | 0 |
| 0xDECBFF | Test-DTC für Diagnose-Master-Client, DM_TEST_COM | 1 |
| 0xDECC1D | CAN_X-Bus: Module Bus Off | 0 |
| 0xDEE400 | Botschaft (0x28A, Bedienung Taster Night-Vision): Ausfall | 1 |
| 0xDEE402 | Botschaft (0x3A0, Fahrzeugzustand): Ausfall | 1 |
| 0xDEE403 | Botschaft (0x1A1, Geschwindigkeit Fahrzeug): Ausfall | 1 |
| 0xDEE404 | Botschaft (0x19F, Giergeschwindigkeit Fahrzeug): Ausfall | 1 |
| 0xDEE405 | Botschaft (0x330, Kilometerstand/Reichweite): Ausfall | 1 |
| 0xDEE406 | Botschaft (0x21A, Lampenzustand): Ausfall | 1 |
| 0xDEE407 | Botschaft (0x199, Längsbeschleunigung Schwerpunkt): Ausfall | 1 |
| 0xDEE409 | Botschaft (0x328, Relativzeit): Ausfall | 1 |
| 0xDEE40A | Botschaft (0x314, Status Fahrlicht): Ausfall | 1 |
| 0xDEE40B | Botschaft (0x23A, Status Funkschlüssel): Ausfall | 1 |
| 0xDEE40C | Botschaft (0x380, Fahrgestellnummer): Ausfall | 1 |
| 0xDEE40D | Botschaft (0x2A5, Status Helligkeit Umgebung): Ausfall | 1 |
| 0xDEE40E | Botschaft (0x2CA, Aussentemperatur): Ausfall | 1 |
| 0xDEE410 | Botschaft (0x213, Status HUD): Ausfall | 1 |
| 0xDEE411 | Botschaft (0x3F9, Daten Antriebsstrang 2): Ausfall | 1 |
| 0xDEE412 | Botschaft (0x1D7, Status GZA Rechts): Ausfall | 1 |
| 0xDEE413 | Botschaft (0x1BE, Status GZA Links): Ausfall | 1 |
| 0xDEE414 | Botschaft (0x95, Objektdaten blendfreier Fernlicht-Assistent): Ausfall | 1 |
| 0xDEE415 | Botschaft (0x163, Neigung Fahrbahn): Ausfall | 1 |
| 0xDEEC04 | Signal (0x28A) ungültig empfangen: Bedienung_Taster_Night-Vision | 1 |
| 0xDEEC07 | Signal (0x19F) ungültig empfangen: Giergeschwindigkeit_Fahrzeug | 1 |
| 0xDEEC09 | Signal (0x199) ungültig empfangen: Längsbeschleunigung_Schwerpunkt | 1 |
| 0xDEEC0A | Signal (0x226) ungültig empfangen: Status_Regensensor | 1 |
| 0xDEEC0B | Signal (0x314) ungültig empfangen: Status_Sensor_Fahrlicht | 1 |
| 0xDEEC0C | Signal (0x380) ungültig empfangen: Nummer_Fahrgestell | 1 |
| 0xDEEC0D | Signal (0x2A5) ungültig empfangen: Wert_Helligkeit_Umgebung | 1 |
| 0xDEEC0E | Signal (0x2CA) ungültig empfangen: Aussentemperatur | 1 |
| 0xDEEC0F | Signal (0x252) ungültig empfangen: Position_Wischerblatt | 1 |
| 0xDEEC10 | Signal (0x213) ungültig empfangen: Status_Backlight_HUD | 1 |
| 0xDEEC11 | Signal (0x3F9) ungültig empfangen: Status_Antrieb_Fahrzeug | 1 |
| 0xDEEC12 | Signal (0x95) ungültig empfangen: Objektdaten blendfreier Fernlicht-Assistent | 1 |
| 0xDEEC13 | Signal (0x163) ungültig empfangen: Neigung_Fahrbahn | 1 |
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
| SystembusDTC | DEC41F | DEC43E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC43F | DEC449 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC47D | DEC486 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC40B | DEC414 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC401 | DEC40A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930030 | 930055 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC473 | DEC47C | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC50B | DEC514 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC487 | DEC48F | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC415 | DEC41E | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC501 | DEC50A | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | 930000 | 930011 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC469 | DEC472 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SystembusDTC | DEC45F | DEC468 | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SubbusDTC | DECC00 | DED3FF | Zulässiger Bereich wird mittels Formel berechnet. Enthält physikalische Fehler bzw. Protokollfehler des Systembusses. |
| SignalDTC | DED400 | DF03FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | DED400 | DF03FF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| SignalDTC | DECBFF | DECBFF | Ist aus einem vorgegebenen Offset-Bereich frei wählbar. Enthält Signalfehler, die SG-spezifisch sind. |
| KomponentenDTC | 800480 | 8004FF | Die zulässigen Bereiche sind für jedes Steuergerät festgelegt. Es können mehrere gültige Bereiche (Kacheln) definiert werden. |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x6F00 | Operation_Status_FZM | 0-n | - | 0xFF | STATUS_FZM | 1 | 1 | 0 |
| 0x6F01 | Kamera_Strom | mA | - | unsigned char | - | 10 | 1 | 0 |
| 0x6F02 | Betriebsspannung_Steuergerät | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x6F03 | Temperatur_Steuergerät | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F04 | STAT_X_CAN_Verbindung | mA | - | unsigned char | - | 1 | 1 | 0 |
| 0x6F05 | Temperatur_Kamera | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F06 | Betriebsstunden_Kamera | Std | - | signed long | - | 1 | 3600 | 0 |
| 0x6F07 | Kamera_Spannung | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x6F08 | Heizung_Temperatur | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F09 | Software_Error | 0-n | - | 0xFFFF | SW_ERROR | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 12 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x57000A | DM_Queue_DELETED | 0 |
| 0x570005 | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x570002 | NVM_E_CONTROL_FAILED | 0 |
| 0x570006 | NVM_E_READ_ALL_FAILED | 0 |
| 0x570001 | NVM_E_READ_FAILED | 0 |
| 0x570004 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x570003 | NVM_E_ERASE_FAILED | 0 |
| 0x570007 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 |
| 0x570009 | DM_Queue_FULL | 0 |
| 0x570000 | NVM_E_WRITE_FAILED | 0 |
| 0x570008 | PIA_E_IO_ERROR | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | ja |
| F_HLZ | ja |
| F_SEVERITY | ja |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x6F00 | Operation_Status_FZM | 0-n | - | 0xFF | STATUS_FZM | 1 | 1 | 0 |
| 0x6F01 | Kamera_Strom | mA | - | unsigned char | - | 10 | 1 | 0 |
| 0x6F02 | Betriebsspannung_Steuergerät | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x6F03 | Temperatur_Steuergerät | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F04 | STAT_X_CAN_Verbindung | mA | - | unsigned char | - | 1 | 1 | 0 |
| 0x6F05 | Temperatur_Kamera | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F06 | Betriebsstunden_Kamera | Std | - | signed long | - | 1 | 3600 | 0 |
| 0x6F07 | Kamera_Spannung | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x6F08 | Heizung_Temperatur | °C | - | signed char | - | 1 | 1 | 0 |
| 0x6F09 | Software_Error | 0-n | - | 0xFFFF | SW_ERROR | 1 | 1 | 0 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 33 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SIGNALAUSGABE | 0xA01A | - | Steuert die Videosignalausgabe eines Steuergerätes (Videoquelle). | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA01A | - |
| PIXELTEST_NIVI_KAM | 0xA380 | - | Auslösen der Korrektur toter Pixel in der Kamera.  Zu diesem Zweck wird das Bild mit/ohne Shutter verglichen.  Die Anzahl toter Pixel und Cluster kann nach Ausführung ausgelesen werden. | - | Modus | - | - | - | - | - | - | - | 31 | ARG_0xA380 | RES_0xA380 |
| GZA_TEST_MODE | 0xA381 | - | Demomode für gezieltes Anleuchten | - | Seite | - | - | - | - | - | - | - | 31 | ARG_0xA381 | - |
| DEMO_MODE_GEZIELTES_ANLEUCHTEN | 0xA382 | - | Demo Mode für gezieltes Anleuchten | - | - | - | - | - | - | - | - | - | 31 | - | - |
| JUSTAGELINIEN | 0xA383 | - | Blendet Justagelinien ins NIVI Bild ein. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA383 | - |
| BUS_IN_TASTE_NIVI_EIN | 0xD382 | STAT_BUS_IN_TASTE_NIVI_EIN | Signal Taster NIVI über BUS, 0= Taster nicht gedrückt, 1= Taster gedrückt | 0/1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| KALIBRIERUNG_NIVI | 0xD384 | - | Der Aufruf liest oder schreibt den Rotations- Nick- und Gierwinkel für die Kamerajustage NIVI. | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD384 | RES_0xD384 |
| SENSOR_ZEILEN_LESEN | 0xD385 | - | Auslesen der gewünschten Sensor-Zeile. | - | - | - | - | - | - | - | - | - | 2F | ARG_0xD385 | RES_0xD385 |
| DIEBSTAHLSCHUTZ_NIVI | 0xD387 | STAT_DIEBSTAHLSCHUTZ_NIVI | Results siehe TAB_DIEBSTAHLSCHUTZ | 0-n | - | - | unsigned char | TAB_DIEBSTAHLSCHUTZ | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NIVI_KAMERA | 0xD38A | - | Ausgabe der verschieden Stati der NiVi-Kamera. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD38A |
| KALIBRIERUNG_NIVI_INIT | 0xD38B | STAT_KALIBRIERUNG_NIVI_INIT | 0 (0x00) = nicht initialisiert, 1 (0x01) =  Initialisierung in Ordnung, 255 (0xFF) = Initialisierung nicht in Ordnung | 0-n | - | - | unsigned char | TAB_INIT | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NIVI_STEUERGERAET | 0xD38C | - | Ausgabe der verschiedenen Betriebsstati des NiVi-Steuergerätes. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD38C |
| PERSONENERKENNUNG_NIVI | 0xD3AC | - | Einschalten der Personenerkennung, auch wenn aufgrund der Umweltbedingungen eine Deaktivierung erfolgen würde. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD3AC | - |
| STEUERN_NIVI_KAM_BLENDE | 0xD3AE | - | Ansteuerung des Blendenmotors der NiVi-Kamera. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD3AE | - |
| STEUERN_NIVI_KAM_HEIZUNG | 0xD3AF | - | Ansteuerung der Linsenheizung der NiVi-Kamera. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD3AF | - |
| KALIBRIERUNG_SERVICE_NIVI | 0xD3B1 | - | Startet die Kalibrierung der NIVI-Kameras mit Hilfe der Software im Service. Es wird solange das  Referenzbild angezeigt, bis Argument REFERENZBILD wieder auf 0 oder 2 geht. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD3B1 | - |
| BLINDHEITSERKENNUNG | 0xD3CF | - | Status Blindheitserkennung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD3CF |
| SPANNUNG_KLEMME_15N_WERT | 0xDAD2 | STAT_SPANNUNG_KLEMME_15N_WERT | Spannungswert am Steuergerät an Klemme 15N (auf eine Nachkommastelle genau) | Volt | - | - | int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| STATUS_KLEMME_15_EIN | 0xDAFE | STAT_STATUS_KLEMME_15_EIN | Status Klemme 15 im Steuergerät: 0=AUS; 1=EIN | 0/1 | - | - | int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NACHLAUFZEIT_KLEMME_15N | 0xDB2D | STAT_NACHLAUFZEIT_KLEMME_15N_WERT | Das Result enthält die Nachlaufzeit der Klemme 15N in Sekunden. | s | - | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _STEUERN_BLENDE_ZYKLUSZEIT | 0x4000 | - | Der Job setzt die Zykluszeit des Shutters. Hinweis: die Zykluszeit wird auch von der Temperatur beeinflusst. Es kannn zu Shutteroperationen innerhalb der gesetzten Zykluszeit kommen. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4000 | - |
| _STATUS_MCU_ADC | 0x4001 | - | Der Job liest die Spannungswerte der 1. Port-Klasse des bidirektionalen Analog/Digital-Konverters aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4001 |
| _STEUERN_MCU_ADC | 0x4002 | - | Der Job setzt den gewählten Port des ADC auf definierten Wert. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4002 | - |
| _STATUS_MCU_IO | 0x4003 | - | Der Job gibt die eingestellten Binärwerte der IO-Ports zurück. Hierbei gilt, jedes Bit entspricht entprechend der Position im Byte einem Port. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4003 |
| _STEUERN_MCU_IO | 0x4004 | - | Der Job setzt den gewählten IO-Port auf den definierten Wert. PORT_VALUE=0x00 nicht aktiv, PORT_VALUE=0x01 aktiv. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4004 | - |
| _STATUS_CAM_VERSION | 0x4005 | - | Job reports following camera informations: serial number, assembly number, firmware number, software number. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4005 |
| _STAT_TASTER | 0x4006 | STAT_TASTER | NIVI-Button not activated-&gt;0, activated-&gt;1 | 0/1 | - | high | char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _STATUS_OPERATING_HOURS__AMB_CAM | 0x4007 | - | Ambient camera temperature operating time for        T &lt; -20C; STAT_..._M20C_WERT  -20C&lt; T &lt;=  0C; STAT_..._M20C__0C_WERT    0C&lt; T &lt;= 30C; STAT_..._0C__30C_WERT   30C&lt; T &lt;= 60C; STAT_..._30C__60C_WERT   60C&lt; T &lt;= 80C; STAT_..._60C__80C_WERT   80C&lt; T       ; STAT_..._80C_WERT | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4007 |
| _STATUS_OPERATING_HOURS__INT_MCU | 0x4008 | - | Ambient ecu temperature operating hours for        T &lt; -20C; STAT_..._M20C_WERT  -20C&lt; T &lt;=  0C; STAT_..._M20C__0C_WERT    0C&lt; T &lt;= 30C; STAT_..._0C__30C_WERT   30C&lt; T &lt;= 60C; STAT_..._30C__60C_WERT   60C&lt; T &lt;= 80C; STAT_..._60C__80C_WERT   80C&lt; T       ; STAT_..._80C_WERT | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4008 |
| _STATUS_OPERATING_HOURS__INT_CAM | 0x4009 | - | Internal camera temperature operating hours for        T &lt; -20C; STAT_..._M20C_WERT  -20C&lt; T &lt;=  0C; STAT_..._M20C__0C_WERT    0C&lt; T &lt;= 30C; STAT_..._0C__30C_WERT   30C&lt; T &lt;= 60C; STAT_..._30C__60C_WERT   60C&lt; T &lt;= 80C; STAT_..._60C__80C_WERT   80C&lt; T       ; STAT_..._80C_WERT | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4009 |
| _STATUS_OPERATION_HOURS__INT_MCU_VP | 0x400A | - | Internal ecu temperature operating hours for        T &lt; -20C; STAT_..._M20C_WERT  -20C&lt; T &lt;=  0C; STAT_..._M20C__0C_WERT    0C&lt; T &lt;= 30C; STAT_..._0C__30C_WERT   30C&lt; T &lt;= 60C; STAT_..._30C__60C_WERT   60C&lt; T &lt;= 80C; STAT_..._60C__80C_WERT   80C&lt; T       ; STAT_..._80C_WERT | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x400A |
| _STEUERN_CAN_TRACE | 0x410B | - | PQ-Import | - | - | - | - | - | - | - | - | - | 31 | ARG_0x410B | RES_0x410B |
| _STATUS_UPTIME | 0x41F1 | - | ECU shall report the uptime status. Each counter shall be counted up from 0 seconds at power-on of the component (MCU/VP/CAM) and increment by one each second. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x41F1 |

<a id="table-status-fzm"></a>
### STATUS_FZM

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Standby |
| 0X02 | Basisbetrieb |
| 0x03 | Startbereitschaft |
| 0x04 | Fahren |
| 0x0F | Signal ungültig |

<a id="table-sw-error"></a>
### SW_ERROR

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | No error |
| 0x8001 | The camera reset condition is equal to  watchdog reset |
| 0x8002 | The camera software error bit is set |
| 0x8003 | ST_RECOVERY_FAIL=TRUE, camera failed to start or is not connected. |
| 0x8004 | CAM status message timeout (2 seconds), could be caused by camera not connected. |
| 0x8005 | CAM request error (no response on CAN, negative response on CAN) |
| 0xC402 | Coding blocks are not transferred in time |
| 0xC802 | DSP B not responding |
| 0xC80C | DSP A main loop is exceeding its timeout |
| 0xC80D | DSP B main loop is exceeding its timeout |
| 0xC80E | Configuration lost during runtime |
| 0xC80F | FPGA configuration failed |
| 0xC810 | Error handler not responding |
| 0xFFFF | signal ungültig |

<a id="table-arg-0xa01a"></a>
### ARG_0XA01A

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SIGNALART | + | - | 0-n | - | unsigned char | - | TSignalArt | 1.0 | 1.0 | 0.0 | - | - | Art der Signalausgabe. |
| ARG_AUSGANG | + | + | 0-n | - | unsigned int | - | TVideoAusgang | 1.0 | 1.0 | 0.0 | - | - | Default: 0 Alle Ausgänge des Steuergerätes müssen einzeln und kombiniert anwählbar sein. |
| ARG_TIMEOUT | + | - | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Wertebereich: 0-30,255 0 schaltet wieder auf Normalbetrieb. 255 schaltet das Signal ohne einen TIMEOUT. Ansonsten legt dies Zahl die Sekunden fest, die das Testbild ausgegeben wird. Default: 255 Wird dieser Parameter nicht angegeben, erfolgt eine Ausgabe, bis: -der Job erneut mit Parameter 0 aufgerufen wird -das Steuergerät neu startet (Aufwachen, Reset, &) |

<a id="table-arg-0xa380"></a>
### ARG_0XA380

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MODUS | + | - | 0-n | high | unsigned char | - | PIXELTEST_MODUS | - | - | - | - | - | Modus |

<a id="table-arg-0xa381"></a>
### ARG_0XA381

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SEITE | + | - | 0-n | high | unsigned char | - | SEITE | - | - | - | - | - | Angesteuertes Licht: 0x01 = Linke Seite 0x02 = Rechte Seite |
| WINKEL | + | - | ° | high | unsigned char | - | - | 1.0 | 0.1 | 125.0 | - | - | Winkel für Anleuchten ( -12.5 ... 12.5°) |
| DISTANZ | + | - | m | high | unsigned char | - | - | 1.0 | 5.0 | -4.0 | - | - | Virtuelle Distanz: (20 ... 90 m) |

<a id="table-arg-0xa383"></a>
### ARG_0XA383

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MODE | + | - | 0-n | high | unsigned char | - | TAB_MODE_JUSTAGELINIEN | 1.0 | 1.0 | 0.0 | - | - | Mode der Justagelinienanzeige: 0x01 = Mode1: Im Bild zentiert 0x02 = Mode 2: Mit Korrektur aus Online-Kalibrierung 0x03 = Mode 3: |

<a id="table-arg-0xd384"></a>
### ARG_0XD384

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ROTATIONSWINKEL | Grad | - | char | - | - | 10.0 | 1.0 | 0.0 | -2.0 | 2.0 | Im Werksprozess (CASCADE) festgestellten Winkel am Halter, Winkel aufgelöst in 0,1° Schritten im Bereich +/- 12,7°  0-127 entspricht 0° - 12,7°  128-255 entspricht (-12,7°) - (-0,1°) |
| NICKWINKEL | Grad | - | char | - | - | 10.0 | 1.0 | 0.0 | -2.0 | 2.0 | Angabe des in der ECU zu speichernden Nickwinkels auf 10-tel Grad genau (z.B. 2,3 °). |
| GIERWINKEL | Grad | - | char | - | - | 10.0 | 1.0 | 0.0 | -2.0 | 2.0 | Angabe des in der ECU zu speichernden Gierwinkels auf 10-tel Grad genau (z.B. 2,3 °). |

<a id="table-arg-0xd385"></a>
### ARG_0XD385

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| IDENTIFIER | hex | - | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Ausgabe der gewünschten Zeile des Sensors.  IDENTIFIER = XX YY Hex,  XX h =  0x01: Pixel 1 - 160 der Zeile,  0x02: Pixel 161 - 320 der Zeile,  YY h =  0x01 - 0xF0: für die Zeile (1 - 240) |

<a id="table-arg-0xd3ac"></a>
### ARG_0XD3AC

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSMODUS | 0-n | - | unsigned char | - | TAB_MODUS_PERSONENERKENNUNG | 1.0 | 1.0 | 0.0 | - | - | STOPP = Ansteuerung beenden, AUS = Personenerkennung AUS, EIN = Personenerkennung EIN (unabhängig von Umweltbedingungen), AUTO = Personenerkennung AUTO (mit Umweltbedingungsprüfung) |

<a id="table-arg-0xd3ae"></a>
### ARG_0XD3AE

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | unsigned char | - | TAB_BLENDE | 1.0 | 1.0 | 0.0 | - | - | Ansteuerung der Blende der NiVi-Kamera: Argument siehe TAB_BLENDE |

<a id="table-arg-0xd3af"></a>
### ARG_0XD3AF

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | unsigned char | - | TAB_ARG_LINSENHEIZUNG | 1.0 | 1.0 | 0.0 | - | - | Ansteuerung der Linsenheizung der NiVi-Kamera: Argumente siehe TAB_ARG_LINSENHEIZUNG |

<a id="table-arg-0xd3b1"></a>
### ARG_0XD3B1

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REFERENZBILD | 0-n | - | unsigned char | - | TAB_KALIBRIERUNG_NIVI | 1.0 | 1.0 | 0.0 | - | - | 0 = Abbrechen Kalibrierung ohne Speichern der Daten und zurück zur normalen Ansicht 1 = Referenzbild mit Ansicht der Justagelinien durch die Veränderung der Werte in Argumenten 2 = Beenden Kalibrierung mit Speichern der Daten und zurück zur normalen Ansicht |
| RICHTUNG | 0-n | - | unsigned char | - | TAB_RICHTUNG | 1.0 | 1.0 | 0.0 | - | - | Angabe der Richtung der Verstellung in Pixel.  1 = OBEN = nach oben,  2 = UNTEN = nach unten |
| ANZ_SCHRITTE | Pixel | - | char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vertikale Verschiebung um die Anzahl der Zeile nach oben bzw unten. 1 - 20 Zeilen. Default = 1, wenn nicht gesetzt. |

<a id="table-res-0xa380"></a>
### RES_0XA380

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PIXELTEST_NR | - | - | + | 0-n | - | unsigned char | - | TAB_NIVI_PIXELTEST | 1.0 | 1.0 | 0.0 | 0 = Test abgebrochen, nicht angefordert,  1 = Test in Ausführung,  2 = Test erfolgreich abgeschlossen,  3 = Test fehlgeschlagen |
| STAT_NIVI_KAM_DEFEKTE_PIXEL_WERT | - | - | + | Pixel | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Anzahl defekter Pixel. |
| STAT_NIVI_KAM_DEFEKTE_CLUSTER_WERT | - | - | + | Cluster | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Anzahl defekter Cluster (Bereiche zusammenhängender defekter Pixel). |

<a id="table-res-0xd384"></a>
### RES_0XD384

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROTATIONSWINKEL_WERT | Grad | - | char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des in der ECU gespeicherten Rotationswinkels bis auf 10-tel Grad (z.B. 2,3 °). |
| STAT_NICKWINKEL_WERT | Grad | - | char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des in der ECU gespeicherten Nickwinkels bis auf 10-tel Grad (z.B. 2,3 °). |
| STAT_GIERWINKEL_WERT | Grad | - | char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des in der ECU gespeicherten Gierwinkels bis auf 10-tel Grad (z.B. 2,3 °). |

<a id="table-res-0xd385"></a>
### RES_0XD385

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NIVI_KAM_ZEILEN_WERT | - | - | data[160] | - | - | 1.0 | 1.0 | 0.0 | Ergebnis [IDENTIFIER, Byte 1, ... , Byte 160] IDENTIFIER = XX YY Hex Byte 1 bis Byte 160 sind die Pixelwerte |

<a id="table-res-0xd38a"></a>
### RES_0XD38A

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NIVI_KAM_FUNKTION | 0-n | - | unsigned char | - | TAB_STAT_NIVI_CAM | 1.0 | 1.0 | 0.0 | Ausgabe des Betriebsstatus der Kamera. Siehe Tabelle TAB_STAT_NIVI_CAM |
| STAT_NIVI_KAM_SPANNUNG_WERT | V | - | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe der Kamerabetriebsspannung bis auf 10-tel Volt. |
| STAT_NIVI_KAM_STROM_WERT | mA | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Ausgabe der Stromaufnahme der Kamera in mA. |
| STAT_NIVI_KAM_TEMP_WERT | °C | - | char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Temperatur der Kamera. |
| STAT_NIVI_KAM_BLENDE_ZYKLUSZEIT_WERT | s | - | int | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Zykluszeit der Blende in Sekunden. |
| STAT_NIVI_KAM_BLENDE | 0-n | - | unsigned char | - | TAB_MODUS_BLENDE | 1.0 | 1.0 | 0.0 | Ausgabe des Betriebsmodus der Blende: Results siehe TAB_MODUS_BLENDE |
| STAT_NIVI_KAM_TEMP_HEIZUNG_WERT | °C | - | char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Temperatur der Linsen vor der Kamera. |
| STAT_NIVI_KAM_LINSENHEIZUNG_EIN | 0-n | - | unsigned char | - | TAB_LINSENHEIZUNG | 1.0 | 1.0 | 0.0 | Ausgabe des Status der Linsenheizung: Results siehe TAB_LINSENHEIZUNG |
| STAT_NIVI_KAM_BETRIEBSSTUNDEN_WERT | Stunden | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Betriebsstunden der Kamera in Stunden. |

<a id="table-res-0xd38c"></a>
### RES_0XD38C

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NIVI_SYSTEM | 0-n | - | unsigned char | - | TAB_NIVI_STATUS | 1.0 | 1.0 | 0.0 | Gibt aus, ob Night-Vision eingeschaltet ist: Results siehe TAB_NIVI_STATUS |
| STAT_NIVI_PERSONENERKENNUNG | 0-n | - | unsigned char | - | TAB_PERSONENERKENNUNG | - | - | - | Gibt aus, ob Personenerkennung eingeschaltet ist: Results siehe TAB_PERSONENERKENNUNG |
| STAT_NIVI_ECU_TEMP_WERT | °C | - | char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der Temperatur des Steuergerätes. |

<a id="table-res-0xd3cf"></a>
### RES_0XD3CF

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KONTRAST_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kontrast der Kamera |
| STAT_DAUER_BIS_CCM_BLINDHEIT_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Dauer der Blindheit in Minuten (0-254), 0xFF wenn Blindheit beim Aufstarten erkannt. Zeit = (Coding-Wert) ¿ (Zeit seit Blockade im Bild) |
| STAT_DAUER_BIS_CCM_NACH_BLINDHEIT_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Dauer in Sekunden (0-254) nach Blindheit, wenn Erkennung wieder aktiv , 0xFF wenn keine Blindheit erkannt wurde. Zeit = (Coding-Wert-2)-(Zeit Ohne Blockade) |

<a id="table-arg-0x4000"></a>
### ARG_0X4000

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CONTROL_SHUTTER_TIME | s | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | CONTROL_SHUTTER_TIME |

<a id="table-arg-0x4002"></a>
### ARG_0X4002

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MCU_ADC_PORT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | - | - | MCU_ADC_PORT |
| MCU_ADC_VALUE | HEX | high | unsigned int | - | - | - | - | - | - | - | MCU_ADC_VALUE |

<a id="table-arg-0x4004"></a>
### ARG_0X4004

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MCU_IO_PORT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | - | - | - |
| MCU_IO_VALUE | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | - | - | - |

<a id="table-arg-0x410b"></a>
### ARG_0X410B

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VP_ | - | - | 0-n | - | char | - | VP__39391829841500 | 1.0 | 1.0 | 0.0 | - | - | - |

<a id="table-res-0x4001"></a>
### RES_0X4001

Dimensions: 21 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VIDEO_DAC__3V_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port00: Video_DAC-Referenz -3V |
| STAT_CORE_VOLTAGE_1.2V_WERT | V | high | unsigned int | - | - | 3.3 | 1024.0 | 0.0 | Port01: Core Spannung 1.2V |
| STAT_CORE_VOLTAGE_1.4V_WERT | V | high | unsigned int | - | - | 3.3 | 1024.0 | 0.0 | Port02: Core Spannung 1.4 V |
| STAT_IO_VOLTAGE_2.5V_WERT | V | high | unsigned int | - | - | 3.3 | 1024.0 | 0.0 | Port03: IO Spannung 2.5V |
| STAT_IO_VOLTAGE_5V_WERT | V | high | unsigned int | - | - | 6.6 | 1024.0 | 0.0 | Port04: IO Spannung 5V |
| STAT_SYSTEM_TEMPERATUR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port05: Temperature Sensor at DSP A |
| STAT_SWITCHED_BATT_VOLTAGE_WERT | V | high | unsigned int | - | - | 36.3 | 1024.0 | 0.64 | Port06: geschaltete Batteriespannung |
| STAT_VIDEO_OUT_POS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port07: positiver Videoausgang |
| STAT_VIDEO_OUT_NEG_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port08: negativer Videoausgang |
| STAT_CAM_PWR_VOLTAGE_WERT | V | high | unsigned int | - | - | 36.3 | 1024.0 | 0.73 | Port09: Kamera Betriebsspannung |
| STAT_CAM_PWR_CURRENT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0A: Kamera Betriebsstrom |
| STAT_DFBAS_IN_POS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0B: Videoausgang, pos. DFBAS |
| STAT_DFBAS_IN_NEG_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0C: Videoausgang, neg. DFBAS |
| STAT_PU_BU_VOLTAGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0D: Ein/Aus-Tastensignal |
| STAT_CAM_CAN_MEAN_VOLTAGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0E: Kamera-CAN_Bus-Mittelwertspannung |
| STAT_VEH_CAN_MEAN_VOLTAGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port0F: Fahrzeug-CAN_Bus-Mittelwertspannung |
| STAT_WUP_SIGNAL_VOLTAGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port10: Weckleitung (Wake Up)-Signalspannung - nicht benutzt |
| STAT_SYSTEM_TEMPERATUR2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port11:Temperature Sensor at Video DAC |
| STAT_SYSTEM_TEMPERATUR3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port12: Temperature Sensor at FPGA |
| STAT_SYSTEM_TEMPERATUR4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port13: Temperature Sensor at DSP B |
| STAT_HW_IDENT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Port14: Hardware Identification |

<a id="table-res-0x4003"></a>
### RES_0X4003

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PORT_BYTE_0_WERT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | Port 00..07 |
| STAT_PORT_BYTE_1_WERT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | Port 08..15 |
| STAT_PORT_BYTE_2_WERT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | Port 16..23 |
| STAT_PORT_BYTE_3_WERT | HEX | high | char | - | - | 1.0 | 1.0 | 0.0 | Port 24..31. Maske = 0x1f |

<a id="table-res-0x4005"></a>
### RES_0X4005

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SERIAL_WERT | - | high | string[10] | - | - | 1.0 | 1.0 | 0.0 | SERIAL |
| STAT_ASSEMBLY_WERT | - | high | string[20] | - | - | 1.0 | 1.0 | 0.0 | ASSEMBLY |
| STAT_FIRMWARE_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | FIRMWARE |
| STAT_SOFTWARE_WERT | - | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | SOFTWARE |

<a id="table-res-0x4007"></a>
### RES_0X4007

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMB_CAM_M20C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T &lt; -20 C Hours |
| STAT_AMB_CAM_M20C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T&lt;-20 C Minutes |
| STAT_AMB_CAM_M20C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T&lt;-20 C Seconds |
| STAT_AMB_CAM_M20C__0C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for -20&lt;T&lt;=0 C Hours |
| STAT_AMB_CAM_M20C__0C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for -20&lt;T&lt;=0 C Minutes |
| STAT_AMB_CAM_M20C__0C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for -20&lt;T&lt;=0 C Seconds |
| STAT_AMB_CAM_0C__30C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 0&lt;T&lt;=30 C Hours |
| STAT_AMB_CAM_0C__30C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 0&lt;T&lt;=30 C Minutes |
| STAT_AMB_CAM_0C__30C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 0&lt;T&lt;=30 C Seconds |
| STAT_AMB_CAM_30C__60C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 30&lt;T&lt;=60 C Hours |
| STAT_AMB_CAM_30C__60C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 30&lt;T&lt;=60 C Minutes |
| STAT_AMB_CAM_30C__60C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 30&lt;T&lt;=60 C Seconds |
| STAT_AMB_CAM_60C__80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 60&lt;T&lt;=80 C Hours |
| STAT_AMB_CAM_60C__80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 60&lt;T&lt;=80 C Minutes |
| STAT_AMB_CAM_60C__80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for 60&lt;T&lt;=80 C Seconds |
| STAT_AMB_CAM_80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T&gt;80 C Hours |
| STAT_AMB_CAM_80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T&gt;80 C Minutes |
| STAT_AMB_CAM_80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ambient temperature camera operating time for T&gt;80 C Seconds |

<a id="table-res-0x4008"></a>
### RES_0X4008

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INT_MCU_M20C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&lt;-20 C Hours |
| STAT_INT_MCU_M20C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&lt;-20 C Minutes |
| STAT_INT_MCU_M20C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&lt;-20 C Seconds |
| STAT_INT_MCU_M20C__0C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for -20&lt;T&lt;=0 C Hours |
| STAT_INT_MCU_M20C__0C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for -20&lt;T&lt;=0 C Minutes |
| STAT_INT_MCU_M20C__0C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for -20&lt;T&lt;=0 C Seconds |
| STAT_INT_MCU_0C__30C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 0&lt;T&lt;=30 C Hours |
| STAT_INT_MCU_0C__30C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 0&lt;T&lt;=30 C Minutes |
| STAT_INT_MCU_0C__30C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 0&lt;T&lt;=30 C Seconds |
| STAT_INT_MCU_30C__60C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 30&lt;T&lt;=60 C Hours |
| STAT_INT_MCU_30C__60C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 30&lt;T&lt;=60 C Minutes |
| STAT_INT_MCU_30C__60C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 30&lt;T&lt;=60 C Seconds |
| STAT_INT_MCU_60C__80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 60&lt;T&lt;=80 C Hours |
| STAT_INT_MCU_60C__80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 60&lt;T&lt;=80 C Minutes |
| STAT_INT_MCU_60C__80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for 60&lt;T&lt;=80 C Seconds |
| STAT_INT_MCU_80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&gt;80 C Hours |
| STAT_INT_MCU_80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&gt;80 C Minutes |
| STAT_INT_MCU_80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal MCU operating time for T&gt;80 C Seconds |

<a id="table-res-0x4009"></a>
### RES_0X4009

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INT_CAM_M20C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for T&lt;-20 C Hours |
| STAT_INT_CAM_M20C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for T&lt;-20 C Minutes |
| STAT_INT_CAM_M20C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for T&lt;-20 C Seconds |
| STAT_INT_CAM_M20C__0C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for -20&lt;T&lt;=0 C Hours |
| STAT_INT_CAM_M20C__0C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for -20&lt;T&lt;=0 C Minutes |
| STAT_INT_CAM_M20C__0C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for -20&lt;T&lt;=0 C Seconds |
| STAT_INT_CAM_0C__30C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for 0&lt;T&lt;=30 C Hours |
| STAT_INT_CAM_0C__30C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for 0&lt;T&lt;=30 C Minutes |
| STAT_INT_CAM_0C__30C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  0&lt;T&lt;=30 C Seconds |
| STAT_INT_CAM_30C__60C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  30&lt;T&lt;=60 C Hours |
| STAT_INT_CAM_30C__60C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  30&lt;T&lt;=60 C Minutes |
| STAT_INT_CAM_30C__60C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  30&lt;T&lt;=60 C Seconds |
| STAT_INT_CAM_60C__80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for 60&lt;T&lt;=80 C Hours |
| STAT_INT_CAM_60C__80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for 60&lt;T&lt;=80 C Minutes |
| STAT_INT_CAM_60C__80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for 60&lt;T&lt;=80 C Seconds |
| STAT_INT_CAM_80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for T&gt;80 C Hours |
| STAT_INT_CAM_80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  T&gt;80 C Minutes |
| STAT_INT_CAM_80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Internal camera temperature operating time for  T&gt;80 C Seconds |

<a id="table-res-0x400a"></a>
### RES_0X400A

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INT_MCU_VP_M20C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&lt;-20 C Hours |
| STAT_INT_MCU_VP_M20C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&lt;-20 C Minutes |
| STAT_INT_MCU_VP_M20C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&lt;-20 C Seconds |
| STAT_INT_MCU_VP_20C__0C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for -20&lt;T&lt;=0 C Hours |
| STAT_INT_MCU_VP_20C__0C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for -20&lt;T&lt;=0 C Minutes |
| STAT_INT_MCU_VP_20C__0C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for -20&lt;T&lt;=0 C Seconds |
| STAT_INT_MCU_VP_0C__30C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 0&lt;T&lt;=30 C Hours |
| STAT_INT_MCU_VP_0C__30C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 0&lt;T&lt;=30 C Minutes |
| STAT_INT_MCU_VP_0C__30C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 0&lt;T&lt;=30 C Seconds |
| STAT_INT_MCU_VP_30C__60C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 30&lt;T&lt;=60 C Hours |
| STAT_INT_MCU_VP_30C__60C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 30&lt;T&lt;=60 C Minutes |
| STAT_INT_MCU_VP_30C__60C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 30&lt;T&lt;=60 C Seconds |
| STAT_INT_MCU_VP_60C__80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 60&lt;T&lt;=80 C Hours |
| STAT_INT_MCU_VP_60C__80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 60&lt;T&lt;=80 C Minutes |
| STAT_INT_MCU_VP_60C__80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for 60&lt;T&lt;=80 C Seconds |
| STAT_INT_MCU_VP_80C_H_WERT | h | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&gt;80 C Hours |
| STAT_INT_MCU_VP_80C_M_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&gt;80 C Minutes |
| STAT_INT_MCU_VP_80C_S_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | internal temperature MCU+VP operating time for T&gt;80 C Seconds |

<a id="table-res-0x410b"></a>
### RES_0X410B

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VP_CAN_TRACE | - | - | - | 0-n | high | unsigned char | - | VP_CAN_TRACE | 1.0 | 1.0 | 0.0 | Trace OK-&gt;0; Trace overflow -&gt;1 |

<a id="table-res-0x41f1"></a>
### RES_0X41F1

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MCU_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | MCU uptime |
| STAT_VP_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | VP uptime |
| STAT_CAM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Camera uptime |
| STAT_VP_RESTARTS_WERT | count | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Number of VP restarts |
| STAT_CAM_RESTARTS_WERT | count | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Number of Camera restarts |
| STAT_ERROR_BI_TRANS_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Number of errors in boot info transmission |
| STAT_ERROR_AL_TRANS_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Number of errors in application loader transmission |
| STAT_TIMEOUT_DSB_RESET_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Number of timeouts for DSPB reset |
| STAT_ERROR_ID_TRANS_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Number of errors in initdata transmission |

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

<a id="table-tab-blende"></a>
### TAB_BLENDE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Blende öffnen |
| 0x01 | Blende schließen |
| 0x02 | Automatische Blendensteuerung |
| 0x03 | Flat Field Correction |

<a id="table-tab-init"></a>
### TAB_INIT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | Initialisierung in Ordnung |
| 0xFF | Initialisierung nicht in Ordnung |

<a id="table-tab-modus-personenerkennung"></a>
### TAB_MODUS_PERSONENERKENNUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | STOPP |
| 0x01 | AUS |
| 0x02 | EIN |
| 0x03 | AUTO |

<a id="table-tab-kalibrierung-nivi"></a>
### TAB_KALIBRIERUNG_NIVI

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ABBRUCH |
| 0x01 | REFERENZBILD |
| 0x02 | SPEICHERN |

<a id="table-tab-diebstahlschutz"></a>
### TAB_DIEBSTAHLSCHUTZ

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zuordnung in Ordnung |
| 0x01 | Kamera passt nicht zur ECU |
| 0x02 | ECU passt nicht zum Fahrzeug |
| 0x03 | Kamera passt nicht zur ECU und ECU nicht zum Fahrzeug. |
| 0x04 | Freischaltcode nicht vollständig geprüft oder Standard FSC-Prüfung fehlgeschlagen |
| 0xFF | Ungültiger Wert |

<a id="table-tab-nivi-pixeltest"></a>
### TAB_NIVI_PIXELTEST

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test abgebrochen oder nicht angefordert |
| 0x01 | Test läuft |
| 0x02 | Test erfolgreich abgeschlossen |
| 0x03 | Test fehlgeschlagen |

<a id="table-seite"></a>
### SEITE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 01 | Links |
| 02 | Rechts |

<a id="table-tab-linsenheizung"></a>
### TAB_LINSENHEIZUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0x02 | Defekt |
| 0xFF | undefinierter Status |

<a id="table-tab-richtung"></a>
### TAB_RICHTUNG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | OBEN |
| 0x02 | UNTEN |

<a id="table-tab-stat-nivi-cam"></a>
### TAB_STAT_NIVI_CAM

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kamera aus, Zuordnung OK, Temperatur OK |
| 0x01 | Kamera an, Zuordnung OK, Temperatur OK |
| 0x02 | Kamera aus, Zuordnung nicht OK, Temperatur OK |
| 0x03 | Kamera an, Zuordnung nicht OK, Temperatur OK |
| 0x04 | Kamera aus, Zuordnung OK, Temperatur zu hoch |
| 0x05 | Kamera an, Zuordnung OK, Temperatur zu hoch |
| 0x06 | Kamera aus, Zuordnung nicht OK, Temperatur zu hoch |
| 0x07 | Kamera an, Zuordnung nicht OK, Temperatur zu hoch |
| 0xFF | Ungültig |

<a id="table-pixeltest-modus"></a>
### PIXELTEST_MODUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 00 | Default Modus, Initialisierung mit automatisch gefundenen defekten Pixeln. |
| 01 | Werkseingestellte defekte Pixel Tabelle laden. |

<a id="table-tab-nivi-status"></a>
### TAB_NIVI_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | System ausgeschaltet (kein Bild) |
| 0x01 | Systeme eingeschaltet (Bild) |
| 0x02 | Testbild (STEUERN_SIGNALAUSGABE) |
| 0x03 | System AUS |
| 0xFF | undefinierter Zustand |

<a id="table-tab-mode-justagelinien"></a>
### TAB_MODE_JUSTAGELINIEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Mode 1: Im Bild zentriert |
| 0x02 | Mode 2: Mit Korrektur aus Onlinekalibrierung |
| 0x03 | Mode 3 |

<a id="table-vp-can-trace"></a>
### VP_CAN_TRACE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | TRACE_OK |
| 0x01 | TRACE_OVERFLOW |
| 0xFF | ungültiger Wert |

<a id="table-tab-modus-blende"></a>
### TAB_MODUS_BLENDE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Offen |
| 0x01 | Geschlossen |
| 0x02 | Automatische Steuerung |
| 0x03 | FFC ist in Bewegung (Blende geschlossen) |
| 0xFF | Undefinierter Modus |

<a id="table-vp-39391829841500"></a>
### VP__39391829841500

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OFF |
| 0x01 | DETP_79B |
| 0x02 | DATA_7BC |
| 0x03 | 01_DATA_7BC |
| 0x04 | CLASS_7BC |
| 0x05 | 01_CLASS_7BC |
| 0x08 | SHUTTER_7BC |
| 0x10 | LVDS_7BC |
| 0x20 | HEATER_7BC |
| 0x40 | X_CAN_7BC |
| 0x80 | DEBUG_79B_7BC |
| 0xFF | ungültige Daten |

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

<a id="table-tab-personenerkennung"></a>
### TAB_PERSONENERKENNUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Personenerkennung nicht aktiv |
| 0x01 | Personenerkennung aktiv |
| 0x02 | nicht verwendet |
| 0x03 | Detektion AUTOMATISCH |
| 0xFF | unbekannter Zustand |

<a id="table-tab-arg-linsenheizung"></a>
### TAB_ARG_LINSENHEIZUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0x02 | Automatische Heizungssteuerung |
