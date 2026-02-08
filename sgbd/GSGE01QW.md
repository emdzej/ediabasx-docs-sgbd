# GSGE01QW.prg

- Jobs: [40](#jobs)
- Tables: [603](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | 7-Gang-Doppelkupplungsgetriebe mit E-Schaltung |
| ORIGIN | BMW EA-511 Plett |
| REVISION | 3.003 |
| AUTHOR | GETRAG-B.V.-&-CO.-KG EA-521 Frenkel |
| COMMENT | - |
| PACKAGE | 1.992 |
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
- [FS_LESEN_PERMANENT](#job-fs-lesen-permanent) - permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default
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
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_INTERNE_DATEN_LESEN](#job-cbs-interne-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS  : $22   ReadDataByIdentifier UDS  : $1003 Data Identifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 6) Fahrzeug muss in einem der folgenden Zustaende sein:) - Pruefen_Analyse_Diagnose - Fahrbereitschaft_herstellen - Wohnen, ab CBS 6.2 - Fahren - Fahrbereitschaft_beenden UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)
- [CBS_RESET_DETAIL_LESEN](#job-cbs-reset-detail-lesen) - Lesen der CBx-Daten aus einem CBx-Steuergerät UDS: $22 ReadDataByIdentifier Modus  : Default
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events $02 eventWindowTime - infinite (LH Diagnosemaster V11 oder höher, Umsetzung nach LH V6 - V10 wird jedoch toleriert)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CALID_CVN_LESEN](#job-calid-cvn-lesen) - OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [_FS_LOESCHEN_FUNKTIONAL](#job-fs-loeschen-funktional) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [STATUS_IDR_EGS_EXTENDED](#job-status-idr-egs-extended) - Lesen der IDR Daten für EGS UDS  : $22 ReadDataByIdentifier Modus: Default

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

<a id="job-fs-lesen-permanent"></a>
### FS_LESEN_PERMANENT

permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
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

<a id="job-cbs-info"></a>
### CBS_INFO

Ausgabe der CBS-Version

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ECU_NAME | string | Steuergeraetename |
| CBS_VERSION_TEXT | string | CBS Version im Klartext |
| CBS_VERSION_HEX | string | CBS Version als Wert |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_K | string | Filter über CBS_K Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ERROR_TEXT | string | ausführliche Fehlerbeschreibung |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Einheit zur Restlaufleistung |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | Einheit der Verfügbarkeit |
| AVAI_CBS_WERT_OEL | int | Verfuegbarkeit OEL in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_OEL | int | Servicezaehler Motoroel, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BR_V | int | Servicezaehler Bremsbelag vorne, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BR_H | int | Servicezaehler Bremsbelag hinten, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BRFL | int | Servicezaehler Bremsfluessigkeit, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_SIC | int | Servicezaehler Sichtpruefung, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC_V | int | Verfuegbarkeit SIC_V in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_SIC_V | int | Servicezaehler Sichtpruefung/Fahrzeug-Check verknuepft, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_UEB | int | Servicezaehler Uebergabedurchsicht, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_NOX | int | Verfuegbarkeit NOX in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_NOX | int | Servicezaehler NOx-Additiv  , fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_EFK | int | Verfuegbarkeit Efk in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_EFK | int | Servicezaehler Einfahrkontrolle, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat als Klartext |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| FRC_INTM_T_CBS_EINH | string | Prognose Zeitintervall im Klartext |
| STATUS_MESSUNG_TEXT | string | Statusbyte im Klartext |
| CHOV_CBS_CBR_VIEW | string | CBx Sichtbarkeit |
| CHOV_CBS_CBR | string | Entscheidungslogik CBS/CBR |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cbs-interne-daten-lesen"></a>
### CBS_INTERNE_DATEN_LESEN

CBS Daten auslesen (fuer CBS-Version 5) UDS  : $22   ReadDataByIdentifier UDS  : $1003 Data Identifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| CBS_ANZAHL | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_CBS_MESS_HEX | string | CBS Umfang [ hex ] |
| ID_CBS_MESS_TEXT | string | CBS Umfang [ Text ] |
| ID_CBS_MESS_K_TEXT | string | CBS Kennung [ Text ] |
| STAT_BAC_VERFGBARK_RESTWEG_WERT | real | Verfuegbarkeit fuer Restwegberechnung [ % ] |
| STAT_BAC_VERFGBARK_RESTWEG_EINH | string | Einheit Verfuegbarkeit fuer Restwegberechnung [ % ] |
| STAT_BAC_RESTWEGSTRECKE_WERT | long | Restwegstrecke [ km ] |
| STAT_BAC_RESTWEGSTRECKE_EINH | string | Einheit Restwegstrecke [ km ] |
| STAT_BAC_WEGPROGNOSE_WERT | unsigned long | Wegprognose [ km ] |
| STAT_BAC_WEGPROGNOSE_EINH | string | Einheit Wegprognose [ km ] |
| STAT_BAC_KM_FZG_WERT | unsigned long | Kilometerstand des Fahrzeugs [ km ] |
| STAT_BAC_KM_FZG_EINH | string | Einheit Kilometerstand des Fahrzeugs [ km ] |
| STAT_BAC_KM_FZG_LETZTER_STD_RESET_WERT | unsigned long | Kilometerstand Fahrzeug beim letzten Standard CBS-Reset [ km ] |
| STAT_BAC_KM_FZG_LETZTER_STD_RESET_EINH | string | Einheit Kilometerstand Fahrzeug beim letzten Standard CBS-Reset [ km ] |
| STAT_BAC_KM_FZG_BERECHNETER_RESET_WERT | long | Kilometerstand Fahrzeug zum errechneten CBS-Reset [ km ] |
| STAT_BAC_KM_FZG_BERECHNETER_RESET_EINH | string | Einheit Kilometerstand Fahrzeug zum errechneten CBS-Reset [ km ] |
| STAT_BAC_WEGPROGNOSE_INTERVALL_WERT | unsigned long | Wegprognose des letzten Serviceintervalls = Sa_intervall [ km ] |
| STAT_BAC_WEGPROGNOSE_INTERVALL_EINH | string | Einheit Wegprognose des letzten Serviceintervalls = Sa_intervall [ km ] |
| STAT_BAC_CODIERUNG_RESTWEGSTRECKE_WERT | unsigned long | Kodierte Restwegstrecke bei 100% Verfügbarkeit [ km ] |
| STAT_BAC_CODIERUNG_RESTWEGSTRECKE_EINH | string | Einheit Kodierte Restwegstrecke bei 100% Verfügbarkeit [ km ] |
| STAT_BAC_CODIERUNG_MIN_WERT | unsigned long | Kodierter Minimalwert Wegintervall [ km ] |
| STAT_BAC_CODIERUNG_MIN_EINH | string | Einheit Kodierter Minimalwert Wegintervall [ km ] |
| STAT_BAC_CODIERUNG_MAX_WERT | unsigned long | Kodierter Maximalwert Wegintervall [ km ] |
| STAT_BAC_CODIERUNG_MAX_EINH | string | Einheit Kodierter Maximalwert Wegintervall [ km ] |
| STAT_BAC_CODIERUNG_MIN_PROZ_WERT | int | Kodierter Minimalwert Wegintervall [ % ] |
| STAT_BAC_CODIERUNG_MIN_PROZ_EINH | string | Einheit Kodierter Minimalwert Wegintervall [ % ] |
| STAT_BAC_CODIERUNG_MAX_PROZ_WERT | int | Kodierter Maximalwert Wegintervall [ % ] |
| STAT_BAC_CODIERUNG_MAX_PROZ_EINH | string | Kodierter Maximalwert Wegintervall [ % ] |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 6) Fahrzeug muss in einem der folgenden Zustaende sein:) - Pruefen_Analyse_Diagnose - Fahrbereitschaft_herstellen - Wohnen, ab CBS 6.2 - Fahren - Fahrbereitschaft_beenden UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, Sic, Sic_v, TUV, AU, Ueb, Efk Werte externe Umfaenge: Oel, NOx_a, Br_v, Br_h Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 0xFFh (255 dez) Defaultwert: 100 (0x64h) Bremsflüssigkeit: 150 (0x96h) erlaubt |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 0x0F Defaultwert: 0x0F |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2062: 0-62 Schalter, keine Aenderung: 0x3F (63 dez) Defaultwert: 0x3F (63 dez) |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 0x8000 Defaultwert: 0x8000 |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0x00 -&gt; % 0x01 -&gt; km*10 0x0F -&gt; d.c. Defaultwert: 0x0F |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0x00 Schalter, keine Aenderung: 0xFF Defaultwert: 0xFF |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 1-254 Monate 0 zurücksetzen Schalter, keine Aenderung: 0xFF Defaultwert: 0xFF |
| CHOV_CBS_CBR_VIEW | int | Sichtbarkeit CBx Umfang) Defaultwert 0, Service anzeigen: 0x00 |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) Defaultwert: 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ERROR_TEXT | string | ausführliche Fehlerbeschreibung |
| ERROR_WERT | string | Wert der zum Fehler geführt hat |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cbs-reset-detail-lesen"></a>
### CBS_RESET_DETAIL_LESEN

Lesen der CBx-Daten aus einem CBx-Steuergerät UDS: $22 ReadDataByIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| CBS_RUECK_GRUND | string | Rücksetz Verhinderungsgrund |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) |
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

<a id="job-fs-loeschen-funktional"></a>
### _FS_LOESCHEN_FUNKTIONAL

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

<a id="job-status-idr-egs-extended"></a>
### STATUS_IDR_EGS_EXTENDED

