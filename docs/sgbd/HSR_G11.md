# HSR_G11.prg

- Jobs: [30](#jobs)
- Tables: [69](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Hinterachs-Schräglauf-Regelung |
| ORIGIN | BMW EF-413 Schillitz |
| REVISION | 2.003 |
| AUTHOR | ZF OTEC2 Schmidt |
| COMMENT | - |
| PACKAGE | 1.89 |
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
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default
- [STATUS_BETRIEBSMODE](#job-status-betriebsmode) - Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default
- [STEUERN_BETRIEBSMODE](#job-steuern-betriebsmode) - Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events $02 eventWindowTime - infinite (LH Diagnosemaster V11 oder höher, Umsetzung nach LH V6 - V10 wird jedoch toleriert)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CALID_CVN_LESEN](#job-calid-cvn-lesen) - OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number
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
- [ARG_0XAB94_R](#table-arg-0xab94-r) (1 × 14)
- [AUSWERTUNG_NVSHARE_INIT](#table-auswertung-nvshare-init) (4 × 2)
- [BF_22_F152_SUPPLIERINFO](#table-bf-22-f152-supplierinfo) (2 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (63 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (26 × 9)
- [HW_MODEL](#table-hw-model) (5 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (105 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (86 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X4000_D](#table-res-0x4000-d) (6 × 10)
- [RES_0X4001_D](#table-res-0x4001-d) (6 × 10)
- [RES_0X4006_R](#table-res-0x4006-r) (1 × 13)
- [RES_0XAB92_R](#table-res-0xab92-r) (6 × 13)
- [RES_0XAB94_R](#table-res-0xab94-r) (6 × 13)
- [RES_0XD6A6_D](#table-res-0xd6a6-d) (4 × 10)
- [RES_0XD6A7_D](#table-res-0xd6a7-d) (4 × 10)
- [RES_0XD6A8_D](#table-res-0xd6a8-d) (8 × 10)
- [RES_0XD6A9_D](#table-res-0xd6a9-d) (5 × 10)
- [RES_0XD6AB_D](#table-res-0xd6ab-d) (3 × 10)
- [RES_0XDB33_D](#table-res-0xdb33-d) (6 × 10)
- [RES_0XDB34_D](#table-res-0xdb34-d) (4 × 10)
- [RES_0XDB35_D](#table-res-0xdb35-d) (5 × 10)
- [RES_0XDB36_D](#table-res-0xdb36-d) (3 × 10)
- [RES_0XDB37_D](#table-res-0xdb37-d) (7 × 10)
- [RES_0XDB3C_D](#table-res-0xdb3c-d) (11 × 10)
- [RES_0XDB3D_D](#table-res-0xdb3d-d) (2 × 10)
- [RES_0XDB3E_D](#table-res-0xdb3e-d) (2 × 10)
- [RES_0XDBB6_D](#table-res-0xdbb6-d) (3 × 10)
- [RES_0XDBBB_D](#table-res-0xdbbb-d) (2 × 10)
- [RES_0XF152_D](#table-res-0xf152-d) (2 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (29 × 16)
- [STATUS_RAM_DATEN_SCHREIBEN_TAB](#table-status-ram-daten-schreiben-tab) (4 × 2)
- [TAB_0X28A6](#table-tab-0x28a6) (1 × 5)
- [TAB_ADSTATE](#table-tab-adstate) (7 × 2)
- [TAB_ENTLASTUNG_GENERATOR](#table-tab-entlastung-generator) (16 × 2)
- [TAB_FEHLERSPEICHERSPERRE](#table-tab-fehlerspeichersperre) (4 × 2)
- [TAB_GUELTIGKEIT_CAS_FAHRGESTELLNR](#table-tab-gueltigkeit-cas-fahrgestellnr) (8 × 2)
- [TAB_LENKWINKEL_ISTWERT_GUELTIGKEIT_NR](#table-tab-lenkwinkel-istwert-gueltigkeit-nr) (3 × 2)
- [TAB_MLW_RESET_DURCH](#table-tab-mlw-reset-durch) (4 × 2)
- [TAB_QUALIFIER_LENKUNG_HINTERACHSE](#table-tab-qualifier-lenkung-hinterachse) (19 × 2)
- [TAB_RESET_OBD](#table-tab-reset-obd) (3 × 2)
- [TAB_ROLLENMODUS_1](#table-tab-rollenmodus-1) (7 × 2)
- [TAB_SIGNALQUALIFIER](#table-tab-signalqualifier) (13 × 2)
- [TAB_SOLLLENKWINKEL_QUALIFIER](#table-tab-solllenkwinkel-qualifier) (5 × 2)
- [TAB_SPANNUNSEINBRUCH_BORDNETZ](#table-tab-spannunseinbruch-bordnetz) (6 × 2)
- [TAB_STATUS_ENERGIE](#table-tab-status-energie) (5 × 2)
- [TAB_STEUERUNG_BASIS_TEILNETZE](#table-tab-steuerung-basis-teilnetze) (16 × 2)
- [TAB_SYSTEM_STATE_HSR](#table-tab-system-state-hsr) (16 × 2)
- [TAB_VM_ANTRIEB](#table-tab-vm-antrieb) (7 × 2)
- [TAB_ZUSTAND_FAHRZEUG_1](#table-tab-zustand-fahrzeug-1) (11 × 2)

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

<a id="table-arg-0xab94-r"></a>
### ARG_0XAB94_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LENKWINKEL | + | - | ° | - | signed long | - | - | 1000.0 | 1.0 | 0.0 | - | - | Fährt den gewünschten Lenkwinkel (LENKWINKEL) an der Hinterachse. |

<a id="table-auswertung-nvshare-init"></a>
### AUSWERTUNG_NVSHARE_INIT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Fehler und CRC Check nicht abgeschlossen |
| 1 | kein Fehler und CRC Check abgeschlossen |
| 16 | Fehler und CRC Check nicht abgeschlossen |
| 17 | Fehler und CRC Check abgeschlossen |

<a id="table-bf-22-f152-supplierinfo"></a>
### BF_22_F152_SUPPLIERINFO

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HWMODEL | 0-n | high | unsigned char | 0xC0 | HW_MODEL | - | - | - | hardware model |
| STAT_SUPPLIERINFOFIELD | 0-n | high | unsigned char | 0x3F | - | - | - | - | supplierInfo |

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

Dimensions: 63 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x022B00 | Energiesparmode aktiv | 0 | - |
| 0x022B08 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x022B09 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x022B0A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x022B0B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x022B0C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02FF2B | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x480380 | Steuergerät intern - Hardwarefehler | 0 | - |
| 0x480381 | Ruhestrom Plausibilisierung Kl15N lokal mit Bus-Signal | 0 | - |
| 0x480385 | Stellmotor Motorblockade | 0 | - |
| 0x480389 | Stellmotor Sensorplausibilisierung | 0 | - |
| 0x48038E | Steuergerät intern - Diversitäres Rechnen | 0 | - |
| 0x480396 | Spannungsversorgung Lokale Unterspannung KL30 | 0 | - |
| 0x480398 | Spannungsversorgung Lokale Überspannung KL30 | 0 | - |
| 0x48039A | Steuergerät intern - Softwarefehler | 0 | - |
| 0x48039C | Steuergerät intern - Übertemperatur | 0 | - |
| 0x4803A9 | Spannungsversorgung - Globale Überspannung extern | 1 | - |
| 0x4803AA | Spannungsversorgung - Globale Unterspannung intern | 1 | - |
| 0x4803AB | Spannungsversorgung - Globale Unterspannung extern | 1 | - |
| 0x4803AC | Spannungsversorgung - Globale Überspannung intern | 1 | - |
| 0x4803AF | Steuergerät intern - ZFLS - Hardware - EEPROM defekt | 0 | - |
| 0x4803B0 | Steuergerät intern - Powerpack Defekt | 0 | - |
| 0x4803B1 | Steuergerät intern - Leistungsdichtebegrenzung aufgetreten | 0 | - |
| 0x4803B2 | Sensor - Rotorlage - Lenkwinkel - Hardware defekt | 0 | - |
| 0x4803B3 | Während Init Position Anfahren nicht möglich | 0 | - |
| 0x4803B4 | Indexsensor Fehler | 0 | - |
| 0x4803B5 | Querverbau Indexsensor | 0 | - |
| 0x4803B6 | Generierte Winkel IFG zu groß | 0 | - |
| 0x4803B7 | Empfangener Lenkwinkel zu groß | 1 | - |
| 0x4803B8 | Lage Drehzahl Kaskade | 0 | - |
| 0x4803B9 | Initialisierung Lenkwinkel konnte nicht abgeschlossen werden innerhalb von 5s | 0 | - |
| 0x4803BA | Steuergerät intern - ROM fehlerhaft | 0 | - |
| 0x4803BB | Steuergerät intern - RAM fehlerhaft | 0 | - |
| 0x4803BC | Steuergerät intern - Watchdog Ereignis | 0 | - |
| 0x4803BD | Steuergerät intern - NVRAM fehlerhaft | 0 | - |
| 0x4803BE | Steuergerät intern - Softwarefehler - OBD | 0 | - |
| 0x4803BF | Steuergerät intern - MCU Temperatur Sensor OOR | 0 | - |
| 0x4803C0 | Steuergerät intern - Hardwarefehler - OBD | 0 | - |
| 0x4803C1 | HSR Abschaltung wegen fehlerhafter Energieversorgung | 1 | - |
| 0x4803C2 | Geringfügig erhöhter Ruhestrom | 0 | - |
| 0x4803C3 | Sensor - Rotorlage - Lenkwinkel - Hardware defekt_OOR | 0 | - |
| 0xD3C41F | Flexray:  Physikalischer Busfehler | 0 | - |
| 0xD3C420 | FLEXRAY Controller Error | 0 | - |
| 0xD3CBFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xD3D4B8 | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Timeout | 1 | - |
| 0xD3D4B9 | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Checksumme | 1 | - |
| 0xD3D4BA | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Alive | 1 | - |
| 0xD3D4BE | Signalfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Ungültig | 1 | - |
| 0xD3D4BF | Signalfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Undefiniert | 1 | - |
| 0xD3D4FF | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Checksumme | 1 | - |
| 0xD3D565 | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Alive | 1 | - |
| 0xD3D600 | Botschaftsfehler (Energie Degradation Fahrdynamik, ID: ENERG_DGR_DRDY) Timeout | 1 | - |
| 0xD3D60C | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Timeout | 1 | - |
| 0xD3D645 | Signalfehler (Energie Degradation Fahrdynamik, ID: ENERG_DGR_DRDY) Ungültig | 1 | - |
| 0xD3D65E | Signalfehler (Zustand Fahrzeug, ID: CON_VEH) Ungültig | 1 | - |
| 0xD3D858 | Signalfehler (Zustand Fahrzeug, ID: CON_VEH) Undefiniert | 1 | - |
| 0xD3D88D | Botschaftsfehler (Soll Lenkwinkel Stellglied, ID: TAR_STEA_ACT) - Timeout | 1 | - |
| 0xD3D88E | Botschaftsfehler (Soll Lenkwinkel Stellglied, ID: TAR_STEA_ACT) - Checksumme | 1 | - |
| 0xD3D88F | Botschaftsfehler (Soll Lenkwinkel Stellglied, ID: TAR_STEA_ACT) - Alive | 1 | - |
| 0xD3D891 | Signalfehler (Soll Lenkwinkel Stellglied, ID: TAR_STEA_ACT) - Ungültig | 1 | - |
| 0xD3D892 | Signalfehler (Soll Lenkwinkel Stellglied, ID: TAR_STEA_ACT) - Undefiniert | 1 | - |
| 0xD3DA3E | Signalfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Qualifier | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 26 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | KALTSTART_VORHANDEN | 0/1 | High | 0x01 | - | - | - | - |
| 0x0002 | MSA_START_VORHANDEN | 0/1 | High | 0x02 | - | - | - | - |
| 0x0003 | MOTOR_LAEUFT | 0/1 | High | 0x04 | - | - | - | - |
| 0x0004 | GLOBALE_BITS_VORHANDEN | 0/1 | High | 0x08 | - | - | - | - |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | Text | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2863 | USP_STATUS_GENERATORENTLASTUNG | 0-n | High | 0xFF | TAB_ENTLASTUNG_GENERATOR | - | - | - |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2898 | USP_DTC_URSAECHLICHER_FEHLER_4BYTE | HEX | High | signed long | - | - | - | - |
| 0x28A6 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x4003 | HSR_VORGABE_MAXSTROM | A | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5000 | AKTUATOR_TEMPERATUR | °C | High | unsigned char | - | 1.0 | 1.0 | -50.0 |
| 0x5001 | SG_TEMPERATUR | °C | High | unsigned char | - | 1.0 | 1.0 | -50.0 |
| 0x5006 | SYSTEMZUSTAND | 0-n | High | 0xFF | TAB_SYSTEM_STATE_HSR | - | - | - |
| 0x5007 | UPTIME | ms | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x5008 | FEHLERCODE | HEX | High | unsigned char | - | - | - | - |
| 0x5009 | Fehlerart | HEX | High | unsigned int | - | - | - | - |
| 0x500A | SOLLWERTQUALIFIER_ANSTEUERUNG | 0-n | High | 0xFF | TAB_SOLLLENKWINKEL_QUALIFIER | - | - | - |
| 0x500B | SERVICEQUALIFIER | 0-n | High | 0xFF | TAB_QUALIFIER_LENKUNG_HINTERACHSE | - | - | - |
| 0x500E | STELLERGESCHWINDIGKEIT | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x501B | MOTORMOMENT | Nm | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x501D | SOLL_LENKWINKEL_HSR | ° | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x501E | IST_LENKWINKEL_HSR | ° | High | signed int | - | 1.0 | 1000.0 | 0.0 |
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

Dimensions: 105 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x200208 | DATA_FLASH_READ | 0 | - |
| 0x200209 | DATA_FLASH_WRITE | 0 | - |
| 0x20020A | DATA_FLASH_VERIFY | 0 | - |
| 0x20020B | DATA_FLASH_WRONG_LAYOUT | 0 | - |
| 0x20020C | NV_SHARE | 0 | - |
| 0x20020D | HWL_SPI_COM | 0 | - |
| 0x20020F | HWL_WD_CHECK | 0 | - |
| 0x200210 | HWL_ASIC | 0 | - |
| 0x200213 | HWL_SPI_OUTPUT_STAGE_DRV | 0 | - |
| 0x200214 | HWL_SHUT_DOWN | 0 | - |
| 0x200215 | HWL_ADC_FREEZE | 0 | - |
| 0x200216 | HWL_CURRENT | 0 | - |
| 0x200217 | HWL_CURRENT_OFFSET | 0 | - |
| 0x200218 | HWL_OUTPUT_STAGE_DRV | 0 | - |
| 0x200219 | HWL_PWD | 0 | - |
| 0x20021A | HWL_ROM | 0 | - |
| 0x20021B | HWL_RAM | 0 | - |
| 0x20021E | HWL_RESET | 0 | - |
| 0x20021F | OS_MON | 0 | - |
| 0x200220 | OS_MEM | 0 | - |
| 0x200221 | HWL_FOR_OC | 0 | - |
| 0x200222 | HWL_FOR_WREL | 0 | - |
| 0x200223 | HWL_FOR_ANGLE | 0 | - |
| 0x200224 | HWL_FOR_LENGTH | 0 | - |
| 0x200225 | HWL_FOR_TIMO | 0 | - |
| 0x200226 | COMP_L1 | 0 | - |
| 0x200227 | COMP_L2 | 0 | - |
| 0x200228 | HWL_CCU_RED | 0 | - |
| 0x200229 | UCU_RED | 0 | - |
| 0x20022A | HWL_UCO_RED | 0 | - |
| 0x20022C | HWL_PD_RED | 0 | - |
| 0x20022D | UUT_RED | 0 | - |
| 0x20022F | HIGH_VOLT_WARN_INT | 0 | - |
| 0x200230 | LOW_VOLT_WARN_INT | 0 | - |
| 0x200231 | HWL_HIGH_VOLT_OFF | 0 | - |
| 0x200232 | HWL_LOW_VOLT_OFF | 0 | - |
| 0x200233 | HWL_VOLT_PLAUSI | 0 | - |
| 0x200234 | HWL_TEMP_OOR | 0 | - |
| 0x200235 | SWGEN | 0 | - |
| 0x200236 | HWL_BIST | 0 | - |
| 0x200237 | HWL_ERROR_PIN | 0 | - |
| 0x200238 | HWL_PBUS | 0 | - |
| 0x200239 | HWL_SGA | 0 | - |
| 0x20023A | EH_MON | 0 | - |
| 0x20023B | HWL_RSRADIUS | 0 | - |
| 0x20023C | HWL_RSDIFF | 0 | - |
| 0x20023E | XCPFLASH | 0 | - |
| 0x20023F | HWL_RS_SLAVE_MON | 0 | - |
| 0x200240 | HWL_TEMP_DIFF | 0 | - |
| 0x200241 | HIGH_VOLT_WARN_EXT | 0 | - |
| 0x200242 | LOW_VOLT_WARN_EXT | 0 | - |
| 0x200243 | DEBUG | 0 | - |
| 0x200260 | ACT_BLOCK | 0 | - |
| 0x200261 | POS_INIT_TIMEOUT | 0 | - |
| 0x200262 | LIN_POS_SENS | 0 | - |
| 0x200263 | ACT_CHECK | 0 | - |
| 0x200264 | PAS_FRAME_ERROR | 0 | - |
| 0x200265 | QDM_COM | 0 | - |
| 0x200266 | LIN_POS_BZ | 0 | - |
| 0x200267 | LIN_POS_CHECKSUMME | 0 | - |
| 0x200268 | LIN_POS_ERRORBYTE | 0 | - |
| 0x200269 | LIN_POS_HALLSWITCH | 0 | - |
| 0x20026A | LIN_POS_RLS_PLAUSI | 0 | - |
| 0x20026B | LIN_POS_TIMEOUT | 0 | - |
| 0x20026C | LIN_POS_QUERVERBAU | 0 | - |
| 0x20026D | LIN_POS_SUM_PLAUSI | 0 | - |
| 0x20026E | LIN_POS_SENS_STARTUP | 0 | - |
| 0x20026F | IFG_ANG | 0 | - |
| 0x200270 | QDM_ANG | 0 | - |
| 0x200271 | HWL_VOLT_NOSTART | 0 | - |
| 0x200273 | LIN_POS_SUM_DYN_PLAUSI | 0 | - |
| 0x200274 | HWL_SW_PLAUSI | 0 | - |
| 0x200275 | HWL_FOC_PLAUSI | 0 | - |
| 0x200276 | HWL_FLOAT | 0 | - |
| 0x200277 | HWL_CURR_SENS_DEFECT | 0 | - |
| 0x200278 | HWL_TLC | 0 | - |
| 0x200279 | HWL_MP_RED | 0 | - |
| 0x20027A | HWL_ERREVT_PLAUSI | 0 | - |
| 0x20027B | PRODMODE_ACTIVE | 0 | - |
| 0x20027C | PAS_CURRENT | 0 | - |
| 0x20027D | KL15N_PLAUSI | 0 | - |
| 0x20027E | HWL_MOTOR_MON | 0 | - |
| 0x20027F | RESET | 0 | - |
| 0x2002A1 | FRSM_E_CLUSTER_STARTUP_0 | 0 | - |
| 0x2002A2 | PORT_E_WRITE_FAILURE | 0 | - |
| 0x2002A4 | PDUR_E_PDU_INSTANCE_LOST | 0 | - |
| 0x2002A6 | MCU_E_WRITE_FAILURE | 0 | - |
| 0x2002A7 | MCU_E_LVI_FAILURE | 0 | - |
| 0x2002A8 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x2002AA | FR_E_ACCESS | 0 | - |
| 0x2002AC | FRIF_E_JLE_SYNC_0 | 0 | - |
| 0x2002AD | FLS_E_WRITE_FAILED | 0 | - |
| 0x2002AE | FLS_E_UNEXPECTED_FLASH_ID | 0 | - |
| 0x2002AF | FLS_E_SET_FREQUENCY_FAILED | 0 | - |
| 0x2002B0 | FLS_E_READ_FAILED | 0 | - |
| 0x2002B1 | FLS_E_ERASE_FAILED | 0 | - |
| 0x2002B2 | FLS_E_COMPARE_FAILED | 0 | - |
| 0x2002B3 | FEE_E_WRITE_FAILED | 0 | - |
| 0x2002B4 | FEE_E_STARTUP_FAILED | 0 | - |
| 0x2002B5 | FEE_E_READ_FAILED | 0 | - |
| 0x2002B6 | FEE_E_FORMAT_FAILED | 0 | - |
| 0x2002B7 | Steuergerät intern - Security DiagnoseRequest in verriegeltem Zustand erhalten | 0 | - |
| 0x4803AD | Versorgung Stromaufnahmebegrenzung | 1 | - |
| 0x4803AE | AGB - Ueberwachung - Ueberlast | 0 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 86 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4003 | HSR_VORGABE_MAXSTROM | A | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4004 | Tester ID Typ | HEX | High | unsigned int | - | - | - | - |
| 0x501D | SOLL_LENKWINKEL_HSR | ° | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x501E | IST_LENKWINKEL_HSR | ° | High | signed int | - | 1.0 | 1000.0 | 0.0 |
| 0x6000 | HallSwitch1_IOValue | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6001 | HallSwitch2_IOValue | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6002 | mlxIndexSensorPositionA | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6003 | mlxIndexSensorPositionB | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6004 | wApplI_RotorPosition_xds32 | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6005 | AscCtrlI_GetLA_REG | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6009 | uadVoltage1V2 | V | High | unsigned char | - | 1.0 | 100.0 | 0.0 |
| 0x600A | uioUdNotFilt | - | High | unsigned int | - | 1.0 | 64.0 | 0.0 |
| 0x600B | uApplI_SupplyVoltage | V | High | unsigned int | - | 1.0 | 64.0 | 0.0 |
| 0x600C | yOsMon_RestartReason | HEX | High | unsigned long | - | - | - | - |
| 0x600D | MK_ERROR_INFO_SERVICE_ID | HEX | High | unsigned char | - | - | - | - |
| 0x600E | MK_ERROR_INFO_ERROR_ID | HEX | High | unsigned char | - | - | - | - |
| 0x600F | MK_ERROR_INFO_CULPRIT_ID | HEX | High | unsigned char | - | - | - | - |
| 0x6010 | MK_ERROR_INFO_CULPRIT_TYPE | HEX | High | unsigned char | - | - | - | - |
| 0x6011 | MK_ERROR_INFO_CULPRIT | HEX | High | unsigned char | - | - | - | - |
| 0x6012 | yOsMon_AktTask | HEX | High | unsigned char | - | - | - | - |
| 0x6013 | NAPPLI_ROTOR_SPEED_FILT | rad/s | High | signed int | - | 1.0 | 50.0 | 0.0 |
| 0x6014 | MAPPLI_LIMITED_MOTOR_TORQUE | Nm | High | signed int | - | 1.0 | 1024.0 | 0.0 |
| 0x6015 | icuCurrentPhaseU_IRQ | A | High | motorola float | - | 16.0 | 1.0 | 0.0 |
| 0x6016 | icuCurrentPhaseW_IRQ | A | High | motorola float | - | 16.0 | 1.0 | 0.0 |
| 0x6017 | wApplI_RotorPosition_xds32_High | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6018 | WRS_CURR_ROTOR_POS_IRQ_HIGH | ° | High | unsigned char | - | 92160.0 | 4096.0 | 0.0 |
| 0x6019 | feeNvShareCrcErrorDetected_gdb \| feeIsNvShareCrcCheckFinished_gdb | 0-n | High | 0xFF | AUSWERTUNG_NVSHARE_INIT | - | - | - |
| 0x601A | yeeFirstUnusedNVShareAddr_gdu32 | HEX | High | unsigned int | - | - | - | - |
| 0x601B | ycrRomRamEccEIPC | HEX | High | unsigned long | - | - | - | - |
| 0x601C | ycrRomRamEccAddr | HEX | High | unsigned long | - | - | - | - |
| 0x601D | ycpErrorIdentLevel1 | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x601E | ycpPosValueLevel1 | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x601F | ycpNegValueLevel1 | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6020 | ycpUpperLimitLevel1 | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6021 | ycpLowerLimitLevel1 | - | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6022 | yodPWM_xau16(0) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6023 | yodPWM_xau16(1) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6024 | yodPWM_xau16(2) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6025 | yodPWD_xau16(0) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6026 | yodPWD_xau16(1) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6027 | yodPWD_xau16(2) | % | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6028 | ioCSIE0TransferStatus | HEX | High | unsigned char | - | - | - | - |
| 0x6029 | zckCSIE0RetryCounter_xdu8 | HEX | High | unsigned char | - | - | - | - |
| 0x602A | zckCSIE0TotalRetryCounter_xdu32 | HEX | High | unsigned long | - | - | - | - |
| 0x602B | ioCSIE0CmdQueuePointer | HEX | High | unsigned char | - | - | - | - |
| 0x602C | ioCSIE0CmdQueueSize | HEX | High | unsigned char | - | - | - | - |
| 0x602D | ioCSIE0FirstCmdNotSend | HEX | High | unsigned int | - | - | - | - |
| 0x602E | uioRpSinMain | V | High | unsigned int | - | 1.0 | 4960.0 | 0.0 |
| 0x602F | uioRpCosMain | V | High | unsigned int | - | 1.0 | 4960.0 | 0.0 |
| 0x6030 | uioRpSin2Main | V | High | unsigned int | - | 1.0 | 4960.0 | 0.0 |
| 0x6031 | uioRpCos2Main | V | High | unsigned int | - | 1.0 | 4960.0 | 0.0 |
| 0x6032 | uadHall1 | V | High | signed char | - | 52.8 | 1023.0 | 0.0 |
| 0x6033 | uadHall2 | V | High | signed char | - | 52.8 | 1023.0 | 0.0 |
| 0x6034 | ursAsicSinOffset_xds16 | mV | High | unsigned char | - | 25.0 | 55.0 | 0.0 |
| 0x6035 | ursAsicCosOffset | mV | High | unsigned char | - | 25.0 | 55.0 | 0.0 |
| 0x6036 | xrsAsicSinAmp | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x6037 | AscWdI_GetOutputState | HEX | High | unsigned char | - | - | - | - |
| 0x6038 | AscCtrlI_GetSyncFSM | HEX | High | unsigned char | - | - | - | - |
| 0x6039 | AscCtrlI_GetREQULOFinish | HEX | High | unsigned char | - | - | - | - |
| 0x603A | AscWdI_GetThreshold | HEX | High | unsigned char | - | - | - | - |
| 0x603B | AscCtrlI_GetSyncRDT_REG | HEX | High | unsigned char | - | - | - | - |
| 0x603C | AscCtrlI_GetSyncEHR_REG | HEX | High | unsigned char | - | - | - | - |
| 0x603D | AscCtrlI_GetDIA1_REG | HEX | High | unsigned char | - | - | - | - |
| 0x603E | AscCtrlI_GetDIA2_REG | HEX | High | unsigned char | - | - | - | - |
| 0x603F | AscCtrlI_GetDIA3_REG | HEX | High | unsigned char | - | - | - | - |
| 0x6040 | AscCtrlI_GetDIA4_REG | HEX | High | unsigned char | - | - | - | - |
| 0x6041 | AscCtrlI_GetDIA5_REG | HEX | High | unsigned char | - | - | - | - |
| 0x6042 | cApplI_DbcTempU_xds16 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6043 | cApplI_DbcTempV_xds16 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6044 | cApplI_DbcTempW_xds16 | °C | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x6045 | ycpErrorIdentLevel2_xdu16 | HEX | High | unsigned int | - | - | - | - |
| 0x6046 | ycpConversionFactor | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x6047 | lApplI_RackPosition | mm | High | signed int | - | 1.0 | 32.0 | 0.0 |
| 0x604E | MK_protectionInfo-&gt;culprit-&gt;regs-&gt;pc | HEX | High | unsigned long | - | - | - | - |
| 0x604F | VMADR | HEX | High | unsigned long | - | - | - | - |
| 0x6050 | MK_protectionInfo-&gt;memoryPartition | HEX | High | unsigned char | - | - | - | - |
| 0x6051 | MK_protectionInfo-&gt;objectType | HEX | High | unsigned char | - | - | - | - |
| 0x6056 | BackgroundStatus | HEX | High | unsigned int | - | - | - | - |
| 0x6057 | OperationStatus | HEX | High | unsigned char | - | - | - | - |
| 0x6058 | AccessStatus | HEX | High | unsigned char | - | - | - | - |
| 0x6059 | BlockBitCoded | HEX | High | unsigned long | - | - | - | - |
| 0x605A | Status | HEX | High | unsigned int | - | - | - | - |
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

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECUMehrmalsProgrammierbar |
| 1 | ECUMindestensEinmalVollstaendigProgrammierbar |
| 2 | ECUNichtMehrProgrammierbar |

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

<a id="table-res-0x4000-d"></a>
### RES_0X4000_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMP_ECU_HSR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -70.0 | Gefilterte Temperatur Leiterplatte |
| STAT_TEMP_PCU_HSR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -70.0 | Gefilterte Temperatur Endstufe |
| STAT_MOTORLAGEWINKEL_SENSOR1_WERT | ° | high | signed int | - | - | 1.0 | 64.0 | 0.0 | Motorlagewinkel Sensor1 |
| STAT_STAT_AGB_AKIV | 0/1 | high | unsigned char | - | - | - | - | - | Info ob Aktuatorgeschwindigkeitsbegrenzung aktuell begrenzt. |
| STAT_SYSTEM_STATE | 0-n | high | unsigned char | - | TAB_SYSTEM_STATE_HSR | - | - | - | Zustand der HSR state machine |
| STAT_VERFAHRWEG_RWL_SET_WERT | mm | high | signed int | - | - | 1.0 | 2048.0 | 0.0 | Verfahrweg des Stellers während RWL-Set |

<a id="table-res-0x4001-d"></a>
### RES_0X4001_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZF_SW_KENNUNG_BASIS_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Basis |
| STAT_ZF_SW_KENNUNG_VARIANTE_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Variante |
| STAT_ZF_SW_KENNUNG_SAMPLE_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Sample |
| STAT_ZF_SW_KENNUNG_VERSION_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Version |
| STAT_ZF_SW_KENNUNG_MAJOR_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Major |
| STAT_ZF_SW_KENNUNG_MINOR_TEXT | TEXT | high | string[4] | - | - | 1.0 | 1.0 | 0.0 | ZF Softwarebezeichnung Minor |

<a id="table-res-0x4006-r"></a>
### RES_0X4006_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RAM_DATEN_SCHREIBEN | - | - | + | 0-n | high | unsigned char | - | STATUS_RAM_DATEN_SCHREIBEN_TAB | - | - | - | Status RAM_DATEN_SCHREIBEN |

<a id="table-res-0xab92-r"></a>
### RES_0XAB92_R

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ICM_FREIGABE | - | - | + | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt an ob die Freigabe seitens ICM-QL besteht: 0=Nein; 1=Ja |
| STAT_SG_FREIGABE | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob die Freigabe seitens SG besteht: 0=Nein; 1=Ja |
| STAT_AUSLENKUNG_MOEGLICH | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob der Auslenkungstest ausgeführ werden kann: 0=Nein; 1=Ja |
| STAT_AUSLENKUNG_AKTIV | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob die Auslenkung momentan aktiv ist: 0=Nein; 1=Ja |
| STAT_SOLLMOMENT_WERT | - | - | + | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Gibt das aktuelle Sollmoment an |
| STAT_LETZTE_AUSLENKUNG | - | - | + | 0-n | high | unsigned char | - | TAB_ADSTATE | - | - | - | Zeigt an, ob der letzte Auslenkungstest erfolgreich ausgeführt wurde |

<a id="table-res-0xab94-r"></a>
### RES_0XAB94_R

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ICM_FREIGABE | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob die Freigabe seitens ICM-QL besteht: 0=Nein; 1=Ja |
| STAT_SG_FREIGABE | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob die Freigabe seitens SG besteht: 0=Nein; 1=Ja |
| STAT_AUSLENKUNG_MOEGLICH | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob der Auslenkungstest ausgefuehrt werden kann: 0=Nein; 1=Ja |
| STAT_AUSLENKUNG_AKTIV | - | - | + | 0/1 | - | unsigned char | - | - | - | - | - | Gibt an ob die Auslenkung momentan aktiv ist : 0=Nein; 1=Ja |
| STAT_SOLLMOMENT_WERT | - | - | + | % | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt das aktuelle Sollmoment an |
| STAT_LETZTE_AUSLENKUNG | - | - | + | 0-n | - | unsigned char | - | TAB_ADSTATE | - | - | - | Zeigt an, ob der letzte Auslenkungstest erfolgreich ausgeführt wurde |

<a id="table-res-0xd6a6-d"></a>
### RES_0XD6A6_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_LOW_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Temperaturbereich  1, (&lt; Abschaltschwelle - 10 °C), Zähltakt 60s |
| STAT_ZAEHLER_MIDDLE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Temperaturbereich 2, (&gt;= Temp1 UND &lt;Abschaltschwelle °C), Zähltakt 60s |
| STAT_ZAEHLER_HIGH_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Temperaturbereich 3, (&gt;= Abschaltschwelle ), Zähltakt 60s |
| STAT_TEMP_MAX_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Maximaler Temperaturwert, Messtakt 100ms |

<a id="table-res-0xd6a7-d"></a>
### RES_0XD6A7_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_USP1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Spannungsbereich 1, (&lt; 6V), Messtakt 1ms |
| STAT_ZAEHLER_USP2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Spannungsbereich 2, (&gt;=6 V UND &lt; 6,8V), Messtakt 1ms |
| STAT_ZAEHLER_USP3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Spannungsbereich 3, (&gt;= 6,8V UND &lt; 8V), Messtakt 1ms |
| STAT_ZAEHLER_USP4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler Spannungsbereich 4, (&gt;=8V), Messtakt 1ms |

<a id="table-res-0xd6a8-d"></a>
### RES_0XD6A8_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPG_KLASSE_U1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &lt; 6,8V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_KLASSE_U2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt;= 6,8V UND &lt;9V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_KLASSE_U3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt;=9V UND &lt; 11V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_KLASSE_U4_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt;= 11V UND &lt; 18V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_KLASSE_U5_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt;= 18V UND &lt; 27V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_KLASSE_U6_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt;= 27V, Messtakt: halbe Filterzeit ms |
| STAT_SPG_MIN_WERT | V | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Spannung unterster Wert, Messtakt: halbe Filterzeit ms |
| STAT_SPG_MAX_WERT | V | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Spannung oberster Wert, Messtakt: halbe Filterzeit ms |

<a id="table-res-0xd6a9-d"></a>
### RES_0XD6A9_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STROM_KLASSE_I1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt; 0,5*Imax UND &lt;= 0,75*Imax, Messtakt: halbe Filterzeit ms |
| STAT_STROM_KLASSE_I2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt; 0,75*Imax UND &lt;= Imax, Messtakt: halbe Filterzeit ms |
| STAT_STROM_KLASSE_I3_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | &gt; Imax, Messtakt: halbe Filterzeit ms |
| STAT_STROM_MIN_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | -100.0 | Strom unterster Wert (Rückspeisung), Messtakt: 10 ms |
| STAT_STROM_MAX_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strom oberster Wert, Messtakt: 10 ms |

<a id="table-res-0xd6ab-d"></a>
### RES_0XD6AB_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_AGB_V1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler  stillstandsnaher Bereich                             (0 - 5Km/h) |
| STAT_ZAEHLER_AGB_V2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler  unterer Geschwindigkeitsbereich         (&gt;5 - &lt;=50Km/h) |
| STAT_ZAEHLER_AGB_V3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler  oberer Geschwindigkeitsbereich           (&gt;50 Km/h) |

<a id="table-res-0xdb33-d"></a>
### RES_0XDB33_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LENKWINKEL_ISTWERT_WERT | ° | high | unsigned int | - | - | 2.747 | 1000.0 | -90.0 | Aktueller Ist-Lenkwinkel Hinterachse (Signal: Ist_Lenkwinkel_Hinterachse_Stellglied) |
| STAT_LENKWINKEL_ISTWERT_GUELTIGKEIT_NR | 0-n | high | unsigned char | - | TAB_LENKWINKEL_ISTWERT_GUELTIGKEIT_NR | - | - | - | Qualifier für den Ist-Lenkwinkel Hinterachse (Signal: Qualifier_Ist_Lenkwinkel_Hinterachse_Stellglied) |
| STAT_LENKWINKEL_SOLLWERT_WERT | ° | high | unsigned int | - | - | 2.747 | 1000.0 | -90.0 | Aktueller Soll-Lenkwinkel Hinterachse (QDM-Vorgabe) |
| STAT_MOTORWINKEL_NULLLAGE_WERT | ° | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Motorlagewinkel-Wert bei Steller-Mittenstellung (Nulllage) (FFFF wenn nicht kalibriert) |
| STAT_ANALOGSENSOR_A_NULLLAGE_WERT | HEX | high | unsigned int | - | - | - | - | - | Analogsensor A -Wert bei Steller-Mittenstellung (Nulllage). Wertebereich 0-7FFF |
| STAT_ANALOGSENSOR_B_NULLLAGE_WERT | HEX | high | unsigned int | - | - | - | - | - | Analogsensor B -Wert bei Steller-Mittenstellung (Nulllage). Wertebereich 8000-FFFF |

<a id="table-res-0xdb34-d"></a>
### RES_0XDB34_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANALOGSENSOR_A_WERT | HEX | high | unsigned int | - | - | - | - | - | Analogsensor A -Wert. Wertebereich 0-7FFF |
| STAT_ANALOGSENSOR_B_WERT | HEX | high | unsigned int | - | - | - | - | - | Analogsensor B -Wert. Wertebereich 8000-FFFF |
| STAT_HALLSENSOR_1 | 0/1 | high | unsigned char | - | - | - | - | - | Digitalsensor 1; 0 - Aus, 1 - Ein |
| STAT_HALLSENSOR_2 | 0/1 | high | unsigned char | - | - | - | - | - | Digitalsensor 2; 0 - Aus, 1 - Ein |

<a id="table-res-0xdb35-d"></a>
### RES_0XDB35_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_QUALIFIER_HSR | 0-n | high | unsigned char | - | TAB_QUALIFIER_LENKUNG_HINTERACHSE | - | - | - | (Signal: Qualifier_Service_Steuerung_Lenkung_Hinterachse_Stellglied) |
| STAT_FEHLER_AMPLITUDE_WERT | ° | high | unsigned int | - | - | 2.747 | 1000.0 | 0.0 | (Signal: Ist_Lenkwinkel_Hinterachse_Stellglied_Fehler_Amplitude) |
| STAT_IST_STROM_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signal: Ist_Strom_Hinterachse_Lenkung |
| STAT_MOTOR_ISTMOMENT_WERT | Nm | high | signed int | - | - | 1.0 | 1024.0 | 0.0 | Aktuelles Motormoment (Istwert) |
| STAT_MOTOR_SOLLMOMENT_WERT | Nm | high | signed int | - | - | 1.0 | 1024.0 | 0.0 | Aktuelles Motormoment (Sollwert) |

<a id="table-res-0xdb36-d"></a>
### RES_0XDB36_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FILTER_ZEIT_KONSTANTE_WERT | HEX | high | unsigned int | - | - | - | - | - | Filterzeit für Sollwinkel (Signal: 0Filter_Zeit_Konstante_Lenkwinkel_Hinterachse_Stellglied) |
| STAT_SOLL_LENKWINKEL_HINTERACHSE_WERT | ° | high | unsigned int | - | - | 2.747 | 1000.0 | -90.0 | Soll-Lenkwinkel vom QDM |
| STAT_QUALIFIER_SOLL_LENKWINKEL_HINTERACHSE | 0-n | high | unsigned char | - | TAB_SOLLLENKWINKEL_QUALIFIER | - | - | - | Soll-Lenkwinkel Qualifier vom QDM |

<a id="table-res-0xdb37-d"></a>
### RES_0XDB37_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPERATUR_AUSSEN_WERT | °C | high | unsigned char | - | - | 0.5 | 1.0 | -40.0 | Außentemperatur (Signal: Temperatur_Außen) (FF: Ungültig) |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_WERT | km/h | high | unsigned int | - | - | 15.625 | 1000.0 | 0.0 | Absolutgeschwindigkeit des Fahrzeugschwerpunktes (Signal: Geschwindigkeit_Fahrzeug_Schwerpunkt) |
| STAT_QUALIFIER_GESCHWINDIGKEIT_FAHRZEUG | 0-n | high | unsigned char | - | TAB_SIGNALQUALIFIER | - | - | - | Qualifier zu Absolutgeschwindigkeit des Fahrzeugschwerpunktes (Signal: Geschwindigkeit_Fahrzeug_Schwerpunkt) |
| STAT_ROLLENMODUS | 0-n | high | unsigned char | - | TAB_ROLLENMODUS_1 | - | - | - | Information über die Betriebsart Rollenprüfstand  (Signal: Status_Rollenmodus) |
| STAT_WEGSTRECKE_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzeigewert des Gesamtwegstreckenzählers  (Signal: Wegstrecke_Kilometer) |
| STAT_RELATIVZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in Sekunden seit dem Start der Systemzeit  (Signal: Zeit_Sekunde_Zähler_Relativ) |
| STAT_VERBRENNUNGSMOTOR_ANTRIEB | 0-n | high | unsigned char | - | TAB_VM_ANTRIEB | - | - | - | Zustand des Antriebs-Verbrennunsmotors (Signal: Status_Verbrennungsmotor_Antrieb) |

<a id="table-res-0xdb3c-d"></a>
### RES_0XDB3C_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VORGABE_MAXSTROM_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Maximal zulässigen DC-Last-Strom am Stecker des SGs (Signal: Maximal_Strom_Vorgabe_Hinterachse_Lenkung) |
| STAT_FEHLERSPEICHERSPERRE | 0-n | high | unsigned char | - | TAB_FEHLERSPEICHERSPERRE | - | - | - | Info zur vorgabe Fehlerspeichersperre (Signal: Status_Sperre_Fehlerspeicher_FZM) |
| STAT_STATUS_ENERGIE | 0-n | high | unsigned char | - | TAB_STATUS_ENERGIE | - | - | - | Status Energie-Info vom FZM (Signal: Status_Energie_FZM) |
| STAT_FEHLERSPEICHER_BORDNETZ_SPANNUNG_WERT | HEX | high | signed char | - | - | - | - | - | Info zu Spannungsschwellen für das Fehlerspeicherhandling (Signal: Steuerung_Fehlerspeicher_Bordnetz_Spannung) |
| STAT_ENTLASTUNG_GENERATOR | 0-n | high | unsigned char | - | TAB_ENTLASTUNG_GENERATOR | - | - | - | Zustand der Generator Entlastungsfunktion (Signal: Status_Entlastung_Generator) |
| STAT_SPANNUNGSEINBRUCH_BORDNETZ | 0-n | high | unsigned char | - | TAB_SPANNUNSEINBRUCH_BORDNETZ | - | - | - | Ankündigung des Startspannungseinbruch vor dem Start und anzeigen während dem Start. (Signal: Status_Spannungseinbruch) |
| STAT_STEUERUNG_BASIS_TEILNETZE | 0-n | high | unsigned char | - | TAB_STEUERUNG_BASIS_TEILNETZE | - | - | - | Gibt an, ob im aktuellen Fahrzeugzustand (PWF)Kommunikation benötigt wird.(Signal: Steuerung_Basis_Teilnetze) |
| STAT_ZUSTAND_FAHRZEUG | 0-n | high | unsigned char | - | TAB_ZUSTAND_FAHRZEUG_1 | - | - | - | Beschreibung des Fahrzeugzustands (PWF) aus Kundensicht(Signal: Status_Zustand_Fahrzeug ) |
| STAT_STEUERUNG_FUNKTIONALE_TEILNETZE_WERT | HEX | high | unsigned long | - | - | - | - | - | Gibt an, welche funktionalen Teilnetze aktiv sind. (Signal: Steuerung_Funktionale_Teilnetze) |
| STAT_KL15N | 0/1 | high | unsigned char | - | - | - | - | - | Status Hardware Kl15N; 0 - Aus, 1 - Ein  |
| STAT_UBAT_WERT | V | high | unsigned int | - | - | 1.0 | 64.0 | 0.0 | An Klemme 30 gemessene Versorgungsspannung |

<a id="table-res-0xdb3d-d"></a>
### RES_0XDB3D_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OBD_ZYKLUS_WERT | HEX | high | unsigned char | - | - | - | - | - | Dieses Signal enthält die Information, welcher Zyklus in der DME aktiv ist (Warm-Up-Zyklus, Driving-Zyklus, RBM-Zyklus). (Signal: Status_OBD_Zyklus) |
| STAT_RESET_OBD | 0-n | high | unsigned char | - | TAB_RESET_OBD | - | - | - | Dieses Signal enthält die Statusinfo vom  Primary Device  an das  Dependent Secondary Device , dass gerade  OBD-Fehlerspeicher löschen  angefordert wurde (Signal: Anforderung_Reset_OBD_Diagnose_Fahrdynamik) |

<a id="table-res-0xdb3e-d"></a>
### RES_0XDB3E_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAHRGESTELLNUMMER_TEXT | TEXT | high | string[7] | - | - | 1.0 | 1.0 | 0.0 | Empfangene Fahrgestellnummer |
| STAT_GUELTIGKEIT_FAHRGESTELLNR_NR | 0-n | high | unsigned char | - | TAB_GUELTIGKEIT_CAS_FAHRGESTELLNR | - | - | - | Gueltigkeit der Fahrgestellnummer CAN Botschaft :0x00 = Botschaft i.o.; 0x02 = Botschaft wurde nie empfangen; 0x04 = Mehrere Botschaften pro Abtastzyklus; 0x08 = Timeout - Botschaft faellt fuer 1 Abtastzyklus Zyklus aus; 0x10 = Fehlerwert laut Nachrichtenkatalog; 0x20 = Alive-Fehler; 0x40 = Checksummen-Fehler; 0x80 = Fehler von CRC Alive Fehlerwert Botschaft nie empfangen |

<a id="table-res-0xdbb6-d"></a>
### RES_0XDBB6_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PHASENSTROM_U_WERT | A | - | signed long | - | - | 1.0 | 1000.0 | 0.0 | Phasenstrom der Phase U am Stator des Stellmotors |
| STAT_PHASENSTROM_V_WERT | A | - | signed long | - | - | 1.0 | 1000.0 | 0.0 | Phasenstro der Phase V am Stator des Stellmotors |
| STAT_PHASENSTROM_W_WERT | A | - | signed long | - | - | 1.0 | 1000.0 | 0.0 | Phasenstrom der Phase W am Stator des Stellmotors |

<a id="table-res-0xdbbb-d"></a>
### RES_0XDBBB_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSORDIFFERENZ_WERT | ° | - | signed long | - | - | 1.0 | 1000.0 | 0.0 | Differenz zwischen Rotorlage und Spurstangenlagesensor - umgerechnet auf Position des Rotors. |
| STAT_GUELTIGKEIT_SENSORDIFFERENZ_NR | 0-n | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gueltigkeit der gebildeten Differenz |

<a id="table-res-0xf152-d"></a>
### RES_0XF152_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HW_MODIFICATION_INDEX_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Index of hardware modification:  FF: Not supported index |
| - | Bit | high | BITFIELD | - | BF_22_F152_SUPPLIERINFO | - | - | - | Tab Supplierinfo |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 29 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | high | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| RAM_DATEN_SCHREIBEN | 0x4006 | - | Dient dazu während der Inbetriebnahme angelernte applikative Daten in den nichtflüchtigen Speicher zu sichern. | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x4006_R |
| AUSLENKUNGSTEST_HINTERACHSE | 0xAB92 | - | Führt die Ansteuerung der HSR nach einem festen  Schema aus ( Steller in 0 Pos --&gt; linker Anschlag  --&gt; rechter Anschlag --&gt; 0 Pos | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAB92_R |
| AUSLENKUNG_HINTERACHSE | 0xAB94 | - | Fährt den gewünschten Lenkwinkel (LENKWINKEL) an der HA an. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAB94_R | RES_0xAB94_R |
| STATUS_TEMPERATUR_MW | 0xD6A6 | - | Statistikwerte der Steuergeräte Temperatur (Endstufe/Leistungsteil) (Abschaltschwelle EPS: 105, HSR: 95°, ASA: 85°) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6A6_D |
| STATUS_USP_MSA_MW | 0xD6A7 | - | Unterspannung während MSA-Start MSA-Minimalspannung: Counter darf nur bei aktivem MSA-Start zählen; Es ist nur ein Zählvorgang für jeden MSA-Start zulässig, der niedrigste Wert wird gezählt | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6A7_D |
| STATUS_SPANNUNG_MW | 0xD6A8 | - | Statistikzähler Spannung Eingangsgröße: gefiltete Spannung (100 ms Filterzeit um Kurzzeitpeaks herauszufiltern) außerhalb Motorstart (Kalt- und Warmstart) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6A8_D |
| STATUS_STROM_MW | 0xD6A9 | - | Statistikzähler Strom | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6A9_D |
| STATUS_MLW_INIT_MW | 0xD6AA | STAT_ZAEHLER_MLW_INIT_WERT | Zähler der Initialisierungsläufe im Kundenbetrieb (keine Werks/HO-Inbetriebnahme) | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_AGB_DEGRADATION_MW | 0xD6AB | - | Anzahl Aktuator-Geschwindigkeits-Begrenzungen Degradationen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6AB_D |
| LENKWINKEL_HINTERACHSE | 0xDB33 | - | Lenkwinkel Hinterachse | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB33_D |
| STATUS_INDEXSENSOR | 0xDB34 | - | Status Indexsensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB34_D |
| STATUS_HSR | 0xDB35 | - | Statusinfo HSR | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB35_D |
| STATUS_QDM | 0xDB36 | - | Signale von QDM | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB36_D |
| STATUS_FR_UMWELTBEDINGUNGEN | 0xDB37 | - | Über Flexray empfangene Umweltbedingungen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB37_D |
| STATUS_FZG_BORDNETZ | 0xDB3C | - | Status Fahrzeug und Bordnetz | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB3C_D |
| STATUS_OBD | 0xDB3D | - | STATUS OBD | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB3D_D |
| STATUS_FAHRGESTELLNUMMER | 0xDB3E | - | Fahrgestellnummer | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB3E_D |
| HSR_MOTORSTROEME | 0xDBB6 | - | Motorstrom des HSR Motors.  Ausgabe des Stroms für alle 3 Phasen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBB6_D |
| SENSORDIFFERENZ | 0xDBBB | - | Differenz zwischen Rotorlage und Spurstangenlagesensor - umgerechnet auf Position des Rotors | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBBB_D |
| READHWMODIFICATIONINDEX | 0xF152 | - | Dieser Service kommt nur zum Einsatz, wenn es eine geringfügige Hardwareänderung an dem Steuergerät gegeben hat, die nicht zu einer Änderung der Sachnummer bzw. der Hardware SGBM-IDs geführt hat. Eine solche Änderung ist von außen nicht diagnostizierbar, daher wurde dieser Dienst dafür eingeführt. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF152_D |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | high | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| STATUS_INTERNE_WERTE | 0x4000 | - | Ausgabe Steuergerät interner Werte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4000_D |
| STATUS_ZF_SW_KENNUNG | 0x4001 | - | ZF Softwarekennung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4001_D |
| STATUS_GESAMTWEG_STELLER_MW | 0x4002 | STAT_GESAMTWEG_STELLER_WERT | Summierter Gesamtverfahrweg des Stellers seit Produktion in m (interne Berechnung und Ablage in mm) | m | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STEUERN_RESET_MESSWERTE | 0xF000 | - | Alle Messwerte und Zähler neu initialiseren. (Zähler auf 0, MIN/MAX-Werte auf aktuellen Wert) | - | - | - | - | - | - | - | - | - | 31 | - | - |

<a id="table-status-ram-daten-schreiben-tab"></a>
### STATUS_RAM_DATEN_SCHREIBEN_TAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Schreiben erfolgreich |
| 0x01 | Schreiben  fehlgeschlagen |
| 0x02 | Schreiben läuft |
| 0x03 | Schreiben noch nicht angestoßen (Routine nicht gestartet) |

<a id="table-tab-0x28a6"></a>
### TAB_0X28A6

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0001 | 0x0002 | 0x0003 | 0x0004 |

<a id="table-tab-adstate"></a>
### TAB_ADSTATE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Abgeschlossen |
| 2 | Verweigert |
| 3 | Angehalten |
| 4 | Fehlerhaft |
| 5 | Läuft |
| 0xFF | Wert ungültig |

<a id="table-tab-entlastung-generator"></a>
### TAB_ENTLASTUNG_GENERATOR

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Entlastungsfkt. Aktiv / Rücknahme |
| 0x01 | iGR-High |
| 0x02 | SULEV-Fkt |
| 0x03 | Entlastung nach Motorstart |
| 0x04 | Rennstart mit oder ohne AGM Batterie |
| 0x05 | ELMOTENTL Hitze |
| 0x06 | ELMOTENTL Kälte |
| 0x07 | Entlastung Anfahrschwäche wie P66,P85 |
| 0x08 | Übertemperatur Generator |
| 0x09 | Entlastung aus Sicherheitsgründen |
| 0x0A | Entlastung Begrenzung Lagerkräfte |
| 0x0B | Entlastung aus Komfortgründen |
| 0x0C | Entlastung aus funktionalen Gründen |
| 0x0D | Keine Entlastungsfkt. Aktiv / Rücknahme |
| 0x0E | Vorhalt |
| 0x0F | Signal ungültig |

<a id="table-tab-fehlerspeichersperre"></a>
### TAB_FEHLERSPEICHERSPERRE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fehlerspeicherfreigabe |
| 1 | Fehlerspeichersperre |
| 2 | Reserve |
| 3 | Signal ungültig |

<a id="table-tab-gueltigkeit-cas-fahrgestellnr"></a>
### TAB_GUELTIGKEIT_CAS_FAHRGESTELLNR

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Botschaft i.O. |
| 0x02 | Botschaft wurde nie empfangen |
| 0x04 | Mehrere Botschaften pro Abtastzyklus |
| 0x08 | Timeout-Botschaft faellt fuer 1 Abtastzyklus aus |
| 0x10 | Fehlerwert laut Nachrichtenkatalag |
| 0x20 | Alive-Fehler |
| 0x40 | Checksummen-Fehler |
| 0x80 | Fehler von CRC Alive Fehlerwert Botschaft nie empfangen |

<a id="table-tab-lenkwinkel-istwert-gueltigkeit-nr"></a>
### TAB_LENKWINKEL_ISTWERT_GUELTIGKEIT_NR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 8 | Initialisierung |
| 1 | Gültig |
| 6 | Ungültig |

<a id="table-tab-mlw-reset-durch"></a>
### TAB_MLW_RESET_DURCH

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | MLW-Reset durch Tester/Diag |
| 2 | MLW-Reset durch ICM/Sollwertqualifier |
| 3 | MLW-Reset durch ASA/Sensorfehler |
| 4 | MLW-Reset durch ASA/Rekonstruktion |

<a id="table-tab-qualifier-lenkung-hinterachse"></a>
### TAB_QUALIFIER_LENKUNG_HINTERACHSE

Dimensions: 19 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 128 | Initialisierung |
| 33 | Service ist verfügbar / Drive Standby |
| 34 | Service ist verfügbar / Drive |
| 49 | Service eingeschränkt verfügbar/ Drive Standby USW1 |
| 53 | Service eingeschränkt verfügbar/ Drive Standby USW2 |
| 57 | Service eingeschränkt verfügbar/ Drive Standby USW3 |
| 50 | Service eingeschränkt verfügbar/ Drive USW1 |
| 54 | Service eingeschränkt verfügbar/ Drive USW2 |
| 58 | Service eingeschränkt verfügbar/ Drive USW3 |
| 224 | Service ist nicht verfügbar, Standby / Postrun |
| 225 | Service ist nicht verfügbar, Standby / Ready for Drive |
| 227 | Service ist nicht verfügbar, Standby / Drive Ramp Zero |
| 228 | Service ist nicht verfügbar, Standby / Wait for RLW set |
| 229 | Service ist nicht verfügbar, Diagnose / Drive Active Diag |
| 233 | Service nicht verfügbar / Unterspannung, Ready for Drive |
| 235 | Service nicht verfügbar / Unterspannung, Drive Ramp Zero |
| 237 | Service nicht verfügbar / Unterspannung, Drive Active Diag |
| 104 | Service ist nicht verfügbar, Fehler |
| 255 | Signal ungültig |

<a id="table-tab-reset-obd"></a>
### TAB_RESET_OBD

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Anforderung Reset OBD Diagnose |
| 2 | Anforderung Reset OBD Diagnose |
| 15 | Signal ungültig |

<a id="table-tab-rollenmodus-1"></a>
### TAB_ROLLENMODUS_1

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Rollprüfstand |
| 1 | Vorderachse auf Rollenprüfstand |
| 2 | Hinterachse auf Rollenprüfstand |
| 3 | Zwei-Achs-Rollenbetrieb |
| 13 | Reserviert |
| 14 | Funktion meldet Fehler |
| 15 | Signal unbefuellt |

<a id="table-tab-signalqualifier"></a>
### TAB_SIGNALQUALIFIER

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 8 | Initialisierung |
| 1 | Signalwert ist gültig und abgesichert und plausibilisiert |
| 9 | Reserved |
| 2 | Reserved |
| 10 | Signalwert ist gültig, Zustand/Status temporär |
| 3 | Reserved |
| 11 | Signalqualität bzw. Überwachung eingeschränkt, Zustand/Status temporär |
| 4 | Reserved |
| 12 | Reserved |
| 6 | Reserved |
| 14 | Signalwert ist ungültig, Zustand/Status temporär |
| 7 | Reserved |
| 15 | Signal ungültig |

<a id="table-tab-solllenkwinkel-qualifier"></a>
### TAB_SOLLLENKWINKEL_QUALIFIER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 32 | Sollwert umsetzen / set active |
| 36 | Sollwert umsetzen, Diagnose / set active |
| 224 | Sollwert nicht umsetzen, Standby / set &lt;no active&gt; |
| 228 | Sollwert nicht umsetzen, Diagnose / set &lt;no active&gt; |
| 255 | Signal ungültig |

<a id="table-tab-spannunseinbruch-bordnetz"></a>
### TAB_SPANNUNSEINBRUCH_BORDNETZ

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Spannungseinbruch |
| 1 | Startspannungseinbruch bis maximal Spannungsschwelle 1 (Warmstart) |
| 2 | Startspannungseinbruch bis maximal Spannungsschwelle 2 (Kaltstart) |
| 13 | Funktionsschnittstelle ist nicht verfuegbar |
| 14 | Reserviert |
| 15 | Signal unbefuellt |

<a id="table-tab-status-energie"></a>
### TAB_STATUS_ENERGIE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ENSTATE_GOOD |
| 1 | ENSTATE_OK |
| 2 | ENSTATE_SHORTAGE |
| 3 | ENSTATE_SEVERE_SHORTAGE |
| 15 | Signal ungültig |

<a id="table-tab-steuerung-basis-teilnetze"></a>
### TAB_STEUERUNG_BASIS_TEILNETZE

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Kommunikation |
| 1 | Kom_Parken_BN_niO |
| 2 | Kom_Parken_BN_iO |
| 3 | Kom_Standfunktionen_Kunde_nicht_im_FZG |
| 4 | reserviert |
| 5 | Kom_Wohnen |
| 6 | reserviert |
| 7 | Kom_Pruefen_Analyse_Diagnose |
| 8 | Kom_Fahrbereitschaft_herstellen |
| 9 | reserviert |
| 10 | Kom_Fahren |
| 11 | reserviert |
| 12 | Kom_Fahrbereitschaft_beenden |
| 13 | reserviert |
| 14 | Nicht verfügbar |
| 15 | Signal ungültig |

<a id="table-tab-system-state-hsr"></a>
### TAB_SYSTEM_STATE_HSR

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | INVALID |
| 1 | NM_WAIT |
| 2 | INIT |
| 3 | WAIT_FOR_RLW_SET |
| 4 | READY_FOR_DRIVE |
| 5 | DRIVE_STANDBYHOLD |
| 6 | DRIVE |
| 7 | DRIVE_ACTIVEDIAG |
| 8 | DRIVE_STANDBY |
| 9 | DRIVE_RAMPZERO |
| 10 | POSTRUN |
| 11 | OFF |
| 12 | FLASH |
| 13 | LOW_VOLT |
| 14 | ERROR |
| 0xFF | Wert ungültig |

<a id="table-tab-vm-antrieb"></a>
### TAB_VM_ANTRIEB

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Motor steht sicher |
| 1 | Motor startet |
| 2 | Motor läuft selbständig |
| 3 | Motor im Auslauf |
| 13 | Funktionsschnittstelle ist nicht verfuegbar |
| 14 | Reserviert |
| 15 | Signal unbefuellt |

<a id="table-tab-zustand-fahrzeug-1"></a>
### TAB_ZUSTAND_FAHRZEUG_1

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserviert |
| 1 | Parken BN niO |
| 2 | Parken BN iO |
| 3 | Standfunktionen Kunde nicht im FZG |
| 5 | Wohnen |
| 7 | Pruefen Analyse Diagnose |
| 8 | Fahrbereitschaft herstellen |
| 10 | Fahren |
| 12 | Fahrbereitschaft beenden |
| 14 | Nicht verfügbar |
| 15 | Signal ungültig |
