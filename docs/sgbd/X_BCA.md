# X_BCA.prg

- Jobs: [32](#jobs)
- Tables: [230](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Motorrad Behördenmodul |
| ORIGIN | BMW UX-EE-2 Warneke |
| REVISION | 3.000 |
| AUTHOR | Dräxlmaier UX-EE-1 Rätscher, Dräxlmaier UX-EE-1 Utter |
| COMMENT | - |
| PACKAGE | 1.60 |
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
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
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
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann '--' |
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

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (140 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (248 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (206 × 2)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [ARG_0X4001_D](#table-arg-0x4001-d) (1 × 12)
- [ARG_0X4003_D](#table-arg-0x4003-d) (1 × 12)
- [ARG_0X4005_D](#table-arg-0x4005-d) (1 × 12)
- [ARG_0X4007_D](#table-arg-0x4007-d) (1 × 12)
- [ARG_0X4009_D](#table-arg-0x4009-d) (5 × 12)
- [ARG_0X400B_D](#table-arg-0x400b-d) (1 × 12)
- [ARG_0X400D_D](#table-arg-0x400d-d) (1 × 12)
- [ARG_0X400F_D](#table-arg-0x400f-d) (1 × 12)
- [ARG_0X4011_D](#table-arg-0x4011-d) (1 × 12)
- [ARG_0X4013_D](#table-arg-0x4013-d) (1 × 12)
- [ARG_0X4015_D](#table-arg-0x4015-d) (1 × 12)
- [ARG_0X4017_D](#table-arg-0x4017-d) (1 × 12)
- [ARG_0X4019_D](#table-arg-0x4019-d) (1 × 12)
- [ARG_0X401B_D](#table-arg-0x401b-d) (1 × 12)
- [ARG_0X401D_D](#table-arg-0x401d-d) (1 × 12)
- [ARG_0X401F_D](#table-arg-0x401f-d) (1 × 12)
- [ARG_0X4021_D](#table-arg-0x4021-d) (1 × 12)
- [ARG_0X4023_D](#table-arg-0x4023-d) (1 × 12)
- [ARG_0X4025_D](#table-arg-0x4025-d) (1 × 12)
- [ARG_0X4027_D](#table-arg-0x4027-d) (1 × 12)
- [ARG_0X4029_D](#table-arg-0x4029-d) (1 × 12)
- [ARG_0X402B_D](#table-arg-0x402b-d) (1 × 12)
- [ARG_0X402D_D](#table-arg-0x402d-d) (1 × 12)
- [ARG_0X402F_D](#table-arg-0x402f-d) (1 × 12)
- [ARG_0X4031_D](#table-arg-0x4031-d) (1 × 12)
- [ARG_0X4033_D](#table-arg-0x4033-d) (8 × 12)
- [ARG_0X4036_D](#table-arg-0x4036-d) (8 × 12)
- [ARG_0XE152_D](#table-arg-0xe152-d) (1 × 12)
- [ARG_0XE156_D](#table-arg-0xe156-d) (9 × 12)
- [ARG_0XE158_D](#table-arg-0xe158-d) (9 × 12)
- [ARG_0XE15A_D](#table-arg-0xe15a-d) (9 × 12)
- [ARG_0XE15C_D](#table-arg-0xe15c-d) (9 × 12)
- [ARG_0XE15E_D](#table-arg-0xe15e-d) (1 × 12)
- [ARG_0XE160_D](#table-arg-0xe160-d) (1 × 12)
- [ARG_0XE162_D](#table-arg-0xe162-d) (1 × 12)
- [ARG_0XE165_D](#table-arg-0xe165-d) (5 × 12)
- [ARG_0XE167_D](#table-arg-0xe167-d) (1 × 12)
- [ARG_0XE168_D](#table-arg-0xe168-d) (1 × 12)
- [ARG_0XE169_D](#table-arg-0xe169-d) (1 × 12)
- [ARG_0XE16E_D](#table-arg-0xe16e-d) (1 × 12)
- [ARG_0XE16F_D](#table-arg-0xe16f-d) (1 × 12)
- [ARG_0XE170_D](#table-arg-0xe170-d) (1 × 12)
- [ARG_0XE171_D](#table-arg-0xe171-d) (1 × 12)
- [ARG_0XE172_D](#table-arg-0xe172-d) (1 × 12)
- [ARG_0XE175_D](#table-arg-0xe175-d) (7 × 12)
- [ARG_0XE176_D](#table-arg-0xe176-d) (7 × 12)
- [ARG_0XE177_D](#table-arg-0xe177-d) (10 × 12)
- [ARG_0XE1A3_D](#table-arg-0xe1a3-d) (8 × 12)
- [ARG_0XE1A4_D](#table-arg-0xe1a4-d) (8 × 12)
- [ARG_0XE1A5_D](#table-arg-0xe1a5-d) (8 × 12)
- [ARG_0XE1A6_D](#table-arg-0xe1a6-d) (8 × 12)
- [ARG_0XE1A7_D](#table-arg-0xe1a7-d) (7 × 12)
- [ARG_0XFD06_D](#table-arg-0xfd06-d) (20 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [ENERGIESPARMODE_DOP](#table-energiesparmode-dop) (4 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FEHLERKLASSE_DOP](#table-fehlerklasse-dop) (4 × 2)
- [FORTTEXTE](#table-forttexte) (164 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [MR_TAB_BCA_CALIBRATION](#table-mr-tab-bca-calibration) (3 × 2)
- [MR_TAB_BCO_CALIBRATION](#table-mr-tab-bco-calibration) (5 × 2)
- [PROG_DEP_DOP](#table-prog-dep-dop) (6 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [RDTCI_LEV_DOP](#table-rdtci-lev-dop) (9 × 2)
- [RES_0X4001_D](#table-res-0x4001-d) (7 × 10)
- [RES_0X4002_D](#table-res-0x4002-d) (8 × 10)
- [RES_0X4003_D](#table-res-0x4003-d) (2 × 10)
- [RES_0X4004_D](#table-res-0x4004-d) (2 × 10)
- [RES_0X4005_D](#table-res-0x4005-d) (5 × 10)
- [RES_0X4006_D](#table-res-0x4006-d) (7 × 10)
- [RES_0X4007_D](#table-res-0x4007-d) (3 × 10)
- [RES_0X4008_D](#table-res-0x4008-d) (12 × 10)
- [RES_0X4009_D](#table-res-0x4009-d) (19 × 10)
- [RES_0X400B_D](#table-res-0x400b-d) (1 × 10)
- [RES_0X400D_D](#table-res-0x400d-d) (1 × 10)
- [RES_0X400F_D](#table-res-0x400f-d) (1 × 10)
- [RES_0X4011_D](#table-res-0x4011-d) (1 × 10)
- [RES_0X4012_D](#table-res-0x4012-d) (7 × 10)
- [RES_0X4013_D](#table-res-0x4013-d) (2 × 10)
- [RES_0X4014_D](#table-res-0x4014-d) (7 × 10)
- [RES_0X4015_D](#table-res-0x4015-d) (2 × 10)
- [RES_0X4016_D](#table-res-0x4016-d) (7 × 10)
- [RES_0X4017_D](#table-res-0x4017-d) (2 × 10)
- [RES_0X4018_D](#table-res-0x4018-d) (18 × 10)
- [RES_0X4019_D](#table-res-0x4019-d) (31 × 10)
- [RES_0X401A_D](#table-res-0x401a-d) (18 × 10)
- [RES_0X401B_D](#table-res-0x401b-d) (31 × 10)
- [RES_0X401C_D](#table-res-0x401c-d) (18 × 10)
- [RES_0X401D_D](#table-res-0x401d-d) (31 × 10)
- [RES_0X401E_D](#table-res-0x401e-d) (18 × 10)
- [RES_0X401F_D](#table-res-0x401f-d) (31 × 10)
- [RES_0X4020_D](#table-res-0x4020-d) (19 × 10)
- [RES_0X4021_D](#table-res-0x4021-d) (12 × 10)
- [RES_0X4022_D](#table-res-0x4022-d) (12 × 10)
- [RES_0X4023_D](#table-res-0x4023-d) (9 × 10)
- [RES_0X4025_D](#table-res-0x4025-d) (1 × 10)
- [RES_0X4027_D](#table-res-0x4027-d) (1 × 10)
- [RES_0X4028_D](#table-res-0x4028-d) (3 × 10)
- [RES_0X4029_D](#table-res-0x4029-d) (1 × 10)
- [RES_0X402B_D](#table-res-0x402b-d) (15 × 10)
- [RES_0X402D_D](#table-res-0x402d-d) (1 × 10)
- [RES_0X402F_D](#table-res-0x402f-d) (1 × 10)
- [RES_0X4030_D](#table-res-0x4030-d) (12 × 10)
- [RES_0X4031_D](#table-res-0x4031-d) (2 × 10)
- [RES_0X4032_D](#table-res-0x4032-d) (24 × 10)
- [RES_0X4033_D](#table-res-0x4033-d) (34 × 10)
- [RES_0X4034_D](#table-res-0x4034-d) (30 × 10)
- [RES_0X4035_D](#table-res-0x4035-d) (30 × 10)
- [RES_0X4036_D](#table-res-0x4036-d) (34 × 10)
- [RES_0XB008_R](#table-res-0xb008-r) (3 × 13)
- [RES_0XB009_R](#table-res-0xb009-r) (1 × 13)
- [RES_0XE152_D](#table-res-0xe152-d) (1 × 10)
- [RES_0XE155_D](#table-res-0xe155-d) (5 × 10)
- [RES_0XE156_D](#table-res-0xe156-d) (17 × 10)
- [RES_0XE157_D](#table-res-0xe157-d) (5 × 10)
- [RES_0XE158_D](#table-res-0xe158-d) (17 × 10)
- [RES_0XE159_D](#table-res-0xe159-d) (5 × 10)
- [RES_0XE15A_D](#table-res-0xe15a-d) (17 × 10)
- [RES_0XE15B_D](#table-res-0xe15b-d) (5 × 10)
- [RES_0XE15C_D](#table-res-0xe15c-d) (17 × 10)
- [RES_0XE15E_D](#table-res-0xe15e-d) (1 × 10)
- [RES_0XE160_D](#table-res-0xe160-d) (1 × 10)
- [RES_0XE162_D](#table-res-0xe162-d) (1 × 10)
- [RES_0XE164_D](#table-res-0xe164-d) (5 × 10)
- [RES_0XE165_D](#table-res-0xe165-d) (12 × 10)
- [RES_0XE167_D](#table-res-0xe167-d) (1 × 10)
- [RES_0XE168_D](#table-res-0xe168-d) (18 × 10)
- [RES_0XE169_D](#table-res-0xe169-d) (1 × 10)
- [RES_0XE16E_D](#table-res-0xe16e-d) (18 × 10)
- [RES_0XE16F_D](#table-res-0xe16f-d) (18 × 10)
- [RES_0XE170_D](#table-res-0xe170-d) (1 × 10)
- [RES_0XE171_D](#table-res-0xe171-d) (1 × 10)
- [RES_0XE172_D](#table-res-0xe172-d) (18 × 10)
- [RES_0XE173_D](#table-res-0xe173-d) (9 × 10)
- [RES_0XE174_D](#table-res-0xe174-d) (9 × 10)
- [RES_0XE175_D](#table-res-0xe175-d) (7 × 10)
- [RES_0XE176_D](#table-res-0xe176-d) (7 × 10)
- [RES_0XE177_D](#table-res-0xe177-d) (12 × 10)
- [RES_0XE1A3_D](#table-res-0xe1a3-d) (17 × 10)
- [RES_0XE1A4_D](#table-res-0xe1a4-d) (17 × 10)
- [RES_0XE1A5_D](#table-res-0xe1a5-d) (17 × 10)
- [RES_0XE1A6_D](#table-res-0xe1a6-d) (17 × 10)
- [RES_0XE1A7_D](#table-res-0xe1a7-d) (12 × 10)
- [RES_0XFD06_D](#table-res-0xfd06-d) (23 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (96 × 16)
- [SVK_VERSION_DOP](#table-svk-version-dop) (2 × 2)
- [TAB_MR_ARG_AKTIV_LIN](#table-tab-mr-arg-aktiv-lin) (4 × 2)
- [TAB_MR_ARG_BEH_HORN_EMULATION](#table-tab-mr-arg-beh-horn-emulation) (4 × 2)
- [TAB_MR_ARG_BEREICH_GESCHWINDIGKEIT](#table-tab-mr-arg-bereich-geschwindigkeit) (4 × 2)
- [TAB_MR_ARG_BKL_HELLIGKEIT](#table-tab-mr-arg-bkl-helligkeit) (4 × 2)
- [TAB_MR_ARG_BKL_SOFU](#table-tab-mr-arg-bkl-sofu) (8 × 2)
- [TAB_MR_ARG_BKL_SYNC](#table-tab-mr-arg-bkl-sync) (4 × 2)
- [TAB_MR_ARG_BLITZMUSTER](#table-tab-mr-arg-blitzmuster) (8 × 2)
- [TAB_MR_ARG_COUNTRY_CODE](#table-tab-mr-arg-country-code) (15 × 2)
- [TAB_MR_ARG_HUPE_LIN](#table-tab-mr-arg-hupe-lin) (4 × 2)
- [TAB_MR_ARG_KL_15_LIN](#table-tab-mr-arg-kl-15-lin) (4 × 2)
- [TAB_MR_ARG_KL_ZWANG](#table-tab-mr-arg-kl-zwang) (4 × 2)
- [TAB_MR_ARG_MMC_TASTER](#table-tab-mr-arg-mmc-taster) (4 × 2)
- [TAB_MR_ARG_TASTER_LIN](#table-tab-mr-arg-taster-lin) (4 × 2)
- [TAB_MR_ARG_TSA_VOLUME](#table-tab-mr-arg-tsa-volume) (16 × 2)
- [TAB_MR_AUDIO_MENUE](#table-tab-mr-audio-menue) (4 × 2)
- [TAB_MR_BEH_HORN_EMULATION](#table-tab-mr-beh-horn-emulation) (4 × 2)
- [TAB_MR_DESIGN](#table-tab-mr-design) (4 × 2)
- [TAB_MR_HUPE_LIN](#table-tab-mr-hupe-lin) (4 × 2)
- [TAB_MR_KL50](#table-tab-mr-kl50) (4 × 2)
- [TAB_MR_LIN_FEHLER](#table-tab-mr-lin-fehler) (4 × 2)
- [TAB_MR_LIN_LEUCHTEN](#table-tab-mr-lin-leuchten) (4 × 2)
- [TAB_MR_PINZUORDNUNG](#table-tab-mr-pinzuordnung) (4 × 2)
- [TAB_MR_RES_ABL_STATUS](#table-tab-mr-res-abl-status) (4 × 2)
- [TAB_MR_RES_AKTIV_LIN](#table-tab-mr-res-aktiv-lin) (4 × 2)
- [TAB_MR_RES_AUDIO_MENUE_CAN](#table-tab-mr-res-audio-menue-can) (4 × 2)
- [TAB_MR_RES_BEH_HORN_EMULATION](#table-tab-mr-res-beh-horn-emulation) (4 × 2)
- [TAB_MR_RES_BKL_FARBEN](#table-tab-mr-res-bkl-farben) (4 × 2)
- [TAB_MR_RES_BKL_HELLIGKEIT](#table-tab-mr-res-bkl-helligkeit) (4 × 2)
- [TAB_MR_RES_BKL_SOFU](#table-tab-mr-res-bkl-sofu) (8 × 2)
- [TAB_MR_RES_BKL_SYNC](#table-tab-mr-res-bkl-sync) (4 × 2)
- [TAB_MR_RES_BKL_TYP](#table-tab-mr-res-bkl-typ) (4 × 2)
- [TAB_MR_RES_BLINKER_STATUS](#table-tab-mr-res-blinker-status) (8 × 2)
- [TAB_MR_RES_BLITZMUSTER](#table-tab-mr-res-blitzmuster) (8 × 2)
- [TAB_MR_RES_BREMSL_STATUS](#table-tab-mr-res-bremsl-status) (4 × 2)
- [TAB_MR_RES_BU_ALT_FRONTL](#table-tab-mr-res-bu-alt-frontl) (4 × 2)
- [TAB_MR_RES_COUNTRY_CODE](#table-tab-mr-res-country-code) (15 × 2)
- [TAB_MR_RES_DESIGN](#table-tab-mr-res-design) (4 × 2)
- [TAB_MR_RES_ELA](#table-tab-mr-res-ela) (4 × 2)
- [TAB_MR_RES_FL_STATUS](#table-tab-mr-res-fl-status) (4 × 2)
- [TAB_MR_RES_GESCHWINDIGKEIT_BEREICH](#table-tab-mr-res-geschwindigkeit-bereich) (4 × 2)
- [TAB_MR_RES_HELMSTATUS](#table-tab-mr-res-helmstatus) (4 × 2)
- [TAB_MR_RES_HOLD_SIG](#table-tab-mr-res-hold-sig) (4 × 2)
- [TAB_MR_RES_HORN](#table-tab-mr-res-horn) (4 × 2)
- [TAB_MR_RES_KL15_LIN](#table-tab-mr-res-kl15-lin) (4 × 2)
- [TAB_MR_RES_KL50](#table-tab-mr-res-kl50) (4 × 2)
- [TAB_MR_RES_KL_15_LIN](#table-tab-mr-res-kl-15-lin) (4 × 2)
- [TAB_MR_RES_KL_ZWANG](#table-tab-mr-res-kl-zwang) (4 × 2)
- [TAB_MR_RES_LEUCHTEN_FEHLER](#table-tab-mr-res-leuchten-fehler) (4 × 2)
- [TAB_MR_RES_LICHT_AUS](#table-tab-mr-res-licht-aus) (4 × 2)
- [TAB_MR_RES_LIN_AKTIVIERUNGSZUSTAND](#table-tab-mr-res-lin-aktivierungszustand) (4 × 2)
- [TAB_MR_RES_LIN_FEHLER](#table-tab-mr-res-lin-fehler) (4 × 2)
- [TAB_MR_RES_MMC_TASTER](#table-tab-mr-res-mmc-taster) (4 × 2)
- [TAB_MR_RES_PARAMETERSTATUS](#table-tab-mr-res-parameterstatus) (4 × 2)
- [TAB_MR_RES_PRES_MODUS](#table-tab-mr-res-pres-modus) (4 × 2)
- [TAB_MR_RES_SONDERBLINKEN](#table-tab-mr-res-sonderblinken) (8 × 2)
- [TAB_MR_RES_TASTER_CAN](#table-tab-mr-res-taster-can) (4 × 2)
- [TAB_MR_RES_TASTER_LIN](#table-tab-mr-res-taster-lin) (4 × 2)
- [TAB_MR_RES_TFL_STATUS](#table-tab-mr-res-tfl-status) (4 × 2)
- [TAB_MR_RES_TSA_VOLUME](#table-tab-mr-res-tsa-volume) (16 × 2)
- [TAB_MR_RES_ZUSTAND_KENNLEUCHTEN](#table-tab-mr-res-zustand-kennleuchten) (3 × 2)
- [TAB_MR_ROUTINE_BCA](#table-tab-mr-routine-bca) (5 × 2)
- [TAB_MR_TASTER_LIN](#table-tab-mr-taster-lin) (4 × 2)
- [TAB_MR_TSA_CODE](#table-tab-mr-tsa-code) (15 × 2)
- [TAB_MR_TSA_VOLUME](#table-tab-mr-tsa-volume) (16 × 2)
- [TAB_MR_ZUSTAND_KENNLEUCHTE](#table-tab-mr-zustand-kennleuchte) (3 × 2)

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

Dimensions: 140 rows × 2 columns

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 248 rows × 3 columns

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
| 0x0F80 | Frontview Kamera vorne | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1210 | Sideview Kamera Kotflügel vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1310 | Sideview Kamera Kotflügel vorne rechts | 1 |
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
| 0x3D80 | Lüfter | 1 |
| 0x3D88 | Lüfter 2 | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3E80 | DCDC Versorgung Zustartbatterie | 1 |
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
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x6500 | Sense-Touch-Modul links | 1 |
| 0x6600 | Sense-Touch-Modul rechts | 1 |
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
| 0x5782 | Fussgängerschutz Zusatzsensor Beschleunigung links | 0 |
| 0x5784 | Fussgängerschutz Zusatzsensor Beschleunigung rechts | 0 |
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
| 0x5A01 | Innenbeleuchtung - Lichtschwert links | 1 |
| 0x5A02 | Innenbeleuchtung - Lichtschwert rechts | 1 |
| 0x5A03 | Innenbeleuchtung - Lautsprecher Hutablage rechts | 1 |
| 0x5A04 | Innenbeleuchtung - Lautsprecher Hutablage links | 1 |
| 0x5A05 | Innenbeleuchtung - Lautsprecher hinten links | 1 |
| 0x5A06 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne links | 1 |
| 0x5A07 | Innenbeleuchtung - Lautsprecher Hochtöner vorne links | 1 |
| 0x5A08 | Innenbeleuchtung - Lautsprecher hinten rechts | 1 |
| 0x5A09 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne rechts | 1 |
| 0x5A0A | Innenbeleuchtung - Lautsprecher Hochtöner vorne rechts | 1 |
| 0x5A0B | Innenbeleuchtung - Lautsprecher Centerspeaker | 1 |
| 0x5A0C | Innenbeleuchtung - Panoramadach LED Modul 1 (hinteres Glasfestelement) | 1 |
| 0x5A0D | Innenbeleuchtung - Panoramadach LED Modul 2 (hinteres Glasfestelement) | 1 |
| 0x5A0E | Innenbeleuchtung - Panoramadach LED Modul 3 (hinteres Glasfestelement) | 1 |
| 0x5A0F | Innenbeleuchtung - Panoramadach LED Modul 4 (hinteres Glasfestelement) | 1 |
| 0x5A10 | Innenbeleuchtung - Panoramadach LED Modul 5 (vorderes Glasschiebedach) | 1 |
| 0x5A11 | Innenbeleuchtung - Panoramadach LED Modul 6 (vorderes Glasschiebedach) | 1 |
| 0x5A12 | Innenbeleuchtung - Panoramadach LED Modul 7 (vorderes Glasschiebedach) | 1 |
| 0x5A13 | Innenbeleuchtung - Panoramadach LED Modul 8 (vorderes Glasschiebedach) | 1 |
| 0x5A14 | Touch Command Snap-In Adapter - Mittelkonsole Fond | 1 |
| 0x5A20 | Innenlichteinheit 2 | 1 |
| 0x5A30 | Innenlichteinheit 3 | 1 |
| 0x5AFF | unbekannter Verbauort | - |
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
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
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
| 0x5F00 | Integrierte Fensterheber Elektronik Fahrer | 1 |
| 0x5F10 | Integrierte Fensterheber Elektronik Beifahrer | 1 |
| 0x5F20 | Integrierte Fensterheber Elektronik Fahrer hinten | 1 |
| 0x5F30 | Integrierte Fensterheber Elektronik Beifahrer hinten | 1 |
| 0x5F40 | Schalterblock Sitzmemory Fahrer | 1 |
| 0x5F50 | Schalterblock Sitzmemory Beifahrer | 1 |
| 0x5F60 | Schalterblock Sitzmemory Fahrer hinten | 1 |
| 0x5F70 | Schalterblock Sitzmemory Beifahrer hinten | 1 |
| 0x5F80 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x5F90 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x5FA0 | Bedieneinheit Mittelkonsole | 1 |
| 0x5FB0 | WB und SARAH Schalter | 1 |
| 0x5FC0 | ABW-Türschloss Fahrer | 1 |
| 0x5FD0 | ABW-Türschloss Beifahrer | 1 |
| 0x7000 | Abschattungs-Elektronik-Dach | 1 |
| 0x7040 | Frontwischermotor | 1 |
| 0x7100 | NFC Leser Innenraum vorne | 1 |
| 0x7108 | NFC Leser Türgriff Fahrer | 1 |
| 0x7200 | Spurwechselradarsensor vorne rechts | 1 |
| 0x7208 | Spurwechselradarsensor vorne links | 1 |
| 0x7210 | Spurwechselradarsensor hinten rechts (Master) | 1 |
| 0x7218 | Spurwechselradarsensor hinten links | 1 |
| 0x7300 | Tanksensor links | 1 |
| 0x7310 | Tanksensor rechts | 1 |
| 0x7400 | Cargo Steuergeraet | 1 |
| 0x7500 | CID-Klappe | 1 |
| 0x7600 | Handschuhkasten | 1 |
| 0x7700 | Booster | - |
| 0x7800 | Dualspeicher | 1 |
| 0x7900 | Tablet | - |
| 0x7A00 | Beschleunigungssensor vorne links | 1 |
| 0x7A08 | Beschleunigungssensor vorne rechts | 1 |
| 0x7A10 | Beschleunigungssensor hinten links | 1 |
| 0x7A18 | Beschleunigungssensor hinten rechts | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 206 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | Daimler AG |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars |
| 0x0008 | Ford Motor Company |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis GmbH |
| 0x0014 | Microchip Technology Inc |
| 0x0015 | Centro Ricerche FIAT |
| 0x0016 | Renesas Technology Europe GmbH - Mitsubishi |
| 0x0017 | Atmel Germany GmbH |
| 0x0018 | Magneti Marelli S.p. A |
| 0x0019 | NEC Electronics GmbH |
| 0x001A | Fujitsu Microelectronics Europe GmbH |
| 0x001B | Adam Opel AG |
| 0x001C | Infineon Technologies AG |
| 0x001D | AMI Semiconductor Belguim BVBA |
| 0x001E | Vector Informatik GmbH |
| 0x001F | Brose Fahrzeugteile GmbH & Co |
| 0x0020 | Zentrum Mikroelektronik Dresden AG |
| 0x0021 | ihr GmbH |
| 0x0022 | Visteon Deutschland GmbH |
| 0x0023 | Elmos Semiconductor AG |
| 0x0024 | ON Semiconductor Germany GmbH |
| 0x0025 | Denso Corporation |
| 0x0026 | C&S Group GmbH |
| 0x0027 | Renault SA |
| 0x0028 | Renesas Technology Europe Ltd  - Hitachi |
| 0x0029 | Yazaki Europe Ltd |
| 0x002A | Trinamic Microchips GmbH |
| 0x002B | Allegro Microsystems, Inc |
| 0x002C | Toyota Motor Engineering and Manufacturing Europe N.V / S.A |
| 0x002D | PSA Peugeot Citroën |
| 0x002E | Forschungs - und Transferzentrum e.V. der Westsächsische Hochschule Zwickau |
| 0x002F | Micron Electronic Devices AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA & Co. |
| 0x0037 | Continental Automotive |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH - Robert Bosch |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electrics Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | DST Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies, Inc. |
| 0x0055 | Lear Corporation  |
| 0x0056 | KOSTAL Ireland GmbH |
| 0x0057 | LIPOWSKY Industrie-Elektronik GmbH  |
| 0x0058 | Sanken Electric Co.,Ltd |
| 0x0059 | Elektrobit Automotive GmbH |
| 0x005A | VIMERCATI S.p.A. |
| 0x005B | VOLVO Group Trucks |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic GmbH & Co. KG |
| 0x0061 | Flextronics / Sidler Automotive GmbH & Co. KG |
| 0x0062 | EAO Automotive GmbH & Co. KG |
| 0x0063 | helag-electronic gmbh |
| 0x0064 | Magna Electronics |
| 0x0065 | INTEVA Products, LLC |
| 0x0066 | Valeo SA |
| 0x0067 | Defond Holding / BJAutomotive / DAC |
| 0x0068 | Industrie Saleri S. p. A. |
| 0x0069 | ROHM Semicon GmbH |
| 0x0070 | Alfmeier Präzision AG |
| 0x0071 | Sanden Corporation |
| 0x0072 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x0073 | ebm-papst St. Georgen GmbH & Co. KG |
| 0x0074 | CATEM |
| 0x0075 | OMRON Automotive Electronics Technology GmbH |
| 0x0076 | Johnson Electric International |
| 0x0077 | A123 Systems |
| 0x0078 | IPG Automotive GmbH, Karlsruhe |
| 0x0079 | Daesung Electric Co. Ltd. |
| 0x007A | Kromberg & Schubert GmbH & Co. KG |
| 0x007B | Bury GmbH & Co. KG |
| 0x007E | Measurement Specialties Inc (MEAS) |
| 0x007F | MRS Electronic GmbH |
| 0x0082 | Dale Electronics Inc |
| 0x0083 | Mirror Controls international |
| 0x0084 | Keboda Technology Co. Ltd. |
| 0x0085 | SPD Control Systems Corporation |
| 0x0087 | Röchling Automotive AG & Co. KG |
| 0x0088 | AEV s.r.o |
| 0x0089 | Kongsberg Automotive AB/Mullsjö Works |
| 0x008A | May & Scofield Ltd |
| 0x008C | C&S Technology Inc |
| 0x008D | RDC Semiconductor Co., Ltd |
| 0x008E | Webasto AG |
| 0x008F | Accel Elektronika UAB |
| 0x0090 | FICOSA International S.A. |
| 0x0091 | Mahle |
| 0x0093 | Phoenix International |
| 0x0094 | John Deere |
| 0x0095 | Grayhill Inc |
| 0x0096 | AppliedSensor GmbH |
| 0x0097 | UST Umweltsensortechnik GmbH |
| 0x0098 | Digades GmbH |
| 0x0099 | Thomson Linear Motion |
| 0x009A | TriMark Corporation |
| 0x009B | KB Auto Tech Co., Ltd. |
| 0x009C | Methode Electronics, Inc |
| 0x009D | Danlaw, Inc. |
| 0x009E | Federal-Mogul Corporation |
| 0x009F | Fujikoki Corporation |
| 0x00A0 | MENTOR Gmbh & Co. Praezisions-Bauteile KG |
| 0x00A1 | Toyota Industries Corporation |
| 0x00A2 | Strattec Security Corp. |
| 0x00A3 | TE Connectivity |
| 0x00A4 | Westfalia Automotive GmbH |
| 0x00A5 | Woco Industrietechnik GmbH |
| 0x00A6 | Minebea Co., Ltd |
| 0x00A7 | Magna |
| 0x00A8 | Dong IL Technology |
| 0x00A9 | Wilo SE |
| 0x00AA | Remy International, Inc. |
| 0x00AB | ACCUmotive |
| 0x00AC | Carling Technologies |
| 0x0100 | Isabellenhuette Heusler GmbH & Co. KG |
| 0x0101 | Huber Automotive AG |
| 0x0102 | Precision Motors Deutsche Minebea GmbH |
| 0x0103 | TK Holdings Inc., Electronics |
| 0x0104 | Cobra Automotive Technologies S.P.A. |
| 0x0105 | Embed Limited |
| 0x0106 | Kissling Elektrotechnik GmbH |
| 0x0107 | Autoliv B.V. & Co. KG |
| 0x0108 | PST Electronics |
| 0x0109 | BCA Leisure Ltd |
| 0x010A | APAG Elektronik AG |
| 0x010B | RAFI GmbH & Co. KG |
| 0x010C | Sonceboz AutomotiveSA |
| 0x010D | i2s Intelligente Sensorsysteme Dresden GmbH |
| 0x010E | AGM Automotive, Inc. |
| 0x010F | S&T Motiv |
| 0x0111 | UG Systems GmbH & Co. KG |
| 0x0113 | CHANGJIANG AUTOMOBILE ELECTRONIC SYSTEM CO.,LTD |
| 0x0114 | MES S.A. |
| 0x0115 | SL Corporation |
| 0x0116 | Dura Automotive Systems |
| 0x0118 | Delta Electronics, Inc. |
| 0x0119 | Penny and Giles Controls Ltd |
| 0x011A | Curtiss Wright Controls Industrial |
| 0x011B | HKR Seuffer Automotive GmbH & Co. KG |
| 0x011C | DMK U.S.A. Inc |
| 0x0120 | Littelfuse |
| 0x0121 | Hyundai MOBIS |
| 0x0122 | Alpine Electronics of America |
| 0x0123 | Ford Motor Company |
| 0x0124 | Hangzhou Sanhua Research Inst. Co, Ltd. |
| 0x0125 | Delvis |
| 0x0126 | Louko |
| 0x0127 | Etratech |
| 0x0128 | HiRain |
| 0x0129 | elobau GmbH & Co. KG |
| 0x012A | I.G.Bauerhin GmbH |
| 0x012B | HANS WIDMAIER  |
| 0x012C | Gentherm Inc |
| 0x012D | LINAK A/S |
| 0x012E | Casco Products Corporation |
| 0x012F | Bühler Motor GmbH |
| 0x0130 | SphereDesign GmbH |
| 0x0131 | Cooper Standard |
| 0x0132 | KÜSTER Automotive Control Systems GmbH |
| 0x0133 | SEWS-Components Europe B.V. |
| 0x0134 | OLHO tronic GmbH |
| 0x0135 | LG Electronics |
| 0x0136 | Eberspächer Controls GmbH & Co. KG |
| 0x0137 | AISIN Seiki Co., Ltd. |
| 0x0138 | Elektrosil Systeme der Elektronik GmbH |
| 0x0139 | Nidec Corporation |
| 0x013A | ISSI – Integrated Silicon Solution Inc |
| 0x013B | Twin Disc, Incorporated |
| 0x013C | SPAL Automotive Srl |
| 0x013D | OTTO Engineering, Inc. |
| 0xFFFF | unbekannter Hersteller |

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

<a id="table-arg-0x4001-d"></a>
### ARG_0X4001_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KL_50_ENTLASTUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung der Funktion Entlastung bei KL_50: 0 = nicht aktiv, 1 = aktiv |

<a id="table-arg-0x4003-d"></a>
### ARG_0X4003_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTION_SPANNUNGSVERSORGUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung der Funktion Spannungsversorgung Zusatzschaltereinheit: 0 = nicht aktiv, 1 = aktiv |

<a id="table-arg-0x4005-d"></a>
### ARG_0X4005_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Licht aus: 0 = aus, 1 = ein |

<a id="table-arg-0x4007-d"></a>
### ARG_0X4007_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTION_NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Nebelschlussleuchte: 0 = aus, 1 = ein |

<a id="table-arg-0x4009-d"></a>
### ARG_0X4009_D

Dimensions: 5 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTION_KENNLEUCHTEN_ALLGEMEIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Kennleuchten allgemein: 0 = aus, 1 = ein |
| ZUSTAND_KENNLEUCHTE_VORNE_LINKS | 0-n | high | unsigned char | - | TAB_MR_ZUSTAND_KENNLEUCHTE | - | - | - | - | - | Kennleuchtenzustand vorne links |
| ZUSTAND_KENNLEUCHTE_VORNE_RECHTS | 0-n | high | unsigned char | - | TAB_MR_ZUSTAND_KENNLEUCHTE | - | - | - | - | - | Kennleuchtenzustand vorne rechts |
| ZUSTAND_KENNLEUCHTE_HINTEN_LINKS | 0-n | high | unsigned char | - | TAB_MR_ZUSTAND_KENNLEUCHTE | - | - | - | - | - | Kennleuchtenzustand hinten links |
| ZUSTAND_KENNLEUCHTE_HINTEN_RECHTS | 0-n | high | unsigned char | - | TAB_MR_ZUSTAND_KENNLEUCHTE | - | - | - | - | - | Kennleuchtenzustand hinten rechts |

<a id="table-arg-0x400b-d"></a>
### ARG_0X400B_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion LED Blitzkennleuchte vorne links (Pin 3): 0 = aus, 1 = ein  |

<a id="table-arg-0x400d-d"></a>
### ARG_0X400D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion LED Blitzkennleuchte vorne rechts (Pin 2): 0 = aus, 1 = ein  |

<a id="table-arg-0x400f-d"></a>
### ARG_0X400F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Rundumkennleuchte hinten links (Pin 20): 0 = aus, 1 = ein  |

<a id="table-arg-0x4011-d"></a>
### ARG_0X4011_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Rundumkennleuchte hinten rechts (Pin 7): 0 = aus, 1 = ein  |

<a id="table-arg-0x4013-d"></a>
### ARG_0X4013_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_STOP_VORNE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Anhaltesignal vorne Stop (Pin 23) 0 = aus, 1 = ein |

<a id="table-arg-0x4015-d"></a>
### ARG_0X4015_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Anhaltesignal hinten Stop (Pin 36) 0 = aus, 1 = ein |

<a id="table-arg-0x4017-d"></a>
### ARG_0X4017_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Anhaltesignal hinten Bitte folgen (Pin 35) 0 = aus, 1 = ein |

<a id="table-arg-0x4019-d"></a>
### ARG_0X4019_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Activation Function Key: 0 = off, 1 = on |

<a id="table-arg-0x401b-d"></a>
### ARG_0X401B_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Activation Function Key: 0 = off, 1 = on |

<a id="table-arg-0x401d-d"></a>
### ARG_0X401D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Activation Function Key: 0 = off, 1 = on |

<a id="table-arg-0x401f-d"></a>
### ARG_0X401F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Activation Function Key: 0 = off, 1 = on |

<a id="table-arg-0x4021-d"></a>
### ARG_0X4021_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Tonsignalanlage (Pin 1): 0 = aus, 1 = ein |

<a id="table-arg-0x4023-d"></a>
### ARG_0X4023_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKANLAGE_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Funkanlage (Pin 5): 0 = aus, 1 = ein |

<a id="table-arg-0x4025-d"></a>
### ARG_0X4025_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KL15_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion KL15 (Pin 33): 0 = aus, 1 = ein |

<a id="table-arg-0x4027-d"></a>
### ARG_0X4027_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KL30_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion KL30: 0 = aus, 1 = ein |

<a id="table-arg-0x4029-d"></a>
### ARG_0X4029_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BEHOERDENRELAIS_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Behördenrelais (Pin 37): 0 = aus, 1 = ein |

<a id="table-arg-0x402b-d"></a>
### ARG_0X402B_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHUTZ_TIEFENTLADUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Schutz vor Tiefentladung: 0 = aus, 1 = ein |

<a id="table-arg-0x402d-d"></a>
### ARG_0X402D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ABSCHALTUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Überspannungsabschaltung: 0 = aus, 1 = ein |

<a id="table-arg-0x402f-d"></a>
### ARG_0X402F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ABSCHALTUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Unterspannungsabschaltung: 0 = aus, 1 = ein |

<a id="table-arg-0x4031-d"></a>
### ARG_0X4031_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTION_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktion Alternierendes Frontlicht: 0 = aus, 1 = ein |

<a id="table-arg-0x4033-d"></a>
### ARG_0X4033_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PIN_20_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 20 (Helm Headset) 0 = aus, 1 = ein |
| PIN_34_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 34 (PTPA) 0 = aus, 1 = ein |
| PIN_36_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 36 (Zubehör III) 0 = aus, 1 = ein |
| PIN_47_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 47 (Kartenlicht) 0 = aus, 1 = ein |
| PIN_23_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 23 (PTT1) 0 = aus, 1 = ein |
| PIN_9_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 9 (Funk) 0 = aus, 1 = ein |
| PIN_33_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 33 (Zubehör I) 0 = aus, 1 = ein |
| PIN_21_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 21 (PTT2) 0 = aus, 1 = ein |

<a id="table-arg-0x4036-d"></a>
### ARG_0X4036_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PIN_35_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 35 (Zubehör II) 0 = aus, 1 = ein |
| PIN_1_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 1 (Sirene) 0 = aus, 1 = ein |
| PIN_2_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 2 (TDL) 0 = aus, 1 = ein |
| PIN_3_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 3 (Radar) 0 = aus, 1 = ein |
| PIN_5_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 5 (LED Steuergerät) 0 = aus, 1 = ein |
| PIN_46_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 46 (Waffenverriegelung) 0 = aus, 1 = ein |
| PIN_8_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 8 (P-Schalter) 0 = aus, 1 = ein |
| PIN_7_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Pin 7 (Lautsprecher) 0 = aus, 1 = ein |

<a id="table-arg-0xe152-d"></a>
### ARG_0XE152_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Nebelschlussleuchte 0 = aus, 1 = ein |

<a id="table-arg-0xe156-d"></a>
### ARG_0XE156_D

Dimensions: 9 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_BLITZKENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Blitzkennleuchte vorne links: 0 = aus, 1 = ein |
| BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BLITZMUSTER | - | - | - | - | - | Ansteuerung Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SYNC | - | - | - | - | - | Ansteuerung Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SOFU | - | - | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_HELLIGKEIT | - | - | - | - | - | Ansteuerung Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |

<a id="table-arg-0xe158-d"></a>
### ARG_0XE158_D

Dimensions: 9 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_BLITZKENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Blitzkennleuchte vorne rechts: 0 = aus, 1 = ein |
| BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BLITZMUSTER | - | - | - | - | - | Ansteuerung Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SYNC | - | - | - | - | - | Ansteuerung Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SOFU | - | - | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_HELLIGKEIT | - | - | - | - | - | Ansteuerung Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |

<a id="table-arg-0xe15a-d"></a>
### ARG_0XE15A_D

Dimensions: 9 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_BLITZKENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Blitzkennleuchte hinten links 0 = aus, 1 = ein |
| BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BLITZMUSTER | - | - | - | - | - | Ansteuerung Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SYNC | - | - | - | - | - | Ansteuerung Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SOFU | - | - | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_HELLIGKEIT | - | - | - | - | - | Ansteuerung Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |

<a id="table-arg-0xe15c-d"></a>
### ARG_0XE15C_D

Dimensions: 9 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_BLITZKENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Blitzkennleuchte hinten rechts: 0 = aus, 1 = ein |
| BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BLITZMUSTER | - | - | - | - | - | Ansteuerung Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SYNC | - | - | - | - | - | Ansteuerung Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_SOFU | - | - | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_ARG_BKL_HELLIGKEIT | - | - | - | - | - | Ansteuerung Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |

<a id="table-arg-0xe15e-d"></a>
### ARG_0XE15E_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_STOP_VORNE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Anhaltesignal STOP vorne 0 = aus, 1 = ein |

<a id="table-arg-0xe160-d"></a>
### ARG_0XE160_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Anhaltesignal hinten STOP 0 = aus, 1 = ein |

<a id="table-arg-0xe162-d"></a>
### ARG_0XE162_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Status Anhaltesignal: 0 = aus, 1 = ein |

<a id="table-arg-0xe165-d"></a>
### ARG_0XE165_D

Dimensions: 5 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Versorgungspin Tonsignalanlage 0 = aus, 1 = ein |
| LAENDERCODE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_ARG_COUNTRY_CODE | - | - | - | - | - | Ländercode Tonsequenz (LIN Signal CTR_CNCD_TOSQ_MOTBK_2010) |
| LAUTSTAERKE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_ARG_TSA_VOLUME | - | - | - | - | - | Ländercode Tonsequenz (LIN Signal CTR_CNCD_TOSQ_MOTBK_2010) |
| HUPE_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_HUPE_LIN | - | - | - | - | - | Hupe aktiv (LIN Signal CTR_HORN_TOSQ_MOTBK_2010) |
| HUPENEMULATION_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_BEH_HORN_EMULATION | - | - | - | - | - | Hupenemulation aktiv (LIN Signal CTR_SUBST_HORN_TOSQ_MOTBK_2010) |

<a id="table-arg-0xe167-d"></a>
### ARG_0XE167_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BEHOERDENRELAIS | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang Behördenrelais 0 = aus, 1 = ein |

<a id="table-arg-0xe168-d"></a>
### ARG_0XE168_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktionstaster: 0 = aus, 1 = ein |

<a id="table-arg-0xe169-d"></a>
### ARG_0XE169_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| WERKSTATTMODUS_EIN | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktivierung Werkstattmodus: 0 = aus, 1 = ein |

<a id="table-arg-0xe16e-d"></a>
### ARG_0XE16E_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktionstaster: 0 = aus, 1 = ein |

<a id="table-arg-0xe16f-d"></a>
### ARG_0XE16F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktionstaster: 0 = aus, 1 = ein |

<a id="table-arg-0xe170-d"></a>
### ARG_0XE170_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KL30_BEH | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausgang KL30 Behörde: 0 = aus, 1 = ein |

<a id="table-arg-0xe171-d"></a>
### ARG_0XE171_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KL15_BEH | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Klemme 15 Behörde: 0 = aus, 1 = ein |

<a id="table-arg-0xe172-d"></a>
### ARG_0XE172_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Funktionstaster: 0 = aus, 1 = ein |

<a id="table-arg-0xe175-d"></a>
### ARG_0XE175_D

Dimensions: 7 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_SCHALTERBLOCK | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Schalterblock 0 = aus, 1 = ein |
| PWM_SSL_TOP_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (A) der oberen Wippe am linken Schalterblock |
| PWM_SSL_TOP_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (B) der oberen Wippe am linken Schalterblock |
| PWM_SSL_MIDDLE_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (C) der mittleren Wippe am linken Schalterblock |
| PWM_SSL_MIDDLE_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (D) der mittleren Wippe am linken Schalterblock |
| PWM_SSL_BOTTOM_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (E) der unteren Wippe am linken Schalterblock |
| PWM_SSL_BOTTOM_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (F) der unteren Wippe am linken Schalterblock |

<a id="table-arg-0xe176-d"></a>
### ARG_0XE176_D

Dimensions: 7 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_SCHALTERBLOCK | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Schalterblock 0 = aus, 1 = ein |
| PWM_SSR_TOP_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (I) der oberen Wippe am rechten Schalterblock |
| PWM_SSR_TOP_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (J) der oberen Wippe am rechten Schalterblock |
| PWM_SSR_MIDDLE_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (K) der mittleren Wippe am rechten Schalterblock |
| PWM_SSR_MIDDLE_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (L) der mittleren Wippe am rechten Schalterblock |
| PWM_SSR_BOTTOM_UP_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der oberen Taste (M) der unteren Wippe am rechten Schalterblock |
| PWM_SSR_BOTTOM_DOWN_WERT | % | high | unsigned char | - | - | 254.0 | 100.0 | 0.0 | 0.0 | 100.0 | PWM Wert Beleuchtung der unteren Taste (N) der unteren Wippe am rechten Schalterblock |

<a id="table-arg-0xe177-d"></a>
### ARG_0XE177_D

Dimensions: 10 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSORGUNG_FUNKANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuerung Versorgungspin Funkanlage: 0 = aus, 1 = ein |
| KL_15_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_KL_15_LIN | - | - | - | - | - | Ansteuerung LIN Signal ST_KL_15_MOTBK_2010 |
| TASTE_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktiviert die Taste PTT1 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| TASTE_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktiviert die Taste PTT2 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| TASTE_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktiviert die Taste PTT3 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| TASTE_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Sendet SIGNAL UNGÜLTIG in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| BEREICH_GESCHWINDIGKEIT | 0-n | high | unsigned char | - | TAB_MR_ARG_BEREICH_GESCHWINDIGKEIT | - | - | - | - | - | Sendet den aktuellen Geschwindigkeitsbereich im LIN Signal CTR_DOM_V_MOTBK_2010 |
| MMC_LINKS_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_MMC_TASTER | - | - | - | - | - | Ansteuerung Taster MMC links im LIN Signal CTR_MMC_LH_MOTBK_2010 |
| MMC_RECHTS_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_MMC_TASTER | - | - | - | - | - | Ansteuerung Taster MMC rechts im LIN Signal CTR_MMC_RH_MOTBK_2010 |
| MMC_POSITION | Stufen | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 254.0 | Ansteuerung MMC Position im LIN Signal CTR_MMC_PO_MOTBK_2010 |

<a id="table-arg-0xe1a3-d"></a>
### ARG_0XE1A3_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-arg-0xe1a4-d"></a>
### ARG_0XE1A4_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-arg-0xe1a5-d"></a>
### ARG_0XE1A5_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-arg-0xe1a6-d"></a>
### ARG_0XE1A6_D

Dimensions: 8 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-arg-0xe1a7-d"></a>
### ARG_0XE1A7_D

Dimensions: 7 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SSL_MIDDLE_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_TASTER_LIN | - | - | - | - | - | Ansteuerung oberen Taste (C) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_UP_MOTBK_2010) |
| SSL_MIDDLE_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_TASTER_LIN | - | - | - | - | - | Ansteuerung unteren Taste (D) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_DWN_MOTBK_2010) |
| SSL_BOTTOM_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_TASTER_LIN | - | - | - | - | - | Ansteuerung oberen Taste (E) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_UP_MOTBK_2010) |
| SSL_BOTTOM_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_TASTER_LIN | - | - | - | - | - | Ansteuerung unteren Taste (F) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_DWN_MOTBK_2010) |
| KL_15_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_KL_15_LIN | - | - | - | - | - | Ansteuerung LIN Signal ST_KL_15_MOTBK_2010 (LIN Signal ST_KL_15_MOTBK_2010) |
| KENNLEUCHTENZWANG_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_KL_ZWANG | - | - | - | - | - | Ansteuerung des LIN Signals ST_IDEN_CONN_MOTBK_2010 |
| KENNLEUCHTEN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_ARG_AKTIV_LIN | - | - | - | - | - | Ansteuerung des LIN Signals ST_IDEN_LI_MOTBK_2010 |

<a id="table-arg-0xfd06-d"></a>
### ARG_0XFD06_D

Dimensions: 20 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MANUFACTURING_DATA_1_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_2_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_3_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_4_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_5_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_6_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_7_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_8_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_9_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_10_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_11_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_12_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_13_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_14_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_15_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_16_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_17_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_18_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_19_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_20_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | End Of Line  Manufacutering data |

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

<a id="table-energiesparmode-dop"></a>
### ENERGIESPARMODE_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalmode |
| 1 | Fertigungsmode |
| 2 | Transportmode |
| 3 | Flashmode |

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

Dimensions: 164 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x025C00 | Energiesparmode aktiv | 0 |
| 0x806D80 | Codierung: Fehler bei Codierung aufgetreten | 0 |
| 0x806D81 | Codierung: Signatur für Daten ungültig | 0 |
| 0x806D82 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x806D83 | Codierung: Unplausible Daten während Transaktion | 0 |
| 0x806D84 | NVM_E_CONTROL_FAILED | 0 |
| 0x806D85 | NVM_E_ERASE_FAILED | 0 |
| 0x806D86 | NVM_E_READ_ALL_FAILED | 0 |
| 0x806D87 | NVM_E_READ_FAILED | 0 |
| 0x806D88 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x806D89 | NVM_E_WRITE_FAILED | 0 |
| 0x806D8A | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x806D8B | Klemme 15 Hardware unplausibel | 1 |
| 0x806D8C | Produktionsmode aktiv | 0 |
| 0x806D8D | Ueberspannung Batterie | 1 |
| 0x806D8E | Unterspannung Batterie | 1 |
| 0x806D8F | Anhaltesignal hinten BITTE FOLGEN: Kurzschluss nach Batterie | 0 |
| 0x806D90 | Anhaltesignal hinten BITTE FOLGEN: Kurzschluss nach Masse | 0 |
| 0x806D91 | Anhaltesignal hinten BITTE FOLGEN: Leitungsunterbrechung | 0 |
| 0x806D92 | Anhaltesignal hinten STOP Kurzschluss nach Batterie | 0 |
| 0x806D93 | Anhaltesignal hinten STOP Kurzschluss nach Masse | 0 |
| 0x806D94 | Anhaltesignal hinten STOP Leitungsunterbrechung | 0 |
| 0x806D95 | Anhaltesignal vorne STOP Kurzschluss nach Batterie | 0 |
| 0x806D96 | Anhaltesignal vorne STOP Kurzschluss nach Masse | 0 |
| 0x806D97 | Anhaltesignal vorne STOP Leitungsunterbrechung | 0 |
| 0x806D98 | Ausgang KL15 Behörde: Kurzschluss nach Batterie | 0 |
| 0x806D99 | Ausgang KL15 Behörde: Kurzschluss nach Masse | 0 |
| 0x806D9A | Ausgang KL30 Behörde: Kurzschluss nach Batterie | 0 |
| 0x806D9B | Ausgang KL30 Behörde: Kurzschluss nach Masse | 0 |
| 0x806D9C | Behördenrelais Kurzschluss nach Batterie | 0 |
| 0x806D9D | Behördenrelais Kurzschluss nach Masse | 0 |
| 0x806D9E | Behördenrelais Leitungsunterbrechung | 0 |
| 0x806D9F | Blitzkennleuchte VL: Kommunikationsfehler | 0 |
| 0x806DA0 | Blitzkennleuchte VL: Leuchte defekt | 0 |
| 0x806DA1 | Blitzkennleuchte VR: Kommunikationsfehler | 0 |
| 0x806DA2 | Blitzkennleuchte VR: Leuchte defekt | 0 |
| 0x806DA3 | Funktionstaster F2: Kurzschluss nach Batterie | 0 |
| 0x806DA4 | Funktionstaster F2: Kurzschluss nach Masse | 0 |
| 0x806DA5 | Funktionstaster F1: Kurzschluss nach Batterie | 0 |
| 0x806DA6 | Funktionstaster F1: Kurzschluss nach Masse | 0 |
| 0x806DA7 | Funktionstaster F3: Kurzschluss nach Batterie | 0 |
| 0x806DA8 | Funktionstaster F3: Kurzschluss nach Masse | 0 |
| 0x806DA9 | Funktionstaster F4: Kurzschluss nach Batterie | 0 |
| 0x806DAA | Funktionstaster F4: Kurzschluss nach Masse | 0 |
| 0x806DAB | Nebelschlussleuchte Kurzschluss nach Batterie | 0 |
| 0x806DAC | Nebelschlussleuchte Kurzschluss nach Masse | 0 |
| 0x806DAD | Nebelschlussleuchte Leitungsunterbrechung | 0 |
| 0x806DAE | Rundumkennleuchte HL: Kommunikationsfehler | 0 |
| 0x806DAF | Rundumkennleuchte HL: Leuchte defekt | 0 |
| 0x806DB0 | Rundumkennleuchte HR: Kommunikationsfehler | 0 |
| 0x806DB1 | Rundumkennleuchte HR: Leuchte defekt | 0 |
| 0x806DB2 | Schalterblock links Kommunikationsfehler | 0 |
| 0x806DB3 | Schalterblock links mittlere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DB4 | Schalterblock links obere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DB5 | Schalterblock links untere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DB6 | Schalterblock rechts Kommunikationsfehler | 0 |
| 0x806DB7 | Schalterblock rechts mittlere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DB8 | Schalterblock rechts obere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DB9 | Schalterblock rechts untere Wippe Kurzschluss zwischen Tasten oben und unten | 0 |
| 0x806DBA | Tiefentladung aktiv | 0 |
| 0x806DBB | Versorgung Blitzkennleuchte VL: Kurzschluss nach Batterie | 0 |
| 0x806DBC | Versorgung Blitzkennleuchte VL: Kurzschluss nach Masse | 0 |
| 0x806DBD | Versorgung Blitzkennleuchte VL: Leitungsunterbrechung | 0 |
| 0x806DBE | Versorgung Blitzkennleuchte VR: Kurzschluss nach Batterie | 0 |
| 0x806DBF | Versorgung Blitzkennleuchte VR: Kurzschluss nach Masse | 0 |
| 0x806DC0 | Versorgung Blitzkennleuchte VR: Leitungsunterbrechung | 0 |
| 0x806DC1 | Versorgung Funkanlage: Kurzschluss nach Batterie | 0 |
| 0x806DC2 | Versorgung Funkanlage: Kurzschluss nach Masse | 0 |
| 0x806DC3 | Versorgung Funkanlage: Leitungsunterbrechung | 0 |
| 0x806DC4 | Versorgung Rundumkennleuchte HL: Kurzschluss nach Batterie | 0 |
| 0x806DC5 | Versorgung Rundumkennleuchte HL: Kurzschluss nach Masse | 0 |
| 0x806DC6 | Versorgung Rundumkennleuchte HL: Leitungsunterbrechung | 0 |
| 0x806DC7 | Versorgung Rundumkennleuchte HR: Kurzschluss nach Batterie | 0 |
| 0x806DC8 | Versorgung Rundumkennleuchte HR Kurzschluss nach Masse | 0 |
| 0x806DC9 | Versorgung Rundumkennleuchte HR: Leitungsunterbrechung | 0 |
| 0x806DCA | Versorgung Schalterblock Kurzschluss nach Batterie | 0 |
| 0x806DCB | Versorgung Schalterblock Kurzschluss nach Masse | 0 |
| 0x806DCC | Versorgung Schalterblock Leitungsunterbrechung | 0 |
| 0x806DCD | Versorgung Tonsignalanlage Kurzschluss nach Batterie | 0 |
| 0x806DCE | Versorgung Tonsignalanlage Kurzschluss nach Masse | 0 |
| 0x806DCF | Versorgung Tonsignalanlage Leitungsunterbrechung | 0 |
| 0x806DD0 | Werkstattmodus aktiv | 0 |
| 0x806DD1 | Hardwarefehler Steuergeraet | 0 |
| 0x806DD2 | Softwarefehler Steuergeraet | 0 |
| 0x806DD3 | FLS_E_COMPARE_FAILED | 0 |
| 0x806DD4 | FLS_E_ERASE_FAILED | 0 |
| 0x806DD5 | FLS_E_READ_FAILED | 0 |
| 0x806DD6 | FLS_E_WRITE_FAILED | 0 |
| 0x806DD7 | SF LED Steuergerät: ALLEY LIGHT links defekt | 0 |
| 0x806DD8 | SF LED Steuergerät: ALLEY LIGHT rechts defekt | 0 |
| 0x806DD9 | SF LED Steuergerät: EMERGENCY LIGHT hinten defekt | 0 |
| 0x806DDA | SF LED Steuergerät: EMERGENCY LIGHT vorne links defekt | 0 |
| 0x806DDB | SF LED Steuergerät: EMERGENCY LIGHT vorne rechts defekt | 0 |
| 0x806DDC | SF LED Steuergerät: Kommunikationsfehler | 0 |
| 0x806DDD | SF LED Steuergerät: TAKEDOWN LIGHT PURSUIT defekt | 0 |
| 0x806DDE | SF LED Steuergerät: TAKEDOWN LIGHT WIG-WAG defekt | 0 |
| 0x806DDF | Tonsignalanlage: defekt | 0 |
| 0x806DE0 | Tonsignalanlage: Kommunikationsfehler | 0 |
| 0x806DE1 | Funkanlage: Bedienteil Fehler | 0 |
| 0x806DE2 | Funkanlage: Bedienteil nicht angesteckt | 0 |
| 0x806DE3 | Funkanlage: Bedienteil nicht erreichbar | 0 |
| 0x806DE4 | Funkanlage: Bedienteil Parameter verändert | 0 |
| 0x806DE5 | Funkanlage: Kommunikation Fehler | 0 |
| 0x806DE6 | Präsentationsmodus aktiv | 0 |
| 0x806DE7 | US Ausgang Funk (Pin 9) Kurzschluss nach Batterie | 0 |
| 0x806DE8 | US Ausgang Funk (Pin 9) Kurzschluss nach Masse | 0 |
| 0x806DE9 | US Ausgang Helm Headset (Pin 20) Kurzschluss nach Batterie | 0 |
| 0x806DEA | US Ausgang Helm Headset (Pin 20) Kurzschluss nach Masse | 0 |
| 0x806DEB | US Ausgang Kartenlicht (Pin 47) Kurzschluss nach Batterie | 0 |
| 0x806DEC | US Ausgang Kartenlicht (Pin 47) Kurzschluss nach Masse | 0 |
| 0x806DED | US Ausgang Lautsprecher (Pin 7) Kurzschluss nach Batterie | 0 |
| 0x806DEE | US Ausgang Lautsprecher (Pin 7) Kurzschluss nach Masse | 0 |
| 0x806DEF | US Ausgang LED Steuergerät (Pin 5) Kurzschluss nach Batterie | 0 |
| 0x806DF0 | US Ausgang LED Steuergerät (Pin 5) Kurzschluss nach Masse | 0 |
| 0x806DF1 | US Ausgang P-Schalter (Pin 8) Kurzschluss nach Batterie | 0 |
| 0x806DF2 | US Ausgang P-Schalter (Pin 8) Kurzschluss nach Masse | 0 |
| 0x806DF3 | US Ausgang PTPA (Pin 34) Kurzschluss nach Batterie | 0 |
| 0x806DF4 | US Ausgang PTPA (Pin 34) Kurzschluss nach Masse | 0 |
| 0x806DF5 | US Ausgang PTT1 (Pin 23) Kurzschluss nach Batterie | 0 |
| 0x806DF6 | US Ausgang PTT1 (Pin 23) Kurzschluss nach Masse | 0 |
| 0x806DF7 | US Ausgang PTT2 (Pin 21) Kurzschluss nach Batterie | 0 |
| 0x806DF8 | US Ausgang PTT2 (Pin 21) Kurzschluss nach Masse | 0 |
| 0x806DF9 | US Ausgang Radar (Pin 3) Kurzschluss nach Batterie | 0 |
| 0x806DFA | US Ausgang Radar (Pin 3) Kurzschluss nach Masse | 0 |
| 0x806DFB | US Ausgang Sirene (Pin 1) Kurzschluss nach Batterie | 0 |
| 0x806DFC | US Ausgang Sirene (Pin 1) Kurzschluss nach Masse | 0 |
| 0x806DFD | US Ausgang TDL (Pin 2) Kurzschluss nach Batterie | 0 |
| 0x806DFE | US Ausgang TDL (Pin 2) Kurzschluss nach Masse | 0 |
| 0x806DFF | US Ausgang Waffenverriegelung (Pin 46) Kurzschluss nach Batterie | 0 |
| 0x806E00 | US Ausgang Waffenverriegelung (Pin 46) Kurzschluss nach Masse | 0 |
| 0x806E01 | US Ausgang Zubehör I (Pin 33) Kurzschluss nach Batterie | 0 |
| 0x806E02 | US Ausgang Zubehör I (Pin 33) Kurzschluss nach Masse | 0 |
| 0x806E03 | US Ausgang Zubehör II (Pin 35) Kurzschluss nach Batterie | 0 |
| 0x806E04 | US Ausgang Zubehör II (Pin 35) Kurzschluss nach Masse | 0 |
| 0x806E05 | US Ausgang Zubehör III (Pin 36) Kurzschluss nach Batterie | 0 |
| 0x806E06 | US Ausgang Zubehör III (Pin 36) Kurzschluss nach Masse | 0 |
| 0x806E07 | Ausgang Anhaltesignal Tonsignalanlage Kurzschluss nach Batterie | 0 |
| 0x806E08 | Ausgang Anhaltesignal Tonsignalanlage Kurzschluss nach Masse | 0 |
| 0x806E09 | Ausgang Anhaltesignal Tonsignalanlage Leitungsunterbrechung | 0 |
| 0x806E0A | Funkanlage: Bedienteil kein Helm angesteckt | 0 |
| 0x806E0B | Versorgung Blitzkennleuchte Zusatzausgang: Kurzschluss nach Batterie | 0 |
| 0x806E0C | Versorgung Blitzkennleuchte Zusatzausgang: Kurzschluss nach Masse | 0 |
| 0x806E0D | Versorgung Blitzkennleuchte Zusatzausgang: Leitungsunterbrechung | 0 |
| 0xE0045F | CAN Bus Off | 1 |
| 0xE00C01 | SF_LIN Eingang_Schalterblock_Sonderfunktion_Links_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C02 | SF_LIN Eingang_Schalterblock_Sonderfunktion_Rechts_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C03 | SF_LIN Status_Blitzleuchte_HL_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C04 | SF_LIN Status_Blitzleuchte_HR_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C05 | SF_LIN Status_Blitzleuchte_VL_Motorrad_2010_LIN : Zeitüberschreitung | 0 |
| 0xE00C06 | SF_LIN Status_Blitzleuchte_VR_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C07 | SF_LIN Status_Tonfolge_System_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C08 | SF_LIN: Busausfall | 0 |
| 0xE00C09 | SF_LIN Status_FUNK_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE00C0A | SF_LIN Status_Sonderfahrzeug_LED_Motorrad_2010_LIN: Zeitüberschreitung | 0 |
| 0xE0141C | CAN KOMBI Nachricht Bedienung_Fahrzeug_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE01420 | CAN KOMBI Nachricht Eingang_Schalterblock_Links_Motorrad_2010_CAN: Zeitüberschreitung | 1 |
| 0xE01422 | CAN ABSBCO Nachricht Geschwindigkeit_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE01424 | CAN DME Nachricht Klemmenstatus_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE01426 | CAN KOMBI Nachricht Kombidaten_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE0142A | CAN DME Nachricht Motordaten_2_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE01434 | CAN FSA-BCO Nachricht Status_Erweitert_Funktion_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE0143A | CAN BCO Nachricht Status_Grund_Funktion_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE01487 | CAN BCO Nachricht Zusatzinformation_Grund_Funktion_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
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

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-mr-tab-bca-calibration"></a>
### MR_TAB_BCA_CALIBRATION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NOT_CALIBRATED |
| 1 | CALIBRATED |
| 0xFF | UNKNOWN |

<a id="table-mr-tab-bco-calibration"></a>
### MR_TAB_BCO_CALIBRATION

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NOT_STARTED |
| 1 | RUNNING |
| 2 | FINISHED_OK |
| 3 | FINISHED_NOK |
| 0xFF | NOT_DEFINED |

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

<a id="table-res-0x4001-d"></a>
### RES_0X4001_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL_50_ENTLASTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Entlastung bei KL_50: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung Nebelschlussleuchte bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung Anhaltesignal hinten Stop bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_STOP_VORNE | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung Anhaltesignal vorne Stop bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung Anhaltesignal hinten Bitte folgen bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_SPANNUNG_SCHALTER | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung Spannungsversorgung Zusatzschaltereinheit bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |
| STAT_FA_US_FREMDVERSORGUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktionsabschaltung US Fremdversorgung bei KL_50 ein: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4002-d"></a>
### RES_0X4002_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Licht aus: 0 = nicht aktiv, 1 = aktiv |
| STAT_COMM_ERR_SSL_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal COMM_ERR_SSL_MOTBK_2010: 0 = kein Fehler, 1 = Fehler vorhanden |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_COMM_ERR_SSR_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal COMM_ERR_SSR_MOTBK_2010: 0 = kein Fehler, 1 = Fehler vorhanden |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_ENTLASTUNG_KL50 | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Entlastung KL50: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4003-d"></a>
### RES_0X4003_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_SPANNUNGSVERSORGUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Spannungsversorgung Zusatzschaltereinheit: 0 = nicht aktiv, 1 = aktiv |
| STAT_AUSGANG_PIN_8 | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 8: 0 = aus, 1 = ein |

<a id="table-res-0x4004-d"></a>
### RES_0X4004_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IN_SSR_TOP_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_TOP_DWN_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |

<a id="table-res-0x4005-d"></a>
### RES_0X4005_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_MODUL_SUCHBELEUCHTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktionsmodul Suchbeleuchtung Taster: 0 = nicht aktiv, 1 = aktiv |
| STAT_MODUL_TASTERBELEUCHTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktionsmodul Tasterbeleuchtung Licht aus: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_ILUM_PWRD_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LICHT_AUS | - | - | - | Wert vom CAN Signal CTR_ILUM_PWRD_MOTBK_2010 |
| STAT_ABSCHALTUNG_ALTERNIERENDES_FRONTLICHT | 0/1 | high | unsigned char | - | - | - | - | - | - |

<a id="table-res-0x4006-d"></a>
### RES_0X4006_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_IN_SSR_TOP_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_TOP_UP_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4007-d"></a>
### RES_0X4007_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Nebelschlussleuchte: 0 = aus, 1 = ein |
| STAT_AUSGANG_PIN_47 | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 47: 0 = aus, 1 = ein |
| STAT_CTR_SSR_TOP_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_TOP_UP_MOTBK_2010 |

<a id="table-res-0x4008-d"></a>
### RES_0X4008_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_ST_CL_PHLI_FLH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Wert vom LIN Signal ST_CL_PHLI_FLH_MOTBK_2010 |
| STAT_ST_CL_PHLI_FRH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Wert vom LIN Signal ST_CL_PHLI_FRH_MOTBK_2010 |
| STAT_ST_CL_PHLI_RRH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Wert vom LIN Signal ST_CL_PHLI_RRH_MOTBK_2010 |
| STAT_ST_CL_PHLI_RLH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Wert vom LIN Signal ST_CL_PHLI_RLH_MOTBK_2010 |
| STAT_IN_SSR_MID_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_MID_UP_MOTBK_2010 |
| STAT_IN_SSR_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_MID_DWN_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_ZUSTAND_KENNLEUCHTE_VORNE_LINKS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand vorne links |
| STAT_ZUSTAND_KENNLEUCHTE_VORNE_RECHTS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand vorne rechts |
| STAT_ZUSTAND_KENNLEUCHTE_HINTEN_LINKS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand hinten links |
| STAT_ZUSTAND_KENNLEUCHTE_HINTEN_RECHTS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand hinten rechts |

<a id="table-res-0x4009-d"></a>
### RES_0X4009_D

Dimensions: 19 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_KENNLEUCHTEN_ALLGEMEIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Kennleuchten allgemein: 0 = aus, 1 = ein |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_ZUSTAND_KENNLEUCHTE_VORNE_LINKS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand vorne links |
| STAT_ZUSTAND_KENNLEUCHTE_VORNE_RECHTS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand vorne rechts |
| STAT_ZUSTAND_KENNLEUCHTE_HINTEN_LINKS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand hinten links |
| STAT_ZUSTAND_KENNLEUCHTE_HINTEN_RECHTS | 0-n | high | unsigned char | - | TAB_MR_RES_ZUSTAND_KENNLEUCHTEN | - | - | - | Kennleuchtenzustand hinten rechts |
| STAT_CTR_PHLI_MOD_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Wert vom LIN Signal CTR_PHLI_MOD_MOTBK_2010 |
| STAT_CTR_PHLI_SYNCN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Wert vom LIN Signal CTR_PHLI_SYNCN_MOTBK_2010 |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte vorne links: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte vorne rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte hinten links: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte hinten rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte vorne links: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte vorne rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte hinten links: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte hinten rechts: 0 = aus, 1 = ein |
| STAT_CTR_SSR_MID_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_MID_UP_MOTBK_2010 |
| STAT_CTR_SSR_MID_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_MID_DWN_MOTBK_2010 |
| STAT_CTR_PHLI_BRIG_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Wert vom LIN Signal CTR_PHLI_BRIG_MOTBK_2010 |

<a id="table-res-0x400b-d"></a>
### RES_0X400B_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion LED Blitzkennleuchte vorne links (Pin 3): 0 = aus, 1 = ein  |

<a id="table-res-0x400d-d"></a>
### RES_0X400D_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion LED Blitzkennleuchte vorne rechts (Pin 2): 0 = aus, 1 = ein  |

<a id="table-res-0x400f-d"></a>
### RES_0X400F_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Rundumkennleuchte hinten links (Pin 20): 0 = aus, 1 = ein  |

<a id="table-res-0x4011-d"></a>
### RES_0X4011_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Rundumkennleuchte hinten rechts (Pin 7): 0 = aus, 1 = ein  |

<a id="table-res-0x4012-d"></a>
### RES_0X4012_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_IN_SSL_TOP_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_TOP_UP_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4013-d"></a>
### RES_0X4013_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_STOP_VORNE | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Anhaltesignal vorne Stop (Pin 23) 0 = aus, 1 = ein |
| STAT_CTR_SSL_TOP_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_TOP_UP_MOTBK_2010 |

<a id="table-res-0x4014-d"></a>
### RES_0X4014_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_IN_SSR_BOT_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_BOT_UP_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4015-d"></a>
### RES_0X4015_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Anhaltesignal hinten Stop (Pin 36) 0 = aus, 1 = ein |
| STAT_CTR_SSR_BOT_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_BOT_UP_MOTBK_2010 |

<a id="table-res-0x4016-d"></a>
### RES_0X4016_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_IN_SSR_BOT_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_BOT_DWN_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4017-d"></a>
### RES_0X4017_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Anhaltesignal hinten Bitte folgen (Pin 35) 0 = aus, 1 = ein |
| STAT_CTR_SSR_BOT_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_BOT_DWN_MOTBK_2010 |

<a id="table-res-0x4018-d"></a>
### RES_0X4018_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IN_SSL_ROSW_LH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_ROSW_LH_MOTBK_2010 |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4019-d"></a>
### RES_0X4019_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_OP_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_DWN_MOTBK_2010 |
| STAT_TASTER_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT1 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT2 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT3 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | Status Signal ungültig in LIN Signal OP_PTT_MOTBK_2010: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_PHLI_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Wert vom LIN Signal CTR_PHLI_SPFN_MOTBK_2010 |
| STAT_IN_SPDM_STOU_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_SPDM_STOU_MOTBK_2010 |

<a id="table-res-0x401a-d"></a>
### RES_0X401A_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IN_SSL_ROSW_RH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_ROSW_RH_MOTBK_2010 |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x401b-d"></a>
### RES_0X401B_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_OP_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_DWN_MOTBK_2010 |
| STAT_TASTER_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT1 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT2 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT3 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | Status Signal ungültig in LIN Signal OP_PTT_MOTBK_2010: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_PHLI_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Wert vom LIN Signal CTR_PHLI_SPFN_MOTBK_2010 |
| STAT_IN_SPDM_STOU_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_SPDM_STOU_MOTBK_2010 |

<a id="table-res-0x401c-d"></a>
### RES_0X401C_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IN_SSR_ROSW_LH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_ROSW_LH_MOTBK_2010 |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x401d-d"></a>
### RES_0X401D_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_OP_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_DWN_MOTBK_2010 |
| STAT_TASTER_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT1 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT2 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT3 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | Status Signal ungültig in LIN Signal OP_PTT_MOTBK_2010: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_PHLI_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Wert vom LIN Signal CTR_PHLI_SPFN_MOTBK_2010 |
| STAT_IN_SPDM_STOU_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_SPDM_STOU_MOTBK_2010 |

<a id="table-res-0x401e-d"></a>
### RES_0X401E_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IN_SSR_ROSW_RH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_ROSW_RH_MOTBK_2010 |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_AUFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 Nebenfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus: 0 = aus, 1 = ein |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x401f-d"></a>
### RES_0X401F_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | - |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte vorne rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten links: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte hinten rechts: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_CL_STD_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 Hauptfarbe Kennleuchte reserviert: 0 = nicht aktiv, 1 = aktiv |
| STAT_OP_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_DWN_MOTBK_2010 |
| STAT_TASTER_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT1 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT2 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTER_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | Status Taster PTT3 aus LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | Status Signal ungültig in LIN Signal OP_PTT_MOTBK_2010: 0 = nicht aktiv, 1 = aktiv |
| STAT_CTR_PHLI_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Wert vom LIN Signal CTR_PHLI_SPFN_MOTBK_2010 |
| STAT_IN_SPDM_STOU_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_SPDM_STOU_MOTBK_2010 |

<a id="table-res-0x4020-d"></a>
### RES_0X4020_D

Dimensions: 19 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ST_VRS_TOSQ_SYS_MOTBK_2010_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom LIN Signal ST_VRS_TOSQ_SYS_MOTBK_2010 (Firmware Version) |
| STAT_V_WHL_RR_MOTBK_2010_WERT | km/h | high | unsigned int | - | - | 1.0 | 8.0 | 0.0 | Wert vom CAN Signal V_WHL_RR_MOTBK_2010 |
| STAT_IN_HORN_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal IN_HORN_MOTBK_2010: 0 = Taster nicht gedrückt, 1 = Taster gedrückt |
| STAT_IN_SSR_TOP_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_TOP_DWN_MOTBK_2010 |
| STAT_IN_SSL_MID_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_MID_UP_MOTBK_2010 (Tonsignal Standby) |
| STAT_IN_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_MID_DWN_MOTBK_2010 (Tonsignal Ein) |
| STAT_IN_SSL_BOT_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_BOT_UP_MOTBK_2010 (Ton Umschaltung 1) |
| STAT_IN_SSL_TOP_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_TOP_UP_MOTBK_2010 (Anhaltesignal) |
| STAT_IN_SSL_BOT_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_BOT_DWN_MOTBK_2010 (Tonsignal Umschaltung 2) |
| STAT_ST_ERR_TOSQ_SYS_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LIN_FEHLER | - | - | - | Wert vom LIN Signal ST_ERR_TOSQ_SYS_MOTBK_2010 (Status Fehler) |
| STAT_COMM_ERR_TSA_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal COMM_ERR_TSA_MOTBK_2010 (Fehler Kommunikation): 0 = kein Fehler, 1 = Fehler |
| STAT_ST_ERR_PHLI_RRH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Wert vom LIN Signal ST_ERR_PHLI_RRH_MOTBK_2010 (Fehler Kennleuchte hinten rechts) |
| STAT_ST_ERR_PHLI_RLH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Wert vom LIN Signal ST_ERR_PHLI_RLH_MOTBK_2010 (Fehler Kennleuchte hinten links) |
| STAT_ST_ERR_PHLI_FLH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Wert vom LIN Signal ST_ERR_PHLI_FLH_MOTBK_2010 (Fehler Kennleuchte vorne links) |
| STAT_ST_ERR_PHLI_FRH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Wert vom LIN Signal ST_ERR_PHLI_FRH_MOTBK_2010 (Fehler Kennleuchte vorne rechts) |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_HLD_SIG_MOTBK_2010 | 0-n | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_HLD_SIG_MOTBK_2010 |

<a id="table-res-0x4021-d"></a>
### RES_0X4021_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Tonsignalanlage (Pin 1): 0 = aus, 1 = ein |
| STAT_CTR_CNCD_TOSQ_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_COUNTRY_CODE | - | - | - | Wert vom LIN Signal CTR_CNCD_TOSQ_MOTBK_2010 (Steuerung Ländercodierung) |
| STAT_CTR_AVOL_TOSQ_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TSA_VOLUME | - | - | - | Wert vom LIN Signal CTR_AVOL_TOSQ_MOTBK_2010 (Steuerung Lautstärke) |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom LIN Signal ST_KL_15_MOTBK_2010 (Status KL15) |
| STAT_OP_SSL_MID_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_UP_MOTBK_2010 (Status Schalter Standby) |
| STAT_OP_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_MID_DWN_MOTBK_2010 (Status Schalter Ein) |
| STAT_OP_SSL_BOT_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_BOT_UP_MOTBK_2010 (Status Schalter Umschaltung 1) |
| STAT_OP_SSL_BOT_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal OP_SSL_BOT_DWN_MOTBK_2010 (Status Schalter Umschaltung 2) |
| STAT_ST_IDEN_CONN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_ZWANG | - | - | - | Wert vom LIN Signal ST_IDEN_CONN_MOTBK_2010 (Status Kennleuchtenzwang) |
| STAT_CTR_SUBST_HORN_TOSQ_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BEH_HORN_EMULATION | - | - | - | Wert vom LIN Signal CTR_SUBST_HORN_TOSQ_MOTBK_2010 (Steuerung Hupenemulation) |
| STAT_CTR_HORN_TOSQ_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_HORN | - | - | - | Wert vom LIN Signal CTR_HORN_TOSQ_MOTBK_2010 (Steuerung Hupe) |
| STAT_ST_IDEN_LI_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_ZWANG | - | - | - | Wert vom LIN Signal ST_IDEN_LI_MOTBK_2010 (Status Kennleuchtenzwang) |

<a id="table-res-0x4022-d"></a>
### RES_0X4022_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_V_WHL_RR_MOTBK_2010_WERT | km/h | high | unsigned int | - | - | 1.0 | 8.0 | 0.0 | Wert vom CAN Signal V_WHL_RR_MOTBK_2010 |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_OP_MMC_AUD_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_AUDIO_MENUE_CAN | - | - | - | Wert vom CAN Signal CTR_OP_MMC_AUD_MOTBK_2010 |
| STAT_IN_MMC_LH_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal IN_MMC_LH_MOTBK_2010: 0 = Taster nicht gedrückt, 1 = Taster gedrückt |
| STAT_IN_MMC_RH_MOTBK_2010 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal IN_MMC_RH_MOTBK_2010: 0 = Taster nicht gedrückt, 1 = Taster gedrückt |
| STAT_ST_MMC_PO_MOTBK_2010_WERT | Stufen | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom CAN Signal ST_MMC_PO_MOTBK_2010 |
| STAT_IN_SSL_ROSW_LH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_ROSW_LH_MOTBK_2010 |
| STAT_IN_SSR_ROSW_LH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_ROSW_LH_MOTBK_2010 |
| STAT_IN_SSR_ROSW_RH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN SignalIN_SSR_ROSW_RH_MOTBK_2010 |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz vor Tiefentladung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung: 0 = nicht aktiv, 1 = aktiv |

<a id="table-res-0x4023-d"></a>
### RES_0X4023_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Funkanlage (Pin 5): 0 = aus, 1 = ein |
| STAT_CTR_DOM_V_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_GESCHWINDIGKEIT_BEREICH | - | - | - | Wert vom LIN Signal CTR_DOM_V_MOTBK_2010 |
| STAT_CTR_MMC_LH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_MMC_TASTER | - | - | - | Wert vom LIN Signal CTR_MMC_LH_MOTBK_2010 |
| STAT_CTR_MMC_RH_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_MMC_TASTER | - | - | - | Wert vom LIN Signal CTR_MMC_RH_MOTBK_2010 |
| STAT_CTR_MMC_PO_MOTBK_2010_WERT | Stufen | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom LIN Signal CTR_MMC_PO_MOTBK_2010 |
| STAT_ST_VRS_FUNK_MOTBK_2010_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom LIN Signal ST_VRS_FUNK_MOTBK_2010 (Firmware Version Funkgerät) |
| STAT_ST_OPUN_FUNK_SP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_HELMSTATUS | - | - | - | Wert vom LIN Signal ST_OPUN_FUNK_SP_MOTBK_2010 (Status Helm Anschluss) |
| STAT_ST_OPUN_FUNK_ELA_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_ELA | - | - | - | Wert vom LIN Signal ST_OPUN_FUNK_ELA_MOTBK_2010 (Status ELA Leitung) |
| STAT_ST_OPUN_FUNK_PRMTR_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_PARAMETERSTATUS | - | - | - | Wert vom LIN Signal ST_OPUN_FUNK_PRMTR_MOTBK_2010 (Parameterstatus) |

<a id="table-res-0x4025-d"></a>
### RES_0X4025_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL15_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion KL15 (Pin 33): 0 = aus, 1 = ein |

<a id="table-res-0x4027-d"></a>
### RES_0X4027_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL30_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang KL30 (Codierparameter kl30_TruthTable) 0 = aus, 1 = ein |

<a id="table-res-0x4028-d"></a>
### RES_0X4028_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_RPM_ENG_MOTBK_2010_WERT | 1/min | high | unsigned int | - | - | 5.0 | 1.0 | 0.0 | Wert vom CAN Signal RPM_ENG_MOTBK_2010 |
| STAT_BATTERIESPANNUNG_PIN51_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Status Batteriespannung Behörde Pin 51 |

<a id="table-res-0x4029-d"></a>
### RES_0X4029_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BEHOERDENRELAIS_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Behördenrelais (Pin 37): 0 = aus, 1 = ein |

<a id="table-res-0x402b-d"></a>
### RES_0X402B_D

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHUTZ_TIEFENTLADUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Schutz vor Tiefentladung: 0 = aus, 1 = ein |
| STAT_NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Nebelschlussleuchte (Pin 47): 0 = aus, 1 = ein |
| STAT_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Kennleuchte vorne links (Pin 3): 0 = aus, 1 = ein |
| STAT_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Kennleuchte vorne rechts (Pin 2): 0 = aus, 1 = ein |
| STAT_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Kennleuchte hinten links (Pin 20): 0 = aus, 1 = ein |
| STAT_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Kennleuchte hinten rechts (Pin 7): 0 = aus, 1 = ein |
| STAT_KL15 | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang KL15 (Pin 33): 0 = aus, 1 = ein |
| STAT_FUNKTIONSTASTER | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Funktionstaster (Pin 34): 0 = aus, 1 = ein |
| STAT_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Anhaltesignal hinten Stop (Pin 36): 0 = aus, 1 = ein |
| STAT_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Anhaltesignal hinten Bitte folgen (Pin 35): 0 = aus, 1 = ein |
| STAT_BEHOERDENRELAIS | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Behördenrelais (Pin 37): 0 = aus, 1 = ein |
| STAT_KL30 | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang KL30 (Pin 46): 0 = aus, 1 = ein |
| STAT_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Tonsignalanlage (Pin 1): 0 = aus, 1 = ein |
| STAT_FUNKANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Funkanlage (Pin 5): 0 = aus, 1 = ein |
| STAT_SV_BEHOERDENSCHALTER | 0/1 | high | unsigned char | - | - | - | - | - | Ausgang Spannungsversorgung Behördenschalter (Pin 8): 0 = aus, 1 = ein |

<a id="table-res-0x402d-d"></a>
### RES_0X402D_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ABSCHALTUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Überspannungsabschaltung: 0 = aus, 1 = ein |

<a id="table-res-0x402f-d"></a>
### RES_0X402F_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ABSCHALTUNG_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Unterspannungsabschaltung: 0 = aus, 1 = ein |

<a id="table-res-0x4030-d"></a>
### RES_0X4030_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CTR_CL_STD_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte vorne links: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte vorne rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte hinten links: 0 = aus, 1 = ein |
| STAT_CTR_CL_STD_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_STD_MOTBK_2010 für Blitzkennleuchte hinten rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_VL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte vorne links: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_VR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte vorne rechts: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_HL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte hinten links: 0 = aus, 1 = ein |
| STAT_CTR_CL_AUFN_MOTBK_2010_HR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_CL_AUFN_MOTBK_2010 für Blitzkennleuchte hinten rechts: 0 = aus, 1 = ein |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_BRIG_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom CAN Signal BRIG_MOTBK_2010 |
| STAT_IN_SSR_TOP_DWN | 0-n | high | unsigned char | - | - | - | - | - | - |
| STAT_ABSCHALTUNG_ALTERNIERENDES_FRONTLICHT | 0/1 | high | unsigned char | - | - | - | - | - | - |

<a id="table-res-0x4031-d"></a>
### RES_0X4031_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Alternierendes Frontlicht: 0 = aus, 1 = ein |
| STAT_CTR_ILUM_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_SONDERBLINKEN | - | - | - | Wert vom CAN Signal CTR_ILUM_SPFN_MOTBK_2010 |

<a id="table-res-0x4032-d"></a>
### RES_0X4032_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTION_LICHT_AUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Funktion Licht aus 0 = aus, 1 = ein |
| STAT_FUNKTION_UEBERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Überspannungsabschaltung 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_UNTERSPANNUNG_ABSCHALTUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Unterspannungsabschaltung 0 = nicht aktiv, 1 = aktiv |
| STAT_FUNKTION_SCHUTZ_TIEFENTLADUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Funktion Schutz Tiefentladung 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_15_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Wert vom CAN Signal ST_KL_15_MOTBK_2010 |
| STAT_CTR_DIM_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_DESIGN | - | - | - | Wert vom CAN Signal CTR_DIM_MOTBK_2010 |
| STAT_IN_SSL_MID_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_MID_UP_MOTBK_2010 |
| STAT_IN_SSL_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_MID_DWN_MOTBK_2010 |
| STAT_IN_SSL_BOT_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_BOT_UP_MOTBK_2010 |
| STAT_IN_SSL_BOT_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSL_BOT_DWN_MOTBK_2010 |
| STAT_IN_SSR_TOP_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_TOP_UP_MOTBK_2010 |
| STAT_IN_SSR_MID_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_MID_UP_MOTBK_2010 |
| STAT_IN_SSR_MID_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_MID_DWN_MOTBK_2010 |
| STAT_IN_SSR_BOT_UP_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_BOT_UP_MOTBK_2010 |
| STAT_IN_SSR_BOT_DWN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Wert vom LIN Signal IN_SSR_BOT_DWN_MOTBK_2010 |
| STAT_ZUSTAND_1_AUSGANG_23 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 1 Ausgang 23 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_2_AUSGANG_23 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 2 Ausgang 23 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_1_AUSGANG_9 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 1 Ausgang 9 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_2_AUSGANG_9 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 2 Ausgang 9 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_1_AUSGANG_22 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 1 Ausgang 22: 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_2_AUSGANG_22 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 2 Ausgang 22: 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_1_AUSGANG_35 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 1 Ausgang 35: 0 = nicht aktiv, 1 = aktiv |
| STAT_ZUSTAND_2_AUSGANG_35 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom Zustand 2 Ausgang 35: 0 = nicht aktiv, 1 = aktiv |
| STAT_ST_KL_50_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_KL50 | - | - | - | Wert vom CAN Signal ST_KL_50_MOTBK_2010 |

<a id="table-res-0x4033-d"></a>
### RES_0X4033_D

Dimensions: 34 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PIN_20_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 20 (Helm Headset) 0 = aus, 1 = ein |
| STAT_PIN_34_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 34 (PTPA) 0 = aus, 1 = ein |
| STAT_PIN_36_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 36 (Zubehör III) 0 = aus, 1 = ein |
| STAT_PIN_47_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 47 (Kartenlicht) 0 = aus, 1 = ein |
| STAT_PIN_23_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 23 (PTT1) 0 = aus, 1 = ein |
| STAT_PIN_9_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 9 (Funk) 0 = aus, 1 = ein |
| STAT_PIN_33_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 33 (Zubehör I) 0 = aus, 1 = ein |
| STAT_PIN_21_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 21 (PTT2) 0 = aus, 1 = ein |
| STAT_PIN_35_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 35 (Zubehör II) 0 = aus, 1 = ein |
| STAT_PIN_1_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 1 (Sirene) 0 = aus, 1 = ein |
| STAT_PIN_2_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 2 (TDL) 0 = aus, 1 = ein |
| STAT_PIN_3_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 3 (Radar) 0 = aus, 1 = ein |
| STAT_PIN_5_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 5 (LED Steuergerät) 0 = aus, 1 = ein |
| STAT_PIN_46_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 46 (Waffenverriegelung) 0 = aus, 1 = ein |
| STAT_PIN_8_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 8 (P-Schalter) 0 = aus, 1 = ein |
| STAT_PIN_7_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 7 (Lautsprecher) 0 = aus, 1 = ein |
| STAT_IN_HAZW_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_HAZW_SPFN_MOTBK_2010 |
| STAT_CTR_SSL_MID_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_MID_UP_MOTBK_2010 |
| STAT_CTR_SSL_MID_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_MID_DWN_MOTBK_2010 |
| STAT_CTR_SSL_BOT_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_BOT_UP_MOTBK_2010 |
| STAT_CTR_SSL_BOT_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_BOT_DWN_MOTBK_2010 |
| STAT_CTR_SSR_TOP_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_TOP_UP_MOTBK_2010 |
| STAT_CTR_SSR_TOP_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_TOP_DWN_MOTBK_2010 |
| STAT_CTR_SSR_BOT_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_BOT_UP_MOTBK_2010 |
| STAT_ST_VRS_SF_LED_MOTBK_2010_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom LIN Signal ST_VRS_SF_LED_MOTBK_2010 (Firmware Version US LED Steuergerät) |
| STAT_ST_HDLI_FLS_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BU_ALT_FRONTL | - | - | - | Wert vom LIN Signal ST_HDLI_FLS_MOTBK_2010 (Status Alternierendes Frontlicht) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_C | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster C) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_D | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster D) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_E | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster E) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_F | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster F) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_I | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster I) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Reserviert1) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Reserviert2) |
| STAT_CTR_ILUM_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_SONDERBLINKEN | - | - | - | Wert vom CAN Signal CTR_ILUM_SPFN_MOTBK_2010 (Beleuchtung Sonderfunktion) |

<a id="table-res-0x4034-d"></a>
### RES_0X4034_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ST_LIDF_RR_MOTBK_2010_RL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Rücklicht |
| STAT_ST_LIDF_RR_MOTBK_2010_BL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Bremslicht |
| STAT_ST_LIDF_RR_MOTBK_2010_KZL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Kennzeichenleuchte |
| STAT_ST_LIDF_RR_MOTBK_2010_BHL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Blinker hinten links |
| STAT_ST_LIDF_RR_MOTBK_2010_BHR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Blinker hinten rechts |
| STAT_ST_LIDF_RR_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_RR_MOTBK_2010: Reserviert |
| STAT_ST_LIDF_AUHL_MOTBK_2010_ZSW1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_AUHL_MOTBK_2010: Zusatzscheinwerfer 1 |
| STAT_ST_LIDF_AUHL_MOTBK_2010_ZSW2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_AUHL_MOTBK_2010: Zusatzscheinwerfer 2 |
| STAT_ST_LIDF_AUHL_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_AUHL_MOTBK_2010: Reserviert |
| STAT_ST_LIDF_FT_MOTBK_2010_POS1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Standlicht 1 vorne |
| STAT_ST_LIDF_FT_MOTBK_2010_POS2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Standlicht 2 vorne |
| STAT_ST_LIDF_FT_MOTBK_2010_ABL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Abblendlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_FL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Fernlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_TFL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Tagfahrlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_BVL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Blinker vorne links |
| STAT_ST_LIDF_FT_MOTBK_2010_BVR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Blinker vorne rechts |
| STAT_ST_LIDF_FT_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_LIDF_FT_MOTBK_2010: Reserviert |
| STAT_ST_DRL_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TFL_STATUS | - | - | - | Wert vom CAN Signal ST_DRL_MOTBK_2010 |
| STAT_CTR_MAB_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_FL_STATUS | - | - | - | Wert vom CAN Signal CTR_MAB_MOTBK_2010 |
| STAT_CTR_DIPB_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_ABL_STATUS | - | - | - | Wert vom CAN Signal CTR_DIPB_MOTBK_2010 |
| STAT_ST_BL_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BREMSL_STATUS | - | - | - | Wert vom CAN Signal ST_BL_MOTBK_2010 |
| STAT_ST_DISP_DRVDIR_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BLINKER_STATUS | - | - | - | Wert vom CAN Signal ST_DISP_DRVDIR_MOTBK_2010 |
| STAT_ST_SHR_MOD_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_PRES_MODUS | - | - | - | Wert vom CAN Signal ST_SHR_MOD_MOTBK_2010 |
| STAT_ST_EXT_LIDF_MOTBK_2010_ABL_FL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Abblendlicht oder Fernlicht |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZBL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzbremslicht |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZSW1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzscheinwerfer 1 |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZSW2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzscheinwerfer 2 |
| STAT_ST_EXT_LIDF_MOTBK_2010_NSL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Nebelschlußleuchte |
| STAT_ST_EXT_LIDF_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom CAN Signal ST_EXT_LIDF_MOTBK_2010: Reserviert |
| STAT_V_WHL_RR_MOTBK_2010_WERT | km/h | high | unsigned int | - | - | 1.0 | 8.0 | 0.0 | Wert vom CAN Signal V_WHL_RR_MOTBK_2010 |

<a id="table-res-0x4035-d"></a>
### RES_0X4035_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ST_LIDF_RR_MOTBK_2010_RL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Rücklicht |
| STAT_ST_LIDF_RR_MOTBK_2010_BL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Bremslicht |
| STAT_ST_LIDF_RR_MOTBK_2010_KZL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Kennzeichenleuchte |
| STAT_ST_LIDF_RR_MOTBK_2010_BHL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Blinker hinten links |
| STAT_ST_LIDF_RR_MOTBK_2010_BHR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Blinker hinten rechts |
| STAT_ST_LIDF_RR_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_RR_MOTBK_2010: Reserviert |
| STAT_ST_LIDF_AUHL_MOTBK_2010_ZSW1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_AUHL_MOTBK_2010: Zusatzscheinwerfer 1 |
| STAT_ST_LIDF_AUHL_MOTBK_2010_ZSW2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_AUHL_MOTBK_2010: Zusatzscheinwerfer 2 |
| STAT_ST_LIDF_AUHL_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_AUHL_MOTBK_2010: Reserviert |
| STAT_ST_LIDF_FT_MOTBK_2010_POS1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Standlicht 1 vorne |
| STAT_ST_LIDF_FT_MOTBK_2010_POS2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Standlicht 2 vorne |
| STAT_ST_LIDF_FT_MOTBK_2010_ABL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Abblendlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_FL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Fernlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_TFL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Tagfahrlicht |
| STAT_ST_LIDF_FT_MOTBK_2010_BVL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Blinker vorne links |
| STAT_ST_LIDF_FT_MOTBK_2010_BVR | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Blinker vorne rechts |
| STAT_ST_LIDF_FT_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_LIDF_FT_MOTBK_2010: Reserviert |
| STAT_ST_DRL_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TFL_STATUS | - | - | - | Wert vom LIN Signal ST_DRL_MOTBK_2010 |
| STAT_CTR_MAB_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_FL_STATUS | - | - | - | Wert vom LIN Signal CTR_MAB_MOTBK_2010 |
| STAT_CTR_DIPB_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_ABL_STATUS | - | - | - | Wert vom LIN Signal CTR_DIPB_MOTBK_2010 |
| STAT_ST_BL_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BREMSL_STATUS | - | - | - | Wert vom LIN Signal ST_BL_MOTBK_2010 |
| STAT_ST_DISP_DRVDIR_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BLINKER_STATUS | - | - | - | Wert vom LIN Signal ST_DISP_DRVDIR_MOTBK_2010 |
| STAT_ST_SHR_MOD_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_PRES_MODUS | - | - | - | Wert vom LIN Signal ST_SHR_MOD_MOTBK_2010 |
| STAT_ST_EXT_LIDF_MOTBK_2010_ABL_FL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Abblendlicht oder Fernlicht |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZBL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzbremslicht |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZSW1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzscheinwerfer 1 |
| STAT_ST_EXT_LIDF_MOTBK_2010_ZSW2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Zusatzscheinwerfer 2 |
| STAT_ST_EXT_LIDF_MOTBK_2010_NSL | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Nebelschlußleuchte |
| STAT_ST_EXT_LIDF_MOTBK_2010_RES | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal ST_EXT_LIDF_MOTBK_2010: Reserviert |
| STAT_V_WHL_RR_MOTBK_2010_WERT | km/h | high | unsigned int | - | - | 1.0 | 8.0 | 0.0 | Wert vom LIN Signal V_WHL_RR_MOTBK_2010 |

<a id="table-res-0x4036-d"></a>
### RES_0X4036_D

Dimensions: 34 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PIN_20_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 20 (Helm Headset) 0 = aus, 1 = ein |
| STAT_PIN_34_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 34 (PTPA) 0 = aus, 1 = ein |
| STAT_PIN_36_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 36 (Zubehör III) 0 = aus, 1 = ein |
| STAT_PIN_47_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 47 (Kartenlicht) 0 = aus, 1 = ein |
| STAT_PIN_23_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 23 (PTT1) 0 = aus, 1 = ein |
| STAT_PIN_9_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 9 (Funk) 0 = aus, 1 = ein |
| STAT_PIN_33_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 33 (Zubehör I) 0 = aus, 1 = ein |
| STAT_PIN_21_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 21 (PTT2) 0 = aus, 1 = ein |
| STAT_PIN_35_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 35 (Zubehör II) 0 = aus, 1 = ein |
| STAT_PIN_1_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 1 (Sirene) 0 = aus, 1 = ein |
| STAT_PIN_2_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 2 (TDL) 0 = aus, 1 = ein |
| STAT_PIN_3_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 3 (Radar) 0 = aus, 1 = ein |
| STAT_PIN_5_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 5 (LED Steuergerät) 0 = aus, 1 = ein |
| STAT_PIN_46_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 46 (Waffenverriegelung) 0 = aus, 1 = ein |
| STAT_PIN_8_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 8 (P-Schalter) 0 = aus, 1 = ein |
| STAT_PIN_7_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Pin 7 (Lautsprecher) 0 = aus, 1 = ein |
| STAT_IN_HAZW_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_CAN | - | - | - | Wert vom CAN Signal IN_HAZW_SPFN_MOTBK_2010 |
| STAT_CTR_SSL_MID_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_MID_UP_MOTBK_2010 |
| STAT_CTR_SSL_MID_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_MID_DWN_MOTBK_2010 |
| STAT_CTR_SSL_BOT_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_BOT_UP_MOTBK_2010 |
| STAT_CTR_SSL_BOT_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSL_BOT_DWN_MOTBK_2010 |
| STAT_CTR_SSR_TOP_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_TOP_UP_MOTBK_2010 |
| STAT_CTR_SSR_TOP_DWN_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_TOP_DWN_MOTBK_2010 |
| STAT_CTR_SSR_BOT_UP_MOTBK_2010_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | Wert vom LIN Signal CTR_SSR_BOT_UP_MOTBK_2010 |
| STAT_ST_VRS_SF_LED_MOTBK_2010_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert vom LIN Signal ST_VRS_SF_LED_MOTBK_2010 (Firmware Version US LED Steuergerät) |
| STAT_ST_HDLI_FLS_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_BU_ALT_FRONTL | - | - | - | Wert vom LIN Signal ST_HDLI_FLS_MOTBK_2010 (Status Alternierendes Frontlicht) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_C | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster C) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_D | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster D) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_E | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster E) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_F | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster F) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_I | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Funktionsbeleuchtung Taster I) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_RESERVIERT1 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Reserviert1) |
| STAT_CTR_FNI_SPFN_MOTBK_2010_RESERVIERT2 | 0/1 | high | unsigned char | - | - | - | - | - | Wert vom LIN Signal CTR_FNI_SPFN_MOTBK_2010 (Reserviert2) |
| STAT_CTR_ILUM_SPFN_MOTBK_2010 | 0-n | high | unsigned char | - | TAB_MR_RES_SONDERBLINKEN | - | - | - | Wert vom CAN Signal CTR_ILUM_SPFN_MOTBK_2010 (Beleuchtung Sonderfunktion) |

<a id="table-res-0xb008-r"></a>
### RES_0XB008_R

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_K0_KALIBRIERUNG_WERT | - | - | + | Stufen | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kalibrierter Wert K0 |
| STAT_K1_KALIBRIERUNG_WERT | - | - | + | Stufen | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kalibrierter Wert K1 |
| STAT_ROUTINE_RESULT | - | - | + | 0-n | high | unsigned char | - | TAB_MR_ROUTINE_BCA | - | - | - | Aktueller Routine Status |

<a id="table-res-0xb009-r"></a>
### RES_0XB009_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | - | - | + | 0-n | high | unsigned char | - | TAB_MR_ROUTINE_BCA | - | - | - | Status Routine Selbsttest |

<a id="table-res-0xe152-d"></a>
### RES_0XE152_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NEBELSCHLUSSLEUCHTE | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Nebelschlussleuchte 0 = aus, 1 = ein |

<a id="table-res-0xe155-d"></a>
### RES_0XE155_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BKL_VL_FIRMWARE_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Firmware Version Blitzkennleuchte vorne links (LIN Signal ST_VRS_PHLI_FLH_MOTBK_2010), FF = Signal ungültig |
| STAT_FEHLER_BLITZKENNLEUCHTE_VL | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Status Fehler in Blitzkennleuchte vorne links (LIN Signal ST_ERR_PHLI_FLH_MOTBK_2010) |
| STAT_FARBE_BLITZLEUCHTE_VL | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Anzahl unterstützter Farben Blitzkennleuchte vorne links (LIN Signal ST_CL_PHLI_FLH_MOTBK_2010) |
| STAT_TYP_BLITZLEUCHTE_VL | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_TYP | - | - | - | Typ der Blitzkennleuchte (LIN Signal ST_TYP_PHLI_FLH_MOTBK_2010) |
| STAT_KOMM_FEHLER_BKL_VL | 0/1 | high | unsigned char | - | - | - | - | - | Status Kommunikationsfehler Blitzkennleuchte VL (LIN Signal COMM_ERR_BKL_FLH_MOTBK_2010): 0 = kein Fehler, 1 = Fehler aktiv |

<a id="table-res-0xe156-d"></a>
### RES_0XE156_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte vorne links: 0 = Versorgung aus, 1 = Versorgung ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |

<a id="table-res-0xe157-d"></a>
### RES_0XE157_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BKL_VR_FIRMWARE_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Firmware Version Blitzkennleuchte vorne rechts (LIN Signal ST_VRS_PHLI_FRH_MOTBK_2010), FF = Signal ungültig |
| STAT_FEHLER_BLITZKENNLEUCHTE_VR | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Status Fehler in Blitzkennleuchte vorne rechts (LIN Signal SST_ERR_PHLI_FRH_MOTBK_2010) |
| STAT_FARBE_BLITZLEUCHTE_VR | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Anzahl unterstützter Farben Blitzkennleuchte vorne rechts (LIN Signal ST_CL_PHLI_FRH_MOTBK_2010) |
| STAT_TYP_BLITZLEUCHTE_VR | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_TYP | - | - | - | Typ der Blitzkennleuchte (LIN Signal ST_TYP_PHLI_FRH_MOTBK_2010) |
| STAT_KOMM_FEHLER_BKL_VR | 0/1 | high | unsigned char | - | - | - | - | - | Status Kommunikationsfehler Blitzkennleuchte VR (LIN Signal COMM_ERR_BKL_FRH_MOTBK_2010): 0 = kein Fehler, 1 = Fehler aktiv |

<a id="table-res-0xe158-d"></a>
### RES_0XE158_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte vorne rechts 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |

<a id="table-res-0xe159-d"></a>
### RES_0XE159_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BKL_HL_FIRMWARE_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Firmware Version Blitzkennleuchte hinten links (LIN Signal ST_VRS_PHLI_RLH_MOTBK_2010), FF = Signal ungültig |
| STAT_FEHLER_BLITZKENNLEUCHTE_HL | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Status Fehler in Blitzkennleuchte hinten links (LIN Signal ST_ERR_PHLI_RLH_MOTBK_2010) |
| STAT_FARBE_BLITZLEUCHTE_HL | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Anzahl unterstützter Farben Blitzkennleuchte hinten links (LIN Signal ST_CL_PHLI_RLH_MOTBK_2010) |
| STAT_TYP_BLITZLEUCHTE_HL | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_TYP | - | - | - | Typ der Blitzkennleuchte (LIN Signal ST_TYP_PHLI_RLH_MOTBK_2010) |
| STAT_KOMM_FEHLER_BKL_HL | 0/1 | high | unsigned char | - | - | - | - | - | Status Kommunikationsfehler Blitzkennleuchte HL (LIN Signal COMM_ERR_BKL_RLH_MOTBK_2010): 0 = kein Fehler, 1 = Fehler aktiv |

<a id="table-res-0xe15a-d"></a>
### RES_0XE15A_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte hinten links 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-res-0xe15b-d"></a>
### RES_0XE15B_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BKL_HR_FIRMWARE_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Firmware Version Blitzkennleuchte hinten rechts (LIN Signal ST_VRS_PHLI_RRH_MOTBK_2010), FF = Signal ungültig |
| STAT_FEHLER_BLITZKENNLEUCHTE_HR | 0-n | high | unsigned char | - | TAB_MR_RES_LEUCHTEN_FEHLER | - | - | - | Status Fehler in Blitzkennleuchte hinten rechts (LIN Signal ST_ERR_PHLI_RRH_MOTBK_2010) |
| STAT_FARBE_BLITZLEUCHTE_HR | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_FARBEN | - | - | - | Anzahl unterstützter Farben Blitzkennleuchte hinten rechts (LIN Signal ST_CL_PHLI_RRH_MOTBK_2010) |
| STAT_TYP_BLITZLEUCHTE_HR | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_TYP | - | - | - | Typ der Blitzkennleuchte (LIN Signal ST_TYP_PHLI_RRH_MOTBK_2010) |
| STAT_KOMM_FEHLER_BKL_HR | 0/1 | high | unsigned char | - | - | - | - | - | Status Kommunikationsfehler Blitzkennleuchte HR (LIN Signal COMM_ERR_BKL_RRH_MOTBK_2010): 0 = kein Fehler, 1 = Fehler aktiv |

<a id="table-res-0xe15c-d"></a>
### RES_0XE15C_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte hinten rechts 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-res-0xe15e-d"></a>
### RES_0XE15E_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_STOP_VORNE | 0/1 | high | unsigned char | - | - | - | - | - | Status Anhaltesignal STOP vorne 0 = aus, 1 = ein |

<a id="table-res-0xe160-d"></a>
### RES_0XE160_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_STOP_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status Anhaltesignal hinten STOP 0 = aus, 1 = ein |

<a id="table-res-0xe162-d"></a>
### RES_0XE162_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSGANG_FOLGEN_HINTEN | 0/1 | high | unsigned char | - | - | - | - | - | Status Anhaltesignal: 0 = aus, 1 = ein |

<a id="table-res-0xe164-d"></a>
### RES_0XE164_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TSA_FIRMWARE_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Firmware Version Tonsignalanlage (LIN Signal ST_VRS_TOSQ_SYS_MOTBK_2010), FF = Signal ungültig |
| STAT_FEHLER_TONSIGNALANLAGE | 0-n | high | unsigned char | - | TAB_MR_RES_LIN_FEHLER | - | - | - | Fehlerzustand in der Tonsignalanlage (LIN Signal ST_ERR_TOSQ_SYS_MOTBK_2010) |
| STAT_TONSIGNALANLAGE_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_LIN_AKTIVIERUNGSZUSTAND | - | - | - | Aktivierungszustand der Tonsignalanlage (LIN Signal ST_SPFN_ACUS_MOTBK_2010) |
| STAT_STROBOSKOPBLITZ_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_LIN_AKTIVIERUNGSZUSTAND | - | - | - | Aktivierungszustand Stroboskopblitz (LIN Signal CTR_PHLI_SPFLS_MOTBK_2010) |
| STAT_KOMM_FEHLER_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Kommunikationsfehler Tonsignalanlage (LIN Signal COMM_ERR_TSA_MOTBK_2010): 0 = kein Fehler, 1 = Fehler aktiv |

<a id="table-res-0xe165-d"></a>
### RES_0XE165_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Tonsignalanlage 0 = aus, 1 = ein |
| STAT_LAENDERCODE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_RES_COUNTRY_CODE | - | - | - | Status Ländercode Tonsequenz (LIN Signal CTR_CNCD_TOSQ_MOTBK_2010) |
| STAT_LAUTSTAERKE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_RES_TSA_VOLUME | - | - | - | Status Lautstärke Tonsequenz (LIN Signal CTR_AVOL_TOSQ_MOTBK_2010) |
| STAT_HUPE_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_HORN | - | - | - | SStatus Hupe aktiv (LIN Signal CTR_HORN_TOSQ_MOTBK_2010) |
| STAT_HUPENEMULATION_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_BEH_HORN_EMULATION | - | - | - | Status Hupenemulation aktiv (LIN Signal CTR_SUBST_HORN_TOSQ_MOTBK_2010) |
| STAT_SSL_MIDDLE_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der oberen Taste (C) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_UP_MOTBK_2010) |
| STAT_SSL_MIDDLE_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der unteren Taste (D) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_DWN_MOTBK_2010) |
| STAT_SSL_BOTTOM_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der oberen Taste (E) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_UP_MOTBK_2010) |
| STAT_SSL_BOTTOM_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der unteren Taste (F) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_DWN_MOTBK_2010) |
| STAT_KL_15_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Status LIN Signal ST_KL_15_MOTBK_2010 (LIN Signal ST_KL_15_MOTBK_2010) |
| STAT_KENNLEUCHTENZWANG_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_KL_ZWANG | - | - | - | Status des LIN Signals ST_IDEN_CONN_MOTBK_2010 |
| STAT_KENNLEUCHTEN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_AKTIV_LIN | - | - | - | Status des LIN Signals ST_IDEN_LI_MOTBK_2010 |

<a id="table-res-0xe167-d"></a>
### RES_0XE167_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BEHOERDENRELAIS | 0/1 | high | unsigned char | - | - | - | - | - | Status Ausgang Behördenrelais 0 = aus, 1 = ein |

<a id="table-res-0xe168-d"></a>
### RES_0XE168_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 01 |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 02 |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 03 |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 05 |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 07 |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 08 |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 09 |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 20 |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 21 |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 22 |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 23 |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 33 |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 34 |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 35 |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 36 |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 37 |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 46 |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 47 |

<a id="table-res-0xe169-d"></a>
### RES_0XE169_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WERKSTATTMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Status Werkstattmodus: 0 = aus, 1 = ein |

<a id="table-res-0xe16e-d"></a>
### RES_0XE16E_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 01 |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 02 |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 03 |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 05 |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 07 |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 08 |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 09 |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 20 |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 21 |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 22 |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 23 |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 33 |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 34 |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 35 |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 36 |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 37 |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 46 |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 47 |

<a id="table-res-0xe16f-d"></a>
### RES_0XE16F_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 01 |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 02 |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 03 |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 05 |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 07 |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 08 |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 09 |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 20 |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 21 |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 22 |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 23 |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 33 |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 34 |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 35 |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 36 |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 37 |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 46 |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 47 |

<a id="table-res-0xe170-d"></a>
### RES_0XE170_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL30_BEH | 0/1 | high | unsigned char | - | - | - | - | - | Status Klemme 30 Behörde: 0 = aus, 1 = ein |

<a id="table-res-0xe171-d"></a>
### RES_0XE171_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL15_BEH | 0/1 | high | unsigned char | - | - | - | - | - | Status Klemme 15 Behörde: 0 = aus, 1 = ein |

<a id="table-res-0xe172-d"></a>
### RES_0XE172_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTASTER_PIN_01 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 01 |
| STAT_FUNKTIONSTASTER_PIN_02 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 02 |
| STAT_FUNKTIONSTASTER_PIN_03 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 03 |
| STAT_FUNKTIONSTASTER_PIN_05 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 05 |
| STAT_FUNKTIONSTASTER_PIN_07 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 07 |
| STAT_FUNKTIONSTASTER_PIN_08 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 08 |
| STAT_FUNKTIONSTASTER_PIN_09 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 09 |
| STAT_FUNKTIONSTASTER_PIN_20 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 20 |
| STAT_FUNKTIONSTASTER_PIN_21 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 21 |
| STAT_FUNKTIONSTASTER_PIN_22 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 22 |
| STAT_FUNKTIONSTASTER_PIN_23 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 23 |
| STAT_FUNKTIONSTASTER_PIN_33 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 33 |
| STAT_FUNKTIONSTASTER_PIN_34 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 34 |
| STAT_FUNKTIONSTASTER_PIN_35 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 35 |
| STAT_FUNKTIONSTASTER_PIN_36 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 36 |
| STAT_FUNKTIONSTASTER_PIN_37 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 37 |
| STAT_FUNKTIONSTASTER_PIN_46 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 46 |
| STAT_FUNKTIONSTASTER_PIN_47 | 0-n | high | unsigned char | - | TAB_MR_PINZUORDNUNG | - | - | - | Status Zuordnung Funktionstaster zu Ausgangspin 47 |

<a id="table-res-0xe173-d"></a>
### RES_0XE173_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SSL_TOP_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (A) der oberen Wippe am linken Schalterblock |
| STAT_SSL_TOP_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (B) der oberen Wippe am linken Schalterblock |
| STAT_SSL_MIDDLE_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (C) der mittleren Wippe am linken Schalterblock |
| STAT_SSL_MIDDLE_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (D) der mittleren Wippe am linken Schalterblock |
| STAT_SSL_BOTTOM_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (E) der unteren Wippe am linken Schalterblock |
| STAT_SSL_BOTTOM_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (F) der unteren Wippe am linken Schalterblock |
| STAT_SSL_ROCKER_SWITCH_LEFT | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des linken Tasters/Schalters (G) der einzelnen Wippe am linken Schalterblock |
| STAT_SSL_ROCKER_SWITCH_RIGHT | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des rechten Tasters/Schalters (H) der einzelnen Wippe am linken Schalterblock |
| STAT_SSL_COMM_ERROR | 0/1 | high | unsigned char | - | - | - | - | - | Schalterblock Kommunikationsfehler: 0 = kein Fehler, 1 = Fehler vorhanden |

<a id="table-res-0xe174-d"></a>
### RES_0XE174_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SSR_TOP_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (I) der oberen Wippe am rechten Schalterblock |
| STAT_SSR_TOP_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (J) der oberen Wippe am rechten Schalterblock |
| STAT_SSR_MIDDLE_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (K) der mittleren Wippe am rechten Schalterblock |
| STAT_SSR_MIDDLE_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (L) der mittleren Wippe am rechten Schalterblock |
| STAT_SSR_BOTTOM_UP | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des oberen Tasters/Schalters (M) der unteren Wippe am rechten Schalterblock |
| STAT_SSR_BOTTOM_DOWN | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des unteren Tasters/Schalters (N) der unteren Wippe am rechten Schalterblock |
| STAT_SSR_ROCKER_SWITCH_LEFT | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des linken Tasters/Schalters (O) der einzelnen Wippe am rechten Schalterblock |
| STAT_SSR_ROCKER_SWITCH_RIGHT | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status des rechten Tasters/Schalters (P) der einzelnen Wippe am rechten Schalterblock |
| STAT_SSR_COMM_ERROR | 0/1 | high | unsigned char | - | - | - | - | - | Schalterblock Kommunikationsfehler: 0 = kein Fehler, 1 = Fehler vorhanden |

<a id="table-res-0xe175-d"></a>
### RES_0XE175_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_SCHALTERBLOCK | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Schalterblock 0 = aus, 1 = ein |
| STAT_PWM_SSL_TOP_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (A) der oberen Wippe am linken Schalterblock |
| STAT_PWM_SSL_TOP_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (B) der oberen Wippe am linken Schalterblock |
| STAT_PWM_SSL_MIDDLE_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (C) der mittleren Wippe am linken Schalterblock |
| STAT_PWM_SSL_MIDDLE_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (D) der mittleren Wippe am linken Schalterblock |
| STAT_PWM_SSL_BOTTOM_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (E) der unteren Wippe am linken Schalterblock |
| STAT_PWM_SSL_BOTTOM_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (F) der unteren Wippe am linken Schalterblock |

<a id="table-res-0xe176-d"></a>
### RES_0XE176_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_SCHALTERBLOCK | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Schalterblock 0 = aus, 1 = ein |
| STAT_PWM_SSR_TOP_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (I) der oberen Wippe am rechten Schalterblock |
| STAT_PWM_SSR_TOP_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (J) der oberen Wippe am rechten Schalterblock |
| STAT_PWM_SSR_MIDDLE_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (K) der mittleren Wippe am rechten Schalterblock |
| STAT_PWM_SSR_MIDDLE_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (L) der mittleren Wippe am rechten Schalterblock |
| STAT_PWM_SSR_BOTTOM_UP_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der oberen Taste (M) der unteren Wippe am rechten Schalterblock |
| STAT_PWM_SSR_BOTTOM_DOWN_WERT | % | high | unsigned char | - | - | 100.0 | 254.0 | 0.0 | PWM Wert Beleuchtung der unteren Taste (N) der unteren Wippe am rechten Schalterblock |

<a id="table-res-0xe177-d"></a>
### RES_0XE177_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_FUNKANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Funkanlage: 0 = aus, 1 = ein |
| STAT_KL_15_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Status LIN Signal ST_KL_15_MOTBK_2010 |
| STAT_TASTE_PTT_1 | 0/1 | high | unsigned char | - | - | - | - | - | Status der Taste PTT1 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTE_PTT_2 | 0/1 | high | unsigned char | - | - | - | - | - | Status der Taste PTT2 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_TASTE_PTT_3 | 0/1 | high | unsigned char | - | - | - | - | - | Status der Taste PTT3 in LIN Signal OP_PTT_MOTBK_2010: 0 = aus, 1 = ein |
| STAT_PTT_UNGUELTIG | 0/1 | high | unsigned char | - | - | - | - | - | Status SIGNAL UNGÜLTIG in LIN Signal OP_PTT_MOTBK_2010: 0 = nicht aktiv, 1 = aktiv |
| STAT_BEREICH_GESCHWINDIGKEIT | 0-n | high | unsigned char | - | TAB_MR_RES_GESCHWINDIGKEIT_BEREICH | - | - | - | Status des aktuellen Geschwindigkeitsbereich im LIN Signal CTR_DOM_V_MOTBK_2010 |
| STAT_MMC_LINKS_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_MMC_TASTER | - | - | - | Status Taster MMC links im LIN Signal CTR_MMC_LH_MOTBK_2010 |
| STAT_MMC_RECHTS_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_MMC_TASTER | - | - | - | Status Taster MMC rechts im LIN Signal CTR_MMC_RH_MOTBK_2010 |
| STAT_MMC_POSITION_WERT | Stufen | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Aktuelle MMC Position im LIN Signal CTR_MMC_PO_MOTBK_2010 |
| STAT_FUNKANLAGE_STROM_WERT | mA | high | int | - | - | 1.0 | 1.0 | 0.0 | Strom am Ausgang Funkanlage |
| STAT_FUNKANLAGE_SPANNUNG_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung am Ausgang Funkanlage |

<a id="table-res-0xe1a3-d"></a>
### RES_0XE1A3_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte vorne links: 0 = Versorgung aus, 1 = Versorgung ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |

<a id="table-res-0xe1a4-d"></a>
### RES_0XE1A4_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte vorne rechts 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010): 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010): 0 = aus, 1 = ein |

<a id="table-res-0xe1a5-d"></a>
### RES_0XE1A5_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte hinten links 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-res-0xe1a6-d"></a>
### RES_0XE1A6_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_BLITZKENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Blitzkennleuchte hinten rechts 0 = aus, 1 = ein |
| STAT_BLITZMUSTER_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BLITZMUSTER | - | - | - | Status Blitzmuster Kennleuchten (LIN Signal CTR_PHLI_MOD_MOTBK_2010) |
| STAT_SYNC_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SYNC | - | - | - | Status Synchronisierung Blitzkennleuchten (LIN Signal CTR_PHLI_SYNCN_MOTBK_2010) |
| STAT_SONDERFUNKTION_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_SOFU | - | - | - | Aktivierte Sonderfunktion Kennleuchten (LIN Signal CTR_PHLI_SPFN_MOTBK_2010) |
| STAT_HELLIGKEIT_KENNLEUCHTEN | 0-n | high | unsigned char | - | TAB_MR_RES_BKL_HELLIGKEIT | - | - | - | Status Helligkeit Kennleuchten (LIN Signal CTR_PHLI_BRIG_MOTBK_2010) |
| STAT_BLITZLEUCHTE_VL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_VR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte vorne rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HL_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten links (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_BLITZLEUCHTE_HR_VERBAUT | 0/1 | high | unsigned char | - | - | - | - | - | Blitzkennleuchte hinten rechts (LIN Signal ST_PHLI_AVLB_MOTBK_2010) 0 = nicht verbaut, 1 = verbaut |
| STAT_HAUPTFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_HAUPTFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Hauptfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_STD_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_VR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte vorne rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HL | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten links (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |
| STAT_NEBENFARBE_KENNLEUCHTE_HR | 0/1 | high | unsigned char | - | - | - | - | - | Nebenfarbe Blitzkennleuchte hinten rechts (LIN Signal CTR_CL_AUFN_MOTBK_2010) 0 = aus, 1 = ein |

<a id="table-res-0xe1a7-d"></a>
### RES_0XE1A7_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERSORGUNG_TONSIGNALANLAGE | 0/1 | high | unsigned char | - | - | - | - | - | Status Versorgungspin Tonsignalanlage 0 = aus, 1 = ein |
| STAT_LAENDERCODE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_RES_COUNTRY_CODE | - | - | - | Status Ländercode Tonsequenz (LIN Signal CTR_CNCD_TOSQ_MOTBK_2010) |
| STAT_LAUTSTAERKE_TONSEQUENZ | 0-n | high | unsigned char | - | TAB_MR_RES_TSA_VOLUME | - | - | - | Status Lautstärke Tonsequenz (LIN Signal CTR_AVOL_TOSQ_MOTBK_2010) |
| STAT_HUPE_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_HORN | - | - | - | SStatus Hupe aktiv (LIN Signal CTR_HORN_TOSQ_MOTBK_2010) |
| STAT_HUPENEMULATION_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_BEH_HORN_EMULATION | - | - | - | Status Hupenemulation aktiv (LIN Signal CTR_SUBST_HORN_TOSQ_MOTBK_2010) |
| STAT_SSL_MIDDLE_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der oberen Taste (C) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_UP_MOTBK_2010) |
| STAT_SSL_MIDDLE_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der unteren Taste (D) der mittleren Wippe am linken Schalterblock (LIN Signal OP_SSL_MID_DWN_MOTBK_2010) |
| STAT_SSL_BOTTOM_UP_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der oberen Taste (E) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_UP_MOTBK_2010) |
| STAT_SSL_BOTTOM_DOWN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_TASTER_LIN | - | - | - | Status der unteren Taste (F) der unteren Wippe am linken Schalterblock (LIN Signal OP_SSL_BOT_DWN_MOTBK_2010) |
| STAT_KL_15_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_KL_15_LIN | - | - | - | Status LIN Signal ST_KL_15_MOTBK_2010 (LIN Signal ST_KL_15_MOTBK_2010) |
| STAT_KENNLEUCHTENZWANG_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_KL_ZWANG | - | - | - | Status des LIN Signals ST_IDEN_CONN_MOTBK_2010 |
| STAT_KENNLEUCHTEN_AKTIV | 0-n | high | unsigned char | - | TAB_MR_RES_AKTIV_LIN | - | - | - | Status des LIN Signals ST_IDEN_LI_MOTBK_2010 |

<a id="table-res-0xfd06-d"></a>
### RES_0XFD06_D

Dimensions: 23 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MANUFACTURING_DATA_1_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_2_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_3_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_4_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_5_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_6_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_7_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_8_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_9_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_10_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_11_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_12_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_13_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_14_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_15_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_16_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_17_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_18_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_19_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_MANUFACTURING_DATA_20_WERT | Stufe | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | End Of Line  Manufacutering data |
| STAT_K0_SOCKET_CALIB_PARAM_WERT | Stufe | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | K0 Radio Equipment Calib Parameter |
| STAT_K1_SOCKET_CALIB_PARAM_WERT | Stufe | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | K1 Radio Equipment Calib Parameter |
| STAT_RADIO_CALIBRATION | 0-n | high | unsigned char | - | MR_TAB_BCA_CALIBRATION | - | - | - | Radio equipment calibration status: NOT_CALIBREATED (0) CALIBRATED (1) UNKNOWN (255) |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 96 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KALIBRIERUNG_AUSGANG_FUNKANLAGE | 0xB008 | - | Kalibrierung der Strommessung am Ausgang Funkanlage | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xB008_R |
| FUNKANLAGE_SELBSTTEST | 0xB009 | - | Selbsttest Funkanlage | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xB009_R |
| KL_15_HW_DIGITAL_MR | 0xE013 | STAT_KL_15_HW_DIGITAL_EIN | Status Klemme 15 Hardware digital | 0/1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| PRODUKTIONSMODE_MR | 0xE0FF | - | Produktionsmode interne Vorgabe RDZ MDZ | - | - | - | - | - | - | - | - | - | 2F | - | - |
| WECKLEITUNG_DIGITAL_MR | 0xE11C | STAT_WECKLEITUNG_DIGITAL_EIN | aktueller Zustand der  Weckleitung | 0/1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| BATTERIESPANNUNG_MR | 0xE142 | STAT_BATTERIESPANNUNG_WERT | Batteriespannung | V | - | - | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AUSGANG_NEBELSCHLUSSLEUCHTE | 0xE152 | - | Ausgang Nebelschlussleuchte | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE152_D | RES_0xE152_D |
| EINGANG_BLITZKENNLEUCHTE_VL | 0xE155 | - | Status Blitzkennleuchte vorne links | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE155_D |
| AUSGANG_BLITZKENNLEUCHTE_VL | 0xE156 | - | Ansteuerung Aktorik Blitzkennleuchte vorne links | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE156_D | RES_0xE156_D |
| EINGANG_BLITZKENNLEUCHTE_VR | 0xE157 | - | Status Blitzkennleuchte vorne rechts | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE157_D |
| AUSGANG_BLITZKENNLEUCHTE_VR | 0xE158 | - | Ansteuerung Aktorik Blitzkennleuchte vorne rechts | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE158_D | RES_0xE158_D |
| EINGANG_RUNDUMKENNLEUCHTE_HL | 0xE159 | - | Status Rundumkennleuchte hinten links | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE159_D |
| AUSGANG_RUNDUMKENNLEUCHTEN_HL | 0xE15A | - | Ansteuerung Aktorik Blitzkennleuchte hinten links | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE15A_D | RES_0xE15A_D |
| EINGANG_RUNDUMKENNLEUCHTEN_HR | 0xE15B | - | Status Rundumkennleuchte hinten rechts | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE15B_D |
| AUSGANG_RUNDUMKENNLEUCHTEN_HR | 0xE15C | - | Ansteuerung Aktorik Blitzkennleuchte hinten rechts | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE15C_D | RES_0xE15C_D |
| AUSGANG_STOPSIGNAL_VORNE | 0xE15E | - | Ausgang STOP vorne | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE15E_D | RES_0xE15E_D |
| AUSGANG_STOPSIGNAL_HINTEN | 0xE160 | - | Ausgang STOP hinten | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE160_D | RES_0xE160_D |
| AUSGANG_FOLGENSIGNAL_HINTEN | 0xE162 | - | Anhaltesignal hinten BITTE FOLGEN | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE162_D | RES_0xE162_D |
| EINGANG_TONSIGNALANLAGE | 0xE164 | - | Eingang Tonsignalanlage | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE164_D |
| AUSGANG_TONSIGNALANLAGE | 0xE165 | - | Ansteuerung der Tonsignalanlage | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE165_D | RES_0xE165_D |
| EINGANG_KL30_BEHOERDE | 0xE166 | STAT_KL30_BEH_WERT | Batteriespannung Pin 51 | V | - | high | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AUSGANG_BEHOERDENRELAIS | 0xE167 | - | Ausgang Behördenrelais | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE167_D | RES_0xE167_D |
| AUSGANG_FUNKTIONSTASTE_F4 | 0xE168 | - | Ausgang Funktionstaste F4 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE168_D | RES_0xE168_D |
| WERKSTATTMODUS | 0xE169 | - | Werkstattmodus Tonsignalanlage aktivieren | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE169_D | RES_0xE169_D |
| AUSGANG_FUNKTIONSTASTE_F2 | 0xE16E | - | Ausgang Funktionstaste F2 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE16E_D | RES_0xE16E_D |
| AUSGANG_FUNKTIONSTASTE_F1 | 0xE16F | - | Ausgang Funktionstaste F1 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE16F_D | RES_0xE16F_D |
| AUSGANG_KL30_BEHOERDE | 0xE170 | - | Ausgang KL30 Behörde | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE170_D | RES_0xE170_D |
| AUSGANG_KL15_BEHOERDE | 0xE171 | - | Ausgang KL15 Behörde | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE171_D | RES_0xE171_D |
| AUSGANG_FUNKTIONSTASTE_F3 | 0xE172 | - | Ausgang Funktionstaste F3 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE172_D | RES_0xE172_D |
| EINGANG_SCHALTERBLOCK_SONDERFUNKTION_LINKS | 0xE173 | - | Zustand der Tasten im Schalterblock Sonderfunktion links | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE173_D |
| EINGANG_SCHALTERBLOCK_SONDERFUNKTION_RECHTS | 0xE174 | - | Zustand der Tasten im Schalterblock Sonderfunktion rechts | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE174_D |
| AUSGANG_SCHALTERBLOCK_SONDERFUNKTION_LINKS | 0xE175 | - | PWM Ansteuerung der Tasterbeleuchtung Schalterblock Sonderfunktion links | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE175_D | RES_0xE175_D |
| AUSGANG_SCHALTERBLOCK_SONDERFUNKTION_RECHTS | 0xE176 | - | PWM Ansteuerung der Tasterbeleuchtung Schalterblock Sonderfunktion rechsts | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE176_D | RES_0xE176_D |
| AUSGANG_FUNKANLAGE | 0xE177 | - | Ausgang Funkanlage | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE177_D | RES_0xE177_D |
| AUSGANG_BLITZKENNLEUCHTE_VL_1 | 0xE1A3 | - | Ausgang Parameter für Blitzkennleuchte vorne links Teil 2 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE1A3_D | RES_0xE1A3_D |
| AUSGANG_BLITZKENNLEUCHTE_VR_1 | 0xE1A4 | - | Ausgang Parameter für Blitzkennleuchte vorne rechts Teil 2 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE1A4_D | RES_0xE1A4_D |
| AUSGANG_RUNDUMKENNLEUCHTEN_HL_1 | 0xE1A5 | - | Ausgang Parameter für Rundumkennleuchte hinten links Teil 2 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE1A5_D | RES_0xE1A5_D |
| AUSGANG_RUNDUMKENNLEUCHTEN_HR_1 | 0xE1A6 | - | Ausgang Parameter für Rundumkennleuchte hinten rechts Teil 2 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE1A6_D | RES_0xE1A6_D |
| AUSGANG_TONSIGNALANLAGE_1 | 0xE1A7 | - | Ausgang Parameter für Tonsignalanlage Teil 2 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xE1A7_D | RES_0xE1A7_D |
| _FUNKTION_ENTLASTUNG_KL50_EINGANG | 0x4000 | STAT_ST_KL_50_MOTBK_2010 | Wert vom CAN Signal ST_KL_50_MOTBK_2010 | 0-n | - | high | unsigned char | TAB_MR_RES_KL50 | - | - | - | - | 22 | - | - |
| _FUNKTION_ENTLASTUNG_KL50_AUSGANG | 0x4001 | - | Ausgangsparameter der Funktion Entlastung bei KL50 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4001_D | RES_0x4001_D |
| _FUNKTION_SPANNUNGSVERSORGUNG_ZUSATZSCHALTER_EINGANG | 0x4002 | - | Eingangsparameter für Funktion Spannungsversorgung Zusatzschaltereinheit | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4002_D |
| _FUNKTION_SPANNUNGSVERSORGUNG_ZUSATZSCHALTER_AUSGANG | 0x4003 | - | Ausgangsparameter der Funktion Spannungsversorgung Zusatzschaltereinheit | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4003_D | RES_0x4003_D |
| _FUNKTION_LICHT_AUS_EINGANG | 0x4004 | - | Eingangsparameter für Funktion Licht aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4004_D |
| _FUNKTION_LICHT_AUS_AUSGANG | 0x4005 | - | Ausgangsparameter der Funktion Licht aus | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4005_D | RES_0x4005_D |
| _FUNKTION_NEBELSCHLUSSLEUCHTE_EINGANG | 0x4006 | - | Eingangsparameter Funktion Nebelschlussleuchte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4006_D |
| _FUNKTION_NEBELSCHLUSSLEUCHTE_AUSGANG | 0x4007 | - | Ausgangsparameter der Funktion Nebelschlussleuchte | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4007_D | RES_0x4007_D |
| _FUNKTION_KENNLEUCHTEN_ALLGEMEIN_EINGANG | 0x4008 | - | Eingangsparameter für Funktion Kennleuchten allgemein | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4008_D |
| _FUNKTION_KENNLEUCHTEN_ALLGEMEIN_AUSGANG | 0x4009 | - | Ausgangsparameter der Funktion Kennleuchten allgemein | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4009_D | RES_0x4009_D |
| _FUNKTION_KENNLEUCHTE_VL_EINGANG | 0x400A | STAT_ST_VRS_PHLI_FLH_MOTBK_2010_WERT | Wert vom LIN Signal ST_VRS_PHLI_FLH_MOTBK_2010 (Firmware Version) | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_KENNLEUCHTE_VL_AUSGANG | 0x400B | - | Ausgangsparameter der Funktion LED Blitzkennleuchte vorne links | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x400B_D | RES_0x400B_D |
| _FUNKTION_KENNLEUCHTE_VR_EINGANG | 0x400C | STAT_ST_VRS_PHLI_FRH_MOTBK_2010_WERT | Wert vom LIN Signal ST_VRS_PHLI_FRH_MOTBK_2010 (Firmware Version) | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_KENNLEUCHTE_VR_AUSGANG | 0x400D | - | Ausgangsparameter der Funktion LED Blitzkennleuchte vorne rechts | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x400D_D | RES_0x400D_D |
| _FUNKTION_KENNLEUCHTE_HL_EINGANG | 0x400E | STAT_ST_VRS_PHLI_RLH_MOTBK_2010_WERT | Wert vom LIN Signal ST_VRS_PHLI_RLH_MOTBK_2010 (Firmware Version) | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_KENNLEUCHTE_HL_AUSGANG | 0x400F | - | Ausgangsparameter der Funktion Rundumkennleuchte hinten links | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x400F_D | RES_0x400F_D |
| _FUNKTION_KENNLEUCHTE_HR_EINGANG | 0x4010 | STAT_ST_VRS_PHLI_RRH_MOTBK_2010_WERT | Wert vom LIN Signal ST_VRS_PHLI_RRH_MOTBK_2010 (Firmware Version) | - | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_KENNLEUCHTE_HR_AUSGANG | 0x4011 | - | Ausgangsparameter der Funktion Rundumkennleuchte hinten rechts | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4011_D | RES_0x4011_D |
| _FUNKTION_STOP_VORNE_EINGANG | 0x4012 | - | Eingangsparameter der Funktion Anhaltesignal vorne Stop | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4012_D |
| _FUNKTION_STOP_VORNE_AUSGANG | 0x4013 | - | Ausgangsparameter der Funktion Anhaltesignal vorne Stop | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4013_D | RES_0x4013_D |
| _FUNKTION_STOP_HINTEN_EINGANG | 0x4014 | - | Eingangsparameter der Funktion Anahltesignal hinten Stop | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4014_D |
| _FUNKTION_STOP_HINTEN_AUSGANG | 0x4015 | - | Ausgangsparameter der Funktion  Anhaltesignal hinten Stop | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4015_D | RES_0x4015_D |
| _FUNKTION_FOLGEN_HINTEN_EINGANG | 0x4016 | - | Eingangsparameter der Funktion Anhaltesignal hinten Bitte folgen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4016_D |
| _FUNKTION_FOLGEN_HINTEN_AUSGANG | 0x4017 | - | Ausgangsparameter der Funktion Anhaltesignal hinten Bitte folgen | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4017_D | RES_0x4017_D |
| _FUNKTION_TASTE_F1_EINGANG | 0x4018 | - | Eingangsparameter der Funktion Funktionstaste F1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4018_D |
| _FUNKTION_TASTE_F1_AUSGANG | 0x4019 | - | Ausgangsparameter der Funktion Funktionstaste F1 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4019_D | RES_0x4019_D |
| _FUNKTION_TASTE_F2_EINGANG | 0x401A | - | Eingangsparameter der Funktion Funktionstaste F1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x401A_D |
| _FUNKTION_TASTE_F2_AUSGANG | 0x401B | - | Ausgangsparameter der Funktion Funktionstaste F2 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x401B_D | RES_0x401B_D |
| _FUNKTION_TASTE_F3_EINGANG | 0x401C | - | Eingangsparameter der Funktion Funktionstaste F3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x401C_D |
| _FUNKTION_TASTE_F3_AUSGANG | 0x401D | - | Ausgangsparameter der Funktion Funktionstaste F3 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x401D_D | RES_0x401D_D |
| _FUNKTION_TASTE_F4_EINGANG | 0x401E | - | Eingangsparameter der Funktion Funktionstaste F4 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x401E_D |
| _FUNKTION_TASTE_F4_AUSGANG | 0x401F | - | Ausgangsparameter der Funktion Funktionstaste F4 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x401F_D | RES_0x401F_D |
| _FUNKTION_TONSIGNALANLAGE_EINGANG | 0x4020 | - | Eingangsparameter der Funktion Tonsignalanlage | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4020_D |
| _FUNKTION_TONSIGNALANLAGE_AUSGANG | 0x4021 | - | Ausgangsparameter der Funktion Tonsignalanlage | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4021_D | RES_0x4021_D |
| _FUNKTION_FUNKANLAGE_EINGANG | 0x4022 | - | Eingangsparameter der Funktion Funkanlage | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4022_D |
| _FUNKTION_FUNKANLAGE_AUSGANG | 0x4023 | - | Ausgangsparameter der Funktion Funkanlage | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4023_D | RES_0x4023_D |
| _FUNKTION_KL15_EINGANG | 0x4024 | STAT_ST_KL_15_MOTBK_2010 | Wert vom CAN Signal ST_KL_15_MOTBK_2010 | 0-n | - | high | unsigned char | TAB_MR_RES_KL_15_LIN | - | - | - | - | 22 | - | - |
| _FUNKTION_KL15_AUSGANG | 0x4025 | - | Ausgangsparameter der Funktion KL15 | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4025_D | RES_0x4025_D |
| _FUNKTION_KL30_EINGANG | 0x4026 | STAT_ST_KL_15_MOTBK_2010 | Wert vom CAN Signal ST_KL_15_MOTBK_2010 | 0-n | - | high | unsigned char | TAB_MR_RES_KL_15_LIN | - | - | - | - | 22 | - | - |
| _FUNKTION_KL30_AUSGANG | 0x4027 | - | Ausgangsparameter der Funktion KL30 | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4027_D | RES_0x4027_D |
| _FUNKTION_BEHOERDENRELAIS_EINGANG | 0x4028 | - | Eingangsparameter der Funktion Behördenrelais | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4028_D |
| _FUNKTION_BEHOERDENRELAIS_AUSGANG | 0x4029 | - | Ausgangsparameter der Funktion Behördenrelais | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4029_D | RES_0x4029_D |
| _FUNKTION_SCHUTZ_TIEFENTLADUNG_EINGANG | 0x402A | STAT_BATTERIESPANNUNG_WERT | Status Batteriespannung Bordnetz | V | - | high | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_SCHUTZ_TIEFENTLADUNG_AUSGANG | 0x402B | - | Ausgangsparameter der Funktion Schutz vor Tiefentladung | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x402B_D | RES_0x402B_D |
| _FUNKTION_UEBERSPANNUNGSABSCHALTUNG_EINGANG | 0x402C | STAT_BATTERIESPANNUNG_WERT | Status Batteriespannung Bordnetz | V | - | high | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_UEBERSPANNUNGSABSCHALTUNG_AUSGANG | 0x402D | - | Ausgangsparameter der Funktion Überspannungsabschaltung | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x402D_D | RES_0x402D_D |
| _FUNKTION_UNTERSPANNUNGSABSCHALTUNG_EINGANG | 0x402E | STAT_BATTERIESPANNUNG_WERT | Status Batteriespannung Bordnetz | V | - | high | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| _FUNKTION_UNTERSPANNUNGSABSCHALTUNG_AUSGANG | 0x402F | - | Ausgangsparameter der Funktion Unterspannungsabschaltung | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x402F_D | RES_0x402F_D |
| _FUNKTION_ALTERNIERENDES_FRONTLICHT_EINGANG | 0x4030 | - | Eingangsparameter der Funktion Alternierendes Frontlicht | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4030_D |
| _FUNKTION_ALTERNIERENDES_FRONTLICHT_AUSGANG | 0x4031 | - | Ausgangsparameter der Funktion Alternierendes Frontlicht | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4031_D | RES_0x4031_D |
| _FUNKTION_UNITED_STATES_EINGANG | 0x4032 | - | Eingangsparameter der Funktion United States | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4032_D |
| _FUNKTION_UNITED_STATES_AUSGANG | 0x4033 | - | Ausgangsparameter der Funktion United States | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0x4033_D | RES_0x4033_D |
| _FUNKTION_GATEWAY_EINGANG | 0x4034 | - | Eingang Parameter für Funktion Gateway | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4034_D |
| _FUNKTION_GATEWAY_AUSGANG | 0x4035 | - | Ausgang Parameter für Funktion Gateway | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4035_D |
| _FUNKTION_UNITED_STATES_AUSGANG_1 | 0x4036 | - | Ausgang Parameter für Funktion United States | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0x4036_D | RES_0x4036_D |
| _RADIO_EQUIPMENT_CALIBRATION | 0x4037 | STAT_RADIO_EQUIP_CALIBRATION | Status radio equipment calibration: NOT_CALIBRATED (0) CALIBRATED (1) UNKNOWN (2) | 0-n | - | high | unsigned char | MR_TAB_BCA_CALIBRATION | - | - | - | - | 22 | - | - |
| END_OF_LINE_DATA | 0xFD06 | - | end of line data ( manufacturer specific) | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xFD06_D | RES_0xFD06_D |

<a id="table-svk-version-dop"></a>
### SVK_VERSION_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | SVKVersion_01 |

<a id="table-tab-mr-arg-aktiv-lin"></a>
### TAB_MR_ARG_AKTIV_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiv |
| 0x01 | Aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-beh-horn-emulation"></a>
### TAB_MR_ARG_BEH_HORN_EMULATION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupenemulation nicht angefordert |
| 0x01 | Hupenemulation angefordert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-bereich-geschwindigkeit"></a>
### TAB_MR_ARG_BEREICH_GESCHWINDIGKEIT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Geschwindigkeitsbereich langsam |
| 0x01 | Geschwindigkeitsbereich mittel |
| 0x02 | Geschwindigkeitsbereich schnell |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-bkl-helligkeit"></a>
### TAB_MR_ARG_BKL_HELLIGKEIT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Werkstattmodus |
| 0x01 | Nachtmodus |
| 0x02 | Tagmodus |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-bkl-sofu"></a>
### TAB_MR_ARG_BKL_SOFU

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Normalbetrieb |
| 0x02 | Kreuzungslicht |
| 0x03 | Rundumblinken |
| 0x04 | Cruising Light |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-arg-bkl-sync"></a>
### TAB_MR_ARG_BKL_SYNC

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Synchron |
| 0x02 | Alternierend |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-blitzmuster"></a>
### TAB_MR_ARG_BLITZMUSTER

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Stroboskop Blitz |
| 0x02 | Quattro Blitz 1 |
| 0x03 | Quattro Blitz 2 |
| 0x04 | Rundumblinken |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-arg-country-code"></a>
### TAB_MR_ARG_COUNTRY_CODE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DIN |
| 0x01 | Frankreich Polizei |
| 0x02 | Frankreich Gendarmerie |
| 0x03 | Niederlande 2 Ton |
| 0x04 | Italien Polizei |
| 0x05 | Österreich Polizei |
| 0x07 | Schweden |
| 0x08 | Sirene (ECE/HiLo) |
| 0x09 | Sirene (US/Airhorn) |
| 0x0A | Sirene (US/1-Tastenbedienung) |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-arg-hupe-lin"></a>
### TAB_MR_ARG_HUPE_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupe nicht aktiviert |
| 0x01 | Hupe aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-kl-15-lin"></a>
### TAB_MR_ARG_KL_15_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KL_15 aus |
| 0x01 | KL_15 ein |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-kl-zwang"></a>
### TAB_MR_ARG_KL_ZWANG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zwang nicht aktiv |
| 0x01 | Zwang aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-mmc-taster"></a>
### TAB_MR_ARG_MMC_TASTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Taster nicht gedrückt |
| 0x02 | Taster gedrückt |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-taster-lin"></a>
### TAB_MR_ARG_TASTER_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Taster nicht gedrückt |
| 0x01 | Taster gedrückt |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-arg-tsa-volume"></a>
### TAB_MR_ARG_TSA_VOLUME

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Leise |
| 0x02 | Mittel |
| 0x03 | Laut |
| 0x04 | Nachtabsenkung |
| 0x05 | Werkstattmodus |
| 0x06 | Reserviert |
| 0x07 | Reserviert |
| 0x08 | Reserviert |
| 0x09 | Reserviert |
| 0x0A | Reserviert |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-audio-menue"></a>
### TAB_MR_AUDIO_MENUE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Audio Menü nicht aktiv |
| 0x02 | Audio Menü aktiv |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-beh-horn-emulation"></a>
### TAB_MR_BEH_HORN_EMULATION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupenemulation nicht angefordert |
| 0x01 | Hupenemulation angefordert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-design"></a>
### TAB_MR_DESIGN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Tageinstellung |
| 0x02 | Nachteinstellung |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-hupe-lin"></a>
### TAB_MR_HUPE_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupe nicht aktiviert |
| 0x01 | Hupe aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-kl50"></a>
### TAB_MR_KL50

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KL_50 nicht aktiv |
| 0x01 | KL_50 aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-lin-fehler"></a>
### TAB_MR_LIN_FEHLER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler vorhanden |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-lin-leuchten"></a>
### TAB_MR_LIN_LEUCHTEN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Leuchte nicht aktiviert |
| 0x01 | Leuchte aktiviert und funktionsfähig |
| 0x02 | Leuchte defekt |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-pinzuordnung"></a>
### TAB_MR_PINZUORDNUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Pin nicht mit Taster verbunden |
| 0x01 | Pin mit Taster verbunden und nicht aktiv |
| 0x02 | Pin mit Taster verbunden und aktiv |
| 0xFF | Nicht definiert |

<a id="table-tab-mr-res-abl-status"></a>
### TAB_MR_RES_ABL_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Abblendlicht aus |
| 0x02 | Abblendlicht ein |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-aktiv-lin"></a>
### TAB_MR_RES_AKTIV_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiviert |
| 0x01 | Aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-audio-menue-can"></a>
### TAB_MR_RES_AUDIO_MENUE_CAN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Audio Menü nicht aktiv |
| 0x02 | Audio Menü aktiv |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-beh-horn-emulation"></a>
### TAB_MR_RES_BEH_HORN_EMULATION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupenemulation nicht angefordert |
| 0x01 | Hupenemulation angefordert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-bkl-farben"></a>
### TAB_MR_RES_BKL_FARBEN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Einfarbenleuchte |
| 0x01 | Zweifarbenleuchte |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-bkl-helligkeit"></a>
### TAB_MR_RES_BKL_HELLIGKEIT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Werkstattmodus |
| 0x01 | Nachtmodus |
| 0x02 | Tagmodus |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-bkl-sofu"></a>
### TAB_MR_RES_BKL_SOFU

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Normalbetrieb |
| 0x02 | Kreuzungslicht |
| 0x03 | Rundumblinken |
| 0x04 | Cruising Light |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-res-bkl-sync"></a>
### TAB_MR_RES_BKL_SYNC

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Synchron |
| 0x02 | Alternierend |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-bkl-typ"></a>
### TAB_MR_RES_BKL_TYP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Gerichtet |
| 0x02 | Rundum |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-blinker-status"></a>
### TAB_MR_RES_BLINKER_STATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Blinker aktiv |
| 0x01 | Blinker links aktiv |
| 0x02 | Blinker rechts aktiv |
| 0x03 | Warnblinken aktiv |
| 0x04 | Reserviert |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-res-blitzmuster"></a>
### TAB_MR_RES_BLITZMUSTER

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Stroboskop Blitz |
| 0x02 | Quattro Blitz 1 |
| 0x03 | Quattro Blitz 2 |
| 0x04 | Rundumblinken |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-res-bremsl-status"></a>
### TAB_MR_RES_BREMSL_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bremslicht aus |
| 0x01 | Bremslicht ein |
| 0x02 | Gefahrenbremslicht aktiv |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-bu-alt-frontl"></a>
### TAB_MR_RES_BU_ALT_FRONTL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Alternierendes Frontlicht nicht aktiv |
| 0x01 | Alternierendes Frontlicht aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-country-code"></a>
### TAB_MR_RES_COUNTRY_CODE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DIN |
| 0x01 | Frankreich Polizei |
| 0x02 | Frankreich Gendarmerie |
| 0x03 | Niederlande 2 Ton |
| 0x04 | Italien Polizei |
| 0x05 | Österreich Polizei |
| 0x07 | Schweden |
| 0x08 | Sirene (ECE/HiLo) |
| 0x09 | Sirene (US/Airhorn) |
| 0x0A | Sirene (US/1-Tastenbedienung) |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-res-design"></a>
### TAB_MR_RES_DESIGN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Tageinstellung |
| 0x02 | Nachteinstellung |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-ela"></a>
### TAB_MR_RES_ELA

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ELA Leitung nicht verbunden |
| 0x01 | ELA Leitung verbunden |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-fl-status"></a>
### TAB_MR_RES_FL_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Fernlicht aus |
| 0x02 | Fernlicht ein |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-geschwindigkeit-bereich"></a>
### TAB_MR_RES_GESCHWINDIGKEIT_BEREICH

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Geschwindigkeitsbereich langsam |
| 0x01 | Geschwindigkeitsbereich mittel |
| 0x02 | Geschwindigkeitsbereich schnell |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-helmstatus"></a>
### TAB_MR_RES_HELMSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Helm angeschlossen |
| 0x01 | Helm erkannt |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-hold-sig"></a>
### TAB_MR_RES_HOLD_SIG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Anhaltesignal nicht aktiviert |
| 0x01 | Anhaltesignal aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungueltig |

<a id="table-tab-mr-res-horn"></a>
### TAB_MR_RES_HORN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Hupe nicht aktiv |
| 0x01 | Hupe aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-kl15-lin"></a>
### TAB_MR_RES_KL15_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KL_15 aus |
| 0x01 | KL_15 ein |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-kl50"></a>
### TAB_MR_RES_KL50

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KL_50 nicht aktiv |
| 0x01 | KL_50 aktiv |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-kl-15-lin"></a>
### TAB_MR_RES_KL_15_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KL_15 aus |
| 0x01 | KL_15 ein |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-kl-zwang"></a>
### TAB_MR_RES_KL_ZWANG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zwang nicht aktiviert |
| 0x01 | Zwang aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-leuchten-fehler"></a>
### TAB_MR_RES_LEUCHTEN_FEHLER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Leuchte nicht aktiviert |
| 0x01 | Leuchte aktiviert und funktionsfähig |
| 0x02 | Leuchte defekt |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-licht-aus"></a>
### TAB_MR_RES_LICHT_AUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Licht aus aktiv |
| 0x02 | Licht aus nicht aktiv |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-lin-aktivierungszustand"></a>
### TAB_MR_RES_LIN_AKTIVIERUNGSZUSTAND

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiviert |
| 0x01 | Aktiviert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-lin-fehler"></a>
### TAB_MR_RES_LIN_FEHLER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler vorhanden |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-mmc-taster"></a>
### TAB_MR_RES_MMC_TASTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Taster nicht gedrückt |
| 0x02 | Taster gedrückt |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-parameterstatus"></a>
### TAB_MR_RES_PARAMETERSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Parameter im Auslieferzustand |
| 0x01 | Parameter verändert |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-pres-modus"></a>
### TAB_MR_RES_PRES_MODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Präsentationsmodus nicht aktiv |
| 0x02 | Präsentationsmodus aktiv |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-sonderblinken"></a>
### TAB_MR_RES_SONDERBLINKEN

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Sonderblinken |
| 0x01 | Blinken 1 Hz |
| 0x02 | Blinken 1.5 Hz |
| 0x03 | Blinken 2 Hz |
| 0x04 | Reserviert |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Signal ungültig |

<a id="table-tab-mr-res-taster-can"></a>
### TAB_MR_RES_TASTER_CAN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Taster nicht gedrückt |
| 0x02 | Taster gedrückt |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-taster-lin"></a>
### TAB_MR_RES_TASTER_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Taster nicht gedrückt |
| 0x01 | Taster gedrückt |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-tfl-status"></a>
### TAB_MR_RES_TFL_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Tagfahrlicht aus |
| 0x02 | Tagfahrlicht ein |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-res-tsa-volume"></a>
### TAB_MR_RES_TSA_VOLUME

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Leise |
| 0x02 | Mittel |
| 0x03 | Laut |
| 0x04 | Nachtabsenkung |
| 0x05 | Werkstattmodus |
| 0x06 | Reserviert |
| 0x07 | Reserviert |
| 0x08 | Reserviert |
| 0x09 | Reserviert |
| 0x0A | Reserviert |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-res-zustand-kennleuchten"></a>
### TAB_MR_RES_ZUSTAND_KENNLEUCHTEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zustand 1: Kennleuchte nicht aktiv |
| 0x01 | Zustand 2: Hauptfarbe aktiv |
| 0x02 | Zustand 3: Zweitfarbe aktiv |

<a id="table-tab-mr-routine-bca"></a>
### TAB_MR_ROUTINE_BCA

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Routine nicht gestartet |
| 0x01 | Routine läuft |
| 0x02 | Routine beendet ohne Fehler |
| 0x03 | Routine beendet mit Fehler |
| 0xFF | Nicht definiert |

<a id="table-tab-mr-taster-lin"></a>
### TAB_MR_TASTER_LIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht gedrückt |
| 0x01 | Gedrückt |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-tab-mr-tsa-code"></a>
### TAB_MR_TSA_CODE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DIN |
| 0x01 | Frankreich Polizei |
| 0x02 | Frankreich Gendarmerie |
| 0x03 | Niederlande 2 Ton |
| 0x04 | Italien Polizei |
| 0x05 | Österreich Polizei |
| 0x07 | Schweden |
| 0x08 | Sirene (ECE/HiLo) |
| 0x09 | Sirene (US/Airhorn) |
| 0x0A | Sirene (US/1-Tastenbedienung) |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-tsa-volume"></a>
### TAB_MR_TSA_VOLUME

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Leise |
| 0x02 | Mittel |
| 0x03 | Laut |
| 0x04 | Nachtabsenkung |
| 0x05 | Werkstattmodus |
| 0x06 | Reserviert |
| 0x07 | Reserviert |
| 0x08 | Reserviert |
| 0x09 | Reserviert |
| 0x0A | Reserviert |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig |

<a id="table-tab-mr-zustand-kennleuchte"></a>
### TAB_MR_ZUSTAND_KENNLEUCHTE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zustand 1: Kennleuchte nicht aktiv |
| 0x01 | Zustand 2: Hauptfarbe aktiv |
| 0x02 | Zustand 3: Zweitfarbe aktiv |
