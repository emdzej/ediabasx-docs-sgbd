# FLM01_R.prg

- Jobs: [30](#jobs)
- Tables: [120](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Frontlichtmodul rechts |
| ORIGIN | BMW EK-532 Florian_HIRTH |
| REVISION | 7.200 |
| AUTHOR | Automotive_Lighting ALDE-RT/EEG4 Cihan_KEDIKLI |
| COMMENT | - |
| PACKAGE | 1.995 |
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
| F_UW_KM_SUPREME | string | Umweltbedingung Kilometerstand metergenau (31 Bit) Wertebereich: 0 - 16777215 km |
| F_UW_KM_SUPREME_INSYNC | unsigned char | Environmental condition mileage (long, LSb 1 Bit) 0 == out of sync, 1 == insync |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_ZEIT_MS | int | Umweltbedingung Zeit Millisekundenanteil Genauigkeit: in 5ms-Schritten -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_ZEIT_SUPREME | string | Umweltbedingung Absolute Zeit mit Sekundenbruchteilen Genauigkeit: in 5ms-Schritten wenn Zeit nicht zur Verfuegung steht "No time received" |
| F_UW_ZEIT_SUPREME_INSYNC | unsigned char | Environmental condition system time (Bit0) 0 == out of sync, 1 == insync |
| F_UW_ZEIT_SUPREME_SYNCMETHOD | unsigned char | Environmental condition system time (Bit1 und Bit2) 00 == Kombizeit, 01 == DMCS, 10 == IEEE802.1AS, 11 == invalid |
| F_UW_ZEIT_SUPREME_SYNCMETHOD_INFO | string | Environmental condition system time (Bit1 und Bit2) table: 0 == Kombizeit, 1 == DMCS, 2 == IEEE802.1AS, 3 == invalid |
| F_UW_ZEIT_SUPREME_USER_INFORMATION | string | Environmental condition system time (Bit0, Bit1 und Bit2) TAB_ZEIT_USER_INFO |
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
| F_UW_KM_SUPREME | string | Umweltbedingung Kilometerstand metergenau (31 Bit) Wertebereich: 0 - 16777215 km |
| F_UW_KM_SUPREME_INSYNC | unsigned char | Environmental condition mileage (long, LSb 1 Bit) 0 == out of sync, 1 == insync |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_ZEIT_MS | int | Umweltbedingung Zeit Millisekundenanteil Genauigkeit: in 5ms-Schritten -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_ZEIT_SUPREME | string | Umweltbedingung Absolute Zeit mit Sekundenbruchteilen Genauigkeit: in 5ms-Schritten wenn Zeit nicht zur Verfuegung steht "No time received" |
| F_UW_ZEIT_SUPREME_INSYNC | unsigned char | Environmental condition system time (Bit0) 0 == out of sync, 1 == insync |
| F_UW_ZEIT_SUPREME_SYNCMETHOD | unsigned char | Environmental condition system time (Bit1 und Bit2) 00 == Kombizeit, 01 == DMCS, 10 == IEEE802.1AS, 11 == invalid |
| F_UW_ZEIT_SUPREME_SYNCMETHOD_INFO | string | Environmental condition system time (Bit1 und Bit2) table: 0 == Kombizeit, 1 == DMCS, 2 == IEEE802.1AS, 3 == invalid |
| F_UW_ZEIT_SUPREME_USER_INFORMATION | string | Environmental condition system time (Bit0, Bit1 und Bit2) TAB_ZEIT_USER_INFO |
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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (154 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (9 × 9)
- [TAB_ZEIT_SYNCMETHOD](#table-tab-zeit-syncmethod) (4 × 2)
- [TAB_ZEIT_USER_INFO](#table-tab-zeit-user-info) (8 × 2)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0X3000_R](#table-arg-0x3000-r) (24 × 14)
- [ARG_0XA543_R](#table-arg-0xa543-r) (1 × 14)
- [ARG_0XA545_R](#table-arg-0xa545-r) (2 × 14)
- [ARG_0XA546_R](#table-arg-0xa546-r) (2 × 14)
- [ARG_0XA547_R](#table-arg-0xa547-r) (2 × 14)
- [ARG_0XD1FD_D](#table-arg-0xd1fd-d) (1 × 12)
- [ARG_0XD1FE_D](#table-arg-0xd1fe-d) (1 × 12)
- [ARG_0XD506_D](#table-arg-0xd506-d) (1 × 12)
- [ARG_0XD633_D](#table-arg-0xd633-d) (1 × 12)
- [ARG_0XD634_D](#table-arg-0xd634-d) (2 × 12)
- [ARG_0XD63C_D](#table-arg-0xd63c-d) (1 × 12)
- [ARG_0XD63D_D](#table-arg-0xd63d-d) (1 × 12)
- [ARG_0XD680_D](#table-arg-0xd680-d) (1 × 12)
- [ARG_0XDF0F_D](#table-arg-0xdf0f-d) (1 × 12)
- [ARG_0XE2F6_D](#table-arg-0xe2f6-d) (2 × 12)
- [ARG_0XE34C_D](#table-arg-0xe34c-d) (1 × 12)
- [ARG_0XFD40_D](#table-arg-0xfd40-d) (1 × 12)
- [ARG_0XFD58_D](#table-arg-0xfd58-d) (1 × 12)
- [BF_SCHEINWERFERINFO_STRUCT](#table-bf-scheinwerferinfo-struct) (2 × 10)
- [BF_VERSIONSINFO_STRUCT](#table-bf-versionsinfo-struct) (2 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FAHRZEUGVARIANTE](#table-fahrzeugvariante) (31 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (182 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (128 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (6 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [LENKERVERSION](#table-lenkerversion) (2 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X3000_R](#table-res-0x3000-r) (25 × 13)
- [RES_0XA538_R](#table-res-0xa538-r) (1 × 13)
- [RES_0XA541_R](#table-res-0xa541-r) (1 × 13)
- [RES_0XA543_R](#table-res-0xa543-r) (2 × 13)
- [RES_0XA545_R](#table-res-0xa545-r) (2 × 13)
- [RES_0XA546_R](#table-res-0xa546-r) (2 × 13)
- [RES_0XA547_R](#table-res-0xa547-r) (2 × 13)
- [RES_0XA548_R](#table-res-0xa548-r) (18 × 13)
- [RES_0XA5A7_R](#table-res-0xa5a7-r) (1 × 13)
- [RES_0XA801_D](#table-res-0xa801-d) (101 × 10)
- [RES_0XD1FD_D](#table-res-0xd1fd-d) (2 × 10)
- [RES_0XD1FE_D](#table-res-0xd1fe-d) (2 × 10)
- [RES_0XD506_D](#table-res-0xd506-d) (12 × 10)
- [RES_0XD529_D](#table-res-0xd529-d) (15 × 10)
- [RES_0XD630_D](#table-res-0xd630-d) (20 × 10)
- [RES_0XD632_D](#table-res-0xd632-d) (48 × 10)
- [RES_0XD634_D](#table-res-0xd634-d) (15 × 10)
- [RES_0XD635_D](#table-res-0xd635-d) (2 × 10)
- [RES_0XD636_D](#table-res-0xd636-d) (2 × 10)
- [RES_0XD638_D](#table-res-0xd638-d) (24 × 10)
- [RES_0XD639_D](#table-res-0xd639-d) (5 × 10)
- [RES_0XD63A_D](#table-res-0xd63a-d) (26 × 10)
- [RES_0XD63C_D](#table-res-0xd63c-d) (2 × 10)
- [RES_0XD63D_D](#table-res-0xd63d-d) (3 × 10)
- [RES_0XD63E_D](#table-res-0xd63e-d) (3 × 10)
- [RES_0XD662_D](#table-res-0xd662-d) (2 × 10)
- [RES_0XD667_D](#table-res-0xd667-d) (24 × 10)
- [RES_0XD680_D](#table-res-0xd680-d) (3 × 10)
- [RES_0XDCA0_D](#table-res-0xdca0-d) (2 × 10)
- [RES_0XDF0F_D](#table-res-0xdf0f-d) (6 × 10)
- [RES_0XE2F6_D](#table-res-0xe2f6-d) (14 × 10)
- [RES_0XFD40_D](#table-res-0xfd40-d) (1 × 10)
- [RES_0XFD41_D](#table-res-0xfd41-d) (12 × 10)
- [RES_0XFD43_D](#table-res-0xfd43-d) (2 × 10)
- [RES_0XFD44_D](#table-res-0xfd44-d) (37 × 10)
- [RES_0XFD47_D](#table-res-0xfd47-d) (35 × 10)
- [RES_0XFD48_D](#table-res-0xfd48-d) (36 × 10)
- [RES_0XFD4A_D](#table-res-0xfd4a-d) (41 × 10)
- [RES_0XFD4B_D](#table-res-0xfd4b-d) (41 × 10)
- [RES_0XFD4C_D](#table-res-0xfd4c-d) (41 × 10)
- [RES_0XFD4D_D](#table-res-0xfd4d-d) (41 × 10)
- [RES_0XFD4E_D](#table-res-0xfd4e-d) (41 × 10)
- [RES_0XFD4F_D](#table-res-0xfd4f-d) (41 × 10)
- [RES_0XFD50_D](#table-res-0xfd50-d) (10 × 10)
- [RES_0XFD51_D](#table-res-0xfd51-d) (10 × 10)
- [RES_0XFD52_D](#table-res-0xfd52-d) (30 × 10)
- [RES_0XFD53_D](#table-res-0xfd53-d) (30 × 10)
- [RES_0XFD54_D](#table-res-0xfd54-d) (17 × 10)
- [RES_0XFD55_D](#table-res-0xfd55-d) (3 × 10)
- [RES_0XFD56_D](#table-res-0xfd56-d) (3 × 10)
- [RES_0XFD58_D](#table-res-0xfd58-d) (24 × 10)
- [RES_0XFD5A_D](#table-res-0xfd5a-d) (4 × 10)
- [RES_0XFD5B_D](#table-res-0xfd5b-d) (25 × 10)
- [SCHEINWERFERHERSTELLER](#table-scheinwerferhersteller) (4 × 2)
- [SCHEINWERFERVARIANTE](#table-scheinwerfervariante) (12 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (66 × 16)
- [TAB_AHL_REFERENZLAUF](#table-tab-ahl-referenzlauf) (5 × 2)
- [TAB_EINLERNDATEN_NVM_STATUS](#table-tab-einlerndaten-nvm-status) (5 × 2)
- [TAB_EINLERNDATEN_STATUS](#table-tab-einlerndaten-status) (3 × 2)
- [TAB_FLE_LEUCHTMITTEL](#table-tab-fle-leuchtmittel) (12 × 2)
- [TAB_FRAZ_MESSUNG](#table-tab-fraz-messung) (3 × 2)
- [TAB_FUNKTION_FLE](#table-tab-funktion-fle) (3 × 2)
- [TAB_GRUND_IMPLAUSIBEL](#table-tab-grund-implausibel) (3 × 2)
- [TAB_LED_LEUCHTMITTEL](#table-tab-led-leuchtmittel) (13 × 2)
- [TAB_LEUCHTEN_SENSOR](#table-tab-leuchten-sensor) (20 × 2)
- [TAB_LEUCHTMITTEL](#table-tab-leuchtmittel) (21 × 2)
- [TAB_LR_AKTIVE_LICHTFUNKTION](#table-tab-lr-aktive-lichtfunktion) (4 × 2)
- [TAB_LR_STATUS](#table-tab-lr-status) (4 × 2)
- [TAB_LWR_REFERENZLAUF](#table-tab-lwr-referenzlauf) (5 × 2)
- [TAB_POS_AHL](#table-tab-pos-ahl) (4 × 2)
- [TAB_POS_LWR](#table-tab-pos-lwr) (4 × 2)
- [TAB_WECKEREIGNIS](#table-tab-weckereignis) (7 × 2)

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

Dimensions: 154 rows × 2 columns

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
| 0x0000CB | A123 Systems |
| 0x0000CC | ZADI |
| 0x0000CD | speedsignal GmbH |
| 0x0000CE | Eldor Corporation |
| 0x0000CF | Delta Electronics Inc. |
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

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0x1750 | PWF_Basinetz | 0-n | - | 0xFF | - | 1 | 1 | 0.000000 |
| 0x1751 | PWF_Teilnetz | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1768 | KM_STAND_SUP | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1769 | ABS_ZEIT_SUP | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0xFFFF | IDENTIFIER_UNKNOWN | - | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |

<a id="table-tab-zeit-syncmethod"></a>
### TAB_ZEIT_SYNCMETHOD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Combi-Time |
| 0x01 | DMCS |
| 0x02 | IEEE802.1AS |
| 0x03 | invalid |

<a id="table-tab-zeit-user-info"></a>
### TAB_ZEIT_USER_INFO

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | out of sync, no time available |
| 0x01 | insync, ms ECU overall, not comparable |
| 0x02 | ms ECU overall, not comparable |
| 0x03 | ms ECU overall, comparable |
| 0x04 | ms ECU overall, not comparable |
| 0x05 | ms ECU overall, comparable |
| 0x06 | invalid |
| 0x07 | invalid |

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

<a id="table-arg-0x3000-r"></a>
### ARG_0X3000_R

Dimensions: 24 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 1 |
| STAT_LED_1_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 1 |
| STAT_LED_2_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 2 |
| STAT_LED_2_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 2 |
| STAT_LED_3_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 3 |
| STAT_LED_3_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 3 |
| STAT_LED_4_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 4 |
| STAT_LED_4_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 4 |
| STAT_LED_5_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 5 |
| STAT_LED_5_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 5 |
| STAT_LED_6_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 6 |
| STAT_LED_6_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 6 |
| STAT_LED_7_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 7 |
| STAT_LED_7_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 7 |
| STAT_LED_8_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 8 |
| STAT_LED_8_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 8 |
| STAT_LED_9_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 9 |
| STAT_LED_9_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 9 |
| STAT_LED_10_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 10 |
| STAT_LED_10_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 10 |
| STAT_LED_11_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 11 |
| STAT_LED_11_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 11 |
| STAT_LED_12_STROM_WERT | + | - | mA | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | 0.0 | 1500.0 | Stromwert LED 12 |
| STAT_LED_12_PWM_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Prozent Wert LED 12 |

<a id="table-arg-0xa543-r"></a>
### ARG_0XA543_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | high | unsigned char | - | TAB_LED_LEUCHTMITTEL | - | - | - | - | - | Auswahl des LED Leuchtmittel |

<a id="table-arg-0xa545-r"></a>
### ARG_0XA545_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | + | - | ° | high | signed int | - | - | 10.0 | 1.0 | 0.0 | -25.0 | 25.0 | Vorgabe Winkel, Wertebereich -25,0°  25,0 ° |
| GESCHWINDIGKEIT | + | - | °/s | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | 0.0 | 45.0 | Geschwindigkeit LWR Wertebereich 0-45°/s. |

<a id="table-arg-0xa546-r"></a>
### ARG_0XA546_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | + | - | ° | high | signed int | - | - | 10.0 | 1.0 | 0.0 | -25.0 | 25.0 | Vorgabe Winkel, Wertebereich -25,0° bis 25,0 ° |
| GESCHWINDIGKEIT | + | - | °/s | high | unsigned int | - | - | 10.0 | 1.0 | 0.0 | 0.0 | 45.0 | Geschwindigkeit AHL Wertebereich: 0-45°/s |

<a id="table-arg-0xa547-r"></a>
### ARG_0XA547_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PWM_LUEFTER_1 | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Vorgabe PWM für Lüfter in Prozent |
| STAT_PWM_LUEFTER_2 | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Vorgabe PWM für Lüfter in Prozent |

<a id="table-arg-0xd1fd-d"></a>
### ARG_0XD1FD_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Loeschen JA/NEIN |

<a id="table-arg-0xd1fe-d"></a>
### ARG_0XD1FE_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Loeschen JA/NEIN |

<a id="table-arg-0xd506-d"></a>
### ARG_0XD506_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1... Einlerndaten zurücksetzten 0...keine Aktion |

<a id="table-arg-0xd633-d"></a>
### ARG_0XD633_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...löschen des Statistikzählers 0...keine Aktion |

<a id="table-arg-0xd634-d"></a>
### ARG_0XD634_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...löscht Betriebsstundenzähler 0...keine Aktion |
| LEUCHTMITTEL | 0-n | high | unsigned char | - | TAB_FLE_LEUCHTMITTEL | - | - | - | - | - | Auswahl des FLE Leuchtmittels |

<a id="table-arg-0xd63c-d"></a>
### ARG_0XD63C_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...Zähler löschen |

<a id="table-arg-0xd63d-d"></a>
### ARG_0XD63D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...Betriebsdauer zurücksetzen |

<a id="table-arg-0xd680-d"></a>
### ARG_0XD680_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...Betriebsdauer zurücksetzen |

<a id="table-arg-0xdf0f-d"></a>
### ARG_0XDF0F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Zähler löschen: 0 = keine Aktion 1 = Start |

<a id="table-arg-0xe2f6-d"></a>
### ARG_0XE2F6_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DIG_SEITE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00 = eigene Seite 0x01 = Partner-Seite 0x02 .. = unbenutzt |
| DATA_BINNING | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | - | - | Binning-Code eigene Seite |

<a id="table-arg-0xe34c-d"></a>
### ARG_0XE34C_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 1...Zähler löschen |

<a id="table-arg-0xfd40-d"></a>
### ARG_0XFD40_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFERDATENBLOCK_DATA | DATA | high | data[16] | - | - | 1.0 | 1.0 | 0.0 | - | - | Scheinwerferdatenblock |

<a id="table-arg-0xfd58-d"></a>
### ARG_0XFD58_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Werte löschen: 0 = Keine Aktion 1 = Start |

<a id="table-bf-scheinwerferinfo-struct"></a>
### BF_SCHEINWERFERINFO_STRUCT

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFERHERSTELLER | 0-n | high | unsigned char | 0x0F | SCHEINWERFERHERSTELLER | - | - | - | Scheinwerferhersteller Bit 1-4 |
| STAT_SCHEINWERFERVARIANTE | 0-n | high | unsigned char | 0xF0 | SCHEINWERFERVARIANTE | - | - | - | Scheinwerfervariante Bit 5-8 |

<a id="table-bf-versionsinfo-struct"></a>
### BF_VERSIONSINFO_STRUCT

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFER_VERSIONSNUMMER | 0-n | high | unsigned char | 0x1F | - | - | - | - | Scheinwerferversionsnummer Bit 1-5 |
| STAT_FAHRZEUG_LENKERVERSION | 0-n | high | unsigned char | 0x20 | LENKERVERSION | - | - | - | Linkslenker oder Rechtslenker des Fahrzeugs Bit 6  |

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

<a id="table-fahrzeugvariante"></a>
### FAHRZEUGVARIANTE

Dimensions: 31 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | F01-F04 (+LCI) |
| 0x01 | F07 (+LCI) |
| 0x02 | F10/F11/F18 (+LCI) |
| 0x03 | F12/F13 |
| 0x04 | F25 |
| 0x05 | RR4/RR5/RR6 |
| 0x86 | F20/F21 |
| 0x87 | F22/F23 |
| 0x88 | F30/F31/F35 |
| 0x89 | F32/F33/F36 |
| 0x0A | RR01 |
| 0x8B | F34 |
| 0x10 | I01 |
| 0x11 | I12 |
| 0x18 | F56 |
| 0x19 | F45/F46 |
| 0x1B | F47 |
| 0x1C | F48 |
| 0x1D | F54 |
| 0x1E | F55 |
| 0x1F | F57 |
| 0x20 | F15/F16 |
| 0x30 | F52 |
| 0x31 | F60 |
| 0x40 | G11/G12 |
| 0x41 | G30/G31 |
| 0x42 | G01/G02 |
| 0x43 | G32 |
| 0x44 | G38 |
| 0x45 | G08 |
| 0x60 | M13 |

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

Dimensions: 182 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x024400 | Energiesparmode aktiv | 0 | - |
| 0x024408 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x024409 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02440A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02440B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02440C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02440D | Codierung: Codierdaten nicht qualifiziert | 0 | - |
| 0x024423 | Flash Memory Fehler (Sammelfehler) | 0 | - |
| 0x024426 | Hardwarefehler (Sammelfehler) | 0 | - |
| 0x024429 | Softwarefehler (Sammelfehler) | 0 | - |
| 0x02FF44 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x805B00 | Binning 5: Fehler | 0 | - |
| 0x805B01 | NTC 5: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B02 | Abbiegelicht: Kurzschluss nach Masse | 0 | - |
| 0x805B03 | Abbiegelicht: Kurzschluss nach Plus | 0 | - |
| 0x805B04 | NTC 5: Kurzschluss Temperatursensor | 0 | - |
| 0x805B05 | NTC 6: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B06 | Abbiegelicht: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B07 | NTC 6: Kurzschluss Temperatursensor | 0 | - |
| 0x805B08 | Abbiegelicht: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805B09 | Abbiegelicht: Strangunterbrechung | 0 | - |
| 0x805B0A | Binning 1: Fehler | 0 | - |
| 0x805B0B | NTC 7: Kurzschluss Temperatursensor | 0 | - |
| 0x805B0C | Abblendlicht: Kurzschluss nach Masse | 0 | - |
| 0x805B0D | Abblendlicht: Kurzschluss nach Plus | 0 | - |
| 0x805B0E | NTC 1: Kurzschluss Temperatursensor | 0 | - |
| 0x805B0F | NTC 7: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B10 | NTC 1: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B11 | Binning 4: Fehler | 0 | - |
| 0x805B12 | Abblendlicht: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B13 | Abblendlicht: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805B14 | NTC 4: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B15 | Abblendlicht: Strangunterbrechung | 0 | - |
| 0x805B16 | Abblendlicht: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805B17 | Binning 2: Fehler | 0 | - |
| 0x805B18 | Fahrtrichtungsanzeiger: Teilweiser Ausfall der Leuchtmittel | 0 | - |
| 0x805B19 | ZFL2-Sensor Defekt | 0 | - |
| 0x805B1B | NTC 2: Kurzschluss Temperatursensor | 0 | - |
| 0x805B1C | NTC 4: Kurzschluss Temperatursensor | 0 | - |
| 0x805B1D | NTC 2: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B1E | Binning 7: Fehler | 0 | - |
| 0x805B1F | Binning 8: Fehler | 0 | - |
| 0x805B20 | Binning 6: Fehler | 0 | - |
| 0x805B21 | Binning 9: Fehler | 0 | - |
| 0x805B22 | Binning 10: Fehler | 0 | - |
| 0x805B23 | Binning 11: Fehler | 0 | - |
| 0x805B24 | Binning 3: Fehler | 0 | - |
| 0x805B25 | Zusatzfernlicht Laser: Kurzschluss nach Masse | 0 | - |
| 0x805B26 | Fernlicht: Kurzschluss nach Masse | 0 | - |
| 0x805B27 | Fernlicht: Kurzschluss nach Plus | 0 | - |
| 0x805B28 | NTC 3: Kurzschluss Temperatursensor | 0 | - |
| 0x805B29 | Abblendlicht - Aktivierung wegen unplausibler Eingangssignale | 1 | - |
| 0x805B2A | NTC 3: Leitungsunterbrechung Temperatursensor | 0 | - |
| 0x805B2B | Fernlicht: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B2C | Zusatzfernlicht Laser: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805B2D | Fernlicht: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805B2E | Fernlicht: Strangunterbrechung | 0 | - |
| 0x805B2F | Fernlicht: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805B30 | Zusatzfernlicht Laser: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B31 | Lüfter 1: Leitungsunterbrechung | 0 | - |
| 0x805B32 | Lüfter 1: Kurzschluss | 0 | - |
| 0x805B34 | Interner Steuergerätefehler | 0 | - |
| 0x805B35 | Steuergerät: Temperatursensor defekt | 0 | - |
| 0x805B36 | Verbauorterkennung unplausibel | 0 | - |
| 0x805B37 | Unterspannung erkannt | 1 | - |
| 0x805B38 | Überspannung erkannt | 1 | - |
| 0x805B39 | Abbiegelicht: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805B3A | Abblendlicht: Funktion defekt | 0 | - |
| 0x805B3B | Binning 12: Fehler | 0 | - |
| 0x805B3E | Variable Lichtverteilung: Funktion defekt | 0 | - |
| 0x805B41 | Stellmotor Leuchtweitenregulierung: Treiber defekt | 0 | - |
| 0x805B42 | Inszenierungslicht: Kurzschluss nach Masse | 0 | - |
| 0x805B43 | Inszenierungslicht: Kurzschluss nach Plus | 0 | - |
| 0x805B44 | Inszenierungslicht: Strangunterbrechung | 0 | - |
| 0x805B45 | Fahrtrichtungsanzeiger: Funktion defekt | 0 | - |
| 0x805B46 | Lüfter 2: Leitungsunterbrechung | 0 | - |
| 0x805B47 | AHL: Sensorflanke fehlt | 0 | - |
| 0x805B48 | Lüfter 2: Kurzschluss | 0 | - |
| 0x805B49 | Inszenierungslicht: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B4C | Inszenierungslicht: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805B4D | Inszenierungslicht: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805B6D | Seitenmarkierungsleuchte: Funktion defekt | 0 | - |
| 0x805B70 | Fernlicht: Laser Sicherheitsfehler | 0 | - |
| 0x805B71 | Fernlicht:  Laser Sicherheitsverriegelung | 0 | - |
| 0x805B72 | Zusatzfernlicht Laser2: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805B73 | Zusatzfernlicht Laser2: Kurzschluss nach Plus | 0 | - |
| 0x805B74 | Zusatzfernlicht Laser2: Kurzschluss nach Masse | 0 | - |
| 0x805B75 | Zusatzfernlicht Laser2: Strangunterbrechung | 0 | - |
| 0x805B76 | Zusatzfernlicht Laser2: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805B77 | Zusatzfernlicht Laser2: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805BA0 | Zusatzfernlicht Laser: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805BA1 | Zusatzfernlicht Laser: Strangunterbrechung | 0 | - |
| 0x805BA2 | Zusatzfernlicht Laser: Kurzschluss nach Plus | 0 | - |
| 0x805BA4 | ZFL-Sensor 1 ausgelöst oder defekt | 0 | - |
| 0x805BD0 | SW Binning 1: Fehler | 0 | - |
| 0x805BD1 | SW Binning 2: Fehler | 0 | - |
| 0x805BD2 | SW Binning 3: Fehler | 0 | - |
| 0x805BD3 | SW Binning 4: Fehler | 0 | - |
| 0x805BD4 | SW Binning 5: Fehler | 0 | - |
| 0x805BD5 | SW Binning 6: Fehler | 0 | - |
| 0x805BD6 | SW Binning 7: Fehler | 0 | - |
| 0x805BD7 | SW Binning 8: Fehler | 0 | - |
| 0x805BD8 | SW Binning 9: Fehler | 0 | - |
| 0x805BD9 | SW Binning 10: Fehler | 0 | - |
| 0x805BDA | SW Binning 11: Fehler | 0 | - |
| 0x805BDB | SW Binning 12: Fehler | 0 | - |
| 0x805E00 | Fahrtrichtungsanzeiger: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805E01 | Fahrtrichtungsanzeiger: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805E13 | Fahrtrichtungsanzeiger: Kurzschluss nach Masse | 0 | - |
| 0x805E14 | Fahrtrichtungsanzeiger: Kurzschluss nach Plus | 0 | - |
| 0x805E1B | Fahrtrichtungsanzeiger: Strangunterbrechung | 0 | - |
| 0x805E1C | Fahrtrichtungsanzeiger: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805E1E | Fahrtrichtungsanzeiger: Ansteuerung unplausibel | 1 | - |
| 0x805E23 | Seitenmarkierungsleuchte: Kurzschluss nach Masse | 0 | - |
| 0x805E24 | Seitenmarkierungsleuchte: Kurzschluss nach Plus | 0 | - |
| 0x805E2B | Seitenmarkierungsleuchte: Strangunterbrechung | 0 | - |
| 0x805E2C | Seitenmarkierungsleuchte: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805E32 | Tagfahrlicht: Funktion defekt | 0 | - |
| 0x805E34 | Tagfahrlicht: Kurzschluss nach Masse | 0 | - |
| 0x805E35 | Tagfahrlicht: Kurzschluss nach Plus | 0 | - |
| 0x805E3C | Tagfahrlicht: Strangunterbrechung | 0 | - |
| 0x805E3D | Tagfahrlicht: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x805E4A | Stellmotor Kurvenlicht: Kurzschluss oder Leitungsunterbrechung an Wicklung 1 | 0 | - |
| 0x805E52 | Stellmotor Kurvenlicht: Übertemperatur (Abschaltung) | 1 | - |
| 0x805E53 | Stellmotor Leuchtweitenregulierung: Kurzschluss oder Leitungsunterbrechung an Wicklung 1 | 0 | - |
| 0x805E5B | Stellmotor Leuchtweitenregulierung: Übertemperatur (Abschaltung) | 1 | - |
| 0x805E5E | Seitenmarkierungsleuchte: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805E5F | Seitenmarkierungsleuchte: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805E60 | Tagfahrlicht: Strangspannung außerhalb Toleranz | 0 | - |
| 0x805E61 | DWA Blinken: Funktion  defekt | 0 | - |
| 0x805E62 | Abbiegelicht: Funktion defekt | 0 | - |
| 0x805E63 | Fernlicht/Lichthupe: Funktion  defekt | 0 | - |
| 0x805E64 | Fernlichtblinken: Funktion defekt | 0 | - |
| 0x805E65 | Follow Me Home: Funktion  defekt | 0 | - |
| 0x805E66 | Panik Blinken: Funktion  defekt | 0 | - |
| 0x805E67 | Parklicht: Funktion defekt | 0 | - |
| 0x805E69 | Remote Light: Funktion  defekt | 0 | - |
| 0x805E6B | Standlicht: Funktion defekt | 0 | - |
| 0x805E6C | Überfallalarm: Funktion defekt | 0 | - |
| 0x805E6E | Welcome Light: Funktion defekt | 0 | - |
| 0x805E6F | Tagfahrlicht: Strangstrom außerhalb Toleranz | 0 | - |
| 0x805E70 | Stellmotor Kurvenlicht: Treiber defekt | 0 | - |
| 0xDA050B | B2-CAN Physikalischer Busfehler | 0 | - |
| 0xDA0514 | B2-CAN Control Module Bus OFF | 0 | - |
| 0xDA0BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xDA1400 | Botschaft 0x1F6 (Blinken): Timeout | 1 | - |
| 0xDA1401 | Botschaft 0x1E4 (CTR_LP_EX_2): Timeout | 1 | - |
| 0xDA1402 | Botschaft 0x2EB (CTR_LP_EX) - Timeout | 1 | - |
| 0xDA1403 | Botschaft 0x1A1 (V_VEH) - Signal QU_V_VEH_COG ungültig | 1 | - |
| 0xDA1404 | Botschaft 0x1E4 (CTR_LP_EX_2): Fehler Alive-Counter | 1 | - |
| 0xDA1408 | Botschaft 0x1A1 (V_VEH) - Timeout | 1 | - |
| 0xDA1409 | Botschaft 0x1A1 (V_VEH) - CRC-Fehler | 1 | - |
| 0xDA140A | Botschaft 0x1A1 (V_VEH) - Fehler Alive-Counter | 1 | - |
| 0xDA140B | Botschaft 0x1A1 (V_VEH) - Signal V_VEH_COG ungültig | 1 | - |
| 0xDA140C | Botschaft 0x3C (CON_VEH) - Timeout | 1 | - |
| 0xDA140D | Botschaft 0x3C (CON_VEH) - CRC-Fehler | 1 | - |
| 0xDA140E | Botschaft 0x3C (CON_VEH) - Fehler Alive-Counter | 1 | - |
| 0xDA140F | Botschaft 0x3C (CON_VEH) - Signal ST_CON_VEH ungültig | 1 | - |
| 0xDA1412 | Botschaft 0x3C (CON_VEH) - Signal QU_ST_CON_VEH ungültig | 1 | - |
| 0xDA14F0 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Timeout | 1 | - |
| 0xDA14F1 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_SPN_ENG_VE ungültig | 1 | - |
| 0xDA14F2 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_V_SPN_VE ungültig | 1 | - |
| 0xDA14F3 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_PO_SPN_VE ungültig | 1 | - |
| 0xDA14F4 | Botschaft 0xE8 (CTR_LP_EX_SPN_HRZTL) - Timeout | 1 | - |
| 0xDA14F5 | Botschaft 0xE8 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_SPN_ENG_HRZTL ungültig | 1 | - |
| 0xDA14F6 | Botschaft 0xE8 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_V_SPN_HRZTL ungültig | 1 | - |
| 0xDA14F7 | Botschaft 0xE8 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_PO_SPN_HRZTL ungültig | 1 | - |
| 0xDA2C00 | Signal (Status_Blinken): ungültig | 1 | - |
| 0xDA2C02 | Signal (CRC_Steuerung_Licht_Außen_2): ungültig | 1 | - |
| 0xDA2C03 | Signal (Steuerung_Funktion_Abbiegelicht_rechts): ungültig | 1 | - |
| 0xDA2C04 | Signal (Steuerung_Funktion_Abblendlicht_rechts): ungültig | 1 | - |
| 0xDA2C05 | Signal (Steuerung_Lichtverteilung_Fahrlicht_rechts): ungültig | 1 | - |
| 0xDA2C06 | Signal (Steuerung_Modus_Funktion_Sonderblinken): ungültig | 1 | - |
| 0xDA2C07 | Signal (Steuerung_Phase_Funktion_Sonderblinken): ungültig | 1 | - |
| 0xDA2C08 | Signal (Steuerung_Funktion_Begrüßungslicht): ungültig | 1 | - |
| 0xDA2C09 | Signal (Steuerung_Funktion_Heimleuchten): ungültig | 1 | - |
| 0xDA2C0A | Signal (Steuerung_Funktion_Parklicht): ungültig | 1 | - |
| 0xDA2C0B | Signal (Steuerung_Funktion_Remote-Light): ungültig | 1 | - |
| 0xDA2C0C | Signal (Steuerung_Funktion_Standlicht): ungültig | 1 | - |
| 0xDA2C0D | Signal (Steuerung_Funktion_Tagfahrlicht): ungültig | 1 | - |
| 0xDA2C0E | Signal (Steuerung_Helligkeitswert_Licht_Außen): ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | AUSSENTEMPARATUR | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4001 | FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4002 | SPANNUNG_KLEMME_30 | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x401E | Spannung_Laserdiode | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x401F | Spannung_Gelbsensor | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
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

Dimensions: 128 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x440106 | Steuergerät: Übertemperatur 1 | 0 | - |
| 0x440107 | LED Ausgang 5: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440108 | LED Ausgang 1: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440109 | LED Ausgang 2: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44010A | LED Ausgang 3: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44010B | Reset | 0 | - |
| 0x44010C | Watchdog hat Reset ausgelöst | 0 | - |
| 0x44010D | Stellmotor Leuchtweitenregulierung: Übertemperatur (Warnung) | 1 | - |
| 0x44010E | Stellmotor Leuchtweitenregulierung: Referenzierung wegen Unterspannung abgebrochen | 1 | - |
| 0x44010F | Stellmotor Leuchtweitenregulierung: Bewegung wegen Unterspannung abgebrochen | 1 | - |
| 0x440110 | Stellmotor Leuchtweitenregulierung: Bewegung wegen Überspannung abgebrochen | 1 | - |
| 0x44011A | CRC-Checksum Fehler | 0 | - |
| 0x44011D | HardReset ausgeführt | 1 | - |
| 0x440122 | Fehlerhafter Quarz-Betrieb des Controllers | 0 | - |
| 0x440129 | Überlauf SPI-Empfangspuffer | 0 | - |
| 0x44012A | LED Ausgang 7: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44012B | LED Ausgang 6: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44012C | LED Ausgang 4: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44012D | ChargePump nicht abschaltbar | 0 | - |
| 0x44012E | Controller nicht abschaltbar | 0 | - |
| 0x44012F | Interner SG-Konfigurationsfehler | 0 | - |
| 0x440131 | Interner CRC-Fehler der Datensicherung für sicherheitsrelevante Steuersignale | 0 | - |
| 0x440132 | LED Ausgang 8: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440133 | LED Ausgang 9: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440134 | LED Ausgang 10: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440140 | Power-Down-Befehl 11 04 | 1 | - |
| 0x440141 | Power-Down-Befehl 11 41 | 1 | - |
| 0x440143 | Booster defekt | 0 | - |
| 0x44016D | Stellmotor Kurvenlicht: Übertemperatur (Warnung) | 1 | - |
| 0x44016E | Stellmotor Kurvenlicht: Referenzierung wegen Unterspannung abgebrochen | 1 | - |
| 0x44016F | Stellmotor Kurvenlicht: Bewegung wegen Unterspannung abgebrochen | 1 | - |
| 0x440170 | Stellmotor Kurvenlicht: Bewegung wegen Überspannung abgebrochen | 1 | - |
| 0x4401F4 | LED Ausgang 1: Kurzschluss nach Masse | 0 | - |
| 0x4401F5 | LED Ausgang 1: Kurzschluss nach Plus | 0 | - |
| 0x4401F6 | LED Ausgang 1: Strangunterbrechung | 0 | - |
| 0x4401F7 | LED Ausgang 1: Strangspannung außerhalb Toleranz | 0 | - |
| 0x4401F8 | LED Ausgang 1: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x4401F9 | LED Ausgang 1: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x4401FA | LED Ausgang 2: Kurzschluss nach Masse | 0 | - |
| 0x4401FB | LED Ausgang 2: Kurzschluss nach Plus | 0 | - |
| 0x4401FC | LED Ausgang 2: Strangunterbrechung | 0 | - |
| 0x4401FD | LED Ausgang 2: Strangspannung außerhalb Toleranz | 0 | - |
| 0x4401FE | LED Ausgang 2: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x4401FF | LED Ausgang 2: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440200 | LED Ausgang 3: Kurzschluss nach Masse | 0 | - |
| 0x440201 | LED Ausgang 3: Kurzschluss nach Plus | 0 | - |
| 0x440202 | LED Ausgang 3: Strangunterbrechung | 0 | - |
| 0x440203 | LED Ausgang 3: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440204 | LED Ausgang 3: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440205 | LED Ausgang 3: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440206 | LED Ausgang 4: Kurzschluss nach Masse | 0 | - |
| 0x440207 | LED Ausgang 4: Kurzschluss nach Plus | 0 | - |
| 0x440208 | LED Ausgang 4: Strangunterbrechung | 0 | - |
| 0x440209 | LED Ausgang 4: Strangspannung außerhalb Toleranz | 0 | - |
| 0x44020A | LED Ausgang 4: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x44020B | LED Ausgang 4: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x44020C | LED Ausgang 5: Kurzschluss nach Masse | 0 | - |
| 0x44020D | LED Ausgang 5: Kurzschluss nach Plus | 0 | - |
| 0x44020E | LED Ausgang 5: Strangunterbrechung | 0 | - |
| 0x44020F | LED Ausgang 5: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440210 | LED Ausgang 5: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440211 | LED Ausgang 5: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440212 | LED Ausgang 6: Kurzschluss nach Masse | 0 | - |
| 0x440213 | LED Ausgang 6: Kurzschluss nach Plus | 0 | - |
| 0x440214 | LED Ausgang 6: Strangunterbrechung | 0 | - |
| 0x440215 | LED Ausgang 6: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440216 | LED Ausgang 6: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440217 | LED Ausgang 6: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440218 | LED Ausgang 7: Kurzschluss nach Masse | 0 | - |
| 0x440219 | LED Ausgang 7: Kurzschluss nach Plus | 0 | - |
| 0x44021A | LED Ausgang 7: Strangunterbrechung | 0 | - |
| 0x44021B | LED Ausgang 7: Strangspannung außerhalb Toleranz | 0 | - |
| 0x44021C | LED Ausgang 7: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x44021D | LED Ausgang 7: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x44021E | LED Ausgang 8: Kurzschluss nach Masse | 0 | - |
| 0x44021F | LED Ausgang 8: Kurzschluss nach Plus | 0 | - |
| 0x440220 | LED Ausgang 8: Strangunterbrechung | 0 | - |
| 0x440221 | LED Ausgang 8: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440222 | LED Ausgang 8: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440223 | LED Ausgang 8: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440224 | LED Ausgang 9: Kurzschluss nach Masse | 0 | - |
| 0x440225 | LED Ausgang 9: Kurzschluss nach Plus | 0 | - |
| 0x440226 | LED Ausgang 9: Strangunterbrechung | 0 | - |
| 0x440227 | LED Ausgang 9: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440228 | LED Ausgang 9: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440229 | LED Ausgang 9: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x44022A | LED Ausgang 10: Kurzschluss nach Masse | 0 | - |
| 0x44022B | LED Ausgang 10: Kurzschluss nach Plus | 0 | - |
| 0x44022C | LED Ausgang 10: Strangunterbrechung | 0 | - |
| 0x44022D | LED Ausgang 10: Strangspannung außerhalb Toleranz | 0 | - |
| 0x44022E | LED Ausgang 10: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x44022F | LED Ausgang 10: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440230 | LED Ausgang 11: Kurzschluss nach Masse | 0 | - |
| 0x440231 | LED Ausgang 11: Kurzschluss nach Plus | 0 | - |
| 0x440232 | LED Ausgang 11: Strangunterbrechung | 0 | - |
| 0x440233 | LED Ausgang 11: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440234 | LED Ausgang 11: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x440235 | LED Ausgang 11: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440236 | LED Ausgang 11: Übertemperatur 1 (Degradation) | 1 | - |
| 0x440237 | LED Ausgang 12: Kurzschluss nach Masse | 0 | - |
| 0x440238 | LED Ausgang 12: Übertemperatur 2 (Abschaltung) | 1 | - |
| 0x440239 | LED Ausgang 12: Strangunterbrechung | 0 | - |
| 0x44023A | LED Ausgang 12: Übertemperatur 1 (Degradation) | 1 | - |
| 0x44023B | LED Ausgang 12: Kurzschluss nach Plus | 0 | - |
| 0x44023C | LED Ausgang 12: Strangsstrom außerhalb Toleranz | 0 | - |
| 0x44023D | LED Ausgang 12: Strangspannung außerhalb Toleranz | 0 | - |
| 0x440250 | Fernlicht: Laser defekt | 0 | - |
| 0x440251 | Fernlicht: Laser Versorgung außerhalb  Toleranz | 0 | - |
| 0x440253 | Fernlicht: Laser Lichtsensor Y Leitungsbruch | 0 | - |
| 0x440254 | Fernlicht: Laser Lichtsensor Y Kurzschluss | 0 | - |
| 0x440255 | Fernlicht: Laser Lichtsensor Übertemperatur | 0 | - |
| 0xDA1500 | Botschaft (Fahrgestellnummer): Timeout | 1 | - |
| 0xDA1502 | Botschaft (A_Temp): Timeout | 1 | - |
| 0xDA1505 | Botschaft (KmStand): Timeout | 1 | - |
| 0xDA1506 | Botschaft (Ctr_Lp_Ex2_Info): Timeout | 1 | - |
| 0xDA1507 | Botschaft (Fahrzeugzustand): Timeout | 1 | - |
| 0xDA1508 | Botschaft (Relativzeit): Timeout | 1 | - |
| 0xDA1509 | Botschaft (Status_Fahrlicht): Timeout | 1 | - |
| 0xDA2D00 | Signal (Nummer_Fahrgestell_1): ungültig | 1 | - |
| 0xDA2D01 | Signal (Nummer_Fahrgestell_2): ungültig | 1 | - |
| 0xDA2D02 | Signal (Nummer_Fahrgestell_3): ungültig | 1 | - |
| 0xDA2D03 | Signal (Nummer_Fahrgestell_4): ungültig | 1 | - |
| 0xDA2D04 | Signal (Nummer_Fahrgestell_5): ungültig | 1 | - |
| 0xDA2D05 | Signal (Nummer_Fahrgestell_6): ungültig | 1 | - |
| 0xDA2D06 | Signal (Nummer_Fahrgestell_7): ungültig | 1 | - |
| 0xDA2D07 | Signal (Temp_Ex): ungültig | 1 | - |
| 0xDA2D0D | Signal (St_Lowb): ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | AUSSENTEMPARATUR | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4001 | FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4002 | SPANNUNG_KLEMME_30 | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x401E | Spannung_Laserdiode | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x401F | Spannung_Gelbsensor | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-lenkerversion"></a>
### LENKERVERSION

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Linkslenker |
| 0x20 | Rechtslenker |

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

<a id="table-res-0x3000-r"></a>
### RES_0X3000_R

Dimensions: 25 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 1 |
| STAT_LED_1_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 1 |
| STAT_LED_2_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 2 |
| STAT_LED_2_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 2 |
| STAT_LED_3_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 3 |
| STAT_LED_3_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 3 |
| STAT_LED_4_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 4 |
| STAT_LED_4_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 4 |
| STAT_LED_5_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 5 |
| STAT_LED_5_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 5 |
| STAT_LED_6_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 6 |
| STAT_LED_6_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 6 |
| STAT_LED_7_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 7 |
| STAT_LED_7_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 7 |
| STAT_LED_8_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 8 |
| STAT_LED_8_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 8 |
| STAT_LED_9_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 9 |
| STAT_LED_9_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 9 |
| STAT_LED_10_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 10 |
| STAT_LED_10_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 10 |
| STAT_LED_11_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 11 |
| STAT_LED_11_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 11 |
| STAT_LED_12_STROM_WERT | - | - | + | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Stromwert LED 12 |
| STAT_LED_12_PWM_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 12 |
| STAT_AKTIV | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | Prozessstatus: 1...aktiv 0...nicht aktiv |

<a id="table-res-0xa538-r"></a>
### RES_0XA538_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_ERGEBNIS | - | - | + | 0-n | high | unsigned char | - | TAB_AHL_REFERENZLAUF | - | - | - | Ergebnisse TAB_AHL_REFERENZLAUF |

<a id="table-res-0xa541-r"></a>
### RES_0XA541_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_ERGEBNIS | - | - | + | 0-n | high | unsigned char | - | TAB_LWR_REFERENZLAUF | - | - | - | Ergebnisse TAB_LWR_REFERENZLAUF |

<a id="table-res-0xa543-r"></a>
### RES_0XA543_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LEUCHTMITTEL_FLE | - | - | + | 0-n | high | unsigned char | - | TAB_LED_LEUCHTMITTEL | - | - | - | Resulttabelle LED Leuchtmittel |
| STAT_AKTIV | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiv 0...nicht aktiv |

<a id="table-res-0xa545-r"></a>
### RES_0XA545_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_POSITION_WERT | - | - | + | ° | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Position LWR in Grad |
| STAT_LWR_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_POS_LWR | - | - | - | Job Status |

<a id="table-res-0xa546-r"></a>
### RES_0XA546_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_POSITION_WERT | - | - | + | ° | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Position AHL in Grad |
| STAT_AHL_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_POS_AHL | - | - | - | Job Status |

<a id="table-res-0xa547-r"></a>
### RES_0XA547_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LUEFTER_1 | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 1...ein 0...aus |
| STAT_LUEFTER_2 | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 1...ein 0...aus |

<a id="table-res-0xa548-r"></a>
### RES_0XA548_R

Dimensions: 18 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTEST_LED_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_3_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_4_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_5_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_6_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_7_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_8_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_9_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_10_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_11_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_12_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_TEMPERATURSENSOREN_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LUEFTER_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LUEFTER_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LR_ERKENNUNG_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_AHL_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LWR_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |

<a id="table-res-0xa5a7-r"></a>
### RES_0XA5A7_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTEST_LASER_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |

<a id="table-res-0xa801-d"></a>
### RES_0XA801_D

Dimensions: 101 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NUMBER_OF_VALID_SAMPLES_DATA | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | Anzahl gültiger Messsets |
| STAT_SAMPLE_0_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_0_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_0_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_0_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_0_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_1_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_1_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_1_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_1_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_1_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_2_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_2_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_2_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_2_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_2_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_3_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_3_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_3_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_3_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_3_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_4_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_4_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_4_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_4_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_4_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_5_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_5_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_5_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_5_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_5_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_6_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_6_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_6_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_6_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_6_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_7_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_7_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_7_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_7_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_7_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_8_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_8_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_8_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_8_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_8_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_9_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_9_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_9_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_9_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_9_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_10_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_10_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_10_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_10_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_10_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_11_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_11_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_11_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_11_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_11_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_12_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_12_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_12_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_12_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_12_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_13_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_13_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_13_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_13_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_13_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_14_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_14_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_14_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_14_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_14_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_15_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_15_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_15_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_15_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_15_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_16_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_16_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_16_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_16_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_16_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_17_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_17_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_17_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_17_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_17_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_18_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_18_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_18_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_18_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_18_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |
| STAT_SAMPLE_19_ERR_TYPE_WERT | HEX | high | unsigned char | - | - | - | - | - | Fehlertyp |
| STAT_SAMPLE_19_U_LASER_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Laserspannung bei Ausfall |
| STAT_SAMPLE_19_U_YSENSOR_WERT | V | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gelbsensorspannung bei Ausfall |
| STAT_SAMPLE_19_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Temperatur Laser-NTC bei Ausfall |
| STAT_SAMPLE_19_TIMESTAMP_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel Relativzeit der Fehlereintragung des passenden DTCs |

<a id="table-res-0xd1fd-d"></a>
### RES_0XD1FD_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_BEGONNEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der begonnenen Referenzläufe |
| STAT_REFERENZLAUF_ABGESCHLOSSEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der abgeschlossenen Referenzläufe |

<a id="table-res-0xd1fe-d"></a>
### RES_0XD1FE_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_BEGONNEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der begonnenen Referenzläufe |
| STAT_REFERENZLAUF_ABGESCHLOSSEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der abgeschlossenen Referenzläufe |

<a id="table-res-0xd506-d"></a>
### RES_0XD506_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPG_FIRST_REF_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Initialwert der Referenz-Spannung (wird nur beim Einlernen gespeichert) |
| STAT_SPG_REF_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aktueller Wert der Referenz-Spannung |
| STAT_STROM_REF_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Referenz-Strom (wird nur beim Einlernen gespeichert) |
| STAT_TEMP_REF_WERT | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Referenz-Temperatur (wird nur beim Einlernen gespeichert) |
| STAT_EINLERN_STATUS | 0-n | high | unsigned char | - | TAB_EINLERNDATEN_STATUS | - | - | - | Einlern-Status der N-1-Ausfallerkennung (wird nur beim Einlernen gespeichert): 0 = nicht eingelernt, 1 = links eingelernt, 2 = rechts eingelernt  |
| STAT_NVM_STATUS | 0-n | high | unsigned char | - | TAB_EINLERNDATEN_NVM_STATUS | - | - | - | Status der Speicherung der Einlerndaten im Flash (NvM) im aktuellen Betriebszyklus. Dieser Wert selbst wird nicht im Einlerndatensatz mit gespeichert. Wenn NVM_REQ_PENDING oder NVM_REQ_DENIED ausgelesen wird, muß dieser DID so lange gelesen werden, bis ein anderer Status zurückgegeben wird. 0 = NVM_OK, 1 = NVM_NOT_OK, 2 = NVM_REQ_PENDING, 3 = NVM_REQ_DENIED, 4 = NVM_SHUTDOWNWRITE  |
| STAT_RESERVED_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |
| STAT_RESERVED_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |
| STAT_RESERVED_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |
| STAT_RESERVED_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |
| STAT_RESERVED_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |
| STAT_RESERVED_6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Reserviert für zukünftige Erweiterungen |

<a id="table-res-0xd529-d"></a>
### RES_0XD529_D

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAU_SIGNAL_1 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_2 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_3 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_4 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_5 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_6 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_7 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_8 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_9 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_10 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_11 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_12 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_13 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_14 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |
| STAT_VERBAU_SIGNAL_15 | 0-n | high | unsigned char | - | TAB_LEUCHTEN_SENSOR | - | - | - | Verbau: Siehe Tabelle TAB_LEUCHTEN_SENSOR |

<a id="table-res-0xd630-d"></a>
### RES_0XD630_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_1_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 1 |
| STAT_SENSOR_2_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 2 |
| STAT_SENSOR_3_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 3 |
| STAT_SENSOR_4_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 4 |
| STAT_SENSOR_5_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 5 |
| STAT_SENSOR_6_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 6 |
| STAT_SENSOR_7_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 7 |
| STAT_SENSOR_8_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Temp Sensor 8 |
| STAT_TEMP_LEUCHTMITTEL_1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_4_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_5_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_6_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_7_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_8_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_9_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_10_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_11_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |
| STAT_TEMP_LEUCHTMITTEL_12_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Status berechnete Leuchtmitteltemperatur |

<a id="table-res-0xd632-d"></a>
### RES_0XD632_D

Dimensions: 48 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_1_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T1 |
| STAT_SENSOR_1_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T2 |
| STAT_SENSOR_1_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T3 |
| STAT_SENSOR_1_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T4 |
| STAT_SENSOR_1_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T5 |
| STAT_SENSOR_1_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 1 T6 |
| STAT_SENSOR_2_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T1 |
| STAT_SENSOR_2_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T2 |
| STAT_SENSOR_2_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T3 |
| STAT_SENSOR_2_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T4 |
| STAT_SENSOR_2_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T5 |
| STAT_SENSOR_2_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 2 T6 |
| STAT_SENSOR_3_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T1 |
| STAT_SENSOR_3_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T2 |
| STAT_SENSOR_3_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T3 |
| STAT_SENSOR_3_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T4 |
| STAT_SENSOR_3_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T5 |
| STAT_SENSOR_3_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 3 T6 |
| STAT_SENSOR_4_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T1 |
| STAT_SENSOR_4_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T2 |
| STAT_SENSOR_4_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T3 |
| STAT_SENSOR_4_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T4 |
| STAT_SENSOR_4_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T5 |
| STAT_SENSOR_4_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 4 T6 |
| STAT_SENSOR_5_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T1 |
| STAT_SENSOR_5_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T2 |
| STAT_SENSOR_5_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T3 |
| STAT_SENSOR_5_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T4 |
| STAT_SENSOR_5_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T5 |
| STAT_SENSOR_5_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 5 T6 |
| STAT_SENSOR_6_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T1 |
| STAT_SENSOR_6_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T2 |
| STAT_SENSOR_6_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T3 |
| STAT_SENSOR_6_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T4 |
| STAT_SENSOR_6_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T5 |
| STAT_SENSOR_6_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 6 T6 |
| STAT_SENSOR_7_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T1 |
| STAT_SENSOR_7_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T2 |
| STAT_SENSOR_7_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T3 |
| STAT_SENSOR_7_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T4 |
| STAT_SENSOR_7_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T5 |
| STAT_SENSOR_7_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 7 T6 |
| STAT_SENSOR_8_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T1 |
| STAT_SENSOR_8_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T2 |
| STAT_SENSOR_8_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T3 |
| STAT_SENSOR_8_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T4 |
| STAT_SENSOR_8_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T5 |
| STAT_SENSOR_8_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | S 8 T6 |

<a id="table-res-0xd634-d"></a>
### RES_0XD634_D

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 1 |
| STAT_LED_2_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 2 |
| STAT_LED_3_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 3 |
| STAT_LED_4_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 4 |
| STAT_LED_5_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 5 |
| STAT_LED_6_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 6 |
| STAT_LED_7_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 7 |
| STAT_LED_8_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 8 |
| STAT_LED_9_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 9 |
| STAT_LED_10_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 10 |
| STAT_LED_11_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 11 |
| STAT_LED_12_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer LED 12 |
| STAT_LUEFTER1_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer Lüfter 1 |
| STAT_LUEFTER2_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer Lüfter 2 |
| STAT_FLE_WERT | s | high | unsigned long | - | - | 10.0 | 1.0 | 0.0 | Betriebsdauer FLE |

<a id="table-res-0xd635-d"></a>
### RES_0XD635_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KL_30_ISENSE_WERT | mA | high | unsigned char | - | - | 100.0 | 1.0 | 0.0 | Stromwert Kl 30 |
| STAT_KL_30_USENSE_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Spannung Kl 30 |

<a id="table-res-0xd636-d"></a>
### RES_0XD636_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIEFTEMPERATUR_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiv 0...nicht aktiv |
| STAT_HOCHTEMPERATUR_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiv 0...nicht aktiv |

<a id="table-res-0xd638-d"></a>
### RES_0XD638_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BINNING_1_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 1 |
| STAT_BINNING_1_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 1 |
| STAT_BINNING_2_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 2 |
| STAT_BINNING_2_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 2 |
| STAT_BINNING_3_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 3 |
| STAT_BINNING_3_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 3 |
| STAT_BINNING_4_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 4 |
| STAT_BINNING_4_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 4 |
| STAT_BINNING_5_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 5 |
| STAT_BINNING_5_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 5 |
| STAT_BINNING_6_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 6 |
| STAT_BINNING_6_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 6 |
| STAT_BINNING_7_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 7 |
| STAT_BINNING_7_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 7 |
| STAT_BINNING_8_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 8 |
| STAT_BINNING_8_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 8 |
| STAT_BINNING_9_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 9 |
| STAT_BINNING_9_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 9 |
| STAT_BINNING_10_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 10 |
| STAT_BINNING_10_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 10 |
| STAT_BINNING_11_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 11 |
| STAT_BINNING_11_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 11 |
| STAT_BINNING_12_WERT | kOhm | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Widerstandwert Binning Kanal 12 |
| STAT_BINNING_12_KLASSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binning Klasse Kanal 12 |

<a id="table-res-0xd639-d"></a>
### RES_0XD639_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LUEFTER_VERSORGUNG_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Versorgungsspannnung |
| STAT_LUEFTER1_DIAG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe Status Diagnoseleitung Lüfter 1 |
| STAT_LUEFTER1_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert |
| STAT_LUEFTER2_DIAG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe Status Diagnoseleitung Lüfter 2 |
| STAT_LUEFTER2_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert |

<a id="table-res-0xd63a-d"></a>
### RES_0XD63A_D

Dimensions: 26 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_2_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_3_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_4_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_5_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_6_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_7_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_8_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_9_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_10_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_11_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_LED_12_VERBAU | 0-n | high | unsigned char | - | TAB_LEUCHTMITTEL | - | - | - | Status Verbau siehe Tabelle TAB_LEUCHTMITTEL |
| STAT_FUNKTION_ABBLENDLICHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_POSITIONSLICHT_STANDLICHT_PARKLICHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_FERNLICHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_TAGFAHRLICHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_ABBIEGELICHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_SONDERBLINKEN | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_REMOTELIGHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_WELCOMELIGHT | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_FOLLOWMEHOME | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_FUNKTION_BLINKEN | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_LWR_MOTOR_VERBAU | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_AHL_MOTOR_VERBAU | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_LUEFTER1_VERBAU | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |
| STAT_LUEFTER2_VERBAU | 0-n | high | unsigned char | - | TAB_FUNKTION_FLE | - | - | - | 0...nicht verbaut 1...verbaut, aktiv 2...verbaut, nicht aktiv |

<a id="table-res-0xd63c-d"></a>
### RES_0XD63C_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESET_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert Resetzähler 1 |
| STAT_RESET_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wert Resetzähler 2 |

<a id="table-res-0xd63d-d"></a>
### RES_0XD63D_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HALTESTROM_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | Lesen der Betriebsdauer des Haltestrom LWR Motor |
| STAT_VERSTELLSTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Lesen der Betriebsdauer des Verstellstrom LWR Motor |
| STAT_VERSTELLUNGEN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verstellungen LWR Motor |

<a id="table-res-0xd63e-d"></a>
### RES_0XD63E_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAHRZEUGTYP | 0-n | high | unsigned char | - | FAHRZEUGVARIANTE | - | - | - | Fahrzeugtyp aus Tabelle |
| - | Bit | high | BITFIELD | - | BF_SCHEINWERFERINFO_STRUCT | - | - | - | Variante |
| - | Bit | high | BITFIELD | - | BF_VERSIONSINFO_STRUCT | - | - | - | Auslesen der Scheinwerferversionsnummer |

<a id="table-res-0xd662-d"></a>
### RES_0XD662_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIEFTEMPERATUR_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiv 0...nicht aktiv |
| STAT_HOCHTEMPERATUR_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiv 0...nicht aktiv |

<a id="table-res-0xd667-d"></a>
### RES_0XD667_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 1 |
| STAT_LED_1_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 1 |
| STAT_LED_2_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 2 |
| STAT_LED_2_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 2 |
| STAT_LED_3_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 3 |
| STAT_LED_3_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 3 |
| STAT_LED_4_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 4 |
| STAT_LED_4_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 4 |
| STAT_LED_5_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 5 |
| STAT_LED_5_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 5 |
| STAT_LED_6_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 6 |
| STAT_LED_6_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 6 |
| STAT_LED_7_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 7 |
| STAT_LED_7_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 7 |
| STAT_LED_8_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 8 |
| STAT_LED_8_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 8 |
| STAT_LED_9_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 9 |
| STAT_LED_9_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 9 |
| STAT_LED_10_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 10 |
| STAT_LED_10_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 10 |
| STAT_LED_11_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 11 |
| STAT_LED_11_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 11 |
| STAT_LED_12_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Strom Wert LED 12 |
| STAT_LED_12_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Prozent Wert LED 12 |

<a id="table-res-0xd680-d"></a>
### RES_0XD680_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HALTESTROM_WERT | s | high | unsigned long | - | - | 30.0 | 1.0 | 0.0 | Lesen der Betriebsdauer des Haltestrom AHL Motor |
| STAT_VERSTELLSTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Lesen der Betriebsdauer des Verstellstrom AHL Motor |
| STAT_VERSTELLUNGEN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Verstellungen LWR Motor |

<a id="table-res-0xdca0-d"></a>
### RES_0XDCA0_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SENSOR_VERSORGUNG | 0/1 | high | unsigned char | - | - | - | - | - | 1...aktiviert 0...nicht aktiviert |
| STAT_ZFL_SENSOR_1_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | ZFL Sensor 1 Wert |

<a id="table-res-0xdf0f-d"></a>
### RES_0XDF0F_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHRITTVERLUST_BEREICH_1_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 1 |
| STAT_SCHRITTVERLUST_BEREICH_2_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 2 |
| STAT_SCHRITTVERLUST_BEREICH_3_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 3 |
| STAT_SCHRITTVERLUST_BEREICH_4_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 4 |
| STAT_SCHRITTVERLUST_BEREICH_5_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 5 |
| STAT_SCHRITTVERLUST_BEREICH_6_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 6 |

<a id="table-res-0xe2f6-d"></a>
### RES_0XE2F6_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EIGENE_DATA | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | Binning Code eigene Seite |
| STAT_PARTNER_DATA | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | Binning Code andere Seite |
| STAT_BINNING1_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING2_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING3_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING4_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING5_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING6_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING7_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING8_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING9_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING10_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING11_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |
| STAT_BINNING12_WERT | HEX | high | unsigned char | - | - | - | - | - | Binning Klasse: 0 = noch nicht programmiert 1 .. 5 = Binning Klasse 7 .. = nicht benutzt |

<a id="table-res-0xfd40-d"></a>
### RES_0XFD40_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFERDATENBLOCK_DATA | DATA | high | data[16] | - | - | 1.0 | 1.0 | 0.0 | Scheinwerferdatenblock |

<a id="table-res-0xfd41-d"></a>
### RES_0XFD41_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FRAZ_STATUS_MESSUNG | 0-n | high | unsigned char | - | TAB_FRAZ_MESSUNG | - | - | - | Zustand der Auswertung der Messung |
| STAT_FRAZ_LEITUNGSZUSTAND | 0/1 | high | unsigned char | - | - | - | - | - | Aktueller Zustand der FRAZ-Leitung |
| STAT_FRAZ_SPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | FRAZ-Spannungswert während der letzen EIN-Phase des Blinkers |
| STAT_FRAZ_STROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | FRAZ-Stromwert während der letzten EIN-Phase des Blinkers |
| STAT_FRAZ_TEMP_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | FRAZ-Temperatur während der letzten EIN-Phase des Blinkers |
| STAT_SG_TEMP_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Steuergeräte-Temperatur während der letzten EIN-Phase des Blinkers |
| STAT_FRAZ_SPG_KOMP_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktueller kompensierter Spannungswert |
| STAT_FRAZ_SOLLSTROM_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Vorgegebener Stromwert |
| STAT_FRAZ_SOLLPWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorgegebener Duty Cycle |
| STAT_FRAZ_SPG_KOMP_AVG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Durchschnittlicher kompensierter Spannungswert |
| STAT_FRAZ_STATUS_MESSUNG_INTERN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Interner Status der Messung |
| STAT_FRAZ_MESSUNG_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | 0 = Messung inaktiv, 1 = Messung aktiv |

<a id="table-res-0xfd43-d"></a>
### RES_0XFD43_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BLOCK_NR_IMPLAUSIBEL_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Plausibilitätsprüfung in Block-Nr. 'x' (bzgl. UDS-Block-Id 0x3000 + x) ist negativ (wobei Default 0xFF = 255 gilt). |
| STAT_GRUND_IMPLAUSIBEL | 0-n | high | unsigned char | - | TAB_GRUND_IMPLAUSIBEL | - | - | - | Grund der negativen Plausibilitätsprüfung (wobei Default 0 gilt) |

<a id="table-res-0xfd44-d"></a>
### RES_0XFD44_D

Dimensions: 37 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RBIN_NTC_6_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 0: Binning-/NTC-Eingang 6 |
| STAT_RBIN_NTC_7_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 1: Binning-/NTC-Eingang 7 |
| STAT_RBIN_NTC_8_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 7: Binning-/NTC-Eingang 8 |
| STAT_ADC_09_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 9: N/A |
| STAT_ADC_10_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 10: N/A |
| STAT_RBIN_NTC_9_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 11: Binning-/NTC-Eingang 9 |
| STAT_ADC_12_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 12: N/A |
| STAT_ADC_13_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 13: N/A |
| STAT_ADC_14_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 14: N/A |
| STAT_ADC_15_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 15: N/A |
| STAT_ADC_16_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 16: N/A |
| STAT_ADC_17_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 17: N/A |
| STAT_ADC_18_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 18: N/A |
| STAT_RBIN_NTC_10_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 19: Binning-/NTC-Eingang 10 |
| STAT_RBIN_NTC_11_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 22: Binning-/NTC-Eingang 11 |
| STAT_RBIN_NTC_12_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 23: Binning-/NTC-Eingang 12 |
| STAT_RBIN_NTC_13_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 26: Binning-/NTC-Eingang 13 |
| STAT_RBIN_NTC_14_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 27: Binning-/NTC-Eingang 14 |
| STAT_RBIN_NTC_15_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 28: Binning-/NTC-Eingang 15 |
| STAT_LR_DETECT_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 29: Links-Rechts-Verbauorterkennung |
| STAT_DIAG_VBAT_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 31: Versorgungsspannung VBAT |
| STAT_ADC_32_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 32: N/A |
| STAT_RBIN_NTC_1_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 33: Binning-/NTC-Eingang 1 |
| STAT_ADC_34_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 34: N/A |
| STAT_RBIN_NTC_3_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 35: Binning-/NTC-Eingang 3 |
| STAT_RBIN_NTC_4_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 36: Binning-/NTC-Eingang 4 |
| STAT_RBIN_NTC_5_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 37: Binning-/NTC-Eingang 5 |
| STAT_RBIN_NTC_2_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 38: Binning-/NTC-Eingang 2 |
| STAT_TEMP_PCB_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 39: Temperatur der Platine |
| STAT_A_U_VPS_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 40: AHL-Positionssensor-Versorgungsspannung VPS |
| STAT_ADC_41_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 41: N/A |
| STAT_A_U_FAN_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 42: Spannung Lüfter 1 |
| STAT_A_U_FAN_2_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 43: Spannung Lüfter 2 |
| STAT_DIAG_BLNK_U_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 44: Spannung Blinker |
| STAT_DIAG_BLNK_I_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 45: Strom Blinker |
| STAT_ADC_46_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 46: N/A |
| STAT_A_U_VLSR_WERT | Digits | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | ADC 47: LASER-Sensor-Versorgungsspannung VLSR |

<a id="table-res-0xfd47-d"></a>
### RES_0XFD47_D

Dimensions: 35 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LR_STATUS | 0-n | high | unsigned char | - | TAB_LR_STATUS | - | - | - | Status Leistungsreduzierung (LR) |
| STAT_LR_AKTIVE_LICHTFUNKTION | 0-n | high | unsigned char | - | TAB_LR_AKTIVE_LICHTFUNKTION | - | - | - | aktive Lichtfunktion |
| STAT_LR_LMVEKTOR_LM1_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM2_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM3_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM4_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM5_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM6_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM7_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM8_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM9_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM10_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM11_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_LMVEKTOR_LM12_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM1_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM2_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM3_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM4_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM5_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM6_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM7_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM8_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM9_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM10_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM11_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_ANGEWANDTER_THERMOVEKTOR_LM12_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Intensität |
| STAT_LR_CLA | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: CLA |
| STAT_LR_CL | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: CL |
| STAT_LR_RL | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: RL |
| STAT_LR_DRL | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: DRL |
| STAT_LR_TI | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: TI |
| STAT_LR_TT | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: TT |
| STAT_LR_NTC_FEHLER | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: NTC-Fehler |
| STAT_LR_LUEFTER_FEHLER | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: Lüfter-Fehler |
| STAT_LR_LEDTREIBER_TEMPWARNUNG | 0/1 | high | unsigned char | - | - | - | - | - | LR-Status: LED Treiber Temperaturwarnung |

<a id="table-res-0xfd48-d"></a>
### RES_0XFD48_D

Dimensions: 36 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_1_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_1_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_2_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_2_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_2_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_3_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_3_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_3_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_4_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_4_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_4_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_5_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_5_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_5_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_6_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_6_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_6_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_7_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_7_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_7_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_8_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_8_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_8_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_9_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_9_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_9_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_10_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_10_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_10_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_11_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_11_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_11_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |
| STAT_LED_12_AKT_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangspannung während der letzten gültigen EIN-Phase |
| STAT_LED_12_MIN_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Strangspannung gemäß Codierdaten |
| STAT_LED_12_MAX_STRANGSPG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Strangspannung gemäß Codierdaten |

<a id="table-res-0xfd4a-d"></a>
### RES_0XFD4A_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd4b-d"></a>
### RES_0XFD4B_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd4c-d"></a>
### RES_0XFD4C_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd4d-d"></a>
### RES_0XFD4D_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd4e-d"></a>
### RES_0XFD4E_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd4f-d"></a>
### RES_0XFD4F_D

Dimensions: 41 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CODING_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | Coding Mode |
| STAT_SYSTEM_MODE_WERT | HEX | high | unsigned char | - | - | - | - | - | System Mode |
| STAT_CTRL_TX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_RX_REG_01_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x01 (Bits 9...0) |
| STAT_CTRL_TX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_RX_REG_02_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x02 (Bits 9...0) |
| STAT_CTRL_TX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_RX_REG_03_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x03 (Bits 9...0) |
| STAT_CTRL_TX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_RX_REG_04_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x04 (Bits 9...0) |
| STAT_CTRL_TX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_RX_REG_05_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x05 (Bits 9...0) |
| STAT_CTRL_TX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_RX_REG_06_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x06 (Bits 9...0) |
| STAT_CTRL_TX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_RX_REG_07_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x07 (Bits 9...0) |
| STAT_CTRL_TX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_RX_REG_08_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x08 (Bits 9...0) |
| STAT_CTRL_TX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_RX_REG_09_PWM1_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x09 - PWM Duty 1 (Bits 9...0) |
| STAT_CTRL_TX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_RX_REG_0A_PWM2_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0A - PWM Duty 2 (Bits 9...0) |
| STAT_CTRL_TX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_RX_REG_0B_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0B (Bits 9...0) |
| STAT_CTRL_TX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_RX_REG_0C_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0C (Bits 9...0) |
| STAT_CTRL_TX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Tx-Register 0x0D (Bits 9...0) |
| STAT_CTRL_RX_REG_0D_WERT | HEX | high | unsigned int | - | - | - | - | - | Control-Rx-Register 0x0D (Bits 9...0) |
| STAT_VLED1ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1ON |
| STAT_VLED2ON_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2ON |
| STAT_VLED1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED1 |
| STAT_VLED2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VLED2 |
| STAT_VTEMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VTEMP |
| STAT_VBOOST_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBOOST |
| STAT_VBAT_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register VBAT (immer 0) |
| STAT_BUCK1_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK1_TON_DUR (immer 0) |
| STAT_BUCK2_TON_DUR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register BUCK2_TON_DUR (immer 0) |
| STAT_STATUS1_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS1 |
| STAT_STATUS2_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register STATUS2 |
| STAT_HWR_VBOOST_OFF_COMP_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register HWR und VBOOST_OFF_COMP |
| STAT_REVID_WERT | HEX | high | unsigned char | - | - | - | - | - | Status-Register REVID |

<a id="table-res-0xfd50-d"></a>
### RES_0XFD50_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BITS_GLOBAL_INIT_ONCE_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | BitsGlobalInitOnce |
| STAT_ABITS_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aBits |
| STAT_ABITSMOD_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aBitsMod |
| STAT_AESTATE_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aeState |
| STAT_ASTPSTATE_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aStpState |
| STAT_ASTPPOS_WERT | HEX | high | unsigned int | - | - | - | - | - | aStpPos |
| STAT_ASTPCTRL_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aStpCtrl |
| STAT_AEVENTBITS_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aEventBits |
| STAT_APSENS_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aPsens |
| STAT_ALLASTDEVIATION_WERT | HEX | high | unsigned long | - | - | - | - | - | alLastDeviation |

<a id="table-res-0xfd51-d"></a>
### RES_0XFD51_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BITS_GLOBAL_INIT_ONCE_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | BitsGlobalInitOnce |
| STAT_ABITS_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aBits |
| STAT_ABITSMOD_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aBitsMod |
| STAT_AESTATE_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aeState |
| STAT_ASTPSTATE_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aStpState |
| STAT_ASTPPOS_WERT | HEX | high | unsigned int | - | - | - | - | - | aStpPos |
| STAT_ASTPCTRL_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aStpCtrl |
| STAT_AEVENTBITS_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aEventBits |
| STAT_APSENS_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | aPsens |
| STAT_ALLASTDEVIATION_WERT | HEX | high | unsigned long | - | - | - | - | - | alLastDeviation |

<a id="table-res-0xfd52-d"></a>
### RES_0XFD52_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CTRL_TX_CREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg1 |
| STAT_CTRL_TX_CREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg2 |
| STAT_CTRL_TX_CREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg3 |
| STAT_CTRL_TX_CREG_04_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg4 |
| STAT_CTRL_TX_CREG_4A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg4A |
| STAT_CTRL_TX_CREG_05_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg5 |
| STAT_CTRL_TX_CREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg6 |
| STAT_CTRL_TX_CREG_07_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg7 |
| STAT_CTRL_TX_CREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg7A |
| STAT_CTRL_RX_CREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg1 |
| STAT_CTRL_RX_CREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg2 |
| STAT_CTRL_RX_CREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg3 |
| STAT_CTRL_RX_CREG_04_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg4 |
| STAT_CTRL_RX_CREG_4A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg4A |
| STAT_CTRL_RX_CREG_05_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg5 |
| STAT_CTRL_RX_CREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg6 |
| STAT_CTRL_RX_CREG_07_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg7 |
| STAT_CTRL_RX_CREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg7A |
| STAT_STAT_RX_SREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg1 |
| STAT_STAT_RX_SREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg2 |
| STAT_STAT_RX_SREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg3 |
| STAT_STAT_RX_SREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg6 |
| STAT_STAT_RX_SREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg7A |
| STAT_STAT_RX_SREG_8A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg8A |
| STAT_STATV_RX_SREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg1 |
| STAT_STATV_RX_SREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg2 |
| STAT_STATV_RX_SREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg3 |
| STAT_STATV_RX_SREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg6 |
| STAT_STATV_RX_SREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg7A |
| STAT_STATV_RX_SREG_8A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg8A |

<a id="table-res-0xfd53-d"></a>
### RES_0XFD53_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CTRL_TX_CREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg1 |
| STAT_CTRL_TX_CREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg2 |
| STAT_CTRL_TX_CREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg3 |
| STAT_CTRL_TX_CREG_04_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg4 |
| STAT_CTRL_TX_CREG_4A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg4A |
| STAT_CTRL_TX_CREG_05_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg5 |
| STAT_CTRL_TX_CREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg6 |
| STAT_CTRL_TX_CREG_07_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg7 |
| STAT_CTRL_TX_CREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlTx.aucCReg7A |
| STAT_CTRL_RX_CREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg1 |
| STAT_CTRL_RX_CREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg2 |
| STAT_CTRL_RX_CREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg3 |
| STAT_CTRL_RX_CREG_04_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg4 |
| STAT_CTRL_RX_CREG_4A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg4A |
| STAT_CTRL_RX_CREG_05_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg5 |
| STAT_CTRL_RX_CREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg6 |
| STAT_CTRL_RX_CREG_07_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg7 |
| STAT_CTRL_RX_CREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | CtrlRx.aucCReg7A |
| STAT_STAT_RX_SREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg1 |
| STAT_STAT_RX_SREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg2 |
| STAT_STAT_RX_SREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg3 |
| STAT_STAT_RX_SREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg6 |
| STAT_STAT_RX_SREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg7A |
| STAT_STAT_RX_SREG_8A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatRx.aucSReg8A |
| STAT_STATV_RX_SREG_01_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg1 |
| STAT_STATV_RX_SREG_02_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg2 |
| STAT_STATV_RX_SREG_03_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg3 |
| STAT_STATV_RX_SREG_06_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg6 |
| STAT_STATV_RX_SREG_7A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg7A |
| STAT_STATV_RX_SREG_8A_WERT | HEX | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | StatvRx.aucSReg8A |

<a id="table-res-0xfd54-d"></a>
### RES_0XFD54_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BITSINT_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | BitsInt |
| STAT_SPI_TX_0_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPI_TX[0] |
| STAT_SPI_TX_1_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPI_TX[1] |
| STAT_SPI_TX_2_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPI_TX[2] |
| STAT_SPI_TX_3_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPI_TX[3] |
| STAT_SPIRRX_0_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPIrRX[0] |
| STAT_SPIRRX_1_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPIrRX[1] |
| STAT_SPIRRX_2_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPIrRX[2] |
| STAT_SPIRRX_3_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | aunSPIrRX[3] |
| STAT_STAT_TX_REG_00_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatTx.unReg0.unRaw |
| STAT_STAT_TX_REG_01_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatTx.unReg1.unRaw |
| STAT_STAT_TX_REG_02_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatTx.unReg2.unRaw |
| STAT_STAT_TX_REG_03_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatTx.unReg3.unRaw |
| STAT_STAT_RX_REG_00_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatRx.unReg0.unRaw |
| STAT_STAT_RX_REG_01_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatRx.unReg1.unRaw |
| STAT_STAT_RX_REG_02_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatRx.unReg2.unRaw |
| STAT_STAT_RX_REG_03_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | StatRx.unReg3.unRaw |

<a id="table-res-0xfd55-d"></a>
### RES_0XFD55_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAN_1_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Momentante Frequenz Lüfter 1 |
| STAT_FAN_1_MIN_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Minimale Frequenz Lüfter 1 gemäß Codierdaten |
| STAT_FAN_1_MAX_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximale Frequenz Lüfter 1 gemäß Codierdaten |

<a id="table-res-0xfd56-d"></a>
### RES_0XFD56_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAN_2_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Momentante Frequenz Lüfter 2 |
| STAT_FAN_2_MIN_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Minimale Frequenz Lüfter 2 gemäß Codierdaten |
| STAT_FAN_2_MAX_FREQ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Maximale Frequenz Lüfter 2 gemäß Codierdaten |

<a id="table-res-0xfd58-d"></a>
### RES_0XFD58_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ULEDMIN_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Minimaler Spannungswert: Spannungswert |
| STAT_ULEDMIN_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Minimaler Spannungswert: Stromwert |
| STAT_ULEDMIN_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Minimaler Spannungswert: Temperaturwert |
| STAT_ULEDMAX_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Maximaler Spannungswert: Spannungswert |
| STAT_ULEDMAX_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Maximaler Spannungswert: Stromwert |
| STAT_ULEDMAX_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Maximaler Spannungswert: Temperaturwert |
| STAT_ILEDMIN_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Minimaler Stromwert: Spannungswert |
| STAT_ILEDMIN_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Minimaler Stromwert: Stromwert |
| STAT_ILEDMIN_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Minimaler Stromwert: Temperaturwert |
| STAT_ILEDMAX_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Maximaler Stromwert: Spannungswert |
| STAT_ILEDMAX_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Maximaler Stromwert: Stromwert |
| STAT_ILEDMAX_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Maximaler Stromwert: Temperaturwert |
| STAT_TLEDMIN_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Minimaler Temperaturwert: Spannungswert |
| STAT_TLEDMIN_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Minimaler Temperaturwert: Stromwert |
| STAT_TLEDMIN_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Minimaler Temperaturwert: Temperaturwert |
| STAT_TLEDMAX_U_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Messung Maximaler Temperaturwert: Spannungswert |
| STAT_TLEDMAX_I_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Messung Maximaler Temperaturwert: Stromwert |
| STAT_TLEDMAX_T_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Messung Maximaler Temperaturwert: Temperaturwert |
| STAT_ULEDAVG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Durchschnittlicher Spannungswert |
| STAT_ILEDAVG_WERT | mA | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Durchschnittlicher Stromwert |
| STAT_TEMPAVG_WERT | °C | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Durchschnittliche Temperatur |
| STAT_UCOMP_DIFFAVG_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Durchschnittliche Abweichung des kompensierten Spannungswertes |
| STAT_BLK_COUNTER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der fehlerfreien N-1 Blinkphasenmessungen |
| STAT_ERR_COUNTER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Maximal aufgetretener N-1 Fehlerzählerwert |

<a id="table-res-0xfd5a-d"></a>
### RES_0XFD5A_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RELATIVZEIT_EINLERNEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Relativzeit zum Einlernzeitpunkt |
| STAT_RELATIVZEIT_LETZTER_DRIFT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Relativzeit beim letzten Drift der N-1 Referenzspannung |
| STAT_FRAZ_SYNC_HIGH_TIME_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | High-Zeit der FRAZ_SYNC-Leitung in Sekunden |
| STAT_ERR_COUNTER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Aktueller N-1 Fehlerzähler-Wert |

<a id="table-res-0xfd5b-d"></a>
### RES_0XFD5B_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VBAT_WERT | mV | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Steuergeräte-Versorgungsspannung |
| STAT_SOLLSTROM_LM1_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM1 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM1_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM1-LED |
| STAT_SOLLSTROM_LM2_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM2 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM2_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM2-LED |
| STAT_SOLLSTROM_LM3_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM3 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM3_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM3-LED |
| STAT_SOLLSTROM_LM4_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM4 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM4_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM4-LED |
| STAT_SOLLSTROM_LM5_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM5 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM5_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM5-LED |
| STAT_SOLLSTROM_LM6_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM6 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM6_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM6-LED |
| STAT_SOLLSTROM_LM7_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM7 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM7_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM7-LED |
| STAT_SOLLSTROM_LM8_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM8 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM8_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM8-LED |
| STAT_SOLLSTROM_LM9_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM9 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM9_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM9-LED |
| STAT_SOLLSTROM_LM10_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM10 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM10_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM10-LED |
| STAT_SOLLSTROM_LM11_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM11 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM11_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM11-LED |
| STAT_SOLLSTROM_LM12_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollstrom für LM12 (aus Codierdaten, anhängig von der Binningklasse) |
| STAT_REDUZIERUNGSFAKTOR_LM12_WERT | % | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | spannungsbedingter Stromreduzierungsfaktor der LM12-LED |

<a id="table-scheinwerferhersteller"></a>
### SCHEINWERFERHERSTELLER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | AL |
| 0x03 | Hella |
| 0x04 | ZKW |
| 0x05 | Valeo |

<a id="table-scheinwerfervariante"></a>
### SCHEINWERFERVARIANTE

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AHL/ECE |
| 0x10 | AHL/SAE |
| 0x20 | Bixenon/ECE |
| 0x30 | Bixenon/SAE |
| 0x40 | Halogen/ECE |
| 0x50 | Halogen/SAE |
| 0x60 | LED/ECE |
| 0x70 | LED/SAE |
| 0x80 | LED_LSR/ECE |
| 0x90 | LED_LSR/SAE |
| 0xA0 | LED_AHL/ECE |
| 0xB0 | LED_AHL/SAE |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 66 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| AHL_REFERENZLAUF | 0xA538 | - | Referenzlauf Kurvenlicht | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA538_R |
| LWR_REFERENZLAUF | 0xA541 | - | Referenzlauf der Leuchtweitenregulierung | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA541_R |
| LEUCHTEN_FUNKTION_LED | 0xA543 | - | Ansteuerung der LED Leuchtmittel | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA543_R | RES_0xA543_R |
| POSITION_LWR | 0xA545 | - | LWR Positionsvorgabe | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA545_R | RES_0xA545_R |
| POSITION_AHL | 0xA546 | - | Position AHL | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA546_R | RES_0xA546_R |
| 2_LUEFTER_AUSSENLICHT | 0xA547 | - | Ansteuerung der 2 Lüfter im Scheinwerfer | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA547_R | RES_0xA547_R |
| FUNKTIONSTEST_SCHEINWERFER | 0xA548 | - | Funktionstest der LED Scheinwerfer | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA548_R |
| FUNKTIONSTEST_LASER_LEUCHTMITTEL | 0xA5A7 | - | Funktionstest | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA5A7_R |
| LASER_FEHLER_DETAILS | 0xA801 | - | Zusatzinformationen bei Laserfehlern auslesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xA801_D |
| REFERENZLAUFZAEHLER_LWR | 0xD1FD | - | Anzahl der begonnenen und abgeschlossenen Referenzläufe | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD1FD_D | RES_0xD1FD_D |
| REFERENZLAUFZAEHLER_AHL | 0xD1FE | - | Anzahl der begonnenen und abgeschlossenen Referenzläufe | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD1FE_D | RES_0xD1FE_D |
| FRAZ_LED_AUSFALL_EINLERNDATEN | 0xD506 | - | Ausfallerkennung für FRAZ  | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD506_D | RES_0xD506_D |
| LEUCHTEN_SENSOR_AUSSTATTUNG | 0xD529 | - | Bei FLE2 und FLM werden die Eingangskanäle variantenabhängig für NTC-/Binning-Verwendung konfiguriert / codiert. Mit diesem Job kann die Zuordnung zu den Eingangskanälen am Steuergerät ausgelesen werden, um  DTC-Einträge oder Daten aus anderen Diagnosejobs (bzgl. Verwendung in codierter Scheinwerfervariante) zuzuordnen.  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD529_D |
| LEUCHTEN_AUSSENLICHT_TEMPERATUR | 0xD630 | - | gibt die Rohwerte der Temperatursensoren, die berechneten Werte für die Leuchten und die Derating-Status aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD630_D |
| LEUCHTEN_TEMP_HISTOGRAMM | 0xD632 | - | Ausgabe der Temperatur Histogramme | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD632_D |
| STATISTIKZAEHLER | 0xD633 | - | Statistikzähler | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD633_D | - |
| BETRIEBSDAUER_KANAELE | 0xD634 | - | Löscht den Betriebsstundenzähler des entsprechenden Kanals | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD634_D | RES_0xD634_D |
| LEUCHTEN_SENSE | 0xD635 | - | gibt die Gesamtstromaufnahme und die gemessene BN-Spannung zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD635_D |
| LWR_TEMPERATURMODUS | 0xD636 | - | Temperaturmodus LWR | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD636_D |
| SCHEINWERFERDATEN | 0xD637 | STAT_SCHEINWERFERDATEN_DATA | Scheinwerferspezifische Daten | DATA | - | high | data[16] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| LED_BINNING | 0xD638 | - | Gibt die ausgewählte Binningklasse und den entsprecheden Rohwert zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD638_D |
| SCHEINWERFER_LUEFTER | 0xD639 | - | Gibt den Betriebszustand und die Betriebsparameter des Lüfters zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD639_D |
| AUSSTATTUNG_FLE | 0xD63A | - | Gibt die verbaute Konfiguration aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD63A_D |
| POSITION_LEUCHTWEITENREGULIERUNG | 0xD63B | STAT_POSITION_LWR_WERT | Lesen der LWR Position | ° | - | high | signed char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| RESETZAEHLER | 0xD63C | - | Erfassung der Resetvorgänge | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD63C_D | RES_0xD63C_D |
| BETRIEBSSTUNDENZAEHLER_LWR | 0xD63D | - | Erfassung der Betriebsstunden LWR | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD63D_D | RES_0xD63D_D |
| STATUS_SCHEINWERFER_VARIANTE | 0xD63E | - | Lesen der codierbaren Variantenkennung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD63E_D |
| AHL_TEMPERATURMODUS | 0xD662 | - | Temperaturmodus AHL | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD662_D |
| SCHEINWERFER_LED_KANAL | 0xD667 | - | Aktivierung der einzelnen LED Kanäle des Frontscheinwerfers | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD667_D |
| BETRIEBSSTUNDENZAEHLER_AHL | 0xD680 | - | Betriebsstunden AHL | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD680_D | RES_0xD680_D |
| ZFL_SENSOR | 0xDCA0 | - | gibt die ZFL-Sensorsignale als Rohwerte zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCA0_D |
| AHL_POSITION | 0xDF05 | STAT_AHL_POSITION_WERT | Position Kurvenlicht | ° | - | high | signed int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AHL_SCHRITTVERLUSTE | 0xDF0F | - | Zähler der Kurvenlicht Schrittverlust | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDF0F_D | RES_0xDF0F_D |
| SW_BINNING | 0xE2F6 | - | Schreiben / Lesen der sw-basierten Binning Information FL-SGs | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xE2F6_D | RES_0xE2F6_D |
| LASER_VERRIEGELUNG_ZURUECKSETZEN | 0xE34C | - | Diagnosejob zur Entriegelung des Lasers | - | - | - | - | - | - | - | - | - | 2E | ARG_0xE34C_D | - |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | high | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| _LEUCHTEN_AUSSENLICHT_KANAL | 0x3000 | - | Ansteuern der einzelnen LED Kanäle | - | - | - | - | - | - | - | - | - | 31 | ARG_0x3000_R | RES_0x3000_R |
| _SCHEINWERFERDATENBLOCK | 0xFD40 | - | Bei der Scheinwerferfertigung können die Daten im Steuergerät abgelegt werden. Dies referenziert auf DID SCHEINWERFERDATEN. | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xFD40_D | RES_0xFD40_D |
| _FRAZ_ZUSTAND | 0xFD41 | - | Informationen zum aktuellen Zustand der FRAZ-Leitung und dem Blinker-Stromwert während der letzten EIN-Phase. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD41_D |
| _SG_ECUVARCFG | 0xFD42 | STAT_ECUVARCFG_DATA | Datenblock 'EcuVarCfg' | DATA | - | high | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _CODING_PLAUSIBILITAETSCHECK | 0xFD43 | - | Informationen zum Plausibilitätscheck der Codierung (als flüchtige RAM-Daten) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD43_D |
| _ADC_ROHWERTE | 0xFD44 | - | Liefert die Rohwerte der 37 Analog-/Digital-Converter-Kanäle zurück (Betriebsspannung, Lüfter, Links-/Rechts-Erkennung, Temperatur, Binning-/NTC-Eingänge etc.). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD44_D |
| _SG_EFTCALIBBLOCK_1 | 0xFD45 | STAT_EFTCALIBBLOCK_1_DATA | Datenblock 'EftCalibBlock' Teil 1 | DATA | - | high | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _SG_EFTCALIBBLOCK_2 | 0xFD46 | STAT_EFTCALIBBLOCK_2_DATA | Datenblock 'EftCalibBlock' Teil 2 | DATA | - | high | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _LEISTUNGSREDUZIERUNG | 0xFD47 | - | Informationen zum aktuellen Derating-Zustand des Thermomodells | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD47_D |
| _LED_STRANGSPANNUNG | 0xFD48 | - | Liest für alle LED-Kanäle die Strangspannung während der letzten EIN-Phase sowie die zugehörigen Minimal- und Maximal-Strangspannungen aus den Codierdaten. Die höheren Kanal-Nummer liefern je nach  Steuergerät und Bestückung ggf. Dummy-Werte. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD48_D |
| _CDDLED_TREIBER_1_SPI_REG | 0xFD4A | - | Liest die SPI-Register des Treiber-Bausteins 1 (für die LED-Kanäle 1 und 2) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4A_D |
| _CDDLED_TREIBER_2_SPI_REG | 0xFD4B | - | Liest die SPI-Register des Treiber-Bausteins 2 (für die LED-Kanäle 3 und 4) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4B_D |
| _CDDLED_TREIBER_3_SPI_REG | 0xFD4C | - | Liest die SPI-Register des Treiber-Bausteins 3 (für die LED-Kanäle 5 und 6) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4C_D |
| _CDDLED_TREIBER_4_SPI_REG | 0xFD4D | - | Liest die SPI-Register des Treiber-Bausteins 4 (für die LED-Kanäle 7 und 8) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4D_D |
| _CDDLED_TREIBER_5_SPI_REG | 0xFD4E | - | Liest die SPI-Register des Treiber-Bausteins 5 (für die LED-Kanäle 9 und 10) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4E_D |
| _CDDLED_TREIBER_6_SPI_REG | 0xFD4F | - | Liest die SPI-Register des Treiber-Bausteins 6 (für die LED-Kanäle 11 und 12) aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD4F_D |
| _CDDSTP_LWR_TREIBER_STATUS | 0xFD50 | - | Liest die internen Zustände der CddStp-LWR-Treiber-Status-Maschine aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD50_D |
| _CDDSTP_AHL_TREIBER_STATUS | 0xFD51 | - | Liest die internen Zustände der CddStp-AHL-Treiber-Status-Maschine aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD51_D |
| _CDDSTP_LWR_TREIBER_SPI_REG | 0xFD52 | - | Liest die SPI-Register des LWR-Treiber-Bausteins aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD52_D |
| _CDDSTP_AHL_TREIBER_SPI_REG | 0xFD53 | - | Liest die SPI-Register des AHL-Treiber-Bausteins aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD53_D |
| _CDDSBC_TREIBER_SPI_REG | 0xFD54 | - | Liest die SPI-Register des SBC aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD54_D |
| _LUEFTER_1_FREQUENZ | 0xFD55 | - | Liest die momentane Frequenz des Lüfters 1 sowie die minimale und maximale Frequenz aus den Codierdaten aus. Sonderwerte für die  momentane Frequenz:  0 = Lüfter aus; 0xFFFF = Lüfter nicht verbaut;  bei Lüftern ohne PWM-Ausgang wird für alle 3 Werte 0xFFFE zurückgegeben. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD55_D |
| _LUEFTER_2_FREQUENZ | 0xFD56 | - | Liest die momentane Frequenz des Lüfters 2 sowie die minimale und maximale Frequenz aus den Codierdaten aus. Sonderwerte für die  momentane Frequenz:  0 = Lüfter aus; 0xFFFF = Lüfter nicht verbaut;  bei Lüftern ohne PWM-Ausgang wird für alle 3 Werte 0xFFFE zurückgegeben. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD56_D |
| _WECKEREIGNIS | 0xFD57 | STAT_WECKEREIGNIS | Ursache für das letzte Weckereignis | 0-n | - | high | unsigned int | TAB_WECKEREIGNIS | - | - | - | - | 22 | - | - |
| FRAZ_N_MINUS_1_STATISTIK_1 | 0xFD58 | - | Liest bzw. löscht die Statistikdaten der N-minus-1-Ausfallerkennung des Fahrtrichtungsanzeigers. | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xFD58_D | RES_0xFD58_D |
| FRAZ_N_MINUS_1_ERWEITERTE_DATEN | 0xFD5A | - | Liest die erweiterten Daten der N-minus-1-Ausfallerkennung des Fahrtrichtungsanzeigers. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD5A_D |
| _LED_STROMABREGELUNG | 0xFD5B | - | Informationen zur aktuellen spannungsbedingten LED-Stromabregelung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xFD5B_D |

<a id="table-tab-ahl-referenzlauf"></a>
### TAB_AHL_REFERENZLAUF

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Referenzlauf nicht gestartet |
| 0x01 | Referenzlauf aktiv |
| 0x02 | Referenzlauf ohne Fehler abgeschlossen |
| 0x03 | Refernezlauf mit Fehler abgebrochen |
| 0xFF | ungültiger Wert |

<a id="table-tab-einlerndaten-nvm-status"></a>
### TAB_EINLERNDATEN_NVM_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NVM_OK |
| 1 | NVM_NOT_OK |
| 2 | NVM_REQ_PENDING |
| 3 | NVM_REQ_DENIED |
| 4 | NVM_SHUTDOWNWRITE |

<a id="table-tab-einlerndaten-status"></a>
### TAB_EINLERNDATEN_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht eingelernt |
| 1 | links eingelernt |
| 2 | rechts eingelernt |

<a id="table-tab-fle-leuchtmittel"></a>
### TAB_FLE_LEUCHTMITTEL

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | LED 1 |
| 0x02 | LED 2 |
| 0x03 | LED 3 |
| 0x04 | LED 4 |
| 0x05 | LED 5 |
| 0x06 | LED 6 |
| 0x07 | LED 7 |
| 0x08 | LED 8 |
| 0x09 | LED 9 |
| 0x0A | LED 10 |
| 0x0B | LED 11 |
| 0x0C | LED 12 |

<a id="table-tab-fraz-messung"></a>
### TAB_FRAZ_MESSUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | noch keine Messung erfolgt |
| 1 | Messung bereits ausgelesen |
| 2 | Messung erfolgt, noch nicht ausgelesen |

<a id="table-tab-funktion-fle"></a>
### TAB_FUNKTION_FLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht verbaut |
| 0x01 | verbaut und aktiv |
| 0x02 | verbaut und nicht aktiv |

<a id="table-tab-grund-implausibel"></a>
### TAB_GRUND_IMPLAUSIBEL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | (Default) |
| 1 | Codierdaten unplausibel bzw. ungeeignet |
| 2 | Codierdaten inkompatibel zu Steuergeräte-Hardware |

<a id="table-tab-led-leuchtmittel"></a>
### TAB_LED_LEUCHTMITTEL

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | LED 1 |
| 0x02 | LED 2 |
| 0x03 | LED 3 |
| 0x04 | LED 4 |
| 0x05 | LED 5 |
| 0x06 | LED 6 |
| 0x07 | LED 7 |
| 0x08 | LED 8 |
| 0x09 | LED 9 |
| 0x0A | LED 10 |
| 0x0B | LED 11 |
| 0x0C | LED 12 |
| 0xFF | alle Leuchtmittel |

<a id="table-tab-leuchten-sensor"></a>
### TAB_LEUCHTEN_SENSOR

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht verbaut |
| 0x01 | NTC1 |
| 0x02 | NTC2 |
| 0x03 | NTC3 |
| 0x04 | NTC4 |
| 0x05 | NTC5 |
| 0x06 | NTC6 |
| 0x07 | NTC7 |
| 0x08 | Binning 1 |
| 0x09 | Binning 2 |
| 0x0A | Binning 3 |
| 0x0B | Binning 4 |
| 0x0C | Binning 5 |
| 0x0D | Binning 6 |
| 0x0E | Binning 7 |
| 0x0F | Binning 8 |
| 0x10 | Binning 9 |
| 0x11 | Binning 10 |
| 0x12 | Binning 11 |
| 0x13 | Binning 12 |

<a id="table-tab-leuchtmittel"></a>
### TAB_LEUCHTMITTEL

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht verbaut |
| 0x01 | Abblendlicht 1 |
| 0x02 | Abblendlicht 2 |
| 0x03 | Abblendlicht 3 |
| 0x04 | Abblendlicht 4 |
| 0x05 | Fernlicht 1 |
| 0x06 | Fernlicht 2 |
| 0x07 | Fernlicht 3 |
| 0x08 | Tagfahrlicht 1 |
| 0x09 | Tagfahrlicht 2 |
| 0x0A | Tagfahrlicht 3 |
| 0x0B | Abbiegelicht 1 |
| 0x0C | Abbiegelicht 2 |
| 0x0D | Abbiegelicht 3 |
| 0x0E | Seitenmarkierungsleuchte 1 |
| 0x0F | Seitenmarkierungsleuchte 2 |
| 0x10 | Seitenmarkierungsleuchte 3 |
| 0x11 | Fahrtrichtungsanzeiger 1 |
| 0x12 | Zusatzfernlicht-Laser 1 |
| 0x13 | Inszenierungslicht 1 |
| 0x14 | Zusatzfernlicht-Laser 2 |

<a id="table-tab-lr-aktive-lichtfunktion"></a>
### TAB_LR_AKTIVE_LICHTFUNKTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | CE |
| 1 | VTW |
| 2 | R |
| 0xFF | keine |

<a id="table-tab-lr-status"></a>
### TAB_LR_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalbetrieb |
| 1 | LR 1 |
| 2 | LR 2 |
| 3 | LR 3 |

<a id="table-tab-lwr-referenzlauf"></a>
### TAB_LWR_REFERENZLAUF

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Referenzlauf nicht gestartet |
| 0x01 | Referenzlauf aktiv |
| 0x02 | Referenzlauf ohne Fehler abgeschlossen |
| 0x03 | Referenzlauf mit Fehler abgebrochen |
| 0xFF | ungültiger Wert |

<a id="table-tab-pos-ahl"></a>
### TAB_POS_AHL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Job aktiv |
| 0x01 | Job nicht aktiv |
| 0x02 | Job erfolgreich abgeschlossen |
| 0xFF | Fehler |

<a id="table-tab-pos-lwr"></a>
### TAB_POS_LWR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Job aktiv |
| 0x01 | Job nicht aktiv |
| 0x02 | Job erfolgreich abgeschlossen |
| 0xFF | Fehler |

<a id="table-tab-weckereignis"></a>
### TAB_WECKEREIGNIS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | (Default) |
| 1 | Klemme-30-Wakeup (Power-On) |
| 4 | Software-Reset |
| 8 | Watchdog-Reset |
| 32 | CAN-Wakeup |
| 64 | PLL-Unlock |
| 256 | Blinker |
