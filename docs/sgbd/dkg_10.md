# dkg_10.prg

- Jobs: [37](#jobs)
- Tables: [105](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Doppelkupplungsgetriebe |
| ORIGIN | Martin BMW Kisch |
| REVISION | 2.003 |
| AUTHOR | GETRAG LES4 Ladner |
| COMMENT | DKG [28] |
| PACKAGE | 1.982 |
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
- [HERSTELLINFO_LESEN](#job-herstellinfo-lesen) - Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CALID_CVN_LESEN](#job-calid-cvn-lesen) - OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number
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

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_KLASSE | string | 'IGNORIERE_EREIGNIS_DTC': Wenn EREIGNIS_DTC = '1', DTC-Fehlereinträge werden ignoriert sonst: FEHLERKLASSE wird ausgewertet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC -1: wird nicht unterstuetzt table FOrtTexte EREIGNIS_DTC |
| F_FEHLERKLASSE | unsigned long | table FOrtTexte FEHLERKLASSE |
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
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
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
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
| F_UW_BN | int | Umweltbedingung Basisnetz (1 Byte) -1, wenn Daten bzgl. Basisnetz nicht zur Verfuegung stehen |
| F_UW_TN | long | Umweltbedingung Teilnetz (3 Byte) -1, wenn Daten bzgl. funktionalem Teilnetz nicht zur Verfuegung stehen |
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
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
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
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
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
| F_UW_BN | int | Umweltbedingung Basisnetz (1 Byte) -1, wenn Daten bzgl. Basisnetz nicht zur Verfuegung stehen |
| F_UW_TN | long | Umweltbedingung Teilnetz (3 Byte) -1, wenn Daten bzgl. funktionalem Teilnetz nicht zur Verfuegung stehen |
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

<a id="job-calid-cvn-lesen"></a>
### CALID_CVN_LESEN

OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_CALID_CVN | int | Anzahl der CAL-ID CVN Paare |
| CALID | string | Calibration ID |
| CVN | string | Calibration verification number |
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
| CPS | string | Codierpruefstempel bis SP2021 bestehend aus VIN7        7 Zeichen (ASCII) Codierpruefstempel ab SP2021 bestehend aus Codierdatum 6 Zeichen (3 Byte Hex) bestehend aus TesterNr    6 Zeichen (3 Byte Hex) bestehend aus LizenzID   10 Zeichen (5 Byte Hex) bestehend aus VIN7        7 Zeichen (ASCII) |
| CPS_VIN7 | string | 7 Zeichen (ASCII) |
| CPS_DATUM | string | erst ab SP2021 Codierdatum 8 Zeichen TT.MM.JJJJ |
| CPS_TESTERNR | string | erst ab SP2021 Tester-Nummer 6 Zeichen hex |
| CPS_LIZENZID | string | erst ab SP2021 Tester-Lizenz-ID 10 Zeichen hex |
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

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (149 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (13 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ACT_GET_ERGEBNIS_ABBRUCH](#table-act-get-ergebnis-abbruch) (20 × 2)
- [ACT_GET_ZUST_ADAP_MAIN_ABBRUCH](#table-act-get-zust-adap-main-abbruch) (5 × 2)
- [ACT_GET_ZUST_ADAP_SUB_ABBRUCH](#table-act-get-zust-adap-sub-abbruch) (8 × 2)
- [ARG_0X4100_D](#table-arg-0x4100-d) (1 × 12)
- [ARG_0X42A4_D](#table-arg-0x42a4-d) (16 × 12)
- [ARG_0X42A5_D](#table-arg-0x42a5-d) (16 × 12)
- [ARG_0X42A6_D](#table-arg-0x42a6-d) (16 × 12)
- [ARG_0X42A7_D](#table-arg-0x42a7-d) (1 × 12)
- [ARG_0X42AB_D](#table-arg-0x42ab-d) (10 × 12)
- [ARG_0X42AC_D](#table-arg-0x42ac-d) (1 × 12)
- [ARG_0X42AD_D](#table-arg-0x42ad-d) (1 × 12)
- [ARG_0X42AE_D](#table-arg-0x42ae-d) (1 × 12)
- [ARG_0X42AF_D](#table-arg-0x42af-d) (1 × 12)
- [ARG_0X4600_D](#table-arg-0x4600-d) (2 × 12)
- [ARG_0XAE30_R](#table-arg-0xae30-r) (2 × 14)
- [ARG_0XDE34_D](#table-arg-0xde34-d) (2 × 12)
- [ARG_0XDE36_D](#table-arg-0xde36-d) (1 × 12)
- [ARG_0XF770_R](#table-arg-0xf770-r) (1 × 14)
- [ARG_0XF771_R](#table-arg-0xf771-r) (2 × 14)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [CLA_CLU_STATE](#table-cla-clu-state) (9 × 2)
- [CLU_STATE_DETAILS](#table-clu-state-details) (24 × 2)
- [DMA_CAN_NOTL_SOURCE](#table-dma-can-notl-source) (3 × 2)
- [DMA_Z_POS](#table-dma-z-pos) (5 × 2)
- [DM_TAB_ROE_ACTIVATED_DOP](#table-dm-tab-roe-activated-dop) (2 × 2)
- [DPL_ERROR](#table-dpl-error) (9 × 2)
- [DPL_ERROR_PSM](#table-dpl-error-psm) (7 × 2)
- [DPL_FA_ST](#table-dpl-fa-st) (6 × 2)
- [E2_DBG_NOCLEAR](#table-e2-dbg-noclear) (8 × 2)
- [E2_OUTPUT_NOCLEAR](#table-e2-output-noclear) (26 × 2)
- [E2_SDS_GWS_NOCLEAR](#table-e2-sds-gws-noclear) (6 × 2)
- [ENERGIESPARMODE_DOP](#table-energiesparmode-dop) (4 × 2)
- [EWS_DIAG_0](#table-ews-diag-0) (8 × 3)
- [EWS_DIAG_1](#table-ews-diag-1) (4 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FEHLERKLASSE_DOP](#table-fehlerklasse-dop) (4 × 2)
- [FORTTEXTE](#table-forttexte) (191 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (157 × 9)
- [GBX_ERR](#table-gbx-err) (10 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (31 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (64 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [LBC_COOL_MODE_DES](#table-lbc-cool-mode-des) (6 × 2)
- [NVM_BLOCK_D2_STATUS](#table-nvm-block-d2-status) (2 × 2)
- [NVM_BLOCK_STATUS](#table-nvm-block-status) (3 × 2)
- [PLM_PL_STATE](#table-plm-pl-state) (10 × 2)
- [PROG_DEP_DOP](#table-prog-dep-dop) (6 × 2)
- [QI_HSD](#table-qi-hsd) (2 × 2)
- [QTEMP_TCU](#table-qtemp-tcu) (3 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [RDTCI_LEV_DOP](#table-rdtci-lev-dop) (9 × 2)
- [RES_0X1061_R](#table-res-0x1061-r) (1 × 13)
- [RES_0X4600_D](#table-res-0x4600-d) (2 × 10)
- [RES_0XAE30_R](#table-res-0xae30-r) (7 × 13)
- [RES_0XDE30_D](#table-res-0xde30-d) (79 × 10)
- [RES_0XDE31_D](#table-res-0xde31-d) (20 × 10)
- [RES_0XDE32_D](#table-res-0xde32-d) (3 × 10)
- [RES_0XDE33_D](#table-res-0xde33-d) (82 × 10)
- [RES_0XDE34_D](#table-res-0xde34-d) (3 × 10)
- [RES_0XDE40_D](#table-res-0xde40-d) (6 × 10)
- [RES_0XDE41_D](#table-res-0xde41-d) (6 × 10)
- [RES_0XDE42_D](#table-res-0xde42-d) (8 × 10)
- [RES_0XDE43_D](#table-res-0xde43-d) (8 × 10)
- [RES_0XDE44_D](#table-res-0xde44-d) (10 × 10)
- [RES_0XDE49_D](#table-res-0xde49-d) (2 × 10)
- [RES_0XDE4A_D](#table-res-0xde4a-d) (3 × 10)
- [RES_0XDE4C_D](#table-res-0xde4c-d) (7 × 10)
- [RES_0XDE50_D](#table-res-0xde50-d) (62 × 10)
- [RES_0XDE51_D](#table-res-0xde51-d) (41 × 10)
- [RES_0XDE52_D](#table-res-0xde52-d) (16 × 10)
- [RES_0XDE53_D](#table-res-0xde53-d) (16 × 10)
- [RES_0XDE54_D](#table-res-0xde54-d) (16 × 10)
- [RES_0XDE5A_D](#table-res-0xde5a-d) (20 × 10)
- [RES_0XF770_R](#table-res-0xf770-r) (1 × 13)
- [RES_0XF771_R](#table-res-0xf771-r) (1 × 13)
- [SCM_ERR_FLG_HI](#table-scm-err-flg-hi) (3 × 2)
- [SCM_ERR_FLG_LO](#table-scm-err-flg-lo) (17 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (46 × 16)
- [SIGNAL_STATUS](#table-signal-status) (3 × 2)
- [SVK_VERSION_DOP](#table-svk-version-dop) (2 × 2)
- [TAB_DKG_GANGSTATUS](#table-tab-dkg-gangstatus) (10 × 2)
- [TAB_DKG_GETRIEBESTATUS](#table-tab-dkg-getriebestatus) (23 × 2)
- [TAB_DKG_IO_SETZEN](#table-tab-dkg-io-setzen) (20 × 2)
- [TAB_DKG_KUPPLUNGSSTATUS](#table-tab-dkg-kupplungsstatus) (10 × 2)
- [TAB_DKG_OBDSTEUERFUNKTION](#table-tab-dkg-obdsteuerfunktion) (16 × 2)
- [TAB_DKG_RUECKGABESTATUS](#table-tab-dkg-rueckgabestatus) (4 × 2)
- [TAB_DKG_SCHALTSTANGENPOSITION](#table-tab-dkg-schaltstangenposition) (11 × 2)
- [TAB_DKG_STATUS_TEST_EINLERN](#table-tab-dkg-status-test-einlern) (6 × 2)
- [TAB_DKG_TEST_UND_EINLERNEN_PRG](#table-tab-dkg-test-und-einlernen-prg) (14 × 2)
- [VBI_ERR_RCPT_ENG_EGS](#table-vbi-err-rcpt-eng-egs) (2 × 2)
- [VBI_TRAI](#table-vbi-trai) (2 × 2)

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

Dimensions: 149 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen / Delphi |
| 0x000002 | Leopold Kostal GmbH & Co. KG |
| 0x000003 | Hella Fahrzeugkomponenten GmbH |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako GmbH |
| 0x000008 | Robert Bosch GmbH |
| 0x000009 | Lear Corporation |
| 0x000010 | VDO |
| 0x000011 | Valeo GmbH |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine Electronics GmbH |
| 0x000018 | Continental Teves AG & Co. OHG |
| 0x000019 | Elektromatik Südafrika |
| 0x000020 | Harman Becker Automotive Systems |
| 0x000021 | Preh GmbH |
| 0x000022 | Alps Electric Co. Ltd. |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto SE |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi Automotive PLC |
| 0x000028 | DODUCO (Beru) |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer Corporation |
| 0x000033 | Jatco |
| 0x000034 | FUBA Automotive GmbH & Co. KG |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE (Fahrzeugtechnik Ebern) |
| 0x000041 | Megamos |
| 0x000042 | TRW Automotive GmbH |
| 0x000043 | WABCO Fahrzeugsysteme GmbH |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC Hella Electronics Corporation |
| 0x000046 | Gemel |
| 0x000047 | ZF Friedrichshafen AG |
| 0x000048 | GMPT |
| 0x000049 | Harman Becker Automotive Systems GmbH |
| 0x000050 | Remes GmbH |
| 0x000051 | ZF Lenksysteme GmbH |
| 0x000052 | Magneti Marelli S.p.A. |
| 0x000053 | Johnson Controls Inc. |
| 0x000054 | GETRAG Getriebe- und Zahnradf. Hermann Hagenmeyer GmbH & Co. KG |
| 0x000055 | Behr-Hella Thermocontrol GmbH |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon Innovation & Technology GmbH |
| 0x000058 | Autoliv AB |
| 0x000059 | Haberl Electronic GmbH & Co. KG |
| 0x000060 | Magna International Inc. |
| 0x000061 | Marquardt GmbH |
| 0x000062 | AB Elektronik GmbH |
| 0x000063 | SDVO/BORG |
| 0x000064 | Hirschmann Car Communication GmbH |
| 0x000065 | hoerbiger-electronics |
| 0x000066 | Thyssen Krupp Automotive |
| 0x000067 | Gentex Corporation |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steeting Europe |
| 0x000071 | NSI Beheer B.V. |
| 0x000072 | Aisin AW Co. Ltd. |
| 0x000073 | Schorlock |
| 0x000074 | Schrader Electronics Ltd. |
| 0x000075 | Huf-Electronics Bretten GmbH |
| 0x000076 | CEL |
| 0x000077 | AUDIO MOBIL Elektronik GmbH |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia-Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A. |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | Sonceboz S.A. |
| 0x000086 | Meta System S.p.A. |
| 0x000087 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x000088 | MANN+HUMMEL GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co. |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.a |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp |
| 0x000094 | Küster Automotive GmbH |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental AG |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls Inc. |
| 0x00009A | Takata-Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN Plc |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | peiker acustic GmbH & Co. KG |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Automotive Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | A.D.C. Automotive Distance Control Systems GmbH |
| 0x0000A5 | Novero Dabendorf GmbH |
| 0x0000A6 | LAMES S.p.a. |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Harbin Wan Yu Technology Co |
| 0x0000A9 | ThyssenKrupp Presta AG |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors Stuttgart GmbH |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA S.p.A. |
| 0x0000AF | Alfmeier Präzision AG |
| 0x0000B0 | Eltek Deutechland GmbH |
| 0x0000B1 | OMRON Automotive Electronics Europe GmbH |
| 0x0000B2 | ASK Industries GmbH |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive |
| 0x0000B6 | Hans Widmaier Fernmelde- und Feinwerktechnik |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | Kyocera Display Europe GmbH |
| 0x0000B9 | Magna Powertrain AG & Co. KG |
| 0x0000BA | BorgWarner Beru Systems GmbH |
| 0x0000BB | BMW AG |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin Deutschland Zugangssysteme GmbH |
| 0x0000BE | Schaeffler Technologies AG & Co. KG |
| 0x0000BF | JTEKT Corporation |
| 0x0000C0 | VLF |
| 0x0000C1 | Flextronics |
| 0x0000C2 | LG Chem |
| 0x0000C3 | Panasonic |
| 0x0000C4 | Alpitronic GmbH |
| 0x0000C5 | Telemotive AG |
| 0x0000C6 | Garmin |
| 0x0000C7 | RSG Elotech Elektronische Baugruppen GmbH |
| 0x0000C8 | KEBODA TECHNOLOGY CORP |
| 0x0000C9 | Aptiv |
| 0x0000CA | SEG Automotive Germany GmbH |
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

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0x1750 | PWF_Basinetz | 0-n | - | 0xFF | - | 1 | 1 | 0.000000 |
| 0x1751 | PWF_Teilnetz | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
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

Dimensions: 13 rows × 3 columns

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
| 0x44 | ECURSU | ECURsuSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0x5F | ECUGDM | ECUGarageDiagnoseMode |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-iarttexte"></a>
### IARTTEXTE

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

<a id="table-uds-tab-roe-aktiv"></a>
### UDS_TAB_ROE_AKTIV

Dimensions: 3 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Aktive Fehlermeldung deaktiviert |
| 0x01 | Aktive Fehlermeldung aktiviert |
| 0xFF | Status der aktiven Fehlermeldung nicht feststellbar |

<a id="table-act-get-ergebnis-abbruch"></a>
### ACT_GET_ERGEBNIS_ABBRUCH

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | start |
| 1 | no gradient_1 |
| 2 | gradient_1 valid |
| 3 | gradient_1 low |
| 4 | gradient_1 high |
| 7 | no gradient_2 |
| 8 | gradient_2 valid |
| 9 | gradient_2 low |
| 10 | gradient_2 high |
| 20 | problem gear shifter |
| 21 | problem preasure |
| 22 | problem timeout |
| 23 | problem execution conditions |
| 30 | kisspoint increment |
| 31 | kisspoint valid |
| 32 | kisspoint decrement low |
| 33 | kisspoint decrement high |
| 34 | kisspoint decrement unsure |
| 35 | kisspoint min-value |
| 36 | kisspoint.max-value |

<a id="table-act-get-zust-adap-main-abbruch"></a>
### ACT_GET_ZUST_ADAP_MAIN_ABBRUCH

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | off |
| 1 | initialisation |
| 2 | measurement of clutch 1 |
| 3 | measurement of clutch 2 |
| 4 | result valid |

<a id="table-act-get-zust-adap-sub-abbruch"></a>
### ACT_GET_ZUST_ADAP_SUB_ABBRUCH

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | set gear |
| 1 | wait gear |
| 2 | gradient 1 |
| 3 | set pressure |
| 4 | gradient 2 |
| 5 | result |
| 6 | ready |
| 7 | break-off |

<a id="table-arg-0x4100-d"></a>
### ARG_0X4100_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LOESCHEN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1=Verleissdaten sollen geloescht werden |

<a id="table-arg-0x42a4-d"></a>
### ARG_0X42A4_D

Dimensions: 16 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PV1_DATEN_1 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 1 |
| PV1_DATEN_2 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 2 |
| PV1_DATEN_3 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 3 |
| PV1_DATEN_4 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 4 |
| PV1_DATEN_5 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 5 |
| PV1_DATEN_6 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 6 |
| PV1_DATEN_7 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 7 |
| PV1_DATEN_8 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 8 |
| PV1_DATEN_9 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 9 |
| PV1_DATEN_10 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 10 |
| PV1_DATEN_11 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 11 |
| PV1_DATEN_12 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 12 |
| PV1_DATEN_13 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 13 |
| PV1_DATEN_14 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 14 |
| PV1_DATEN_15 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 15 |
| PV1_DATEN_16 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV1 Daten Byte 16 |

<a id="table-arg-0x42a5-d"></a>
### ARG_0X42A5_D

Dimensions: 16 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PV2_DATEN_1 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 1 |
| PV2_DATEN_2 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 2 |
| PV2_DATEN_3 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 3 |
| PV2_DATEN_4 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 4 |
| PV2_DATEN_5 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 5 |
| PV2_DATEN_6 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 6 |
| PV2_DATEN_7 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 7 |
| PV2_DATEN_8 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 8 |
| PV2_DATEN_9 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 9 |
| PV2_DATEN_10 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 10 |
| PV2_DATEN_11 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 11 |
| PV2_DATEN_12 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 12 |
| PV2_DATEN_13 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 13 |
| PV2_DATEN_14 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 14 |
| PV2_DATEN_15 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 15 |
| PV2_DATEN_16 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV2 Daten Byte 16 |

<a id="table-arg-0x42a6-d"></a>
### ARG_0X42A6_D

Dimensions: 16 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PV6_DATEN_1 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 1 |
| PV6_DATEN_2 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 2 |
| PV6_DATEN_3 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 3 |
| PV6_DATEN_4 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 4 |
| PV6_DATEN_5 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 5 |
| PV6_DATEN_6 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 6 |
| PV6_DATEN_7 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 7 |
| PV6_DATEN_8 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 8 |
| PV6_DATEN_9 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 9 |
| PV6_DATEN_10 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 10 |
| PV6_DATEN_11 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 11 |
| PV6_DATEN_12 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 12 |
| PV6_DATEN_13 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 13 |
| PV6_DATEN_14 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 14 |
| PV6_DATEN_15 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 15 |
| PV6_DATEN_16 | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV6 Daten Byte 16 |

<a id="table-arg-0x42a7-d"></a>
### ARG_0X42A7_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PV7_DATEN | - | high | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert PV7 Daten Byte 1 |

<a id="table-arg-0x42ab-d"></a>
### ARG_0X42AB_D

Dimensions: 10 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GETRIEBECODE_1 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 1 |
| GETRIEBECODE_2 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 2 |
| GETRIEBECODE_3 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 3 |
| GETRIEBECODE_4 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 4 |
| GETRIEBECODE_5 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 5 |
| GETRIEBECODE_6 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 6 |
| GETRIEBECODE_7 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 7 |
| GETRIEBECODE_8 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 8 |
| GETRIEBECODE_9 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 9 |
| GETRIEBECODE_10 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswerte für den Getriebecode Byte 10 |

<a id="table-arg-0x42ac-d"></a>
### ARG_0X42AC_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RADSATZVARIANTE_1 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert  für die Radsatzvariante Byte 1 |

<a id="table-arg-0x42ad-d"></a>
### ARG_0X42AD_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HYDRAULIKPUMPE_1 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert für die Hydraulikpumpe Byte 1 |

<a id="table-arg-0x42ae-d"></a>
### ARG_0X42AE_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TEMPERATURSENSOR_1 | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert  für die Radsatzvariante Byte 1 |

<a id="table-arg-0x42af-d"></a>
### ARG_0X42AF_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TEMPERATURSENSOR_WIDERSTAND | kOhm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert |

<a id="table-arg-0x4600-d"></a>
### ARG_0X4600_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CODIERUNG | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=ROLLENBETRIEB, 1=RADABRISS |
| AKTIVIERUNG | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0=inaktiv, 1=aktiv |

<a id="table-arg-0xae30-r"></a>
### ARG_0XAE30_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TESTPRG_NR | + | - | 0-n | high | unsigned char | - | TAB_DKG_TEST_UND_EINLERNEN_PRG | 1.0 | 1.0 | 0.0 | - | - | Testprogramm, welches gestartet werden soll: 0x20 = Beliebigen Gang einlegen 0x21 = Spülfunktion starten 0x22 = Solldruckvorgabe Kupplung 1 0x23 = Solldruckvorgabe Kupplung 2 0x24 = Vorgabe des Systemdrucks 0x25 = Kupplungskuehlung aktivieren 0x26 = Diagnose Parksperrenmagnet 0x27 = Diagnose PV7 0x30 = Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1+2) 0x32 = Getriebe einlernen 0x33 = Adaptionswerte in NVRAM speichern 0x34 = Ventilkennlinien einlernen PV1 und PV2 0x35 = Fehlerspeicher formatieren |
| STARTWERT | + | - | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Beliebigen Gang einlegen - Eingabebereich = 0 bis 7 oder 14 für Rückwärts Gang Solldruckvorgabe Kupplung 1 - Eingabebereich = 0 - 15000 (mbar) Solldruckvorgabe Kupplung 2 - Eingabebereich = 0 - 15000 (mbar) Vorgabe des Systemdrucks  - Eingabebereich = 0 - 20000 (mbar) Kupplungskuehlung aktivieren - 0x00 = Geschlossen Kupplungskuehlung aktivieren - 0x01 = min. Kupplungskuehlung Kupplungskuehlung aktivieren - 0x02 = max. Kupplungskuehlung Kupplungsschleifunkt einlernen - 0x00 = Einlernen am EOL Kupplungsschleifunkt einlernen - 0x01 = Einlernen in der Werkstatt Adaptionswerte in NVRAM speichern - 0x00 = Block A - 0x01 = Block B Adaptionswerte in NVRAM speichern - 0x02 = Block C - 0x03 = Block D |

<a id="table-arg-0xde34-d"></a>
### ARG_0XDE34_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STELLGLIED_IO_HEX | 0-n | high | unsigned char | - | TAB_DKG_IO_SETZEN | 1.0 | 1.0 | 0.0 | - | - | Stellglied, welches angesteuert werden soll. Siehe Tabelle |
| STELLGLIED_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Wert, der für das Stellglied angenommen werden soll. |

<a id="table-arg-0xde36-d"></a>
### ARG_0XDE36_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ADAPTIONSWERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Eingebe des Hexwertes 0xA0 = Adaptionswerte Kisspoint K1 0xA1 = Adaptionswerte Kisspoint K2 0xA2 = Adaptionswerte Kupplungsmomentenkennlinie K1 0xA3 = Adaptionswerte Kupplungsmomentenkennlinie K2 0xAA = Adaptionswerte für Ventilkennline PV6 0xB0 = Adaptionswerte für Ventilkennline PV1 + PV2 0xB1 = Adaptionswerte für DRM 0xB2 = Adaptionswerte des Semischlupfs für Gänge 1-7 |

<a id="table-arg-0xf770-r"></a>
### ARG_0XF770_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BLOCK_ID | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 255.0 | zulässige Werte 0...23 |

<a id="table-arg-0xf771-r"></a>
### ARG_0XF771_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BLOCK_ID | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 255.0 | zulässige Werte 0...23 |
| BLOCK_OFFSET | + | - | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 65535.0 | Werte 0..65535 |

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

<a id="table-cla-clu-state"></a>
### CLA_CLU_STATE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | GEN_CLU_NO_ACTION |
| 1 | GEN_CLU_DISENGAGE |
| 2 | GEN_CLU_TQ_CTRL |
| 3 | GEN_CLU_FIRST_FILL |
| 4 | GEN_CLU_DEFLATE |
| 5 | GEN_CLU_MOD_CHG |
| 6 | GEN_CLU_PARKING |
| 7 | GEN_CLU_STR_ERR |
| 8 | GEN_CLU_TG_LOCKED |

<a id="table-clu-state-details"></a>
### CLU_STATE_DETAILS

Dimensions: 24 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x16 | CLA_BANK_VPM |
| 0x0A | CLA_DEFLATED |
| 0x09 | CLA_DEFLTING |
| 0x05 | CLA_DESTKING_EXIT |
| 0x03 | CLA_DESTKING_INIT |
| 0x04 | CLA_DESTKING_STATIC |
| 0x0E | CLA_DESTKING_WASH |
| 0x14 | CLA_DIA_PV7 |
| 0x0B | CLA_FIRSTFILLED |
| 0x0C | CLA_FIRSTFILLING |
| 0x12 | CLA_FOR_FILLED |
| 0x17 | CLA_HOOKDIA |
| 0x10 | CLA_KPA |
| 0x15 | CLA_MICROSLIP |
| 0x0F | CLA_PARKING_LOCK |
| 0x02 | CLA_STRKING_EXIT |
| 0x00 | CLA_STRKING_INIT |
| 0x01 | CLA_STRKING_STATIC |
| 0x11 | CLA_STROKING_ERROR |
| 0x13 | CLA_TG_LOCKED |
| 0x08 | CLA_TQ_CTRL_EXIT |
| 0x06 | CLA_TQ_CTRL_INIT |
| 0x07 | CLA_TQ_CTRL_STATIC |
| 0x0D | CLA_TQ_CTRL_WASH |

<a id="table-dma-can-notl-source"></a>
### DMA_CAN_NOTL_SOURCE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Fehlerspeicher |
| 2 | Motor |
| 4 | Test |

<a id="table-dma-z-pos"></a>
### DMA_Z_POS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 5 | D |
| 6 | N |
| 7 | R |
| 8 | P |
| 14 | M |

<a id="table-dm-tab-roe-activated-dop"></a>
### DM_TAB_ROE_ACTIVATED_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Aktive Fehlermeldung deaktiviert |
| 1 | Aktive Fehlermeldung aktiviert |

<a id="table-dpl-error"></a>
### DPL_ERROR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Fehler |
| 1 | ungewollt eingefallen |
| 4 | ungewollt ausgelegt |
| 8 | Parksperrensensorfehler |
| 44 | Druck an Kupplungen beim Auslegen |
| 50 | hängendes Absperrventil |
| 60 | Sicherheitszeit Auslegen |
| 70 | Halbe Sicherheitszeit Einlegen |
| 80 | Sicherheitszeit Einlegen |

<a id="table-dpl-error-psm"></a>
### DPL_ERROR_PSM

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Kurzschluss Highside =&gt; Masse |
| 0x02 | Kurzschluss Lowside =&gt; Masse od. Leitungsunterbrechung |
| 0x04 | Wicklungsschluss od. Kurzschluss Highside =&gt; Ubat |
| 0x08 | HS-Ubat |
| 0x10 | Kurzschluss Lowside =&gt; Ubat |
| 0x20 | Unbekannter Fehler =&gt; kleine Diagnose |
| 0x40 | Erhöhter Widerstand |

<a id="table-dpl-fa-st"></a>
### DPL_FA_ST

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | undefiniert |
| 0x01 | Sicherheitszeit Einlegen |
| 0x02 | Halbe Sicherheitszeit Einlegen |
| 0x04 | Sicherheitszeit Auslegen |
| 0x08 | Sicherheitszeit Einlegen weil TG gesperrt |
| 0x0E | Sicherheitszeit Einlegen weil Tieftemperatur |

<a id="table-e2-dbg-noclear"></a>
### E2_DBG_NOCLEAR

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Status Motorschleppmomentenregelung MSR in Ebene2 |
| 1 | Status Kupplungsdruck 1 |
| 2 | Status Kupplungsdruck 2 |
| 3 | Rückschaltverhinderung aktiviert |
| 4 | P einlegen verhindern (ABS, V_Fzg &gt; V_Wheel, V_VA &gt; V_HA) |
| 5 | Schalten nach Rückwärts unterbinden |
| 6 | Radgeschw. P + NP defekt |
| 7 | Wahlhebelnotlauf aktiv |

<a id="table-e2-output-noclear"></a>
### E2_OUTPUT_NOCLEAR

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0002 | Schutzziel 001 |
| 0x0004 | Schutzziel 003 |
| 0x0008 | Schutzziel 004a |
| 0x0010 | Schutzziel 006 |
| 0x0020 | Schutzziel 009a |
| 0x0040 | Schutzziel 009b |
| 0x0080 | Schutzziel 010 |
| 0x0100 | Schutzziel 013 |
| 0x0200 | Schutzziel 014 |
| 0x0400 | Schutzziel 019 |
| 0x0800 | TEMIC Sollwertverletzung |
| 0x1000 | Schutzziel 016 |
| 0x1001 | undefiniert |
| 0x8002 | Schutzziel 001 |
| 0x8004 | Schutzziel 003 |
| 0x8008 | Schutzziel 004a |
| 0x8010 | Schutzziel 006 |
| 0x8020 | Schutzziel 009a |
| 0x8040 | Schutzziel 009b |
| 0x8080 | Schutzziel 010 |
| 0x8100 | Schutzziel 013 |
| 0x8200 | Schutzziel 014 |
| 0x8400 | Schutzziel 019 |
| 0x8800 | TEMIC Sollwertverletzung |
| 0x9000 | Schutzziel 016 |
| 0xFFFF | undefiniert |

<a id="table-e2-sds-gws-noclear"></a>
### E2_SDS_GWS_NOCLEAR

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x03 | DRI_Drive_AG |
| 0x04 | DRI_Fehler_AG |
| 0x02 | DRI_Neutral_AG |
| 0x05 | DRI_No_Action_AG |
| 0x00 | DRI_Parking_AG |
| 0x01 | DRI_Reverse_AG |

<a id="table-energiesparmode-dop"></a>
### ENERGIESPARMODE_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalmode |
| 1 | Fertigungsmode |
| 2 | Transportmode |
| 3 | Flashmode |

<a id="table-ews-diag-0"></a>
### EWS_DIAG_0

Dimensions: 8 rows × 3 columns

| WERT | TEXT | TEXT_EN |
| --- | --- | --- |
| 0 | Freigabe noch nicht erteilt, SK nicht verriegelt | - |
| 1 | Freigabe erteilt, SK nicht verriegelt | - |
| 2 | Freigabe abgelehnt, SK nicht verriegelt | - |
| 3 | Nicht definiert, SK nicht verriegelt | - |
| 128 | Freigabe noch nicht erteilt, SK verriegelt | - |
| 129 | Freigabe erteilt, SK verriegelt | - |
| 130 | Freigabe abgelehnt, SK verriegelt | - |
| 131 | Nicht definiert, SK verriegelt | - |

<a id="table-ews-diag-1"></a>
### EWS_DIAG_1

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DH-Abgleichvorgang nicht aktiv |
| 1 | DH-Abgleichvorgang aktiv |
| 2 | DH-Abgleichvorgang nicht aktiv, E-Label gleich 1 |
| 3 | DH-Abgleichvorgang aktiv, E-Label gleich 1 |

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
| F_HLZ_VIEW | ja |

<a id="table-fehlerklasse-dop"></a>
### FEHLERKLASSE_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Fehlerklasse verfuegbar |
| 1 | Ueberpruefung beim naechsten Werkstattbesuch |
| 2 | Ueberpruefung beim naechsten Halt |
| 4 | Ueberpruefung sofort erforderlich |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 191 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021800 | Energiesparmode aktiv | 1 | -Eventgetriggert über Diagnoseschnittstelle |
| 0x02FF18 | Test Diagnosemaster | 1 | keine |
| 0x40D001 | Drucksensor Kupplung 1: hängt | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D002 | Drucksensor Kupplung 1: Offset | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt -Kupplung wurde entleert |
| 0x40D004 | Drucksensor Kupplung 1: Kurzschluss | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D008 | Drucksensor Kupplung 1: Kabelbruch | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D108 | Referenzmoment Kupplung 1:  zu hoch | 0 | -Konstantfahrt -Kupplungstemperatur 60°C bis 120°C -Drehzahlbereich 1300U/min - 3500U/min -Funktion  Einlernen Kisspoint  angestoßen |
| 0x40D201 | Drucksensor Kupplung 2: hängt | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D202 | Drucksensor Kupplung 2: Offset | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt -Kupplung wurde entleert |
| 0x40D204 | Drucksensor Kupplung 2: Kurzschluss | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D208 | Drucksensor Kupplung 2: Kabelbruch | 0 | -Nach Systemstart sind 320ms vergangen -Das System befindet sich nicht im Nachlauf -Die Diagnose der Sensorversorgungsspannung hat keine Fehler festgestellt |
| 0x40D304 | Druckvergleich Kupplung 1:  Druck zu niedrig | 0 | -Drucksignal i.O. -Cut-Off nicht auf Tank geschaltet -Der Druckregler arbeitet open-Loop oder closed-Loop (d.h. keine Stromsteuerung) -Die Endstufe wurde nicht abgeschaltet |
| 0x40D308 | Druckvergleich Kupplung 1:  Druck zu hoch | 0 | -Drucksignal i.O. -Cut-Off nicht auf Tank geschaltet -Der Druckregler arbeitet open-Loop oder closed-Loop (d.h. keine Stromsteuerung) -Die Endstufe wurde nicht abgeschaltet |
| 0x40D404 | Druckvergleich Kupplung 2:  Druck zu niedrig | 0 | -Drucksignal i.O. -Cut-Off nicht auf Tank geschaltet -Der Druckregler arbeitet open-Loop oder closed-Loop (d.h. keine Stromsteuerung) -Die Endstufe wurde nicht abgeschaltet |
| 0x40D408 | Druckvergleich Kupplung 2:  Druck zu hoch | 0 | -Drucksignal i.O. -Cut-Off nicht auf Tank geschaltet -Der Druckregler arbeitet open-Loop oder closed-Loop (d.h. keine Stromsteuerung) -Die Endstufe wurde nicht abgeschaltet |
| 0x40D502 | Regelventil PV1: Kurzschluss in Endstufe | 0 | - |
| 0x40D504 | Regelventil PV1: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D508 | Regelventil PV1: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D602 | Regelventil PV2: Kurzschluss in Endstufe | 0 | - |
| 0x40D604 | Regelventil PV2: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D608 | Regelventil PV2: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D702 | Regelventil PV3: Kurzschluss in Endstufe | 0 | - |
| 0x40D704 | Regelventil PV3: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D708 | Regelventil PV3: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D802 | Regelventil PV4: Kurzschluss in Endstufe | 0 | - |
| 0x40D804 | Regelventil PV4: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D808 | Regelventil PV4: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D902 | Regelventil PV6: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D904 | Regelventil PV6: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40D908 | Regelventil PV6: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40DA02 | Regelventil PV7: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40DA04 | Regelventil PV7: Kabelbruch | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40DA08 | Regelventil PV7: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40DB01 | Kühlung: kein Kühlöl oder kein Kühlstrom | 0 | keine |
| 0x40DC01 | Sensor für Kühlöltemperatur: Default (Modell+5C) | 0 | keine |
| 0x40DE01 | Temperatur Kupplung: Phase Rot | 0 | keine |
| 0x40DF01 | Temperatur Kupplung: Phase Schwarz | 0 | keine |
| 0x40E001 | Sensor für Kühlöltemperatur: Bereichsverletzung (Modell+5C) | 0 | keine |
| 0x40E002 | Sensor für Kühlöltemperatur: Gradientenüberwachung (Modell+5C) | 0 | keine |
| 0x40E101 | Abschaltpfad 1 defekt:  klemmt in Position 1 | 0 | -Beim Spülen von Kupplung 1 |
| 0x40E201 | Abschaltpfad 2 defekt:  klemmt in Position 1 | 0 | -Beim Spülen von Kupplung 2 |
| 0x40E301 | Regelventil PV7: klemmt in unbekannter Stellung (Hotmode II) | 0 | keine |
| 0x40E402 | Schaltventil SV1: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E408 | Schaltventil SV1: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E502 | Schaltventil SV2: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E508 | Schaltventil SV2: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E602 | Schaltventil SV3: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E608 | Schaltventil SV3: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E702 | Schaltventil SV4: Kurzschluss in Endstufe | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40E708 | Schaltventil SV4: Kurzschluss | 0 | -Endstufen aktiv -Endstufen melden keine Fehler |
| 0x40EB04 | Adaption Regelventil PV6: untere Grenze verletzt | 0 | -Konstantfahrt |
| 0x40EB08 | Adaption Regelventil PV6: obere Grenze verletzt | 0 | -Konstantfahrt |
| 0x40EC02 | Befüllzeit Kupplung 1 | 0 | -Drucksignal i.O. -Kupplung wird gerade befüllt |
| 0x40ED02 | Befüllzeit Kupplung 2 | 0 | -Drucksignal i.O. -Kupplung wird gerade befüllt |
| 0x40EE08 | Referenzmoment Kupplung 2:  zu hoch | 0 | -Konstantfahrt -Kupplungstemperatur 60°C bis 120°C -Drehzahlbereich 1300U/min - 3500U/min -Funktion  Einlernen Kisspoint  angestoßen |
| 0x40F001 | Schaltstange 1-3 | 0 | -Motor an |
| 0x40F002 | Schaltstange 1-3: Quellenfehler | 0 | -Motor an |
| 0x40F101 | Schaltstange 2-R | 0 | -Motor an |
| 0x40F102 | Schaltstange 2-R: Quellenfehler | 0 | -Motor an |
| 0x40F201 | Schaltstange 6-4 | 0 | -Motor an |
| 0x40F202 | Schaltstange 6-4: Quellenfehler | 0 | -Motor an |
| 0x40F301 | Schaltstange 5-7 | 0 | -Motor an |
| 0x40F302 | Schaltstange 5-7: Quellenfehler | 0 | -Motor an |
| 0x40F401 | Schaltstangensensor  6-4: unter Schwelle | 0 | keine |
| 0x40F402 | Schaltstangensensor  6-4: ueber Schwelle | 0 | keine |
| 0x40F501 | Schaltstangensensor  5-7: unter Schwelle | 0 | keine |
| 0x40F502 | Schaltstangensensor  5-7: ueber Schwelle | 0 | keine |
| 0x40F601 | Schaltstangensensor  2-R: unter Schwelle | 0 | keine |
| 0x40F602 | Schaltstangensensor 2-R: ueber Schwelle | 0 | keine |
| 0x40F701 | Schaltstangensensor 1-3: unter Schwelle | 0 | keine |
| 0x40F702 | Schaltstangensensor 1-3: ueber Schwelle | 0 | keine |
| 0x40FA01 | Schaltstange 1-3: Gangfehler | 0 | Motor an |
| 0x40FB01 | Schaltstange 2-R: Gangfehler | 0 | Motor an |
| 0x40FC01 | Schaltstange 5-7: Gangfehler | 0 | Motor an |
| 0x40FD01 | Schaltstange 6-4: Gangfehler | 0 | Motor an |
| 0x40FF01 | Temperatursensor 1: Temperaturwert oberhalb zulässigem Grenzwert | 0 | keine |
| 0x40FF02 | Temperatursensor 1: Temperaturwert unterhalb zulässigem Grenzwert | 0 | keine |
| 0x40FF08 | Temperatursensor 1: Wert unplausibel | 0 | keine |
| 0x410001 | Temperatursensor 2: Temperaturwert oberhalb zulässigem Grenzwert | 0 | keine |
| 0x410002 | Temperatursensor 2: Temperaturwert unterhalb zulässigem Grenzwert | 0 | keine |
| 0x410008 | Temperatursensor 2:  Wert unplausibel | 0 | keine |
| 0x410101 | Lokale Versorgungsspannung Überspannung | 0 | keine |
| 0x410102 | Lokale Versorgungsspannung Unterspannung | 0 | keine |
| 0x410308 | Drehzahlsensor TG1: Wert nicht plausibel | 0 | -Motor EIN, Gang im entsprechenden Teilgetriebe eingelegt, Kupplung ¿geschlossen¿. |
| 0x410408 | Drehzahlsensor TG2: Wert nicht plausibel | 0 | -Motor EIN, Gang im entsprechenden Teilgetriebe eingelegt, Kupplung ¿geschlossen¿. |
| 0x410501 | Sicherheitszeit Einlegen:  überschritten beim Einlegen über PS_1 | 0 | Parksperre muss betätigt werden |
| 0x410502 | Sicherheitszeit Einlegen:  überschritten beim Einlegen über PS_2 | 0 | Parksperre muss betätigt werden |
| 0x410701 | Parksperrensensor | 0 | keine |
| 0x410804 | Sicherheitszeit Auslegen: überschritten beim Auslegen | 0 | -Parksperre muss betätigt werden |
| 0x410A01 | Parksperre: Ungewollte Bewegung Auslegen | 0 | Parksperre Ein- oder Ausgelegt |
| 0x410C01 | Parksperrenschieber 1: hängt | 0 | -Parksperre auslegen |
| 0x410C02 | Parksperrenschieber 2: hängt | 0 | -Parksperre auslegen |
| 0x410D01 | Parksperrenhaken: hängt nicht am Seil | 0 | -Parksperre einlegen |
| 0x410E01 | N-Haltephase: über Tester deaktiviert | 0 | keine |
| 0x410F01 | Vorspannung UH2_7V4: oberhalb Schwelle | 0 | keine |
| 0x410F02 | Vorspannung UH2_7V4: unterhalb Schwelle | 0 | keine |
| 0x411001 | interne 5V  Spannung: oberhalb Schwelle | 0 | keine |
| 0x411002 | interne 5V Spannung: unterhalb Schwelle | 0 | keine |
| 0x411101 | Sensorversorgung SV1_5V: oberhalb Schwelle | 0 | keine |
| 0x411102 | Sensorversorgung SV1_5V: unterhalb Schwelle | 0 | keine |
| 0x411201 | Sensorversorgung SV2_5V: oberhalb Schwelle | 0 | keine |
| 0x411202 | Sensorversorgung SV2_5V: unterhalb Schwelle | 0 | keine |
| 0x411408 | DKG Getriebesteuerung: interner Fehler (Core Eigendiagnose: Fehler 1) | 0 | keine |
| 0x411508 | DKG Getriebesteuerung: interner Fehler (Prozessortemepratur TC  1766 unplausibel) | 0 | keine |
| 0x411608 | DKG Getriebesteuerung: interner Fehler (EEPROM-Daten, Blöcke A,B) | 0 | Aufstarten des Steuergeräts |
| 0x411702 | Endstufe 1: Versorgungsspannung Ventilgruppe 1 unterhalb zulässigem Grenzwert | 0 | keine |
| 0x411802 | Endstufe 2: Versorgungsspannung Ventilgruppe 2 unterhalb zulässigem Grenzwert | 0 | keine |
| 0x411902 | Endstufe 3: Versorgungsspannung Ventilgruppe 3 unterhalb zulässigem Grenzwert | 0 | keine |
| 0x411A08 | Getriebe: Heissabschaltung | 0 | keine |
| 0x411C08 | Antriebsdrehzahlsensor: Wert nicht plausibel | 0 | Motor an |
| 0x412301 | Parksperrenmagnet: Bestromung eventuell nicht mehr möglich | 0 | -v &gt; 10km/h, Getr. Pos = D -PS einlegen |
| 0x412501 | DKG Getriebesteuerung: interner Fehler (Ebene 2, Schutzziele 13, 14, 16, 19, Temic) | 0 | keine |
| 0x412601 | DKG Getriebesteuerung: interner Fehler (Ebene 2, Schutzziele 3, 4a, 6) | 0 | keine |
| 0x412701 | DKG Getriebesteuerung: interner Fehler (Ebene 2, Schutzziele 1, 10) | 0 | keine |
| 0x412801 | DKG Getriebesteuerung: interner Fehler (Ebene 2, Schutzziele 9a, 9b) | 0 | keine |
| 0x412901 | DKG Getriebesteuerung: interner Fehler (Ebene 2-Strich) | 0 | keine |
| 0x412B01 | Einlernvorgang Kupplung: Abbruch | 0 | -Fahrzeug steht, Bremse betätigt, kein Fahrpedal, Einlernen Kisspoint läuft |
| 0x412D04 | Parksperre: eingefallen | 0 | -Parksperre ausgelegt |
| 0x412F08 | EWS: Fahrerwunsch verworfen | 1 | Klemme 15 EIN |
| 0xCF040A | DKG, FA-CAN: Kommunikationsfehler | 1 | keine |
| 0xCF0486 | DKG, A-CAN: Kommunikationsfehler | 1 | keine |
| 0xCF0BFF | DM-Trigger NW | 1 | keine |
| 0xCF1401 | Botschaft (Status GWS, 0x0197 A-CAN) fehlt, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1402 | Botschaft (Status GWS, 0x0197 A CAN) nicht aktuell, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1404 | Botschaft (Status GWS, 0x0197 A CAN) Prüfsumme falsch, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1501 | Botschaft (Status GWS, 0x0197 FA CAN) fehlt, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1502 | Botschaft (Status GWS, 0x0197 FA CAN) nicht aktuell, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1504 | Botschaft (Status GWS, 0x0197 FA CAN) Prüfsumme falsch, Empfänger DKG, Sender GWS | 1 | keine |
| 0xCF1601 | Botschaft (Drehmoment Kurbelwelle 1, 0x00A5) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1602 | Botschaft (Drehmoment Kurbelwelle 1, 0x00A5) nicht aktuell, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1604 | Botschaft (Drehmoment Kurbelwelle 1, 0x00A5) Prüfsumme falsch, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1701 | Botschaft (Drehmoment Kurbelwelle 2, 0x00A6) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1702 | Botschaft (Drehmoment Kurbelwelle 2, 0x00A6) nicht aktuell, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1704 | Botschaft (Drehmoment Kurbelwelle 2, 0x00A6) Prüfsumme falsch, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1801 | Botschaft (Drehmoment Kurbelwelle 3, 0x00A7) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1802 | Botschaft (Drehmoment Kurbelwelle 3, 0x00A7) nicht aktuell, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1804 | Botschaft (Drehmoment Kurbelwelle 3, 0x00A7) Prüfsumme falsch, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1901 | Botschaft (Status Klemmen, 0x012F) fehlt, Empfänger DKG, Sender CAS | 1 | keine |
| 0xCF1902 | Botschaft (Status Klemmen, 0x012F) nicht aktuell, Empfänger DKG, Sender CAS | 1 | keine |
| 0xCF1904 | Botschaft (Status Klemmen, 0x012F) Prüfsummen falsch, Empfänger DKG, Sender CAS | 1 | keine |
| 0xCF1A01 | Botschaft (Daten Antriebsstrang, 0x03FB) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF1B01 | Botschaft (Ist Drehzahl Rad ungesichert, 0x0254) fehlt, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF1C01 | Botschaft (Status Gurtkontakt, 0x0297) fehlt, Empfänger DKG, Sender ACSM | 1 | keine |
| 0xCF1C02 | Botschaft (Status Gurtkontakt, 0x0297) nicht aktuell, Empfänger DKG, Sender ACSM | 1 | keine |
| 0xCF1C04 | Botschaft (Status Gurtkontakt, 0x0297) Prüfsumme falsch, Empfänger DKG, Sender ACSM | 1 | keine |
| 0xCF1D01 | Botschaft (Status Anhänger, 0x02E4) fehlt, Empfänger DKG, Sender AHM | 1 | keine |
| 0xCF1E01 | Botschaft (Status Stabilisierung, 0x0173) fehlt, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF1E02 | Botschaft (Status Stabilisierung, 0x0173) nicht aktuell, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF1E04 | Botschaft (Status Stabilisierung, 0x0173) Prüfsumme falsch, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF1F01 | Botschaft (Status Türsensoren, 0x01E1) fehlt, Empfänger DKG, Sender FRMFA | 1 | keine |
| 0xCF1F02 | Botschaft (Status Türsensoren, 0x01E1) nicht aktuell, Empfänger DKG, Sender FRMFA | 1 | keine |
| 0xCF1F04 | Botschaft (Status Türsensoren, 0x01E1) Prüfsummen falsch, Empfänger DKG, Sender FRMFA | 1 | keine |
| 0xCF2001 | Botschaft (Diagnose OBD, 0x0397) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF2201 | Botschaft (Bedienung Schaltwippen, 0x0207) fehlt, Empfänger DKG, Sender SZL | 1 | keine |
| 0xCF2202 | Botschaft (Bedienung Schaltwippen, 0x0207) nicht aktuell, Empfänger DKG, Sender SZL | 1 | keine |
| 0xCF2204 | Botschaft (Bedienung Schaltwippen, 0x0207) Prüfsumme falsch, Empfänger DKG, Sender SZL | 1 | keine |
| 0xCF2301 | Botschaft (Ist-Bremsmoment Summe, 0x00EF) fehlt, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF2302 | Botschaft (Ist-Bremsmoment Summe, 0x00EF) nicht aktuell, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF2304 | Botschaft (Ist-Bremsmoment Summe, 0x00EF) Prüfsumme falsch, Empfänger DKG, Sender DSC | 1 | keine |
| 0xCF2401 | Botschaft (Längsbeschleunigung Schwerpunkt, 0x0199) fehlt, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2402 | Botschaft (Längsbeschleunigung Schwerpunkt, 0x0199) nicht aktuell, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2404 | Botschaft (Längsbeschleunigung Schwerpunkt, 0x0199) Prüfsumme falsch, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2501 | Botschaft (Querbeschleunigung Schwerpunkt, 0x019A) fehlt, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2502 | Botschaft (Querbeschleunigung Schwerpunkt, 0x019A) nicht aktuell, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2504 | Botschaft (Querbeschleunigung Schwerpunkt, 0x019A) Prüfsumme falsch, Empfänger DKG, Sender ICM_QL | 1 | keine |
| 0xCF2601 | Botschaft (Winkel Fahrpedal, 0x00D9) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF2602 | Botschaft (Winkel Fahrpedal, 0x00D9) nicht aktuell, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF2604 | Botschaft (Winkel Fahrpedal, 0x00D9) Prüfsumme falsch, Empfänger DKG, Sender Motorsteuerung | 1 | keine |
| 0xCF2801 | Botschaft (Fahrzeugzustand, 0x03A0) fehlt, Empfänger DKG, Sender JBBF | 1 | keine |
| 0xCF2C08 | Schnittstelle DSC  (ID 0x254): Raddrehzahl VL ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF2D08 | Schnittstelle DSC  (ID 0x254): Raddrehzahl VR ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF2E08 | Schnittstelle DSC  (ID 0x254): Raddrehzahl HL ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF2F08 | Schnittstelle DSC  (ID 0x254): Raddrehzahl HR ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3008 | Schnittstelle Motorsteuerung (ID 0xA4): Ist-Drehmoment Kurbelwelle Motorsteuerung ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3108 | Schnittstelle Motorsteuerung (ID 0xA4): Ist-Drehmoment Kurbelwelle ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3208 | Schnittstelle Motorsteuerung (ID 0xA7): Ist-Drehmoment Kurbelwelle Fahrerwunsch Ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3308 | Schnittstelle Motorsteuerung (ID 0xA4): Drehzahl Motor ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3408 | Schnittstelle Motorsteuerung (ID 0x3FB): Solldrehzahl Leerlauf ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3508 | Schnittstelle Motorsteuerung (ID 0xD9): Winkel Fahrpedal ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3608 | Schnittstelle DSC (ID 0x173): Bremsung Fahrer ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3708 | Schnittstelle DSC (ID 0x173): Qualifier Funktion ABS ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3808 | Schnittstelle CAS (ID 0x12F): Status Klemme ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3908 | Schnittstelle CAS (ID 0x12F): Status Schluessel valid  ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3A08 | Schnittstelle FRMFA (ID 0x1E1): Status Tuerkontakt FAT ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3B08 | Schnittstelle ACSM (ID 0x297): Gurtschloss FA Status ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3C08 | Schnittstelle ACSM (ID 0x297): Status Sitzbelegung FA ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3D08 | Schnittstelle GWS (ID 0x197): Signale ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3E08 | Schnittstelle DSC (ID 0x254): alle 4 Radgeschwindigkeiten ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xCF3F08 | Botschaften GWS (ID 0x197): Wahlhebelausfall | 1 | keine |
| 0xCF4008 | Schnittstelle DSC (ID 0x173): Qualifier Funktion FDR ungültig | 1 | -CAN-Botschaft störungsfrei |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 157 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x6001 | Spannungsversorgung UBatt | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x6002 | Temperatur TCU | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6004 | Istgang Teilgetriebe 1 | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x6005 | Istgang Teilgetriebe 2 | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x600A | Fahrzeuggeschwindigkeit | km/h | High | signed int | - | 1.0 | 40.0 | 0.0 |
| 0x600B | Motordrehzahl | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600C | Getriebeeingangsdrehzahl 1 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600D | Getriebeeingangsdrehzahl 2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600E | Getriebeausgangsdrehzahl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x600F | Schaltstangenposition GBX 1/3 | mm | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6010 | Schaltstangenposition GBX 2/R | mm | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6011 | Schaltstangenposition GBX 5/7 | mm | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6012 | Schaltstangenposition GBX 6/4 | mm | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6013 | Kombinierte Umweltgröße GBX (gepuffert) | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6017 | Sollstrom PV3 GBX (gepuffert) | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x6018 | Sollstrom PV4 GBX (gepuffert) | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x6019 | Signal Positionssensor Schaltstange 6/4 | V | High | unsigned int | - | 5.0 | 1024.0 | 0.0 |
| 0x601A | Signal Positionssensor Schaltstange 5/7  | V | High | unsigned int | - | 5.0 | 1024.0 | 0.0 |
| 0x601B | Signal Positionssensor Schaltstange 2/R | V | High | unsigned int | - | 5.0 | 1024.0 | 0.0 |
| 0x601C | Signal Positionssensor Schaltstange 1/3 | V | High | unsigned int | - | 5.0 | 1024.0 | 0.0 |
| 0x601D | Fehlerstatus Schaltstange 1/3 (GBX) | 0-n | High | 0xFF | GBX_ERR | 1.0 | 1.0 | 0.0 |
| 0x601E | Fehlerstatus Schaltstange 2/R (GBX) | 0-n | High | 0xFF | GBX_ERR | 1.0 | 1.0 | 0.0 |
| 0x601F | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | High | 0xFF | GBX_ERR | 1.0 | 1.0 | 0.0 |
| 0x6020 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | High | 0xFF | GBX_ERR | 1.0 | 1.0 | 0.0 |
| 0x6029 | Radgeschwindigkeit vorne links, Rohwert | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x602A | Radgeschwindigkeit vorne rechts, Rohwert | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x602B | Radgeschwindigkeit hinten links, Rohwert | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x602C | Radgeschwindigkeit hinten rechts, Rohwert | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x602D | aktiver Gang | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x602E | Klemmenstatus KL15 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x602F | Status Kupplung 1 | 0-n | High | 0xFF | CLA_CLU_STATE | 1.0 | 1.0 | 0.0 |
| 0x6030 | Status Kupplung 2 | 0-n | High | 0xFF | CLA_CLU_STATE | 1.0 | 1.0 | 0.0 |
| 0x6031 | Drehzahl Getriebeeingang 1, Rohwert | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x6032 | Drehzahl Getriebeeingang 2, Rohwert | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x6033 | Geschwindigkeit der nicht angetriebenen Achse | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x6034 | Geschwindigkeit der angetriebenen Achse | km/h | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x6035 | Temperatur TCU, redundant, Rohwert | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6036 | Temperatur TC1766 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6037 | Motortemperatur | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6038 | Status Temperatur TCU | 0-n | High | 0xFF | QTEMP_TCU | 1.0 | 1.0 | 0.0 |
| 0x6039 | Status Temperatur TCU, redundant | 0-n | High | 0xFF | QTEMP_TCU | 1.0 | 1.0 | 0.0 |
| 0x603A | Spannung CH1 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x603B | Spannung CH2 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x603C | Spannung CH3 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x603D | Vorspannung UH2_7V4 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x603E | Sensorversorgungsspannung SV1 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x603F | Sensorversorgungsspannung SV2 | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x6040 | Interne 5V Sensorversorungsspannung | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x6042 | Temperatur TCU, Rohwert | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6043 | Quality-Information PV1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6044 | Quality-Information PV2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6045 | Quality-Information PV3 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6046 | Quality-Information PV4 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6047 | Quality-Information PV6 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6048 | Quality-Information PV7 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6049 | Quality-Information Drucksensor 1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x604A | Quality-Information Drucksensor 2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x604B | gefilterter Ist-Druck Kupplung 1 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x604C | gefilterter Ist-Druck Kupplung 2 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x604D | Solldruck Kupplung 1 | bar | High | signed int | - | 1.0 | 100.0 | 1.0 |
| 0x604E | Solldruck Kupplung 2 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x604F | detail. Status Kupplung 1 | 0-n | High | 0xFF | CLU_STATE_DETAILS | 1.0 | 1.0 | 0.0 |
| 0x6050 | detail. Status Kupplung 2 | 0-n | High | 0xFF | CLU_STATE_DETAILS | 1.0 | 1.0 | 0.0 |
| 0x6051 | Antriebsdrehzahl, Rohwert | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x6056 | Fehlerflags Sicherheitskonzept 1 | 0-n | High | 0xFFFF | SCM_ERR_FLG_LO | - | - | - |
| 0x6057 | Fehlerflags Sicherheitskonzept 2 | 0-n | High | 0xFFFF | SCM_ERR_FLG_HI | - | - | - |
| 0x6059 | Ist-Strom PV1 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605A | Ist-Strom PV2 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605B | Ist-Strom PV3 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605C | Ist-Strom PV4 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605D | Ist-Strom PV6 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605E | Ist-Strom PV7 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605F | Temperatur Abspritz-Öl | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6060 | Temperatur Sumpf-Öl | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6061 | RSC Status | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6062 | RSC Testgrösse | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6064 | Soll-Status SV3 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6065 | Soll-Status CutOff 1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6066 | Soll-Status CutOff 2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6069 | Fehlerwert PS-Diagnose | 0-n | High | 0xFF | DPL_ERROR | 1.0 | 1.0 | 0.0 |
| 0x606A | Parksperrenzustand | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x606B | Fehlerart PSM-Diagnose | 0-n | High | 0xFF | DPL_ERROR_PSM | 1.0 | 1.0 | 0.0 |
| 0x606C | Status Parksperrenmanager | 0-n | High | 0xFF | PLM_PL_STATE | 1.0 | 1.0 | 0.0 |
| 0x606D | logischer Getriebezustand | 0-n | High | 0xFF | DMA_Z_POS | 1.0 | 1.0 | 0.0 |
| 0x606E | Auto-P supply | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x606F | Auto-P switch | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6070 | PS-Sensor 1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6071 | PS-Sensor 2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6074 | Fehlerart Sicherheitszeit | 0-n | High | 0xFF | DPL_FA_ST | - | - | - |
| 0x6076 | Ausgabe Ebene 2 | 0-n | High | 0xFFFF | E2_OUTPUT_NOCLEAR | - | - | - |
| 0x6077 | Motordrehzahl CAN | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x6079 | Modelltemperatur K1 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x607A | Modelltemperatur K2 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x607B | Kühlmodus | 0-n | High | 0xFF | LBC_COOL_MODE_DES | 1.0 | 1.0 | 0.0 |
| 0x607C | Drucktoleranz K1 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x607D | Drucktoleranz K2 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x607E | Status A | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x607F | Status B | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6080 | Status C | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6081 | Status D | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6082 | Status E | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6083 | Sollwertüberwachung Temic | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6084 | Ölfilm-Temperatur K1 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6085 | Ölfilm-Temperatur K2 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6086 | statisches Motormoment | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x6087 | Abspritzsensor Rohwert | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x608B | Umgebungsluftdruck | bar | High | unsigned char | - | 2.0 | 1.0 | 299.0 |
| 0x608C | Querbeschleunigung | m/s² | High | signed int | - | 1.0 | 40.0 | 0.0 |
| 0x608D | Anzeige Getriebeposition Ebene2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x608E | Getriebesollposition aus Ebene1 | 0-n | High | 0xFF | DMA_Z_POS | 1.0 | 1.0 | 0.0 |
| 0x608F | Druck PV1 Ebene2 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6090 | Druck PV2 Ebene2 | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6091 | Parksperrenstatus Ebene2 | 0-n | High | 0xFF | PLM_PL_STATE | 1.0 | 1.0 | 0.0 |
| 0x6092 | Fahrerwunsch Ebene2 | 0-n | High | 0xFF | E2_SDS_GWS_NOCLEAR | 1.0 | 1.0 | 0.0 |
| 0x6093 | Fahrzeuggeschwindigkeit Ebene2 | - | High | unsigned int | - | 1.0 | 5.0 | 0.0 |
| 0x6094 | Eingelegte Gänge Ebene2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6095 | Aktive Schaltventile Ebene2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6096 | Drehrichtung Getriebeeingang Ebene2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6097 | Sollstrom PV1 | A | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x6098 | Sollstrom PV2 | A | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x6099 | Eingangsdrehzahl TG1 Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x609A | Eingangsdrehzahl TG2 Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x609B | Fahrpedal Ebene2 | % | High | unsigned int | - | 1.0 | 40.0 | 0.0 |
| 0x609C | Status Motorschleppmomen-tenregelung MSR Ebene2 | 0-n | High | 0xFF | SIGNAL_STATUS | 1.0 | 1.0 | 0.0 |
| 0x609D | Berechnete Eingangsdrehzahl TG1 über Sollgang Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x609E | Berechnete Eingangsdrehzahl TG2 über Sollgang Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x609F | Status Modus DKG bezüglich Motoranforderung aus Ebene 1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60A0 | Drehmoment Fahrerwunsch Ebene 2 | Nm | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x60A1 | Gefilterte Eingangsdrehzahl TG1 Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x60A2 | Gefilterte Eingangsdrehzahl TG2 Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x60A3 | Motordrehzahl Ebene2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x60A4 | Erster gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x60A5 | Minimal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x60A6 | Maximal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x60A7 | Status HSD 0 | 0-n | High | 0xFF | QI_HSD | 1.0 | 1.0 | 0.0 |
| 0x60A8 | Status HSD 1 | 0-n | High | 0xFF | QI_HSD | 1.0 | 1.0 | 0.0 |
| 0x60A9 | Status HSD 2 | 0-n | High | 0xFF | QI_HSD | 1.0 | 1.0 | 0.0 |
| 0x60AA | Status D2 | 0-n | High | 0xFF | NVM_BLOCK_D2_STATUS | 1.0 | 1.0 | 0.0 |
| 0x60AB | akt. Kupplungsreferenzmoment | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x60AC | Istdruck Kupplung 1, Rohwert | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x60AD | Istdruck Kupplung 2, Rohwert | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x60AE | Ebene2s-Analyse | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60AF | Spannung Abspritzsensor | V | High | unsigned int | - | 1.0 | 310.0 | 0.0 |
| 0x60B0 | Hauptzustand KP-Einlernroutine | 0-n | High | 0xFF | ACT_GET_ZUST_ADAP_MAIN_ABBRUCH | 1.0 | 1.0 | 0.0 |
| 0x60B1 | Unterzustand KP-Einlernroutine | 0-n | High | 0xFF | ACT_GET_ZUST_ADAP_SUB_ABBRUCH | 1.0 | 1.0 | 0.0 |
| 0x60B2 | Ergebnis KP-Einlernroutine | 0-n | High | 0xFF | ACT_GET_ERGEBNIS_ABBRUCH | 1.0 | 1.0 | 0.0 |
| 0x60B3 | HS Diagnose Parksperrenmagnet | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60B4 | Widerstandswert Parksperrenmagnet | Ohm | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60B5 | HS-Dia-Startwert | Ohm | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60B6 | Widerstands Startwert | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x60BF | Fahrzeugstatus 1 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60C0 | Fahrzeugstatus 2 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60C1 | Status EWS Diag Info 0 | 0-n | High | 0xFF | EWS_DIAG_0 | 1.0 | 1.0 | 0.0 |
| 0x60C2 | Status EWS Diag Info 1 | 0-n | High | 0xFF | EWS_DIAG_1 | 1.0 | 1.0 | 0.0 |
| 0x60C3 | SOLLSTROM PV1 RESETFEST | A | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x60C4 | SOLLSTROM PV2 RESETFEST | A | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-gbx-err"></a>
### GBX_ERR

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Quellenfehler (passiv) |
| 1 | Unerlaubte Bewegung SST aus N |
| 2 | Unerlaubte Bewegung SST aus Gang |
| 3 | Timeout Neutral einregeln SST |
| 4 | Falsche Bewegungsrichtung SST |
| 5 | Einlegeproblem / -hängen |
| 6 | Auslegeproblem / -hängen |
| 7 | Schaltgabelbruch |
| 8 | Drehzahlfehler |
| 9 | Gangspringer |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | ja |
| F_UWB_SATZ | 2 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 31 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x40DD01 | Temperatur Kupplung: Phase Gelb | 0 | - |
| 0x40E804 | Adaption Kupplung 1:  untere Grenze verletzt | 0 | - |
| 0x40E808 | Adaption Kupplung 1:  obere Grenze verletzt | 0 | - |
| 0x40E904 | Adaption Kupplung 2:  untere Grenze verletzt | 0 | - |
| 0x40E908 | Adaption Kupplung 2:  obere Grenze verletzt | 0 | - |
| 0x40EA04 | Systemdruck falsch: untere Grenze verletzt | 0 | - |
| 0x40EA08 | Systemdruck falsch: obere Grenze verletzt | 0 | - |
| 0x40EF01 | Eingangsdrehzahl: Überdrehzahl | 0 | - |
| 0x40F801 | Schaltstange 1-3: Überhöhter Verschleiß Endlage | 0 | - |
| 0x40F802 | Schaltstange 2-R: Überhöhter Verschleiß Endlage | 0 | - |
| 0x40F804 | Schaltstange 5-7: Überhöhter Verschleiß Endlage | 0 | - |
| 0x40F808 | Schaltstange 6-4: Überhöhter Verschleiß Endlage | 0 | - |
| 0x40F901 | Schaltstange 1-3: Überhöhter Verschleiß Neutrallage | 0 | - |
| 0x40F902 | Schaltstange 2-R: Überhöhter Verschleiß Neutrallage | 0 | - |
| 0x40F904 | Schaltstange 5-7: Überhöhter Verschleiß Neutrallage | 0 | - |
| 0x40F908 | Schaltstange 6-4: Überhöhter Verschleiß Neutrallage | 0 | - |
| 0x411308 | DKG Getriebesteuerung: interner Fehler | 0 | - |
| 0x411D08 | DKG Getriebesteuerung: interner Fehler (EEPROM-Daten, Blöcke C-E) | 0 | - |
| 0x412108 | CAS: Keine Verlängerung Nachlaufzeit | 0 | - |
| 0x412201 | N-Haltephase: 20 min aktiv | 0 | - |
| 0x412A01 | Parksperre: Missbrauch | 0 | - |
| 0x412C01 | CAN-Notlauf: Angefordert | 0 | - |
| 0x412E08 | EWS: Manipulationsversuch | 0 | - |
| 0x413108 | SC CSM Modul | 1 | - |
| 0x413201 | DKG Getriebesteuerung: interner Fehler (Ebene 2, Debug Information) | 0 | - |
| 0xCF2101 | Botschaft (Status  Daten Antriebsstrang 2, 0x03F9) fehlt, Empfänger DKG, Sender Motorsteuerung | 1 | - |
| 0xCF2102 | Botschaft (Daten Antriebsstrang 2, 0x03F9) nicht aktuell, Empfänger DKG, Sender Motorsteuerung | 1 | - |
| 0xCF2104 | Botschaft (Daten Antriebsstrang 2, 0x03F9) Prüfsumme falsch, Empfänger DKG, Sender Motorsteuerung | 1 | - |
| 0xCF2108 | Botschaft (Daten Antriebsstrang 2, 0x03F9) Signal ungültig, Empfänger DKG, Sender Motorsteuerung | 1 | - |
| 0xCF2701 | Botschaft (Relativzeit, ID 0x328)  Timeout | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 64 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x6001 | Spannungsversorgung UBatt | V | High | unsigned int | - | 1.0 | 2048.0 | 0.0 |
| 0x6002 | Temperatur TCU | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6004 | Istgang Teilgetriebe 1 | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x6005 | Istgang Teilgetriebe 2 | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x600A | Fahrzeuggeschwindigkeit | km/h | High | signed int | - | 1.0 | 40.0 | 0.0 |
| 0x600B | Motordrehzahl | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600C | Getriebeeingangsdrehzahl 1 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600D | Getriebeeingangsdrehzahl 2 | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x600E | Getriebeausgangsdrehzahl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x6013 | Kombinierte Umweltgröße GBX (gepuffert) | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6017 | Sollstrom PV3 GBX (gepuffert) | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x6018 | Sollstrom PV4 GBX (gepuffert) | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x6021 | Nachadaptionswert Gang 1 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6022 | Nachadaptionswert Gang 2 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6023 | Nachadaptionswert Gang 3 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6024 | Nachadaptionswert Gang 4 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6025 | Nachadaptionswert Gang 5 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6026 | Nachadaptionswert Gang 6 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6027 | Nachadaptionswert Gang 7 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6028 | Nachadaptionswert Gang R | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x602E | Klemmenstatus KL15 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6037 | Motortemperatur | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6051 | Antriebsdrehzahl, Rohwert | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0x6052 | Nachadaptionswert Neutral SST 1/3 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6053 | Nachadaptionswert Neutral SST 2/R | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6054 | Nachadaptionswert Neutral SST 5/7 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x6055 | Nachadaptionswert Neutral SST 6/4 | mm | High | signed char | - | 1.0 | 40.0 | 0.0 |
| 0x605E | Ist-Strom PV7 | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x605F | Temperatur Abspritz-Öl | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6060 | Temperatur Sumpf-Öl | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x606D | logischer Getriebezustand | 0-n | High | 0xFF | DMA_Z_POS | 1.0 | 1.0 | 0.0 |
| 0x6070 | PS-Sensor 1 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6071 | PS-Sensor 2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6076 | Ausgabe Ebene 2 | 0-n | High | 0xFFFF | E2_OUTPUT_NOCLEAR | - | - | - |
| 0x6079 | Modelltemperatur K1 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x607A | Modelltemperatur K2 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x607E | Status A | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x607F | Status B | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6080 | Status C | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6081 | Status D | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6082 | Status E | 0-n | High | 0xFF | NVM_BLOCK_STATUS | 1.0 | 1.0 | 0.0 |
| 0x6088 | Abweichung zu erw. Systemdruck | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x6089 | erw. Systemdruck | bar | High | signed int | - | 1.0 | 100.0 | 0.0 |
| 0x608A | Adaptionsstrom Offset | A | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x60AA | Status D2 | 0-n | High | 0xFF | NVM_BLOCK_D2_STATUS | 1.0 | 1.0 | 0.0 |
| 0x60B7 | Status Motor fehlerhaft | 0-n | High | 0xFF | VBI_ERR_RCPT_ENG_EGS | 1.0 | 1.0 | 0.0 |
| 0x60B8 | CAN Notlauf Ursache | 0-n | High | 0xFF | DMA_CAN_NOTL_SOURCE | 1.0 | 1.0 | 0.0 |
| 0x60B9 | Ebene 2 Debug Flag | 0-n | High | 0xFFFF | E2_DBG_NOCLEAR | 1.0 | 1.0 | 0.0 |
| 0x60BA | Pfad Fahrerwunsch | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60BF | Fahrzeugstatus 1 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60C0 | Fahrzeugstatus 2 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60C1 | Status EWS Diag Info 0 | 0-n | High | 0xFF | EWS_DIAG_0 | 1.0 | 1.0 | 0.0 |
| 0x60C2 | Status EWS Diag Info 1 | 0-n | High | 0xFF | EWS_DIAG_1 | 1.0 | 1.0 | 0.0 |
| 0x60F5 | Umweltdatum 1 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60F6 | Umweltdatum 2 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60F7 | Umweltdatum 3 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60F8 | Umweltdatum 4 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60F9 | Umweltdatum 5 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60FA | Umweltdatum 6 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60FB | Umweltdatum 7 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60FC | Umweltdatum 8 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60FD | Umweltdatum 9 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x60FE | Umweltdatum 10 | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-lbc-cool-mode-des"></a>
### LBC_COOL_MODE_DES

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x05 | lbc_cs_max |
| 0x04 | lbc_cs_min |
| 0x03 | lbc_cs_off |
| 0x02 | lbc_pulse_max |
| 0x01 | lbc_pulse_min |
| 0x00 | lbc_pulse_temp |

<a id="table-nvm-block-d2-status"></a>
### NVM_BLOCK_D2_STATUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Checksumme i.O. |
| 2 | Checksumme nicht i.O. und Default Werte eingespielt |

<a id="table-nvm-block-status"></a>
### NVM_BLOCK_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Checksumme n.i.O. keine default Werte vorhanden |
| 0x01 | Checksumme i.O. |
| 0x02 | Checksumme n.i.O. default Werte eingespielt |

<a id="table-plm-pl-state"></a>
### PLM_PL_STATE

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x04 | PLM_pl_error |
| 0x09 | PLM_pl_init |
| 0x05 | PLM_pl_l_error |
| 0x00 | PLM_pl_locked |
| 0x02 | PLM_pl_locking |
| 0x07 | PLM_pl_pss_error |
| 0x08 | PLM_pl_service |
| 0x01 | PLM_pl_unlocked |
| 0x03 | PLM_pl_unlocking |
| 0x06 | PLM_pl_uul_error |

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

<a id="table-qi-hsd"></a>
### QI_HSD

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Fehler |
| 1 | Überstrom / Unterspannung |

<a id="table-qtemp-tcu"></a>
### QTEMP_TCU

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Untere elektrische Grenze unterschritten |
| 1 | Sensorwert OK |
| 2 | Obere elektrische Grenze überschritten |

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

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECUMehrmalsProgrammierbar |
| 1 | ECUMindestensEinmalVollstaendigProgrammierbar |
| 2 | ECUNichtMehrProgrammierbar |

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

<a id="table-res-0x1061-r"></a>
### RES_0X1061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_ENDE_WABL | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Verriegelt (loeschen von Einzelfehlern und PDTCs wird unterbunden) 1: Entriegelt (loeschen von Einzelfehlern und PDTCs wird nicht unterbunden) |

<a id="table-res-0x4600-d"></a>
### RES_0X4600_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROLLENBETRIEB_AKTIV | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0=inaktiv, 1=aktiv |
| STAT_RADABRISS_ABSCHALTUNG_AKTIV | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0=inaktiv, 1=aktiv |

<a id="table-res-0xae30-r"></a>
### RES_0XAE30_R

Dimensions: 7 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TESTPRG_IM_TEST_NR | + | - | + | 0-n | high | unsigned char | - | TAB_DKG_TEST_UND_EINLERNEN_PRG | 1.0 | 1.0 | 0.0 | Rückgabe welches Programm gestartet wurde |
| STAT_STATUS_TESTPRG_DEZIMAL | + | - | + | 0-n | high | unsigned char | - | TAB_DKG_STATUS_TEST_EINLERN | 1.0 | 1.0 | 0.0 | Während und nach dem Betrieb liefert das Steuergerät einen Status Wert zurück table  StatusTestEinlern |
| STAT_ZUSTAND_TESTPRG_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des Zustands Wert  des Test- und Einlernprogramm table InfoTextZustand ZUSTANDSNR ZUSTANDSTEXT |
| STAT_FEHLERMELDUNG_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des Fehlermeldungswert |
| STAT_MESS_WERT | - | - | + | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des Messwerts aus Test- und Einlernprogramm |
| STAT_MESS_1_WERT | - | - | + | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des Messwerts aus Test- und Einlernprogramm |
| STAT_MESS_2_WERT | - | - | + | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des Messwerts aus Test- und Einlernprogramm |

<a id="table-res-0xde30-d"></a>
### RES_0XDE30_D

Dimensions: 79 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Motordrezahl Bereich von 0 bis 15000 [1/min] |
| STAT_EINGANGSDREHZAHL1_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Getriebeeingangsdrehzahl 1 Bereich von 0 bis 15000 |
| STAT_EINGANGSDREHZAHL2_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Getriebeeingangsdrehzahl 2 Bereich von 0 bis 15000 |
| STAT_AUSGANGSDREHZAHL_WERT | 1/min | high | int | - | - | 1.0 | 2.0 | 0.0 | Getriebeausgangsdrehzahl Bereich von -10000 bis 10000 [1/min] |
| STAT_GESCHWINDIGKEIT_WERT | km/h | high | int | - | - | 1.0 | 40.0 | 0.0 | Fahrzeuggeschwindigkeit Bereich von -300 bis 400 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VL_WERT | km/h | high | int | - | - | 1.0 | 16.0 | 0.0 | Radgeschwindigkeit vorne links Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VR_WERT | km/h | high | int | - | - | 1.0 | 16.0 | 0.0 | Radgeschwindigkeit vorne rechts Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HL_WERT | km/h | high | int | - | - | 1.0 | 16.0 | 0.0 | Radgeschwindigkeit hinten links Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HR_WERT | km/h | high | int | - | - | 1.0 | 16.0 | 0.0 | Radgeschwindigkeit hinten rechts Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | km/h | high | int | - | - | 1.0 | 16.0 | 0.0 | Radgeschwindigkeit Hinterachse Bereich -320 bis 555 [km/h] |
| STAT_MOTORTEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Motortemperatur Bereich von -100  bis 300 [°C] |
| STAT_MOTOROELTEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Motoröltemperatur Bereich von -100 bis 300 [°C] |
| STAT_KUPPLUNGSOELTEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Ölsumpftemperatur Bereich von -100 bis 300 [°C] |
| STAT_SG_TEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | SG-Temperatur Bereich von -100 bis 300 [°C] |
| STAT_UMGEBUNGSTEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Umgebungstemperatur Bereich von -100 bis 300 [°C] |
| STAT_UBAT_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Spannungsversorgung U_Bat (Klemme 30) Bereich von 0 bis 31,9995 [V] |
| STAT_SPANNUNGSVERSORGUNG_7V4_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung 7V4_UH2 Spannungsbereich von 0 bis 31,9995 [V] Arbeitsbereich Min:6,6V  Default:7,4V Max:8,2V Spannungsversorgung für Drehzahlsensoren,Parksperrensensoren, Temperatursensoren und Schaltwippen |
| STAT_SENSORSPANNUNGSVERSORGUNG_VCC_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung 5V VCC Bereich von 0 bis 31,9995 [V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorung für Drucksensoren der Kupplung |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV1_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung SV 1 Bereich von 0 bis 31,9995 [V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorgung für Positionssensor der Schaltstange 1/3 und der Schaltstange 5/7 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV2_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung SV 2 Bereich von 0 bis 31,9995[V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorgung für Positionssensor der Schaltstange 6/4 und der Schaltstange 2/R |
| STAT_ISTSTROM_MAGNETVENTIL_PV1_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil Kupplung PV 1 Bereich von -3 bis 3 [A] PV1 steuert die Kupplung 1 |
| STAT_ISTSTROM_MAGNETVENTIL_PV2_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil Kupplung PV 2 Bereich von -3 bis 3 [A] PV2 steuert die Kupplung 2 |
| STAT_ISTSTROM_MAGNETVENTIL_PV3_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil PV 3 Bereich von -3 bis 3 [A] PV3 steuert die Schaltstangen |
| STAT_ISTSTROM_MAGNETVENTIL_PV4_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil PV4 Bereich von -3 bis 3 [A] PV4 steuert die Schaltstangen |
| STAT_ISTSTROM_MAGNETVENTIL_PV6_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil PV 6 Bereich von -3 bis 3 [A] PV6 steuert den Systemdruck |
| STAT_ISTSTROM_MAGNETVENTIL_PV7_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Iststrom Magnetventil PV7 Bereich von -3 bis 3 [A] PV7 steuert den Kühlölstrom für die Kupplungskühlung |
| STAT_SOLLSTROM_MAGNETVENTIL_PV1_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Sollstrom Magnetventil Kupplung PV 1 Bereich von -3 bis 3 [A] PV1 steuert die Kupplung 1 |
| STAT_SOLLSTROM_MAGNETVENTIL_PV2_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Sollstrom Magnetventil Kupplung PV 2 Bereich von -3 bis 3 [A] PV2 steuert die Kupplung 2 |
| STAT_SOLLSTROM_MAGNETVENTIL_PV3_WERT | mA | high | int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom Magnetventil PV 3 Bereich von 0 bis 3000 [mA] PV3 steuert die Schaltstangen |
| STAT_SOLLSTROM_MAGNETVENTIL_PV4_WERT | mA | high | int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom Magnetventil PV4 Bereich von 0 bis 3000 [mA] PV4 steuert die Schaltstangen |
| STAT_SOLLSTROM_MAGNETVENTIL_PV6_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Sollstrom Magnetventil PV 6 Bereich von -3 bis 3 [A] PV6 steuert den Systemdruck |
| STAT_SOLLSTROM_MAGNETVENTIL_PV7_WERT | A | high | int | - | - | 1.0 | 1000.0 | 0.0 | Sollstrom Magnetventil PV7 Bereich von -3 bis 3 [A] PV7 steuert den Kühlölstrom für die Kupplungskühlung |
| STAT_ISTDRUCK_KUPPLUNG1_WERT | bar | high | int | - | - | 1.0 | 100.0 | 0.0 | Istdruck Kupplung 1 Bereich von -5 bis 50 [bar] |
| STAT_ISTDRUCK_KUPPLUNG2_WERT | bar | high | int | - | - | 1.0 | 100.0 | 0.0 | Istdruck Kupplung 2 Bereich von -5 bis 50 [bar] |
| STAT_SOLLDRUCK_KUPPLUNG1_WERT | bar | high | int | - | - | 1.0 | 100.0 | 0.0 | Solldruck Kupplung 1 Bereich von -5 bis 50 [bar] |
| STAT_SOLLDRUCK_KUPPLUNG2_WERT | bar | high | int | - | - | 1.0 | 100.0 | 0.0 | Solldruck Kupplung 2 Bereich von -5 bis 50 [bar] |
| STAT_ISTMOMENT_KUPPLUNG1_WERT | Nm | high | int | - | - | 1.0 | 8.0 | 0.0 | Istmoment Kupplung 1 Bereich von -4000 bis 4000 [Nm] |
| STAT_ISTMOMENT_KUPPLUNG2_WERT | Nm | high | int | - | - | 1.0 | 8.0 | 0.0 | Istmoment Kupplung 2 Bereich von -4000 bis 4000 [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG1_WERT | Nm | high | int | - | - | 1.0 | 8.0 | 0.0 | Sollmoment Kupplung 1 Bereich von -4096 bis 4095,875 [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG2_WERT | Nm | high | int | - | - | 1.0 | 8.0 | 0.0 | Sollmoment Kupplung 2 Bereich von -4096 bis 4095,875 [Nm] |
| STAT_ISTPOSITION_SCHALTSTANGE_6_4_WERT | mm | high | int | - | - | 1.0 | 100.0 | 0.0 | Istposition Schaltstange 6/4 Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_5_7_WERT | mm | high | int | - | - | 1.0 | 100.0 | 0.0 | Istposition Schaltstange 5/7 Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_2_R_WERT | mm | high | int | - | - | 1.0 | 100.0 | 0.0 | Istposition Schaltstange 2/R Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_1_3_WERT | mm | high | int | - | - | 1.0 | 100.0 | 0.0 | Istposition Schaltstange 1/3 Bereich von -12 bis 12 [mm] |
| STAT_SOLLPOSITION_SCHALTSTANGE_6_4_NR | 0-n | high | unsigned char | - | TAB_DKG_SCHALTSTANGENPOSITION | 1.0 | 1.0 | 0.0 | Sollposition Schaltstange 6/4 table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_5_7_NR | 0-n | high | unsigned char | - | TAB_DKG_SCHALTSTANGENPOSITION | 1.0 | 1.0 | 0.0 | Sollposition Schaltstange 5/7 table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_2_R_NR | 0-n | high | unsigned char | - | TAB_DKG_SCHALTSTANGENPOSITION | 1.0 | 1.0 | 0.0 | Sollposition Schaltstange 2/R table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_1_3_NR | 0-n | high | unsigned char | - | TAB_DKG_SCHALTSTANGENPOSITION | 1.0 | 1.0 | 0.0 | Sollposition Schaltstange 1/3 table SchaltstangePosition WERT |
| STAT_FAHRPEDAL_WERT | % | high | unsigned char | - | - | 0.4 | 1.0 | 0.0 | Fahrpedalwert Bereich von 0 bis 102 [%] |
| STAT_MOTORISTMOMENT_WERT | A | high | int | - | - | 1.0 | 8.0 | 0.0 | Motor-Istmoment Bereich von -4000 bis 4000 [Nm] |
| STAT_AQUER_CAN_WERT | m/s² | high | int | - | - | 1.0 | 40.0 | 0.0 | Querbeschleunigung von CAN Bereich von -51,2 bis 51,2 [m_s^2] |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand von CAN Bereich von 0 bis 524280 [km] |
| STAT_HYDRAULIKDRUCK_WERT | bar | high | int | - | - | 1.0 | 100.0 | 0.0 | Systemdruck Bereich von -5 bis 50 [bar] |
| STAT_PARKSPERRE_AKTIV | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signal Parksperre an CAS: 0= nicht aktiv, 1= aktiv |
| STAT_PARKSPERRE_SENSOR1_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parksperrensenor  1 0= nicht aktiv, 1= aktiv |
| STAT_PARKSPERRE_SENSOR2_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parksperrensenor  2 / redundant 0= nicht aktiv, 1= aktiv |
| STAT_KL15_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | True (1) = Wake Up ist aktiv False (0) = Wake Up ist inaktiv |
| STAT_KUPPLUNG1_NR | 0-n | high | unsigned char | - | TAB_DKG_KUPPLUNGSSTATUS | 1.0 | 1.0 | 0.0 | Kupplungsstatus Kupplung 1 table KupplungsStati WERT |
| STAT_KUPPLUNG2_NR | 0-n | high | unsigned char | - | TAB_DKG_KUPPLUNGSSTATUS | 1.0 | 1.0 | 0.0 | Kupplungsstatus Kupplung 2 table KupplungsStati WERT |
| STAT_ISTGANG_NR | 0-n | high | unsigned char | - | TAB_DKG_GANGSTATUS | 1.0 | 1.0 | 0.0 | Istgang |
| STAT_SCHALTSTANGE_6_4_NR | 0-n | high | unsigned char | - | TAB_DKG_GETRIEBESTATUS | 1.0 | 1.0 | 0.0 | Getriebestatus SST6_4 table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_5_7_NR | 0-n | high | unsigned char | - | TAB_DKG_GETRIEBESTATUS | 1.0 | 1.0 | 0.0 | Getriebestatus SST5_7 table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_2_R_NR | 0-n | high | unsigned char | - | TAB_DKG_GETRIEBESTATUS | 1.0 | 1.0 | 0.0 | Getriebestatus SST2_R table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_1_3_NR | 0-n | high | unsigned char | - | TAB_DKG_GETRIEBESTATUS | 1.0 | 1.0 | 0.0 | Getriebestatus SST1_3 table GetriebeStatus WERT |
| STAT_GETRIEBEPOSITION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Getriebeposition Wert |
| STAT_OBD_STEUERFUNKTION | 0-n | high | unsigned char | - | TAB_DKG_OBDSTEUERFUNKTION | 1.0 | 1.0 | 0.0 | OBD Steuerfunktionen table OBD-Steuerfunktion WERT |
| STAT_SPORT_TASTER_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0 = Sportschalter inaktiv 1 = Sporttaster aktiv |
| STAT_PROGRAMMINFO_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 - 6 = Drive Logic Mode 1-6 7 - 12 = Rennstart Mode 1-6 129 - 131 = Drive Logic Mode 1-3 |
| STAT_GANGANZEIGE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0=Dunkel, 5=1.Gang, 6=2.Gang, 7=3.Gang usw. 15=Signal ungültig |
| STAT_WAEHLHEBELANZEIGE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0=Anzeige dunkel, 1=P, 2=R, 3=P_30sec, 4=N, 6=N_30,5min, 7=N_5min, 8=D, 15=ungültiges Signal |
| STAT_MIL_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0= Keine Anforderung 1= Anforderung MIL aus 2= Anforderung MIL ein 3= Signal ungültig |
| STAT_KL15_CAN_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | True (1) = Klemme 15 ein False (0) = Klemme 15 aus KL15 CAN |
| STAT_BREMSLICHTSCHALTER_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | True (1) = Bremse aktiv False (0) = Bremse inaktiv |
| STAT_ENDSTUFE_FEHLER | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | True(1)= Kein Fehler False(0)= Fehler liegt vor |
| STAT_ISTGANG_TEILGETRIEBE1_NR | 0-n | high | unsigned char | - | TAB_DKG_GANGSTATUS | 1.0 | 1.0 | 0.0 | Istgang für Teilgetriebe 1 Wert table GANGSTATUS WERT |
| STAT_ISTGANG_TEILGETRIEBE2_NR | 0-n | high | unsigned char | - | TAB_DKG_GANGSTATUS | 1.0 | 1.0 | 0.0 | Istgang für Teilgetriebe 2 Wert table IGANGSTATUS WERT |
| STAT_FESTSTELLBREMSE_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | True (1) = Bremse betätigt False (0) = Bremse nicht betätigt |
| STAT_SCHALTDIAGRAMM_AGS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Schaltdiagramm AGS |
| STAT_ANTRIEBSDREHZAHLSENSOR_WERT | - | high | int | - | - | 1.0 | 4.0 | 0.0 | Antriebsdrehzahlsensor Wert |

<a id="table-res-0xde31-d"></a>
### RES_0XDE31_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SG_TEMPERATUR_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | SG-Temperatur Bereich von -32768 bis 32767 [°C] |
| STAT_VERSORGUNGSSPANNUNGSSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Versorgungsspannungssensor Bereich von 0 bis 32 [V] |
| STAT_SENSORSPANNUNGSVERSORGUNG_VCC_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung 5V VCC Bereich von 0 bis 32 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV1_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung SV 1 Bereich von 0 bis 32 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV2_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung SV 2 Bereich von 0 bis 32 |
| STAT_SPANNUNGSVERSORGUNG_7SV4_WERT | V | high | unsigned int | - | - | 1.0 | 2048.0 | 0.0 | Sensorspannungsversorgung 7V SV4 Spannungsbereich von 0 bis 32 |
| STAT_ANTRIEBSDREHZAHLSENSOR_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Antriebsdrehzahlsensor Min: 0 Max: 16383,75 |
| STAT_EINGANGSDREHZAHLSENSOR_1_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Getriebeeingangsdrehzahlsensor 1 Min: 0 Max: 16383,75 |
| STAT_EINGANGSDREHZAHLSENSOR_2_WERT | 1/min | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Getriebeeingangsdrehzahlsensor 2 Min: 0 Max: 16383,75 |
| STAT_ABSPRITZTEMPERATURSENSOR_WERT | °C | high | unsigned int | - | - | 1.0 | 310.0 | 0.0 | Abspritztemperatursensor Min: 0 Max: 211,4 |
| STAT_TEMPERATURSENSOR_1_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Temperatursensor 1 Min: -32768 Max: 32767 |
| STAT_TEMPERATURSENSOR_2_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Temperatursensor 2 Min: -32768 Max: 32767 |
| STAT_DRUCKSENSOR_KUPPL_1_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | Drucksensor Kupplung 1 Min: -327,68 Max: -327,67 |
| STAT_DRUCKSENSOR_KUPPL_2_WERT | °C | high | int | - | - | 1.0 | 100.0 | 0.0 | Drucksensor Kupplung 2 Min: -327,68 Max: -327,67 |
| STAT_WEGSENSOR_SST_R_2_WERT | - | high | unsigned int | - | - | 1.0 | 204.8 | 0.0 | Wegsensor Schaltstange R/2 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_1_3_WERT | - | high | unsigned int | - | - | 1.0 | 204.8 | 0.0 | Wegsensor Schaltstange 1/3 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_6_4_WERT | - | high | unsigned int | - | - | 1.0 | 204.8 | 0.0 | Wegsensor Schaltstange 6/4 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_5_7_WERT | - | high | unsigned int | - | - | 1.0 | 204.8 | 0.0 | Wegsensor Schaltstange 5/7 Min: 0 Max: 320 |
| STAT_PARKSPERRENSENSOR_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parksperrensensor 1 Min: 0 Max: 255 |
| STAT_PARKSPERRENSENSOR_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parksperrensensor 1 Min: 0 Max: 255 |

<a id="table-res-0xde32-d"></a>
### RES_0XDE32_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GETRIEBE_INIT | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlernvorgang Getriebe komplett: 0= nicht eingelernt, 1= eingelernt |
| STAT_KUPPLUNGSSCHLEIFPUNKT1_INIT | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlernvorgang Kupplungsschleifpunkt 1: 0= nicht eingelernt, 1= eingelernt |
| STAT_KUPPLUNGSSCHLEIFPUNKT2_INIT | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlernvorgang Kupplungsschleifpunkt 1: 0= nicht eingelernt, 1= eingelernt |

<a id="table-res-0xde33-d"></a>
### RES_0XDE33_D

Dimensions: 82 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IGNITION_CYCLE_COUNTER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_GENERAL_DENOMINATOR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_9_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_9_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_10_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_10_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_11_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_11_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_12_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_12_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_13_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_13_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_14_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_14_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_15_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_15_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_16_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_16_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_17_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_17_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_18_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_18_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_19_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_19_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_21_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_21_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_22_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_22_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_23_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_23_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_24_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_24_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_25_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_25_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_26_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_26_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_27_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_27_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_28_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_28_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_29_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_29_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_30_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_30_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_31_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_31_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_32_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_32_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_33_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_33_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_34_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_34_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_35_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_35_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_36_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_36_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_37_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_37_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_38_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_38_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_39_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_39_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_40_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_40_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Werte bis 65534 |

<a id="table-res-0xde34-d"></a>
### RES_0XDE34_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STELLGLIED_IO_NR | 0-n | high | unsigned char | - | TAB_DKG_IO_SETZEN | 1.0 | 1.0 | 0.0 | Stellglied, welches angesteuert wird. Siehe Tabelle |
| STAT_RUECKGABESTATUS_NR | 0-n | high | unsigned char | - | TAB_DKG_RUECKGABESTATUS | 1.0 | 1.0 | 0.0 | Rückgabestatus |
| STAT_STELLGLIED_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert, den das Stellglied angenommen hat.  Interpretation des Rückgabewertes wird Offline gemäß dem angehängten Dokument durchgeführt |

<a id="table-res-0xde40-d"></a>
### RES_0XDE40_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kupplungsschleifpunkt der im EOL ermittelt wurde Min: -327 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Schleifpunkt, der in der Werkstatt ermittelt wurde (beim Nachlernen z.B. nach Kupplungstausch) Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Schleifpunkt nach 10 Adaptionsschritten Kisspoint K1 3.Wert Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Für die Funktion relevante Kupplungsschleifpunkt (aktuell gefahrener Schleifpunkt) Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kleinster durch Adaption ermittelter Schleifpunkt Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Größter durch Adaption ermittelter Schleifpunkt Min: -327 Default:1,8 Max: 327 |

<a id="table-res-0xde41-d"></a>
### RES_0XDE41_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kupplungsschleifpunkt,der am EOL ermittelt wurde Min: -327 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kupplungsschleifpunkt, der in der Werkstatt ermittelt wurde (beim Nachlernen z.B. nach Kupplungstausch) Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kupplungsschleifpunkt nach 10 Adaptionsschritten Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Für die Funktion relevante Kupplungsschleifpunkt (aktuell gefahrener Kupplungsschleifpunkt) Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Kleinster durch Adaption ermittelter Kupplungsschleifpunkt Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Größter durch Adaption ermittelter Kupplungsschleifpunkt Min: -327 Default: 1,85 Max: 327 |

<a id="table-res-0xde42-d"></a>
### RES_0XDE42_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K1 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K3 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K4 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K5 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K6 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_7_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K7 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_8_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K8 Min: -12.29 Default: 1 Max: 12.29 |

<a id="table-res-0xde43-d"></a>
### RES_0XDE43_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K3 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K4 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K5 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K6 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_7_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K7 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_8_WERT | - | high | int | - | - | 1.0 | 2666.7 | 0.0 | Adaptionswerte Kupplungsmomentenkennlinie K8 Min: -12.29 Default: 1 Max: 12.29 |

<a id="table-res-0xde44-d"></a>
### RES_0XDE44_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADAPTION_GETRIEBECODE_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 1 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 2 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 3 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 4 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 5 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 6 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 7 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_8_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 8 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_9_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 9 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_10_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswerte für den Getriebecode Wert 10 Min: 0 Max: 255 |

<a id="table-res-0xde49-d"></a>
### RES_0XDE49_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADAPTION_VENTILKENNLINIE_PV1_WERT | - | high | char | - | - | 1.0 | 128.0 | 0.0 | Adaptionswert für PV1 Ventilkennlinie |
| STAT_ADAPTION_VENTILKENNLINIE_PV2_WERT | - | high | char | - | - | 1.0 | 128.0 | 0.0 | Adaptionswert für PV2 Ventilkennlinie |

<a id="table-res-0xde4a-d"></a>
### RES_0XDE4A_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_0_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 0) Min: -5 Max: 30 |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 1) Min: -5 Max: 30 |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 2) Min: -5 Max: 30 |

<a id="table-res-0xde4c-d"></a>
### RES_0XDE4C_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_1_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 1. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_2_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 2. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_3_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 3. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_4_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 4. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_5_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 5. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_6_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 6. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_7_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Adaptionswert des Semischlupfs für den 7. Gang Min: -120 Max: 120 |

<a id="table-res-0xde50-d"></a>
### RES_0XDE50_D

Dimensions: 62 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAHRZEUGTYP | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0 = AG Fahrzeug, 1 = M Fahrzeug |
| STAT_ANZ_LOESCHUNGEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Löschungen von Verschleißdaten |
| STAT_KM_STAND_LETZTER_LOESCHUNG_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand der letzten Löschung der Verschleißdaten |
| STAT_ANZ_RENNSTARTS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Rennstarts |
| STAT_ANZ_SCHALTUNG_GANG_1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 1 |
| STAT_ANZ_SCHALTUNG_GANG_2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 2 |
| STAT_ANZ_SCHALTUNG_GANG_3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 3 |
| STAT_ANZ_SCHALTUNG_GANG_4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 4 |
| STAT_ANZ_SCHALTUNG_GANG_5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 5 |
| STAT_ANZ_SCHALTUNG_GANG_6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 6 |
| STAT_ANZ_SCHALTUNG_GANG_7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang 7 |
| STAT_ANZ_SCHALTUNG_GANG_R_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der ausgeführten Schaltungen: Gang R |
| STAT_ANZ_SMOKIE_BURNOUTS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Smokie Burnouts |
| STAT_ANZ_EINLEGEHAENGER_GANG_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 1. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 2. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 3. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 4. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 5. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 6. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den 7. Gang |
| STAT_ANZ_EINLEGEHAENGER_GANG_R_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Einlegehänger für den Rückwärtsgang |
| STAT_AUFENTHALTSDAUER_OELSUMPF_KLEINER_MINUS_30_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich &lt; -30°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_MINUS_30_BIS_MINUS_20_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -30 bis -20°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_MINUS_20_BIS_MINUS_10_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -20 bis -10°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_MINUS_10_BIS_0_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -10 bis 0°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_0_BIS_10_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 0 bis 10°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_10_BIS_20_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 10 bis 20°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_20_BIS_30_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 20 bis 30°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_30_BIS_40_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 30 bis 40°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_40_BIS_50_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 40 bis 50°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_50_BIS_60_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 50 bis 60°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_60_BIS_70_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 60 bis 70°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_70_BIS_80_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 70 bis 80°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_80_BIS_90_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 80 bis 90°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_90_BIS_100_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 90 bis 100°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_100_BIS_110_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 100 bis 110°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_110_BIS_120_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 110 bis 120°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_120_BIS_130_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 120 bis 130°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_130_BIS_140_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 130 bis 140°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_140_BIS_150_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 140 bis 150°C, Zeit in Minuten |
| STAT_AUFENTHALTSDAUER_OELSUMPF_150_BIS_160_GRAD_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 150 bis 160°C, Zeit in Minuten |
| STAT_ANZ_FAHRSTUFE_ANFORDERN_OHNE_BREMSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrstufe anfordern ohne Bremse |
| STAT_ANZ_R_GANG_ANFORDERN_UEBER_V_SCHWELLE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | R-Gang anfordern bei Geschwindigkeit  größer Schwelle |
| STAT_ANZ_AUTO_P_FAHRZEUGVERLASSEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Auto-P bei Fahrzeugverlassen |
| STAT_ANZ_P_ANFORDERN_V_UEBER_SCHWELLE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | P anfordern bei Geschwindigkeit größer Schwelle |
| STAT_KUPPLUNGSTEMPERATUR_K1_MAX_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Maximale Temperatur Kupplung 1 |
| STAT_ANZ_K1_MAX_TEMPERATUR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler max. Kupplungstemperatur K1 ( 320ms Ticks ) |
| STAT_KUPPLUNGSTEMPERATUR_K2_MAX_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Maximale Temperatur Kupplung 2 |
| STAT_ANZ_K2_MAX_TEMPERATUR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler max. Kupplungstemperatur K2 ( 320ms Ticks ) |
| STAT_ABSPRITZSSENSORTEMPERATUR_MAX_WERT | °C | high | int | - | - | 1.0 | 1.0 | 0.0 | Maximale Temperatur des Abspritzsensors |
| STAT_ANZ_MAX_TEMPERATUR_ABSPRITZSENSOR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler max. Temperatur Abspritzsensor ( 320ms Ticks ) |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell Normal (E9x) BMW AG Fahrzeug Modi - Manuell / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 1 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Manuell / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 2 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi:3 BMW AG Fahrzeug Modi - Automatik Normal (E9x) BMW AG Fahrzeug Modi - D-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 3 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Automatik (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - D-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 4 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse Normal (E9x) BMW AG Fahrzeug Modi - S-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 5 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - S-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 6 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_7_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell Normal (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Komfort (E89) M3 Fahrzeug Modi - Automatik Stufe 1 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_8_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Sport (E89) M3 Fahrzeug Modi - Automatik 2 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_9_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 3 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_10_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - D-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 4 Wert in Sekunden |
| STAT_AUFENTHALTSDAUER_FAHRMODUS_11_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - S-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 5 Wert in Sekunden |

<a id="table-res-0xde51-d"></a>
### RES_0XDE51_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZ_ZAEHLER_0_PV6_ADAPTIONEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 0) |
| STAT_ANZ_ZAEHLER_1_PV6_ADAPTIONEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 1) |
| STAT_ANZ_ZAEHLER_2_PV6_ADAPTIONEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 2) |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Erfolgszähler für durchgeführte Kisspointadationen Kupplung 1 |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Erfolgszähler für durchgeführte Kisspointadationen Kupplung 2 |
| STAT_KILOMETERSTAND_LETZTER_K1_ADAPTION_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K1 |
| STAT_KILOMETERSTAND_LETZTER_K2_ADAPTION_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K2 |
| STAT_KISSPOINT_K1_MIN_WERT | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Min. adaptierter Kisspoint K1 |
| STAT_KISSPOINT_K2_MIN_WERT | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Min. adaptierter Kisspoint K2 |
| STAT_KILOMETERSTAND_K1_MIN_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand der Min. Kisspointadaption Kupplung 1 |
| STAT_KILOMETERSTAND_K2_MIN_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand der Min. Kisspointadaption Kupplung 2 |
| STAT_KISSPOINT_K1_MAX_WERT | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Max. adaptierter Kisspoint K1 |
| STAT_KISSPOINT_K2_MAX_WERT | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Max. adaptierter Kisspoint K2 |
| STAT_KILOMETERSTAND_K1_MAX_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand der Max. Kisspointadaption Kupplung 1 |
| STAT_KILOMETERSTAND_K2_MAX_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand der Max. Kisspointadaption Kupplung 2 |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_MAX50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 Max 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_MIN50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 Min 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_MAX300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 Max 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_MIN300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 Min 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_MAX50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 Max 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_MIN50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 Min 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_MAX300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 Max 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_MIN300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 Min 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_300_BEI_MAX50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 akt.Wert 300Nm bei Max 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_300_BEI_MIN50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 akt.Wert 300Nm bei Min 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_50_BEI_MAX300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 akt.Wert 50Nm bei Max 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K1_50_BEI_MIN300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K1 akt.Wert 50Nm bei Min 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_300_BEI_MAX50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 akt.Wert 300Nm bei Max 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_300_BEI_MIN50_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 akt.Wert 300Nm bei Min 50Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_50_BEI_MAX300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 akt.Wert 50Nm bei Max 300Nm |
| STAT_KUPPLUNGSADAPTIONSKENNLINIE_K2_50_BEI_MIN300_WERT | - | high | char | - | - | 1.0 | 1.0 | 0.0 | Kupplungsadaptionskennlinie K2 akt.Wert 50Nm bei Min 300Nm |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_50NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 1 Adaptionszähler 50Nm |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_75NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 1 Adaptionszähler 75Nm |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_125NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 1 Adaptionszähler 125Nm |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_200NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 1 Adaptionszähler 200Nm |
| STAT_ANZ_ZAEHLER_K1_ADAPTIONEN_300NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 1 Adaptionszähler 300Nm |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_50NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 2 Adaptionszähler 50Nm |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_75NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 2 Adaptionszähler 75Nm |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_125NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 2 Adaptionszähler 125Nm |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_200NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 2 Adaptionszähler 200Nm |
| STAT_ANZ_ZAEHLER_K2_ADAPTIONEN_300NM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kupplung 2 Adaptionszähler 300Nm |

<a id="table-res-0xde52-d"></a>
### RES_0XDE52_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_7_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_8_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_9_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_10_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_11_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_12_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_13_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_14_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_15_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_16_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |

<a id="table-res-0xde53-d"></a>
### RES_0XDE53_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_7_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_8_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_9_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_10_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_11_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_12_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_13_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_14_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_15_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_16_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |

<a id="table-res-0xde54-d"></a>
### RES_0XDE54_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_1_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_2_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_3_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_4_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_5_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_6_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_7_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_8_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_9_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_10_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_11_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_12_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_13_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_14_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_15_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_16_WERT | - | high | int | - | - | 1.0 | 100.0 | 0.0 | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |

<a id="table-res-0xde5a-d"></a>
### RES_0XDE5A_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_0_WERT | - | high | unsigned int | - | - | 1.0 | 8192.0 | 0.0 | Faktor der Amplitude tin_amp_[0] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_1_WERT | - | high | unsigned int | - | - | 1.0 | 8192.0 | 0.0 | Faktor der Amplitude tin_amp_[1] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_2_WERT | - | high | unsigned int | - | - | 1.0 | 8192.0 | 0.0 | Faktor der Amplitude tin_amp_[2] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_3_WERT | - | high | unsigned int | - | - | 1.0 | 8192.0 | 0.0 | Faktor der Amplitude tin_amp_[3] Min: 0 Default: tbd  Max: 8 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P0_WERT | - | high | int | - | - | 1.0 | 8192.0 | 0.0 | Verschiebung der Kennlinie tin_p[0] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P1_WERT | - | high | int | - | - | 1.0 | 8192.0 | 0.0 | Verschiebung der Kennlinie tin_p[1] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P2_WERT | - | high | int | - | - | 1.0 | 8192.0 | 0.0 | Verschiebung der Kennlinie tin_p[2] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P3_WERT | - | high | int | - | - | 1.0 | 8192.0 | 0.0 | Verschiebung der Kennlinie tin_p[3] Min: -4 Default: tbd  Max: 4 |
| STAT_NACHADAPTION_GANG_1_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 1. Gang |
| STAT_NACHADAPTION_GANG_2_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 2. Gang |
| STAT_NACHADAPTION_GANG_3_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 3. Gang |
| STAT_NACHADAPTION_GANG_4_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 4. Gang |
| STAT_NACHADAPTION_GANG_5_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 5. Gang |
| STAT_NACHADAPTION_GANG_6_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 6. Gang |
| STAT_NACHADAPTION_GANG_7_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert 7. Gang |
| STAT_NACHADAPTION_GANG_R_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert R-Gang |
| STAT_NACHADAPTION_NEUTRAL_SST_1_3_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert Neutral SST 1/3 |
| STAT_NACHADAPTION_NEUTRAL_SST_2_R_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert Neutral SST 2/R |
| STAT_NACHADAPTION_NEUTRAL_SST_5_7_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert Neutral SST 5/7 |
| STAT_NACHADAPTION_NEUTRAL_SST_6_4_WERT | - | high | char | - | - | 1.0 | 40.0 | 0.0 | Nachadaptionswert Neutral SST 6/4 |

<a id="table-res-0xf770-r"></a>
### RES_0XF770_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BLOCK_WERT | + | - | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0:NVM_REQ_OK 1: NVM_REQ_NOT_OK 4: NVM_REQ_INTEGRITY_FAILED 6: NVM_REQ_NV_INVALID 7: NVM_REQ_NV_BLANK |

<a id="table-res-0xf771-r"></a>
### RES_0XF771_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BLOCKCONTENT_WERT | + | - | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Inhalt |

<a id="table-scm-err-flg-hi"></a>
### SCM_ERR_FLG_HI

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0001 | Non maskable interrupt |
| 0x0002 | RAM-Test |
| 0x0000 | No Error |

<a id="table-scm-err-flg-lo"></a>
### SCM_ERR_FLG_LO

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0001 | unknown-fault |
| 0x0002 | shutdown by FSW |
| 0x0004 | SCM_CCP_FLASH |
| 0x0008 | ECC single-bit |
| 0x0010 | Level 3 monitoring |
| 0x0020 | Trap X3 |
| 0x0040 | Parity Error RAM |
| 0x0080 | Reset by external hardware |
| 0x0100 | AD-Converter fail |
| 0x0200 | Watchdog |
| 0x0400 | PCP |
| 0x0800 | Trap X2 |
| 0x1000 | ECC double-bit |
| 0x2000 | Program flow |
| 0x4000 | Abschaltpfad |
| 0x8000 | Trap X1 |
| 0x0000 | No Error |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 46 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FS_LOESCHEN_PERMANENT | 0x1060 | - | Job zum Löschen der Permanent-DTCs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FEHLERSPEICHER_ENDE_WERKSABLAUF | 0x1061 | - | Löschen von Einzelfehlern und Permanent-DTCs unterbindet | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x1061_R |
| DKG_TEST_PROGRAMM | 0xAE30 | - | Testprogramm für Doppelkupplungsgetriebe | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAE30_R | RES_0xAE30_R |
| DKG_ISTWERTE | 0xDE30 | - | Ist-Werte Doppelkupplungsgetriebe | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE30_D |
| DKG_ROHWERTE | 0xDE31 | - | Rohwerte Doppelkupplungsgetriebe | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE31_D |
| DKG_INITALISIERUNG | 0xDE32 | - | Initialisierung Doppelkupplungsgetriebe | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE32_D |
| DKG_RBM_RATIO | 0xDE33 | - | Text | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE33_D |
| DKG_STELLGLIED_STEUERN | 0xDE34 | - | Steuert die Stellglieder im DKG an | - | - | - | - | - | - | - | - | - | 2F | ARG_0xDE34_D | RES_0xDE34_D |
| DKG_ADAPTIONSWERTE_ZURUECKSETZEN | 0xDE36 | - | Adaptionswerte in DKG zurücksetzen | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDE36_D | - |
| DKG_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K1 | 0xDE40 | - | Adaptionswert Kupplungsschleifpunkt K1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE40_D |
| DKG_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K2 | 0xDE41 | - | Adaptionswert Kupplungsschleifpunkt K2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE41_D |
| DKG_ADAPTION_MOMENTENKENNLINIE_K1 | 0xDE42 | - | Adaptionswert Momentenkennlinie K1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE42_D |
| DKG_ADAPTION_MOMENTENKENNLINIE_K2 | 0xDE43 | - | Adaptionswert Momentenkennlinie K2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE43_D |
| DKG_ADAPTIONSWERT_GETRIEBECODE | 0xDE44 | - | Adaptionswert Getriebecode | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE44_D |
| DKG_ADAPTIONSWERT_HYDRAULIKPUMPE | 0xDE45 | STAT_ADAPTION_HYDRAULIKPUMPE_WERT | Job: Adaptionswert Hydraulikpumpe Result: Adaptionswert für die Hydraulikpumpe Min: 0 Max: 255 | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_ADAPTIONSWERT_RADSATZVARIANTE | 0xDE46 | STAT_ADAPTION_RADSATZVARIANTE_WERT | Job: Adaptionswert Radsatzvariante Result: Adaptionswert für die Radsatzvariante Min: 0 Max: 255 | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_ADAPTIONSWERT_TEMPERATURSENSOR | 0xDE47 | STAT_ADAPTION_TEMPERATURSENSOR_WERT | Job: Adaptionswert Temperatursensor Result: Adaptionswert für den Temperatursensor Abspritzöl (Typ) Min: 0 Max: 2 | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND | 0xDE48 | STAT_ADAPTION_TEMPERATURSENSOR_WIDERSTAND_WERT | Job: Adaptionswert Widerstand Temperatursensor Result: Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert Min: 0 Max: 65535 | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_ADAPTIONSWERT_VENTILKENNLINIE_PV1_PV2 | 0xDE49 | - | Adaptionswert Ventilkennlinie PV1 und PV2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE49_D |
| DKG_ADAPTIONSWERT_PV6 | 0xDE4A | - | Adaptionswert PV6 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE4A_D |
| DKG_ADAPTIONSWERTE_DRM | 0xDE4B | STAT_DRM_HEX_DATA | Job: Adaptionswerte DRM Result: Adaptionswerte des DRM | DATA | - | high | data[242] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_ADAPTIONSWERTE_SEMISCHLUPF_GAENGE | 0xDE4C | - | Adaptionswerte Semischlupf Gänge | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE4C_D |
| DKG_STATISTIKDATENSATZ_1 | 0xDE50 | - | Statistikdatensatz 1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE50_D |
| DKG_STATISTIKDATENSATZ_2 | 0xDE51 | - | Statistikdatensatz 2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE51_D |
| DKG_VENTILKENNLINIE_PV1 | 0xDE52 | - | Ventilkennlinie PV1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE52_D |
| DKG_VENTILKENNLINIE_PV2 | 0xDE53 | - | Ventilkennlinie PV2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE53_D |
| DKG_VENTILKENNLINIE_PV6 | 0xDE54 | - | Ventilkennlinie PV6 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE54_D |
| DKG_SPERRSTELLUNG_PV7 | 0xDE55 | STAT_PV7_SPERRVENTIL_WERT | Job: Sperrstellung PV7 Result: Adaptionswerte Sperrventil Wert Min: 0 Max: 65535 | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DKG_GETRIEBE_TEACHEN | 0xDE5A | - | Getriebe teachen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE5A_D |
| _DKG_STATISTIKDATEN_LOESCHEN | 0x4100 | - | Statistikdaten löschen DKG | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4100_D | - |
| _DKG_ADAPTIONSWERTE_PV1 | 0x42A4 | - | Adaptionswert für PV1 | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42A4_D | - |
| _DKG_ADAPTIONSWERTE_PV2 | 0x42A5 | - | Adaptionswert für PV2 | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42A5_D | - |
| _DKG_ADAPTIONSWERTE_PV6 | 0x42A6 | - | Adaptionswert für PV6 | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42A6_D | - |
| _DKG_ADAPTIONSWERTE_PV7 | 0x42A7 | - | Adaptionswert für PV7 | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42A7_D | - |
| _DKG_GETRIEBECODE | 0x42AB | - | Getriebecode DKG | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42AB_D | - |
| _DKG_ADAPTIONSWERT_RADSATZVARIANTE | 0x42AC | - | Adaptionswert für Radsatzvariante DKG | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42AC_D | - |
| _DKG_ADAPTIONSWERT_HYDRAULIKPUMPE | 0x42AD | - | Adaptionswert für Hydraulikpumpe DKG | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42AD_D | - |
| _DKG_ADAPTIONSWERT_TEMPERATURSENSOR | 0x42AE | - | Adaptionswert für Temperatursensor | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42AE_D | - |
| _DKG_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND | 0x42AF | - | Adaptionswert für Widerstand Temperatursensor | - | - | - | - | - | - | - | - | - | 2E | ARG_0x42AF_D | - |
| _DKG_PRODUKTIONSDATEN_HYBRID | 0x42B0 | STAT_DKG_PRODUKTIONSDATEN_HYBRID_WERT | Job: DKG_PRODUKTIONSDATEN_HYBRID; Service-ID 0x22; Ergebnis 128 Bytes als Hex-Dump Result: DKG_PRODUKTIONSDATEN_HYBRID | - | - | high | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _DKG_PRODUKTIONSDATEN_FIN | 0x42B1 | STAT_DKG_PRODUKTIONSDATEN_FIN_WERT | Job: DKG_PRODUKTIONSDATEN_FIN; Service-ID 0x22; Ergebnis 128 Bytes als Hex-Dump Result: DKG_PRODUKTIONSDATEN_FIN | - | - | high | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _DKG_NOCLEAR_DATEN | 0x42B2 | STAT_DKG_NOCLEAR_DATEN_WERT | Job: DKG_NOCLEAR_DATEN; Service-ID 0x22; Ergebnis 48 Bytes als Hex-Dump Result: DKG_NOCLEAR_DATEN | - | - | high | data[48] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _DKG_SOFTWARE_VERSION | 0x42B3 | STAT_DKG_SOFTWARE_VERSION_WERT | Job: DKG_SOFTWARE_VERSION; Service-ID 0x22; Ergebnis 2 Bytes als unsigned Char Result: DKG_SOFTWARE_VERSION | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _DKG_CODIERDATEN | 0x4600 | - | Codierdaten DKG | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x4600_D | RES_0x4600_D |
| _RID_F770 | 0xF770 | - | RID F770 | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF770_R | RES_0xF770_R |
| _RID_F771 | 0xF771 | - | RID F771 | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF771_R | RES_0xF771_R |

<a id="table-signal-status"></a>
### SIGNAL_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | SignalNotValid |
| 0x01 | SignalSubstitudeValue |
| 0x00 | SignalValid |

<a id="table-svk-version-dop"></a>
### SVK_VERSION_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | SVKVersion_01 |

<a id="table-tab-dkg-gangstatus"></a>
### TAB_DKG_GANGSTATUS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Neutral |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | 7. Gang |
| 0x0E | Rueckwärtsgang |
| 0x0F | Undefiniert |

<a id="table-tab-dkg-getriebestatus"></a>
### TAB_DKG_GETRIEBESTATUS

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Status undefiniert |
| 0x01 | Status Neutral |
| 0x02 | Status Gang geschaltet oben |
| 0x03 | Status Gang geschaltet unten |
| 0x04 | Status Vorsynchron fahren oben |
| 0x05 | Status Vorsynchron fahren unten |
| 0x06 | Status Synchronisieren oben |
| 0x07 | Status Synchronisieren unten |
| 0x08 | Status Durchschalten oben |
| 0x09 | Status Durchschalten unten |
| 0x0A | Status Gang nachdrücken oben |
| 0x0B | Status Gang nachdrücken unten |
| 0x0C | Status Vorspannen oben |
| 0x0D | Status Vorspannen unten |
| 0x0E | Status Vorspannen abbrechen oben |
| 0x0F | Status Vorspannen abbrechen unten |
| 0x10 | Status Gang auslegen oben |
| 0x11 | Status Gang auslegen unten |
| 0x12 | Status Neutral überschieben oben |
| 0x13 | Status Neutral überschieben unten |
| 0x14 | Status Neutral einregeln oben |
| 0x15 | Status Neutral einregeln unten |
| 0xFF | Undefiniert |

<a id="table-tab-dkg-io-setzen"></a>
### TAB_DKG_IO_SETZEN

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | SOLLSTROM MAGNETVENTIL PV1 |
| 0x21 | SOLLSTROM MAGNETVENTIL PV2 |
| 0x22 | SOLLSTROM MAGNETVENTIL PV3 |
| 0x23 | SOLLSTROM MAGNETVENTIL PV4 |
| 0x24 | SOLLSTROM MAGNETVENTIL PV6 |
| 0x25 | SOLLSTROM MAGNETVENTIL PV7 |
| 0x26 | SOLLZUSTAND MAGNETVENTIL SV1 |
| 0x27 | SOLLZUSTAND MAGNETVENTIL SV2 |
| 0x28 | SOLLZUSTAND MAGNETVENTIL SV3 |
| 0x29 | SOLLZUSTAND MAGNETVENTIL SV4 |
| 0x2A | PARKSPERRE_VERRIEGELN |
| 0x2B | ANZEIGE_PROGRAMMINFORMATION |
| 0x2C | GETRIEBE NACH NEUTRAL STELLEN |
| 0x2D | PARKSPERRE HAKENTEST |
| 0x2E | PARKSPERRE MAGNETTEST |
| 0x2F | ANSTEUERUNG PARKSPERRE AUS/EIN |
| 0x30 | ANZEIGE WAHLHEBELSCHEMA |
| 0x31 | ANZEIGE GAENGE |
| 0x32 | ANZEIGE CC MELDUNG |
| 0xFE | ALLE AUSGANGSGRÖSSEN |

<a id="table-tab-dkg-kupplungsstatus"></a>
### TAB_DKG_KUPPLUNGSSTATUS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierungswert |
| 0x01 | Kupplung offen |
| 0x02 | Kupplung überträgt Moment |
| 0x03 | Erstbefüllung nach Reset |
| 0x04 | Zustand nach Initialisierung |
| 0x05 | Kupplung entleeren oder Füllen. Überstandszustand zwischen 2 nach 1 oder umgekehrt. |
| 0x06 | Kupplungs-PVs reagieren auf Anforderungen aus dem Parksperrenmodul |
| 0x07 | Kupplung kann innerhalb bestimmter Zeit nicht gefüllt werden. Reset durch Wechsel nach Disengaged. |
| 0x08 | Kupplungszweig gesperrt |
| 0xFF | Undefiniert |

<a id="table-tab-dkg-obdsteuerfunktion"></a>
### TAB_DKG_OBDSTEUERFUNKTION

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Warm Up Cycle erfüllt - kein Freeze-Frame im Master gespeichert |
| 0x02 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - kein Freeze-Frame im Master gespeichert |
| 0x03 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - kein Freeze-Frame im Master gespeichert |
| 0x09 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: DME (Master) |
| 0x0A | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME (Master) |
| 0x0B | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME (Master) |
| 0x11 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: EGS |
| 0x12 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EGS |
| 0x13 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EGS |
| 0x21 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: EKP |
| 0x22 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EKP |
| 0x23 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EKP |
| 0x31 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für:DME links |
| 0x32 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME links |
| 0x33 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME links |
| 0xFF | Signal ungültig |

<a id="table-tab-dkg-rueckgabestatus"></a>
### TAB_DKG_RUECKGABESTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Ansteuerwert nicht definiert |
| 0x02 | Ansteuerbedingung nicht erfüllt |
| 0x03 | Ansteuerwert nicht im vorgegebenen Bereich |

<a id="table-tab-dkg-schaltstangenposition"></a>
### TAB_DKG_SCHALTSTANGENPOSITION

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Position undefiniert |
| 0x01 | Position Neutral |
| 0x02 | Position oben |
| 0x03 | Position unten |
| 0x04 | Position Synchron oben |
| 0x05 | Position Synchron unten |
| 0x06 | Position vor Synchron oben |
| 0x07 | Position vor Synchron unten |
| 0x08 | Position nach Synchron oben |
| 0x09 | Position nach Synchron unten |
| 0xFF | Undefiniert |

<a id="table-tab-dkg-status-test-einlern"></a>
### TAB_DKG_STATUS_TEST_EINLERN

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Testbedingungen nicht erfüllt |
| 0x01 | Testprogramm läuft |
| 0x02 | Testprogramm beendet |
| 0x03 | Testprogramm nicht ordnungsgemäß beendet |
| 0x04 | Testprogramm abgebrochen |
| 0xFF | Undefiniert |

<a id="table-tab-dkg-test-und-einlernen-prg"></a>
### TAB_DKG_TEST_UND_EINLERNEN_PRG

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | Beliebigen Gang einlegen |
| 0x21 | Spülfunktion starten |
| 0x22 | Solldruckvorgabe Kupplung 1 |
| 0x23 | Solldruckvorgabe Kupplung 2 |
| 0x24 | Vorgabe des Systemdrucks |
| 0x25 | Kupplungskühlung aktivieren |
| 0x26 | Diagnose Parksperrenmagnet |
| 0x27 | Diagnose PV7 |
| 0x30 | Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1+2) |
| 0x32 | Getriebe einlernen |
| 0x33 | Adaptionswerte in NVRAM speichern |
| 0x34 | Ventilkennlinien einlernen PV1/2 |
| 0x35 | Fehlerspeicher formatieren |
| 0xFF | Undefiniert |

<a id="table-vbi-err-rcpt-eng-egs"></a>
### VBI_ERR_RCPT_ENG_EGS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | ja |
| 0 | nein |

<a id="table-vbi-trai"></a>
### VBI_TRAI

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ohne Anhänger |
| 1 | mit Anhänger |