Lesen der IDR Daten für EGS UDS  : $22 ReadDataByIdentifier Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_OQM_DV0_GEAR_1_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_1_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_2_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_2_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_3_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_3_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_3_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_4_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_4_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_4_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_5_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_5_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_5_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_6_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_6_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_6_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_7_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_7_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_7_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_R_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV0_GEAR_R_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV0_GEAR_R_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_1_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_1_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_2_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_2_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_3_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_3_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_3_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_4_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_4_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_4_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_5_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_5_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_5_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_6_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_6_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_6_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_7_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_7_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_7_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_R_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_DV3_GEAR_R_EINH | string | OQM-Einheit zur Drehzahl |
| STAT_OQM_DV3_GEAR_R_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_1_WERT | unsigned int | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_1_EINH | string | OQM-Counter |
| STAT_OQM_JDDR_CNT_CLASS_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_2_WERT | unsigned int | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_2_EINH | string | OQM-Counter |
| STAT_OQM_JDDR_CNT_CLASS_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_3_WERT | unsigned int | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_3_EINH | string | OQM-Counter |
| STAT_OQM_JDDR_CNT_CLASS_3_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_4_WERT | unsigned int | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_CNT_CLASS_4_EINH | string | OQM-Counter |
| STAT_OQM_JDDR_CNT_CLASS_4_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_1_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_1_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_2_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_2_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_3_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_3_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_3_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_4_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_4_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_JDDR_OCCR_MLG_CLASS_4_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OF_OIL_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OF_OIL_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_OF_OIL_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OIL_AGED_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OIL_AGED_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_OIL_AGED_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_1_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_1_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_2_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_2_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_3_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_3_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_3_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_4_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_4_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_4_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_5_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_5_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_5_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_6_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_6_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_6_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_7_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_7_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_7_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_8_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_8_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_8_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_9_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_9_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_9_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_10_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_10_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_10_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_11_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_11_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_11_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_12_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GEAR_PWR_TIME_CLASS_12_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_GEAR_PWR_TIME_CLASS_12_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_STEPS_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_STEPS_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_CAP_TEMP_STEPS_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_SUM_1_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_SUM_1_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_CAP_TEMP_SUM_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_SUM_2_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_SUM_2_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_CAP_TEMP_SUM_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_WERT | real | OQM-Kennung als Zahl |
| STAT_OQM_MLG_CAP_TEMP_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_CAP_TEMP_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MIN_AVG_CALC_MLG_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MIN_AVG_CALC_MLG_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MIN_AVG_CALC_MLG_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OILMODEL_AGED_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_MLG_OILMODEL_AGED_EINH | string | OQM-Einheit zu Kilometer |
| STAT_OQM_MLG_OILMODEL_AGED_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_TIM_ABSOLUTE_FILL_DATE_WERT | long | OQM-Kennung als Zahl |
| STAT_OQM_TIM_ABSOLUTE_FILL_DATE_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_TIM_ABSOLUTE_FILL_DATE_RAW | long | OQM-Kennung als Zahl |
| STAT_OQM_TIM_ABSOLUTE_OLD_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_TIM_ABSOLUTE_OLD_EINH | string | OQM-Einheit zu Zeit |
| STAT_OQM_TIM_ABSOLUTE_OLD_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_CLU_ENERGY_1_WERT | real | OQM-Kennung als Zahl |
| STAT_CLU_ENERGY_1_EINH | string | OQM-Einheit zu Energie |
| STAT_CLU_ENERGY_1_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_CLU_ENERGY_2_WERT | real | OQM-Kennung als Zahl |
| STAT_CLU_ENERGY_2_EINH | string | OQM-Einheit zu Energie |
| STAT_CLU_ENERGY_2_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_CLU_MLG_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_CLU_MLG_EINH | string | OQM-Einheit zu Kilometer |
| STAT_CLU_MLG_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_CLU_ENERGY_WERT | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_CLU_ENERGY_EINH | string | OQM-Einheit zu Energie |
| STAT_OQM_CLU_ENERGY_RAW | unsigned long | OQM-Kennung als Zahl |
| STAT_OQM_GBX_SERVICE_WERT | unsigned char | OQM-Kennung als Zahl |
| STAT_OQM_GBX_SERVICE_STATE | string | OQM-Kennung als Zahl |
| STAT_OQM_VERSION_WERT | unsigned char | OQM-Kennung als Zahl |

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
- [CBSNRTEXT](#table-cbsnrtext) (27 × 3)
- [CBSKENNUNG](#table-cbskennung) (30 × 3)
- [TAB_ECU_NAME](#table-tab-ecu-name) (6 × 2)
- [TAB_CBS_EINHEITEN](#table-tab-cbs-einheiten) (5 × 2)
- [TAB_CBS_STATUS](#table-tab-cbs-status) (17 × 2)
- [TAB_CBS_MONAT](#table-tab-cbs-monat) (16 × 2)
- [TAB_RUECK_GRUND](#table-tab-rueck-grund) (11 × 2)
- [ARG_0X400A_D](#table-arg-0x400a-d) (1 × 12)
- [ARG_0X4142_D](#table-arg-0x4142-d) (1 × 12)
- [ARG_0X4143_D](#table-arg-0x4143-d) (1 × 12)
- [ARG_0X4148_D](#table-arg-0x4148-d) (1 × 12)
- [ARG_0X4310_D](#table-arg-0x4310-d) (1 × 12)
- [ARG_0X4312_D](#table-arg-0x4312-d) (1 × 12)
- [ARG_0X4313_D](#table-arg-0x4313-d) (1 × 12)
- [ARG_0X4314_D](#table-arg-0x4314-d) (1 × 12)
- [ARG_0XC001_D](#table-arg-0xc001-d) (2 × 12)
- [ARG_0XD9CA_D](#table-arg-0xd9ca-d) (1 × 12)
- [ARG_0XDA15_D](#table-arg-0xda15-d) (1 × 12)
- [ARG_0XDA66_D](#table-arg-0xda66-d) (1 × 12)
- [ARG_0XDA68_D](#table-arg-0xda68-d) (1 × 12)
- [ARG_0XF100_R](#table-arg-0xf100-r) (3 × 14)
- [ARG_0XF402_R](#table-arg-0xf402-r) (4 × 14)
- [ARG_0XF410_R](#table-arg-0xf410-r) (1 × 14)
- [ARG_0XF411_R](#table-arg-0xf411-r) (7 × 14)
- [ARG_0XF413_R](#table-arg-0xf413-r) (7 × 14)
- [ARG_0XF415_R](#table-arg-0xf415-r) (2 × 14)
- [ARG_0XF416_R](#table-arg-0xf416-r) (7 × 14)
- [BACK_LIGHT_STATE_TABLE](#table-back-light-state-table) (3 × 2)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_0](#table-bf-drag-ind-bit-mapping-fsp-id-0) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_1](#table-bf-drag-ind-bit-mapping-fsp-id-1) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_10](#table-bf-drag-ind-bit-mapping-fsp-id-10) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_100](#table-bf-drag-ind-bit-mapping-fsp-id-100) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_101](#table-bf-drag-ind-bit-mapping-fsp-id-101) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_102](#table-bf-drag-ind-bit-mapping-fsp-id-102) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_103](#table-bf-drag-ind-bit-mapping-fsp-id-103) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_104](#table-bf-drag-ind-bit-mapping-fsp-id-104) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_105](#table-bf-drag-ind-bit-mapping-fsp-id-105) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_106](#table-bf-drag-ind-bit-mapping-fsp-id-106) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_107](#table-bf-drag-ind-bit-mapping-fsp-id-107) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_108](#table-bf-drag-ind-bit-mapping-fsp-id-108) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_109](#table-bf-drag-ind-bit-mapping-fsp-id-109) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_11](#table-bf-drag-ind-bit-mapping-fsp-id-11) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_110](#table-bf-drag-ind-bit-mapping-fsp-id-110) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_111](#table-bf-drag-ind-bit-mapping-fsp-id-111) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_112](#table-bf-drag-ind-bit-mapping-fsp-id-112) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_113](#table-bf-drag-ind-bit-mapping-fsp-id-113) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_114](#table-bf-drag-ind-bit-mapping-fsp-id-114) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_115](#table-bf-drag-ind-bit-mapping-fsp-id-115) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_116](#table-bf-drag-ind-bit-mapping-fsp-id-116) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_117](#table-bf-drag-ind-bit-mapping-fsp-id-117) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_118](#table-bf-drag-ind-bit-mapping-fsp-id-118) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_119](#table-bf-drag-ind-bit-mapping-fsp-id-119) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_12](#table-bf-drag-ind-bit-mapping-fsp-id-12) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_120](#table-bf-drag-ind-bit-mapping-fsp-id-120) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_121](#table-bf-drag-ind-bit-mapping-fsp-id-121) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_122](#table-bf-drag-ind-bit-mapping-fsp-id-122) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_123](#table-bf-drag-ind-bit-mapping-fsp-id-123) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_124](#table-bf-drag-ind-bit-mapping-fsp-id-124) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_125](#table-bf-drag-ind-bit-mapping-fsp-id-125) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_126](#table-bf-drag-ind-bit-mapping-fsp-id-126) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_127](#table-bf-drag-ind-bit-mapping-fsp-id-127) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_128](#table-bf-drag-ind-bit-mapping-fsp-id-128) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_129](#table-bf-drag-ind-bit-mapping-fsp-id-129) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_13](#table-bf-drag-ind-bit-mapping-fsp-id-13) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_130](#table-bf-drag-ind-bit-mapping-fsp-id-130) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_131](#table-bf-drag-ind-bit-mapping-fsp-id-131) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_132](#table-bf-drag-ind-bit-mapping-fsp-id-132) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_133](#table-bf-drag-ind-bit-mapping-fsp-id-133) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_134](#table-bf-drag-ind-bit-mapping-fsp-id-134) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_135](#table-bf-drag-ind-bit-mapping-fsp-id-135) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_136](#table-bf-drag-ind-bit-mapping-fsp-id-136) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_137](#table-bf-drag-ind-bit-mapping-fsp-id-137) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_138](#table-bf-drag-ind-bit-mapping-fsp-id-138) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_139](#table-bf-drag-ind-bit-mapping-fsp-id-139) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_14](#table-bf-drag-ind-bit-mapping-fsp-id-14) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_140](#table-bf-drag-ind-bit-mapping-fsp-id-140) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_141](#table-bf-drag-ind-bit-mapping-fsp-id-141) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_142](#table-bf-drag-ind-bit-mapping-fsp-id-142) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_143](#table-bf-drag-ind-bit-mapping-fsp-id-143) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_144](#table-bf-drag-ind-bit-mapping-fsp-id-144) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_145](#table-bf-drag-ind-bit-mapping-fsp-id-145) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_146](#table-bf-drag-ind-bit-mapping-fsp-id-146) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_147](#table-bf-drag-ind-bit-mapping-fsp-id-147) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_148](#table-bf-drag-ind-bit-mapping-fsp-id-148) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_149](#table-bf-drag-ind-bit-mapping-fsp-id-149) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_15](#table-bf-drag-ind-bit-mapping-fsp-id-15) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_150](#table-bf-drag-ind-bit-mapping-fsp-id-150) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_151](#table-bf-drag-ind-bit-mapping-fsp-id-151) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_152](#table-bf-drag-ind-bit-mapping-fsp-id-152) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_153](#table-bf-drag-ind-bit-mapping-fsp-id-153) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_154](#table-bf-drag-ind-bit-mapping-fsp-id-154) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_155](#table-bf-drag-ind-bit-mapping-fsp-id-155) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_156](#table-bf-drag-ind-bit-mapping-fsp-id-156) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_157](#table-bf-drag-ind-bit-mapping-fsp-id-157) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_158](#table-bf-drag-ind-bit-mapping-fsp-id-158) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_159](#table-bf-drag-ind-bit-mapping-fsp-id-159) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_16](#table-bf-drag-ind-bit-mapping-fsp-id-16) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_160](#table-bf-drag-ind-bit-mapping-fsp-id-160) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_161](#table-bf-drag-ind-bit-mapping-fsp-id-161) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_162](#table-bf-drag-ind-bit-mapping-fsp-id-162) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_163](#table-bf-drag-ind-bit-mapping-fsp-id-163) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_164](#table-bf-drag-ind-bit-mapping-fsp-id-164) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_165](#table-bf-drag-ind-bit-mapping-fsp-id-165) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_166](#table-bf-drag-ind-bit-mapping-fsp-id-166) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_167](#table-bf-drag-ind-bit-mapping-fsp-id-167) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_168](#table-bf-drag-ind-bit-mapping-fsp-id-168) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_169](#table-bf-drag-ind-bit-mapping-fsp-id-169) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_17](#table-bf-drag-ind-bit-mapping-fsp-id-17) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_170](#table-bf-drag-ind-bit-mapping-fsp-id-170) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_171](#table-bf-drag-ind-bit-mapping-fsp-id-171) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_172](#table-bf-drag-ind-bit-mapping-fsp-id-172) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_173](#table-bf-drag-ind-bit-mapping-fsp-id-173) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_174](#table-bf-drag-ind-bit-mapping-fsp-id-174) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_175](#table-bf-drag-ind-bit-mapping-fsp-id-175) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_176](#table-bf-drag-ind-bit-mapping-fsp-id-176) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_177](#table-bf-drag-ind-bit-mapping-fsp-id-177) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_178](#table-bf-drag-ind-bit-mapping-fsp-id-178) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_179](#table-bf-drag-ind-bit-mapping-fsp-id-179) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_18](#table-bf-drag-ind-bit-mapping-fsp-id-18) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_180](#table-bf-drag-ind-bit-mapping-fsp-id-180) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_181](#table-bf-drag-ind-bit-mapping-fsp-id-181) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_182](#table-bf-drag-ind-bit-mapping-fsp-id-182) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_183](#table-bf-drag-ind-bit-mapping-fsp-id-183) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_184](#table-bf-drag-ind-bit-mapping-fsp-id-184) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_185](#table-bf-drag-ind-bit-mapping-fsp-id-185) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_186](#table-bf-drag-ind-bit-mapping-fsp-id-186) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_187](#table-bf-drag-ind-bit-mapping-fsp-id-187) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_188](#table-bf-drag-ind-bit-mapping-fsp-id-188) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_189](#table-bf-drag-ind-bit-mapping-fsp-id-189) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_19](#table-bf-drag-ind-bit-mapping-fsp-id-19) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_190](#table-bf-drag-ind-bit-mapping-fsp-id-190) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_191](#table-bf-drag-ind-bit-mapping-fsp-id-191) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_192](#table-bf-drag-ind-bit-mapping-fsp-id-192) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_193](#table-bf-drag-ind-bit-mapping-fsp-id-193) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_194](#table-bf-drag-ind-bit-mapping-fsp-id-194) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_195](#table-bf-drag-ind-bit-mapping-fsp-id-195) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_196](#table-bf-drag-ind-bit-mapping-fsp-id-196) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_197](#table-bf-drag-ind-bit-mapping-fsp-id-197) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_198](#table-bf-drag-ind-bit-mapping-fsp-id-198) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_199](#table-bf-drag-ind-bit-mapping-fsp-id-199) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_2](#table-bf-drag-ind-bit-mapping-fsp-id-2) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_20](#table-bf-drag-ind-bit-mapping-fsp-id-20) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_200](#table-bf-drag-ind-bit-mapping-fsp-id-200) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_201](#table-bf-drag-ind-bit-mapping-fsp-id-201) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_202](#table-bf-drag-ind-bit-mapping-fsp-id-202) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_203](#table-bf-drag-ind-bit-mapping-fsp-id-203) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_204](#table-bf-drag-ind-bit-mapping-fsp-id-204) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_205](#table-bf-drag-ind-bit-mapping-fsp-id-205) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_206](#table-bf-drag-ind-bit-mapping-fsp-id-206) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_207](#table-bf-drag-ind-bit-mapping-fsp-id-207) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_208](#table-bf-drag-ind-bit-mapping-fsp-id-208) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_209](#table-bf-drag-ind-bit-mapping-fsp-id-209) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_21](#table-bf-drag-ind-bit-mapping-fsp-id-21) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_210](#table-bf-drag-ind-bit-mapping-fsp-id-210) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_211](#table-bf-drag-ind-bit-mapping-fsp-id-211) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_212](#table-bf-drag-ind-bit-mapping-fsp-id-212) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_213](#table-bf-drag-ind-bit-mapping-fsp-id-213) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_214](#table-bf-drag-ind-bit-mapping-fsp-id-214) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_215](#table-bf-drag-ind-bit-mapping-fsp-id-215) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_216](#table-bf-drag-ind-bit-mapping-fsp-id-216) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_217](#table-bf-drag-ind-bit-mapping-fsp-id-217) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_218](#table-bf-drag-ind-bit-mapping-fsp-id-218) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_219](#table-bf-drag-ind-bit-mapping-fsp-id-219) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_22](#table-bf-drag-ind-bit-mapping-fsp-id-22) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_220](#table-bf-drag-ind-bit-mapping-fsp-id-220) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_221](#table-bf-drag-ind-bit-mapping-fsp-id-221) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_222](#table-bf-drag-ind-bit-mapping-fsp-id-222) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_223](#table-bf-drag-ind-bit-mapping-fsp-id-223) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_224](#table-bf-drag-ind-bit-mapping-fsp-id-224) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_225](#table-bf-drag-ind-bit-mapping-fsp-id-225) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_226](#table-bf-drag-ind-bit-mapping-fsp-id-226) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_227](#table-bf-drag-ind-bit-mapping-fsp-id-227) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_228](#table-bf-drag-ind-bit-mapping-fsp-id-228) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_229](#table-bf-drag-ind-bit-mapping-fsp-id-229) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_23](#table-bf-drag-ind-bit-mapping-fsp-id-23) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_230](#table-bf-drag-ind-bit-mapping-fsp-id-230) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_231](#table-bf-drag-ind-bit-mapping-fsp-id-231) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_232](#table-bf-drag-ind-bit-mapping-fsp-id-232) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_233](#table-bf-drag-ind-bit-mapping-fsp-id-233) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_234](#table-bf-drag-ind-bit-mapping-fsp-id-234) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_235](#table-bf-drag-ind-bit-mapping-fsp-id-235) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_236](#table-bf-drag-ind-bit-mapping-fsp-id-236) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_237](#table-bf-drag-ind-bit-mapping-fsp-id-237) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_238](#table-bf-drag-ind-bit-mapping-fsp-id-238) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_239](#table-bf-drag-ind-bit-mapping-fsp-id-239) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_24](#table-bf-drag-ind-bit-mapping-fsp-id-24) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_240](#table-bf-drag-ind-bit-mapping-fsp-id-240) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_241](#table-bf-drag-ind-bit-mapping-fsp-id-241) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_242](#table-bf-drag-ind-bit-mapping-fsp-id-242) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_243](#table-bf-drag-ind-bit-mapping-fsp-id-243) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_244](#table-bf-drag-ind-bit-mapping-fsp-id-244) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_245](#table-bf-drag-ind-bit-mapping-fsp-id-245) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_246](#table-bf-drag-ind-bit-mapping-fsp-id-246) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_247](#table-bf-drag-ind-bit-mapping-fsp-id-247) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_248](#table-bf-drag-ind-bit-mapping-fsp-id-248) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_249](#table-bf-drag-ind-bit-mapping-fsp-id-249) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_25](#table-bf-drag-ind-bit-mapping-fsp-id-25) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_250](#table-bf-drag-ind-bit-mapping-fsp-id-250) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_251](#table-bf-drag-ind-bit-mapping-fsp-id-251) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_252](#table-bf-drag-ind-bit-mapping-fsp-id-252) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_253](#table-bf-drag-ind-bit-mapping-fsp-id-253) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_254](#table-bf-drag-ind-bit-mapping-fsp-id-254) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_255](#table-bf-drag-ind-bit-mapping-fsp-id-255) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_256](#table-bf-drag-ind-bit-mapping-fsp-id-256) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_257](#table-bf-drag-ind-bit-mapping-fsp-id-257) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_258](#table-bf-drag-ind-bit-mapping-fsp-id-258) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_259](#table-bf-drag-ind-bit-mapping-fsp-id-259) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_26](#table-bf-drag-ind-bit-mapping-fsp-id-26) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_260](#table-bf-drag-ind-bit-mapping-fsp-id-260) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_261](#table-bf-drag-ind-bit-mapping-fsp-id-261) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_262](#table-bf-drag-ind-bit-mapping-fsp-id-262) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_263](#table-bf-drag-ind-bit-mapping-fsp-id-263) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_264](#table-bf-drag-ind-bit-mapping-fsp-id-264) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_265](#table-bf-drag-ind-bit-mapping-fsp-id-265) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_266](#table-bf-drag-ind-bit-mapping-fsp-id-266) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_267](#table-bf-drag-ind-bit-mapping-fsp-id-267) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_268](#table-bf-drag-ind-bit-mapping-fsp-id-268) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_269](#table-bf-drag-ind-bit-mapping-fsp-id-269) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_27](#table-bf-drag-ind-bit-mapping-fsp-id-27) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_270](#table-bf-drag-ind-bit-mapping-fsp-id-270) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_271](#table-bf-drag-ind-bit-mapping-fsp-id-271) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_272](#table-bf-drag-ind-bit-mapping-fsp-id-272) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_273](#table-bf-drag-ind-bit-mapping-fsp-id-273) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_274](#table-bf-drag-ind-bit-mapping-fsp-id-274) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_275](#table-bf-drag-ind-bit-mapping-fsp-id-275) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_276](#table-bf-drag-ind-bit-mapping-fsp-id-276) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_277](#table-bf-drag-ind-bit-mapping-fsp-id-277) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_278](#table-bf-drag-ind-bit-mapping-fsp-id-278) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_279](#table-bf-drag-ind-bit-mapping-fsp-id-279) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_28](#table-bf-drag-ind-bit-mapping-fsp-id-28) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_280](#table-bf-drag-ind-bit-mapping-fsp-id-280) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_281](#table-bf-drag-ind-bit-mapping-fsp-id-281) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_282](#table-bf-drag-ind-bit-mapping-fsp-id-282) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_283](#table-bf-drag-ind-bit-mapping-fsp-id-283) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_284](#table-bf-drag-ind-bit-mapping-fsp-id-284) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_285](#table-bf-drag-ind-bit-mapping-fsp-id-285) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_286](#table-bf-drag-ind-bit-mapping-fsp-id-286) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_287](#table-bf-drag-ind-bit-mapping-fsp-id-287) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_288](#table-bf-drag-ind-bit-mapping-fsp-id-288) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_289](#table-bf-drag-ind-bit-mapping-fsp-id-289) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_29](#table-bf-drag-ind-bit-mapping-fsp-id-29) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_290](#table-bf-drag-ind-bit-mapping-fsp-id-290) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_291](#table-bf-drag-ind-bit-mapping-fsp-id-291) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_292](#table-bf-drag-ind-bit-mapping-fsp-id-292) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_293](#table-bf-drag-ind-bit-mapping-fsp-id-293) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_294](#table-bf-drag-ind-bit-mapping-fsp-id-294) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_295](#table-bf-drag-ind-bit-mapping-fsp-id-295) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_296](#table-bf-drag-ind-bit-mapping-fsp-id-296) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_297](#table-bf-drag-ind-bit-mapping-fsp-id-297) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_298](#table-bf-drag-ind-bit-mapping-fsp-id-298) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_299](#table-bf-drag-ind-bit-mapping-fsp-id-299) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_3](#table-bf-drag-ind-bit-mapping-fsp-id-3) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_30](#table-bf-drag-ind-bit-mapping-fsp-id-30) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_300](#table-bf-drag-ind-bit-mapping-fsp-id-300) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_301](#table-bf-drag-ind-bit-mapping-fsp-id-301) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_302](#table-bf-drag-ind-bit-mapping-fsp-id-302) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_303](#table-bf-drag-ind-bit-mapping-fsp-id-303) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_304](#table-bf-drag-ind-bit-mapping-fsp-id-304) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_305](#table-bf-drag-ind-bit-mapping-fsp-id-305) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_306](#table-bf-drag-ind-bit-mapping-fsp-id-306) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_307](#table-bf-drag-ind-bit-mapping-fsp-id-307) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_308](#table-bf-drag-ind-bit-mapping-fsp-id-308) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_309](#table-bf-drag-ind-bit-mapping-fsp-id-309) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_31](#table-bf-drag-ind-bit-mapping-fsp-id-31) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_310](#table-bf-drag-ind-bit-mapping-fsp-id-310) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_311](#table-bf-drag-ind-bit-mapping-fsp-id-311) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_312](#table-bf-drag-ind-bit-mapping-fsp-id-312) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_313](#table-bf-drag-ind-bit-mapping-fsp-id-313) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_314](#table-bf-drag-ind-bit-mapping-fsp-id-314) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_315](#table-bf-drag-ind-bit-mapping-fsp-id-315) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_316](#table-bf-drag-ind-bit-mapping-fsp-id-316) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_317](#table-bf-drag-ind-bit-mapping-fsp-id-317) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_318](#table-bf-drag-ind-bit-mapping-fsp-id-318) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_319](#table-bf-drag-ind-bit-mapping-fsp-id-319) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_32](#table-bf-drag-ind-bit-mapping-fsp-id-32) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_320](#table-bf-drag-ind-bit-mapping-fsp-id-320) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_321](#table-bf-drag-ind-bit-mapping-fsp-id-321) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_322](#table-bf-drag-ind-bit-mapping-fsp-id-322) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_323](#table-bf-drag-ind-bit-mapping-fsp-id-323) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_324](#table-bf-drag-ind-bit-mapping-fsp-id-324) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_325](#table-bf-drag-ind-bit-mapping-fsp-id-325) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_326](#table-bf-drag-ind-bit-mapping-fsp-id-326) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_327](#table-bf-drag-ind-bit-mapping-fsp-id-327) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_328](#table-bf-drag-ind-bit-mapping-fsp-id-328) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_329](#table-bf-drag-ind-bit-mapping-fsp-id-329) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_33](#table-bf-drag-ind-bit-mapping-fsp-id-33) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_330](#table-bf-drag-ind-bit-mapping-fsp-id-330) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_331](#table-bf-drag-ind-bit-mapping-fsp-id-331) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_332](#table-bf-drag-ind-bit-mapping-fsp-id-332) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_333](#table-bf-drag-ind-bit-mapping-fsp-id-333) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_334](#table-bf-drag-ind-bit-mapping-fsp-id-334) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_335](#table-bf-drag-ind-bit-mapping-fsp-id-335) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_336](#table-bf-drag-ind-bit-mapping-fsp-id-336) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_337](#table-bf-drag-ind-bit-mapping-fsp-id-337) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_338](#table-bf-drag-ind-bit-mapping-fsp-id-338) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_339](#table-bf-drag-ind-bit-mapping-fsp-id-339) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_34](#table-bf-drag-ind-bit-mapping-fsp-id-34) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_340](#table-bf-drag-ind-bit-mapping-fsp-id-340) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_341](#table-bf-drag-ind-bit-mapping-fsp-id-341) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_342](#table-bf-drag-ind-bit-mapping-fsp-id-342) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_343](#table-bf-drag-ind-bit-mapping-fsp-id-343) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_344](#table-bf-drag-ind-bit-mapping-fsp-id-344) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_345](#table-bf-drag-ind-bit-mapping-fsp-id-345) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_346](#table-bf-drag-ind-bit-mapping-fsp-id-346) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_347](#table-bf-drag-ind-bit-mapping-fsp-id-347) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_348](#table-bf-drag-ind-bit-mapping-fsp-id-348) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_349](#table-bf-drag-ind-bit-mapping-fsp-id-349) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_35](#table-bf-drag-ind-bit-mapping-fsp-id-35) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_350](#table-bf-drag-ind-bit-mapping-fsp-id-350) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_351](#table-bf-drag-ind-bit-mapping-fsp-id-351) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_352](#table-bf-drag-ind-bit-mapping-fsp-id-352) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_353](#table-bf-drag-ind-bit-mapping-fsp-id-353) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_354](#table-bf-drag-ind-bit-mapping-fsp-id-354) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_355](#table-bf-drag-ind-bit-mapping-fsp-id-355) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_356](#table-bf-drag-ind-bit-mapping-fsp-id-356) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_357](#table-bf-drag-ind-bit-mapping-fsp-id-357) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_358](#table-bf-drag-ind-bit-mapping-fsp-id-358) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_359](#table-bf-drag-ind-bit-mapping-fsp-id-359) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_36](#table-bf-drag-ind-bit-mapping-fsp-id-36) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_360](#table-bf-drag-ind-bit-mapping-fsp-id-360) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_361](#table-bf-drag-ind-bit-mapping-fsp-id-361) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_362](#table-bf-drag-ind-bit-mapping-fsp-id-362) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_363](#table-bf-drag-ind-bit-mapping-fsp-id-363) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_364](#table-bf-drag-ind-bit-mapping-fsp-id-364) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_365](#table-bf-drag-ind-bit-mapping-fsp-id-365) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_366](#table-bf-drag-ind-bit-mapping-fsp-id-366) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_367](#table-bf-drag-ind-bit-mapping-fsp-id-367) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_368](#table-bf-drag-ind-bit-mapping-fsp-id-368) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_369](#table-bf-drag-ind-bit-mapping-fsp-id-369) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_37](#table-bf-drag-ind-bit-mapping-fsp-id-37) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_370](#table-bf-drag-ind-bit-mapping-fsp-id-370) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_371](#table-bf-drag-ind-bit-mapping-fsp-id-371) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_372](#table-bf-drag-ind-bit-mapping-fsp-id-372) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_373](#table-bf-drag-ind-bit-mapping-fsp-id-373) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_374](#table-bf-drag-ind-bit-mapping-fsp-id-374) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_375](#table-bf-drag-ind-bit-mapping-fsp-id-375) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_376](#table-bf-drag-ind-bit-mapping-fsp-id-376) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_377](#table-bf-drag-ind-bit-mapping-fsp-id-377) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_378](#table-bf-drag-ind-bit-mapping-fsp-id-378) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_379](#table-bf-drag-ind-bit-mapping-fsp-id-379) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_38](#table-bf-drag-ind-bit-mapping-fsp-id-38) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_380](#table-bf-drag-ind-bit-mapping-fsp-id-380) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_381](#table-bf-drag-ind-bit-mapping-fsp-id-381) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_382](#table-bf-drag-ind-bit-mapping-fsp-id-382) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_383](#table-bf-drag-ind-bit-mapping-fsp-id-383) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_384](#table-bf-drag-ind-bit-mapping-fsp-id-384) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_385](#table-bf-drag-ind-bit-mapping-fsp-id-385) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_386](#table-bf-drag-ind-bit-mapping-fsp-id-386) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_387](#table-bf-drag-ind-bit-mapping-fsp-id-387) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_388](#table-bf-drag-ind-bit-mapping-fsp-id-388) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_389](#table-bf-drag-ind-bit-mapping-fsp-id-389) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_39](#table-bf-drag-ind-bit-mapping-fsp-id-39) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_390](#table-bf-drag-ind-bit-mapping-fsp-id-390) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_391](#table-bf-drag-ind-bit-mapping-fsp-id-391) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_392](#table-bf-drag-ind-bit-mapping-fsp-id-392) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_393](#table-bf-drag-ind-bit-mapping-fsp-id-393) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_394](#table-bf-drag-ind-bit-mapping-fsp-id-394) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_395](#table-bf-drag-ind-bit-mapping-fsp-id-395) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_396](#table-bf-drag-ind-bit-mapping-fsp-id-396) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_397](#table-bf-drag-ind-bit-mapping-fsp-id-397) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_398](#table-bf-drag-ind-bit-mapping-fsp-id-398) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_399](#table-bf-drag-ind-bit-mapping-fsp-id-399) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_4](#table-bf-drag-ind-bit-mapping-fsp-id-4) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_40](#table-bf-drag-ind-bit-mapping-fsp-id-40) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_400](#table-bf-drag-ind-bit-mapping-fsp-id-400) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_401](#table-bf-drag-ind-bit-mapping-fsp-id-401) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_402](#table-bf-drag-ind-bit-mapping-fsp-id-402) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_403](#table-bf-drag-ind-bit-mapping-fsp-id-403) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_404](#table-bf-drag-ind-bit-mapping-fsp-id-404) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_405](#table-bf-drag-ind-bit-mapping-fsp-id-405) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_406](#table-bf-drag-ind-bit-mapping-fsp-id-406) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_407](#table-bf-drag-ind-bit-mapping-fsp-id-407) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_408](#table-bf-drag-ind-bit-mapping-fsp-id-408) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_409](#table-bf-drag-ind-bit-mapping-fsp-id-409) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_41](#table-bf-drag-ind-bit-mapping-fsp-id-41) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_410](#table-bf-drag-ind-bit-mapping-fsp-id-410) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_411](#table-bf-drag-ind-bit-mapping-fsp-id-411) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_412](#table-bf-drag-ind-bit-mapping-fsp-id-412) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_413](#table-bf-drag-ind-bit-mapping-fsp-id-413) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_414](#table-bf-drag-ind-bit-mapping-fsp-id-414) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_415](#table-bf-drag-ind-bit-mapping-fsp-id-415) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_42](#table-bf-drag-ind-bit-mapping-fsp-id-42) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_43](#table-bf-drag-ind-bit-mapping-fsp-id-43) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_44](#table-bf-drag-ind-bit-mapping-fsp-id-44) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_45](#table-bf-drag-ind-bit-mapping-fsp-id-45) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_46](#table-bf-drag-ind-bit-mapping-fsp-id-46) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_47](#table-bf-drag-ind-bit-mapping-fsp-id-47) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_48](#table-bf-drag-ind-bit-mapping-fsp-id-48) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_49](#table-bf-drag-ind-bit-mapping-fsp-id-49) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_5](#table-bf-drag-ind-bit-mapping-fsp-id-5) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_50](#table-bf-drag-ind-bit-mapping-fsp-id-50) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_51](#table-bf-drag-ind-bit-mapping-fsp-id-51) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_52](#table-bf-drag-ind-bit-mapping-fsp-id-52) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_53](#table-bf-drag-ind-bit-mapping-fsp-id-53) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_54](#table-bf-drag-ind-bit-mapping-fsp-id-54) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_55](#table-bf-drag-ind-bit-mapping-fsp-id-55) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_56](#table-bf-drag-ind-bit-mapping-fsp-id-56) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_57](#table-bf-drag-ind-bit-mapping-fsp-id-57) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_58](#table-bf-drag-ind-bit-mapping-fsp-id-58) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_59](#table-bf-drag-ind-bit-mapping-fsp-id-59) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_6](#table-bf-drag-ind-bit-mapping-fsp-id-6) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_60](#table-bf-drag-ind-bit-mapping-fsp-id-60) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_61](#table-bf-drag-ind-bit-mapping-fsp-id-61) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_62](#table-bf-drag-ind-bit-mapping-fsp-id-62) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_63](#table-bf-drag-ind-bit-mapping-fsp-id-63) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_64](#table-bf-drag-ind-bit-mapping-fsp-id-64) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_65](#table-bf-drag-ind-bit-mapping-fsp-id-65) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_66](#table-bf-drag-ind-bit-mapping-fsp-id-66) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_67](#table-bf-drag-ind-bit-mapping-fsp-id-67) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_68](#table-bf-drag-ind-bit-mapping-fsp-id-68) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_69](#table-bf-drag-ind-bit-mapping-fsp-id-69) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_7](#table-bf-drag-ind-bit-mapping-fsp-id-7) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_70](#table-bf-drag-ind-bit-mapping-fsp-id-70) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_71](#table-bf-drag-ind-bit-mapping-fsp-id-71) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_72](#table-bf-drag-ind-bit-mapping-fsp-id-72) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_73](#table-bf-drag-ind-bit-mapping-fsp-id-73) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_74](#table-bf-drag-ind-bit-mapping-fsp-id-74) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_75](#table-bf-drag-ind-bit-mapping-fsp-id-75) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_76](#table-bf-drag-ind-bit-mapping-fsp-id-76) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_77](#table-bf-drag-ind-bit-mapping-fsp-id-77) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_78](#table-bf-drag-ind-bit-mapping-fsp-id-78) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_79](#table-bf-drag-ind-bit-mapping-fsp-id-79) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_8](#table-bf-drag-ind-bit-mapping-fsp-id-8) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_80](#table-bf-drag-ind-bit-mapping-fsp-id-80) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_81](#table-bf-drag-ind-bit-mapping-fsp-id-81) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_82](#table-bf-drag-ind-bit-mapping-fsp-id-82) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_83](#table-bf-drag-ind-bit-mapping-fsp-id-83) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_84](#table-bf-drag-ind-bit-mapping-fsp-id-84) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_85](#table-bf-drag-ind-bit-mapping-fsp-id-85) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_86](#table-bf-drag-ind-bit-mapping-fsp-id-86) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_87](#table-bf-drag-ind-bit-mapping-fsp-id-87) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_88](#table-bf-drag-ind-bit-mapping-fsp-id-88) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_89](#table-bf-drag-ind-bit-mapping-fsp-id-89) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_9](#table-bf-drag-ind-bit-mapping-fsp-id-9) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_90](#table-bf-drag-ind-bit-mapping-fsp-id-90) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_91](#table-bf-drag-ind-bit-mapping-fsp-id-91) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_92](#table-bf-drag-ind-bit-mapping-fsp-id-92) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_93](#table-bf-drag-ind-bit-mapping-fsp-id-93) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_94](#table-bf-drag-ind-bit-mapping-fsp-id-94) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_95](#table-bf-drag-ind-bit-mapping-fsp-id-95) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_96](#table-bf-drag-ind-bit-mapping-fsp-id-96) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_97](#table-bf-drag-ind-bit-mapping-fsp-id-97) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_98](#table-bf-drag-ind-bit-mapping-fsp-id-98) (2 × 10)
- [BF_DRAG_IND_BIT_MAPPING_FSP_ID_99](#table-bf-drag-ind-bit-mapping-fsp-id-99) (2 × 10)
- [BF_ESP_STATE_STRUCT](#table-bf-esp-state-struct) (3 × 10)
- [BF_FAIL_LIGHT_STATE_STRUCT](#table-bf-fail-light-state-struct) (1 × 10)
- [BF_FSP_ID_0_DRAG_IND](#table-bf-fsp-id-0-drag-ind) (2 × 10)
- [BF_HND_BRK_STATE_BIT_STRUCT](#table-bf-hnd-brk-state-bit-struct) (2 × 10)
- [BF_LAUNCH_STATE](#table-bf-launch-state) (3 × 10)
- [BF_LHM1_STRUCT](#table-bf-lhm1-struct) (8 × 10)
- [BF_LHM2_STRUCT](#table-bf-lhm2-struct) (8 × 10)
- [BF_LHM3_STRUCT](#table-bf-lhm3-struct) (8 × 10)
- [BF_LHM4_STRUCT](#table-bf-lhm4-struct) (8 × 10)
- [BF_LHM5_STRUCT](#table-bf-lhm5-struct) (8 × 10)
- [BF_LHM6_STRUCT](#table-bf-lhm6-struct) (8 × 10)
- [BF_LHM7_STRUCT](#table-bf-lhm7-struct) (4 × 10)
- [BF_MSA_LOCKING_FUNCTION_STRUCT](#table-bf-msa-locking-function-struct) (10 × 10)
- [BF_SAILINGS_TATUS_STRUCT](#table-bf-sailings-tatus-struct) (32 × 10)
- [BRK_STATE_BIT0_TABLE](#table-brk-state-bit0-table) (3 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [CLUTCH_RUN_IN_STATE](#table-clutch-run-in-state) (3 × 2)
- [CLU_MOT_COOL_SPD_CONVERSION](#table-clu-mot-cool-spd-conversion) (15 × 2)
- [CLU_PRS_CNTRL_SHFT_GEAR_1_TAB](#table-clu-prs-cntrl-shft-gear-1-tab) (8 × 2)
- [DHCLIENTSTATE](#table-dhclientstate) (9 × 2)
- [ECU_DEVICE_STATE_TABLE](#table-ecu-device-state-table) (5 × 2)
- [EEP_COR_FLG_TABLE](#table-eep-cor-flg-table) (6 × 2)
- [ENG_CRNK_ENA_TABLE](#table-eng-crnk-ena-table) (5 × 2)
- [EWS4STATE](#table-ews4state) (9 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FOOT_BRK_STATE_TABLE](#table-foot-brk-state-table) (3 × 2)
- [FORTTEXTE](#table-forttexte) (349 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (238 × 9)
- [GEAR_INFO](#table-gear-info) (20 × 2)
- [HND_BRK_STATE_BIT1_TABLE](#table-hnd-brk-state-bit1-table) (3 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (16 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (238 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [OIL_CLUTCH_CHANGED](#table-oil-clutch-changed) (5 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (4 × 2)
- [RESERVE](#table-reserve) (1 × 2)
- [RES_0X1061_R](#table-res-0x1061-r) (1 × 13)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X4005_D](#table-res-0x4005-d) (31 × 10)
- [RES_0X4006_D](#table-res-0x4006-d) (9 × 10)
- [RES_0X4006_R](#table-res-0x4006-r) (1 × 13)
- [RES_0X4007_D](#table-res-0x4007-d) (309 × 10)
- [RES_0X4008_D](#table-res-0x4008-d) (38 × 10)
- [RES_0X4009_D](#table-res-0x4009-d) (25 × 10)
- [RES_0X413C_D](#table-res-0x413c-d) (2 × 10)
- [RES_0X4141_D](#table-res-0x4141-d) (18 × 10)
- [RES_0X4142_D](#table-res-0x4142-d) (13 × 10)
- [RES_0X4143_D](#table-res-0x4143-d) (24 × 10)
- [RES_0X4144_D](#table-res-0x4144-d) (17 × 10)
- [RES_0X4145_D](#table-res-0x4145-d) (20 × 10)
- [RES_0X4146_D](#table-res-0x4146-d) (10 × 10)
- [RES_0X4148_D](#table-res-0x4148-d) (81 × 10)
- [RES_0X4149_D](#table-res-0x4149-d) (2 × 10)
- [RES_0X4300_D](#table-res-0x4300-d) (2 × 10)
- [RES_0X4312_D](#table-res-0x4312-d) (1 × 10)
- [RES_0X4314_D](#table-res-0x4314-d) (416 × 10)
- [RES_0XC000_D](#table-res-0xc000-d) (16 × 10)
- [RES_0XD9C9_D](#table-res-0xd9c9-d) (7 × 10)
- [RES_0XDA2E_D](#table-res-0xda2e-d) (2 × 10)
- [RES_0XDA65_D](#table-res-0xda65-d) (26 × 10)
- [RES_0XF100_R](#table-res-0xf100-r) (2 × 13)
- [RES_0XF401_R](#table-res-0xf401-r) (7 × 13)
- [RES_0XF402_R](#table-res-0xf402-r) (5 × 13)
- [RES_0XF410_R](#table-res-0xf410-r) (3 × 13)
- [RES_0XF411_R](#table-res-0xf411-r) (3 × 13)
- [RES_0XF413_R](#table-res-0xf413-r) (8 × 13)
- [RES_0XF415_R](#table-res-0xf415-r) (1 × 13)
- [RES_0XF416_R](#table-res-0xf416-r) (8 × 13)
- [RES_0XF417_R](#table-res-0xf417-r) (2 × 13)
- [RES_0XF422_R](#table-res-0xf422-r) (1 × 13)
- [RES_0XF432_R](#table-res-0xf432-r) (1 × 13)
- [SAILING_MODE](#table-sailing-mode) (9 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (115 × 16)
- [SHFT_LEV_DSPL_VAL_TABLE](#table-shft-lev-dspl-val-table) (8 × 2)
- [SHFT_LEV_POS_TABLE](#table-shft-lev-pos-table) (14 × 2)
- [STATUS_CLU_PRS_CNTRL_TAB](#table-status-clu-prs-cntrl-tab) (7 × 2)
- [STATUS_RAM_DATEN_SCHREIBEN_TAB](#table-status-ram-daten-schreiben-tab) (4 × 2)
- [STAT_CLU_PRS_CNTRL_SHFT_GEAR_2_TAB](#table-stat-clu-prs-cntrl-shft-gear-2-tab) (9 × 2)
- [STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_1_ARG_TAB](#table-steuern-clu-prs-cntrl-shft-gear-1-arg-tab) (7 × 2)
- [STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_2_ARG_TAB](#table-steuern-clu-prs-cntrl-shft-gear-2-arg-tab) (8 × 2)
- [TABLE_CC_STATE](#table-table-cc-state) (4 × 2)
- [TABLE_MSA_STATE](#table-table-msa-state) (4 × 2)
- [TABLE_REQUEST_MSA_SHUTOFF](#table-table-request-msa-shutoff) (3 × 2)
- [TABLE_SHIFT_LOGIC_DIAGNOSTIC](#table-table-shift-logic-diagnostic) (19 × 2)
- [TAB_AUTOP_DEACTIVATION](#table-tab-autop-deactivation) (3 × 2)
- [TAB_AUTOP_DEACTIVATION_STAT](#table-tab-autop-deactivation-stat) (3 × 2)
- [TAB_CAP_SPD_2_PRS_ADA](#table-tab-cap-spd-2-prs-ada) (7 × 2)
- [TAB_CHECK_ISS_SENS_STATUS](#table-tab-check-iss-sens-status) (8 × 2)
- [TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1_ARG](#table-tab-clu-actu-pwm-cntrl-shft-gear-1-arg) (7 × 2)
- [TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2_ARG](#table-tab-clu-actu-pwm-cntrl-shft-gear-2-arg) (8 × 2)
- [TAB_DEZ_VALUES](#table-tab-dez-values) (256 × 2)
- [TAB_DRM_INFO_STATE](#table-tab-drm-info-state) (17 × 2)
- [TAB_EEPROM_STATUS](#table-tab-eeprom-status) (8 × 2)
- [TAB_ENCOD_ERROR](#table-tab-encod-error) (9 × 2)
- [TAB_ENG_STATE](#table-tab-eng-state) (5 × 2)
- [TAB_EWS_MODE_ARG](#table-tab-ews-mode-arg) (2 × 2)
- [TAB_FAHRSTUFE](#table-tab-fahrstufe) (6 × 2)
- [TAB_GEN_STATUS](#table-tab-gen-status) (6 × 2)
- [TAB_IMO_KEY_COND](#table-tab-imo-key-cond) (17 × 2)
- [TAB_ISTGANG](#table-tab-istgang) (12 × 2)
- [TAB_PHYS_PRND](#table-tab-phys-prnd) (9 × 2)
- [TAB_PRDNL_POS_ENA](#table-tab-prdnl-pos-ena) (6 × 2)
- [TAB_REF_DRIVE_ERROR_STATUS](#table-tab-ref-drive-error-status) (5 × 2)
- [TAB_REPLACE_ME](#table-tab-replace-me) (3 × 2)
- [TAB_REPLACE_ME_1](#table-tab-replace-me-1) (2 × 2)
- [TAB_REPLACE_ME_2](#table-tab-replace-me-2) (2 × 2)
- [TAB_REPLACE_ME_4](#table-tab-replace-me-4) (2 × 2)
- [TAB_REPLACE_ME_5](#table-tab-replace-me-5) (2 × 2)
- [TAB_REPLACE_ME_6](#table-tab-replace-me-6) (2 × 2)
- [TAB_REPLACE_ME_8](#table-tab-replace-me-8) (2 × 2)
- [TAB_SD_ERROR_STATUS](#table-tab-sd-error-status) (6 × 2)
- [TAB_SECRET_KEY](#table-tab-secret-key) (6 × 2)
- [TAB_SECRET_NUMBER](#table-tab-secret-number) (4 × 2)
- [TAB_SHFTLCK_STATE](#table-tab-shftlck-state) (7 × 2)
- [TAB_SHIFT_GEAR_P](#table-tab-shift-gear-p) (3 × 2)
- [TAB_STATUS_CHECK_ISS_SENS](#table-tab-status-check-iss-sens) (7 × 2)
- [TAB_STATUS_CLU_ACTU_PWM_CNTRL](#table-tab-status-clu-actu-pwm-cntrl) (7 × 2)
- [TAB_STATUS_CLU_GAIN_ADA_RST_VALUES](#table-tab-status-clu-gain-ada-rst-values) (7 × 2)
- [TAB_STATUS_CLU_SELF_OPEN_TST](#table-tab-status-clu-self-open-tst) (7 × 2)
- [TAB_STATUS_CLU_SIM_PRS_CNTRL](#table-tab-status-clu-sim-prs-cntrl) (7 × 2)
- [TAB_STATUS_CLU_TP_ADA](#table-tab-status-clu-tp-ada) (7 × 2)
- [TAB_STATUS_GTI_REQ_INFO_SD1](#table-tab-status-gti-req-info-sd1) (25 × 2)
- [TAB_STATUS_REF_SD_POS](#table-tab-status-ref-sd-pos) (7 × 2)
- [TAB_STATUS_RST_TEACHIN_VAL](#table-tab-status-rst-teachin-val) (7 × 2)
- [TAB_STATUS_SEGELN_ROLLE](#table-tab-status-segeln-rolle) (4 × 2)
- [TAB_STATUS_SHFT_GEARS](#table-tab-status-shft-gears) (7 × 2)
- [TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1](#table-tab-stat-clu-actu-pwm-cntrl-shft-gear-1) (8 × 2)
- [TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2](#table-tab-stat-clu-actu-pwm-cntrl-shft-gear-2) (9 × 2)
- [TAB_STAT_GTI_REQ_INFO_SD1](#table-tab-stat-gti-req-info-sd1) (25 × 2)
- [TAB_STAT_GTI_REQ_INFO_SD2](#table-tab-stat-gti-req-info-sd2) (25 × 2)
- [TAB_STAT_SDS_INS_SPD_FRM_STATUS_1](#table-tab-stat-sds-ins-spd-frm-status-1) (6 × 2)
- [TAB_STAT_SDS_INS_SPD_FRM_STATUS_2](#table-tab-stat-sds-ins-spd-frm-status-2) (6 × 2)
- [TAB_STEUERN_CLU_SELF_OPEN_TST_CLU_NR](#table-tab-steuern-clu-self-open-tst-clu-nr) (2 × 2)
- [TAB_STEUERN_CLU_SELF_OPEN_TST_CNTRL_STRAT](#table-tab-steuern-clu-self-open-tst-cntrl-strat) (3 × 2)
- [TAB_STEUERN_CLU_TP_ADA_START_CLU_NR_ARG](#table-tab-steuern-clu-tp-ada-start-clu-nr-arg) (3 × 2)
- [TAB_STEUERN_EWS_FSC_EWS_OPT](#table-tab-steuern-ews-fsc-ews-opt) (2 × 2)
- [TAB_STEUERN_SEGELN_ROLLE](#table-tab-steuern-segeln-rolle) (4 × 2)
- [TAB_TARGET_GEAR_SD1](#table-tab-target-gear-sd1) (7 × 2)
- [TAB_TARGET_GEAR_SD2](#table-tab-target-gear-sd2) (8 × 2)
- [TSL_GEAR_CNT_TABLE](#table-tsl-gear-cnt-table) (1 × 2)
- [VERSION](#table-version) (9 × 2)
- [WDBYI_RESET_FLAG_TABLE](#table-wdbyi-reset-flag-table) (1 × 2)

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

<a id="table-cbsnrtext"></a>
### CBSNRTEXT

Dimensions: 27 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelaege vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x05 | Bsi | Service Inclusive |
| 0x06 | Br_h | Bremsbelaege hinten |
| 0x07 | Pf | Partikelfilter |
| 0x08 | Soh | State of Health |
| 0x0A | Zuend | Zuendkerzen/Gluehkerzen |
| 0x0D | NOx_a | NOx-Additiv |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x17 | Wf | Wasserfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x23 | Goel | Getriebeoel |
| 0x31 | Reif | Reifenalter |
| 0x32 | Kup | Kupplung |
| 0x33 | Gdf | Gasdruckdämpfer Frontklappe bei aktivem Fußgängerschutz |
| 0x34 | Verb | Verbandskasten |
| 0x35 | Tir_f | Tire Fit |
| 0x36 | Kat | Katalysator |
| 0x37 | Sto | Stossdaempfer |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |
| 0xE0 | Cbs_e | CBS Evalboard |
| 0xE1 | Cbr_e | CBR Evalboard |
| 0xFF | rda | Anlieferzustand |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 30 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelaege vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x05 | Bsi | Service Inclusive |
| 0x06 | Br_h | Bremsbelaege hinten |
| 0x07 | Pf | Partikelfilter |
| 0x07 | Dpf | Partikelfilter |
| 0x07 | Opf | Partikelfilter |
| 0x08 | Soh | State of Health |
| 0x0A | Zuend | Zuendkerzen/Gluehkerzen |
| 0x0D | NOx_a | NOx-Additiv |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x17 | Wf | Wasserfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x23 | Goel | Getriebeoel |
| 0x23 | Oel_a | Getriebeoel (Automatik) |
| 0x31 | Reif | Reifenalter |
| 0x32 | Kup | Kupplung |
| 0x33 | Gdf | Gasdruckdämpfer Frontklappe bei aktivem Fußgängerschutz |
| 0x34 | Verb | Verbandskasten |
| 0x35 | Tir_f | Tire Fit |
| 0x36 | Kat | Katalysator |
| 0x37 | Sto | Stossdaempfer |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |
| 0xE0 | Cbs_e | CBS Evalboard |
| 0xE1 | Cbr_e | CBR Evalboard |
| 0xFF | rda | Anlieferzustand |

<a id="table-tab-ecu-name"></a>
### TAB_ECU_NAME

Dimensions: 6 rows × 2 columns

| ADR | NAME |
| --- | --- |
| 0x12 | DME/DDE |
| 0x13 | DME/DDE_Slave |
| 0x18 | EGS |
| 0x29 | DSC/IB |
| 0x60 | KOMBI |
| 0xFF | unbekannt |

<a id="table-tab-cbs-einheiten"></a>
### TAB_CBS_EINHEITEN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | % |
| 0x01 | Weg |
| 0x02 | Tage |
| 0x0F | Signal ungültig |
| 0xFF | nicht erlaubt |

<a id="table-tab-cbs-status"></a>
### TAB_CBS_STATUS

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Status ok |
| 0x10 | Messung basiert auf Ersatzwerten |
| 0x20 | Status ok und Baukasten Client |
| 0x30 | Baukasten Client und Messung basiert auf Ersatzwerten |
| 0x40 | CBS Daten manipuliert |
| 0x50 | CBS Daten manipuliert und Messung basiert auf Ersatzwerten |
| 0x60 | CBS Daten manipuliert und Baukasten Client |
| 0x70 | CBS Daten manipuliert, Messung basiert auf Ersatzwerten und Baukasten Client |
| 0x80 | Signal ungültig |
| 0x90 | Signal ungültig |
| 0xA0 | Signal ungültig |
| 0xB0 | Signal ungültig |
| 0xC0 | Signal ungültig |
| 0xD0 | Signal ungültig |
| 0xE0 | Signal ungültig |
| 0xF0 | Signal ungültig |
| 0xFF | nicht erlaubt |

<a id="table-tab-cbs-monat"></a>
### TAB_CBS_MONAT

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht relevant |
| 0x01 | Januar |
| 0x02 | Februar |
| 0x03 | März |
| 0x04 | April |
| 0x05 | Mai |
| 0x06 | Juni |
| 0x07 | Juli |
| 0x08 | August |
| 0x09 | September |
| 0x0A | Oktober |
| 0x0B | November |
| 0x0C | Dezember |
| 0x0E | Neues Steuergerät |
| 0x0F | Wert ungültig, Datum nicht verfügbar |
| 0xFF | nicht erlaubt |

<a id="table-tab-rueck-grund"></a>
### TAB_RUECK_GRUND

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Verhinderungsgründe |
| 0x01 | ungültiger km-Stand |
| 0x02 | ungültiges Borddatum |
| 0x03 | ungültige Codierung |
| 0x04 | SG nicht initialisiert oder im falschen Zustand |
| 0x05 | Fahrzeug im fahrenden Zustand |
| 0x06 | Reset beim CBR nicht erlaubt |
| 0x07 | Reset bei aktivem Ersatzwert nicht erlaubt |
| 0x08 | Fahrzeug im Zustand Wohnen |
| 0xFE | keine Angabe |
| 0xFF | ungültig |

<a id="table-arg-0x400a-d"></a>
### ARG_0X400A_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RESET_DATA_ARG | 0-n | high | unsigned char | - | WDBYI_RESET_FLAG_TABLE | - | - | - | - | - | Reset Flag zum Zurücksetzen der Daten |

<a id="table-arg-0x4142-d"></a>
### ARG_0X4142_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TSL_GEAR_CNT_TBL | 0-n | high | unsigned char | - | TSL_GEAR_CNT_TABLE | - | - | - | - | - | Reset Flag zum Zurücksetzen der Daten |

<a id="table-arg-0x4143-d"></a>
### ARG_0X4143_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RESET_FLAG | 0-n | high | unsigned char | - | WDBYI_RESET_FLAG_TABLE | - | - | - | - | - | Reset Flag zum Zurücksetzen der Daten |

<a id="table-arg-0x4148-d"></a>
### ARG_0X4148_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RESET_FLAG | 0-n | high | unsigned char | - | WDBYI_RESET_FLAG_TABLE | - | - | - | - | - | Reset Flag zum Zurücksetzen der Daten |

<a id="table-arg-0x4310-d"></a>
### ARG_0X4310_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OILSCHADENSMODEL_RESET_FLAG | 0-n | high | unsigned char | - | OIL_CLUTCH_CHANGED | - | - | - | - | - | Reset flag zum Zurücksetzen des Öl-Schadensmodel |

<a id="table-arg-0x4312-d"></a>
### ARG_0X4312_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| IDR_EGS_DATA | DATA | high | data[240] | - | - | 1.0 | 1.0 | 0.0 | - | - | Daten der IDR für EGS |

<a id="table-arg-0x4313-d"></a>
### ARG_0X4313_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CLUTCH_RUN_IN_STATE | 0-n | high | unsigned char | - | CLUTCH_RUN_IN_STATE | - | - | - | - | - | Einlaufstatus der Kupplung |

<a id="table-arg-0x4314-d"></a>
### ARG_0X4314_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RESET_DATA_ARG | 0-n | - | unsigned char | - | WDBYI_RESET_FLAG_TABLE | - | - | - | - | - | Reset Flag zum Zurücksetzen der Daten |

<a id="table-arg-0xc001-d"></a>
### ARG_0XC001_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MODE | 0-n | - | unsigned char | - | TAB_EWS_MODE_ARG | - | - | - | - | - | Der Parameter MODE legt die durchzuführende Aktion fest. |
| DATA | DATA | - | data[16] | - | - | 1.0 | 1.0 | 0.0 | - | - | Legt die Daten für die durchzuführende Aktion fest. Folgende Formate müssen unterstützt werden: 01 23 45 67 89 AB CD EF 01 23 45 67 89 AB CD EF und 0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF,0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF. |

<a id="table-arg-0xd9ca-d"></a>
### ARG_0XD9CA_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SEGELN_ROLLE | 0-n | high | unsigned char | - | TAB_STEUERN_SEGELN_ROLLE | - | - | - | - | - | 0x00: Segeln Aktivieren; 0x01: Segeln Deaktivieren; |

<a id="table-arg-0xda15-d"></a>
### ARG_0XDA15_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LERNFKT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Alle Lernfunktionen zurücksetzen = 0 |

<a id="table-arg-0xda66-d"></a>
### ARG_0XDA66_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTOP_DEACTIVATE | 0-n | high | unsigned char | - | TAB_AUTOP_DEACTIVATION | - | - | - | - | - | Deaktivieren von AUTO-P. Siehe Tabelle TAB_AUTOP_DEACTIVATION |

<a id="table-arg-0xda68-d"></a>
### ARG_0XDA68_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SHIFT_GEAR_P | 0-n | high | unsigned char | - | TAB_SHIFT_GEAR_P | - | - | - | - | - | Gang P ein- und auslegen. Siehe Tabelle TAB_SHIFT_GEAR_P |

<a id="table-arg-0xf100-r"></a>
### ARG_0XF100_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RC_EWS_OPT | + | - | 0-n | high | unsigned char | - | TAB_STEUERN_EWS_FSC_EWS_OPT | - | - | - | - | - | Routine Control Option |
| RC_EWS_SW_ID | + | - | HEX | high | unsigned long | - | - | - | - | - | - | - | 4 Byte der SWID für die der Freischaltcode eingespielt werden soll (Big Endian) |
| RC_EWS_DATA | + | - | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | - | - | Routine Control Data |

<a id="table-arg-0xf402-r"></a>
### ARG_0XF402_R

Dimensions: 4 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_SHFT_GEARS_SD1_ARG | + | - | 0-n | high | signed int | - | TAB_TARGET_GEAR_SD1 | - | - | - | - | - | Schaltgänge: Kontrol-Parameter für Schaltwalze1 |
| STEUERN_SHFT_GEARS_SD2_ARG | + | - | 0-n | high | signed int | - | TAB_TARGET_GEAR_SD2 | - | - | - | - | - | Schaltgänge: kontrol Parameter für Schaltwalze 2 |
| STEUERN_SHFT_GEARS_DRB_IDX_SD1_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Fahr-Index von Schaltwalze 1 |
| STEUERN_SHFT_GEARS_DRB_IDX_SD2_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Fahr-Index von Schaltwalze 2 |

<a id="table-arg-0xf410-r"></a>
### ARG_0XF410_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_CLU_TP_ADA_START_CLU_NR_ARG | + | - | 0-n | high | signed int | - | TAB_STEUERN_CLU_TP_ADA_START_CLU_NR_ARG | - | - | - | - | - | Kupplungsnummer |

<a id="table-arg-0xf411-r"></a>
### ARG_0XF411_R

Dimensions: 7 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_CLU_SELF_OPEN_TST_CLU_NR_ARG | + | - | 0-n | high | signed int | - | TAB_STEUERN_CLU_SELF_OPEN_TST_CLU_NR | - | - | - | - | - | Kupplungsnummer |
| STEUERN_CLU_SELF_OPEN_TST_CNTRL_STRAT_ARG | + | - | 0-n | high | signed int | - | TAB_STEUERN_CLU_SELF_OPEN_TST_CNTRL_STRAT | - | - | - | - | - | Steuerstrategie |
| STEUERN_CLU_SELF_OPEN_TST_STRT_LEV_ARG | + | - | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 11500.0 | Voraussetzung: Start-Level muss großer als Finish-Level für Modus 'Passiv' and 'Aktive open'  !!! muss größer als Finishing-Level sein !!! |
| STEUERN_CLU_SELF_OPEN_TST_FIN_LEV_ARG | + | - | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 11500.0 | Finishing-Level !!!Muss größer als die minimale Berührungsposition!!! |
| STEUERN_CLU_SELF_OPEN_TST_HLD_TIM_ARG | + | - | ms | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 32000.0 | Haltezeit der Startdruck |
| STEUERN_CLU_SELF_OPEN_TST_TRG_VOLT_ARG | + | - | mV | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 32000.0 | absolute aktive Öffnung-Sollspannung |
| STEUERN_CLU_SELF_OPEN_TST_OPEN_DUR_ARG | + | - | ms | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 1.0 | 32000.0 | aktive Öffnung-Dauer |

<a id="table-arg-0xf413-r"></a>
### ARG_0XF413_R

Dimensions: 7 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_1_ARG | + | - | 0-n | high | signed int | - | STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_1_ARG_TAB | - | - | - | - | - | Gangschaltung 1 |
| STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_2_ARG | + | - | 0-n | high | signed int | - | STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_2_ARG_TAB | - | - | - | - | - | Gangschaltung 2 |
| STEUERN_CLU_PRS_CNTRL_SHFT_IDX_SD_1_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Schaltung-Index Schaltwalze 1 |
| STEUERN_CLU_PRS_CNTRL_SHFT_IDX_SD_2_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Schaltung-Index - Schaltwalze 2 |
| STEUERN_CLU_PRS_CNTRL_PRS_CAP_1_ARG | + | - | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | Kupplungsaktuatordruck 1 (CAP1) |
| STEUERN_CLU_PRS_CNTRL_PRS_CAP_2_ARG | + | - | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | Kupplungsaktuatordruck 2 (CAP 2) |
| STEUERN_CLU_PRS_CNTRL_FLW_CCP_ARG | + | - | l/h | high | signed int | - | - | 1000.0 | 60.0 | 0.0 | - | - | Fluß von Kupplungskühlung-Druck |

<a id="table-arg-0xf415-r"></a>
### ARG_0XF415_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_CLU_SIM_PRS_CNTRL_PRS_1_ARG | + | - | mbar | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Druck 1 |
| STEUERN_CLU_SIM_PRS_CNTRL_PRS_2_ARG | + | - | mbar | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Druck 2 |

<a id="table-arg-0xf416-r"></a>
### ARG_0XF416_R

Dimensions: 7 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1_ARG | + | - | 0-n | high | signed int | - | TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1_ARG | - | - | - | - | - | Schalt-Gang 1 |
| STEUERN_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2_ARG | + | - | 0-n | high | signed int | - | TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2_ARG | - | - | - | - | - | Schalt-Gang 2 |
| STEUERN_CLU_ACTU_PWM_CNTRL_SHFT_IDX_SD_1_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Schalt-Index-Schaltwalze-1 |
| STEUERN_CLU_ACTU_PWM_CNTRL_SHFT_IDX_SD_2_ARG | + | - | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Schalt-Index-Schaltwalze 2 |
| STEUERN_CLU_ACTU_PWM_CNTRL_CAP_1_ARG | + | - | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | -100.0 | 100.0 | PWM Kupplungsbetätigungspumpe1 |
| STEUERN_CLU_ACTU_PWM_CNTRL_CAP_2_ARG | + | - | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | -100.0 | 100.0 | PWM Kupplungsbetätigungspumpe 2 |
| STEUERN_CLU_ACTU_PWM_CNTRL_CCP_ARG | + | - | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | -100.0 | 100.0 | PWM Kupplung-Kühlpumpe |

<a id="table-back-light-state-table"></a>
### BACK_LIGHT_STATE_TABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Rücklicht aus |
| 0x01 | Rücklicht an |
| 0xFF | Wert ungültig |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-0"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_0

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_0 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_0 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-1"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_1

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_1 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_1 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-10"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_10

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_10 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_10 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-100"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_100

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_100 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_100 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-101"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_101

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_101 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_101 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-102"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_102

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_102 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_102 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-103"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_103

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_103 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_103 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-104"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_104

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_104 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_104 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-105"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_105

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_105 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_105 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-106"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_106

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_106 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_106 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-107"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_107

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_107 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_107 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-108"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_108

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_108 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_108 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-109"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_109

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_109 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_109 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-11"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_11

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_11 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_11 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-110"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_110

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_110 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_110 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-111"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_111

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_111 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_111 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-112"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_112

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_112 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_112 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-113"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_113

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_113 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_113 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-114"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_114

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_114 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_114 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-115"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_115

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_115 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_115 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-116"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_116

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_116 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_116 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-117"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_117

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_117 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_117 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-118"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_118

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_118 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_118 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-119"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_119

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_119 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_119 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-12"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_12

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_12 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_12 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-120"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_120

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_120 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_120 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-121"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_121

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_121 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_121 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-122"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_122

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_122 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_122 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-123"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_123

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_123 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_123 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-124"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_124

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_124 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_124 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-125"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_125

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_125 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_125 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-126"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_126

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_126 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_126 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-127"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_127

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_127 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_127 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-128"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_128

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_128 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_128 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-129"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_129

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_129 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_129 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-13"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_13

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_13 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_13 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-130"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_130

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_130 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_130 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-131"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_131

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_131 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_131 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-132"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_132

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_132 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_132 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-133"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_133

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_133 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_133 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-134"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_134

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_134 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_134 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-135"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_135

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_135 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_135 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-136"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_136

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_136 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_136 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-137"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_137

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_137 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_137 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-138"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_138

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_138 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_138 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-139"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_139

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_139 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_139 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-14"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_14

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_14 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_14 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-140"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_140

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_140 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_140 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-141"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_141

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_141 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_141 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-142"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_142

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_142 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_142 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-143"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_143

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_143 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_143 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-144"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_144

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_144 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_144 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-145"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_145

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_145 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_145 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-146"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_146

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_146 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_146 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-147"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_147

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_147 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_147 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-148"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_148

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_148 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_148 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-149"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_149

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_149 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_149 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-15"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_15

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_15 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_15 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-150"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_150

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_150 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_150 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-151"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_151

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_151 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_151 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-152"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_152

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_152 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_152 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-153"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_153

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_153 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_153 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-154"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_154

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_154 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_154 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-155"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_155

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_155 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_155 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-156"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_156

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_156 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_156 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-157"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_157

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_157 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_157 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-158"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_158

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_158 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_158 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-159"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_159

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_159 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_159 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-16"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_16

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_16 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_16 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-160"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_160

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_160 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_160 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-161"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_161

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_161 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_161 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-162"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_162

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_162 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_162 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-163"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_163

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_163 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_163 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-164"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_164

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_164 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_164 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-165"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_165

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_165 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_165 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-166"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_166

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_166 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_166 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-167"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_167

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_167 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_167 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-168"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_168

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_168 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_168 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-169"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_169

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_169 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_169 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-17"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_17

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_17 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_17 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-170"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_170

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_170 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_170 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-171"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_171

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_171 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_171 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-172"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_172

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_172 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_172 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-173"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_173

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_173 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_173 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-174"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_174

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_174 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_174 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-175"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_175

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_175 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_175 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-176"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_176

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_176 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_176 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-177"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_177

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_177 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_177 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-178"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_178

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_178 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_178 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-179"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_179

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_179 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_179 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-18"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_18

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_18 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_18 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-180"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_180

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_180 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_180 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-181"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_181

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_181 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_181 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-182"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_182

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_182 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_182 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-183"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_183

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_183 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_183 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-184"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_184

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_184 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_184 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-185"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_185

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_185 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_185 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-186"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_186

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_186 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_186 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-187"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_187

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_187 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_187 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-188"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_188

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_188 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_188 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-189"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_189

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_189 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_189 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-19"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_19

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_19 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_19 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-190"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_190

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_190 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_190 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-191"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_191

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_191 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_191 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-192"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_192

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_192 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_192 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-193"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_193

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_193 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_193 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-194"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_194

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_194 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_194 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-195"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_195

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_195 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_195 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-196"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_196

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_196 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_196 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-197"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_197

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_197 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_197 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-198"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_198

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_198 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_198 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-199"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_199

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_199 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_199 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-2"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_2

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_2 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_2 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-20"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_20

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_20 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_20 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-200"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_200

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_200 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_200 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-201"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_201

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_201 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_201 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-202"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_202

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_202 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_202 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-203"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_203

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_203 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_203 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-204"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_204

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_204 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_204 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-205"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_205

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_205 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_205 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-206"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_206

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_206 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_206 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-207"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_207

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_207 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_207 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-208"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_208

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_208 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_208 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-209"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_209

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_209 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_209 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-21"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_21

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_21 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_21 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-210"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_210

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_210 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_210 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-211"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_211

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_211 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_211 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-212"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_212

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_212 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_212 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-213"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_213

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_213 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_213 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-214"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_214

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_214 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_214 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-215"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_215

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_215 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_215 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-216"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_216

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_216 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_216 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-217"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_217

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_217 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_217 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-218"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_218

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_218 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_218 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-219"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_219

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_219 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_219 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-22"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_22

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_22 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_22 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-220"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_220

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_220 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_220 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-221"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_221

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_221 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_221 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-222"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_222

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_222 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_222 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-223"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_223

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_223 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_223 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-224"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_224

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_224 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_224 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-225"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_225

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_225 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_225 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-226"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_226

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_226 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_226 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-227"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_227

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_227 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_227 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-228"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_228

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_228 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_228 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-229"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_229

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_229 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_229 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-23"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_23

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_23 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_23 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-230"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_230

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_230 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_230 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-231"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_231

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_231 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_231 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-232"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_232

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_232 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_232 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-233"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_233

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_233 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_233 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-234"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_234

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_234 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_234 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-235"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_235

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_235 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_235 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-236"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_236

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_236 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_236 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-237"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_237

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_237 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_237 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-238"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_238

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_238 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_238 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-239"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_239

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_239 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_239 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-24"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_24

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_24 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_24 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-240"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_240

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_240 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_240 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-241"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_241

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_241 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_241 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-242"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_242

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_242 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_242 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-243"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_243

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_243 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_243 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-244"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_244

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_244 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_244 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-245"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_245

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_245 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_245 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-246"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_246

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_246 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_246 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-247"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_247

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_247 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_247 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-248"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_248

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_248 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_248 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-249"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_249

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_249 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_249 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-25"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_25

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_25 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_25 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-250"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_250

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_250 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_250 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-251"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_251

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_251 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_251 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-252"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_252

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_252 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_252 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-253"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_253

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_253 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_253 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-254"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_254

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_254 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_254 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-255"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_255

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_255 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_255 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-256"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_256

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_256 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_256 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-257"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_257

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_257 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_257 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-258"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_258

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_258 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_258 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-259"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_259

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_259 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_259 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-26"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_26

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_26 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_26 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-260"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_260

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_260 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_260 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-261"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_261

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_261 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_261 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-262"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_262

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_262 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_262 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-263"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_263

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_263 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_263 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-264"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_264

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_264 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_264 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-265"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_265

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_265 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_265 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-266"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_266

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_266 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_266 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-267"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_267

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_267 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_267 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-268"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_268

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_268 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_268 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-269"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_269

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_269 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_269 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-27"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_27

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_27 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_27 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-270"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_270

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_270 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_270 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-271"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_271

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_271 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_271 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-272"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_272

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_272 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_272 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-273"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_273

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_273 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_273 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-274"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_274

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_274 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_274 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-275"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_275

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_275 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_275 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-276"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_276

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_276 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_276 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-277"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_277

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_277 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_277 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-278"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_278

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_278 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_278 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-279"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_279

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_279 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_279 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-28"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_28

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_28 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_28 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-280"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_280

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_280 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_280 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-281"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_281

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_281 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_281 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-282"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_282

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_282 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_282 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-283"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_283

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_283 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_283 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-284"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_284

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_284 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_284 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-285"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_285

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_285 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_285 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-286"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_286

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_286 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_286 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-287"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_287

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_287 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_287 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-288"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_288

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_288 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_288 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-289"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_289

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_289 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_289 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-29"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_29

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_29 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_29 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-290"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_290

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_290 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_290 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-291"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_291

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_291 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_291 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-292"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_292

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_292 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_292 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-293"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_293

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_293 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_293 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-294"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_294

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_294 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_294 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-295"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_295

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_295 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_295 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-296"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_296

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_296 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_296 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-297"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_297

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_297 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_297 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-298"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_298

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_298 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_298 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-299"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_299

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_299 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_299 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-3"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_3

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_3 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_3 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-30"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_30

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_30 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_30 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-300"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_300

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_300 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_300 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-301"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_301

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_301 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_301 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-302"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_302

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_302 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_302 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-303"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_303

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_303 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_303 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-304"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_304

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_304 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_304 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-305"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_305

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_305 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_305 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-306"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_306

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_306 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_306 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-307"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_307

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_307 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_307 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-308"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_308

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_308 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_308 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-309"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_309

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_309 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_309 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-31"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_31

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_31 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_31 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-310"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_310

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_310 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_310 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-311"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_311

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_311 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_311 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-312"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_312

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_312 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_312 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-313"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_313

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_313 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_313 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-314"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_314

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_314 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_314 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-315"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_315

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_315 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_315 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-316"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_316

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_316 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_316 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-317"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_317

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_317 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_317 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-318"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_318

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_318 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_318 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-319"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_319

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_319 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_319 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-32"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_32

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_32 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_32 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-320"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_320

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_320 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_320 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-321"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_321

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_321 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_321 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-322"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_322

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_322 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_322 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-323"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_323

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_323 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_323 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-324"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_324

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_324 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_324 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-325"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_325

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_325 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_325 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-326"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_326

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_326 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_326 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-327"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_327

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_327 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_327 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-328"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_328

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_328 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_328 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-329"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_329

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_329 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_329 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-33"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_33

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_33 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_33 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-330"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_330

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_330 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_330 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-331"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_331

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_331 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_331 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-332"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_332

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_332 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_332 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-333"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_333

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_333 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_333 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-334"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_334

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_334 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_334 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-335"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_335

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_335 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_335 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-336"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_336

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_336 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_336 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-337"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_337

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_337 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_337 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-338"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_338

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_338 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_338 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-339"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_339

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_339 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_339 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-34"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_34

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_34 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_34 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-340"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_340

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_340 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_340 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-341"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_341

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_341 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_341 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-342"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_342

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_342 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_342 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-343"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_343

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_343 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_343 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-344"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_344

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_344 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_344 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-345"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_345

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_345 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_345 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-346"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_346

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_346 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_346 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-347"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_347

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_347 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_347 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-348"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_348

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_348 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_348 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-349"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_349

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_349 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_349 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-35"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_35

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_35 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_35 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-350"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_350

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_350 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_350 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-351"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_351

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_351 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_351 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-352"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_352

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_352 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_352 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-353"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_353

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_353 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_353 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-354"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_354

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_354 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_354 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-355"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_355

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_355 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_355 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-356"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_356

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_356 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_356 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-357"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_357

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_357 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_357 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-358"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_358

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_358 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_358 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-359"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_359

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_359 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_359 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-36"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_36

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_36 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_36 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-360"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_360

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_360 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_360 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-361"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_361

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_361 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_361 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-362"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_362

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_362 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_362 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-363"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_363

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_363 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_363 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-364"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_364

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_364 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_364 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-365"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_365

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_365 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_365 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-366"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_366

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_366 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_366 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-367"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_367

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_367 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_367 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-368"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_368

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_368 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_368 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-369"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_369

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_369 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_369 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-37"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_37

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_37 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_37 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-370"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_370

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_370 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_370 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-371"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_371

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_371 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_371 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-372"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_372

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_372 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_372 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-373"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_373

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_373 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_373 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-374"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_374

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_374 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_374 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-375"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_375

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_375 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_375 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-376"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_376

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_376 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_376 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-377"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_377

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_377 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_377 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-378"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_378

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_378 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_378 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-379"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_379

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_379 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_379 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-38"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_38

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_38 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_38 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-380"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_380

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_380 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_380 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-381"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_381

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_381 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_381 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-382"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_382

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_382 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_382 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-383"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_383

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_383 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_383 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-384"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_384

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_384 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_384 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-385"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_385

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_385 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_385 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-386"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_386

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_386 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_386 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-387"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_387

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_387 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_387 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-388"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_388

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_388 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_388 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-389"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_389

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_389 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_389 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-39"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_39

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_39 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_39 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-390"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_390

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_390 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_390 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-391"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_391

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_391 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_391 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-392"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_392

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_392 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_392 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-393"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_393

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_393 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_393 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-394"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_394

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_394 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_394 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-395"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_395

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_395 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_395 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-396"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_396

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_396 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_396 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-397"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_397

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_397 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_397 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-398"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_398

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_398 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_398 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-399"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_399

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_399 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_399 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-4"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_4

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_4 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_4 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-40"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_40

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_40 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_40 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-400"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_400

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_400 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_400 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-401"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_401

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_401 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_401 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-402"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_402

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_402 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_402 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-403"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_403

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_403 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_403 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-404"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_404

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_404 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_404 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-405"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_405

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_405 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_405 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-406"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_406

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_406 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_406 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-407"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_407

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_407 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_407 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-408"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_408

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_408 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_408 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-409"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_409

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_409 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_409 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-41"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_41

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_41 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_41 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-410"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_410

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_410 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_410 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-411"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_411

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_411 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_411 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-412"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_412

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_412 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_412 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-413"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_413

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_413 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_413 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-414"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_414

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_414 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_414 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-415"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_415

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_415 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_415 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-42"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_42

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_42 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_42 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-43"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_43

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_43 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_43 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-44"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_44

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_44 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_44 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-45"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_45

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_45 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_45 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-46"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_46

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_46 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_46 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-47"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_47

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_47 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_47 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-48"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_48

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_48 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_48 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-49"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_49

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_49 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_49 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-5"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_5

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_5 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_5 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-50"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_50

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_50 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_50 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-51"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_51

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_51 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_51 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-52"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_52

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_52 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_52 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-53"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_53

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_53 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_53 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-54"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_54

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_54 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_54 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-55"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_55

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_55 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_55 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-56"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_56

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_56 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_56 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-57"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_57

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_57 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_57 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-58"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_58

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_58 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_58 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-59"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_59

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_59 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_59 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-6"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_6

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_6 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_6 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-60"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_60

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_60 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_60 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-61"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_61

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_61 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_61 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-62"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_62

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_62 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_62 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-63"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_63

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_63 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_63 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-64"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_64

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_64 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_64 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-65"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_65

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_65 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_65 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-66"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_66

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_66 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_66 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-67"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_67

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_67 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_67 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-68"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_68

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_68 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_68 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-69"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_69

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_69 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_69 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-7"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_7

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_7 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_7 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-70"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_70

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_70 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_70 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-71"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_71

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_71 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_71 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-72"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_72

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_72 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_72 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-73"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_73

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_73 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_73 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-74"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_74

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_74 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_74 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-75"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_75

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_75 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_75 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-76"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_76

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_76 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_76 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-77"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_77

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_77 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_77 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-78"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_78

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_78 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_78 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-79"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_79

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_79 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_79 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-8"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_8

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_8 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_8 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-80"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_80

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_80 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_80 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-81"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_81

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_81 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_81 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-82"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_82

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_82 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_82 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-83"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_83

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_83 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_83 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-84"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_84

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_84 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_84 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-85"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_85

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_85 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_85 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-86"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_86

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_86 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_86 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-87"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_87

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_87 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_87 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-88"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_88

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_88 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_88 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-89"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_89

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_89 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_89 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-9"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_9

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_9 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_9 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-90"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_90

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_90 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_90 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-91"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_91

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_91 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_91 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-92"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_92

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_92 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_92 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-93"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_93

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_93 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_93 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-94"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_94

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_94 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_94 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-95"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_95

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MAX_FSP_ID_95 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |
| STAT_AMOUNT_FSP_ID_95 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-96"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_96

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_96 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_96 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-97"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_97

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_97 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_97 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-98"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_98

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_98 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_98 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-drag-ind-bit-mapping-fsp-id-99"></a>
### BF_DRAG_IND_BIT_MAPPING_FSP_ID_99

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT_FSP_ID_99 | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX_FSP_ID_99 | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-esp-state-struct"></a>
### BF_ESP_STATE_STRUCT

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AYC_FUNCTION_ACTIVE | 0/1 | high | unsigned char | 0x02 | - | - | - | - | Status AYC Funktion vom BSC System |
| STAT_MSR_FUNCTION_ACTIVE | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Status MSR funktion vom BSC system |
| STAT_ASR_FUNCTION_ACTIVE | 0/1 | high | unsigned char | 0x01 | - | - | - | - | ASR Funktion vom BSC System |

<a id="table-bf-fail-light-state-struct"></a>
### BF_FAIL_LIGHT_STATE_STRUCT

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MIL_STATE_ACTIVE | 0/1 | high | unsigned char | 0x1 | - | - | - | - | MIL Indication Status |

<a id="table-bf-fsp-id-0-drag-ind"></a>
### BF_FSP_ID_0_DRAG_IND

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AMOUNT | 0/1 | high | unsigned char | 0x1F | - | - | - | - | 0x248 Amount of counts of threshold |
| STAT_MAX | 0/1 | high | unsigned char | 0xE0 | - | - | - | - | 0x07 max-Value |

<a id="table-bf-hnd-brk-state-bit-struct"></a>
### BF_HND_BRK_STATE_BIT_STRUCT

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BRK_STATE_BIT0 | 0-n | high | unsigned char | 0x01 | BRK_STATE_BIT0_TABLE | - | - | - | Brems Status |
| STAT_HND_BRK_STATE_BIT1 | 0-n | high | unsigned char | 0x02 | HND_BRK_STATE_BIT1_TABLE | - | - | - | Handbremse Status |

<a id="table-bf-launch-state"></a>
### BF_LAUNCH_STATE

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LAUNCH_POSSIBLE_GENERAL | 0/1 | high | unsigned char | 0x01 | - | - | - | - | 0x01:Anfahren ist generell möglich |
| STAT_LAUNCH_POSSIBLE_CLUTCHES | 0/1 | high | unsigned char | 0x02 | - | - | - | - | 0x02: Anfahren ist möglich bei den Kupplungen |
| STAT_LAUNCH_POSSIBLE_OIL_COOLING | 0/1 | high | unsigned char | 0x04 | - | - | - | - | 0x04: Anfahren ist möglich für Ölkühlung |

<a id="table-bf-lhm1-struct"></a>
### BF_LHM1_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_8 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 8 aktiv |
| STAT_LHM_7 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 7 aktiv |
| STAT_LHM_6 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 6 aktiv |
| STAT_LHM_5 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 5 aktiv |
| STAT_LHM_4 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 4 aktiv |
| STAT_LHM_3 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 3 aktiv |
| STAT_LHM_2 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 2 aktiv |
| STAT_LHM_1 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 1 aktiv |

<a id="table-bf-lhm2-struct"></a>
### BF_LHM2_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_16 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 16 aktiv |
| STAT_LHM_15 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 15 aktiv |
| STAT_LHM_14 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 14 aktiv |
| STAT_LHM_13 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 13 aktiv |
| STAT_LHM_12 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 12 aktiv |
| STAT_LHM_11 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 11 aktiv |
| STAT_LHM_10 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 10 aktiv |
| STAT_LHM_9 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 9 aktiv |

<a id="table-bf-lhm3-struct"></a>
### BF_LHM3_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_24 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 24 aktiv |
| STAT_LHM_23 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 23 aktiv |
| STAT_LHM_22 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 22 aktiv |
| STAT_LHM_21 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 21 aktiv |
| STAT_LHM_20 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 20 aktiv |
| STAT_LHM_19 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 19 aktiv |
| STAT_LHM_18 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 18 aktiv |
| STAT_LHM_17 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 17 aktiv |

<a id="table-bf-lhm4-struct"></a>
### BF_LHM4_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_32 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 32 aktiv |
| STAT_LHM_31 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 31 aktiv |
| STAT_LHM_30 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 30 aktiv |
| STAT_LHM_29 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 29 aktiv |
| STAT_LHM_28 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 28 aktiv |
| STAT_LHM_27 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 27 aktiv |
| STAT_LHM_26 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 26 aktiv |
| STAT_LHM_25 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 25 aktiv |

<a id="table-bf-lhm5-struct"></a>
### BF_LHM5_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_40 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 40 aktiv |
| STAT_LHM_39 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 39 aktiv |
| STAT_LHM_38 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 38 aktiv |
| STAT_LHM_37 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 37 aktiv |
| STAT_LHM_36 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 36 aktiv |
| STAT_LHM_35 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 35 aktiv |
| STAT_LHM_34 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 34 aktiv |
| STAT_LHM_33 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 33 aktiv |

<a id="table-bf-lhm6-struct"></a>
### BF_LHM6_STRUCT

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_48 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 48 aktiv |
| STAT_LHM_47 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 47 aktiv |
| STAT_LHM_46 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | LHM 46 aktiv |
| STAT_LHM_45 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | LHM 45 aktiv |
| STAT_LHM_44 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | LHM 44 aktiv |
| STAT_LHM_43 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | LHM 43 aktiv |
| STAT_LHM_42 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 42 aktiv |
| STAT_LHM_41 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 41 aktiv |

<a id="table-bf-lhm7-struct"></a>
### BF_LHM7_STRUCT

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LHM_52 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | LHM 52 aktiv |
| STAT_LHM_51 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | LHM 51 aktiv |
| STAT_LHM_50 | 0/1 | high | unsigned char | 0x02 | - | - | - | - | LHM 50 aktiv |
| STAT_LHM_49 | 0/1 | high | unsigned char | 0x01 | - | - | - | - | LHM 49 aktiv |

<a id="table-bf-msa-locking-function-struct"></a>
### BF_MSA_LOCKING_FUNCTION_STRUCT

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPERATURE_MSA_BLOCKER | 0/1 | high | unsigned int | 0x2 | - | - | - | - | Abschaltverhinderer_Getriebetemperatur, Getriebetemperatur zu niedrig/zu hoch |
| STAT_CLU_PRS_MSA_BLOCKER | 0/1 | high | unsigned int | 0x3 | - | - | - | - | Abschaltverhinderer_fehlende_Druckversorgung, keine ausreichenden Druckversorgung |
| STAT_GEAR_MSA_BLOCKER | 0/1 | high | unsigned int | 0x4 | - | - | - | - | Abschaltverhinderer_Gang, Gang zu groß |
| STAT_OUTPUT_SPD_MSA_BLOCKER | 0/1 | high | unsigned int | 0x5 | - | - | - | - | Abschaltverhinderer_vnab, Ausgangsdrehzahl zu hoch |
| STAT_R_GEAR_MSA_BLOCKER | 0/1 | high | unsigned int | 0x6 | - | - | - | - | Abschaltverhinderer_PosR, R ist eingelegt |
| STAT_TRANSMISSION_FAULT_MSA_BLOCKER | 0/1 | high | unsigned int | 0xC | - | - | - | - | Abschaltverhinderer, Getriebesystemfehler |
| STAT_PASSIV_MSA_BLOCKER | 0/1 | high | unsigned int | 0xE | - | - | - | - | Abschaltverhinderer wegen passivierung MSA durch DxE |
| STAT_AGS_MSA_BLOCKER | 0/1 | high | unsigned int | 0xD | - | - | - | - | Abschaltverhinderer durch AGS |
| STAT_FROM_P_MSA_ACTIV | 0/1 | high | unsigned int | 0xA | - | - | - | - | Einschalt Aufforderer Verlassen P Position |
| STAT_R_POS_MSA_ACTIV | 0/1 | high | unsigned int | 0xB | - | - | - | - | Einschalt Aufforderer Einlegen Position R |

<a id="table-bf-sailings-tatus-struct"></a>
### BF_SAILINGS_TATUS_STRUCT

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BIT0 | 0/1 | high | unsigned long | 0x1 | - | - | - | - | Freigabesteuerung - SAS |
| STAT_BIT1 | 0/1 | high | unsigned long | 0x2 | - | - | - | - | Freigabesteuerung - DME |
| STAT_BIT2 | 0/1 | high | unsigned long | 0x4 | - | - | - | - | Init - Beschleunigungswunsch |
| STAT_BIT3 | 0/1 | high | unsigned long | 0x8 | - | - | - | - | Init - Steigung |
| STAT_BIT4 | 0/1 | high | unsigned long | 0x10 | - | - | - | - | Init - laufender Segelausstieg |
| STAT_BIT5 | 0/1 | high | unsigned long | 0x20 | - | - | - | - | Einstieg - ECO-Taster |
| STAT_BIT6 | 0/1 | high | unsigned long | 0x40 | - | - | - | - | Einstieg - Freigabesteuerung AGS |
| STAT_BIT7 | 0/1 | high | unsigned long | 0x80 | - | - | - | - | Einstieg - Position Wählhebel |
| STAT_BIT8 | 0/1 | high | unsigned long | 0x100 | - | - | - | - | Einstieg - Geschwindigkeitsbereich |
| STAT_BIT9 | 0/1 | high | unsigned long | 0x200 | - | - | - | - | :Einstieg - Gangeinschränkung |
| STAT_BIT10 | 0/1 | high | unsigned long | 0x400 | - | - | - | - | Einstieg - Verzögerungswunsch |
| STAT_BIT11 | 0/1 | high | unsigned long | 0x800 | - | - | - | - | Einstieg - Beschleunigungswunsch |
| STAT_BIT12 | 0/1 | high | unsigned long | 0x1000 | - | - | - | - | Einstieg - Querbeschleunigung |
| STAT_BIT13 | 0/1 | high | unsigned long | 0x2000 | - | - | - | - | Einstieg - DSC Fehler |
| STAT_BIT14 | 0/1 | high | unsigned long | 0x4000 | - | - | - | - | Einstieg - Getriebetemperatur |
| STAT_BIT15 | 0/1 | high | unsigned long | 0x8000 | - | - | - | - | Einstieg - Außentemperatur |
| STAT_BIT16 | 0/1 | high | unsigned long | 0x10000 | - | - | - | - | Einstieg - Gangsteuerung |
| STAT_BIT17 | 0/1 | high | unsigned long | 0x20000 | - | - | - | - | Einstieg - Drehzahlsteuerung |
| STAT_BIT18 | 0/1 | high | unsigned long | 0x40000 | - | - | - | - | Einstieg - Momentensteuerung |
| STAT_BIT19 | 0/1 | high | unsigned long | 0x80000 | - | - | - | - | Einstieg - Anhängererkennung |
| STAT_BIT20 | 0/1 | high | unsigned long | 0x100000 | - | - | - | - | Einstieg - Betriebsmodus |
| STAT_BIT21 | 0/1 | high | unsigned long | 0x200000 | - | - | - | - | Ausstieg - ECO-Taster |
| STAT_BIT22 | 0/1 | high | unsigned long | 0x400000 | - | - | - | - | Ausstieg - Freigabesteuerung AGS |
| STAT_BIT23 | 0/1 | high | unsigned long | 0x800000 | - | - | - | - | Ausstieg - Position Waehlhebel |
| STAT_BIT24 | 0/1 | high | unsigned long | 0x1000000 | - | - | - | - | Ausstieg - Geschwindigkeitsbereich |
| STAT_BIT25 | 0/1 | high | unsigned long | 0x2000000 | - | - | - | - | Ausstieg - Gangeinschraenkung |
| STAT_BIT26 | 0/1 | high | unsigned long | 0x4000000 | - | - | - | - | Ausstieg - Verzoegerungswunsch |
| STAT_BIT27 | 0/1 | high | unsigned long | 0x8000000 | - | - | - | - | Ausstieg - Beschleunigungswunsch |
| STAT_BIT28 | 0/1 | high | unsigned long | 0x10000000 | - | - | - | - | Ausstieg - Querbeschleunigung |
| STAT_BIT29 | 0/1 | high | unsigned long | 0x20000000 | - | - | - | - | Ausstieg - DSC Fehler |
| STAT_BIT30 | 0/1 | high | unsigned long | 0x40000000 | - | - | - | - | Ausstieg - Getriebetemperatur |
| STAT_BIT31 | 0/1 | high | unsigned long | 0x80000000 | - | - | - | - | Ausstieg - Diagnosesteuerung |

<a id="table-brk-state-bit0-table"></a>
### BRK_STATE_BIT0_TABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bremspedal nicht betätigt |
| 0x01 | Bremspedal betätigt |
| 0xFF | Wert ungültig |

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

<a id="table-clutch-run-in-state"></a>
### CLUTCH_RUN_IN_STATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | GREEN_CLUTCH |
| 0x02 | HALF_RUN_IN_CLUTCH |
| 0x04 | RUN_IN_CLUTCH |

<a id="table-clu-mot-cool-spd-conversion"></a>
### CLU_MOT_COOL_SPD_CONVERSION

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Gang 1 |
| 0x02 | Gang  2 |
| 0x03 | Gang 3 |
| 0x04 | Gang 4 |
| 0x05 | Gang 5 |
| 0x06 | Gang 6 |
| 0x07 | Gang 7 |
| 0x09 | Gang R |
| 0x0D | Gang N13 |
| 0x0E | Gang N35 |
| 0x0F | Gang N57 |
| 0x10 | Gang NR2 |
| 0xFFFF | Wert ungültig |
| 0x11 | Gang N24 |
| 0x12 | Gang N46 |

<a id="table-clu-prs-cntrl-shft-gear-1-tab"></a>
### CLU_PRS_CNTRL_SHFT_GEAR_1_TAB

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Gang 1 |
| 0x0D | Leerlauf 1-3 |
| 0x03 | Gang 3 |
| 0x0E | Leerlauf 3-5 |
| 0x05 | Gang 5 |
| 0x0F | Leerlauf 5-7 |
| 0x07 | Gang 7 |
| 0xFFFF | Wert ungültig |

<a id="table-dhclientstate"></a>
### DHCLIENTSTATE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | DH-Abgleichvorgang aktiv (ab Start Berechnung eigener Keyfaktor bis erfolgreiches Speichern DH-SecretKey) |
| 0x02 | E-Label == 1 |
| 0x04 | Reserviert |
| 0x08 | Reserviert |
| 0x10 | Reserviert |
| 0x20 | Reserviert |
| 0x40 | Reserviert |
| 0x80 | Reserviert |
| 0xFF | Wert ungültig |

<a id="table-ecu-device-state-table"></a>
### ECU_DEVICE_STATE_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fehler |
| 0x01 | Produktion |
| 0x02 | Entwicklung |
| 0x03 | Wiederhergestellt |
| 0xFF | Wert ungültig |

<a id="table-eep-cor-flg-table"></a>
### EEP_COR_FLG_TABLE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Daten vom letzten Zyklus geladen |
| 0x01 | Datenblock Getrag oder LuK korrupt |
| 0x02 | Datenblock Continental is korrupt |
| 0x03 | Software Version ID hat sich zum letzten Fahrzyklus geändert, Datenstruktur könnte inkompatibel sein |
| 0x04 | Daten des letzten Fahrzyklus wurden nicht gespeichert, Daten von einem früheren Fahrzyklus wurden geladen |
| 0xFF | Wert ungültig |

<a id="table-eng-crnk-ena-table"></a>
### ENG_CRNK_ENA_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Motorstart nicht erlaubt |
| 0x01 | Motorstart erlaubt, Getriebe in Position N |
| 0x03 | Signal nicht verfügbar |
| 0x02 | Motorstart erlaubt, Motor Stop erlaubt, Getriebe in Position P |
| 0xFF | Wert ungültig |

<a id="table-ews4state"></a>
### EWS4STATE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Client authentisiert |
| 0x02 | Nicht authentische Response |
| 0x04 | Reserviert |
| 0x08 | Reserviert |
| 0x10 | Reserviert |
| 0x20 | Reserviert |
| 0x40 | Reserviert |
| 0x80 | SK verriegelt |
| 0xFF | Wert ungültig |

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

<a id="table-foot-brk-state-table"></a>
### FOOT_BRK_STATE_TABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bremspedal nicht betätigt |
| 0x01 | Bremspedal betätigt |
| 0xFF | Wert ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 349 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021800 | Energiesparmode aktiv | 0 | - |
| 0x021808 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x021809 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02180A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02180B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02180C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x021829 | Softwarefehler (Sammelfehler) | 0 | - |
| 0x02FF18 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x420000 | Elektromotor Kupplung 1: Kurzschluss nach Masse | 0 | - |
| 0x420001 | Elektromotor Kupplung 1: Kurzschluss nach Plus | 0 | - |
| 0x420002 | Elektromotor Kupplung 1: Leitungsunterbrechung | 0 | - |
| 0x420004 | Elektromotor Kupplung 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x42000A | Elektromotor Kupplung 1: Geschwindigkeit überschreitet oberen Schwellenwert | 0 | - |
| 0x42000B | Elektromotor Kupplung 1: Geschwindigkeit unterschreitet unteren Schwellenwert | 0 | - |
| 0x42000F | Elektromotor Kupplung 1: Sammelfehler Funktionsweise beeinträchtigt | 0 | - |
| 0x42001A | Elektromotor Kupplung 1: falsches Tastverhältnis | 0 | - |
| 0x420100 | Elektromotor Kupplung 2: Kurzschluss nach Masse | 0 | - |
| 0x420101 | Elektromotor Kupplung 2: Kurzschluss nach Plus | 0 | - |
| 0x420102 | Elektromotor Kupplung 2: Leitungsunterbrechung | 0 | - |
| 0x420104 | Elektromotor Kupplung 2: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x42010A | Elektromotor Kupplung 2: Geschwindigkeit überschreitet oberen Schwellenwert | 0 | - |
| 0x42010B | Elektromotor Kupplung 2: Geschwindigkeit unterschreitet unteren Schwellenwert | 0 | - |
| 0x42010F | Elektromotor Kupplung 2: Sammelfehler Funktionsweise beeinträchtigt | 0 | - |
| 0x42011A | Elektromotor Kupplung 2: falsches Tastverhältnis | 0 | - |
| 0x420200 | Elektromotor Schaltwalze 1: Kurzschluss nach Masse | 0 | - |
| 0x420201 | Elektromotor Schaltwalze 1: Kurzschluss nach Plus | 0 | - |
| 0x420202 | Elektromotor Schaltwalze 1: Leitungsunterbrechung | 0 | - |
| 0x420204 | Elektromotor Schaltwalze 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x42020A | Elektromotor Schaltwalze 1: Geschwindigkeit überschreitet oberen Schwellenwert | 0 | - |
| 0x42020F | Elektromotor Schaltwalze 1: Sammelfehler Funktionsweise beeinträchtigt | 0 | - |
| 0x42021A | Elektromotor Schaltwalze 1: falsches Tastverhältnis | 0 | - |
| 0x420300 | Elektromotor Schaltwalze 2: Kurzschluss nach Masse | 0 | - |
| 0x420301 | Elektromotor Schaltwalze 2: Kurzschluss nach Plus | 0 | - |
| 0x420302 | Elektromotor Schaltwalze 2: Leitungsunterbrechung | 0 | - |
| 0x420304 | Elektromotor Schaltwalze 2: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x42030A | Elektromotor Schaltwalze 2: Geschwindigkeit überschreitet oberen Schwellenwert | 0 | - |
| 0x42030F | Elektromotor Schaltwalze 2: Sammelfehler Funktionsweise beeinträchtigt | 0 | - |
| 0x42031A | Elektromotor Schaltwalze 2: falsches Tastverhältnis | 0 | - |
| 0x420400 | Elektromotor Getriebeölkühlung: Kurzschluss nach Masse | 0 | - |
| 0x420401 | Elektromotor Getriebeölkühlung: Kurzschluss nach Plus | 0 | - |
| 0x420402 | Elektromotor Getriebeölkühlung: Leitungsunterbrechung | 0 | - |
| 0x420404 | Elektromotor Getriebeölkühlung: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x42040A | Elektromotor Getriebeölkühlung: Geschwindigkeit überschreitet oberen Schwellenwert | 0 | - |
| 0x42040B | Elektromotor Getriebeölkühlung: Geschwindigkeit unterschreitet unteren Schwellenwert | 0 | - |
| 0x42040F | Elektromotor Getriebeölkühlung: Sammelfehler Funktionsweise beeinträchtigt | 0 | - |
| 0x42041A | Elektromotor Getriebeölkühlung: Geschwindigkeit unerwartet null oder negativ | 0 | - |
| 0x42041B | Elektromotor Getriebeölkühlung: falsches Tastverhältnis | 0 | - |
| 0x420500 | Getriebeeingangsdrehzahlsensor 1: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420501 | Getriebeeingangsdrehzahlsensor 1: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x420506 | Getriebeeingangsdrehzahlsensor 1: Signal Kurzschluss nach Plus | 0 | - |
| 0x420508 | Getriebeeingangsdrehzahlsensor 1: Signal Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x42050A | Getriebeeingangsdrehzahlsensor 1: Frequenz überschreitet oberen Schwellenwert | 0 | - |
| 0x42050E | Getriebeeingangsdrehzahlsensor 1: Gradientenüberwachung | 0 | - |
| 0x42050F | Getriebeeingangsdrehzahlsensor 1: Signalmodulationsfehler | 0 | - |
| 0x420510 | Getriebeeingangsdrehzahlsensor 1: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420511 | Getriebeeingangsdrehzahlsensor 1: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x42051A | Getriebeeingangsdrehzahlsensor 1: Signalwert nicht plausibel | 0 | - |
| 0x420600 | Getriebeeingangsdrehzahlsensor 2: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420601 | Getriebeeingangsdrehzahlsensor 2: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x420606 | Getriebeeingangsdrehzahlsensor 2: Signal Kurzschluss nach Plus | 0 | - |
| 0x420608 | Getriebeeingangsdrehzahlsensor 2: Signal Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x42060A | Getriebeeingangsdrehzahlsensor 2: Frequenz überschreitet oberen Schwellenwert | 0 | - |
| 0x42060E | Getriebeeingangsdrehzahlsensor 2: Gradientenüberwachung | 0 | - |
| 0x42060F | Getriebeeingangsdrehzahlsensor 2: Signalmodulationsfehler | 0 | - |
| 0x420610 | Getriebeeingangsdrehzahlsensor 2: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420611 | Getriebeeingangsdrehzahlsensor 2: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x42061A | Getriebeeingangsdrehzahlsensor 2: Signalwert nicht plausibel | 0 | - |
| 0x420700 | Sensor Elektromotor Kupplung 1: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420701 | Sensor Elektromotor Kupplung 1: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x42070E | Sensor Elektromotor Kupplung 1: Hallsensorsignale nicht plausibel | 0 | - |
| 0x420710 | Sensor Elektromotor Kupplung 1: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420711 | Sensor Elektromotor Kupplung 1: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420720 | Sensor Elektromotor Kupplung 1: Hallsensor 1 Kurzschluss nach Masse | 0 | - |
| 0x420721 | Sensor Elektromotor Kupplung 1: Hallsensor 1 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420730 | Sensor Elektromotor Kupplung 1: Hallsensor 2 Kurzschluss nach Masse | 0 | - |
| 0x420731 | Sensor Elektromotor Kupplung 1: Hallsensor 2 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420740 | Sensor Elektromotor Kupplung 1: Hallsensor 3 Kurzschluss nach Masse | 0 | - |
| 0x420741 | Sensor Elektromotor Kupplung 1: Hallsensor 3 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420800 | Sensor Elektromotor Kupplung 2: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420801 | Sensor Elektromotor Kupplung 2: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x42080E | Sensor Elektromotor Kupplung 2: Hallsensorsignale nicht plausibel | 0 | - |
| 0x420810 | Sensor Elektromotor Kupplung 2: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420811 | Sensor Elektromotor Kupplung 2: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420820 | Sensor Elektromotor Kupplung 2: Hallsensor 1 Kurzschluss nach Masse | 0 | - |
| 0x420821 | Sensor Elektromotor Kupplung 2: Hallsensor 1 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420830 | Sensor Elektromotor Kupplung 2: Hallsensor 2 Kurzschluss nach Masse | 0 | - |
| 0x420831 | Sensor Elektromotor Kupplung 2: Hallsensor 2 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420840 | Sensor Elektromotor Kupplung 2: Hallsensor 3 Kurzschluss nach Masse | 0 | - |
| 0x420841 | Sensor Elektromotor Kupplung 2: Hallsensor 3 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420900 | Sensor Elektromotor Schaltwalze 1: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420901 | Sensor Elektromotor Schaltwalze 1: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x42090A | Sensor Elektromotor Schaltwalze 1: Pulsweitenmodulation Tastverhältnis überschreitet oberen Schwellenwert | 0 | - |
| 0x42090B | Sensor Elektromotor Schaltwalze 1: Pulsweitenmodulation Tastverhältnis unterschreitet unteren Schwellenwert | 0 | - |
| 0x42090E | Sensor Elektromotor Schaltwalze 1: Hallsensorsignale nicht plausibel | 0 | - |
| 0x42090F | Sensor Elektromotor Schaltwalze 1: Trägerfrequenz überschreitet oberen Schwellenwert | 0 | - |
| 0x420910 | Sensor Elektromotor Schaltwalze 1: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420911 | Sensor Elektromotor Schaltwalze 1: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420912 | Sensor Elektromotor Schaltwalze 1: Signal Soll/Ist Vergleich fehlgeschlagen | 0 | - |
| 0x42091A | Sensor Elektromotor Schaltwalze 1: Trägerfrequenz unterschreitet unteren Schwellenwert | 0 | - |
| 0x420920 | Sensor Elektromotor Schaltwalze 1: Hallsensor 1 Kurzschluss nach Masse | 0 | - |
| 0x420921 | Sensor Elektromotor Schaltwalze 1: Hallsensor 1 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420930 | Sensor Elektromotor Schaltwalze 1: Hallsensor 2 Kurzschluss nach Masse | 0 | - |
| 0x420931 | Sensor Elektromotor Schaltwalze 1: Hallsensor 2 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420940 | Sensor Elektromotor Schaltwalze 1: Hallsensor 3 Kurzschluss nach Masse | 0 | - |
| 0x420941 | Sensor Elektromotor Schaltwalze 1: Hallsensor 3 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420A00 | Sensor Elektromotor Schaltwalze 2: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420A01 | Sensor Elektromotor Schaltwalze 2: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x420A0A | Sensor Elektromotor Schaltwalze 2: Pulsweitenmodulation Tastverhältnis überschreitet oberen Schwellenwert | 0 | - |
| 0x420A0B | Sensor Elektromotor Schaltwalze 2: Pulsweitenmodulation Tastverhältnis unterschreitet unteren Schwellenwert | 0 | - |
| 0x420A0E | Sensor Elektromotor Schaltwalze 2: Hallsensorsignale nicht plausibel | 0 | - |
| 0x420A0F | Sensor Elektromotor Schaltwalze 2: Trägerfrequenz überschreitet oberen Schwellenwert | 0 | - |
| 0x420A10 | Sensor Elektromotor Schaltwalze 2: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420A11 | Sensor Elektromotor Schaltwalze 2: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420A12 | Sensor Elektromotor Schaltwalze 2: Signal Soll/Ist Vergleich fehlgeschlagen | 0 | - |
| 0x420A1A | Sensor Elektromotor Schaltwalze 2: Trägerfrequenz unterschreitet unteren Schwellenwert | 0 | - |
| 0x420A20 | Sensor Elektromotor Schaltwalze 2: Hallsensor 1 Kurzschluss nach Masse | 0 | - |
| 0x420A21 | Sensor Elektromotor Schaltwalze 2: Hallsensor 1 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420A30 | Sensor Elektromotor Schaltwalze 2: Hallsensor 2 Kurzschluss nach Masse | 0 | - |
| 0x420A31 | Sensor Elektromotor Schaltwalze 2: Hallsensor 2 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420A40 | Sensor Elektromotor Schaltwalze 2: Hallsensor 3 Kurzschluss nach Masse | 0 | - |
| 0x420A41 | Sensor Elektromotor Schaltwalze 2: Hallsensor 3 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420B00 | Sensor Elektromotor Getriebeölkühlung: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420B01 | Sensor Elektromotor Getriebeölkühlung: Versorgung Kurzschluss nach Plus | 0 | - |
| 0x420B0E | Sensor Elektromotor Getriebeölkühlung: Hallsensorsignale nicht plausibel | 0 | - |
| 0x420B10 | Sensor Elektromotor Getriebeölkühlung: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420B11 | Sensor Elektromotor Getriebeölkühlung: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420B20 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 1 Kurzschluss nach Masse | 0 | - |
| 0x420B21 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 1 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420B30 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 2 Kurzschluss nach Masse | 0 | - |
| 0x420B31 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 2 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420B40 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 3 Kurzschluss nach Masse | 0 | - |
| 0x420B41 | Sensor Elektromotor Getriebeölkühlung: Hallsensor 3 Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420C00 | Drucksensor 1: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420C04 | Drucksensor 1: Versorgung Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420C05 | Drucksensor 1: Signal Kurzschluss nach Masse | 0 | - |
| 0x420C09 | Drucksensor 1: Signal Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420C0A | Drucksensor 1: Signal überschreitet oberen Schwellenwert | 0 | - |
| 0x420C0B | Drucksensor 1: Signal unterschreitet unteren Schwellenwert | 0 | - |
| 0x420C0E | Drucksensor 1: hängendes Signal | 0 | - |
| 0x420C0F | Drucksensor 1: Soll/Ist Vergleich Druck überschreitet oberen Schwellenwert | 0 | - |
| 0x420C10 | Drucksensor 1: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420C11 | Drucksensor 1: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420C1A | Drucksensor 1: Soll/Ist Vergleich Druck unterschreitet unteren Schwellenwert | 0 | - |
| 0x420C1B | Drucksensor 1: Offset überschreitet Schwellenwert | 0 | - |
| 0x420C1C | Drucksensor 1: Gradient überschreitet Schwellenwert | 0 | - |
| 0x420D00 | Drucksensor 2: Versorgung Kurzschluss nach Masse | 0 | - |
| 0x420D04 | Drucksensor 2: Versorgung Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420D05 | Drucksensor 2: Signal Kurzschluss nach Masse | 0 | - |
| 0x420D09 | Drucksensor 2: Signal Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420D0A | Drucksensor 2: Signal überschreitet oberen Schwellenwert | 0 | - |
| 0x420D0B | Drucksensor 2: Signal unterschreitet unteren Schwellenwert | 0 | - |
| 0x420D0E | Drucksensor 2: hängendes Signal | 0 | - |
| 0x420D0F | Drucksensor 2: Soll/Ist Vergleich Druck überschreitet oberen Schwellenwert | 0 | - |
| 0x420D10 | Drucksensor 2: Versorgungsspannung außerhalb oberen Wertebereichs | 0 | - |
| 0x420D11 | Drucksensor 2: Versorgungsspannung außerhalb unteren Wertebereichs | 0 | - |
| 0x420D1A | Drucksensor 2: Soll/Ist Vergleich Druck unterschreitet unteren Schwellenwert | 0 | - |
| 0x420D1B | Drucksensor 2: Offset überschreitet Schwellenwert | 0 | - |
| 0x420D1C | Drucksensor 2: Gradient überschreitet Schwellenwert | 0 | - |
| 0x420E05 | Ölsumpftemperatur Sensor 1: Signal Kurzschluss nach Masse | 0 | - |
| 0x420E09 | Ölsumpftemperatur Sensor 1: Signal Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420E0D | Ölsumpftemperatur Sensor 1: Gradientenüberwachung | 0 | - |
| 0x420E0F | Ölsumpftemperatur Sensor 1: Offset | 0 | - |
| 0x420E1A | Ölsumpftemperatur Sensor 1: Hängen beim Erhitzen | 0 | - |
| 0x420E20 | Ölsumpftemperatur Sensor 1 und 2: Differenz zu groß | 0 | - |
| 0x420E25 | Ölsumpftemperatur Sensor 2: Signal Kurzschluss nach Masse | 0 | - |
| 0x420E29 | Ölsumpftemperatur Sensor 2: Signal Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x420E2D | Ölsumpftemperatur Sensor 2: Gradientenüberwachung | 0 | - |
| 0x420E2F | Ölsumpftemperatur Sensor 2: Offset | 0 | - |
| 0x420E3A | Ölsumpftemperatur Sensor 2: Hängen beim Erhitzen | 0 | - |
| 0x420F01 | Interner Temperatursensor 1: Wert nicht plausibel | 0 | - |
| 0x420F02 | Interner Temperatursensor 1: Wert hängt | 0 | - |
| 0x420F03 | Interner Temperatursensor 1: unplausibler Gradient | 0 | - |
| 0x420F0A | Interner Temperatursensor 1: Signal Spannung über Schwellenwert | 0 | - |
| 0x420F0B | Interner Temperatursensor 1: Signal Spannung unter Schwellenwert | 0 | - |
| 0x420F11 | Interner Temperatursensor 2: Wert nicht plausibel | 0 | - |
| 0x420F12 | Interner Temperatursensor 2: Wert hängt | 0 | - |
| 0x420F13 | Interner Temperatursensor 2: unplausibler Gradient | 0 | - |
| 0x420F1A | Interner Temperatursensor 2: Signal Spannung über Schwellenwert | 0 | - |
| 0x420F1B | Interner Temperatursensor 2: Signal Spannung unter Schwellenwert | 0 | - |
| 0x420F21 | Interner Temperatursensor 3: Wert nicht plausibel | 0 | - |
| 0x420F22 | Interner Temperatursensor 3: Wert hängt | 0 | - |
| 0x420F23 | Interner Temperatursensor 3: unplausibler Gradient | 0 | - |
| 0x420F2A | Interner Temperatursensor 3: Signal Spannung über Schwellenwert | 0 | - |
| 0x420F2B | Interner Temperatursensor 3: Signal Spannung unter Schwellenwert | 0 | - |
| 0x420F31 | Interner Temperatursensor 4: Wert nicht plausibel | 0 | - |
| 0x420F32 | Interner Temperatursensor 4: Wert hängt | 0 | - |
| 0x420F33 | Interner Temperatursensor 4: unplausibler Gradient | 0 | - |
| 0x420F3A | Interner Temperatursensor 4: Signal Spannung über Schwellenwert | 0 | - |
| 0x420F3B | Interner Temperatursensor 4: Signal Spannung unter Schwellenwert | 0 | - |
| 0x421000 | Kupplung 1: Moment zu niedrig | 0 | - |
| 0x421001 | Kupplung 2: Moment zu niedrig | 0 | - |
| 0x421002 | Kupplung 1: Übertemperatur | 0 | - |
| 0x421003 | Kupplung 2: Übertemperatur | 0 | - |
| 0x421004 | Kupplung 1: Schleppmoment zu hoch | 0 | - |
| 0x421005 | Kupplung 2: Schleppmoment zu hoch | 0 | - |
| 0x421006 | Kupplungsgehäuse: Schweißnahtbruch | 0 | - |
| 0x421061 | EWS: Wählhebelposition P verlassen wurde durch EWS verhindert | 1 | - |
| 0x421100 | Teilgetriebe 1: Gangspringer | 0 | - |
| 0x421101 | Teilgetriebe 2: Gangspringer | 0 | - |
| 0x421102 | Schaltwalze 1: unerwarteter Stillstand | 0 | - |
| 0x421103 | Schaltwalze 2: unerwarteter Stillstand | 0 | - |
| 0x421104 | Teilgetriebe 1: Fehler bei Synchronisierung | 0 | - |
| 0x421105 | Teilgetriebe 2: Fehler bei Synchronisierung | 0 | - |
| 0x421106 | Teilgetriebe 1: Fehler beim Auslegen des Ganges | 0 | - |
| 0x421107 | Teilgetriebe 2: Fehler beim Auslegen des Ganges | 0 | - |
| 0x421108 | Schaltwalze 1: Überwachung mechanischer Endanschlag | 0 | - |
| 0x421109 | Schaltwalze 2: Überwachung mechanischer Endanschlag | 0 | - |
| 0x42110A | Teilgetriebe 1: Fehler beim Einlegen des Ganges | 0 | - |
| 0x42110B | Teilgetriebe 2: Fehler beim Einlegen des Ganges | 0 | - |
| 0x42110D | Schaltwalze 1: Fehler beim Einlernen | 0 | - |
| 0x42110E | Schaltwalze 2: Fehler beim Einlernen | 0 | - |
| 0x42110F | Parksperre: nicht einlegbar | 0 | - |
| 0x421200 | Ölsumpf: Übertemperatur | 1 | - |
| 0x421201 | Ölsumpf und Kupplung 1/2: Temperatur überschreitet Schwellenwert 1 | 1 | - |
| 0x421202 | Ölsumpf und Kupplung 1/2: Temperatur überschreitet Schwellenwert 2 | 1 | - |
| 0x421203 | Getriebeöl: Haltbarkeit überschritten | 0 | - |
| 0x421204 | Teilgetriebe 1/2: Teach-in aufgrund von nicht beendetem Nachlauf | 1 | - |
| 0x421300 | Prozessor: Übertemperatur | 1 | - |
| 0x421301 | Endstufe Aktor Schaltwalze 1: Übertemperatur | 1 | - |
| 0x421302 | Endstufe Aktor Schaltwalze 2: Übertemperatur | 1 | - |
| 0x421303 | Endstufe Kupplungsaktuator 1: Übertemperatur | 1 | - |
| 0x421304 | Endstufe Kupplungsaktuator 2: Übertemperatur | 1 | - |
| 0x421305 | Endstufe Getriebeölkühlung Aktor 1: Übertemperatur | 1 | - |
| 0x421306 | Versorgungsspannung Logik/Sensorik: Überspannung | 1 | - |
| 0x421307 | Versorgungsspannung Logik/Sensorik: Unterspannung | 1 | - |
| 0x421308 | Versorgungsspannung Leistungsendstufe: Überspannung Schwellenwert 1 | 1 | - |
| 0x421309 | Versorgungsspannung Leistungsendstufe: Unterspannung Schwellenwert 1 | 1 | - |
| 0x42130A | Versorgungsspannung Leistungsendstufe: Überspannung Schwellenwert 2 | 1 | - |
| 0x42130B | Versorgungsspannung Leistungsendstufe: Unterspannung Schwellenwert 2 | 1 | - |
| 0x421400 | Funktionale Sicherheit: ungewollte Erhöhung Motordrehmoment | 0 | - |
| 0x421401 | Funktionale Sicherheit: ungewolltes Anfahren in falsche Richtung | 0 | - |
| 0x421402 | Funktionale Sicherheit: ungewolltes Schalten nach R während Fahrt | 0 | - |
| 0x421403 | Funktionale Sicherheit: ungewolltes Anfahren | 0 | - |
| 0x421404 | Funktionale Sicherheit: ungewolltes Runterschalten (innerhalb gültigen Bereichs Getriebeeingangsdrehzahl) | 0 | - |
| 0x421405 | Funktionale Sicherheit: ungewolltes Runterschalten (außerhalb gültigen Bereichs Getriebeeingangsdrehzahl) | 0 | - |
| 0x421406 | Funktionale Sicherheit: Aufziehen der Kupplungen | 0 | - |
| 0x421407 | Funktionale Sicherheit: zu hohe Kupplungsdrehzahl | 0 | - |
| 0x421408 | Funktionale Sicherheit: ungewolltes Auslegen von P | 0 | - |
| 0x421409 | Funktionale Sicherheit: Einlegen von P nicht möglich | 0 | - |
| 0x42140A | Funktionale Sicherheit: ungewolltes Einlegen von P | 0 | - |
| 0x42140B | Funktionale Sicherheit: im Display angezeigte Gangposition P nicht korrekt | 0 | - |
| 0x42140C | Funktionale Sicherheit: im Display angezeigte Gangposition D/R nicht korrekt | 0 | - |
| 0x42140D | Funktionale Sicherheit: im Display angezeigte Gangposition N/P nicht korrekt | 0 | - |
| 0x42140F | Funktionale Sicherheit: Ausgabe einer falschen Eingangsdrehzahl verhindern | 0 | - |
| 0x421410 | Funktionale Sicherheit: Ausgabe einer falschen Abtriebsdrehzahl verhindern | 0 | - |
| 0x421411 | Funktionale Sicherheit: Ausgabe einer falschen Getriebeübersetzung verhindern | 0 | - |
| 0x421413 | Funktionale Sicherheit: Einlegen von Position N sicherstellen | 0 | - |
| 0x421414 | Funktionale Sicherheit: Ausgabe einer Check-Control-Meldung sicherstellen | 0 | - |
| 0x421415 | Funktionale Sicherheit: Ausgabe eines falschen Drehmoments verhindern | 0 | - |
| 0x421416 | Funktionale Sicherheit: Überwachung Anfahrmoment | 0 | - |
| 0x421417 | Funktionale Sicherheit: Überwachung Speicher | 0 | - |
| 0x421418 | Funktionale Sicherheit: Überwachung Speicher Kalibrierung | 0 | - |
| 0x421419 | Funktionale Sicherheit: Basissoftware und Ebene 3 Überwachung | 0 | - |
| 0x42141A | EEPROM: Zugriffsfehler (Sammelfehler) | 0 | - |
| 0x42141B | Prozessor: Stilllegung durch Mehrfach-Resets | 0 | - |
| 0x421607 | Automatisches Einlegen der Parksperre ist deaktiviert bei Klemme 15 aus/Wechsel PWF-Zustand | 1 | - |
| 0x42160C | E-Schaltung: Parksperre trotz Bestätigung nicht eingelegt | 0 | - |
| 0x42160D | E-Schaltung: Wählhebelposition P verlassen durch Motorfreigabe verhindert | 0 | - |
| 0x421610 | Parksperre: Missbrauch | 1 | - |
| 0x421611 | Parksperre: Missbrauch bei niedriger Geschwindigkeit | 0 | - |
| 0x421613 | Parksperre: Motorstart verzögert durch Reinigungsvorgang | 0 | - |
| 0xCF0472 | LP-CAN Control Module Bus OFF | 0 | - |
| 0xCF0BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xCF1401 | Botschaft (Drehmoment Kurbelwelle 1, 0xA5) fehlt,  Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1405 | Botschaft (Drehmoment Kurbelwelle 1, 0xA5) nicht aktuell oder Prüfsumme falsch, Sender DME | 1 | - |
| 0xCF1411 | Botschaft (Drehmoment Kurbelwelle 2, 0xA6) fehlt,  Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1421 | Botschaft (Drehmoment Kurbelwelle 3, 0xA7) fehlt,  Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1425 | Botschaft (Drehmoment Kurbelwelle 3, 0xA7) nicht aktuell oder Prüfsumme falsch, Sender DME | 1 | - |
| 0xCF1431 | Botschaft (Antriebsstrang 1, 0x3FB) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1441 | Botschaft (Antriebsstrang 2, 0x3F9) fehlt, Empfänger EGS, Sender DME/DDE | 0 | - |
| 0xCF1445 | Botschaft (Daten Antriebsstrang 2, 0x3F9) nicht aktuell oder Prüfsumme falsch, Sender DME | 1 | - |
| 0xCF1451 | Botschaft (Winkel Fahrpedal, 0xD9) fehlt, Empfänger EGS, Sender DME/DDE | 0 | - |
| 0xCF1455 | Botschaft (Winkel Fahrpedal, 0xD9) nicht aktuell oder Prüfsumme falsch, Sender DME | 1 | - |
| 0xCF1461 | Botschaft (Diagnose OBD Motor, 0x397) fehlt, Sender DME/DDE | 1 | - |
| 0xCF1473 | Botschaft (Navigation System Information, 0x34E) fehlt, Empfänger EGS, Sender Kombi | 1 | - |
| 0xCF1474 | Botschaft (Status Gangwahlschalter, 0x197) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender GWS | 1 | - |
| 0xCF1481 | Botschaft (Radmoment 3, 0x145) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1484 | Botschaft (Klemmen , 0x12F) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender BDC | 1 | - |
| 0xCF1494 | Botschaft (Radmoment Antrieb 1, 0x8F) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender DME1 | 1 | - |
| 0xCF14A1 | Botschaft (Absicherung Antriebsstrang, 0x1D0) fehlt, Sender DME/DDE | 0 | - |
| 0xCF14B1 | Botschaft (Radmoment 1, 0x8F) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF14C1 | Botschaft (Status MSA, 0x30B) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF14E1 | Botschaft (Daten Antriebsstrang 4, 0x1FC) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1524 | Botschaft (Ist Bremsmoment Summe, 0xEF) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender DSC_2013 | 1 | - |
| 0xCF1551 | Botschaft (Drehmoment Kurbelwelle 4, 0xC2) fehlt,  Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1571 | Botschaft (Daten Voraussage Betriebsstrategie, 0xFE) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF1581 | Botschaft (Information Antriebsstrang, 0x138) fehlt,  Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF15B4 | Botschaft (Status Fahrzeugstillstand , 0x2ED) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender DSC_2013 | 1 | - |
| 0xCF15C1 | Botschaft (Konfiguration Stellhebel Antrieb Fahrerlebnis, 0x324) fehlt, Sender DME | 1 | - |
| 0xCF15E4 | Botschaft (Status Türsensoren Abgesichert, 0x1E1) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender BDC | 1 | - |
| 0xCF1601 | Botschaft (Ist Drehzahl Rad ungesichert, 0x254) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1611 | Botschaft (Status Stabilisierung DSC, 0x173) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1615 | Botschaft (Status Stabilisierung DSC, 0x173) nicht aktuell oder Prüfsumme falsch, Sender DSC | 1 | - |
| 0xCF1621 | Botschaft (Ist Bremsmoment Summe, 0xEF) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1631 | Botschaft (Status Fahrzeugstillstand, 0x2ED) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1644 | Botschaft (Neigung Fahrbahn, 0x163) nicht aktuell oder Prüfsumme falsch, Empfänger EGS, Sender DSC_2013 | 1 | - |
| 0xCF1704 | Botschaft (Status Gangwahlschalter, 0x197) fehlt,  Empfänger EGS, Sender GWS | 1 | - |
| 0xCF1811 | Botschaft (Neigung Fahrbahn, 0x163) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1821 | Botschaft (Längsbeschleunigung Schwerpunkt, 0x199) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1831 | Botschaft (Querbeschleunigung Schwerpunkt, 0x19A) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1841 | Botschaft (Konfiguration Schalter Fahrdynamik, 0x3A7) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1851 | Botschaft (Geschwindigkeit Fahrzeug, 0x1A1) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1861 | Botschaft (Giergeschwindigkeit Fahrzeug, 0x19F) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1871 | Botschaft (Masse/Gewicht Fahrzeug, 0x2E0) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1881 | Botschaft (Lenkwinkel Vorderachse Effektiv, 0x302) fehlt, Empfänger EGS, Sender DSC | 1 | - |
| 0xCF1901 | Botschaft (Relativzeit, 0x328) fehlt, Empfänger EGS, Sender KOMBI | 1 | - |
| 0xCF1911 | Botschaft (Außentemperatur, 0x2CA) fehlt, Sender KOMBI | 1 | - |
| 0xCF1931 | Botschaft (Kilometerstand/Reichweite, 0x330) fehlt, Empfänger EGS, Sender KOMBI | 1 | - |
| 0xCF2001 | Botschaft (Klemmen, 0x12F) fehlt, Empfänger EGS, Sender BDC | 1 | - |
| 0xCF2011 | Botschaft (Status Türsensoren Abgesichert , 0x1E1) fehlt, Empfänger EGS, Sender BDC | 1 | - |
| 0xCF2021 | Botschaft (Fahrzeugzustand, 0x3A0) fehlt, Sender ZGW; Empfänger EGS | 1 | - |
| 0xCF2051 | Botschaft (Status Kontakt Handbremse, 0x34F) fehlt,  Empfänger EGS, Sender BDC | 1 | - |
| 0xCF20D1 | Botschaft (Blinken, 0x1F6) fehlt,  Empfänger EGS, Sender BDC | 1 | - |
| 0xCF2101 | Botschaft (Bedienung Schaltpaddel, 0x207) fehlt, Empfänger EGS, Sender BDC | 1 | - |
| 0xCF2411 | Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC) fehlt, Empfänger EGS, Sender DME/DDE | 1 | - |
| 0xCF2501 | Botschaft (Status Anhänger, 0x2E4) fehlt, Empfänger EGS, Sender AAG | 1 | - |
| 0xCF2B51 | Botschaft (Status Verteilung Längsmoment Vorderachse Hinterachse, 0xE9) fehlt,  Empfänger EGS, Sender LMV_FQ | 1 | - |
| 0xCF2C01 | Signal (Drehmoment Kurbelwelle 1, 0xA5) ungültig Ist Drehzahl Motor Kurbelwelle, Sender DME | 1 | - |
| 0xCF2C02 | Signal (Ist Drehzahl Rad ungesichert, 0x254) ungültig Ist Drehzahl Rad VL, Sender DSC | 1 | - |
| 0xCF2C03 | Signal (Ist Drehzahl Rad ungesichert, 0x254) ungültig Ist Drehzahl Rad VR, Sender DSC | 1 | - |
| 0xCF2C04 | Signal (Ist Drehzahl Rad ungesichert, 0x254) ungültig Ist Drehzahl Rad HL, Sender DSC | 1 | - |
| 0xCF2C05 | Signal (Ist Drehzahl Rad ungesichert, 0x254) ungültig Ist Drehzahl Rad HR, Sender DSC | 1 | - |
| 0xCF2C06 | Signal (Status Stabilisierung DSC, 0x173) ungültig Status Bremsung Fahrer, Sender DSC | 1 | - |
| 0xCF2C07 | Signal (Status Kontakt Handbremse, 0x34F) ungültig Status Kontakt Handbremse, Sender BDC oder Signal (Status Fahrzeugstillstand Parkbremse, 0x2DC) ungültig Status Fahrzeugstillstand Parkbremse, Sender DSC | 1 | - |
| 0xCF2C08 | Signal (Daten Antriebsstrang 1, 0x3FB) ungültig Soll Drehzahl Leerlauf Antrieb, Sender DME | 1 | - |
| 0xCF2C09 | Signal (Winkel Fahrpedal, 0xD9) ungültig Ist Winkel Fahrpedal, Sender DME | 1 | - |
| 0xCF2C0A | Signal (Außentemperatur, 0x2CA) ungültig Temperatur Außen, Sender Kombi | 1 | - |
| 0xCF2C0B | Signal (Drehmoment Kurbelwelle 3, 0xA7) ungültig Ist Drehmoment Kurbelwelle Fahrerwunsch FAS, Sender DME | 1 | - |
| 0xCF2C0C | Signal (Drehmoment Kurbelwelle 2, 0xA6) ungültig Ist Drehmoment Kurbelwelle Minimal, Sender DME | 1 | - |
| 0xCF2C0D | Signal (Drehmoment Kurbelwelle 2, 0xA6) ungültig Ist Drehmoment Kurbelwelle Maximal, Sender DME | 1 | - |
| 0xCF2C0E | Signal (Daten Antriebsstrang 2, 0x3F9) ungültig Temperatur Motor Antrieb, Sender DME | 1 | - |
| 0xCF2C0F | Signal (Drehmoment Kurbelwelle 1, 0xA5) ungültig Ist Drehmoment Kurbelwelle, Sender DME | 1 | - |
| 0xCF2C10 | Signal (Klemmen , 0x12F) ungültig Status_Klemme, Sender BDC | 1 | - |
| 0xCF2C11 | Signal (Status Gangwahlschalter, 0x197) ungültig Bedienung_Gangwahlschalter, Sender GWS | 1 | - |
| 0xCF2C12 | Signal (Status Gangwahlschalter, 0x197) ungültig  Bedienung_Gangwahlschalter_Taster_Parken, Sender GWS | 1 | - |
| 0xCF2C13 | Signal (Bedienung Schaltpaddel, 0x207) ungültig Bedienung Schaltpaddel, Sender BDC | 1 | - |
| 0xCF2C14 | Signal (Status Türsensoren Abgesichert, 0x1E1) ungültig Status_Türkontakt_FAT_Abgesichert, Sender GWS | 1 | - |
| 0xCF2C16 | Signal (Ist Bremsmoment Summe, 0xEF) ungültig Ist_Bremsmoment_Summe_Fahrerwunsch, Sender DSC_2013 | 1 | - |
| 0xCF2C18 | Signal (Ist Bremsmoment Summe, 0xEF) ungültig Ist_Bremsmoment_Summe, Sender DSC_2013 | 1 | - |
| 0xCF2C1B | Signal (Drehmoment Kurbelwelle 3, 0xA7) ungültig Soll_Radmoment_Antrieb_Summe_Koordiniert, Sender DME1 | 1 | - |
| 0xCF2C1C | Signal (Status Stabilisierung DSC, 0x173) ungültig Qualifier_Funktion_ABS, Sender DSC_2013 | 1 | - |
| 0xCF2C1D | Signal (Status Stabilisierung DSC, 0x173) ungültig Qualifier_Funktion_ASC, Sender DSC_2013 | 1 | - |
| 0xCF2C1E | Signal (Status Stabilisierung DSC, 0x173) ungültig Qualifier_Funktion_FDR, Sender DSC_2013 | 1 | - |
| 0xCF2C1F | Signal (Information Antriebsstrang, 0x138) ungültig Status_Zustand_MSA_Erweitert, Sender DME1_BK | 1 | - |
| 0xCF2C20 | Signal (Status Motor Start Auto, 0x30B) ungültig Status_Verfügbarkeit_Segeln_DME, Sender DME1 | 1 | - |
| 0xCF2C22 | Signal (Neigung Fahrbahn, 0x163) ungültig Ist_Längsneigung_Fahrbahn, Sender DSC_2013 | 1 | - |
| 0xCF2C23 | Signal (Drehmoment Kurbelwelle 1, 0xA5) ungültig Ist Drehmoment Kurbelwelle DMEE, Sender DME | 1 | - |
| 0xCF2C24 | Signal (Konfiguration Stellhebel Antrieb Fahrerlebnis, 0x324) ungültig Status Verhinderung Gangwahl, Sender DME | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 238 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | motor_x_absolut_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4001 | sd_motor_1_relative_postion | HEX | High | unsigned long | - | - | - | - |
| 0x4002 | sd_motor_1_speed | 1/min | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4003 | sd_motor_1_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4004 | sd_motor_1_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4010 | sd_motor_2_absolut_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4011 | sd_motor_2_relative_postion | HEX | High | unsigned long | - | - | - | - |
| 0x4012 | sd_motor_2_speed | 1/min | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4013 | sd_motor_2_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4014 | sd_motor_2_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4020 | clu_motor_1_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4021 | clu_motor_1_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4022 | clu_motor_1_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4030 | clu_motor_2_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4031 | clu_motor_2_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4032 | clu_motor_2_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4040 | clu_motor_cool_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4041 | clu_motor_cool_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4042 | clu_motor_cool_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4050 | prs_sens_clu_1_sig | - | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4051 | prs_sens_clu_1_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4060 | prs_sens_clu_2_sig | - | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4061 | prs_sens_clu_2_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4070 | spd_sens_iss_1_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4071 | spd_sens_iss_1_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4080 | spd_sens_iss_2_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4081 | spd_sens_iss_2_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40A0 | temp_sens_sig | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x40A1 | temp_sens_sup_volt | °C | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40B0 | high_pow_volt | V | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x40B1 | low_pow_volt | V | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x40C0 | shft_lev_pos | 0-n | High | 0xFF | TAB_DEZ_VALUES | - | - | - |
| 0x40C1 | shft_lev_dspl_val | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40D0 | pad_up_shft_sig_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40D1 | pad_down_shft_sig_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40D2 | foot_brk_state | 0/1 | High | 0x01 | - | - | - | - |
| 0x40D3 | back_light_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40F1 | eng_tq_static | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x40F2 | eng_tq_exp | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x40F3 | eng_tq_off_est | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x40F4 | cc_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40F5 | ped_pos | % | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x40F6 | hnd_brk_state | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x40FA | eng_crnk_ena | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40FB | ped_pos_raw | % | High | unsigned int | - | 1.0 | 40.0 | 0.0 |
| 0x40FC | whl_spd_fr | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FD | whl_spd_fl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FE | whl_spd_rr | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FF | whl_spd_rl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4101 | esp_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4102 | veh_vel_can | km/h | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x4103 | und_axle_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4104 | ous_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4111 | gear_engage_err_cnt_r | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4112 | gear_engage_err_cnt_1 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4113 | gear_engage_err_cnt_2 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4114 | gear_engage_err_cnt_3 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4115 | gear_engage_err_cnt_4 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4116 | gear_engage_err_cnt_5 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4117 | gear_engage_err_cnt_6 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4118 | gear_engage_err_cnt_7 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4131 | eep_cor_flg | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4132 | dist_lst_limp_home | km | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4133 | dc_lst_limp_home | 0-n | High | 0xFFFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4134 | fail_lght_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4135 | gear_info | 0-n | High | 0xFFFF | GEAR_INFO | - | - | - |
| 0x4139 | ped_pos_rate | %/s | High | signed char | - | 10.0 | 1.0 | 0.0 |
| 0x413A | veh_acc | g | High | signed int | - | 1.0 | 1024.0 | 0.0 |
| 0x413C | rc_strt_odo | TEXT | High | 40 | - | 1.0 | 1.0 | 0.0 |
| 0x4141 | mech_data | TEXT | High | 33 | - | 1.0 | 1.0 | 0.0 |
| 0x4142 | tsl_gear_cnt | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4143 | tsl_clu_cnt | TEXT | High | 40 | - | 1.0 | 1.0 | 0.0 |
| 0x4144 | gear_dat_part_1 | TEXT | High | 23 | - | 1.0 | 1.0 | 0.0 |
| 0x4145 | gear_dat_part_2 | TEXT | High | 21 | - | 1.0 | 1.0 | 0.0 |
| 0x4146 | gear_dat_part_3 | TEXT | High | 10 | - | 1.0 | 1.0 | 0.0 |
| 0x4147 | trnms_dat | TEXT | High | 16 | - | 1.0 | 1.0 | 0.0 |
| 0x4148 | l2s_cnt_dat | TEXT | High | 32 | - | 1.0 | 1.0 | 0.0 |
| 0x4149 | iss_data | TEXT | High | 2 | - | 1.0 | 1.0 | 0.0 |
| 0x4201 | err_storage_dis | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4205 | tcu_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4210 | auto_p_inh | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4211 | cur_gear | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4212 | BIOS_buffer | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4213 | AVL_TORQ_CRSH_DVCH_DRS | Nm | High | unsigned int | - | 1.0 | 2.0 | -1023.5 |
| 0x4214 | AVL_TORQ_CRSH_DMEE | Nm | High | unsigned int | - | 1.0 | 2.0 | -1023.5 |
| 0x4215 | clu_motor_1_pwm_duty_des | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4216 | clu_1_friction_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4217 | clu_2_friction_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4218 | clu_1_prot_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4219 | clu_2_prot_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x421A | clu_1_pwr_intake | W | High | signed int | - | 16.0 | 1.0 | 0.0 |
| 0x421B | clu_2_pwr_intake | W | High | signed int | - | 16.0 | 1.0 | 0.0 |
| 0x421C | clu_1_est_tq_pos | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421D | clu_2_est_tq_pos | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421E | clu_1_est_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421F | clu_2_est_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4220 | clu_motor_cool_des_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4221 | clu_1_des_tq_drm | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4222 | clu_2_des_tq_drm | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4223 | drm_info_state | 0-n | High | 0xFF | TAB_DRM_INFO_STATE | - | - | - |
| 0x4224 | dtd_wrn_flg | 0/1 | High | 0x01 | - | - | - | - |
| 0x4225 | eep_block_d_valid | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4226 | ffd_buffer_fom | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4227 | ffd_buffer_gti | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4228 | ffd_buffer_psc_1 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4229 | ffd_buffer_psc_2 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422A | ffd_buffer_sdl_1 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422B | ffd_buffer_sdl_2 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422C | gbm_parklock_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x422D | l2s_ffd_errlog_info | TEXT | High | 10 | - | 1.0 | 1.0 | 0.0 |
| 0x422E | pac_clu_1_prs_des | bar | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x422F | pac_clu_2_prs_des | bar | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4230 | spd_sens_iss_1_sig_raw | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4231 | spd_sens_iss_2_sig_raw | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4232 | sd_motor_2_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4233 | engine_spd_CAN | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4234 | engine_spd_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4235 | sds_iss_1_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4236 | sds_iss_2_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4237 | sds_iss_1_sig_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4238 | sds_iss_2_sig_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4239 | sds_parklock_pos | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x423A | temp_sens_sig_high | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x423B | temp_sens_sig_high_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x423C | d_axle_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x423D | eng_msa_status_can | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x423E | abs_state | 0/1 | High | 0x01 | - | - | - | - |
| 0x423F | air_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4240 | foot_brk_fault | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4241 | foot_brk_prs | bar | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x4242 | ca_bus_error_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4243 | clu_motor_cool_stress | % | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4244 | clu_motor_cool_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x4245 | clu_motor_1_pwm_duty | % | High | signed int | - | 100.0 | 32768.0 | 0.0 |
| 0x4246 | clu_motor_2_pwm_duty | % | High | signed int | - | 100.0 | 32768.0 | 0.0 |
| 0x4247 | engine_idle_spd_CAN | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4248 | engine_spd_CAN_status | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4249 | engine_status | 0-n | High | 0xFF | TAB_ENG_STATE | - | - | - |
| 0x424A | engine_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x424B | engine_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x424C | eng_tq_des | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424D | eng_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424E | eng_tq_min | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424F | eng_tq_static_status | Nm | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4250 | sd_motor_1_voltage_hall | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4251 | sd_motor_2_voltage_hall | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4252 | spd_sens_iss_1_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4253 | spd_sens_iss_2_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4254 | ped_pos_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4255 | sd_motor_1_amp_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4256 | sd_motor_2_amp_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4257 | sd_motor_1_remain_shift_cnt | HEX | High | unsigned char | - | - | - | - |
| 0x4258 | sd_motor_2_remain_shift_cnt | HEX | High | unsigned char | - | - | - | - |
| 0x4259 | sd_motor_1_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x425A | sd_motor_2_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x425B | sd_motor_1_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425C | sd_motor_2_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425D | sd_motor_1_corr_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425E | sd_motor_2_corr_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425F | sd_motor_1_orh | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4260 | sd_motor_2_orh | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4261 | sd_motor_1_orl | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4262 | sd_motor_2_orl | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4263 | sd_motor_1_sensor_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4264 | sd_motor_2_sensor_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4265 | pad_up_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4266 | pad_down_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4267 | lev_up_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4268 | lev_down_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4269 | temp_sens_sig_raw | °C | High | unsigned int | - | 5.0 | 4096.0 | 0.0 |
| 0x426A | vbi_time_abs | HEX | High | unsigned long | - | - | - | - |
| 0x426B | vbi_timeout_err | HEX | High | unsigned long | - | - | - | - |
| 0x426C | whl_spd_fr_status | HEX | High | unsigned char | - | - | - | - |
| 0x426D | whl_spd_fl_status | HEX | High | unsigned char | - | - | - | - |
| 0x426E | whl_spd_rr_status | HEX | High | unsigned char | - | - | - | - |
| 0x426F | whl_spd_rl_status | HEX | High | unsigned char | - | - | - | - |
| 0x4270 | clu_motor_1_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4271 | clu_motor_2_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4272 | clu_motor_cool_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4273 | clu_motor_2_pwm_duty_des | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4274 | std_data | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4275 | prnd_phys | 0-n | High | 0xFF | TAB_PHYS_PRND | - | - | - |
| 0x4276 | prnd_driver_choice | 0-n | High | 0xFF | TAB_PHYS_PRND | - | - | - |
| 0x4277 | sft_lck_status_received | 0-n | High | 0xFF | TAB_SHFTLCK_STATE | - | - | - |
| 0x4278 | dri_prndl_position_enable | 0-n | High | 0xFF | TAB_PRDNL_POS_ENA | - | - | - |
| 0x4279 | IMO_AUTH_COND | 0/1 | High | 0x01 | - | - | - | - |
| 0x427A | IMO_SECRET_NUMBER | 0-n | High | 0xFF | TAB_SECRET_NUMBER | - | - | - |
| 0x427B | IMO_SECRET_KEY | 0-n | High | 0xFF | TAB_SECRET_KEY | - | - | - |
| 0x427C | IMO_KEY_CONDITION | 0-n | High | 0xFF | TAB_IMO_KEY_COND | - | - | - |
| 0x427D | WUP_STATE | 0/1 | High | 0x01 | - | - | - | - |
| 0x427E | IMO_RESPONSE_TIMEOUT | HEX | High | unsigned char | - | - | - | - |
| 0x427F | IMO_SERVER_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4280 | IMO_CLIENT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4281 | TCU_SLEEP_INDICATION | 0/1 | High | 0x01 | - | - | - | - |
| 0x4282 | IMO_CHALLENGE_TIMEOUT | HEX | High | unsigned char | - | - | - | - |
| 0x4283 | VEH_ODO | km | High | signed long | - | 1.0 | 100.0 | 0.0 |
| 0x4284 | RESET_CAUSE | HEX | High | unsigned char | - | - | - | - |
| 0x4285 | POWERSTAGE_A_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4286 | POWERSTAGE_B_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4287 | POWERSTAGE_C_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4288 | POWERSTAGE_D_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4289 | POWERSTAGE_E_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x428A | temp_sens_2_sig | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x428B | temp_sens_2_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x428C | Geh_regbuff_sp[current] | HEX | High | unsigned long | - | - | - | - |
| 0x428D | Geh_regbuff_vec[current] | HEX | High | unsigned int | - | - | - | - |
| 0x428E | Geh_regbuff_pc[current] | HEX | High | unsigned long | - | - | - | - |
| 0x428F | Geh_regbuff_par1[current] | HEX | High | unsigned long | - | - | - | - |
| 0x4290 | Geh_regbuff_cnt[current] | HEX | High | unsigned int | - | - | - | - |
| 0x4291 | Geh_regbuff_stck[current] | HEX | High | unsigned long | - | - | - | - |
| 0x4292 | TEMP_SENS_1_STATIONARY_STATE | HEX | - | unsigned char | - | - | - | - |
| 0x4293 | TEMP_SENS_2_STATIONARY_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4294 | FKT_EWS | HEX | High | unsigned int | - | - | - | - |
| 0x4295 | E6KEY_HASH | HEX | High | unsigned char | - | - | - | - |
| 0x4296 | IN_SPD_COUNTS | HEX | - | unsigned int | - | - | - | - |
| 0x4297 | ROAD_SLOPE | % | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4298 | START_STOP_BUTTON | HEX | - | unsigned char | - | - | - | - |
| 0x4299 | SHUTDOWN_DURATION | HEX | High | unsigned long | - | - | - | - |
| 0x429A | ENGINE_TEMP_SHUTDOWN | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429B | GEARBOX_TEMP_SHUTDOWN | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x429C | SUMP_OIL_TEMP_EST_BY_COOLANT | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429D | SUMP_OIL_TEMP_EST_BY_TIME | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429E | SHDR1_ANGL_LV2 | °C | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x429F | SHDR2_ANGL_LV2 | °C | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x42A0 | SHDR2_EEPROM_BLOCK_STATUS | 0-n | High | 0xFF | TAB_EEPROM_STATUS | - | - | - |
| 0x42A1 | SHDR1_2_SHDR_SHIFT_FLAG | HEX | High | unsigned int | - | - | - | - |
| 0xF402 | DTC that caused required freeze frame data storage | HEX | High | unsigned int | - | - | - | - |
| 0xF404 | Calculated LOAD Value | - | High | unsigned char | - | 100.0 | 255.0 | 0.0 |
| 0xF405 | Engine Coolant Temperature | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0xF40C | Engine RPM | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0xF40D | Vehicle Speed Sensor | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xF411 | Absolute Throttle Position | % | High | unsigned char | - | 100.0 | 255.0 | 0.0 |
| 0xF442 | Control module voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-gear-info"></a>
### GEAR_INFO

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | GEN_GEAR_1 |
| 0x02 | GEN_GEAR_2 |
| 0x03 | GEN_GEAR_3 |
| 0x04 | GEN_GEAR_4 |
| 0x05 | GEN_GEAR_5 |
| 0x06 | GEN_GEAR_6 |
| 0x07 | GEN_GEAR_7 |
| 0x08 | GEN_GEAR_8 |
| 0x09 | GEN_GEAR_REVERSE |
| 0x0A | GEN_GEAR_UNDEFINED |
| 0x0B | GEN_GEAR_UNDEFINED |
| 0x0C | GEN_GEAR_UNDEFINED |
| 0x0D | GEN_GEAR_N_13 |
| 0x0E | GEN_GEAR_N_35 |
| 0x0F | GEN_GEAR_N_57 |
| 0x10 | GEN_GEAR_N_R2 |
| 0x11 | GEN_GEAR_N_24 |
| 0x12 | GEN_GEAR_N_46 |
| 0x13 | GEN_GEAR_N_68 |
| 0xFFFF | Wert ungültig |

<a id="table-hnd-brk-state-bit1-table"></a>
### HND_BRK_STATE_BIT1_TABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | Handbremse aktiv |
| 0x00 | Handbremse nicht aktiv |
| 0xFF | Wert ungültig |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 16 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x421062 | EWS: Manipulationsversuch | 1 | - |
| 0x421600 | E-Schaltung: elektrische Getriebenotentriegelung aktiviert | 1 | - |
| 0x421601 | E-Schaltung: Infozähler für automatisches Einlegen von P bei angezogener Handbremse | 1 | - |
| 0x421602 | E-Schaltung: Automatisches Einlegen von N durch erkannten Gegenbremsbetrieb | 1 | - |
| 0x421603 | E-Schaltung: PWF-Wechsel in N | 1 | - |
| 0x421604 | E-Schaltung: Auto-N PWF-Wechsel in D/R/N | 1 | - |
| 0x421605 | E-Schaltung: Infozähler für automatisches Einlegen von P bei Fahrzeugverlassen | 1 | - |
| 0x421606 | E-Schaltung: Infozähler für Gurtdummy und unbekannter Fahreranwesenheit | 1 | - |
| 0x421609 | E-Schaltung: Infozähler für Hilferuf von DSC oder EMF in Getriebeposition R/D oder N | 1 | - |
| 0x42160A | E-Schaltung: Zielfahrstufe nicht erreicht | 0 | - |
| 0x42160B | E-Schaltung: PMA Abbruch durch Signal Fehler | 0 | - |
| 0x42160E | E-Schaltung: Batterieloser Betrieb erkannt beim Beenden der Fahrbereitschaft | 1 | - |
| 0x421612 | Parksperre: Reinigungsvorgang aktiviert | 0 | - |
| 0x421614 | Signal (Information Anstriebsstrang, 0x312) Anforderung Ersatz Reaktion Getriebe hat den Wert: Stillstandssicherung_bei_FB_aus, Sender DME | 0 | - |
| 0xCF1591 | Botschaft (Daten EWS 4, 0x413) fehlt, Sender DME | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 238 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | motor_x_absolut_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4001 | sd_motor_1_relative_postion | HEX | High | unsigned long | - | - | - | - |
| 0x4002 | sd_motor_1_speed | 1/min | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4003 | sd_motor_1_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4004 | sd_motor_1_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4010 | sd_motor_2_absolut_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4011 | sd_motor_2_relative_postion | HEX | High | unsigned long | - | - | - | - |
| 0x4012 | sd_motor_2_speed | 1/min | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x4013 | sd_motor_2_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4014 | sd_motor_2_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4020 | clu_motor_1_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4021 | clu_motor_1_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4022 | clu_motor_1_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4030 | clu_motor_2_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4031 | clu_motor_2_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4032 | clu_motor_2_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4040 | clu_motor_cool_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4041 | clu_motor_cool_current | A | High | unsigned int | - | 1.0 | 128.0 | 0.0 |
| 0x4042 | clu_motor_cool_voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4050 | prs_sens_clu_1_sig | - | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4051 | prs_sens_clu_1_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4060 | prs_sens_clu_2_sig | - | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4061 | prs_sens_clu_2_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4070 | spd_sens_iss_1_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4071 | spd_sens_iss_1_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4080 | spd_sens_iss_2_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4081 | spd_sens_iss_2_sup_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40A0 | temp_sens_sig | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x40A1 | temp_sens_sup_volt | °C | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40B0 | high_pow_volt | V | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x40B1 | low_pow_volt | V | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x40C0 | shft_lev_pos | 0-n | High | 0xFF | TAB_DEZ_VALUES | - | - | - |
| 0x40C1 | shft_lev_dspl_val | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40D0 | pad_up_shft_sig_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40D1 | pad_down_shft_sig_volt | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x40D2 | foot_brk_state | 0/1 | High | 0x01 | - | - | - | - |
| 0x40D3 | back_light_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40F1 | eng_tq_static | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x40F2 | eng_tq_exp | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x40F3 | eng_tq_off_est | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x40F4 | cc_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40F5 | ped_pos | % | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x40F6 | hnd_brk_state | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x40FA | eng_crnk_ena | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x40FB | ped_pos_raw | % | High | unsigned int | - | 1.0 | 40.0 | 0.0 |
| 0x40FC | whl_spd_fr | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FD | whl_spd_fl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FE | whl_spd_rr | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x40FF | whl_spd_rl | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4101 | esp_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4102 | veh_vel_can | km/h | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x4103 | und_axle_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4104 | ous_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4111 | gear_engage_err_cnt_r | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4112 | gear_engage_err_cnt_1 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4113 | gear_engage_err_cnt_2 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4114 | gear_engage_err_cnt_3 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4115 | gear_engage_err_cnt_4 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4116 | gear_engage_err_cnt_5 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4117 | gear_engage_err_cnt_6 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4118 | gear_engage_err_cnt_7 | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4131 | eep_cor_flg | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4132 | dist_lst_limp_home | km | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4133 | dc_lst_limp_home | 0-n | High | 0xFFFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4134 | fail_lght_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4135 | gear_info | 0-n | High | 0xFFFF | GEAR_INFO | - | - | - |
| 0x4139 | ped_pos_rate | %/s | High | signed char | - | 10.0 | 1.0 | 0.0 |
| 0x413A | veh_acc | g | High | signed int | - | 1.0 | 1024.0 | 0.0 |
| 0x413C | rc_strt_odo | TEXT | High | 40 | - | 1.0 | 1.0 | 0.0 |
| 0x4141 | mech_data | TEXT | High | 33 | - | 1.0 | 1.0 | 0.0 |
| 0x4142 | tsl_gear_cnt | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4143 | tsl_clu_cnt | TEXT | High | 40 | - | 1.0 | 1.0 | 0.0 |
| 0x4144 | gear_dat_part_1 | TEXT | High | 23 | - | 1.0 | 1.0 | 0.0 |
| 0x4145 | gear_dat_part_2 | TEXT | High | 21 | - | 1.0 | 1.0 | 0.0 |
| 0x4146 | gear_dat_part_3 | TEXT | High | 10 | - | 1.0 | 1.0 | 0.0 |
| 0x4147 | trnms_dat | TEXT | High | 16 | - | 1.0 | 1.0 | 0.0 |
| 0x4148 | l2s_cnt_dat | TEXT | High | 32 | - | 1.0 | 1.0 | 0.0 |
| 0x4149 | iss_data | TEXT | High | 2 | - | 1.0 | 1.0 | 0.0 |
| 0x4201 | err_storage_dis | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4205 | tcu_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4210 | auto_p_inh | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4211 | cur_gear | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4212 | BIOS_buffer | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4213 | AVL_TORQ_CRSH_DVCH_DRS | Nm | High | unsigned int | - | 1.0 | 2.0 | -1023.5 |
| 0x4214 | AVL_TORQ_CRSH_DMEE | Nm | High | unsigned int | - | 1.0 | 2.0 | -1023.5 |
| 0x4215 | clu_motor_1_pwm_duty_des | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4216 | clu_1_friction_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4217 | clu_2_friction_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4218 | clu_1_prot_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4219 | clu_2_prot_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x421A | clu_1_pwr_intake | W | High | signed int | - | 16.0 | 1.0 | 0.0 |
| 0x421B | clu_2_pwr_intake | W | High | signed int | - | 16.0 | 1.0 | 0.0 |
| 0x421C | clu_1_est_tq_pos | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421D | clu_2_est_tq_pos | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421E | clu_1_est_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x421F | clu_2_est_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4220 | clu_motor_cool_des_speed | 1/min | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4221 | clu_1_des_tq_drm | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4222 | clu_2_des_tq_drm | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x4223 | drm_info_state | 0-n | High | 0xFF | TAB_DRM_INFO_STATE | - | - | - |
| 0x4224 | dtd_wrn_flg | 0/1 | High | 0x01 | - | - | - | - |
| 0x4225 | eep_block_d_valid | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4226 | ffd_buffer_fom | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4227 | ffd_buffer_gti | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4228 | ffd_buffer_psc_1 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4229 | ffd_buffer_psc_2 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422A | ffd_buffer_sdl_1 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422B | ffd_buffer_sdl_2 | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x422C | gbm_parklock_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x422D | l2s_ffd_errlog_info | TEXT | High | 10 | - | 1.0 | 1.0 | 0.0 |
| 0x422E | pac_clu_1_prs_des | bar | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x422F | pac_clu_2_prs_des | bar | High | signed int | - | 1.0 | 512.0 | 0.0 |
| 0x4230 | spd_sens_iss_1_sig_raw | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4231 | spd_sens_iss_2_sig_raw | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4232 | sd_motor_2_postion | Nm | High | signed int | - | 1.0 | 16.0 | 0.0 |
| 0x4233 | engine_spd_CAN | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4234 | engine_spd_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4235 | sds_iss_1_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4236 | sds_iss_2_sig | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4237 | sds_iss_1_sig_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4238 | sds_iss_2_sig_rate | 1/s | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x4239 | sds_parklock_pos | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x423A | temp_sens_sig_high | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x423B | temp_sens_sig_high_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x423C | d_axle_spd | 1/min | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x423D | eng_msa_status_can | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x423E | abs_state | 0/1 | High | 0x01 | - | - | - | - |
| 0x423F | air_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x4240 | foot_brk_fault | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4241 | foot_brk_prs | bar | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x4242 | ca_bus_error_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4243 | clu_motor_cool_stress | % | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4244 | clu_motor_cool_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x4245 | clu_motor_1_pwm_duty | % | High | signed int | - | 100.0 | 32768.0 | 0.0 |
| 0x4246 | clu_motor_2_pwm_duty | % | High | signed int | - | 100.0 | 32768.0 | 0.0 |
| 0x4247 | engine_idle_spd_CAN | 1/min | High | signed int | - | 1.0 | 2.0 | 0.0 |
| 0x4248 | engine_spd_CAN_status | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4249 | engine_status | 0-n | High | 0xFF | TAB_ENG_STATE | - | - | - |
| 0x424A | engine_temp | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x424B | engine_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x424C | eng_tq_des | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424D | eng_tq_max | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424E | eng_tq_min | Nm | High | signed int | - | 1.0 | 8.0 | 0.0 |
| 0x424F | eng_tq_static_status | Nm | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4250 | sd_motor_1_voltage_hall | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4251 | sd_motor_2_voltage_hall | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x4252 | spd_sens_iss_1_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4253 | spd_sens_iss_2_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4254 | ped_pos_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4255 | sd_motor_1_amp_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4256 | sd_motor_2_amp_temp_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4257 | sd_motor_1_remain_shift_cnt | HEX | High | unsigned char | - | - | - | - |
| 0x4258 | sd_motor_2_remain_shift_cnt | HEX | High | unsigned char | - | - | - | - |
| 0x4259 | sd_motor_1_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x425A | sd_motor_2_disa | 0/1 | High | 0x01 | - | - | - | - |
| 0x425B | sd_motor_1_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425C | sd_motor_2_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425D | sd_motor_1_corr_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425E | sd_motor_2_corr_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x425F | sd_motor_1_orh | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4260 | sd_motor_2_orh | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4261 | sd_motor_1_orl | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4262 | sd_motor_2_orl | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4263 | sd_motor_1_sensor_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4264 | sd_motor_2_sensor_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x4265 | pad_up_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4266 | pad_down_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4267 | lev_up_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4268 | lev_down_shft_sig_state | 0-n | High | 0xFF | TAB_DEZ_VALUES | 1.0 | 1.0 | 0.0 |
| 0x4269 | temp_sens_sig_raw | °C | High | unsigned int | - | 5.0 | 4096.0 | 0.0 |
| 0x426A | vbi_time_abs | HEX | High | unsigned long | - | - | - | - |
| 0x426B | vbi_timeout_err | HEX | High | unsigned long | - | - | - | - |
| 0x426C | whl_spd_fr_status | HEX | High | unsigned char | - | - | - | - |
| 0x426D | whl_spd_fl_status | HEX | High | unsigned char | - | - | - | - |
| 0x426E | whl_spd_rr_status | HEX | High | unsigned char | - | - | - | - |
| 0x426F | whl_spd_rl_status | HEX | High | unsigned char | - | - | - | - |
| 0x4270 | clu_motor_1_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4271 | clu_motor_2_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4272 | clu_motor_cool_pwm_duty_des_out | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4273 | clu_motor_2_pwm_duty_des | % | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4274 | std_data | TEXT | High | 20 | - | 1.0 | 1.0 | 0.0 |
| 0x4275 | prnd_phys | 0-n | High | 0xFF | TAB_PHYS_PRND | - | - | - |
| 0x4276 | prnd_driver_choice | 0-n | High | 0xFF | TAB_PHYS_PRND | - | - | - |
| 0x4277 | sft_lck_status_received | 0-n | High | 0xFF | TAB_SHFTLCK_STATE | - | - | - |
| 0x4278 | dri_prndl_position_enable | 0-n | High | 0xFF | TAB_PRDNL_POS_ENA | - | - | - |
| 0x4279 | IMO_AUTH_COND | 0/1 | High | 0x01 | - | - | - | - |
| 0x427A | IMO_SECRET_NUMBER | 0-n | High | 0xFF | TAB_SECRET_NUMBER | - | - | - |
| 0x427B | IMO_SECRET_KEY | 0-n | High | 0xFF | TAB_SECRET_KEY | - | - | - |
| 0x427C | IMO_KEY_CONDITION | 0-n | High | 0xFF | TAB_IMO_KEY_COND | - | - | - |
| 0x427D | WUP_STATE | 0/1 | High | 0x01 | - | - | - | - |
| 0x427E | IMO_RESPONSE_TIMEOUT | HEX | High | unsigned char | - | - | - | - |
| 0x427F | IMO_SERVER_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4280 | IMO_CLIENT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4281 | TCU_SLEEP_INDICATION | 0/1 | High | 0x01 | - | - | - | - |
| 0x4282 | IMO_CHALLENGE_TIMEOUT | HEX | High | unsigned char | - | - | - | - |
| 0x4283 | VEH_ODO | km | High | signed long | - | 1.0 | 100.0 | 0.0 |
| 0x4284 | RESET_CAUSE | HEX | High | unsigned char | - | - | - | - |
| 0x4285 | POWERSTAGE_A_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4286 | POWERSTAGE_B_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4287 | POWERSTAGE_C_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4288 | POWERSTAGE_D_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4289 | POWERSTAGE_E_IPT_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x428A | temp_sens_2_sig | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x428B | temp_sens_2_sig_status | 0-n | High | 0xFF | TAB_GEN_STATUS | - | - | - |
| 0x428C | Geh_regbuff_sp[current] | HEX | High | unsigned long | - | - | - | - |
| 0x428D | Geh_regbuff_vec[current] | HEX | High | unsigned int | - | - | - | - |
| 0x428E | Geh_regbuff_pc[current] | HEX | High | unsigned long | - | - | - | - |
| 0x428F | Geh_regbuff_par1[current] | HEX | High | unsigned long | - | - | - | - |
| 0x4290 | Geh_regbuff_cnt[current] | HEX | High | unsigned int | - | - | - | - |
| 0x4291 | Geh_regbuff_stck[current] | HEX | High | unsigned long | - | - | - | - |
| 0x4292 | TEMP_SENS_1_STATIONARY_STATE | HEX | - | unsigned char | - | - | - | - |
| 0x4293 | TEMP_SENS_2_STATIONARY_STATE | HEX | High | unsigned char | - | - | - | - |
| 0x4294 | FKT_EWS | HEX | High | unsigned int | - | - | - | - |
| 0x4295 | E6KEY_HASH | HEX | High | unsigned char | - | - | - | - |
| 0x4296 | IN_SPD_COUNTS | HEX | - | unsigned int | - | - | - | - |
| 0x4297 | ROAD_SLOPE | % | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4298 | START_STOP_BUTTON | HEX | - | unsigned char | - | - | - | - |
| 0x4299 | SHUTDOWN_DURATION | HEX | High | unsigned long | - | - | - | - |
| 0x429A | ENGINE_TEMP_SHUTDOWN | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429B | GEARBOX_TEMP_SHUTDOWN | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x429C | SUMP_OIL_TEMP_EST_BY_COOLANT | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429D | SUMP_OIL_TEMP_EST_BY_TIME | °C | High | signed int | - | 1.0 | 4.0 | 0.0 |
| 0x429E | SHDR1_ANGL_LV2 | °C | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x429F | SHDR2_ANGL_LV2 | °C | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x42A0 | SHDR2_EEPROM_BLOCK_STATUS | 0-n | High | 0xFF | TAB_EEPROM_STATUS | - | - | - |
| 0x42A1 | SHDR1_2_SHDR_SHIFT_FLAG | HEX | High | unsigned int | - | - | - | - |
| 0xF402 | DTC that caused required freeze frame data storage | HEX | High | unsigned int | - | - | - | - |
| 0xF404 | Calculated LOAD Value | - | High | unsigned char | - | 100.0 | 255.0 | 0.0 |
| 0xF405 | Engine Coolant Temperature | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0xF40C | Engine RPM | 1/min | High | unsigned int | - | 1.0 | 4.0 | 0.0 |
| 0xF40D | Vehicle Speed Sensor | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xF411 | Absolute Throttle Position | % | High | unsigned char | - | 100.0 | 255.0 | 0.0 |
| 0xF442 | Control module voltage | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-oil-clutch-changed"></a>
### OIL_CLUTCH_CHANGED

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | OIL_CHANGED |
| 0x02 | OIL_AND_CLUTCH_CHANGED |
| 0x03 | OIL_REFILL |
| 0x04 | OIL_DUMMY_1 |
| 0x05 | OIL_DUMMY_2 |

<a id="table-rdbi-ads-dop"></a>
### RDBI_ADS_DOP

Dimensions: 8 rows × 2 columns

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

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECU mehrmals programmierbar |
| 0x01 | ECU mindestens einmal vollstaendig programmierbar |
| 0x02 | ECU nicht mehr programmierbar |
| 0xff | ungültig |

<a id="table-reserve"></a>
### RESERVE

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xFF | Reserve |

<a id="table-res-0x1061-r"></a>
### RES_0X1061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_ENDE_WABL | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Verriegelt (loeschen von Einzelfehlern und PDTCs wird unterbunden) 1: Entriegelt (loeschen von Einzelfehlern und PDTCs wird nicht unterbunden) |

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

<a id="table-res-0x4005-d"></a>
### RES_0X4005_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OIL_TEMPERATURE_RANGE_MINUS30_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich kleiner minus 30 Grad |
| STAT_OIL_TEMPERATURE_RANGE_MINUS30_TO_MINUS10_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich von minus 30 bis minus 10 Grad |
| STAT_OIL_TEMPERATURE_RANGE_MINUS10_TO_10_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich  von minus 10 bis 10 Grad |
| STAT_OIL_TEMPERATURE_RANGE_10_TO_30_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich  von 10 bis 30 Grad |
| STAT_OIL_TEMPERATURE_RANGE_30_TO_50_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl  Temperaturbereich von 30 bis 50 Grad |
| STAT_OIL_TEMPERATURE_RANGE_50_TO_70_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich von 50 bis 70 Grad |
| STAT_OIL_TEMPERATURE_RANGE_70_TO_90_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich  von 70 bis 90 Grad |
| STAT_OIL_TEMPERATURE_RANGE_90_TO_110_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich  von 90 bis 110 Grad |
| STAT_OIL_TEMPERATURE_RANGE_110_TO_120_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich von 110 bis 120 Grad |
| STAT_OIL_TEMPERATURE_RANGE_120_TO_130_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich von 120 bis 130 Grad |
| STAT_OIL_TEMPERATURE_RANGE_GREATERTHAN_130_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im Öl Temperaturbereich größer als 130 Grad |
| STAT_TCU_TEMPERATURE_RANGE_LESSTHAN_NULL_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich kleiner als NULL |
| STAT_TCU_TEMPERATURE_RANGE_0_TO_40_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich von NULL bis 40 Grad |
| STAT_TCU_TEMPERATURE_RANGE_40_TO_60_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich von 40 bis 60 Grad |
| STAT_TCU_TEMPERATURE_RANGE_60_TO_80_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich von 60 bis 80 Grad |
| STAT_TCU_TEMPERATURE_RANGE_80_TO_100_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich von 80 bis 100 Grad |
| STAT_TCU_TEMPERATURE_RANGE_100_TO_110_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich von 100 bis 110 Grad |
| STAT_TCU_TEMPERATURE_RANGE_110_TO_120_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich  von 110 bis 120 Grad |
| STAT_TCU_TEMPERATURE_RANGE_120_TO_130_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich  von 120 bis 130 Grad |
| STAT_TCU_TEMPERATURE_RANGE_GREATERTHAN_130_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit im TCU Temperaturbereich größer als 130 Grad |
| STAT_SUPPLY_VOLTAGE_RANGE_LESSTHAN_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in der die Versorgungsspannung kleiner als 6 Volt ist |
| STAT_SUPPLY_VOLTAGE_RANGE_6_TO_9_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in der die Versorgungsspannung von 6 bis 9 Volt ist |
| STAT_SUPPLY_VOLTAGE_RANGE_9_TO_10POINT5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in der die Versorgungsspannung von 9 bis 10.5 Volt ist |
| STAT_SUPPLY_VOLTAGE_RANGE_10POINT5_TO_16_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in der die Versorgungsspannung von 10.5  bis 16 Volt ist |
| STAT_SUPPLY_VOLTAGE_RANGE_GREATER_16_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in der die Versorgungsspannung größer als 16 Volt ist |
| STAT_ENGINE_START_STOP_COUNTER_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler der Engine-Stops |
| STAT_SAILING_MODE_EVENTS_COUNTER_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler der Sailing-Mode-Events |
| STAT_NEUTRAL_IDLE_CONTROL_COUNTER_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zähler der Neutral-Idle-Control-Situationen |
| STAT_D_MODE_DURATION_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in D-Mode |
| STAT_M_MODE_DURATION_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in M-Mode |
| STAT_S_MODE_DURATION_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebszeit in S-Mode |

<a id="table-res-0x4006-d"></a>
### RES_0X4006_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STATE_MSA_FUNCTION | 0-n | high | unsigned char | - | TABLE_MSA_STATE | - | - | - | Status der MSA Funktion |
| - | Bit | high | BITFIELD | - | BF_MSA_LOCKING_FUNCTION_STRUCT | - | - | - | Information welche Funktion MSA verhindert. |
| STAT_DESIRED_GEAR_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Soll-Gang |
| STAT_DYNAMIC_INDEX_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Der Dynamic Index enthält die Information wie die Schaltung ausgeführt und wie die TCC-Control gehandhabt wird. |
| STAT_SAILING_FUNCTION_MODE | 0-n | high | unsigned char | - | SAILING_MODE | - | - | - | State of sailing-function mode from gearbox |
| STAT_MSA_SHUT_OFF_REQUEST | 0-n | high | unsigned char | - | TABLE_REQUEST_MSA_SHUTOFF | - | - | - | Anfrage for MSA Shut-off |
| STAT_SLIP_REF_REQUEST_WERT | 1/min | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Soll Schlupf |
| STAT_SHIFT_LOGIC_DIAGNOSTIC | 0-n | high | unsigned int | - | TABLE_SHIFT_LOGIC_DIAGNOSTIC | - | - | - | shift-logic-information for diagnostic systems |
| - | Bit | high | BITFIELD | - | BF_SAILINGS_TATUS_STRUCT | - | - | - | 32 Bit-Maske Segel-Betriebsstrategie zur Analyse der AGS-internen Fahrer- und Fahrverhaltens-Segelverhinderer |

<a id="table-res-0x4006-r"></a>
### RES_0X4006_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RAM_DATEN_SCHREIBEN | - | - | + | 0-n | high | unsigned char | - | STATUS_RAM_DATEN_SCHREIBEN_TAB | - | - | - | Status RAM_DATEN_SCHREIBEN |

<a id="table-res-0x4007-d"></a>
### RES_0X4007_D

Dimensions: 309 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NO_OF_SUPERVISED_DTCS_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der überwachten Dtcs |
| STAT_IUMPR_1_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_1_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_1_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_1_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_2_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_2_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_2_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_2_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_3_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_3_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_3_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_3_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_4_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_4_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_4_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_4_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_5_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_5_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_5_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_5_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_6_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_6_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_6_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_6_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_7_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_7_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_7_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_7_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_8_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_8_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_8_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_8_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_9_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_9_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_9_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_9_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_10_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_10_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_10_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_10_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_11_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_11_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_11_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_11_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_12_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_12_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_12_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_12_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_13_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_13_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_13_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_13_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_14_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_14_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_14_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_14_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_15_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_15_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_15_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_15_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_16_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_16_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_16_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_16_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_17_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_17_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_17_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_17_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_18_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_18_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_18_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_18_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_19_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_19_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_19_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_19_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_20_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_20_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_20_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_20_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_21_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_21_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_21_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_21_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_22_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_22_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_22_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_22_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_23_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_23_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_23_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_23_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_24_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_24_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_24_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_24_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_25_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_25_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_25_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_25_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_26_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_26_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_26_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_26_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_27_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_27_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_27_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_27_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_28_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_28_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_28_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_28_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_29_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_29_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_29_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_29_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_30_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_30_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_30_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_30_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_31_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_31_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_31_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_31_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_32_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_32_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_32_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_32_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_33_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_33_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_33_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_33_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_34_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_34_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_34_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_34_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_35_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_35_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_35_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_35_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_36_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_36_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_36_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_36_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_37_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_37_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_37_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_37_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_38_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_38_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_38_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_38_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_39_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_39_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_39_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_39_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_40_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_40_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_40_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_40_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_41_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_41_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_41_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_41_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_42_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_42_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_42_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_42_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_43_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_43_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_43_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_43_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_44_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_44_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_44_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_44_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_45_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_45_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_45_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_45_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_46_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_46_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_46_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_46_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_47_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_47_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_47_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_47_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_48_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_48_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_48_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_48_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_49_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_49_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_49_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_49_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_50_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_50_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_50_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_50_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_51_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_51_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_51_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_51_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_52_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_52_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_52_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_52_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_53_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_53_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_53_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_53_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_54_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_54_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_54_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_54_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_55_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_55_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_55_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_55_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_56_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_56_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_56_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_56_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_57_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_57_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_57_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_57_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_58_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_58_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_58_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_58_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_59_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_59_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_59_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_59_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_60_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_60_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_60_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_60_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_61_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_61_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_61_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_61_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_62_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_62_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_62_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_62_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_63_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_63_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_63_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_63_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_64_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_64_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_64_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_64_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_65_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_65_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_65_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_65_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_66_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_66_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_66_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_66_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_67_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_67_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_67_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_67_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_68_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_68_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_68_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_68_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_69_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_69_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_69_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_69_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_70_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_70_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_70_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_70_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_71_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_71_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_71_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_71_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_72_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_72_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_72_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_72_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_73_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_73_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_73_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_73_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_74_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_74_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_74_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_74_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_75_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_75_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_75_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_75_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_76_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_76_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_76_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_76_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |
| STAT_IUMPR_77_UDS_DTC_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | IUMPR UDS DTC |
| STAT_IUMPR_77_OBD_DTC_WERT | HEX | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | IUMPR OBD DTC |
| STAT_IUMPR_77_DENOMINATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Denominators |
| STAT_IUMPR_77_NUMERATOR_WERT | Counts | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Wert des Numerators |

<a id="table-res-0x4008-d"></a>
### RES_0X4008_D

Dimensions: 38 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_LESS_2KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse kleiner als 2 Kilo Joule (KJ) |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_2KJ_6KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse von 2 KJ bis 6 KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_6KJ_14KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse von 6 KJ bis 14 KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_14KJ_33KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse von 14 KJ bis 33 KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_33KJ_80KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse von 33 KJ bis 80 KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_80KJ_180KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse von 80 KJ bis 180 KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_ENERGYCLASS_LARGER_190KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Energieklasse großer als 190KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_LESS_2KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse kleiner als 2 Kilo Joule (KJ) |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_2KJ_6KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse von 2 KJ bis 6 KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_6KJ_14KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse von 6 KJ bis 14 KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_14KJ_33KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse von 14 KJ bis 33 KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_33KJ_80KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse von 33 KJ bis 80 KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_80KJ_180KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse von 80 KJ bis 180 KJ |
| STAT_CLUTCH2_EVENTS_COUNTER_ENERGYCLASS_LARGER_190KJ_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler in der Energieklasse großer als 190KJ |
| STAT_CLUTCH1_EVENTS_COUNTER_POWERCLASS_LESS_5KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler in der Leistungsklasse kleiner als 5 Kilo Watt (kW) |
| STAT_CLUTCH1_EVENTS_COUNTER_POWERCLASS_5KW_20KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Leistung-Zähler in der Leistungsklasse von 5 kW bis 20 kW |
| STAT_CLUTCH1_EVENTS_COUNTER_POWERCLASS_20KW_50KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Leistung-Zähler in der Leistungsklasse von 20 kW bis 50 kW |
| STAT_CLUTCH1_EVENTS_COUNTER_POWERCLASS_50KW_80KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Leistung-Zähler in der Leistungsklasse von 50 kW bis 80 kW |
| STAT_CLUTCH1_EVENTS_COUNTER_POWERCLASS_LARGER_80KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Leistung-Zähler in der Leistungsklasse großer als 80 kW |
| STAT_CLUTCH2_EVENTS_COUNTER_POWERCLASS_LESS_5KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Leistung-Zähler in der Leistungsklasse kleiner als 5 Kilo Watt (kW) |
| STAT_CLUTCH2_EVENTS_COUNTER_POWERCLASS_5KW_20KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Leistung-Zähler in der Leistungsklasse von 5 kW bis 20 kW |
| STAT_CLUTCH2_EVENTS_COUNTER_POWERCLASS_20KW_50KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Leistung-Zähler in der Leistungsklasse von 20 kW bis 50 kW |
| STAT_CLUTCH2_EVENTS_COUNTER_POWERCLASS_50KW_80KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Leistung-Zähler in der Leistungsklasse von 50 kW bis 80 kW |
| STAT_CLUTCH2_EVENTS_COUNTER_POWERCLASS_LARGER_80KW_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Leistung-Zähler in der Leistungsklasse großer als 80 kW |
| STAT_CLUTCH1_EVENTS_COUNTER_TEMPCLASS_LESS_0GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler der Temperaturklasse kleiner als 0 Grad |
| STAT_CLUTCH1_EVENTS_COUNTER_TEMPCLASS_0_100GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler der Temperaturklasse von 0 bis 100 Grad |
| STAT_CLUTCH1_EVENTS_COUNTER_TEMPCLASS_100_200GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler der Temperaturklasse von 100 bis 200 Grad |
| STAT_CLUTCH1_EVENTS_COUNTER_TEMPCLASS_200_300GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler der Temperaturklasse von 200 bis 300 Grad |
| STAT_CLUTCH1_EVENTS_COUNTER_TEMPCLASS_LARGER_300GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung1-Ereignisse-Zähler der Temperaturklasse großer als 300 Grad |
| STAT_CLUTCH2_EVENTS_COUNTER_TEMPCLASS_LESS_0GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler der Temperaturklasse kleiner als 0 Grad Celsius |
| STAT_CLUTCH2_EVENTS_COUNTER_TEMPCLASS_0_100GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler der Temperaturklasse von 0 bis 100 Grad |
| STAT_CLUTCH2_EVENTS_COUNTER_TEMPCLASS_100_200GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler der Temperaturklasse von 100 bis 200 Grad |
| STAT_CLUTCH2_EVENTS_COUNTER_TEMPCLASS_200_300GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler der Temperaturklasse von 200 bis 300 Grad |
| STAT_CLUTCH2_EVENTS_COUNTER_TEMPCLASS_LARGER_300GRAD_WERT | Counts | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kupplung2-Ereignisse-Zähler der Temperaturklasse großer als 300 Grad |
| STAT_CLUTCH1_MAX_TEMPERATURE_WERT | ° | high | signed int | - | - | 1.0 | 4.0 | 0.0 | höchste Temperatur der Kupplung1 in einem Ereignis |
| STAT_CLUTCH2_MAX_TEMPERATURE_WERT | ° | high | signed int | - | - | 1.0 | 4.0 | 0.0 | höchste Temperatur der Kupplung2 in einem Ereignis |
| STAT_CLUTCH1_ENERGIE_WERT | J | high | unsigned long | - | - | 4.0 | 1.0 | 0.0 | Energie Verbrauch in Kupplung 1 im gesamten Lebenszyklus |
| STAT_CLUTCH2_ENERGIE_WERT | J | high | unsigned long | - | - | 4.0 | 1.0 | 0.0 | Energie Verbrauch in Kupplung 2 im gesamten Lebenszyklus |

<a id="table-res-0x4009-d"></a>
### RES_0X4009_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPEED_FEED_FORW_ADAPTATION_CLU1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Geschwindigkeitseinspeisung Adaptionswert für Kupplung 1 ( Einheit Druck/Drehzahlverlauf) |
| STAT_SPEED_FEED_FORW_ADAPTATION_STATUS_CLU1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus der Pumpenaktuators Kupplung 1 |
| STAT_SPEED_FEED_FORW_ADAPTATION_COUNTER_CLU1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler des Pumpenaktuators Kupplung 1 |
| STAT_SPEED_FEED_FORW_ADAPTATION_CLU2_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Geschwindigkeitseinspeisung Adaptionswert für Kupplung 2 ( Einheit Druck/Drehzahlverlauf) |
| STAT_SPEED_FEED_FORW_ADAPTATION_STATUS_CLU2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus der Pumpenaktuators Kupplung 2 |
| STAT_SPEED_FEED_FORW_ADAPTATION_COUNTER_CLU2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler des Pumpenaktuators Kupplung 2 |
| STAT_GAIN_ADAPTATION_FACTOR1_CLU1_WERT | - | high | unsigned int | - | - | 1.0 | 32768.0 | 0.0 | Gain Adaptionsdaten Kupplung 1- Faktor 1 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_FACTOR2_CLU1_WERT | - | high | signed int | - | - | 1.0 | 8388608.0 | 0.0 | Gain Adaptionsdaten Kupplung 1 Faktor 2 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_FACTOR3_CLU1_WERT | - | high | signed int | - | - | 1.0 | 8388608.0 | 0.0 | Gain Adaptionsdaten Kupplung 1 Faktor 3 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_STATUS_CLU1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus des Kupplung1-Gains |
| STAT_GAIN_ADAPTATION_COUNTER_CLU1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler des Kupplung1-Gains |
| STAT_GAIN_ADAPTATION_FACTOR1_CLU2_WERT | - | high | unsigned int | - | - | 1.0 | 32768.0 | 0.0 | Gain Adaptionsdaten Kupplung 2- Faktor 1 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_FACTOR2_CLU2_WERT | - | high | signed int | - | - | 1.0 | 8388608.0 | 0.0 | Gain Adaptionsdaten Kupplung 2 Faktor 2 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_FACTOR3_CLU2_WERT | - | high | signed int | - | - | 1.0 | 8388608.0 | 0.0 | Gain Adaptionsdaten Kupplung 2 Faktor 3 (Faktor1 + Moment*Faktor2 + EngSpeed * Faktor3) |
| STAT_GAIN_ADAPTATION_STATUS_CLU2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus des Kupplung2-Gains |
| STAT_GAIN_ADAPTATION_COUNTER_CLU2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler Kupplung2-Gains |
| STAT_CLU1_GAIN_TEACHIN_VALUE_WERT | - | high | unsigned int | - | - | 1.0 | 16384.0 | 0.0 | Kupplung 1  Gain Teachin Wert |
| STAT_CLU2_GAIN_TEACHIN_VALUE_WERT | - | high | unsigned int | - | - | 1.0 | 16384.0 | 0.0 | Kupplung 2  Gain Teachin Wert |
| STAT_KISSPOINT_ADAP_VALUE_CLU1_WERT | - | high | unsigned int | - | - | 1.0 | 32768.0 | 0.0 | Aktueller Kisspoint Adaptionswert - Kupplung 1 |
| STAT_KISSPOINT_ADAPTATION_STATUS_CLU1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus des Kupplung1-Kisspoints |
| STAT_KISSPOINT_ADAPTATION_COUNTER_CLU1_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler des Kupplung1-Kisspoints |
| STAT_KISSPOINT_ADAP_VALUE_CLU2_WERT | - | high | unsigned int | - | - | 1.0 | 32768.0 | 0.0 | Aktueller Kisspoint Adaptionswert - Kupplung 2 |
| STAT_KISSPOINT_ADAPTATION_STATUS_CLU2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Adaptionsstatus des Kupplung2-Kisspoints |
| STAT_KISSPOINT_ADAPTATION_COUNTER_CLU2_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Adaptionszähler des Kupplung2-Kisspoints |
| STAT_BLOCK_J_EEPROM_VERSION_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | EEPROM version |

<a id="table-res-0x413c-d"></a>
### RES_0X413C_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RC_STRT_ODO_DATA | DATA | high | data[2] | - | - | 1.0 | 1.0 | 0.0 | Rennstart - Odometer |
| STAT__DATA | DATA | high | data[38] | - | - | 1.0 | 1.0 | 0.0 | reserviert |

<a id="table-res-0x4141-d"></a>
### RES_0X4141_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DSM_LCH_GEAR_1_CNT_DAT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für den Start im 1. Gang |
| STAT_DSM_LCH_GEAR_R_CNT_DAT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für den Start im Rückwärtsgang |
| STAT_DSM_RE_LCH_GEAR_2_CNT_DAT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für das wiederholte Einlegen in den 2. Gang |
| STAT_DSM_REQ_P_GT_VEL_THRES_DAT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für Schalthebel in Parkposition mit Fahrzeuggeschwindigkeit über den Grenzwert |
| STAT_DSM_REQ_R_GT_VEL_THRES_DAT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für Schalthebel in Rückwärts-Position mit der Fahrzeuggeschwindigkeit über den Grenzwert |
| STAT_DSM_CLU1_SUM_ENRG_DAT_WERT | kJ | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Max-Wert der Kupplungsenergie (Kupplung 1) für ein einzelnes Ereignis |
| STAT_DSM_CLU2_SUM_ENRG_DAT_WERT | kJ | high | unsigned int | - | - | 1.0 | 4.0 | 0.0 | Max-Wert der Kupplungsenergie (Kupplung 2) für ein einzelnes Ereignis |
| STAT_DSM_CLU1_POW_WERT | W | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximaler Wert der Kupplungsleistung (Kupplung 1) |
| STAT_DSM_CLU2_POW_WERT | W | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Maximaler Wert der Kupplungsleistung (Kupplung 2) |
| STAT_DSM_DIST_NEG_TEMP_CNT_DAT_WERT | km | high | unsigned int | - | - | 2.0 | 1.0 | 0.0 | Gefahrene km bei niedriger Temperatur |
| STAT_DSM_DIST_POS_TEMP_CNT_DAT_WERT | km | high | unsigned int | - | - | 2.0 | 1.0 | 0.0 | Gefahrene km bei einer Temperatur höher 0 Grad |
| STAT_DSM_INS_SPD1_MAX_DAT_WERT | 1/min | high | unsigned char | - | - | 16.0 | 1.0 | 3500.0 | Statistikprotokollierung für die maximale Eingangswellendrehzahl 1 |
| STAT_DSM_INS_SPD2_MAX_DAT_WERT | 1/min | high | unsigned char | - | - | 16.0 | 1.0 | 3500.0 | Statistikprotokollierung für die maximalen Eingangswellendrehzahl 2 |
| STAT_DSM_MAX_ACTU_POS_TP_CLU1_DAT_WERT | - | high | unsigned char | - | - | 1.0 | 1024.0 | 0.0 | Maximaler normalisierter Aktorwert für den Berührungspunkt für Kupplung 1 über die gesamte Lebensdauer |
| STAT_DSM_MAX_ACTU_POS_TP_CLU2_DAT_WERT | - | high | unsigned char | - | - | 1.0 | 1024.0 | 0.0 | Maximaler normalisierter Aktorwert für den Berührungspunkt für Kupplung 2 über die gesamte Lebensdauer |
| STAT_DSM_MIN_ACTU_POS_TP_CLU1_DAT_WERT | - | high | unsigned char | - | - | 1.0 | 1024.0 | 0.0 | Minimaler normalisierter Aktorwert für den Berührungspunkt für Kupplung 1 über die gesamte Lebensdauer |
| STAT_TSL_MIN_ACTU_POS_TP_CLU2_DAT_WERT | - | high | unsigned char | - | - | 1.0 | 1024.0 | 0.0 | Minimaler normalisierter Aktorwert für den Berührungspunkt für Kupplung 2 über die gesamte Lebensdauer |
| STAT_DSM_NR_RESETS_DAT_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Zurücksetzungen |

<a id="table-res-0x4142-d"></a>
### RES_0X4142_D

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VALUE1_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Reserved |
| STAT_VALUE2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | clutch red state counter |
| STAT_VALUE3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | clutch red state counter |
| STAT_VALUE4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | clutch yellow state counter |
| STAT_VALUE5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | clutch yellow state counter |
| STAT_VALUE6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | clutch fading counter |
| STAT_VALUE7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | clutch fading counter |
| STAT_VALUE8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | counter for powerlaunches with full pedal |
| STAT_VALUE9_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | counter for launches not in 1st or Rev. gear |
| STAT_VALUE10_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | counter for launches not in 1st or Rev. gear |
| STAT_VALUE11_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | counter for change of active gear with correct passive gear decision |
| STAT_VALUE12_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | counter for change of active gear with wrong passive gear decision |
| STAT_VALUE13_WERT | - | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | counter for change of passive gear without change of active gear |

<a id="table-res-0x4143-d"></a>
### RES_0X4143_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VALUE1_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 1 |
| STAT_VALUE2_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 2 |
| STAT_VALUE3_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 3 |
| STAT_VALUE4_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 4 |
| STAT_VALUE5_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 5 |
| STAT_VALUE6_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang 6 |
| STAT_VALUE7_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang7 |
| STAT_VALUE8_WERT | Counts | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Counter für Einlegefehler - Gang R |
| STAT_VALUE9_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 1 |
| STAT_VALUE10_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 2 |
| STAT_VALUE11_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 3 |
| STAT_VALUE12_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 4 |
| STAT_VALUE13_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 5 |
| STAT_VALUE14_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 6 |
| STAT_VALUE15_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang 7 |
| STAT_VALUE16_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Counter für Einlegeversuche - Gang R |
| STAT_VALUE17_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 1- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE18_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 2- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE19_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 3- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE20_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 4 - Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE21_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 5- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE22_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 6- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE23_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang 7- Counter für Einlegeaktionen vor der Synchronisierung |
| STAT_VALUE24_WERT | Counts | high | unsigned int | - | - | 4.0 | 1.0 | 0.0 | Gang R- Counter für Einlegeaktionen vor der Synchronisierung |

<a id="table-res-0x4144-d"></a>
### RES_0X4144_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EEP_S_SD1_ENC_RAW_IF_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Geberwert der Schaltwalze 1 während der letzten Herunterfahren |
| STAT_NVR_S_SD1_ENC_LOEND_WERT | - | high | signed int | - | - | 1.0 | 16.0 | 0.0 | untere Position von Schaltwalze 1 bestimmt durch der Referenzwalze |
| STAT_NVR_S_SD1_ENC_HIEND_WERT | - | high | signed int | - | - | 1.0 | 16.0 | 0.0 | oberen Position der Schaltwalze 1  bestimmt durch die Referenz-Walze |
| STAT_NVR_S_SD2_ENC_RAW_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Geberwert der Schaltwalze 2 während des letzten Herunterfahren |
| STAT_NVR_S_SD2_ENC_LOEND_WERT | - | high | signed int | - | - | 1.0 | 16.0 | 0.0 | untere Position der Schaltwalze 2 bestimmt durch dier Referenzwalze |
| STAT_NVR_S_SD2_ENC_HIEND_WERT | - | high | signed int | - | - | 1.0 | 16.0 | 0.0 | oberen Position der Schaltwalze 2  bestimmt durch die Referenz-Walze |
| STAT_NVR_SYNCGEAR1_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 1 |
| STAT_EEP_SDIF_SYNCGEAR2UP_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 2 aufwärts |
| STAT_EEP_SDIF_SYNCGEAR2DWN_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 2 abwärts |
| STAT_EEP_SDIF_SYNCGEAR3UP_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 3 aufwärts |
| STAT_EEP_SDIF_SYNCGEAR3DWN_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 3 abwärts |
| STAT_EEP_SDIF_SYNCGEAR4UP_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 4 aufwärts |
| STAT_EEP_SDIF_SYNCGEAR4DWN_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 4 abwärts |
| STAT_EEP_SDIF_SYNCGEAR5_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 5 |
| STAT_EEP_SDIF_SYNCGEAR5DWN_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 5 abwärts |
| STAT_EEP_SDIF_SYNCGEAR6_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 6 |
| STAT_EEP_SDIF_SYNCGEAR7_WERT | ° | high | signed char | - | - | 1.0 | 16.0 | 0.0 | Offset Synchron-Position Gear 7 |

<a id="table-res-0x4145-d"></a>
### RES_0X4145_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SDIF_MAX_REF_SD1_LO_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Maximale Differenz zwischen der Endreferenzposition und der unteren gemessenen Position auf Schaltwalze 1 - Unterer Wert |
| STAT_SDIF_MAX_REF_SD1_HI_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Maximale Differenz zwischen der Endreferenzposition und der oberen gemessenen Position auf Schaltwalze 1  - Oberer Wert |
| STAT_SDIF_MAX_REF_SD2_LO_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Maximale Differenz zwischen der Endreferenzposition und  der unteren gemessenen Position  auf Schaltwalze 2 - Unterer Wert |
| STAT_SDIF_MAX_REF_SD2_HI_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Maximale Differenz zwischen der Endreferenzposition und der oberen gemessenen Position auf Schaltwalze 2 - Oberer Wert |
| STAT_SDIF_MIN_REF_SD1_LO_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Minimale Differenz zwischen der Endreferenzposition und der unteren gemessenen Position auf Schaltwalze 1 - Unterer Wert |
| STAT_SDIF_MIN_REF_SD1_HI_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Minimale Differenz zwischen der Endreferenzposition und der oberen gemessenen Position auf Schaltwalze 1 - Oberer Wert |
| STAT_SDIF_MIN_REF_SD2_LO_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Minimale Differenz zwischen der Endreferenzposition und der unteren gemessenen Position auf Schaltwalze 2 - Unterer Wert |
| STAT_SDIF_MIN_REF_SD2_HI_WERT | - | high | signed char | - | - | 1.0 | 8.0 | 0.0 | Minimale Differenz zwischen der Endreferenzposition und der oberen gemessenen Position auf Schaltwalze 2 - Oberer Wert |
| STAT_SD1_EMERG_REQ_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Notfall-Anfrage auf Schaltwalze 1 während dem letzten Lauf |
| STAT_SD2_EMERG_REQ_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Notfall-Anfrage auf Schaltwalze 2 während dem letzten Lauf |
| STAT_GTI_REQ_INFO_SD2 | 0-n | high | unsigned char | - | TAB_STAT_GTI_REQ_INFO_SD2 | - | - | - | Information warum Referenzfahrt für Schaltwalze 2 benötigt wird |
| STAT_GTI_REQ_INFO_SD1 | 0-n | high | unsigned char | - | TAB_STAT_GTI_REQ_INFO_SD1 | - | - | - | Information warum Referenzfahrt für Schaltwalze 1 benötigt wird |
| STAT_GTI_ERR_BIT_SD2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Die zuletzt ausgeführte Referenz-Fahrt war fehlerhaft, Schaltwalze 2 |
| STAT_GTI_ERR_BIT_SD1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Die zuletzt ausgeführte Referenz-Fahrt war fehlerhaft; Schaltwalze 1 |
| STAT_WRN_REF_POINT_SD2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Referenz-Punkt-Drift von Schaltwalze 2 wurde während dem letzten Lauf entdeckt |
| STAT_WRN_REF_POINT_SD1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Referenz-Punkt-Drift von Schaltwalze 1 wurde während dem letzten Lauf entdeckt |
| STAT_GBX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Getriebetemperatur |
| STAT_ENG_TEMP_WERT | °C | high | signed int | - | - | 1.0 | 4.0 | 0.0 | Motortemperatur |
| STAT_BROKEN_FORK_SD2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gebrochene Gabel auf Schaltwalze 2 ist bestätigt |
| STAT_BROKEN_FORK_SD1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gebrochene Gabel auf Schaltwalze 1 ist bestätigt |

<a id="table-res-0x4146-d"></a>
### RES_0X4146_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TRS0_DATA_IF_0_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [0]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_1_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [1]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_2_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [2]-TRS0 Daten aus dem EEPROM lesen |
| STAT_TRS0_DATA_IF_3_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [3]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_4_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [4]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_5_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [5]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_6_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [6]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_TRS0_DATA_IF_7_WERT | - | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | [7]-TRS0 Daten aus dem EEPROM  lesen |
| STAT_SDS_INS_SPD_FRM_STATUS_1 | 0-n | high | unsigned char | - | TAB_STAT_SDS_INS_SPD_FRM_STATUS_1 | - | - | - | Eingangswelle 1 -  Geschwindigkeitsfehlerstatus für Fehlerspeicher |
| STAT_SDS_INS_SPD_FRM_STATUS_2 | 0-n | high | unsigned char | - | TAB_STAT_SDS_INS_SPD_FRM_STATUS_2 | - | - | - | Eingangswelle 2 -  Geschwindigkeitsfehlerstatus für Fehlerspeicher |

<a id="table-res-0x4148-d"></a>
### RES_0X4148_D

Dimensions: 81 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AVG_CNT_VAL_SG_001_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 001 |
| STAT_HURT_CNT_VAL_SG_001_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 001 |
| STAT_MIN_CNT_VAL_SG_001_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 001 |
| STAT_AVG_CNT_VAL_SG_002_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 002; Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_002_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 002; Getriebe Ohne R |
| STAT_MIN_CNT_VAL_SG_002_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 002, Getriebe Ohne R |
| STAT_AVG_CNT_VAL_SG_002_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 002, Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_002_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 002; Getriebe mit R |
| STAT_MIN_CNT_VAL_SG_002_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 002, Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_003_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 003; Getriebe Ohne R |
| STAT_HURT_CNT_VAL_SG_003_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 008; Getriebe Ohne R |
| STAT_MIN_CNT_VAL_SG_003_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 003; Getriebe Ohne R |
| STAT_AVG_CNT_VAL_SG_003_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 003, Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_003_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 003; Getriebe mit R |
| STAT_MIN_CNT_VAL_SG_003_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 003, Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_004_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 004; Getriebe Ohne R |
| STAT_HUTR_CNT_VAL_SG_004_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 004; Getriebe Ohne  R |
| STAT_MIN_CNT_VAL_SG_004_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 004; Getriebe Ohne R |
| STAT_AVG_CNT_VAL_SG_004_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 004; Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_004_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 004; Getriebe mit R |
| STAT_MIN_CNT_VAL_SG_004_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 004; Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_006A_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 006a; Getriebe Ohne R |
| STAT_HURT_CNT_VAL_SG_006A_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 006a; Getriebe ohne R |
| STAT_MIN_CNT_VAL_SG_006A_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 006a; Getriebe ohne R |
| STAT_AVG_CNT_VAL_SG_006A_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 006a; Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_006A_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 006a; Getriebe mit R |
| STAT_MIN_CNT_VAL_SG_006A_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 006a; Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_006B_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 006b; Getriebe ohne R |
| STAT_HURT_CNT_VAL_SG_006B_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 006b; Getriebe ohne R |
| STAT_MIN_CNT_VAL_SG_006B_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 006b; Getriebe ohne R |
| STAT_AVG_CNT_VAL_SG_006B_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 006b; Getriebe mit R |
| STAT_HURT_CNT_VAL_006B_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 006b; Getriebe mit R |
| STAT_MIN_CNT_VAL_006B_R_WERT | ms | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 006b; Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_007_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 007 |
| STAT_HURT_CNT_VAL_SG_007_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 007 |
| STAT_MIN_CNT_VAL_SG_007_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 007 |
| STAT_AVG_CNT_VAL_SG_008_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 008; Getriebe ohne R |
| STAT_HURT_CNT_VAL_SG_008_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 008; Getriebe Ohne R |
| STAT_MIN_CNT_VAL_SG_008_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 008; Getriebe Ohne R |
| STAT_AVG_CNT_VAL_SG_008_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 008, Getriebe mit R |
| STAT_HURT_CNT_VAL_SG_008_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 008; Getriebe mit R |
| STAT_MIN_CNT_VAL_SG_008_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 008; Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_013_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 0013 |
| STAT_HURT_CNT_VAL_SG_013_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 013 |
| STAT_MIN_CNT_VAL_SG_013_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 013 |
| STAT_AVG_CNT_VAL_SG_014_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 014 |
| STAT_HURT_CNT_VAL_SG_014_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 014 |
| STAT_MIN_CNT_VAL_SG_014_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 014 |
| STAT_AVG_CNT_VAL_SG_016_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 016 |
| STAT_HURT_CNT_VAL_SG_016_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 016 |
| STAT_MIN_CNT_VAL_SG_016_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 016 |
| STAT_AVG_CNT_VAL_SG_019A_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 019a |
| STAT_HURT_CNT_VAL_SG_019A_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 019a |
| STAT_MIN_CNT_VAL_SG_019A_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 019a |
| STAT_AVG_CNT_VAL_SG_019B_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 019b |
| STAT_HURT_CNT_VAL_SG_019B_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 019b |
| STAT_MIN_CNT_VAL_SG_019B_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 019b |
| STAT_AVG_CNT_VAL_SG_019C_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 019c; Getriebe Ohne R |
| STAT_HUTR_CNT_VAL_SG_019C_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 019c; Getriebe Ohne  R |
| STAT_MIN_CNT_VAL_SG_019C_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 019c; Getriebe Ohne R |
| STAT_AVG_CNT_VAL_SG_019C_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel 019c; Getriebe mit R |
| STAT_HUTR_CNT_VAL_SG_019C_R_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel 019c; Getriebe mit  R |
| STAT_MIN_CNT_VAL_SG_019C_R_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel 019c; Getriebe mit R |
| STAT_AVG_CNT_VAL_SG_SB01_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb01 |
| STAT_HURT_CNT_VAL_SG_SB01_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb01 |
| STAT_MIN_CNT_VAL_SG_SB01_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb01 |
| STAT_AVG_CNT_VAL_SG_SB02_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb02 |
| STAT_HURT_CNT_VAL_SG_SB02_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb02 |
| STAT_MIN_CNT_VAL_SG_SB02_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb02 |
| STAT_AVG_CNT_VAL_SG_SB03_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb03 |
| STAT_HURT_CNT_VAL_SG_SB03_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb03 |
| STAT_MIN_CNT_VAL_SG_SB03_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb03 |
| STAT_AVG_CNT_VAL_SG_SB04_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb04 |
| STAT_HURT_CNT_VAL_SG_SB04_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb04 |
| STAT_MIN_CNT_VAL_SG_SB04_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb04 |
| STAT_AVG_CNT_VAL_SG_SB05_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb05 |
| STAT_HURT_CNT_VAL_SG_SB05_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb05 |
| STAT_MIN_CNT_VAL_SG_SB05_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb05 |
| STAT_AVG_CNT_VAL_SG_SB06_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Durchschnittswert von Sicherheitsziel sb06 |
| STAT_HURT_CNT_VAL_SG_SB06_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler-Zielverletzung von Sicherheitsziel sb06 |
| STAT_MIN_CNT_VAL_SG_SB06_WERT | ms | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Zähler-Mindestwert von Sicherheitsziel sb06 |

<a id="table-res-0x4149-d"></a>
### RES_0X4149_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ISS_DATA_WERT | 1/min | high | signed int | - | - | 1.0 | 2.0 | 0.0 | Geschwindigkeit Eingangswelle 1 |
| STAT_ISS_DATA_2_WERT | 1/min | high | signed int | - | - | 1.0 | 2.0 | 0.0 | Geschwindigkeit Eingangswelle 2 |

<a id="table-res-0x4300-d"></a>
### RES_0X4300_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ECU_DEVICE_STATE | 0-n | high | unsigned char | - | ECU_DEVICE_STATE_TABLE | - | - | - | Ecu device state |
| STAT_ECU_SAMPLE_LEVEL_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | ECU Sample Level |

<a id="table-res-0x4312-d"></a>
### RES_0X4312_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IDR_EGS_DATA | DATA | high | data[240] | - | - | 1.0 | 1.0 | 0.0 | Daten der IDR für EGS |

<a id="table-res-0x4314-d"></a>
### RES_0X4314_D

Dimensions: 416 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_0 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 0 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_1 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 1 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_2 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 2 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_3 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 3 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_4 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 4 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_5 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 5 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_6 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 6 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_7 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 7 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_8 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 8 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_9 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 9 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_10 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 10 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_11 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 11 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_12 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 12 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_13 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 13 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_14 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 14 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_15 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 15 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_16 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 16 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_17 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 17 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_18 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 18 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_19 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 19 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_20 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 20 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_21 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 21 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_22 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 22 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_23 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 23 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_24 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 24 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_25 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 25 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_26 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 26 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_27 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 27 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_28 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 28 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_29 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 29 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_30 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 30 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_31 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 31 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_32 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 32 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_33 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 33 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_34 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 34 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_35 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 35 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_36 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 36 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_37 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 37 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_38 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 38 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_39 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 39 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_40 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 40 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_41 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 41 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_42 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 42 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_43 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 43 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_44 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 44 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_45 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 45 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_46 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 46 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_47 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 47 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_48 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 48 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_49 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 49 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_50 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 50 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_51 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 51 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_52 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 52 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_53 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 53 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_54 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 54 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_55 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 55 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_56 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 56 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_57 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 57 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_58 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 58 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_59 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 59 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_60 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 60 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_61 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 61 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_62 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 62 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_63 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 63 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_64 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 64 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_65 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 65 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_66 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 66 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_67 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 67 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_68 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 68 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_69 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 69 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_70 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 70 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_71 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 71 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_72 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 72 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_73 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 73 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_74 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 74 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_75 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 75 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_76 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 76 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_77 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 77 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_78 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 78 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_79 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 79 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_80 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 80 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_81 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 81 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_82 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 82 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_83 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 83 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_84 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 84 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_85 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 85 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_86 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 86 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_87 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 87 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_88 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 88 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_89 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 89 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_90 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 90 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_91 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 91 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_92 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 92 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_93 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 93 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_94 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 94 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_95 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 95 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_96 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 96 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_97 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 97 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_98 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 98 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_99 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 99 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_100 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 100 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_101 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 101 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_102 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 102 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_103 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 103 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_104 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 104 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_105 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 105 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_106 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 106 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_107 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 107 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_108 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 108 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_109 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 109 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_110 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 110 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_111 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 111 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_112 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 112 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_113 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 113 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_114 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 114 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_115 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 115 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_116 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 116 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_117 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 117 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_118 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 118 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_119 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 119 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_120 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 120 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_121 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 121 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_122 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 122 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_123 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 123 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_124 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 124 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_125 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 125 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_126 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 126 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_127 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 127 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_128 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 128 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_129 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 129 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_130 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 130 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_131 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 131 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_132 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 132 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_133 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 133 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_134 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 134 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_135 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 135 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_136 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 136 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_137 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 137 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_138 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 138 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_139 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 139 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_140 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 140 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_141 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 141 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_142 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 142 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_143 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 143 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_144 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 144 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_145 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 145 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_146 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 146 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_147 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 147 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_148 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 148 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_149 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 149 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_150 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 150 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_151 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 151 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_152 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 152 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_153 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 153 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_154 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 154 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_155 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 155 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_156 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 156 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_157 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 157 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_158 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 158 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_159 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 159 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_160 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 160 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_161 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 161 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_162 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 162 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_163 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 163 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_164 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 164 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_165 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 165 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_166 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 166 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_167 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 167 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_168 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 168 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_169 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 169 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_170 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 170 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_171 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 171 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_172 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 172 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_173 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 173 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_174 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 174 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_175 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 175 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_176 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 176 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_177 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 177 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_178 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 178 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_179 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 179 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_180 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 180 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_181 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 181 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_182 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 182 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_183 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 183 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_184 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 184 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_185 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 185 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_186 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 186 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_187 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 187 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_188 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 188 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_189 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 189 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_190 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 190 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_191 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 191 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_192 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 192 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_193 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 193 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_194 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 194 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_195 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 195 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_196 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 196 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_197 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 197 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_198 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 198 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_199 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 199 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_200 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 200 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_201 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 201 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_202 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 202 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_203 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 203 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_204 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 204 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_205 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 205 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_206 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 206 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_207 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 207 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_208 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 208 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_209 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 209 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_210 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 210 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_211 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 211 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_212 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 212 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_213 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 213 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_214 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 214 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_215 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 215 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_216 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 216 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_217 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 217 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_218 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 218 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_219 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 219 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_220 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 220 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_221 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 221 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_222 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 222 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_223 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 223 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_224 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 224 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_225 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 225 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_226 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 226 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_227 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 227 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_228 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 228 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_229 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 229 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_230 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 230 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_231 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 231 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_232 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 232 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_233 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 233 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_234 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 234 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_235 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 235 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_236 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 236 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_237 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 237 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_238 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 238 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_239 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 239 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_240 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 240 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_241 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 241 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_242 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 242 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_243 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 243 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_244 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 244 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_245 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 245 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_246 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 246 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_247 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 247 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_248 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 248 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_249 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 249 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_250 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 250 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_251 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 251 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_252 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 252 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_253 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 253 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_254 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 254 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_255 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 255 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_256 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 256 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_257 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 257 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_258 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 258 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_259 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 259 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_260 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 260 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_261 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 261 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_262 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 262 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_263 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 263 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_264 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 264 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_265 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 265 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_266 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 266 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_267 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 267 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_268 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 268 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_269 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 269 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_270 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 270 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_271 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 271 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_272 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 272 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_273 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 273 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_274 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 274 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_275 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 275 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_276 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 276 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_277 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 277 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_278 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 278 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_279 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 279 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_280 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 280 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_281 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 281 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_282 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 282 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_283 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 283 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_284 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 284 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_285 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 285 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_286 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 286 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_287 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 287 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_288 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 288 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_289 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 289 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_290 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 290 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_291 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 291 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_292 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 292 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_293 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 293 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_294 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 294 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_295 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 295 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_296 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 296 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_297 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 297 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_298 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 298 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_299 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 299 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_300 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 300 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_301 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 301 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_302 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 302 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_303 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 303 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_304 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 304 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_305 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 305 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_306 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 306 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_307 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 307 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_308 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 308 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_309 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 309 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_310 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 310 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_311 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 311 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_312 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 312 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_313 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 313 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_314 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 314 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_315 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 315 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_316 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 316 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_317 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 317 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_318 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 318 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_319 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 319 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_320 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 320 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_321 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 321 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_322 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 322 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_323 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 323 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_324 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 324 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_325 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 325 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_326 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 326 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_327 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 327 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_328 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 328 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_329 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 329 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_330 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 330 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_331 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 331 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_332 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 332 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_333 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 333 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_334 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 334 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_335 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 335 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_336 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 336 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_337 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 337 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_338 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 338 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_339 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 339 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_340 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 340 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_341 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 341 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_342 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 342 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_343 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 343 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_344 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 344 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_345 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 345 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_346 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 346 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_347 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 347 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_348 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 348 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_349 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 349 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_350 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 350 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_351 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 351 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_352 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 352 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_353 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 353 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_354 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 354 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_355 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 355 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_356 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 356 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_357 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 357 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_358 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 358 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_359 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 359 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_360 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 360 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_361 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 361 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_362 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 362 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_363 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 363 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_364 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 364 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_365 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 365 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_366 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 366 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_367 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 367 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_368 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 368 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_369 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 369 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_370 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 370 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_371 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 371 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_372 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 372 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_373 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 373 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_374 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 374 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_375 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 375 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_376 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 376 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_377 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 377 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_378 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 378 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_379 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 379 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_380 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 380 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_381 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 381 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_382 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 382 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_383 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 383 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_384 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 384 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_385 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 385 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_386 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 386 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_387 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 387 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_388 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 388 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_389 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 389 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_390 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 390 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_391 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 391 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_392 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 392 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_393 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 393 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_394 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 394 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_395 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 395 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_396 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 396 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_397 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 397 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_398 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 398 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_399 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 399 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_400 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 400 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_401 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 401 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_402 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 402 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_403 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 403 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_404 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 404 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_405 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 405 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_406 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 406 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_407 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 407 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_408 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 408 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_409 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 409 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_410 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 410 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_411 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 411 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_412 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 412 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_413 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 413 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_414 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 414 |
| - | Bit | high | BITFIELD | - | BF_DRAG_IND_BIT_MAPPING_FSP_ID_415 | - | - | - | Max and Amount of threshold reached counters for FSP_ID 415 |

<a id="table-res-0xc000-d"></a>
### RES_0XC000_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EWS4STATE | 0-n | high | unsigned char | - | EWS4STATE | - | - | - | EWS4STATE |
| STAT_DHCLIENTSTATE | 0-n | high | unsigned char | - | DHCLIENTSTATE | - | - | - | DHclientState |
| STAT_FKT0_INT_WERT | HEX | high | unsigned char | - | - | - | - | - | interner Zustand im Steuergerät |
| STAT_FKT1_INT_WERT | HEX | high | unsigned char | - | - | - | - | - | interner Zustand im Steuergerät |
| STAT_FKT0_EXT_WERT | HEX | high | unsigned char | - | - | - | - | - | von INFO_EWS eingelesener Zustand |
| STAT_FKT1_EXT_WERT | HEX | high | unsigned char | - | - | - | - | - | von INFO_EWS eingelesener Zustand |
| STAT_RESERVE | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_1 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_FREIE_SECRETKEYS0_WERT | HEX | high | unsigned char | - | - | - | - | - | Anzahl freier SecretKeys0 FE: Speicher-Ablage nicht begrenzt 0..n: Verbleibende Anzahl Speicher-ablagen |
| STAT_RESERVE_2 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_3 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_4 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_5 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_6 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_RESERVE_7 | 0-n | high | unsigned char | - | RESERVE | - | - | - | Reserve |
| STAT_VERSION | 0-n | high | unsigned char | - | VERSION | - | - | - | Version |

<a id="table-res-0xd9c9-d"></a>
### RES_0XD9C9_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Bit | high | BITFIELD | - | BF_LHM7_STRUCT | - | - | - | Aktive Limp Home Modes (49-52) |
| - | Bit | high | BITFIELD | - | BF_LHM6_STRUCT | - | - | - | Aktive Limp Home Modes (41-48) |
| - | Bit | high | BITFIELD | - | BF_LHM5_STRUCT | - | - | - | Aktive Limp Home Modes (33-40) |
| - | Bit | high | BITFIELD | - | BF_LHM4_STRUCT | - | - | - | Aktive Limp Home Modes (25-32) |
| - | Bit | high | BITFIELD | - | BF_LHM3_STRUCT | - | - | - | Aktive Limp Home Modes (17-24) |
| - | Bit | high | BITFIELD | - | BF_LHM2_STRUCT | - | - | - | Aktive Limp Home Modes (9-16) |
| - | Bit | high | BITFIELD | - | BF_LHM1_STRUCT | - | - | - | Aktive Limp Home Modes (1-8) |

<a id="table-res-0xda2e-d"></a>
### RES_0XDA2E_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ISTGANG | 0-n | high | unsigned char | - | TAB_ISTGANG | - | - | - | Eingelegter Gang im Getriebe: P, R, N, 0-8 |
| STAT_FAHRSTUFE | 0-n | high | unsigned char | - | TAB_FAHRSTUFE | - | - | - | Eingelegte Fahrstufe: P, R, N, D, M |

<a id="table-res-0xda65-d"></a>
### RES_0XDA65_D

Dimensions: 26 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SBW_CTR_PD_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung P nach D |
| STAT_SBW_CTR_PR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung P nach R |
| STAT_SBW_CTR_PN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung P nach N |
| STAT_SBW_CTR_RD_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung R nach D |
| STAT_SBW_CTR_RN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung R nach N |
| STAT_SBW_CTR_RP_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung R nach P |
| STAT_SBW_CTR_ND_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung N nach D |
| STAT_SBW_CTR_NR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung N nach R |
| STAT_SBW_CTR_NP_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung N nach P |
| STAT_SBW_CTR_DR_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung D nach R |
| STAT_SBW_CTR_DN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung D nach N |
| STAT_SBW_CTR_DP_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Auslesen Wert von Shift-by-Wire Zähler für Schaltung D nach P |
| STAT_SBW_CTR_AUTON_ROLLING_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Auto-N Rollen falsche Fahrtrichtung |
| STAT_SBW_CTR_AUTOP_LEAVE_CAR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Auto-P bei Fzg. Verlassen |
| STAT_SBW_CTR_BELT_DUMMY_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gurtdummyerkennung (Tür auf , Gurt gesteckt bei FB an und D/R) |
| STAT_SBW_CTR_CAR_WASH_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Waschtraßenzähler (N und SST) |
| STAT_SBW_CTR_DRIVING_READINESS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Fahrbereitschaftsverlustzähler (FB aus ohne SST) |
| STAT_SBW_CTR_AUTOPN_HOT_TRANSMISSION_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für Auto-P/N bei heißem Getriebe  |
| STAT_SBW_CTR_P_OVER_5KMH_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | P bei v&gt;5km/h |
| STAT_SBW_CTR_EGNER_OK_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | eGNER  erfolgreich |
| STAT_SBW_CTR_EGNER_MISUSE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | eGNER Missbrauch (Abschleppen Fahrzeug und P) |
| STAT_SBW_CTR_BRSYS_HLP_D_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Hilferuf Bremssystem in D |
| STAT_SBW_CTR_BRSYS_HLP_R_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Hilferuf Bremssystem in R |
| STAT_SBW_CTR_BRSYS_HLP_N_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Hilferuf Bremssystem in N |
| STAT_SBW_CTR_REJSHFTRQ_N_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Rücknahme Positionswunsch nach N |
| STAT_SBW_CTR_REJSHFTRQ_P_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Rücknahme Positionswunsch nach P |

<a id="table-res-0xf100-r"></a>
### RES_0XF100_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OPT_WERT | + | - | - | HEX | high | unsigned char | - | - | - | - | - | Routine Control Option |
| STAT_CODE_WERT | + | - | - | HEX | high | unsigned char | - | - | - | - | - | Routine Control Status |

<a id="table-res-0xf401-r"></a>
### RES_0XF401_R

Dimensions: 7 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REF_SD_POS_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_REF_SD_POS | - | - | - | Status Referenzschaltwalze-Position |
| STAT_SD1_ERROR_STATUS | - | - | + | 0-n | high | signed int | - | TAB_SD_ERROR_STATUS | - | - | - | Aktuator-Fehlerstatus- Schaltwalze 1 |
| STAT_SD2_ERROR_STATUS | - | - | + | 0-n | high | signed int | - | TAB_SD_ERROR_STATUS | - | - | - | Aktuator-Fehlerstatus- Schaltwalze 2 |
| STAT_SD1_REF_DRIVE_ERROR_STATUS | - | - | + | 0-n | high | signed int | - | TAB_REF_DRIVE_ERROR_STATUS | - | - | - | Referenzfahrt Fehlerstatus - Schalzwalze 1 |
| STAT_SD2_REF_DRIVE_ERROR_STATUS | - | - | + | 0-n | high | signed int | - | TAB_REF_DRIVE_ERROR_STATUS | - | - | - | Referenzfahrt Fehlerstatus - Schalzwalze 2 |
| STAT_SD1_ENCOD_ERROR | - | - | + | 0-n | high | signed int | - | TAB_ENCOD_ERROR | - | - | - | Inkrementalgeber Fehler - Schalzwalze 1 |
| STAT_SD2_ENCOD_ERROR | - | - | + | 0-n | high | signed int | - | TAB_ENCOD_ERROR | - | - | - | Inkrementalgeber Fehler - Schalzwalze 2 |

<a id="table-res-0xf402-r"></a>
### RES_0XF402_R

Dimensions: 5 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHFT_GEARS | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_SHFT_GEARS | - | - | - | Schaltgänge |
| STAT_STATUS_SHFT_GEARS_SD1_ARG | - | - | + | 0-n | high | signed int | - | TAB_TARGET_GEAR_SD1 | - | - | - | Schaltgänge: Kontrol-Parameter für Schaltwalze1 |
| STAT_STATUS_SHFT_GEARS_SD2_ARG | - | - | + | 0-n | high | signed int | - | TAB_TARGET_GEAR_SD2 | - | - | - | Schaltgänge: kontrol Parameter für Schaltwalze 2 |
| STAT_STATUS_SHFT_GEARS_DRB_IDX_SD1_ARG_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Fahr-Index von Schaltwalze 1 |
| STAT_STATUS_SHFT_GEARS_DRB_IDX_SD2_ARG_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Fahr-Index von Schaltwalze 2 |

<a id="table-res-0xf410-r"></a>
### RES_0XF410_R

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_TP_ADA | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CLU_TP_ADA | - | - | - | Status Kupplungsberührungspunkt-Adaption |
| STAT_CLU_TP_ADA_CLU1_WERT | - | - | + | mbar | high | signed int | - | - | 1000.0 | 512.0 | 0.0 | Berührungspunkt-Kupplung 1 |
| STAT_CLU_TP_ADA_CLU2_WERT | - | - | + | mbar | high | signed int | - | - | 1000.0 | 512.0 | 0.0 | Berührungspunkt-Kupplung 2 |

<a id="table-res-0xf411-r"></a>
### RES_0XF411_R

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_SELF_OPEN_TST | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CLU_SELF_OPEN_TST | - | - | - | Status Kupplung selbst offenen Test |
| STAT_CLU_SELF_OPEN_TST_REAL_DUR_WERT | - | - | + | ms | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Echtöffnungsdauer |
| STAT_CLU_SELF_OPEN_TST_MAX_PRS_WERT | - | - | + | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Clutch Selbst offenen Test; max.  Druck erreicht |

<a id="table-res-0xf413-r"></a>
### RES_0XF413_R

Dimensions: 8 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_PRS_CNTRL | - | - | + | 0-n | high | unsigned char | - | STATUS_CLU_PRS_CNTRL_TAB | - | - | - | Status Kupplungsdrucksteuerung |
| STAT_CLU_PRS_CNTRL_SHFT_GEAR_1 | - | - | + | 0-n | high | signed int | - | CLU_PRS_CNTRL_SHFT_GEAR_1_TAB | - | - | - | Kupplungsdrucksteuerung-Schaltgang 1 |
| STAT_CLU_PRS_CNTRL_SHFT_GEAR_2 | - | - | + | 0-n | high | signed int | - | STAT_CLU_PRS_CNTRL_SHFT_GEAR_2_TAB | - | - | - | Kupplungsdrucksteuerung-Schaltgang 2 |
| STAT_CLU_PRS_CNTRL_SHFT_IDX_SD_1_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Kupplungsdrucksteuerung-Schaltindex von Schaltwalze 1 |
| STAT_CLU_PRS_CNTRL_SHFT_IDX_SD_2_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Kupplungsdrucksteuerung-Schaltindex von Schaltwalze 2 |
| STAT_CLU_PRS_CNTRL_PRS_CAP_1_WERT | - | - | + | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Kupplungsaktuatordruck 1 |
| STAT_CLU_PRS_CNTRL_PRS_CAP_2_WERT | - | - | + | mbar | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Kupplungsaktuatordruck 2 |
| STAT_CLU_PRS_CNTRL_FLW_CCP_WERT | - | - | + | l/h | high | signed int | - | - | 60.0 | 1000.0 | 0.0 | flow Kupplungskühlung-Druck(CCP) |

<a id="table-res-0xf415-r"></a>
### RES_0XF415_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_SIM_PRS_CNTRL | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CLU_SIM_PRS_CNTRL | - | - | - | Status Kupplung gleichzeitigen Druckregelung |

<a id="table-res-0xf416-r"></a>
### RES_0XF416_R

Dimensions: 8 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_ACTU_PWM_CNTRL | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CLU_ACTU_PWM_CNTRL | - | - | - | Status Kupplungsaktuator PWM-Steuerung |
| STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1 | - | - | + | 0-n | high | signed int | - | TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1 | - | - | - | Schalt-Gang 1 |
| STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2 | - | - | + | 0-n | high | signed int | - | TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2 | - | - | - | Schalt-Gang 2 |
| STAT_CLU_ACTU_PWM_CNTRL_SHFT_IDX_SD_1_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Schalt-Index Schaltwalze1 |
| STAT_CLU_ACTU_PWM_CNTRL_SHFT_IDX_SD_2_WERT | - | - | + | - | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Schalt-Index Schaltwalze 2 |
| STAT_CLU_ACTU_PWM_CNTRL_CAP_1_WERT | - | - | + | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | PWM kupplungsaktuator-pumpe |
| STAT_CLU_ACTU_PWM_CNTRL_CAP_2_WERT | - | - | + | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | PWM kupplungsaktuator-pumpe2 |
| STAT_CLU_ACTU_PWM_CNTRL_CCP_WERT | - | - | + | % | high | signed int | - | - | 1.0 | 1.0 | 0.0 | PWM Kupplung-Kühlpumpe |

<a id="table-res-0xf417-r"></a>
### RES_0XF417_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CHECK_ISS_SENS | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CHECK_ISS_SENS | - | - | - | Statusprüfung Eingangswellendrehzahlsensoren |
| STAT_CHECK_ISS_SENS_STATUS | - | - | + | 0-n | high | signed int | - | TAB_CHECK_ISS_SENS_STATUS | - | - | - | Drehzahlsensor-Status |

<a id="table-res-0xf422-r"></a>
### RES_0XF422_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CLU_GAIN_ADA_RST_VALUES | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_CLU_GAIN_ADA_RST_VALUES | - | - | - | Status der Routine zum Zurücksetzen der Kupplungs-Gain-Adaptionswerte |

<a id="table-res-0xf432-r"></a>
### RES_0XF432_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CAP_SPD_2_PRS_ADA | - | - | + | 0-n | high | unsigned char | - | TAB_CAP_SPD_2_PRS_ADA | - | - | - | Kupplungsaktuator Speed2Pressure Adaption / Status |

<a id="table-sailing-mode"></a>
### SAILING_MODE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sailing deaktiviert |
| 0x01 | Sailing aktiviert, aber nicht aktiv |
| 0x02 | Statusänderung zu 'Sailing aktiv' |
| 0x03 | Sailing aktiv |
| 0x04 | Statusänderung zu 'Sailing inaktiv' |
| 0x0D | Signal nicht vorhanden |
| 0x0E | Error |
| 0x0F | Signal ungültig |
| 0xFF | Wert ungültig |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 115 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FS_LOESCHEN_PERMANENT | 0x1060 | - | Job zum Löschen der Permanent-DTCs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FEHLERSPEICHER_ENDE_WERKSABLAUF | 0x1061 | - | Löschen von Einzelfehlern und Permanent-DTCs unterbindet | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x1061_R |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| SHFT_MOT_1_ABS_POS | 0x4000 | STAT_SHFT_MOT_1_ABS_POS_WERT | shiftdrum motor 1 - absolute position | Nm | - | High | signed int | - | 1.0 | 16.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_1_REL_POS | 0x4001 | STAT_SHFT_MOT_1_REL_POS_WERT | Schaltwalzenmotor 1 - Relative Position (falls der Wert 2^31 überschreitet, wird er auf 0 zurück gesetzt) | Counts | - | High | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_1_SPD | 0x4002 | STAT_SHFT_MOT_1_SPD_WERT | Schaltwalzenmotor 1 - Geschwindigkeit | 1/min | - | High | signed long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_1_CUR | 0x4003 | STAT_SHFT_MOT_1_CUR_WERT | Schaltwalzenmotor 1 - Strom | A | - | High | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_1_VOLT | 0x4004 | STAT_SHFT_MOT_1_VOLT_WERT | Schaltwalzenmotor 1 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| TSL_OPERATION_DATA | 0x4005 | - | Statistic Data | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4005_D |
| RAM_DATEN_SCHREIBEN | 0x4006 | - | Dient dazu während der Inbetriebnahme angelernte applikative Daten in den nichtflüchtigen Speicher zu sichern. | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x4006_R |
| AGS_STATUS_INFO | 0x4006 | - | AGs Status Informationen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4006_D |
| IUMPR_DATA | 0x4007 | - | IUMPR Daten der OBD Dtcs | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4007_D |
| TSL_CLU_OPERATION_DATA | 0x4008 | - | Betriebsdaten der Kupplungen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4008_D |
| CLU_ADAPTION_VALUES | 0x4009 | - | Kupplung Adaptionswerte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4009_D |
| OPERATION_DATA | 0x400A | - | Diagnostic Interface um die Operation Statistic Daten und statistische Daten der Kupplung zurückzusetzen. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x400A_D | - |
| SHFT_MOT_2_ABS_POS | 0x4010 | STAT_SHFT_MOT_2_ABS_POS_WERT | Schaltwalzenmotor 2 - Absolute Position | Nm | - | High | signed int | - | 1.0 | 16.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_2_REL_POS | 0x4011 | STAT_SHFT_MOT_2_REL_POS_WERT | Schaltwalzenmotor 2 - Relative Position (falls der Wert 2^31 überschreitet, wird er auf 0 zurück gesetzt) | Counts | - | High | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_2_SPD | 0x4012 | STAT_SHFT_MOT_2_SPD_WERT | Schaltwalzenmotor 2 - Geschwindigkeit | 1/min | - | High | signed long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_2_CUR | 0x4013 | STAT_SHFT_MOT_2_CUR_WERT | Schaltwalzenmotor 2 - Strom | A | - | High | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| SHFT_MOT_2_VOLT | 0x4014 | STAT_SHFT_MOT_2_VOLT_WERT | Schaltwalzenmotor 2 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_1_SPD | 0x4020 | STAT_CLU_MOT_1_SPD_WERT | Kupplungsmotor 1 - Geschwindigkeit | 1/min | - | High | signed int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_1_CUR | 0x4021 | STAT_CLU_MOT_1_CUR_WERT | Kupplungsmotor 1 - Strom | A | - | High | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_1_VOLT | 0x4022 | STAT_CLU_MOT_1_VOLT_WERT | Kupplungsmotor 1 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_2_SPD | 0x4030 | STAT_CLU_MOT_2_SPD_WERT | Kupplungsmotor 2 - Geschwindigkeit | 1/min | - | High | signed int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_2_CUR | 0x4031 | STAT_CLU_MOT_2_CUR_WERT | Kupplungsmotor 2 - Strom | A | - | High | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_2_VOLT | 0x4032 | STAT_CLU_MOT_2_VOLT_WERT | Kupplungsmotor 2 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_COOL_SPD | 0x4040 | STAT_CLU_MOT_COOL_SPD_WERT | Kupplungsmotor Kühlung - Geschwindigkeit | 1/min | - | High | signed int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_COOL_CUR | 0x4041 | STAT_CLU_MOT_COOL_CUR_WERT | Kupplungsmotor Kühlung - Strom | A | - | High | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| CLU_MOT_COOL_VOLT | 0x4042 | STAT_CLU_MOT_COOL_VOLT_WERT | Kupplungsmotor Kühlung - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| PRS_SENS_CLU_1_SIG | 0x4050 | STAT_PRS_SENS_CLU_1_SIG_WERT | Drucksensor Kupplung 1 - Signal | - | - | High | signed int | - | 1.0 | 512.0 | 0.0 | - | 22 | - | - |
| PRS_SENS_CLU_1_VOLT | 0x4051 | STAT_PRS_SENS_CLU_1_VOLT_WERT | Drucksensor Kupplung 1 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| PRS_SENS_CLU_2_SIG | 0x4060 | STAT_PRS_SENS_CLU_2_SIG_WERT | Drucksensor Kupplung 2 - Signal | - | - | High | signed int | - | 1.0 | 512.0 | 0.0 | - | 22 | - | - |
| PRS_SENS_CLU_2_VOLT | 0x4061 | STAT_PRS_SENS_CLU_2_VOLT_WERT | Drucksensor Kupplung 2 - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| SPD_SENS_ISS_1_SIG | 0x4070 | STAT_SPD_SENS_ISS_1_SIG_WERT | Geschwindigkeitsensor Eingangswelle 1 - Signal | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| SPD_SENS_ISS_1_VOLT | 0x4071 | STAT_SPD_SENS_ISS_1_VOLT_WERT | Geschwindigkeitsensor Eingangswelle 1- Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| SPD_SENS_ISS_2_SIG | 0x4080 | STAT_SPD_SENS_ISS_2_SIG_WERT | Geschwindigkeitsensor Eingangswelle 2 - Signal | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| SPD_SENS_ISS_2_VOLT | 0x4081 | STAT_SPD_SENS_ISS_2_VOLT_WERT | Geschwindigkeitsensor Eingangswelle 2- Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| TEMP_SENS_SIG | 0x40A0 | STAT_TEMP_SENS_SIG_WERT | Temperatursensor - Signal | °C | - | High | signed int | - | 1.0 | 4.0 | 0.0 | - | 22 | - | - |
| TEMP_SENS_VOLT | 0x40A1 | STAT_TEMP_SENS_VOLT_WERT | Temperatursensor - Versorgungsspannung | V | - | High | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22 | - | - |
| HIGH_VOLT | 0x40B0 | STAT_HIGH_VOLT_WERT | Hochleistungsspannung | V | - | High | unsigned int | - | 1.0 | 512.0 | 0.0 | - | 22 | - | - |
| LOW_VOLT | 0x40B1 | STAT_LOW_VOLT_WERT | Niederleistungsspannung | V | - | High | unsigned int | - | 1.0 | 512.0 | 0.0 | - | 22 | - | - |
| SHFT_LEV_POS | 0x40C0 | STAT_SHFT_LEV_POS | Position Gangwahlschalter | 0-n | - | High | unsigned char | SHFT_LEV_POS_TABLE | - | - | - | - | 22 | - | - |
| SHFT_LEV_DSPL_VAL | 0x40C1 | STAT_SHFT_LEV_DSPL_VAL | Anzeigewert Gangwahlschalter | 0-n | - | High | unsigned char | SHFT_LEV_DSPL_VAL_TABLE | - | - | - | - | 22 | - | - |
| FOOT_BRK_STATE | 0x40D2 | STAT_FOOT_BRK_STATE | Status Bremspedal | 0-n | - | High | unsigned char | FOOT_BRK_STATE_TABLE | - | - | - | - | 22 | - | - |
| ENG_TQ_STATIC | 0x40F1 | STAT_ENG_TQ_STATIC_WERT | Drehmoment - statisch | Nm | - | High | signed int | - | 1.0 | 8.0 | 0.0 | - | 22 | - | - |
| ENG_TQ_EXP | 0x40F2 | STAT_ENG_TQ_EXP_WERT | Drehmoment - erwartet | Nm | - | High | signed int | - | 1.0 | 8.0 | 0.0 | - | 22 | - | - |
| CC_STATE | 0x40F4 | STAT_CC_STATE | Status Geschwindigkeitsregelanlage | 0-n | - | High | unsigned char | TABLE_CC_STATE | - | - | - | - | 22 | - | - |
| PED_POS | 0x40F5 | STAT_PED_POS_WERT | Fahrpedalstellung | % | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| HND_BRK_STATE | 0x40F6 | - | Status Handbremse | Bit | - | High | BITFIELD | BF_HND_BRK_STATE_BIT_STRUCT | - | - | - | - | 22 | - | - |
| ENG_CRNK_ENA | 0x40FA | STAT_ENG_CRNK_ENA | Motorstart Erlaubnis | 0-n | - | High | unsigned char | ENG_CRNK_ENA_TABLE | - | - | - | - | 22 | - | - |
| PED_POS_RAW | 0x40FB | STAT_PED_POS_RAW_WERT | Fahrpedalstellung - Rohwert | % | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| WHL_SPD_FR | 0x40FC | STAT_WHL_SPD_FR_WERT | Raddrehzahl - vorne rechts | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| WHL_SPD_FL | 0x40FD | STAT_WHL_SPD_FL_WERT | Raddrehzahl - vorne links | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| WHL_SPD_RR | 0x40FE | STAT_WHL_SPD_RR_WERT | Raddrehzahl - hinten rechts | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| WHL_SPD_RL | 0x40FF | STAT_WHL_SPD_RL_WERT | Raddrehzahl - hinten links | 1/min | - | High | signed int | - | 1.0 | 2.0 | 0.0 | - | 22 | - | - |
| ESP_STATE | 0x4101 | - | ESP Status | Bit | - | High | BITFIELD | BF_ESP_STATE_STRUCT | - | - | - | - | 22 | - | - |
| VEH_VEL_CAN | 0x4102 | STAT_VEH_VEL_CAN_WERT | Fahrzeuggeschwindigkeit CAN | km/h | - | High | signed int | - | 1.0 | 16.0 | 0.0 | - | 22 | - | - |
| UND_AXLE_SPD | 0x4103 | STAT_UND_AXLE_SPD_WERT | Geschwindigkeit nicht angetriebene Achse | 1/min | - | High | signed int | - | 1.0 | 8.0 | 0.0 | - | 22 | - | - |
| OUS_SPD | 0x4104 | STAT_OUS_SPD_WERT | Geschwindigkeit Abtriebswelle | 1/min | - | High | signed int | - | 1.0 | 8.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_R | 0x4111 | STAT_GEAR_ENGAGE_ERR_CNT_R_DATA | Zähler Gangeinlegefehler R | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_1 | 0x4112 | STAT_GEAR_ENGAGE_ERR_CNT_1_DATA | Zähler Gangeinlegefehler 1 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_2 | 0x4113 | STAT_GEAR_ENGAGE_ERR_CNT_2_DATA | Zähler Gangeinlegefehler 2 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_3 | 0x4114 | STAT_GEAR_ENGAGE_ERR_CNT_3_DATA | Zähler Gangeinlegefehler 3 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_4 | 0x4115 | STAT_GEAR_ENGAGE_ERR_CNT_4_DATA | Zähler Gangeinlegefehler 4 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_5 | 0x4116 | STAT_GEAR_ENGAGE_ERR_CNT_5_DATA | Zähler Gangeinlegefehler 5 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_6 | 0x4117 | STAT_GEAR_ENGAGE_ERR_CNT_6_DATA | Zähler Gangeinlegefehler 6 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_ENGAGE_ERR_CNT_7 | 0x4118 | STAT_GEAR_ENGAGE_ERR_CNT_7_DATA | Zähler Gangeinlegefehler 7 | DATA | - | High | data[1] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| GEAR_INFO | 0x4135 | STAT_GEAR_INFORMATION | Gang Information | 0-n | - | High | unsigned int | CLU_MOT_COOL_SPD_CONVERSION | - | - | - | - | 22 | - | - |
| PED_POS_RATE | 0x4139 | STAT_PED_POS_RATE_WERT | Fahrpedalstellung - Änderungsrate | %/s | - | High | signed char | - | 10.0 | 1.0 | 0.0 | - | 22 | - | - |
| VEH_ACC | 0x413A | STAT_VEH_ACC_WERT | Fahrzeugbeschleunigung | g | - | High | signed int | - | 1.0 | 1024.0 | 0.0 | - | 22 | - | - |
| RC_STRT_ODO | 0x413C | - | Rennstart - Odometer | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x413C_D |
| MECH_DATA | 0x4141 | - | Mechanische Daten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4141_D |
| TSL_GEAR_CNT | 0x4142 | - | TSL Gangzähler | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x4142_D | RES_0x4142_D |
| TSL_CLU_CNT | 0x4143 | - | TSL Kupplungszähler | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x4143_D | RES_0x4143_D |
| GEAR_DAT_PART_1 | 0x4144 | - | Gang Daten (Teil 1) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4144_D |
| GEAR_DAT_PART_2 | 0x4145 | - | Gang Daten (Teil 2) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4145_D |
| GEAR_DAT_PART_3 | 0x4146 | - | Gang Daten (Teil 3) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4146_D |
| L2S_CNT_DAT | 0x4148 | - | Level 2 SW Zähler Daten | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x4148_D | RES_0x4148_D |
| ISS_DATA | 0x4149 | - | ISS Daten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4149_D |
| TCU_TEMP | 0x4205 | STAT_TCU_TEMP_WERT | TCU / EGS Temperatur | °C | - | High | signed int | - | 1.0 | 4.0 | 0.0 | - | 22 | - | - |
| CUR_GEAR | 0x4211 | STAT_CUR_GEAR_WERT | Aktueller Gang | count | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_DEVICE_STATE_SAMPLE_LEVEL | 0x4300 | - | Status device state and sample level | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4300_D |
| STATUS_ANFAHREN | 0x4301 | - | Status des Anfahrens | Bit | - | High | BITFIELD | BF_LAUNCH_STATE | - | - | - | - | 22 | - | - |
| OILSCHADENSMODEL_RUECKSETZEN | 0x4310 | - | Öl-Schadensmodel zurücksetzen | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4310_D | - |
| OILSCHADENSMODEL_LAUFLEISTUNG | 0x4311 | STAT_OILSCHADENSMODEL_LAUFLEISTUNG_WERT | Laufleistung der Diagnose des Öl-Schadensmodel | km | - | High | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| IDR_EGS | 0x4312 | - | IDR-Daten für EGS | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x4312_D | RES_0x4312_D |
| SET_CLUTCH_RUN_IN_STATE | 0x4313 | - | Einlaufstatus der Kupplung setzen | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4313_D | - |
| DRAG_INDICATOR_PARAMETER | 0x4314 | - | Schleppzeigerdaten Rücksetzten | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x4314_D | RES_0x4314_D |
| STATUS_EWS | 0xC000 | - | Steuergeräte interner Zustand der EWS Funktion | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xC000_D |
| STEUERN_EWS4_SK | 0xC001 | - | EWS4-data schreiben | - | - | - | - | - | - | - | - | - | 2E | ARG_0xC001_D | - |
| STATUS_EWS4_KF | 0xC003 | STAT_KF_DATA | Rohdaten des KF | DATA | - | High | data[128] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| ERSATZMASSNAHMEN_AKTIV | 0xD9C9 | - | Auslesen der aktiven Ersatzmaßnahmen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9C9_D |
| _STEUERN_LL_SEGELN_ROLLE_OEKO_INNO_NACHWEIS | 0xD9CA | - | Segeln im Rollenbetrieb aktivieren und deaktivieren | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD9CA_D | - |
| _STATUS_LL_SEGELN_ROLLE_OEKO_INNO_NACHWEIS | 0xD9CB | STAT_SEGELN_ROLLE | aktueller Status der Segeln-Funktion: 0x00: Segeln aktiv 0x01: Segeln inaktiv | 0-n | - | High | unsigned char | TAB_STATUS_SEGELN_ROLLE | - | - | - | - | 22 | - | - |
| STEUERN_LERNFKT_RUECKSETZEN | 0xDA15 | - | Rücksetzen der Lernfunktion | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDA15_D | - |
| ISTGANG | 0xDA2E | - | Aktuell eingelegter Gang | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDA2E_D |
| WUC_COUNTER | 0xDA63 | STAT_WUC_COUNTER_WERT | Warm Up Cycle (WUC) Zähler | - | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SBW_COUNTER | 0xDA65 | - | Auslesen der Shift-by-Wire Zähler | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDA65_D |
| AUTO_P_DEACTIVATE | 0xDA66 | - | Deaktivieren von Auto-P bei KL15_Aus / bei PWF-Zustandswechsel-Funktion | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDA66_D | - |
| AUTO_P_DEACTIVATE_STATUS | 0xDA67 | STAT_AUTO_P_DEACTIVATE | Status von Auto-P Deaktivieren. Siehe Tabelle TAB_AUTOP_DEACTIVATION_STAT | 0-n | - | High | unsigned char | TAB_AUTOP_DEACTIVATION_STAT | - | - | - | - | 22 | - | - |
| SHIFT_P | 0xDA68 | - | Gang P ein- und auslegen | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDA68_D | - |
| EWS_FSC | 0xF100 | - | DID zum schreiben und prüfen des FSC für EWS | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF100_R | RES_0xF100_R |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| REF_SD_POS | 0xF401 | - | reference shiftdrum position | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF401_R |
| SHFT_GEARS | 0xF402 | - | shift gears | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF402_R | RES_0xF402_R |
| CLU_TP_ADA | 0xF410 | - | clutch touchpoint adaption | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF410_R | RES_0xF410_R |
| CLU_SELF_OPEN_TST | 0xF411 | - | clutch self open test | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF411_R | RES_0xF411_R |
| CLU_PRS_CNTRL | 0xF413 | - | clutch pressure control | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF413_R | RES_0xF413_R |
| CLU_SIM_PRS_CNTRL | 0xF415 | - | clutch simultaneous pressure control | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF415_R | RES_0xF415_R |
| CLU_ACTU_PWM_CNTRL | 0xF416 | - | clutch actuator pwm control | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF416_R | RES_0xF416_R |
| CHECK_ISS_SENS | 0xF417 | - | check input shaft speed sensors | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF417_R |
| CLU_GAIN_ADA_RST_VALUES | 0xF422 | - | Kupplung-Gain-Adaptionswerte zurücksetzen | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF422_R |
| CAP_SPD_2_PRS_ADA | 0xF432 | - | Kupplungsaktuator Speed2Pressure-Adaption | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF432_R |

<a id="table-shft-lev-dspl-val-table"></a>
### SHFT_LEV_DSPL_VAL_TABLE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Undefiniert |
| 0x01 | Position P |
| 0x02 | Position R |
| 0x03 | Position N |
| 0x04 | Position D |
| 0x05 | Position M |
| 0x06 | Position L |
| 0xFF | Wert ungültig |

<a id="table-shft-lev-pos-table"></a>
### SHFT_LEV_POS_TABLE

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Undefiniert |
| 0x01 | Position P |
| 0x02 | Position R |
| 0x03 | Position N |
| 0x04 | Position D |
| 0x05 | Position M |
| 0x06 | Position L |
| 0x07 | Error |
| 0x08 | Undefinierter Übergang |
| 0x11 | Übergang PR |
| 0xFF | Wert ungültig |
| 0x12 | Übergang RN |
| 0x13 | Übergang ND |
| 0x14 | Übergang DL |

<a id="table-status-clu-prs-cntrl-tab"></a>
### STATUS_CLU_PRS_CNTRL_TAB

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett Fehler |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-status-ram-daten-schreiben-tab"></a>
### STATUS_RAM_DATEN_SCHREIBEN_TAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Schreiben erfolgreich |
| 0x01 | Schreiben  fehlgeschlagen |
| 0x02 | Schreiben läuft |
| 0x03 | Schreiben noch nicht angestoßen (Routine nicht gestartet) |

<a id="table-stat-clu-prs-cntrl-shft-gear-2-tab"></a>
### STAT_CLU_PRS_CNTRL_SHFT_GEAR_2_TAB

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x63 | Park |
| 09 | Rückwärtsgang |
| 0x10 | Leerlauf-Rückwärtsgang-2 |
| 0x02 | Gang 2 |
| 0x11 | Leerlauf 2-4 |
| 0x04 | Gang 4 |
| 0x12 | Leerlauf 4-6 |
| 0x06 | Gang 6 |
| 0xFFFF | Wert ungültig |

<a id="table-steuern-clu-prs-cntrl-shft-gear-1-arg-tab"></a>
### STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_1_ARG_TAB

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Gang1 |
| 0x0D | Leerlauf: Neutral 1-3 |
| 0x03 | Gang3 |
| 0x0E | Leerlauf: Neutral 3-5 |
| 0x05 | Gang5 |
| 0x0F | Leerlauf: Neutral 5-7 |
| 0x07 | Gang7 |

<a id="table-steuern-clu-prs-cntrl-shft-gear-2-arg-tab"></a>
### STEUERN_CLU_PRS_CNTRL_SHFT_GEAR_2_ARG_TAB

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x63 | P |
| 09 | GR |
| 0x10 | NR-2 |
| 0x02 | G2 |
| 0x11 | N2-4 |
| 0x04 | G4 |
| 0x12 | N4-6 |
| 0x06 | G6 |

<a id="table-table-cc-state"></a>
### TABLE_CC_STATE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | inaktiv |
| 0x01 | überschrieben |
| 0x02 | aktiv |
| 0xFF | Wert ungültig |

<a id="table-table-msa-state"></a>
### TABLE_MSA_STATE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MSA aktiviert |
| 0x01 | MSA deaktiviert |
| 0x03 | Signal ungültig |
| 0xFF | Wert ungültig |

<a id="table-table-request-msa-shutoff"></a>
### TABLE_REQUEST_MSA_SHUTOFF

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MSA kein Request |
| 0x01 | MSA verhindert Abschaltung Motor |
| 0xFF | Wert ungültig |

<a id="table-table-shift-logic-diagnostic"></a>
### TABLE_SHIFT_LOGIC_DIAGNOSTIC

Dimensions: 19 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DS2_XE |
| 0x01 | DS2_E |
| 0x02 | DS2_S |
| 0x03 | DS2_XS |
| 0x04 | DS2_A1 |
| 0x05 | DS2_A2 |
| 0x06 | DS2_A3 |
| 0x07 | DS2_A4 |
| 0x08 | DS2_STEPTR |
| 0x09 | DS2_SO |
| 0x0A | DS2_B0 |
| 0x0B | DS2_LM |
| 0x0C | DS2_HM |
| 0x0D | DS2_WL |
| 0x0E | DS2_LD |
| 0x0F | DS2_ACC |
| 0x10 | DS2_A5 |
| 0xFFFF | Wert ungültig |
| 0x11 | DS2_TMS |

<a id="table-tab-autop-deactivation"></a>
### TAB_AUTOP_DEACTIVATION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Aktion |
| 0x01 | Auto-P deaktivieren |
| 0x02 | Auto-P aktivieren |

<a id="table-tab-autop-deactivation-stat"></a>
### TAB_AUTOP_DEACTIVATION_STAT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Auto-P aktiv |
| 0x01 | Auto-P inaktiv |
| 0xFF | Ungültiger Wert |

<a id="table-tab-cap-spd-2-prs-ada"></a>
### TAB_CAP_SPD_2_PRS_ADA

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-check-iss-sens-status"></a>
### TAB_CHECK_ISS_SENS_STATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Routine beendet und Sensor ok |
| 0x06 | Zustand Fehler |
| 0x07 | Eingriffsfehlerleerlauf |
| 0x08 | Fehler beim Schließen beider Kupplungen |
| 0x09 | Geschwindigkeitssensor 1 Fehler |
| 0x0A | Geschwindigkeitssensor 2 Fehler |
| 0x0B | Geschwindigkeitssensor 1 und 2 Fehler |
| 0xFFFF | Wert ungültig |

<a id="table-tab-clu-actu-pwm-cntrl-shft-gear-1-arg"></a>
### TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1_ARG

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Gang-1 |
| 0x0D | Leerlauf 1-3 (N1-3) |
| 0x03 | Gang-3 |
| 0x0E | Leerlauf 3-5 (N3-5) |
| 0x05 | Gang-5 |
| 0x0F | Leerlauf 5-7 (N5-7) |
| 0x07 | Gang-7 |

<a id="table-tab-clu-actu-pwm-cntrl-shft-gear-2-arg"></a>
### TAB_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2_ARG

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x63 | Parking-Position (P) |
| 09 | Rückwärtsgang (GR) |
| 0x10 | Leerlauf-Rückwärts(NR-2) |
| 0x02 | Gang-2 |
| 0x11 | Leerlauf 2-4(N2-4) |
| 0x04 | Gang-4 |
| 0x12 | Leerlauf 4-6(N4-6) |
| 0x06 | Gang-6 |

<a id="table-tab-dez-values"></a>
### TAB_DEZ_VALUES

Dimensions: 256 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0 |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | 5 |
| 0x06 | 6 |
| 0x07 | 7 |
| 0x08 | 8 |
| 0x09 | 9 |
| 0x0A | 10 |
| 0x0B | 11 |
| 0x0C | 12 |
| 0x0D | 13 |
| 0x0E | 14 |
| 0x0F | 15 |
| 0x10 | 16 |
| 0x11 | 17 |
| 0x12 | 18 |
| 0x13 | 19 |
| 0x14 | 20 |
| 0x15 | 21 |
| 0x16 | 22 |
| 0x17 | 23 |
| 0x18 | 24 |
| 0x19 | 25 |
| 0x1A | 26 |
| 0x1B | 27 |
| 0x1C | 28 |
| 0x1D | 29 |
| 0x1E | 30 |
| 0x1F | 31 |
| 0x20 | 32 |
| 0x21 | 33 |
| 0x22 | 34 |
| 0x23 | 35 |
| 0x24 | 36 |
| 0x25 | 37 |
| 0x26 | 38 |
| 0x27 | 39 |
| 0x28 | 40 |
| 0x29 | 41 |
| 0x2A | 42 |
| 0x2B | 43 |
| 0x2C | 44 |
| 0x2D | 45 |
| 0x2E | 46 |
| 0x2F | 47 |
| 0x30 | 48 |
| 0x31 | 49 |
| 0x32 | 50 |
| 0x33 | 51 |
| 0x34 | 52 |
| 0x35 | 53 |
| 0x36 | 54 |
| 0x37 | 55 |
| 0x38 | 56 |
| 0x39 | 57 |
| 0x3A | 58 |
| 0x3B | 59 |
| 0x3C | 60 |
| 0x3D | 61 |
| 0x3E | 62 |
| 0x3F | 63 |
| 0x40 | 64 |
| 0x41 | 65 |
| 0x42 | 66 |
| 0x43 | 67 |
| 0x44 | 68 |
| 0x45 | 69 |
| 0x46 | 70 |
| 0x47 | 71 |
| 0x48 | 72 |
| 0x49 | 73 |
| 0x4A | 74 |
| 0x4B | 75 |
| 0x4C | 76 |
| 0x4D | 77 |
| 0x4E | 78 |
| 0x4F | 79 |
| 0x50 | 80 |
| 0x51 | 81 |
| 0x52 | 82 |
| 0x53 | 83 |
| 0x54 | 84 |
| 0x55 | 85 |
| 0x56 | 86 |
| 0x57 | 87 |
| 0x58 | 88 |
| 0x59 | 89 |
| 0x5A | 90 |
| 0x5B | 91 |
| 0x5C | 92 |
| 0x5D | 93 |
| 0x5E | 94 |
| 0x5F | 95 |
| 0x60 | 96 |
| 0x61 | 97 |
| 0x62 | 98 |
| 0x63 | 99 |
| 0x64 | 100 |
| 0x65 | 101 |
| 0x66 | 102 |
| 0x67 | 103 |
| 0x68 | 104 |
| 0x69 | 105 |
| 0x6A | 106 |
| 0x6B | 107 |
| 0x6C | 108 |
| 0x6D | 109 |
| 0x6E | 110 |
| 0x6F | 111 |
| 0x70 | 112 |
| 0x71 | 113 |
| 0x72 | 114 |
| 0x73 | 115 |
| 0x74 | 116 |
| 0x75 | 117 |
| 0x76 | 118 |
| 0x77 | 119 |
| 0x78 | 120 |
| 0x79 | 121 |
| 0x7A | 122 |
| 0x7B | 123 |
| 0x7C | 124 |
| 0x7D | 125 |
| 0x7E | 126 |
| 0x7F | 127 |
| 0x80 | 128 |
| 0x81 | 129 |
| 0x82 | 130 |
| 0x83 | 131 |
| 0x84 | 132 |
| 0x85 | 133 |
| 0x86 | 134 |
| 0x87 | 135 |
| 0x88 | 136 |
| 0x89 | 137 |
| 0x8A | 138 |
| 0x8B | 139 |
| 0x8C | 140 |
| 0x8D | 141 |
| 0x8E | 142 |
| 0x8F | 143 |
| 0x90 | 144 |
| 0x91 | 145 |
| 0x92 | 146 |
| 0x93 | 147 |
| 0x94 | 148 |
| 0x95 | 149 |
| 0x96 | 150 |
| 0x97 | 151 |
| 0x98 | 152 |
| 0x99 | 153 |
| 0x9A | 154 |
| 0x9B | 155 |
| 0x9C | 156 |
| 0x9D | 157 |
| 0x9E | 158 |
| 0x9F | 159 |
| 0xA0 | 160 |
| 0xA1 | 161 |
| 0xA2 | 162 |
| 0xA3 | 163 |
| 0xA4 | 164 |
| 0xA5 | 165 |
| 0xA6 | 166 |
| 0xA7 | 167 |
| 0xA8 | 168 |
| 0xA9 | 169 |
| 0xAA | 170 |
| 0xAB | 171 |
| 0xAC | 172 |
| 0xAD | 173 |
| 0xAE | 174 |
| 0xAF | 175 |
| 0xB0 | 176 |
| 0xB1 | 177 |
| 0xB2 | 178 |
| 0xB3 | 179 |
| 0xB4 | 180 |
| 0xB5 | 181 |
| 0xB6 | 182 |
| 0xB7 | 183 |
| 0xB8 | 184 |
| 0xB9 | 185 |
| 0xBA | 186 |
| 0xBB | 187 |
| 0xBC | 188 |
| 0xBD | 189 |
| 0xBE | 190 |
| 0xBF | 191 |
| 0xC0 | 192 |
| 0xC1 | 193 |
| 0xC2 | 194 |
| 0xC3 | 195 |
| 0xC4 | 196 |
| 0xC5 | 197 |
| 0xC6 | 198 |
| 0xC7 | 199 |
| 0xC8 | 200 |
| 0xC9 | 201 |
| 0xCA | 202 |
| 0xCB | 203 |
| 0xCC | 204 |
| 0xCD | 205 |
| 0xCE | 206 |
| 0xCF | 207 |
| 0xD0 | 208 |
| 0xD1 | 209 |
| 0xD2 | 210 |
| 0xD3 | 211 |
| 0xD4 | 212 |
| 0xD5 | 213 |
| 0xD6 | 214 |
| 0xD7 | 215 |
| 0xD8 | 216 |
| 0xD9 | 217 |
| 0xDA | 218 |
| 0xDB | 219 |
| 0xDC | 220 |
| 0xDD | 221 |
| 0xDE | 222 |
| 0xDF | 223 |
| 0xE0 | 224 |
| 0xE1 | 225 |
| 0xE2 | 226 |
| 0xE3 | 227 |
| 0xE4 | 228 |
| 0xE5 | 229 |
| 0xE6 | 230 |
| 0xE7 | 231 |
| 0xE8 | 232 |
| 0xE9 | 233 |
| 0xEA | 234 |
| 0xEB | 235 |
| 0xEC | 236 |
| 0xED | 237 |
| 0xEE | 238 |
| 0xEF | 239 |
| 0xF0 | 240 |
| 0xF1 | 241 |
| 0xF2 | 242 |
| 0xF3 | 243 |
| 0xF4 | 244 |
| 0xF5 | 245 |
| 0xF6 | 246 |
| 0xF7 | 247 |
| 0xF8 | 248 |
| 0xF9 | 249 |
| 0xFA | 250 |
| 0xFB | 251 |
| 0xFC | 252 |
| 0xFD | 253 |
| 0xFE | 254 |
| 0xFF | 255 |

<a id="table-tab-drm-info-state"></a>
### TAB_DRM_INFO_STATE

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | DRM_INFO_UDEF |
| 0x1 | DRM_INFO_DRIVELINE_OPEN |
| 0x2 | DRM_INFO_DRIVELINE_OPENING |
| 0x3 | DRM_INFO_SLIP_CONTROL |
| 0x4 | DRM_INFO_SPD_CONTROL |
| 0x5 | DRM_INFO_TQ_FOLLOW_UP |
| 0x6 | DRM_INFO_LAUNCH |
| 0x7 | DRM_INFO_SHIFT |
| 0x8 | DRM_INFO_LAUNCH_SHIFT |
| 0x9 | DRM_INFO_TOW_START |
| 0xA | DRM_INFO_CREEP |
| 0xB | DRM_INFO_CREEP_SHIFT |
| 0xC | DRM_INFO_STOP_START |
| 0xD | DRM_INFO_STARTUP |
| 0xE | DRM_INFO_SHUTDOWN |
| 0xF | DRM_INFO_DIAG |
| 0xFF | Wert ungültig |

<a id="table-tab-eeprom-status"></a>
### TAB_EEPROM_STATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | L2S_VALID_EEPROM_DATA |
| 0x02 | L2S_EEPROM_DATA_OLD_ERR |
| 0x03 | L2S_EEPROM_DATA_CRC_ERR |
| 0x04 | L2S_EEPROM_DATA_REV_ERR |
| 0x05 | L2S_VALID_NVRAM_DATA |
| 0x06 | L2S_NVRAM_DATA_FIDDLED |
| 0x07 | L2S_CTR_TEST_FAILED |
| 0x08 | L2S_VALID_EOL_DATA |

<a id="table-tab-encod-error"></a>
### TAB_ENCOD_ERROR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Init |
| 0x02 | Einstellwert vom Encoder ist im ungültigen Bereich |
| 0x03 | Wert vom Encoder übersteigt oberen Schwellwert |
| 0x04 | Wert vom Encoder übersteigt unteren Schwellwert |
| 0x05 | Winkelgeschwindigkeit ist im ungültigen Bereich |
| 0x06 | Bewegung in falsche  Richtung |
| 0x07 | Inkrementalgeber Hardware-Fehler |
| 0xFFFF | Wert ungültig |

<a id="table-tab-eng-state"></a>
### TAB_ENG_STATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ENGINE_STOPPED |
| 0x01 | ENGINE_DRIVEN |
| 0x02 | ENGINE_RUNNING |
| 0x05 | ENGINE_UNDEFINED |
| 0xFF | Wert ungültig |

<a id="table-tab-ews-mode-arg"></a>
### TAB_EWS_MODE_ARG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x07 | M7: Unlock & delete Client-SK mit SK |
| 0x11 | M17: Unlock & delete Client-SK mit Hash (SK |

<a id="table-tab-fahrstufe"></a>
### TAB_FAHRSTUFE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | P - parken |
| 0x01 | R - rückwärts |
| 0x02 | N - neutral |
| 0x03 | D - dauer |
| 0x04 | M - manuelle Schaltgasse |
| 0xFF | ungültiger Wert |

<a id="table-tab-gen-status"></a>
### TAB_GEN_STATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GEN_SIG_INIT |
| 0x01 | GEN_SIG_VALID |
| 0x02 | GEN_SIG_SUBSTITUTED |
| 0x03 | GEN_SIG_ERR_DEB |
| 0x04 | GEN_SIG_ERROR |
| 0xFF | Wert ungültig |

<a id="table-tab-imo-key-cond"></a>
### TAB_IMO_KEY_COND

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Init |
| 0x01 | Schlüssel ungültig |
| 0x02 | Schlüsselsuche aktiv |
| 0x03 | Schlüssel gültig im AR erkannt |
| 0x04 | Schlüssel gültig im IR erkannt |
| 0x05 | Schlüssel im 10 s - Nachlauf |
| 0x06 | Schlüssel gültig für MFS |
| 0x07 | Reserve |
| 0x08 | Reserve |
| 0x09 | Reserve |
| 0x0A | Reserve |
| 0x0B | Reserve |
| 0x0C | Reserve |
| 0x0D | Reserve |
| 0x0E | Reserve |
| 0x0F | Signal ungültig |
| 0xFF | Wert ungültig |

<a id="table-tab-istgang"></a>
### TAB_ISTGANG

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | P - parken |
| 0x01 | R - rückwärts |
| 0x02 | N - neutral |
| 0x03 | Gang 1 |
| 0x04 | Gang 2 |
| 0x05 | Gang 3 |
| 0x06 | Gang 4 |
| 0x07 | Gang 5 |
| 0x08 | Gang 6 |
| 0x09 | Gang 7 |
| 0x10 | Gang 8 |
| 0xFF | ungültiger Wert |

<a id="table-tab-phys-prnd"></a>
### TAB_PHYS_PRND

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MAIN_UNDEFINED |
| 0x01 | MAIN_P |
| 0x02 | MAIN_R |
| 0x03 | MAIN_N |
| 0x04 | MAIN_D |
| 0x05 | MAIN_M |
| 0x06 | MAIN_UNDEFINED |
| 0x07 | MAIN_ERR |
| 0xFF | Wert ungültig |

<a id="table-tab-prdnl-pos-ena"></a>
### TAB_PRDNL_POS_ENA

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | POS_ENA_OFF |
| 0x01 | POS_ENA_P |
| 0x02 | POS_ENA_PX |
| 0x04 | POS_ENA_R |
| 0x08 | POS_ENA_D |
| 0xFF | Wert ungültig |

<a id="table-tab-ref-drive-error-status"></a>
### TAB_REF_DRIVE_ERROR_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Ausserhalb des gültigen Bereichs |
| 0x02 | Timeout Fehler |
| 0x03 | Fehler beim Einlegen Neutral |
| 0xFFFF | Wert ungültig |

<a id="table-tab-replace-me"></a>
### TAB_REPLACE_ME

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |
| 0x01 | Dummy Value |

<a id="table-tab-replace-me-1"></a>
### TAB_REPLACE_ME_1

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |

<a id="table-tab-replace-me-2"></a>
### TAB_REPLACE_ME_2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Dummy Value |
| 0x1 | Dummy Value |

<a id="table-tab-replace-me-4"></a>
### TAB_REPLACE_ME_4

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |

<a id="table-tab-replace-me-5"></a>
### TAB_REPLACE_ME_5

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |

<a id="table-tab-replace-me-6"></a>
### TAB_REPLACE_ME_6

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |

<a id="table-tab-replace-me-8"></a>
### TAB_REPLACE_ME_8

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Dummy Value |
| 0xFF | Wert ungültig |

<a id="table-tab-sd-error-status"></a>
### TAB_SD_ERROR_STATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | falsche Richtung |
| 0x02 | Verbindung vertauscht |
| 0x03 | Keine Reaktion |
| 0x04 | Position falsch  eingestellt |
| 0xFFFF | Wert ungültig |

<a id="table-tab-secret-key"></a>
### TAB_SECRET_KEY

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Secret Key Invalid |
| 0x01 | Secret Key Init |
| 0x02 | Secret Key temp. Wert |
| 0x03 | Secret Key gespeichert |
| 0x04 | Secret Key gespeichert und gesperrt |
| 0xFF | Wert ungültig |

<a id="table-tab-secret-number"></a>
### TAB_SECRET_NUMBER

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Secret Number Invalid |
| 0x01 | Secret Number Init |
| 0x02 | Secret Number gespeichert |
| 0xFF | Wert ungültig |

<a id="table-tab-shftlck-state"></a>
### TAB_SHFTLCK_STATE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SLCK_OFF |
| 0x01 | SLCK_BRK |
| 0x02 | SLCK_ENG |
| 0x04 | SLCK_CAN |
| 0x08 | SLCK_ENDDRV |
| 0x10 | SLCK_PARKLOCK |
| 0xFF | Wert ungültig |

<a id="table-tab-shift-gear-p"></a>
### TAB_SHIFT_GEAR_P

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion |
| 0x01 | P einlegen |
| 0x02 | P auslegen |

<a id="table-tab-status-check-iss-sens"></a>
### TAB_STATUS_CHECK_ISS_SENS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-clu-actu-pwm-cntrl"></a>
### TAB_STATUS_CLU_ACTU_PWM_CNTRL

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett Fehler |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-clu-gain-ada-rst-values"></a>
### TAB_STATUS_CLU_GAIN_ADA_RST_VALUES

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-clu-self-open-tst"></a>
### TAB_STATUS_CLU_SELF_OPEN_TST

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-clu-sim-prs-cntrl"></a>
### TAB_STATUS_CLU_SIM_PRS_CNTRL

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-clu-tp-ada"></a>
### TAB_STATUS_CLU_TP_ADA

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett fehlerhaft |
| 0x11 | abgebrochen |
| 0x12 | interner Felher |
| 0xFF | Wert ungültig |

<a id="table-tab-status-gti-req-info-sd1"></a>
### TAB_STATUS_GTI_REQ_INFO_SD1

Dimensions: 25 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | req_no |
| 0x01 | req_always |
| 0x02 | req_nvr_read_con |
| 0x03 | req_nvr_wrn_refpoint |
| 0x04 | req_nvr_NRC |
| 0x05 | req_nv_s_inval |
| 0x06 | req_nv_ctr_on |
| 0x07 | req_err_set_inc |
| 0x08 | req_act_move |
| 0x09 | req_nv_gti_err |
| 0x0A | req_gti_active |
| 0x0B | req_nv_s_end_inval |
| 0x0C | req_nv_pwm_on |
| 0x0D | req_s_inval |
| 0x0E | req_tst_exit_not_teached |
| 0x0F | req_nv_version |
| 0x10 | req_manual |
| 0x11 | req_eol |
| 0x12 | req_broken_fork |
| 0x13 | req_setup_err_SD2_gear2 |
| 0x14 | req_level2 |
| 0x15 | req_check_P |
| 0x16 | req_ref_P |
| 0x17 | req_unexp_err |
| 0xFF | Wert ungültig |

<a id="table-tab-status-ref-sd-pos"></a>
### TAB_STATUS_REF_SD_POS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett ok |
| 0x3 | komplett Fehler |
| 0x11 | abgebrochen |
| 0x12 | interner Felher |
| 0xFF | Wert ungültig |

<a id="table-tab-status-rst-teachin-val"></a>
### TAB_STATUS_RST_TEACHIN_VAL

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett  ok |
| 0x3 | komplett Fehler |
| 0x11 | abgebrochen |
| 0x12 | interner Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-status-segeln-rolle"></a>
### TAB_STATUS_SEGELN_ROLLE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Segeln aktiv |
| 0x01 | Segeln inaktiv |
| 0x02 | Segeln aktiv bei größer 40 km/h |
| 0xFF | Ungültig |

<a id="table-tab-status-shft-gears"></a>
### TAB_STATUS_SHFT_GEARS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Leerlauf |
| 0x1 | im Gange |
| 0x2 | komplett  ok |
| 0x3 | komplett Fehler |
| 0x11 | abgebrochen |
| 0x12 | intener Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-clu-actu-pwm-cntrl-shft-gear-1"></a>
### TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_1

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Gang-1 |
| 0x0D | Leerlauf 1-3 |
| 0x03 | Gang-3 |
| 0x0E | Leerlauf 3-5 |
| 0x05 | Gang-5 |
| 0x0F | Leerlauf 5-7 |
| 0x07 | Gang 7 |
| 0xFFFF | Wert ungültig |

<a id="table-tab-stat-clu-actu-pwm-cntrl-shft-gear-2"></a>
### TAB_STAT_CLU_ACTU_PWM_CNTRL_SHFT_GEAR_2

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x63 | Rückwärtsgang + park Anfrage |
| 09 | Rückwärtsgang |
| 0x10 | Leerlauf-Rückwärtsgang-2 |
| 0x02 | Gang-2 |
| 0x11 | Leerlauf 2-4 |
| 0x04 | Gang-4 |
| 0x12 | Leerlauf 4-6 |
| 0x06 | Gang-6 |
| 0xFFFF | Wert ungültig |

<a id="table-tab-stat-gti-req-info-sd1"></a>
### TAB_STAT_GTI_REQ_INFO_SD1

Dimensions: 25 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Einlernen ist nicht notewendig |
| 0x01 | Getriebe immer einlernen |
| 0x02 | n/a |
| 0x03 | Warnbit von Anschlag-Referenzierungsfunktion wurde gesetzt |
| 0x04 | Weder EEP noch NVRAM Werte sind gültig |
| 0x05 | Schaltwalze war im Notfallmodus vor Reset |
| 0x06 | Schaltwalze-Kontroller war aktiv vor Reset |
| 0x07 | Ausrichten von Schaltwalzenposition ist nicht möglich |
| 0x08 | Schaltwalzen-Aktuatorbewegung vor Reset ist erkannt |
| 0x09 | Einlernen wurde vor Reset nicht erfolgreich abgeschlossen |
| 0x0A | Einlernen war aktiv bevor Reset |
| 0x0B | Unplausible Anschlagspositionen aus dem NVRAM |
| 0x0C | PWM-Ausgang für Schaltwalze Aktor vor Reset |
| 0x0D | kein Konfidenz in die Schaltwalze-Position |
| 0x0E | Schaltwalze braucht Einlernen nach der EOL-Modus-Aktivierung |
| 0x0F | SW-Version-Fehler aus dem NVRAM |
| 0x10 | Einlernen Anfrage pro Parameter |
| 0x11 | Einlernen-Anforderung von EOL-Modus |
| 0x12 | Kein Einlernen nach gebrochener Schaltgabel-Diagnose |
| 0x13 | Kein Einlernen nach eine Blockadeerkennung auf Gear2 auf Schaltwalze 2 |
| 0x14 | Einlernen-Anforderung von Level 2 Software |
| 0x15 | Einlernen-Modus 'Überprüfen P eingelegt' |
| 0x16 | Einlernen-Modus 'Referenz P' |
| 0x17 | unerwarteter Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-gti-req-info-sd2"></a>
### TAB_STAT_GTI_REQ_INFO_SD2

Dimensions: 25 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Einlernen ist nicht notwendig |
| 0x01 | Getriebe immer einlernen |
| 0x02 | n/a |
| 0x03 | Warnbit von Anschlag-Referenzierungsfunktion wurde gesetzt |
| 0x04 | Weder EEP noch NVRAM Werte sind gültig |
| 0x05 | Schaltwalze war im Notfallmodus vor Reset |
| 0x06 | Schaltwalze-Controller war aktiv vor Reset |
| 0x07 | Ausrichten von Schaltwalzenposition ist nicht möglich |
| 0x08 | Schaltwalzen-Aktuatorbewegung vor Reset ist erkannt |
| 0x09 | Einlernen wurde vor Reset nicht erfolgreich abgeschlossen |
| 0x0A | Einlernen war aktiv bevor Reset |
| 0x0B | Unplausible Anschlagspositionen aus dem NVRAM |
| 0x0C | PWM-Ausgang für Schaltwalze Aktor vor Reset |
| 0x0D | Keine Konfidenz in der Schaltwalzenposition |
| 0x0E | Schaltwalze braucht Einlernen nach der EOL-Modus-Aktivierung |
| 0x0F | SW-Version-Fehler aus dem NVRAM |
| 0x10 | Teach-in Anfrage durch Parametern |
| 0x11 | Einlernen-Anforderung von EOL-Modus |
| 0x12 | Kein Einlernen nach gebrochener Schaltgabel-Diagnose |
| 0x13 | Kein Einlernen nach dem Blockadeerkennung auf Zahnrad 2 auf Schaltwalze # 2 |
| 0x14 | Einlernen-Anforderung von Level 2 Software |
| 0x15 | Einlernen-Modus 'Überprüfen P eingelegt' |
| 0x16 | Einlernen-Modus 'Referenz P' |
| 0x17 | unerwarteter Fehler |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-sds-ins-spd-frm-status-1"></a>
### TAB_STAT_SDS_INS_SPD_FRM_STATUS_1

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GEN_SIG_INIT |
| 0x01 | GEN_SIG_VALID |
| 0x02 | GEN_SIG_SUBSTITUTED |
| 0x03 | GEN_SIG_ERR_DEB |
| 0x04 | GEN_SIG_ERROR |
| 0xFF | Wert ungültig |

<a id="table-tab-stat-sds-ins-spd-frm-status-2"></a>
### TAB_STAT_SDS_INS_SPD_FRM_STATUS_2

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GEN_SIG_INIT |
| 0x01 | GEN_SIG_VALID |
| 0x02 | GEN_SIG_SUBSTITUTED |
| 0x03 | GEN_SIG_ERR_DEB |
| 0x04 | GEN_SIG_ERROR |
| 0xFF | Wert ungültig |

<a id="table-tab-steuern-clu-self-open-tst-clu-nr"></a>
### TAB_STEUERN_CLU_SELF_OPEN_TST_CLU_NR

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Kupplung 1 |
| 0x02 | Kupplung 2 |

<a id="table-tab-steuern-clu-self-open-tst-cntrl-strat"></a>
### TAB_STEUERN_CLU_SELF_OPEN_TST_CNTRL_STRAT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | passiv : passive |
| 0x02 | aktiv : active |
| 0x03 | aktiv geschlossen-offen : active close-open |

<a id="table-tab-steuern-clu-tp-ada-start-clu-nr-arg"></a>
### TAB_STEUERN_CLU_TP_ADA_START_CLU_NR_ARG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Kupplung 1 |
| 0x02 | Kupplung 2 |
| 0x03 | Kupplung 1 und 2 |

<a id="table-tab-steuern-ews-fsc-ews-opt"></a>
### TAB_STEUERN_EWS_FSC_EWS_OPT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x07 | FREISCHALTCODE_SCHREIBEN |
| 0x09 | FREISCHALTCODE_PRÜFEN |

<a id="table-tab-steuern-segeln-rolle"></a>
### TAB_STEUERN_SEGELN_ROLLE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Segeln aktivieren |
| 0x01 | Segeln deaktivieren |
| 0x02 | Segeln aktiv bei größer 40 km/h |
| 0xFF | Wert ungültig |

<a id="table-tab-target-gear-sd1"></a>
### TAB_TARGET_GEAR_SD1

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | gear 1 |
| 0x03 | gear 3 |
| 0x05 | gear 5 |
| 0x07 | gear 7 |
| 0xD | gear Neutral-Position 1 to 3; N1-3 |
| 0xE | gear Neutral-Position 3 to 5; N3-5 |
| 0xF | gear Neutral-Position 5 to 7; N5-7 |

<a id="table-tab-target-gear-sd2"></a>
### TAB_TARGET_GEAR_SD2

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | gear 2 |
| 0x04 | gear 4 |
| 0x06 | gear 6 |
| 0x09 | gear R |
| 0x10 | gear Neutral-Reverse-Position 2; NR2 |
| 0x11 | gear Neutral-Position 2 to 4; N2-4 |
| 0x12 | gear Neutral-Position 4 to 6; N4-6 |
| 0x63 | park position |

<a id="table-tsl-gear-cnt-table"></a>
### TSL_GEAR_CNT_TABLE

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Daten zurücksetzten |

<a id="table-version"></a>
### VERSION

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Direktschreiben + EWS4 |
| 0x02 | Direktschreiben + EWS4 + DH-Abgleich |
| 0x03 | DH-Abgleich + EWS4 |
| 0x11 | Direktschreiben + EWS5 |
| 0x12 | Direktschreiben + EWS5 + DH-Abgleich |
| 0x22 | Direktschreiben + EWS6 + DH-Abgleich |
| 0x23 | DH-Abgleich + EWS6 |
| 0x24 | DH-Abgleich +EWS6 +ECC |
| 0xFF | Wert ungültig |

<a id="table-wdbyi-reset-flag-table"></a>
### WDBYI_RESET_FLAG_TABLE

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Daten zurücksetzten |
