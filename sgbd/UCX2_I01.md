# UCX2_I01.prg

- Jobs: [33](#jobs)
- Tables: [46](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Universal Charging Extension |
| ORIGIN | BMW EA-440 Jochen_Tempelhoff |
| REVISION | 3.001 |
| AUTHOR | BMW TI-544 Meierhofer, BMW TI-544 Bauer, TELEMOTIVE-AG EE-23 Ri |
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
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [BF_AUSLOESER_FAILSAFE_UCXII](#table-bf-ausloeser-failsafe-ucxii) (11 × 10)
- [BF_LADEGERAET_DERATING](#table-bf-ladegeraet-derating) (7 × 10)
- [BF_LADEGERAET_FEHLERZUSTAND_UCXII](#table-bf-ladegeraet-fehlerzustand-ucxii) (4 × 10)
- [BF_LADEGERAET_URSACHE_LADEUNTERBRECHUNG](#table-bf-ladegeraet-ursache-ladeunterbrechung) (3 × 10)
- [BF_MOD_ERR](#table-bf-mod-err) (32 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [DSP_FLASHING_STATUS](#table-dsp-flashing-status) (5 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (227 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (6 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0XAF43_R](#table-res-0xaf43-r) (1 × 13)
- [RES_0XDE84_D](#table-res-0xde84-d) (11 × 10)
- [RES_0XDE85_D](#table-res-0xde85-d) (3 × 10)
- [RES_0XDE86_D](#table-res-0xde86-d) (7 × 10)
- [RES_0XDE87_D](#table-res-0xde87-d) (7 × 10)
- [RES_0XDFB0_D](#table-res-0xdfb0-d) (3 × 10)
- [RES_0XDFB1_D](#table-res-0xdfb1-d) (10 × 10)
- [RES_0XDFB4_D](#table-res-0xdfb4-d) (3 × 10)
- [RES_0XDFB6_D](#table-res-0xdfb6-d) (10 × 10)
- [RES_0XDFB7_D](#table-res-0xdfb7-d) (10 × 10)
- [RES_0XDFB8_D](#table-res-0xdfb8-d) (3 × 10)
- [RES_0XDFB9_D](#table-res-0xdfb9-d) (8 × 10)
- [RES_0XDFBA_D](#table-res-0xdfba-d) (7 × 10)
- [RES_0XDFBB_D](#table-res-0xdfbb-d) (7 × 10)
- [RES_0XDFBC_D](#table-res-0xdfbc-d) (11 × 10)
- [RES_0XDFBD_D](#table-res-0xdfbd-d) (6 × 10)
- [RES_0XF000_R](#table-res-0xf000-r) (1 × 13)
- [SG_FUNKTIONEN](#table-sg-funktionen) (18 × 16)
- [TAB_LADEGERAET_BETRIEBSART](#table-tab-ladegeraet-betriebsart) (9 × 2)
- [UCX_02_DSP_FLASHING_STATUS](#table-ucx-02-dsp-flashing-status) (5 × 2)

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

<a id="table-bf-ausloeser-failsafe-ucxii"></a>
### BF_AUSLOESER_FAILSAFE_UCXII

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUSLOESER_FAILSAFE_BIT0 | 0/1 | high | unsigned int | 0x001 | - | - | - | - | Hardware Fehler: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT1 | 0/1 | high | unsigned int | 0x002 | - | - | - | - | Unterspannung AC: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT2 | 0/1 | high | unsigned int | 0x004 | - | - | - | - | Überspannung AC: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT3 | 0/1 | high | unsigned int | 0x008 | - | - | - | - | Überstrom AC: 0 = nicht aktiv; 1  = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT4 | 0/1 | high | unsigned int | 0x010 | - | - | - | - | Unterspannung DC: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT5 | 0/1 | high | unsigned int | 0x020 | - | - | - | - | Überspannung DC: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT6 | 0/1 | high | unsigned int | 0x040 | - | - | - | - | Überstrom DC: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT7 | 0/1 | high | unsigned int | 0x080 | - | - | - | - | Temperatur: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT8 | 0/1 | high | unsigned int | 0x100 | - | - | - | - | Kommunikationsfehler: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT9 | 0/1 | high | unsigned int | 0x200 | - | - | - | - | Timeout Ladeinitialisierung: 0 = nicht aktiv; 1 = aktiv |
| STAT_AUSLOESER_FAILSAFE_BIT10 | 0/1 | high | unsigned int | 0x400 | - | - | - | - | Unterspannung Controller: 0 = nicht aktiv; 1 = aktiv |

<a id="table-bf-ladegeraet-derating"></a>
### BF_LADEGERAET_DERATING

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DERATING_BIT0 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Übertempertur: 0 = nicht aktiv; 1 = aktiv |
| STAT_DERATING_BIT1 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | Netzfrequenz zu niedrig: 0 = nicht aktiv; 1 = aktiv |
| STAT_DERATING_BIT2 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Ausfall eines Lademoduls: 0 = nicht aktiv; 1 = aktiv |
| STAT_DERATING_BIT3 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | DC Strombegrenzung: 0 = nicht aktiv; 1 = aktiv |
| STAT_DERATING_BIT4 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | Netz verfügbare Leistung kleiner Nennleistung : 0 = nicht aktiv; 1 = aktiv |
| STAT_DERATING_BIT5 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | Reserviert |
| STAT_DERATING_BIT6 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | Reserviert |

<a id="table-bf-ladegeraet-fehlerzustand-ucxii"></a>
### BF_LADEGERAET_FEHLERZUSTAND_UCXII

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FEHLERZUSTAND_BIT0 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Derating: 0 = nicht aktiv; 1 = aktiv |
| STAT_FEHLERZUSTAND_BIT1 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | Ladeunterbrechung: 0 = nicht aktiv; 1 = aktiv |
| STAT_FEHLERZUSTAND_BIT2 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Failsafe: 0 = nicht aktiv; 1 = aktiv |
| STAT_FEHLERZUSTAND_BIT3 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | Kommunikationsausfall: 0 = nicht aktiv; 1 = aktiv |

<a id="table-bf-ladegeraet-ursache-ladeunterbrechung"></a>
### BF_LADEGERAET_URSACHE_LADEUNTERBRECHUNG

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_URSACHE_LADEUNTERBRECHUNG_BIT0 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Gewalttrennung des Steckers: 0 = nicht aktiv; 1  = aktiv |
| STAT_URSACHE_LADEUNTERBRECHUNG_BIT1 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | AC Spannung fehlt oder Netzverbindung instabil: 0 = nicht aktiv; 1 = aktiv |
| STAT_URSACHE_LADEUNTERBRECHUNG_BIT2 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Stecker nicht verriegelt: 0 = nicht aktiv; 1 = aktiv |

<a id="table-bf-mod-err"></a>
### BF_MOD_ERR

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BF_DSP_ERR_HVDCV_OORL | 0/1 | high | unsigned long | 0x00000001 | - | - | - | - | PM HVDC Spannungs Sensor außerhalb unterem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_HVDCV_OORH | 0/1 | high | unsigned long | 0x00000002 | - | - | - | - | PM HVDC Spannungs Sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_HVDCI_OORH | 0/1 | high | unsigned long | 0x00000004 | - | - | - | - | PM HVDC Strom Sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_IRES_OORH | 0/1 | high | unsigned long | 0x00000008 | - | - | - | - | PM Sensor Resonanzstrom außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VBUS_OORL | 0/1 | high | unsigned long | 0x00000010 | - | - | - | - | PM Sensor Busspannung außerhalb unterem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VBUS_OORH | 0/1 | high | unsigned long | 0x00000020 | - | - | - | - | PM Sensor Busspannung außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_OVERTEMPERATURE | 0/1 | high | unsigned long | 0x00000040 | - | - | - | - | PM Temperatur sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_UNDERTEMPERATURE | 0/1 | high | unsigned long | 0x00000080 | - | - | - | - | PM Temperatursensor außerhalb unterem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_HVDCV_SHGND | 0/1 | high | unsigned long | 0x00000100 | - | - | - | - | PM HVDC Spannungs Sensor Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_HVDCI_SHGND | 0/1 | high | unsigned long | 0x00000200 | - | - | - | - | PM HVDC Strom Sensor Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_AC_I_OORH | 0/1 | high | unsigned long | 0x00000400 | - | - | - | - | PM AC Strom Sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_AC_I_SHGND | 0/1 | high | unsigned long | 0x00000800 | - | - | - | - | PM AC Strom Sensor Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LX_SHBATT | 0/1 | high | unsigned long | 0x00001000 | - | - | - | - | PM AC Lx Strom Sensor Kurzschluss nach Plus: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LX_SHGND | 0/1 | high | unsigned long | 0x00002000 | - | - | - | - | PM AC Lx Strom Sensor Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_IRES_SHBATT | 0/1 | high | unsigned long | 0x00004000 | - | - | - | - | PM Sensor Resonanzstrom Kurzschluss nach Plus: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_IRES_SHGND | 0/1 | high | unsigned long | 0x00008000 | - | - | - | - | PM Sensor Resonanzstrom Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_CAN_ALIVE | 0/1 | high | unsigned long | 0x00010000 | - | - | - | - | PM Fehler Test ALIVE: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_CAN_MSG401_TOUT | 0/1 | high | unsigned long | 0x00020000 | - | - | - | - | PM Fehler Timeout Telegramm 0x401: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_CAN_MSG300_TOUT | 0/1 | high | unsigned long | 0x00040000 | - | - | - | - | PM Fehler Timeout Telegramm 0x300: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_SPI_PROTOCOL | 0/1 | high | unsigned long | 0x00080000 | - | - | - | - | PM Fehler SPI Protokoll: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_SPI_WIPER0_MISMATCH | 0/1 | high | unsigned long | 0x00100000 | - | - | - | - | PM Fehler SPI Wiper0 Diskrepanz: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_SPI_WIPER1_MISMATCH | 0/1 | high | unsigned long | 0x00200000 | - | - | - | - | PM Fehler SPI Wiper1 Diskrepanz: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_RAM | 0/1 | high | unsigned long | 0x00400000 | - | - | - | - | PM Fehler RAM: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_WATCHDOG | 0/1 | high | unsigned long | 0x00800000 | - | - | - | - | PM Fehler Watchdog: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_STACKOVFL | 0/1 | high | unsigned long | 0x01000000 | - | - | - | - | PM Stack Überlauf: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_DATA_INTEGRITY | 0/1 | high | unsigned long | 0x02000000 | - | - | - | - | PM Data Integrität: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_CLOCK | 0/1 | high | unsigned long | 0x04000000 | - | - | - | - | PM Uhr: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_CRC_CALIBRATION | 0/1 | high | unsigned long | 0x08000000 | - | - | - | - | PM CRC Kalibrierung: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LY_SHBATT | 0/1 | high | unsigned long | 0x10000000 | - | - | - | - | PM AC Ly Spannungs Sensor Kurzschluss nach Plus: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LY_SHGND | 0/1 | high | unsigned long | 0x20000000 | - | - | - | - | PM AC Ly Spannungs Sensor Kurzschluss nach Masse: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LX_OORH | 0/1 | high | unsigned long | 0x40000000 | - | - | - | - | PM AC Lx Spannungs Sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |
| STAT_BF_DSP_ERR_VAC_LY_OORH | 0/1 | high | unsigned long | 0x80000000 | - | - | - | - | PM AC Ly Spannungs Sensor außerhalb oberem Schwellenwert: 0 = nicht aktiv; 1 = aktiv |

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

<a id="table-dsp-flashing-status"></a>
### DSP_FLASHING_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Programmierung erfolgreich abgeschlossen |
| 0x01 | Programmierung noch nicht abgeschlossen |
| 0x02 | Programmierung mit Fehler abgeschlossen |
| 0x03 | Programmierung nicht möglich |
| 0xFF | Wert ungültig |

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

Dimensions: 227 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x021500 | Energiesparmode aktiv | 0 |
| 0x02FF15 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x031806 | AC-Laden - Modul 2 - Kommunikationsfehler - Timeout | 0 |
| 0x031807 | AC-Laden - Modul 2 - Digitaler Signalprozesser - Interner Fehler | 0 |
| 0x031808 | AC-Laden - AC-Spannungssensor 2 - Unterer Schwellenwert unterschritten | 0 |
| 0x031809 | AC-Laden - AC-Spannungssensor 2 - Plausibilitätsfehler | 0 |
| 0x03180B | AC-Laden - AC-Spannungssensor 2 - Oberer Schwellenwert überschritten | 0 |
| 0x03180C | AC-Laden - AC-Spannungssensor 2 - Kurzschluss nach Plus | 0 |
| 0x03180D | AC-Laden - AC-Spannungssensor 2 - Kurzschluss nach Masse | 0 |
| 0x03180E | AC Charger Module 1 - Internal Memory - Plausibility check | 0 |
| 0x03180F | AC-Laden - Modul 1 - PFC - Kommunikationsfehler | 0 |
| 0x031810 | AC-Laden - AC-Spannungssensor 3 - Unterer Schwellenwert unterschritten | 0 |
| 0x031813 | AC-Laden - AC-Spannungssensor 3 - Oberer Schwellenwert überschritten | 0 |
| 0x031814 | AC-Laden - AC-Spannungssensor 3 - Kurzschluss nach Plus | 0 |
| 0x031815 | AC-Laden - AC-Spannungssensor 3 - Kurzschluss nach Masse | 0 |
| 0x031816 | AC-Laden - Modul 2 - PFC - Kommunikationsfehler | 0 |
| 0x031818 | AC-Laden - AC-Spannungssensor 4 - Unterer Schwellenwert unterschritten | 0 |
| 0x031819 | AC-Laden - AC-Spannungssensor 4 - Plausibilitätsfehler 2 | 0 |
| 0x03181B | AC-Laden - AC-Spannungssensor 4 - Oberer Schwellenwert überschritten | 0 |
| 0x03181C | AC-Laden - AC-Spannungssensor 4 - Kurzschluss nach Plus | 0 |
| 0x03181D | AC-Laden - AC-Spannungssensor 4 - Kurzschluss nach Masse | 0 |
| 0x031828 | AC-Laden - DC-Spannungssensor 2 - Unterer Schwellenwert unterschritten | 0 |
| 0x031829 | AC-Laden - DC-Spannungssensor 2 - Plausibilitätsfehler 2 | 0 |
| 0x03182A | AC-Laden - DC-Spannungssensor 2 - Plausibilitätsfehler | 0 |
| 0x03182B | AC-Laden - DC-Spannungssensor 2 - Oberer Schwellenwert überschritten | 0 |
| 0x03182C | AC-Laden - DC-Spannungssensor 2 - Kurzschluss nach Plus | 0 |
| 0x03182D | AC-Laden - DC-Spannungssensor 2 - Kurzschluss nach Masse | 0 |
| 0x03182F | AC-Laden - DC-Spannungssensor 2 - Kalibrierung fehlerhaft | 0 |
| 0x031838 | AC-Laden - PFC-Spannungssensor 2 - Unterer Schwellenwert unterschritten | 0 |
| 0x031839 | AC-Laden - PFC-Spannungssensor 2 - Plausibilitätsfehler | 0 |
| 0x03183B | AC-Laden - PFC-Spannungssensor 2 - Oberer Schwellenwert überschritten | 0 |
| 0x03183C | AC-Laden - PFC-Spannungssensor 2 - Kurzschluss nach Plus | 0 |
| 0x03183D | AC-Laden - PFC-Spannungssensor 2 - Kurzschluss nach Masse | 0 |
| 0x03184E | AC-Laden - AC-Stromsensor 2 - Plausibilitätsfehler 2 | 0 |
| 0x03184F | AC-Laden - AC-Stromsensor 2 - Plausibilitätsfehler | 0 |
| 0x031850 | AC-Laden - AC-Stromsensor 2 - Oberer Schwellenwert überschritten | 0 |
| 0x031851 | AC-Laden - AC-Stromsensor 2 - Kurzschluss nach Plus | 0 |
| 0x031852 | AC-Laden - AC-Stromsensor 2 - Kurzschluss nach Masse | 0 |
| 0x03185E | AC-Laden - DC-Stromsensor 2 - Plausibilitätsfehler 2 | 0 |
| 0x03185F | AC-Laden - DC-Stromsensor 2 - Plausibilitätsfehler | 0 |
| 0x031860 | AC-Laden - DC-Stromsensor 2 - Oberer Schwellenwert überschritten | 0 |
| 0x031861 | AC-Laden - DC-Stromsensor 2 - Kurzschluss nach Plus | 0 |
| 0x031862 | AC-Laden - DC-Stromsensor 2 - Kurzschluss nach Masse | 0 |
| 0x031863 | AC-Laden - Modul 2 - Kein Ausgangsstrom | 0 |
| 0x03187D | Ladekoordinator - Schaltmatrix - Spannungsversorgung | 0 |
| 0x031881 | LLC Resonant converter Module 1 - Temperature sensor (Transformer temperature sensor) - Cold start check | 0 |
| 0x03188A | LLC Resonant converter Module 1 - Temperature sensor (resonant inductor temperature sensor) - Cold start check | 0 |
| 0x03188B | AC-Laden - Temperatursensor 5 - Kurzschluss nach Masse | 0 |
| 0x03188C | AC-Laden - Temperatursensor 5 - Kurzschluss nach Plus | 0 |
| 0x03188D | AC-Laden - Temperatursensor 5 - Oberer Schwellenwert überschritten | 0 |
| 0x03188E | AC-Laden - Temperatursensor 5 - Plausiblitätsfehler | 0 |
| 0x03188F | AC-Laden - Temperatursensor 5 - Unterer Schwellenwert unterschritten | 0 |
| 0x031894 | AC-Laden - Temperatursensor 6 - Kurzschluss nach Masse | 0 |
| 0x031895 | AC-Laden - Temperatursensor 6 - Kurzschluss nach Plus | 0 |
| 0x031896 | AC-Laden - Temperatursensor 6 - Oberer Schwellenwert überschritten | 0 |
| 0x031897 | AC-Laden - Temperatursensor 6 - Plausiblitätsfehler | 0 |
| 0x031898 | AC-Laden - Temperatursensor 6 - Unterer Schwellenwert unterschritten | 0 |
| 0x03189A | LLC Resonant converter Module 2 - Temperature sensor (Transformer temperature sensor) - Cold start check | 0 |
| 0x03189C | PFC Converter Module 2 - Temperature Sensor (PFC temperature sensor) - Cold start check | 0 |
| 0x03189D | AC-Laden - Temperatursensor 7 - Kurzschluss nach Masse | 0 |
| 0x03189E | AC-Laden - Temperatursensor 7 - Kurzschluss nach Plus | 0 |
| 0x03189F | AC-Laden - Temperatursensor 7 - Oberer Schwellenwert überschritten | 0 |
| 0x0318A0 | AC-Laden - Temperatursensor 7 - Plausiblitätsfehler | 0 |
| 0x0318A1 | AC-Laden - Temperatursensor 7 - Unterer Schwellenwert unterschritten | 0 |
| 0x0318A4 | AC-Laden - Temperatursensor 8 - Unterer Schwellenwert unterschritten | 0 |
| 0x0318A5 | AC-Laden - Temperatursensor 8 - Plausiblitätsfehler | 0 |
| 0x0318A6 | AC-Laden - Temperatursensor 8 - Oberer Schwellenwert überschritten | 0 |
| 0x0318A7 | AC-Laden - Temperatursensor 8 - Kurzschluss nach Plus | 0 |
| 0x0318A8 | AC-Laden - Temperatursensor 8 - Kurzschluss nach Masse | 0 |
| 0x0318AD | AC-Laden - Temperatursensor 9 - Unterer Schwellenwert unterschritten | 0 |
| 0x0318AE | AC-Laden - Temperatursensor 9 - Plausiblitätsfehler | 0 |
| 0x0318AF | AC-Laden - Temperatursensor 9 - Oberer Schwellenwert überschritten | 0 |
| 0x0318B0 | AC-Laden - Temperatursensor 9 - Kurzschluss nach Plus | 0 |
| 0x0318B1 | AC-Laden - Temperatursensor 9 - Kurzschluss nach Masse | 0 |
| 0x0318B2 | LLC Resonant converter Module 2 - Temperature sensor (resonant inductor temperature sensor) - Cold start check | 0 |
| 0x0318B5 | AC-Laden - Modul 2 - Ausgangsleistung unplausibel | 0 |
| 0x0318B6 | AC-Laden - Modul 2 - Digitaler Signalprozessor - Fehler der Uhr | 0 |
| 0x0318B7 | AC-Laden - Modul 2 - Crash-Sensor unplausibel | 0 |
| 0x0318B8 | AC-Laden - Schaltmatrix - Relaiskleber 1 - geschlossen | 0 |
| 0x0318B9 | AC-Laden - Schaltmatrix - Relaiskleber 2 - geschlossen | 0 |
| 0x0318BA | AC-Laden - Schaltmatrix - Überspannungsschutz 1 | 0 |
| 0x0318BB | AC-Laden - Schaltmatrix - Überspannungsschutz 2 | 0 |
| 0x0318BC | AC-Laden - Schaltmatrix - Überspannungsschutz 3 | 0 |
| 0x0318BD | AC-Laden - Schaltmatrix - Überspannungsschutz 4 | 0 |
| 0x0318BE | AC-Laden - Schaltmatrix - Relaiskleber 3 - geschlossen | 0 |
| 0x0318C0 | AC-Laden - DC-Stromsensor 3 - Kurzschluss nach Masse | 0 |
| 0x0318C1 | AC-Laden - DC-Stromsensor 3 - Kurzschluss nach Plus | 0 |
| 0x0318C2 | AC-Laden - DC-Stromsensor 3 - Oberer Schwellenwert überschritten | 0 |
| 0x0318C8 | Internal Charge Coordinator - Temperature sensor (Board temperature sensor) - Cold start check | 0 |
| 0x0318C9 | Internal Charge Coordinator - Temperature sensor - Short Circuit to Battery (NTC) | 0 |
| 0x0318CA | AC-Laden - Temperatursensor 10 - Unterer Schwellenwert unterschritten | 0 |
| 0x0318CB | AC-Laden - Temperatursensor 10 - Plausiblitätsfehler | 0 |
| 0x0318CC | Internal Charge Coordinator - Temperature sensor (Board temperature sensor) - Short Circuit to Ground  (NTC) | 0 |
| 0x0318CD | AC-Laden - Temperatursensor 10 - Oberer Schwellenwert überschritten | 0 |
| 0x0318D0 | AC-Laden - Schaltmatrix - Relaiskleber 1 - offen | 0 |
| 0x0318D1 | AC-Laden - Schaltmatrix - Relaiskleber 2 - offen | 0 |
| 0x0318D2 | AC-Laden - Schaltmatrix - Relaiskleber 3 - offen | 0 |
| 0x0318D5 | AC-Laden - Modul 2 - Kommunikationsfehler - Ungültig | 0 |
| 0x0318D6 | AC-Laden - Modul 1 - Kommunikationsfehler - Timeout | 0 |
| 0x0318D7 | AC-Laden - Modul 1 - Kommunikationsfehler - Ungültig | 0 |
| 0x0318D8 | AC-Laden - AC-Spannungssensor 2 - Unterer Schwellenwert unterschritten 2 | 0 |
| 0x0318D9 | AC-Laden - Modul 2 - Kommunikationsfehler - Bus off | 0 |
| 0x21E605 | Ladeelektronik: Überspannung an 12V Spannungsversorgung | 0 |
| 0x21E606 | Ladeelektronik: Unterspannung an 12V Spannungsversorgung | 0 |
| 0x21E60B | Ladeelektronik: Software-Fehler | 0 |
| 0x21E60C | Charger internal bus off  Module 1 | 0 |
| 0x21E60D | Ladeelektronik: Unterspannung am AC-Anschluss | 0 |
| 0x21E60E | Ladeelektronik: Überspannung am AC-Anschluss | 0 |
| 0x21E60F | Ladeelektronik: Unterspannung am DC-Anschluss | 0 |
| 0x21E610 | Ladeelektronik: Überspannung am DC-Anschluss | 0 |
| 0x21E611 | Ladeelektronik: DC Überstrom | 0 |
| 0x21E612 | Ladeunterbrechung - Temperaturunterschreitung | 1 |
| 0x21E613 | Ladeunterbrechung - Temperaturüberschreitung | 1 |
| 0x21E614 | Ladeelektronik: Zustand Service Disconnect zu KL30C unplausibel | 0 |
| 0x21E615 | Ladeelektronik: Wirkungsgrad außerhalb Bereich (Low) | 0 |
| 0x21E616 | Ladeelektronik: Wirkungsgrad außerhalb Bereich (High) | 0 |
| 0x21E617 | Coolant System - Charge Coordinator - Lower deviation temperature | 0 |
| 0x21E618 | Coolant System - Charge Coordinator - Temperature exceed | 0 |
| 0x21E61C | Ladeelektronik: AC Überstrom | 0 |
| 0x21E622 | Ladeelektronik, HV DC Spannungssensor: Kurzschluss nach Masse | 0 |
| 0x21E623 | Ladeelektronik, HV DC Spannungssensor: Kurzschluss nach Plus | 0 |
| 0x21E624 | Ladeelektronik, HV DC Spannung: Messwert unplausibel und zu niedrig | 0 |
| 0x21E625 | Ladeelektronik, HV DC Spannung: Messwert unplausibel und zu hoch | 0 |
| 0x21E626 | Ladeelektronik, HV AC Spannungssensor: Kurzschluss nach Masse | 0 |
| 0x21E627 | Ladeelektronik, HV AC Spannungssensor: Kurzschluss nach Plus | 0 |
| 0x21E628 | Ladeelektronik: HV AC Spannung unplausibel zu niedrig | 0 |
| 0x21E629 | Ladeelektronik: HV AC Spannung unplausibel | 0 |
| 0x21E62A | Ladeelektronik, Spannungssensor KL30C: Kurzschluß nach Masse | 0 |
| 0x21E62B | Ladeelektronik, Spannungssensor KL30C: Kurzschluss nach Plus | 0 |
| 0x21E62C | Ladeelektronik: Unterspannung KL30C | 0 |
| 0x21E62D | Ladeelektronik: Überspannung KL30C | 0 |
| 0x21E62E | Lade-Elektronik: Ladebereitschaft Leitung, Kurzschluss nach Masse | 0 |
| 0x21E62F | Lade-Elektronik: Ladebereitschaft Leitung, Kurzschluss nach Plus | 0 |
| 0x21E630 | Lade-Elektronik: Ladebereitschaft, Signal außerhalb Sollbereich (unten) | 1 |
| 0x21E631 | Lade-Elektronik: Ladebereitschaft, Signal außerhalb Sollbereich (oben) | 1 |
| 0x21E632 | Lade-Elektronik: Ladebereitschaft, Signal unplausibel | 0 |
| 0x21E633 | Ladeelektronik, Sensor Versorgungsspannung: Kurzschluss nach Masse | 0 |
| 0x21E634 | Ladeelektronik, Sensor Versorgungsspannung: Kurzschluss nach Plus | 0 |
| 0x21E635 | Ladeelektronik, Sensor Versorgungsspannung: Unplausibel im Vergleich zu KL30C | 0 |
| 0x21E636 | Lade-Elektronik: Hochvolt DC Spannungssensor, Kalibrierung, Checksumme falsch | 1 |
| 0x21E637 | Lade-Elektronik: Temperatursensor 1, Kurzschluss nach Masse | 0 |
| 0x21E638 | Lade-Elektronik: Temperatursensor 1, Kurzschluss nach Plus | 0 |
| 0x21E639 | Lade-Elektronik: Temperatursensor 1, Wert außerhalb Sollbreich (oben) | 0 |
| 0x21E63A | Lade-Elektronik: Temperatursensor 1, Wert außerhalb Sollbreich (unten) | 0 |
| 0x21E63B | Lade-Elektronik: Temperatursensor 1, Wert unplausibel | 0 |
| 0x21E63C | Lade-Elektronik: Temperatursensor 2, Kurzschluss nach Masse | 0 |
| 0x21E63D | Lade-Elektronik: Temperatursensor 2, Kurzschluss nach Plus | 0 |
| 0x21E63E | Lade-Elektronik: Temperatursensor 2, Wert außerhalb Sollbreich (oben) | 0 |
| 0x21E63F | Lade-Elektronik: Temperatursensor 2, Wert außerhalb Sollbreich (unten) | 0 |
| 0x21E641 | Lade-Elektronik: Temperatursensor 3, Kurzschluss nach Masse | 0 |
| 0x21E642 | Lade-Elektronik: Temperatursensor 3, Kurzschluss nach Plus | 0 |
| 0x21E643 | Lade-Elektronik: Temperatursensor 3, Wert außerhalb Sollbreich (oben) | 0 |
| 0x21E644 | Lade-Elektronik: Temperatursensor 3, Wert außerhalb Sollbreich (unten) | 0 |
| 0x21E645 | Lade-Elektronik: Temperatursensor 3, Wert unplausibel | 0 |
| 0x21E646 | Ladeelektronik, HV AC Stromsensor: Kurzschluss nach Masse | 0 |
| 0x21E647 | Ladeelektronik, HV AC Stromsensor: Kurzschluss nach Plus | 0 |
| 0x21E648 | Ladeelektronik, AC Eingang: Strom unplausibel (Low) | 0 |
| 0x21E649 | Ladeelektronik, AC Eingang: Strom unplausibel (High) | 0 |
| 0x21E64A | Lade-Elektronik: digitaler Signalprozessor, Fehler der Uhr | 0 |
| 0x21E64B | Lade-Elektronik: digitaler Signalprozessor, Crash-Sensor unplausibel | 0 |
| 0x21E64C | Ladeelektronik, HV DC Stromsensor: Kurzschluss nach Masse | 0 |
| 0x21E64D | Ladeelektronik, HV DC Stromsensor: Kurzschluss nach Plus | 0 |
| 0x21E64E | Ladeelektronik: HV DC Stromsensor unplausibel und zu niedrig | 0 |
| 0x21E64F | Ladeelektronik: HV DC Stromsensor unplausibel und zu hoch | 0 |
| 0x21E650 | Lade-Elektronik: PFC Spannunssensor, Kurzschluss nach Masse | 0 |
| 0x21E651 | Lade-Elektronik: PFC Spannunssensor, Kurzschluss nach Plus | 0 |
| 0x21E652 | Lade-Elektronik: PFC Spannung, Wert außerhalb Sollbereich (unten) bei aktivem Laden | 0 |
| 0x21E653 | Lade-Elektronik: PFC Spannung, Wert außerhalb Sollbereich (oben) bei aktivem Laden | 0 |
| 0x21E654 | Lade-Elektronik: PFC Spannung, Wert außerhalb Sollbereich (oben) bei Vorladen | 0 |
| 0x21E655 | Ladeelektronik: HV DC Spannung unplausibel | 0 |
| 0x21E656 | Lade-Elektronik: Ausgangleistung unplausibel | 0 |
| 0x21E659 | Lade-Elektronik: Temperatursensor 3, Start unplausibel | 0 |
| 0x21E65A | Lade-Elektronik: Temperatursensor 4, Wert außerhalb Sollbreich (oben) | 0 |
| 0x21E65B | Lade-Elektronik: Temperatursensor 4, Wert außerhalb Sollbreich (unten) | 0 |
| 0x21E687 | Klemme 30C - Crash erkannt | 1 |
| 0x21E68C | Ladeelektronik: Timeout Zustandswechsel Precharge zu Charge | 1 |
| 0x21E68F | Ladeelektronik: Kein HV DC Strom trotz Ladeanforderung | 0 |
| 0x21E690 | Lade-Elektronik: Temperatursensor 4, Kurzschluss nach Masse | 0 |
| 0x21E691 | Lade-Elektronik: Temperatursensor 4, Kurzschluss nach Plus | 0 |
| 0x21E692 | Lade-Elektronik: Temperatursensor 4, Wert unplausibel | 0 |
| 0x21E694 | Internal DC Link Circuit Module 2 - Voltage sensor (Link Circuit Voltage) - Out of Range Low - immediate failure | 0 |
| 0x21E695 | Internal DC Link Circuit Module 2 - Voltage sensor (Link Circuit Voltage) - Out of Range High - immediate failure | 0 |
| 0x21E69C | Lade-Elektronik: Resonanzspule, Strom außerhalb Sollbereich | 0 |
| 0x21E69D | Lade-Elektronik: Resonanzspule, Stromsensor, Kurzschluss nach Masse | 0 |
| 0x21E69E | Lade-Elektronik: Resonanzspule, Stromsensor, Kurzschluss nach Plus | 0 |
| 0x21E6E2 | LLC Resonant converter Module 2 - HV-DC current sensor - FuSi Overcurrent | 0 |
| 0x21E6E3 | LLC Resonant converter Module 2 - HV-DC current sensor - Overcurrent immediate | 0 |
| 0x21E6E4 | LLC Resonant converter Module 2 - HV-DC voltage sensor - Out of Range High - immediate failure | 0 |
| 0x21E6E7 | LLC Resonant converter Module 2 - HV-DC voltage sensor - Out of Range Low - immediate failure | 0 |
| 0x21E6EF | PFC Module 2 - HVAC Current Out of Range | 0 |
| 0x21E6F0 | Lade-Elektronik: Überspannung am DC-Anschluss | 1 |
| 0x21E6F1 | Lade-Elektronik: DC Überstrom | 0 |
| 0x21E6F2 | Lade-Elektronik: PFC Spannung, Wert außerhalb Sollbereich (unten) bei aktivem Laden | 0 |
| 0x21E6F3 | Lade-Elektronik: PFC Spannung, Wert außerhalb Sollbereich (oben) bei aktivem Laden | 0 |
| 0x21E6F4 | Lade-Elektronik: Unterspannung am AC-Anschluss | 1 |
| 0x21E6F5 | Lade-Elektronik: Überspannung am AC-Anschluss | 1 |
| 0x21E6F6 | Lade-Elektronik: AC Überstrom | 0 |
| 0x21E6F7 | Lade-Elektronik: Unterspannung am DC-Anschluss | 1 |
| 0x21E6F9 | Ladeelektronik: Ladeunterbrechung während Laden aktiv | 1 |
| 0x21E6FC | Lade-Elektronik: DC Überstrom 1 | 0 |
| 0x21E6FD | PFC Converter Module 2 - Out of Range Low - immediate failure | 0 |
| 0xCE4486 | A-CAN Control Module Bus OFF | 0 |
| 0xCE4BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xCE5400 | Botschaft (Vorgabe Komfort Ladeelektronik, 0x153) fehlt, Empfänger UCX, Sender AE | 1 |
| 0xCE5401 | Botschaft (Klemmen, 0x12F) fehlt, Empfänger UCX, Sender BDC | 1 |
| 0xCE5402 | Botschaft (Status Hochvoltspeicher 2, 0x112) fehlt | 1 |
| 0xCE5403 | Botschaft (Begrenzung Ladung Entladung Hochvoltspeicher, 0x2F5) fehlt, Empfänger UCX, Sender SME | 1 |
| 0xCE5404 | Botschaft (Steuerung Teilnetze, 0x19E) fehlt, Empfänger UCX, Sender eDME | 1 |
| 0xCE5406 | Botschaft (Daten Hochvoltspeicher, 0x431) fehlt, Empfänger UCX, Sender SME | 1 |
| 0xCE540A | Signal (U_MAX_CHG_HVSTO) ungültig, Sender SME | 1 |
| 0xCE540E | Botschaft (AVL_U_HVSTO) ungültig | 1 |
| 0xCE5410 | Signal (TAR_OPMO_CF_CHGE) ungültig, Sender AE | 1 |
| 0xCE5411 | Botschaft (TAR_OPMO_CF_CHGE) undefiniert | 1 |
| 0xCE5412 | Botschaft (SPEC_I_MAX_DC_CF_CHGE) ungültig | 1 |
| 0xCE5414 | Botschaft (TAR_PWR_CF_CHGNG) ungültig | 1 |
| 0xCE5416 | Signal (ST_SER_DSCO_PLG) ungültig, Sender SME | 1 |
| 0xCE5417 | Botschaft (ST_SER_DSCO_PLG) undeifniert | 1 |
| 0xCE5418 | Signal (CTR_FKTN_PRTNT_DRV) ungültig, Sender eDME | 1 |
| 0xCE5419 | Botschaft (CTR_FKTN_PRTNT_DRV) undefiniert | 1 |
| 0xCE541A | Botschaft (AVL_U_LINK) ungültig | 1 |
| 0xCE541B | Botschaft (AVL_U_LINK) undefiniert | 1 |
| 0xCE541C | Botschaft (SPEC_I_MAX_ALTC_CF_CHGE) ungültig | 1 |
| 0xCE541D | Botschaft (SPEC_U_MAX_CHG_CHGE) ungültig | 1 |
| 0xCE541F | Communication - A-CAN - Invalid A-CAN signal | 1 |
| 0xCE5420 | Botschaft (TAR_CHG_MOD_CF_CHGE) undefiniert | 1 |
| 0xCE5421 | Botschaft (TAR_CHG_MOD_CF_CHGE) ungültig | 1 |
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

Dimensions: 6 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x001001 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 1 |
| 0x21E696 | DSPs reflash error | 0 |
| 0x21E6EB | Klemme 30 emergency low | 1 |
| 0xC90401 | Puffer für ausgehende Fehlermeldungen ist voll | 1 |
| 0xC90402 | Fehler konnte nach maximaler Anzahl von Versuchen nicht gesendet werden | 1 |
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

<a id="table-res-0xaf43-r"></a>
### RES_0XAF43_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DSP_FLASHING | + | - | + | 0-n | high | unsigned char | - | DSP_FLASHING_STATUS | - | - | - | Status der DSP-Programmierung. |

<a id="table-res-0xde84-d"></a>
### RES_0XDE84_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NETZFREQUENZ_PHASE_1_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 1 |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_DERATING | - | - | - | Grund für Derating |
| STAT_LEISTUNG_DERATING_WERT | W | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | Derating Leistung |
| STAT_DERATING_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Derating |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_FEHLERZUSTAND_UCXII | - | - | - | Ladegerät Fehlerzustände  |
| - | Bit | high | BITFIELD | - | BF_AUSLOESER_FAILSAFE_UCXII | - | - | - | Auslöser Failsafe |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_URSACHE_LADEUNTERBRECHUNG | - | - | - | Ursache für Ladeunterbrechung |
| STAT_BETRIEBSART_NR | 0-n | high | unsigned char | - | TAB_LADEGERAET_BETRIEBSART | - | - | - | Betriebsart |
| STAT_NETZFREQUENZ_PHASE_2_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 2 |
| STAT_NETZFREQUENZ_PHASE_3_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 3 |
| - | Bit | high | BITFIELD | - | BF_MOD_ERR | - | - | - | Fehlerzustände Lademodul |

<a id="table-res-0xde85-d"></a>
### RES_0XDE85_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WIRKUNGSGRAD_LADEZYKLUS_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wirkungsgrad Ladezyklus |
| STAT_WIRKUNGSGRAD_DC_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wirkungsgrad DC |
| STAT_LADEGERAET_DC_HV_LEISTUNG_WERT | W | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abgegebende Momentanleistung in den Zwischenkreis |

<a id="table-res-0xde86-d"></a>
### RES_0XDE86_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_RMS_AC_PHASE_1_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase1) |
| STAT_SPANNUNG_DC_HV_OBERGRENZE_WERT | V | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | HV DC Spannungsobergrenze |
| STAT_SPANNUNG_DC_HV_WERT | V | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | HV DC Spannung |
| STAT_SPANNUNG_KL30_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | KL30 Spannung |
| STAT_SPANNUNG_KL30C_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | KL30C Spannung |
| STAT_SPANNUNG_RMS_AC_PHASE_2_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase 2) |
| STAT_SPANNUNG_RMS_AC_PHASE_3_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase 3) |

<a id="table-res-0xde87-d"></a>
### RES_0XDE87_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STROM_AC_PHASE_1_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 1 |
| STAT_STROM_AC_MAX_GESPEICHERT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximal gespeicherter AC Strom |
| STAT_STROM_HV_DC_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | -204.7 | HV DC Strom |
| STAT_STROM_HV_DC_MAX_LIMIT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximal erlaubter HV DC Strom |
| STAT_STROM_HV_DC_MAX_GESPEICHERT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | -204.7 | Maximal gespeicherter DC Strom |
| STAT_STROM_AC_PHASE_2_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 2 |
| STAT_STROM_AC_PHASE_3_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 3 |

<a id="table-res-0xdfb0-d"></a>
### RES_0XDFB0_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MINUTEN_LADEZYKLUS_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Minuten |
| STAT_SEKUNDEN_LADEZYKLUS_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Sekunden |
| STAT_LADEZYKLEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladezyklen |

<a id="table-res-0xdfb1-d"></a>
### RES_0XDFB1_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NTC1_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 1) |
| STAT_NTC2_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 2) |
| STAT_NTC3_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 3) |
| STAT_NTC4_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 4) |
| STAT_NTC5_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 5) |
| STAT_NTC6_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 6) |
| STAT_NTC7_TEMPERAUTR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 7) |
| STAT_NTC8_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Tempeartur (Temperatursensor 8) |
| STAT_NTC9_TEMPEARTUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 9) |
| STAT_NTC10_TEMPEARTUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -75.0 | interne Temperatur (Temperatursensor 10) |

<a id="table-res-0xdfb4-d"></a>
### RES_0XDFB4_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WIRKUNGSGRAD_LADEZYKLUS_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wirkungsgrad Ladezyklus |
| STAT_WIRKUNGSGRAD_DC_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wirkungsgrad DC |
| STAT_LADEGERAET_DC_HV_LEISTUNG_WERT | W | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Abgegebende Momentanleistung in den Zwischenkreis |

<a id="table-res-0xdfb6-d"></a>
### RES_0XDFB6_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur unter 0°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 0°C und 45°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 46°C und 60°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden im Temperaturbereich zwischen 61°C und 70°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 71°C und 85°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur über 85°C |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung unter 1000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung zwischen 1001W und 2000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung zwischen 2001W und 3000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung über 3000W |

<a id="table-res-0xdfb7-d"></a>
### RES_0XDFB7_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur unter 0°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 0°C und 45°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 46°C und 60°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden im Temperaturbereich zwischen 61°C und 70°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur zwischen 71°C und 85°C |
| STAT_SEKUNDEN_TEMPERATUR_BEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Temperatur über 85°C |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung unter 1000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung zwischen 1001W und 2000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung zwischen 2001W und 3000W |
| STAT_SEKUNDEN_LEISTUNG_BEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sekunden bei Leistung über 3000W |

<a id="table-res-0xdfb8-d"></a>
### RES_0XDFB8_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MINUTEN_LADEZYKLUS_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Minuten |
| STAT_SEKUNDEN_LADEZYKLUS_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Sekunden |
| STAT_LADEZYKLEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladezyklen |

<a id="table-res-0xdfb9-d"></a>
### RES_0XDFB9_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER1_SCHALTZYKLEN_ANZAHL_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Schaltzyklen für Schalter 1 (mehrphasiges Laden: Phase 1) |
| STAT_SCHALTER2_SCHALTZYKLEN_ANZAHL_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Schaltzyklen für Schalter 2 (mehrphasiges Laden: Phase 2) |
| STAT_SCHALTER3_SCHALTZYKLEN_ANZAHL_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Schaltzyklen für Schalter 3 (mehrphasiges Laden: Phase 3) |
| STAT_SCHALTER4_SCHALTZYKLEN_ANZAHL_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl von Schaltzyklen für Schalter 4 (mehrphasiges Laden: Umschaltung) |
| STAT_SCHALTER1 | 0/1 | high | unsigned char | - | - | - | - | - | Zustand vom Schalter 1 (0= offen, 1=geschlossen) |
| STAT_SCHALTER2 | 0/1 | high | unsigned char | - | - | - | - | - | Zustand vom Schalter 2 (0= offen, 1=geschlossen) |
| STAT_SCHALTER3 | 0/1 | high | unsigned char | - | - | - | - | - | Zustand vom Schalter 3 (0= offen, 1=geschlossen) |
| STAT_SCHALTER4 | 0/1 | high | unsigned char | - | - | - | - | - | Zustand vom Schalter 4 (0= Ladegerät 1, 1=Ladegerät 2) |

<a id="table-res-0xdfba-d"></a>
### RES_0XDFBA_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_RMS_AC_PHASE_1_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase1) |
| STAT_SPANNUNG_DC_HV_OBERGRENZE_WERT | V | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | HV DC Spannungsobergrenze |
| STAT_SPANNUNG_DC_HV_WERT | V | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | HV DC Spannung |
| STAT_SPANNUNG_KL30_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | KL30 Spannung |
| STAT_SPANNUNG_KL30C_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | KL30C Spannung |
| STAT_SPANNUNG_RMS_AC_PHASE_2_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase 2) |
| STAT_SPANNUNG_RMS_AC_PHASE_3_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Effektivwerte der AC Leiterspannungen (Phase 3) |

<a id="table-res-0xdfbb-d"></a>
### RES_0XDFBB_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STROM_AC_PHASE_1_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 1 |
| STAT_STROM_AC_MAX_GESPEICHERT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximal gespeicherter AC Strom |
| STAT_STROM_HV_DC_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | -204.7 | HV DC Strom |
| STAT_STROM_HV_DC_MAX_LIMIT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximal erlaubter HV DC Strom |
| STAT_STROM_HV_DC_MAX_GESPEICHERT_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | -204.7 | Maximal gespeicherter DC Strom |
| STAT_STROM_AC_PHASE_2_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 2 |
| STAT_STROM_AC_PHASE_3_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | AC Strom Phase 3 |

<a id="table-res-0xdfbc-d"></a>
### RES_0XDFBC_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NETZFREQUENZ_PHASE_1_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 1 |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_DERATING | - | - | - | Grund für Derating |
| STAT_LEISTUNG_DERATING_WERT | W | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | Derating Leistung |
| STAT_DERATING_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Derating |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_FEHLERZUSTAND_UCXII | - | - | - | Ladegerät Fehlerzustände |
| - | Bit | high | BITFIELD | - | BF_AUSLOESER_FAILSAFE_UCXII | - | - | - | Auslöser Failsafe |
| - | Bit | high | BITFIELD | - | BF_LADEGERAET_URSACHE_LADEUNTERBRECHUNG | - | - | - | Ursache für Ladeunterbrechung |
| STAT_BETRIEBSART_NR | 0-n | high | unsigned char | - | TAB_LADEGERAET_BETRIEBSART | - | - | - | Betriebsart |
| STAT_NETZFREQUENZ_PHASE_2_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 2 |
| STAT_NETZFREQUENZ_PHASE_3_WERT | Hz | high | unsigned char | - | - | 1.0 | 4.0 | 0.0 | Aktuelle Netzfrequenz Phase 3 |
| - | Bit | high | BITFIELD | - | BF_MOD_ERR | - | - | - | Fehlerzustände Lademodul |

<a id="table-res-0xdfbd-d"></a>
### RES_0XDFBD_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MINUTEN_LADEZYKLUS_1PH_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Minuten für einphasiges Laden |
| STAT_SEKUNDEN_LADEZYKLUS_1PH_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Sekunden für einphasiges Laden |
| STAT_LADEZYKLUS_1PH_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Ladezyklus einphasiges Laden |
| STAT_MINUTEN_LADEZYKLUS_3PH_WERT | min | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Minuten für mehrphasiges Laden |
| STAT_SEKUNDEN_LADEZYKLUS_3PH_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Ladezeit in Sekunden für mehrphasiges Laden |
| STAT_LADEZYKLUS_3PH_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Ladezyklus mehrphasiges Laden |

<a id="table-res-0xf000-r"></a>
### RES_0XF000_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DSP_FLASHING | + | - | + | 0-n | high | unsigned char | - | UCX_02_DSP_FLASHING_STATUS | - | - | - | Status der DSP-Programmierung. |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 18 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FLASH_DSPS | 0xAF43 | - | Programmierung von DSP | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAF43_R |
| BETRIEBSZUSTAND_LADEGERAET | 0xDE84 | - | Betriebsarten Ladegerät | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE84_D |
| LADEGERAET_LEISTUNG | 0xDE85 | - | Leistungswerte Zwischenkreis des Ladegeräts | - | xle_P_IntLe_hv_ist | - | - | - | - | - | - | - | 22 | - | RES_0xDE85_D |
| LADEGERAET_SPANNUNG | 0xDE86 | - | AC und DC Spannungen Ladegerät | - | V_U_SleAc | - | - | - | - | - | - | - | 22 | - | RES_0xDE86_D |
| LADEGERAET_STROM | 0xDE87 | - | AC und DC Ströme Ladegerät | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE87_D |
| AC_PHASENANZAHL | 0xDF25 | STAT_AC_PHASENANZAHL_WERT | Status AC-Phasenanzahl | - | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| LADEGERAET_LADEDAUER | 0xDFB0 | - | Information zur Ladedauer | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB0_D |
| LADEGERAET_TEMPERATUREN | 0xDFB1 | - | Auslesen Temperaturen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB1_D |
| LADEGERAET_LEISTUNG2 | 0xDFB4 | - | Leistungswerte für zweites Ladegerät (mehrphasiges Laden) | - | xle_P_IntLe_hv_ist | - | - | - | - | - | - | - | 22 | - | RES_0xDFB4_D |
| LADEGERAET_LADE_HISTOGRAMM | 0xDFB6 | - | Ladehistogramm bezüglich Temperatur und Leistung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB6_D |
| LADEGERAET_LADE_HISTOGRAMM2 | 0xDFB7 | - | Ladehistogramm bezüglich Temperatur und Leistung für ein zweites Ladegerät (mehrphasiges Laden). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB7_D |
| LADEGERAET_LADEDAUER2 | 0xDFB8 | - | Information zur Ladedauer für ein zweites Ladegerät (mehrphasiges Laden) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB8_D |
| UMSCHALTMATRIX | 0xDFB9 | - | Umschaltmatrix (mehrphasiges Laden): Anzahl von Schaltzyklen und Zustand der Schalter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFB9_D |
| LADEGERAET_SPANNUNG2 | 0xDFBA | - | AC und DC Spannungen für zweites Ladegerät (mehrphasiges Laden) | - | V_U_SleAc | - | - | - | - | - | - | - | 22 | - | RES_0xDFBA_D |
| LADEGERAET_STROM2 | 0xDFBB | - | Ströme des Ladegeräts für zweits Ladegerät (mehrphasiges Laden) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFBB_D |
| BETRIEBSZUSTAND_LADEGERAET2 | 0xDFBC | - | Betriebsarten Ladegerät für zweites Ladegerät (mehrphasiges Laden) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFBC_D |
| LADEDAUER_LADEART | 0xDFBD | - | Ladedauer für verschiedene Ladearten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFBD_D |
| FLASH_DSPS | 0xF000 | - | RID used to flash DSPs | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF000_R |

<a id="table-tab-ladegeraet-betriebsart"></a>
### TAB_LADEGERAET_BETRIEBSART

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Standby |
| 0x02 | HV DC Laden |
| 0x03 | Derating |
| 0x04 | Ladeunterbrechung |
| 0x05 | Fehler |
| 0x06 | Crash |
| 0x07 | Betriebsartwechsel |
| 0x08 | Ladeinitialisierung |
| 0x0F | Signal ungültig |

<a id="table-ucx-02-dsp-flashing-status"></a>
### UCX_02_DSP_FLASHING_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Programmierung erfolgreich abgeschlossen |
| 0x01 | Programmierung noch nicht abgeschlossen |
| 0x02 | Programmierung mit Fehler abgeschlossen |
| 0x03 | Programmierung nicht möglich |
| 0xFF | Wert ungültig |
