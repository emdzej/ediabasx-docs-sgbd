# sle_f15.prg

- Jobs: [35](#jobs)
- Tables: [51](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Standardladeelektronik incl. Ladeinterfacemodul, SGBD Index: 0x0F1EC0 |
| ORIGIN | BMW EA-441 Dennis_Dumke |
| REVISION | 5.002 |
| AUTHOR | ALTRAN-DEUTSCHLAND-S.A.S.&-CO. EA-451 SalamancaRios |
| COMMENT | Umsetzung der nach Neubewertung OBD-relevanten DTCs für SLE und Umsetzung des UDS Job in der 249.100.001 |
| PACKAGE | 1.989 |
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
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (9 × 9)
- [TAB_ZEIT_SYNCMETHOD](#table-tab-zeit-syncmethod) (4 × 2)
- [TAB_ZEIT_USER_INFO](#table-tab-zeit-user-info) (8 × 2)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XAF40_R](#table-arg-0xaf40-r) (1 × 14)
- [ARG_0XAF41_R](#table-arg-0xaf41-r) (1 × 14)
- [ARG_0XDEF0_D](#table-arg-0xdef0-d) (1 × 12)
- [ARG_0XDEF1_D](#table-arg-0xdef1-d) (1 × 12)
- [ARG_0XDEF3_D](#table-arg-0xdef3-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (185 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (51 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (23 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (51 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [LADEN_LED_STATUSANZEIGE](#table-laden-led-statusanzeige) (7 × 2)
- [OBC_STATE_TYPE](#table-obc-state-type) (10 × 2)
- [RES_0XAF40_R](#table-res-0xaf40-r) (2 × 13)
- [RES_0XAF41_R](#table-res-0xaf41-r) (5 × 13)
- [RES_0XDEF0_D](#table-res-0xdef0-d) (2 × 10)
- [RES_0XDEF1_D](#table-res-0xdef1-d) (2 × 10)
- [RES_0XDEF3_D](#table-res-0xdef3-d) (1 × 10)
- [RES_0XDEF5_D](#table-res-0xdef5-d) (2 × 10)
- [RES_0XDEF6_D](#table-res-0xdef6-d) (6 × 10)
- [RES_0XDF29_D](#table-res-0xdf29-d) (2 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (28 × 16)
- [ST_CHGNHG_VALUES](#table-st-chgnhg-values) (6 × 2)
- [ST_CHGRDY_VALUE](#table-st-chgrdy-value) (3 × 2)
- [TAB_BETRIEBSART](#table-tab-betriebsart) (10 × 2)
- [TAB_BETRIEBSART_LADEGERAET_KOMMANDIEREN](#table-tab-betriebsart-ladegeraet-kommandieren) (1 × 2)
- [TAB_FUNKSTATUS](#table-tab-funkstatus) (12 × 2)
- [TAB_LADEKLAPPE](#table-tab-ladeklappe) (3 × 2)
- [TAB_LIM_STECKER](#table-tab-lim-stecker) (4 × 2)
- [TAB_SLE_TEMPERATURSENSOR](#table-tab-sle-temperatursensor) (3 × 2)
- [TAB_ZV_LADEKLAPPE](#table-tab-zv-ladeklappe) (3 × 2)
- [TAB_0X400D](#table-tab-0x400d) (1 × 4)
- [TAB_0X401B](#table-tab-0x401b) (1 × 2)
- [WAKEUP_SOURCE_TABLE](#table-wakeup-source-table) (7 × 2)
- [ZV_LADESTECKER](#table-zv-ladestecker) (4 × 2)

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
| 0x01 | ms ECU overall, not comparable |
| 0x02 | ms ECU overall, not comparable |
| 0x03 | invalid |
| 0x04 | insync, ms ECU overall, not comparable |
| 0x05 | ms ECU overall, comparable |
| 0x06 | ms ECU overall, comparable |
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

<a id="table-arg-0xaf40-r"></a>
### ARG_0XAF40_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSART | + | - | 0-n | high | unsigned char | - | TAB_BETRIEBSART_LADEGERAET_KOMMANDIEREN | - | - | - | - | - | Gewünschte Betriebsart |

<a id="table-arg-0xaf41-r"></a>
### ARG_0XAF41_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TEMPERATUR_SENSOR | + | - | 0-n | high | unsigned char | - | TAB_SLE_TEMPERATURSENSOR | - | - | - | - | - | Auswahl Temperatursensor |

<a id="table-arg-0xdef0-d"></a>
### ARG_0XDEF0_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_ZV_LADESTECKER | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuern des Ladestecker (nur bei Typ 2 Stecker): 0 = entriegeln, 1 = verriegeln |

<a id="table-arg-0xdef1-d"></a>
### ARG_0XDEF1_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_ZV_LADEKLAPPE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ansteuern der Ladeklappe (0 = entriegeln, 1 = verriegeln) |

<a id="table-arg-0xdef3-d"></a>
### ARG_0XDEF3_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_LED_LADESTATUS | 0-n | high | unsigned char | - | LADEN_LED_STATUSANZEIGE | - | - | - | - | - | Ansteuern LED für Ladestatus (Leuchtprofile) |

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

Dimensions: 185 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021400 | Energiesparmode aktiv | 0 | - |
| 0x021408 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x021409 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02140A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02140B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02140C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02140D | Codierung: Codierdaten nicht qualifiziert | 0 | - |
| 0x02FF14 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x21E600 | Ladeanschluss: Gewaltrennung des Ladesteckers erkannt | 0 | - |
| 0x21E601 | Ladeunterbrechung - Kommunikationausfall | 0 | - |
| 0x21E602 | Ladeelektronik: Selbstschutz Notaus | 0 | - |
| 0x21E603 | Ladeelektronik: SW und HW inkompatibel | 0 | - |
| 0x21E606 | Ladeelektronik: Hardwarefehler erkannt | 0 | - |
| 0x21E609 | Zwischenstecker Pilot/Proxy nicht gesteckt | 0 | - |
| 0x21E60B | Ladeelektronik: Software-Fehler | 0 | - |
| 0x21E612 | Ladeunterbrechung - Temperaturunterschreitung | 0 | - |
| 0x21E615 | Ladeelektronik: Überspannung am DC-Anschluss | 0 | - |
| 0x21E616 | Ladeelektronik: Überspannung am AC-Anschluss | 0 | - |
| 0x21E617 | Ladeelektronik: Unterspannung am DC-Anschluss | 0 | - |
| 0x21E618 | Ladeelektronik: Unterspannung am AC-Anschluss | 0 | - |
| 0x21E619 | Ladeunterbrechung - Temperaturüberschreitung | 0 | - |
| 0x21E61C | Ladeelektronik:  HV AC Stromsensor oberen Schwellenwert überschritten | 0 | - |
| 0x21E61D | Ladeelektronik: Unterspannung an 12V Spannungsversorgung | 0 | - |
| 0x21E61E | Ladeelektronik: Überspannung an 12V Spannungsversorgung | 0 | - |
| 0x21E622 | Ladeelektronik, HV DC Spannungssensor: Kurzschluss nach Masse | 0 | - |
| 0x21E623 | Ladeelektronik, HV DC Spannungssensor: Kurzschluss nach Plus | 0 | - |
| 0x21E626 | Ladeelektronik, HV AC Spannungssensor: Kurzschluss nach Masse | 0 | - |
| 0x21E627 | Ladeelektronik, HV AC Spannungssensor: Kurzschluss nach Plus | 0 | - |
| 0x21E629 | Weckleitung 15_WUP unplausibel | 0 | - |
| 0x21E640 | Ladeelektronik, interner Fehler: AC Stromsensor, Kurzschluss nach Masse | 0 | - |
| 0x21E641 | Ladeelektronik, interner Fehler: Hochsetzsteller Spannungssensor, Kurzschluss nach Plus | 0 | - |
| 0x21E645 | Ladeelektronik, interner Fehler: Kühlmitteltemperatursensor, Kurzschluss nach Plus | 0 | - |
| 0x21E648 | Ladeelektronik, interner Fehler: Kühlmitteltemperatursensor, Kurzschluss nach Masse | 0 | - |
| 0x21E649 | Ladeelektronik, interner Fehler: Hochsetzsteller Spannungssensor, Messwert außerhalb Sollbereich (oben) | 0 | - |
| 0x21E64A | Ladeelektronik, interner Fehler: Hochsetzsteller Spannungssensor, Messwert außerhalb Sollbereich (unten) | 0 | - |
| 0x21E64B | Ladeelektronik, interner Fehler: AC Stromsensor, Kurzschluss nach Plus | 0 | - |
| 0x21E64D | Ladeelektronik, interner Fehler: AC Stromsensor, Leitungsunterbrechung | 0 | - |
| 0x21E64E | Ladeelektronik, interner Fehler: Umgebungstemperatursensor, Kurzschluss nach Plus | 0 | - |
| 0x21E64F | Ladeelektronik, interner Fehler: Umgebungstemperatursensor, Kurzschluss nach Masse | 0 | - |
| 0x21E652 | Ladeelektronik, interner Fehler: Hochsetzsteller Spannungssensor, Kurzschluss nach Masse | 0 | - |
| 0x21E653 | Ladeelektronik, interner Fehler: AC Stromsensor, Messwert außerhalb Sollbereich (unten) | 0 | - |
| 0x21E655 | Ladeelektronik, interner Fehler: Treiber Temperatursensor, Kurzschluss nach Masse | 0 | - |
| 0x21E658 | Ladeelektronik, interner Fehler: Treiber Temperatursensor, Kurzschluss nach Plus | 0 | - |
| 0x21E65C | Ladeelektronik, HV DC Stromsensor: Kurzschluss nach Masse | 0 | - |
| 0x21E65D | Ladeelektronik, HV DC Stromsensor: Kurzschluss nach Plus | 0 | - |
| 0x21E65F | Ladeelektronik: Crash über CAN erkannt | 1 | - |
| 0x21E660 | Ladeelektronik, HV DC Stromsensor: Unterer Schwellenwert unterschritten | 0 | - |
| 0x21E661 | Ladeelektronik, HV DC Stromsensor: Oberer Schwellenwert überschritten | 0 | - |
| 0x21E66F | Ladeanschlussklappe, Hallsensor, Versorgung Minus: Oberer Schwellenwert überschritten | 0 | - |
| 0x21E679 | Ladeanschlussklappe, Hallsensor, Versorgung Minus: Kurzschluss nach Masse | 0 | - |
| 0x21E67A | Ladeanschlussklappe, Hallsensor, Versorgung Minus: Kurzschluss nach Plus | 0 | - |
| 0x21E67B | Ladeanschlussklappe, Hallsensor: Leitungsunterbrechung | 0 | - |
| 0x21E67C | AC-Laden: Proximity Signal, Kurzschluss nach Masse | 0 | - |
| 0x21E67D | Ladeelektronik, Spannungsversorgung Sensoren: Unterer Schwellenwert unterschritten | 0 | - |
| 0x21E67E | Ladeelektronik, Spannungsversorgung Sensoren: Oberer Schwellenwert überschritten | 0 | - |
| 0x21E67F | Ladeanschlussklappe, Hallsensor, Versorgung Plus: Unterer Schwellenwert unterschritten | 0 | - |
| 0x21E680 | Ladeanschlussklappe, Hallsensor, Versorgung Plus: Oberer Schwellenwert überschritten | 0 | - |
| 0x21E681 | AC-Laden: Ladesteckererkennung unplausibel | 1 | - |
| 0x21E682 | Ladeanschluss: Verriegelung des Ladesteckers, Kurzschluss nach Masse | 0 | - |
| 0x21E683 | Ladeanschluss: Verriegelung des Ladesteckers, Kurzschluss nach Plus | 0 | - |
| 0x21E684 | Ladeanschluss: Verriegelung des Ladesteckers, Leitungsunterbrechung | 0 | - |
| 0x21E685 | Ladeanschlussklappe: Verriegelung, Kurzschluss nach Masse | 0 | - |
| 0x21E686 | Ladeanschlussklappe: Verriegelung, Kurzschluss nach Plus | 0 | - |
| 0x21E687 | Ladeanschlussklappe: Verriegelung, Leitungsunterbrechung | 0 | - |
| 0x21E688 | Entriegelung des Ladesteckers (Typ 1): Dauerbetätigung | 1 | - |
| 0x21E689 | Ladeanschluss: Verriegelung des Ladesteckers, Zustand unplausibel | 0 | - |
| 0x21E68C | Statusanzeige Laden: Ansteuerung, Kurzschluss nach Masse | 0 | - |
| 0x21E68D | Statusanzeige Laden: Ansteuerung, Kurzschluss nach Plus | 0 | - |
| 0x21E68E | Statusanzeige Laden: Ansteuerung, Leitungsunterbrechung | 0 | - |
| 0x21E691 | Ladeanschlussklappe und Ladeanschluss: Status unplausibel | 0 | - |
| 0x21E693 | AC-Laden: PWM-Signal, Frequenz ausserhalb Sollbereich | 1 | - |
| 0x21E694 | AC-Laden: PWM-Signal, Pegel ausserhalb Sollbereich | 1 | - |
| 0x21E696 | AC-Laden: PWM-Signal, Tastverhältnis ausserhalb Sollbereich | 1 | - |
| 0x21E697 | Ladeanschlussklappe, Hallsensor, Versorgung Plus: Kurzschluss nach Plus | 0 | - |
| 0x21E698 | Ladeanschluss: Sensor der Ladesteckerverriegelung, Kurzschluss nach Plus | 0 | - |
| 0x21E69A | Ladeanschluss: Sensor der Ladesteckerverriegelung, Kurzschluss nach Masse | 0 | - |
| 0x21E69B | Ladeanschlussklappe, Hallsensor, Versorgung Plus: Kurzschluss nach Masse | 0 | - |
| 0x21E69C | AC-Laden: PWM-Signal, Kurzschluss nach Plus | 0 | - |
| 0x21E69D | AC-Laden: kein Ladestecker erkannt obwohl Ladesterckerverriegelung aktiv | 0 | - |
| 0x21E69F | AC-Laden: unerwartete Spannung an der Ladevorrichtung detektiert | 1 | - |
| 0x21E6A0 | HV DC Anschluss 1 nicht gesteckt | 0 | - |
| 0x21E6A1 | HV DC Anschluss 2 nicht gesteckt | 0 | - |
| 0x21E6A2 | HV DC Anschluss 3 nicht gesteckt | 0 | - |
| 0x21E6A3 | HV AC Anschluss Ladedose nicht gesteckt | 0 | - |
| 0x21E6A4 | HV DC Anschluss 3, Steckererkennung: Kurzschluss nach Masse | 0 | - |
| 0x21E6A5 | HV DC Anschluss 3, Steckererkennung: Kurzschluss nach Plus | 0 | - |
| 0x21E6A6 | HV DC Anschluss 2, Steckererkennung: Kurzschluss nach Masse | 0 | - |
| 0x21E6A7 | HV DC Anschluss 2, Steckererkennung: Kurzschluss nach Plus | 0 | - |
| 0x21E6A8 | HV DC Anschluss 1, Steckererkennung: Kurzschluss nach Masse | 0 | - |
| 0x21E6A9 | HV DC Anschluss 1, Steckererkennung: Kurzschluss nach Plus | 0 | - |
| 0x21E6AA | HV AC Anschluss Ladedose, Steckererkennung: Kurzschluss nach Masse | 0 | - |
| 0x21E6AB | HV AC Anschluss Ladedose, Steckererkennung: Kurzschluss nach Plus | 0 | - |
| 0x21E6AC | Ladeelektronik, Umgebungstemperatur Sensor: Plausiblität | 0 | - |
| 0x21E6AD | Ladeelektronik, Kühlmitteltemperatur Sensor: Plausibilität | 0 | - |
| 0x21E6AE | Ladeelektronik, Wirkungsgrad: Plausibilität | 0 | - |
| 0x21E6AF | Ladeelektronik, AC Spannungssensor: Plausibilität | 0 | - |
| 0x21E6B0 | Ladeelektronik, AC Stromsensor: Plausibilität | 0 | - |
| 0x21E6B1 | Ladeelektronik, HV DC Stromsensor: Plausibilität | 0 | - |
| 0x21E6B2 | Ladeelektronik, HV DC Spannungssensor: Plausibilität | 0 | - |
| 0x21E6B3 | Ladeelektronik, Ausgangsspannung Hochsetzsteller: Plausibilität | 0 | - |
| 0x21E6B4 | Ladeelektronik, Leistungs-Feldeffekttransistor (FET), Temperatursensor: Plausibilität | 0 | - |
| 0x21E6B5 | Ladeelektronik: Fehler bei internem Watchdog und Überwachung Programmablauf | 0 | - |
| 0x21E6B6 | Ladeelektronik: Watchdog Power Down Test | 0 | - |
| 0x21E6B7 | Ladeelektronik: SPI Bus Performance | 0 | - |
| 0x21E6B8 | AC-Laden: Proximity Signal, unterer Schwellenwert unterschritten | 0 | - |
| 0x21E6B9 | AC-Laden: Proximity Signal, oberer Schwellenwert überschritten | 0 | - |
| 0x21E6FA | Ladeelektronik: RAM, Prüfsummenfehler | 0 | - |
| 0x21E6FB | Ladeelektronik, FLASH EEPROM: Prüfsummenfehler | 0 | - |
| 0x21E6FC | Ladeelektronik: ROM, Prüfsummenfehler | 0 | - |
| 0x21E6FE | Ladeelektronik: Programmablauf Fehler / Prozessorfehler | 0 | - |
| 0x21E701 | Ladeelektronik, interne Spannungsversorgung, Kurzschluss nach Masse | 0 | - |
| 0x21E702 | Ladeelektronik, interne Spannungsversorgung Kurzschluss nach Plus | 0 | - |
| 0x21E703 | Ladeelektronik, Parameter Aktuator Ladeklappenverriegelung, geringe Glaubwürdigkeit | 0 | - |
| 0x21E704 | Sensor Ladeklappe, Parameter Klappensensor, hohe Glaubwürdigkeit | 0 | - |
| 0x21E705 | Ladeelektronik, Sensor Umgebungstemperatur, hohe Glaubwürdigkeit | 0 | - |
| 0x21E706 | Ladeelektronik, Parameter Sensor Temperatur Kühlmittel: hohe Glaubwürdigkeit | 0 | - |
| 0x21E707 | Ladeelektronik, Leistungs Feldeffekttransistor (FET), Parameter Temperatursensor: hohe Glaubwürdigkeit | 0 | - |
| 0x21E708 | Ladeelektronik, Kaltstart Plausibilitätscheck | 0 | - |
| 0x21E709 | Ladeelektronik, Kaltstartprüfung Plausibilität zwischen Kühlmitteltemperatur und Umgebungstemperatur | 0 | - |
| 0x21E70A | HV AC Current Limit Rationality based on CAN signal | 0 | - |
| 0x21E70B | HV DC Output Current Limit Rationality based on CAN limit | 0 | - |
| 0x21E70C | S2 Switch Monitor Fault | 0 | - |
| 0x21E710 | Ladeelektronik, Parameter Wirkungsgrad: hohe Glaubwürdigkeit | 0 | - |
| 0x21E711 | Ladeelektronik, Parameter AC Stromsensor: hohe Glaubwürdigkeit | 0 | - |
| 0x21E712 | Ladeelektronik, Parameter HV DC Stromsensor: hohe Glaubwürdigkeit | 0 | - |
| 0x21E713 | Ladeelektronik, Parameter HV DC Spannungssensor: hohe Glaubwürdigkeit | 0 | - |
| 0x21E714 | Ladeelektronik, Parameter Ausgangsspannung Hochsetzsteller: hohe Glaubwürdigkeit | 0 | - |
| 0x21E715 | Ladeelektronik, RAM Testmust interner Fehler | 0 | - |
| 0x21E716 | HV AC Anschluss Ladedose nicht gesteckt | 0 | - |
| 0x21E717 | HV DC Anschluss  1, nicht gesteckt | 0 | - |
| 0x21E718 | HV DC Anschluss 2, nicht gesteckt | 0 | - |
| 0x21E719 | HV DC Anschluss 3, nicht gesteckt | 0 | - |
| 0x21E71A | Charger electronics,  Precharge Ready Timeout | 0 | - |
| 0x21E71B | Charger Electronics; Software Error Stack overflow | 1 | - |
| 0x21E71C | Charger Electronics:  Memory Protection Error | 0 | - |
| 0x21E720 | HV DC Kabel an Leistungselektronik Richtung Ladegerät nicht angeschlossen | 0 | - |
| 0xCE040A | FA-CAN Control Module Bus OFF | 0 | - |
| 0xCE0486 | A-CAN Control Module Bus OFF | 0 | - |
| 0xCE0BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xCE1401 | Undefined Signal(ST_GRSEL_DRV,0x3F9) Reciever SLE, trasmitter DME | 1 | - |
| 0xCE1402 | FA-CAN, Botschaft (Zustand Fahrzeug, 0x3C) fehlt, Empfänger SLE, Sender ZGW | 1 | - |
| 0xCE1404 | Invalid_Signal(ST_GRSEL_DRV,0x3F9) Reciever SLE, trasmitter DME | 1 | - |
| 0xCE1405 | FA-CAN, Botschaft (Klemmen, 0x12F) fehlt, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE1406 | FA-CAN, Botschaft (Fahrzeugsgeschwindigkeit, 0x1A1) fehlt, Empfänger SLE, Sender DSC | 1 | - |
| 0xCE1409 | FA-CAN, Botschaft (Zentralverriegelung und Klappenzustand, 0x2FC) fehlt, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE140B | FA-CAN, Botschaft (Steuerung Zentralverriegelung, 0x2A0) fehlt, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE140D | FA-CAN, Botschaft (Relativzeit, 0x328) fehlt, Empfänger SLE, Sender KOMBI | 1 | - |
| 0xCE140E | FA-CAN, Botschaft (Kilometerstand und Reichweite, 0x330) fehlt, Empfänger SLE, Sender KOMBI | 1 | - |
| 0xCE140F | FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0) fehlt, Empfänger SLE, Sender ZGW | 1 | - |
| 0xCE1410 | FA-CAN, Botschaft (Ladestatus, 0x3E9) fehlt, Empfänger SLE, Sender AE | 1 | - |
| 0xCE1411 | FA-CAN, Botschaft (Daten Antriebsstrang 2, 0x3F9) fehlt, Empfänger SLE, Sender DME | 1 | - |
| 0xCE1412 | Signal (ST_KL, 0x12F) nicht defniert, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE1413 | Signal (ST_CHGRDI, 0x3E9) nicht definiert, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1414 | Signal (ST_CHGRDI,0x3E9) nicht definiert, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1415 | Signal (CTR_SWO_EKP_CR, 0x19B) ungültig, Empfänger SLE, Sender ACSM | 1 | - |
| 0xCE1416 | Signal (CTR_SWO_EKP_CR, 0x19B) nicht definiert, Empfänger SLE, Sender ACSM | 1 | - |
| 0xCE1417 | Signal (CTR_CLSY_DRD, 0x2A0) ungültig, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE1418 | Signal (ST_CLSY, 0x2FC) ungültig, Empfänger SLE, Sender BDC | 1 | - |
| 0xCE1419 | Keine Meldung ( Steuerung Crash, 19B), Empfänger SLE, Sender DSC | 1 | - |
| 0xCE1500 | Keine Meldung (Kilometerstand, 0x330), Empfänger SLE, Sender Kombi | 1 | - |
| 0xCE1501 | Keine Meldung (CTR_PRNT, 0x09E), Empfänger SLE, Sender EME | 1 | - |
| 0xCE1502 | Keine Meldung (ST_HVSTO_1, 0x1FA), Empfänger SLE, Sender KMU | 1 | - |
| 0xCE1505 | Keine Meldung (ST_OPMO_MOT_TRCT, 2E8) SLE Empfänger, Sender EME | 1 | - |
| 0xCE1506 | Keine Meldung (SPEC_CF_CHGE, 0x153) SLE Empfänger, Sender EME | 1 | - |
| 0xCE1507 | A-CAN, Botschaft (Status Hochvolt-Batterieeinheit 2, 0x112) fehlt, Empfänger SLE, Sender SME | 1 | - |
| 0xCE1509 | A-CAN, Botschaft (Hochvolt-Batterie, 0x431) fehlt, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150A | Signal (ST_SER_DSCO_PLG, 0x431) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150B | Signal (ST_SER_DSCO_PLG, 0x431) nicht definiert, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150C | Signal (ST_DCSW_HVSTO, 0x1FA) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150D | Signal (AVL_U_HVS, 0x112) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150E | Signal (AVL_U_HVS, 0x112) nicht defniniert, Empfänger SLE, Sender SME | 1 | - |
| 0xCE150F | Signal (RQ_OPN_DCSW_HVSTO_ILY, 0x112) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE1510 | Signal (RQ_OPN_DCSW_HVSTO_FAST, 0x112) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE1511 | Signal (AVL_U_LINK, 0x112) ungültig, Empfänger SLE, Sender SME | 1 | - |
| 0xCE1512 | Signal (AVL_U_LINK, 0x112) nicht definiert, Empfänger SLE, Sender SME | 1 | - |
| 0xCE1513 | Signal (CTR_FKTN_PRTNT_DRV, 0x19E) ungültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1514 | Signal (CTR_BS_PRTNT_DRV, 0x19E) ungültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1515 | Signal (SPEC_U_MAX_CHG_CHGE, 0x153) undgültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1516 | Signal (SPEC_U_MAX_CHG_CHGE, 0x153) nicht definiert, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1517 | Signal (SPEC_I_MAX_ALTC_CF_CHGE, 0x153) ungültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1518 | Signal (SPEC_I_MAX_DC_CF_CHGE, 0x153) ungültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE1519 | Signal (TAR_OPMO_CF_CHGE, 0x153) ungültig, Empfänger SLE, Sender EME | 1 | - |
| 0xCE151A | Signal (TAR_OPMO_CF_CHGE, 0x153) nicht definiert, Empfänger SLE, Sender EME | 1 | - |
| 0xCE151B | Signal ( TAR_PWR_CF_CHGNG, 0x153) ungültig, Empfänger SLE,  Sender EME | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 51 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | MAJOR | HEX | High | - | - | - | - | - |
| 0x0002 | MINOR | HEX | High | - | - | - | - | - |
| 0x0003 | PATCH | HEX | High | - | - | - | - | - |
| 0x0004 | PROGRAM_FLOW_TASK_INDICATION | 0-n | High | 0xFF | - | - | - | - |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x2001 | ChargeReadiness | 0-n | Low | 0xFF | ST_CHGRDY_VALUE | - | - | - |
| 0x2002 | ChargeStatus | 0-n | Low | 0xFF | ST_CHGNHG_VALUES | - | - | - |
| 0x4000 | Boost Voltage | V | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4001 | Coolant Temperature | °C | High | unsigned int | - | 1.0 | 2.0 | -45.0 |
| 0x4002 | Umgebungstemperatur | °C | High | unsigned char | - | 1.0 | 2.0 | -45.0 |
| 0x4003 | Stromversorgungsgerät Temperatur | °C | High | unsigned char | - | 1.0 | 2.0 | -45.0 |
| 0x4004 | Externe A / D referance Spannung | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4005 | Pilot Frequency | Hz | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4006 | Pilot_Dutycycle | % | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4007 | LED1 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4008 | LED2 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4009 | LED3 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400A | Proximity AD | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400B | Pilot AD | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400C | Control board ID | Byte | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x400D | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x400E | Hardware Overvoltage | 0/1 | High | 0x01 | - | - | - | - |
| 0x400F | Hardware Overcurrent | 0/1 | High | 0x01 | - | - | - | - |
| 0x4010 | Wakeup Source | 0-n | High | 0xFF | WAKEUP_SOURCE_TABLE | - | - | - |
| 0x4011 | OBC_STATE | 0-n | High | 0xFF | OBC_STATE_TYPE | - | - | - |
| 0x4012 | AC Line Frequency | Hz | High | unsigned char | - | 1.0 | 4.0 | 0.0 |
| 0x4013 | DC Output Power | W | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4014 | AC Line Voltage | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4015 | HVDC Voltage | V | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4016 | HVDC Current | A | High | unsigned int | - | 1.0 | 10.0 | -204.0 |
| 0x4017 | AC Line Current | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4018 | LV Battery Voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4019 | Address of the exception | HEX | High | unsigned long | - | - | - | - |
| 0x401A | Address of exception access | HEX | High | unsigned long | - | - | - | - |
| 0x401B | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x401C | PlugLock Current | A | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0x401D | FlapLock Current | A | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0x401E | SEC_DTC_FOR_21E602 | HEX | High | unsigned long | - | - | - | - |
| 0x401F | SEC_DTC_FOR_21E606 | HEX | High | unsigned long | - | - | - | - |
| 0x4020 | SEC_DTC_FOR_21E615 | HEX | High | unsigned long | - | - | - | - |
| 0x4021 | SEC_DTC_FOR_21E619 | HEX | High | unsigned long | - | - | - | - |
| 0xDF20 | STAT_BETRIEBSART | 0-n | High | 0xFF | TAB_BETRIEBSART | - | - | - |
| 0xDF26 | STAT_NETZFREQUENZ_WERT | - | High | unsigned char | - | 1.0 | 4.0 | 0.0 |
| 0xDF2E | STAT_HVDC_LEISTUNG_WERT | W | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0xDF31 | STAT_AC_SPANNUNG_EFFEKTIV_WERT | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xDF32 | STAT_HVDC_SPANNUNG_WERT | V | High | unsigned int | - | 1.0 | 50.0 | 0.0 |
| 0xDF35 | STAT_HVDC_STROM_MAX_WERT | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0xDF36 | STAT_AC_STROM_EFFEKTIV_LEITER_WERT | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0xDF38 | STAT_SPANNUNG_KL30_WERT | V | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
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

Dimensions: 23 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x001001 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 | - |
| 0x1AE627 | AC Frequency Range High fault | 0 | - |
| 0x1AE628 | AC Frequency Low Fault | 0 | - |
| 0x2AE601 | External A/D Reference voltage high fault | 0 | - |
| 0x2AE602 | External A/D Reference Voltage low fault | 0 | - |
| 0x2AE611 | Coolant Overtemperature Shutdown | 0 | - |
| 0x2AE612 | FET Overtemperature fault | 0 | - |
| 0x2AE613 | Charger Internal Ambient overtemperature fault | 0 | - |
| 0x2AE614 | DCDC IC Enable diagnostic | 0 | - |
| 0x2AE615 | PFC IC Enabled | 0 | - |
| 0x2AE616 | Main precharge relay stuck closed | 0 | - |
| 0x2AE624 | AC Current high Fast fault | 0 | - |
| 0x2AE625 | AC Current High Fault Slow | 0 | - |
| 0x2AE626 | Precharge Timeout fault | 0 | - |
| 0x2AE631 | High Voltage DC Overvoltage fault | 0 | - |
| 0x2AE632 | High Voltage DC Overcharge fault | 0 | - |
| 0x2AE633 | High Voltage DC Overvoltage fault Hardware | 0 | - |
| 0x2AE641 | Non-volatile Memory Checksum fault | 0 | - |
| 0x2AE642 | Volatile Memory fault | 0 | - |
| 0x2AE643 | Over voltage detect circuit fault | 0 | - |
| 0x2AE644 | Over current detect circuit fualt | 0 | - |
| 0x2AE645 | ECC Fault | 0 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 51 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | MAJOR | HEX | High | - | - | - | - | - |
| 0x0002 | MINOR | HEX | High | - | - | - | - | - |
| 0x0003 | PATCH | HEX | High | - | - | - | - | - |
| 0x0004 | PROGRAM_FLOW_TASK_INDICATION | 0-n | High | 0xFF | - | - | - | - |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x2001 | ChargeReadiness | 0-n | Low | 0xFF | ST_CHGRDY_VALUE | - | - | - |
| 0x2002 | ChargeStatus | 0-n | Low | 0xFF | ST_CHGNHG_VALUES | - | - | - |
| 0x4000 | Boost Voltage | V | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4001 | Coolant Temperature | °C | High | unsigned int | - | 1.0 | 2.0 | -45.0 |
| 0x4002 | Umgebungstemperatur | °C | High | unsigned char | - | 1.0 | 2.0 | -45.0 |
| 0x4003 | Stromversorgungsgerät Temperatur | °C | High | unsigned char | - | 1.0 | 2.0 | -45.0 |
| 0x4004 | Externe A / D referance Spannung | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4005 | Pilot Frequency | Hz | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4006 | Pilot_Dutycycle | % | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4007 | LED1 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4008 | LED2 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4009 | LED3 Current Sense A/D | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400A | Proximity AD | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400B | Pilot AD | Counts | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x400C | Control board ID | Byte | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x400D | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x400E | Hardware Overvoltage | 0/1 | High | 0x01 | - | - | - | - |
| 0x400F | Hardware Overcurrent | 0/1 | High | 0x01 | - | - | - | - |
| 0x4010 | Wakeup Source | 0-n | High | 0xFF | WAKEUP_SOURCE_TABLE | - | - | - |
| 0x4011 | OBC_STATE | 0-n | High | 0xFF | OBC_STATE_TYPE | - | - | - |
| 0x4012 | AC Line Frequency | Hz | High | unsigned char | - | 1.0 | 4.0 | 0.0 |
| 0x4013 | DC Output Power | W | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4014 | AC Line Voltage | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4015 | HVDC Voltage | V | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4016 | HVDC Current | A | High | unsigned int | - | 1.0 | 10.0 | -204.0 |
| 0x4017 | AC Line Current | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x4018 | LV Battery Voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4019 | Address of the exception | HEX | High | unsigned long | - | - | - | - |
| 0x401A | Address of exception access | HEX | High | unsigned long | - | - | - | - |
| 0x401B | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x401C | PlugLock Current | A | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0x401D | FlapLock Current | A | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0x401E | SEC_DTC_FOR_21E602 | HEX | High | unsigned long | - | - | - | - |
| 0x401F | SEC_DTC_FOR_21E606 | HEX | High | unsigned long | - | - | - | - |
| 0x4020 | SEC_DTC_FOR_21E615 | HEX | High | unsigned long | - | - | - | - |
| 0x4021 | SEC_DTC_FOR_21E619 | HEX | High | unsigned long | - | - | - | - |
| 0xDF20 | STAT_BETRIEBSART | 0-n | High | 0xFF | TAB_BETRIEBSART | - | - | - |
| 0xDF26 | STAT_NETZFREQUENZ_WERT | - | High | unsigned char | - | 1.0 | 4.0 | 0.0 |
| 0xDF2E | STAT_HVDC_LEISTUNG_WERT | W | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0xDF31 | STAT_AC_SPANNUNG_EFFEKTIV_WERT | V | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xDF32 | STAT_HVDC_SPANNUNG_WERT | V | High | unsigned int | - | 1.0 | 50.0 | 0.0 |
| 0xDF35 | STAT_HVDC_STROM_MAX_WERT | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0xDF36 | STAT_AC_STROM_EFFEKTIV_LEITER_WERT | A | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0xDF38 | STAT_SPANNUNG_KL30_WERT | V | High | unsigned int | - | 1.0 | 100.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-laden-led-statusanzeige"></a>
### LADEN_LED_STATUSANZEIGE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Initialisierung (Blinken Orange) |
| 0x02 | Ladebereitschaft (Dauer Ein Blau) |
| 0x03 | Laden (Blinken Blau) |
| 0x04 | Ladeende (Dauer Ein Grün) |
| 0x05 | Fehler (Blinken in Gruppen Rot) |
| 0x06 | Suchbeleuchtung (Dauer Ein Weiß) |

<a id="table-obc-state-type"></a>
### OBC_STATE_TYPE

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | OBC_INIT |
| 2 | STANDBY |
| 3 | CHARGE |
| 4 | DERATE |
| 5 | INTERRUPT |
| 6 | ERROR |
| 7 | CRASH |
| 8 | POWEROFF |
| 9 | PRECHARGE |
| A | PRECHARGE_READY |

<a id="table-res-0xaf40-r"></a>
### RES_0XAF40_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_BETRIEBSART | - | + | + | 0-n | high | unsigned char | - | TAB_FUNKSTATUS | - | - | - | Funktionsstatus |
| STAT_ST_BETRIEBSART | - | + | + | 0-n | high | unsigned char | - | TAB_BETRIEBSART | - | - | - | Angeforderte Betriebsart |

<a id="table-res-0xaf41-r"></a>
### RES_0XAF41_R

Dimensions: 5 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPERATUR_BEREICH_1_WERT | + | - | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | relative Häufigkeit im Temperatur Bereich 1 (abhängig vom ausgewählten Temperatursensor) |
| STAT_TEMPERATUR_BEREICH_2_WERT | + | - | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | relative Häufigkeit im Temperatur Bereich 2 (abhängig vom ausgewählten Temperatursensor) |
| STAT_TEMPERATUR_BEREICH_3_WERT | + | - | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | relative Häufigkeit im Temperatur Bereich 3 (abhängig vom ausgewählten Temperatursensor) |
| STAT_TEMPERATUR_BEREICH_4_WERT | + | - | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | relative Häufigkeit im Temperatur Bereich 4 (abhängig vom ausgewählten Temperatursensor) |
| STAT_TEMPERATUR_BEREICH_5_WERT | + | - | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | relative Häufigkeit im Temperatur Bereich 5 (abhängig vom ausgewählten Temperatursensor) |

<a id="table-res-0xdef0-d"></a>
### RES_0XDEF0_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZV_LADESTECKER_EIN | 0/1 | high | unsigned char | - | - | - | - | - | Status Aktuator Ladestecker (0 = entriegelt, 1 = verriegelt). Steckertyp- und Marktabhängig. |
| STAT_LADESTECKER_EIN | 0-n | high | unsigned char | - | ZV_LADESTECKER | - | - | - | Status Sensor Ladestecker (0 = entriegelt, 1 = verriegelt). Steckertyp- und Marktabhängig. |

<a id="table-res-0xdef1-d"></a>
### RES_0XDEF1_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZV_LADEKLAPPE_EIN | 0-n | high | unsigned char | - | TAB_ZV_LADEKLAPPE | - | - | - | Zustand Verriegelung Ladeklappe |
| STAT_LADEKLAPPE | 0-n | high | unsigned char | - | TAB_LADEKLAPPE | - | - | - | Zustand der Ladeklappe |

<a id="table-res-0xdef3-d"></a>
### RES_0XDEF3_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_LADESTATUS_EIN | 0-n | high | unsigned char | - | LADEN_LED_STATUSANZEIGE | - | - | - | Zustand LED für Ladestatus (0 = nicht angesteuert, 1 = angesteuert) |

<a id="table-res-0xdef5-d"></a>
### RES_0XDEF5_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STECKER_NR | 0-n | high | unsigned char | - | TAB_LIM_STECKER | - | - | - | Zustand des Steckers |
| STAT_STROMTRAGFAEHIGKEIT_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Stromtragfähigkeit des angeschlossenen Kabels |

<a id="table-res-0xdef6-d"></a>
### RES_0XDEF6_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PILOT_AKTIV | 0/1 | high | unsigned char | - | - | - | - | - | Zustand des Pilotsignals (0 = nicht aktiv, 1 = aktiv) |
| STAT_PILOT_PWM_DUTYCYCLE_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Tastverhältnis PWM Pilotsignal |
| STAT_PILOT_CURRENT_WERT | A | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Errechneter Stromwert aus Pilotsignal |
| STAT_PILOT_LADEBEREIT | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zustand Ladebereitschaft Fahrzeug (0 = nicht ladebereit, 1 = ladebereit) |
| STAT_PILOT_FREQUENZ_WERT | Hz | high | unsigned int | - | - | 1.0 | 10.0 | 0.0 | Frequenz des Pilotsignals |
| STAT_PILOT_PEGEL_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Pegel des Pilotsignals |

<a id="table-res-0xdf29-d"></a>
### RES_0XDF29_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_I_MAX_WERT | A | high | unsigned int | - | - | 1.0 | 10.0 | -819.2 | Dynamische Stromgrenze bei Ladung |
| STAT_U_MAX_WERT | V | high | unsigned int | - | - | 1.0 | 10.0 | 1.0 | Spannungsgrenze bei Ladung |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 28 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSART | 0xAF40 | - | Ändern der Betriebsart Ladeelektronik | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAF40_R | RES_0xAF40_R |
| SLE_TEMPHISTOGRAMM_LESEN | 0xAF41 | - | Auslesen derTemperatur-Histogramme SLE | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAF41_R | RES_0xAF41_R |
| ZV_LADESTECKER | 0xDEF0 | - | Status und Steuern Ladestecker (Steckertyp- und Marktabhängig) 0 = entriegelt, 1 = verriegelt | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDEF0_D | RES_0xDEF0_D |
| ZV_LADEKLAPPE | 0xDEF1 | - | Status oder Steuern loading flap (0 = entriegelt, 1 = verriegelt) | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDEF1_D | RES_0xDEF1_D |
| LADEBEREITSCHAFT_LIM | 0xDEF2 | STAT_LADEBEREITSCHAFT_LIM | Ladebereitschaft (HW-Leitung), (1 = ja, 0 = nein) vom LIM an SLE gesendet | 0/1 | - | High | unsigned char | - | - | - | - | - | 22 | - | - |
| LED_LADESTATUS | 0xDEF3 | - | Zustand oder Ansteuern LED für Ladestatus (RGB-Leuchtring) | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDEF3_D | RES_0xDEF3_D |
| PROXIMITY | 0xDEF5 | - | Aktueller Zustand des Proximity | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEF5_D |
| PILOTSIGNAL | 0xDEF6 | - | aktuelle Daten des Pilotsignals über den Ladestrom | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEF6_D |
| BETRIEBSART_AKTUELL | 0xDF20 | STAT_BETRIEBSART | Status aktuelle Betriebsart Ladeelektronik | 0-n | - | High | unsigned char | TAB_BETRIEBSART | - | - | - | - | 22 | - | - |
| WIRKUNGSGRAD | 0xDF23 | STAT_WIRKUNGSGRAD_WERT | Status Wirkungsgrad | % | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| WIRKUNGSGRAD_LADEZYKLUS | 0xDF24 | STAT_WIRKUNGSGRAD_LADEZYKLUS_WERT | Status Wirkungsgrad Ladezyklus | % | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| AC_PHASENANZAHL | 0xDF25 | STAT_AC_PHASENANZAHL_WERT | Status AC-Phasenanzahl | - | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| NETZFREQUENZ | 0xDF26 | STAT_NETZFREQUENZ_WERT | Status Netzfrequenz pro Leiter | - | - | High | unsigned char | - | 1.0 | 4.0 | 0.0 | - | 22 | - | - |
| LADEDAUER | 0xDF27 | STAT_LADEDAUER_WERT | Status Ladedauer | s | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| TEMPERATUR_LADEELEKTRONIK | 0xDF28 | STAT_TEMPERATUR_WERT | aktuelle Temperatur Ladeelektronik | °C | - | High | unsigned char | - | 1.0 | 1.0 | -48.0 | - | 22 | - | - |
| SME_BEGRENZUNGSGROESSEN | 0xDF29 | - | Begrenzungsgrößen der Ladeleistung durch SME | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF29_D |
| HVDC_LEISTUNG | 0xDF2E | STAT_HVDC_LEISTUNG_WERT | Status HV-DC Leistung Ladeelektronik | W | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| HVDC_LEISTUNG_MAX | 0xDF2F | STAT_HVDC_LEISTUNG_MAX_WERT | Status maximale HV-DC Leistung Ladeelektronik | W | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| AC_WIRKLEISTUNG_LADEZYKLUS | 0xDF30 | STAT_AC_WIRKLEISTUNG_LADEZYKLUS_WERT | Status aus dem Netz entnommene Wirkleistung aktueller Ladezyklus | W | - | High | unsigned int | - | 5.0 | 1.0 | 0.0 | - | 22 | - | - |
| AC_SPANNUNG_EFFEKTIV | 0xDF31 | STAT_AC_SPANNUNG_EFFEKTIV_WERT | Status Effektivwerte der AC-Leiterspannungen pro Leiter | V | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| HVDC_SPANNUNG | 0xDF32 | STAT_HVDC_SPANNUNG_WERT | HV-DC Spannung an der Ladeelektronik | V | - | High | unsigned int | - | 1.0 | 50.0 | 0.0 | - | 22 | - | - |
| HVDC_SPANNUNG_MAX | 0xDF33 | STAT_HVDC_SPANNUNG_MAX_WERT | maximale HV-DC Spannung an der Ladeelektronik | V | - | High | unsigned int | - | 1.0 | 4.0 | 0.0 | - | 22 | - | - |
| HVDC_STROM | 0xDF34 | STAT_HVDC_STROM_WERT | Status HV-DC Strom Ladeelektronik | A | - | High | unsigned int | - | 1.0 | 10.0 | -204.7 | - | 22 | - | - |
| HVDC_STROM_MAX | 0xDF35 | STAT_HVDC_STROM_MAX_WERT | Status maximaler HV-DC Strom Ladeelektronik | A | - | High | unsigned int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AC_STROM_EFFEKTIV_LEITER | 0xDF36 | STAT_AC_STROM_EFFEKTIV_LEITER_WERT | Status Effektivwerte der AC-Leiterströme pro Leiter | A | - | High | unsigned int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| AC_STROM_MAX | 0xDF37 | STAT_AC_STROM_MAX_WERT | Status maximaler AC-Strom Ladeelektronik | A | - | High | unsigned int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| KL30_SPANNUNG | 0xDF38 | STAT_SPANNUNG_KL30_WERT | Aktuelle Spannung an KL30 der Ladeelektronik | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| LADEBETRIEBSDAUER | 0xDF3C | STAT_LADEBETRIEBSDAUER_WERT | Charger gesamte Ladebetriebsdauer in Minuten | min | - | High | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |

<a id="table-st-chgnhg-values"></a>
### ST_CHGNHG_VALUES

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | No Charging |
| 1 | Initialization |
| 2 | Charging |
| 3 | Charge Pause |
| 4 | Charge Completed |
| 5 | Error |

<a id="table-st-chgrdy-value"></a>
### ST_CHGRDY_VALUE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Inactive |
| 1 | Active |
| 3 | Invalid |

<a id="table-tab-betriebsart"></a>
### TAB_BETRIEBSART

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Standby |
| 0x02 | HV-DC Laden |
| 0x03 | Derating |
| 0x04 | Ladeunterbrechung |
| 0x05 | Error |
| 0x06 | Crash |
| 0x07 | Betriebsartwechsel |
| 0x08 | Ladeinitialisierung |
| 0x09 | Ladeinitalisierung abgeschlossen |
| 0x0F | Signal ungültig |

<a id="table-tab-betriebsart-ladegeraet-kommandieren"></a>
### TAB_BETRIEBSART_LADEGERAET_KOMMANDIEREN

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Standby |

<a id="table-tab-funkstatus"></a>
### TAB_FUNKSTATUS

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Funktion noch nicht gestartet |
| 0x01 | Start-/Ansteuerbedingung nicht erfuellt |
| 0x02 | Uebergabeparameter nicht plausibel |
| 0x03 | Funktion wartet auf Freigabe |
| 0x04 | nicht verfuegbarer Wert |
| 0x05 | Funktion laeuft |
| 0x06 | Funktion beendet (ohne Ergebnis) |
| 0x07 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 0x08 | Funktion vollständig durchlaufen (Zyklusflag/Readiness gesetzt) und kein Fehler erkannt |
| 0x09 | Funktion vollständig durchlaufen (Zyklusflag/Readiness gesetzt) und Fehler erkannt |
| 0xFE | nicht definiert |
| 0xFF | ungueltiger Wert |

<a id="table-tab-ladeklappe"></a>
### TAB_LADEKLAPPE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Offen |
| 0x01 | Geschlossen |
| 0x02 | Fehler - nicht verbaut |

<a id="table-tab-lim-stecker"></a>
### TAB_LIM_STECKER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Ladestecker angesteckt |
| 0x01 | Ladestecker angesteckt |
| 0x02 | Ladestecker angesteckt und Entriegelungstaste betätigt |
| 0x03 | ungültiger Zustand |

<a id="table-tab-sle-temperatursensor"></a>
### TAB_SLE_TEMPERATURSENSOR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Board (Ambient) |
| 0x01 | Power Board (FET) |
| 0x02 | Kühlmittel (Coolant) |

<a id="table-tab-zv-ladeklappe"></a>
### TAB_ZV_LADEKLAPPE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | entriegelt |
| 1 | verriegelt |
| 3 | Fehler - nicht verbaut |

<a id="table-tab-0x400d"></a>
### TAB_0X400D

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0001 | 0x0002 | 0x0003 |

<a id="table-tab-0x401b"></a>
### TAB_0X401B

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x0004 |

<a id="table-wakeup-source-table"></a>
### WAKEUP_SOURCE_TABLE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x1 | CAN  (Not valid for C hardware) |
| 0x2 | AC Present  &gt;=25VAC  (Not valid for C hardware) |
| 0x4 | KL15 Wakeup |
| 0x8 | Hall Sensor wakeup  (Not valid for B1/B2A) |
| 0x10 | RESERVED  (Not valid) |
| 0x20 | Pilot |
| 0x40 | Battery |

<a id="table-zv-ladestecker"></a>
### ZV_LADESTECKER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht verriegelt |
| 1 | Verriegelt |
| 2 | Fehler |
| 3 | Signal ungültig |
