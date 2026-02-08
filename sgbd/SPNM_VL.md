# SPNM_VL.prg

- Jobs: [31](#jobs)
- Tables: [61](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sitz-Pneumatik-Modul vorne links |
| ORIGIN | BMW EI-431 Huth |
| REVISION | 7.000 |
| AUTHOR | iSYS_RTS 1 Donath, KPIT DT Biebach |
| COMMENT | - |
| PACKAGE | 1.70 |
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
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events $02 eventWindowTime - infinite (LH Diagnosemaster V11 oder höher, Umsetzung nach LH V6 - V10 wird jedoch toleriert)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default

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

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events $02 eventWindowTime - infinite (LH Diagnosemaster V11 oder höher, Umsetzung nach LH V6 - V10 wird jedoch toleriert)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF  = Status der aktiven Fehlermeldung nicht feststellbar |
| STAT_ROE_AKTIV_TEXT | string | Interpretation von STAT_ROE_AKTIV table UDS_TAB_ROE_AKTIV TEXT |
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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (141 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XD7E3_D](#table-arg-0xd7e3-d) (2 × 12)
- [ARG_0XD7E5_D](#table-arg-0xd7e5-d) (1 × 12)
- [ARG_0XD7F4_D](#table-arg-0xd7f4-d) (3 × 12)
- [ARG_0XD7F5_D](#table-arg-0xd7f5-d) (1 × 12)
- [ARG_0XD7F6_D](#table-arg-0xd7f6-d) (2 × 12)
- [ARG_0XD7F8_D](#table-arg-0xd7f8-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (62 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (21 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (4 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0XA710_R](#table-res-0xa710-r) (6 × 13)
- [RES_0XA711_R](#table-res-0xa711-r) (21 × 13)
- [RES_0XD7E5_D](#table-res-0xd7e5-d) (2 × 10)
- [RES_0XD7E8_D](#table-res-0xd7e8-d) (14 × 10)
- [RES_0XD7E9_D](#table-res-0xd7e9-d) (4 × 10)
- [RES_0XD7ED_D](#table-res-0xd7ed-d) (2 × 10)
- [RES_0XD7F3_D](#table-res-0xd7f3-d) (3 × 10)
- [RES_0XD7F4_D](#table-res-0xd7f4-d) (2 × 10)
- [RES_0XD7F5_D](#table-res-0xd7f5-d) (2 × 10)
- [RES_0XD7F6_D](#table-res-0xd7f6-d) (3 × 10)
- [RES_0XD7F7_D](#table-res-0xd7f7-d) (9 × 10)
- [RES_0XD7F8_D](#table-res-0xd7f8-d) (33 × 10)
- [RES_0XD7F9_D](#table-res-0xd7f9-d) (7 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (19 × 16)
- [TAB_SPNM_BUS_IN_CRASH](#table-tab-spnm-bus-in-crash) (8 × 2)
- [TAB_SPNM_BUS_IN_KLEMMEN](#table-tab-spnm-bus-in-klemmen) (12 × 2)
- [TAB_SPNM_BUS_IN_LENKUNG](#table-tab-spnm-bus-in-lenkung) (3 × 2)
- [TAB_SPNM_DELETE_STATISTIK](#table-tab-spnm-delete-statistik) (5 × 2)
- [TAB_SPNM_LORDOSE_ANST](#table-tab-spnm-lordose-anst) (5 × 2)
- [TAB_SPNM_LORDOSE_SCHALTER](#table-tab-spnm-lordose-schalter) (7 × 2)
- [TAB_SPNM_LORDOSE_STAT](#table-tab-spnm-lordose-stat) (7 × 2)
- [TAB_SPNM_LUFTBLASEN](#table-tab-spnm-luftblasen) (15 × 2)
- [TAB_SPNM_LUFTBLASEN_AKTION](#table-tab-spnm-luftblasen-aktion) (3 × 2)
- [TAB_SPNM_MASSAGE_PROG](#table-tab-spnm-massage-prog) (14 × 2)
- [TAB_SPNM_MASSAGE_PROG_ANST](#table-tab-spnm-massage-prog-anst) (14 × 2)
- [TAB_SPNM_MASSAGE_SCHALTER](#table-tab-spnm-massage-schalter) (3 × 2)
- [TAB_SPNM_MASSAGE_STUFE](#table-tab-spnm-massage-stufe) (5 × 2)
- [TAB_SPNM_STEST_AKTIV](#table-tab-spnm-stest-aktiv) (11 × 2)
- [TAB_SPNM_STEST_LORDOSE_SCHALTER](#table-tab-spnm-stest-lordose-schalter) (5 × 2)
- [TAB_SPNM_STEST_STATUS](#table-tab-spnm-stest-status) (4 × 2)
- [TAB_SPNM_STEST_STATUS_PN](#table-tab-spnm-stest-status-pn) (5 × 2)
- [TAB_SPNM_VENTILE_STAT](#table-tab-spnm-ventile-stat) (6 × 2)
- [TAB_SPNM_VERBAUPOSITION](#table-tab-spnm-verbauposition) (6 × 2)

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

Dimensions: 141 rows × 2 columns

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

<a id="table-arg-0xd7e3-d"></a>
### ARG_0XD7E3_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | high | unsigned char | - | TAB_SPNM_LUFTBLASEN_AKTION | - | - | - | - | - | Auswahl der Aktion (siehe TAB_SPNM_LUFTBLASEN_AKTION) |
| BLASE | 0-n | high | unsigned char | - | TAB_SPNM_LUFTBLASEN | - | - | - | - | - | Auswahl der Luftblase (siehe TAB_SPNM_LUFTBLASEN) |

<a id="table-arg-0xd7e5-d"></a>
### ARG_0XD7E5_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ANLERNEN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0 = keine Aktion 1 = Verbauposition anlernen (SG speichert sofort die aktuelle Pin-Codierung) |

<a id="table-arg-0xd7f4-d"></a>
### ARG_0XD7F4_D

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Pumpe: 0 = Pumpe ausschalten, 1 = Pumpe einschalten |
| PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | PWM-Wert für die Ansteuerung (Bereich: 0-100 %) |
| TIMEOUT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Timeout-Zeit für die Ansteuerung in Sekunden (Bereich: 0-255 Sekunden) |

<a id="table-arg-0xd7f5-d"></a>
### ARG_0XD7F5_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | high | unsigned char | - | TAB_SPNM_LORDOSE_ANST | - | - | - | - | - | Richtung der Lordosenansteuerung (siehe TAB_SPNM_LORDOSE_ANST) |

<a id="table-arg-0xd7f6-d"></a>
### ARG_0XD7F6_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROGRAMM | 0-n | high | unsigned char | - | TAB_SPNM_MASSAGE_PROG_ANST | - | - | - | - | - | Auswahl Massageprogramm (siehe TAB_SPNM_MASSAGE_PROG_ANST) |
| STUFE | 0-n | high | unsigned char | - | TAB_SPNM_MASSAGE_STUFE | - | - | - | - | - | Auswahl Intensitätsstufe (siehe TAB_SPNM_MASSAGE_STUFE) |

<a id="table-arg-0xd7f8-d"></a>
### ARG_0XD7F8_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | high | unsigned char | - | TAB_SPNM_DELETE_STATISTIK | - | - | - | - | - | Löschen der Statistikdaten für einzelne oder alle Funktionen im SPNM (siehe TAB_SPNM_DELETE_STATISTIK) |

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

Dimensions: 62 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x025300 | Energiesparmode aktiv | 0 |
| 0x025308 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x025309 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02530A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02530B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 |
| 0x02530C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x02530D | Codierung: Codierdaten nicht qualifiziert | 0 |
| 0x025320 | CAN-Fehler (Sammelfehler) | 0 |
| 0x025323 | Flash Memory Fehler (Sammelfehler) | 0 |
| 0x025329 | Softwarefehler (Sammelfehler) | 0 |
| 0x02FF53 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x806780 | Überspannung erkannt | 1 |
| 0x806781 | Unterspannung erkannt | 1 |
| 0x806782 | SPNM_VL: Verbauort unplausibel | 0 |
| 0x806783 | SPNM Pumpe: Leitungsunterbrechung | 0 |
| 0x806784 | SPNM Pumpe: Überlast oder Kurzschluss | 0 |
| 0x806785 | Lordose, obere Blase (Ventil 1): Zieldruck wird nicht erreicht | 0 |
| 0x806786 | Lordose, untere Blase (Ventil 2): Zieldruck wird nicht erreicht | 0 |
| 0x806787 | Aktivsitz, linke Blase (Ventil 3): Zieldruck wird nicht erreicht | 0 |
| 0x806788 | Aktivsitz, rechte Blase (Ventil 4): Zieldruck wird nicht erreicht | 0 |
| 0x806789 | Massage, Blase 1 (Ventil 5): Zieldruck wird nicht erreicht | 0 |
| 0x80678A | Massage, Blase 2 (Ventil 6): Zieldruck wird nicht erreicht | 0 |
| 0x80678B | Massage, Blase 3 (Ventil 7): Zieldruck wird nicht erreicht | 0 |
| 0x80678C | Massage, Blase 4 (Ventil 8): Zieldruck wird nicht erreicht | 0 |
| 0x80678D | Massage, Blase 5 (Ventil 9): Zieldruck wird nicht erreicht | 0 |
| 0x80678E | Massage, Blase 6 (Ventil 10): Zieldruck wird nicht erreicht | 0 |
| 0x80678F | Rotationsblase mitte links (Ventil 11): Zieldruck wird nicht erreicht | 0 |
| 0x806790 | Rotationsblase mitte rechts (Ventil 12): Zieldruck wird nicht erreicht | 0 |
| 0x806791 | Rotationsblase oben rechts (Ventil 13): Zieldruck wird nicht erreicht | 0 |
| 0x806792 | Rotationsblase oben links (Ventil 14): Zieldruck wird nicht erreicht | 0 |
| 0x806793 | Taster Lordose: Taster hängt | 0 |
| 0x806795 | Taster Lordose: Leitungsfehler | 0 |
| 0x806796 | Taste Massage: Taste hängt | 0 |
| 0x806797 | SPNM: interner Hardwarefehler (Sammelfehler für Ventile und Drucksensoren) | 0 |
| 0x806799 | Lordose, obere Blase (Ventil 1): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679A | Lordose, untere Blase (Ventil 2): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679B | Aktivsitz, linke Blase (Ventil 3): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679C | Aktivsitz, rechte Blase (Ventil 4): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679D | Massage, Blase 1 (Ventil 5): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679E | Massage, Blase 2 (Ventil 6): Zieldruck wird zu schnell erreicht | 0 |
| 0x80679F | Massage, Blase 3 (Ventil 7): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A0 | Massage, Blase 4 (Ventil 8): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A1 | Massage, Blase 5 (Ventil 9): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A2 | Massage, Blase 6 (Ventil 10): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A3 | Rotationsblase mitte links (Ventil 11): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A4 | Rotationsblase mitte rechts (Ventil 12): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A5 | Rotationsblase oben rechts (Ventil 13): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A6 | Rotationsblase oben links (Ventil 14): Zieldruck wird zu schnell erreicht | 0 |
| 0x8067A7 | SPNM_VL: Verbauort nicht angelernt | 0 |
| 0x8067A8 | Temperatur im Steuergerät ausserhalb des Betriebsbereichs | 1 |
| 0x8067A9 | Umgebungsdruck ausserhalb des Betriebsbereichs | 1 |
| 0x8067AA | SPNM: Vordruckkanal undicht | 0 |
| 0x8067AB | Drucksensor Vordruckkanal: Druck ausserhalb des zulässigen Bereichs | 1 |
| 0x8067AC | Drucksensor Rotationsblase oben rechts: Druck ausserhalb des zulässigen Bereichs | 1 |
| 0x8067AD | Drucksensor Rotationsblase oben links: Druck ausserhalb des zulässigen Bereichs | 1 |
| 0xDDC468 | BODY-CAN Control Module Bus OFF | 0 |
| 0xDDCBFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xDDD400 | Botschaft (0x1A1, Geschwindigkeit Fahrzeug): Ausfall | 1 |
| 0xDDD401 | Botschaft (0x19A, Querbeschleunigung Schwerpunkt): Ausfall | 1 |
| 0xDDD402 | Botschaft (0xAB, Status Crash): Ausfall | 1 |
| 0xDDD403 | Botschaft (0x3C, Zustand Fahrzeug): Ausfall | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4020 | Spannung | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4021 | Druckwert | hPa | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4022 | Temperatur | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 21 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x530015 | Ventil  M1 defekt | 0 |
| 0x530016 | Ventil  M2 defekt | 0 |
| 0x530017 | Ventil  M3 defekt | 0 |
| 0x530018 | Ventil  M4 defekt | 0 |
| 0x530019 | Ventil  M5 defekt | 0 |
| 0x530020 | Ventil  M6 defekt | 0 |
| 0x530021 | Ventil  R1 defekt | 0 |
| 0x530022 | Ventil  R2 defekt | 0 |
| 0x530023 | Ventil  R1 AS2 defekt | 0 |
| 0x530024 | Ventil  R2 AS1 defekt | 0 |
| 0x530025 | Ventil  LD1 defekt | 0 |
| 0x530026 | Ventil  LD2 defekt | 0 |
| 0x530027 | Ventil  AS1 defekt | 0 |
| 0x530028 | Ventil  AS2 defekt | 0 |
| 0x530029 | Drucksensor Umgebungsdruck defekt | 0 |
| 0x530030 | Drucksensor Vordruck defekt | 0 |
| 0x530031 | Drucksensor Rotationsblase oben rechts defekt | 0 |
| 0x530032 | Drucksensor Rotationsblase oben links defekt | 0 |
| 0x530033 | Temperatursensor defekt | 0 |
| 0x530125 | Codierwert über Grenzwert des Systems | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4020 | Spannung | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4021 | Druckwert | hPa | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4022 | Temperatur | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

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

<a id="table-res-0x2504-d"></a>
### RES_0X2504_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ERASE_MEMORY_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | EraseMemoryTime, maximale SWE-Löschzeit mit Ablaufkontrolle im Steuergerät. |
| STAT_CHECK_MEMORY_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | CheckMemoryTime (Bsp.: Signaturprüfung), maximale Speicherprüfzeit mit Ablaufkontrolle im Steuergerät. |
| STAT_BOOTLOADER_INSTALLATION_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | BootloaderInstallationTime Die Zeit, die nach dem Reset benötigt wird, damit der Hilfsbootloader gestartet wird, den Bootloader löscht, den neuen Bootloader kopiert, dessen Signatur prüf und der neue Bootloader gestartet wird bis er wieder diagnosefähig ist. Angabe ist verpflichtend für alle Steuergeräte, auch wenn das Steuergerät keinen Bootloader Update geplant hat. Ein Wert von 0x0000 ist verboten. |
| STAT_AUTHENTICATION_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AuthenticationTime, die maximale Zeit, die das Steuergerät zur Prüfung der Authentisierung (sendKey) benötigt mit Ablaufkontrolle im Steuergerät. |
| STAT_RESET_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ResetTime Die Zeitangabe bezieht sich auf den Übergang von der ApplicationExtendedSesssion in die ProgrammingSession bzw. bei Übergang von der ProgrammingSession in die DefaultSession. Es ist der Maximalwert auszugeben. Nach Ablauf der ResetTime ist das Steuergerät durch Diagnose ansprechbar. |
| STAT_TRANSFER_DATA_TIME_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | TransferDataTime Die Angabe hat sich zu beziehen auf einen TransferData mit maximaler Blocklänge auf die Zeitspanne vom vollständigen Empfang der Daten im Steuergerät über das ggf. erforderliche Dekomprimieren und dem vollständigen Speichern im nichtflüchtigen Speicher bis einschließlich dem Senden der positiven Response. |

<a id="table-res-0xa710-r"></a>
### RES_0XA710_R

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SELBSTTEST_AKTIV | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_AKTIV | - | - | - | aktueller Status des Selbsttests (siehe TAB_SPNM_STEST_AKTIV) |
| STAT_SELBSTTEST | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Gesamtergebnis des Selbsttests (siehe TAB_SPNM_STEST_STATUS) |
| STAT_SENSOREN | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Sensoren (siehe TAB_SPNM_STEST_STATUS) |
| STAT_VENTILE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Ventile (siehe TAB_SPNM_STEST_STATUS) |
| STAT_PUMPE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Pumpe (siehe TAB_SPNM_STEST_STATUS) |
| STAT_BEDIENSCHALTER_LORDOSE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_LORDOSE_SCHALTER | - | - | - | Ergebnis Selbsttest des Bedienschalters Lordose (siehe TAB_SPNM_STEST_LORDOSE_SCHALTER) |

<a id="table-res-0xa711-r"></a>
### RES_0XA711_R

Dimensions: 21 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SELBSTTEST_AKTIV | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_AKTIV | - | - | - | aktueller Status des Selbsttests (siehe TAB_SPNM_STEST_AKTIV) |
| STAT_SELBSTTEST | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Gesamtergebnis des Selbsttests (siehe TAB_SPNM_STEST_STATUS) |
| STAT_SENSOREN | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Sensoren (siehe TAB_SPNM_STEST_STATUS) |
| STAT_VENTILE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Ventile (siehe TAB_SPNM_STEST_STATUS) |
| STAT_PUMPE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest der Pumpe (siehe TAB_SPNM_STEST_STATUS) |
| STAT_BEDIENSCHALTER_LORDOSE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_LORDOSE_SCHALTER | - | - | - | Ergebnis Selbsttest des Bedienschalters Lordose (siehe TAB_SPNM_STEST_LORDOSE_SCHALTER) |
| STAT_VORDRUCK | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS | - | - | - | Ergebnis Selbsttest Dichtigkeit des Vordruckkanals (Pumpe, Druckzuleitung, Vordruckkammer) |
| STAT_LORDOSE_BLASE_OBEN | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Lordose, obere Blase (Ventil 1) |
| STAT_LORDOSE_BLASE_UNTEN | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Lordose, untere Blase (Ventil 2) |
| STAT_AKTIVSITZ_BLASE_LINKS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Aktivsitz, linke Blase (Ventil 3) |
| STAT_AKTIVSITZ_BLASE_RECHTS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Aktivsitz, rechte Blase (Ventil 4) |
| STAT_MASSAGE_BLASE_1 | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Massage, Blase 1 (Ventil 5) |
| STAT_MASSAGE_BLASE_2 | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Massage, Blase 2 (Ventil 6) |
| STAT_MASSAGE_BLASE_3 | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Massage, Blase 3 (Ventil 7) |
| STAT_MASSAGE_BLASE_4 | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Massage, Blase 4 (Ventil 8) |
| STAT_MASSAGE_BLASE_5 | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Massage, Blase 5 (Ventil 9) |
| STAT_RESERVE | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Reserve Ergebnis Selbsttest (Ventil 10) |
| STAT_ROTATIONSBLASE_MITTE_LINKS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Rotationsblase mitte links (Ventil 11) |
| STAT_ROTATIONSBLASE_MITTE_RECHTS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Rotationsblase mitte rechts (Ventil 12) |
| STAT_ROTATIONSBLASE_OBEN_RECHTS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Rotationsblase oben rechts (Ventil 13) |
| STAT_ROTATIONSBLASE_OBEN_LINKS | - | - | + | 0-n | high | unsigned char | - | TAB_SPNM_STEST_STATUS_PN | - | - | - | Ergebnis Selbsttest Rotationsblase oben links (Ventil 14) |

<a id="table-res-0xd7e5-d"></a>
### RES_0XD7E5_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAUPOSITION_AKTUELL | 0-n | high | unsigned char | - | TAB_SPNM_VERBAUPOSITION | - | - | - | Aktuelle Verbauposition laut Pin-Codierung (siehe TAB_SPNM_VERBAUPOSITION) |
| STAT_VERBAUPOSITION_SOLL | 0-n | high | unsigned char | - | TAB_SPNM_VERBAUPOSITION | - | - | - | Angelernte Verbauposition beim letzten Anlernvorgang (siehe TAB_SPNM_VERBAUPOSITION) |

<a id="table-res-0xd7e8-d"></a>
### RES_0XD7E8_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VENTIL_1 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 1 - Lordose oben (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_2 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 2 - Lordose unten (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_3 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 3 - Aktivsitz links (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_4 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 4 - Aktivsitz rechts (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_5 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 5 - Massage 1 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_6 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 6 - Massage 2 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_7 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 7 - Massage 3 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_8 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 8 - Massage 4 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_9 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 9 - Massage 5 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_10 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 10 (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_11 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 11 - Rotation mitte links (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_12 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 12 - Rotation mitte rechts (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_13 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 13 - Rotation oben rechts (siehe TAB_SPNM_VENTILE_STAT) |
| STAT_VENTIL_14 | 0-n | high | unsigned char | - | TAB_SPNM_VENTILE_STAT | - | - | - | Status Ventil 14 - Rotation oben links (siehe TAB_SPNM_VENTILE_STAT) |

<a id="table-res-0xd7e9-d"></a>
### RES_0XD7E9_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DRUCKSENSOR_1_WERT | hPa | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Status Drucksensor 1 - Umgebungsdruck (Wertebereich: 0 bis 2000 hPa; ungültig = 65535) |
| STAT_DRUCKSENSOR_2_WERT | hPa | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Status Drucksensor 2 - Vordruckkammer (Wertebereich: 0 bis 2000 hPa; ungültig = 65535) |
| STAT_DRUCKSENSOR_3_WERT | hPa | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Status Drucksensor 3 - Rotationsblase oben rechts (Wertebereich: 0 bis 2000 hPa; ungültig = 65535) |
| STAT_DRUCKSENSOR_4_WERT | hPa | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Status Drucksensor 4 - Rotationsblase oben links (Wertebereich: 0 bis 2000 hPa; ungültig = 65535) |

<a id="table-res-0xd7ed-d"></a>
### RES_0XD7ED_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temperatur im SPNM nach SW-Korrektur (Wertebereich: -40 bis 150 °C) |
| STAT_TEMPERATUR_ROH_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temperatur Rohwert im SPNM (Wertebereich: -40 bis 150 °C) |

<a id="table-res-0xd7f3-d"></a>
### RES_0XD7F3_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_LORDOSE | 0-n | high | unsigned char | - | TAB_SPNM_LORDOSE_SCHALTER | - | - | - | Statusabfrage Bedienschalter für Lordosenstütze (siehe TAB_SPNM_LORDOSE_STAT) |
| STAT_ANBINDUNG_SCHALTER_LORDOSE | 0/1 | high | unsigned char | - | - | - | - | - | Verbauort des Bedienschalters Lordose: 0 = direkt am SPNM angeschlossen, 1 = Empfang Statusnachrichten über Bus |
| STAT_SCHALTER_MASSAGE | 0-n | high | unsigned char | - | TAB_SPNM_MASSAGE_SCHALTER | - | - | - | Statusabfrage Bedienschalter für Massage (siehe TAB_SPNM_MASSAGE_SCHALTER) |

<a id="table-res-0xd7f4-d"></a>
### RES_0XD7F4_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PUMPE | 0/1 | high | unsigned char | - | - | - | - | - | aktueller Status der Pumpe: 0 = ausgeschaltet, 1 = eingeschaltet |
| STAT_PUMPE_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM-Wert der Pumpenansteuerung (0-100 %) |

<a id="table-res-0xd7f5-d"></a>
### RES_0XD7F5_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZUSTAND | 0/1 | high | unsigned char | - | - | - | - | - | Status Lordose: 0 = aus, 1 = ein |
| STAT_RICHTUNG | 0-n | high | unsigned char | - | TAB_SPNM_LORDOSE_STAT | - | - | - | Richtung der Lordosenverstellung (siehe TAB_SPNM_LORDOSE_STAT) |

<a id="table-res-0xd7f6-d"></a>
### RES_0XD7F6_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZUSTAND | 0/1 | high | unsigned char | - | - | - | - | - | Status Massagefunktion 0 = aus, 1 = ein |
| STAT_PROGRAMM | 0-n | high | unsigned char | - | TAB_SPNM_MASSAGE_PROG | - | - | - | Aktuelles Massageprogramm (siehe TAB_SPNM_MASSAGE_PROG) |
| STAT_STUFE | 0-n | high | unsigned char | - | TAB_SPNM_MASSAGE_STUFE | - | - | - | Intensitätsstufe (siehe TAB_SPNM_MASSAGE_STUFE) |

<a id="table-res-0xd7f7-d"></a>
### RES_0XD7F7_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PWF | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_KLEMMEN | - | - | - | Status Klemmen PWF (siehe TAB_SPNM_BUS_IN_KLEMMEN) |
| STAT_GESCHWINDIGKEIT_WERT | km/h | high | unsigned int | - | - | 0.015625 | 1.0 | 0.0 | Status Geschwindigkeit: Wertebereich von 0 bis 350 km/h (1024 = ungültig) |
| STAT_QUERBESCHLEUNIGUNG_WERT | m/s² | high | unsigned int | - | - | 0.002 | 1.0 | -65.0 | Status Querbeschleunigung: Wertebereich von -65 bis 65 (66 = ungültig) |
| STAT_RESERVE | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_LENKUNG | - | - | - | Reserve (aktuell nicht verwendet) |
| STAT_CRASHSCHWERE_FRONT | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_CRASH | - | - | - | Status Crashschwere front (siehe TAB_SPNM_BUS_IN_CRASH) |
| STAT_CRASHSCHWERE_SEITE_RECHTS | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_CRASH | - | - | - | Status Crashschwere Seite rechts (siehe TAB_SPNM_BUS_IN_CRASH) |
| STAT_CRASHSCHWERE_SEITE_LINKS | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_CRASH | - | - | - | Status Crashschwere Seite links (siehe TAB_SPNM_BUS_IN_CRASH) |
| STAT_CRASHSCHWERE_HECK | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_CRASH | - | - | - | Status Crashschwere heck (siehe TAB_SPNM_BUS_IN_CRASH) |
| STAT_CRASHSCHWERE_ROLL_OVER | 0-n | high | unsigned char | - | TAB_SPNM_BUS_IN_CRASH | - | - | - | Status Crashschwere Überschlag (siehe TAB_SPNM_BUS_IN_CRASH) |

<a id="table-res-0xd7f8-d"></a>
### RES_0XD7F8_D

Dimensions: 33 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PUMPE_ANLAEUFE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Pumpenanläufe |
| STAT_PUMPE_BETRIEBSDAUER_WERT | min | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer der Pumpe in min |
| STAT_LORDOSE_WAKE_UPS_PARKEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Weckvorkänge über Lordose im Zustand Parken |
| STAT_LORDOSE_WAKE_UPS_WOHNEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Weckvorkänge über Lordose im Zustand Wohnen |
| STAT_LORDOSE_ANZAHL_RAUF_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Betätigungen nach oben |
| STAT_LORDOSE_ANZAHL_RUNTER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Betätigungen nach unten |
| STAT_LORDOSE_ANZAHL_VOR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Betätigungen nach vorne |
| STAT_LORDOSE_ANZAHL_ZURUECK_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Betätigungen nach hinten |
| STAT_MASSAGE_PROG_1_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_1_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_1_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_2_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_2_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_2_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_3_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_3_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_3_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_4_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_4_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_4_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_5_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_5_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_5_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_6_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_6_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_6_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_7_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_7_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_7_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_8_INT_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_8_INT_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_8_INT_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |
| STAT_MASSAGE_PROG_9_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Programm/Intensität mit Dauer länger als 1 Minute |

<a id="table-res-0xd7f9-d"></a>
### RES_0XD7F9_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSION_MAJOR | 0-n | high | unsigned char | - | - | - | - | - | SW Hauptversion |
| STAT_VERSION_MINOR | 0-n | high | unsigned char | - | - | - | - | - | SW Unterversion |
| STAT_VERSION_PATCH | 0-n | high | unsigned char | - | - | - | - | - | SW Patchversion |
| STAT_VERSION_DATE_YEAR_HI | 0-n | high | unsigned char | - | - | - | - | - | SW Releasedatum: Jahr (higher bit) |
| STAT_VERSION_DATE_YEAR_LO | 0-n | high | unsigned char | - | - | - | - | - | SW Releasedatum: Jahr (lower bit) |
| STAT_VERSION_DATE_MONTH | 0-n | high | unsigned char | - | - | - | - | - | SW Releasedatum: Monat |
| STAT_VERSION_DATE_DAY | 0-n | high | unsigned char | - | - | - | - | - | SW Releasedatum: Tag |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 19 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | high | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SELBSTTEST_SPNM_EL | 0xA710 | - | Selbsttest SPNM elektrisch | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA710_R |
| SELBSTTEST_SPNM_ELPN | 0xA711 | - | Selbsttest SPNM elektrisch und pneumatisch | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA711_R |
| LUFTBLASEN_SPNM | 0xD7E3 | - | Steuern Luftblasen | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7E3_D | - |
| VERBAUPOSITION_SPNM | 0xD7E5 | - | Verbauposition des SPNM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD7E5_D | RES_0xD7E5_D |
| GATEWAY_SPNM | 0xD7E6 | STAT_GATEWAY_VORHANDEN | Abfrage, ob Gateway im SPNM vorhanden ist: 0 = kein Gateway verbaut, 1 = Gateway verbaut | 0/1 | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| VERSORGUNG_SPNM | 0xD7E7 | STAT_VERSORGUNGSSPANNUNG_WERT | Höhe der Versorgungsspannung in Volt | V | - | high | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| VENTILE_SPNM | 0xD7E8 | - | Ventile im SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7E8_D |
| DRUCKSENSOREN_SPNM | 0xD7E9 | - | Drucksensoren im SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7E9_D |
| TEMPERATURSENSOR_SPNM | 0xD7ED | - | Temperatursensor im SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7ED_D |
| BEDIENSCHALTER_SPNM | 0xD7F3 | - | Bedienschalter für SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7F3_D |
| PUMPE_SPNM | 0xD7F4 | - | Pumpe des SPNM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD7F4_D | RES_0xD7F4_D |
| LORDOSE_SPNM | 0xD7F5 | - | Funktion Lordose im SPNM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD7F5_D | RES_0xD7F5_D |
| MASSAGE_SPNM | 0xD7F6 | - | Funktion Massage im SPNM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD7F6_D | RES_0xD7F6_D |
| BUS_IN_SIGNALE_SPNM | 0xD7F7 | - | Bus-Signale für SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7F7_D |
| STATISTIKZAEHLER_SPNM | 0xD7F8 | - | Statistikdaten für Lordose/Massage und Pumpe im SPNM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD7F8_D | RES_0xD7F8_D |
| VERSION_PNSF | 0xD7F9 | - | Softwareversion der PNSF-Komponente im SPNM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7F9_D |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | high | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |

<a id="table-tab-spnm-bus-in-crash"></a>
### TAB_SPNM_BUS_IN_CRASH

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Crash |
| 0x01 | Crashschwere 1 |
| 0x02 | Crashschwere 2 |
| 0x03 | Crashschwere 3 |
| 0x04 | Crashschwere 4 |
| 0x0D | Funktionsschnittstelle ist nicht verfuegbar |
| 0x0F | Funktion meldet Fehler |
| 0xFF | ungültig |

<a id="table-tab-spnm-bus-in-klemmen"></a>
### TAB_SPNM_BUS_IN_KLEMMEN

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | reserviert |
| 0x01 | Parken Bordnetz n.i.O. |
| 0x02 | Parken Bordnetz i.O. |
| 0x03 | Standfunktionen Kunde nicht im Fahrzeug |
| 0x05 | Wohnen |
| 0x07 | Pruefen / Analyse / Diagnose |
| 0x08 | Fahrbereitschaft herstellen |
| 0x0A | Fahren |
| 0x0C | Fahrbereitschaft beenden |
| 0x0E | nicht verfügbar |
| 0x0F | Signal ungültig |
| 0xFF | ungültig |

<a id="table-tab-spnm-bus-in-lenkung"></a>
### TAB_SPNM_BUS_IN_LENKUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Linkslenker |
| 0x02 | Rechtslenker |
| 0xFF | ungültig |

<a id="table-tab-spnm-delete-statistik"></a>
### TAB_SPNM_DELETE_STATISTIK

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Daten Lordose |
| 0x01 | Daten Massage |
| 0x02 | Daten Pumpe |
| 0x03 | Weckvorgänge Lordose |
| 0x04 | alle Daten löschen |

<a id="table-tab-spnm-lordose-anst"></a>
### TAB_SPNM_LORDOSE_ANST

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | nach oben |
| 0x02 | nach unten |
| 0x04 | nach vorne |
| 0x08 | nach hinten |

<a id="table-tab-spnm-lordose-schalter"></a>
### TAB_SPNM_LORDOSE_SCHALTER

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Aktion |
| 0x01 | nach oben |
| 0x02 | nach unten |
| 0x04 | nach hinten |
| 0x08 | nach vorne |
| 0xFE | nicht vorhanden / nicht codiert |
| 0xFF | ungültig |

<a id="table-tab-spnm-lordose-stat"></a>
### TAB_SPNM_LORDOSE_STAT

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Aktion |
| 0x01 | nach oben |
| 0x02 | nach unten |
| 0x04 | nach vorne |
| 0x08 | nach hinten |
| 0xFE | nicht vorhanden / nicht codiert |
| 0xFF | ungültig |

<a id="table-tab-spnm-luftblasen"></a>
### TAB_SPNM_LUFTBLASEN

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | Lordose oben |
| 0x02 | Lordose unten |
| 0x03 | Aktivsitz links |
| 0x04 | Aktivsitz rechts |
| 0x05 | Massage Blase 1 |
| 0x06 | Massage Blase 2 |
| 0x07 | Massage Blase 3 |
| 0x08 | Massage Blase 4 |
| 0x09 | Massage Blase 5 |
| 0x0A | Reserve |
| 0x0B | Rotation Blase mitte links |
| 0x0C | Rotation Blase mitte rechts |
| 0x0D | Rotation Blase oben rechts |
| 0x0E | Rotation Blase oben links |

<a id="table-tab-spnm-luftblasen-aktion"></a>
### TAB_SPNM_LUFTBLASEN_AKTION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | fluten |
| 0x02 | entlüften |

<a id="table-tab-spnm-massage-prog"></a>
### TAB_SPNM_MASSAGE_PROG

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | P1 (Beckenmobilisation) |
| 0x02 | P2 (Oberkörpermobilisation) |
| 0x03 | P3 (Ganzkörpermobilisation) |
| 0x04 | P4 (Rückenmassage) |
| 0x05 | P5 (Schultermassage) |
| 0x06 | P6 (Lendenmassage) |
| 0x07 | P7 (Rückenmassage und Oberkörpermobilisation) |
| 0x08 | P8 (Rückenmassage und Ganzkörpermobilisation) |
| 0x09 | P9 (Körpertraining) |
| 0x0A | P10 (Reserve) |
| 0x0B | P11 (Reserve) |
| 0x0C | P12 (Reserve) |
| 0xFF | ungültig |

<a id="table-tab-spnm-massage-prog-anst"></a>
### TAB_SPNM_MASSAGE_PROG_ANST

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | P1 (Beckenmobilisation) |
| 0x02 | P2 (Oberkörpermobilisation) |
| 0x03 | P3 (Ganzkörpermobilisation) |
| 0x04 | P4 (Rückenmassage) |
| 0x05 | P5 (Schultermassage) |
| 0x06 | P6 (Lendenmassage) |
| 0x07 | P7 (Rückenmassage und Oberkörpermobilisation) |
| 0x08 | P8 (Rückenmassage und Ganzkörpermobilisation) |
| 0x09 | P9 (Reserve) |
| 0x0A | P10 (Reserve) |
| 0x0B | P11 (Reserve) |
| 0x0C | P12 (Reserve) |
| 0xFF | ungültig |

<a id="table-tab-spnm-massage-schalter"></a>
### TAB_SPNM_MASSAGE_SCHALTER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht betätigt |
| 0x01 | betätigt |
| 0xFF | ungültig |

<a id="table-tab-spnm-massage-stufe"></a>
### TAB_SPNM_MASSAGE_STUFE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | Stufe 1 |
| 0x02 | Stufe 2 |
| 0x03 | Stufe 3 |
| 0xFF | ungültig |

<a id="table-tab-spnm-stest-aktiv"></a>
### TAB_SPNM_STEST_AKTIV

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | noch nicht gestartet |
| 0x01 | Selbsttest aktiv |
| 0x02 | Selbsttest beendet |
| 0x03 | abgebrochen wegen Vorbedingung Bordnetzspannung |
| 0x04 | abgebrochen wegen Vorbedingung SG-Temperatur |
| 0x05 | abgebrochen wegen Vorbedingung Umgebungsdruck |
| 0x06 | abgebrochen wegen nicht gespeicherten / nicht plausiblen Verbauort |
| 0x07 | abgebrochen wegen einem internen Fehler im SG |
| 0x08 | abgebrochen durch Diagnosebefehl |
| 0x09 | Reserve |
| 0xFF | ungültig |

<a id="table-tab-spnm-stest-lordose-schalter"></a>
### TAB_SPNM_STEST_LORDOSE_SCHALTER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Ergebnis vorhanden |
| 0x01 | keine Fehler festgestellt |
| 0x02 | Fehler festgestellt |
| 0x03 | nicht direkt angeschlossen oder nicht vorhanden |
| 0xFF | ungültig |

<a id="table-tab-spnm-stest-status"></a>
### TAB_SPNM_STEST_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Ergebnis vorhanden |
| 0x01 | keine Fehler festgestellt |
| 0x02 | Fehler festgestellt |
| 0xFF | ungültig |

<a id="table-tab-spnm-stest-status-pn"></a>
### TAB_SPNM_STEST_STATUS_PN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Ergebnis vorhanden |
| 0x01 | keine Fehler festgestellt |
| 0x02 | Zieldruck nicht erreicht (Blase, Druckleitung oder Ventil undicht) |
| 0x03 | Zieldruck zu schnell erreicht oder Entlüftungszeit zu lang |
| 0xFF | ungültig |

<a id="table-tab-spnm-ventile-stat"></a>
### TAB_SPNM_VENTILE_STAT

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | entlüften |
| 0x01 | befüllen |
| 0x02 | halten |
| 0x03 | nicht verwendet |
| 0x04 | Fehler / Status unplausibel |
| 0xFF | ungültig |

<a id="table-tab-spnm-verbauposition"></a>
### TAB_SPNM_VERBAUPOSITION

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | unbekannt |
| 0x01 | SPNM_VL |
| 0x02 | SPNM_VR |
| 0x03 | SPNM_HL |
| 0x04 | SPNM_HR |
| 0xFF | ungültig |
