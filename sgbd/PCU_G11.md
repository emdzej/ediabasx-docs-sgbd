# PCU_G11.prg

- Jobs: [34](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Power Control Unit |
| ORIGIN | BMW EE-411 Lea_Schreiber |
| REVISION | 2.001 |
| AUTHOR | BMW EE-411 Schreiber |
| COMMENT | - |
| PACKAGE | 1.98 |
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
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events $02 eventWindowTime - infinite (LH Diagnosemaster V11 oder höher, Umsetzung nach LH V6 - V10 wird jedoch toleriert)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
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
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XA14F_R](#table-arg-0xa14f-r) (3 × 14)
- [ARG_0XAE01_R](#table-arg-0xae01-r) (4 × 14)
- [ARG_0XDA56_D](#table-arg-0xda56-d) (1 × 12)
- [ARG_0XDA5B_D](#table-arg-0xda5b-d) (1 × 12)
- [ARG_0XDAFB_D](#table-arg-0xdafb-d) (1 × 12)
- [ARG_0XFD00_D](#table-arg-0xfd00-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (75 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (58 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0XA14F_R](#table-res-0xa14f-r) (2 × 13)
- [RES_0XAE01_R](#table-res-0xae01-r) (1 × 13)
- [RES_0XDA56_D](#table-res-0xda56-d) (38 × 10)
- [RES_0XDA57_D](#table-res-0xda57-d) (15 × 10)
- [RES_0XDA5B_D](#table-res-0xda5b-d) (2 × 10)
- [RES_0XDB0C_D](#table-res-0xdb0c-d) (11 × 10)
- [RES_0XDB0D_D](#table-res-0xdb0d-d) (2 × 10)
- [RES_0XDB28_D](#table-res-0xdb28-d) (29 × 10)
- [RES_0XFD00_D](#table-res-0xfd00-d) (8 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (11 × 16)
- [STATUS_LTO_RELAIS](#table-status-lto-relais) (9 × 2)
- [TAB_DCDC_ANSTEUERUNG](#table-tab-dcdc-ansteuerung) (3 × 2)
- [TAB_DCDC_WANDLUNGSRICHTUNG](#table-tab-dcdc-wandlungsrichtung) (18 × 2)

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

<a id="table-arg-0xa14f-r"></a>
### ARG_0XA14F_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LTO_RELAIS_DIAGNOSE | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: LTO Relais öffnen 0x01: LTO Relais schliessen |
| LTO_RELAIS_ART | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: persistent 0x01: temporaer |
| LTO_RELAIS_STOP | - | + | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: Keine Aktion 0x01: LTO Diagnosemodus beenden |

<a id="table-arg-0xae01-r"></a>
### ARG_0XAE01_R

Dimensions: 4 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSMODUS | + | - | 0-n | high | unsigned char | - | TAB_DCDC_ANSTEUERUNG | - | - | - | - | - | Betriebszustand (Wandlungsrichtung) |
| VORGABE_SPANNUNG | + | - | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 25000.0 | Vorgabe Spannung |
| VORGABE_EINGANGSSTROM | + | - | mA | high | unsigned char | - | - | 1.0 | 250.0 | 0.0 | 0.0 | 45000.0 | Vorgabe Eingangsstrom |
| VORGABE_AUSGANGSSTROM | + | - | mA | high | unsigned char | - | - | 1.0 | 250.0 | 0.0 | 0.0 | 45000.0 | Vorgabe Ausgangsstrom |

<a id="table-arg-0xda56-d"></a>
### ARG_0XDA56_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0 = Histogramm löschen; 1 = Keine Aktion |

<a id="table-arg-0xda5b-d"></a>
### ARG_0XDA5B_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0 = Zähler löschen; 1 = Keine Aktion |

<a id="table-arg-0xdafb-d"></a>
### ARG_0XDAFB_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LTO_BATTERIETAUSCH | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: Keine Aktion 0x01: Job Batterietausch ausführen |

<a id="table-arg-0xfd00-d"></a>
### ARG_0XFD00_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HELLA_SESSION_ENTRY | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Steuern der PCU in der Fertigung. |

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
| F_HLZ_VIEW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 75 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x022E00 | Energiesparmode aktiv | 0 | - |
| 0x022E08 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x022E09 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x022E0A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x022E0B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x022E0C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02FF2E | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x803D05 | PCU: Netz N1, Überspannung | 1 | - |
| 0x803D06 | PCU: Weckleitung, Leitungsunterbrechung oder Kurzschluss nach Masse | 0 | - |
| 0x803D07 | Überspannung N2 (Elko Out of Spec) | 0 | - |
| 0x803D09 | PCU: Weckleitung, Kurzschluss nach Plus | 0 | - |
| 0x803D0A | PCU: Netz N1, Unterspannung | 1 | - |
| 0x803D0B | PCU: Anschluss Netz N1, Kurzschluss nach Masse | 0 | - |
| 0x803D0E | PCU: Anschluss Netz N2, Kurzschluss nach Plus | 0 | - |
| 0x803D0F | Zusatzbatterie (ES2): Kapazität nicht ausreichend | 0 | - |
| 0x803D10 | Zusatzbatterie (ES2): Zellschluss erkannt | 0 | - |
| 0x803D11 | PCU: Netz N2, Überstrom | 0 | - |
| 0x803D12 | Zusatzbatterie (ES2): Zusatzbatterie an PCU nicht angeschlossen | 0 | - |
| 0x803D14 | PCU: Netz N2, Überspannung | 0 | - |
| 0x803D15 | PCU: Anschluss Netz N1, Leitungsunterbrechung | 0 | - |
| 0x803D17 | PCU: Netz N1, Überstrom | 1 | - |
| 0x803D19 | PCU: Übertemperatur | 1 | - |
| 0x803D1A | Zusatzbatterie (ES2): Zusatzbatterie tiefentladen | 0 | - |
| 0x803D1B | PCU: Netz N2, Unterspannung | 0 | - |
| 0x803D1C | Unterspannung erkannt | 1 | - |
| 0x803D1D | Überspannung erkannt | 1 | - |
| 0x803D1E | PCU: Fehler in der Hardware | 1 | - |
| 0x803D1F | Interne Spannung nicht stabil | 0 | - |
| 0x803D20 | Stromfluss in das Gerät auf N1 Seite für Stromrichtung N2 nach N1 | 1 | - |
| 0x803D21 | Stromfluss in das Gerät auf N2 Seite für Stromrichtung N1 nach N2 | 0 | - |
| 0x803D22 | Zusatzbatterie: Anschluss Netz N2, Kurzschluss nach Masse | 0 | - |
| 0x803D49 | PCU: ROM-Fehler (Prüfsumme) | 0 | - |
| 0x803D4A | PCU: ROM-Fehler (ausgelöst durch EccH) | 0 | - |
| 0x803D4B | PCU: Fehler bei RAM-Test | 0 | - |
| 0x803D4C | PCU: Fehler bei der Prüfung des Stacks | 0 | - |
| 0x803D4D | Unterspannung N1 erkannt (Langzeit) | 1 | - |
| 0x803D4E | Unterspannung N2 erkannt (Langzeit) | 0 | - |
| 0x803D4F | Unterspannung Kl. 30F erkannt (Langzeit) | 1 | - |
| 0x803D50 | Signal zur Crash-Abschaltung empfangen | 1 | - |
| 0x803D51 | Batteriezustandserkennung LTO: Entgasung der Batterie | 0 | - |
| 0x803D52 | Batteriezustandserkennung LTO: Fehler RAM | 0 | - |
| 0x803D53 | Batteriezustandserkennung LTO: Checksummenfehler Programmcode | 0 | - |
| 0x803D54 | Batteriezustandserkennung LTO: Nicht Reversibler Fehler | 1 | - |
| 0x803D55 | Batteriezustandserkennung LTO: Reversibler Fehler | 1 | - |
| 0x803D56 | Batteriezustandserkennung LTO: Tiefenentladung | 0 | - |
| 0x803D57 | Batteriezustandserkennung LTO: Batterieloser Betrieb | 0 | - |
| 0x803D58 | Batteriezustandserkennung LTO: Crash | 0 | - |
| 0x803D59 | Batteriezustandserkennung LTO: UDS-Übertragungsfehler Seriennummer | 0 | - |
| 0x803D5A | Batteriezustandserkennung LTO: Zelldefekt der Batterie | 0 | - |
| 0x803D5B | Batteriezustandserkennung LTO: Checksummenfehler Parameterdaten | 0 | - |
| 0x803D5C | Batteriezustandserkennung LTO: Checksummenfehler Kalibrierdaten | 0 | - |
| 0x803D5D | Batteriezustandserkennung LTO: Sensorfehler elektrisch Spannung | 0 | - |
| 0x803D5E | Batteriezustandserkennung LTO: Seriennummer ungleich | 0 | - |
| 0x803D66 | Batteriezustandserkennung LTO: Sensorfehler Plausibel check Spannung | 0 | - |
| 0x803D67 | Batteriezustandserkennung LTO: Sensorfehler elektrisch Strom | 0 | - |
| 0x803D68 | Batteriezustandserkennung LTO: Sensorfehler Plausibel check Strom | 0 | - |
| 0x803D69 | Batteriezustandserkennung LTO: Sensorfehler elektrisch Temperatur | 0 | - |
| 0x803D6A | Batteriezustandserkennung LTO: Sensorfehler Plausibel check Temperatur | 0 | - |
| 0x803D6B | Batteriezustandserkennung LTO: Relais elektrischer Fehler | 0 | - |
| 0x803D6C | Batteriezustandserkennung LTO: Relais klemmt offen | 0 | - |
| 0x803D6D | Batteriezustandserkennung LTO: Relais klemmt geschlossen | 0 | - |
| 0xD48472 | LP-CAN Control Module Bus OFF | 0 | - |
| 0xD48BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xD49400 | ID 1BAh Zeitüberschreitung von ST_ENERG_GEN Frame | 1 | - |
| 0xD49402 | ID 3BEh CAN_MSG_TIMEOUT_FLLUPT_GPWSUP | 1 | - |
| 0xD49403 | ID 3B3h Zeitüberschreitung von POWERMGMT_CTR_COS Frame | 1 | - |
| 0xD49405 | ID 0ABh Zeitüberschreitung von Signal ST_CR | 1 | - |
| 0xD49407 | ID 03Ch CAN_MSG_TIMEOUT_CON_VEH | 1 | - |
| 0xD49408 | ID 032h CAN_MSG_TIMEOUT_ST_CENG | 1 | - |
| 0xD49409 | ID 2D9h CAN_MSG_TIMEOUT_CTR_I_U_ENBN | 1 | - |
| 0xD4940A | ID 330h CAN_MSG_TIMEOUT_KILOMETERSTAND | 1 | - |
| 0xD4940B | ID 1A1h CAN_MSG_TIMEOUT_V_VEH | 1 | - |
| 0xD4940E | ID 0B7h CAN_MSG_TIMEOUT_ECU_DOM_CENG | 1 | - |
| 0xD4940F | ID 2F0h CAN_MSG_TIMEOUT_STAT_KLIMA_STAND | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1602 | SPANNUNG_BMS_UN2 | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
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

Dimensions: 58 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x803D08 | OVERVOLTAGE_ELKO_OOS_INFO | 0 | - |
| 0x803D23 | CAN_E_TIMEOUT | 0 | - |
| 0x803D24 | CANIF_E_FULL_TX_BUFFER | 0 | - |
| 0x803D25 | CANIF_E_STOPPED | 0 | - |
| 0x803D26 | CANIF_E_INVALID_DLC | 0 | - |
| 0x803D27 | CANNM_E_NETWORK_TIMEOUT | 0 | - |
| 0x803D28 | CANNM_E_TX_PATH_FAILED | 0 | - |
| 0x803D29 | CANSM_E_MODE_CHANGE_NETWORK_0 | 0 | - |
| 0x803D2A | CANSM_E_SETTRSCVMODE_NETWORK_0 | 0 | - |
| 0x803D2B | CSM_E_ERROR_EVENT | 0 | - |
| 0x803D2D | DM_QUEUE_DELETED | 0 | - |
| 0x803D2E | DM_QUEUE_FULL | 0 | - |
| 0x803D2F | ECUM_E_ALL_RUN_REQUESTS_KILLED | 0 | - |
| 0x803D30 | ECUM_E_RAM_CHECK_FAILED | 0 | - |
| 0x803D31 | FEE_E_WRITE_FAILED | 0 | - |
| 0x803D32 | FLS_E_COMPARE_FAILED | 0 | - |
| 0x803D33 | FLS_E_ERASE_FAILED | 0 | - |
| 0x803D34 | FLS_E_READ_FAILED | 0 | - |
| 0x803D35 | FLS_E_WRITE_FAILED | 0 | - |
| 0x803D36 | IPDUM_E_TRANSMIT_FAILED | 0 | - |
| 0x803D37 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x803D38 | NVM_E_INTEGRITY_FAILED | 0 | - |
| 0x803D39 | NVM_E_REQ_FAILED | 0 | - |
| 0x803D3A | PDUR_E_INIT_FAILED | 0 | - |
| 0x803D3B | PDUR_E_PDU_INSTANCE_LOST | 0 | - |
| 0x803D3C | VSM_EVENT_VEHICLESTATE | 0 | - |
| 0x803D3D | ADC_E_TIMEOUT | 0 | - |
| 0x803D3E | SPI_E_TIMEOUT | 0 | - |
| 0x803D3F | MCU_E_TIMEOUT_TRANSITION | 0 | - |
| 0x803D40 | MCU_E_QUARTZ_FAILURE | 0 | - |
| 0x803D41 | MCU_E_LOCK_FAILURE | 0 | - |
| 0x803D42 | PWM_E_UNEXPECTED_IRQ | 0 | - |
| 0x803D43 | FUNCTION_FREMDLADUNG_ACTIVE | 0 | - |
| 0x803D44 | PCU_BLOCK_GENERATOR_CHARGING | 0 | - |
| 0x803D45 | UNDERVOLTAGE_N1_INFO | 0 | - |
| 0x803D46 | UNDERVOLTAGE_N2_INFO | 0 | - |
| 0x803D47 | UNDERVOLTAGE_INFO | 0 | - |
| 0x803D48 | VCC2_VCP_RANGE_INFO | 0 | - |
| 0x803D60 | LINSM_E_CONFIRMATION_TIMEOUT | 0 | - |
| 0x803D61 | LINSM_E_WRONG_TRCV_MODE | 0 | - |
| 0x803D62 | LINIF_E_NC_NO_RESPONSE | 0 | - |
| 0x803D63 | LINIF_E_RESPONSE | 0 | - |
| 0x803D64 | LINIF_E_CHANNEL_0_SLAVE_DSS | 0 | - |
| 0x803D65 | LIN_E_TIMEOUT | 0 | - |
| 0x803D70 | Batteriezustandserkennung LTO: Emergency Shutdown Spannung zu hoch | 0 | - |
| 0x803D71 | Batteriezustandserkennung LTO: Grenzwertverletzung Spannung zu hoch | 0 | - |
| 0x803D72 | Batteriezustandserkennung LTO: Emergency Shutdown Spannung zu tief | 0 | - |
| 0x803D73 | Batteriezustandserkennung LTO: Grenzwertverletzung Spannung zu tief | 0 | - |
| 0x803D74 | Batteriezustandserkennung LTO: Emergency Shutdown Temperatur zu hoch | 0 | - |
| 0x803D75 | Batteriezustandserkennung LTO: Grenzwertverletzung Temperatur zu hoch | 0 | - |
| 0x803D76 | Batteriezustandserkennung LTO: Grenzwertverletzung Temperatur zu niedrig | 0 | - |
| 0x803D77 | Batteriezustandserkennung LTO: Emergency Shutdown Entladestrom zu hoch | 0 | - |
| 0x803D78 | Batteriezustandserkennung LTO: Grenzwertverletzung Ladestrom zu hoch | 0 | - |
| 0x803D79 | Batteriezustandserkennung LTO: Emergency Shutdown Ladestrom zu hoch | 0 | - |
| 0x803D7A | Batteriezustandserkennung LTO: Diagnosejob Relais aktiv | 0 | - |
| 0xD48C00 | Batteriezustandserkennung LTO: BMS Kommunikationsausfall | 0 | - |
| 0xD49410 | ID 328h DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0xa14f-r"></a>
### RES_0XA14F_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LTO_RELAIS_DIAGNOSE_STATUS | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0x00: Relais zu 0x01: Relais offen |
| STAT_LTO_RELAIS_ART | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0x00: peresistent 0x01: temporaer |

<a id="table-res-0xae01-r"></a>
### RES_0XAE01_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BETRIEBSMODUS | - | - | + | 0-n | high | unsigned char | - | TAB_DCDC_WANDLUNGSRICHTUNG | - | - | - | Betriebszustand (Wandlungsrichtung) |

<a id="table-res-0xda56-d"></a>
### RES_0XDA56_D

Dimensions: 38 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FREMDLADEN_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 10 bis 11 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 11 bis 12 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12 bis 13 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 13 bis 14 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 14 bis 15 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 15 bis 16 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 16 bis 17 V und im Betriebsmodus Fremdladen |
| STAT_FREMDLADEN_U8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 17 bis 18 V und im Betriebsmodus Fremdladen |
| STAT_N1NACHN2_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 10 bis 11 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 11 bis 12 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12 bis 13 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 13 bis 14 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 14 bis 15 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 15 bis 16 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 16 bis 17 V und im Betriebsmodus N1 nach N2 |
| STAT_N1NACHN2_U8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 17 bis 18 V und im Betriebsmodus N1 nach N2 |
| STAT_N2NACHN1_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 10 bis 11 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 11 bis 12 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12 bis 13 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 13 bis 14 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 14 bis 15 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 15 bis 16 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 16 bis 17 V und im Betriebsmodus N2 nach N1 |
| STAT_N2NACHN1_U8_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 17 bis 18 V und im Betriebsmodus N2 nach N1 |
| STAT_STANDBY_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 11,6 bis 11,8 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 11,8 bis 12 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12 bis 12,2 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12,2 bis 12,4 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12,4 bis 12,6 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12,6 bis 12,8 V und im Betriebsmodus Stand-By |
| STAT_STANDBY_U7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Häufigkeit (Sekunde) in Spannungsbereich 12,8 bis 13 V und im Betriebsmodus Stand-By |
| STAT_WAKEUP_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 11,6V bis 11,8V im Status Wakeup |
| STAT_WAKEUP_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 11,8V bis 12,0V im Status Wakeup |
| STAT_WAKEUP_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 12,0V bis 12,2V im Status Wakeup |
| STAT_WAKEUP_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 12,2V bis 12,4V im Status Wakeup |
| STAT_WAKEUP_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 12,4V bis 12,6V im Status Wakeup |
| STAT_WAKEUP_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 12,6V bis 12,8V im Status Wakeup |
| STAT_WAKEUP_U7_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl im Spannungsbereich 12,8V bis 13,0V im Status Wakeup |

<a id="table-res-0xda57-d"></a>
### RES_0XDA57_D

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_N1_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung im Netz 1 |
| STAT_SPANNUNG_N2_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung im Netz 2 |
| STAT_STROM_N1_WERT | A | high | unsigned int | - | - | 1.0 | 100.0 | -55.555 | Strom im Netz 1 |
| STAT_STROM_N2_WERT | A | high | unsigned int | - | - | 1.0 | 100.0 | -55.555 | Strom im Netz 2 |
| STAT_KLEMME15_WUP_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Status der Klemme 15 (Weckleitung) |
| STAT_KLEMME30B | 0/1 | high | unsigned char | - | - | - | - | - | Status der Klemme 30B (Signal über CAN-Bus): 0 = Klemme 30B aus / 1 = Klemme 30B ein |
| STAT_TEMPERATUR1_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR2_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR3_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR4_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR5_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR6_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des DC-DC-Wandlers |
| STAT_TEMPERATUR_MIKROPROZESSOR_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | -100.0 | Temperatur des µC des DC-DC-Wandlers |
| STAT_KLEMME30F_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Versorgungsspannung |
| STAT_SPANNUNG_N2_KOMPENSIERT_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Kompensierte Spannung an UN2 |

<a id="table-res-0xda5b-d"></a>
### RES_0XDA5B_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LADEZAEHLER_WERT | Ah | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ladezähler |
| STAT_ENTLADEZAEHLER_WERT | Ah | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Entladezähler |

<a id="table-res-0xdb0c-d"></a>
### RES_0XDB0C_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LTO_SOC_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | LTO Speicher: Momentaner SOC Wert des Speichers |
| STAT_LTO_SPANNUNG_WERT | V | high | unsigned int | - | - | 1.0 | 200.0 | 0.0 | LTO Speicher: Momentane Spannung zwischen den power Terminals  |
| STAT_LTO_RELAIS | 0-n | high | unsigned char | - | STATUS_LTO_RELAIS | - | - | - | Status Relais |
| STAT_LTO_STROM_WERT | A | high | unsigned int | - | - | 1.0 | 20.0 | -1638.35 | Aktueller Strom der LTO Batterie |
| STAT_LTO_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -127.0 | Aktuelle Temperatur LTO Speicher |
| STAT_LTO_MAX_SPANNUNG_WERT | V | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Maximale Zulässige Spannung an LTO Speicher |
| STAT_LTO_CRASH | 0/1 | high | unsigned char | - | - | - | - | - | 0x00: Kein Crash 0x01: Crash aktiv |
| STAT_LTO_SCHALTVORGAENGE_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schaltvorgänge des LTO Speichers |
| STAT_ANZAHL_BATTERIETAUSCH_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der registrierten LTO Batterietausch |
| STAT_LTO_SOH_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | LTO Speicher SOH Wert |
| STAT_LTO_SOH_ABS_FEHLER_WERT | % | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Absoltuer Fehler SOH |

<a id="table-res-0xdb0d-d"></a>
### RES_0XDB0D_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LTO_BMS_PARTNUMMER_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | LTO Speicher BMS Part Nummer |
| STAT_LTO_BMS_PARTNUMMER_NV_RAM_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | LTO Speicher BMS Part Nummer gespeichert in NV RAM |

<a id="table-res-0xdb28-d"></a>
### RES_0XDB28_D

Dimensions: 29 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LTO_SOC_0_10_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 0 bis 10 Prozent |
| STAT_LTO_SOC_10_20_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 10 bis 20 Prozent |
| STAT_LTO_SOC_20_30_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 20 bis 30 Prozent |
| STAT_LTO_SOC_30_40_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 30 bis 40 Prozent |
| STAT_LTO_SOC_40_50_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 40 bis 50 Prozent |
| STAT_LTO_SOC_50_60_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 50 bis 60 Prozent |
| STAT_LTO_SOC_60_70_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 60 bis 70 Prozent |
| STAT_LTO_SOC_70_80_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 70 bis 80 Prozent |
| STAT_LTO_SOC_80_90_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 80 bis 90 Prozent |
| STAT_LTO_SOC_90_100_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO SOC Speicher gespeichert jede Minute: 90 bis 100 Prozent |
| STAT_LTO_TEMPERATUR_UNTER_NEG40_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: &lt;-40 Grad Celsius |
| STAT_LTO_TEMPERATUR_NEG40_NEG20_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: -40 bis -20 Grad Celsius |
| STAT_LTO_TEMPERATUR_NEG20_0_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: -20 bis 0 Grad Celsius |
| STAT_LTO_TEMPERATUR_0_40_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: 0 bis 40 Grad Celsius |
| STAT_LTO_TEMPERATUR_40_60_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: 40 bis 60 Grad Celsius |
| STAT_LTO_TEMPERATUR_60_80_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: 60 bis 80 Grad Celsius |
| STAT_LTO_TEMPERATUR_AB_80_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Temperatur: &gt;80 Grad Celsius |
| STAT_LTO_STROM_UNTER_NEG200A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: &lt; -200A |
| STAT_LTO_STROM_NEG200_NEG100A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: -200A bis -100A |
| STAT_LTO_STROM_NEG100_NEG75A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: -100A bis -75A |
| STAT_LTO_STROM_NEG75_NEG50A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: -75A bis -50A |
| STAT_LTO_STROM_NEG50_NEG25A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: -50A bis -25A |
| STAT_LTO_STROM_NEG25_0A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: -25A bis 0A |
| STAT_LTO_STROM_0A_25A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: 0A bis 25A |
| STAT_LTO_STROM_25A_50A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: 25A bis 50A |
| STAT_LTO_STROM_50A_75A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: 50A bis 75A |
| STAT_LTO_STROM_75A_100A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: 75A bis 100A |
| STAT_LTO_STROM_100A_200A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: 100A bis 200A |
| STAT_LTO_STROM_AB_200A_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Histogramm LTO Speicher Strom: &gt;200A |

<a id="table-res-0xfd00-d"></a>
### RES_0XFD00_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_U_OUT_REQUEST_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Voltage output request value. |
| STAT_I_OUT_REQUEST_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Current output request value. |
| STAT_I_IN_REQUEST_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Input current request value. |
| STAT_I_ZERO_REQUEST_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Zero current request value. |
| STAT_U_OUT_READBACK_WERT | V | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Voltage output readback value. |
| STAT_I_OUT_READBACK_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Current output readback value. |
| STAT_I_IN_READBACK_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Input current readback value. |
| STAT_I_ZERO_READBACK_WERT | A | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Zero current readback value. |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 11 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PCU_LTO_RELAIS | 0xA14F | - | Diagnosemodus für LTO Speicher Relais Ansteuerung | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA14F_R | RES_0xA14F_R |
| PCU_DCDC_WANDLER | 0xAE01 | - | Wechsel oder Auslesen des Betriebszustandes vom DC/DC-Wandler | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAE01_R | RES_0xAE01_R |
| PCU_DCDC_SPANNUNGSHISTOGRAMM | 0xDA56 | - | Spannungshistrogramm für PCU500 in den jeweiligen Betriebzuständen (Stand-by, Fremdladen, Wandlung N1 nach N2, Wandlung N2 nach N1) auslesen / Rücksetzen (0 = Histogramm löschen; 1 = Keine Aktion) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDA56_D | RES_0xDA56_D |
| DC_DC_DATA_LESEN | 0xDA57 | - | Daten des DC-DC Wandlers lesen - Eingangs-/Ausgangsspannung - Eingangs-/Ausgangsstrom - Temperatur des DC-DC-Wandlers | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDA57_D |
| ZUSATZBATTERIE_ES2_ZAEHLER | 0xDA5B | - | Lade/Entladezähler für Zusatzbatterie  (ES2) auslesen/löschen (0 = Zähler löschen; 1 = Keine Aktion) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDA5B_D | RES_0xDA5B_D |
| PCU_LTO_BATTERIETAUSCH | 0xDAFB | - | Diagnosejob Batterietausch PCU LTO 12V | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDAFB_D | - |
| PCU_LTO_STATUS | 0xDB0C | - | Status LTO Speicher SOC, Temperatur, Trennelement.. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB0C_D |
| LTO_HERSTELLINFO | 0xDB0D | - | Herstellinfos werden abgerufen.  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB0D_D |
| PCU_LTO_HISTOGRAMM | 0xDB28 | - | PCU LTO Histogramme lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB28_D |
| PCU_VARIANTE | 0xE2D8 | STAT_PCU500_VARIANTE | 0x00: BUM Variante 0x01: LTO Variante | 0/1 | - | High | unsigned char | - | - | - | - | - | 22 | - | - |
| HELLA_PCU_READ_SET | 0xFD00 | - | Hella session controls. Additional PCU values. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xFD00_D | RES_0xFD00_D |

<a id="table-status-lto-relais"></a>
### STATUS_LTO_RELAIS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | closed |
| 1 | open_automatic_connectable |
| 2 | open_coupleable |
| 3 | open_forced_connectable |
| 4 | open_prevent_connect |
| 5 | open_diagnosis |
| 6 | closed_diagnosis |
| 7 | open_crash |
| 255 | Signal_unbefuellt |

<a id="table-tab-dcdc-ansteuerung"></a>
### TAB_DCDC_ANSTEUERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Standby |
| 0x01 | Wandlung N1 zu N2 |
| 0x02 | Wandlung N2 zu N1 |

<a id="table-tab-dcdc-wandlungsrichtung"></a>
### TAB_DCDC_WANDLUNGSRICHTUNG

Dimensions: 18 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initial Zustand |
| 0x01 | Aufstarten |
| 0x02 | Herunterfahren |
| 0x03 | Bereitschaft |
| 0x04 | Fehler |
| 0x05 | Funktionaler Abbruch |
| 0x06 | Notbetrieb N1 nach N2 |
| 0x07 | Automatikbetrieb N1 nach N2 |
| 0x08 | Automatikbetrieb N2 nach N1 |
| 0x09 | Diagnosebereitschaft |
| 0x0A | Diagnosebetrieb N1 nach N2 |
| 0x0B | Diagnosebetrieb N2 nach N1 |
| 0x0C | Externes Laden N1 nach N2 |
| 0x0D | Zusatzheizung N2 nach N1 |
| 0x0E | Ladung N2 nach N1 |
| 0x0F | Bereitschaft kommandierter Modus |
| 0x10 | Kommandierter Modus N1 nach N2 |
| 0x11 | Kommandierter Modus N2 nach N1 |
