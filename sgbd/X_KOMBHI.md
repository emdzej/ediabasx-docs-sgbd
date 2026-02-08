# X_KOMBHI.prg

- Jobs: [34](#jobs)
- Tables: [108](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Motorrad Instrumentenkombi Baukasten High |
| ORIGIN | BMW UX-EE-2 Hupens |
| REVISION | 0.014 |
| AUTHOR | Dräxlmaier UX-EE-1 Rätscher, In-Tech UX-EE-1 Tiefholz |
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
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [STATUS_IP_CONFIGURATION](#job-status-ip-configuration) - Reads out the actual ipconfig of the Ethernet interface of the HeadUnit.

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

<a id="job-status-ip-configuration"></a>
### STATUS_IP_CONFIGURATION

Reads out the actual ipconfig of the Ethernet interface of the HeadUnit.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FORMAT | unsigned char | 0x00  IPv4, 0x01  IPv6 |
| STAT_IPADDRESS | string | IP Adress e.g. 10.230.1.60 |
| STAT_NETMASK | string | Netmask e.g. 255.255.255.0 |
| STAT_GATEWAY | string | default Gateway Adress e.g. 10.230.1.1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
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
- [VERBAUORTTABELLE](#table-verbauorttabelle) (261 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (211 × 2)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [ARG_0X1023_R](#table-arg-0x1023-r) (1 × 14)
- [ARG_0X4000_D](#table-arg-0x4000-d) (2 × 12)
- [ARG_0XB011_R](#table-arg-0xb011-r) (2 × 14)
- [ARG_0XB012_R](#table-arg-0xb012-r) (1 × 14)
- [ARG_0XB053_R](#table-arg-0xb053-r) (1 × 14)
- [ARG_0XB054_R](#table-arg-0xb054-r) (1 × 14)
- [ARG_0XB055_R](#table-arg-0xb055-r) (1 × 14)
- [ARG_0XB05E_R](#table-arg-0xb05e-r) (8 × 14)
- [ARG_0XB05F_R](#table-arg-0xb05f-r) (8 × 14)
- [ARG_0XB062_R](#table-arg-0xb062-r) (1 × 14)
- [ARG_0XB065_R](#table-arg-0xb065-r) (1 × 14)
- [ARG_0XE07A_D](#table-arg-0xe07a-d) (1 × 12)
- [ARG_0XE119_D](#table-arg-0xe119-d) (1 × 12)
- [ARG_0XE125_D](#table-arg-0xe125-d) (1 × 12)
- [ARG_0XE126_D](#table-arg-0xe126-d) (1 × 12)
- [ARG_0XE127_D](#table-arg-0xe127-d) (1 × 12)
- [ARG_0XE129_D](#table-arg-0xe129-d) (1 × 12)
- [ARG_0XE12B_D](#table-arg-0xe12b-d) (6 × 12)
- [ARG_0XE12C_D](#table-arg-0xe12c-d) (3 × 12)
- [ARG_0XE12D_D](#table-arg-0xe12d-d) (1 × 12)
- [ARG_0XE1BD_D](#table-arg-0xe1bd-d) (2 × 12)
- [ARG_0XE1D6_D](#table-arg-0xe1d6-d) (1 × 12)
- [ARG_0XE1DB_D](#table-arg-0xe1db-d) (12 × 12)
- [ARG_0XE1DC_D](#table-arg-0xe1dc-d) (1 × 12)
- [ARG_0XE1E4_D](#table-arg-0xe1e4-d) (4 × 12)
- [ARG_0XE1EF_D](#table-arg-0xe1ef-d) (2 × 12)
- [ARG_0XF190_D](#table-arg-0xf190-d) (1 × 12)
- [BF_22_F152_SUPPLIERINFO](#table-bf-22-f152-supplierinfo) (2 × 10)
- [BT_DEVICE](#table-bt-device) (3 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [EXTERNAL_HSFZ_ACTIVATION_TAB](#table-external-hsfz-activation-tab) (2 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE_EREIGNIS_DTC](#table-forttexte-ereignis-dtc) (3 × 2)
- [FORTTEXTE](#table-forttexte) (31 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [HW_MODEL](#table-hw-model) (5 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [PROG_DEP_DOP](#table-prog-dep-dop) (6 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (10 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (4 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0XB004_R](#table-res-0xb004-r) (1 × 13)
- [RES_0XB054_R](#table-res-0xb054-r) (1 × 13)
- [RES_0XB055_R](#table-res-0xb055-r) (1 × 13)
- [RES_0XB062_R](#table-res-0xb062-r) (4 × 13)
- [RES_0XE07A_D](#table-res-0xe07a-d) (3 × 10)
- [RES_0XE119_D](#table-res-0xe119-d) (1 × 10)
- [RES_0XE120_D](#table-res-0xe120-d) (14 × 10)
- [RES_0XE121_D](#table-res-0xe121-d) (2 × 10)
- [RES_0XE125_D](#table-res-0xe125-d) (1 × 10)
- [RES_0XE126_D](#table-res-0xe126-d) (1 × 10)
- [RES_0XE127_D](#table-res-0xe127-d) (1 × 10)
- [RES_0XE129_D](#table-res-0xe129-d) (3 × 10)
- [RES_0XE12B_D](#table-res-0xe12b-d) (6 × 10)
- [RES_0XE12C_D](#table-res-0xe12c-d) (3 × 10)
- [RES_0XE12D_D](#table-res-0xe12d-d) (1 × 10)
- [RES_0XE1D6_D](#table-res-0xe1d6-d) (1 × 10)
- [RES_0XE1D7_D](#table-res-0xe1d7-d) (3 × 10)
- [RES_0XE1D8_D](#table-res-0xe1d8-d) (2 × 10)
- [RES_0XE1D9_D](#table-res-0xe1d9-d) (5 × 10)
- [RES_0XE1DA_D](#table-res-0xe1da-d) (3 × 10)
- [RES_0XE1DB_D](#table-res-0xe1db-d) (12 × 10)
- [RES_0XE1DC_D](#table-res-0xe1dc-d) (1 × 10)
- [RES_0XE1DD_D](#table-res-0xe1dd-d) (2 × 10)
- [RES_0XE1DE_D](#table-res-0xe1de-d) (3 × 10)
- [RES_0XE1DF_D](#table-res-0xe1df-d) (2 × 10)
- [RES_0XE1E0_D](#table-res-0xe1e0-d) (14 × 10)
- [RES_0XE1E2_D](#table-res-0xe1e2-d) (13 × 10)
- [RES_0XE1E3_D](#table-res-0xe1e3-d) (4 × 10)
- [RES_0XE1EF_D](#table-res-0xe1ef-d) (2 × 10)
- [RES_0XE211_D](#table-res-0xe211-d) (2 × 10)
- [RES_0XE212_D](#table-res-0xe212-d) (6 × 10)
- [RES_0XE213_D](#table-res-0xe213-d) (4 × 10)
- [RES_0XE214_D](#table-res-0xe214-d) (2 × 10)
- [RES_0XF152_D](#table-res-0xf152-d) (2 × 10)
- [RES_0XF190_D](#table-res-0xf190-d) (1 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (61 × 16)
- [SVK_VERSION_DOP](#table-svk-version-dop) (2 × 2)
- [TAB_BLUETOOTH_STAT](#table-tab-bluetooth-stat) (3 × 2)
- [TAB_BT](#table-tab-bt) (5 × 2)
- [TAB_BT_ERKENNUNGSMODUS_MR](#table-tab-bt-erkennungsmodus-mr) (3 × 2)
- [TAB_DLT](#table-tab-dlt) (3 × 2)
- [TAB_GANG](#table-tab-gang) (8 × 2)
- [TAB_GANG_ARG](#table-tab-gang-arg) (7 × 2)
- [TAB_KLANGZEICHEN_MR](#table-tab-klangzeichen-mr) (4 × 2)
- [TAB_MMC_BED](#table-tab-mmc-bed) (4 × 2)
- [TAB_MR_KONTROLLLEUCHTE](#table-tab-mr-kontrollleuchte) (16 × 2)
- [TAB_MR_ROUTINE](#table-tab-mr-routine) (4 × 2)
- [TAB_SENKE](#table-tab-senke) (2 × 2)
- [TAB_TESTBILDER](#table-tab-testbilder) (19 × 2)

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 261 rows × 3 columns

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
| 0x2210 | Aussenspiegel Fahrer | 1 |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2310 | Aussenspiegel Beifahrer | 1 |
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
| 0x3D10 | Aktiver Kühlluftklappensteller oberer Kühllufteinlass | 1 |
| 0x3D20 | Aktiver Kühlluftklappensteller unterer Kühllufteinlass | 1 |
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
| 0x4C80 | Klimabedienteil 3. Sitzreihe | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6180 | LIN-Zusatzwasserpumpe | 1 |
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
| 0x5A40 | Innenlichteinheit 4 | 1 |
| 0x5A50 | Innenlichteinheit 5 | 1 |
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
| 0x5EC0 | Thermocupholder | 1 |
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
| 0x7700 | Booster | 1 |
| 0x7800 | Dualspeicher | 1 |
| 0x7900 | Tablet | - |
| 0x7A00 | Beschleunigungssensor vorne links | 1 |
| 0x7A08 | Beschleunigungssensor vorne rechts | 1 |
| 0x7A10 | Beschleunigungssensor hinten links | 1 |
| 0x7A18 | Beschleunigungssensor hinten rechts | 1 |
| 0x7A20 | Abdeckrollo-Steuergerät | 1 |
| 0x7A28 | Schalterblock Gepäckraum | 1 |
| 0x7A30 | Unteres Heckklappenschloss links | 1 |
| 0x7A38 | Unteres Heckklappenschloss rechts | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 211 rows × 2 columns

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
| 0x0016 | Renesas Technology Europe GmbH (formerly Mitsubishi) |
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
| 0x0028 | Renesas Technology Europe Ltd (formerly Hitachi) |
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
| 0x0065 | INTEVA Products, LLC (formerly Arvinmeritor 2011-03-29) |
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
| 0x00B0 | Hanon Systems Korea |
| 0x00B1 | Eberspächer Controls Esslingen GmbH & Co. KG |
| 0x00B2 | WABCO Development GmbH |
| 0x00B3 | Sensirion AG |
| 0x00B4 | OSHINO Electronics Estonia OÜ |
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

<a id="table-arg-0x1023-r"></a>
### ARG_0X1023_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ACTIVATION | + | - | 0-n | high | unsigned char | - | EXTERNAL_HSFZ_ACTIVATION_TAB | - | - | - | - | - | Aktiviert bzw. deaktiviert den externen HSFZ. |

<a id="table-arg-0x4000-d"></a>
### ARG_0X4000_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ACTIVATION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktivierung/ Deaktivierung der CCM |
| CCM_PRIO_ID | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | ID der CCM (Priorität) |

<a id="table-arg-0xb011-r"></a>
### ARG_0XB011_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_FREQUENZ | + | - | Hz | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 20.0 | 20000.0 | Frequenzeinstellung 20...20000Hz |
| ARG_SENKE | + | - | 0-n | high | unsigned long | - | TAB_SENKE | - | - | - | - | - | Kanal Signalausgabe |

<a id="table-arg-0xb012-r"></a>
### ARG_0XB012_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_LEVEL | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 20.0 | Lautstärkewert  Wertebereich 0...20 |

<a id="table-arg-0xb053-r"></a>
### ARG_0XB053_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_KLANGZEICHEN_MR | + | - | 0-n | high | unsigned char | - | TAB_KLANGZEICHEN_MR | - | - | - | - | - | Legt das auszugebene Signal fest (siehe Tabelle) |

<a id="table-arg-0xb054-r"></a>
### ARG_0XB054_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT | + | - | 0-n | high | unsigned char | - | TAB_BLUETOOTH_STAT | - | - | - | - | - | setzt den Bluetooth Status |

<a id="table-arg-0xb055-r"></a>
### ARG_0XB055_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_ERKENNUNGSMODUS_MR | + | - | 0-n | high | unsigned char | - | TAB_BT_ERKENNUNGSMODUS_MR | - | - | - | - | - | Steuert den Bluetooth Erkennungsmodus |

<a id="table-arg-0xb05e-r"></a>
### ARG_0XB05E_R

Dimensions: 8 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHANNEL | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Kanal 0..79, 255=hopping |
| DATA_PATTERN | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Data Pattern |
| TRANSMIT_INTERVAL | + | - | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Übertragungsinterval Quantisierung 1,25ms |
| DATA_LENGTH | + | - | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Datei Laenge |
| PAKET_TYPE | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Paket Typ |
| TX_POWER | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 20.0 | -12.0 | 20.0 | TX Power -20..12dB |
| WHITENING | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aufhellung 0x01 on 0x00 off |
| TX_ADRESS | + | - | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | - | - | TX Adresse |

<a id="table-arg-0xb05f-r"></a>
### ARG_0XB05F_R

Dimensions: 8 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHANNEL | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Kanal 0..79, 255=hopping |
| DATA_PATTERN | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Data Pattern |
| TRANSMIT_INTERVAL | + | - | ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | BT Übertragungsinterval Quantisierung 1,25ms |
| DATA_LENGTH | + | - | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Datei Laenge |
| PAKET_TYPE | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Paket Typ |
| TX_POWER | + | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 20.0 | -12.0 | 20.0 | TX Power -20..12dB |
| WHITENING | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aufhellung  0x01 on 0x00 off |
| TX_ADRESS | + | - | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | - | - | TX Adresse |

<a id="table-arg-0xb062-r"></a>
### ARG_0XB062_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BT_DEVICE | + | - | 0-n | high | unsigned char | - | BT_DEVICE | - | - | - | - | - | Selector for the connected device |

<a id="table-arg-0xb065-r"></a>
### ARG_0XB065_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DLT_STATUS | + | - | 0-n | high | unsigned char | - | TAB_DLT | - | - | - | - | - | Aktiviert / deaktiviert DLT-Ausgabe DLT ON / DLT OFF |

<a id="table-arg-0xe07a-d"></a>
### ARG_0XE07A_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TANKINHALT | Liter | - | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | Fuer interne Funktionslogik zu nutzender Tankinhalt für Tankanzeige |

<a id="table-arg-0xe119-d"></a>
### ARG_0XE119_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GWSZ_SCHREIBEN | km | - | signed long | - | - | 1.0 | 1.0 | 0.0 | 0.0 | - | GWSZ im Kombi auf neuen Wert setzen |

<a id="table-arg-0xe125-d"></a>
### ARG_0XE125_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DREHZAHL | 1/min | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der aktuell im Kombi anzuzeigenden Drehzahl |

<a id="table-arg-0xe126-d"></a>
### ARG_0XE126_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GESCHWINDIGKEIT | km/h | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der aktuell im Kombi anzuzeigenden Geschwindigkeit |

<a id="table-arg-0xe127-d"></a>
### ARG_0XE127_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GANG | 0-n | - | unsigned char | - | TAB_GANG_ARG | 1.0 | 1.0 | 0.0 | - | - | Vorgabe des aktuell im Kombi anzuzeigenden Ganges Vorgabewerte gemäß Tabelle TAB_GANG N == Neutral; 1 == 1. Gang; 2 == 2. Gang; 3 == 3. Gang; 4 == 4. Gang; 5 == 5. Gang; 6 == 6. Gang |

<a id="table-arg-0xe129-d"></a>
### ARG_0XE129_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MOTORTEMPERATUR | °C | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | fuer interne Funktionslogik zu nutzende Motortemperatur |

<a id="table-arg-0xe12b-d"></a>
### ARG_0XE12B_D

Dimensions: 6 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KOMBI_STUNDE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 23.0 | Stunde |
| KOMBI_MINUTE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 59.0 | Minute |
| KOMBI_SEKUNDE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 59.0 | Sekunde |
| KOMBI_TAG_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | 1.0 | 31.0 | Tag |
| KOMBI_MONAT_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | 1.0 | 12.0 | Monat |
| KOMBI_JAHR_WERT | - | - | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | Jahr |

<a id="table-arg-0xe12c-d"></a>
### ARG_0XE12C_D

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SERVICE_TAG | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | - | - | Tag, an dem der nächste Service fällig ist |
| SERVICE_MONAT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | - | - | Monat, an dem der nächste Service fällig ist |
| SERVICE_JAHR | - | - | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | Jahr, an dem der nächste Service fällig ist |

<a id="table-arg-0xe12d-d"></a>
### ARG_0XE12D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RESTWEG | km | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Setzen des Wegstreckenintervalles bis zur nächsten Seviceanzeige |

<a id="table-arg-0xe1bd-d"></a>
### ARG_0XE1BD_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KONTROLLLEUCHTE | 0-n | high | unsigned char | - | TAB_MR_KONTROLLLEUCHTE | - | - | - | - | - | Aktive Kontrollleuchte |
| EIN_AUS | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0 = aus, 1 = ein |

<a id="table-arg-0xe1d6-d"></a>
### ARG_0XE1D6_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL_TESTBILD | 0-n | high | unsigned int | - | TAB_TESTBILDER | - | - | - | - | - | Auswahl der anzusteuernden Testbilder |

<a id="table-arg-0xe1db-d"></a>
### ARG_0XE1DB_D

Dimensions: 12 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DISPLAY_BACKLIGHT_PERCENTAGE_1_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level in Prozent |
| ARG_DISPLAY_BACKLIGHT_PERCENTAGE_2_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level in Prozent |
| ARG_TELLTALE_YELLOW_PERCENTAGE_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level TELLTALE_YELLOW_PERCENTAGE in Prozent |
| ARG_TELLTALE_RED_PERCENTAGE_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level TELLTALE_RED_PERCENTAGE in Prozent |
| ARG_TELLTALE_GREEN_PERCENTAGE_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level TELLTALE_GREEN_PERCENTAGE in Prozent |
| ARG_TELLTALE_WHITE_PERCENTAGE_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | - | PWM Level TELLTALE_WHITE_PERCENTAGE in Prozent |
| ARG_DISPLAY_BACKLIGHT_PWM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert 1 |
| ARG_DISPLAY_BACKLIGHT_PWM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert 2 |
| ARG_TELLTALE_YELLOW_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert TELLTALE_YELLOW_PWM |
| ARG_TELLTALE_RED_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert TELLTALE_RED_PWM |
| ARG_TELLTALE_GREEN_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert TELLTALE_GREEN_PWM |
| ARG_TELLTALE_WHITE_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Aktueller PWM Wert TELLTALE_WHITE_PWM |

<a id="table-arg-0xe1dc-d"></a>
### ARG_0XE1DC_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_HELLIGKEITSSENSOR_WERT | % | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | - | 100.0 | Schreiben des Helligkeitssensors in Prozent |

<a id="table-arg-0xe1e4-d"></a>
### ARG_0XE1E4_D

Dimensions: 4 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_ADDRESS_FORMAT_ID | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Address-Format-Id ist 0x00 für IPv4 oder 0x01 für IPv6 |
| ARG_IP | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | ip-Adresse Beispiel 192.168.100.2 |
| ARG_SUBNETMASK | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Subnetzmaske       Beispiel 255.255.0.0 |
| ARG_GATEWAY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | gateway;    192.168.0.254 |

<a id="table-arg-0xe1ef-d"></a>
### ARG_0XE1EF_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_GERAETENAME_1 | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | Name BT-Gerät 1 |
| ARG_BT_GERAETENAME_2 | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | Name BT-Gerät 2 |

<a id="table-arg-0xf190-d"></a>
### ARG_0XF190_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FGNR17 | TEXT | - | string[17] | - | - | 1.0 | 1.0 | 0.0 | - | - | 17-stellige Fahrgestellnummer |

<a id="table-bf-22-f152-supplierinfo"></a>
### BF_22_F152_SUPPLIERINFO

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HWMODEL | 0-n | high | unsigned char | 0xC0 | HW_MODEL | - | - | - | hardware model |
| STAT_SUPPLIERINFOFIELD | 0-n | high | unsigned char | 0x3F | - | - | - | - | supplierInfo |

<a id="table-bt-device"></a>
### BT_DEVICE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Smartphone |
| 1 | Rider Helmet |
| 2 | Pillion Helmet |

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

<a id="table-external-hsfz-activation-tab"></a>
### EXTERNAL_HSFZ_ACTIVATION_TAB

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | activate external HSFZ |
| 0x01 | deactivate external HSFZ |

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

<a id="table-forttexte-ereignis-dtc"></a>
### FORTTEXTE_EREIGNIS_DTC

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DTC kein Ereignis DTC |
| 1 | DTC ist Ereignis DTC |
| 0xFF | Wert ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 31 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x026000 | Energiesparmode aktiv | 0 |
| 0x026008 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x026009 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02600A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02600C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x02600D | Codierung: Codierdaten nicht qualifiziert | 0 |
| 0x026020 | CAN Control Module Bus OFF | 0 |
| 0x026023 | LIN Fehler (SW, HW) | 0 |
| 0x026024 | NVM_E_HARDWARE | 0 |
| 0xB7F610 | Kilometerstand  manipuliert | 0 |
| 0xB7F63C | LIN LIN to Bluetooth Zeitüberschreitung | 0 |
| 0xE10515 | MR-CAN  Physikalischer Busfehler | 0 |
| 0xE10516 | MR-CAN Control Module Bus OFF | 0 |
| 0xE11422 | CAN ABSBCO Nachricht Geschwindigkeit_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11424 | CAN DME Nachricht Klemmenstatus_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11428 | CAN DME Nachricht Motordaten_1_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE1142A | CAN DME Nachricht Motordaten_2_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11432 | CAN DWA Nachricht Status_DWA_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11434 | CAN FSA-BCO Nachricht Status_Erweitert_Funktion_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE11436 | CAN SLZ Nachricht Status_Fahrzeug_Zugriff_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE11438 | CAN ESA-SAF Nachricht Status_Federbein_Verstellung_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE1143A | CAN BCO Nachricht Status_Grund_Funktion_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE1143C | CAN RDC Nachricht Status_RDC_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11440 | CAN DME Nachricht Wegstrecke_Redundant_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11442 | CAN ABS-BCO Nachricht Wegstrecke_Relativ_Motorrad_2010: Zeitüberschreitung | 1 |
| 0xE11446 | CAN DME Nachricht Modus_Fahrzeug_Motorrad_2010 - Zeitüberschreitung | 1 |
| 0xE11454 | CAN ABSBCO Nachricht Geschwindigkeit_Motorrad_2010: CRC Fehler | 1 |
| 0xE11455 | CAN ABSBCO Nachricht Geschwindigkeit_Motorrad_2010: Alive Fehler | 1 |
| 0xE11456 | CAN DME Nachricht Modus_Fahrzeug_Motorrad_2010  CRC Fehler | 1 |
| 0xE11457 | CAN DME Nachricht Modus_Fahrzeug_Motorrad_2010  Alive Fehler | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-hw-model"></a>
### HW_MODEL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | A-Muster |
| 0x40 | B-Muster |
| 0x80 | C-Muster |
| 0xC0 | D-Muster |
| 0xFF | Wert ungültig |

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

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ISOSAEReserved_00 |
| 0x01 | defaultSession |
| 0x02 | programmingSession |
| 0x03 | extendedDiagnosticSession |
| 0x04 | safetySystemDiagnosticSession |
| 0x40 | vehicleManufacturerSpecific_40 |
| 0x41 | codingSession |
| 0x42 | SWTSession |
| 0x43 | HDDUpdateSession |
| 0xff | ungültig |

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECU mehrmals programmierbar |
| 0x01 | ECU mindestens einmal vollstaendig programmierbar |
| 0x02 | ECU nicht mehr programmierbar |
| 0xff | ungültig |

<a id="table-res-0x2502-d"></a>
### RES_0X2502_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESERVE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserve. Konstante = 0x00 |
| STAT_PROG_ZAEHLER_STATUS | 0-n | high | unsigned char | - | RDBI_PC_PCS_DOP | - | - | - | ProgrammingCounterStatus |
| STAT_PROG_ZAEHLER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ProgrammingCounter |

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

<a id="table-res-0xb004-r"></a>
### RES_0XB004_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | - | - | + | 0-n | high | unsigned char | - | TAB_MR_ROUTINE | - | - | - | Aktueller Zustand Routine |

<a id="table-res-0xb054-r"></a>
### RES_0XB054_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT | - | - | + | 0-n | high | unsigned char | - | TAB_BLUETOOTH_STAT | - | - | - | setzt den Bluetooth Status |

<a id="table-res-0xb055-r"></a>
### RES_0XB055_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_ERKENNUNGSMODUS_MR | - | - | + | 0-n | high | unsigned char | - | TAB_BT_ERKENNUNGSMODUS_MR | - | - | - | Steuert den Bluetooth Erkennungsmodus |

<a id="table-res-0xb062-r"></a>
### RES_0XB062_R

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_DEVICE | + | - | - | 0-n | high | unsigned char | - | BT_DEVICE | - | - | - | Copy of input parameter to specify the type of the device this link key belongs to |
| STAT_MAC_ADRESS_DATA | + | - | - | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | Bluetooth address of the remote device; 00:00:00:00:00:00 if no such device is connected) |
| STAT_LINK_KEY_DATA | + | - | - | DATA | high | data[16] | - | - | 1.0 | 1.0 | 0.0 | Link key used for the connection; all-00s if no such device is connected |
| STAT_TYPE_WERT | + | - | - | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Type of the returned link key; 00 if no such device is connected |

<a id="table-res-0xe07a-d"></a>
### RES_0XE07A_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TANKINHALT_CAN_WERT | Liter | - | unsigned int | - | - | 1.0 | 10.0 | 0.0 | aktueller Tankinhalt vom CAN-Bus |
| STAT_TANKINHALT_KOMBIINTERN_WERT | Liter | - | unsigned int | - | - | 1.0 | 10.0 | 0.0 | aktuell kombiintern fuer Funktionslogik genutzer Tankinhalt |
| STAT_TANKANZ_BALKEN_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Tankanzeige: im Kombi angezeigte Balken |

<a id="table-res-0xe119-d"></a>
### RES_0XE119_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GWSZ_WERT | km | - | signed long | - | - | 1.0 | 1.0 | 0.0 | aktueller GWSZ-Wert |

<a id="table-res-0xe120-d"></a>
### RES_0XE120_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WIPPE_RE_AB | 0/1 | - | unsigned int | 0x0001 | - | 1.0 | 1.0 | 0.0 | Wippschalter rechts abwärts (Windschild ab) 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_WIPPE_RE_AUF | 0/1 | - | unsigned int | 0x0002 | - | 1.0 | 1.0 | 0.0 | Wippschalter rechts aufwärts (Windschild auf) 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_RE | 0/1 | - | unsigned int | 0x0004 | - | 1.0 | 1.0 | 0.0 | Taster rechts (Warnblinktaster) 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_TEMPOMAT_EIN | 0/1 | - | unsigned int | 0x0008 | - | 1.0 | 1.0 | 0.0 | Tempomat ein 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_BLINKER_LI | 0/1 | - | unsigned int | 0x0010 | - | 1.0 | 1.0 | 0.0 | Blinker links 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_BLINKER_RE | 0/1 | - | unsigned int | 0x0020 | - | 1.0 | 1.0 | 0.0 | Blinker rechts 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_BLINKER_RUECKSTELL | 0/1 | - | unsigned int | 0x0040 | - | 1.0 | 1.0 | 0.0 | Blinker Rückstellung 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_HORN | 0/1 | - | unsigned int | 0x0080 | - | 1.0 | 1.0 | 0.0 | Horn 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_TEMPOMAT_VERZOEGERN | 0/1 | - | unsigned int | 0x0400 | - | 1.0 | 1.0 | 0.0 | Tempomat Verzögern 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_TEMPOMAT_BESCHLEUNIGEN | 0/1 | - | unsigned int | 0x0800 | - | 1.0 | 1.0 | 0.0 | Tempomat Beschleunigen 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_WIPPE_LI_AB | 0/1 | - | unsigned int | 0x1000 | - | 1.0 | 1.0 | 0.0 | Wippschalter links abwärts 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_WIPPE_LI_AUF | 0/1 | - | unsigned int | 0x2000 | - | 1.0 | 1.0 | 0.0 | Wippschalter links aufwärts 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_LI | 0/1 | - | unsigned int | 0x4000 | - | 1.0 | 1.0 | 0.0 | Taster links 1: Taster gedrueckt 0: Taster nicht gedrueckt |
| STAT_TASTE_FERNLICHT | 0/1 | - | unsigned int | 0x0200 | - | 1.0 | 1.0 | 0.0 | Fernlicht 1: Taster gedrueckt 0: Taster nicht gedrueckt |

<a id="table-res-0xe121-d"></a>
### RES_0XE121_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MMC_BEDIENUNG | 0-n | - | unsigned char | 0x02 | TAB_MMC_BED | 1.0 | 1.0 | 0.0 | Betätigungsrichtung des MMC: |
| STAT_MMC_POSITION_WERT | Schritte | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Position des MMC 0..254 |

<a id="table-res-0xe125-d"></a>
### RES_0XE125_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DREHZAHL_WERT | 1/min | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aktuell im Kombi angezeigte Drehzahl |

<a id="table-res-0xe126-d"></a>
### RES_0XE126_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GESCHWINDIGKEIT_WERT | km/h | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aktuell im Kombi angezeigte Geschwindigkeit |

<a id="table-res-0xe127-d"></a>
### RES_0XE127_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GANG | 0-n | - | unsigned char | - | TAB_GANG | 1.0 | 1.0 | 0.0 | aktuell im Kombi angezeigter Gang Anzeige gemäß Tabelle TAB_GANG N == Neutral; 1 == 1. Gang; 2 == 2. Gang; 3 == 3. Gang; 4 == 4. Gang; 5 == 5. Gang; 6 == 6. Gang |

<a id="table-res-0xe129-d"></a>
### RES_0XE129_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MOTORTEMP_CAN_WERT | °C | - | signed int | - | - | 1.0 | 1.0 | 0.0 | aktuelle Motortemperatur vom CAN-Bus |
| STAT_MOTORTEMP_KOMBIINTERN_WERT | °C | - | signed int | - | - | 1.0 | 1.0 | 0.0 | aktuell kombiintern fuer Funktionslogik genutze Motortemperatur |
| STAT_MOTORTEMP_BALKEN_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Motortemperatur-Anzeige im Kombi angezeigte Balken |

<a id="table-res-0xe12b-d"></a>
### RES_0XE12B_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KOMBI_STUNDE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe der aktuellen Stunde |
| STAT_KOMBI_MINUTE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe der aktuellen Minute |
| STAT_KOMBI_SEKUNDE_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe der aktuellen Sekunde |
| STAT_KOMBI_TAG_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des aktuellen Tag |
| STAT_KOMBI_MONAT_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des aktuellen Monat |
| STAT_KOMBI_JAHR_WERT | - | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Rückgabe des aktuellen Jahr |

<a id="table-res-0xe12c-d"></a>
### RES_0XE12C_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SERVICE_TAG_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Tag, an dem der nächste Service fällig ist |
| STAT_SERVICE_MONAT_WERT | - | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Monat, an dem der nächste Service fällig ist |
| STAT_SERVICE_JAHR_WERT | - | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Jahr, an dem der nächste Service fällig ist |

<a id="table-res-0xe12d-d"></a>
### RES_0XE12D_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESTWEG_WERT | km | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | verbleibendes Wegstreckenintervall bis wegabhängiger Service als überfällig angezeigt wird |

<a id="table-res-0xe1d6-d"></a>
### RES_0XE1D6_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSWAHL_TESTBILD | 0-n | high | unsigned int | - | TAB_TESTBILDER | - | - | - | Auswahl der anzusteuernden Testbilder |

<a id="table-res-0xe1d7-d"></a>
### RES_0XE1D7_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VALUE_1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -100.0 | Interne Temperatur Wert 1 |
| STAT_VALUE_2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -100.0 | Interne Temperatur Wert 2 |
| STAT_VALUE_3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -100.0 | Interne Temperatur Wert 3 |

<a id="table-res-0xe1d8-d"></a>
### RES_0XE1D8_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MCU_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 1.0 | Auslastung des MCU |
| STAT_GPU_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 1.0 | Auslastung des GPU |

<a id="table-res-0xe1d9-d"></a>
### RES_0XE1D9_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CAN_EINGANGSWERT_WERT | l | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | CAN Eingangswert |
| STAT_INTERNER_KOMBIWERT_WERT | l | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Interner Kombiwert |
| STAT_NUMBER_OF_TOTAL_BARS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gesamtanzahl der Balken |
| STAT_NUMBER_OF_FILLED_BARS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl ausgefüllter Balken |
| STAT_FUELLSTATUS_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Füllstatus |

<a id="table-res-0xe1da-d"></a>
### RES_0XE1DA_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADC_VALUE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC Wert |
| STAT_HELLIGKEIT_IN_PROZENT_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Helligkeit in Prozent |
| STAT_HELLIGKEIT_LUX_WERT | lx | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Helligkeit in LUX |

<a id="table-res-0xe1db-d"></a>
### RES_0XE1DB_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DISPLAY_BACKLIGHT_PERCENTAGE_1_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level in Prozent |
| STAT_DISPLAY_BACKLIGHT_PERCENTAGE_2_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level in Prozent |
| STAT_TELLTALE_YELLOW_PERCENTAGE_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level TELLTALE_YELLOW_PERCENTAGE in Prozent |
| STAT_TELLTALE_RED_PERCENTAGE_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level TELLTALE_RED_PERCENTAGE in Prozent |
| STAT_TELLTALE_GREEN_PERCENTAGE_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level TELLTALE_GREEN_PERCENTAGE in Prozent |
| STAT_TELLTALE_WHITE_PERCENTAGE_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | PWM Level TELLTALE_WHITE_PERCENTAGE in Prozent |
| STAT_DISPLAY_BACKLIGHT_PWM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert 1 |
| STAT_DISPLAY_BACKLIGHT_PWM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert 2 |
| STAT_TELLTALE_YELLOW_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert TELLTALE_YELLOW_PWM |
| STAT_TELLTALE_RED_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert TELLTALE_RED_PWM |
| STAT_TELLTALE_GREEN_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert TELLTALE_GREEN_PWM |
| STAT_TELLTALE_WHITE_PWM_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller PWM Wert TELLTALE_WHITE_PWM |

<a id="table-res-0xe1dc-d"></a>
### RES_0XE1DC_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HELLIGKEITSSENSOR_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Auslesen des Helligkeitssensors in Prozent |

<a id="table-res-0xe1dd-d"></a>
### RES_0XE1DD_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FELDSTAERKE_ANT1_WERT | dBm | high | unsigned char | - | - | 1.0 | 1.0 | -120.0 | Wert der Feldstärke an Antenne1 |
| STAT_FELDSTAERKE_ANT2_WERT | dBm | high | unsigned char | - | - | 1.0 | 1.0 | -120.0 | Wert der Feldstärke an Antenne2 |

<a id="table-res-0xe1de-d"></a>
### RES_0XE1DE_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZ_EINTRAEGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Telefonbucheinträge |
| STAT_SPEICHER_EINTRAEGE_WERT | MByte | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Größe des benutzten Speicherplatzes für Telefonbucheinträge |
| STAT_SPEICHER_FOTOS_WERT | MByte | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Größe des benutzten Speicherplatzes für Fotos |

<a id="table-res-0xe1df-d"></a>
### RES_0XE1DF_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_GERAETEADRESSE_MR_1_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | Liefert die Adresse des Bluetooth Gerätes 1 |
| STAT_BT_GERAETEADRESSE_MR_2_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | Liefert die Adresse des Bluetooth Gerätes 2 |

<a id="table-res-0xe1e0-d"></a>
### RES_0XE1E0_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_ADRESSE_HELMET_1_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Helm 1 |
| STAT_BT_ADRESSE_HELMET_2_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Helm 2 |
| STAT_BT_ADRESSE_HELMET_3_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Helm 3 |
| STAT_BT_ADRESSE_HELMET_4_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Helm 4 |
| STAT_BT_ADRESSE_HELMET_5_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Helm 5 |
| STAT_BT_ADRESSE_PHONE_1_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Phone 1 |
| STAT_BT_ADRESSE_PHONE_2_DATA | DATA | high | data[6] | - | - | 1.0 | 1.0 | 0.0 | BT Adresse Phone 2 |
| STAT_BT_HELMET_1 | 0/1 | high | unsigned char | - | - | - | - | - | Helm 1 Verbindungsstatus  0=nicht verbunden 1=verbunden |
| STAT_BT_HELMET_2 | 0/1 | high | unsigned char | - | - | - | - | - | Helm 2 Verbindungsstatus 0=nicht verbunden 1=verbunden |
| STAT_BT_HELMET_3 | 0/1 | high | unsigned char | - | - | - | - | - | Helm 3 Verbindungsstatus 0=nicht verbunden 1=verbunden |
| STAT_BT_HELMET_4 | 0/1 | high | unsigned char | - | - | - | - | - | Helm 4 Verbindungsstatus 0=nicht verbunden 1=verbunden |
| STAT_BT_HELMET_5 | 0/1 | high | unsigned char | - | - | - | - | - | Helm 5 Verbindungsstatus 0=nicht verbunden 1=verbunden |
| STAT_BT_PHONE_1 | 0/1 | high | unsigned char | - | - | - | - | - | Telefon 1 Verbindungsstatus 0=nicht verbunden 1=verbunden |
| STAT_BT_PHONE_2 | 0/1 | high | unsigned char | - | - | - | - | - | Telefon 2 Verbindungsstatus 0=nicht verbunden 1=verbunden |

<a id="table-res-0xe1e2-d"></a>
### RES_0XE1E2_D

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OBD_LINK_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD Link |
| STAT_OBD_AUTO_NEGOTIATION_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD Auto-Negotiation |
| STAT_OBD_MDI_X_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD MDI-X |
| STAT_OBD_FAR_END_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD Far-End |
| STAT_OBD_LINK_DUPLEX_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD Link-Duplex |
| STAT_OBD_LINK_GESCHW_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status OBD Link Geschwindigkeit |
| STAT_PHY_LINK_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status PHY Link |
| STAT_PHY_REMOTE_TEXT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status PHY Remote |
| STAT_SMI_REGISTER_ID_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Identifier der SMI Register |
| STAT_SMI_REGISTER_INHALT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Inhalt der SMI Register |
| STAT_MMI_REGISTER_CHANNEL_ID_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Kanal Identifier der MMI Register |
| STAT_MMI_REGISTER_ID_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Identifier der MMI Register |
| STAT_MMI_REGISTER_INHALT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Inhalt der MMI Register |

<a id="table-res-0xe1e3-d"></a>
### RES_0XE1E3_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OBD_AKTIVIERUNGSLEITUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status OBD Aktivierungsleitung: 0 = aus, 1 = ein |
| STAT_OBD_LINK_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status OBD Link: 0 = aus, 1 = ein |
| STAT_OABR1_LINK_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status OABR1 Link: 0 = aus, 1 = ein |
| STAT_OABR2_LINK_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status OABR2 Link: 0 = aus, 1 = ein |

<a id="table-res-0xe1ef-d"></a>
### RES_0XE1EF_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_GERAETENAME_1_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Name BT-Gerät 1 |
| STAT_BT_GERAETENAME_2_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Name BT-Gerät 2 |

<a id="table-res-0xe211-d"></a>
### RES_0XE211_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_BER_01_WERT | - | high | motorola double | - | - | 1.0 | 1.0 | 0.0 | aktuelle Bitfehlerrate 01 |
| STAT_BT_BER_02_WERT | - | high | motorola double | - | - | 1.0 | 1.0 | 0.0 | aktuelle Bitfehlerrate 02 |

<a id="table-res-0xe212-d"></a>
### RES_0XE212_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MEMORYSPACE_FLASH_KBYTE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Flashspeicher in kByte |
| STAT_FREE_MEMORYSPACE_FLASH_KBYTE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | freier Flashspeicher |
| STAT_FREE_MEMORYSPACE_FLASH_PERCENT_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Freier Flashspeicher in % |
| STAT_MEMORYSPACE_RAM_KBYTE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | RAM Speicher in kByte |
| STAT_FREE_MEMORYSPACE_RAM_KBYTE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | freier RAM Speicher in kByte |
| STAT_FREE_MEMORYSPACE_RAM_PERCENT_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | freier RAM Speicher in % |

<a id="table-res-0xe213-d"></a>
### RES_0XE213_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CONNECTIVITY | 0/1 | high | unsigned char | - | - | - | - | - | Rücklesen ob die Connectivity-Features aktiv codiert sind: (1=aktiv / 0=nicht aktiv)  Connectivity allgemein  |
| STAT_MEDIA | 0/1 | high | unsigned char | - | - | - | - | - | Rücklesen ob die Connectivity-Features aktiv codiert sind: (1=aktiv / 0=nicht aktiv)  Media  |
| STAT_PHONE | 0/1 | high | unsigned char | - | - | - | - | - | Rücklesen ob die Connectivity-Features aktiv codiert sind: (1=aktiv / 0=nicht aktiv)  Telefon |
| STAT_NAVIGATION | 0/1 | high | unsigned char | - | - | - | - | - | Rücklesen ob die Connectivity-Features aktiv codiert sind: (1=aktiv / 0=nicht aktiv)  Navigation |

<a id="table-res-0xe214-d"></a>
### RES_0XE214_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_01_CONNECTION | 0-n | high | unsigned char | - | TAB_BT | - | - | - | Status der Bluetooth-Verbindung: Bluetooth 1 (Telefon) |
| STAT_BT_02_CONNECTION | 0-n | high | unsigned char | - | TAB_BT | - | - | - | Status der Bluetooth-Verbindung:  Bluetooth 2 (Helmstack) |

<a id="table-res-0xf152-d"></a>
### RES_0XF152_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HW_MODIFICATION_INDEX_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Index of hardware modification:  FF: Not supported index |
| - | Bit | high | BITFIELD | - | BF_22_F152_SUPPLIERINFO | - | - | - | Tab Supplierinfo |

<a id="table-res-0xf190-d"></a>
### RES_0XF190_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FGNR17_TEXT | TEXT | - | string[17] | - | - | 1.0 | 1.0 | 0.0 | 17-Stellige Fahrgestellnummer |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 61 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EXTERNAL_HSFZ | 0x1023 | - | DOORS-ID: FZHS_5992 | - | - | - | - | - | - | - | - | - | 31 | ARG_0x1023_R | - |
| RESET_AKTIVIERUNGSLEITUNG | 0x1024 | - | Reset_Aktivierungsleitung DOORS-ID: FZHS_3798 | - | - | - | - | - | - | - | - | - | 31 | - | - |
| SYSTEMZEIT | 0x1701 | STAT_SYSTEMZEIT_WERT | Systemzeit | s | - | high | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | high | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SELBSTTEST_DISPLAY | 0xB004 | - | Display Selbsttest | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xB004_R |
| SINUSGENERATOR_MR | 0xB011 | - | Gibt einen Sinuston auf einen oder mehrere Kanäle aus | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB011_R | - |
| VOLUMEAUDIO_HELM | 0xB012 | - | Setzen der Lautstärkewerte für Helm | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB012_R | - |
| KLANGZEICHEN_MR | 0xB053 | - | Steuert eine Tonart im Helm an | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB053_R | - |
| BT_ON_OFF | 0xB054 | - | aktiviert/dekativiert Bluetooth | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB054_R | RES_0xB054_R |
| BT_ERKENNUNGSMODUS_MR | 0xB055 | - | Steuerung Bluetooth Erkennungsmodus | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB055_R | RES_0xB055_R |
| BT_DELETE_ALL_PHONE_ID_MR | 0xB056 | - | Löschen angekoppelter Bluetooth Geräte | - | - | - | - | - | - | - | - | - | 31 | - | - |
| BT_DELETE_PHONEBOOK | 0xB057 | - | Löschen des Telefonbuchs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| BT_TX_TEST_SMARTPHONE | 0xB05E | - | Sets BT chip into the desired test mode. Switch off with resetting GSS-part | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB05E_R | - |
| BT_TX_TEST_HELMET | 0xB05F | - | Sets BT chip into the desired test mode. Switch off with resetting GSS-part. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB05F_R | - |
| SSP_DEBUG_MODE_SMARTPHONE | 0xB060 | - | SSP Debug Modus Smartphone | - | - | - | - | - | - | - | - | - | 31 | - | - |
| SSP_DEBUG_MODE_HELMET | 0xB061 | - | SSP Debug Modus Helm | - | - | - | - | - | - | - | - | - | 31 | - | - |
| READ_BT_LINK_KEY | 0xB062 | - | Read out the link key of a currently connected BT device | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB062_R | RES_0xB062_R |
| PERSISTENZ_MR | 0xB064 | - | Persistenz löschen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DLT_TRACE | 0xB065 | - | Aktiviert / deaktiviert DLT-Ausgabe | - | - | - | - | - | - | - | - | - | 31 | ARG_0xB065_R | - |
| TANKANZEIGE_1_MR | 0xE07A | - | Testen der Tankanzeige mittels Vorgabe Tankinhalt | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE07A_D | RES_0xE07A_D |
| WEGSTRECKENEINHEIT_MR | 0xE117 | STAT_EINHEIT | Im Kombi dargestellte Wegstreckeneinheit: 0 = km, 1 = Meilen | 0/1 | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GWSZ_MR | 0xE119 | - | Gesamtwegstreckenzähler Motorrad | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE119_D | RES_0xE119_D |
| PHOTOSENSOR_MR | 0xE11B | STAT_PHOTOSENS_WERT | Helligkeitswert vom Fotosensor | % | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| LIN_SCHALTERBLOCK_LINKS_MR | 0xE120 | - | Status der Tasten am linken Lenkerschalterblock (dieser ist über LIN am Kombi angeschlossen) nicht gedrückt/ gedrückt | bit | - | - | BITFIELD | RES_0xE120_D | - | - | - | - | 22 | - | - |
| LIN_MMC_BEDIENUNG_MR | 0xE121 | - | Status MMC-Bedienung (MMC ist über LIN am Kombi angeschlossen) links- / rechts gedrückt;  Position der AUF-/AB-Bewegung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE121_D |
| DREHZAHLANZEIGE_MR | 0xE125 | - | Ansteuern und Auslesen Drehzahl für Drehzahlmesser-Zeiger in U/min | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE125_D | RES_0xE125_D |
| GESCHWINDIGKEIT_ANZEIGE_MR | 0xE126 | - | Ansteuern und Auslesen Geschwindigkeit für Tacho-Zeiger in km/h | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE126_D | RES_0xE126_D |
| GANG_ANZEIGE_MR | 0xE127 | - | Vorgeben und Auslesen des im Kombi angezeigten Ganges | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE127_D | RES_0xE127_D |
| MOTORTEMP_ANZEIGE_MR | 0xE129 | - | Steuern der Motortemperaturanzeige über Vorgabe einer Temperatur und Status aktuelle Motortemperatur | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE129_D | RES_0xE129_D |
| UHRZEIT_DATUM_MR | 0xE12B | - | Uhrzeit und Datum im Kombi | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE12B_D | RES_0xE12B_D |
| SERVICE_DATUM_MR | 0xE12C | - | Auslesen und Schreiben der bis zum nächsten fälligen Service verbleibende Zeit | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE12C_D | RES_0xE12C_D |
| SERVICE_RESTWEG_MR | 0xE12D | - | Auslesen und Schreiben der bis zum nächsten fälligen Service verbleibende Weg | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE12D_D | RES_0xE12D_D |
| BATTERIESPANNUNG_MR | 0xE142 | STAT_BATTERIESPANNUNG_WERT | Batteriespannung | V | - | - | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AUSGANG_KONTROLLLEUCHTEN_MR | 0xE1BD | - | Ansteuerung Kombi Kontrollleuchten | - | - | - | - | - | - | - | - | - | 2F | ARG_0xE1BD_D | - |
| TESTBILD_ANZEIGE_MR | 0xE1D6 | - | Anzeige von Testbildern im Kombi | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE1D6_D | RES_0xE1D6_D |
| SG_TEMPERATUR | 0xE1D7 | - | Interne Temperatur des Steuergerätes | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1D7_D |
| PROZESSOR_LAST | 0xE1D8 | - | Es wird die Prozessor Auslastung in Prozent angegeben | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1D8_D |
| TANKANZEIGE_MR_KOMBHI | 0xE1D9 | - | Tankanzeige | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1D9_D |
| HELLIGKEITSSENSOR_ADC | 0xE1DA | - | Wert des Helligkeitssensors | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1DA_D |
| BACKLIGHT_PWM_WERTE | 0xE1DB | - | Hintergrundbeleuchtung PWM Werte | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE1DB_D | RES_0xE1DB_D |
| HELLIGKEITSSENSOR_PERCENT | 0xE1DC | - | Steuern des Helligkeitssensors in Prozent | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xE1DC_D | RES_0xE1DC_D |
| ANT | 0xE1DD | - | gibt die Feldstärke aus, welche aktuell an der Antenne  empfangen wird | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1DD_D |
| PHONEBOOK | 0xE1DE | - | Auslesen der Anzahl der gespeicherten Telefonbucheinträge und des benötigten Speichers Telefonbucheinträge und Kontaktfotos | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1DE_D |
| BT_GERAETEADRESSE_MR | 0xE1DF | - | Liefert die eigenen Adressen der Bluetooth Geräte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1DF_D |
| BT_GEKOPPELTE_GERAETE_LESEN_MR | 0xE1E0 | - | Liest die Geräte-Adressen der gekoppelten Bluetooth Geräte und zeigt an welche Geräte verbunden sind | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1E0_D |
| VOLUMEAUDIO_MR | 0xE1E1 | STAT_VOLUMEAUDIO_WERT | Liest die ausgewählte Lautstärke aus | % | - | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| ETHERNET_REGISTER_LESEN | 0xE1E2 | - | Ethernet Register wird ausgelesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1E2_D |
| ETHERNET_INFORMATION | 0xE1E3 | - | Ethernet Aktivierungs- und Link-Informationen auslesen für HSFZ und OABR | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE1E3_D |
| IP_CONFIGURATION_SCHREIBEN | 0xE1E4 | - | Setzen der IP Konfiguration | - | - | - | - | - | - | - | - | - | 2E | ARG_0xE1E4_D | - |
| BT_GERAETENAME_MR | 0xE1EF | - | Schreibt/Liest den Bluetooth Gerätenamen | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE1EF_D | RES_0xE1EF_D |
| BT_BER | 0xE211 | - | Die aktuelle Bitfehlerrate BER (BT1/BT2) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE211_D |
| MEMORY_USAGE_MR | 0xE212 | - | Gibt die Auslastung und Größe des benutzten RAM und Flash-Speichers zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE212_D |
| STATUS_APPLICATION | 0xE213 | - | Rücklesen ob die Connectivity-Features aktiv codiert sind: (1=aktiv / 0=nicht aktiv) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE213_D |
| BT_CONNECTION | 0xE214 | - | Status der Bluetooth-Verbindungen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE214_D |
| READHWMODIFICATIONINDEX | 0xF152 | - | Dieser Service kommt nur zum Einsatz, wenn es eine geringfügige Hardwareänderung an dem Steuergerät gegeben hat, die nicht zu einer Änderung der Sachnummer bzw. der Hardware SGBM-IDs geführt hat. Eine solche Änderung ist von außen nicht diagnostizierbar, daher wurde dieser Dienst dafür eingeführt. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF152_D |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | high | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| VIN | 0xF190 | - | Fahrgestellnummer | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xF190_D | RES_0xF190_D |
| CHECK_CONTROL_TRIGGER | 0x4000 | - | Trigger Check Control | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4000_D | - |

<a id="table-svk-version-dop"></a>
### SVK_VERSION_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | SVKVersion_01 |

<a id="table-tab-bluetooth-stat"></a>
### TAB_BLUETOOTH_STAT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bluetooth nicht aktiv |
| 0x01 | Bluetooth aktiv |
| 0xFF | nicht definiert |

<a id="table-tab-bt"></a>
### TAB_BT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | searching |
| 0x01 | visible |
| 0x02 | connected |
| 0x03 | error |
| 0xFF | Wert ungültig |

<a id="table-tab-bt-erkennungsmodus-mr"></a>
### TAB_BT_ERKENNUNGSMODUS_MR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | BT Erkennungsmodus aus |
| 0x01 | BT Erkennungsmodus ein |
| 0xFF | nicht definiert |

<a id="table-tab-dlt"></a>
### TAB_DLT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | deactivate DLT |
| 0x01 | activate DLT |
| 0xFF | not defined |

<a id="table-tab-gang"></a>
### TAB_GANG

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | N |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | 5 |
| 0x06 | 6 |
| 0xFF | ungültiger Gang |

<a id="table-tab-gang-arg"></a>
### TAB_GANG_ARG

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | N |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | 5 |
| 0x06 | 6 |

<a id="table-tab-klangzeichen-mr"></a>
### TAB_KLANGZEICHEN_MR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Chime_1 |
| 0x02 | Chime_2 |
| 0x03 | Chime_3 |

<a id="table-tab-mmc-bed"></a>
### TAB_MMC_BED

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Bedienung |
| 0x01 | Betätigung nach links |
| 0x02 | Betätigung nach rechts |
| 0xFF | nicht definiert |

<a id="table-tab-mr-kontrollleuchte"></a>
### TAB_MR_KONTROLLLEUCHTE

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Blinker links |
| 0x02 | Blinker rechts |
| 0x03 | ABS |
| 0x04 | Warnleuchte rot |
| 0x05 | Fernlicht |
| 0x07 | Reservelampe |
| 0x08 | MIL |
| 0x0A | Warnleuchte gelb |
| 0x0B | Neutral Gang |
| 0x0F | Schaltblitz |
| 0x10 | Batteriewarnung |
| 0x11 | DWA-Leuchte |
| 0x12 | Tagfahrlicht |
| 0x13 | ASC, DTC |
| 0x14 | Zusatzscheinwerfer |
| 0xFE | Alle Kontrollleuchten |

<a id="table-tab-mr-routine"></a>
### TAB_MR_ROUTINE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Routine läuft |
| 0x01 | Routine abgebrochen |
| 0x02 | Routine beendet |
| 0xFF | unbekannt |

<a id="table-tab-senke"></a>
### TAB_SENKE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 01 | Helmet_01 |
| 02 | Helmet_02 |

<a id="table-tab-testbilder"></a>
### TAB_TESTBILDER

Dimensions: 19 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Normale HMI |
| 0x01 | Color Bar |
| 0x01 | Voll Screen ROT |
| 0x02 | Voll Screen GRUEN |
| 0x03 | Voll Screen BLAU |
| 0x04 | Voll Screen WEISS |
| 0x05 | Voll Sceen SCHWARZ |
| 0x06 | BLACK MURA Einrichtungsbild |
| 0x07 | Schachbrett |
| 0x08 | Flicker Horizontal |
| 0x09 | Flicker Vertikal |
| 0x0A | Smooth Graustufen Horizontal |
| 0x0B | Smooth Graustufen Vertikal |
| 0x0C | Smooth Gradient ROT Horizontal |
| 0x0D | Smooth Gradient ROT Vertikal |
| 0x0E | Smooth Gradient GRUEN Horizontal |
| 0x0F | Smooth Gradient GRUEN Vertikal |
| 0x10 | Smooth Gardient BLAU Horizontal |
| 0x11 | Smooth Gradient BLAU Vertikal |
