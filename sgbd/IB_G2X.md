# IB_G2X.prg

- Jobs: [45](#jobs)
- Tables: [178](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integriertes Bremssystem (Bremsregelsystem) |
| ORIGIN | BMW EF-510 Matthias_Amberger |
| REVISION | 0.004 |
| AUTHOR | BMW EF-510 Terhorst |
| COMMENT | Version 1 21-11-205 [1] |
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
- [_EEPROM_LESEN](#job-eeprom-lesen)
- [_FS_LOESCHEN_FUNKTIONAL](#job-fs-loeschen-funktional) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [STATUS_FLM_LESEN](#job-status-flm-lesen) - Auslesen der FASTA Daten und der Debug Codierung UDS: $22 $D6D6 ReadDataByID UDS: $22 $E2F8 ReadDataByID Modus   : Default
- [STATUS_RBM_DETAIL_INFO](#job-status-rbm-detail-info) - Auslesen der Detailinfos zu IUMPR Ueberwachungen UDS: $22 ReadDataByIdentifier Modus   : Default
- [STATUS_RDC_ERFS_ECO_TABELLE_LESEN](#job-status-rdc-erfs-eco-tabelle-lesen) - Elektronischer Reifenfuelldruckschild Codierte ECO Reifen Tabelle Lesen UDS  : $22   ReadDataByIdentifier Modus: Default
- [_OBD_BEGU_SDC_LESEN](#job-obd-begu-sdc-lesen) - Auslesen von aktuell geflashte BEGU-Einheit und aktive Secondary Dependent Controller UDS  : $22   ReadDataByIdentifier
- [_OBD_LIEFERANTENFEHLER_INFO](#job-obd-lieferantenfehler-info) - Auslesen der Detailinfos zu den OBD-relevanten Ueberwachungen UDS: $22 ReadDataByIdentifier Modus   : Default

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

<a id="job-eeprom-lesen"></a>
### _EEPROM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_DATEN | binary | ausgelesene EEPROM-Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-status-flm-lesen"></a>
### STATUS_FLM_LESEN

Auslesen der FASTA Daten und der Debug Codierung UDS: $22 $D6D6 ReadDataByID UDS: $22 $E2F8 ReadDataByID Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLM_DATEN_ROHDATENZAEHLER_DATA | binary | Klassierte Zählung von Rohsignalen |
| STAT_FLM_DATEN_SNAPSHOT_FOTOS_DATA | binary | Lerndaten der FLM Snapshotsfunktionen |
| STAT_FLM_CODIERUNG_DATA | binary | Codierparameter der FLM Funktion |
| STAT_FLM_CODIERUNG_PHYSIK_DATA | binary | Codierparameter der FLM Funktion mit physikalischem Bezug |
| STAT_FLM_ACTIV_DATA | binary | Codierschalter zur de-/aktivierung der FLM Funktion |
| STAT_FLM_TYPSCHLUESSEL_DATA | binary | Fahrzeugtypschlüssel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-rbm-detail-info"></a>
### STATUS_RBM_DETAIL_INFO

Auslesen der Detailinfos zu IUMPR Ueberwachungen UDS: $22 ReadDataByIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_GENERAL_DENOMINATOR_WERT | unsigned int | Anzahl, wie oft das Signal ST_OBD_CYC den Status "aktiv"/"erfüllt" erreicht hat |
| STAT_ANZAHL_DENOMINATOR_V1_V2_WERT | unsigned int | Anzahl, wie oft das Signal ST_DIAG_EVA_CYC den Status "erfüllt" erreicht hat |
| STAT_INHALT_DENOMINATOR_V1_V2_WERT | unsigned char | Inhalt des Signals ST_DIAG_EVA_CYC (gültig/ungültig) |
| STAT_ANZAHL_RBM_FEHLER_WERT | unsigned int | Anzahl der in der SW umgesetzten RBM-relevanten Überwachungen |
| STAT_RBM_FEHLERNUMMER_INTERN_WERT | binary | Lieferanten-Fehlercode der RBM-relevanten Überwachung |
| STAT_RBM_FEHLERNUMMER_BMW_WERT | binary | BMW-Fehlercode der RBM-relevanten Überwachung |
| STAT_SAE_CODE_WERT | binary | SAE-Code der RBM-relevanten Überwachung |
| STAT_RBM_ZAEHLER_WERT | unsigned int | Der RBM Zaehler zu der RBM-relevanten Überwachung (Numerator) |
| STAT_RBM_NENNER_WERT | unsigned int | Der RBM Nenner zu der RBM-relevanten Überwachung  (Denominator) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Anfrage an das SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rdc-erfs-eco-tabelle-lesen"></a>
### STATUS_RDC_ERFS_ECO_TABELLE_LESEN

Elektronischer Reifenfuelldruckschild Codierte ECO Reifen Tabelle Lesen UDS  : $22   ReadDataByIdentifier Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REIFEN_TAB_ANZAHL_WERT | unsigned char | Anzahl ausgelesener Tabelleneintraege |
| STAT_REIFEN_TAB_ANZAHL_SW_WERT | unsigned char | Anzahl der Tabelleneintraege, die ueber die SW geliefert wurde |
| STAT_REIFEN_TAB_POSITION_WERT | unsigned char | Reifentabelle ausgelesene Position |
| STAT_REIFENBREITE_WERT | unsigned int | Reifenbreite |
| STAT_REIFENBREITE_EINH | string | Reifenbreite Einheit: Zoll |
| STAT_KARKASSE | unsigned char | Reifen Karkasse |
| STAT_KARKASSE_TEXT | string | table Karkasen UDS_TAB_ERFS_KARKASE |
| STAT_WERKSAUSLIEFERUNG | unsigned char | table Werksauslieferung UDS_TAB_ERFS_WERKSAUSLIEFERUNG Reifen ab Werksauslieferung: Ja/Nein |
| STAT_WERKSAUSLIEFERUNG_TEXT | string | table Werksauslieferung UDS_TAB_ERFS_WERKSAUSLIEFERUNG Reifen ab Werksauslieferung: Ja/Nein |
| STAT_QUERSCHNITTSVERHAELTNIS_WERT | unsigned char | Reifen Querschnittsverhaeltnis |
| STAT_REIFENTYP | unsigned char | Reifen Technologie |
| STAT_REIFENTYP_TEXT | string | table Tyre Technology UDS_TAB_ERFS_RSC |
| STAT_DURCHMESSER_WERT | unsigned char | Reifen Durchmesser |
| STAT_DURCHMESSER_EINH | string | Reifendurchmesser Einheit: Zoll |
| STAT_GESCHWINDIGKEITSINDEX | unsigned char | Reifen Geschwindigkeitsindex |
| STAT_GESCHWINDIGKEITSINDEX_TEXT | string | table Reifen Geschwindigkeitsindex TAB_ERFS_GESCHW_IDX |
| STAT_TRAGFAEHIGKEIT_WERT | unsigned char | Reifen Tragfaehigkeit |
| STAT_SAISON | unsigned char | Reifen Saison |
| STAT_SAISON_TEXT | string | table Reifen Saison TAB_ERFS_SAISON |
| STAT_REIFEN_TAB_RCP_VA_TB_WERT | real | Solldruck Vorderachse Teilbeladen |
| STAT_REIFEN_TAB_RCP_HA_TB_WERT | real | Solldruck Hinterachse Teilbeladen |
| STAT_REIFEN_TAB_RCP_VA_VB_WERT | real | Solldruck Vorderachse Vollbeladen |
| STAT_REIFEN_TAB_RCP_HA_VB_WERT | real | Solldruck Hinterachse Vollbeladen |
| STAT_REIFEN_TAB_RCP_VA_TB_ECO_WERT | real | Solldruck Vorderachse Vollbeladen |
| STAT_REIFEN_TAB_RCP_HA_TB_ECO_WERT | real | Solldruck Hinterachse Vollbeladen |
| STAT_REIFEN_TAB_RCP_VA_TB_EINH | string | Einheit Bar |
| STAT_REIFEN_TAB_RCP_HA_TB_EINH | string | Einheit Bar |
| STAT_REIFEN_TAB_RCP_VA_VB_EINH | string | Einheit Bar |
| STAT_REIFEN_TAB_RCP_HA_VB_EINH | string | Einheit Bar |
| STAT_REIFEN_TAB_RCP_VA_TB_ECO_EINH | string | Einheit Bar |
| STAT_REIFEN_TAB_RCP_HA_TB_ECO_EINH | string | Einheit Bar |
| STAT_CRC_WERT | unsigned char | CRC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-obd-begu-sdc-lesen"></a>
### _OBD_BEGU_SDC_LESEN

Auslesen von aktuell geflashte BEGU-Einheit und aktive Secondary Dependent Controller UDS  : $22   ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _BEGU_WERT | unsigned char | Response-Daten |
| _BEGU_TEXT | string | geflashte BEGU-Einheit in Text |
| _ASCM_AKTIV_WERT | unsigned char | Response-Daten |
| _ASCM_AKTIV_TEXT | string | aktiv/inaktiv |
| _EPS_AKTIV_WERT | unsigned char | Response-Daten |
| _EPS_AKTIV_TEXT | string | aktiv/inaktiv |
| _HSR_AKTIV_WERT | unsigned char | Response-Daten |
| _HSR_AKTIV_TEXT | string | aktiv/inaktiv |
| _LMV_AKTIV_WERT | unsigned char | Response-Daten |
| _LMV_AKTIV_TEXT | string | aktiv/inaktiv |
| _VIP_AKTIV_WERT | unsigned char | Response-Daten |
| _VIP_AKTIV_TEXT | string | aktiv/inaktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-obd-lieferantenfehler-info"></a>
### _OBD_LIEFERANTENFEHLER_INFO

Auslesen der Detailinfos zu den OBD-relevanten Ueberwachungen UDS: $22 ReadDataByIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _ANZAHL_LIEFERANTENFEHLER | unsigned int | Anzahl der aktiven Lieferantenfehler |
| _BMW_FEHLERNUMMER | binary | BMW-Fehlernummer als Hexcode |
| _SAE_CODE | binary | SAE-Code als Hexcode |
| _MIL_TRIP | unsigned char | Mil Trip Info |
| _LIEFERANTENFEHLERNUMMER | binary | Lieferanten-Fehlernummer |
| _STATUS_BIT_0_WERT | char | Status bit_0 |
| _STATUS_BIT_0_TEXT | string | Status bit_0 |
| _STATUS_BIT_1_WERT | char | Status bit_1 |
| _STATUS_BIT_1_TEXT | string | Status bit_1 |
| _STATUS_BIT_4_WERT | char | Status bit_4 |
| _STATUS_BIT_4_TEXT | string | Status bit_4 |
| _STATUS_BIT_5_WERT | char | Status bit_5 |
| _STATUS_BIT_5_TEXT | string | Status bit_5 |
| _STATUS_BIT_6_WERT | char | Status bit_6 |
| _STATUS_BIT_6_TEXT | string | Status bit_6 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Anfrage an das SG |
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
- [CBSNRTEXT](#table-cbsnrtext) (27 × 3)
- [CBSKENNUNG](#table-cbskennung) (30 × 3)
- [TAB_ECU_NAME](#table-tab-ecu-name) (6 × 2)
- [TAB_CBS_EINHEITEN](#table-tab-cbs-einheiten) (5 × 2)
- [TAB_CBS_STATUS](#table-tab-cbs-status) (17 × 2)
- [TAB_CBS_MONAT](#table-tab-cbs-monat) (16 × 2)
- [TAB_RUECK_GRUND](#table-tab-rueck-grund) (11 × 2)
- [ARG_0X5000_D](#table-arg-0x5000-d) (2 × 12)
- [ARG_0X5001_D](#table-arg-0x5001-d) (2 × 12)
- [ARG_0XA065_R](#table-arg-0xa065-r) (1 × 14)
- [ARG_0XA3A0_R](#table-arg-0xa3a0-r) (2 × 14)
- [ARG_0XA3A1_R](#table-arg-0xa3a1-r) (1 × 14)
- [ARG_0XA3A4_R](#table-arg-0xa3a4-r) (3 × 14)
- [ARG_0XA803_R](#table-arg-0xa803-r) (1 × 14)
- [ARG_0XD80F_D](#table-arg-0xd80f-d) (1 × 12)
- [ARG_0XD8E9_D](#table-arg-0xd8e9-d) (1 × 12)
- [ARG_0XD8F3_D](#table-arg-0xd8f3-d) (2 × 12)
- [ARG_0XD8F4_D](#table-arg-0xd8f4-d) (2 × 12)
- [ARG_0XD8F5_D](#table-arg-0xd8f5-d) (1 × 12)
- [ARG_0XDB2A_D](#table-arg-0xdb2a-d) (1 × 12)
- [ARG_0XDBE2_D](#table-arg-0xdbe2-d) (1 × 12)
- [ARG_0XDC1D_D](#table-arg-0xdc1d-d) (1 × 12)
- [ARG_0XDCC0_D](#table-arg-0xdcc0-d) (2 × 12)
- [ARG_0XDCC6_D](#table-arg-0xdcc6-d) (2 × 12)
- [ARG_0XF000_R](#table-arg-0xf000-r) (1 × 14)
- [BF_HA_FLAG_BVA](#table-bf-ha-flag-bva) (1 × 10)
- [BF_HA_RESET_VERHINDERER_1](#table-bf-ha-reset-verhinderer-1) (3 × 10)
- [BF_HA_RESET_VERHINDERER_2](#table-bf-ha-reset-verhinderer-2) (7 × 10)
- [BF_OBS_ERGEBNIS_BEFUELLUNG](#table-bf-obs-ergebnis-befuellung) (8 × 10)
- [BF_VA_FLAG_BVA](#table-bf-va-flag-bva) (1 × 10)
- [BF_VA_RESET_VERHINDERER_1](#table-bf-va-reset-verhinderer-1) (3 × 10)
- [BF_VA_RESET_VERHINDERER_2](#table-bf-va-reset-verhinderer-2) (7 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (466 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (67 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (111 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (67 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (11 × 2)
- [RDC_INT_KONFIG](#table-rdc-int-konfig) (5 × 2)
- [RDC_TAB_POSITION_SENSOR](#table-rdc-tab-position-sensor) (10 × 2)
- [RES_0X1061_R](#table-res-0x1061-r) (1 × 13)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X5002_D](#table-res-0x5002-d) (2 × 10)
- [RES_0X5038_D](#table-res-0x5038-d) (27 × 10)
- [RES_0XA065_R](#table-res-0xa065-r) (9 × 13)
- [RES_0XA130_R](#table-res-0xa130-r) (1 × 13)
- [RES_0XA14B_R](#table-res-0xa14b-r) (2 × 13)
- [RES_0XA154_R](#table-res-0xa154-r) (2 × 13)
- [RES_0XA3A0_R](#table-res-0xa3a0-r) (2 × 13)
- [RES_0XA3A1_R](#table-res-0xa3a1-r) (2 × 13)
- [RES_0XA3A2_R](#table-res-0xa3a2-r) (5 × 13)
- [RES_0XA3A3_R](#table-res-0xa3a3-r) (14 × 13)
- [RES_0XA3A4_R](#table-res-0xa3a4-r) (6 × 13)
- [RES_0XA3A5_R](#table-res-0xa3a5-r) (2 × 13)
- [RES_0XA803_R](#table-res-0xa803-r) (1 × 13)
- [RES_0XD272_D](#table-res-0xd272-d) (28 × 10)
- [RES_0XD690_D](#table-res-0xd690-d) (6 × 10)
- [RES_0XD805_D](#table-res-0xd805-d) (9 × 10)
- [RES_0XD80F_D](#table-res-0xd80f-d) (1 × 10)
- [RES_0XD81E_D](#table-res-0xd81e-d) (2 × 10)
- [RES_0XD8E7_D](#table-res-0xd8e7-d) (30 × 10)
- [RES_0XD8F2_D](#table-res-0xd8f2-d) (34 × 10)
- [RES_0XDB29_D](#table-res-0xdb29-d) (2 × 10)
- [RES_0XDB2A_D](#table-res-0xdb2a-d) (1 × 10)
- [RES_0XDBDF_D](#table-res-0xdbdf-d) (2 × 10)
- [RES_0XDBE2_D](#table-res-0xdbe2-d) (1 × 10)
- [RES_0XDBE3_D](#table-res-0xdbe3-d) (10 × 10)
- [RES_0XDBE4_D](#table-res-0xdbe4-d) (14 × 10)
- [RES_0XDBF6_D](#table-res-0xdbf6-d) (2 × 10)
- [RES_0XDC14_D](#table-res-0xdc14-d) (25 × 10)
- [RES_0XDC15_D](#table-res-0xdc15-d) (24 × 10)
- [RES_0XDC1D_D](#table-res-0xdc1d-d) (1 × 10)
- [RES_0XDC6C_D](#table-res-0xdc6c-d) (3 × 10)
- [RES_0XDC6D_D](#table-res-0xdc6d-d) (3 × 10)
- [RES_0XDC6E_D](#table-res-0xdc6e-d) (3 × 10)
- [RES_0XDC70_D](#table-res-0xdc70-d) (3 × 10)
- [RES_0XDC95_D](#table-res-0xdc95-d) (17 × 10)
- [RES_0XDC96_D](#table-res-0xdc96-d) (15 × 10)
- [RES_0XDC97_D](#table-res-0xdc97-d) (72 × 10)
- [RES_0XDC98_D](#table-res-0xdc98-d) (16 × 10)
- [RES_0XDC99_D](#table-res-0xdc99-d) (16 × 10)
- [RES_0XDC9A_D](#table-res-0xdc9a-d) (16 × 10)
- [RES_0XDC9B_D](#table-res-0xdc9b-d) (16 × 10)
- [RES_0XDC9C_D](#table-res-0xdc9c-d) (29 × 10)
- [RES_0XDC9D_D](#table-res-0xdc9d-d) (29 × 10)
- [RES_0XDC9E_D](#table-res-0xdc9e-d) (29 × 10)
- [RES_0XDC9F_D](#table-res-0xdc9f-d) (25 × 10)
- [RES_0XDCD9_D](#table-res-0xdcd9-d) (32 × 10)
- [RES_0XDCF1_D](#table-res-0xdcf1-d) (25 × 10)
- [RES_0XDCF2_D](#table-res-0xdcf2-d) (25 × 10)
- [RES_0XDCF3_D](#table-res-0xdcf3-d) (25 × 10)
- [RES_0XDE5B_D](#table-res-0xde5b-d) (28 × 10)
- [RES_0XDE5C_D](#table-res-0xde5c-d) (56 × 10)
- [RES_0XDE5D_D](#table-res-0xde5d-d) (24 × 10)
- [RES_0XDE5E_D](#table-res-0xde5e-d) (48 × 10)
- [RES_0XF000_R](#table-res-0xf000-r) (1 × 13)
- [SG_FUNKTIONEN](#table-sg-funktionen) (84 × 16)
- [TAB_ABS_FUNKTION](#table-tab-abs-funktion) (4 × 2)
- [TAB_AKTIV_INAKTIV](#table-tab-aktiv-inaktiv) (3 × 2)
- [TAB_ASC_FUNKTION](#table-tab-asc-funktion) (6 × 2)
- [TAB_BREMSBELAGVERSCHLEISSSENSOR](#table-tab-bremsbelagverschleisssensor) (3 × 2)
- [TAB_BREMSENSTATUS_LINKS](#table-tab-bremsenstatus-links) (10 × 2)
- [TAB_BREMSENSTATUS_RECHTS](#table-tab-bremsenstatus-rechts) (10 × 2)
- [TAB_DIFFERENZGESCHWINDIGKEIT](#table-tab-differenzgeschwindigkeit) (3 × 2)
- [TAB_DREHRICHTUNG](#table-tab-drehrichtung) (4 × 2)
- [TAB_EMF_HU_MODE](#table-tab-emf-hu-mode) (8 × 2)
- [TAB_EMF_POSITION](#table-tab-emf-position) (10 × 2)
- [TAB_EMF_TASTER](#table-tab-emf-taster) (5 × 2)
- [TAB_EMF_VERFAHREN](#table-tab-emf-verfahren) (14 × 2)
- [TAB_ENTLASTUNG_GENERATOR](#table-tab-entlastung-generator) (16 × 2)
- [TAB_EPB_EREIGNIS](#table-tab-epb-ereignis) (21 × 2)
- [TAB_ERFS_AKT_VERBAUT](#table-tab-erfs-akt-verbaut) (3 × 2)
- [TAB_ERFS_GESCHW_IDX](#table-tab-erfs-geschw-idx) (16 × 2)
- [TAB_ERFS_KARKASSE](#table-tab-erfs-karkasse) (3 × 2)
- [TAB_ERFS_RSC](#table-tab-erfs-rsc) (5 × 2)
- [TAB_ERFS_SAISON](#table-tab-erfs-saison) (4 × 2)
- [TAB_ERFS_WERKSAUSLIEFERUNG](#table-tab-erfs-werksauslieferung) (3 × 2)
- [TAB_FDR_FUNKTION](#table-tab-fdr-funktion) (4 × 2)
- [TAB_HDC_FUNKTION](#table-tab-hdc-funktion) (3 × 2)
- [TAB_KALIBRIERUNG](#table-tab-kalibrierung) (26 × 2)
- [TAB_NACHARBEITSENTLUEFTUNG_PHASEN](#table-tab-nacharbeitsentlueftung-phasen) (8 × 2)
- [TAB_OBS_ROUTINE_ERGEBNIS](#table-tab-obs-routine-ergebnis) (5 × 2)
- [TAB_OBS_ROUTINE_FEHLERINFORMATIONEN](#table-tab-obs-routine-fehlerinformationen) (12 × 2)
- [TAB_OBS_ROUTINE_STATUS](#table-tab-obs-routine-status) (4 × 2)
- [TAB_PHASE_EVAK_UND_BEFUELL](#table-tab-phase-evak-und-befuell) (4 × 2)
- [TAB_PLAUSI_DRUCK](#table-tab-plausi-druck) (6 × 2)
- [TAB_POSITION_RAD](#table-tab-position-rad) (5 × 2)
- [TAB_PRODUKTIONSSTATUS](#table-tab-produktionsstatus) (3 × 2)
- [TAB_RDC_AKTIONSNR](#table-tab-rdc-aktionsnr) (3 × 2)
- [TAB_RDC_AKTIV_INAKTIV](#table-tab-rdc-aktiv-inaktiv) (5 × 2)
- [TAB_RDC_BANDMODE_ACTIVE](#table-tab-rdc-bandmode-active) (3 × 2)
- [TAB_RDC_BEKANNT_NICHT_BEKANNT](#table-tab-rdc-bekannt-nicht-bekannt) (3 × 2)
- [TAB_RDC_CAL_ACTIVE](#table-tab-rdc-cal-active) (4 × 2)
- [TAB_RDC_CHANGED](#table-tab-rdc-changed) (3 × 2)
- [TAB_RDC_DETECTED](#table-tab-rdc-detected) (3 × 2)
- [TAB_RDC_DTC_ACTIVE_STATUS](#table-tab-rdc-dtc-active-status) (33 × 2)
- [TAB_RDC_INTERNE_STATUS](#table-tab-rdc-interne-status) (4 × 2)
- [TAB_RDC_INT_FEHLER](#table-tab-rdc-int-fehler) (25 × 2)
- [TAB_RDC_ON_OFF](#table-tab-rdc-on-off) (4 × 2)
- [TAB_RDC_RAD_POSITION_NR](#table-tab-rdc-rad-position-nr) (71 × 2)
- [TAB_RDC_RE_HERSTELLER](#table-tab-rdc-re-hersteller) (21 × 2)
- [TAB_RDC_RE_SENDEMODE_AK](#table-tab-rdc-re-sendemode-ak) (10 × 2)
- [TAB_RDC_RE_STATUS](#table-tab-rdc-re-status) (5 × 2)
- [TAB_RDC_STARTED](#table-tab-rdc-started) (3 × 2)
- [TAB_RDC_STEUERFUNKTIONEN](#table-tab-rdc-steuerfunktionen) (4 × 2)
- [TAB_RDC_TIMEOUT](#table-tab-rdc-timeout) (3 × 2)
- [TAB_RDC_VEHICLE_RUNNING](#table-tab-rdc-vehicle-running) (3 × 2)
- [TAB_RDC_ZUSTAND](#table-tab-rdc-zustand) (5 × 2)
- [TAB_RE_HERSTELLER](#table-tab-re-hersteller) (8 × 2)
- [TAB_RE_TELEGRAMMTYP](#table-tab-re-telegrammtyp) (6 × 2)
- [TAB_SCHALTERSTATUS](#table-tab-schalterstatus) (5 × 2)
- [TAB_START_TTS_CAL_STATUS](#table-tab-start-tts-cal-status) (3 × 2)
- [TAB_STATE_TTS_CAL_STATUS](#table-tab-state-tts-cal-status) (9 × 2)
- [TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT](#table-tab-status-laden-hochspannung-powermanagement) (8 × 2)
- [TAB_STATUS_ROUTINE](#table-tab-status-routine) (7 × 2)
- [TAB_STATUS_SPANNUNGSEINBRUCH](#table-tab-status-spannungseinbruch) (7 × 2)
- [TAB_STATUS_VERBRENNUNGSMOTOR_ANTRIEB](#table-tab-status-verbrennungsmotor-antrieb) (7 × 2)
- [TAB_VERTAUSCHUNGSTEST_RAD](#table-tab-vertauschungstest-rad) (4 × 2)
- [TAB_ZEITRAHMEN_AUSWAHL](#table-tab-zeitrahmen-auswahl) (6 × 2)
- [TAB_0X2951](#table-tab-0x2951) (1 × 2)
- [TAB_0X502F](#table-tab-0x502f) (1 × 7)

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

<a id="table-arg-0x5000-d"></a>
### ARG_0X5000_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RDC_COMMAND | HEX | high | unsigned char | - | - | - | - | - | - | - | Test Befehl Nummer. |
| RDC_TEST_DATA | DATA | high | data[50] | - | - | 1.0 | 1.0 | 0.0 | - | - | Test Daten. |

<a id="table-arg-0x5001-d"></a>
### ARG_0X5001_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ERFS_COMMAND | HEX | high | unsigned char | - | - | - | - | - | - | - | Befehl Nummer. |
| ERFS_TEST_DATA | DATA | high | data[15] | - | - | 1.0 | 1.0 | 0.0 | - | - | Test Daten. |

<a id="table-arg-0xa065-r"></a>
### ARG_0XA065_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT_ROUTINE | + | - | s | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | - | - | max. Ausführungsdauer |

<a id="table-arg-0xa3a0-r"></a>
### ARG_0XA3A0_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EVAKUIERUNG_UND_BEFUELLUNG_PHASE | + | - | 0-n | high | unsigned char | - | TAB_PHASE_EVAK_UND_BEFUELL | - | - | - | - | - | Definition der Routinen Phase welches gestartet werden soll |
| EVAKUIERUNG_UND_BEFUELLUNG_ZEITVORGABE | + | - | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 65535.0 | Routine Zeitvorgabe fuer die Phase |

<a id="table-arg-0xa3a1-r"></a>
### ARG_0XA3A1_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NACHARBEITSENTLUEFTUNG_PHASE | + | - | 0-n | high | unsigned char | - | TAB_NACHARBEITSENTLUEFTUNG_PHASEN | - | - | - | - | - | Definition der Routinen Phase |

<a id="table-arg-0xa3a4-r"></a>
### ARG_0XA3A4_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZIEL_RAD | + | - | 0-n | high | unsigned char | - | TAB_VERTAUSCHUNGSTEST_RAD | - | - | - | - | - | Rad das abgebremst werden soll |
| ZIEL_GESCHWINDIGKEITS_UNTERSCHIED | + | - | km/h | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | 0.1 | 20.0 | Die Ziel-Differenz Geschwindigkeit wird eingestellt |
| ZIEL_DRUCK | + | - | bar | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | 2.0 | 120.0 | Der Druck wird eingestellt mit dem gebremst werden soll. |

<a id="table-arg-0xa803-r"></a>
### ARG_0XA803_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | + | - | 0-n | - | unsigned char | - | TAB_EMF_VERFAHREN | - | - | - | - | - | Gewählte Position |

<a id="table-arg-0xd80f-d"></a>
### ARG_0XD80F_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MODE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = aktiv; 0 = nicht aktiv |

<a id="table-arg-0xd8e9-d"></a>
### ARG_0XD8E9_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TSA_DATA | DATA | high | data[104] | - | - | 1.0 | 1.0 | 0.0 | - | - | Tyre Sales Assistant Händler Daten |

<a id="table-arg-0xd8f3-d"></a>
### ARG_0XD8F3_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ECO_AKT_REIFEN_POSITION | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 19.0 | ECO Reifen Position in die Reifentabelle: 0 bis 19. |
| ECO_AKT_REIFEN_DATEN | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | - | - | Codierte Reifen Dimensionen wie im CAF Datei |

<a id="table-arg-0xd8f4-d"></a>
### ARG_0XD8F4_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REIFEN_POSITION | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 19.0 | Neue Reifen Position in die Reifentabelle: 0 bis 19. |
| REIFEN_DATEN | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | - | - | Neue codierte Reifen Dimensionen wie im CAF Datei |

<a id="table-arg-0xd8f5-d"></a>
### ARG_0XD8F5_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NEUE_REIFEN_TABELLE | DATA | high | data[162] | - | - | 1.0 | 1.0 | 0.0 | - | - | Neue Codierte Reifen Tabelle |

<a id="table-arg-0xdb2a-d"></a>
### ARG_0XDB2A_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PRODUKTIONSSTATUS | 0-n | high | unsigned char | - | TAB_PRODUKTIONSSTATUS | - | - | - | - | - | Ändert  den Zustand des Produktionsstatus |

<a id="table-arg-0xdbe2-d"></a>
### ARG_0XDBE2_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REKU_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = aktiv;  0 = inaktiv |

<a id="table-arg-0xdc1d-d"></a>
### ARG_0XDC1D_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTOHOLDLED_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = LED ein  0 = LED aus |

<a id="table-arg-0xdcc0-d"></a>
### ARG_0XDCC0_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RE_ID | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | ID der Radelektronik |
| RE_POS | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | - | - | Position der Radelektronik |

<a id="table-arg-0xdcc6-d"></a>
### ARG_0XDCC6_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSNR | 0-n | high | unsigned char | - | TAB_RDC_STEUERFUNKTIONEN | - | - | - | - | - | 1 = BANDMODE - Bandmode; 4 = TEST_ER_FAHRT - Empfang der Eigenraeder bei Fahrt pruefen; 8 = CAL_REQUEST - Kalibrieranforderung; |
| AKTIONSNR | 0-n | high | unsigned char | - | TAB_RDC_AKTIONSNR | - | - | - | - | - | 1 - SET; 0 - RESET; 2 - RECEPTION TEST NO SPEED |

<a id="table-arg-0xf000-r"></a>
### ARG_0XF000_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| _ZEITRAHMEN_AUSWAHL | + | - | 0-n | high | unsigned char | - | TAB_ZEITRAHMEN_AUSWAHL | - | - | - | - | - | Erlaubt über die Argumenten-Auswahl verschiedener Zeitrahmen die Ausgabe der max CPU Last in % für den ausgewählten Zeitrahmen. |

<a id="table-bf-ha-flag-bva"></a>
### BF_HA_FLAG_BVA

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HA_FLAG_BVA | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Zustand BVA-Sensor: 0 = BVA-Sersor nicht durchgeschliffen, 1 = BVA-Sersor durchgeschliffen |

<a id="table-bf-ha-reset-verhinderer-1"></a>
### BF_HA_RESET_VERHINDERER_1

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HA_DATUM_UHRZEIT_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Datum_Uhrzeit_gueltig_bei_reset 1. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_KM_STAND_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x02 | - | - | - | - | KM_Stand_gueltig_bei_reset 2. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_VIN_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x04 | - | - | - | - | VIN_gueltig_bei_reset 3. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |

<a id="table-bf-ha-reset-verhinderer-2"></a>
### BF_HA_RESET_VERHINDERER_2

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HA_BBV_SENSOR_NICHT_GEST_BEI_RESET | 0/1 | high | unsigned char | 0x01 | - | - | - | - | BBV_Sensor_nicht_angesteckt_bei_reset 4. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_BBV_SENSOR_FEHLER_BEI_RESET | 0/1 | high | unsigned char | 0x02 | - | - | - | - | BBV_Sensor_Fehler_bei_reset 5. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_VORDRUCK_BEI_RESET | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Vordruck_bei_reset 6. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_EMF_ANGEZ_BEI_RESET | 0/1 | high | unsigned char | 0x08 | - | - | - | - | EMF_angezogen_bei_reset 7. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_KOMM_FEHLER_EMF_BEI_RESET | 0/1 | high | unsigned char | 0x10 | - | - | - | - | Kommunikationsfehler_mit_EMF_bei_reset 8. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_GESCHW_BEI_RESET | 0/1 | high | unsigned char | 0x20 | - | - | - | - | Geschwindigkeit_bei_reset 9. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_HA_AKTIVER_DRUCKAUFBAU_BEI_RESET | 0/1 | high | unsigned char | 0x40 | - | - | - | - | Aktiver_Druckaufbau_bei_reset 10. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |

<a id="table-bf-obs-ergebnis-befuellung"></a>
### BF_OBS_ERGEBNIS_BEFUELLUNG

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LAC_UND_HAUPTBREMSZYLINDER_ENTLUEFTUNG_TEST | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Bit 0: Linearaktuator und Hauptbremszylinder Entlueftung Test. 0 - niO. 1 - iO. |
| STAT_SIMULATOR_ENTLUEFTUNG_TEST | 0/1 | high | unsigned char | 0x02 | - | - | - | - | Bit 1: Simulator Entlueftung Test 0 - niO. 1 - iO. |
| STAT_RESERVE_1 | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Bit 2: Reserviert |
| STAT_RESERVE_2 | 0/1 | high | unsigned char | 0x08 | - | - | - | - | Bit 3: Reserviert |
| STAT_RESERVE_3 | 0/1 | high | unsigned char | 0x10 | - | - | - | - | Bit 4: Reserviert |
| STAT_RESERVE_4 | 0/1 | high | unsigned char | 0x20 | - | - | - | - | Bit 5: Reserviert |
| STAT_RESERVE_5 | 0/1 | high | unsigned char | 0x40 | - | - | - | - | Bit 6: Reserviert |
| STAT_RESERVE_6 | 0/1 | high | unsigned char | 0x80 | - | - | - | - | Bit 7: Reserviert |

<a id="table-bf-va-flag-bva"></a>
### BF_VA_FLAG_BVA

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VA_FLAG_BVA | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Zustand BVA-Sensor: 0 = BVA-Sersor nicht durchgeschliffen, 1 = BVA-Sersor durchgeschliffen |

<a id="table-bf-va-reset-verhinderer-1"></a>
### BF_VA_RESET_VERHINDERER_1

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VA_DATUM_UHRZEIT_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x01 | - | - | - | - | Datum_Uhrzeit_gueltig_bei_reset 1. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_KM_STAND_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x02 | - | - | - | - | KM_Stand_gueltig_bei_reset 2. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_VIN_GUELTIG_BEI_RESET | 0/1 | high | unsigned char | 0x04 | - | - | - | - | VIN_gueltig_bei_reset 3. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |

<a id="table-bf-va-reset-verhinderer-2"></a>
### BF_VA_RESET_VERHINDERER_2

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VA_BBV_SENSOR_NICHT_GEST_BEI_RESET | 0/1 | high | unsigned char | 0x01 | - | - | - | - | BBV_Sensor_nicht_angesteckt_bei_reset 4. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_BBV_SENSOR_FEHLER_BEI_RESET | 0/1 | high | unsigned char | 0x02 | - | - | - | - | BBV_Sensor_Fehler_bei_reset 5. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_VORDRUCK_BEI_RESET | 0/1 | high | unsigned char | 0x04 | - | - | - | - | Vordruck_bei_reset 6. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu  |
| STAT_VA_EMF_ANGEZ_BEI_RESET | 0/1 | high | unsigned char | 0x08 | - | - | - | - | EMF_angezogen_bei_reset 7. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_KOMM_FEHLER_EMF_BEI_RESET | 0/1 | high | unsigned char | 0x10 | - | - | - | - | Kommunikationsfehler_mit_EMF_bei_reset 8. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_GESCHW_BEI_RESET | 0/1 | high | unsigned char | 0x20 | - | - | - | - | Geschwindigkeit_bei_reset 9. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |
| STAT_VA_AKTIVER_DRUCKAUFBAU_BEI_RESET | 0/1 | high | unsigned char | 0x40 | - | - | - | - | Aktiver_Druckaufbau_bei_reset 10. Resetverhinderer: 0 = Aussage trifft nicht zu, 1 = Aussage trifft zu |

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

Dimensions: 466 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x022900 | Energiesparmode aktiv | 0 | - |
| 0x022908 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x022909 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02290A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02290B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02290C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02290D | Codierung: Codierdaten nicht qualifiziert | 0 | - |
| 0x02FF29 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x480686 | Raddrehzahlsensor - Hinten Rechts - Anfahrerkennung fehlerhaft | 0 | - |
| 0x48068C | Verteilergetriebe - Kupplung voruebergehend stillgelegt, evtl. Überhitzung | 1 | - |
| 0x480698 | Peripherial/Funktional error Schnittstelle QDM Initialisierung Signal ungültig | 0 | - |
| 0x48069B | RDCi Funkverbindung durch Fremdeinfluss gestoert | 1 | - |
| 0x48069C | Rollenbetrieb - Aktiviert | 0 | - |
| 0x48069D | Fahrzeugregler - Ist Lenkwinkel VA Rad - Phase 1: Fehleramplitude zu groß | 0 | - |
| 0x48069E | RDCi Kalibrierung Raderkennung nicht moeglich | 0 | - |
| 0x4806A1 | RDCi Alle Radelektroniken bedingt kompatibel keine Positionsanzeige | 0 | - |
| 0x4806A6 | RDCi Radelektronik Position unbekannt Mischverbau | 0 | - |
| 0x4806B2 | Fahrzeugregler - Querbeschleunigung - Phase 1: Fehleramplitude zu groß | 0 | - |
| 0x4806B8 | RDCi Radelektronik vorn links kein Empfang | 0 | - |
| 0x4806CC | Fahrzeugregler - Gierrate - Soll - Fehleramplitude des Ackermann-Sollgierraten-Signals übersteigt zulässigen Schwellwert - Phase 1 | 0 | - |
| 0x4806CD | Fahrzeugregler - Gierrate - Soll - Fehleramplitude des Ackermann-Sollgierraten-Signals übersteigt zulässigen Schwellwert - Phase 2 und 3 | 0 | - |
| 0x4806D9 | Steuergerät intern - EEPROM Fehler | 0 | - |
| 0x4806DA | RDCi Radelektronik vorn rechts kein Empfang | 0 | - |
| 0x4806F0 | RDCi Radelektronik hinten links kein Empfang | 0 | - |
| 0x4806F4 | RDCi Radelektronik hinten rechts kein Empfang | 0 | - |
| 0x4806FA | RDCi Radelektronik vorn links defekt | 0 | - |
| 0x480702 | RDCi Radelektronik vorn rechts defekt | 0 | - |
| 0x480704 | Steuergerät intern - Laufzeitfehler | 0 | - |
| 0x480705 | Steuergerät intern - HW Fehler ASG intern, System ASIC | 0 | - |
| 0x480706 | Steuergerät intern - HW Fehler ASG intern | 0 | - |
| 0x480707 | Steuergerät intern - RAM Fehler | 0 | - |
| 0x48070C | Steuergerät intern - Conti - EEPROM Fehler - RPA-Daten | 0 | - |
| 0x48070D | Steuergerät intern - Conti - EEPROM Fehler - Einlassventildaten | 0 | - |
| 0x48070F | RDCi Radelektronik hinten links defekt | 0 | - |
| 0x480710 | Raddrehzahlsensor - Vorn Links - Plausi: Drehrichtung | 0 | - |
| 0x480711 | Raddrehzahlsensor - Vorn Links - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480713 | Raddrehzahlsensor - Vorn Rechts - Plausi: Drehrichtung | 0 | - |
| 0x480714 | Raddrehzahlsensor - Vorn Rechts - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480716 | Raddrehzahlsensor - Hinten Links - Plausi: Drehrichtung | 0 | - |
| 0x480717 | Raddrehzahlsensor - Hinten Links - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480719 | Raddrehzahlsensor - Hinten Rechts - Plausi: Drehrichtung | 0 | - |
| 0x48071A | Raddrehzahlsensor - Hinten Rechts - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x48071F | RDCi Radelektronik Position unbekannt | 0 | - |
| 0x480728 | RDCi Radelektronik hinten rechts defekt | 0 | - |
| 0x480758 | EPBi Taster dauerhaft betätigt | 0 | - |
| 0x480760 | EPBi - Montagemodus ist aktiv | 0 | - |
| 0x480762 | EPBi Links - Elektrischer Kurzschluss | 0 | - |
| 0x480763 | EPBi Rechts - Elektrischer Kurzschluss | 0 | - |
| 0x480764 | EPBi Aktuator Links - Elektrischer Fehler Offene Leitung | 0 | - |
| 0x480765 | EPBi Aktuator Rechts - Elektrischer Fehler Offene Leitung | 0 | - |
| 0x480766 | EPBi Aktuator Links - Elektrischer Kurzschluss GND oder KL30 | 0 | - |
| 0x480767 | EPBi Aktuator Rechts - Elektrischer Kurzschluss GND oder KL30 | 0 | - |
| 0x480768 | EPBi H-Brücke - Defekt | 0 | - |
| 0x480772 | Steuergerät intern - Plausibilität Temperatursensor | 0 | - |
| 0x48077C | RDCi Radelektronik vorn links Batterie Unterspannung | 1 | - |
| 0x48077D | RDCi Radelektronik vorn rechts Batterie Unterspannung | 1 | - |
| 0x48077E | RDCi Radelektronik hinten links Batterie Unterspannung | 1 | - |
| 0x48077F | RDCi Radelektronik hinten rechts Batterie Unterspannung | 1 | - |
| 0x480780 | RDCi Radelektronik Bandmode | 0 | - |
| 0x480781 | Steuergerät intern - Falsche Zuordnung von Hydraulikeinheit zu Anbausteuergerät | 0 | - |
| 0x48078A | Allradkupplung - Kupplungsposition offen, nur Frontantrieb | 0 | - |
| 0x48079B | Steuergerät intern - Transceiver - Unterspannung | 0 | - |
| 0x48079C | Steuergerät intern - Transceiver - Medium Temperatur | 0 | - |
| 0x4807BF | EPBi Initialisierung nicht durchgeführt | 0 | - |
| 0x4807C0 | Fahrzeugregler - Querbeschleunigung - Fehleramplitude zu groß Phase 2 und 3 | 0 | - |
| 0x4807C1 | Fahrzeugregler - Ist Lenkwinkel VA Rad - Fehleramplitude zu groß Phase 2 und 3 | 0 | - |
| 0x4807C2 | Fahrzeugregler - Giergeschwindigkeit - Fehleramplitude zu groß Phase 2 und 3 | 0 | - |
| 0x4807CC | Spannungsversorgung - Globale Überspannung extern | 1 | - |
| 0x4807CD | Spannungsversorgung - Globale Überspannung intern | 1 | - |
| 0x4807CE | Spannungsversorgung - Globale Unterspannung extern | 1 | - |
| 0x4807CF | Spannungsversorgung - Globale Unterspannung intern | 0 | - |
| 0x4807D0 | Spannungsversorgung - Lokale Überspannung | 0 | - |
| 0x4807D1 | Spannungsversorgung - Lokale Unterspannung | 0 | - |
| 0x480813 | EPBi - PBC - Links Mechanischer Fehler | 0 | - |
| 0x480814 | EPBi - PBC - Links Spannkraft nicht erreicht | 0 | - |
| 0x480816 | EPBi - PBC - Links schwergängig | 0 | - |
| 0x480818 | EPBi - PBC - Rechts Mechanischer Fehler | 0 | - |
| 0x480819 | EPBi - PBC - Rechts Spannkraft nicht erreicht | 0 | - |
| 0x48081B | EPBi - PBC - Rechts schwergängig | 0 | - |
| 0x480821 | EPBi LIN-Taster - Kommunikationsfehler | 0 | - |
| 0x480822 | EPBi LIN-Taster - Tasterfehler | 0 | - |
| 0x480826 | EPBi - PBC - Master Unbekannter Bremsenzustand | 0 | - |
| 0x480827 | EPBi - PBC - Intern Unbekannter Bremsenzustand | 0 | - |
| 0x480829 | Raddrehzahlsensor - Hinten Links - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082A | Raddrehzahlsensor - Hinten Rechts - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082B | Raddrehzahlsensor - Vorn Links - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082C | Raddrehzahlsensor - Vorn Rechts - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082F | Steuergerät intern - ROM / Flash Fehler | 0 | - |
| 0x480830 | Steuergerät intern - Conti - EEPROM Fehler - Ventildaten - defekt | 0 | - |
| 0x480831 | Drucksensor - Hauptzylinder - Integrität Funktionalität unzureichend | 0 | - |
| 0x480832 | Drucksensor Versorgungsspannung interne Bremsdrucksensoren außerhalb spezifizierten Bereich | 0 | - |
| 0x48083B | Peripherial/Funktional error Schnittstelle QDM Ist Lenkwinkel Vorderachse Signal temporär ungültig | 0 | - |
| 0x48083E | EPBi Spannungsversorgung Überspannung Funktionseinschränkung EPBi | 0 | - |
| 0x48083F | Raddrehzahlsensor - Vorn Links - Signal unplausibel | 0 | - |
| 0x480840 | Raddrehzahlsensor - Hinten Links - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x48084C | EPBi Spannungsversorgung Unterspannung Funktionseinschränkung EPBi | 0 | - |
| 0x48084D | Raddrehzahlsensor - Hinten Rechts - Signal unplausibel | 0 | - |
| 0x48084F | Raddrehzahlsensor - Vorn Links - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x480850 | Raddrehzahlsensor - Vorn Rechts - Signal unplausibel | 0 | - |
| 0x480864 | BEGU - Datenstand unplausibel | 0 | - |
| 0x480866 | EPBi LIN LED-Fehler | 0 | - |
| 0x480874 | Raddrehzahlsensor - Hinten Links - Signal unplausibel | 0 | - |
| 0x480875 | Raddrehzahlsensor - Hinten Rechts - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x48087B | Raddrehzahlsensor - Vorn Rechts - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x48087D | ECBA - Bremsscheibentemperatur überschreitet den erlaubten Schwellwert | 0 | - |
| 0x480894 | EPBi - PBC - EEPROM Fehler | 0 | - |
| 0x480895 | EPBi - PBC - Parameterfehler | 0 | - |
| 0x48089D | Drucksensor - Signal 1 im oberen Fehlerband | 0 | - |
| 0x48089E | Drucksensor - Signal 1 im unteren Fehlerband | 0 | - |
| 0x48089F | Drucksensor - Signal 2 im oberen Fehlerband | 0 | - |
| 0x4808A0 | Drucksensor - Signal 2 im unteren Fehlerband | 0 | - |
| 0x4808A1 | Drucksensor - Signal T1 außerhalb oberem Fehlerband | 0 | - |
| 0x4808A2 | Drucksensor - Signal T1 außerhalb unterem Fehlerband | 0 | - |
| 0x4808A3 | Drucksensor - Signal T2 außerhalb oberem Fehlerband | 0 | - |
| 0x4808A4 | Drucksensor - Signal T2 außerhalb unterem Fehlerband | 0 | - |
| 0x4808A5 | Systemdrucksensor - Fehlerhafte Versorgungsspannung | 0 | - |
| 0x4808A6 | Systemdrucksensor - Signal 1 im oberen Fehlerband | 0 | - |
| 0x4808A7 | Systemdrucksensor - Signal 1 im unteren Fehlerband | 0 | - |
| 0x4808A8 | Systemdrucksensor - Signalsstörung oder Signalfehler | 0 | - |
| 0x4808A9 | Systemdrucksensor - Konfigurationsdatenfehler | 0 | - |
| 0x4808AA | Systemdrucksensor - Signal 2 im oberen Fehlerband | 0 | - |
| 0x4808AB | Systemdrucksensor - Kommunikationsdatenfehler | 0 | - |
| 0x4808AC | Systemdrucksensor - Signalsstörung oder Signalfehler des Temperatursensor | 0 | - |
| 0x4808AD | Systemdrucksensor - Signal 2 im unteren Fehlerband | 0 | - |
| 0x4808AE | Systemdrucksensor - Signalintegrität gestört | 0 | - |
| 0x4808AF | Systemdrucksensor - Signal T1 außerhalb oberen Fehlerband | 0 | - |
| 0x4808B0 | Systemdrucksensor - Signal T1 außerhalb unterem Fehlerband | 0 | - |
| 0x4808B1 | Systemdrucksensor - Signal T2 außerhalb oberen Fehlerband | 0 | - |
| 0x4808B2 | Systemdrucksensor - Signal T2 außerhalb unterem Fehlerband | 0 | - |
| 0x4808B3 | Systemdruck unplausibel zu niedrig | 0 | - |
| 0x4808B4 | Systemdruck unplausibel zu hoch | 0 | - |
| 0x4808B5 | THZ Wegsensor - elektrischer Fehler | 0 | - |
| 0x4808B6 | THZ Wegsensor - Offset Fehler | 0 | - |
| 0x4808B7 | THZ Wegsensor - EEPROM Fehler | 0 | - |
| 0x4808B8 | THZ Wegsensor - Signal Fehler | 0 | - |
| 0x4808B9 | IB Motor - Positionssensor elektrischer Fehler | 0 | - |
| 0x4808BA | IB Motor - Winkelfehler | 0 | - |
| 0x4808BB | IB Motor - Winkelausrichtung fehlerhaft | 0 | - |
| 0x4808BC | IB Motor - Stromsensor-Fehler | 0 | - |
| 0x4808BD | IB Motor - Temperatur zu hoch | 0 | - |
| 0x4808BE | IB Motor - Ausgangsspannung zu niedrig | 0 | - |
| 0x4808BF | IB Motor - Ausgangsspannung zu hoch | 0 | - |
| 0x4808C1 | IB Motor - Winkelsignal unplausibel | 0 | - |
| 0x4808C4 | Steuergerät intern - Spannungsversorgung Sensoren - Kurzschluss nach Masse | 0 | - |
| 0x4808C5 | Steuergerät intern - Spannungsversorgung Sensoren - Kurzschluss nach Plus | 0 | - |
| 0x4808C6 | Steuergerät intern - B6Brücke - Übertemperatur | 0 | - |
| 0x4808C7 | Steuergerät intern - B6Brücke - Ausgangsspannung zu niedrig | 0 | - |
| 0x4808C8 | Steuergerät intern - B6Brücke - Ausgangsspannung zu hoch | 0 | - |
| 0x4808C9 | Steuergerät intern - B6Brücke -  elektrischer Fehler | 0 | - |
| 0x4808CA | Steuergerät intern - B6Brücke - Treiberfehler | 0 | - |
| 0x4808CB | Steuergerät intern - THZ Kolbenfehler | 0 | - |
| 0x4808CF | Steuergerät intern - Selbsttestfehler | 0 | - |
| 0x4808D1 | Druckzuschaltventil - Primärkreis unerwartet offen | 0 | - |
| 0x4808D2 | Druckzuschaltventil - Primärkreis unerwartet geschlossen | 0 | - |
| 0x4808D3 | Druckzuschaltventil - Sekundärkreis unerwartet offen | 0 | - |
| 0x4808D4 | Druckzuschaltventil - Sekundärkreis unerwartet geschlossen | 0 | - |
| 0x4808D5 | Fahrertrennventil - Primärkreis unerwartet offen | 0 | - |
| 0x4808D6 | Fahrertrennventil - Primärkreis unerwartet geschlossen | 0 | - |
| 0x4808D7 | Fahrertrennventil - Sekundärkreis unerwartet offen | 0 | - |
| 0x4808D8 | Fahrertrennventil - Sekundärkreis unerwartet geschlossen | 0 | - |
| 0x4808D9 | Ventilgruppe - elektrischer Fehler | 0 | - |
| 0x4808DA | Volumenüberwachung unplausibel | 0 | - |
| 0x4808DB | Lufteintrag in LAC Kreis zu hoch | 0 | - |
| 0x4808DD | Lufteintrag in THZ Kreis zu hoch | 0 | - |
| 0x4808DE | Große Leckage im Primär Radbremskreis | 0 | - |
| 0x4808DF | Große Leckage im Sekundär Radbremskreis | 0 | - |
| 0x4808E0 | Lufteintrag im by-wire Kreis zu hoch | 0 | - |
| 0x4808E3 | EPBi - PBC - Ausfall dynamische Abbremsung | 0 | - |
| 0x4808E9 | Steuergerät intern - IPEX - Treiberfehler | 0 | - |
| 0x4808EC | EPBi - PBC - Links elektrischer Fehler | 0 | - |
| 0x4808ED | EPBi - PBC - Rechts elektrischer Fehler | 0 | - |
| 0x4808F0 | Bremsflüssigkeit - Bremsflüssigkeitsleckage im Bremssystem erkannt | 0 | - |
| 0x4808F1 | Bremsflüssigkeitssensor - Niedriger Bremsflüssigkeitsstand erste Warnstufe | 0 | - |
| 0x4808F2 | Schnittstelle QDM - Ist Lenkwinkel Hinterachse - Signal unplausibel | 0 | - |
| 0x4808F3 | Schnittstelle QDM - Ist Lenkwinkel Hinterachse - Initialisierung Signal ungültig | 0 | - |
| 0x4808F6 | Steuergerät intern - Verpolschutz-FET funktioniert nicht | 0 | - |
| 0x4808F7 | Steuergerät intern - MCU Startup-Fehler | 0 | - |
| 0x4808F8 | Steuergerät intern - KL30_M Unterspannung | 0 | - |
| 0x4808F9 | Steuergerät intern - KL30_M Überspannung | 0 | - |
| 0x4808FA | Steuergerät intern - elektrischer Fehler beim LOW-Side-Treiber oder Magnetventilen | 0 | - |
| 0x4808FD | Spannungsversorgung - KL30_1 Unterbrechung | 0 | - |
| 0x4808FE | Spannungsversorgung - KL30_2 Unterbrechung | 0 | - |
| 0x4808FF | Raddrehzahlsensor - Hinten Links - Interne Schnittstelle fehlerhaft | 0 | - |
| 0x480900 | Raddrehzahlsensor - Hinten Rechts - Interne Schnittstelle fehlerhaft | 0 | - |
| 0x480901 | Raddrehzahlsensor - Vorn Links - Interne Schnittstelle fehlerhaft | 0 | - |
| 0x480902 | Raddrehzahlsensor - Vorn Rechts - Interne Schnittstelle fehlerhaft | 0 | - |
| 0x480903 | Luftfeder - Fehler - RPA deaktiviert | 0 | - |
| 0x480907 | Schnittstelle QDM - Ackermannsollgierrate - Signal ungültig | 0 | - |
| 0x480908 | Steuergerät intern - A/D-Wandler - defekt | 0 | - |
| 0x48090A | Globales Powermanagement - Reduzierung elektrischer Leistungsaufnahme | 0 | - |
| 0x48090B | EPBi - Überlast Leistungselektronik | 0 | - |
| 0x48090C | EPBi H-Brücke - Spannungsfehler | 0 | - |
| 0x48091C | Steuergerät intern - Betriebssystem - MCU-Fehler | 0 | - |
| 0x480928 | Raddrehzahlsensor - Vorn Links - Fehlender Zahn | 0 | - |
| 0x480932 | Bremsflüssigkeitssensor - Bremsflüssigkeitsstand zu niedrig | 0 | - |
| 0x480975 | Steuergerät intern - Transceiver - VIO Fehler | 0 | - |
| 0x480976 | Steuergerät intern - Transceiver - Übertemperatur | 0 | - |
| 0x4809AD | Steuergerät intern - Transceiver - Babbling Idiot | 0 | - |
| 0x4809B0 | Raddrehzahlsensor - Vorn Links - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809B7 | Raddrehzahlsensor - Hinten Links - Fehlender Zahn | 0 | - |
| 0x4809B9 | Raddrehzahlsensor - Hinten Links - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809C0 | Lokale Spannungsversorgung - Steuergeräte Reset | 0 | - |
| 0x4809C2 | Raddrehzahlsensor - Hinten Rechts - Fehlender Zahn | 0 | - |
| 0x4809CB | Raddrehzahlsensor - Vorn Rechts - Fehlender Zahn | 0 | - |
| 0x4809CD | Raddrehzahlsensor - Vorn Rechts - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809D7 | Steuergerät intern - Busfehler - Fehler Failsafe Schaltung | 0 | - |
| 0x4809D8 | Steuergerät intern - Busfehler - Fehler Memory Access | 0 | - |
| 0x4809DB | Steuergerät intern - Transceiver - VCC Fehler | 0 | - |
| 0x4809DF | Fahrzeugregler - Giergeschwindigkeit - Phase 1: Fehleramplitude zu groß | 0 | - |
| 0x4809EA | RDCi Radelektronik Position unbekannt defekt | 0 | - |
| 0x4809EB | RDCi Radelektronik (Position unbekannt) kein Empfang | 0 | - |
| 0x480A08 | Drucksensor - Hauptzylinder - Leitungsfehler | 0 | - |
| 0x480A11 | Bremsbelagsensor - Vorderachse - Verschleissgrenze erreicht | 0 | - |
| 0x480A12 | Bremsbelagsensor - Hinterachse - Verschleissgrenze erreicht | 0 | - |
| 0x480A22 | Drucksensor - nicht kalibriert | 0 | - |
| 0x480A46 | RDCi Gateway oder Antennen Fehler | 0 | - |
| 0x480A47 | FUSI - Übergang aktiv | 1 | - |
| 0x480A69 | Drucksensor - Hauptzylinder - Impulstest fehlgeschlagen | 0 | - |
| 0x480A8B | Drucksensor - Interne Plausibilisierung fehlgeschlagen | 0 | - |
| 0x480A8D | Drucksensor - Plausibilisierung Temperatur intern | 0 | - |
| 0x480A91 | Drucksensor - Hauptzylinder - Offsetfehler | 0 | - |
| 0x480A92 | Raddrehzahlsensor - Allgemein - Unterspannung bei aktiven Anfahrassistenten | 0 | - |
| 0x480A9B | Fahrzeugregler Dauerregelung | 0 | - |
| 0x480A9D | Raddrehzahlsensor - Vorn Links - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480A9E | Raddrehzahlsensor - Vorn Links - unerwarteter Signalsprung | 0 | - |
| 0x480A9F | Raddrehzahlsensor - Vorn Links - Rauschüberwachung | 0 | - |
| 0x480AA0 | Steuergerät intern - Falscher HW Musterstand oder nicht freigegebene Software | 0 | - |
| 0x480AA4 | Raddrehzahlsensor - Vorn Rechts - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AA5 | Raddrehzahlsensor - Vorn Rechts - unerwarteter Signalsprung | 0 | - |
| 0x480AA6 | Raddrehzahlsensor - Vorn Rechts - Rauschüberwachung | 0 | - |
| 0x480AAB | Raddrehzahlsensor - Hinten Links - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AAC | Raddrehzahlsensor - Hinten Links - unerwarteter Signalsprung | 0 | - |
| 0x480AAD | Raddrehzahlsensor - Hinten Links - Rauschüberwachung | 0 | - |
| 0x480AB2 | Raddrehzahlsensor - Hinten Rechts - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AB3 | Raddrehzahlsensor - Hinten Rechts - unerwarteter Signalsprung | 0 | - |
| 0x480AB4 | Raddrehzahlsensor - Hinten Rechts - Rauschüberwachung | 0 | - |
| 0x480AC0 | Codierung - Falsche Antriebsvariante Allrad | 0 | - |
| 0x480ACA | EPBi Initialisierung nach Montagemodus nicht durchgeführt | 0 | - |
| 0x480ACE | eRFS Codierdaten inkonsistent | 0 | - |
| 0x480AD5 | Steuergerät intern - Zwischenkreiskondensatoren - Temperatur zu hoch | 0 | - |
| 0x480AE3 | EPBi - Host - Sicherheitsbedingungen nicht erfüllt | 0 | - |
| 0x480AE4 | Schnittstelle QDM - Ist Lenkwinkel Vorderachse - Signal unplausibel | 0 | - |
| 0x480AE5 | Schnittstelle QDM - Giergeschwindigkeit Fahrzeug - Signal unplausibel | 0 | - |
| 0x480AE6 | Schnittstelle QDM - Querbeschleunigung Schwerpunkt - Signal unplausibel | 0 | - |
| 0x480AE7 | Schnittstelle QDM - Längsbeschleunigung Schwerpunkt - Signal unplausibel | 0 | - |
| 0x480AE8 | IB Motor - Motorbewegung ohne Anforderung | 0 | - |
| 0x480AEA | Steuergerät intern - Dämpfer-Diode funktioniert nicht | 0 | - |
| 0x480AF5 | Steuergerät intern - LAC - Maximale Anzahl der Umdrehungen überschritten | 0 | - |
| 0x480AF6 | Steuergerät intern - LAC - Nullpunkterkennung Timeout | 0 | - |
| 0x480AF8 | Bremsflüssigkeitssensor - Kurzschluss Sensorleitungen nach Masse | 0 | - |
| 0x480AF9 | Bremsflüssigkeitssensor - Kurzschluss Sensorleitungen nach Plus | 0 | - |
| 0x480AFA | Bremsflüssigkeitssensor - Kurzschluss Sensorleitungen gegeneinander | 0 | - |
| 0x480AFB | Bremsflüssigkeitssensor - Leitungsunterbrechung | 0 | - |
| 0x480AFC | Bremsflüssigkeitssensor - Signal unplausibel | 0 | - |
| 0x480AFD | Produktionsstatus - Inbetriebnahme nicht abgeschlossen; System nicht verfügbar | 0 | - |
| 0x480B01 | Codierung - Anhängersteuergerät verbaut, aber Anhängerschlingerlogik nicht eincodiert | 0 | - |
| 0x480B1E | Steuergerät intern - Betriebssystem - Watchdog-Fehler | 0 | - |
| 0x480B2F | Steuergerät intern - MCU ADC nicht kalibriert | 0 | - |
| 0x480B30 | Steuergerät intern - Interner Selbsttest des MCU ADC Moduls fehlgeschlagen | 0 | - |
| 0x480B3C | Stillstandsmanagement - maximale Haltezeit überschritten | 0 | - |
| 0x480B3D | Stillstandsmanagement - Fahrzeug rollt trotz maximaler Druckanforderung an den Bremsen | 0 | - |
| 0x480B3F | Steuergerät intern - Rotormagnet - Temperatur zu hoch | 0 | - |
| 0x480B40 | Steuergerät intern - LAC Kolben klemmt | 0 | - |
| 0x480B42 | Steuergerät intern - P1 Drucksensorsignal-Offset außerhalb Wertebereich | 0 | - |
| 0x480B43 | Steuergerät intern - P2 Drucksensorsignal-Offset außerhalb Wertebereich | 0 | - |
| 0x480B44 | Steuergerät intern - Niedrige Effizienz des Nachsaugzyklus | 0 | - |
| 0x480B45 | Steuergerät intern - Timeout Nachsaugzyklus | 0 | - |
| 0x480B46 | Steuergerät intern - LAC Gradient außerhalb der Arbeitsgrenzen | 0 | - |
| 0x480B47 | Steuergerät intern - LAC Position vorne außerhalb der Arbeitsgrenzen | 0 | - |
| 0x480B48 | Steuergerät intern - LAC Position hinten außerhalb der Arbeitsgrenzen | 0 | - |
| 0x480B49 | Steuergerät intern - Systemdruck gegenüber Motormoment unplausibel | 0 | - |
| 0x480B4A | Kleine Leckage im Radbremskreis | 0 | - |
| 0x480B4B | Große Leckage im Radbremskreis | 0 | - |
| 0x480B4C | Leckage in der Druckkreis-Primärmanschette | 0 | - |
| 0x480B4D | Steuergerät intern - 5V Spannungsversorgung außerhalb des gültigen Bereichs | 0 | - |
| 0x480B4E | GDU PWM Feedback Signale unplausibel | 0 | - |
| 0x480B52 | Steuergerät intern - Unplausibel hohe Verzögerung des Längstbeschleunigungsregler (ACC, iBrake,..) | 0 | - |
| 0x480B53 | Steuergerät intern - Unplausibel niedrige Verzögerung des Längsbeschleunigungsreglers (ACC, iBrake,..) | 0 | - |
| 0x480B54 | Codierung - ABS Rückfallebene aktiv | 0 | - |
| 0x480B57 | EPBi - Unterdrückung einer Löseanforderung durch RSU | 1 | - |
| 0x480B5C | Steuergerät intern - Betriebssystem - Kritischer Ausnahmefehler | 0 | - |
| 0x480B7F | EPBi - potenzielles Restbremsmoment erkannt | 0 | - |
| 0xD3441F | FLEXRAY Physical bus error | 0 | - |
| 0xD34420 | FLEXRAY controller error | 0 | - |
| 0xD34487 | FLEXRAY StartUpFailed | 0 | - |
| 0xD34BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xD35418 | Botschaft(Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) fehlt | 1 | - |
| 0xD35419 | Botschaft(Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) Prüfsumme falsch | 1 | - |
| 0xD3541A | Botschaft(Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) nicht aktuell | 1 | - |
| 0xD35428 | Botschaft(Außentemperatur, ID: A_TEMP) fehlt | 1 | - |
| 0xD3542C | Signal(Außentemperatur, ID: A_TEMP) ungültig | 1 | - |
| 0xD35442 | Signal(Bedienung Fahrwerk, ID: BEDIENUNG_FAHRWERK) ungültig | 1 | - |
| 0xD35445 | Botschaft(Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) Prüfsumme falsch | 1 | - |
| 0xD35476 | Signal(Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) ungültig | 1 | - |
| 0xD354A9 | Botschaft(Fehlerspeicher Bordnetz Spannung, ID: ERRM_BN_U) fehlt | 1 | - |
| 0xD354AA | Signal(Fehlerspeicher Bordnetz Spannung, ID: ERRM_BN_U) ungültig | 1 | - |
| 0xD354AB | Signal(Fehlerspeicher Bordnetz Spannung, ID: ERRM_BN_U) undefiniert | 1 | - |
| 0xD354B6 | Signal(Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) ungültig | 1 | - |
| 0xD354B8 | Botschaft(Geschwindigkeit Fahrzeug, ID: V_VEH) fehlt | 1 | - |
| 0xD354B9 | Botschaft(Geschwindigkeit Fahrzeug, ID: V_VEH) Prüfsumme falsch | 1 | - |
| 0xD354BA | Botschaft(Geschwindigkeit Fahrzeug, ID: V_VEH) nicht aktuell | 1 | - |
| 0xD354BE | Signal(Geschwindigkeit Fahrzeug, ID: V_VEH) ungültig | 1 | - |
| 0xD354BF | Signal(Geschwindigkeit Fahrzeug, ID: V_VEH) undefiniert | 1 | - |
| 0xD354C2 | Botschaft(Giergeschwindigkeit Fahrzeug, ID: VYAW_VEH) fehlt | 1 | - |
| 0xD354C3 | Botschaft(Giergeschwindigkeit Fahrzeug, ID: VYAW_VEH) Prüfsumme falsch | 1 | - |
| 0xD354C4 | Botschaft(Giergeschwindigkeit Fahrzeug, ID: VYAW_VEH) nicht aktuell | 1 | - |
| 0xD354C8 | Signal(Giergeschwindigkeit Fahrzeug, ID: VYAW_VEH) ungültig | 1 | - |
| 0xD354C9 | Signal(Giergeschwindigkeit Fahrzeug, ID: VYAW_VEH) undefiniert | 1 | - |
| 0xD354E5 | Botschaft(Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) Prüfsumme falsch | 1 | - |
| 0xD354E8 | Botschaft(Ist Lenkwinkel Vorderachse, ID: AVL_STEA_FTAX) fehlt | 1 | - |
| 0xD354E9 | Botschaft(Ist Lenkwinkel Vorderachse, ID: AVL_STEA_FTAX) Prüfsumme falsch | 1 | - |
| 0xD354EA | Botschaft(Ist Lenkwinkel Vorderachse, ID: AVL_STEA_FTAX) nicht aktuell | 1 | - |
| 0xD354EE | Signal(Ist Lenkwinkel Vorderachse, ID: AVL_STEA_FTAX) ungültig | 1 | - |
| 0xD354EF | Signal(Ist Lenkwinkel Vorderachse, ID: AVL_STEA_FTAX) undefiniert | 1 | - |
| 0xD354FF | Botschaft(Zustand Fahrzeug, ID: CON_VEH) Prüfsumme falsch | 1 | - |
| 0xD35513 | Botschaft(Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) nicht aktuell | 1 | - |
| 0xD3551C | Signal(Längsbeschleunigung Schwerpunkt, ID: ACLNX_MASSCNTR) ungültig | 1 | - |
| 0xD3551D | Signal(Längsbeschleunigung Schwerpunkt, ID: ACLNX_MASSCNTR) undefiniert | 1 | - |
| 0xD35526 | Signal(Lenkwinkel Vorderachse Effektiv, ID: STEA_FTAX_EFFV) ungültig | 1 | - |
| 0xD35527 | Signal(Lenkwinkel Vorderachse Effektiv, ID: STEA_FTAX_EFFV, ID:STEA_FTAX_EFFV) undefiniert | 1 | - |
| 0xD35538 | Botschaft(Neigung Fahrbahn, ID: TLT_RW) fehlt | 1 | - |
| 0xD35539 | Botschaft(Neigung Fahrbahn, ID: TLT_RW) Prüfsumme falsch | 1 | - |
| 0xD3553A | Botschaft(Neigung Fahrbahn, ID: TLT_RW) nicht aktuell | 1 | - |
| 0xD3553E | Signal(Neigung Fahrbahn, ID: TLT_RW) ungültig | 1 | - |
| 0xD3553F | Signal(Neigung Fahrbahn, ID: TLT_RW) undefiniert | 1 | - |
| 0xD35542 | Botschaft(Querbeschleunigung Schwerpunkt, ID: ACLNY_MASSCNTR) fehlt | 1 | - |
| 0xD35543 | Botschaft(Querbeschleunigung Schwerpunkt, ID: ACLNY_MASSCNTR) Prüfsumme falsch | 1 | - |
| 0xD35544 | Botschaft(Querbeschleunigung Schwerpunkt, ID: ACLNY_MASSCNTR) nicht aktuell | 1 | - |
| 0xD35548 | Signal(Querbeschleunigung Schwerpunkt, ID: ACLNY_MASSCNTR) ungültig | 1 | - |
| 0xD35549 | Signal(Querbeschleunigung Schwerpunkt, ID: ACLNY_MASSCNTR) undefiniert | 1 | - |
| 0xD35565 | Botschaft(Zustand Fahrzeug, ID: CON_VEH) nicht aktuell | 1 | - |
| 0xD35570 | Botschaft(Radmoment Antrieb 4, ID: WMOM_DRV_4) fehlt | 1 | - |
| 0xD35571 | Botschaft(Radmoment Antrieb 4, ID: WMOM_DRV_4) Prüfsumme falsch | 1 | - |
| 0xD35572 | Botschaft(Radmoment Antrieb 4, ID: WMOM_DRV_4) nicht aktuell | 1 | - |
| 0xD3557A | Signal(Radmoment Antrieb 4, ID: WMOM_DRV_4) ungültig | 1 | - |
| 0xD3557B | Signal(Radmoment Antrieb 4, ID: WMOM_DRV_4) undefiniert | 1 | - |
| 0xD35586 | Botschaft(Regensensor-Wischergeschwindigkeit, ID: WISCHERGESCHWINDIGKEIT) fehlt | 1 | - |
| 0xD3558A | Signal(Regensensor-Wischergeschwindigkeit, ID: WISCHERGESCHWINDIGKEIT) ungültig | 1 | - |
| 0xD355CA | Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) fehlt | 1 | - |
| 0xD355CB | Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) Prüfsumme falsch | 1 | - |
| 0xD355CC | Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) nicht aktuell | 1 | - |
| 0xD355D0 | Signal(Status Lenkung Hinterachse, ID: ST_STE_BAX) ungültig | 1 | - |
| 0xD355D1 | Signal(Status Lenkung Hinterachse, ID: ST_STE_BAX) undefiniert | 1 | - |
| 0xD3560C | Botschaft(Zustand Fahrzeug, ID: CON_VEH) fehlt | 1 | - |
| 0xD35646 | Botschaft(Winkel Fahrpedal, ID: ANG_ACPD) fehlt | 1 | - |
| 0xD35647 | Botschaft(Winkel Fahrpedal, ID: ANG_ACPD) Prüfsumme falsch | 1 | - |
| 0xD35648 | Botschaft(Winkel Fahrpedal, ID: ANG_ACPD) nicht aktuell | 1 | - |
| 0xD3564C | Signal(Winkel Fahrpedal, ID: ANG_ACPD) ungültig | 1 | - |
| 0xD3564D | Signal(Winkel Fahrpedal, ID: ANG_ACPD) undefiniert | 1 | - |
| 0xD3565E | Signal(Zustand Fahrzeug, ID: CON_VEH) ungültig | 1 | - |
| 0xD3567D | Botschaft(Einheiten BN2020, ID: EINHEITEN_BN2020) fehlt | 1 | - |
| 0xD35694 | Botschaft(RDC Daten Paket 1, ID: RDC_DT_PCKG_1) fehlt | 1 | - |
| 0xD3569B | Botschaft(Diagnose OBD Motor, ID:DIAG_OBD_ENG) fehlt | 1 | - |
| 0xD356A0 | Botschaft(Status Crash, ID: ST_CR) Prüfsumme falsch | 1 | - |
| 0xD356E4 | Botschaft(Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) fehlt | 1 | - |
| 0xD356E5 | Botschaft(Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) Prüfsumme falsch | 1 | - |
| 0xD356E6 | Botschaft(Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) nicht aktuell | 1 | - |
| 0xD356F5 | Botschaft(Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) fehlt | 1 | - |
| 0xD356F6 | Botschaft(Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) nicht aktuell | 1 | - |
| 0xD35713 | Signal(Einheiten BN2020, ID: EINHEITEN_BN2020) ungültig | 1 | - |
| 0xD35720 | Botschaft(RDC Daten Paket 1, ID: RDC_DT_PCKG_1) nicht aktuell | 1 | - |
| 0xD35744 | Botschaft(Daten Antriebsstrang 2, ID: DT_PT_2) fehlt | 1 | - |
| 0xD35745 | Botschaft(Daten Antriebsstrang 2, ID: DT_PT_2) Prüfsumme falsch | 1 | - |
| 0xD35746 | Botschaft(Daten Antriebsstrang 2, ID: DT_PT_2) nicht aktuell | 1 | - |
| 0xD35777 | Signal(RDC Daten Paket 1, ID: RDC_DT_PCKG_1) ungültig | 1 | - |
| 0xD35799 | Signal(Diagnose OBD Motor, ID:DIAG_OBD_ENG) ungültig | 1 | - |
| 0xD35858 | Signal(Zustand Fahrzeug, ID: CON_VEH) undefiniert | 1 | - |
| 0xD358BE | Botschaft(Status Crash, ID: ST_CR) fehlt | 1 | - |
| 0xD358E1 | Botschaft(Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) fehlt | 1 | - |
| 0xD358F8 | Signal(Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) ungültig | 1 | - |
| 0xD358F9 | Signal(Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) undefiniert | 1 | - |
| 0xD35902 | Signal(Status Crash, ID: ST_CR) undefiniert | 1 | - |
| 0xD35938 | Signal(Status Crash, ID: ST_CR) ungültig | 1 | - |
| 0xD35966 | Signal(Status Verbrennungsmotor, ID: ST_CENG) ungültig | 1 | - |
| 0xD35973 | Botschaft(Status Crash, ID: ST_CR) nicht aktuell | 1 | - |
| 0xD359AB | Signal(Daten Antriebsstrang 2, ID: DT_PT_2) ungültig | 1 | - |
| 0xD359CC | Botschaft(Status Verbrennungsmotor, ID: ST_CENG) fehlt | 1 | - |
| 0xD359DF | Botschaft(Relativzeit BN2020, ID: RELATIVZEIT) fehlt | 1 | - |
| 0xD35A38 | Signal(Status Verbrennungsmotor, ID: ST_CENG) undefiniert | 1 | - |
| 0xD35AE9 | Signal(Relativzeit BN2020, ID: RELATIVZEIT) ungültig | 1 | - |
| 0xD35B2C | Botschaft(Längsbeschleunigung Schwerpunkt, ID: ACLNX_MASSCNTR) fehlt | 1 | - |
| 0xD35B2E | Botschaft(Längsbeschleunigung Schwerpunkt, ID: ACLNX_MASSCNTR) Prüfsumme falsch | 1 | - |
| 0xD35B2F | Botschaft(Längsbeschleunigung Schwerpunkt, ID: ACLNX_MASSCNTR) nicht aktuell | 1 | - |
| 0xD35B36 | Botschaft(Lenkwinkel Vorderachse Effektiv, ID: STEA_FTAX_EFFV) fehlt | 1 | - |
| 0xD35B37 | Botschaft(Lenkwinkel Vorderachse Effektiv, ID: STEA_FTAX_EFFV) Prüfsumme falsch | 1 | - |
| 0xD35B38 | Botschaft(Lenkwinkel Vorderachse Effektiv, ID: STEA_FTAX_EFFV) nicht aktuell | 1 | - |
| 0xD35C61 | Botschaft(Anforderung Radmoment Antriebsstrang Summe Soll Begrenzung, ID: FAS:RQ_WMOM_PT_SUM_TAR_LIM_DRS) fehlt | 1 | - |
| 0xD35C6B | Botschaft(Momentenpotential Antriebsstrang, ID: TPO_PT) fehlt | 1 | - |
| 0xD35C70 | Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) fehlt | 1 | - |
| 0xD35C71 | Botschaft(Radmoment Antrieb 9, ID: WMOM_DRV_9) fehlt | 1 | - |
| 0xD35C7C | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) fehlt | 1 | - |
| 0xD35CBA | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) fehlt | 1 | - |
| 0xD35CCA | Botschaft(Fehler_Status_EPB_LIN, ID: ERR_ST_EPB_LIN) fehlt | 1 | - |
| 0xD35CDD | Botschaft(Status Niveauregulierung Fahrzeug 2, ID: ST_LCS_VEH_2) fehlt | 1 | - |
| 0xD35CE6 | Botschaft(Radmoment Antrieb 9, ID: WMOM_DRV_9) nicht aktuell | 1 | - |
| 0xD35CE9 | Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) nicht aktuell | 1 | - |
| 0xD35CF5 | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) nicht aktuell | 1 | - |
| 0xD35CFB | Botschaft(Momentenpotential Antriebsstrang, ID: TPO_PT) nicht aktuell | 1 | - |
| 0xD35D25 | Botschaft(Fehler_Status_EPB_LIN, ID: ERR_ST_EPB_LIN) nicht aktuell | 1 | - |
| 0xD35D2F | Botschaft(Status Niveauregulierung Fahrzeug 2, ID: ST_LCS_VEH_2) nicht aktuell | 1 | - |
| 0xD35D43 | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) nicht aktuell | 1 | - |
| 0xD35D53 | Signal(Status_EPB_LIN, ID: ST_EPB_LIN) undefiniert | 1 | - |
| 0xD35D57 | Signal(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) undefiniert | 1 | - |
| 0xD35D58 | Signal(Radmoment Antrieb 9, ID: WMOM_DRV_9) undefiniert | 1 | - |
| 0xD35D5D | Signal(Momentenpotential Antriebsstrang, ID: TPO_PT) undefiniert | 1 | - |
| 0xD35D61 | Signal(Anforderung Radmoment Antriebsstrang Summe Soll Begrenzung, ID: FAS:RQ_WMOM_PT_SUM_TAR_LIM_DRS) undefiniert | 1 | - |
| 0xD35D7F | Signal(Status_EPB_LIN, ID: ST_EPB_LIN) undefiniert | 1 | - |
| 0xD35D8E | Signal(Fehler_Status_EPB_LIN, ID: ERR_ST_EPB_LIN) undefiniert | 1 | - |
| 0xD35DA9 | Signal(Radmoment Antrieb 9, ID: WMOM_DRV_9) ungültig | 1 | - |
| 0xD35DAB | Signal(Status_EPB_LIN, ID: ST_EPB_LIN) ungültig | 1 | - |
| 0xD35DC3 | Signal(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) ungültig | 1 | - |
| 0xD35DC4 | Signal(Anforderung Radmoment Antriebsstrang Summe Soll Begrenzung, ID: FAS:RQ_WMOM_PT_SUM_TAR_LIM_DRS) ungültig | 1 | - |
| 0xD35DC7 | Signal(Fehler_Status_EPB_LIN, ID: ERR_ST_EPB_LIN) ungültig | 1 | - |
| 0xD35DCC | Signal(Status_EPB_LIN, ID: ST_EPB_LIN) ungültig | 1 | - |
| 0xD35DCF | Signal(Momentenpotential Antriebsstrang, ID: TPO_PT) ungültig | 1 | - |
| 0xD35E32 | Botschaft(Momentenpotential Antriebsstrang, ID: TPO_PT) Prüfsumme falsch | 1 | - |
| 0xD35E36 | Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) Prüfsumme falsch | 1 | - |
| 0xD35E4C | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) Prüfsumme falsch | 1 | - |
| 0xD35E4D | Botschaft(Radmoment Antrieb 9, ID: WMOM_DRV_9) Prüfsumme falsch | 1 | - |
| 0xD35E5C | Botschaft(Status_EPB_LIN, ID: ST_EPB_LIN) Prüfsumme falsch | 1 | - |
| 0xD35E68 | Botschaft(Fehler_Status_EPB_LIN, ID: ERR_ST_EPB_LIN) Prüfsumme falsch | 1 | - |
| 0xD35ED9 | Signal(Status Niveauregulierung Fahrzeug 2, ID: ST_LCS_VEH_2) undefiniert | 1 | - |
| 0xD35F0B | Signal(Status Niveauregulierung Fahrzeug 2, ID: ST_LCS_VEH_2) ungültig | 1 | - |
| 0xD35F3A | D-OBD 1 - ICM oder ACSM - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35F3B | D-OBD 1 - ICM oder ACSM - OBD-Diagnosestatusbotschaft Timeout | 1 | - |
| 0xD35F3C | D-OBD 1 - ICM oder ACSM - Zähler Alive | 1 | - |
| 0xD35F40 | D-OBD 3 - EPS - Zähler Alive | 1 | - |
| 0xD35F41 | D-OBD 3 - EPS - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35F42 | D-OBD 3 - EPS - OBD-Diagnosestatusbotschaft Timeout | 1 | - |
| 0xD35F47 | D-OBD 1 - ICM oder ACSM - CVN und/oder CALID unplausibel | 1 | - |
| 0xD35F4D | D-OBD 3 - EPS - CVN und/oder CALID unplausibel | 1 | - |
| 0xD35F5A | D-OBD 5 - HSR - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35F5B | D-OBD 5 - HSR - OBD-Diagnosestatusbotschaft Timeout | 1 | - |
| 0xD35F5C | D-OBD 5 - HSR - Zähler Alive | 1 | - |
| 0xD35F5D | D-OBD 5 - HSR - CVN und/oder CALID unplausibel | 1 | - |
| 0xD35F61 | D-OBD 6 - VIP - CVN und/oder CALID unplausibel | 1 | - |
| 0xD35F62 | D-OBD 6 - VIP - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35F63 | D-OBD 6 - VIP - OBD-Diagnosestatusbotschaft Timeout | 1 | - |
| 0xD35F64 | D-OBD 6 - VIP - Zähler Alive | 1 | - |
| 0xD35F91 | Botschaft(Status Niveauregulierung Fahrzeug 2, ID: ST_LCS_VEH_2) Prüfsumme falsch | 1 | - |
| 0xD36420 | Botschaft(Daten Einspurmodell Fahrdynamik 2, ID: DT_STMD_DRDY_2) fehlt | 1 | - |
| 0xD36421 | Botschaft(Daten Einspurmodell Fahrdynamik 2, ID: DT_STMD_DRDY_2) nicht aktuell | 1 | - |
| 0xD36422 | Botschaft(Daten Einspurmodell Fahrdynamik 2, ID: DT_STMD_DRDY_2) Prüfsumme falsch | 1 | - |
| 0xD36423 | Signal(Daten Einspurmodell Fahrdynamik 2, ID: DT_STMD_DRDY_2) undefiniert | 1 | - |
| 0xD36424 | Signal(Daten Einspurmodell Fahrdynamik 2, ID: DT_STMD_DRDY_2) ungültig | 1 | - |
| 0xD36425 | Botschaft(Interne Kommunikation VIP-BRS 1, ID: INTL_KOMM_VIP_BRS_1) fehlt | 1 | - |
| 0xD36426 | Botschaft(Interne Kommunikation VIP-BRS 1, ID: INTL_KOMM_VIP_BRS_1) nicht aktuell | 1 | - |
| 0xD36427 | Botschaft(Interne Kommunikation VIP-BRS 1, ID: INTL_KOMM_VIP_BRS_1) Prüfsumme falsch | 1 | - |
| 0xD36428 | Signal(Interne Kommunikation VIP-BRS 1, ID: INTL_KOMM_VIP_BRS_1) ungültig | 1 | - |
| 0xD36429 | Signal(Interne Kommunikation VIP-BRS 1, ID: INTL_KOMM_VIP_BRS_1) undefiniert | 1 | - |
| 0xD36434 | Botschaft(Vorgabe Parametrisierung FAS, ID: SPEC_PRMSN_DRS) fehlt | 1 | - |
| 0xD36435 | Botschaft(Vorgabe Parametrisierung FAS, ID: SPEC_PRMSN_DRS) nicht aktuell | 1 | - |
| 0xD36436 | Botschaft(Vorgabe Parametrisierung FAS, ID: SPEC_PRMSN_DRS) Prüfsumme falsch | 1 | - |
| 0xD36437 | Signal(Vorgabe Parametrisierung FAS, ID: SPEC_PRMSN_DRS) ungültig | 1 | - |
| 0xD36438 | Signal(Vorgabe Parametrisierung FAS, ID: SPEC_PRMSN_DRS) undefiniert | 1 | - |
| 0xD36439 | Botschaft(Interne Kommunikation VIP-BRS 2, ID: INTL_KOMM_VIP_BRS_2) fehlt | 1 | - |
| 0xD3643A | Botschaft(Interne Kommunikation VIP-BRS 2, ID: INTL_KOMM_VIP_BRS_2) nicht aktuell | 1 | - |
| 0xD3643B | Botschaft(Interne Kommunikation VIP-BRS 2, ID: INTL_KOMM_VIP_BRS_2) Prüfsumme falsch | 1 | - |
| 0xD3643C | Signal(Interne Kommunikation VIP-BRS 2, ID: INTL_KOMM_VIP_BRS_2) ungültig | 1 | - |
| 0xD3643D | Signal(Interne Kommunikation VIP-BRS 2, ID: INTL_KOMM_VIP_BRS_2) undefiniert | 1 | - |
| 0xD36442 | Botschaft(Ist Daten E-Motor 1, ID: AVL_DT_MOT_1) fehlt | 1 | - |
| 0xD36445 | Signal(Ist Daten E-Motor 1, ID: AVL_DT_MOT_1) ungültig | 1 | - |
| 0xD36C0D | Signal(Daten Antriebsstrang 2, ID: DT_PT_2) undefiniert | 1 | - |
| 0xD36C19 | Signal(Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) undefiniert | 1 | - |
| 0xD36C81 | Signal(Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 67 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | EPB_TASTER_DRUECKEN_DEFECT | 0-n | High | 0x01 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0002 | EPB_TASTER_ZIEHEN_DEFECT | 0-n | High | 0x02 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0003 | EPB_TASTER_SIGNALMUSTER_UNGUELTIG | 0-n | High | 0x04 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0004 | EPB_TASTER_WATCHDOG_FEHLER | 0-n | High | 0x08 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0005 | EPB_TASTER_ROM_FEHLER | 0-n | High | 0x10 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0006 | EPB_TASTER_RAM_FEHLER | 0-n | High | 0x20 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0007 | Hybrid power Managment Zustand | 0-n | High | 0xFF | TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT | - | - | - |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x1702 | SAE_CODE | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
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
| 0x4100 | RDC_RE_HERSTELLER | 0-n | High | 0xFF | TAB_RDC_RE_HERSTELLER | - | - | - |
| 0x4101 | RDC_REFERENZ_AUSSENTEMPERATUR | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4102 | RDC Aussendruck | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4103 | Aktuelle Reifendruck vorn links | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4104 | Aktuelle Reifendruck vorn rechts | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4105 | Aktuelle Reifendruck hinten links | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4106 | Aktuelle Reifendruck hinten rechts | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4107 | Aktuelle Reifentemperatur vorn links | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4108 | Aktuelle Reifentemperatur vorn rechts | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4109 | Aktuelle Reifentemperatur hinten links | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410A | Aktuelle Reifentemperatur hinten rechts | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410B | Aktuelle Aussentemperatur | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410C | RDC Inaktiv Status | 0-n | High | 0xFF | TAB_RDC_INT_FEHLER | - | - | - |
| 0x410D | RDC Kalibrierungsstatus | 0-n | High | 0xFF | TAB_KALIBRIERUNG | - | - | - |
| 0x410E | RDC Status | 0-n | High | 0xFF | TAB_RDC_INTERNE_STATUS | - | - | - |
| 0x410F | RDC Konfiguration | 0-n | High | 0xFF | RDC_INT_KONFIG | - | - | - |
| 0x4110 | RDC Reifensolldruck Vorderachse | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4111 | RDC Reifensolldruck Hinterachse | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4112 | RDC Position für die Meldung | 0-n | High | 0xFF | RDC_TAB_POSITION_SENSOR | - | - | - |
| 0x5003 | STAT_FAHRZEUGZUSTAND | HEX | High | unsigned char | - | - | - | - |
| 0x5004 | STAT_ANTRIEBSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5008 | STAT_SPANNUNGSMASTER_VERFUEGBAR | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500A | STAT_FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500B | STAT_FUNKTIONSZUSTAND | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500C | STAT_INTERNER_FUNKTIONSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500E | STAT_INTERNE_FEHLERNUMMER | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500F | STAT_FEHLERSPEICHERSPERRE_AKTIV | 0/1 | High | 0x01 | - | - | - | - |
| 0x5023 | STROM_MOTOR_L | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5024 | STROM_MOTOR_R | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5026 | BREMSENSTATUS_LINKS | 0-n | High | 0xF0 | TAB_BREMSENSTATUS_LINKS | - | - | - |
| 0x5027 | BREMSENSTATUS_RECHTS | 0-n | High | 0x0F | TAB_BREMSENSTATUS_RECHTS | - | - | - |
| 0x5028 | SCHALTERSTATUS | 0-n | High | 0xFF | TAB_SCHALTERSTATUS | - | - | - |
| 0x502F | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5032 | EPB_LETZTES_EREIGNIS | 0-n | High | 0xFF | TAB_EPB_EREIGNIS | - | - | - |
| 0x5040 | SG_RESET_INFO | HEX | High | unsigned char | - | - | - | - |
| 0x5041 | OBD_1_ACSM_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5043 | OBD_3_EPS_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5045 | OBD_5_HSR_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5046 | OBD_6_VIP_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5050 | FS_SWBUGNR_00 | HEX | High | unsigned int | - | - | - | - |
| 0x5051 | FS_SWBUGNR_01_02 | HEX | High | unsigned long | - | - | - | - |
| 0x5055 | OBD_BEGU_IST_SOLL | HEX | High | unsigned int | - | - | - | - |
| 0x5056 | CONTI_SW_VERSION | TEXT | High | 9 | - | 1.0 | 1.0 | 0.0 |
| 0x5057 | OS_KENNUNG | TEXT | High | 12 | - | 1.0 | 1.0 | 0.0 |
| 0x5058 | CURRENT_TASK | HEX | High | unsigned int | - | - | - | - |
| 0x5059 | NEXT_TASK | HEX | High | unsigned int | - | - | - | - |
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

Dimensions: 111 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x000002 | FLEXRAY controller ACS error | 0 | - |
| 0x000003 | FLEXRAY controller NIT error | 0 | - |
| 0x020108 | DOBD - ACSM-05 - Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x02010B | DOBD - ACSM-05 - Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02010D | DOBD - ACSM-05 - Codierung: Codierdaten nicht qualifiziert | 0 | - |
| 0x030541 | DOBD - VIP - QDM-SBS - Gierratensensor Modellfehler Sensor 1 | 0 | - |
| 0x030543 | DOBD - VIP - QDM-SBS - Gierratensensor Signalqualität Sensor 1 | 0 | - |
| 0x03054A | DOBD - VIP - QDM-SBS - Lenkwinkel effektiv Modellfehler | 0 | - |
| 0x03054B | DOBD - VIP - QDM-SBS - Lenkwinkel effektiv Randueberwachung | 0 | - |
| 0x03055A | DOBD - VIP - QDM-SBS - Laengsbeschleunigungssensor Modellfehler | 0 | - |
| 0x03055B | DOBD - VIP - QDM-SBS - Laengsbeschleunigungssensor Signalqualitaet | 0 | - |
| 0x03056B | DOBD - VIP - QDM-SBS - Querbeschleunigungssensor Modellfehler Sensor 1 | 0 | - |
| 0x03056D | DOBD - VIP - QDM-SBS - Querbeschleunigungssensor Signalqualitaet Sensor 1 | 0 | - |
| 0x480380 | DOBD - HSR-02ZF - Steuergerät intern - Hardwarefehler | 0 | - |
| 0x480385 | DOBD - HSR-02ZF - Stellmotor Motorblockade | 0 | - |
| 0x480389 | DOBD - HSR-02ZF - Stellmotor Sensorplausibilisierung | 0 | - |
| 0x48038E | DOBD - HSR-02ZF - Steuergerät intern - Diversitäres Rechnen | 0 | - |
| 0x48039A | DOBD - HSR-02ZF - Steuergerät intern - Softwarefehler | 0 | - |
| 0x4803B2 | DOBD - HSR-02ZF - Sensor - Rotorlage - Lenkwinkel - Hardware defekt | 0 | - |
| 0x4803B3 | DOBD - HSR-02ZF - Während Init Position Anfahren nicht möglich | 0 | - |
| 0x4803B4 | DOBD - HSR-02ZF - Indexsensor Fehler | 0 | - |
| 0x4803B5 | DOBD - HSR-02ZF - Querverbau Indexsensor | 0 | - |
| 0x4803B8 | DOBD - HSR-02ZF - Lage Drehzahl Kaskade | 0 | - |
| 0x4803BA | DOBD - HSR-02ZF - Steuergerät intern - ROM fehlerhaft | 0 | - |
| 0x4803BB | DOBD - HSR-02ZF - Steuergerät intern - RAM fehlerhaft | 0 | - |
| 0x4803BC | DOBD - HSR-02ZF - Steuergerät intern - Watchdog Ereignis | 0 | - |
| 0x4803BE | DOBD - HSR-02ZF - Steuergerät intern - Softwarefehler - OBD | 0 | - |
| 0x4803BF | DOBD - HSR-02ZF - Steuergerät intern - MCU Temperatur Sensor OOR | 0 | - |
| 0x4803C0 | DOBD - HSR-02ZF - Steuergerät intern - Hardwarefehler - OBD | 0 | - |
| 0x4803C3 | DOBD - HSR-02ZF - Sensor - Rotorlage - Lenkwinkel - Hardware defekt_OOR | 0 | - |
| 0x48075E | EPBi Missbrauch durch Fahrer erkannt | 0 | - |
| 0x480761 | EPBi -PBC - Fahrzeug rollt trotz nachspannen | 0 | - |
| 0x480896 | EPBi - PBC - Host-Verhalten unerwartet | 0 | - |
| 0x480897 | EPBi - PBC - Hydraulische Druckunterstützung nicht umsetzbar | 0 | - |
| 0x480904 | Spezielle Fahrsituation: kein By-Wire Modus möglich | 1 | - |
| 0x480905 | Stillstandsmanagement - EPBi Aktuator Stellvorgang nicht umgesetzt | 0 | - |
| 0x4809FF | RSU-Mission aktiv | 1 | - |
| 0x480ACD | RDCi Radelektronik anderer Typ | 0 | - |
| 0x480ACF | RDC Ausfall | 0 | - |
| 0x480AD0 | RDC Befüllhinweis | 0 | - |
| 0x480AD1 | RDC Druckwarnung | 0 | - |
| 0x480AD2 | RDC Pannenwarnung | 0 | - |
| 0x480AD3 | RDC Warnungsrücknahme | 0 | - |
| 0x480AD4 | RDC Kalibrierung | 0 | - |
| 0x480AD6 | EPBi - PBC - Außerhalb der Spezifikation | 0 | - |
| 0x480AE1 | Steuergerät intern - DC/DC-Aufwärtswandler im IPEX-Regler - Boost-Funktion gestört | 0 | - |
| 0x480AE2 | EPBI - PBC - Timeout Power Latch | 0 | - |
| 0x480B00 | Steuergerät intern - VIP - Peripheriefehler | 0 | - |
| 0x480B3B | Stillstandsmanagement - Übergabe an Getriebe P nicht möglich | 0 | - |
| 0x4822D9 | DOBD - EPS-TK03 - Sensor - Lenkwinkel Index Riemensprung Lenkwinkel ungültig | 0 | - |
| 0x4822DF | DOBD - EPS-ZF02 - Steuergerät intern - ROM fehlerhaft | 0 | - |
| 0x4822E0 | DOBD - EPS-ZF02 - Steuergerät intern - NVRAM fehlerhaft | 0 | - |
| 0x4822E3 | DOBD - EPS-ZF02 - Steuergerät intern - RAM fehlerhaft | 0 | - |
| 0x4822E7 | DOBD - EPS - Steuergerät intern - Watchdog Ereignis | 0 | - |
| 0x4822E9 | DOBD - EPS - Steuergerät intern - Softwarefehler - OBD | 0 | - |
| 0x4822EA | DOBD - EPS-ZF02 - Steuergerät intern - ZFLS - Hardware - Defekt - OBD | 0 | - |
| 0x4822EE | DOBD - EPS-ZF02 - Steuergerät intern - Softwarefehler - Program-Flow Control | 0 | - |
| 0x4822F0 | DOBD - EPS-ZF02 - Sensor - Rotorlage - Lenkwinkel - Harware defekt_OOR | 0 | - |
| 0x4822F6 | DOBD - EPS-TK03 - Steuergerät intern - Speicherfehler | 0 | - |
| 0x4822F8 | DOBD - EPS-TK03 - Steuergerät intern - Hardwarefehler - OBD | 0 | - |
| 0x4822F9 | DOBD - EPS-TK03 - Sensor - Rotorlage - Lenkwinkel - Software defekt | 0 | - |
| 0x4822FC | DOBD - EPS-TK03 - Sensor - Rotorlage - Lenkwinkel - Hardware defekt - Abschaltung Lenkunterstützung | 0 | - |
| 0x482394 | DOBD - EPS - Sensor - Rotorlage - Lenkwinkel - Verlust Multiturnwert | 1 | - |
| 0x48239C | DOBD - EPS - Sensor - Lenkwinkel Index - Defekt | 0 | - |
| 0x4823D2 | DOBD - EPS-ZF02 - Sensor - Rotorlage - Lenkwinkel - Hardware defekt | 0 | - |
| 0x483900 | DOBD - VIP - Steuergerät intern - Error Mode VIP | 0 | - |
| 0x483907 | DOBD - VIP - Steuergerät intern - ROM / Flash Fehler | 0 | - |
| 0x483908 | DOBD - VIP - Steuergerät intern - EEPROM Fehler | 0 | - |
| 0x483909 | DOBD - VIP - Steuergerät intern - P2P Fehler | 0 | - |
| 0x930C1E | DOBD - ACSM-05 - Interner Steuergerätefehler allgemeiner Sensorclusterfehler OBD relevant | 0 | - |
| 0x930C28 | DOBD - ACSM-05 - Interner Steuergerätefehler Sensorclusterfehler Kommunikation | 0 | - |
| 0x930C29 | DOBD - ACSM-05 - Interner Steuergerätefehler Sensorclusterfehler Spannungsversorgung | 0 | - |
| 0xD35D0C | D-OBD 1 - ICM oder ACSM - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35D1F | D-OBD 3 - EPS - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35D29 | D-OBD 5 - HSR - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD35D50 | D-OBD 6 - VIP - Kommunikationsfehler Diagnosestatusnachricht Sammelfehler | 1 | - |
| 0xD3C41F | DOBD - HSR-02ZF - Flexray:  Physikalischer Busfehler | 0 | - |
| 0xD3C420 | DOBD - HSR-02ZF - FLEXRAY Controller Error | 0 | - |
| 0xD5041F | DOBD - EPS - Flexray:  Physikalischer Busfehler | 0 | - |
| 0xD50420 | DOBD - EPS - FLEXRAY Controller Error | 0 | - |
| 0xD51414 | DOBD - EPS-TK03 - Botschaft(Offset Quadrant EPS, ID: OFFS_QUAD_EPS) fehlt | 1 | - |
| 0xD51415 | DOBD - EPS-TK03 - Botschaft(Offset Quadrant EPS, ID: OFFS_QUAD_EPS) nicht aktuell | 1 | - |
| 0xD51416 | DOBD - EPS-TK03 - Botschaft(Offset Quadrant EPS, ID: OFFS_QUAD_EPS) Prüfsumme falsch | 1 | - |
| 0xD51418 | DOBD - EPS-TK03 - Signal(Offset Quadrant EPS, ID: OFFS_QUAD_EPS) undefiniert | 1 | - |
| 0xD51458 | DOBD - EPS-ZF02 - Botschaftsfehler (Offset Quadrant EPS, ID: OFFS_QUAD_EPS) - Timeout | 1 | - |
| 0xD51459 | DOBD - EPS-ZF02 - Botschaftsfehler (Offset Quadrant EPS, ID: OFFS_QUAD_EPS) - Checksumme | 1 | - |
| 0xD5145A | DOBD - EPS-ZF02 - Botschaftsfehler (Offset Quadrant EPS, ID: OFFS_QUAD_EPS) - Alive | 1 | - |
| 0xD5145B | DOBD - EPS-ZF02 - Signalfehler (Offset Quadrant EPS, ID: OFFS_QUAD_EPS) - Ungültig | 1 | - |
| 0xD5145C | DOBD - EPS-ZF02 - Signalfehler (Offset Quadrant EPS, ID: OFFS_QUAD_EPS) - Undefiniert | 1 | - |
| 0xD7441F | DOBD - VIP - FLEXRAY Physical bus error | 0 | - |
| 0xD74420 | DOBD - VIP - FLEXRAY controller error | 0 | - |
| 0xD75452 | DOBD - VIP - Botschaft(Ist Bremsmoment Summe, ID: AVL_BRTORQ_SUM) fehlt | 1 | - |
| 0xD7545E | DOBD - VIP - Botschaft(Ist Position EPS, ID: AVL_PO_EPS) fehlt | 1 | - |
| 0xD7545F | DOBD - VIP - Botschaft(Ist Position EPS, ID: AVL_PO_EPS) nicht aktuell | 1 | - |
| 0xD75460 | DOBD - VIP - Botschaft(Ist Position EPS, ID: AVL_PO_EPS) Prüfsumme falsch | 1 | - |
| 0xD754E6 | DOBD - VIP - Botschaft(Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) fehlt | 1 | - |
| 0xD754E7 | DOBD - VIP - Botschaft(Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) nicht aktuell | 1 | - |
| 0xD754E8 | DOBD - VIP - Botschaft(Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) Prüfsumme falsch | 1 | - |
| 0xD75542 | DOBD - VIP - Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) fehlt | 1 | - |
| 0xD75543 | DOBD - VIP - Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) nicht aktuell | 1 | - |
| 0xD75544 | DOBD - VIP - Botschaft(Status Lenkung Hinterachse, ID: ST_STE_BAX) Prüfsumme falsch | 1 | - |
| 0xD7558A | DOBD - VIP - Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) fehlt | 1 | - |
| 0xD7558B | DOBD - VIP - Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) nicht aktuell | 1 | - |
| 0xD7558C | DOBD - VIP - Botschaft(Radmoment Antriebsstrang Ist, ID: WMOM_PT_AVL) Prüfsumme falsch | 1 | - |
| 0xD755EE | DOBD - VIP - Botschaft(Interne Kommunikation BRS-VIP 2, ID: INTL_KOMM_BRS_VIP_2) fehlt | 1 | - |
| 0xD755EF | DOBD - VIP - Botschaft(Interne Kommunikation BRS-VIP 2, ID: INTL_KOMM_BRS_VIP_2) nicht aktuell | 1 | - |
| 0xD755F0 | DOBD - VIP - Botschaft(Interne Kommunikation BRS-VIP 2, ID: INTL_KOMM_BRS_VIP_2) Prüfsumme falsch | 1 | - |
| 0xD755F6 | DOBD - VIP - Botschaft(Ist Drehzahl Rad, ID: AVL_RPM_WHL) fehlt | 1 | - |
| 0xD755F7 | DOBD - VIP - Botschaft(Ist Drehzahl Rad, ID: AVL_RPM_WHL) nicht aktuell | 1 | - |
| 0xD755F8 | DOBD - VIP - Botschaft(Ist Drehzahl Rad, ID: AVL_RPM_WHL) Prüfsumme falsch | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 67 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | EPB_TASTER_DRUECKEN_DEFECT | 0-n | High | 0x01 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0002 | EPB_TASTER_ZIEHEN_DEFECT | 0-n | High | 0x02 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0003 | EPB_TASTER_SIGNALMUSTER_UNGUELTIG | 0-n | High | 0x04 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0004 | EPB_TASTER_WATCHDOG_FEHLER | 0-n | High | 0x08 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0005 | EPB_TASTER_ROM_FEHLER | 0-n | High | 0x10 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0006 | EPB_TASTER_RAM_FEHLER | 0-n | High | 0x20 | TAB_AKTIV_INAKTIV | - | - | - |
| 0x0007 | Hybrid power Managment Zustand | 0-n | High | 0xFF | TAB_STATUS_LADEN_HOCHSPANNUNG_POWERMANAGEMENT | - | - | - |
| 0x1700 | Kilometerstand | TEXT | High | 3 | - | - | - | - |
| 0x1701 | Systemzeit | s | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x1702 | SAE_CODE | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
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
| 0x4100 | RDC_RE_HERSTELLER | 0-n | High | 0xFF | TAB_RDC_RE_HERSTELLER | - | - | - |
| 0x4101 | RDC_REFERENZ_AUSSENTEMPERATUR | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4102 | RDC Aussendruck | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4103 | Aktuelle Reifendruck vorn links | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4104 | Aktuelle Reifendruck vorn rechts | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4105 | Aktuelle Reifendruck hinten links | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4106 | Aktuelle Reifendruck hinten rechts | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4107 | Aktuelle Reifentemperatur vorn links | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4108 | Aktuelle Reifentemperatur vorn rechts | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x4109 | Aktuelle Reifentemperatur hinten links | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410A | Aktuelle Reifentemperatur hinten rechts | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410B | Aktuelle Aussentemperatur | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x410C | RDC Inaktiv Status | 0-n | High | 0xFF | TAB_RDC_INT_FEHLER | - | - | - |
| 0x410D | RDC Kalibrierungsstatus | 0-n | High | 0xFF | TAB_KALIBRIERUNG | - | - | - |
| 0x410E | RDC Status | 0-n | High | 0xFF | TAB_RDC_INTERNE_STATUS | - | - | - |
| 0x410F | RDC Konfiguration | 0-n | High | 0xFF | RDC_INT_KONFIG | - | - | - |
| 0x4110 | RDC Reifensolldruck Vorderachse | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4111 | RDC Reifensolldruck Hinterachse | mbar | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4112 | RDC Position für die Meldung | 0-n | High | 0xFF | RDC_TAB_POSITION_SENSOR | - | - | - |
| 0x5003 | STAT_FAHRZEUGZUSTAND | HEX | High | unsigned char | - | - | - | - |
| 0x5004 | STAT_ANTRIEBSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5008 | STAT_SPANNUNGSMASTER_VERFUEGBAR | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500A | STAT_FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500B | STAT_FUNKTIONSZUSTAND | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500C | STAT_INTERNER_FUNKTIONSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500E | STAT_INTERNE_FEHLERNUMMER | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500F | STAT_FEHLERSPEICHERSPERRE_AKTIV | 0/1 | High | 0x01 | - | - | - | - |
| 0x5023 | STROM_MOTOR_L | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5024 | STROM_MOTOR_R | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5026 | BREMSENSTATUS_LINKS | 0-n | High | 0xF0 | TAB_BREMSENSTATUS_LINKS | - | - | - |
| 0x5027 | BREMSENSTATUS_RECHTS | 0-n | High | 0x0F | TAB_BREMSENSTATUS_RECHTS | - | - | - |
| 0x5028 | SCHALTERSTATUS | 0-n | High | 0xFF | TAB_SCHALTERSTATUS | - | - | - |
| 0x502F | Sub-Tabelle | 0-n | - | 0xFF | - | - | - | - |
| 0x5032 | EPB_LETZTES_EREIGNIS | 0-n | High | 0xFF | TAB_EPB_EREIGNIS | - | - | - |
| 0x5040 | SG_RESET_INFO | HEX | High | unsigned char | - | - | - | - |
| 0x5041 | OBD_1_ACSM_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5043 | OBD_3_EPS_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5045 | OBD_5_HSR_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5046 | OBD_6_VIP_MUX_FEHLER | HEX | High | unsigned char | - | - | - | - |
| 0x5050 | FS_SWBUGNR_00 | HEX | High | unsigned int | - | - | - | - |
| 0x5051 | FS_SWBUGNR_01_02 | HEX | High | unsigned long | - | - | - | - |
| 0x5055 | OBD_BEGU_IST_SOLL | HEX | High | unsigned int | - | - | - | - |
| 0x5056 | CONTI_SW_VERSION | TEXT | High | 9 | - | 1.0 | 1.0 | 0.0 |
| 0x5057 | OS_KENNUNG | TEXT | High | 12 | - | 1.0 | 1.0 | 0.0 |
| 0x5058 | CURRENT_TASK | HEX | High | unsigned int | - | - | - | - |
| 0x5059 | NEXT_TASK | HEX | High | unsigned int | - | - | - | - |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-rdbi-ads-dop"></a>
### RDBI_ADS_DOP

Dimensions: 11 rows × 2 columns

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
| 0x44 | RSUSession |
| 0xFF | Wert ungültig |

<a id="table-rdc-int-konfig"></a>
### RDC_INT_KONFIG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Anderer Reifen mit RDC Reset |
| 0x01 | eRFS ohne RID |
| 0x02 | eRFS mit RID manuelle Auswahl |
| 0x03 | eRFS mit RID automatische Auswahl |
| 0xFF | Ungültig |

<a id="table-rdc-tab-position-sensor"></a>
### RDC_TAB_POSITION_SENSOR

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Position unbekannt |
| 0x01 | Vorn Links |
| 0x02 | Vorn Rechts |
| 0x04 | Hinten Links |
| 0x08 | Hinten Rechts |
| 0x10 | Vorn Links aus Historie |
| 0x20 | Vorn Rechts aus Historie |
| 0x40 | Hinten Links aus Historie |
| 0x80 | Hinten Rechts aus Historie |
| 0xFF | Wert ungültig |

<a id="table-res-0x1061-r"></a>
### RES_0X1061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_ENDE_WABL | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Verriegelt (loeschen von Einzelfehlern und PDTCs wird unterbunden) 1: Entriegelt (loeschen von Einzelfehlern und PDTCs wird nicht unterbunden) |

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

<a id="table-res-0x5002-d"></a>
### RES_0X5002_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RDC_DEVELOPER_INDEX_WERT | HEX | high | unsigned char | - | - | - | - | - | Übergibt einen Multiplex Index Nummer der anhand einer Entwickler Tabelle die Daten entschlüsselt. |
| STAT_RDC_DEVELOPER_DATA | DATA | high | data[20] | - | - | 1.0 | 1.0 | 0.0 | Entwickler Daten. |

<a id="table-res-0x5038-d"></a>
### RES_0X5038_D

Dimensions: 27 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ACTUATIONCOUNTER_ADRRELEASE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Lösen per ADR' zurück. |
| STAT_ACTUATIONCOUNTER_APPLYLEFT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen des linken Aktuators' zurück. |
| STAT_ACTUATIONCOUNTER_APPLYRIGHT_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen des rechten Aktuators' zurück. |
| STAT_ACTUATIONCOUNTER_BRAKEPADADJUSTMENT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Nachjustierung aufgrund Bremsbelagverschleiß' zurück. |
| STAT_ACTUATIONCOUNTER_DYNAMICDECELERATION_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Dynamische Abbremsung' zurück. |
| STAT_ACTUATIONCOUNTER_DYNAMICDECELERATIONACTUATOR_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Abbremsen über Aktuator' zurück. |
| STAT_ACTUATIONCOUNTER_EXTERNALAPPLY_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen aufgrund SSM-Anforderung' zurück. |
| STAT_ACTUATIONCOUNTER_EXTERNALRELEASE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Lösen aufgrund SSM-Anforderung' zurück. |
| STAT_ACTUATIONCOUNTER_HIGHTEMPERATURRECLAMP_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Nachspannen aufgrund hoher Bremsentemperatur' zurück. |
| STAT_ACTUATIONCOUNTER_MAINTANENCEMODE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Einnahme des Montage Modus' zurück. |
| STAT_ACTUATIONCOUNTER_OUTOFSPEC_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Zuständen außerhalb der Spezifikation*' zurück. |
| STAT_ACTUATIONCOUNTER_ROLLAWAYRECLAMP_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Nachspannen aufgrund Rollüberwachung' zurück. |
| STAT_ACTUATIONCOUNTER_ROLLERBENCHAPPLY_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei aktivem Rollenmodus' zurück. |
| STAT_ACTUATIONCOUNTER_SERVICEMESSAGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen aufgrund Dienstenachricht' zurück. |
| STAT_ACTUATIONCOUNTER_SLOPE__0_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Steigungen bis 5%' zurück. |
| STAT_ACTUATIONCOUNTER_SLOPE__5_12_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Steigungen zwischen 5% und 12%' zurück. |
| STAT_ACTUATIONCOUNTER_SLOPE__12_20_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Steigungen zwischen 12% und 20%' zurück. |
| STAT_ACTUATIONCOUNTER_SLOPE__20_ABOVE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Steigungen über 20%' zurück. |
| STAT_ACTUATIONCOUNTER_SLOPEINVALID_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei ungültigem Steigungswert' zurück. |
| STAT_ACTUATIONCOUNTER_SWITCHAPPLY_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen aufgrund von Tasterbetätigung' zurück. |
| STAT_ACTUATIONCOUNTER_SWITCHRELEASE_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Lösen aufgrund von Tasterbetätigung' zurück. |
| STAT_ACTUATIONCOUNTER_TEMP__200_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Bremsentemperaturen bis 200°C' zurück. |
| STAT_ACTUATIONCOUNTER_TEMP__200_300_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Bremsentemperaturen zwischen 200°C und 300°C' zurück. |
| STAT_ACTUATIONCOUNTER_TEMP__300_400_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Bremsentemperaturen zwischen 300°C und 400°C' zurück. |
| STAT_ACTUATIONCOUNTER_TEMP__400_500_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Bremsentemperaturen zwischen 400°C und 500°C' zurück. |
| STAT_ACTUATIONCOUNTER_TEMP__500_ABOVE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'Feststellen bei Bremsentemperaturen über 500°C' zurück. |
| STAT_ACTUATIONCOUNTER_UNEXPECTEDPOWERDOWN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die Zähler der Aktion 'unerwartetes Abschalten' zurück. |

<a id="table-res-0xa065-r"></a>
### RES_0XA065_R

Dimensions: 9 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_GESCHW_RAD_VL_MIN_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | min. Radgeschwindigkeit vorne links |
| STAT_GESCHW_RAD_VL_MAX_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | max. Radgeschwindigkeit vorne links |
| STAT_GESCHW_RAD_VR_MIN_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | min. Radgeschwindigkeit vorne rechts |
| STAT_GESCHW_RAD_VR_MAX_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | max. Radgeschwindigkeit vorne rechts |
| STAT_GESCHW_RAD_HL_MIN_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | min. Radgeschwindigkeit hinten rechts |
| STAT_GESCHW_RAD_HL_MAX_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | max. Radgeschwindigkeit hinten links |
| STAT_GESCHW_RAD_HR_MIN_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | min. Radgeschwindigkeit hinten rechts |
| STAT_GESCHW_RAD_HR_MAX_WERT | - | - | + | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | max. Radgeschwindigkeit hinten rechts |

<a id="table-res-0xa130-r"></a>
### RES_0XA130_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FLM_RESET | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ROUTINE | - | - | - | Ausführungsstatus |

<a id="table-res-0xa14b-r"></a>
### RES_0XA14B_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TMC_TRAVEL_SENSOR_CALIBRATION_START_STATUS | + | - | - | 0-n | high | unsigned char | - | TAB_START_TTS_CAL_STATUS | - | - | - | Status der Start Routine Offset Abgleichs vom TMC Travel sensor (TTS) |
| STAT_TMC_TRAVEL_SENSOR_CALIBRATION_RESULT_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_STATE_TTS_CAL_STATUS | - | - | - | Status der Kalibrierung und der Grund bei nichterfolgreicher Kalibrierung |

<a id="table-res-0xa154-r"></a>
### RES_0XA154_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ENTLUEFTUNG_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_ERGEBNIS | - | - | - | Status der Entlueftungs Routine |
| STAT_ENTLUEFTUNG_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Fehlerinformationen zur Entlüftungs-Routine |

<a id="table-res-0xa3a0-r"></a>
### RES_0XA3A0_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EVAKUIERUNG_UND_BEFUELLUNG_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_ERGEBNIS | - | - | - | Es wird der Status der Routine ausgegeben |
| STAT_EVAKUIERUNG_UND_BEFUELLUNG_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben |

<a id="table-res-0xa3a1-r"></a>
### RES_0XA3A1_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NACHARBEITSENTLUEFTUNG_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_ERGEBNIS | - | - | - | Es wird der Status der Routine ausgegeben. |
| STAT_NACHARBEITSENTLUEFTUNG_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben |

<a id="table-res-0xa3a2-r"></a>
### RES_0XA3A2_R

Dimensions: 5 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BEFUELLKONTROLLE_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_STATUS | - | - | - | Es wird der Status der Routine ausgegeben. |
| STAT_BEFUELLKONTROLLE_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben.  |
| - | - | - | + | Bit | high | BITFIELD | - | BF_OBS_ERGEBNIS_BEFUELLUNG | - | - | - | Ergebnis der Tests auf Befuellung fuer Hauptbremszylinder, Linearaktuator und Simulator |
| STAT_BEFUELLKONTROLLE_LAC_UND_TMC_VOLUMEN_RESERVE_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Differenz zwischen dem zur Erreichung des Mindestdrucks maximal erlaubten Volumen und dem dazu real verbrauchten Volumen im Linearaktuator und Hauptbremszylinder. |
| STAT_BEFUELLKONTROLLE_SIM_VOLUMEN_RESERVE_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Differenz zwischen dem zur Erreichung des Mindestdrucks maximal erlaubten Volumen und dem dazu real verbrauchten Volumen im Simulator. |

<a id="table-res-0xa3a3-r"></a>
### RES_0XA3A3_R

Dimensions: 14 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EVAKUIERUNG_UND_BEFUELLUNG_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_ERGEBNIS | - | - | - | Es wird der Status der Routine ausgegeben. Es wird mit diesem Status keine Aussage über das Testergebnis (z.B. OK / NOK) getroffen. Die Messungen müssen durch den OEM bewertet werden. |
| STAT_EVAKUIERUNG_UND_BEFUELLUNG_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben |
| STAT_VOLUMEN_VORNE_LINKS_GEMESSEN_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Im Linearaktuator verschobenes Volumen zur Erreichung des Arbeitspunktes (Zielwert 50 bar)  in der Radseite Vorne Links.  |
| STAT_VOLUMEN_VORNE_LINKS_MODELL_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Laut parametrierter Druck-Volumen Kurve zum Arbeitspunkt (Zielwert 50 bar) gehörendes Volumen in der Radseite Vorne Links. |
| STAT_LECKAGE_VOLUMEN_VORNE_LINKS_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Nach dem Druckaufbau zum Druckhalten im Arbeitspunkt zusaetzlich verschobenes Volumen in der Radseite Vorne Links. |
| STAT_VOLUMEN_VORNE_RECHTS_GEMESSEN_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Im Linearaktuator verschobenes Volumen zur Erreichung des Arbeitspunktes (Zielwert 50 bar)  in der Radseite Vorne Rechts.  |
| STAT_VOLUMEN_VORNE_RECHTS_MODELL_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Laut parametrierter Druck-Volumen Kurve zum Arbeitspunkt (Zielwert 50 bar) gehörendes Volumen in der Radseite Vorne Rechts. |
| STAT_LECKAGE_VOLUMEN_VORNE_RECHTS_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Nach dem Druckaufbau zum Druckhalten im Arbeitspunkt zusaetzlich verschobenes Volumen in der Radseite Vorne Rechts. |
| STAT_VOLUMEN_HINTEN_RECHTS_GEMESSEN_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Im Linearaktuator verschobenes Volumen zur Erreichung des Arbeitspunktes (Zielwert 50 bar)  in der Radseite Hinten Rechts. |
| STAT_VOLUMEN_HINTEN_RECHTS_MODELL_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Laut parametrierter Druck-Volumen Kurve zum Arbeitspunkt (Zielwert 50 bar) gehörendes Volumen in der Radseite Hinten Rechts. |
| STAT_LECKAGE_VOLUMEN_HINTEN_RECHTS_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Nach dem Druckaufbau zum Druckhalten im Arbeitspunkt zusaetzlich verschobenes Volumen in der Radseite Hinten Rechts. |
| STAT_VOLUMEN_HINTEN_LINKS_GEMESSEN_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Im Linearaktuator verschobenes Volumen zur Erreichung des Arbeitspunktes (Zielwert 50 bar)  in der Radseite Hinten Links.  |
| STAT_VOLUMEN_HINTEN_LINKS_MODELL_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Laut parametrierter Druck-Volumen Kurve zum Arbeitspunkt (Zielwert 50 bar) gehörendes Volumen in der Radseite Hinten Links. |
| STAT_LECKAGE_VOLUMEN_HINTEN_LINKS_WERT | - | - | + | mm³ | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Nach dem Druckaufbau zum Druckhalten im Arbeitspunkt zusaetzlich verschobenes Volumen in der Radseite Hinten Links. |

<a id="table-res-0xa3a4-r"></a>
### RES_0XA3A4_R

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERTAUSCHUNGSTEST_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_STATUS | - | - | - | Es wird der Status der Routine ausgegeben. |
| STAT_VERTAUSCHUNGSTEST_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben |
| STAT_VERTAUSCHUNGSTEST_ERGEBNIS | - | - | + | 0-n | high | unsigned char | - | TAB_DIFFERENZGESCHWINDIGKEIT | - | - | - | Ist die Differenzgeschwindigkeit erreicht 0x00 = OK 0x01 =Not OK |
| STAT_RAD_GESCHWINDIGKEIT_VOR_DRUCKAUFBAU_WERT | - | - | + | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Radgeschwindigkeit vor Druckaufbau / bei Start des Service. |
| STAT_ZEITVERZOEGERUNG_DRUCKAUFBAU_WERT | - | - | + | ms | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Dauer von Start des Druckaufbaus bis zur Erreichung des Zieldrucks. |
| STAT_GEMESSENE_DIFFERENZ_GESCHWINDIGKEIT_WERT | - | - | + | km/h | high | signed int | - | - | 1.0 | 100.0 | 0.0 | Gemessene Differenz der Geschwindigkeiten bei Start des Druckaufbaus und bei Erreichen des Zieldrucks. |

<a id="table-res-0xa3a5-r"></a>
### RES_0XA3A5_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DRUCKSENSOR_OFFSET_ABGLEICH_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_STATUS | - | - | - | Es wird der Status der Routine ausgegeben. |
| STAT_DRUCKSENSOR_OFFSET_ABGLEICH_FEHLERINFORMATION | - | - | + | 0-n | high | unsigned char | - | TAB_OBS_ROUTINE_FEHLERINFORMATIONEN | - | - | - | Es werden Fehlerinformationen zu der Routine ausgegeben |

<a id="table-res-0xa803-r"></a>
### RES_0XA803_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xd272-d"></a>
### RES_0XD272_D

Dimensions: 28 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VA_IDENT_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Identifikation als VA -&gt; Wert = 0x02 |
| STAT_VA_S_SIGNAL_WERT | km | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | km-Stand bei Sensorsignal |
| STAT_VA_S_WECHSEL_WERT | km | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | km-Stand bei letztem Belagwechsel |
| STAT_VA_S_REST_ORIG_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Restlaufstrecke ohne min- u. max-Beschränkung |
| STAT_VA_S_MIN_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | minimale Restlaufstrecke |
| STAT_VA_S_MAX_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | maximale Restlaufstrecke |
| STAT_VA_S_REST_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Restlaufstrecke |
| STAT_VA_S_GESAMT_1_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 1. Hochrechnung Gesamtlaufstrecke |
| STAT_VA_S_GESAMT_2_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 2. Hochrechnung Gesamtlaufstrecke |
| STAT_VA_S_GESAMT_3_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 3. Hochrechnung Gesamtlaufstrecke |
| STAT_VA_SZ_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Servicezähler |
| - | Bit | high | BITFIELD | - | BF_VA_FLAG_BVA | - | - | - | Bitfield Zustand BVA-Sensor |
| - | Bit | high | BITFIELD | - | BF_VA_RESET_VERHINDERER_1 | - | - | - | Bitfield Resetverhinderer |
| - | Bit | high | BITFIELD | - | BF_VA_RESET_VERHINDERER_2 | - | - | - | Bitfield Resetverhinderer |
| STAT_HA_IDENT_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Identifikation als HA -&gt; Wert = 0x06 |
| STAT_HA_S_SIGNAL_WERT | km | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | km-Stand bei Sensorsignal |
| STAT_HA_S_WECHSEL_WERT | km | high | unsigned int | - | - | 100.0 | 1.0 | 0.0 | km-Stand bei letztem Belagwechsel |
| STAT_HA_S_REST_ORIG_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Restlaufstrecke ohne min- u. max-Beschränkung |
| STAT_HA_S_MIN_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | minimale Restlaufstrecke |
| STAT_HA_S_MAX_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | maximale Restlaufstrecke |
| STAT_HA_S_REST_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Restlaufstrecke |
| STAT_HA_S_GESAMT_1_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 1. Hochrechnung Gesamtlaufstrecke |
| STAT_HA_S_GESAMT_2_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 2. Hochrechnung Gesamtlaufstrecke |
| STAT_HA_S_GESAMT_3_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 3. Hochrechnung Gesamtlaufstrecke |
| STAT_HA_SZ_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Servicezähler |
| - | Bit | high | BITFIELD | - | BF_HA_FLAG_BVA | - | - | - | Bitfield Zustand BVA-Sensor |
| - | Bit | high | BITFIELD | - | BF_HA_RESET_VERHINDERER_1 | - | - | - | Bitfield Resetverhinderer |
| - | Bit | high | BITFIELD | - | BF_HA_RESET_VERHINDERER_2 | - | - | - | Bitfield Resetverhinderer |

<a id="table-res-0xd690-d"></a>
### RES_0XD690_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PBC_SW_VERSION_0_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 0 |
| STAT_PBC_SW_VERSION_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 1 |
| STAT_PBC_SW_VERSION_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 2 |
| STAT_PBC_SW_VERSION_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 3 |
| STAT_PBC_SW_VERSION_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 4 |
| STAT_PBC_SW_VERSION_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PBC Software Version Byte 5 |

<a id="table-res-0xd805-d"></a>
### RES_0XD805_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_MOTOR_HL_WERT | V | - | signed int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Motor hinten links |
| STAT_STROM_MOTOR_HL_WERT | A | - | signed int | - | - | 1.0 | 1000.0 | 0.0 | Strom Motor hinten links |
| STAT_TEMPERATUR_MOTOR_HL_WERT | °C | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Temperatur Motor hinten links |
| STAT_SPANNUNG_MOTOR_HR_WERT | V | - | signed int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Motor hinten rechts |
| STAT_STROM_MOTOR_HR_WERT | A | - | signed int | - | - | 1.0 | 1000.0 | 0.0 | Strom Motor hinten rechts |
| STAT_TEMPERATUR_MOTOR_HR_WERT | °C | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Temperatur Motor hinten rechts |
| STAT_AKTUATOR_R | 0-n | - | unsigned char | - | TAB_EMF_POSITION | 1.0 | 1.0 | 0.0 | Position Bremsbacken hinten rechts |
| STAT_AKTUATOR_L | 0-n | - | unsigned char | - | TAB_EMF_POSITION | 1.0 | 1.0 | 0.0 | Position Bremsbacken hinten rechts |
| STAT_HU_MODE_STATUS | 0-n | - | unsigned char | - | TAB_EMF_HU_MODE | - | - | - | Status Modus Hauptuntersuchung |

<a id="table-res-0xd80f-d"></a>
### RES_0XD80F_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MODE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = aktiv; 0 = nicht aktiv |

<a id="table-res-0xd81e-d"></a>
### RES_0XD81E_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TMC_TRAVEL_SENSOR_HW_VERSION_ID_DATA | DATA | high | data[2] | - | - | 1.0 | 1.0 | 0.0 | Hardware-Version ID des verwendeten TMC-Travel Sensor. Wert 0xFFFF bedeutet keine Daten verfügbar. |
| STAT_TMC_TRAVEL_SENSOR_SW_VERSION_ID_DATA | DATA | high | data[2] | - | - | 1.0 | 1.0 | 0.0 | Software-Version ID des verwendeten TMC-Travel Sensor. Wert 0xFFFF bedeutet keine Daten verfügbar. |

<a id="table-res-0xd8e7-d"></a>
### RES_0XD8E7_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AKT_VERBAUT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_AKT_VERBAUT | - | - | - | Aktuell verbaut - ja, nein |
| STAT_AKT_POSITION_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Position in der codierte Reifentabelle |
| STAT_AKT_BREITE_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 10.0 | 1.0 | 95.0 | Reifen Breite |
| STAT_AKT_QUER_VERH_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 5.0 | 1.0 | 10.0 | Reifen Querschnittsverhältnis |
| STAT_AKT_DURCHMESSER_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 12.0 | Reifen Durchmesser |
| STAT_AKT_TRAGFAEHIGKEIT_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 75.0 | Reifen Tragfähigkeit |
| STAT_AKT_GESCHW_IDX_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_GESCHW_IDX | - | - | - | Reifen Geschwindigkeitsindex |
| STAT_AKT_SAISON_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_SAISON | - | - | - | Reifen Saison |
| STAT_AKT_KARKASSE_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_KARKASSE | - | - | - | Reifen Karkasse |
| STAT_AKT_RUNFLAT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_RSC | - | - | - | Reifen Technologie |
| STAT_AKT_WERK_VERBAUT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_WERKSAUSLIEFERUNG | - | - | - | Reifen ab Werksauslieferung: Ja/Nein |
| STAT_AKT_RCP_VA_TB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_AKT_RCP_HA_TB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_AKT_RCP_VA_VB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_AKT_RCP_HA_VB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_AKT_VERBAUT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_AKT_VERBAUT | - | - | - | Aktuell verbaut |
| STAT_AKT_POSITION_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Position in der codierte Reifentabelle |
| STAT_AKT_BREITE_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 10.0 | 1.0 | 95.0 | Reifen Breite |
| STAT_AKT_QUER_VERH_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 5.0 | 1.0 | 10.0 | Reifen Querschnittsverhältnis |
| STAT_AKT_DURCHMESSER_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 12.0 | Reifen Durchmesser |
| STAT_AKT_TRAGFAEHIGKEIT_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 75.0 | Reifen Tragfähigkeit |
| STAT_AKT_GESCHW_IDX_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_GESCHW_IDX | - | - | - | Reifen Geschwindigkeitsindex |
| STAT_AKT_SAISON_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_SAISON | - | - | - | Reifen Saison |
| STAT_AKT_KARKASSE_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_KARKASSE | - | - | - | Reifen Karkasse |
| STAT_AKT_RUNFLAT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_RSC | - | - | - | Reifen Technologie |
| STAT_AKT_WERK_VERBAUT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_WERKSAUSLIEFERUNG | - | - | - | Reifen ab Werksauslieferung: Ja/Nein |
| STAT_AKT_RCP_VA_TB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_AKT_RCP_HA_TB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_AKT_RCP_VA_VB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_AKT_RCP_HA_VB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Vollbeladen oder Geschw. &gt; 160 km/h |

<a id="table-res-0xd8f2-d"></a>
### RES_0XD8F2_D

Dimensions: 34 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ECO_AKT_VERBAUT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_AKT_VERBAUT | - | - | - | Aktuell verbaut - ja, nein |
| STAT_ECO_AKT_POSITION_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Position in der codierte Reifentabelle |
| STAT_ECO_AKT_BREITE_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 10.0 | 1.0 | 95.0 | Reifen Breite |
| STAT_ECO_AKT_QUER_VERH_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 5.0 | 1.0 | 10.0 | Reifen Querschnittsverhältnis |
| STAT_ECO_AKT_DURCHMESSER_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 12.0 | Reifen Durchmesser |
| STAT_ECO_AKT_TRAGFAEHIGKEIT_SOMMERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 75.0 | Reifen Tragfähigkeit |
| STAT_ECO_AKT_GESCHW_IDX_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_GESCHW_IDX | - | - | - | Reifen Geschwindigkeitsindex |
| STAT_ECO_AKT_SAISON_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_SAISON | - | - | - | Reifen Saison |
| STAT_ECO_AKT_KARKASSE_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_KARKASSE | - | - | - | Reifen Karkasse |
| STAT_ECO_AKT_RUNFLAT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_RSC | - | - | - | Reifen Technologie |
| STAT_ECO_AKT_WERK_VERBAUT_SOMMERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_WERKSAUSLIEFERUNG | - | - | - | Reifen ab Werksauslieferung: Ja/Nein |
| STAT_ECO_AKT_RCP_VA_TB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen Eco oder Geschwindigkeit kleiner oder = 160 km/h |
| STAT_ECO_AKT_RCP_HA_TB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen Eco oder Geschwindigkeit  kleiner oder = 160 km/h |
| STAT_ECO_AKT_RCP_VA_TB_ECO_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_ECO_AKT_RCP_HA_TB_ECO_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_ECO_AKT_RCP_VA_VB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_ECO_AKT_RCP_HA_VB_SOMMERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_ECO_AKT_VERBAUT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_AKT_VERBAUT | - | - | - | Aktuell verbaut |
| STAT_ECO_AKT_POSITION_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Position in der codierte Reifentabelle |
| STAT_ECO_AKT_BREITE_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 10.0 | 1.0 | 95.0 | Reifen Breite |
| STAT_ECO_AKT_QUER_VERH_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 5.0 | 1.0 | 10.0 | Reifen Querschnittsverhältnis |
| STAT_ECO_AKT_DURCHMESSER_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 12.0 | Reifen Durchmesser |
| STAT_ECO_AKT_TRAGFAEHIGKEIT_WINTERREIFEN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 75.0 | Reifen Tragfähigkeit |
| STAT_ECO_AKT_GESCHW_IDX_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_GESCHW_IDX | - | - | - | Reifen Geschwindigkeitsindex |
| STAT_ECO_AKT_SAISON_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_SAISON | - | - | - | Reifen Saison |
| STAT_ECO_AKT_KARKASSE_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_KARKASSE | - | - | - | Reifen Karkasse |
| STAT_ECO_AKT_RUNFLAT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_RSC | - | - | - | Reifen Technologie |
| STAT_ECO_AKT_WERK_VERBAUT_WINTERREIFEN | 0-n | high | unsigned char | - | TAB_ERFS_WERKSAUSLIEFERUNG | - | - | - | Reifen ab Werksauslieferung: Ja/Nein |
| STAT_ECO_AKT_RCP_VA_TB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_ECO_AKT_RCP_HA_TB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen oder Geschw. &lt;= 160 km/h |
| STAT_ECO_AKT_RCP_VA_TB_ECO_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Teilbeladen Eco oder Geschwindigkeit kleiner oder = 160 km/h |
| STAT_ECO_AKT_RCP_HA_TB_ECO_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Teilbeladen Eco oder Geschwindigkeit  kleiner oder = 160 km/h |
| STAT_ECO_AKT_RCP_VA_VB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Vorderachse Vollbeladen oder Geschw. &gt; 160 km/h |
| STAT_ECO_AKT_RCP_HA_VB_WINTERREIFEN_WERT | bar | high | unsigned char | - | - | 1.0 | 10.0 | 2.0 | Solldruck Hinterachse Vollbeladen oder Geschw. &gt; 160 km/h |

<a id="table-res-0xdb29-d"></a>
### RES_0XDB29_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TMC_DRUCK_WERT | bar | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Gemessener Druck  im Hauptbremszylinder |
| STAT_SYSTEM_DRUCK_WERT | bar | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Gemessener System Druck |

<a id="table-res-0xdb2a-d"></a>
### RES_0XDB2A_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PRODUKTIONSSTATUS | 0-n | high | unsigned char | - | TAB_PRODUKTIONSSTATUS | - | - | - | Gibt den Zustand des aktuellen Produktionsstatus wieder |

<a id="table-res-0xdbdf-d"></a>
### RES_0XDBDF_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PILLE_VA | 0-n | - | unsigned char | - | TAB_BREMSBELAGVERSCHLEISSSENSOR | - | - | - | Bremsbelagspille Vorderachse |
| STAT_PILLE_HA | 0-n | - | unsigned char | - | TAB_BREMSBELAGVERSCHLEISSSENSOR | - | - | - | Bremsbelagspille Hinterachse |

<a id="table-res-0xdbe2-d"></a>
### RES_0XDBE2_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REKU_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = aktiv;  0 = inaktiv |

<a id="table-res-0xdbe3-d"></a>
### RES_0XDBE3_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WARNUNG_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Warnung (0= inaktiv; 1= aktiv) |
| STAT_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | RPA-System (0= inaktiv; 1= aktiv) |
| STAT_PLATTROLLEN_ERKANNT | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Platte Reifen (0= nicht erkannt; 1= erkannt) |
| STAT_3PLUS1_ERKANNT | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 3Plus1 Konstellation (0= nicht erkannt; 1= erkannt) |
| STAT_NEUREIFEN_ERKANNT | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Neureifen Konstellation (0= nicht erkannt; 1= erkannt) |
| STAT_NAEHERUNG_WARNGRENZE_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aktueller Wert Näherung Warngrenze |
| STAT_PANNEN_POSITION | 0-n | - | unsigned char | - | TAB_POSITION_RAD | - | - | - | Position druckreduziertes Rad |
| STAT_LERNSTATUS_BEREICH_0_100_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 0..100 km/h |
| STAT_LERNSTATUS_BEREICH_100_190_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 100..190 km/h |
| STAT_LERNSTATUS_BEREICH_UEBER_190_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich &gt; 190 km/h |

<a id="table-res-0xdbe4-d"></a>
### RES_0XDBE4_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GESCHWINDIGKEIT_RAD_VL_WERT | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Radgeschwindigkeit vorne links |
| STAT_GESCHWINDIGKEIT_RAD_VR_WERT | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Radgeschwindigkeit vorne rechts |
| STAT_GESCHWINDIGKEIT_RAD_HL_WERT | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Radgeschwindigkeit hinten links |
| STAT_GESCHWINDIGKEIT_RAD_HR_WERT | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Radgeschwindigkeit hinten rechts |
| STAT_GESCHWINDIGKEIT_FZG_WERT | km/h | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Fahrzeuggeschwindigkeit |
| STAT_DREHRICHTUNG_VL | 0-n | - | unsigned char | - | TAB_DREHRICHTUNG | 1.0 | 1.0 | 0.0 | Raddrehrichtung vorne links |
| STAT_DREHRICHTUNG_VR | 0-n | - | unsigned char | - | TAB_DREHRICHTUNG | 1.0 | 1.0 | 0.0 | Raddrehrichtung vorne rechts |
| STAT_DREHRICHTUNG_HL | 0-n | - | unsigned char | - | TAB_DREHRICHTUNG | 1.0 | 1.0 | 0.0 | Raddrehrichtung hinten links |
| STAT_DREHRICHTUNG_HR | 0-n | - | unsigned char | - | TAB_DREHRICHTUNG | 1.0 | 1.0 | 0.0 | Raddrehrichtung hinten rechts |
| STAT_DREHRICHTUNG_REF | 0-n | - | unsigned char | - | TAB_DREHRICHTUNG | 1.0 | 1.0 | 0.0 | Fahrrichtung |
| STAT_SIGNALQUALITAET_VL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signalqualität vorne links x &lt; 10 % = kein Signal;  10 % &lt;= x &lt;= 50 % schwaches Signal;  x &gt; 50 % Signal in Ordnung |
| STAT_SIGNALQUALITAET_VR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signalqualität vorne rechts x &lt; 10 % = kein Signal;  10 % &lt;= x &lt;= 50 % schwaches Signal;  x &gt; 50 % Signal in Ordnung |
| STAT_SIGNALQUALITAET_HL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signalqualität hinten links x &lt; 10 % = kein Signal;  10 % &lt;= x &lt;= 50 % schwaches Signal;  x &gt; 50 % Signal in Ordnung |
| STAT_SIGNALQUALITAET_HR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Signalqualität hinten rechts x &lt; 10 % = kein Signal;  10 % &lt;= x &lt;= 50 % schwaches Signal;  x &gt; 50 % Signal in Ordnung |

<a id="table-res-0xdbf6-d"></a>
### RES_0XDBF6_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MOMENT_SOLL_WERT | Nm | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Sollwert Bremsrekuperation |
| STAT_MOMENT_IST_WERT | Nm | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Istwert Bremsrekuperation |

<a id="table-res-0xdc14-d"></a>
### RES_0XDC14_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RPA_VERSION_NR_1_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hauptversionsnummer RPA-Software |
| STAT_RPA_VERSION_NR_2_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Unterversionsnummer RPA-Software |
| STAT_KM_LETZTE_STANDARDISIERUNG_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand letzte Initialisierung |
| STAT_KM_LETZTE_STANDARDISIERUNG_MINUS_1_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand vorletzte Initialisierung |
| STAT_KM_LETZTE_STANDARDISIERUNG_MINUS_2_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand vor-vorletzten Initialisierung |
| STAT_TAGE_SEIT_LETZTER_STANDARDISIERUNG_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Tage seit der letzten Initialisierung |
| STAT_TAGE_SEIT_LETZTER_STANDARDISIERUNG_MINUS_1_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Tage seit der vorletzten Initialisierung |
| STAT_TAGE_SEIT_LETZTER_STANDARDISIERUNG_MINUS_2_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Tage seit der vor-vorletzten Initialisierung |
| STAT_KM_LETZTE_PANNE_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand letzte erkannten Reifenpanne |
| STAT_KM_LETZTE_PANNE_MINUS_1_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand vorletzte erkannten Reifenpanne |
| STAT_KM_LETZTE_PANNE_MINUS_2_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand vor-vorletzte erkannten Reifenpanne |
| STAT_TAGE_SEIT_LETZTER_PANNE_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Tage seit der letzten erkannten Reifenpanne |
| STAT_TAGE_SEIT_LETZTER_PANNE_MINUS_1_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Tage seit der vorletzten erkannten Reifenpanne |
| STAT_TAGE_SEIT_LETZTER_PANNE_MINUS_2_WERT | d | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Tage seit der vor-vorletzten erkannten Reifenpanne |
| STAT_GESCHWINDIGKEIT_LETZTE_PANNE_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrzeuggeschwindigkeit während der letzten erkannten Reifenpanne |
| STAT_GESCHWINDIGKEIT_LETZTE_PANNE_MINUS_1_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrzeuggeschwindigkeit während der vorletzten erkannten Reifenpanne |
| STAT_GESCHWINDIGKEIT_LETZTE_PANNE_MINUS_2_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrzeuggeschwindigkeit während der vor-vorletzten erkannten Reifenpanne |
| STAT_GESCHWINDIGKEIT_MAX_LETZTE_PANNE_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | max. Fahrzeuggeschwindigkeit nach der letzten erkannten Reifenpanne (erster wert wird frühestens 30 Sekunden nach der Pannenerkennung eingetragen) |
| STAT_GESCHWINDIGKEIT_MAX_LETZTE_PANNE_MINUS_1_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrzeuggeschwindigkeit während der vorletzten erkannten Reifenpanne |
| STAT_GESCHWINDIGKEIT_MAX_LETZTE_PANNE_MINUS_2_WERT | km/h | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Fahrzeuggeschwindigkeit während der vor-vorletzten erkannten Reifenpanne |
| STAT_KM_LETZTE_3PLUS1_ERKENNUNG_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand letzte erkannte 3plus-Konstellation |
| STAT_KM_LETZTE_NEUREIFEN_ERKENNUNG_WERT | km | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand  letzte erkannte Neureifen-Konstellation |
| STAT_NEUREIFEN_POSITON | 0-n | - | unsigned char | - | TAB_POSITION_RAD | - | - | - | Position des Neureifens bei der letzten Erkennung |
| STAT_URSACHE_WARNUNG_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Typ der Warnmeldung (z.B. schnelle Luftfruckverlust etc.) |
| STAT_MAX_NAEHERUNG_WARNGRENZE_SEIT_LETZTER_STD_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Maximale Näherung zur applizierten Warngrenze siet der letzte Initialisierung |

<a id="table-res-0xdc15-d"></a>
### RES_0XDC15_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LERNSTATUS_BEREICH_0_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 0 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_1_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 1 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_2_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 2 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_3_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 3 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_4_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 4 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_5_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 5 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_6_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 6 (100 % = vollständig eingelernt) |
| STAT_LERNSTATUS_BEREICH_7_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernfortschritt Geschwindigkeitsbereich 7 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_0_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 0 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_1_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 1 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_2_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 2 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_3_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 3 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_4_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 4 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_5_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 5 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_6_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 6 (100 % = vollständig eingelernt) |
| STAT_KURVENKOMPENSATION_7_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Kurvenkompensation Geschwindigkeitsbereich 7 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_0_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 0 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_1_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 1 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_2_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 2 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_3_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 3 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_4_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 4 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_5_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 5 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_6_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 6 (100 % = vollständig eingelernt) |
| STAT_MOMENTENKOMPENSATION_7_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Lernstatus Momentenkompensation Momentenbereich 7 (100 % = vollständig eingelernt) |

<a id="table-res-0xdc1d-d"></a>
### RES_0XDC1D_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AUTOHOLD_LED_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = LED ein 0 = LED aus |

<a id="table-res-0xdc6c-d"></a>
### RES_0XDC6C_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ABS_FUNKTION | 0-n | high | unsigned char | - | TAB_ABS_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Antiblockiersystem (ABS) |
| STAT_ABS_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Antiblockiersystem (ABS) |
| STAT_ABS_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Antiblockiersystem (ABS) |

<a id="table-res-0xdc6d-d"></a>
### RES_0XDC6D_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ASC_FUNKTION | 0-n | high | unsigned char | - | TAB_ASC_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Antriebsschlupfregelung (ASC) |
| STAT_ASC_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Antriebsschlupfregelung (ASC) |
| STAT_ASC_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Antriebsschlupfregelung (ASC) |

<a id="table-res-0xdc6e-d"></a>
### RES_0XDC6E_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FDR_FUNKTION | 0-n | high | unsigned char | - | TAB_FDR_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Fahrzeugstabilisierung (FDR) |
| STAT_FDR_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Fahrzeugstabilisierung (FDR) |
| STAT_FDR_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Fahrzeugstabilisierung (FDR) |

<a id="table-res-0xdc70-d"></a>
### RES_0XDC70_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HDC_FUNKTION | 0-n | high | unsigned char | - | TAB_HDC_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Bergabfahrassistent (HDC) |
| STAT_HDC_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Bergabfahrassistent (HDC) |
| STAT_HDC_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Bergabfahrassistent (HDC) |

<a id="table-res-0xdc95-d"></a>
### RES_0XDC95_D

Dimensions: 17 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | 0-n | high | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Status Eigenräder |
| STAT_RADPOS_ER_BEKANNT | 0-n | high | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Status Radposition der Eigenräder |
| STAT_DTC_INACTIVE | 0-n | high | unsigned char | - | TAB_RDC_DTC_ACTIVE_STATUS | - | - | - | Status DTC Fehler mit Warnlampe im Fehlerspeicher. |
| STAT_KAL_ANFORDERUNG_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_CAL_ACTIVE | - | - | - | Status Kalibrieranforderung. |
| STAT_RAD_ZUORDNUNG_TIMEOUT | 0-n | high | unsigned char | - | TAB_RDC_TIMEOUT | - | - | - | Status Radzuordnung Timeout |
| STAT_BANDMODE_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_BANDMODE_ACTIVE | - | - | - | Status Bandmode. |
| STAT_TEST_EIGENRAD_FAHRT | 0-n | high | unsigned char | - | TAB_RDC_STARTED | - | - | - | Status Test-Eigenraderkennung in Fahrt. |
| STAT_ER_FAHRT_VTHRS_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert. |
| STAT_BM_TIMEOUT_ACTIVE | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Bandmode Timeout laeuft. |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Harte Warnung unspezifisch |
| STAT_HARTE_WARNUNG_VL_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Harte Warnung vorn links |
| STAT_HARTE_WARNUNG_VR_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Harte Warnung vorn rechts |
| STAT_HARTE_WARNUNG_HL_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Harte Warnung hinten links |
| STAT_HARTE_WARNUNG_HR_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_ZUSTAND | - | - | - | Status Harte Warnung hinten rechts |
| STAT_KL_15_EIN | 0-n | high | unsigned char | - | TAB_RDC_ON_OFF | - | - | - | Status Klemme 15 |
| STAT_FZG_FAEHRT | 0-n | high | unsigned char | - | TAB_RDC_VEHICLE_RUNNING | - | - | - | Status Fahrzeug fährt |
| STAT_ERKENNUNG_ALLE_RE | 0-n | high | unsigned char | - | TAB_RDC_DETECTED | - | - | - | Status erkennung Radelektroniken |

<a id="table-res-0xdc96-d"></a>
### RES_0XDC96_D

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_1_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_1_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_1_INTERNER_FEHLERCODE | 0-n | high | unsigned char | - | TAB_RDC_INT_FEHLER | - | - | - | SG-interner Fehlercode |
| STAT_1_ZAEHLER_INAKTIV_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Inaktiv-Ereignisse |
| STAT_2_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_2_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_2_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_2_INTERNER_FEHLERCODE | 0-n | high | unsigned char | - | TAB_RDC_INT_FEHLER | - | - | - | SG-interner Fehlercode |
| STAT_2_ZAEHLER_INAKTIV_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Inaktiv-Ereignisse |
| STAT_3_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_3_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_3_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_3_INTERNER_FEHLERCODE | 0-n | high | unsigned char | - | TAB_RDC_INT_FEHLER | - | - | - | SG-interner Fehlercode |
| STAT_3_ZAEHLER_INAKTIV_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Inaktiv-Ereignisse |

<a id="table-res-0xdc97-d"></a>
### RES_0XDC97_D

Dimensions: 72 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_PLAUSI_DRUCK | 0-n | high | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_1_KALIBRIERUNG | 0-n | high | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_1_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_1_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_1_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_1_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierte Aussentemperatur beim Befüllen |
| STAT_1_BEFUELL_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_1_RADPOSITION_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_1_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_1_SOLLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE0 |
| STAT_1_RADPOSITION_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_1_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_1_SOLLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE1 |
| STAT_1_RADPOSITION_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_1_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_1_SOLLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE2 |
| STAT_1_RADPOSITION_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_1_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_1_SOLLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE3 |
| STAT_1_ZAEHLER_KALIBRIERUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Kalibrierereignisse |
| STAT_2_PLAUSI_DRUCK | 0-n | high | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_2_KALIBRIERUNG | 0-n | high | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_2_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_2_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_2_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_2_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierte Aussentemperatur beim Befüllen |
| STAT_2_BEFUELL_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_2_RADPOSITION_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_2_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_2_SOLLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE0 |
| STAT_2_RADPOSITION_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_2_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_2_SOLLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE1 |
| STAT_2_RADPOSITION_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_2_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_2_SOLLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE2 |
| STAT_2_RADPOSITION_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_2_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_2_SOLLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE3 |
| STAT_2_ZAEHLER_KALIBRIERUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Kalibrierereignisse |
| STAT_3_PLAUSI_DRUCK | 0-n | high | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_3_KALIBRIERUNG | 0-n | high | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_3_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_3_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_3_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_3_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierte Aussentemperatur beim Befüllen |
| STAT_3_BEFUELL_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_3_RADPOSITION_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_3_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_3_SOLLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE0 |
| STAT_3_RADPOSITION_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_3_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_3_SOLLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE1 |
| STAT_3_RADPOSITION_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_3_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_3_SOLLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE2 |
| STAT_3_RADPOSITION_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_3_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Befuelltemperaturwert Radelektronik RE0 (215 °C =&gt; ungueltig) |
| STAT_3_SOLLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruckwert Radelektronik RE3 |
| STAT_3_ZAEHLER_KALIBRIERUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Kalibrierereignisse |

<a id="table-res-0xdc98-d"></a>
### RES_0XDC98_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_WERT | HEX | high | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock). |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL_WERT | dBm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Störpegelabstand |
| STAT_RESTLEBENSDAUER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor. Entweder analoger Wert in 10% - Schritte oder kodierter Wert (11=i.O; 1=n.i.O) |
| STAT_RADELEKTRONIK_STATUS | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad |
| STAT_POS_CHANGED | 0-n | high | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert |
| STAT_FOLGEAUSFALL_WERT | s | high | unsigned char | - | - | 5.0 | 1.0 | 0.0 | Fahrzeit ohne Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | high | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | high | unsigned char | - | TAB_RDC_RE_SENDEMODE_AK | - | - | - | Sendemode der Radelektronik |
| STAT_TELEGRAMMTYP | 0-n | high | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc99-d"></a>
### RES_0XDC99_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_WERT | HEX | high | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock). |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL_WERT | dBm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Störpegelabstand |
| STAT_RESTLEBENSDAUER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor. Entweder analoger Wert in 10% - Schritte oder kodierter Wert (11=i.O; 1=n.i.O) |
| STAT_RADELEKTRONIK_STATUS | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad |
| STAT_POS_CHANGED | 0-n | high | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert |
| STAT_FOLGEAUSFALL_WERT | s | high | unsigned char | - | - | 5.0 | 1.0 | 0.0 | Fahrzeit ohne Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | high | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | high | unsigned char | - | TAB_RDC_RE_SENDEMODE_AK | - | - | - | Sendemode der Radelektronik |
| STAT_TELEGRAMMTYP | 0-n | high | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9a-d"></a>
### RES_0XDC9A_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_WERT | HEX | high | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock). |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL_WERT | dBm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Störpegelabstand |
| STAT_RESTLEBENSDAUER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor. Entweder analoger Wert in 10% - Schritte oder kodierter Wert (11=i.O; 1=n.i.O) |
| STAT_RADELEKTRONIK_STATUS | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad |
| STAT_POS_CHANGED | 0-n | high | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert |
| STAT_FOLGEAUSFALL_WERT | s | high | unsigned char | - | - | 5.0 | 1.0 | 0.0 | Fahrzeit ohne Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | high | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | high | unsigned char | - | TAB_RDC_RE_SENDEMODE_AK | - | - | - | Sendemode der Radelektronik |
| STAT_TELEGRAMMTYP | 0-n | high | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9b-d"></a>
### RES_0XDC9B_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_WERT | HEX | high | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock). |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL_WERT | dBm | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Störpegelabstand |
| STAT_RESTLEBENSDAUER_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor. Entweder analoger Wert in 10% - Schritte oder kodierter Wert (11=i.O; 1=n.i.O) |
| STAT_RADELEKTRONIK_STATUS | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | high | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad |
| STAT_POS_CHANGED | 0-n | high | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert |
| STAT_FOLGEAUSFALL_WERT | s | high | unsigned char | - | - | 5.0 | 1.0 | 0.0 | Fahrzeit ohne Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | high | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | high | unsigned char | - | TAB_RDC_RE_SENDEMODE_AK | - | - | - | Sendemode der Radelektronik |
| STAT_TELEGRAMMTYP | 0-n | high | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9c-d"></a>
### RES_0XDC9C_D

Dimensions: 29 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Warnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Warnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Warnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Warnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Warnereignis Anzahl |
| STAT_ZAEHLER_KM_V_BIS_100KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &lt;= 100 km/h |
| STAT_ZAEHLER_KM_100KMH_V_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit 100 km/h &lt; v &lt;= 160 km/h |
| STAT_ZAEHLER_KM_V_MEHLR_ALS_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &gt; 160 km/h |
| STAT_MAX_GESCHW_MIT_WARNUNG_WERT | km/h | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Maximale Geschwindigkeit mit vorliegende Warnung |

<a id="table-res-0xdc9d-d"></a>
### RES_0XDC9D_D

Dimensions: 29 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Warnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Warnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Warnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Warnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Warnereignis Anzahl |
| STAT_ZAEHLER_KM_V_BIS_100KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &lt;= 100 km/h |
| STAT_ZAEHLER_KM_100KMH_V_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit 100 km/h &lt; v &lt;= 160 km/h |
| STAT_ZAEHLER_KM_V_MEHLR_ALS_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &gt; 160 km/h |
| STAT_MAX_GESCHW_MIT_WARNUNG_WERT | km/h | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Maximale Geschwindigkeit mit vorliegende Warnung |

<a id="table-res-0xdc9e-d"></a>
### RES_0XDC9E_D

Dimensions: 29 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Warnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Warnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Warnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Warnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Warnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Warnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Warnereignis Anzahl |
| STAT_ZAEHLER_KM_V_BIS_100KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &lt;= 100 km/h |
| STAT_ZAEHLER_KM_100KMH_V_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit 100 km/h &lt; v &lt;= 160 km/h |
| STAT_ZAEHLER_KM_V_MEHLR_ALS_160KMH_WERT | km | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer mit v &gt; 160 km/h |
| STAT_MAX_GESCHW_MIT_WARNUNG_WERT | km/h | high | unsigned char | - | - | 2.0 | 1.0 | 0.0 | Maximale Geschwindigkeit mit vorliegende Warnung |

<a id="table-res-0xdc9f-d"></a>
### RES_0XDC9F_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnung Rücknahme. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnung Rücknahme. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Warnung Rücknahme. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnung Rücknahme. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Warnungs- Rüchnahmeauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Warnungs- Rüchnahmeauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Warnung Rücknahme. |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Warnung Rücknahme. |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Warnung Rücknahme. |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Warnung Rücknahme. |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Warnung Rücknahme. |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Warnung Rücknahme. |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Warnung Rücknahme. |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Warnung Rücknahme. |
| STAT_ZAEHLER_WARN_RUECKNAHME_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zähler für Warnungsrücknahmen durch Luftnachfüllen oder Radtausch. |

<a id="table-res-0xdcd9-d"></a>
### RES_0XDCD9_D

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_RE0_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE0 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE0. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE0_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE0 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE1 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE1. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE1 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE2 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE2. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE2 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE3 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE3. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE3 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE4_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE4 |
| STAT_REIFENDRUCK_RE4_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE4 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE4. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE4 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE5_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE5 |
| STAT_REIFENDRUCK_RE5_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE5 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE5. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE5 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE6_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE6 |
| STAT_REIFENDRUCK_RE6_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE6 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE6. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE6 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE7_WERT | HEX | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Identifier Radelektronik RE7 |
| STAT_REIFENDRUCK_RE7_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE7 (65.535 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Batterie Status der Radsensor RE7. Analog Wert in Prozent oder kodiert (11=i.O; 1=n.i.O) |
| STAT_EMPFANGSZAEHLER_RE7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE7 (255 =&gt; ungueltig) |

<a id="table-res-0xdcf1-d"></a>
### RES_0XDCF1_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Vorwarnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Vorwarnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorwarnereignis Anzahl |

<a id="table-res-0xdcf2-d"></a>
### RES_0XDCF2_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Vorwarnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Vorwarnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorwarnereignis Anzahl |

<a id="table-res-0xdcf3-d"></a>
### RES_0XDCF3_D

Dimensions: 25 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | high | string[8] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Vorwarnung. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand. 4.294.967.295 =&gt; ungültig |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Korrigierter Aussentemperatur beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aussentemperatur beim Vorwarnung. |
| STAT_AUSSENDRUCK_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Vorwarnung. |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RE_STATUS | - | - | - | Radelektronik-Status des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Vorwarnungsauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE0 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE0_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE0 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE1 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE1 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE1 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE2 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE2 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE2 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_RADPOSITON_RE3 | 0-n | high | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Solldruck RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | high | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Von Radelektronik RE3 gesendete Druckwert bei Vorwarnereignis |
| STAT_REIFENTEMPERATUR_RE3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -50.0 | Von Radelektronik RE3 gesendete Temperaturwert bei Vorwarnereignis |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorwarnereignis Anzahl |

<a id="table-res-0xde5b-d"></a>
### RES_0XDE5B_D

Dimensions: 28 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_1_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_1_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_1_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_1_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_1_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_1_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_2_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_2_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_2_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_2_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_2_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_2_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_2_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_3_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_3_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_3_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_3_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_3_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_3_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_3_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_4_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_4_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_4_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_4_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_4_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_4_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_4_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |

<a id="table-res-0xde5c-d"></a>
### RES_0XDE5C_D

Dimensions: 56 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_1_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_1_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_1_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_1_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_1_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_1_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_2_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_2_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_2_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_2_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_2_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_2_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_2_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_3_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_3_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_3_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_3_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_3_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_3_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_3_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_4_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_4_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_4_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_4_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_4_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_4_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_4_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_5_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_5_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_5_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_5_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_5_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_5_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_5_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_6_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_6_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_6_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_6_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_6_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_6_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_6_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_7_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_7_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_7_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_7_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_7_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_7_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_7_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |
| STAT_8_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_8_REIFENSERIENNR_DATA | DATA | - | data[11] | - | - | - | - | - | Reifenseriennummer |
| STAT_8_DOT_DATA | DATA | - | data[9] | - | - | - | - | - | DOT |
| STAT_8_REIFENDIMENSION_DATA | DATA | - | data[6] | - | - | - | - | - | Reifendimension |
| STAT_8_REIFENTYP_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifentyp |
| STAT_8_REIFEN_POSTION_WERT | HEX | - | unsigned char | - | - | - | - | - | Reifen position |
| STAT_8_MONTAGE_WERT | HEX | - | unsigned char | - | - | - | - | - | Montiert Ja/Nein |

<a id="table-res-0xde5d-d"></a>
### RES_0XDE5D_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_1_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_1_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_1_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_1_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_1_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_2_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_2_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_2_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_2_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_2_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_2_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_3_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_3_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_3_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_3_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_3_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_3_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_4_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_4_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_4_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_4_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_4_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_4_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |

<a id="table-res-0xde5e-d"></a>
### RES_0XDE5E_D

Dimensions: 48 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_1_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_1_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_1_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_1_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_1_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_2_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_2_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_2_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_2_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_2_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_2_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_3_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_3_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_3_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_3_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_3_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_3_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_4_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_4_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_4_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_4_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_4_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_4_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_5_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_5_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_5_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_5_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_5_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_5_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_6_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_6_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_6_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_6_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_6_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_6_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_7_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_7_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_7_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_7_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_7_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_7_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |
| STAT_8_REIFEN_NR_WERT | - | - | unsigned char | - | - | - | - | - | Reifennummer am Fahrzeug |
| STAT_8_LETZTE_MONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Montage Datum |
| STAT_8_LETZTE_MONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Montage Km |
| STAT_8_LETZTE_DEMONTAGE_DATUM_DATA | DATA | - | data[6] | - | - | - | - | - | Letzte Demontage Datum |
| STAT_8_LETZTE_DEMONTAGE_KM_WERT | km | - | unsigned long | - | - | - | - | - | Letzte Demontage Km |
| STAT_8_LAUFLEISTUNG_AM_FZG_WERT | km | - | unsigned long | - | - | - | - | - | Laufleistung an diesem Fahrzeug |

<a id="table-res-0xf000-r"></a>
### RES_0XF000_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CPU_LAST_WERT | + | - | - | % | high | signed int | - | - | 1.0 | 10.0 | 0.0 | Ausgabe der max CPU Last in % |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 84 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FS_LOESCHEN_PERMANENT | 0x1060 | - | Job zum Löschen der Permanent-DTCs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FEHLERSPEICHER_ENDE_WERKSABLAUF | 0x1061 | - | Löschen von Einzelfehlern und Permanent-DTCs unterbindet | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x1061_R |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| KILOMETERSTAND_BRS | 0x2595 | STAT_KILOMETERSTAND_WERT | Von dem Steuergerät berechneter Kilometerstand | km | - | High | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _SW_IDENTIFIKATION | 0x4000 | STAT_SW_DATA | 11 Bytes SW-Identifikation | DATA | - | High | data[11] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _STEUERN_RDC_DEVELOPER_CONFIG | 0x5000 | - | Steuert Software Parameter Änderungen um die automatisierte Tests am HIL zu unterstützen. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5000_D | - |
| _STEUERN_RDC_ERFS_DEVELOPER_CONFIG | 0x5001 | - | Entwicklungs Diagnose Job für automatisierte Tests. Ändert Software Parametern. | - | - | - | - | - | - | - | - | - | 2E | ARG_0x5001_D | - |
| _STATUS_RDC_DEVELOPER_DATA_LESEN | 0x5002 | - | Liest Entwicklungs spezifische Daten aus dem RDCi Software. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x5002_D |
| EPB_COUNTER | 0x5038 | - | Gibt Zähler der Ereignisse mit Parkbremsaktivität zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x5038_D |
| RADDREHZAHLSENSORPRUEFUNG | 0xA065 | - | Starten, Stoppen und Status Funktionsprüfung Raddrehzahlsensor | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA065_R | RES_0xA065_R |
| RPA_RESET_STATISTIK | 0xA068 | - | Reset RPA Lerndaten Statistik | - | - | - | - | - | - | - | - | - | 31 | - | - |
| RPA_RESET_STANDARDISIERUNG | 0xA074 | - | Reset RPA Standardisierung | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FLM_RESET | 0xA130 | - | Field Load Manager (FLM) Daten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA130_R |
| TMC_TRAVEL_SENSOR_CALIBRATION | 0xA14B | - | Start und Statusabfrage der Kalibrierung vom TMC Travel Sensor (TTS) | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA14B_R |
| IB_ENTLUEFTUNG | 0xA154 | - | Starten, Stoppen und Status Entlüftung | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA154_R |
| EXTERNE_ANFORDERUNG_GKU_IPB_ZAEHLER_RUECKSETZEN | 0xA1AA | - | Zaehler fuer Uebernahmen durch externe Anforderung Getriebe ruecksetzen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| EVAKUIERUNG_UND_BEFUELLUNG | 0xA3A0 | - | Diese Routine soll im Werk während der Evakuierung und Befuellung des Bremssystems am Band ausgefuehrt werden. Die Routine schaltet Ventile des elektronischen Bremssystems, um eine korrekte Befuellung des gesamten Bremssystems zu ermoeglichen. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA3A0_R | RES_0xA3A0_R |
| NACHARBEITSENTLUEFTUNG | 0xA3A1 | - | Diese Routine soll  im Werk während der Evakuierung und Befuellung des Bremssystems im Nacharbeitsbereich ausgefuehrt werden, wenn der Standard Prozess zur Evakuierung und Befuellung am Band fehlgeschlagen ist. Die Routine schaltet Ventile des elektronischen Bremssystems, um eine korrekte Befuellung des gesamten Bremssystems zu ermoeglichen. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA3A1_R | RES_0xA3A1_R |
| BEFUELLKONTROLLE | 0xA3A2 | - | Diese Routine soll nach der Befuellung des Bremssystems (Evakuierung und Befuellung / Nacharbeitsentlueftung)  ausgefuehrt werden, um zu kontrollieren, ob die Hydraulische Steuereinheit korrekt befuellt wurde.  Die Routine bewertet, ob das LAC Verschiebevolumen, um einen definierten Druck zu erreichen unter einem Grenzwert ist, der bei ordnungsgemäßer Anwendung der spezifizierten Befüllroutinen erreichbar ist.  | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA3A2_R |
| VOLUMENAUFNAHME_DICHTHEITSUEBERPRUEFUNG_DER_RADSEITE | 0xA3A3 | - | Diese Routine kann nach der Befuellung des Bremssystems (Evakuierung und Befuellung / Nacharbeitsentlueftung)  ausgefuehrt werden, um zu testen, ob die Radseite des Bremssystems korrekt befuellt wurde. Die Routine stoesst den Druckregler an, um fuer einen definierten Arbeitspunkt im Rad (50 bar) das verschobene Volumen zu messen. Auf dieser Basis kann der OEM eine Druck-Zu-Weg Plausibilisierung durchfuehren und so Luft und Leckagen in den Radbremsen zu erkennen. | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA3A3_R |
| VERTAUSCHUNGSTEST | 0xA3A4 | - | Diese Routine soll ausgefuehrt werden, um den korrekten Anschluss der Radbremsleitungen an die Hydraulische Steuereinheit und die korrekte Zuordnung der Raddrehzahl-Sensoren zu den Rändern zu verifizieren. Dafuer wird das Fahrzeug auf einem Rollenpruefstand platziert. Das zu testende Rad wird auf eine festgelegte Geschwindigkeit beschleunigt und die Routine fuer das entsprechende Rad wird gestartet. Die Radgeschwindigkeiten vor und nach der Verzoegerung werden gemessen und deren Delta gebildet. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA3A4_R | RES_0xA3A4_R |
| DRUCKSENSOR_OFFSET_ABGLEICH | 0xA3A5 | - | Dieser Diagnoseservice soll ausgefuehrt werden, um den Nullpunkt der Drucksensoren (Hauptbremszylinder / System) im Speicher der Elektronischen Steuereinheit abzulegen. | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA3A5_R |
| EMF_VERFAHREN | 0xA803 | - | Anfahren Position | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA803_R | RES_0xA803_R |
| CBS_BREMSE_DETAILS | 0xD272 | - | CBS-Daten der Bremsen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD272_D |
| LESEN_KOMPATIBILITAETSINDEX | 0xD367 | STAT_KOMPATIBILITAETSINDEX_WERT | Lesen der Kompatibilitaets-Index vom Steuergeraet. | HEX | - | High | signed long | - | - | - | - | - | 22 | - | - |
| PBC_SW_VERSION | 0xD690 | - | Gibt die PBC (Park Brake Control) SW Version zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD690_D |
| EMF_AKTUATOR_KOMBISATTEL | 0xD805 | - | Auslesen Daten Aktuator | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD805_D |
| EMF_TASTER | 0xD80D | STAT_TASTER_EMF | Bedienzustand | 0-n | - | - | unsigned char | TAB_EMF_TASTER | - | - | - | - | 22 | - | - |
| EMF_MONTAGE_MODE | 0xD80F | - | Auslesen und Vorgeben Montagemodus (Sperrung Bedienung) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD80F_D | RES_0xD80F_D |
| EXTERNE_ANFORDERUNG_GKU_IPB_ZAEHLER_LESEN | 0xD81A | STAT_AKTUELLER_ZAEHLERSTAND_GKU_WERT | Gibt Anzahl der IPB-Uebernahmen durch externe Getriebe-Anforderungen zurueck | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| TMC_TRAVEL_SENSOR_HW_SW_VERSION_ID | 0xD81E | - | Der Diagnoseservice dient zum Auslesen der Hard- und Software-Version - Identifikationsnummern des verwendeten TMC-Travel Sensor (Hauptbremszylinder Wegsensor). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD81E_D |
| STATUS_RDC_ERFS_AKT_REIFEN_LESEN | 0xD8E7 | - | Elektronischer Reifenfülldruckschild aktuell verbaute Reifen lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD8E7_D |
| STATUS_RDC_ERFS_TSA_DATEN_LESEN | 0xD8E8 | STAT_TSA_DATA | Tyre Sales Assistant Händler Daten | DATA | - | High | data[104] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STEUERN_RDC_ERFS_TSA_DATEN_VORGEBEN | 0xD8E9 | - | Tyre Sales Assistant Daten vorgeben | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD8E9_D | - |
| STATUS_RDC_ERFS_AKT_REIFEN_ECO_LESEN | 0xD8F2 | - | Elektronischer Reifenfülldruckschild aktuell verbaute Reifen ECO lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD8F2_D |
| STEUERN_RDC_ERFS_ECO_AKT_REIFEN_POS_VORGEBEN | 0xD8F3 | - | Elektronischer Reifenfülldruckschild aktuell verbaute ECO Reifen vorgeben | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD8F3_D | - |
| STEUERN_RDC_ERFS_ECO_NEUE_REIFEN_VORGEBEN | 0xD8F4 | - | Elektronischer Reifenfülldruckschild neue Reifen vorgeben | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD8F4_D | - |
| STEUERN_RDC_ERFS_ECO_REIFENTABELLE_VORGEBEN | 0xD8F5 | - | Reifentabelle Vorgeben | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD8F5_D | - |
| STATUS_BREMSPEDAL | 0xD9EF | STAT_BREMSPEDAL | Auslesen Bremspedal;  Auswertung des Signals BLS_OUT: 0 - Bremspedal nicht betätigt; 1 - Bremspedal betätigt | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| TMC_TRAVEL_SENSOR_SIGNAL | 0xD9F4 | STAT_TMC_TRAVEL_SENSOR_SIGNAL_WERT | Der kalibrierrte (Offset korrigierte) TMC-Travel Sensor Signal Wert | mm | - | High | signed int | - | 4.0 | 100.0 | 0.0 | - | 22 | - | - |
| DRUCKSENSOR_LESEN | 0xDB29 | - | Dieser Diagnoseservice soll ausgefuehrt werden, um den aktuell gemessenen Wert der Drucksensoren (Hauptbremszylinder / System) zu lesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDB29_D |
| PRODUKTIONSSTATUS_SCHALTEN | 0xDB2A | - | Dieser Diagnoseservice soll genutzt werden, um den Produktionsstatus zu verändern. Der Produktionsstatus muss manuell durch den Bediener während des Befuellens des Bremssystems gesetzt werden, um ein ungewolltes, trockenes Bewegen des Linearaktuators zu vermeiden. | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDB2A_D | RES_0xDB2A_D |
| RDC_ANLERNEN_LOKALISIERUNG_LESEN | 0xDB45 | STAT_RDC_ANLERNEN_LOKALISIERUNG_DATA | Lokalisierungs-/Anlerndaten der RDC Radelektronik | DATA | - | High | data[200] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| BREMSBELAGSSENSOR | 0xDBDF | - | Auslesen Bremsbelagssensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBDF_D |
| REKU_FUNKTION | 0xDBE2 | - | Auslesen und Vorgeben Aktivierung Funktion Rekuperation (Bremsenergierückgewinnung) aktueller Klemme15 Zyklus | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDBE2_D | RES_0xDBE2_D |
| REIFENPANNENANZEIGE | 0xDBE3 | - | Reifenpannenanzeige | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE3_D |
| GESCHWINDIGKEIT_RAD | 0xDBE4 | - | Auslesen Raddrehzahlfühler | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE4_D |
| BREMSREKUPERATIONSMOMENT | 0xDBF6 | - | Auslesen Radmoment Bremsrekuperation | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBF6_D |
| RPA_LERNDATEN_STATISTIK | 0xDC14 | - | Auslesen Lerndaten Statisik | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC14_D |
| RPA_LERNDATEN_STD | 0xDC15 | - | Auslesen Lerndaten Standardisierung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC15_D |
| AUTOHOLDLED | 0xDC1D | - | Auslesen und Vorgeben AutoHold LED | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC1D_D | RES_0xDC1D_D |
| BREMSFLUESSIGKEITSSCHALTER | 0xDC1F | STAT_BREMSFLUESSIGKEIT_NIVEAU_SCHALTER_EIN | Auslesen Niveau Bremsflüssigkeit 1 = Bremsflüssigkeit vorhanden;  0 = Bremsflüssigkeit leer oder Unterbrechung | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| ABS_FUNKTION | 0xDC6C | - | Auslesen Status Funktion Antiblockiersystem (ABS) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6C_D |
| ASC_FUNKTION | 0xDC6D | - | Auslesen Status Funktion Antriebsschlupfregelung (ASC) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6D_D |
| FDR_FUNKTION | 0xDC6E | - | Auslesen Status Funktion Fahrzeugstabilisierung (FDR) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6E_D |
| HDC_FUNKTION | 0xDC70 | - | Auslesen Status Funktion Bergabfahrassistent (HDC) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC70_D |
| STATUS_RDC_VERSION | 0xDC94 | STAT_RDC_VERSION_WERT | Aktuelle Software Version | HEX | - | High | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_RDC_LESEN | 0xDC95 | - | Reifendruckkontrolle Status Abfragen bezüglich Eigenradabfragen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC95_D |
| RDC_HS_INAKTIVEREIGNIS | 0xDC96 | - | Reifendruckkontrolle Systemzustand beim Systemausfall und Ausfallursache. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC96_D |
| RDC_HS_KALIBRIEREREIGNIS | 0xDC97 | - | Reifendruckkontrolle Systemzustand nach Radzuordung (Kalibrierung). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC97_D |
| RDC_MESSDATENBLOCK_1 | 0xDC98 | - | Reifendruckkontrolle System Informationen vom am Fahrzeug erkannten Radelektroniken. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC98_D |
| RDC_MESSDATENBLOCK_2 | 0xDC99 | - | Reifendruckkontrolle System Informationen vom am Fahrzeug erkannten Radelektroniken. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC99_D |
| RDC_MESSDATENBLOCK_3 | 0xDC9A | - | Reifendruckkontrolle System Informationen vom am Fahrzeug erkannten Radelektroniken. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9A_D |
| RDC_MESSDATENBLOCK_4 | 0xDC9B | - | Reifendruckkontrolle System Informationen vom am Fahrzeug erkannten Radelektroniken. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9B_D |
| RDC_HS_WARNEREIGNIS_1 | 0xDC9C | - | Reifendruckkontrolle Systemzustand beim Warnereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9C_D |
| RDC_HS_WARNEREIGNIS_2 | 0xDC9D | - | Reifendruckkontrolle Systemzustand beim Warnereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9D_D |
| RDC_HS_WARNEREIGNIS_3 | 0xDC9E | - | Reifendruckkontrolle Systemzustand beim Warnereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9E_D |
| RDC_HS_WARNEREIGNIS_RUECKNAHME | 0xDC9F | - | Reifendruckkontrolle Systemzustand beim Warnereignis Rücknahme. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9F_D |
| STEUERN_RADELEKTRONIK_VORGEBEN | 0xDCC0 | - | Radelektronik vorgeben. Der Job weist der Radelektronik die durch das 1.Argument angewählt wurde, ihre Position am Fahrzeug zu (z.B. vorn rechts). Die Radelektronik kennt sonst ihre Position im Fahrzeug nicht. Sie kennt nur ihre ID. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC0_D | - |
| STEUERN_DIGITAL_RDC | 0xDCC6 | - | Reifendruckkontrolle steuern diverser Bandmodi | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC6_D | - |
| STATUS_RE_LESEN_DRUCKCODIERUNG | 0xDCD9 | - | Reifendruckcodierung für RDC-Sensoren (HO) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD9_D |
| RDC_HS_WARNEREIGNIS_WEICH_1 | 0xDCF1 | - | Reifendruckkontrolle Systemzustand beim Befüll Hinweis Ereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF1_D |
| RDC_HS_WARNEREIGNIS_WEICH_2 | 0xDCF2 | - | Reifendruckkontrolle Systemzustand beim Befüll Hinweis Ereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF2_D |
| RDC_HS_WARNEREIGNIS_WEICH_3 | 0xDCF3 | - | Reifendruckkontrolle Systemzustand beim Befüll Hinweis Ereignis. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF3_D |
| RDC_RID_AKT_REIFEN_QR_CODE_LESEN | 0xDE5B | - | Aktuelle Reifen QR Code Lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE5B_D |
| RDC_RID_ALTE_REIFEN_QR_CODE_LESEN | 0xDE5C | - | Alte Reifen QR Code Lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE5C_D |
| RDC_RID_AKT_REIFEN_LAUFSTRECKE_LESEN | 0xDE5D | - | Aktuelle Reifen Laufstrecke Lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE5D_D |
| RDC_RID_ALTE_REIFEN_LAUFSTRECKE_LESEN | 0xDE5E | - | Alte Reifen Laufstrecke Lesen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE5E_D |
| SECURITY_ZAEHLER_LESEN | 0xE37A | STAT_ZAEHLERSTAND_SECURITY_ZAEHLER_WERT | Stand des Security-Zählers | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _AUSGABE_PROZESSOR_LAST | 0xF000 | - | Diese Routine soll genutzt werden, um die ermittelten max CPU Last Werte auszugeben. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF000_R | RES_0xF000_R |
| _LOESCHEN_PROZESSOR_LAST | 0xF001 | - | Diese Routine soll genutzt werden, um die ermittelten max CPU Last Werte zurückzusetzen. | - | - | - | - | - | - | - | - | - | 31 | - | - |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |
| _OBD_PERMANENT_ENTRIEGELN | 0xFD05 | - | Entriegelung von permanenten OBD-Fehlerspeicher: Verriegelungsbit wird auf 1 gesetzt. | - | - | - | - | - | - | - | - | - | 31 | - | - |

<a id="table-tab-abs-funktion"></a>
### TAB_ABS_FUNKTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verfügbar |
| 1 | verfügbar |
| 2 | verfügbar Rückfallebene |
| 0xFF | ungültig |

<a id="table-tab-aktiv-inaktiv"></a>
### TAB_AKTIV_INAKTIV

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |
| 0xFF | Wert ungültig |

<a id="table-tab-asc-funktion"></a>
### TAB_ASC_FUNKTION

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verfügbar |
| 1 | verfügbar |
| 2 | verfügbar Rückfallebene |
| 3 | verfügbar Schlupf aufgeweitet |
| 4 | verfügbar Rückfallebene Schlupf aufgeweitet |
| 0xFF | ungültig |

<a id="table-tab-bremsbelagverschleisssensor"></a>
### TAB_BREMSBELAGVERSCHLEISSSENSOR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | Pille durchgeschliffen |
| 0xFF | ungültig |

<a id="table-tab-bremsenstatus-links"></a>
### TAB_BREMSENSTATUS_LINKS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Angelegt |
| 0x10 | beim Schließen |
| 0x20 | Geschlossen |
| 0x30 | Geöffnet |
| 0x40 | beim Öffnen |
| 0x50 | unbekannt / fehlerhaft |
| 0x60 | Initialisierung |
| 0x70 | in Montageposition |
| 0x80 | beim Anfahren der Montageposition |
| 0xFF | Wert ungültig |

<a id="table-tab-bremsenstatus-rechts"></a>
### TAB_BREMSENSTATUS_RECHTS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Angelegt |
| 0x01 | beim Schließen |
| 0x02 | Geschlossen |
| 0x03 | Geöffnet |
| 0x04 | beim Öffnen |
| 0x05 | unbekannt / fehlerhaft |
| 0x06 | Initialisierung |
| 0x07 | in Montageposition |
| 0x08 | beim Anfahren der Montageposition |
| 0xFF | Wert ungültig |

<a id="table-tab-differenzgeschwindigkeit"></a>
### TAB_DIFFERENZGESCHWINDIGKEIT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK, Differenzgeschwindigkeit erreicht |
| 0x01 | Not OK, Differenzgeschwindigkeit nicht erreicht |
| 0xFF | Wert ungültig |

<a id="table-tab-drehrichtung"></a>
### TAB_DREHRICHTUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stand |
| 0x01 | Vorwaerts |
| 0x02 | Rueckwaerts |
| 0x03 | nicht definiert |

<a id="table-tab-emf-hu-mode"></a>
### TAB_EMF_HU_MODE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aktiv |
| 0x01 | Stufe 1 |
| 0x02 | Stufe 2 |
| 0x03 | Stufe 3 |
| 0x04 | Stufe 4 |
| 0x05 | Stufe 5 |
| 0x06 | Stufe 6 |
| 0xFF | nicht aktiv |

<a id="table-tab-emf-position"></a>
### TAB_EMF_POSITION

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Angelegt |
| 0x01 | beim Schließen |
| 0x02 | Geschlossen |
| 0x03 | Geöffnet |
| 0x04 | beim Öffnen |
| 0x05 | Initialisierung |
| 0x06 | unbekannt / fehlerhaft |
| 0x07 | Montageposition |
| 0x08 | beim Anfahren Montageposition |
| 0xFF | nicht definiert |

<a id="table-tab-emf-taster"></a>
### TAB_EMF_TASTER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | neutral |
| 0x01 | gezogen |
| 0x02 | gedrueckt |
| 0x03 | Fehler |
| 0xFF | undefinierter Zustand |

<a id="table-tab-emf-verfahren"></a>
### TAB_EMF_VERFAHREN

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lösen |
| 1 | Feststellen |
| 2 | Montage |
| 3 | Anlegen |
| 4 | OpenBrakeRearLeft |
| 5 | OpenBrakeRearRight |
| 6 | OpenBrakeBoth |
| 7 | CloseBrakeRearLeft |
| 8 | CloseBrakeRearRight |
| 9 | CloseBrakeBoth |
| 10 | TouchBrakeRearLeft |
| 11 | TouchBrakeRearRight |
| 12 | TouchBrakeBoth |
| 13 | AssemblyCheck |

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

<a id="table-tab-epb-ereignis"></a>
### TAB_EPB_EREIGNIS

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Idle |
| 0x01 | Aktuatorbremsung |
| 0x02 | Diagnose Festellen |
| 0x03 | Diagnose Lösen |
| 0x04 | Diagnose Touch-Brake |
| 0x05 | HTR Nachspannen |
| 0x06 | RAR Nachspannen |
| 0x07 | Taster Feststellen |
| 0x08 | Taster Lösen |
| 0x09 | ADR Lösen |
| 0x10 | Engine Stall Feststellen |
| 0x11 | Auto Apply |
| 0x12 | Dienste Nachricht Feststellen |
| 0x13 | Fahrerassistenz Feststellen |
| 0x14 | Fahrerassistenz Lösen |
| 0x15 | ACC, Auto-H Feststellen |
| 0x16 | ACC, Auto-H Release |
| 0x17 | Bremsbelagverschleiß |
| 0x18 | Getriebeknallunterstützung Feststellen |
| 0x19 | Getriebeknallunterstützung Lösen |
| 0xFF | Wert ungültig |

<a id="table-tab-erfs-akt-verbaut"></a>
### TAB_ERFS_AKT_VERBAUT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nein |
| 0x01 | Ja |
| 0xFF | Ungültig |

<a id="table-tab-erfs-geschw-idx"></a>
### TAB_ERFS_GESCHW_IDX

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | L |
| 0x01 | M |
| 0x02 | N |
| 0x03 | P |
| 0x04 | Q |
| 0x05 | R |
| 0x06 | S |
| 0x07 | T |
| 0x08 | U |
| 0x09 | H |
| 0x0A | V |
| 0x0B | VR |
| 0x0C | W |
| 0x0D | ZR |
| 0x0E | Y |
| 0xFF | Ungültig |

<a id="table-tab-erfs-karkasse"></a>
### TAB_ERFS_KARKASSE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Normal Last |
| 0x01 | Extra Last |
| 0xFF | Ungültig |

<a id="table-tab-erfs-rsc"></a>
### TAB_ERFS_RSC

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RSC |
| 0x01 | Standard |
| 0x02 | PAX |
| 0x03 | Seal |
| 0xFF | Ungültig |

<a id="table-tab-erfs-saison"></a>
### TAB_ERFS_SAISON

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sommer |
| 0x01 | Winter |
| 0x02 | Ganzjahres |
| 0xFF | Ungültig |

<a id="table-tab-erfs-werksauslieferung"></a>
### TAB_ERFS_WERKSAUSLIEFERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nein |
| 0x01 | Ja |
| 0xFF | Ungültig |

<a id="table-tab-fdr-funktion"></a>
### TAB_FDR_FUNKTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verfügbar |
| 1 | verfügbar |
| 3 | verfügbar Schlupf aufgeweitet |
| 0xFF | ungültig |

<a id="table-tab-hdc-funktion"></a>
### TAB_HDC_FUNKTION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verfügbar |
| 1 | verfügbar |
| 0xFF | ungültig |

<a id="table-tab-kalibrierung"></a>
### TAB_KALIBRIERUNG

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RDC unterbrochen mit Fehler |
| 0x01 | RDC Reset Erfolgreich abgeschlossen |
| 0x02 | eRFS - Auswahl über ABK |
| 0x03 | eRFS - Auswahl über Diagnose |
| 0x04 | Steuegerät noch nicht kalibriert |
| 0x05 | Automatische Befüllerkennung RE0 |
| 0x06 | Automatische Befüllerkennung RE1 |
| 0x07 | Automatische Befüllerkennung RE2 |
| 0x08 | Automatische Befüllerkennung RE3 |
| 0x09 | NVM beschädigt |
| 0x0A | RID - Erkennung ohne Fortschrittsanzeige |
| 0x0B | RID - Erkennung mit Fortschrittsanzeige |
| 0x0C | Saisonale Anpassung |
| 0x81 | RDC Reset abgeschlossen - RE Positionen vermutet |
| 0x82 | eRFS - Auswahl über ABK - RE Positionen vermutet |
| 0x83 | eRFS - Auswahl über Diagnose - RE Positionen vermutet |
| 0x84 | Steuegerät noch nicht kalibriert - RE Positionen vermutet |
| 0x85 | Automatische Befüllerkennung RE0 - RE Positionen vermutet |
| 0x86 | Automatische Befüllerkennung RE1 - RE Positionen vermutet |
| 0x87 | Automatische Befüllerkennung RE2 - RE Positionen vermutet |
| 0x88 | Automatische Befüllerkennung RE3 - RE Positionen vermutet |
| 0x8A | RID - Erkennung ohne Fortschrittsanzeige - RE Positionen vermutet |
| 0x8B | RID - Erkennung with Fortschrittsanzeige - RE Positionen vermutet |
| 0x8C | Saisonale Anpassung - RE Positionen vermutet |
| 0xFE | Kalibrierung läuft |
| 0xFF | Ungültig |

<a id="table-tab-nacharbeitsentlueftung-phasen"></a>
### TAB_NACHARBEITSENTLUEFTUNG_PHASEN

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Evakuierung |
| 2 | Befuellung |
| 3 | Entlueftung VL |
| 4 | Entlueftung VR |
| 5 | Entlueftung HR |
| 6 | Entlueftung HL |
| 7 | Entlueftung Hauptbremszylinder |
| 8 | Entlueftung Simulator |

<a id="table-tab-obs-routine-ergebnis"></a>
### TAB_OBS_ROUTINE_ERGEBNIS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Aktiv |
| 2 | Erfolg |
| 4 | Fehler |
| 5 | Phasenende |
| 0xFF | Wert ungültig |

<a id="table-tab-obs-routine-fehlerinformationen"></a>
### TAB_OBS_ROUTINE_FEHLERINFORMATIONEN

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Fehler |
| 1 | Abbruch aufgrund HW-Problem oder Unterspannung |
| 2 | Gestoppt durch Tester |
| 3 | Bremspedal getreten |
| 4 | Timeout |
| 5 | Falscher Parameter |
| 6 | Systemdruck zu hoch |
| 7 | Falscher PSM Zustand |
| 8 | Predrive-Prüfung aktiv |
| 9 | Arbeitspunkt nicht erreicht (Nachfülldruck oder Druck am Rad nicht erreicht) |
| 10 | Radgeschwindigkeit zu gering für die Auswertung |
| 0xFF | Wert ungültig |

<a id="table-tab-obs-routine-status"></a>
### TAB_OBS_ROUTINE_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Aktiv |
| 2 | Beendet |
| 3 | Abgebrochen vor Beendigung |
| 0xFF | Wert ungültig |

<a id="table-tab-phase-evak-und-befuell"></a>
### TAB_PHASE_EVAK_UND_BEFUELL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Evakuierung |
| 1 | LeckageTest |
| 2 | BefuellungStabilisierung |
| 3 | Fuellstandsausgleich |

<a id="table-tab-plausi-druck"></a>
### TAB_PLAUSI_DRUCK

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fehlgeschlagen |
| 0x01 | Erfolgreich |
| 0x02 | Manuelle Kalibrierung fehlgeschlagen |
| 0x03 | Manuelle Kalibrierung erfolgreich |
| 0xFE | Läuft |
| 0xFF | Ungültig |

<a id="table-tab-position-rad"></a>
### TAB_POSITION_RAD

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine |
| 1 | vorn links |
| 2 | vorn rechts |
| 3 | hinten links |
| 4 | hinten rechts |

<a id="table-tab-produktionsstatus"></a>
### TAB_PRODUKTIONSSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Deaktiviert |
| 1 | Aktiviert |
| 2 | Aktiviert fuer Test |

<a id="table-tab-rdc-aktionsnr"></a>
### TAB_RDC_AKTIONSNR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RESET |
| 0x01 | SET |
| 0x02 | RECEPTION TEST NO SPEED |

<a id="table-tab-rdc-aktiv-inaktiv"></a>
### TAB_RDC_AKTIV_INAKTIV

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Inaktiv |
| 0x01 | Aktiv |
| 0x03 | Gateway oder Antenne Fehler |
| 0x04 | Weiche Warnung aktiv |
| 0xFF | Ungültig |

<a id="table-tab-rdc-bandmode-active"></a>
### TAB_RDC_BANDMODE_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bandmode nicht aktiv |
| 1 | Bandmode aktiv |
| 255 | Nicht definiert |

<a id="table-tab-rdc-bekannt-nicht-bekannt"></a>
### TAB_RDC_BEKANNT_NICHT_BEKANNT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht bekannt |
| 1 | Bekannt |
| 255 | Nicht definiert |

<a id="table-tab-rdc-cal-active"></a>
### TAB_RDC_CAL_ACTIVE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kalibrieranforderung inaktiv |
| 1 | Kalibrieranforderung aktiv |
| 2 | Kalibrierung abgewiesen |
| 255 | Nicht definiert |

<a id="table-tab-rdc-changed"></a>
### TAB_RDC_CHANGED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht geändert |
| 1 | Geändert |
| 255 | Ungültig |

<a id="table-tab-rdc-detected"></a>
### TAB_RDC_DETECTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht erkannt |
| 1 | Erkannt |
| 255 | Nicht definiert |

<a id="table-tab-rdc-dtc-active-status"></a>
### TAB_RDC_DTC_ACTIVE_STATUS

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bandmode Eigenradprüfung i.O. (in Kundenbetrieb: DTC nicht aktiv). |
| 0x01 | Bandmode Eigenradprüfung - Sensor Defekt entdeckt. (in Kundenbetrieb: DTC aktiv). |
| 0x10 | Bandmode: Sensoren VL nicht empfangen. |
| 0x20 | Bandmode: Sensoren VR nicht empfangen. |
| 0x30 | Bandmode: Sensoren VR, VL nicht empfangen. |
| 0x40 | Bandmode: Sensoren HR nicht empfangen. |
| 0x50 | Bandmode: Sensoren HR, VL nicht empfangen. |
| 0x60 | Bandmode: Sensoren HR, VR nicht empfangen. |
| 0x70 | Bandmode: Sensoren HR, VR, VL nicht empfangen. |
| 0x80 | Bandmode: Sensoren HL nicht empfangen. |
| 0x90 | Bandmode: Sensoren HL, VL nicht empfangen. |
| 0xA0 | Bandmode: Sensoren HL, VR nicht empfangen. |
| 0xB0 | Bandmode: Sensoren HL, VR, VL nicht empfangen. |
| 0xC0 | Bandmode: Sensoren HL, HR nicht empfangen. |
| 0xD0 | Bandmode: Sensoren HL, HR, VL nicht empfangen. |
| 0xE0 | Bandmode: Sensoren HL, HR, VR nicht empfangen. |
| 0xF0 | Bandmode: Sensoren HL, HR, VR, VL nicht empfangen (in Kundenbetrieb: DTC nicht aktiv). |
| 0x11 | Bandmode: Sensoren VL nicht empfangen. - Sensor Defekt entdeckt |
| 0x21 | Bandmode: Sensoren VR nicht empfangen. - Sensor Defekt entdeckt |
| 0x31 | Bandmode: Sensoren VR, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0x41 | Bandmode: Sensoren HR nicht empfangen. - Sensor Defekt entdeckt |
| 0x51 | Bandmode: Sensoren HR, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0x61 | Bandmode: Sensoren HR, VR nicht empfangen. - Sensor Defekt entdeckt |
| 0x71 | Bandmode: Sensoren HR, VR, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0x81 | Bandmode: Sensoren HL nicht empfangen. - Sensor Defekt entdeckt |
| 0x91 | Bandmode: Sensoren HL, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0xA1 | Bandmode: Sensoren HL, VR nicht empfangen. - Sensor Defekt entdeckt |
| 0xB1 | Bandmode: Sensoren HL, VR, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0xC1 | Bandmode: Sensoren HL, HR nicht empfangen. - Sensor Defekt entdeckt |
| 0xD1 | Bandmode: Sensoren HL, HR, VL nicht empfangen. - Sensor Defekt entdeckt |
| 0xE1 | Bandmode: Sensoren HL, HR, VR nicht empfangen. - Sensor Defekt entdeckt |
| 0xF1 | Bandmode: Sensoren HL, HR, VR, VL nicht empfangen (in Kundenbetrieb: DTC nicht aktiv). - Sensor Defekt entdeckt |
| 0xFF | Nicht definiert |

<a id="table-tab-rdc-interne-status"></a>
### TAB_RDC_INTERNE_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sensoren nicht angelernt und nicht lokalisiert |
| 0x01 | Sensoren angelernt |
| 0x03 | Sensoren angelernt und lokalisiert |
| 0xFF | Ungültig |

<a id="table-tab-rdc-int-fehler"></a>
### TAB_RDC_INT_FEHLER

Dimensions: 25 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Radelektronik 0 mute |
| 1 | Radelektronik 1 mute |
| 2 | Radelektronik 2 mute |
| 3 | Radelektronik 3 mute |
| 4 | Radelektronik Ausfall positionslos |
| 5 | Radelektronik 0 defekt |
| 6 | Radelektronik 1 defekt |
| 7 | Radelektronik 2 defekt |
| 8 | Radelektronik 3 defekt |
| 9 | RDCi Bandmode aktiv |
| 10 | Eigenrad Einlernfehler |
| 11 | Gateway / Antenne Fehler |
| 12 | Eingangssignal fehlt |
| 13 | Eingangssignal ungültig |
| 14 | Eingangssignal Alive Fehler |
| 15 | Eingangssignal CRC Fehler |
| 16 | HF Überdeckung |
| 17 | Geschwindigkeitssignal Fehler |
| 18 | Radelektronik Defekt positionslos |
| 128 | Geschütztes RAM Bereich Fehler |
| 129 | EEPROM Fehler beim Initialisierung |
| 130 | EEPROM Fehler beim Laufzeit |
| 131 | Betriebssystem Task Fehler |
| 132 | SW Watchdog Fehler |
| 255 | Ungültig |

<a id="table-tab-rdc-on-off"></a>
### TAB_RDC_ON_OFF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Aus |
| 1 | Ein |
| 9 | Nicht bedient |
| 255 | Nicht definiert |

<a id="table-tab-rdc-rad-position-nr"></a>
### TAB_RDC_RAD_POSITION_NR

Dimensions: 71 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | vorn links |
| 0x01 | vorn rechts |
| 0x02 | hinten links |
| 0x03 | hinten rechts |
| 0x05 | unbekannt 1 |
| 0x04 | Reserverad (nur RDC Gen2) |
| 0x06 | unbekannt 2 |
| 0x07 | unbekannt 3 |
| 0x08 | unbekannt 4 |
| 0x09 | unbekannt 5 (nur RDC Gen2) |
| 0x10 | Reifen 1 vorn links |
| 0x11 | Reifen 1 vorn rechts |
| 0x12 | Reifen 1 hinten links |
| 0x13 | Reifen 1 hinten rechts |
| 0x15 | Reifen 1 unbekannt |
| 0x20 | Reifen 2 vorn links |
| 0x21 | Reifen 2 vorn rechts |
| 0x22 | Reifen 2 hinten links |
| 0x23 | Reifen 2 hinten rechts |
| 0x25 | Reifen 2 unbekannt |
| 0x30 | Reifen 3 vorn links |
| 0x31 | Reifen 3 vorn rechts |
| 0x32 | Reifen 3 hinten links |
| 0x33 | Reifen 3 hinten rechts |
| 0x35 | Reifen 3 unbekannt |
| 0x40 | Reifen 4 vorn links |
| 0x41 | Reifen 4 vorn rechts |
| 0x42 | Reifen 4 hinten links |
| 0x43 | Reifen 4 hinten rechts |
| 0x45 | Reifen 4 unbekannt |
| 0x50 | Reifen 5 vorn links |
| 0x51 | Reifen 5 vorn rechts |
| 0x52 | Reifen 5 hinten links |
| 0x53 | Reifen 5 hinten rechts |
| 0x55 | Reifen 5 unbekannt |
| 0x60 | Reifen 6 vorn links |
| 0x61 | Reifen 6 vorn rechts |
| 0x62 | Reifen 6 hinten links |
| 0x63 | Reifen 6 hinten rechts |
| 0x65 | Reifen 6 unbekannt |
| 0x70 | Reifen 7 vorn links |
| 0x71 | Reifen 7 vorn rechts |
| 0x72 | Reifen 7 hinten links |
| 0x73 | Reifen 7 hinten rechts |
| 0x75 | Reifen 7 unbekannt |
| 0x80 | Reifen 8 vorn links |
| 0x81 | Reifen 8 vorn rechts |
| 0x82 | Reifen 8 hinten links |
| 0x83 | Reifen 8 hinten rechts |
| 0x85 | Reifen 8 unbekannt |
| 0x90 | Reifen 9 vorn links |
| 0x91 | Reifen 9 vorn rechts |
| 0x92 | Reifen 9 hinten links |
| 0x93 | Reifen 9 hinten rechts |
| 0x95 | Reifen 9 unbekannt |
| 0xA0 | Reifen 10 vorn links |
| 0xA1 | Reifen 10 vorn rechts |
| 0xA2 | Reifen 10 hinten links |
| 0xA3 | Reifen 10 hinten rechts |
| 0xA5 | Reifen 10 unbekannt |
| 0xB0 | Reifen 11 vorn links |
| 0xB1 | Reifen 11 vorn rechts |
| 0xB2 | Reifen 11 hinten links |
| 0xB3 | Reifen 11 hinten rechts |
| 0xB5 | Reifen 11 unbekannt |
| 0xC0 | Reifen 12 vorn links |
| 0xC1 | Reifen 12 vorn rechts |
| 0xC2 | Reifen 12 hinten links |
| 0xC3 | Reifen 12 hinten rechts |
| 0xC5 | Reifen 12 unbekannt |
| 0xFF | Ungültig |

<a id="table-tab-rdc-re-hersteller"></a>
### TAB_RDC_RE_HERSTELLER

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reserviert |
| 0x01 | Frei |
| 0x02 | Huf |
| 0x03 | Continental |
| 0x04 | Frei |
| 0x05 | Schrader |
| 0x06 | Frei |
| 0x07 | Frei |
| 0x08 | Frei |
| 0x09 | Frei |
| 0x0A | Frei |
| 0x0B | Frei |
| 0x0C | Frei |
| 0x0D | Frei |
| 0x0E | Frei |
| 0x0F | Andere |
| 0x12 | Huf - RE Positionen vermutet |
| 0x13 | Continental - RE Positionen vermutet |
| 0x15 | Schrader - RE Positionen vermutet |
| 0x1F | Andere - RE Positionen vermutet |
| 0xFF | Ungueltig |

<a id="table-tab-rdc-re-sendemode-ak"></a>
### TAB_RDC_RE_SENDEMODE_AK

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stationär |
| 0x01 | Stationär TFA |
| 0x02 | Einlernen Fahren |
| 0x03 | Normal Fahren |
| 0x04 | Einlernen Interim |
| 0x05 | Normal Interim |
| 0x06 | Delta P |
| 0x07 | OFF Modus |
| 0x08 | Über LF angefordert |
| 0xFF | Ungültig |

<a id="table-tab-rdc-re-status"></a>
### TAB_RDC_RE_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Radelektronik i.O. |
| 0x01 | Radelektronik mute |
| 0x02 | Radelektronik defekt |
| 0x03 | Radelektronik Daten noch nicht empfangen |
| 0xFF | Ungültig |

<a id="table-tab-rdc-started"></a>
### TAB_RDC_STARTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht gestartet |
| 1 | Gestartet |
| 255 | Nicht definiert |

<a id="table-tab-rdc-steuerfunktionen"></a>
### TAB_RDC_STEUERFUNKTIONEN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Bandmode |
| 4 | Test Eigenrad in Fahrt |
| 8 | Calibrierung |
| 255 | Ungültig |

<a id="table-tab-rdc-timeout"></a>
### TAB_RDC_TIMEOUT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Timeout |
| 1 | Timeout |
| 255 | Nicht definiert |

<a id="table-tab-rdc-vehicle-running"></a>
### TAB_RDC_VEHICLE_RUNNING

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug fährt |
| 255 | Nicht definiert |

<a id="table-tab-rdc-zustand"></a>
### TAB_RDC_ZUSTAND

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Inaktiv |
| 0x01 | Aktiv |
| 0x03 | Gateway oder Antenne Fehler |
| 0x04 | Weiche Warnung aktiv |
| 0xFF | Nicht definiert |

<a id="table-tab-re-hersteller"></a>
### TAB_RE_HERSTELLER

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht bedient |
| 0x01 | Autonet |
| 0x02 | HUF |
| 0x03 | Continental |
| 0x04 | TRW |
| 0x05 | Schrader |
| 0x0F | Hersteller unbekannt |
| 0xFF | Ungültig |

<a id="table-tab-re-telegrammtyp"></a>
### TAB_RE_TELEGRAMMTYP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AK35 default |
| 0x82 | HUF G3  |
| 0x88 | AK35 HUF lang |
| 0xA0 | AK35 HUF mittel |
| 0xC1 | AK35 HUF kurz |
| 0xFF | Ungültig |

<a id="table-tab-schalterstatus"></a>
### TAB_SCHALTERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Idle |
| 0x01 | Release |
| 0x02 | Clamp |
| 0x03 | Error |
| 0xFF | undefinierter Zustand |

<a id="table-tab-start-tts-cal-status"></a>
### TAB_START_TTS_CAL_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Kalibrierung aktiv |
| 0x03 | Kalibrierung ist bereits erfolgreich abgeschlossen (nur eine erfolgreiche Kalibrierung im aktuellen Zündungslauf möglich) |
| 0x04 | Kalibrierung gestartet jedoch aufgrund von Fehler unmittelbar abgebrochen (details abrufbar über Routine Status) |

<a id="table-tab-state-tts-cal-status"></a>
### TAB_STATE_TTS_CAL_STATUS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kalibrierung erfolgreich |
| 0x01 | Kalibrierung aktiv |
| 0x02 | Kalibrierung abgebrochen - TTS Fehler |
| 0x03 | Kalibrierung abgebrochen - Pedal bewegt |
| 0x04 | Kalibrierung abgebrochen - Position ausserhalb Grenze |
| 0x05 | Kalibrierung abgebrochen - Daten konnten nicht ins EEPROM geschrieben werden |
| 0x06 | TTS Komponente meldet unbekannten Zustand |
| 0x07 | Kalibrier Ereignis wurde zum Multi-Kern gesendet, es werden noch Daten empfangen |
| 0x08 | Kalibrierung wurde abgebrochen weil das Fahrzeug bewegt wurde |

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

<a id="table-tab-status-routine"></a>
### TAB_STATUS_ROUTINE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Unbekannt |
| 0x01 | Aktiv |
| 0x02 | Erfolg |
| 0x03 | Abbruch |
| 0x04 | Fehler |
| 0x05 | Phasenende |
| 0xFF | Ungültig |

<a id="table-tab-status-spannungseinbruch"></a>
### TAB_STATUS_SPANNUNGSEINBRUCH

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Spannungseinbruch |
| 1 | Startspannungseinbruch bis maximal Spannungsschwelle 1 |
| 2 | Startspannungseinbruch bis maximal Spannungsschwelle 2 |
| 13 | Funktionsschnittstelle_ist_nicht_verfuegbar |
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
| 13 | Funktionsschnittstelle_ist_nicht_verfuegbar |
| 14 | Reserviert |
| 15 | Signal_unbefuellt |
| 0xFF | Wert ungültig |

<a id="table-tab-vertauschungstest-rad"></a>
### TAB_VERTAUSCHUNGSTEST_RAD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Vorne links |
| 1 | Vorne rechts |
| 2 | Hinten links |
| 3 | Hinten rechts |

<a id="table-tab-zeitrahmen-auswahl"></a>
### TAB_ZEITRAHMEN_AUSWAHL

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | System Laufzeit |
| 1 | Zeitrahmen 2.5 ms |
| 2 | Zeitrahmen 5 ms |
| 3 | Zeitrahmen 10 ms |
| 4 | Zeitrahmen 20 ms |
| 5 | Zeitrahmen 100 ms |

<a id="table-tab-0x2951"></a>
### TAB_0X2951

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x0007 |

<a id="table-tab-0x502f"></a>
### TAB_0X502F

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0001 | 0x0002 | 0x0003 | 0x0004 | 0x0005 | 0x0006 |
