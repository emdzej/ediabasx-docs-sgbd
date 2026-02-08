# ELV_G30.prg

- Jobs: [31](#jobs)
- Tables: [118](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektrische Lenksäulenverriegelung |
| ORIGIN | BMW EF-414 Markus_Schmidt |
| REVISION | 2.020 |
| AUTHOR | U-SHIN-DEUTSCHLAND EF-414 Fernandez |
| COMMENT | Aditional Dummy DTC added |
| PACKAGE | 1.75 |
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
- [STATUS_EWS](#job-status-ews) - Der Job liefert den SG-internen Zustand der EWS-Funktion. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC000 STATUS_EWS
- [STATUS_EWS_KF](#job-status-ews-kf) - Auslesen des KF aus dem SG. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC003 STATUS_EWS_KF
- [STEUERN_EWS](#job-steuern-ews) - Der Job dient zum Ansteuern von EWS-Aktionen. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC001 STEUERN_EWS_SK

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

<a id="job-status-ews"></a>
### STATUS_EWS

Der Job liefert den SG-internen Zustand der EWS-Funktion. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC000 STATUS_EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSION | unsigned char | Version der EWS-Schnittstelle, |
| STAT_VERSION_TEXT | string | Version der EWS-Schnittstelle, |
| STAT_CLIENT_LOCKED | unsigned char | Das Result liefert den Anlern- und Verriegelungs-Status der EWS. |
| STAT_CLIENT_LOCKED_TEXT | string | Das Result liefert den Anlern- und Verriegelungs-Status der EWS. |
| STAT_CLIENT_AUTHENTICATED | unsigned char | Das Result den Authentisierungs-Status. |
| STAT_CLIENT_AUTHENTICATED_TEXT | string | Das Result den Authentisierungs-Status. |
| STAT_DH_ACTIVE | unsigned char | Das Result liefert den DH-Berechnungs-Status (läuft bzw. läuft nicht). |
| STAT_DH_ACTIVE_TEXT | string | Das Result liefert den DH-Berechnungs-Status (läuft bzw. läuft nicht). |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ews-kf"></a>
### STATUS_EWS_KF

Auslesen des KF aus dem SG. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC003 STATUS_EWS_KF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KF_DATA | binary | Rohdaten des KF |
| STAT_KF_DATA_EINH | string | Rohdaten des KF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ews"></a>
### STEUERN_EWS

Der Job dient zum Ansteuern von EWS-Aktionen. Weitere Details zum Telegramm-Aufbau siehe EWS6-LH.  0xC001 STEUERN_EWS_SK

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Der Parameter MODE legt die durchzuführende Aktion fest. |
| DATA | string | Legt die Daten für die durchzuführende Aktion fest. Folgende Formate müssen unterstützt werden: 01 23 45 67 89 AB CD EF 01 23 45 67 89 AB CD EF und 0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF,0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
- [ARG_0X102F_R](#table-arg-0x102f-r) (1 × 14)
- [ARG_0XA205_R](#table-arg-0xa205-r) (1 × 14)
- [ARG_0XF785_R](#table-arg-0xf785-r) (3 × 14)
- [ARG_0XF788_R](#table-arg-0xf788-r) (2 × 14)
- [ARG_0XF789_R](#table-arg-0xf789-r) (1 × 14)
- [ARG_0XF78A_R](#table-arg-0xf78a-r) (4 × 14)
- [ARG_0XF78B_R](#table-arg-0xf78b-r) (1 × 14)
- [ARG_0XFD01_D](#table-arg-0xfd01-d) (1 × 12)
- [ARG_0XFD02_D](#table-arg-0xfd02-d) (1 × 12)
- [ARG_0XFD03_D](#table-arg-0xfd03-d) (3 × 12)
- [ARG_0XFD05_D](#table-arg-0xfd05-d) (1 × 12)
- [ARG_0XFD06_D](#table-arg-0xfd06-d) (1 × 12)
- [ARG_0XFD16_D](#table-arg-0xfd16-d) (1 × 12)
- [ARG_0XFD19_D](#table-arg-0xfd19-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (54 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (58 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (55 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (63 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [PROCESS_CLASS_DOP](#table-process-class-dop) (20 × 2)
- [PWF_MESSEMODUS](#table-pwf-messemodus) (3 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (10 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (4 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0XA205_R](#table-res-0xa205-r) (2 × 13)
- [RES_0XF781_R](#table-res-0xf781-r) (1 × 13)
- [RES_0XF782_R](#table-res-0xf782-r) (1 × 13)
- [RES_0XF785_R](#table-res-0xf785-r) (1 × 13)
- [RES_0XF788_R](#table-res-0xf788-r) (1 × 13)
- [RES_0XF789_R](#table-res-0xf789-r) (1 × 13)
- [RES_0XF78A_R](#table-res-0xf78a-r) (1 × 13)
- [RES_0XF78B_R](#table-res-0xf78b-r) (1 × 13)
- [RES_0XFD01_D](#table-res-0xfd01-d) (1 × 10)
- [RES_0XFD02_D](#table-res-0xfd02-d) (1 × 10)
- [RES_0XFD04_D](#table-res-0xfd04-d) (4 × 10)
- [RES_0XFD05_D](#table-res-0xfd05-d) (1 × 10)
- [RES_0XFD06_D](#table-res-0xfd06-d) (1 × 10)
- [RES_0XFD07_D](#table-res-0xfd07-d) (3 × 10)
- [RES_0XFD08_D](#table-res-0xfd08-d) (3 × 10)
- [RES_0XFD09_D](#table-res-0xfd09-d) (2 × 10)
- [RES_0XFD0A_D](#table-res-0xfd0a-d) (4 × 10)
- [RES_0XFD0F_D](#table-res-0xfd0f-d) (4 × 10)
- [RES_0XFD10_D](#table-res-0xfd10-d) (2 × 10)
- [RES_0XFD11_D](#table-res-0xfd11-d) (7 × 10)
- [RES_0XFD13_D](#table-res-0xfd13-d) (11 × 10)
- [RES_0XFD19_D](#table-res-0xfd19-d) (1 × 10)
- [RES_0XFD1B_D](#table-res-0xfd1b-d) (37 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (39 × 16)
- [STATES_OF_JOB](#table-states-of-job) (3 × 2)
- [STAT_TABLE_CALIBRATION](#table-stat-table-calibration) (14 × 2)
- [STAT_TAB_SENSOR_READ](#table-stat-tab-sensor-read) (8 × 2)
- [STAT_TAB_SENSOR_READ_MEMORY](#table-stat-tab-sensor-read-memory) (9 × 2)
- [STAT_TAB_SENSOR_WRITE](#table-stat-tab-sensor-write) (6 × 2)
- [TAB_CALIBRATION_STAUTS](#table-tab-calibration-stauts) (3 × 2)
- [TAB_ELV_AUSFUEHRUNGSSTATUS](#table-tab-elv-ausfuehrungsstatus) (12 × 2)
- [TAB_ELV_CALIBRATIONSTATUS](#table-tab-elv-calibrationstatus) (1 × 2)
- [TAB_ELV_CLEAR_HISTORY](#table-tab-elv-clear-history) (2 × 2)
- [TAB_ELV_CLEAR_HISTORY_PROCESS](#table-tab-elv-clear-history-process) (4 × 2)
- [TAB_ELV_MEM_INIT](#table-tab-elv-mem-init) (1 × 2)
- [TAB_ELV_PROC_STEP](#table-tab-elv-proc-step) (4 × 2)
- [TAB_ELV_PROD_STEP](#table-tab-elv-prod-step) (2 × 2)
- [TAB_ELV_RESET_STAT](#table-tab-elv-reset-stat) (4 × 2)
- [TAB_ELV_SERIALNUMBER_WRITE](#table-tab-elv-serialnumber-write) (2 × 2)
- [TAB_ELV_ZUSTAND](#table-tab-elv-zustand) (8 × 2)
- [TAB_ENDZUSTAND](#table-tab-endzustand) (3 × 2)
- [TAB_ENTLASTUNG_GENERATOR](#table-tab-entlastung-generator) (16 × 2)
- [TAB_ESCAPE_COUNTER](#table-tab-escape-counter) (10 × 2)
- [TAB_EWS_CLIENT_AUTH](#table-tab-ews-client-auth) (4 × 2)
- [TAB_EWS_CLIENT_LOCKED](#table-tab-ews-client-locked) (3 × 2)
- [TAB_EWS_DH_STATUS](#table-tab-ews-dh-status) (3 × 2)
- [TAB_EWS_MODE_ARG](#table-tab-ews-mode-arg) (1 × 2)
- [TAB_EWS_VERSION](#table-tab-ews-version) (3 × 2)
- [TAB_MEM_INIT_RESULT](#table-tab-mem-init-result) (4 × 2)
- [TAB_PCBA_PROD_STEP](#table-tab-pcba-prod-step) (3 × 2)
- [TAB_PROC_STEP](#table-tab-proc-step) (2 × 2)
- [TAB_PROD_DATA_WRITE_PROCESS](#table-tab-prod-data-write-process) (3 × 2)
- [TAB_PROD_STEP](#table-tab-prod-step) (1 × 2)
- [TAB_PROZESSSCHRITT](#table-tab-prozessschritt) (3 × 2)
- [TAB_PWF_ZUSTAND](#table-tab-pwf-zustand) (10 × 2)
- [TAB_SERIAL_NUMBER_AND_AI](#table-tab-serial-number-and-ai) (3 × 2)
- [TAB_STATUS_ELV_KALIBRIERUNG](#table-tab-status-elv-kalibrierung) (4 × 2)
- [TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT](#table-tab-status-laden-hochspannung-powermanagement) (8 × 2)
- [TAB_STATUS_SPANNUNGSEINBRUCH](#table-tab-status-spannungseinbruch) (7 × 2)
- [TAB_STATUS_VERBRENNUNGSMOTOR_ANTRIEB](#table-tab-status-verbrennungsmotor-antrieb) (7 × 2)
- [TAB_STAT_ELV_MEM_RESET_VAL](#table-tab-stat-elv-mem-reset-val) (3 × 2)
- [TAB_STAT_SENSORS_READ](#table-tab-stat-sensors-read) (5 × 2)
- [TAB_STAT_SENSOR_READ_VAL](#table-tab-stat-sensor-read-val) (4 × 2)
- [TAB_STAT_WRITE_DATA](#table-tab-stat-write-data) (3 × 2)
- [TAB_STEUERN_ELV_ARG](#table-tab-steuern-elv-arg) (2 × 2)
- [TAB_VERFAHRART](#table-tab-verfahrart) (3 × 2)
- [TAB_VERFAHR_FEHLER](#table-tab-verfahr-fehler) (5 × 2)
- [TAB_VERFAHR_TRIGGER](#table-tab-verfahr-trigger) (6 × 2)
- [TAB_WRITE_EEPROM_STA](#table-tab-write-eeprom-sta) (4 × 2)
- [TAB_0X2951](#table-tab-0x2951) (1 × 2)
- [TAB_0X505A](#table-tab-0x505a) (1 × 5)
- [TAB_0X505B](#table-tab-0x505b) (1 × 5)
- [TAB_0X505C](#table-tab-0x505c) (1 × 3)
- [TAB_0X5060](#table-tab-0x5060) (1 × 14)
- [TAB_0X5061](#table-tab-0x5061) (1 × 7)
- [TAB_0X5062](#table-tab-0x5062) (1 × 2)
- [TAB_0X5063](#table-tab-0x5063) (1 × 5)
- [TAB_0X5064](#table-tab-0x5064) (1 × 8)

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

<a id="table-arg-0x102f-r"></a>
### ARG_0X102F_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MESSEMODUS | + | - | 0-n | high | unsigned char | - | PWF_MESSEMODUS | - | - | - | - | - | Das Argument gibt an in welchen Fahrzeugzustand  geschaltet werden soll. |

<a id="table-arg-0xa205-r"></a>
### ARG_0XA205_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELV_ANSTEUERN | + | - | 0-n | high | unsigned char | - | TAB_STEUERN_ELV_ARG | - | - | - | - | - | Das Argument enthält die durchzuführende ELV-Aktion |

<a id="table-arg-0xf785-r"></a>
### ARG_0XF785_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SENSOR_EEPROM_ADRESS | + | - | HEX | high | unsigned int | - | - | - | - | - | - | - | Speicheradresse der zu schreibenden Daten |
| SENSOR_EEPROM_KEY | + | - | HEX | high | unsigned int | - | - | - | - | - | - | - | nötiger Key zum auslesen eines bestimmten Speicherbereiches |
| SENSOR_EEPROM_DATA | + | - | HEX | high | unsigned int | - | - | - | - | - | - | - | zu schreibende Daten  |

<a id="table-arg-0xf788-r"></a>
### ARG_0XF788_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SENSOR_MOMORY_ADDRESS_1 | + | - | HEX | high | unsigned int | - | - | - | - | - | - | - | erster Teil der Speicheradresen zum Auslesen des Sensorspeichers |
| SENSOR_MOMORY_ADDRESS_2 | + | - | HEX | high | unsigned int | - | - | - | - | - | - | - | zweiter Teil der Speicheradresen zum Auslesen des Sensorspeichers |

<a id="table-arg-0xf789-r"></a>
### ARG_0XF789_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INIT_MEM_WERT | + | - | 0-n | high | unsigned char | - | TAB_ELV_MEM_INIT | - | - | - | - | - | Startet die Initialisierung des Speichers |

<a id="table-arg-0xf78a-r"></a>
### ARG_0XF78A_R

Dimensions: 4 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_SERIAL_NUMBER_DATA | + | - | DATA | high | data[12] | - | - | 1.0 | 1.0 | 0.0 | - | - | UShin ECU Seriennummer |
| STAT_ELV_PROC_STEP_DATA | + | - | 0-n | high | unsigned char | - | TAB_ELV_PROD_STEP | - | - | - | - | - | Durchgeführte Process- und Prüfschritte bei UShin. |
| STAT_ELV_TGS_DATA | + | - | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | - | - | Teilegenerationsstand bei UShin |
| STAT_ELV_BMW_SACHNUMMER_DATA | + | - | DATA | high | data[9] | - | - | 1.0 | 1.0 | 0.0 | - | - | BMW Sachnummer |

<a id="table-arg-0xf78b-r"></a>
### ARG_0XF78B_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_CLEAR_HISTORYSTORAGE | + | - | 0-n | high | unsigned char | - | TAB_ELV_CLEAR_HISTORY | - | - | - | - | - | Löschen des Inhaltes des Historienspeichers in abhängigkeit des Übergabeparameters |

<a id="table-arg-0xfd01-d"></a>
### ARG_0XFD01_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| USHIN_PROCESS_STEP | 0-n | high | unsigned char | - | TAB_PROC_STEP | - | - | - | - | - | Die Herstellung der ELV und der EOL Test wurden positiv durchlaufen und abgeschlossen. |

<a id="table-arg-0xfd02-d"></a>
### ARG_0XFD02_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PCBA_PROCESS_STEP_DATA | 0-n | high | unsigned char | - | TAB_PROD_STEP | - | - | - | - | - | Durchlaufende Prozess-Schritte als iO geprüft bestätigen. ICT,AOI,FCT,Coating etc. |

<a id="table-arg-0xfd03-d"></a>
### ARG_0XFD03_D

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PCBA_PROD_DATE_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | - | - | Herstelldatum der PCBA |
| STAT_PCBA_PN_VALUE_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | - | - | interne Produktidentifizierung der PCBA bei IMI - BCD codiert |
| STAT_PCBA_CONSECUTIVE_NUMBER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | - | - | Seriennummer der PCBA bei IMI, 8 digits, fortlaufende nummer |

<a id="table-arg-0xfd05-d"></a>
### ARG_0XFD05_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_TGS_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | - | - | Teilegenerationsstand (ASCII-Coded) |

<a id="table-arg-0xfd06-d"></a>
### ARG_0XFD06_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_SERIAL_NUMBER_DATA | DATA | high | data[12] | - | - | 1.0 | 1.0 | 0.0 | - | - | UShin Seriennummer der ELV |

<a id="table-arg-0xfd16-d"></a>
### ARG_0XFD16_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELV_RESET_DATA | 0-n | high | unsigned char | - | TAB_STAT_ELV_MEM_RESET_VAL | - | - | - | - | - | Definitione der Daten die Rückgesetzt werden sollen. |

<a id="table-arg-0xfd19-d"></a>
### ARG_0XFD19_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_BMW_SACHNUMMER | DATA | high | data[9] | - | - | 1.0 | 1.0 | 0.0 | - | - | BMW Sachnummer der ELV |

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

Dimensions: 54 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x026500 | Energiesparmode aktiv | 0 |
| 0x026520 | CAN-Fehler (Sammelfehler) | 0 |
| 0x026521 | EEPROM-Fehler (Sammelfehler) | 0 |
| 0x026523 | Flash Memory Fehler (Sammelfehler) | 0 |
| 0x026526 | Hardwarefehler (Sammelfehler) | 0 |
| 0x026529 | Softwarefehler (Sammelfehler) | 0 |
| 0x02FF65 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x483800 | Elektrische Lenksäulenverriegelung (ELV): Motoransteuerung unplausibel - High Side | 0 |
| 0x483804 | Elektrische Lenksäulenverriegelung (ELV): Motor ohne Funktion | 0 |
| 0x483806 | Elektrische Lenksäulenverriegelung (ELV): Fehler Positionssensor | 0 |
| 0x483807 | Elektrische Lenksäulenverriegelung (ELV): ELV nicht kalibriert | 0 |
| 0x483809 | Elektrische Lenksäulenverriegelung (ELV): keine Entriegelung möglich (Verspannte Lenksäule) | 1 |
| 0x48380A | Elektrische Lenksäulenverriegelung (ELV): keine Entriegelung möglich (verspannte Mechanik) | 0 |
| 0x48380B | Elektrische Lenksäulenverriegelung (ELV): Keine Entriegelung möglich (Authentisierungsfehler) | 0 |
| 0x48380C | Spannungsversorgung - Globale Überspannung extern | 1 |
| 0x48380D | Spannungsversorgung - Globale Überspannung intern | 1 |
| 0x48380E | Spannungsversorgung - Globale Unterspannung extern | 1 |
| 0x48380F | Spannungsversorgung - Globale Unterspannung intern | 1 |
| 0x483810 | Spannungsversorgung - Lokale Überspannung | 0 |
| 0x483811 | Spannungsversorgung - Lokale Unterspannung | 0 |
| 0x483815 | Elektrische Lenksäulenverriegelung (ELV): Watchdog Fehler (Sammelfehler) | 0 |
| 0x483819 | Elektrische Lenksäulenverriegelung (ELV):Spannungsmonitoring Main uC Safety uC (Sammel DTC) | 0 |
| 0x48381B | Elektrische Lenksäulenverriegelung (ELV): Safety uC Verriegel-Bedingung ungültig | 1 |
| 0x48381F | Elektrische Lenksäulenverriegelung (ELV): Motoransteuerung unplausibel - Low Side | 0 |
| 0x483820 | Elektrische Lenksäulenverriegelung (ELV): Motor-Treiber Kurzschluss | 1 |
| 0x483821 | Elektrische Lenksäulenverriegelung (ELV): Keine Aktivierung der Safety Active Leitung seitens des Safety uC | 0 |
| 0x483823 | Elektrische Lenksäulenverriegelung (ELV): Authentisierungsfehler - EWS angelernt und nicht authentisiert (UNLOCK-Trigger) | 1 |
| 0x483824 | Elektrische Lenksäulenverriegelung (ELV): Authentisierungsfehler - EWS angelernt und nicht authentisiert (Fahreraktion) | 1 |
| 0x483825 | Elektrische Lenksäulenverriegelung (ELV): EWS noch nicht angelernt | 1 |
| 0x483826 | Elektrische Lenksäulenverriegelung (ELV): Escape Counter - Zähler im kritischen Bereich | 0 |
| 0x483827 | Elektrische Lenksäulenverriegelung (ELV): Escape Counter - Zähler-Grenze erreicht | 0 |
| 0x483828 | Elektrische Lenksäulenverriegelung (ELV): Communication Error  Main uC - Safety uC | 0 |
| 0x483829 | Elektrische Lenksäulenverriegelung (ELV): Fehler Plausibilisierung Sensorwert | 0 |
| 0x48382A | Elektrische Lenksäulenverriegelung (ELV): Main uc HW/SW Monitor (Sammelfehler) | 0 |
| 0x48382B | Elektrische Lenksäulenverriegelung (ELV): AUTOSAR- Fehler (Sammelfehler) | 0 |
| 0x48382C | Elektrische Lenksäulenverriegelung (ELV): EWS Manipulationsversuch | 0 |
| 0x48382D | Spannungsversorgung - Lokale Überspannung(U_BAT) | 0 |
| 0x48382E | Spannungsversorgung - Lokale Unterspannung (U_BAT) | 0 |
| 0x48387F | Dummy DTC für Kompatibilitaet der SGBD (alte Umweltdaten) | 1 |
| 0xE2440A | FA-CAN Control Module Bus OFF | 0 |
| 0xE24BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xE254B8 | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Timeout | 1 |
| 0xE254B9 | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Checksumme | 1 |
| 0xE254BA | Botschaftsfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Alive | 1 |
| 0xE254BE | Signalfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Ungültig | 1 |
| 0xE254BF | Signalfehler (Geschwindigkeit Fahrzeug, ID: V_VEH) - Undefiniert | 1 |
| 0xE254FF | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Checksumme | 1 |
| 0xE25565 | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Alive | 1 |
| 0xE2560C | Botschaftsfehler (Zustand Fahrzeug, ID: CON_VEH) Timeout | 1 |
| 0xE25652 | Botschaftsfehler (ZV und Klappenzustand, ID: STAT_ZV_KLAPPEN) - Timeout | 1 |
| 0xE2565E | Signalfehler (Zustand Fahrzeug, ID: CON_VEH) Ungültig | 1 |
| 0xE25858 | Signalfehler (Zustand Fahrzeug, ID: CON_VEH) Undefiniert | 1 |
| 0xE25CB1 | Botschaftsfehler (Daten_EWS_7, ID: DT_EWS_7) Timeout | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 58 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Hybrid power Managment Zustand | 0-n | High | 0xFF | TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT | - | - | - |
| 0x0002 | SPI_E_HARDWARE_ERROR | 0/1 | High | 0x0001 | - | - | - | - |
| 0x0003 | MCU_E_CLOCK_FAILURE | 0/1 | High | 0x0002 | - | - | - | - |
| 0x0004 | ECUM_E_RAM_CHECK_FAILED | 0/1 | High | 0x0004 | - | - | - | - |
| 0x0005 | MCU_E_WRITE_FAILURE | 0/1 | High | 0x0008 | - | - | - | - |
| 0x0006 | MCU_E_LVI_FAILURE | 0/1 | High | 0x0010 | - | - | - | - |
| 0x0007 | MCU_E_BURAM_WRITE_FAILURE | 0/1 | High | 0x0020 | - | - | - | - |
| 0x0008 | MCU_E_PORTGROUP_STATUS_BACKUP_FAILURE | 0/1 | High | 0x0040 | - | - | - | - |
| 0x0009 | PORT_E_WRITE_FAILURE | 0/1 | High | 0x0080 | - | - | - | - |
| 0x000A | MCU_E_POWER_DOWN_MODE_FAILURE | 0/1 | High | 0x0100 | - | - | - | - |
| 0x000B | APPL_E_LIN_BUS_ERROR | 0/1 | High | 0x0200 | - | - | - | - |
| 0x000C | APPL_E_FATAL_HARDWARE_ERROR | 0/1 | High | 0x0400 | - | - | - | - |
| 0x000D | APPL_E_MINOR_HARDWARE_FAILURE | 0/1 | High | 0x0800 | - | - | - | - |
| 0x000E | APPL_E_LIN_COMMUNICATION_ERROR | 0/1 | High | 0x1000 | - | - | - | - |
| 0x000F | WDG_E_DISABLE_REJECTED | 0/1 | High | 0x01 | - | - | - | - |
| 0x0010 | WDG_E_MODE_FAILED | 0/1 | High | 0x02 | - | - | - | - |
| 0x0011 | WDGM_E_IMPROPER_CALLER | 0/1 | High | 0x04 | - | - | - | - |
| 0x0012 | WDGM_E_SET_MODE | 0/1 | High | 0x08 | - | - | - | - |
| 0x0013 | WDG_E_TRIGGER_TIMEOUT | 0/1 | High | 0x10 | - | - | - | - |
| 0x0014 | WDGM_E_SUPERVISION | 0/1 | High | 0x20 | - | - | - | - |
| 0x0015 | FEE_E_READ_FAILED | 0/1 | High | 0x01 | - | - | - | - |
| 0x0016 | FEE_E_WRITE_FAILED | 0/1 | High | 0x02 | - | - | - | - |
| 0x0017 | FEE_E_FORMAT_FAILED | 0/1 | High | 0x04 | - | - | - | - |
| 0x0018 | FEE_E_STARTUP_FAILED | 0/1 | High | 0x08 | - | - | - | - |
| 0x0019 | NVM_E_INTEGRITY_FAILED | 0/1 | High | 0x01 | - | - | - | - |
| 0x001A | NVM_E_LOSS_OF_REDUNDANCY | 0/1 | High | 0x02 | - | - | - | - |
| 0x001B | NVM_E_QUEUE_OVERFLOW | 0/1 | High | 0x04 | - | - | - | - |
| 0x001C | NVM_E_REQ_FAILED | 0/1 | High | 0x08 | - | - | - | - |
| 0x001D | NVM_E_VERIFY_FAILED | 0/1 | High | 0x10 | - | - | - | - |
| 0x001E | NVM_E_WRITE_PROTECTED | 0/1 | High | 0x20 | - | - | - | - |
| 0x001F | NVM_E_WRONG_BLOCK_ID | 0/1 | High | 0x40 | - | - | - | - |
| 0x0020 | APPL_E_NO_LCK_H_CMD_EN_ACT | 0/1 | High | 0x01 | - | - | - | - |
| 0x0021 | APPL_E_NO_LCK_H_CMD_COND_ACT | 0/1 | High | 0x02 | - | - | - | - |
| 0x0022 | APPL_E_UNINT_LCK_H_CMD_EN_ACT | 0/1 | High | 0x04 | - | - | - | - |
| 0x0023 | APPL_E_UNINT_LCK_H_CMD_COND_ACT | 0/1 | High | 0x08 | - | - | - | - |
| 0x0029 | APPL_E_SAFETY_UC_UNDER_OR_OVERVOLTAGE | 0/1 | High | 0x01 | - | - | - | - |
| 0x002A | APPL_E_MAIN_UC_UNDER_OR_OVERVOLTAGE | 0/1 | High | 0x02 | - | - | - | - |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2863 | USP_STATUS_GENERATORENTLASTUNG | 0-n | High | 0xFF | TAB_ENTLASTUNG_GENERATOR | - | - | - |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2898 | USP_DTC_URSAECHLICHER_FEHLER_4BYTE | HEX | High | signed long | - | - | - | - |
| 0x294F | Status Spannungseinbruch | 0-n | High | 0xFF | TAB_STATUS_SPANNUNGSEINBRUCH | - | - | - |
| 0x2950 | Status Verbrennungsmotor Antrieb | 0-n | High | 0xFF | TAB_STATUS_VERBRENNUNGSMOTOR_ANTRIEB | - | - | - |
| 0x2951 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x4007 | BSP_INFO | TEXT | High | 28 | - | 1.0 | 1.0 | 0.0 |
| 0x4008 | BSP_SENSOR_COEF | HEX | High | unsigned long | - | - | - | - |
| 0x505B | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x505C | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x505D | MOT_DIAG_VAL | HEX | High | unsigned int | - | - | - | - |
| 0x505E | VCC | HEX | High | unsigned int | - | - | - | - |
| 0x5060 | Sub-Tabelle | 0-n | - | 0xFFFF | - | - | - | - |
| 0x5061 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5063 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5064 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
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

Dimensions: 55 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x483824 | Elektrische Lenksäulenverriegelung (ELV): EWS Manipulationsversuch | 1 |
| 0x483830 | Fehler interne Spannungsversorgung: VCC_2 -  Spannungsschwelle überschritten/unterschritten (Safety uC iO) | 0 |
| 0x483831 | Fehler interne Spannungsversorgung: VCC_1 - Spannungsschwelle überschritten/unterschritten | 0 |
| 0x483832 | Fehler interne Spannungsversorgung: VCC_2 - Spannungsschwelle überschritten (Safety uC niO) | 0 |
| 0x48383A | Motoransteuerung unplausibel - Low Side | 0 |
| 0x48383B | Motoransteuerung unplausibel - High Side | 0 |
| 0x48383C | Motoransteuerung unplausibel - High Side | 0 |
| 0x48383D | Motoransteuerung unplausibel - High Side | 0 |
| 0x483840 | Softwarefehler - WDT Modewechsel verhindert | 0 |
| 0x483841 | Softwarefehler - WDG Modewechsel fehlgeschlagen | 0 |
| 0x483842 | Softwarefehler - WDGM unsicherer Aufruf | 0 |
| 0x483843 | Softwarefehler - WDG Treiber fehler | 0 |
| 0x483844 | Softwarefehler - SBC WDG hat Reset ausgeführt | 0 |
| 0x483845 | Softwarefehler - WDGM reset | 0 |
| 0x483846 | Softwarefehler - unerlaubter Speicherzugriff auf ASIL Bereich | 0 |
| 0x483847 | Softwarefehler - OS Fehler | 0 |
| 0x483848 | Softwarefehler - OS shutdown | 0 |
| 0x48384A | Safety uC Verriegelungsbedingungen - ungültig | 0 |
| 0x48384B | Safety uC Verriegelungsbedingungen - Timeout | 0 |
| 0x48384C | Safety uC Verriegelungsbedingungen - SPI Fehler | 0 |
| 0x48384D | Safety uC Verriegelungsbedingungen - ADC Fehler | 0 |
| 0x48384E | Safety uC Verriegelungsbedingungen  - Fehler Konfigurationsregister | 0 |
| 0x48384F | Safety uC Verriegelungsbedingungen (Sammelfehler) - RAM Fehler | 0 |
| 0x483850 | EEPROM-Fehler -  Lesefehler NV-RAM | 0 |
| 0x483851 | EEPROM-Fehler - Schreibfehler NV-RAM | 0 |
| 0x483852 | EEPROM-Fehler - Formatfehler NV-RAM | 0 |
| 0x483853 | EEPROM-Fehler - Startupfehler NV-RAM | 0 |
| 0x483860 | AUTOSAR-Fehler- SPI Treiber Fehler | 0 |
| 0x483863 | AUTOSAR-Fehler - Schreibfehler (geschütztes REG) | 0 |
| 0x483864 | AUTOSAR-Fehler - Spannungsbereichsfehler | 0 |
| 0x483865 | AUTOSAR-Fehler - Schreibfehler (BURAM) | 0 |
| 0x483866 | AUTOSAR-Fehler - Port Group Backup Fehler (BURAM) | 0 |
| 0x483867 | AUTOSAR-Fehler - Schreibfehler (PORT) | 0 |
| 0x483869 | Main uC HW/SW Monitor - Fehler Programmfluß | 0 |
| 0x48386A | Main uC HW/SW Monitor - Fehler Konfig-Reg check | 0 |
| 0x48386B | Main uC HW/SW Monitor - Watchdog reset | 0 |
| 0x48386C | Main uC HW/SW Monitor - Fehler Konfig-Reg Korrektur | 0 |
| 0x48386D | Main uC HW/SW Monitor - Fehler WDG not running | 0 |
| 0x48386E | Main uC HW/SW Monitor - ASIL ROM check failed (startup) | 0 |
| 0x48386F | Flash Memory Fehler - Fehler Integrität NVM | 0 |
| 0x483870 | Flash Memory Fehler - Fehler redundaten Daten | 0 |
| 0x483871 | Flash Memory Fehler- Fehler Überlauf Nachrichtenpuffer | 0 |
| 0x483872 | Flash Memory Fehler - Fehler Wiederherstellung bei Speicherzugriff | 0 |
| 0x483873 | Flash Memory Fehler - Fehler schreiben in NvM | 0 |
| 0x483874 | Flash Memory Fehler: Fehler Schreibschutz NvM | 0 |
| 0x483875 | Flash Memory Fehler: Fehler falsche NvM Block ID | 0 |
| 0x483876 | Main uC HW/SW Monitor - QM ROM check fehler (startup) | 0 |
| 0x483877 | Main uC HW/SW Monitor - RAM check failed | 0 |
| 0x483878 | Main uC HW/SW Monitor - Prozessortakt fehler | 0 |
| 0x483879 | Main uC HW/SW Monitor - MDU Selbstcheck Fehler | 0 |
| 0x48387A | Main uC HW/SW Monitor - WDT Selbstcheck Fehler | 0 |
| 0x48387B | Main uC HW/SW Monitor (Sammelfehler) - DIS Test Fehler | 0 |
| 0x48387C | Main uC HW/SW Monitor - Main uC ADC Fehler | 0 |
| 0x48387F | Dummy DTC für Kompatibilitaet der SGBD (alte Umweltdaten) | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 63 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Hybrid power Managment Zustand | 0-n | High | 0xFF | TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT | - | - | - |
| 0x0002 | SPI_E_HARDWARE_ERROR | 0/1 | High | 0x0001 | - | - | - | - |
| 0x0003 | MCU_E_CLOCK_FAILURE | 0/1 | High | 0x0002 | - | - | - | - |
| 0x0004 | ECUM_E_RAM_CHECK_FAILED | 0/1 | High | 0x0004 | - | - | - | - |
| 0x0005 | MCU_E_WRITE_FAILURE | 0/1 | High | 0x0008 | - | - | - | - |
| 0x0006 | MCU_E_LVI_FAILURE | 0/1 | High | 0x0010 | - | - | - | - |
| 0x0007 | MCU_E_BURAM_WRITE_FAILURE | 0/1 | High | 0x0020 | - | - | - | - |
| 0x0008 | MCU_E_PORTGROUP_STATUS_BACKUP_FAILURE | 0/1 | High | 0x0040 | - | - | - | - |
| 0x0009 | PORT_E_WRITE_FAILURE | 0/1 | High | 0x0080 | - | - | - | - |
| 0x000A | MCU_E_POWER_DOWN_MODE_FAILURE | 0/1 | High | 0x0100 | - | - | - | - |
| 0x000B | APPL_E_LIN_BUS_ERROR | 0/1 | High | 0x0200 | - | - | - | - |
| 0x000C | APPL_E_FATAL_HARDWARE_ERROR | 0/1 | High | 0x0400 | - | - | - | - |
| 0x000D | APPL_E_MINOR_HARDWARE_FAILURE | 0/1 | High | 0x0800 | - | - | - | - |
| 0x000E | APPL_E_LIN_COMMUNICATION_ERROR | 0/1 | High | 0x1000 | - | - | - | - |
| 0x000F | WDG_E_DISABLE_REJECTED | 0/1 | High | 0x01 | - | - | - | - |
| 0x0010 | WDG_E_MODE_FAILED | 0/1 | High | 0x02 | - | - | - | - |
| 0x0011 | WDGM_E_IMPROPER_CALLER | 0/1 | High | 0x04 | - | - | - | - |
| 0x0012 | WDGM_E_SET_MODE | 0/1 | High | 0x08 | - | - | - | - |
| 0x0013 | WDG_E_TRIGGER_TIMEOUT | 0/1 | High | 0x10 | - | - | - | - |
| 0x0014 | WDGM_E_SUPERVISION | 0/1 | High | 0x20 | - | - | - | - |
| 0x0015 | FEE_E_READ_FAILED | 0/1 | High | 0x01 | - | - | - | - |
| 0x0016 | FEE_E_WRITE_FAILED | 0/1 | High | 0x02 | - | - | - | - |
| 0x0017 | FEE_E_FORMAT_FAILED | 0/1 | High | 0x04 | - | - | - | - |
| 0x0018 | FEE_E_STARTUP_FAILED | 0/1 | High | 0x08 | - | - | - | - |
| 0x0019 | NVM_E_INTEGRITY_FAILED | 0/1 | High | 0x01 | - | - | - | - |
| 0x001A | NVM_E_LOSS_OF_REDUNDANCY | 0/1 | High | 0x02 | - | - | - | - |
| 0x001B | NVM_E_QUEUE_OVERFLOW | 0/1 | High | 0x04 | - | - | - | - |
| 0x001C | NVM_E_REQ_FAILED | 0/1 | High | 0x08 | - | - | - | - |
| 0x001D | NVM_E_VERIFY_FAILED | 0/1 | High | 0x10 | - | - | - | - |
| 0x001E | NVM_E_WRITE_PROTECTED | 0/1 | High | 0x20 | - | - | - | - |
| 0x001F | NVM_E_WRONG_BLOCK_ID | 0/1 | High | 0x40 | - | - | - | - |
| 0x0024 | APPL_E_LIN_BUS_ERROR | 0/1 | Low | 0x01 | - | - | - | - |
| 0x0025 | APPL_E_FATAL_HARDWARE_ERROR | 0/1 | High | 0x02 | - | - | - | - |
| 0x0026 | APPL_E_MINOR_HARDWARE_FAILURE | 0/1 | High | 0x04 | - | - | - | - |
| 0x0027 | APPL_E_LIN_COMMUNICATION_ERROR | 0/1 | High | 0x08 | - | - | - | - |
| 0x0028 | CANSM_E_BUS_OFF | 0/1 | High | 0x01 | - | - | - | - |
| 0x0029 | APPL_E_SAFETY_UC_UNDER_OR_OVERVOLTAGE | 0/1 | High | 0x01 | - | - | - | - |
| 0x002A | APPL_E_MAIN_UC_UNDER_OR_OVERVOLTAGE | 0/1 | High | 0x02 | - | - | - | - |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2863 | USP_STATUS_GENERATORENTLASTUNG | 0-n | High | 0xFF | TAB_ENTLASTUNG_GENERATOR | - | - | - |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2898 | USP_DTC_URSAECHLICHER_FEHLER_4BYTE | HEX | High | signed long | - | - | - | - |
| 0x294F | Status Spannungseinbruch | 0-n | High | 0xFF | TAB_STATUS_SPANNUNGSEINBRUCH | - | - | - |
| 0x2950 | Status Verbrennungsmotor Antrieb | 0-n | High | 0xFF | TAB_STATUS_VERBRENNUNGSMOTOR_ANTRIEB | - | - | - |
| 0x2951 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x4007 | BSP_INFO | TEXT | High | 28 | - | 1.0 | 1.0 | 0.0 |
| 0x5057 | UWB_ERROR_NVM_BLOCK_1 | HEX | High | unsigned long | - | - | - | - |
| 0x5058 | UWB_ERROR_NVM_BLOCK_2 | HEX | High | unsigned long | - | - | - | - |
| 0x5059 | UWB_ERROR_NVM_BLOCK_3 | HEX | High | unsigned long | - | - | - | - |
| 0x505A | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x505C | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x505D | MOT_DIAG_VAL | HEX | High | unsigned int | - | - | - | - |
| 0x505E | VCC | HEX | High | unsigned int | - | - | - | - |
| 0x505F | EVENT_VALUE | HEX | High | unsigned char | - | - | - | - |
| 0x5060 | Sub-Tabelle | 0-n | - | 0xFFFF | - | - | - | - |
| 0x5061 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5062 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5063 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5064 | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-process-class-dop"></a>
### PROCESS_CLASS_DOP

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | reserved |
| 1 | Hardware (Elektrik) |
| 2 | Hardwareausprägung |
| 3 | Hardwarefarbe |
| 5 | Codierdate (CAF) |
| 6 | Bootloader |
| 7 | Flashloader Slave |
| 8 | Software ECU-Speicherimage |
| 9 | Flash File Software |
| 10 | Prüfsoftware |
| 11 | Programmiersystem |
| 12 | Interaktive Betriebsanleitung Daten |
| 15 | FA2FP |
| 16 | FreischaltecodeFzgAuftrag |
| 26 | Temporaere Loesch Routing |
| 27 | Temporäre Programmier Routing |
| 160 | Entertainment Daten |
| 161 | Navigation Daten |
| 162 | FreischaltecodeFunktion |
| 255 | reserved |

<a id="table-pwf-messemodus"></a>
### PWF_MESSEMODUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MESSEMODUS_NICHT_AKTIV |
| 0x01 | MESSEMODUS_AKTIV |
| 0xFF | Wert ungültig |

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

<a id="table-res-0xa205-r"></a>
### RES_0XA205_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_AUSFUEHRUNGSSTATUS | + | - | - | 0-n | high | unsigned char | - | TAB_ELV_AUSFUEHRUNGSSTATUS | - | - | - | Das Ergebnis liefert bei der  Ausführung der angeforderten Aktion u.U. aufgetretene Fehler. Hinweis:  Es wird nur der erste aufgetretene Fehler zurückgeliefert  |
| STAT_AUSFUERUNGSSTATUS | - | - | + | 0-n | high | unsigned char | - | TAB_ELV_AUSFUEHRUNGSSTATUS | - | - | - | Ausführungsstatus laut Tabelle TAB_ELV_AUSFUERUNGSSTATUS |

<a id="table-res-0xf781-r"></a>
### RES_0XF781_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CALIBRATION_RESULT | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ELV_KALIBRIERUNG | - | - | - | Gibt es Status der Kalibrierroutine zurück |

<a id="table-res-0xf782-r"></a>
### RES_0XF782_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_EEPROM_READ | - | - | + | 0-n | high | unsigned char | - | STAT_TAB_SENSOR_READ_MEMORY | - | - | - | Status der Routine des Auslesevorganges der ELV aus dem EEPROM |

<a id="table-res-0xf785-r"></a>
### RES_0XF785_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_EEPROM_READ | - | - | + | 0-n | high | unsigned char | - | STAT_TAB_SENSOR_READ_MEMORY | - | - | - | Status der Routine des Auslesevorganges der ELV aus dem EEPROM |

<a id="table-res-0xf788-r"></a>
### RES_0XF788_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_READ_RESULT | - | - | + | 0-n | high | unsigned char | - | STAT_TAB_SENSOR_READ | - | - | - | Ergebnis des Leseprozesses der ELV aus dem Sensorspeicher |

<a id="table-res-0xf789-r"></a>
### RES_0XF789_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MEM_INIT_RESULT | - | - | + | 0-n | high | unsigned char | - | TAB_MEM_INIT_RESULT | - | - | - | Gibt das ergebniss der Routine der Initialisierung des Speichers zurück. |

<a id="table-res-0xf78a-r"></a>
### RES_0XF78A_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PROD_DATA_WRITE_RESULT | - | - | + | 0-n | high | unsigned char | - | TAB_PROD_DATA_WRITE_PROCESS | - | - | - | Ergebnis der Schreibrouting der Produktionsdaten der ELV |

<a id="table-res-0xf78b-r"></a>
### RES_0XF78B_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HISTORYSTORAGE_CLEAR_PROCESS | - | - | + | 0-n | high | unsigned char | - | TAB_ELV_CLEAR_HISTORY_PROCESS | - | - | - | Gibt den Status des Löschprozesses des Historienspeichers der ELV zurück |

<a id="table-res-0xfd01-d"></a>
### RES_0XFD01_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PROCESS_STEP_ELV | 0-n | high | unsigned char | - | TAB_ELV_PROC_STEP | - | - | - | Prüfschritte bei UShin erfolgreich abgeschlossen |

<a id="table-res-0xfd02-d"></a>
### RES_0XFD02_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PCBA_PROCESS_STEP | 0-n | high | unsigned char | - | TAB_PCBA_PROD_STEP | - | - | - | Prüfschritte beim Leiterplatten-Lieferant erfolgreich abgeschlossen ( ICT,AOI,FCT, flashing, coting etc. ) |

<a id="table-res-0xfd04-d"></a>
### RES_0XFD04_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PCBA_PROD_DATE_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Herstelldatum der PCBA |
| STAT_PCBA_PN_WERT_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Interne Produktidentifizierung der PCBA bei IMI - BCD codiert |
| STAT_PCBA_CONSECUTIVE_NUMBER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Seriennummer der PCBA bei IMI, 8 digits, fortlaufende nummer |
| STAT_BMW_HW_SGBM_ID_DATA | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | Hardware Index der PCBA |

<a id="table-res-0xfd05-d"></a>
### RES_0XFD05_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_TGS_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Teilegenerationsstand der ELV |

<a id="table-res-0xfd06-d"></a>
### RES_0XFD06_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_SERIAL_NUMBER_DATA | DATA | high | data[12] | - | - | 1.0 | 1.0 | 0.0 | UShin Seriennummer der ELV |

<a id="table-res-0xfd07-d"></a>
### RES_0XFD07_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_PROC | 0-n | high | unsigned char | - | STAT_TAB_SENSOR_READ | - | - | - | Status des Auslesevorgangs |
| STAT_SENSOR_MEMORY_1_WERT | HEX | high | unsigned int | - | - | - | - | - | Daten aus dem Speicher des Hall Sensors Teil 1 |
| STAT_SENSOR_MEMORY_2_WERT | HEX | high | unsigned int | - | - | - | - | - | Daten aus dem Speicher des Hall Sensors Teil 2 |

<a id="table-res-0xfd08-d"></a>
### RES_0XFD08_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_PROC | 0-n | high | unsigned char | - | TAB_STAT_SENSORS_READ | - | - | - | Status des Auslesevorganges |
| STAT_SENSOR_EEPROM_LENGH_WERT | HEX | high | unsigned int | - | - | - | - | - | Länge der ausgelesenen Daten |
| STAT_SENSOR_EEPROM_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Ausgelesene Daten aus dem EEPROM des Hall Sensors |

<a id="table-res-0xfd09-d"></a>
### RES_0XFD09_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_RAW_ANGLE_WERT | HEX | high | unsigned long | - | - | - | - | - | 14 Bits RAW Wert des Sensors |
| STAT_SENSOR_CAL_ANGLE_WERT | HEX | high | unsigned long | - | - | - | - | - | kalibrierter 32 Bit Sensorwert inkl. Korrektur |

<a id="table-res-0xfd0a-d"></a>
### RES_0XFD0A_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LCK_BRAKE_COEF_WERT | HEX | high | unsigned char | - | - | - | - | - | Coeffizient für die Gewichtung der Geschwindigkeit für die Bremspunktbestimmung in Entriegelungsrichtung. (ms) |
| STAT_LCK_BRAKE_POS_WERT | HEX | high | unsigned long | - | - | - | - | - | Konstante zur Ermittlung des Bremspunkts in Verriegelungssrichtung. Referenzwinkel für die Bremsposition (LSB=360*2^-16) (° Grad) |
| STAT_UNL_BRAKE_COEF_WERT | HEX | high | unsigned char | - | - | - | - | - | Coeffizient für die Gewichtung der Geschwindigkeit für die Bremspunktbestimmung in Entriegelungsrichtung. (ms) |
| STAT_UNL_BREAK_POS_WERT | HEX | high | unsigned long | - | - | - | - | - | Konstante zur Ermittlung des Bremspunkts in Entriegelungssrichtung. Referenzwinkel für die Bremsposition (LSB=360*2^-16) (° Grad) |

<a id="table-res-0xfd0f-d"></a>
### RES_0XFD0F_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_SERIAL_NUMBER_DATA | DATA | high | data[12] | - | - | 1.0 | 1.0 | 0.0 | UShin ECU Seriennummer + test equipment ASCII + consecutive number + shift + production date |
| STAT_ELV_PROC_STEP_DATA | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | Durchgeführte Prozess - und Prüfschritte bei UShin |
| STAT_ELV_TGS_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Teilegenerationsstand bei UShin |
| STAT_ELV_BMW_SACHNUMMER_DATA | DATA | high | data[9] | - | - | 1.0 | 1.0 | 0.0 | BMW Sachnummer |

<a id="table-res-0xfd10-d"></a>
### RES_0XFD10_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_INV_CALIBRATION_WERT | HEX | high | unsigned int | - | - | - | - | - | Invertierter Wert zur Korrektur der Sensorwerte |
| STAT_ELV_CALIBRATION_WERT | HEX | high | unsigned int | - | - | - | - | - | Wert zur Korrektur der Sensorwerte |

<a id="table-res-0xfd11-d"></a>
### RES_0XFD11_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_SERIAL_NUMBER_DATA | DATA | high | data[12] | - | - | 1.0 | 1.0 | 0.0 | Seriennummer der ELV |
| STAT_ELV_PROC_STEP_DATA | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | Durchgeführte Process- und Prüfschritte bei UShin. |
| STAT_ELV_TGS_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Teilegenerationsstand bei Ushin |
| STAT_PCBA_PROD_DATE_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Herstelldatum der PCBA |
| STAT_PCBA_PN_WERT_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Interne Produktidentifizierung der PCBA bei IMI - BCD codiert |
| STAT_PCBA_CONSECUTIVE_NUMBER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Seriennummer der PCBA bei IMI, 8 digits, fortlaufende nummer |
| STAT_PCBA_PROCESS_STEP_DATA | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | Prüfschritte beim Leiterplatten-Lieferant erfolgreich abgeschlossen ( ICT,AOI,FCT, flashing, coting etc. ) |

<a id="table-res-0xfd13-d"></a>
### RES_0XFD13_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_HW_VERSION | 0-n | high | unsigned char | - | - | - | - | - | Sensor Hardware Version |
| STAT_SENSOR_SW_VERSION | 0-n | high | unsigned char | - | - | - | - | - | Sensor Software Version  |
| STAT_SENSOR_STATUS_WERT | HEX | high | unsigned char | - | - | - | - | - | Sensor State |
| STAT_SENSOR_RESERVED_VALUE_1_WERT | HEX | high | unsigned char | - | - | - | - | - | Reserverd 0  |
| STAT_SENSOR_RESERVED_VALUE_2_WERT | HEX | high | unsigned char | - | - | - | - | - | Reserverd 1  |
| STAT_SENSOR_RESERVED_VALUE_3_WERT | HEX | high | unsigned char | - | - | - | - | - | Reserverd 2  |
| STAT_SENSOR_RAW_ANGLE_WERT | ° | high | unsigned long | - | - | 360.0 | 16383.0 | 0.0 | No zero-point correction. Unsigned scaled: LSB=360x2^-16 [degree] |
| STAT_SENSOR_CALC_ANGLE_WERT | ° | high | unsigned long | - | - | 360.0 | 16383.0 | 0.0 | Zero-point corrected. Unsigned scaled: LSB=360x2^-16 [degree] |
| STAT_SENSOR_SPEED_WERT | °/s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 |  Signed scaled: LSB=360x2^-16 [degree/s] |
| STAT_SENSOR_FAIL_SAFE_REPORT_WERT | HEX | high | unsigned char | - | - | - | - | - | Fail Save Report des Sensors |
| STAT_SENSOR_INTERNAL_FAULT_WERT | HEX | high | unsigned long | - | - | - | - | - | Internal Fault Information |

<a id="table-res-0xfd19-d"></a>
### RES_0XFD19_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELV_BMW_SACHNUMMER_DATA | DATA | high | data[9] | - | - | 1.0 | 1.0 | 0.0 | BMW Sachnummer |

<a id="table-res-0xfd1b-d"></a>
### RES_0XFD1B_D

Dimensions: 37 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LOCK_CYCLE_COUNT_WERT | HEX | high | unsigned long | - | - | - | - | - | Gesamtwert des LOCK/UNLOCK Zyklenzähler der ELV |
| STAT_TIMESTAMP_FIRST_EWS_TRAINING_WERT | HEX | high | unsigned long | - | - | - | - | - | Systemzeit des ersten erfolgreichen Anlernens (Werk BMW) in Sekunden. |
| STAT_TIMESTAMP_LAST_EWS_TRAINING_WERT | HEX | high | unsigned long | - | - | - | - | - | Systemzeit des letzten erfolgreichen Anlernens (Werk BMW oder Feld) |
| STAT_TIMESTAMP_FIRST_UNLOCK_WERT | HEX | high | unsigned long | - | - | - | - | - | Systemzeit des ersten erfolgreichen UNLOCK nach dem ersten erfolgreichen Anlernen (Werk BMW) in Sekunden. |
| STAT_RETRY_COUNT_BLOCKING_SC_WERT | HEX | high | unsigned long | - | - | - | - | - | Anzahl Wiederholstrategie bei verspannter Lenksäule |
| STAT_HISTORYSTORAGE_DEL_COUNT_DATA | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | Anzahl Löschvorgänge des UShin Historienspeicher + Systemzeit des letzten erfolgreichen Löschvorganges in Sekunden |
| STAT_UNLOCK_TRIGGER_COUNT_EWS_DATA | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | UNLOCK Trigger bei angelernter, aber nicht authentifizierter EWS. Auch bei gesperrter EWS. Zähler + Systemzeit in Sekunden |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 1/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_1_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 2/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_2_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 3/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_3_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 4/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_4_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 5/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_5_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 6/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_6_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 7/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_7_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 8/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_8_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 9/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_RETRY_WHILE_BLOCKED_SC_9_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 10/10 Wiederholstrategien bei verspannter Lenksäule mit Systemzeit in Sekunden und Kilometerstand. |
| STAT_RINGBUFFER_FAILED_ACTIVATION_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 1/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_1_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 2/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_2_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 3/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_3_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 4/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_4_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 5/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_5_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 6/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_6_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 7/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_7_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 8/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_8_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 9/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_9_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 10/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_10_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 11/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_11_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 12/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_12_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 13/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_13_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 14/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_14_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 15/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_15_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 16/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_16_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 17/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_17_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 18/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_18_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 19/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |
| STAT_RINGBUFFER_FAILED_ACTIVATION_19_DATA | DATA | high | data[23] | - | - | 1.0 | 1.0 | 0.0 | Die letzten 20/20 fehlgeschlagenen Verfahrversuche inkl. Retry (LOCK & UNLOCK) |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 39 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_PWF_MESSEMODUS | 0x102F | - | Dieser RID wird zum Setzden des Messemodus im PWF-Master verwendet. | - | - | - | - | - | - | - | - | - | 31 | ARG_0x102F_R | - |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| STATUS_PWF_MESSEMODUS | 0x2532 | STAT_PWF_MESSEMODUS | Das Result enthält den aktuellen PWF_Messemodus | 0-n | - | High | unsigned char | PWF_MESSEMODUS | - | - | - | - | 22 | - | - |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STEUERN_ELV | 0xA205 | - | Ansteuerung ELV - Verriegelung oder Entriegelung  | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA205_R | RES_0xA205_R |
| ELV_VERRIEGELUNGSSTATUS | 0xD6F6 | STAT_ELV_ZUSTAND | Aktueller Verriegelungs-/Entriegelungszustand der ELV | 0-n | - | High | unsigned char | TAB_ELV_ZUSTAND | - | - | - | - | 22 | - | - |
| ESCAPE_COUNTER | 0xDAF1 | STAT_ESCAPE_COUNTER | Werte von 0 bis 8 möglich.  Dem ELV-ESC ist keine direkte Anzeige einer CCM zu zuordnen. Die Fehlerreaktionen und Anzeige der CCM sind den Fehlerursachen (DTCs) zugeordnet. Bei ELV-ESC = 6 oder 7 darf die ELV nicht mehr verriegelt werden. Bei ELV-ESC größer oder = 8 muss der ELV-Status auf ungültig gesetzt werden. | 0-n | - | High | unsigned char | TAB_ESCAPE_COUNTER | - | - | - | - | 22 | - | - |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| _ELV_CALIBRATION_PROCESS | 0xF781 | - | Routine der automatischen Kalibrierung | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF781_R |
| _SENSOR_EEPROM_READ | 0xF782 | - | Ausleseroutine des Sensorspeichers (EEPROM) | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF782_R |
| _SENSOR_EEPROM_DATA_WRITE | 0xF785 | - | Schreibroutine des Sensorspeichers (EEPROM) | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF785_R | RES_0xF785_R |
| _SENSOR_MEMORY_DATA_READ | 0xF788 | - | Auslesevorgang des Sensorspeichers (RAM,ROM,EEPROM) | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF788_R | RES_0xF788_R |
| _ELV_MEM_INIT_PROCESS | 0xF789 | - | Startet die Routine der Initialisierung noch nicht initialisierter Speicherblöcke. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF789_R | RES_0xF789_R |
| _ELV_PROD_DATA_WRITE | 0xF78A | - | Produktionsdaten bei UShin schreiben | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF78A_R | RES_0xF78A_R |
| _USHIN_HISTORYSTORAGE_CLEAR | 0xF78B | - | Löscht den Inhalt des Historienspeichers und inkrementiert den Löschzähler. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF78B_R | RES_0xF78B_R |
| _ELV_CALIBRATION_PROCESS_RESULT | 0xFD00 | STAT_ELV_CALIBRATION_STATUS | Status der aktuellen Kalibrierung | 0-n | ELV_StatTableCal | High | unsigned char | STAT_TABLE_CALIBRATION | - | - | - | - | 22 | - | - |
| _ELV_PROCESS_STEP | 0xFD01 | - | Prozess-Schritte bei UShin | - | ECU_ProcessStep | - | - | - | - | - | - | - | 2E;22 | ARG_0xFD01_D | RES_0xFD01_D |
| _PCBA_PROCESS_STEP | 0xFD02 | - | erfolgreich abgeschlossenen Prozessschritte bei der Platinenherstellung | - | PCBA_ProcessStepTab | - | - | - | - | - | - | - | 22;2E | ARG_0xFD02_D | RES_0xFD02_D |
| _PCBA_PROD_DATA | 0xFD03 | - | Produktionsdaten des PCBA Herstellers | - | - | - | - | - | - | - | - | - | 2E | ARG_0xFD03_D | - |
| _PCBA_PROD_DATA_READ | 0xFD04 | - | Liest die Produktionsdaten der ELV aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD04_D |
| _ELV_TGS_DATA | 0xFD05 | - | Teilegenerationsstand bei UShin | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xFD05_D | RES_0xFD05_D |
| _ELV_SERIAL_NUMBER | 0xFD06 | - | UShin Seriennmmer | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xFD06_D | RES_0xFD06_D |
| _SENSOR_MEMORY_DATA_READ_RESULT | 0xFD07 | - | Speicher Daten des Hall Sensors | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD07_D |
| _SENSOR_EEPROM_READ_RESULT | 0xFD08 | - | Liefert den Status und Rückgabewerte des Auslesevorganges des Sensorspeichers (EEPROM) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD08_D |
| _ELV_ROTATION_ANGLE | 0xFD09 | - | Aktuelle Drehwinkelinformationen des Sensors | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD09_D |
| _ELV_MOVEMENT_PARAMETER | 0xFD0A | - | Parameter für die Motoransteuerung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD0A_D |
| _ELV_PROD_DATA_READ | 0xFD0F | - | Produktionsdaten bei UShin lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD0F_D |
| _ELV_CALIBRATION_VALUE | 0xFD10 | - | Korrekturwert für die Sensorwerte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD10_D |
| _ELV_VK_READ | 0xFD11 | - | Alle Herstellinformationen der ELV | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD11_D |
| _SENSOR_EEPROM_DATA_WRITE_RESULT | 0xFD12 | STAT_SENSOR_PROC | Status des Auslesevorganges | 0-n | SENSOR_StatTabReadEE | High | unsigned char | STAT_TAB_SENSOR_READ_MEMORY | - | - | - | - | 22 | - | - |
| _SENSOR_INFO_DATA_READ | 0xFD13 | - | detaillierte Informationen vom Hall-Sensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD13_D |
| _ELV_MEM_DATA_WRITE | 0xFD16 | - | dedizierte Daten, die geschrieben werden sollen | - | - | - | - | - | - | - | - | - | 2E | ARG_0xFD16_D | - |
| _PCBA_PROD_DATE_READ | 0xFD17 | STAT_PCBA_PROD_DATE_DATA | Herstelldatum der PCBA | DATA | PCBA_ManufactoringDate | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _ELV_MEM_INIT_RESULT | 0xFD18 | STAT_INIT_MEM_RESULT | Ergebnis der Speicherinitialisierung | 0-n | ELV_InitMemResultTab | High | unsigned char | TAB_MEM_INIT_RESULT | - | - | - | - | 22 | - | - |
| _ELV_BMW_SACHNUMMER | 0xFD19 | - | BMW Sachnummer | - | ELV_BMWSachnummer | - | - | - | - | - | - | - | 22;2E | ARG_0xFD19_D | RES_0xFD19_D |
| _ELV_LOCK_CYCLE_COUNT | 0xFD1A | STAT_CYCLE_COUNT_WERT | Rückgabe der Anzahl ausgeführter Verriegelungszyklen seid Produktion | HEX | ELV_LockCycleCount | High | unsigned int | - | - | - | - | - | 22 | - | - |
| _USHIN_HISTORYSTORAGE_READ_RESULT | 0xFD1B | - | Liest den gesamten Speicherbereich der Historiendaten aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD1B_D |

<a id="table-states-of-job"></a>
### STATES_OF_JOB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | OK |
| 2 | NOK (bei nicht kalibriertem Sensor) |
| 0xFF | Wert ungültig |

<a id="table-stat-table-calibration"></a>
### STAT_TABLE_CALIBRATION

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Die Kalibrierung wurde erfolgreich durchgeführt. OK |
| 0x02 | Die ELV ist an ein BDC angelernt. Bitte erst das angelernte BDC 'entlernen'. Keine Kalibrieung möglich. |
| 0x03 | Es ist eine zu hohe/niedrige Eingangsspannung festgestellt worden. Bitte korrigieren Sie den Wert der Spannung auf 12V +/-100mv. Es ist keine Kalibrierung möglich. |
| 0x04 | Der Sensor hat während der Kalibrierung einen Fehler gemeldet.  Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x05 | Die H-Brückendiagnose hat während der Kalibrierung einen Fehler gemeldet. Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x06 | Der Sensor hat keine plausiblen Werte geliefert.  Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x07 | Die Kalibrierinformationen befinden sich nicht im erwarteten Bereich. Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x08 | Die Kalibrierinformationen konnten nicht gespeichert werden. Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x09 | Es ist ein unerwarteter Timeout beim Kalibrieren aufgetreten.  Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x0A | Der Kalibriervorgang ist noch in Ausführung. Bitte warten bis Vorgang abgeschlossen ist. |
| 0x0B | Die LOCK-Bedingungen (Konditions) wurden nicht erkannt.  Kalibrierung abgebrochen. Bitte wiederholen. |
| 0x0C | Bei der Kalibrierung wuede der min. Verfahrweg von 300° nicht eingehalten. Kalibrierung abgebrochen. Bitte wiederholen. |
| 0xEE | Es ist ein unbekannter Fehler aufgetreten. Kalibrierung abgebrochen. Bitte wiederholen. |
| 0xFF | Wert ungültig |

<a id="table-stat-tab-sensor-read"></a>
### STAT_TAB_SENSOR_READ

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Vorgang in Arbeit |
| 0x02 | Fertig, iO |
| 0x04 | Fehler beim Auslesen des Sensor EEPROMs. Sensor meldet fehler. |
| 0x08 | Fehler beim Auslesen des Sensor EEPROMs. Kommunikationsfehler Sensor |
| 0x10 | Fehler beim Auslesen des Sensor EEPROMs. Main uC meldet fehler |
| 0x20 | falscher Addressbereich erkannt |
| 0x40 | falsche Bytelaenge der Adresse erkannt |
| 0xFF | Wert ungültig |

<a id="table-stat-tab-sensor-read-memory"></a>
### STAT_TAB_SENSOR_READ_MEMORY

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | iO, keine Fehler |
| 0x02 | Main uC, Verarbeitungsfehler |
| 0x03 | Main/Sensor, Kommunikationsfehler |
| 0x04 | Sensorfehler, Schreiben/Löschen des Speichers fehlgeschlagen |
| 0x05 | Sensorfehler, schreiben/löschen des CRC fehlgeschlagen |
| 0x06 | Sensorfehler, Key für Speicherzelle ungültig |
| 0x07 | Sensorfehler, Challenge fehlgeschlagen |
| 0x08 | Sensorfehler, ungerade Adresse erkannt |
| 0xFF | Wert ungültig |

<a id="table-stat-tab-sensor-write"></a>
### STAT_TAB_SENSOR_WRITE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Vorgang noch nicht abgeschlossen. Bitte warten |
| 0x02 | Vorgang abgeschlossen. iO |
| 0x04 | Sensor meldet Fehler, niO |
| 0x08 | Kommunikationsfehler, niO |
| 0x10 | Main uC meldet Fehler, niO |
| 0xFF | Wert ungültig |

<a id="table-tab-calibration-stauts"></a>
### TAB_CALIBRATION_STAUTS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kalibrierung erfolgreich angestoßen |
| 0x0E | Unbekannter Fehler |
| 0xFF | Wert nicht gültig |

<a id="table-tab-elv-ausfuehrungsstatus"></a>
### TAB_ELV_AUSFUEHRUNGSSTATUS

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Erfolgreich verfahren / kein Fehler aufgetreten |
| 1 | Fahrzeug nicht im stillstandnahen Bereich |
| 2 | Ungültiger / Unzulässiger PWF-Zustand |
| 3 | Keine Funktionsfreigabe aufgrund fehlender EWS-Freigabe |
| 4 | Verspannte Lenksäule |
| 5 | Verriegelung gerade im Gange |
| 6 | Entriegelung gerade im Gange |
| 7 | Keine Funktionsfreigabe aufgrund Escape-Counter |
| 8 | Spannungsbedingungen nicht erfüllt |
| 9 | Hardware-Fehler |
| 10 | Unbekannter ELV-Fehler |
| 255 | Wert ungültig |

<a id="table-tab-elv-calibrationstatus"></a>
### TAB_ELV_CALIBRATIONSTATUS

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Calibration successful |

<a id="table-tab-elv-clear-history"></a>
### TAB_ELV_CLEAR_HISTORY

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x95 | Löscht den Inhalt des Historienspeichers. Löscht nicht den Löschzähler sonder inkrementiert diesen. |
| 0x6A | Setzt den Löschzähler des Historienspeichers zurück |

<a id="table-tab-elv-clear-history-process"></a>
### TAB_ELV_CLEAR_HISTORY_PROCESS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Löschen des Historienspeichers erfolgreich abgeschlossen |
| 0x02 | Es konnten nicht alle Einträge des Historienspeichers gelöscht werden. Bitte wiederholen Sie den Vorgang. |
| 0x04 | Es ist ein Timeout beim Löschen des Historienspeichers aufgetreten. Bitte wiederholen Sie den Vorgang |
| 0xFF | Wert ungültig |

<a id="table-tab-elv-mem-init"></a>
### TAB_ELV_MEM_INIT

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x69 | Starten der Initialisieung |

<a id="table-tab-elv-proc-step"></a>
### TAB_ELV_PROC_STEP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x22 | EOL passed |
| 0x44 | SCR passed |
| 0x66 | EOL & SCR passed |
| 0xFF | Wert ungültig |

<a id="table-tab-elv-prod-step"></a>
### TAB_ELV_PROD_STEP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x22 | EOL passed, OK |
| 0x44 | Screening passed, OK |

<a id="table-tab-elv-reset-stat"></a>
### TAB_ELV_RESET_STAT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | fertig, iO |
| 2 | in Bearbeitung, bitte warten |
| 3 | Fehler beim Speichern. Der Wert konnte nicht geändert werden |
| 0xFF | Wert ungültig |

<a id="table-tab-elv-serialnumber-write"></a>
### TAB_ELV_SERIALNUMBER_WRITE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x5A | JA |
| 0xFF | Wert ungültig |

<a id="table-tab-elv-zustand"></a>
### TAB_ELV_ZUSTAND

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Entriegelt |
| 1 | Verriegelungsvorgang aktiv |
| 2 | Verriegelt |
| 3 | Entriegelungsvorgang aktiv |
| 13 | Unplausibler Zustand - nicht sicher bestimmbar |
| 14 | Sicherheitskritscher Fehler erkannt |
| 15 | Initialisierungs-Zustand beim Hochstarten |
| 0xFF | Wert ungültig |

<a id="table-tab-endzustand"></a>
### TAB_ENDZUSTAND

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | ELV verriegelt |
| 0x02 | ELV entriegelt |
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

<a id="table-tab-escape-counter"></a>
### TAB_ESCAPE_COUNTER

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xF0 | Zähler = 0 |
| 0xE1 | Zähler = 1 |
| 0xD2 | Zähler = 2 |
| 0xC3 | Zähler = 3 |
| 0xB4 | Zähler = 4 |
| 0xA5 | Zähler = 5 |
| 0x96 | Zähler = 6, ELV darf nicht mehr verriegelt werden |
| 0x87 | Zähler = 7, ELV darf nicht mehr verriegelt werden |
| 0x78 | Zähler = 8, ELV legt Fahrzeug still |
| 0xFF | Ungültig |

<a id="table-tab-ews-client-auth"></a>
### TAB_EWS_CLIENT_AUTH

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Freigabe (noch) nicht erteilt (noch nicht versucht, oder Kommunikation gestört) |
| 1 | Freigabe erteilt (Authentisierung erfolgreich) |
| 2 | Freigabe abgelehnt (Authentisierung fehlgeschlagen) |
| 0xFF | Wert ungültig |

<a id="table-tab-ews-client-locked"></a>
### TAB_EWS_CLIENT_LOCKED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht angelernt |
| 1 | angelernt und verriegelt |
| 0xFF | Wert ungültig |

<a id="table-tab-ews-dh-status"></a>
### TAB_EWS_DH_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DH-Abgleich läuft nicht |
| 1 | DH-Abgleich läuft gerade |
| 0xFF | Wert ungültig |

<a id="table-tab-ews-mode-arg"></a>
### TAB_EWS_MODE_ARG

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 17 | UNLOCK_CLIENT |

<a id="table-tab-ews-version"></a>
### TAB_EWS_VERSION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x23 | EWS6 mit DH |
| 0x24 | EWS6 mit DH-E |
| 0xFF | Wert ungültig |

<a id="table-tab-mem-init-result"></a>
### TAB_MEM_INIT_RESULT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Vorgang noch nicht abgeschlossen. Bitte warten ... |
| 0x02 | Vorgang abgeschlossen, keine Fehler. iO |
| 0x04 | Fehler bei der Initialisierung, niO |
| 0xFF | Wert ungültig |

<a id="table-tab-pcba-prod-step"></a>
### TAB_PCBA_PROD_STEP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x11 | All Tests passed |
| 0x00 | No Tests passed |
| 0xFF | Wert ungültig |

<a id="table-tab-proc-step"></a>
### TAB_PROC_STEP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x22 | EOL passed |
| 0x44 | SCR passed |

<a id="table-tab-prod-data-write-process"></a>
### TAB_PROD_DATA_WRITE_PROCESS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Prozess erfolgreich beendet |
| 0x02 | Prozess nicht erfolgreich beendet. FEHLER. Daten wurden nicht geschrieben. |
| 0xFF | Wert ungültig |

<a id="table-tab-prod-step"></a>
### TAB_PROD_STEP

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x11 | alle Tests bestanden |

<a id="table-tab-prozessschritt"></a>
### TAB_PROZESSSCHRITT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Prozesschritt 1 durchgeführt (IMI) |
| 0x02 | Prozesschritt 2 durchgeführt (U-SHIN) |
| 0x03 | Prozesschritt 2 durchgeführt (ZF) |

<a id="table-tab-pwf-zustand"></a>
### TAB_PWF_ZUSTAND

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fahren |
| 0x01 | Wohnen |
| 0x02 | Parken |
| 0x03 | Prüfen Analyse Diagnose |
| 0x04 | Parken BN niO |
| 0x05 | Parken BN iO |
| 0x06 | Standfunktion Kunde nicht im Fahrzeug |
| 0x07 | Fahrbereitschaft herstellen |
| 0x08 | Fahrbereitschaft beenden |
| 0xFF | Wert ungültig |

<a id="table-tab-serial-number-and-ai"></a>
### TAB_SERIAL_NUMBER_AND_AI

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 2048 | Serial number (0-2048) |
| 32 | AI number |
| 0xFFFF | Wert ungültig |

<a id="table-tab-status-elv-kalibrierung"></a>
### TAB_STATUS_ELV_KALIBRIERUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kalibrierung OK |
| 0x01 | Kalibrierung NOK |
| 0x02 | Kalibrierung in Progress |
| 0xFF | Wert ungültig |

<a id="table-tab-status-laden-hochspannung-powermanagement"></a>
### TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Anforderung |
| 0x01 | Energiemangel im Hochvoltspeicher |
| 0x02 | Abbruch wegen HV-Fehler |
| 0x04 | Abbruch wegen DCDC-Ausfall |
| 0x08 | Zyklisches Nachladen beendet durch Laden |
| 0x20 | nächster zyklischer Ladevorgang möglich |
| 0x30 | nächster zyklischer Ladevorgang nicht mehr möglich |
| 0xFF | Wert ungültig |

<a id="table-tab-status-spannungseinbruch"></a>
### TAB_STATUS_SPANNUNGSEINBRUCH

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Spannungseinbruch |
| 1 | Startspannungseinbruch bis maximal Spannungsschwelle 1 |
| 2 | Startspannungseinbruch bis maximal Spannungsschwelle 2 |
| 13 | Funktionsschnittstelle ist nicht verfuegbar |
| 14 | Reserviert |
| 15 | Signal unbefuellt |
| 0xFF | Wert ungültig |

<a id="table-tab-status-verbrennungsmotor-antrieb"></a>
### TAB_STATUS_VERBRENNUNGSMOTOR_ANTRIEB

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Motor steht |
| 1 | Motor startet |
| 2 | Motor läuft |
| 13 | Funktionsschnittstelle ist nicht verfuegbar |
| 14 | Reserviert |
| 15 | Signal_unbefuellt |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-elv-mem-reset-val"></a>
### TAB_STAT_ELV_MEM_RESET_VAL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x11 | UShin_Process_Step_Value |
| 0x22 | IMI_Process_Step_Value |
| 0xCC | Calibration_Vaule_Invalid |

<a id="table-tab-stat-sensors-read"></a>
### TAB_STAT_SENSORS_READ

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | iO, kein Fehler |
| 0x02 | Main uC, Verarbeitungsfehler |
| 0x03 | Main/Sensor, Kommunikationsfehler |
| 0x04 | Sensor, Speicherzugriff Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-sensor-read-val"></a>
### TAB_STAT_SENSOR_READ_VAL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | fertig, in Ordnug |
| 2 | in Bearbeitung, bitte warten |
| 3 | Es ist ein Fehler beim Lesen aufgetreten. Wert steht nicht zur Verfügung |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-write-data"></a>
### TAB_STAT_WRITE_DATA

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | ferting, i.O. |
| 2 | in Bearbeitung |
| 3 | Fehler beim Schreiben, Wert nicht rückgesetzt |

<a id="table-tab-steuern-elv-arg"></a>
### TAB_STEUERN_ELV_ARG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | UNLOCK |
| 1 | LOCK |

<a id="table-tab-verfahrart"></a>
### TAB_VERFAHRART

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | ELV soll verriegeln |
| 0x02 | ELV soll  entriegeln |
| 0xFF | Wert ungültig |

<a id="table-tab-verfahr-fehler"></a>
### TAB_VERFAHR_FEHLER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Lenksäule verklemmt |
| 0x01 | Keine EWS Authentisierung |
| 0x02 | FuSi seitiger Fehler (Qualifier inkorrekt, nicht im stillstandsnahen Bereich) |
| 0x03 | Entriegellungsbedingung nicht gegeben (Bei triggerung durch Diagnosejob) |
| 0xFF | Wert ungültig |

<a id="table-tab-verfahr-trigger"></a>
### TAB_VERFAHR_TRIGGER

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ansteuerung über Diagnosebefehl ELV-VR |
| 0x01 | Fahrertür länger als 2 Sekunden offen |
| 0x02 | ZV-Sichern |
| 0x03 | Ansteuerung über Diagnosebefehl ELV-ER |
| 0x04 | Schlüssel im Innenraum gefunden |
| 0xFF | Wert ungültig |

<a id="table-tab-write-eeprom-sta"></a>
### TAB_WRITE_EEPROM_STA

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | OK |
| 1 | NOK |
| 2 | PENDING |
| 0xFF | Wert ungültig |

<a id="table-tab-0x2951"></a>
### TAB_0X2951

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x0001 |

<a id="table-tab-0x505a"></a>
### TAB_0X505A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0024 | 0x0025 | 0x0026 | 0x0027 |

<a id="table-tab-0x505b"></a>
### TAB_0X505B

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0020 | 0x0021 | 0x0022 | 0x0023 |

<a id="table-tab-0x505c"></a>
### TAB_0X505C

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0029 | 0x002A |

<a id="table-tab-0x5060"></a>
### TAB_0X5060

Dimensions: 1 rows × 14 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13 | 0x0002 | 0x0003 | 0x0004 | 0x0005 | 0x0006 | 0x0007 | 0x0008 | 0x0009 | 0x000A | 0x000B | 0x000C | 0x000D | 0x000E |

<a id="table-tab-0x5061"></a>
### TAB_0X5061

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x000F | 0x0010 | 0x0011 | 0x0012 | 0x0013 | 0x0014 |

<a id="table-tab-0x5062"></a>
### TAB_0X5062

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x0028 |

<a id="table-tab-0x5063"></a>
### TAB_0X5063

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0015 | 0x0016 | 0x0017 | 0x0018 |

<a id="table-tab-0x5064"></a>
### TAB_0X5064

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0019 | 0x001A | 0x001B | 0x001C | 0x001D | 0x001E | 0x001F |
