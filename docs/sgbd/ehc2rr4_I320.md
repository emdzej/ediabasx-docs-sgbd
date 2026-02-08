# ehc2rr4_I320.prg

- Jobs: [35](#jobs)
- Tables: [49](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | 2-Achs-Luftfeder_RollsRoyce_RR4 |
| ORIGIN | BMW EF631 Thasler |
| REVISION | 0.022 |
| AUTHOR | WABCO CAR-PD CarstenPetry, SCL SW-DesignCentre NatarajanRamesh |
| COMMENT | N/A |
| PACKAGE | 0.27 |
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
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default
- [HERSTELLINFO_LESEN](#job-herstellinfo-lesen) - Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
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
| PROZESSKLASSE_WERT | int | table Prozessklasse WERT dezimale Angabe der Prozessklasse |
| PROZESSKLASSE_TEXT | string | table Prozessklasse BEZEICHNUNG Text-Angabe der Prozessklasse |
| SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| VERSION | string | Angabe der Version der Prozessklasse |
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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (64 × 2)
- [LIEFERANTEN](#table-lieferanten) (100 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (20 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (4 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (88 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (5 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [IORTTEXTE](#table-iorttexte) (18 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (3 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (5 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (60 × 16)
- [ARG_0X40A7](#table-arg-0x40a7) (1 × 12)
- [ARG_0X40EE](#table-arg-0x40ee) (2 × 12)
- [RES_0X40A8](#table-res-0x40a8) (7 × 10)
- [ARG_0X4091](#table-arg-0x4091) (12 × 14)
- [RES_0XDB7C](#table-res-0xdb7c) (3 × 10)
- [RES_0XDB69](#table-res-0xdb69) (7 × 10)
- [ARG_0XDB6A](#table-arg-0xdb6a) (2 × 12)
- [RES_0XDB7D](#table-res-0xdb7d) (8 × 10)
- [RES_0XDB8A](#table-res-0xdb8a) (35 × 10)
- [ARG_0XDB8C](#table-arg-0xdb8c) (3 × 12)
- [RES_0XDB7F](#table-res-0xdb7f) (12 × 10)
- [ARG_0XDB7B](#table-arg-0xdb7b) (1 × 12)
- [ARG_0XDB6E](#table-arg-0xdb6e) (2 × 12)
- [RES_0XDB7E](#table-res-0xdb7e) (3 × 10)
- [RES_0XDB68](#table-res-0xdb68) (11 × 10)
- [RES_0XAB63](#table-res-0xab63) (8 × 13)
- [RES_0XAB64](#table-res-0xab64) (8 × 13)
- [ARG_0XAB64](#table-arg-0xab64) (3 × 14)
- [RES_0XDC0D](#table-res-0xdc0d) (18 × 10)
- [ARG_0XDC0F](#table-arg-0xdc0f) (1 × 12)
- [ARG_0XDC10](#table-arg-0xdc10) (3 × 12)
- [ARG_0XDC11](#table-arg-0xdc11) (1 × 12)
- [RES_0XDC33](#table-res-0xdc33) (4 × 10)
- [RES_0XDC32](#table-res-0xdc32) (4 × 13)
- [ARG_0XAB65](#table-arg-0xab65) (1 × 14)
- [ARG_0XF18C](#table-arg-0xf18c) (6 × 12)
- [ARG_0XF191](#table-arg-0xf191) (6 × 12)
- [ARG_0XF192](#table-arg-0xf192) (5 × 12)
- [ARG_0XF193](#table-arg-0xf193) (1 × 12)

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

Dimensions: 100 rows × 2 columns

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

Dimensions: 20 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
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

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFF | - | 1 | 1 | 0.000000 |
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

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler gespeichert |
| 0x44 | Fehler momentan vorhanden und bereits gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler momentan vorhanden und bereits gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler momentan vorhanden und bereits gespeichert |
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

| WERT | TEXT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | kein Betreibsmode gesetzt | kein Betreibsmode |
| 0xFF | ungültiger Betreibsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 88 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x023800 | Energiesparmode aktiv | 1 |
| 0x480D80 | Sensor hinten links, Sensorspannung oder Sensorversorgung außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach Ubat oder Leitungsbruch) | 0 |
| 0x480D82 | aktueller Sensorwert hinten links hat zu große Abweichung zum vorhergehenden Wert | 0 |
| 0x480D83 | Sensor hinten rechts, Sensorspannung oder Sensorversorgung außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach Ubat oder Leitungsbruch) | 0 |
| 0x480D85 | aktueller Sensorwert hinten rechts hat zu große Abweichung zum vorhergehenden Wert | 0 |
| 0x480D86 | Sensor vorne links, Sensorspannung oder Sensorversorgung außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach Ubat oder Leitungsbruch) | 0 |
| 0x480D88 | aktueller Sensorwert vorn links hat zu große Abweichung zum vorhergehenden Wert | 0 |
| 0x480D89 | Sensor vorne rechts, Sensorspannung oder Sensorversorgung außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach Ubat oder Leitungsbruch) | 0 |
| 0x480D8B | aktueller Sensorwert vorn rechts hat zu große Abweichung zum vorhergehenden Wert | 0 |
| 0x480D8C | Sensorspannungsversorgung hinten links außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach U-Bat) | 0 |
| 0x480D8D | Sensorspannungsversorgung hinten rechts außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach U-Bat) | 0 |
| 0x480D8E | Sensorspannungsversorgung vorne links außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach U-Bat) | 0 |
| 0x480D8F | Sensorspannungsversorgung vorne rechts außerhalb Betriebsbereich (Kurzschluss nach Masse oder nach U-Bat) | 0 |
| 0x480D90 | Druckspeichersensor, Spannung größer als Betriebsbereich (Kurzschluss gegen U-Bat) | 0 |
| 0x480D91 | Druckspeichersensor, Spannungsversorgung größer Fehlergrenzwert | 0 |
| 0x480D92 | Druckspeichersensor, Spannungsversorgung kleiner Fehlergrenzwert | 0 |
| 0x480D94 | Temperatursensor, Spannung größer als Betriebsbereich (Kurzschluss gegen U-Bat) | 0 |
| 0x480D95 | Temperatursensor, Spannung kleiner als Betriebsbereich (Kurzschluss gegen Masse oder Leitungsbruch) | 0 |
| 0x480DA0 | LED Tiefniveau, Spannungsversorgung größer als Betriebsbereich (Kurzschluss gegen U-Bat oder Leitungsbruch) | 0 |
| 0x480DA1 | LED Tiefniveau, Spannung kleiner als Betriebsbereich (Kurzschluss gegen Masse) | 0 |
| 0x480DA2 | LED Hochniveau, Spannungsversorgung größer als Betriebsbereich (Kurzschluss gegen U-Bat oder Leitungsbruch) | 0 |
| 0x480DA3 | LED Hochniveau, Spannung kleiner als Betriebsbereich (Kurzschluss gegen Masse) | 0 |
| 0x480DA4 | LED Standardniveau, Spannungsversorgung größer als Betriebsbereich (Kurzschluss gegen U-Bat oder Leitungsbruch) | 0 |
| 0x480DA5 | LED Standardniveau, Spannung kleiner als Betriebsbereich (Kurzschluss gegen Masse) | 0 |
| 0x480DA6 | Temperatursensor, Plausibilitätscheck COMP aktiv | 0 |
| 0x480DA7 | Temperatursensor, Plausibilitätscheck COMP inaktiv | 0 |
| 0x480DB0 | Magnetventil hinten links oder hinten rechts, Kurzschluss nach Ubat | 0 |
| 0x480DB1 | Magnetventil hinten links oder hinten rechts, Kurzschluss nach Masse | 0 |
| 0x480DB2 | Magnetventil zur Steuerung der Luftfeder hinten links, Leitungsunterbrechung | 0 |
| 0x480DB3 | Magnetventil zur Steuerung der Luftfeder hinten rechts, Leitungsunterbrechung | 0 |
| 0x480DB4 | Magnetventil vorne links oder vorne rechts, Kurzschluss nach U-Bat | 0 |
| 0x480DB5 | Magnetventil vorne links oder vorne rechts, Kurzschluss nach Masse | 0 |
| 0x480DB6 | Magnetventil zur Steuerung der Luftfeder vorne links, Leitungsunterbrechung | 0 |
| 0x480DB7 | Magnetventil zur Steuerung der Luftfeder vorne rechts, Leitungsunterbrechung | 0 |
| 0x480DB8 | Ablassventil oder Druckspeicherventil, Kurzschluss nach U-Bat | 0 |
| 0x480DB9 | Ablassventil oder Druckspeicherventil, Kurzschluss nach Masse | 0 |
| 0x480DBA | Ablassventil, Leitungsunterbrechung | 0 |
| 0x480DBC | Druckspeicherventil, Leitungsunterbrechung | 0 |
| 0x480DBD | Kompressorrelais, Kurzschluss nach U-Bat oder Leitungsbruch | 0 |
| 0x480DBE | Kompressorrelais, Kurzschluss nach Masse | 0 |
| 0x480DD0 | Sensoraktivitätsüberwachung hinten links (Korrlation des Schwingungsverhaltens) | 0 |
| 0x480DD1 | Sensoraktivitätsüberwachung hinten rechts (Korrlation des Schwingungsverhaltens) | 0 |
| 0x480DD2 | Sensoraktivitätsüberwachung vorn links (Korrlation des Schwingungsverhaltens) | 0 |
| 0x480DD3 | Sensoraktivitätsüberwachung vorn rechts (Korrlation des Schwingungsverhaltens) | 0 |
| 0x480DD4 | Höhenstandsänderung, falsche Richtung wenn Heben angefordert | 0 |
| 0x480DD5 | Höhenstandsänderung, falsche Richtung wenn Senken angefordert | 0 |
| 0x480DD6 | Zu viel Energie zur Regelung benötigt, Vorderachse | 0 |
| 0x480DD7 | Zu viel Energie zur Regelung benötigt, Hinterachse rechts | 0 |
| 0x480DD8 | Zu viel Energie zur Regelung benötigt, Hinterachse links | 0 |
| 0x480DD9 | Zu viel Energie um die Zielhöhe zu erreichen benötigt, vorn | 0 |
| 0x480DDA | Zu viel Energie um die Zielhöhe zu erreichen benötigt, hinten rechts | 0 |
| 0x480DDB | Zu viel Energie um die Zielhöhe zu erreichen benötigt, hinten links | 0 |
| 0x480DDC | Sensorgestänge der Wegsensoren beschädigt oder fehlerhafte Höhenstandskalibrierung | 0 |
| 0x480DDD | Speicherdruck steigt, wenn Speicher nicht aktiv ist | 0 |
| 0x480DDE | Speicherdruck sinkt, wenn Speicher nicht aktiv ist | 0 |
| 0x480DDF | Speicherdruck bleibt konstant, wenn Speicher füllen angefordert wird | 0 |
| 0x480DE0 | Speicherdruck sinkt, wenn Speicher füllen angefordert wird | 0 |
| 0x480DE1 | Speicherdruck sinkt anfänglich, wenn Speicher füllen angefordert wird | 0 |
| 0x480DE2 | Speicherdruck bleibt konstant, wenn aus dem Speicher nach oben verfahren wird | 0 |
| 0x480DE3 | Speicherdruck steigt, wenn aus dem Speicher nach oben verfahren wird | 0 |
| 0xD70414 | K-CAN Control Module Bus OFF | 0 |
| 0xD7040B | K-CAN Bus | 0 |
| 0x480E02 | Unterspannung | 1 |
| 0x480E03 | Steuergerät ist nicht codiert oder SG arbeitet mit Default-Codierdaten | 1 |
| 0x480E04 | Fehler während der Codierdaten-Transaktion aufgetreten | 1 |
| 0x480E05 | Signatur über Nettocodierdaten ungültig. Default-Codierdaten verwendet | 1 |
| 0x480E06 | Steuergerät ist nicht für das Fahrzeug codiert, in dem es verbaut ist. Vergleich zwischen CPS und VIN negativ | 1 |
| 0x480E07 | Die während einer Codierdatentransaktion gesendeten Daten sind nicht plausibel | 1 |
| 0x480E08 | Höhenstandsabgleich fehlt oder fehlerhaft (BMW) | 1 |
| 0x480E10 | ECU-interner Fehler, Details im sekundären FS | 0 |
| 0x480E12 | Überspannung | 1 |
| 0x02FF38 | DM_TEST_APPL | 1 |
| 0xD70BFF | DM_TEST_COM | 1 |
| 0xD70DA0 | Timeout , Bus Botschaft  ZV und Klappenzustand  | 1 |
| 0xD70DA1 | Ungültiges Signal, Bus-Botschaft  ZV und Klappenzustand  | 1 |
| 0xD70DA2 | Timeout, Bus-Botschaft  Geschwindigkeit Fahrzeug  | 1 |
| 0xD70DA3 | Ungültiges Signal, Bus-Botschaft  Geschwindigkeit Fahrzeug  | 1 |
| 0xD70DA4 | Timeout, Bus-Botschaft  Klemmen  | 1 |
| 0xD70DA5 | Ungültiges Signal, Bus-Botschaft  Klemmen  | 1 |
| 0xD70DA6 | Timeout, Bus-Botschaft  Status Reifen  | 1 |
| 0xD70DA7 | Ungültiges Signal, Bus-Botschaft  Status Reifen  | 1 |
| 0xD70DA8 | Timeout, Bus-Botschaft  Querbeschleunigung Schwerpunkt  | 1 |
| 0xD70DA9 | Ungültiges Signal, Bus-Botschaft  Querbeschleunigung Schwerpunkt  | 1 |
| 0xD70DAA | Timeout Bus-Botschaft  Drehmoment Kurbelwelle 1  | 1 |
| 0xD70DAB | ungültiges Signal, Bus-Botschaft  Drehmoment Kurbelwelle 1  | 1 |
| 0xD70DAC | Timeout, Bus-Botschaft  Status Stabilisierung DSC   | 1 |
| 0xD70DAD | ungültiges Signal, Bus-Botschaft   Status Stabilisierung DSC    | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x5000 | ValveStatus-Bitmaske(bit7-&gt;bit0)[Reserviert\|Komp\|Ex\|Res\|HL\|HR\|VL\|VR] | - | - | unsigned char | - | - | - | - |
| 0x5001 | Speicherdruck | bar | - | unsigned char | - | - | - | - |
| 0x5002 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 2 | - | - |
| 0x5003 | Batteriespannung | V | - | unsigned char | - | - | 8 | - |
| 0x5004 | durchschn. Fahrzeughoehe | mm | - | signed char | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 18 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x380E00 | Onboard adapter Kalibierung fehlerhaft (WABCO) | 0 |
| 0x380E01 | Kommunikation PIC - Hauptrechner gestört | 0 |
| 0x380E02 | HSS-Abschaltung über PIC ist erfolgt | 0 |
| 0x380E03 | Steuergerät interner Fehler, Checksummenfehler Flash | 0 |
| 0x380E04 | Steuergerät interner Fehler, Checksummenfehler RAM | 0 |
| 0x384001 | NVM writing operation is failed for a given block. | 0 |
| 0x384002 | NVM reading operation is failed for a given block. | 0 |
| 0x384003 | NVM failed to check the consistency for the given block or restoring of default data for the given block | 0 |
| 0x384004 | NVM erase operation is failed for a given block. | 0 |
| 0x384005 | NVM writing operation is failed for a given block. | 0 |
| 0x384006 | Wrong configuration ID is given for NVM | 0 |
| 0x384007 | NVM reading operation is failed for a request to read all the blocks | 0 |
| 0x38D700 | DM_EVENT_Zeitbotschaft_Timeout | 0 |
| 0x38D701 | DM_Queue_DELETED | 1 |
| 0x38D702 | DM_Queue_FULL | 1 |
| 0x38D703 | Timeout, Bus Botschaft Fahrzeugzustand | 0 |
| 0x38D704 | Radentlastungsfunktion aktiv | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x5000 | ValveStatus-Bitmaske(bit7-&gt;bit0)[Reserviert\|Komp\|Ex\|Res\|HL\|HR\|VL\|VR] | - | - | unsigned char | - | - | - | - |
| 0x5001 | Speicherdruck | bar | - | unsigned char | - | - | - | - |
| 0x5002 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 2 | - | - |
| 0x5003 | Batteriespannung | V | - | unsigned char | - | - | 8 | - |
| 0x5004 | durchschn. Fahrzeughoehe | mm | - | signed char | - | - | - | - |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 60 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STATUS_EHC_ECU | 0xDB7F | - | Status: Steuergerät | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB7F |
| STATUS_EHC_HEIGHT_SENSOR | 0xDB69 | - | Status: Höhenstandssensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB69 |
| STATUS_EHC_INTERNAL | 0xDB8A | - | Status: intern | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB8A |
| STATUS_EHC_LED_STAT | 0xDB7C | - | Status: LED | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB7C |
| STATUS_EHC_MAGNETVALVE | 0xDB7D | - | Status: Magnetventile | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB7D |
| STATUS_EHC_SWITCH | 0xDB7E | - | Status: Tasterwippe | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB7E |
| STATUS_EHC_VOLTAGE | 0xDB68 | - | Status:SpannungsWert. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB68 |
| STEUERN_EHC_ACTUATOR | 0xDB8C | - | Steuern: Aktuator | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDB8C | - |
| STEUERN_EHC_LEDS | 0xDB7B | - | Steuern: LEDs | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDB7B | - |
| STEUERN_EHC_VALVE_SW1_HSS | 0xDB6A | - | Steuern: Ventile | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDB6A | - |
| STEUERN_EHC_VALVE_SW1_LSS | 0xDB6E | - | Steuern: Ventile | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDB6E | - |
| STATUS_EHC_VALUE_CALIBRATION | 0xAB63 | - | Status:Calibration Value | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAB63 |
| STEUERN_EHC_HEIGHT_CALIBRATE | 0xAB64 | - | Steuern:Height Calibration | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAB64 | RES_0xAB64 |
| STATUS_EHC_REF_HISTORY | 0xDC0D | - | Status:REF History | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC0D |
| STATUS_EHC_REF | 0xDC0E | STAT_REF_WERT | Status:REF | - | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STEUERN_EHC_REF | 0xDC0F | - | Steuern:REF | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDC0F | - |
| STEUERN_EHC_MANUAL_LEVELING | 0xDC10 | - | Steuern:Manual Levelling | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDC10 | - |
| STEUERN_EHC_VEHICLE_HEIGHT | 0xDC11 | - | Steuern:Vehicle Height | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDC11 | - |
| STATUS_EHC_VALUE_LEAK | 0xDC33 | - | Status:Leakage Value | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC33 |
| STEUERN_EHC_VALUE_LEAK | 0xDC32 | - | Steuern:Leakage Value | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xDC32 |
| STEUERN_ECUMODE | 0xAB65 | - | Steuern:ECU Mode | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAB65 | - |
| STATUS_ACTUATOR_VALVE_RL | 0x4011 | STAT_ACTUATOR_VALVE_RL_ON | Status of the Actuator Rear Left | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_RR | 0x4012 | STAT_ACTUATOR_VALVE_RR_ON | Status of the Actuator Rear Right | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_EX | 0x4013 | STAT_ACTUATOR_VALVE_EX_ON | Status of the Actuator Exhaust | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_COMPRESSOR | 0x4014 | STAT_ACTUATOR_COMPRESSOR_ON | Status of the Compressor | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_RES | 0x4015 | STAT_ACTUATOR_VALVE_RES_ON | Status of the Actuator Reservoir | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_HPEX | 0x4016 | STAT_ACTUATOR_VALVE_HPEX_ON | Status of the Actuator High Pressure Exhaust | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_INHIBIT | 0x4017 | STAT_ACTUATOR_INHIBIT_ON | Status of inhibit pin | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_FL | 0x4018 | STAT_ACTUATOR_VALVE_FL_ON | Status of the Actuator Front Left | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_ACTUATOR_VALVE_FR | 0x4019 | STAT_ACTUATOR_VALVE_FR_ON | Status of the Actuator Front Right | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_VOLTAGE_HTSENSOR_FL | 0x4001 | STAT_VOLTAGE_HTSENSOR_FL_WERT | Analog Voltage Height sensor FL | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_HTSENSOR_FR | 0x4002 | STAT_VOLTAGE_HTSENSOR_FR_WERT | Analog Voltage Height sensor FR | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_HTSENSOR_RL | 0x4003 | STAT_VOLTAGE_HTSENSOR_RL_WERT | Analog Voltage Height sensor RL | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_TSENSOR_COMP | 0x4006 | STAT_VOLTAGE_TSENSOR_COMP_WERT | Analog Voltage Temp sensor Compressor | V | - | - | int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_U_KL30 | 0x4007 | STAT_VOLTAGE_U_KL30_WERT | Analog Voltage KL30 | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_USENS1 | 0x4008 | STAT_VOLTAGE_USENS1_WERT | Analog Voltage USENS1 RR | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_USENS2 | 0x4009 | STAT_VOLTAGE_USENS2_WERT | Analog Voltage USENS2 RL | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_USENS3 | 0x400A | STAT_VOLTAGE_USENS3_WERT | Analog Voltage USENS3 | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_VOLTAGE_PSENS_GALLERY | 0x400B | STAT_VOLTAGE_PSENS_GALLERY_WERT | Analog Voltage Pressure Sensor Gallery | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_HEIGHT_FL | 0x4050 | STAT_VALUE_HEIGHT_FL_WERT | Value of Height Front Left | mm | - | - | int | - | - | 8 | - | - | 22 | - | - |
| STATUS_HEIGHT_FR | 0x4051 | STAT_VALUE_HEIGHT_FR_WERT | Value of Height Front Right | mm | - | - | int | - | - | 8 | - | - | 22 | - | - |
| STATUS_HEIGHT_RL | 0x4052 | STAT_VALUE_HEIGHT_RL_WERT | Value of Height Rear Left | mm | - | - | int | - | - | 8 | - | - | 22 | - | - |
| STATUS_HEIGHT_RR | 0x4053 | STAT_VALUE_HEIGHT_RR_WERT | Value of Height Rear Right | mm | - | - | int | - | - | 8 | - | - | 22 | - | - |
| STATUS_P_RESERVOIR | 0x4054 | STAT_VALUE_P_RESERVOIR_WERT | Value of Pressure in the Reservoir | bar | - | - | int | - | - | 128 | - | - | 22 | - | - |
| STATUS_T_COMPRESSOR | 0x4055 | STAT_VALUE_T_COMPRESSOR_WERT | Value of Temperature in the Compressor | °C | - | - | int | - | - | 100 | - | - | 22 | - | - |
| STATUS_SENSORVALUE_U_KL30 | 0x4056 | STAT_SENSORVALUE_U_KL30_WERT | Value of U_KL30 | count | - | - | int | - | - | 100 | - | - | 22 | - | - |
| STATUS_P_GALLERY | 0x4057 | STAT_VALUE_P_GALLERY_WERT | Value of Pressure in the Gallery | bar | - | - | int | - | - | 128 | - | - | 22 | - | - |
| STATUS_PIC_VERSION | 0x4099 | STAT_PIC_VERSION_WERT | Reads the PIC Version | - | - | - | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_HIGH_SIDE_SWITCH | 0x4097 | STAT_HSS_WERT | Reads the status of High Side Switch | - | - | - | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_VOLTAGE_HTSENSOR_RR | 0x4004 | STAT_VOLTAGE_HTSENSOR_RR_WERT | Analog Voltage Height Sensor RR | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STEUERN_ENDOFLINE | 0x40EE | - | Writes EOL data into EEPROM | - | - | - | - | - | - | - | - | - | 2E | ARG_0x40EE | - |
| STEUERN_RELEASE_ACTUATORS | 0x40A7 | - | Releases Actuator | - | - | - | - | - | - | - | - | - | 2F | ARG_0x40A7 | - |
| STATUS_VOLTAGE_PSENSOR_RES | 0x4005 | STAT_VOLTAGE_PSENSOR_RES_WERT | Analog voltage Reservoir pressure sensor | V | - | - | unsigned int | - | - | 100 | - | - | 22 | - | - |
| STATUS_LOW_SIDE_SWITCH | 0x4098 | STAT_LSS_WERT | Low side switch status | - | - | - | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_INFO_PORT | 0x40A8 | - | Reads Port status | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x40A8 |
| STEUERN_ADC_CALIBRATE | 0x4091 | - | Calibrates ADC channels | - | - | - | - | - | - | - | - | - | 31 | ARG_0x4091 | - |
| STEUERN_ECUSN | 0xF18C | - | Writes ECU Serial No. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF18C | - |
| STEUERN_VMECUHN | 0xF191 | - | Writes Vehicle Manufacturer ECU Hardware Number | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF191 | - |
| STEUERN_SSECUHN | 0xF192 | - | Writes System Supplier ECU Hardware Number | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF192 | - |
| STEUERN_SSECUHWVN | 0xF193 | - | Writes System Supplier ECU Hardware Version Number | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF193 | - |

<a id="table-arg-0x40a7"></a>
### ARG_0X40A7

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LOCAL_ID_WERT | - | - | unsigned int | - | - | - | - | - | - | - |  Local ID : 0x11 MV-RL   0x12 MV-RR 0x13 MV-EX 0x14 COMP                             0x15 MV-RES 0x16 MV-HPEX 0x17 INHIBIT                              0x18 MV-FL                                                 0x19 MV-FR   |

<a id="table-arg-0x40ee"></a>
### ARG_0X40EE

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MODE_EOL_WERT | - | - | unsigned int | - | - | - | - | - | - | - | 0001- BootProgStatus  0002 - BootProgCounter auf 0  0004 - BootProgData  0008 - SvkHistoryMemory  0018 - SvkHistoryMemory + Aktuelle SVK in SvkSysSupp Eintrag abspeichern  001A - SvkHistoryMemory + Aktuelle SVK in SvkSysSupp Eintrag abspeichern +                                                                                               BootProgCounter auf 1 |
| LOCAL_ID_WERT | - | - | unsigned int | - | - | - | - | - | - | - | Local ID = 0x00EE |

<a id="table-res-0x40a8"></a>
### RES_0X40A8

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INFO_P1H_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P1H |
| STAT_INFO_P1L_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P1L |
| STAT_INFO_P2_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P2 |
| STAT_INFO_P8_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P8 |
| STAT_INFO_P7_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P7 |
| STAT_INFO_P4_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P4 |
| STAT_INFO_P3_WERT | - | - | unsigned int | - | - | - | - | - | Port Info P3 |

<a id="table-arg-0x4091"></a>
### ARG_0X4091

Dimensions: 12 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DIAG_CAL_U_FL_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Front Left |
| DIAG_CAL_U_FR_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Front Right |
| DIAG_CAL_U_RL_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Rear Left |
| DIAG_CAL_U_RR_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Rear Right |
| DIAG_CAL_U_RES_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Reservoir |
| DIAG_CAL_U_GAL_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Gallery |
| DIAG_CAL_U_KL30_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage KL30 |
| DIAG_CAL_U_INHIBIT_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Inhibit |
| DIAG_CAL_U_SENS1_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Sens1 |
| DIAG_CAL_U_SENS2_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Sens2 |
| DIAG_CAL_U_SENS3_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Sens3 |
| DIAG_CAL_U_COMP_WERT | + | - | V | - | unsigned int | - | - | 100 | - | - | - | - | Calibration Voltage Compressor |

<a id="table-res-0xdb7c"></a>
### RES_0XDB7C

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STANDARD_ON | 0/1 | - | char | - | - | - | - | - | Standard-Höhe: Strasse |
| STAT_OFFROAD_ON | 0/1 | - | char | - | - | - | - | - | Spezial-Höhe: Gelände |
| STAT_ACCESS_ON | 0/1 | - | char | - | - | - | - | - | Standard-Höhe: Strasse |

<a id="table-res-0xdb69"></a>
### RES_0XDB69

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HEIGHT_SENSOR_FRONT_LEFT_WERT | mm | - | int | - | - | - | 8 | - | Gibt den Wert des Höhenstandssensor vorne links in mm zurück. |
| STAT_HEIGHT_SENSOR_FRONT_RIGHT_WERT | mm | - | int | - | - | - | 8 | - | Gibt die Spannung des Höhenstandssensor vorne rechts in mm zurück. |
| STAT_HEIGHT_SENSOR_REAR_LEFT_WERT | mm | - | int | - | - | - | 8 | - | Gibt die Spannung des Höhenstandssensor hinten links in mm zurück. |
| STAT_HEIGHT_SENSOR_REAR_RIGHT_WERT | mm | - | int | - | - | - | 8 | - | Gibt die Spannung des Höhenstandssensor hinten rechts in mm zurück. |
| STAT_PRESSURE_RESERVOIRE_WERT | bar | - | int | - | - | - | 128 | - | Gibt den Speicherdruck in bar an |
| STAT_TEMPERATURE_COMPRESSOR_WERT | °C | - | int | - | - | - | 100 | - | Gibt die Temperatur des Kompressors in ° C an |
| STAT_PRESSURE_GALLERY_WERT | bar | - | int | - | - | - | 128 | - | Gallery Pressure in bar |

<a id="table-arg-0xdb6a"></a>
### ARG_0XDB6A

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VALVE_SW1_NR | - | - | unsigned char | - | - | - | - | - | - | - | Bit0: PWR_SENS1,  Bit1: PWR_SENS2,  Bit2: PWR_SENS3,  Bit3: Reserved;  Bit4: Reserved,  Bit5: Reserved,  Bit6: Reserved,  Bit7: Reserved; |
| VALVE_SW2_NR | - | - | unsigned char | - | - | - | - | - | - | - | Bit0: HSS_FRONT,  Bit1: HSS_REAR,  Bit2: HSS_RES,  Bit3: Reserved;  Bit4: Reserved,  Bit5: PWR_UPULL,  Bit6: Reserved,  Bit7: Reserved; |

<a id="table-res-0xdb7d"></a>
### RES_0XDB7D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAGNETVALVE_FRONT_LEFT_ON | 0/1 | - | int | - | - | - | - | - | Magnetventil vorn links: auf/ zu |
| STAT_MAGNETVALVE_FRONT_RIGHT_ON | 0/1 | - | int | - | - | - | - | - | Magnetventil vorn rechts: auf/ zu |
| STAT_MAGNETVALVE_REAR_LEFT_ON | 0/1 | - | int | - | - | - | - | - | Magnetventil hinten links: auf/ zu |
| STAT_MAGNETVALVE_REAR_RIGHT_ON | 0/1 | - | int | - | - | - | - | - | Magnetventil hinten rechts: auf/ zu |
| STAT_MAGNETVALVE_RESERVOIRE_ON | 0/1 | - | int | - | - | - | - | - | Magnetventil-Speicher: auf/ zu |
| STAT_MAGNETVALVE_EXHAUST_ON | 0/1 | - | int | - | - | - | - | - | Großes AuslassVentil |
| STAT_COMPRESSOR_SWITCH_ON | 0/1 | - | int | - | - | - | - | - | Kompressor-Schalter |
| STAT_MAGNETVALVE_HIGH_PRESSURE_EXHAUST_ON | 0/1 | - | int | - | - | - | - | - | AuslassVentil zum Abbau hoher Druckspitzen/ aktiv vor der Öffnung des großen AuslassVentils |

<a id="table-res-0xdb8a"></a>
### RES_0XDB8A

Dimensions: 35 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PREVENT_CURVE_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Kurve Aktiv |
| STAT_PREVENT_ACCEL_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Laengsbeschleunigung Aktiv |
| STAT_PREVENT_PLAUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Plausibilitaet Aktiv |
| STAT_PREVENT_CARLIFT_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Wagenheber Aktiv |
| STAT_PREVENT_DOOR_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Tuer Aktiv |
| STAT_PREVENT_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Verschraenkung Aktiv |
| STAT_PREVENT_VALVE_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Ventil ED Aktiv |
| STAT_PREVENT_BRAKES_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer Bremse Aktiv |
| STAT_PREVENT_USER_ON | 0/1 | - | unsigned char | - | - | - | - | - | Regelungsverhinderer unterbrochenes Absenken Aktiv |
| STAT_CAN_V_CAR_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Fahrzeuggeschwindigkeit |
| STAT_CAN_ABS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus DSC Aktivitaet |
| STAT_CAN_N_MOT_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Motordrehzahl |
| STAT_CAN_KM_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Kilometerstand |
| STAT_CAN_A_Q_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Querbeschleunigung |
| STAT_CAN_BAS_FBR_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Fahrerbremsung |
| STAT_CAN_S_ANH_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Anhaenger |
| STAT_CAN_S_TNS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Tag/Nachtumschaltung |
| STAT_CAN_S_HBR_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Handbremse |
| STAT_CAN_L_ASC_DEF_ON | 0/1 | - | unsigned char | - | - | - | - | - | Empfangsstatus Fehlerstatus DSC |
| STAT_GMMNGR_OPMODE_ON_WERT | - | - | unsigned char | - | - | - | - | - | Global Modemanager Opmode |
| STAT_REG_SLOW_ON | 0/1 | - | unsigned char | - | - | - | - | - | Slowfilter aktiv |
| STAT_REG_NORMTOL_ON | 0/1 | - | unsigned char | - | - | - | - | - | Normales Toleranzband aktiv |
| STAT_REG_EXTTOL_ON | 0/1 | - | unsigned char | - | - | - | - | - | Erweitertes Toleranzband aktiv |
| STAT_REG_LOWTOL_ON | 0/1 | - | unsigned char | - | - | - | - | - | Enges Toleranzband aktiv |
| STAT_REG_WUPTOL_ON | 0/1 | - | unsigned char | - | - | - | - | - | Wakeup Toleranzband aktiv |
| STAT_REG_KERB_ON | 0/1 | - | unsigned char | - | - | - | - | - | Randsteinerkennung aktiv |
| STAT_REG_OTEMP_FILL_ON | 0/1 | - | unsigned char | - | - | - | - | - | ÖlTemperatur zu hoch |
| STAT_REG_OTEMP_REG_ON | 0/1 | - | unsigned char | - | - | - | - | - | ÖlTemperatur regulär |
| STAT_UNDERVOLTAGE_ON | 0/1 | - | unsigned char | - | - | - | - | - | Unterspannung aktiv |
| STAT_OVERVOLTAGE_ON | 0/1 | - | unsigned char | - | - | - | - | - | Ueberspannung aktiv |
| STAT_XXXSTATEFR_ON_WERT | - | - | unsigned char | - | - | - | - | - | Zustand des Reglerblocks Vorderachse |
| STAT_XXXSTATERR_ON_WERT | - | - | unsigned char | - | - | - | - | - | Zustand des Reglerblocks hinten rechts |
| STAT_XXXSTATERL_ON_WERT | - | - | unsigned char | - | - | - | - | - | Zustand des Reglerblocks hinten links |
| STAT_VLVCTRL_STATE_ON_WERT | - | - | unsigned char | - | - | - | - | - | Zustand des ValveCtrl Blocks |
| STAT_ACTUATOR_BA_WARN_ON_WERT | - | - | unsigned int | - | - | - | - | - | actuator_ba_warn Variable |

<a id="table-arg-0xdb8c"></a>
### ARG_0XDB8C

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CONTROLOPTION_NR | - | - | int | - | - | - | - | - | - | - | 1=on 0=off |
| TIME_NR | - | - | int | - | - | - | - | - | 0 | 760 | Adj-time = 0-760  * 30ms |
| LOCAL_ID_NR | - | - | int | - | - | - | - | - | - | - |  Local ID : 0x11 MV-RL                                0x12 MV-RR 0x13 MV-EX 0x14 COMP                             0x15 MV-RES 0x16 MV-HPEX 0x17 INHIBIT                              0x18 MV-FL                                                0x19 MV-FR   |

<a id="table-res-0xdb7f"></a>
### RES_0XDB7F

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DUMP_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Speicherausdruck aktiv/ Zusatzbotschaften fuer FESTUS |
| STAT_BAND_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Aktivierungs-Sperre/ Modus1 |
| STAT_VERLADE_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Einstellungen fuer den Transport |
| STAT_LOWTOL_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Aktiviert sehr enge Toleranzen |
| STAT_EMV_KUNDEN_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | fuer webaco EMV-Tests |
| STAT_HANDSTEUER_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Freischaltung fuer I/O Status-Vorgabe |
| STAT_NOPLAU_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | fuer Laborauto Tests |
| STAT_NOUSER_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | SG reagiert nicht mehr auf Benutzeranforderungen/  Modus1 |
| STAT_ZYKEMV_MODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Modus um im EMV Test zyklische Ventilansteuerungen zu haben/ Modus2 |
| STAT_NOPREVENTMODUS_ON | 0/1 | - | unsigned char | - | - | - | - | - | Modus um Regelungsverhinderer zu deaktivieren |
| STAT_ECUMOD1_WERT | - | - | unsigned char | - | - | - | - | - |  Status Steuergeraet (Modus) Bit0:  CYCLIC EMC,  Bit1: Band_ECU,  Bit2: No Prevent,  Bit3: reserved; Bit4: reserved,  Bit5: reserved,  Bit6: reserved,  Bit7: reserved;  |
| STAT_ECUMOD2_WERT | - | - | unsigned char | - | - | - | - | - |  Status Steuergeraet (Modus) Bit0: Dump Modus,  Bit1: Band Modus,  Bit2: Verlademodus,  Bit3: Lowtolmodus; Bit4: EMV Kundenmodus,  Bit5: Handsteuermodus,  Bit6: Noplausmodus,  Bit7: Nousermodus  |

<a id="table-arg-0xdb7b"></a>
### ARG_0XDB7B

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LEDS_NR | - | - | int | - | - | - | - | - | - | - | Bit0: Access,     Bit1: Reserved;     Bit2: Standard;       Bit3: Off Road,      Bit4: Reserved,      Bit5: reserved,     Bit6: reserved,       Bit7: reserved, |

<a id="table-arg-0xdb6e"></a>
### ARG_0XDB6E

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VALVE_SW1_NR | - | - | unsigned char | - | - | - | - | - | - | - | Bit 0 - MV_HPEX   Bit1-Bit 7 - Reserved |
| VALVE_SW2_NR | - | - | unsigned char | - | - | - | - | - | - | - | Bit0: MV_FR,  Bit1: MV_FL,  Bit2: MV_RR,  Bit3: MV_RL;  Bit4: MV_RES,  Bit5: MV_EX,  Bit6: C_SW,  Bit7: reserved |

<a id="table-res-0xdb7e"></a>
### RES_0XDB7E

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SWITCH_UP_ON | 0/1 | - | char | - | - | - | - | - | Tasterwippe aufwärts: EIN |
| STAT_SWITCH_DOWN_ON | 0/1 | - | char | - | - | - | - | - | Tasterwippe runter: EIN |
| STAT_VA_ON | 0/1 | - | char | - | - | - | - | - | Signalunterdrückung: Tasterwippe |

<a id="table-res-0xdb68"></a>
### RES_0XDB68

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VOLTAGE_FRONT_LEFT_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Höhenstandssensor vorne links in [V] zurück. |
| STAT_VOLTAGE_FRONT_RIGHT_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Höhenstandssensor vorne rechts in [V] zurück. |
| STAT_VOLTAGE_REAR_LEFT_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Höhenstandssensor hinten links in [V] zurück. |
| STAT_VOLTAGE_REAR_RIGHT_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Höhenstandssensor hinten rechts in [V] zurück. |
| STAT_VOLTAGE_RESERVOIR_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Reservoires in [V] zurück. |
| STAT_VOLTAGE_COMPRESSOR_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Kompressors in [V] zurück. |
| STAT_SPANNUNG_KLEMME_30_WERT | V | - | int | - | - | - | 100 | - | Spannungswert am Steuergerät an Klemme 30 (auf eine Nachkommastelle genau) |
| STAT_VOLTAGE_SENS1_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Sensors 1in [V] zurück. |
| STAT_VOLTAGE_SENS2_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Sensors 2 in [V] zurück. |
| STAT_VOLTAGE_SENS3_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Sensors 3 in [V] zurück. |
| STAT_VOLTAGE_GALLERY_WERT | V | - | int | - | - | - | 100 | - | Gibt den SpannungsWert des Gallery in [V] zurück. |

<a id="table-res-0xab63"></a>
### RES_0XAB63

Dimensions: 8 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HCNT_FL_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Offset value Front left |
| STAT_HCNT_FR_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Offset value Front right |
| STAT_HCNT_RL_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Offset value Rear left |
| STAT_HCNT_RR_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Offset value Rear Right |
| STAT_FL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value  Front left |
| STAT_FR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Front Right |
| STAT_RL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Rear Left |
| STAT_RR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Rear Right |

<a id="table-res-0xab64"></a>
### RES_0XAB64

Dimensions: 8 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HCNT_FL_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Height Offset Value Front Left |
| STAT_HCNT_FR_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Height Offset value Front right |
| STAT_HCNT_RL_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Height Offset value Rear left |
| STAT_HCNT_RR_OFFSET_WERT | + | - | - | count | - | unsigned int | - | - | - | - | - | Height Offset value Rear Right |
| STAT_FL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value  Front left |
| STAT_FR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Front Right |
| STAT_RL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Rear Left |
| STAT_RR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak value Rear Right |

<a id="table-arg-0xab64"></a>
### ARG_0XAB64

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HEIGHT_LEFT_WERT | + | - | mm | - | int | - | - | 8 | - | - | - | - | Height Left |
| HEIGHT_RIGHT_WERT | + | - | mm | - | int | - | - | 8 | - | - | - | - | Height Right |
| AXLE_WERT | + | - | - | - | char | - | - | - | - | - | - | - | Axle to be Calibrated |

<a id="table-res-0xdc0d"></a>
### RES_0XDC0D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REF_STATUS1_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON1_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO1_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |
| STAT_REF_STATUS2_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON2_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO2_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |
| STAT_REF_STATUS3_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON3_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO3_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |
| STAT_REF_STATUS4_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON4_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO4_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |
| STAT_REF_STATUS5_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON5_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO5_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |
| STAT_REF_STATUS6_WERT | - | - | unsigned char | - | - | - | - | - | REF Status |
| STAT_REF_REASON6_WERT | - | - | unsigned char | - | - | - | - | - | REF Reason |
| STAT_MILEAGE_INFO6_WERT | - | - | data[3] | - | - | - | - | - | Mileage Information |

<a id="table-arg-0xdc0f"></a>
### ARG_0XDC0F

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CONTROLOPTION_WERT | - | - | unsigned char | - | - | - | - | - | - | - | Set REF Function 0  -  Deactivate  active REF 1  -  Activate REF by lifting RL and  lowering  RR(FlatTyre RR) 2  -  Activate REF by lifting RR  and  lowering  RL(FlatTyre RL) 3  -  Activate REF by lifting RR and  lowering  RL(FlatTyre FR) 4  -  Activate REF by lifting RL and  lowering  RR(FlatTyre FL) |

<a id="table-arg-0xdc10"></a>
### ARG_0XDC10

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LOCAL_ID_NR | - | - | unsigned int | - | - | - | - | - | 1 | 7 |  Local ID :  0x0001 -  Front Axle   0x0002 -  Rear Axle  0x0003 -  Front Axle Corner Front left alone  0x0004 -  Front Axle   Corner Front Right alone                         0x0005 -  Rear Axle Corner Rear left alone 0x0006 -  Rear Axle Corner Rear Right alone 0x0007 -  Reservoir |
| CONTROLOPTION_NR | - | - | unsigned char | - | - | - | - | - | 0 | 2 | ControlOption: 0x00 -  Stop 0x01 -  Lift / Fill 0x02 -  Lower/ Empty |
| TIME_NR | - | - | unsigned char | - | - | - | - | - | 0 | 25 | Minimum 0 Second to Maximum of 25 seconds. |

<a id="table-arg-0xdc11"></a>
### ARG_0XDC11

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NIVEAU_WERT | - | - | unsigned int | - | - | - | - | - | - | - |  ACCESS              0x0002  STANDARD         0x0008  OFFROAD           0x0010  |

<a id="table-res-0xdc33"></a>
### RES_0XDC33

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FL_LEAK_WERT | mm | - | int | - | - | - | 8 | - | Leak Value Front Left |
| STAT_FR_LEAK_WERT | mm | - | int | - | - | - | 8 | - | Leak Value Front Right |
| STAT_RL_LEAK_WERT | mm | - | int | - | - | - | 8 | - | Leak Value Rear Left |
| STAT_RR_LEAK_WERT | mm | - | int | - | - | - | 8 | - | Leak Value Rear Right |

<a id="table-res-0xdc32"></a>
### RES_0XDC32

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak Value Front Left |
| STAT_FR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak Value Front Right |
| STAT_RL_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak Value Rear Left |
| STAT_RR_LEAK_WERT | + | - | - | mm | - | int | - | - | - | 8 | - | Leak Value Rear Right |

<a id="table-arg-0xab65"></a>
### ARG_0XAB65

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ECUMODE_WERT | + | + | - | - | unsigned char | - | - | - | - | - | 0 | 12 | 0x00 - Reset all modes 0x01 - Dump Mode 0x02 - Line Mode 0x03 - Transport Mode 0x04 - Low Tolerance Mode 0x05 - EMC Mode 0x06 - Hand Mode 0x07 - NoPlaus Mode 0x08 - NoUser Mode 0x09 - Cyclic EMC Mode 0x0A - Band ECU Mode 0x0B - NoPrevent Mode 0x0C - WABCO HW Mode |

<a id="table-arg-0xf18c"></a>
### ARG_0XF18C

Dimensions: 6 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TYPENO_BYTE1_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 |  |
| TYPENO_BYTE2_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 |  |
| RESERVED_WERT | - | - | unsigned char | - | - | - | - | - | 255 | 255 |  |
| SERIALNO_BYTE1_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 |  |
| SERIALNO_BYTE2_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 |  |
| SERIALNO_BYTE3_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 |  |

<a id="table-arg-0xf191"></a>
### ARG_0XF191

Dimensions: 6 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BYTE1_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |
| BYTE2_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |
| BYTE3_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |
| BYTE4_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |
| BYTE5_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |
| BYTE6_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | Vehicle Manufacturer ECU Hardware No. |

<a id="table-arg-0xf192"></a>
### ARG_0XF192

Dimensions: 5 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BYTE1_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware No. |
| BYTE2_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware No. |
| BYTE3_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware No. |
| BYTE4_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware No. |
| BYTE5_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware No. |

<a id="table-arg-0xf193"></a>
### ARG_0XF193

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BYTE1_WERT | - | - | unsigned char | - | - | - | - | - | 0 | 255 | System Supplier ECU Hardware Version No. |
