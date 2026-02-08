# GWS_G11B.prg

- Jobs: [29](#jobs)
- Tables: [51](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Gangwahlschalter |
| ORIGIN | BMW EI-823 Sefik_Uzun |
| REVISION | 2.001 |
| AUTHOR | MARQUARDT-GMBH EI-512 Agbomenou |
| COMMENT | - |
| PACKAGE | 1.983 |
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
- [DIAGMODE](#table-diagmode) (14 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XD5AA_D](#table-arg-0xd5aa-d) (2 × 12)
- [ARG_0XD5AB_D](#table-arg-0xd5ab-d) (1 × 12)
- [ARG_0XD5B4_D](#table-arg-0xd5b4-d) (1 × 12)
- [ARG_0XD5B5_D](#table-arg-0xd5b5-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (41 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (64 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (10 × 2)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X4200_D](#table-res-0x4200-d) (3 × 10)
- [RES_0X4210_D](#table-res-0x4210-d) (6 × 10)
- [RES_0X4220_D](#table-res-0x4220-d) (6 × 10)
- [RES_0X4225_D](#table-res-0x4225-d) (4 × 10)
- [RES_0X4230_D](#table-res-0x4230-d) (10 × 10)
- [RES_0X4240_D](#table-res-0x4240-d) (11 × 10)
- [RES_0X4245_D](#table-res-0x4245-d) (12 × 10)
- [RES_0X4250_D](#table-res-0x4250-d) (4 × 10)
- [RES_0X4260_D](#table-res-0x4260-d) (5 × 10)
- [RES_0X4280_D](#table-res-0x4280-d) (2 × 10)
- [RES_0X4290_D](#table-res-0x4290-d) (3 × 10)
- [RES_0XD5AE_D](#table-res-0xd5ae-d) (2 × 10)
- [RES_0XD5AF_D](#table-res-0xd5af-d) (2 × 10)
- [RES_0XD5B6_D](#table-res-0xd5b6-d) (2 × 10)
- [RES_0XD5B7_D](#table-res-0xd5b7-d) (4 × 10)
- [RES_0XD5DD_D](#table-res-0xd5dd-d) (2 × 10)
- [RES_0XDFDB_D](#table-res-0xdfdb-d) (4 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (28 × 16)
- [TAB_ENTR_TASTER](#table-tab-entr-taster) (4 × 2)
- [TAB_GWS_POS](#table-tab-gws-pos) (20 × 2)
- [TAB_LED_STATUS](#table-tab-led-status) (17 × 2)
- [TAB_PWF_BASE](#table-tab-pwf-base) (16 × 2)
- [TAB_SPERRE](#table-tab-sperre) (4 × 2)
- [TAB_STATUS_TASTER](#table-tab-status-taster) (3 × 2)
- [TAB_TASTER_PLUS_MINUS](#table-tab-taster-plus-minus) (3 × 2)

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

Dimensions: 14 rows × 3 columns

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
| 0x61 | ECUSUPSPEC | ECUSupplierSpecificSession |
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

<a id="table-arg-0xd5aa-d"></a>
### ARG_0XD5AA_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | Steuerung der Suchbeleuchtung über Diagnose ein- oder auschalten aus = Steuerung über Diagnose ausschalten ein = Steuerung über Diagnose einschalten |
| DIMMBELEUCHTUNGSWERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Beleuchtungswert: Bereich: 0 bis 253 -&gt; Nachtbeleuchtung Bereich: 254 -&gt; Tag (Lichtschalter aus) Bereich: 255 -&gt; Signal fehlerhaft, Licht aus |

<a id="table-arg-0xd5ab-d"></a>
### ARG_0XD5AB_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | - | - | ein- oder auschalten Steuerung der Funktionsanzeige über Diagnose  ein = Steuerung über Diagnose einschalten aus = Steuerung über Diagnose ausschalten |

<a id="table-arg-0xd5b4-d"></a>
### ARG_0XD5B4_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | - | - | ein- oder ausschalten Sperre  ein = Sperre einschalten aus = Sperre freigeben |

<a id="table-arg-0xd5b5-d"></a>
### ARG_0XD5B5_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | - | - | aktivieren Rückstellsystem  ein = Rückstellsystem aktivieren |

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
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 41 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x025E00 | Energiesparmode aktiv | 0 | - |
| 0x025E20 | CAN-Fehler (Sammelfehler) | 0 | - |
| 0x025E21 | EEPROM-Fehler (Sammelfehler) | 0 | - |
| 0x025E23 | Flash Memory Fehler (Sammelfehler) | 0 | - |
| 0x025E26 | Hardwarefehler (Sammelfehler) | 0 | - |
| 0x025E29 | Softwarefehler (Sammelfehler) | 0 | - |
| 0x02FF5E | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x802680 | Funktionsanzeige fehlerhaft | 0 | - |
| 0x802688 | Sperrsystem: Sperre Manuelle Gasse defekt | 0 | - |
| 0x80268A | Rückstellsystem: Hebel konnte nicht zurückgestellt werden | 0 | - |
| 0x80268B | Rückstellsystem: Motor defekt | 0 | - |
| 0x80268C | Suchbeleuchtung fehlerhaft | 0 | - |
| 0x80268E | Parktaster klemmt | 0 | - |
| 0x80268F | Parktaster defekt | 0 | - |
| 0x802690 | Entriegelungstaster klemmt | 0 | - |
| 0x802691 | Entriegelungstaster defekt | 0 | - |
| 0x802692 | Hall-Sensoren Einfachfehler | 0 | - |
| 0x802694 | Hall-Sensoren Zweifachfehler | 0 | - |
| 0x802696 | Unterspannung erkannt | 1 | - |
| 0x802698 | Überspannung erkannt | 1 | - |
| 0x80269A | ROM Check CRC32 fehlt | 0 | - |
| 0x8026A0 | Drivelogic Wipptaster: klemmt | 0 | - |
| 0x8026A1 | Drivelogic Wipptaster: defekt | 0 | - |
| 0xE08472 | LP-CAN Control Module Bus OFF | 0 | - |
| 0xE0847C | LE-CAN Control Module Bus OFF | 0 | - |
| 0xE08BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xE09400 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) fehlt, Empfänger GWS (LP-CAN), Sender EGS (LP-CAN) | 1 | - |
| 0xE09402 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) nicht aktuell, Empfänger GWS (LP-CAN), Sender EGS (LP-CAN) | 1 | - |
| 0xE09404 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) Prüfsumme falsch, Empfänger GWS (LP-CAN), Sender EGS (LP-CAN) | 1 | - |
| 0xE0940A | Botschaft (Dimmung, 0x202) fehlt, Empfänger GWS (LP-CAN), Sender FRM (LP-CAN) | 1 | - |
| 0xE0940C | Botschaft (LCD Helligkeit Regelung, 0x393) fehlt, Empfänger GWS (LP-CAN), Sender KOMBI (LP-CAN) | 1 | - |
| 0xE0940E | Botschaft (Geschwindigkeit Fahrzeug, 0x1A1) fehlt, Empfänger GWS (LP-CAN), Sender ICM (LP-CAN) | 1 | - |
| 0xE09410 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) fehlt, Empfänger GWS (LE-/Private-CAN), Sender EGS (LE-/Private-CAN) | 1 | - |
| 0xE09412 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) nicht aktuell, Empfänger GWS (LE-/Private-CAN), Sender EGS (LE-/Private-CAN) | 1 | - |
| 0xE09414 | Botschaft (Daten Anzeige Getriebestrang, 0x3FD) Prüfsumme falsch, Empfänger GWS (LE-/Private-CAN), Sender EGS (LE-/Private-CAN) | 1 | - |
| 0xE0AC00 | Schnittstelle EGS (Daten Anzeige Getriebestrang, LP-CAN): Signal ungültig | 1 | - |
| 0xE0AC06 | Schnittstelle FRM (Dimmung): Signal ungültig | 1 | - |
| 0xE0AC08 | Schnittstelle KOMBI (LCD Helligkeit Regelung): Signal ungültig | 1 | - |
| 0xE0AC0A | Schnittstelle ICM (Geschwindigkeit Fahrzeug): Signal ungültig | 1 | - |
| 0xE0AC20 | Schnittstelle EGS (Daten Anzeige Getriebestrang, LE-/Private-CAN): Signal ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 64 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | Temperatur Steuergerät | ° | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4010 | Versorgungsspannung GWS | V | Low | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x4011 | STATUS_VDROP | HEX | Low | unsigned char | - | - | - | - |
| 0x4100 | Betriebsstunden GWS | h | Low | signed long | - | 1.0 | 3600.0 | 0.0 |
| 0x4101 | COUNT_PON | count | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4102 | TIME_AFTER_PWRON | s | Low | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0x4105 | COUNT_M_DS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4106 | COUNT_M_N | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4107 | COUNT_M_R | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4108 | COUNT_M_MINUS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4109 | COUNT_M_PLUS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4110 | COUNT_MP | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4111 | COUNT_MM | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4112 | COUNT_V | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4113 | COUNT_VV | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4114 | COUNT_H | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4115 | COUNT_HH | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4116 | COUNT_NA | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4117 | COUNT_MS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4118 | COUNT_MOTOR_SEQ | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4119 | COUNT_RETRACTIONS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4120 | COUNT_P1 | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4121 | COUNT_P2 | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4122 | AD_P1 | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4123 | AD_P2 | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4124 | COUNT_UNLOCK1 | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4125 | COUNT_UNLOCK2 | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4126 | AD_UNLOCK1 | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4127 | AD_UNLOCK2 | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4128 | COUNT_DRIVELOGIC_PLUS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4129 | COUNT_DRIVELOGIC_MINUS | count | Low | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x412A | AD_DRIVELOGIC | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4130 | LEVER_POSITION | 0-n | Low | 0xFF | TAB_GWS_POS | - | - | - |
| 0x4131 | HALL_WERT | - | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4132 | LOCK_STATUS | 0-n | Low | 0xFF | TAB_SPERRE | - | - | - |
| 0x4140 | LED_STATUS | 0-n | Low | 0xFF | TAB_LED_STATUS | - | - | - |
| 0x4141 | AD LED P | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4142 | AD LED R | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4143 | AD LED N | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4144 | AD LED D | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4145 | AD LED MS | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4146 | AD LEDs Backlight | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4147 | PWM_FI_LED | % | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4148 | PWM_SB_LED | % | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4150 | AD MOTOR | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4151 | STATUS_MOTOR | HEX | Low | unsigned char | - | - | - | - |
| 0x4152 | DEBUG_MOTOR | - | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4153 | MOTOR_CONTROL_HI_1 | 0/1 | Low | 0x01 | - | - | - | - |
| 0x4154 | MOTOR_CONTROL_HI_2 | 0/1 | Low | 0x01 | - | - | - | - |
| 0x4155 | MOTOR_CONTROL_PWM_LO_1 | % | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4156 | MOTOR_CONTROL_PWM_LO_2 | % | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4160 | ADC_STATUS | HEX | Low | unsigned char | - | - | - | - |
| 0x4161 | AD_VSAFE_5V | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4162 | AD_VSAFE_7V | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4170 | CAN_VERH_CAN_KOM | count | Low | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4171 | AD_MLED_PBUT | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4172 | AD_MLED_R | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4173 | AD_MLED_N | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4174 | AD_MLED_DS | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4175 | AD_MLED_KARO | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4176 | AD_MLED_PLUS_MINUS | Digits | Low | unsigned int | - | 1.0 | 1.0 | 0.0 |
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

Dimensions: 1 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

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

<a id="table-res-0x4200-d"></a>
### RES_0X4200_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HEBELPOSITION | 0-n | low | unsigned char | - | TAB_GWS_POS | - | - | - | Interne Hebelposition des GWS |
| STAT_CODEWORT_WERT | HEX | high | unsigned int | - | - | - | - | - | Interes Codewort der Hallsensoren an der Codeplatte |
| STAT_AD_VSAFE7_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 7V intern |

<a id="table-res-0x4210-d"></a>
### RES_0X4210_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PARKTASTER_1 | 0-n | low | unsigned char | - | TAB_STATUS_TASTER | - | - | - | Zustand Parktaster 1 |
| STAT_PARKTASTER_2 | 0-n | low | unsigned char | - | TAB_STATUS_TASTER | - | - | - | Zustand Parktaster 2 |
| STAT_AD_PARKTASTER_1_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Partaster 1 |
| STAT_AD_PARKTASTER_2_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Partaster 2 |
| STAT_INTERN_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Interner Status des Parktasters |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 5V intern |

<a id="table-res-0x4220-d"></a>
### RES_0X4220_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ENTRIEGELUNGSTASTER_1 | 0-n | low | unsigned char | - | TAB_STATUS_TASTER | - | - | - | Status des Entriegelungstasters 1 |
| STAT_ENTRIEGELUNGSTASTER_2 | 0-n | low | unsigned char | - | TAB_STATUS_TASTER | - | - | - | Status des Entriegelungstasters 2 |
| STAT_AD_TASTER_1_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Entriegelungstaster 1 |
| STAT_AD_TASTER_2_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Entriegelungstaster 2 |
| STAT_INTERN_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Interner Status des Entriegelungstasters |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 5V intern |

<a id="table-res-0x4225-d"></a>
### RES_0X4225_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_PLUS | 0-n | low | unsigned char | - | TAB_TASTER_PLUS_MINUS | - | - | - | Status Taster Drivelogic Plus |
| STAT_TASTER_MINUS | 0-n | low | unsigned char | - | TAB_TASTER_PLUS_MINUS | - | - | - | Status Taster Drivelogic Minus |
| STAT_AD_DRIVELOGIC_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Drivelogic Wippe |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Versorgungsspannung 5V intern |

<a id="table-res-0x4230-d"></a>
### RES_0X4230_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPERRE | 0-n | low | unsigned char | - | TAB_SPERRE | - | - | - | Status der Sperre |
| STAT_MOTOR_TREIBER_WERT | HEX | low | unsigned char | - | - | - | - | - | Internes Status-Byte des Motor-Triebers im GWS |
| STAT_MOTOR_H1 | 0/1 | low | unsigned char | - | - | - | - | - | Highside 1 Status |
| STAT_MOTOR_H2 | 0/1 | low | unsigned char | - | - | - | - | - | Highside 2 Status |
| STAT_MOTOR_PWM_L1_WERT | % | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktuelles PWM Verhältnis der Motoransteuerung L1 im GWS |
| STAT_MOTOR_PWM_L2_WERT | % | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktuelles PWM Verhältnis der Motoransteuerung L2 im GWS |
| STAT_AD_MOTOR_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert des Motors im GWS |
| STAT_MOTOR_STATE_WERT | HEX | low | unsigned char | - | - | - | - | - | Interner Zustand Motoransteuerung |
| STAT_MOTOR_SUBSTATE_WERT | HEX | low | unsigned char | - | - | - | - | - | Interner Zustand Motoransteuerung |
| STAT_MOTOR_STATEPOS_WERT | HEX | low | unsigned char | - | - | - | - | - | Interner Zustand Motorposition |

<a id="table-res-0x4240-d"></a>
### RES_0X4240_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_GWS_WERT | V | low | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung KL30 gemessen am GWS |
| STAT_AKTIVE_LED | 0-n | low | unsigned char | - | TAB_LED_STATUS | - | - | - | Aktuell aktive LED |
| STAT_PWM_LED_WERT | % | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | PWM Verhältnis der Funktionsanzeige im GWS |
| STAT_AD_LED_P_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED P |
| STAT_AD_LED_R_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED R |
| STAT_AD_LED_N_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED N |
| STAT_AD_LED_D_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED D |
| STAT_AD_LED_MS_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED MS |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Versorgungsspannung 5V intern |
| STAT_AD_VSAFE7_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Versorgungsspannung 7V intern |
| STAT_ADC_STATUS | 0-n | high | unsigned char | - | - | - | - | - | Status des AD Wandlers im GWS |

<a id="table-res-0x4245-d"></a>
### RES_0X4245_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_GWS_WERT | V | low | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung KL30 gemessen am GWS |
| STAT_AKTIVE_LED | 0-n | low | unsigned char | - | TAB_LED_STATUS | - | - | - | Aktuell aktive LED |
| STAT_PWM_LED_WERT | % | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | PWM Verhältnis der Funktionsanzeige im GWS |
| STAT_AD_MLED_PBUT_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED P |
| STAT_AD_MLED_R_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED R |
| STAT_AD_MLED_N_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED N |
| STAT_AD_MLED_DS_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED DS |
| STAT_AD_LED_KARO_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED KARO |
| STAT_AD_LED_PLUS_MINUS_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der LED Plus Minus |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Versorgungsspannung 5V intern |
| STAT_AD_VSAFE7_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Versorgungsspannung 7V intern |
| STAT_ADC_STATUS | 0-n | high | unsigned char | - | - | - | - | - | Status des AD Wandlers im GWS |

<a id="table-res-0x4250-d"></a>
### RES_0X4250_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_GWS_WERT | V | low | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung KL30 gemessen im GWS |
| STAT_PWM_SB_WERT | % | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Verhältnis der Suchbeleuchtung im GWS |
| STAT_AD_SB_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert der Suchbeleuchtung im GWS |
| STAT_AD_VSAFE7_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 7V intern |

<a id="table-res-0x4260-d"></a>
### RES_0X4260_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_WERT | V | low | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung KL30 gemessen im GWS |
| STAT_VDROP_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Statusbyte Spannungsmessung  intern |
| STAT_AD_VSAFE7_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 7V intern |
| STAT_AD_VSAFE5_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Versorgungsspannung 5V intern |
| STAT_AD_VSAFE_GND_WERT | Digits | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | AD Wandler Wert Masse intern |

<a id="table-res-0x4280-d"></a>
### RES_0X4280_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BASEPN | 0-n | low | unsigned char | - | TAB_PWF_BASE | - | - | - | Status Basisteilnetze |
| STAT_FUNCPN_WERT | - | low | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Status funktionale Teilnetze |

<a id="table-res-0x4290-d"></a>
### RES_0X4290_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BETRIEBSSTUNDEN_WERT | h | low | unsigned long | - | - | 1.0 | 3600.0 | 0.0 | Bestriebsstunden |
| STAT_TIME_AFTER_PWRON_WERT | s | low | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Zeit nach Power On |
| STAT_COUNT_PON | 0-n | low | unsigned int | - | - | - | - | - | Anzahl Startzyklen |

<a id="table-res-0xd5ae-d"></a>
### RES_0XD5AE_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PARKTASTER_1_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | - | - | - | Status Parktaster Kontakt 1; siehe TAB_ENTR_TASTER |
| STAT_PARKTASTER_2_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | - | - | - | Status Parktaster Kontakt 2; siehe TAB_ENTR_TASTER |

<a id="table-res-0xd5af-d"></a>
### RES_0XD5AF_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ENTR_TASTER_1_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | 1.0 | 1.0 | 0.0 | Status Entriegelungstaster Kontakt 1; siehe TAB_ENTR_TASTER |
| STAT_ENTR_TASTER_2_NR | 0-n | - | unsigned int | - | TAB_ENTR_TASTER | 1.0 | 1.0 | 0.0 | Status Entriegelungstaster Kontakt 2; siehe TAB_ENTR_TASTER |

<a id="table-res-0xd5b6-d"></a>
### RES_0XD5B6_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_DEFEKT | 0/1 | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Status Positionssensor 0 = kein Fehler 1 = defekt |
| STAT_TREIBER_DEFEKT | 0/1 | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Status Motortreiber 0 = kein Fehler 1 = defekt |

<a id="table-res-0xd5b7-d"></a>
### RES_0XD5B7_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MODULBEZ_TEXT | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | GWS Modulbezeichnung |
| STAT_SW_VERSION_TEXT | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | GWS Software Version |
| STAT_HW_VERSION_TEXT | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | GWS Hardware-Version. |
| STAT_SBC_VERSION_TEXT | TEXT | - | string | - | - | 1.0 | 1.0 | 0.0 | GWS SBC Version |

<a id="table-res-0xd5dd-d"></a>
### RES_0XD5DD_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DRIVELOGIC_WIPPE_PLUS_NR | 0-n | high | unsigned char | - | TAB_TASTER_PLUS_MINUS | 1.0 | 1.0 | 0.0 | Betätigungszustand Drivelogic Taster in Richtung  + |
| STAT_DRIVELOGIC_WIPPE_MINUS_NR | 0-n | high | unsigned char | - | TAB_TASTER_PLUS_MINUS | 1.0 | 1.0 | 0.0 | Betätigungszustand Drivelogic Taster in Richtung  - |

<a id="table-res-0xdfdb-d"></a>
### RES_0XDFDB_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERHINDERUNGSZAEHLER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verhinderung Liegenbleiber |
| STAT_VERHINDERUNGSZAEHLER_KL1S_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verhinderung Liegenbleiber kleiner als 1s |
| STAT_VERHINDERUNGSZAEHLER_KL10S_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verhinderung Liegenbleiber kleiner als 10s  |
| STAT_VERHINDERUNGSZAEHLER_GR10S_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verhinderung Liegenbleiber größer als 10s  |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 28 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_HEBEL_INTERN | 0x4200 | - | Liefert Hebelposition und internes Codewort | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4200_D |
| STATUS_PARKTASTER_INTERN | 0x4210 | - | Liefert interne Werte des Parktasters im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4210_D |
| STATUS_ENTRIEGELUNGSTASTER_INTERN | 0x4220 | - | Liefert interne Werte des Entriegelungstasters im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4220_D |
| STATUS_DRIVELOGIC_INTERN | 0x4225 | - | Liefert interne Werte der Drivelogic Wippe | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4225_D |
| STATUS_MOTOR_INTERN | 0x4230 | - | Interner Status Motor im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4230_D |
| STATUS_FUNKTIONSANZEIGE_INTERN | 0x4240 | - | Interner Status der Funktionsanzeige im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4240_D |
| STATUS_FUNKTIONSANZEIGE_INTERN_M | 0x4245 | - | Interner Status der Funktionsanzeige im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4245_D |
| STATUS_SUCHBELEUCHTUNG_INTERN | 0x4250 | - | Intere Werte der Suchbeleuchtung im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4250_D |
| STATUS_GWS_SPANNUNG_INTERN | 0x4260 | - | Interne Werte der Spannungsmessung im GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4260_D |
| STATUS_GWS_TEMPERATUR | 0x4270 | STAT_GWS_TEMPERATUR_WERT | Temperatur im GWS | °C | - | High | signed char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_GWS_PWF | 0x4280 | - | Status der PWF Schnittstelle | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4280_D |
| STATUS_ENVIRONMENT | 0x4290 | - | Nutzungsdaten GWS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4290_D |
| STEUERN_SUCHBELEUCHTUNG | 0xD5AA | - | Suchbeleuchtung: Steuern | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD5AA_D | - |
| STEUERN_FUNKTIONSANZEIGE | 0xD5AB | - | ein- oder auschalten Steuerung der Funktionsanzeige über Diagnose  ein = Steuerung über Diagnose einschalten aus = Steuerung über Diagnose ausschalten | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD5AB_D | - |
| HALLSENSORIK_WERT | 0xD5AC | STAT_HALLSENSORIK_WERT | Bitmuster der Hallsensorik. | HEX | - | High | unsigned int | - | - | - | - | - | 22 | - | - |
| HEBELPOSITION_WERT | 0xD5AD | STAT_HEBELPOSITION | aktuelle Hebelposition. siehe Tabelle  TAB_GWS_POS  | 0-n | - | High | unsigned int | TAB_GWS_POS | - | - | - | - | 22 | - | - |
| STATUS_GWS_PARKTASTER_1_UND_2 | 0xD5AE | - | Status Parktaster Kontake 1 und 2; 0= nicht gedrückt 1= gedrückt 2= klemmt | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5AE_D |
| STATUS_GWS_ENTR_TASTER_1_UND_2 | 0xD5AF | - | Status Entriegelungstaster Kontakt 1 und 2 0= nicht gedrückt 1= gedrückt 2= klemmt | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5AF_D |
| STATUS_SPERRE_MG | 0xD5B0 | STAT_SPERRE_MG_NR | Status Sperre Manuelle Gasse; siehe TAB_SPERRE | 0-n | - | - | unsigned int | TAB_SPERRE | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STEUERN_SPERRE_MG | 0xD5B4 | - | Steuern der GWS-Sperre manuelle Gasse. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD5B4_D | - |
| STEUERN_RUECKSTELLSYSTEM | 0xD5B5 | - | Steuern des GWS Rueckstellsystems. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD5B5_D | - |
| STATUS_RUECKSTELLSYSTEM | 0xD5B6 | - | Ausgabe Status Rückstellsystem | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5B6_D |
| VERSION_AUSLESEN | 0xD5B7 | - | Auslesen der GWS Version. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5B7_D |
| STATUS_DRIVELOGIC_WIPPE | 0xD5DD | - | Auslesen Tasten Fahrdynamik | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD5DD_D |
| ZAEHLERSTATUS_CAN_KOM | 0xDFDB | - | Anzahl der Bedienungen, bei welchen der LE-CAN einen Liegenbleiber verhindert hat. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDFDB_D |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |

<a id="table-tab-entr-taster"></a>
### TAB_ENTR_TASTER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht gedrueckt |
| 0x01 | gedrueckt |
| 0x02 | klemmt |
| 0xFF | unbekannnter Fehlerort |

<a id="table-tab-gws-pos"></a>
### TAB_GWS_POS

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | NA - Ruhelage Automatikgasse |
| 2 | M/S - Ruhelage Sportgasse |
| 3 | V - Vorne tippen |
| 4 | VV - Vorne überdrückt |
| 5 | H - Hinten tippen |
| 6 | HH - Hinten überdrückt |
| 7 | M+ Manuell plus |
| 8 | M- Manuell minus |
| 9 | ZP - Zwischenposition |
| 10 | INIT - Initialsierung nicht abgeschlossen |
| 15 | UNGÜLTIG - Keine gültige Position erkannt |
| 17 | NA - Ruhelage Automatikgasse |
| 18 | R - Rückwärtsgang |
| 19 | N - Neutral |
| 20 | M- Manuell minus |
| 21 | M+ Manuell plus |
| 22 | D/S - Manuelle Gasse |
| 23 | INIT - Initialisierung nicht abgeschlossen |
| 31 | UNGÜLTIG - Keine gültige Position erkannt |
| 65535 | Ungültiger Wert |

<a id="table-tab-led-status"></a>
### TAB_LED_STATUS

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | LED P |
| 0x01 | LED R |
| 0x02 | LED N |
| 0x03 | LED D |
| 0x04 | LED MS |
| 0x05 | Alle aus |
| 0x06 | Alle an |
| 0x0A | LED P |
| 0x0B | LED R |
| 0x0C | LED N |
| 0x0D | LED D/S |
| 0x0E | LED D/S MPM |
| 0x0F | LED P Punkt |
| 0x10 | LED D/S Punkt |
| 0x11 | LED D/S MPM Punkt |
| 0x12 | Alle aus |
| 0x13 | Alle an |

<a id="table-tab-pwf-base"></a>
### TAB_PWF_BASE

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Kommunikation |
| 0x01 | Parken niO |
| 0x02 | Parken iO |
| 0x03 | Kunde nicht im FZG |
| 0x04 | reserviert |
| 0x05 | Wohnen |
| 0x06 | reserviert |
| 0x07 | Prüfen Analyse Diagnose |
| 0x08 | Fahrbereitschaft herstellen |
| 0x09 | reserviert |
| 0x0A | Fahren |
| 0x0B | reserviert |
| 0x0C | Fahrbereitschaft beenden |
| 0x0D | reserviert |
| 0x0E | reserviert |
| 0x0F | Signal unbefuellt |

<a id="table-tab-sperre"></a>
### TAB_SPERRE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | frei |
| 0x01 | gesperrt |
| 0x03 | defekt |
| 0xFF | unbekannter Fehlerort |

<a id="table-tab-status-taster"></a>
### TAB_STATUS_TASTER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht gedrueckt |
| 0x01 | gedrueckt |
| 0x02 | klemmt |

<a id="table-tab-taster-plus-minus"></a>
### TAB_TASTER_PLUS_MINUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Taster nicht gedrückt |
| 0x01 | Taster gedrückt |
| 0x02 | Taster ungültig |
