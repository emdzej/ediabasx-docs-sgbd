# dsc_i1.prg

- Jobs: [55](#jobs)
- Tables: [216](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitätscontrolle |
| ORIGIN | BMW EF-513 Hoedl |
| REVISION | 13.002 |
| AUTHOR | BMW EF-601 Rudolph, Berner&Mattner EF-513 Miess, ESG EF-613 Mac |
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
- [CBS_RESET_KOR](#job-cbs-reset-kor) - CBS Daten Zuruecksetzen (fuer CBS-Version 6) Fahrzeug muss in einem der folgenden Zustaende sein:) - Pruefen_Analyse_Diagnose - Fahrbereitschaft_herstellen - Fahren - Fahrbereitschaft_beenden UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)
- [STEUERN_HYDRO_SPUELEN](#job-steuern-hydro-spuelen) - DSC Hydraulikblock spuelen
- [_STEUERN_PUMPE_PWM](#job-steuern-pumpe-pwm) - Variables Ansteuern des Pumpenmotors Als Argument wird uebergeben: PWM-Tastverhaeltnis in Prozent UDS: $2F InputOutputControlByIdentifier
- [_PIA_DATEN_LESEN](#job-pia-daten-lesen) - Auslesen der PIA-Daten aus EEPROM Steuergeraete-Speicher UDS: $23 ReadMemoryByAddress Modus   : Default
- [FLM_LESEN_BMW](#job-flm-lesen-bmw) - Auslesen der FLM Daten und der Debug Codierung UDS: $22 $D6D6 ReadDataByID FLM_DATEN UDS: $22 $3000 ReadDataByID Codierdaten Allgemein Modus   : Default
- [_EEPROM_LESEN](#job-eeprom-lesen)
- [_BBV_LESEN_GEN2](#job-bbv-lesen-gen2)
- [_STATUS_VIN](#job-status-vin) - HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F190 Sub-Parameter VIN Modus: Default
- [_HCU_TYP_BESTIMMEN](#job-hcu-typ-bestimmen) - Bestimmung des HCU-Typs im EEPROM UDS: $23 ReadMemoryByAddress Modus   : Default
- [_DSC_SPEICHER_LESEN](#job-dsc-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse und Anzahl der Datenbytes UDS: $23 ReadMemoryByAddress Modus   : Default
- [_FS_LOESCHEN_FUNKTIONAL](#job-fs-loeschen-funktional) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default

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

<a id="job-cbs-reset-kor"></a>
### CBS_RESET_KOR

CBS Daten Zuruecksetzen (fuer CBS-Version 6) Fahrzeug muss in einem der folgenden Zustaende sein:) - Pruefen_Analyse_Diagnose - Fahrbereitschaft_herstellen - Fahren - Fahrbereitschaft_beenden UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)

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
| CHOV_CBS_CBR_VIEW | int | Sichtbarkeit CBx Umfang) Defaultwert 0, Service nicht anzeigen: 0x00 |
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

<a id="job-steuern-hydro-spuelen"></a>
### STEUERN_HYDRO_SPUELEN

DSC Hydraulikblock spuelen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" when command succeded |
| _REQUEST | binary | CustomerDiagnosis request for STEUERN_SOLLDRUCK_VORGEBEN job |
| _RESPONSE | binary | CustomerDiagnosis response for STEUERN_SOLLDRUCK_VORGEBEN job |

<a id="job-steuern-pumpe-pwm"></a>
### _STEUERN_PUMPE_PWM

Variables Ansteuern des Pumpenmotors Als Argument wird uebergeben: PWM-Tastverhaeltnis in Prozent UDS: $2F InputOutputControlByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| _TASTVERHAELTNIS | unsigned char | 0 - 100 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Anfrage an das SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pia-daten-lesen"></a>
### _PIA_DATEN_LESEN

Auslesen der PIA-Daten aus EEPROM Steuergeraete-Speicher UDS: $23 ReadMemoryByAddress Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _PROFIL | string | Profilname |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Anfrage an das SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-flm-lesen-bmw"></a>
### FLM_LESEN_BMW

Auslesen der FLM Daten und der Debug Codierung UDS: $22 $D6D6 ReadDataByID FLM_DATEN UDS: $22 $3000 ReadDataByID Codierdaten Allgemein Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLM_DATEN | binary | ausgelesene Daten |
| FLM_CODIER_DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-eeprom-lesen"></a>
### _EEPROM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_DATEN | binary | ausgelesene EEPROM-Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-bbv-lesen-gen2"></a>
### _BBV_LESEN_GEN2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BELAG_DICKE_VORN_ROH | binary | ausgelesene Daten |
| BELAG_DICKE_VORN_WERT | unsigned long | ausgelesene Daten |
| BELAG_DICKE_VORN_EINHEIT | string | ausgelesene Daten |
| BELAG_DICKE_HINTEN_ROH | binary | ausgelesene Daten |
| BELAG_DICKE_HINTEN_WERT | unsigned long | ausgelesene Daten |
| BELAG_DICKE_HINTEN_EINHEIT | string | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-vin"></a>
### _STATUS_VIN

HW_NR UDS  : $22   ReadDataByIdentifier UDS  : $F190 Sub-Parameter VIN Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VIN | long | HW-Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-hcu-typ-bestimmen"></a>
### _HCU_TYP_BESTIMMEN

Bestimmung des HCU-Typs im EEPROM UDS: $23 ReadMemoryByAddress Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _HCU_TYP | string | Request-Auswertung |
| _REQUEST | binary | Hex-Anfrage an das SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-dsc-speicher-lesen"></a>
### _DSC_SPEICHER_LESEN

Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse und Anzahl der Datenbytes UDS: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Anfrage an das SG |
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
- [ARG_0XA061_R](#table-arg-0xa061-r) (2 × 14)
- [ARG_0XA064_R](#table-arg-0xa064-r) (13 × 14)
- [ARG_0XA065_R](#table-arg-0xa065-r) (1 × 14)
- [ARG_0XA066_R](#table-arg-0xa066-r) (2 × 14)
- [ARG_0XA067_R](#table-arg-0xa067-r) (1 × 14)
- [ARG_0XA06D_R](#table-arg-0xa06d-r) (2 × 14)
- [ARG_0XA08F_R](#table-arg-0xa08f-r) (1 × 14)
- [ARG_0XA193_R](#table-arg-0xa193-r) (1 × 14)
- [ARG_0XA803_R](#table-arg-0xa803-r) (1 × 14)
- [ARG_0XD80F_D](#table-arg-0xd80f-d) (1 × 12)
- [ARG_0XDB98_D](#table-arg-0xdb98-d) (1 × 12)
- [ARG_0XDBE1_D](#table-arg-0xdbe1-d) (1 × 12)
- [ARG_0XDBE2_D](#table-arg-0xdbe2-d) (1 × 12)
- [ARG_0XDBE8_D](#table-arg-0xdbe8-d) (1 × 12)
- [ARG_0XDBE9_D](#table-arg-0xdbe9-d) (12 × 12)
- [ARG_0XDC89_D](#table-arg-0xdc89-d) (2 × 12)
- [ARG_0XDC8A_D](#table-arg-0xdc8a-d) (2 × 12)
- [ARG_0XDC8B_D](#table-arg-0xdc8b-d) (2 × 12)
- [ARG_0XDC8C_D](#table-arg-0xdc8c-d) (2 × 12)
- [ARG_0XDC8D_D](#table-arg-0xdc8d-d) (2 × 12)
- [ARG_0XDCC0_D](#table-arg-0xdcc0-d) (2 × 12)
- [ARG_0XDCC6_D](#table-arg-0xdcc6-d) (2 × 12)
- [ARG_0XDCEE_D](#table-arg-0xdcee-d) (2 × 12)
- [ARG_0XDD0C_D](#table-arg-0xdd0c-d) (1 × 12)
- [BF_HA_FLAG_BVA](#table-bf-ha-flag-bva) (1 × 10)
- [BF_HA_RESET_VERHINDERER_1](#table-bf-ha-reset-verhinderer-1) (3 × 10)
- [BF_HA_RESET_VERHINDERER_2](#table-bf-ha-reset-verhinderer-2) (7 × 10)
- [BF_VA_FLAG_BVA](#table-bf-va-flag-bva) (1 × 10)
- [BF_VA_RESET_VERHINDERER_1](#table-bf-va-reset-verhinderer-1) (3 × 10)
- [BF_VA_RESET_VERHINDERER_2](#table-bf-va-reset-verhinderer-2) (7 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [EINZELFEHLER_BIT](#table-einzelfehler-bit) (2 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (479 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (71 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (134 × 4)
- [IPB_LED_ZUSTAND](#table-ipb-led-zustand) (2 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (122 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0X1061_R](#table-res-0x1061-r) (1 × 13)
- [RES_0XA051_R](#table-res-0xa051-r) (1 × 13)
- [RES_0XA052_R](#table-res-0xa052-r) (1 × 13)
- [RES_0XA053_R](#table-res-0xa053-r) (1 × 13)
- [RES_0XA05B_R](#table-res-0xa05b-r) (2 × 13)
- [RES_0XA061_R](#table-res-0xa061-r) (1 × 13)
- [RES_0XA064_R](#table-res-0xa064-r) (1 × 13)
- [RES_0XA065_R](#table-res-0xa065-r) (9 × 13)
- [RES_0XA066_R](#table-res-0xa066-r) (4 × 13)
- [RES_0XA067_R](#table-res-0xa067-r) (2 × 13)
- [RES_0XA06D_R](#table-res-0xa06d-r) (1 × 13)
- [RES_0XA08F_R](#table-res-0xa08f-r) (4 × 13)
- [RES_0XA123_R](#table-res-0xa123-r) (1 × 13)
- [RES_0XA130_R](#table-res-0xa130-r) (1 × 13)
- [RES_0XA193_R](#table-res-0xa193-r) (1 × 13)
- [RES_0XA222_R](#table-res-0xa222-r) (4 × 13)
- [RES_0XA803_R](#table-res-0xa803-r) (1 × 13)
- [RES_0XAB5B_R](#table-res-0xab5b-r) (2 × 13)
- [RES_0XABA3_R](#table-res-0xaba3-r) (1 × 13)
- [RES_0XD09A_D](#table-res-0xd09a-d) (9 × 10)
- [RES_0XD0D2_D](#table-res-0xd0d2-d) (7 × 10)
- [RES_0XD272_D](#table-res-0xd272-d) (28 × 10)
- [RES_0XD6D6_D](#table-res-0xd6d6-d) (4 × 10)
- [RES_0XD804_D](#table-res-0xd804-d) (10 × 10)
- [RES_0XD805_D](#table-res-0xd805-d) (9 × 10)
- [RES_0XD808_D](#table-res-0xd808-d) (2 × 10)
- [RES_0XD80A_D](#table-res-0xd80a-d) (4 × 10)
- [RES_0XD80C_D](#table-res-0xd80c-d) (4 × 10)
- [RES_0XD80D_D](#table-res-0xd80d-d) (7 × 10)
- [RES_0XD80F_D](#table-res-0xd80f-d) (1 × 10)
- [RES_0XDBD9_D](#table-res-0xdbd9-d) (2 × 10)
- [RES_0XDBDA_D](#table-res-0xdbda-d) (2 × 10)
- [RES_0XDBDB_D](#table-res-0xdbdb-d) (2 × 10)
- [RES_0XDBDF_D](#table-res-0xdbdf-d) (2 × 10)
- [RES_0XDBE1_D](#table-res-0xdbe1-d) (1 × 10)
- [RES_0XDBE2_D](#table-res-0xdbe2-d) (1 × 10)
- [RES_0XDBE3_D](#table-res-0xdbe3-d) (10 × 10)
- [RES_0XDBE4_D](#table-res-0xdbe4-d) (14 × 10)
- [RES_0XDBE5_D](#table-res-0xdbe5-d) (6 × 10)
- [RES_0XDBE7_D](#table-res-0xdbe7-d) (4 × 10)
- [RES_0XDBE8_D](#table-res-0xdbe8-d) (1 × 10)
- [RES_0XDBE9_D](#table-res-0xdbe9-d) (12 × 10)
- [RES_0XDBF4_D](#table-res-0xdbf4-d) (2 × 10)
- [RES_0XDBF5_D](#table-res-0xdbf5-d) (4 × 10)
- [RES_0XDBF6_D](#table-res-0xdbf6-d) (2 × 10)
- [RES_0XDC13_D](#table-res-0xdc13-d) (8 × 10)
- [RES_0XDC14_D](#table-res-0xdc14-d) (25 × 10)
- [RES_0XDC15_D](#table-res-0xdc15-d) (24 × 10)
- [RES_0XDC3A_D](#table-res-0xdc3a-d) (10 × 10)
- [RES_0XDC42_D](#table-res-0xdc42-d) (30 × 10)
- [RES_0XDC6C_D](#table-res-0xdc6c-d) (3 × 10)
- [RES_0XDC6D_D](#table-res-0xdc6d-d) (3 × 10)
- [RES_0XDC6E_D](#table-res-0xdc6e-d) (3 × 10)
- [RES_0XDC6F_D](#table-res-0xdc6f-d) (3 × 10)
- [RES_0XDC70_D](#table-res-0xdc70-d) (3 × 10)
- [RES_0XDC89_D](#table-res-0xdc89-d) (42 × 10)
- [RES_0XDC8A_D](#table-res-0xdc8a-d) (2 × 10)
- [RES_0XDC8B_D](#table-res-0xdc8b-d) (6 × 10)
- [RES_0XDC8C_D](#table-res-0xdc8c-d) (1 × 10)
- [RES_0XDC8D_D](#table-res-0xdc8d-d) (1 × 10)
- [RES_0XDC8F_D](#table-res-0xdc8f-d) (2 × 10)
- [RES_0XDC90_D](#table-res-0xdc90-d) (6 × 10)
- [RES_0XDC91_D](#table-res-0xdc91-d) (42 × 10)
- [RES_0XDC95_D](#table-res-0xdc95-d) (24 × 10)
- [RES_0XDC96_D](#table-res-0xdc96-d) (18 × 10)
- [RES_0XDC97_D](#table-res-0xdc97-d) (63 × 10)
- [RES_0XDC98_D](#table-res-0xdc98-d) (20 × 10)
- [RES_0XDC99_D](#table-res-0xdc99-d) (20 × 10)
- [RES_0XDC9A_D](#table-res-0xdc9a-d) (20 × 10)
- [RES_0XDC9B_D](#table-res-0xdc9b-d) (20 × 10)
- [RES_0XDC9C_D](#table-res-0xdc9c-d) (31 × 10)
- [RES_0XDC9D_D](#table-res-0xdc9d-d) (31 × 10)
- [RES_0XDC9E_D](#table-res-0xdc9e-d) (31 × 10)
- [RES_0XDC9F_D](#table-res-0xdc9f-d) (31 × 10)
- [RES_0XDCD9_D](#table-res-0xdcd9-d) (32 × 10)
- [RES_0XDCF1_D](#table-res-0xdcf1-d) (31 × 10)
- [RES_0XDCF2_D](#table-res-0xdcf2-d) (31 × 10)
- [RES_0XDCF3_D](#table-res-0xdcf3-d) (31 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (111 × 16)
- [TAB_0X2840](#table-tab-0x2840) (1 × 21)
- [TAB_0X2858](#table-tab-0x2858) (1 × 9)
- [TAB_0X2859](#table-tab-0x2859) (1 × 9)
- [TAB_ABS_FUNKTION](#table-tab-abs-funktion) (4 × 2)
- [TAB_ADAPTIVDATEN_AAEPS](#table-tab-adaptivdaten-aaeps) (3 × 2)
- [TAB_ADAPTIVDATEN_EV](#table-tab-adaptivdaten-ev) (7 × 2)
- [TAB_ADAPTIVDATEN_LERNEN](#table-tab-adaptivdaten-lernen) (3 × 2)
- [TAB_ADAPTIVDATEN_RESET](#table-tab-adaptivdaten-reset) (3 × 2)
- [TAB_ADAPTIVDATEN_SBS](#table-tab-adaptivdaten-sbs) (45 × 2)
- [TAB_ADAPTIVDATEN_TSC](#table-tab-adaptivdaten-tsc) (2 × 2)
- [TAB_ADAPTIVDATEN_WERK](#table-tab-adaptivdaten-werk) (3 × 2)
- [TAB_ADAPTIVDATEN_ZFM](#table-tab-adaptivdaten-zfm) (2 × 2)
- [TAB_ASC_FUNKTION](#table-tab-asc-funktion) (6 × 2)
- [TAB_AX_AY_ABGLEICH](#table-tab-ax-ay-abgleich) (3 × 2)
- [TAB_BBV_SENSOR](#table-tab-bbv-sensor) (4 × 2)
- [TAB_BPWS_DETAIL_INITIALISIERUNG](#table-tab-bpws-detail-initialisierung) (16 × 2)
- [TAB_BREMSENSTATUS_LINKS](#table-tab-bremsenstatus-links) (10 × 2)
- [TAB_BREMSENSTATUS_RECHTS](#table-tab-bremsenstatus-rechts) (10 × 2)
- [TAB_DREHRICHTUNG](#table-tab-drehrichtung) (4 × 2)
- [TAB_DSC_PHASE_ENTLUEFTUNG](#table-tab-dsc-phase-entlueftung) (10 × 2)
- [TAB_DSC_PHASE_VAKUUMBEFUELLUNG](#table-tab-dsc-phase-vakuumbefuellung) (4 × 2)
- [TAB_DSC_PHASE_VENTILE_KALIBRIERUNG](#table-tab-dsc-phase-ventile-kalibrierung) (5 × 2)
- [TAB_DSC_VENTILE](#table-tab-dsc-ventile) (14 × 2)
- [TAB_EMF_HU_MODE](#table-tab-emf-hu-mode) (6 × 2)
- [TAB_EMF_POSITION](#table-tab-emf-position) (10 × 2)
- [TAB_EMF_TASTER](#table-tab-emf-taster) (5 × 2)
- [TAB_EMF_VERFAHREN](#table-tab-emf-verfahren) (15 × 2)
- [TAB_ENTLASTUNG_GENERATOR](#table-tab-entlastung-generator) (16 × 2)
- [TAB_EPB_ACTION](#table-tab-epb-action) (2 × 2)
- [TAB_ERRID_FASCBAS](#table-tab-errid-fascbas) (16 × 2)
- [TAB_ERRID_FASCEBC](#table-tab-errid-fascebc) (26 × 2)
- [TAB_ERRID_FASCFI](#table-tab-errid-fascfi) (256 × 2)
- [TAB_ERRID_FASCFO](#table-tab-errid-fascfo) (16 × 2)
- [TAB_ERRID_FASDSP](#table-tab-errid-fasdsp) (51 × 2)
- [TAB_ERRID_FASSCG](#table-tab-errid-fasscg) (16 × 2)
- [TAB_FAHRERLEBNIS_FILTER](#table-tab-fahrerlebnis-filter) (5 × 2)
- [TAB_FAHRERLEBNIS_MODUS](#table-tab-fahrerlebnis-modus) (10 × 2)
- [TAB_FDR_FUNKTION](#table-tab-fdr-funktion) (4 × 2)
- [TAB_HDC_FUNKTION](#table-tab-hdc-funktion) (3 × 2)
- [TAB_JA_NEIN](#table-tab-ja-nein) (2 × 2)
- [TAB_KALIBRIERUNG](#table-tab-kalibrierung) (3 × 2)
- [TAB_LETZTESBREMSENEVENT_LINKS](#table-tab-letztesbremsenevent-links) (11 × 2)
- [TAB_LETZTESBREMSENEVENT_RECHTS](#table-tab-letztesbremsenevent-rechts) (11 × 2)
- [TAB_MODE_OLD](#table-tab-mode-old) (2 × 2)
- [TAB_PLAUSI_DRUCK](#table-tab-plausi-druck) (3 × 2)
- [TAB_POSITION_RAD](#table-tab-position-rad) (5 × 2)
- [TAB_RDC_AKTIV_INAKTIV](#table-tab-rdc-aktiv-inaktiv) (6 × 2)
- [TAB_RDC_BANDMODE_ACTIVE](#table-tab-rdc-bandmode-active) (3 × 2)
- [TAB_RDC_BEKANNT_NICHT_BEKANNT](#table-tab-rdc-bekannt-nicht-bekannt) (3 × 2)
- [TAB_RDC_CAL_ACTIVE](#table-tab-rdc-cal-active) (4 × 2)
- [TAB_RDC_CHANGED](#table-tab-rdc-changed) (3 × 2)
- [TAB_RDC_CONFIRMED](#table-tab-rdc-confirmed) (3 × 2)
- [TAB_RDC_DETECTED](#table-tab-rdc-detected) (3 × 2)
- [TAB_RDC_DTC_ACTIVE](#table-tab-rdc-dtc-active) (3 × 2)
- [TAB_RDC_ON_OFF](#table-tab-rdc-on-off) (4 × 2)
- [TAB_RDC_RAD_DREHRICHTUNG](#table-tab-rdc-rad-drehrichtung) (5 × 2)
- [TAB_RDC_RAD_POSITION_NR](#table-tab-rdc-rad-position-nr) (10 × 2)
- [TAB_RDC_RAD_POSITION_NR_UINT](#table-tab-rdc-rad-position-nr-uint) (10 × 2)
- [TAB_RDC_STARTED](#table-tab-rdc-started) (3 × 2)
- [TAB_RDC_STEUERFUNKTIONEN](#table-tab-rdc-steuerfunktionen) (11 × 2)
- [TAB_RDC_TIMEOUT](#table-tab-rdc-timeout) (3 × 2)
- [TAB_RDC_VEHICLE_RUNNING](#table-tab-rdc-vehicle-running) (3 × 2)
- [TAB_RE_HERSTELLER](#table-tab-re-hersteller) (7 × 2)
- [TAB_RE_ROLLSWITCH](#table-tab-re-rollswitch) (3 × 2)
- [TAB_RE_SENDEMODE](#table-tab-re-sendemode) (10 × 2)
- [TAB_RE_TELEGRAMMTYP](#table-tab-re-telegrammtyp) (6 × 2)
- [TAB_ROLLENMODUS](#table-tab-rollenmodus) (3 × 2)
- [TAB_SBS_GUELTIGKEIT_UINT](#table-tab-sbs-gueltigkeit-uint) (9 × 2)
- [TAB_SCHALTERSTATUS](#table-tab-schalterstatus) (5 × 2)
- [TAB_SHUTDOWNLEVEL_OLD](#table-tab-shutdownlevel-old) (4 × 2)
- [TAB_STATUS_NM](#table-tab-status-nm) (7 × 2)
- [TAB_STATUS_ROLLENMODUS](#table-tab-status-rollenmodus) (6 × 2)
- [TAB_STATUS_ROUTINE](#table-tab-status-routine) (7 × 2)
- [TAB_VENTILE_KALIBRIERUNG_1](#table-tab-ventile-kalibrierung-1) (8 × 2)
- [TAB_VENTILE_KALIBRIERUNG_2](#table-tab-ventile-kalibrierung-2) (8 × 2)
- [TAB_VENTILE_KALIBRIERUNG_3](#table-tab-ventile-kalibrierung-3) (8 × 2)

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

<a id="table-arg-0xa061-r"></a>
### ARG_0XA061_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PHASE | + | - | 0-n | - | unsigned char | - | TAB_DSC_PHASE_ENTLUEFTUNG | - | - | - | - | - | Phase |
| WIEDERHOLUNG | + | - | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Anzahl Wiederholungen |

<a id="table-arg-0xa064-r"></a>
### ARG_0XA064_R

Dimensions: 13 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT_ROUTINE | + | - | ms | - | unsigned char | - | - | 1.0 | 10.0 | 0.0 | - | - | max. Ausführungsdauer |
| VENTIL_1 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | - | - | - | - | - | Ventil Auswahl |
| WERT_1 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |
| VENTIL_2 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | 1.0 | 1.0 | 0.0 | - | - | Ventil Auswahl |
| WERT_2 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |
| VENTIL_3 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | 1.0 | 1.0 | 0.0 | - | - | Ventil Auswahl |
| WERT_3 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |
| VENTIL_4 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | 1.0 | 1.0 | 0.0 | - | - | Ventil Auswahl |
| WERT_4 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |
| VENTIL_5 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | 1.0 | 1.0 | 0.0 | - | - | Ventil Auswahl |
| WERT_5 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |
| VENTIL_6 | + | - | 0-n | - | unsigned char | - | TAB_DSC_VENTILE | 1.0 | 1.0 | 0.0 | - | - | Ventil Auswahl |
| WERT_6 | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Ventil Ansteuerung |

<a id="table-arg-0xa065-r"></a>
### ARG_0XA065_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT_ROUTINE | + | - | s | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | - | - | max. Ausführungsdauer |

<a id="table-arg-0xa066-r"></a>
### ARG_0XA066_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT_TV_EIN | + | - | ms | - | unsigned char | - | - | 1.0 | 10.0 | 0.0 | - | - | Verzögerung Schliessen Trennventil |
| ZEIT_PUMPE_AUS | + | - | ms | - | unsigned char | - | - | 1.0 | 10.0 | 0.0 | - | - | Verzögerung Stop Pumpe (&gt; ZEIT_TV_EIN) |

<a id="table-arg-0xa067-r"></a>
### ARG_0XA067_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT | + | - | s | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | max. Ausführungsdauer |

<a id="table-arg-0xa06d-r"></a>
### ARG_0XA06D_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZEIT_ROUTINE | + | - | s | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | max. Ausführungsdauer |
| PHASE | + | - | 0-n | - | unsigned char | - | TAB_DSC_PHASE_VAKUUMBEFUELLUNG | 1.0 | 1.0 | 0.0 | - | - | Phase |

<a id="table-arg-0xa08f-r"></a>
### ARG_0XA08F_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PHASE | + | + | 0-n | - | unsigned char | - | TAB_DSC_PHASE_VENTILE_KALIBRIERUNG | 1.0 | 1.0 | 0.0 | - | - | Phase |

<a id="table-arg-0xa193-r"></a>
### ARG_0XA193_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EPB_ACTION | + | - | 0-n | high | unsigned long | - | TAB_EPB_ACTION | - | - | - | - | - | Aktion der Parkbremse |

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

<a id="table-arg-0xdb98-d"></a>
### ARG_0XDB98_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | signed char | - | TAB_ROLLENMODUS | - | - | - | - | - | Setzen / Rücksetzen Rollenmodus (2=Setzen Rollenmodus Innenraum; 1 = Setzen Werksrollenmodus; 0 =  Rücksetzen) |

<a id="table-arg-0xdbe1-d"></a>
### ARG_0XDBE1_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LMV_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = aktiv;  0 = inaktiv |

<a id="table-arg-0xdbe2-d"></a>
### ARG_0XDBE2_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REKU_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = aktiv;  0 = inaktiv |

<a id="table-arg-0xdbe8-d"></a>
### ARG_0XDBE8_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PUMPE_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 1 = ein; 0 = aus |

<a id="table-arg-0xdbe9-d"></a>
### ARG_0XDBE9_D

Dimensions: 12 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EINLASSVENTIL_VL | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Einlassventil vorne links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| EINLASSVENTIL_VR | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Einlassventil vorne rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| EINLASSVENTIL_HL | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Einlassventil hinten links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| EINLASSVENTIL_HR | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Einlassventil hinten rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| AUSLASSVENTIL_VL | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auslassventil vorne links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| AUSLASSVENTIL_VR | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auslassventil vorne rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| AUSLASSVENTIL_HL | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auslassventil hinten links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| AUSLASSVENTIL_HR | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auslassventil hinten rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| VORLADEVENTIL_VA | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Schwarz-Weiß: Vorladeventil Vorderachse;  Diagonal: Vorladeventil Kreis 1 (VL/HR) (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| VORLADEVENTIL_HA | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Schwarz-Weiß: Vorladeventil Hinterachse;  Diagonal: Vorladeventil Kreis 2 (VR/HL) (0 % = nicht angesteuert; 100 % = voll angesteuert); ESPPremium: Vorladeventil HA (HSV 2); ESPhev: Seperationsventil HA (SV)  ESPPremium: Vorladeventil HA (HSV 2) ESPhev: Seperationsventil HA (SV) |
| TRENNVENTIL_VA | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Schwarz-Weiß: Trennventil Vorderachse; Diagonal: Trennventil Kreis 1 (VL/HR) (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| TRENNVENTIL_HA | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Schwarz-Weiß: Trennventil Hinterachse; Diagonal: Trennventil Kreis 2 (VR/HL) (0 % = nicht angesteuert; 100 % = voll angesteuert); ESPPremium: Trennventil VA (USV 2); ESPhev: Druckregelventil VA (PCR) |

<a id="table-arg-0xdc89-d"></a>
### ARG_0XDC89_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX | 0-n | high | signed int | - | TAB_ADAPTIVDATEN_SBS | - | - | - | - | - | Auswahl Adaptivdatum |
| WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | - | - | Übergebener Wert |

<a id="table-arg-0xdc8a-d"></a>
### ARG_0XDC8A_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX | 0-n | high | signed int | - | TAB_ADAPTIVDATEN_AAEPS | - | - | - | - | - | Auswahl Adaptivdatum |
| WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | - | - | Übergebener Wert |

<a id="table-arg-0xdc8b-d"></a>
### ARG_0XDC8B_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX | 0-n | high | signed int | - | TAB_ADAPTIVDATEN_EV | 1.0 | 1.0 | 0.0 | - | - | Auswahl Adaptivdatum |
| WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | - | - | Übergebener Wert |

<a id="table-arg-0xdc8c-d"></a>
### ARG_0XDC8C_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX | 0-n | high | signed int | - | TAB_ADAPTIVDATEN_TSC | - | - | - | - | - | Auswahl Adaptivdatum |
| WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | - | - | Übergebener Wert |

<a id="table-arg-0xdc8d-d"></a>
### ARG_0XDC8D_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| INDEX | 0-n | high | signed int | - | TAB_ADAPTIVDATEN_ZFM | 1.0 | 1.0 | 0.0 | - | - | Auswahl Adaptivdatum |
| WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | - | - | Übergebener Wert |

<a id="table-arg-0xdcc0-d"></a>
### ARG_0XDCC0_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RE_ID | - | low | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | ID der Radelektronik |
| RE_POS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | - | - | Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts, 4 = Reserverad(nur RDC Gen2), 5, 6, 7, 8, 9 = Radposition nicht bekannt |

<a id="table-arg-0xdcc6-d"></a>
### ARG_0XDCC6_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSNR | 0-n | - | unsigned char | - | TAB_RDC_STEUERFUNKTIONEN | - | - | - | - | - | 1 = BANDMODE - Bandmode; 2 = ER_FAHRT - Eigenraderkennung bei Fahrt; 3 = ER_STAND - Eigenraderkennung im Stand (Gen2); 4 = TEST_ER_FAHRT - Empfang der Eigenraeder bei Fahrt pruefen; 5 = TEST_ER_STAND - Empfang der Eigenraeder im Stand pruefen (Gen2); 6 = RDCBUS_DIAG - Stromdiagnose LIN-Teilnehmer (Gen2); 7 = SOLLDRUCK_SCHREIBEN - aktuelle Reifendruckwerte als Sollwert; 8 = CAL_REQUEST - Kalibrieranforderung; 9 = ER_FAHRT_OHNE_TRIGGER - Eigenraderkennung bei Fahrt ohne Auswertung Triggerbit (Gen3); 10 = TEST_ER_FAHRT_OHNE_TRIGGER = Empfang der Eigenraeder bei Fahrt pruefen ohne Auswertung Triggerbit (Gen3) |
| AKTIONSNR | 0/1 | - | unsigned char | - | - | - | - | - | - | - | 1 - SET; 0 - RESET |

<a id="table-arg-0xdcee-d"></a>
### ARG_0XDCEE_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SOLLDRUCK | bar | low | unsigned int | - | - | 1000.0 | 1.0 | 0.0 | 3.0 | 4.8 | Sollwert Raddruck für Radelektronik |
| RADPOS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | - | - | Position Rad |

<a id="table-arg-0xdd0c-d"></a>
### ARG_0XDD0C_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PRD_PWR_EL_EPS | kW | high | unsigned char | - | - | 10.0 | 1.0 | 120.0 | -12.0 | 12.0 | Stellwert |

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

<a id="table-einzelfehler-bit"></a>
### EINZELFEHLER_BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nein |
| 1 | Ja |

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
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 479 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x022900 | Energiesparmode aktiv | 0 | - |
| 0x022908 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x022909 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02290A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02290B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02290C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02FF29 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x030541 | QDM-SBS - Gierratensensor Modellfehler Sensor 1 | 0 | - |
| 0x030543 | QDM-SBS - Gierratensensor Signalqualität Sensor 1 | 0 | - |
| 0x030545 | QDM-SBS - Gierratensensor Diversitaeres Rechnen HL-Software | 0 | - |
| 0x03054A | QDM-SBS - Lenkwinkel effektiv Modellfehler | 0 | - |
| 0x03054B | QDM-SBS - Lenkwinkel effektiv Randueberwachung | 0 | - |
| 0x03054E | QDM-SBS - Lenkwinkel effektiv Diversitaeres Rechnen HL-Software | 0 | - |
| 0x030557 | QDM-SBS - Lenkwinkel Fahrer Adaptivdaten fuer Lenkwinkeltoleranz auf Maximalwert | 0 | - |
| 0x03055A | QDM-SBS - Laengsbeschleunigungssensor Modellfehler | 0 | - |
| 0x03055B | QDM-SBS - Laengsbeschleunigungssensor Signalqualitaet | 0 | - |
| 0x03055C | QDM-SBS - Laengsbeschleunigungssensor Diversitaeres Rechnen HL-Software | 0 | - |
| 0x03056B | QDM-SBS - Querbeschleunigungssensor Modellfehler Sensor 1 | 0 | - |
| 0x03056D | QDM-SBS - Querbeschleunigungssensor Signalqualitaet Sensor 1 | 0 | - |
| 0x03056F | QDM-SBS - Querbeschleunigungssensor Diversitaeres Rechnen HL-Software | 0 | - |
| 0x03058A | QDM-SBS - Inkorrekter Rollenbetrieb erkannt | 0 | - |
| 0x03058C | QDM-SBS - Schwellen Querbeschleunigungsueberwachung aufgeweitet | 0 | - |
| 0x03058D | QDM-SBS - Schwerpunktsgeschwindigkeit Diversitaeres Rechnen HL-Software | 0 | - |
| 0x03058E | QDM-SBS - Beschleunigungssensoren Adaptivdaten Sensortoleranz auf Maximalwert | 0 | - |
| 0x03058F | QDM-SBS - Sensorcluster Seriennummer geändert oder fehlerhaft | 0 | - |
| 0x030800 | FAS - Globale Sicherheitsabschaltung | 0 | - |
| 0x030801 | FAS - ACC/DCC - Sicherheitsabschaltung | 0 | - |
| 0x030802 | FAS - SpeedLimiter - Sicherheitsabschaltung | 0 | - |
| 0x030804 | FAS - Frontschutz - Sicherheitsabschaltung | 0 | - |
| 0x030820 | FAS - Abschaltung - Unerwartete Reaktion eines Kommunikationspartners | 1 | - |
| 0x480681 | Weckleitung aktiv - Bus Sleep registriert bei aktiver Weckleitung | 0 | - |
| 0x480682 | Verteilergetriebe - Kupplungsposition unbekannt | 1 | - |
| 0x480686 | Raddrehzahlsensor - Hinten Rechts - Anfahrerkennung fehlerhaft | 0 | - |
| 0x48068C | Verteilergetriebe - Kupplung voruebergehend stillgelegt, evtl. Überhitzung | 1 | - |
| 0x480698 | Peripherial/Funktional error Schnittstelle QDM Initialisierung Signal ungültig | 0 | - |
| 0x48069B | RDCi Funkverbindung durch Fremdeinfluss gestoert | 1 | - |
| 0x48069D | Fahrzeugregler - Ist Lenkwinkel VA Rad - Phase 1: Fehleramplitude zu groß | 1 | - |
| 0x48069E | RDCi  Kalibrierung Raderkennung nicht moeglich | 0 | - |
| 0x4806A1 | RDCi Alle Radelektroniken bedingt kompatibel keine Positionsanzeige | 0 | - |
| 0x4806A6 | RDCi Radelektronik Position unbekannt Mischverbau | 0 | - |
| 0x4806B2 | Fahrzeugregler - Querbeschleunigung - Phase 1: Fehleramplitude zu groß | 1 | - |
| 0x4806B4 | Steuergerät intern - Main Treiber Fehler | 0 | - |
| 0x4806B8 | RDCi Radelektronik vorn links kein Empfang | 0 | - |
| 0x4806BA | Vacuumsensor - Plausi: mit Hauptzylinderbremsdruck | 0 | - |
| 0x4806D9 | Steuergerät intern - EEPROM Fehler | 0 | - |
| 0x4806DA | RDCi Radelektronik vorn rechts kein Empfang | 0 | - |
| 0x4806F0 | RDCi Radelektronik hinten links kein Empfang | 0 | - |
| 0x4806F1 | Drucksensor - Vorn Rechts - Federkontakt oder Sensor defekt | 0 | - |
| 0x4806F2 | Drucksensor - Vorn Rechts - Unplausibler Druckunterschied | 0 | - |
| 0x4806F3 | Drucksensor - Vorn Rechts - Temperaturfehler | 0 | - |
| 0x4806F4 | RDCi Radelektronik hinten rechts kein Empfang | 0 | - |
| 0x4806F5 | Drucksensor - Vorn Rechts - Offsetfehler | 0 | - |
| 0x4806F6 | Drucksensor - Primärkreis - Hydraulisches Bremssystem undicht | 0 | - |
| 0x4806FA | RDCi Radelektronik vorn links defekt | 0 | - |
| 0x4806FB | Drucksensor - Sekundärkreis - Hydraulisches Bremssystem undicht | 0 | - |
| 0x480702 | RDCi Radelektronik vorn rechts defekt | 0 | - |
| 0x480703 | Steuergerät intern - Ventile Fehler | 0 | - |
| 0x480704 | Steuergerät intern - Laufzeitfehler | 0 | - |
| 0x480705 | Steuergerät intern - HW Fehler ASG intern, System ASIC | 0 | - |
| 0x480706 | Steuergerät intern - HW Fehler ASG intern | 0 | - |
| 0x480707 | Steuergerät intern - RAM Fehler | 0 | - |
| 0x480709 | Steuergerät intern - Unplausibler Ventilstrom | 0 | - |
| 0x48070B | Steuergerät intern - Conti - EEPROM Fehler - Ventildaten | 0 | - |
| 0x48070C | Steuergerät intern - Conti - EEPROM Fehler - RPA-Daten | 0 | - |
| 0x48070D | Steuergerät intern - Conti - EEPROM Fehler - Einlassventildaten | 0 | - |
| 0x48070E | Bremslichtschalter - Plausibilitätsfehler | 0 | - |
| 0x48070F | RDCi Radelektronik hinten links defekt | 0 | - |
| 0x480710 | Raddrehzahlsensor - Vorn Links - Plausi: Drehrichtung | 0 | - |
| 0x480711 | Raddrehzahlsensor - Vorn Links - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480712 | Raddrehzahlsensor - Vorn Links - Elektrischer Fehler | 0 | - |
| 0x480713 | Raddrehzahlsensor - Vorn Rechts - Plausi: Drehrichtung | 0 | - |
| 0x480714 | Raddrehzahlsensor - Vorn Rechts - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480715 | Raddrehzahlsensor - Vorn Rechts - Elektrischer Fehler | 0 | - |
| 0x480716 | Raddrehzahlsensor - Hinten Links - Plausi: Drehrichtung | 0 | - |
| 0x480717 | Raddrehzahlsensor - Hinten Links - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x480718 | Raddrehzahlsensor - Hinten Links - Elektrischer Fehler | 0 | - |
| 0x480719 | Raddrehzahlsensor - Hinten Rechts - Plausi: Drehrichtung | 0 | - |
| 0x48071A | Raddrehzahlsensor - Hinten Rechts - Unplausibilität bei ABS-Regelung | 0 | - |
| 0x48071B | Raddrehzahlsensor - Hinten Rechts -  Elektrischer Fehler | 0 | - |
| 0x48071C | Elektrohydraulischer Bremsaktuator  - Versorgungsspannung | 0 | - |
| 0x48071E | Steuergerät intern - Hardware Fehler | 0 | - |
| 0x48071F | RDCi Radelektronik Position unbekannt | 0 | - |
| 0x480728 | RDCi Radelektronik hinten rechts defekt | 0 | - |
| 0x480730 | EPBi Aktuator - Hinten Links elektrischer Anschluss defekt | 0 | - |
| 0x480731 | EPBi Aktuator - Hinten Rechts elektrischer Anschluss defekt | 0 | - |
| 0x480732 | EPBi Aktuator Stromversorgung Links defekt | 0 | - |
| 0x480733 | EPBi Aktuator Stromversorgung Rechts defekt | 0 | - |
| 0x480734 | EPBi Aktuator Links defekt | 0 | - |
| 0x480735 | EPBi Aktuator Rechts defekt | 0 | - |
| 0x480744 | EPBi Taster Leitung 1 Kurzschluss Versorgung KL30 | 0 | - |
| 0x480745 | EPBi Taster Leitung 1 Kurzschluss nach Masse KL31 | 0 | - |
| 0x480746 | EPBi Taster Leitung 1 Leitungsunterbrechung | 0 | - |
| 0x480747 | EPBi Taster Leitung 2 Kurzschluss Versorgung KL30 | 0 | - |
| 0x480748 | EPBi Taster Leitung 2 Kurzschluss nach Masse KL31 | 0 | - |
| 0x480749 | EPBi Taster Leitung 2 Leitungsunterbrechung | 0 | - |
| 0x48074A | EPBi Taster Leitung 3 Kurzschluss Versorgung KL30 | 0 | - |
| 0x48074B | EPBi Taster Leitung 3 Kurzschluss nach Masse KL31 | 0 | - |
| 0x48074C | EPBi Taster Leitung 3 Leitungsunterbrechung | 0 | - |
| 0x48074D | EPBi Taster Leitung 4 Kurzschluss Versorgung KL30 | 0 | - |
| 0x48074E | EPBi Taster Leitung 4 Kurzschluss nach Masse KL31 | 0 | - |
| 0x48074F | EPBi Taster Leitung 4 Leitungsunterbrechung | 0 | - |
| 0x480750 | EPBi Taster Leitung 5 Kurzschluss Versorgung KL30 | 0 | - |
| 0x480751 | EPBi Taster Leitung 5 Kurzschluss nach Masse KL31 | 0 | - |
| 0x480752 | EPBi Taster Leitung 5 Leitungsunterbrechung | 0 | - |
| 0x480753 | EPBi Funktionsbeleuchtung - Kurzschluss Versorgung KL30 | 0 | - |
| 0x480754 | EPBi Funktionsbeleuchtung - Kurzschluss nach Masse KL31 | 0 | - |
| 0x480755 | EPBi Funktionsbeleuchtung - Unterbrechung | 0 | - |
| 0x480756 | EPBi Taster weckt zu oft | 0 | - |
| 0x480757 | EPBi Tasterleitungen nicht verbunden | 0 | - |
| 0x480758 | EPBi Taster dauerhaft betätigt | 0 | - |
| 0x480759 | EPBi Taster Unplausibles Signal | 0 | - |
| 0x480760 | EPBi - Montagemodus ist aktiv | 0 | - |
| 0x480762 | EPBi Links - Elektrischer Kurzschluss | 0 | - |
| 0x480763 | EPBi Rechts - Elektrischer Kurzschluss | 0 | - |
| 0x480764 | EPBi Aktuator Links - Elektrischer Fehler Offene Leitung | 0 | - |
| 0x480765 | EPBi Aktuator Rechts - Elektrischer Fehler Offene Leitung | 0 | - |
| 0x480766 | EPBi Aktuator Links - Elektrischer Kurzschluss GND oder KL30 | 0 | - |
| 0x480767 | EPBi Aktuator Rechts - Elektrischer Kurzschluss GND oder KL30 | 0 | - |
| 0x480769 | EPBi H-Brücke - Übertemperatur | 0 | - |
| 0x480771 | Steuergerät intern - EPBi - ECU | 0 | - |
| 0x48077C | RDCi Radelektronik vorn links Batterie Unterspannung | 1 | - |
| 0x48077D | RDCi Radelektronik vorn rechts Batterie Unterspannung | 1 | - |
| 0x48077E | RDCi Radelektronik hinten links Batterie Unterspannung | 1 | - |
| 0x48077F | RDCi Radelektronik hinten rechts Batterie Unterspannung | 1 | - |
| 0x480780 | RDCi Radelektronik Bandmode | 0 | - |
| 0x480781 | Steuergerät intern - Falsche Zuordnung von Hydraulikeinheit zu Anbausteuergerät | 0 | - |
| 0x48078A | Allradkupplung - Kupplungsposition offen, nur Frontantrieb | 0 | - |
| 0x480797 | Bremspedalwegsensor - Plausibilisierung - Tandem Hauptzylinder eGap nicht aktiv zu niedrig | 0 | - |
| 0x480798 | Bremspedalwegsensor - Plausibilisierung - Tandem Hauptzylinder eGap nicht aktiv zu hoch | 0 | - |
| 0x480799 | Bremspedalwegsensor - Plausibilisierung - Tandem Hauptzylinder eGap aktiv zu niedrig | 0 | - |
| 0x48079B | Steuergerät intern - Transceiver - Unterspannung | 0 | - |
| 0x48079C | Steuergerät intern - Transceiver - Medium Temperatur | 0 | - |
| 0x4807BF | EPBi Initialisierung nicht durchgeführt | 0 | - |
| 0x4807C0 | Fahrzeugregler - Querbeschleunigung - Fehleramplitude zu groß Phase 2 und 3 | 1 | - |
| 0x4807C1 | Fahrzeugregler - Ist Lenkwinkel VA Rad - Fehleramplitude zu groß Phase 2 und 3 | 1 | - |
| 0x4807C2 | Fahrzeugregler - Giergeschwindigkeit - Fehleramplitude zu groß Phase 2 und 3 | 1 | - |
| 0x480829 | Raddrehzahlsensor - Hinten Links - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082A | Raddrehzahlsensor - Hinten Rechts - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082B | Raddrehzahlsensor - Vorn Links - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082C | Raddrehzahlsensor - Vorn Rechts - Versorgung - Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x48082F | Steuergerät intern - ROM / Flash Fehler | 0 | - |
| 0x480830 | Steuergerät intern - Conti - EEPROM Fehler - Ventildaten - defekt | 0 | - |
| 0x480831 | Drucksensor - Hauptzylinder - Integrität Funktionalität unzureichend | 0 | - |
| 0x480832 | Drucksensor Versorgungsspannung interne Bremsdrucksensoren außerhalb spezifizierten Bereich | 0 | - |
| 0x480833 | Steuergerät intern - Fehlfunktion ADC externen Multiplexers | 0 | - |
| 0x480834 | Bremspedalwegsensor Signal 1 Bereichsfehler außerhalb oberen Gültigkeitsbereich | 0 | - |
| 0x480835 | Bremspedalwegsensor Signal 1 Bereichsfehler außerhalb unteren Gültigkeitsbereich | 0 | - |
| 0x480836 | Bremspedalwegsensor Signal 2 Bereichsfehler außerhalb oberen Gültigkeitsbereich | 0 | - |
| 0x480837 | Bremspedalwegsensor Signal 2 Bereichsfehler außerhalb unteren Gültigkeitsbereich | 0 | - |
| 0x480838 | EPBi Diversitäres Rechnen | 1 | - |
| 0x48083B | Peripherial/Funktional error Schnittstelle QDM Ist Lenkwinkel Vorderachse Signal temporär ungültig | 1 | - |
| 0x480840 | Raddrehzahlsensor - Hinten Links - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x48084B | Drucksensor - Vorn Rechts - Impulstest fehlgeschlagen | 0 | - |
| 0x48084F | Raddrehzahlsensor - Vorn Links - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x480856 | Drucksensor - Vorn Links - Offsetfehler | 0 | - |
| 0x480858 | Drucksensor - Vorn Links - Temperaturfehler | 0 | - |
| 0x48085B | Drucksensor - Vorn Links - Impulstest fehlgeschlagen | 0 | - |
| 0x480860 | Drucksensor - Vorn Links - Federkontakt oder Sensor defekt | 0 | - |
| 0x480869 | Drucksensor - Vorn Links - Unplausibler Druckunterschied | 0 | - |
| 0x48086A | Drucksensor - Vorn Rechts - Integrität Funktionalität unzureichend | 0 | - |
| 0x48086E | Drucksensor - Vorn Links - Integrität Funktionalität unzureichend | 0 | - |
| 0x480875 | Raddrehzahlsensor - Hinten Rechts - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x48087B | Raddrehzahlsensor - Vorn Rechts - Versorgung - Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x480883 | Bremsscheibentemperatur zu hoch | 0 | - |
| 0x480889 | Steuergerät intern - Lenkwinkel nicht aufgesetzt | 0 | - |
| 0x48088F | Allraddegradation - Notrad erkannt | 1 | - |
| 0x480928 | Raddrehzahlsensor - Vorn Links - Fehlender Zahn | 0 | - |
| 0x48092F | EPBi Aktuator Inkohärenter Aktuatorzustand | 0 | - |
| 0x480932 | Bremsflüssigkeitssensor - Bremsflüssigkeitsstand zu niedrig | 0 | - |
| 0x480964 | Lokale Spannungsversorgung - schwere Unterspannung | 1 | - |
| 0x480965 | Lokale Spannungsversorgung - Überspannung | 1 | - |
| 0x480975 | Steuergerät intern - Transceiver - VIO Fehler | 0 | - |
| 0x480976 | Steuergerät intern - Transceiver - Übertemperatur | 0 | - |
| 0x4809AB | Globale Spannungsversorgung - Unterspannung extern | 1 | - |
| 0x4809AC | Globale Spannungsversorgung - Überspannung extern | 1 | - |
| 0x4809AD | Steuergerät intern - Transceiver - Babbling Idiot | 0 | - |
| 0x4809B0 | Raddrehzahlsensor - Vorn Links - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809B7 | Raddrehzahlsensor - Hinten Links - Fehlender Zahn | 0 | - |
| 0x4809B9 | Raddrehzahlsensor - Hinten Links - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809C2 | Raddrehzahlsensor - Hinten Rechts - Fehlender Zahn | 0 | - |
| 0x4809CB | Raddrehzahlsensor - Vorn Rechts - Fehlender Zahn | 0 | - |
| 0x4809CD | Raddrehzahlsensor - Vorn Rechts - Anfahrerkennung fehlerhaft | 0 | - |
| 0x4809D7 | Steuergerät intern - Busfehler - Fehler Failsafe Schaltung | 0 | - |
| 0x4809D8 | Steuergerät intern - Busfehler - Fehler Memory Access | 0 | - |
| 0x4809D9 | Steuergerät intern - Temperatursensor - Elektrischer Fehler | 0 | - |
| 0x4809DB | Steuergerät intern - Transceiver - VCC Fehler | 0 | - |
| 0x4809DC | ECBA - Drehmoment angefordert, aber Release-Bit nicht gesetzt | 1 | - |
| 0x4809DF | Fahrzeugregler - Giergeschwindigkeit - Phase 1: Fehleramplitude zu groß | 1 | - |
| 0x4809EA | RDCi Radelektronik Position unbekannt defekt | 0 | - |
| 0x4809EB | RDCi Radelektronik (Position unbekannt) kein Empfang | 0 | - |
| 0x480A08 | Drucksensor - Hauptzylinder - Leitungsfehler | 0 | - |
| 0x480A11 | Bremsbelagsensor - Vorderachse - Verschleissgrenze erreicht | 0 | - |
| 0x480A12 | Bremsbelagsensor - Hinterachse - Verschleissgrenze erreicht | 0 | - |
| 0x480A13 | Bremsbelagsensor - Vorderachse - Plausibilität | 0 | - |
| 0x480A14 | Bremsbelagsensor - Hinterachse - Plausibilität | 0 | - |
| 0x480A22 | Drucksensor - nicht kalibriert | 0 | - |
| 0x480A46 | RDCi Gateway oder Antennen Fehler | 1 | - |
| 0x480A5B | Elektrohydraulischer Bremsaktuator - gemessene Drehzahl trotz Ansteuerung zu gering - RFP laeuft nicht | 0 | - |
| 0x480A69 | Drucksensor - Hauptzylinder - Impulstest fehlgeschlagen | 0 | - |
| 0x480A85 | Bremspedalwegsensor -  Nullstellung nicht initialisiert | 0 | - |
| 0x480A86 | Bremspedalwegsensor -  Plausibilisierung Signalleitung 1 Unterbrechung oder auf Masse unteres Fehlerband | 0 | - |
| 0x480A87 | Bremspedalwegsensor -  Plausibilisierung Signalleitung 2 Unterbrechung oder auf Masse unteres Fehlerband | 0 | - |
| 0x480A88 | Bremspedalwegsensor -  Plausibilisierung Signalleitung 1 Kurzschluss nach Plus | 0 | - |
| 0x480A8B | Drucksensor - Interne Plausibilisierung fehlgeschlagen | 0 | - |
| 0x480A8C | Drucksensor - Rauschüberwachung | 0 | - |
| 0x480A8D | Drucksensor - Plausibilisierung Temperatur intern | 0 | - |
| 0x480A8F | Drucksensor - Plausibilisierung zwischen Hauptzylinder und Kreisdrucksensor | 0 | - |
| 0x480A90 | Raddrehzahlsensor - Allgemein - Rollenmodus aktiv | 0 | - |
| 0x480A91 | Drucksensor - Hauptzylinder - Offsetfehler | 0 | - |
| 0x480A92 | Raddrehzahlsensor - Allgemein - Unterspannung bei aktiven Anfahrassistenten | 0 | - |
| 0x480A9B | Fahrzeugregler Dauerregelung | 0 | - |
| 0x480A9C | Raddrehzahlsensor - Vorn Links - Falscher Sensortyp | 0 | - |
| 0x480A9D | Raddrehzahlsensor - Vorn Links - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480A9E | Raddrehzahlsensor - Vorn Links - unerwarteter Signalsprung | 0 | - |
| 0x480A9F | Raddrehzahlsensor - Vorn Links - Rauschüberwachung | 0 | - |
| 0x480AA0 | Steuergerät intern - Falscher HW Musterstand oder nicht freigegebene Software | 0 | - |
| 0x480AA1 | ECBA - Plausi Fahrzeugverzögerung | 1 | - |
| 0x480AA2 | Bremspedalwegsensor -  Plausibilisierung Signalleitung 2 Kurzschluss nach Plus | 0 | - |
| 0x480AA3 | Raddrehzahlsensor - Vorn Rechts - Falscher Sensortyp | 0 | - |
| 0x480AA4 | Raddrehzahlsensor - Vorn Rechts - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AA5 | Raddrehzahlsensor - Vorn Rechts - unerwarteter Signalsprung | 0 | - |
| 0x480AA6 | Raddrehzahlsensor - Vorn Rechts - Rauschüberwachung | 0 | - |
| 0x480AA8 | Bremspedalwegsensor -  Plausibilisierung Signalleitung 1 zu Signalleitung 2 fehlgeschlagen | 0 | - |
| 0x480AA9 | Bremspedalwegsensor -  Plausibilisierung Nullpunkt Offset zu groß | 0 | - |
| 0x480AAA | Raddrehzahlsensor - Hinten Links - Falscher Sensortyp | 0 | - |
| 0x480AAB | Raddrehzahlsensor - Hinten Links - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AAC | Raddrehzahlsensor - Hinten Links - unerwarteter Signalsprung | 0 | - |
| 0x480AAD | Raddrehzahlsensor - Hinten Links - Rauschüberwachung | 0 | - |
| 0x480AB1 | Raddrehzahlsensor - Hinten Rechts - Falscher Sensortyp | 0 | - |
| 0x480AB2 | Raddrehzahlsensor - Hinten Rechts - Plausi gegen Radgeschwindigkeit | 0 | - |
| 0x480AB3 | Raddrehzahlsensor - Hinten Rechts - unerwarteter Signalsprung | 0 | - |
| 0x480AB4 | Raddrehzahlsensor - Hinten Rechts - Rauschüberwachung | 0 | - |
| 0x480AB8 | Internes Zustandsmanagement Kompletter Überwachungsumfang | 1 | - |
| 0x480ABF | Bremspedalwegsensor -  Nullpunktabgleich Checksummenfehler | 0 | - |
| 0x480AC0 | Codierung - Falsche Antriebsvariante Allrad | 0 | - |
| 0x480AC4 | Bremspedalwegsensor - Plausibilisierung - Versorgungsleitung Kurzschluss nach Masse | 0 | - |
| 0x480AC5 | Bremspedalwegsensor - Plausibilisierung - Versorgungsleitung Kurzschluss nach Plus | 0 | - |
| 0x480ACF | Auslösung Anti Power Hop Funktion | 1 | - |
| 0xD3441F | FLEXRAY Bus 1 | 0 | - |
| 0xD34420 | FLEXRAY Controller Error Bus 1 | 0 | - |
| 0xD34BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xD35418 | Botschaftsfehler (Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) - Timeout | 1 | - |
| 0xD35419 | Botschaftsfehler (Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) - Checksumme | 1 | - |
| 0xD3541A | Botschaftsfehler (Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) - Alive | 1 | - |
| 0xD35420 | Botschaftsfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Timeout | 1 | - |
| 0xD35421 | Botschaftsfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Checksumme | 1 | - |
| 0xD35422 | Botschaftsfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Alive | 1 | - |
| 0xD35426 | Signalfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Ungültig | 1 | - |
| 0xD35427 | Signalfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Undefiniert | 1 | - |
| 0xD35428 | Botschaftsfehler (Außentemperatur, ID: A_TEMP) - Timeout | 1 | - |
| 0xD3542C | Signalfehler (Außentemperatur, ID: A_TEMP) - Ungültig | 1 | - |
| 0xD35444 | Botschaftsfehler (Bedienung Wischertaster, ID: BEDIENUNG_WISCHER) - Timeout | 1 | - |
| 0xD35445 | Botschaftsfehler (Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) - Checksumme | 1 | - |
| 0xD3544D | Signalfehler (Steuerung Crash, ID: CTR_CR) - Ungültig | 1 | - |
| 0xD3544E | Signalfehler (Fahrgestellnummer, ID: FAHRGESTELLNUMMER) - Ungültig | 1 | - |
| 0xD35452 | Botschaftsfehler (Daten Antriebsstrang 3, ID: DT_PT_3) - Timeout | 1 | - |
| 0xD3545D | Botschaftsfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Timeout | 1 | - |
| 0xD3545F | Botschaftsfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Checksumme | 1 | - |
| 0xD35460 | Botschaftsfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Alive | 1 | - |
| 0xD35461 | Signalfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Ungültig | 1 | - |
| 0xD35463 | Signalfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Undefiniert | 1 | - |
| 0xD3546A | Botschaftsfehler (Ist Daten E-Motor Traktion, ID: AVL_DT_MOT_TRCT) Checksumme | 1 | - |
| 0xD35476 | Signalfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Ungültig | 1 | - |
| 0xD35482 | Botschaftsfehler (Fahrgestellnummer, ID: FAHRGESTELLNUMMER) - Timeout | 1 | - |
| 0xD3548B | Botschaftsfehler (Anforderung FAS, ID: RQ_FAS) - Checksumme | 1 | - |
| 0xD3548F | Signalfehler (Anforderung FAS, ID: RQ_FAS) - Ungültig | 1 | - |
| 0xD3549B | Signalfehler (Soll Radlenkwinkel Vorderachse Parkassistent, ID: TAR_WSTA_FTAX_PMA) - Qualifier | 1 | - |
| 0xD3549C | Signalfehler (Klemmen, ID: KLEMMEN) - Qualifier | 1 | - |
| 0xD3549D | Signalfehler (Status Elektrische-Lenkung Vorderachse, ID: ST_EST) - Qualifier | 1 | - |
| 0xD3549F | Signalfehler (Daten Bremssystem Motorsteuerung, ID: DT_BRKSYS_ENGMG) - Qualifier | 1 | - |
| 0xD354A1 | Signalfehler (Ist Position EPS, ID: AVL_PO_EPS) - Qualifier | 1 | - |
| 0xD354AC | Botschaftsfehler (Fahrzeugzustand, ID: FZZSTD) - Timeout | 1 | - |
| 0xD354B6 | Signalfehler (Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) - Ungültig | 1 | - |
| 0xD354E5 | Botschaftsfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Checksumme | 1 | - |
| 0xD354F2 | Botschaftsfehler (Kilometerstand/Reichweite, ID: KILOMETERSTAND) - Timeout | 1 | - |
| 0xD354F6 | Signalfehler (Kilometerstand/Reichweite, ID: KILOMETERSTAND) - Ungültig | 1 | - |
| 0xD354F8 | Botschaftsfehler (Klemmen, ID: KLEMMEN) - Timeout | 1 | - |
| 0xD354F9 | Botschaftsfehler (Klemmen, ID: KLEMMEN) - Checksumme | 1 | - |
| 0xD354FA | Botschaftsfehler (Klemmen, ID: KLEMMEN) - Alive | 1 | - |
| 0xD354FC | Signalfehler (Klemmen, ID: KLEMMEN) - Ungültig | 1 | - |
| 0xD354FD | Signalfehler (Klemmen, ID: KLEMMEN) - Undefiniert | 1 | - |
| 0xD35513 | Botschaftsfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Alive | 1 | - |
| 0xD3553C | Signalfehler (Anzeige Checkcontrol Fahrdynamik 02, ID: DISP_CC_DRDY_02) - Ungültig | 1 | - |
| 0xD35552 | Signalfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Ungültig | 1 | - |
| 0xD35553 | Signalfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Undefiniert | 1 | - |
| 0xD35557 | Botschaftsfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Timeout | 1 | - |
| 0xD35558 | Botschaftsfehler (Radmoment Antrieb 2, ID: WMOM_DRV_2) - Timeout | 1 | - |
| 0xD35559 | Botschaftsfehler (Radmoment Antrieb 2, ID: WMOM_DRV_2) - Checksumme | 1 | - |
| 0xD3555A | Botschaftsfehler (Radmoment Antrieb 2, ID: WMOM_DRV_2) - Alive | 1 | - |
| 0xD3555E | Signalfehler (Radmoment Antrieb 2, ID: WMOM_DRV_2) - Ungültig | 1 | - |
| 0xD35560 | Botschaftsfehler (Ist Daten E-Motor Traktion, ID: AVL_DT_MOT_TRCT) Alive | 1 | - |
| 0xD3556C | Signalfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) - Ungültig | 1 | - |
| 0xD3556D | Botschaftsfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) - Timeout | 1 | - |
| 0xD35570 | Botschaftsfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Timeout | 1 | - |
| 0xD35571 | Botschaftsfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Checksumme | 1 | - |
| 0xD35572 | Botschaftsfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Alive | 1 | - |
| 0xD35577 | Signalfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Qualifier | 1 | - |
| 0xD3557A | Signalfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Ungültig | 1 | - |
| 0xD3557B | Signalfehler (Radmoment Antrieb 4, ID: WMOM_DRV_4) - Undefiniert | 1 | - |
| 0xD35584 | Signalfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Ungültig | 1 | - |
| 0xD35585 | Signalfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Undefiniert | 1 | - |
| 0xD35586 | Botschaftsfehler (Regensensor-Wischergeschwindigkeit, ID: WISCHERGESCHWINDIGKEIT) - Timeout | 1 | - |
| 0xD3558C | Botschaftsfehler (Relativzeit BN2020, ID: RELATIVZEIT) - Timeout | 1 | - |
| 0xD355A0 | Botschaftsfehler (Status Anhänger, ID: STAT_ANHAENGER) - Timeout | 1 | - |
| 0xD355A4 | Signalfehler (Status Anhänger, ID: STAT_ANHAENGER) - Ungültig | 1 | - |
| 0xD355B4 | Botschaftsfehler (Status Bedienelement HDC, ID: ST_OPEL_HDC) - Timeout | 1 | - |
| 0xD355B8 | Signalfehler (Status Bedienelement HDC, ID: ST_OPEL_HDC) - Ungültig | 1 | - |
| 0xD355C4 | Botschaftsfehler (Status Elektrische-Lenkung Vorderachse, ID: ST_EST) - Timeout | 1 | - |
| 0xD355C8 | Signalfehler (Status Elektrische-Lenkung Vorderachse, ID: ST_EST) - Ungültig | 1 | - |
| 0xD355F2 | Botschaftsfehler (Steuerung Crash, ID: CTR_CR ) - Timeout | 1 | - |
| 0xD355F3 | Botschaftsfehler (Steuerung Crash, ID: CTR_CR ) - Checksumme | 1 | - |
| 0xD355F4 | Botschaftsfehler  (Steuerung Crash, ID: CTR_CR ) -  Alive | 1 | - |
| 0xD355FF | Botschaftsfehler (Ist Daten E-Motor Traktion, ID: AVL_DT_MOT_TRCT) Timeout | 1 | - |
| 0xD35644 | Signalfehler (Ist Daten E-Motor Traktion, ID: AVL_DT_MOT_TRCT) Ungültig | 1 | - |
| 0xD35646 | Botschaftsfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Timeout | 1 | - |
| 0xD35647 | Botschaftsfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Checksumme | 1 | - |
| 0xD35648 | Botschaftsfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Alive | 1 | - |
| 0xD3564C | Signalfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Ungültig | 1 | - |
| 0xD3564D | Signalfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Undefiniert | 1 | - |
| 0xD35677 | Signalfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Qualifier | 1 | - |
| 0xD3567D | Botschaftsfehler (Einheiten BN2020, ID: EINHEITEN_BN2020) Timeout | 1 | - |
| 0xD3567E | Botschaftsfehler (Fahrerlebnis Modus, ID: DXP_MOD) - Timeout | 1 | - |
| 0xD3568A | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Timeout | 1 | - |
| 0xD3568B | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Timeout | 1 | - |
| 0xD35693 | Botschaftsfehler (Daten Antriebsstrang 1, ID: DT_PT_1) Timeout | 1 | - |
| 0xD35694 | Botschaftsfehler (RDC Daten Paket 1, ID: RDC_DT_PCKG_1) - Timeout | 1 | - |
| 0xD35698 | Botschaftsfehler (Anforderung Drehmoment Betriebsstrategie, ID:RQ_TORQ_OSTR) - Timeout | 1 | - |
| 0xD3569B | Botschaftsfehler (Diagnose OBD Motor, ID: DIAG_OBD_ENG) - Timeout | 1 | - |
| 0xD356A3 | Botschaftsfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Timeout | 1 | - |
| 0xD356A4 | Botschaftsfehler (Status Diagnose OBD 3 Fahrdynamik, ID: ST_DIAG_OBD_3_DRDY) - Timeout | 1 | - |
| 0xD356A5 | Botschaftsfehler (Anzeige Checkcontrol Fahrdynamik 02, ID: DISP_CC_DRDY_02) - Timeout | 1 | - |
| 0xD356A8 | Botschaftsfehler (Status Diagnose OBD 1 Fahrdynamik, ID: ST_DIAG_OBD_1_DRDY) - Timeout | 1 | - |
| 0xD356AA | Botschaftsfehler (Status Start Leistung Antrieb, ID: ST_STA_PWR_DRV) - Timeout | 1 | - |
| 0xD356B6 | Botschaftsfehler (Anzeige Checkcontrol Fahrdynamik 02, ID: DISP_CC_DRDY_02) - Alive | 1 | - |
| 0xD356C6 | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Checksumme | 1 | - |
| 0xD356C7 | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Checksumme | 1 | - |
| 0xD356D9 | Botschaftsfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Checksumme | 1 | - |
| 0xD356DC | Botschaftsfehler (Status Anzeige Fahrdynamik, ID: ST_DISP_DRDY) - Timeout | 1 | - |
| 0xD356E1 | Signalfehler (Status Anzeige Fahrdynamik, ID: ST_DISP_DRDY) - Ungültig | 1 | - |
| 0xD356E4 | Botschaftsfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Timeout | 1 | - |
| 0xD356E5 | Botschaftsfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Checksumme | 1 | - |
| 0xD356E6 | Botschaftsfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Alive | 1 | - |
| 0xD356F5 | Botschaftsfehler (Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) - Timeout | 1 | - |
| 0xD356F6 | Botschaftsfehler (Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) - Alive | 1 | - |
| 0xD35713 | Signalfehler (Einheiten BN2020, ID: EINHEITEN_BN2020) Ungültig | 1 | - |
| 0xD35714 | Signalfehler (Fahrerlebnis Modus, ID: DXP_MOD) - Ungültig | 1 | - |
| 0xD35720 | Botschaftsfehler (RDC Daten Paket 1, ID: RDC_DT_PCKG_1) - Alive | 1 | - |
| 0xD3572F | Botschaftsfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Alive | 1 | - |
| 0xD35732 | Botschaftsfehler (Bedienung Tempomat, ID: OP_CCTR) - Timeout | 1 | - |
| 0xD35736 | Signalfehler (Bedienung Tempomat, ID: OP_CCTR) - Ungültig | 1 | - |
| 0xD35742 | Botschaftsfehler (Status Diagnose OBD 3 Fahrdynamik, ID: ST_DIAG_OBD_3_DRDY) - Alive | 1 | - |
| 0xD35743 | Botschaftsfehler (Status Diagnose OBD 1 Fahrdynamik, ID: ST_DIAG_OBD_1_DRDY) - Alive | 1 | - |
| 0xD35744 | Botschaftsfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Timeout | 1 | - |
| 0xD35745 | Botschaftsfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Checksumme | 1 | - |
| 0xD35746 | Botschaftsfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Alive | 1 | - |
| 0xD3574D | Botschaftsfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) - Checksumme | 1 | - |
| 0xD3574E | Botschaftsfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) - Alive | 1 | - |
| 0xD35751 | Botschaftsfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Checksumme | 1 | - |
| 0xD35752 | Botschaftsfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Alive | 1 | - |
| 0xD35755 | Botschaftsfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Timeout | 1 | - |
| 0xD35757 | Botschaftsfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Checksumme | 1 | - |
| 0xD35758 | Botschaftsfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Alive | 1 | - |
| 0xD3576E | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Alive | 1 | - |
| 0xD3576F | Botschaftsfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Alive | 1 | - |
| 0xD35772 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Ungültig | 1 | - |
| 0xD35773 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Ungültig | 1 | - |
| 0xD35775 | Signalfehler (Daten Antriebsstrang 1, ID: DT_PT_1) Ungültig | 1 | - |
| 0xD3577B | Signalfehler (Anforderung Drehmoment Betriebsstrategie, ID:RQ_TORQ_OSTR) - Ungültig | 1 | - |
| 0xD3577F | Signalfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Ungültig | 1 | - |
| 0xD35789 | Signalfehler (Status Diagnose OBD 3 Fahrdynamik, ID: ST_DIAG_OBD_3_DRDY) - Ungültig | 1 | - |
| 0xD3578A | Signalfehler (Status Diagnose OBD 1 Fahrdynamik, ID: ST_DIAG_OBD_1_DRDY) - Ungültig | 1 | - |
| 0xD3578B | Signalfehler (Navigationsgraph Karten Daten, ID: NAV_GRAPH_MAPDATA) - Ungültig | 1 | - |
| 0xD3578F | Signalfehler (Status Start Leistung Antrieb, ID: ST_STA_PWR_DRV) - Ungültig | 1 | - |
| 0xD35799 | Signalfehler (Diagnose OBD Motor, ID: DIAG_OBD_ENG) - Ungültig | 1 | - |
| 0xD3579B | Signalfehler (Navigationsgraph Fahrspur, ID: NAV_GRAPH_LNE) - Ungültig | 1 | - |
| 0xD357B2 | Signalfehler (Fahrerlebnis Modus, ID: DXP_MOD) - Qualifier | 1 | - |
| 0xD357C8 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Qualifier | 1 | - |
| 0xD357C9 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Qualifier | 1 | - |
| 0xD357CA | Signalfehler (Anforderung Drehmoment Betriebsstrategie, ID:RQ_TORQ_OSTR) - Qualifier | 1 | - |
| 0xD357CC | Signalfehler (Status Start Leistung Antrieb, ID: ST_STA_PWR_DRV) - Qualifier | 1 | - |
| 0xD357E1 | Signalfehler (Anforderung Bremsmoment Summe, ID: RQ_BRTORQ_SUM) - Qualifier | 1 | - |
| 0xD357E5 | Signalfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Qualifier | 1 | - |
| 0xD357E7 | Signalfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Qualifier | 1 | - |
| 0xD357EA | Botschaftsfehler (LCD Helligkeit Regelung, ID: LCD_BRIG_CLCTR) - Timeout | 1 | - |
| 0xD357F2 | Signalfehler (Radmoment Antrieb 2, ID: WMOM_DRV_2) - Qualifier | 1 | - |
| 0xD357F3 | Signalfehler (Navigationsgraph Fahrspur, ID: NAV_GRAPH_LNE) - Qualifier | 1 | - |
| 0xD357F5 | Signalfehler (Status Anzeige Kombi, ID: ST_DISP_KI) - Qualifier | 1 | - |
| 0xD35803 | Signalfehler (Uhrzeit/Datum, ID: UHRZEIT_DATUM) Qualifier | 1 | - |
| 0xD35807 | Signalfehler (Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) Qualifier | 1 | - |
| 0xD3580B | Signalfehler (Status Bedienelement HDC, ID: ST_OPEL_HDC) Qualifier | 1 | - |
| 0xD35811 | Botschaftsfehler (Navigation System Information, ID: NAV_SYS_INF) - Timeout | 1 | - |
| 0xD35815 | Signalfehler (Navigation System Information, ID: NAV_SYS_INF) - Ungültig | 1 | - |
| 0xD3581F | Signalfehler (Navigationsgraph, ID: NAV_GRAPH) - Ungültig | 1 | - |
| 0xD35822 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 2, ID: WMOM_DRV_ELD_AW_2) - Undefiniert | 1 | - |
| 0xD35823 | Signalfehler (Radmoment Antrieb elektrifizierter Allrad 1, ID: WMOM_DRV_ELD_AW_1) - Undefiniert | 1 | - |
| 0xD3582B | Signalfehler (Status Start Leistung Antrieb, ID: ST_STA_PWR_DRV) - Undefiniert | 1 | - |
| 0xD35833 | Signalfehler (Status Diagnose OBD 3 Fahrdynamik, ID: ST_DIAG_OBD_3_DRDY) - Undefiniert | 1 | - |
| 0xD35834 | Signalfehler (Status Diagnose OBD 1 Fahrdynamik, ID: ST_DIAG_OBD_1_DRDY) - Undefiniert | 1 | - |
| 0xD3583F | Signalfehler (Navigationsgraph Geschwindigkeit, ID: NAV_GRAPH_V) - Ungültig | 1 | - |
| 0xD35843 | Signalfehler (Radmoment Antrieb Elektrifizierter Allrad 3, ID: WMOM_DRV_ELD_AW_3) - Undefiniert | 1 | - |
| 0xD35845 | Signalfehler (Diagnose OBD Motor, ID: DIAG_OBD_ENG) - Undefiniert | 1 | - |
| 0xD358A6 | Signalfehler (Navigationsgraph Geschwindigkeit, ID: NAV_GRAPH_V) Qualifier | 1 | - |
| 0xD358A7 | Signalfehler (Synchronisation Navigationsgraph, ID: NAV_GRAPH_SYNC) Qualifier | 1 | - |
| 0xD358AD | Signalfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) Qualifier | 1 | - |
| 0xD358B2 | Signalfehler (Status Gurt Kontakt Sitzbelegung, ID: ST_BLT_CT_SOCCU) - Qualifier | 1 | - |
| 0xD358B5 | Botschaftsfehler (Status Anzeige Kombi, ID: ST_DISP_KI) - Timeout | 1 | - |
| 0xD358B9 | Signalfehler (Status Anzeige Kombi, ID: ST_DISP_KI) - Ungültig | 1 | - |
| 0xD358E1 | Botschaftsfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Timeout | 1 | - |
| 0xD358E6 | Botschaftsfehler (Status Parkassistent, ID: ST_PMA) - Timeout | 1 | - |
| 0xD358F8 | Signalfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Ungültig | 1 | - |
| 0xD358F9 | Signalfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Undefiniert | 1 | - |
| 0xD35914 | Signalfehler (Synchronisation Navigationsgraph, ID: NAV_GRAPH_SYNC) - Ungültig | 1 | - |
| 0xD35922 | Botschaftsfehler (Übereinstimmung Navigationsgraph, ID: NAV_GRAPH_MATCH) - Timeout | 1 | - |
| 0xD35926 | Signalfehler (Übereinstimmung Navigationsgraph, ID: NAV_GRAPH_MATCH) - Ungültig | 1 | - |
| 0xD35932 | Botschaftsfehler (Uhrzeit/Datum, ID: UHRZEIT_DATUM) - Timeout | 1 | - |
| 0xD35936 | Signalfehler (Uhrzeit/Datum, ID: UHRZEIT_DATUM) - Ungültig | 1 | - |
| 0xD35937 | Signalfehler (Uhrzeit/Datum, ID: UHRZEIT_DATUM) - Undefiniert | 1 | - |
| 0xD3593C | Botschaftsfehler (Vorgabe Dämpfer Anteil passiv, ID: SPEC_DMP_QTA_PSV) - Timeout | 1 | - |
| 0xD35948 | Signalfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Ungültig | 1 | - |
| 0xD35949 | Signalfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Undefiniert | 1 | - |
| 0xD35996 | Signalfehler (Status Parkassistent, ID: ST_PMA) - Ungültig | 1 | - |
| 0xD359AB | Signalfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Ungültig | 1 | - |
| 0xD359BF | Botschaftsfehler (Ist Lenkmoment Fahrer Stellglied, ID: AVL_STMOM_DV_ACT) - Timeout | 1 | - |
| 0xD359C0 | Botschaftsfehler (Ist Lenkmoment Fahrer Stellglied, ID: AVL_STMOM_DV_ACT) - Checksumme | 1 | - |
| 0xD359C1 | Botschaftsfehler (Ist Lenkmoment Fahrer Stellglied, ID: AVL_STMOM_DV_ACT) - Alive | 1 | - |
| 0xD359C3 | Signalfehler (Ist Lenkmoment Fahrer Stellglied, ID: AVL_STMOM_DV_ACT) - Ungültig | 1 | - |
| 0xD35A08 | Botschaftsfehler (Radmoment Antrieb 6, ID: WMOM_DRV_6) - Timeout | 1 | - |
| 0xD35A09 | Botschaftsfehler (Radmoment Antrieb 6, ID: WMOM_DRV_6) - Checksumme | 1 | - |
| 0xD35A0A | Botschaftsfehler (Radmoment Antrieb 6, ID: WMOM_DRV_6) - Alive | 1 | - |
| 0xD35A0C | Signalfehler (Radmoment Antrieb 6, ID: WMOM_DRV_6) - Ungültig | 1 | - |
| 0xD35A9C | Signalfehler (Vorgabe Parametrisierung I-Brake/HDC, ID: SPEC_PRMSN_IBRK_HDC) - Qualifier | 1 | - |
| 0xD35ACA | Signalfehler (Navigation System Information, ID: NAV_SYS_INF) - Qualifier | 1 | - |
| 0xD35ACC | Signalfehler (Radmoment Antrieb 6, ID: WMOM_DRV_6) - Qualifier | 1 | - |
| 0xD35ADA | Signalfehler (Steuerung Crash, ID: CTR_CR) - Undefiniert | 1 | - |
| 0xD35B00 | Botschaftsfehler (Anforderung Hydraulikfunktion, ID: RQ_HYDFN) - Timeout | 1 | - |
| 0xD35B01 | Botschaftsfehler (Anforderung Hydraulikfunktion, ID: RQ_HYDFN) - Checksumme | 1 | - |
| 0xD35B02 | Botschaftsfehler (Anforderung Hydraulikfunktion, ID: RQ_HYDFN) - Alive | 1 | - |
| 0xD35B04 | Signalfehler (Anforderung Hydraulikfunktion, ID: RQ_HYDFN) - Ungültig | 1 | - |
| 0xD35B26 | Botschaftsfehler (Ist Position EPS, ID: AVL_PO_EPS) - Timeout | 1 | - |
| 0xD35B27 | Botschaftsfehler (Ist Position EPS, ID: AVL_PO_EPS) - Checksumme | 1 | - |
| 0xD35B28 | Botschaftsfehler (Ist Position EPS, ID: AVL_PO_EPS) - Alive | 1 | - |
| 0xD35B2A | Signalfehler (Ist Position EPS, ID: AVL_PO_EPS) - Ungültig | 1 | - |
| 0xD35B3F | Botschaftsfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Timeout | 1 | - |
| 0xD35B40 | Botschaftsfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Checksumme | 1 | - |
| 0xD35B41 | Botschaftsfehler (Radmoment Antrieb 5, ID: WMOM_DRV_5) - Alive | 1 | - |
| 0xD35C0C | Botschaftsfehler (Ist Kraft Zahnstange, ID: AVL_FORC_GRD) - Timeout | 1 | - |
| 0xD35C18 | Botschaftsfehler (Soll Radlenkwinkel Vorderachse Parkassistent, ID: TAR_WSTA_FTAX_PMA) - Timeout | 1 | - |
| 0xD35C1A | Botschaftsfehler (Soll Radlenkwinkel Vorderachse Parkassistent, ID: TAR_WSTA_FTAX_PMA) - Alive | 1 | - |
| 0xD35C1C | Botschaftsfehler (Status Gang Rückwärts, ID: STAT_GANG_RUECKWAERTS) - Timeout | 1 | - |
| 0xD35C1D | Botschaftsfehler (Status Kontakt Handbremse, ID: STAT_CT_HABR) - Timeout | 1 | - |
| 0xD3642E | Botschaftsfehler (Status Drehzahl, ID: ST_RPM) Timeout | 1 | - |
| 0xD3642F | Botschaftsfehler(Status Drehzahl, ID: ST_RPM) Alive | 1 | - |
| 0xD36430 | Botschaftsfehler (Status Drehzahl, ID: ST_RPM) Checksumme | 1 | - |
| 0xD36500 | Botschaftsfehler (xDrive Stellglied Information, ID: XDRV_ACT_INFO) - Timeout | 1 | - |
| 0xD36508 | Signalfehler (Status Parkassistent, ID: ST_PMA) - Qualifier | 1 | - |
| 0xD3650C | Botschaftsfehler (Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) - Timeout | 1 | - |
| 0xD3650D | Botschaftsfehler (Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) - Checksumme | 1 | - |
| 0xD3650E | Botschaftsfehler (Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) - Alive | 1 | - |
| 0xD3650F | Signalfehler (Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) - Ungültig | 1 | - |
| 0xD36511 | Signalfehler (Sensorclusterdaten Rohwerte, ID: SEN_CLU_DT_RAW) - Qualifier | 1 | - |
| 0xD36C0D | Signalfehler (Daten Antriebsstrang 2, ID: DT_PT_2) - Undefiniert | 1 | - |
| 0xD36C19 | Signalfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Undefiniert | 1 | - |
| 0xD36C3B | Signalfehler (Radmoment Antrieb 3, ID: WMOM_DRV_3) - Undefiniert | 1 | - |
| 0xD36C41 | Signalfehler (Soll Radlenkwinkel Vorderachse Parkassistent, ID: TAR_WSTA_FTAX_PMA) - Ungültig | 1 | - |
| 0xD36C60 | Signalfehler (Status Anzeige Fahrdynamik, ID: ST_DISP_DRDY) - Qualifier | 1 | - |
| 0xD36C81 | Signalfehler (Status Türsensoren Abgesichert, ID: STAT_DS_VRFD) - Ungültig | 1 | - |
| 0xD36D01 | Signalfehler (Winkel Fahrpedal, ID: ANG_ACPD) - Qualifier | 1 | - |
| 0xD36D07 | Signalfehler (Ist Lenkmoment Fahrer Stellglied, ID: AVL_STMOM_DV_ACT) - Qualifier | 1 | - |
| 0xD36D1B | Botschaftsfehler (Anforderung FAS, ID: RQ_FAS) - Timeout | 1 | - |
| 0xD36D1E | Signalfehler (Bedienung Tempomat, ID: OP_CCTR ) - Qualifier | 1 | - |
| 0xD36D2D | Botschaftsfehler (Anforderung FAS, ID: RQ_FAS) - Alive | 1 | - |
| 0xD36D31 | Botschaftsfehler (Kamera Frontraumüberwachung, ID: CAM_HDWOBS) - Timeout | 1 | - |
| 0xD36D32 | Signalfehler (Kamera Frontraumüberwachung, ID: CAM_HDWOBS) - Qualifier | 1 | - |
| 0xD36D33 | Botschaftsfehler (Kamera Frontraumüberwachung, ID: CAM_HDWOBS) - Alive | 1 | - |
| 0xD36D3A | Signalfehler (Kamera Frontraumüberwachung, ID: CAM_HDWOBS) - Ungültig | 1 | - |
| 0xD36D44 | Signalfehler (Status Verteilung Längsmoment Vorderachse Hinterachse, ID: ST_REPAT_XTRQ_FTAX_BAX) - Qualifier | 1 | - |
| 0xD36D54 | Signalfehler (Drehmoment Kurbelwelle 1, ID: TORQ_CRSH_1) - Qualifier | 1 | - |
| 0xD36D58 | Signalfehler (Radmoment Antrieb 1, ID: WMOM_DRV_1) - Qualifier | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 71 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x2800 | STAT_KL30_SPANNUNG_WERT | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x2801 | STAT_GESCHWINDIGKEIT_SCHWERPUNKT_WERT | km/h | High | unsigned char | - | 2.0 | 1.0 | -100.0 |
| 0x2802 | STAT_QUERBESCHLEUNIGUNG_SCHWERPUNKT_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x2803 | STAT_GIERRATE_SCHWERPUNKT_WERT | °/s | High | signed char | - | 1.0 | 0.77 | 0.0 |
| 0x2804 | STAT_EINGANG_SENSOR_FAHRERLENKWINKEL_WERT | ° | High | unsigned int | - | 1.0 | 23.0 | 0.0 |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2807 | STAT_SENSOR_QUERBESCHLEUNIGUNG_1_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2809 | STAT_SENSOR_GIERRATE_1_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280A | STAT_SENSOR_LAENGSBESCHLEUNIGUNG_1_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280B | STAT_FAHRERLENKWINKEL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280C | STAT_RADLENKWINKEL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280D | STAT_LAENGSBESCHLEUNIGUNG_SCHWERPUNKT_WERT | m/s² | High | signed char | - | 1.0 | 10.0 | 0.0 |
| 0x280E | STAT_IST_LENKWINKEL_FAHRER_WERT | ° | High | signed char | - | 1.0 | 15.0 | 0.0 |
| 0x280F | STAT_LENKWINKEL_VA_EFFEKTIV_WERT | rad | High | signed char | - | 1.0 | 75.0 | 0.0 |
| 0x2810 | STAT_SEITENNEIGUNG_WERT | HEX | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2811 | STAT_LAENGSGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 2.0 | 1.0 | -100.0 |
| 0x2812 | STAT_FAHRZUSTAND_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2813 | STAT_TOLERANZ_AUS_AX_ABGLEICH_WERT | m/s² | High | unsigned int | - | 1.0 | 50.0 | 0.0 |
| 0x2814 | STAT_EINGANG_SENSOR_QUERBESCHLEUNIGUNG_1_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x2815 | STAT_EINGANG_SENSOR_GIERRATE_1_WERT | rad/s | High | signed char | - | 1.0 | 44.0 | 0.0 |
| 0x2816 | STAT_EINGANG_SENSOR_LAENGSBESCHLEUNIGUNG_WERT | m/s² | High | signed char | - | 1.0 | 10.0 | 0.0 |
| 0x2817 | STAT_LENKWINKEL_FAHRER_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 8.0 | 0.0 |
| 0x2818 | STAT_REFERNZGESCHWINDIGKEIT_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2819 | STAT_EINGANG_SENSOR_QUERBESCHLEUNIGUNG_2_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x281A | STAT_EINGANG_SENSOR_GIERRATE_2_WERT | rad/s | High | signed char | - | 1.0 | 44.0 | 0.0 |
| 0x281B | STAT_LENKWINKEL_VA_AKTUATOR_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 8.0 | 0.0 |
| 0x281C | STAT_LENKWINKEL_HA_AKTUATOR_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 1200.0 | 0.0 |
| 0x283A | STAT_SIGNALTOLERANZ_QUERBESCHLEUNIGUNG_WERT | m/s² | High | unsigned char | - | 1.0 | 12.0 | 0.0 |
| 0x283B | STAT_SIGNALTOLERANZ_LAENGSBESCHLEUNIGUNG_WERT | m/s² | High | unsigned char | - | 1.0 | 12.0 | 0.0 |
| 0x283C | STAT_SIGNALTOLERANZ_GIERRATE_WERT | rad/s | High | unsigned char | - | 1.0 | 300.0 | 0.0 |
| 0x283D | STAT_SIGNALTOLERANZ_LENKWINKEL_WERT | rad | High | unsigned char | - | 1.0 | 1000.0 | 0.0 |
| 0x285F | URSAECHLICHER_FEHLER | HEX | High | unsigned int | - | - | - | - |
| 0x2860 | USP_KALTSTART_VORHANDEN | 0-n | High | 0xFF | TAB_JA_NEIN | - | - | - |
| 0x2861 | USP_MSA_START_VORHANDEN | 0-n | High | 0xFF | TAB_JA_NEIN | - | - | - |
| 0x2862 | USP_MOTOR_LAEUFT | 0-n | High | 0xFF | TAB_JA_NEIN | - | - | - |
| 0x2863 | USP_STATUS_GENERATORENTLASTUNG | 0-n | High | 0xFF | TAB_ENTLASTUNG_GENERATOR | - | - | - |
| 0x2864 | USP_GLOBALE_BITS_VERFUEGBAR | 0-n | High | 0xFF | TAB_JA_NEIN | - | - | - |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2876 | FAHRZEUGGESCHWINDIGKEIT_16BIT | m/s | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x2877 | WUNSCH_GESCHWINDIGKEIT_FAS_KMPH_ODER_MPH | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2878 | WUNSCH_ANTRIEBSMOMENT_FAS | Nm | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x2879 | WUNSCH_BREMSMOMENT_FAS | Nm | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x287A | ERROR_ID_FASCFI | 0-n | High | 0xFF | TAB_ERRID_FASCFI | - | - | - |
| 0x287B | ERROR_DUMP_32BIT_FASCFI | HEX | High | signed long | - | - | - | - |
| 0x287C | ERROR_ID_FASCFO | 0-n | High | 0xFF | TAB_ERRID_FASCFO | - | - | - |
| 0x287D | ERROR_DUMP_32BIT_FASCFO | HEX | High | signed long | - | - | - | - |
| 0x287E | ERROR_ID_FASCEBC | 0-n | High | 0xFF | TAB_ERRID_FASCEBC | - | - | - |
| 0x287F | ERROR_DUMP_32BIT_FASCEBC | HEX | High | signed long | - | - | - | - |
| 0x2880 | ERROR_ID_FASSCG | 0-n | High | 0xFF | TAB_ERRID_FASSCG | - | - | - |
| 0x2881 | ERROR_DUMP_32BIT_FASSCG | HEX | High | signed long | - | - | - | - |
| 0x2882 | ERROR_ID_FASCBAS | 0-n | High | 0xFF | TAB_ERRID_FASCBAS | - | - | - |
| 0x2883 | ERROR_DUMP_32BIT_FASCBAS | HEX | High | signed long | - | - | - | - |
| 0x5002 | STAT_FAHRZEUGZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5004 | STAT_ANTRIEBSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5008 | STAT_SPANNUNGSMASTER_VERFUEGBAR | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500B | STAT_FUNKTIONSZUSTAND | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500C | STAT_INTERNER_FUNKTIONSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500F | STAT_FEHLERSPEICHERSPERRE_AKTIV | 0/1 | High | 0x01 | - | - | - | - |
| 0x5010 | STAT_ROHDATEN_WERT | HEX | High | signed long | - | - | - | - |
| 0x5023 | STROM_MOTOR_L | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5024 | STROM_MOTOR_R | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5025 | NM_STATUS | 0-n | High | 0x0F | TAB_STATUS_NM | - | - | - |
| 0x5026 | BREMSENSTATUS_LINKS | 0-n | High | 0xF0 | TAB_BREMSENSTATUS_LINKS | - | - | - |
| 0x5027 | BREMSENSTATUS_RECHTS | 0-n | High | 0x0F | TAB_BREMSENSTATUS_RECHTS | - | - | - |
| 0x5028 | SCHALTERSTATUS | 0-n | High | 0xFF | TAB_SCHALTERSTATUS | - | - | - |
| 0x5029 | LETZTESBREMSENEVENT_LINKS | 0-n | High | 0xFF | TAB_LETZTESBREMSENEVENT_LINKS | - | - | - |
| 0x502A | LETZTESBREMSENEVENT_RECHTS | 0-n | High | 0xFF | TAB_LETZTESBREMSENEVENT_RECHTS | - | - | - |
| 0x502B | SHUTDOWNLEVEL | 0-n | High | 0x0F | TAB_SHUTDOWNLEVEL_OLD | - | - | - |
| 0x502C | MODE | 0-n | High | 0x0F | TAB_MODE_OLD | - | - | - |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

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

Dimensions: 134 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x030546 | QDM-SBS - Gierratensensor Signaltoleranz aufgrund Fehlerverdacht | 0 | - |
| 0x03054C | QDM-SBS - Lenkwinkel effektiv Signaltoleranz aufgrund Fehlerverdacht | 0 | - |
| 0x03054D | QDM-SBS - Lenkwinkel effektiv Signaltoleranz aufgrund Abgleichstoleranz | 0 | - |
| 0x03055D | QDM-SBS - Laengsbeschleunigungssensor Signaltoleranz aufgrund Fehlerverdacht | 0 | - |
| 0x03055F | QDM-SBS - Laengsbeschleunigungssensor Signaltoleranz aufgrund nicht ausgeführtem Werksmodus | 0 | - |
| 0x030570 | QDM-SBS - Querbeschleunigungssensor Signaltoleranz aufgrund Fehlerverdacht | 0 | - |
| 0x03058B | QDM-SBS - Aktiver Rollenmodus | 0 | - |
| 0x03059A | QDM-Aaeps - Aufgesetzt mittels Modellvergleich | 1 | - |
| 0x03059B | QDM-Aaeps - Aufgesetzt mittels Indexsignal | 1 | - |
| 0x03059C | QDM-Aaeps - Korrektur der Ist-Position EPS | 0 | - |
| 0x03059D | QDM-EV - VCH an oberer Lerngrenze | 0 | - |
| 0x03059E | QDM-EV - VCH an unterer Lerngrenze | 0 | - |
| 0x03059F | QDM-Aaeps - Aufgesetzt mittels Anschlag lenken | 1 | - |
| 0x0305A5 | QDM-QEI - Fehlertoleranz SBS zu hoch | 1 | - |
| 0x0305A6 | QDM-QEI - Fehlertoleranz FZB zu hoch | 1 | - |
| 0x0305A7 | QDM-QEI - Inputs nicht gültig SBS | 1 | - |
| 0x0305A8 | QDM-QEI - Inputs nicht gültig FZB | 1 | - |
| 0x0305A9 | QDM-QEI - eingeschränkte Modellgültigkeit | 1 | - |
| 0x0305AA | QDM-QEI - Plausibilisierungsfehler | 1 | - |
| 0x0305AB | QDM-QEI - Funktion oder Applikation nicht vorhanden | 1 | - |
| 0x0305AC | QDM-QEI - interne Degradation wegen SBS | 1 | - |
| 0x030640 | QDM-ZFM - Fahrtrichtung unsicher bei vx größer 2m/s | 0 | - |
| 0x030644 | QDM-ZFM - Signaltoleranz auf empfangenem Signal Ist-Lenkwinkel VA | 1 | - |
| 0x030645 | QDM-KOORFV - Zwangsaktivierung DSC | 1 | - |
| 0x030646 | QDM-LAEPS - Berechnung korregierte Längsbeschleunigung nicht möglich | 1 | - |
| 0x030647 | QDM-LAEPS - Berechnung Algorithmus Parken nicht möglich | 1 | - |
| 0x030648 | QDM-LAEPS - Berechnung Algorithmus Wenden nicht möglich | 1 | - |
| 0x030649 | QDM-LAEPS - Berechnung Extrapolation elektrische Leistung EPS nicht möglich | 1 | - |
| 0x03064A | QDM-LAEPS - Berechnung Extrapolation mechanische Leistung EPS nicht möglich | 1 | - |
| 0x03064B | QDM-LAEPS - Berechnung maximale Leistung EPS nicht möglich | 1 | - |
| 0x03064C | QDM-LAEPS - Berechnung LLP wegen fehlerhafter Geschwindigkeit nicht möglich | 1 | - |
| 0x030760 | FES Koordinator Innenraum Softwarefehler | 0 | - |
| 0x030807 | FAS - Funktionale Deaktivierung | 0 | - |
| 0x030808 | FAS - Antrieb - Betriebsbereitschaft | 1 | - |
| 0x030809 | FAS - Bremse - Betriebsbereitschaft | 1 | - |
| 0x03080C | FAS - Bedienfeld - HDC - fehlerhaft | 1 | - |
| 0x03080D | FAS - Inkorrekte Codierung Fahrfunktion | 1 | - |
| 0x03080E | FAS - KAFAS - Betriebsbereitschaft | 1 | - |
| 0x03080F | FAS - Abweichung VKombi gegen V-Ist zu groß | 1 | - |
| 0x030812 | FAS - Fahrzeugsenorik Betriebsbereitschaft | 1 | - |
| 0x030814 | FAS - pFGS - Verzögerungsanforderung | 0 | - |
| 0x030815 | FAS - CCM - Verzögerungsanforderung | 0 | - |
| 0x030816 | FAS - Antriebsaktuator - Betriebsbereitschaft | 1 | - |
| 0x030817 | FAS - Bremsaktuator - Betriebsbereitschaft | 1 | - |
| 0x030818 | FAS - Bedienung Lenkrad - Betriebsbereitschaft | 1 | - |
| 0x03081A | FAS - HDC - Betriebsbereitschaft | 1 | - |
| 0x03081B | FAS - Kombi - Betriebsbereitschaft | 0 | - |
| 0x03081C | FAS - Fehler Navigationsdaten | 0 | - |
| 0x03081E | FAS Signalfehler - Undefinierter Inhalt oder unzureichende Qualität | 1 | - |
| 0x03081F | FAS - Frontschutz - Akutwarnung ausgelöst | 0 | - |
| 0x030850 | FAS - Frontschutz - Anbremsen Stufe 1 ausgelöst | 0 | - |
| 0x030900 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 1 | 1 | - |
| 0x030901 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 2 | 1 | - |
| 0x030902 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 3 | 1 | - |
| 0x030903 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 4 | 1 | - |
| 0x030904 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 5 | 1 | - |
| 0x030905 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 6 | 1 | - |
| 0x030906 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 7 | 1 | - |
| 0x030907 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 8 | 1 | - |
| 0x030908 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 9 | 1 | - |
| 0x030909 | D-OBD 1 - ICM oder ACSM - Diagnosestatus 10 | 1 | - |
| 0x03090A | D-OBD 1 - ICM oder ACSM - Diagnosestatus 11 | 1 | - |
| 0x030B40 | D-OBD 3 - EPS - Diagnosestatus 1 | 1 | - |
| 0x030B41 | D-OBD 3 - EPS - Diagnosestatus 2 | 1 | - |
| 0x030B42 | D-OBD 3 - EPS - Diagnosestatus 3 | 1 | - |
| 0x030B43 | D-OBD 3 - EPS - Diagnosestatus 4 | 1 | - |
| 0x030B44 | D-OBD 3 - EPS - Diagnosestatus 5 | 1 | - |
| 0x030B45 | D-OBD 3 - EPS - Diagnosestatus 6 | 1 | - |
| 0x030B46 | D-OBD 3 - EPS - Diagnosestatus 7 | 1 | - |
| 0x030B47 | D-OBD 3 - EPS - Diagnosestatus 8 | 1 | - |
| 0x030B48 | D-OBD 3 - EPS - Diagnosestatus 9 | 1 | - |
| 0x030B49 | D-OBD 3 - EPS - Diagnosestatus 10 | 1 | - |
| 0x030B4A | D-OBD 3 - EPS - Diagnosestatus 11 | 1 | - |
| 0x030B4B | D-OBD 3 - EPS - Diagnosestatus 12 | 1 | - |
| 0x030B4C | D-OBD 3 - EPS - Diagnosestatus 13 | 1 | - |
| 0x030B4D | D-OBD 3 - EPS - Diagnosestatus 14 | 1 | - |
| 0x030B4E | D-OBD 3 - EPS - Diagnosestatus 15 | 1 | - |
| 0x030B4F | D-OBD 3 - EPS - Diagnosestatus 16 | 1 | - |
| 0x030B50 | D-OBD 3 - EPS - Diagnosestatus 17 | 1 | - |
| 0x030B51 | D-OBD 3 - EPS - Diagnosestatus 18 | 1 | - |
| 0x030B52 | D-OBD 3 - EPS - Diagnosestatus 19 | 1 | - |
| 0x030B53 | D-OBD 3 - EPS - Diagnosestatus 20 | 1 | - |
| 0x030B54 | D-OBD 3 - EPS - Diagnosestatus 21 | 1 | - |
| 0x030B55 | D-OBD 3 - EPS - Diagnosestatus 22 | 1 | - |
| 0x030B56 | D-OBD 3 - EPS - Diagnosestatus 23 | 1 | - |
| 0x030B57 | D-OBD 3 - EPS - Diagnosestatus 24 | 1 | - |
| 0x030B58 | D-OBD 3 - EPS - Diagnosestatus 25 | 1 | - |
| 0x030B59 | D-OBD 3 - EPS - Diagnosestatus 26 | 1 | - |
| 0x030B5A | D-OBD 3 - EPS - Diagnosestatus 27 | 1 | - |
| 0x030B5B | D-OBD 3 - EPS - Diagnosestatus 28 | 1 | - |
| 0x030B5C | D-OBD 3 - EPS - Diagnosestatus 29 | 1 | - |
| 0x480694 | Peripherial/Funktional error Schnittstelle QDM Ist Lenkwinkel Vorderachse Signal ungültig | 0 | - |
| 0x480695 | Peripherial/Funktional error Schnittstelle QDM Giergeschwindigkeit Fahrzeug Signal ungültig | 0 | - |
| 0x480699 | Peripherial/Funktional error Schnittstelle QDM Querbeschleunigung Schwerpunkt Signal ungültig | 0 | - |
| 0x48069A | Peripherial/Funktional error Schnittstelle QDM Längsbeschleunigung Schwerpunkt Signal ungültig | 0 | - |
| 0x480736 | EPBi - Aktuator - IPB_HIGH_CURRENT_ACTING_RL | 0 | - |
| 0x480737 | EPBi - Aktuator - IPB_HIGH_CURRENT_ACTING_RR | 0 | - |
| 0x480738 | EPBi - Aktuator - IPB_HIGH_FREE_RUN_CURR_RL | 0 | - |
| 0x480739 | EPBi - Aktuator - IPB_HIGH_FREE_RUN_CURR_RR | 0 | - |
| 0x48073A | EPBi - Aktuator - IPB_CLAMP_POW_LOSS_RL | 0 | - |
| 0x48073B | EPBi - Aktuator - IPB_CLAMP_POW_LOSS_RR | 0 | - |
| 0x48073C | EPBi - Aktuator - IPB_RELEASE_POW_LOSS_RL | 0 | - |
| 0x48073D | EPBi - Aktuator - IPB_RELEASE_POW_LOSS_RR | 0 | - |
| 0x48073E | EPBi - Aktuator - IPB_RELEASE_STNDSTL_RL | 0 | - |
| 0x48073F | EPBi - Aktuator - IPB_RELEASE_STNDSTL_RR | 0 | - |
| 0x480740 | EPBi - Aktuator - IPB_ACT_IRREG_CLAMP_CURR_RL | 0 | - |
| 0x480741 | EPBi - Aktuator - IPB_ACT_IRREG_CLAMP_CURR_RR | 0 | - |
| 0x480742 | EPBi - Aktuator - IPB_ACT_IRREG_RELEAS_CURR_RL | 0 | - |
| 0x480743 | EPBi - Aktuator - IPB_ACT_IRREG_RELEAS_CURR_RR | 0 | - |
| 0x48075A | EPBi - IPB_ESC_HDBF_AVAILABLE_MISSING | 0 | - |
| 0x48075B | EPBi - IPB_ESC_DDBF_AVAILABLE_MISSING | 0 | - |
| 0x48075C | EPBi - IPB_ESC_HDBF_RESPONCE_MISSING | 0 | - |
| 0x48075D | EPBi - IPB_ESC_DDBF_RESPONCE_MISSING | 0 | - |
| 0x48075E | EPBi Missbrauch durch Fahrer erkannt | 0 | - |
| 0x480761 | EPBi -Fahrzeug rollt trotz nachspannen | 0 | - |
| 0x48076A | EPBi H-Brücke - IPB_HBRSV_PASSIVE_INTERN_RL | 0 | - |
| 0x48076B | EPBi H-Brücke - IPB_HBRSV_PASSIVE_INTERN_RR | 0 | - |
| 0x48076C | EPBi H-Brücke - IPB_TEMP WARNING_REC FET | 0 | - |
| 0x48076D | EPBi H-Brücke - IPB_OVERTEMP_RECFET | 0 | - |
| 0x48076E | EPBi H-Brücke - IPB_OVERLOAD_RECFET | 0 | - |
| 0x48076F | EPBi H-Brücke - IPB_SENSORTEMP_RECFET | 0 | - |
| 0x480770 | EPBi H-Brücke - IPB_KL30V_RECFET | 0 | - |
| 0x48077B | EPBi - Ausfall dynamische Abbremsung | 0 | - |
| 0x48079A | Peripherial/Funktional error Schnittstelle QDM Anforderung Bremsmoment Summe Signal ungültig | 0 | - |
| 0x4807BE | Fahrleistungsreduzierung - Fahrleistungsreduzierung durch DSC-Befehl aktiv | 0 | - |
| 0x48083A | EPBi Bremstemperaturmodell - Lernphase aktiv | 0 | - |
| 0x48086D | Fehler Schnittstelle intern - WBK/ HDC | 0 | - |
| 0x480881 | Internes Zustandsmanagement Kompletter Überwachungsumfang | 0 | - |
| 0x480884 | EPBi Aktuator Stellvorgang nicht umgesetzt | 0 | - |
| 0x4809C0 | Lokale Spannungsversorgung - Steuergeräte Reset | 0 | - |
| 0x480A19 | Allradkupplung LMV Schutzfunktion aktiv | 0 | - |
| 0x480B56 | Handbremskontakt - Handbremskontakt bei Fahrt aktiv | 1 | - |
| 0x480B5D | EPBi - Externe Anziehen-Anforderung | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-ipb-led-zustand"></a>
### IPB_LED_ZUSTAND

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | IPB LED aus |
| 1 | IPB LED an |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 122 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | AX_KORR - Längsbeschleunigung fehlerhaft | 0-n | High | 0x80000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0002 | AX_KORR - Längsneigung fehlerhaft | 0-n | High | 0x40000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0003 | STOP - Geschwindigkeit fehlerhaft | 0-n | High | 0x20000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0004 | STOP - Ritzelwinkel fehlerhaft | 0-n | High | 0x10000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0005 | STOP - Fahrtrichtungswunsch fehlerhaft | 0-n | High | 0x08000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0006 | STOP - Istleistung EPS fehlerhaft | 0-n | High | 0x04000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0007 | RETURN - Geschwindigkeit fehlerhaft | 0-n | High | 0x02000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0008 | RETURN - Ritzelwinkel fehlerhaft | 0-n | High | 0x01000000 | EINZELFEHLER_BIT | - | - | - |
| 0x0009 | RETURN - Winkel Fahrpedal fehlerhaft | 0-n | High | 0x00800000 | EINZELFEHLER_BIT | - | - | - |
| 0x000A | RETURN - Längsbeschleunigung fehlerhaft | 0-n | High | 0x00400000 | EINZELFEHLER_BIT | - | - | - |
| 0x000B | EXTRAP_PEL - Istleistung EPS fehlerhaft | 0-n | High | 0x00200000 | EINZELFEHLER_BIT | - | - | - |
| 0x000C | EXTRAP_FZS - Fahrerhandmoment fehlerhaft | 0-n | High | 0x00100000 | EINZELFEHLER_BIT | - | - | - |
| 0x000D | EXTRAP_FZS - Ritzelwinkel fehlerhaft | 0-n | High | 0x00080000 | EINZELFEHLER_BIT | - | - | - |
| 0x000E | EXTRAP_FZS - Zahnstangenkraft fehlerhaft | 0-n | High | 0x00040000 | EINZELFEHLER_BIT | - | - | - |
| 0x000F | FZSREDUC_BRAKE - Bremsmoment VL fehlerhaft | 0-n | High | 0x00020000 | EINZELFEHLER_BIT | - | - | - |
| 0x0010 | FZSREDUC_BRAKE - Bremsmoment VR fehlerhaft | 0-n | High | 0x00010000 | EINZELFEHLER_BIT | - | - | - |
| 0x0011 | FZSREDUC_BRAKE - Status Bremsung fehlerhaft | 0-n | High | 0x00008000 | EINZELFEHLER_BIT | - | - | - |
| 0x0012 | VX - Geschwindigkeit fehlerhaft | 0-n | High | 0x00002000 | EINZELFEHLER_BIT | - | - | - |
| 0x0013 | EXTRAP_FZS - Hub fehlerhaft | 0-n | High | 0x00001000 | EINZELFEHLER_BIT | - | - | - |
| 0x0014 | EXTRAP_FZS - Einheit Position EPS fehlerhaft | 0-n | High | 0x00000800 | EINZELFEHLER_BIT | - | - | - |
| 0x0015 | Ausfall DSC | 0/1 | High | 0x80 | - | - | - | - |
| 0x0016 | Ausfall ASC | 0/1 | High | 0x40 | - | - | - | - |
| 0x0017 | Ausfall VDC | 0/1 | High | 0x20 | - | - | - | - |
| 0x0018 | Ausfall LMV | 0/1 | High | 0x10 | - | - | - | - |
| 0x0019 | Aktiver Heckspoiler | 0/1 | High | 0x08 | - | - | - | - |
| 0x001A | Reifendruckverlust | 0/1 | High | 0x04 | - | - | - | - |
| 0x001B | State of Charge low | 0/1 | High | 0x02 | - | - | - | - |
| 0x001C | Reserve_7 | 0/1 | High | 0x01 | - | - | - | - |
| 0x001D | Rollenmodus | 0/1 | High | 0x80 | - | - | - | - |
| 0x001E | Motorstart | 0/1 | High | 0x40 | - | - | - | - |
| 0x001F | Reserve_2 | 0/1 | High | 0x20 | - | - | - | - |
| 0x0020 | Reserve_3 | 0/1 | High | 0x10 | - | - | - | - |
| 0x0021 | Reserve_4 | 0/1 | High | 0x08 | - | - | - | - |
| 0x0022 | Reserve_5 | 0/1 | High | 0x04 | - | - | - | - |
| 0x0023 | Reserve_6 | 0/1 | High | 0x02 | - | - | - | - |
| 0x0024 | Reserve_7 | 0/1 | High | 0x01 | - | - | - | - |
| 0x2800 | STAT_KL30_SPANNUNG_WERT | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x2801 | STAT_GESCHWINDIGKEIT_SCHWERPUNKT_WERT | km/h | High | unsigned char | - | 2.0 | 1.0 | -100.0 |
| 0x2802 | STAT_QUERBESCHLEUNIGUNG_SCHWERPUNKT_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x2803 | STAT_GIERRATE_SCHWERPUNKT_WERT | °/s | High | signed char | - | 1.0 | 0.77 | 0.0 |
| 0x2804 | STAT_EINGANG_SENSOR_FAHRERLENKWINKEL_WERT | ° | High | unsigned int | - | 1.0 | 23.0 | 0.0 |
| 0x2805 | STAT_AUSSENTEMPERATUR_WERT | °C | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2806 | STAT_QUERBESCHLEUNIGUNGSNUTZSIGNAL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2808 | STAT_GIERRATENNUTZSIGNAL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280A | STAT_SENSOR_LAENGSBESCHLEUNIGUNG_1_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280B | STAT_FAHRERLENKWINKEL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280C | STAT_RADLENKWINKEL_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x280D | STAT_LAENGSBESCHLEUNIGUNG_SCHWERPUNKT_WERT | m/s² | High | signed char | - | 1.0 | 10.0 | 0.0 |
| 0x280E | STAT_IST_LENKWINKEL_FAHRER_WERT | ° | High | signed char | - | 1.0 | 15.0 | 0.0 |
| 0x2812 | STAT_FAHRZUSTAND_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2814 | STAT_EINGANG_SENSOR_QUERBESCHLEUNIGUNG_1_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x2815 | STAT_EINGANG_SENSOR_GIERRATE_1_WERT | rad/s | High | signed char | - | 1.0 | 44.0 | 0.0 |
| 0x2816 | STAT_EINGANG_SENSOR_LAENGSBESCHLEUNIGUNG_WERT | m/s² | High | signed char | - | 1.0 | 10.0 | 0.0 |
| 0x2817 | STAT_LENKWINKEL_FAHRER_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 8.0 | 0.0 |
| 0x2819 | STAT_EINGANG_SENSOR_QUERBESCHLEUNIGUNG_2_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x281A | STAT_EINGANG_SENSOR_GIERRATE_2_WERT | rad/s | High | signed char | - | 1.0 | 44.0 | 0.0 |
| 0x281B | STAT_LENKWINKEL_VA_AKTUATOR_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 8.0 | 0.0 |
| 0x281C | STAT_LENKWINKEL_HA_AKTUATOR_TEILAUFBEREITET_WERT | rad | High | signed char | - | 1.0 | 1200.0 | 0.0 |
| 0x2825 | STAT_GESAMTSTATUS_SCHWIMMWINKELSCHAETZER_WERT | HEX | High | signed long | - | - | - | - |
| 0x2826 | STAT_INFORMATION_SCHWIMMWINKELSCHAETZER_WERT | HEX | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x2827 | STAT_SCHWIMMWINKEL_WERT | ° | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2828 | STAT_SCHWIMMWINKEL_SIGNALTOLERANZ_WERT | ° | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2829 | STAT_QUERGESCHWINDIGKEIT_WERT | km/h | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x282A | STAT_QUERGESCHWINDIGKEIT_SIGNALTOLERANZ_WERT | km/h | High | unsigned char | - | 1.0 | 2.0 | 0.0 |
| 0x282B | STAT_SCHWIMMWINKELGESCHWINDIGKEIT_WERT | °/s | High | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x282C | STAT_SCHWIMMWINKELGESCHWINDIGKEIT_SIGNALTOLERANZ_WERT | °/s | High | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x282D | STAT_LERNWERT_BEIDE_KURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x282E | STAT_LERNWERT_LINKSKURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x282F | STAT_LERNWERT_RECHTSKURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2830 | STAT_LERNINTERVALL_BEIDE_KURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2831 | STAT_LERNINTERVALL_LINKSKURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2832 | STAT_LERNINTERVALL_RECHTSKURVEN_WERT | HEX | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2833 | STAT_LERNALGO_WERT | HEX | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0x2834 | STAT_LENKWINKELOFFSET_WERT | rad | High | signed char | - | 1.0 | 500.0 | 0.0 |
| 0x2835 | STAT_LENKWINKELOFFSET_TOLERANZ_WERT | rad | High | unsigned char | - | 1.0 | 500.0 | 0.0 |
| 0x2836 | STAT_ZAHNSTANGENKRAFT_WERT | kN | High | unsigned char | - | 1.0 | 5.0 | -20.0 |
| 0x2837 | STAT_ZAHNSTANGENGESCHWINDIGKEIT_WERT | m/s | High | unsigned char | - | 1.0 | 200.0 | -0.5 |
| 0x2838 | STAT_ISTLEISTUNG_EPS_WERT | kW | High | unsigned char | - | 1.0 | 10.0 | -12.0 |
| 0x2839 | STAT_PRAEDIZIERTE_LEISTUNG_EPS_WERT | kW | High | unsigned char | - | 1.0 | 10.0 | -12.0 |
| 0x283A | STAT_SIGNALTOLERANZ_QUERBESCHLEUNIGUNG_WERT | m/s² | High | unsigned char | - | 1.0 | 12.0 | 0.0 |
| 0x283B | STAT_SIGNALTOLERANZ_LAENGSBESCHLEUNIGUNG_WERT | m/s² | High | unsigned char | - | 1.0 | 12.0 | 0.0 |
| 0x283C | STAT_SIGNALTOLERANZ_GIERRATE_WERT | rad/s | High | unsigned char | - | 1.0 | 300.0 | 0.0 |
| 0x283D | STAT_SIGNALTOLERANZ_LENKWINKEL_WERT | rad | High | unsigned char | - | 1.0 | 1000.0 | 0.0 |
| 0x2840 | Sub-Tabelle | 0-n | - | 0xFFFFFFFF | - | - | - | - |
| 0x2858 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x2859 | Sub-Tabelle | 0/1 | - | 0xFF | - | - | - | - |
| 0x285A | STAT_IST_MODUS_SCHALTER_FAHRERLEBNIS | 0-n | High | 0xFF | TAB_FAHRERLEBNIS_MODUS | - | - | - |
| 0x285B | STAT_ANFORDERUNG_MODUS_WECHSEL | 0-n | High | 0xFF | TAB_FAHRERLEBNIS_MODUS | - | - | - |
| 0x285C | STAT_FILTER_MODUS_WECHSEL | 0-n | High | 0xFF | TAB_FAHRERLEBNIS_FILTER | - | - | - |
| 0x285D | STAT_INDIVIDUALISIERTE_AUSPRAEGUNG_SPORTMODUS_WERT | HEX | High | unsigned int | - | - | - | - |
| 0x2866 | STAT_BETRIEBSSPANNUNG_WERT | V | High | unsigned char | - | 8.0 | 100.0 | 0.0 |
| 0x2867 | STAT_FAHRZEUGGESCHWINDIGKEIT_WERT | km/h | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2868 | STAT_GESCHWINDIGKEIT_BEI_GROBOFFSET_WERT | km/h | High | unsigned char | - | 2.0 | 1.0 | -100.0 |
| 0x2869 | STAT_MAX_GESCHWINDIGKEIT_AUFSETZVORGANG_WERT | km/h | High | unsigned char | - | 2.0 | 1.0 | -100.0 |
| 0x286A | STAT_MAX_QUERBESCHLEUNIGUNG_AUFSETZVORGANG_WERT | m/s² | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x286B | STAT_KORREKTUR_MULTITURNS_WERT | - | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x2876 | FAHRZEUGGESCHWINDIGKEIT_16BIT | m/s | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x2877 | WUNSCH_GESCHWINDIGKEIT_FAS_KMPH_ODER_MPH | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x2878 | WUNSCH_ANTRIEBSMOMENT_FAS | Nm | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x2879 | WUNSCH_BREMSMOMENT_FAS | Nm | High | signed int | - | 1.0 | 1.0 | 0.0 |
| 0x287A | ERROR_ID_FASCFI | 0-n | High | 0xFF | TAB_ERRID_FASCFI | - | - | - |
| 0x287B | ERROR_DUMP_32BIT_FASCFI | HEX | High | signed long | - | - | - | - |
| 0x2886 | ERROR_ID_FASDSP | 0-n | High | 0xFF | TAB_ERRID_FASDSP | - | - | - |
| 0x2887 | ERROR_DUMP_32BIT_FASDSP | HEX | High | signed long | - | - | - | - |
| 0x5002 | STAT_FAHRZEUGZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5004 | STAT_ANTRIEBSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5008 | STAT_SPANNUNGSMASTER_VERFUEGBAR | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500B | STAT_FUNKTIONSZUSTAND | HEX | - | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x500C | STAT_INTERNER_FUNKTIONSZUSTAND | HEX | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x500F | STAT_FEHLERSPEICHERSPERRE_AKTIV | 0/1 | High | 0x01 | - | - | - | - |
| 0x5023 | STROM_MOTOR_L | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5024 | STROM_MOTOR_R | A | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x5025 | NM_STATUS | 0-n | High | 0x0F | TAB_STATUS_NM | - | - | - |
| 0x5026 | BREMSENSTATUS_LINKS | 0-n | High | 0xF0 | TAB_BREMSENSTATUS_LINKS | - | - | - |
| 0x5027 | BREMSENSTATUS_RECHTS | 0-n | High | 0x0F | TAB_BREMSENSTATUS_RECHTS | - | - | - |
| 0x5028 | SCHALTERSTATUS | 0-n | High | 0xFF | TAB_SCHALTERSTATUS | - | - | - |
| 0x5029 | LETZTESBREMSENEVENT_LINKS | 0-n | High | 0xFF | TAB_LETZTESBREMSENEVENT_LINKS | - | - | - |
| 0x502A | LETZTESBREMSENEVENT_RECHTS | 0-n | High | 0xFF | TAB_LETZTESBREMSENEVENT_RECHTS | - | - | - |
| 0x502B | SHUTDOWNLEVEL | 0-n | High | 0x0F | TAB_SHUTDOWNLEVEL_OLD | - | - | - |
| 0x502C | MODE | 0-n | High | 0x0F | TAB_MODE_OLD | - | - | - |
| 0xD62E | FES_COORDINT_SW_FEHLER_INFO | - | High | signed long | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0x1061-r"></a>
### RES_0X1061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_ENDE_WABL | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Verriegelt (loeschen von Einzelfehlern und PDTCs wird unterbunden) 1: Entriegelt (loeschen von Einzelfehlern und PDTCs wird nicht unterbunden) |

<a id="table-res-0xa051-r"></a>
### RES_0XA051_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | + | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xa052-r"></a>
### RES_0XA052_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xa053-r"></a>
### RES_0XA053_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | + | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xa05b-r"></a>
### RES_0XA05B_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | + | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_DATEN_SCHREIBEN_AKTIV_NR | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Information ob der Schreibvorgang der Adaptivdaten läuft. |

<a id="table-res-0xa061-r"></a>
### RES_0XA061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xa064-r"></a>
### RES_0XA064_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

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

<a id="table-res-0xa066-r"></a>
### RES_0XA066_R

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_ABFALL_ZEIT_1_WERT | - | - | + | ms | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Druckabfall Bremskreis 1 (Vorderachse) |
| STAT_ABFALL_ZEIT_2_WERT | - | - | + | ms | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Druckabfall Bremskreis 2 (Hinterachse) |
| STAT_ABFALL_ZEIT_3_WERT | - | - | + | ms | - | unsigned char | - | - | 10.0 | 1.0 | 0.0 | Druckabfall Bremskreis 1 und 2 (Vorderachse und Hinterachse) |

<a id="table-res-0xa067-r"></a>
### RES_0XA067_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_FEHLER_DETAIL | - | - | + | 0-n | - | unsigned char | - | TAB_BPWS_DETAIL_INITIALISIERUNG | - | - | - | Fehler Detail |

<a id="table-res-0xa06d-r"></a>
### RES_0XA06D_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xa08f-r"></a>
### RES_0XA08F_R

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_VENTILE_KALIBRIERUNG_1 | - | - | + | 0-n | high | unsigned char | - | TAB_VENTILE_KALIBRIERUNG_1 | - | - | - | STAT_VENTILE_KALIBRIERUNG_1 |
| STAT_VENTILE_KALIBRIERUNG_2 | - | - | + | 0-n | high | unsigned char | - | TAB_VENTILE_KALIBRIERUNG_2 | - | - | - | STAT_VENTILE_KALIBRIERUNG_2 |
| STAT_VENTILE_KALIBRIERUNG_3 | - | - | + | 0-n | high | unsigned char | - | TAB_VENTILE_KALIBRIERUNG_3 | - | - | - | STAT_VENTILE_KALIBRIERUNG_3 |

<a id="table-res-0xa123-r"></a>
### RES_0XA123_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_IPB_LED_ZUSTAND | - | - | + | 0-n | high | unsigned char | - | IPB_LED_ZUSTAND | - | - | - | 0- LED aus, 1-LED an |

<a id="table-res-0xa130-r"></a>
### RES_0XA130_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FLM_RESET | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ROUTINE | - | - | - | Ausführungsstatus |

<a id="table-res-0xa193-r"></a>
### RES_0XA193_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ROUTINE | - | - | - | Ausführungsstatus |

<a id="table-res-0xa222-r"></a>
### RES_0XA222_R

Dimensions: 4 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ROUTINE | - | - | - | Ausführungsstatus |
| STAT_PUMPENLEISTUNG_LEERLAUF_WERT | - | - | + | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Pumpenleistung während Kreisförderung (Leerlauf ohne Wiederstand, kein aktiver Bremsdruckaufbau) |
| STAT_PUMPENLEISTUNG_KREIS_1_WERT | - | - | + | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Pumpenleistung während Belastung gegen das Trennventil im primären Bremskreis |
| STAT_PUMPENLEISTUNG_KREIS_2_WERT | - | - | + | % | high | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Pumpenleistung während Belastung gegen das Trennventil im sekundären Bremskreis |

<a id="table-res-0xa803-r"></a>
### RES_0XA803_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |

<a id="table-res-0xab5b-r"></a>
### RES_0XAB5B_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | + | - | + | 0-n | - | unsigned char | - | TAB_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus |
| STAT_EEPROM_SICHERN_NR | - | - | + | 0-n | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status der EEPROM Sicherung  0=Sicherung erfolgreich 1= Sicherung läuft |

<a id="table-res-0xaba3-r"></a>
### RES_0XABA3_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | + | - | + | 0-n | high | unsigned char | - | TAB_STATUS_ROUTINE | - | - | - | Ausführungsstatus |

<a id="table-res-0xd09a-d"></a>
### RES_0XD09A_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZUSTAND_IST_GMK_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ist-Zustand der GMK-Funktion (abhängig von Qualifiern der Eingänge) |
| STAT_ZUSTAND_SOLL_GMK_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Soll-Zustand der GMK-Funktion |
| STAT_MMOTOR_OFFSET_EPS_WERT | Nm | high | signed char | - | - | 1.0 | 100.0 | 0.0 | Offset-Motormoment, das die EPS dem eigenen Motormoment additiv überlagert |
| STAT_OFFSET_EPS_QUALIFIER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Sollwert-Qualifier zum OffsetMotormoment (2 = umsetzen; 14 = nicht umsetzen) |
| STAT_FUNKTION_GMK_CODIERUNG_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | GMK-Funktion (1 = eincodiert; 0 = auscodiert) |
| STAT_MMOTOR_OFFSET_GMK_EPS_WERT | Nm | high | signed char | - | - | 1.0 | 100.0 | 0.0 | Offset-Motormoment, welches die EPS aufgrund der GMK Funktion zu stellen hat |
| STAT_LENKUNG_VERBAUT_FAHRZEUG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Datensatz EPS ohne IAS (1..ja,0..nein) |
| STAT_EPS_FAKT_MOM_SERVICE_QUALIFIER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Service-Qualifier der EPS für Umsetzung der Faktoren und des Offset-Motormoments (alles i.O wenn 32 od 33) |
| STAT_FUNKTION_GBR_KENNLINIE_NUMMER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aktiver GBR Kennliniensatz |

<a id="table-res-0xd0d2-d"></a>
### RES_0XD0D2_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WEG_IST_SENSOR1_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedalweg (bezogen auf WEG_NULLPUNKT_IST) |
| STAT_WEG_NULLPUNKT_INIT_SENSOR1_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Initialisierung Pedal Nullpunkt |
| STAT_WEG_NULLPUNKT_IST_SENSOR1_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Nullpunkt |
| STAT_WEG_LEERWEG_IST_SENSOR1_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Leerweg (Einsatz Hydraulik bezogen auf WEG_NULLPUNKT_IST) |
| STAT_WEG_NULLPUNKT_INIT_SENSOR2_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Initialisierung Pedal Nullpunkt |
| STAT_WEG_NULLPUNKT_IST_SENSOR2_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Nullpunkt |
| STAT_WEG_LEERWEG_IST_SENSOR2_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Leerweg (Einsatz Hydraulik bezogen auf WEG_NULLPUNKT_IST) |

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

<a id="table-res-0xd6d6-d"></a>
### RES_0XD6D6_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FLM_1_DATA | DATA | high | data[200] | - | - | 1.0 | 1.0 | 0.0 | Alle FLM Daten Teil 1 |
| STAT_FLM_2_DATA | DATA | high | data[200] | - | - | 1.0 | 1.0 | 0.0 | Alle FLM Daten Teil 2 |
| STAT_FLM_3_DATA | DATA | high | data[200] | - | - | 1.0 | 1.0 | 0.0 | Alle FLM Daten Teil 3 |
| STAT_FLM_4_DATA | DATA | high | data[211] | - | - | 1.0 | 1.0 | 0.0 | Alle FLM Daten Teil 4 |

<a id="table-res-0xd804-d"></a>
### RES_0XD804_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_FESTELLEN_STEIGUNG20_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Feststellen Steigung &gt; 20 % |
| STAT_ZAEHLER_NACHSPANNEN_ROLLUEBERWACHUNG_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Nachspannen wegen Rollen erkannt |
| STAT_ZAEHLER_NACHSPANNEN_TEMPERATUR_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Nachspannen wegen Temperatur Bremsscheibe |
| STAT_ZAEHLER_AUTO_ADJUST_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl automatische Justage |
| STAT_ZAEHLER_NACHSPANNEN_PRAEVENTIV_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Nachspannen vorbeugend |
| STAT_RESERVE5_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | unbenutzt |
| STAT_RESERVE6_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | unbenutzt |
| STAT_RESERVE7_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | unbenutzt |
| STAT_RESERVE8_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | unbenutzt |
| STAT_RESERVE9_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | unbenutzt |

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
| STAT_HU_MODE_STATUS | 0-n | - | unsigned char | - | TAB_EMF_HU_MODE | 1.0 | 1.0 | 0.0 | Status Modus Hauptuntersuchung |

<a id="table-res-0xd808-d"></a>
### RES_0XD808_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_TASTER_FESTSTELLEN_WERT | - | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Bedienung Feststellen |
| STAT_ZAEHLER_TASTER_LOESEN_WERT | - | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Bedienungen Lösen |

<a id="table-res-0xd80a-d"></a>
### RES_0XD80A_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_AKTUATOR_FESTSTELLEN_WERT | - | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Feststellen |
| STAT_ZAEHLER_AKTUATOR_NOTENTRIEGELN_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Notentriegelung |
| STAT_ZAEHLER_AKTUATOR_BOOST_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Nachstellen |
| STAT_ZAEHLER_AKTUATOR_UEBERLAST_WERT | - | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Überlast |

<a id="table-res-0xd80c-d"></a>
### RES_0XD80C_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_ELEKTRONIK_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Steuergerät |
| STAT_SPANNUNG_AKUATOR_HL_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Aktuator hinten links |
| STAT_SPANNUNG_AKUATOR_HR_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Aktuator hinten rechts |
| STAT_SPANNUNG_WECKLEITUNG_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Weckleitung |

<a id="table-res-0xd80d-d"></a>
### RES_0XD80D_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_EMF | 0-n | - | unsigned char | - | TAB_EMF_TASTER | - | - | - | Bedienzustand |
| STAT_TASTER_EMF_DIGITAL_WERT | - | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | digitaler Status Taster |
| STAT_TASTER_EMF_1_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Taster Leitung 1 |
| STAT_TASTER_EMF_2_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Taster Leitung 2 |
| STAT_TASTER_EMF_3_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Taster Leitung 3 |
| STAT_TASTER_EMF_4_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Taster Leitung 4 |
| STAT_TASTER_EMF_5_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Taster Leitung 5 |

<a id="table-res-0xd80f-d"></a>
### RES_0XD80F_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MODE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = aktiv; 0 = nicht aktiv |

<a id="table-res-0xdbd9-d"></a>
### RES_0XDBD9_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GIERRATE_SENSOR_WERT | °/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Gierrate. Gemittelter Wert aus SBS für Sensor 1 und 2. |
| STAT_GIERRATE_SENSOR_NR | 0-n | - | unsigned int | - | TAB_SBS_GUELTIGKEIT_UINT | - | - | - | Plausibilisierung Sensor |

<a id="table-res-0xdbda-d"></a>
### RES_0XDBDA_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_QUERBESCHLEUNIGUNG_SENSOR_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Querbeschleunigung (Gemittelter Wert Sensor 1 und 2) |
| STAT_QUERBESCHLEUNIGUNG_SENSOR_NR | 0-n | - | unsigned int | - | TAB_SBS_GUELTIGKEIT_UINT | - | - | - | Plausibilisierung Sensor |

<a id="table-res-0xdbdb-d"></a>
### RES_0XDBDB_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LAENGSBESCHLEUNIGUNG_SENSOR1_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Längsbeschleunigung Sensor 1 |
| STAT_LAENGSBESCHLEUNIGUNG_SENSOR1_NR | 0-n | - | unsigned int | - | TAB_SBS_GUELTIGKEIT_UINT | - | - | - | Plausibilisierung Sensor 1 |

<a id="table-res-0xdbdf-d"></a>
### RES_0XDBDF_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PILLE_VA | 0-n | - | unsigned char | - | TAB_BBV_SENSOR | 1.0 | 1.0 | 0.0 | Bremsbelagspille Vorderachse |
| STAT_PILLE_HA | 0-n | - | unsigned char | - | TAB_BBV_SENSOR | 1.0 | 1.0 | 0.0 | Bremsbelagspille Hinterachse |

<a id="table-res-0xdbe1-d"></a>
### RES_0XDBE1_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LMV_FUNKTION_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = aktiv;  0 = inaktiv |

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

<a id="table-res-0xdbe5-d"></a>
### RES_0XDBE5_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DRUCK_KREIS1_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck Kreis 1 LG, 35up, LG-X: Bremsvordruck;  LU/LI: Bremsvordruck (THZ-Tandem-Hauptbremszylinder) |
| STAT_DRUCK_KREIS2_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck Kreis 2 |
| STAT_DRUCK_VL_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck vorne links LG, 35up, LG-X: Kreis1 (VA);  I12/F4xPHEV Kreis1 (VL/HR);  UKL/I01 unbelegt |
| STAT_DRUCK_VR_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck vorne rechts LG, 35up, LG-X, LU/LI: unbelegt |
| STAT_DRUCK_HL_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck hinten links LG, 35up, LG-X: Kreis2 (HA);  I12/F4xPHEV Kreis2 (VR/HL);  UKL/I01 unbelegt |
| STAT_DRUCK_HR_WERT | bar | - | signed int | - | - | 1.0 | 10.0 | 0.0 | Druck hinten rechts LG, 35up, LG-X, LU/LI: unbelegt |

<a id="table-res-0xdbe7-d"></a>
### RES_0XDBE7_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_ELEKTRONIK_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Elektronikversorgung |
| STAT_SPANNUNG_PUMPE_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Pumpenversorgung |
| STAT_SPANNUNG_VENTILE_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Ventilversorgung |
| STAT_SPANNUNG_WECKLEITUNG_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | Spannung Weckleitung |

<a id="table-res-0xdbe8-d"></a>
### RES_0XDBE8_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PUMPE_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 1 = ein; 0 = aus |

<a id="table-res-0xdbe9-d"></a>
### RES_0XDBE9_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EINLASSVENTIL_VL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlassventil vorne links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_EINLASSVENTIL_VR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlassventil vorne rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) ESPPremium: Vorladeventil HA (HSV 2) ESPhev: Seperationsventil HA (SV) |
| STAT_EINLASSVENTIL_HL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlassventil hinten links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_EINLASSVENTIL_HR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Einlassventil hinten rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) ESPPremium: Trennventil VA (USV 2) ESPhev: Druckregelventil VA (PCR) |
| STAT_AUSLASSVENTIL_VL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Auslassventil vorne links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_AUSLASSVENTIL_VR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Auslassventil vorne rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_AUSLASSVENTIL_HL_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Auslassventil hinten links (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_AUSLASSVENTIL_HR_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Auslassventil hinten rechts (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_VORLADEVENTIL_VA_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorladeventil Vorderachse (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_VORLADEVENTIL_HA_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorladeventil Hinterachse (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_TRENNVENTIL_VA_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Trennventil Vorderachse (0 % = nicht angesteuert; 100 % = voll angesteuert) |
| STAT_TRENNVENTIL_HA_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Trennventil Hinterachse (0 % = nicht angesteuert; 100 % = voll angesteuert) |

<a id="table-res-0xdbf4-d"></a>
### RES_0XDBF4_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DRUCK_IST_WERT | bar | - | signed int | - | - | 1.0 | 1000.0 | 0.0 | aktueller Druck |
| STAT_SPANNUNG_IST_WERT | V | - | unsigned int | - | - | 1.0 | 1000.0 | 0.0 | aktuelle Spannung |

<a id="table-res-0xdbf5-d"></a>
### RES_0XDBF5_D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WEG_IST_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedalweg (bezogen auf WEG_NULLPUNKT_IST) |
| STAT_WEG_NULLPUNKT_INIT_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Initialisierung Pedal Nullpunkt |
| STAT_WEG_NULLPUNKT_IST_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Nullpunkt |
| STAT_WEG_LEERWEG_IST_WERT | mm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | aktueller Pedal Leerweg (Einsatz Hydraulik bezogen auf WEG_NULLPUNKT_IST) |

<a id="table-res-0xdbf6-d"></a>
### RES_0XDBF6_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MOMENT_SOLL_WERT | Nm | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Sollwert Bremsrekuperation |
| STAT_MOMENT_IST_WERT | Nm | - | signed int | - | - | 1.0 | 1.0 | 0.0 | Istwert Bremsrekuperation |

<a id="table-res-0xdc13-d"></a>
### RES_0XDC13_D

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADAPTIVDATEN_RUECKSETZEN_AJ_DATA | DATA | - | data[2] | - | - | 1.0 | 1.0 | 0.0 | Adaptivdaten Grundeinstellung gesetzt |
| STAT_ADAPTIVDATEN_RUECKSETZEN_NR | 0-n | - | signed int | - | TAB_ADAPTIVDATEN_RESET | - | - | - | Adaptivdaten Grundeinstellung gesetzt |
| STAT_AX_AY_ABGLEICH_AJ_DATA | DATA | - | data[1] | - | - | 1.0 | 1.0 | 0.0 | Ablgeich Beschleunigungssensoren erfolgt |
| STAT_AX_AY_ABGLEICH_NR | 0-n | - | signed char | - | TAB_AX_AY_ABGLEICH | - | - | - | Ablgeich Beschleunigungssensoren erfolgt |
| STAT_ADAPTIVDATEN_WERKSMODUS_AJ_DATA | DATA | - | data[2] | - | - | 1.0 | 1.0 | 0.0 | Adaptivdaten Werkseinstellung gesetzt |
| STAT_ADAPTIVDATEN_WERKSMODUS_NR | 0-n | - | signed char | - | TAB_ADAPTIVDATEN_WERK | - | - | - | Adaptivdaten Werkseinstellung gesetzt |
| STAT_ADAPTIVDATEN_LERNWERTE_AKTIV_AJ_DATA | DATA | - | data[1] | - | - | 1.0 | 1.0 | 0.0 | Adaptivdaten im Lernbereich |
| STAT_ADAPTIVDATEN_LERNWERTE_AKTIV_NR | 0-n | - | signed char | - | TAB_ADAPTIVDATEN_LERNEN | - | - | - | Adaptivdaten im Lernbereich |

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

<a id="table-res-0xdc3a-d"></a>
### RES_0XDC3A_D

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAKTORU_EPS_WERT | - | high | unsigned char | - | - | 1.0 | 100.0 | 0.0 | Faktor, über den die GBR die Lenkunterstützung der EPS beeinflusst |
| STAT_FAKTORARD_EPS_WERT | - | high | unsigned char | - | - | 1.0 | 100.0 | 0.0 | Faktor, über den die GBR die Dämpfung der EPS beinflusst |
| STAT_FAKTORARZ_EPS_WERT | - | high | unsigned char | - | - | 1.0 | 100.0 | 0.0 | Faktor, über den die GBR den aktiven Rücklauf der EPS beeinflusst |
| STAT_MMOTOR_OFFSET_EPS_WERT | - | high | signed char | - | - | 1.0 | 100.0 | 0.0 | Offset-Motormoment, das die EPS dem eigenen Motormoment additiv überlagert |
| STAT_FAKTOR_EPS_QUALIFIER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Sollwert-Qualifier zu den 3 Faktoren (2 = umsetzen, 14 = nicht umsetzen) |
| STAT_OFFSET_EPS_QUALIFIER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Sollwert-Qualifier zum OffsetMotormoment (2 = umsetzen; 14 = nicht umsetzen) |
| STAT_FUNKTION_GBR_CODIERUNG_EIN | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | GBR-Funktion (1 = eincodiert; 0 = auscodiert) |
| STAT_FUNKTION_GBR_KENNLINIE_NUMMER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aktiver GBR Kennliniensatz |
| STAT_EPS_FAKT_MOM_SERVICE_QUALIFIER_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Service-Qualifier der EPS für Umsetzung der Faktoren und des Offset-Motormoments (alles i.O wenn 32 od 33) |
| STAT_ZUSTAND_GRENZBEREICHSREUCKMELDUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ist-Zustand der GBR-Funktion (abhängig von Qualifiern der Eingänge) |

<a id="table-res-0xdc42-d"></a>
### RES_0XDC42_D

Dimensions: 30 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LLP_MANI_AKTIV | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Manueller Eingriff (0= nicht aktiv; 1 = aktiv) |
| STAT_LLP_MANI_WERT | kW | - | signed char | - | - | 1.0 | 10.0 | 0.0 | Manueller Wert |
| STAT_LLP_CALC_WERT | kW | - | signed char | - | - | 1.0 | 10.0 | 0.0 | Berechneter Wert |
| STAT_LLP_PEL_IST_WERT | kW | - | signed char | - | - | 1.0 | 10.0 | 0.0 | Gemessener Wert |
| STAT_LLP_FZS_WERT | N | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Kraft Zahnstange |
| STAT_LLP_RITZELWINKEL_WERT | ° | high | signed int | - | - | 1.0 | 1.0 | 0.0 | Ritzelwinkel |
| STAT_LLP_ANTEIL_HUB_WERT | % | - | signed char | - | - | 1.0 | 1.0 | 0.0 | Normierter Zahnstangenhub |
| STAT_LLP_V_ZS_WERT | m/s | high | signed int | - | - | 1.0 | 1000.0 | 0.0 | Geschwindigkeit Zahnstange |
| STAT_LLP_FAHRERHANDMOMENT_WERT | Nm | - | signed int | - | - | 1.0 | 100.0 | 0.0 | Drehmoment Lenkrad (Fahrer) |
| STAT_LLP_VX_ENTRY | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Geschwindigkeit fehlerhaft |
| STAT_LLP_AX_KORR | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Längsbeschleunigung fehlerhaft |
| STAT_LLP_RETURN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wenden erkannt |
| STAT_LLP_STOP | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parken erkannt |
| STAT_LLP_EXTRAP_PEL | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Elektrische Leistung extrapoliert |
| STAT_LLP_EXTRAP_FZS | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Kraft Zahnstange extrapoliert |
| STAT_LLP_FZSREDUC_BRAKE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorderachse entbremst |
| STAT_LLP_PMA | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parkenmanöverassistent erkannt |
| STAT_LLP_PDC | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Park Distance Control erkannt |
| STAT_LLP_TEMP_A | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Außentemperatur erkannt |
| STAT_LLP_RAIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Regen erkannt |
| STAT_LLP_FLAG_AX | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Längsbeschleunigung aktiv |
| STAT_LLP_FLAG_STOP | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parken aktiv |
| STAT_LLP_FLAG_RAIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Regen aktiv |
| STAT_LLP_FLAG_PMA | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Parkenmanöverassistent aktiv |
| STAT_LLP_FLAG_PDC | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Park Distance Control aktiv |
| STAT_LLP_FLAG_RETURN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Wenden aktiv |
| STAT_LLP_FLAG_TEMP_A | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Außentemperatur aktiv |
| STAT_LLP_FLAG_EXTRAP_FZS | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Kraft Zahnstange aktiv |
| STAT_LLP_FLAG_EXTRAP_PEL | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Elektrische Leistung aktiv |
| STAT_LLP_FLAG_FZSREDUC_BRAKE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Vorderachse aktiv |

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

<a id="table-res-0xdc6f-d"></a>
### RES_0XDC6F_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PBRK_FUNKTION | 0-n | high | unsigned char | - | TAB_HDC_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Parkbremse (PBRK) |
| STAT_PBRK_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Parkbremse (PBRK) |
| STAT_PBRK_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Parkbremse (PBRK) |

<a id="table-res-0xdc70-d"></a>
### RES_0XDC70_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HDC_FUNKTION | 0-n | high | unsigned char | - | TAB_HDC_FUNKTION | 1.0 | 1.0 | 0.0 | Status Funktion Bergabfahrassistent (HDC) |
| STAT_HDC_FUNKTION_QUALIFIER_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Basis Qualifier Funktion Bergabfahrassistent (HDC) |
| STAT_HDC_FUNKTION_QUALIFIER_ERW_WERT | HEX | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Erweiterter Qualifier Funktion Bergabfahrassistent (HDC) |

<a id="table-res-0xdc89-d"></a>
### RES_0XDC89_D

Dimensions: 42 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_COMP_OFS_AX1_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Längsbeschleunigungssensor 1 |
| STAT_COMP_OFS_AX1_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Längsbeschleunigung 1 |
| STAT_COMP_SENS_AX1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Längsbeschleunigungssensor 1 |
| STAT_COMP_OFS_AY1_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Querbeschleunigungssensor 1 |
| STAT_COMP_OFS_AY1_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Querbeschleunigung 1 |
| STAT_COMP_OFS_AY2_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Querbeschleunigungssensor 2 |
| STAT_COMP_OFS_AY2_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Querbeschleunigung 2 |
| STAT_COMP_OFS_AZ1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Vertikalbeschleunigungssensor 1 |
| STAT_COMP_OFS_AZ1_TOL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Vertikalbeschleunigungssensor 1 |
| STAT_COMP_SENS_AZ1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Vertikalbeschleunigungssensor 1 |
| STAT_COMP_OFS_DE_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Langzeitabgleich Ritzel bezogen |
| STAT_COMP_OFS_DEW_LT_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Langzeitabgleich Rad bezogen |
| STAT_COMP_OFS_DEYR_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Abgleich über Gierrate Ritzel bezogen |
| STAT_COMP_OFS_DEWYR_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Abgleich über Gierrate Rad bezogen |
| STAT_COMP_OFS_DE_TOL_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeltoleranz Ritzel bezogen |
| STAT_COMP_OFS_DEW_TOL_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeltoleranz Rad bezogen |
| STAT_COMP_SENS_VWHL_HL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz hinten links |
| STAT_COMP_SENS_VWHL_HR_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz hinten rechts |
| STAT_COMP_SENS_VWHL_VL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz vorne links |
| STAT_COMP_SENS_VWHL_VR_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz vorne rechts |
| STAT_COMP_OFS_RY1_STST_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Nickratensensor 1 Stillstandsabgleich |
| STAT_COMP_OFS_RY1_DRV_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Nickratensensor 1 Fahrtabgleich |
| STAT_COMP_OFS_RY1_TOL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Nickratensensor 1 |
| STAT_COMP_KYR_RY1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturfaktor Nickrate Kompensation Gierratenübersprechen |
| STAT_COMP_OFS_XR1_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Rollratensensor 1 |
| STAT_COMP_OFS_XR1_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Rollrate 1 |
| STAT_COMP_SENS_XR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Rollratensensor 1 |
| STAT_COMP_KYR_XR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturfaktor Rollrate (Kompensation Gierratenübersprechen) |
| STAT_COMP_OFS_YR1_STST1_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 1 (aus Stillstandsabgleich) |
| STAT_COMP_OFS_YR1_DRV_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 1 (aus Fahrtabgleich) |
| STAT_COMP_OFS_YR1_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Gierrate 1 |
| STAT_COMP_SENS_YR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Gierratensensor 1 |
| STAT_COMP_OFS_YR2_DRV_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 2 (aus Fahrtabgleich) |
| STAT_COMP_OFS_YR2_STST_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 2 (aus Stillstandsabgleich) |
| STAT_COMP_OFS_YR2_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Gierrate 2 |
| STAT_COMP_SENS_YR2_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Gierratensensor 2 |
| STAT_I_SBS_3DE_IDE_CODE_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Lenkwinkelkodierüberwachung |
| STAT_I_AY1_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Querbeschleunigung 1 |
| STAT_I_AY2_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Querbeschleunigung 2 |
| STAT_I_YR1_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate 1 |
| STAT_I_YR2_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate 2 |
| STAT_I_YR_WH_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate (aus Radgeschwindigkeiten) |

<a id="table-res-0xdc8a-d"></a>
### RES_0XDC8A_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LWA_EPS_OFFSET_BESTAET_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Bestätigung EPS Positionsoffset |
| STAT_LWA_EPS_OFFS_KORR_ZAEHL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturzählerwert EPS Positionsoffset |

<a id="table-res-0xdc8b-d"></a>
### RES_0XDC8B_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SBS2EV_R_VCH_INTRO_B_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Beide Kurven) |
| STAT_SBS2EV_R_VCH_INTRO_L_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Linke Kurve) |
| STAT_SBS2EV_R_VCH_INTRO_R_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Rechte Kurve) |
| STAT_SBS_2EV_R_VCH_WERT0_B_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Beide Kurven) |
| STAT_SBS_2EV_R_VCH_WERT0_L_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Links Kurven) |
| STAT_SBS_2EV_R_VCH_WERT0_R_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Rechts Kurven) |

<a id="table-res-0xdc8c-d"></a>
### RES_0XDC8C_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TSC_FAKTOR_SOLL_HANDMOMENT_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Faktor Soll-Handmoment |

<a id="table-res-0xdc8d-d"></a>
### RES_0XDC8D_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZFMFS_OFS_AXM_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Längsbeschleunigung Motormoment |

<a id="table-res-0xdc8f-d"></a>
### RES_0XDC8F_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LWA_EPS_OFFSET_BESTAET_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Bestätigung EPS Positionsoffset |
| STAT_LWA_EPS_OFFS_KORR_ZAEHL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturzählerwert EPS Positionsoffset |

<a id="table-res-0xdc90-d"></a>
### RES_0XDC90_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SBS2EV_R_VCH_INTRO_B_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Beide Kurven) |
| STAT_SBS2EV_R_VCH_INTRO_L_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Linke Kurve) |
| STAT_SBS2EV_R_VCH_INTRO_R_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwerttoleranz (Rechte Kurve) |
| STAT_SBS_2EV_R_VCH_WERT0_B_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Beide Kurven) |
| STAT_SBS_2EV_R_VCH_WERT0_L_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Links Kurven) |
| STAT_SBS_2EV_R_VCH_WERT0_R_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | VCH Lernwert (Rechts Kurven) |

<a id="table-res-0xdc91-d"></a>
### RES_0XDC91_D

Dimensions: 42 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_COMP_OFS_AX1_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Längsbeschleunigungssensor 1 |
| STAT_COMP_OFS_AX1_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Längsbeschleunigung 1 |
| STAT_COMP_SENS_AX1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Längsbeschleunigungssensor 1 |
| STAT_COMP_OFS_AY1_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Querbeschleunigungssensor 1 |
| STAT_COMP_OFS_AY1_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Querbeschleunigung 1 |
| STAT_COMP_OFS_AY2_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Querbeschleunigungssensor 2 |
| STAT_COMP_OFS_AY2_TOL_WERT | m/s² | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Querbeschleunigung 2 |
| STAT_COMP_OFS_AZ1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Vertikalbeschleunigungssensor 1 |
| STAT_COMP_OFS_AZ1_TOL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Vertikalbeschleunigungssensor 1 |
| STAT_COMP_SENS_AZ1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Vertikalbeschleunigungssensor 1 |
| STAT_COMP_OFS_DE_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Langzeitabgleich Ritzel bezogen |
| STAT_COMP_OFS_DEW_LT_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Langzeitabgleich Rad bezogen |
| STAT_COMP_OFS_DEYR_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Abgleich über Gierrate Ritzel bezogen |
| STAT_COMP_OFS_DEWYR_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeloffset aus Abgleich über Gierrate Rad bezogen |
| STAT_COMP_OFS_DE_TOL_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeltoleranz Ritzel bezogen |
| STAT_COMP_OFS_DEW_TOL_WERT | rad | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lenkwinkeltoleranz Rad bezogen |
| STAT_COMP_SENS_VWHL_HL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz hinten links |
| STAT_COMP_SENS_VWHL_HR_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz hinten rechts |
| STAT_COMP_SENS_VWHL_VL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz vorne links |
| STAT_COMP_SENS_VWHL_VR_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Radtoleranz vorne rechts |
| STAT_COMP_OFS_RY1_STST_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Nickratensensor 1 Stillstandsabgleich |
| STAT_COMP_OFS_RY1_DRV_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Nickratensensor 1 Fahrtabgleich |
| STAT_COMP_OFS_RY1_TOL_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Nickratensensor 1 |
| STAT_COMP_KYR_RY1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturfaktor Nickrate Kompensation Gierratenübersprechen |
| STAT_COMP_OFS_XR1_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Rollratensensor 1 |
| STAT_COMP_OFS_XR1_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Rollrate 1 |
| STAT_COMP_SENS_XR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Rollratensensor 1 |
| STAT_COMP_KYR_XR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Korrekturfaktor Rollrate (Kompensation Gierratenübersprechen) |
| STAT_COMP_OFS_YR1_DRV_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 1 (aus Fahrtabgleich) |
| STAT_COMP_OFS_YR1_STST1_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 1 (aus Stillstandsabgleich) |
| STAT_COMP_OFS_YR1_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Gierrate 1 |
| STAT_COMP_SENS_YR1_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Gierratensensor 1 |
| STAT_COMP_OFS_YR2_DRV_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 2 (aus Fahrtabgleich) |
| STAT_COMP_OFS_YR2_STST_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Offset Gierratensensor 2 (aus Stillstandsabgleich) |
| STAT_COMP_OFS_YR2_TOL_WERT | rad/s | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Signaltoleranz Gierrate 2 |
| STAT_COMP_SENS_YR2_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Empfindlichkeit Gierratensensor 2 |
| STAT_I_SBS_3DE_IDE_CODE_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Lenkwinkelkodierüberwachung |
| STAT_I_AY1_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Querbeschleunigung 1 |
| STAT_I_AY2_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Querbeschleunigung 2 |
| STAT_I_YR1_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate 1 |
| STAT_I_YR2_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate 2 |
| STAT_I_YR_WH_SGN_WERT | - | high | motorola float | - | - | 1.0 | 1.0 | 0.0 | Lernwert Vorzeichenüberwachung Gierrate (aus Radgeschwindigkeiten) |

<a id="table-res-0xdc95-d"></a>
### RES_0XDC95_D

Dimensions: 24 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | 0-n | low | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Alle Eigenraeder sind bekannt: 0 = nicht bekannt; 1 = bekannt |
| STAT_RADPOS_ER_BEKANNT | 0-n | low | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Radpositionen aller Eigenraeder sind bekannt: 0 = nicht bekannt; 1 = bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | 0-n | low | unsigned char | - | TAB_RDC_CONFIRMED | - | - | - | Alle Radpositionen sind ueberprueft und bestaetigt: 0 = nicht bestätigt; 1 = bestätigt |
| STAT_DTC_INACTIVE | 0-n | low | unsigned char | - | TAB_RDC_DTC_ACTIVE | - | - | - | Aktiver DTC Fehler mit Warnlampe im Fehlerspeicher vorhanden: 0 = DTC inaktiv; 1 = DTC aktiv |
| STAT_KAL_ANFORDERUNG_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_CAL_ACTIVE | - | - | - | Kalibrieranforderung steht an: 0 = Kalibrieranforderung inaktiv; 1 = Kalibrieranforderung aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | 0-n | low | unsigned char | - | TAB_RDC_TIMEOUT | - | - | - | Radzuordnung konnte nicht abgeschlossen werden: 0 = kein Timeout; 1 = Timeout |
| STAT_BANDMODE_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_BANDMODE_ACTIVE | - | - | - | Abfrage ob Bandmode im RDC aktiviert ist: 0 = Bandmode inaktiv ; 1 = Bandmode aktiv |
| STAT_ER_ERKENNUNG_FAHRT | 0-n | low | unsigned char | - | TAB_RDC_STARTED | - | - | - | Eigenraderkennung waehrend der Fahrt wurde gestartet: 0 = nicht gestartet 1 = gestartet |
| STAT_TEST_EIGENRAD_FAHRT | 0-n | low | unsigned char | - | TAB_RDC_STARTED | - | - | - | Test-Eigenraderkennung in Fahrt wurde gestartet: 0 = nicht gestartet , 1 = gestartet |
| STAT_TEST_EIGENRAD_STAND | 0-n | low | unsigned char | - | TAB_RDC_STARTED | - | - | - | Test-Eigenraderkennung im Stand wurde gestartet: 0 = nicht gestartet, 1 = gestartet |
| STAT_ER_FAHRT_VTHRS_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert : 0 = inaktiv , 1 = aktiv |
| STAT_BM_TIMEOUT_ACTIVE | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Bandmode Timeout laeuft : 0 = inaktiv , 1 = aktiv |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung unspezifisch, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_VL_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung vorne links, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_VR_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung vorne rechts, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_HL_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung hinten links, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_HR_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung hinten rechts, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_KL_15_EIN | 0-n | low | unsigned char | - | TAB_RDC_ON_OFF | - | - | - | Klemme 15 EIN : 0 = AUS, 1 = EIN |
| STAT_MOTOR_LAEUFT_EIN | 0-n | low | unsigned char | - | TAB_RDC_ON_OFF | - | - | - | Motor läuft : 0 = Aus ; 1 = EIN |
| STAT_FZG_FAEHRT | 0-n | low | unsigned char | - | TAB_RDC_VEHICLE_RUNNING | - | - | - | Signal Fahrzeug fährt : 0 = steht , 1 = fährt |
| STAT_ERKENNUNG_ALLE_RE | 0-n | low | unsigned char | - | TAB_RDC_DETECTED | - | - | - | Alle Radelektroniken erkannt : 0 = nicht erkannt 1 = erkannt |
| STAT_ERKENNUNG_ZUVIELE_RE | 0-n | low | unsigned char | - | TAB_RDC_DETECTED | - | - | - | Zu viele Radelektroniken erkannt : 0 = nicht erkannt , 1 = erkannt |
| STAT_STOERSENDER | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Funkstoerung vorhanden : 0 = inaktiv , 1 = aktiv |
| STAT_FREQUENZ_WERT | MHz | low | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Gibt die aktuelle RF-Frequenz zurück. Die Frequenz ist abhaengig von der Codierung. (315 oder 433). Angabe in MHz |

<a id="table-res-0xdc96-d"></a>
### RES_0XDC96_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_1_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_1_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_1_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_1_INTERNER_FEHLERCODE_WERT | HEX | low | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_1_ZAEHLER_INAKTIV | 0-n | low | unsigned char | - | - | - | - | - | Zähler für Inaktiv-Ereignisse |
| STAT_2_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_2_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_2_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_2_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_2_INTERNER_FEHLERCODE_WERT | HEX | low | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_2_ZAEHLER_INAKTIV | 0-n | low | unsigned char | - | - | - | - | - | Zähler für Inaktiv-Ereignisse |
| STAT_3_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_3_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Inaktivereignis. 99.99.99 =&gt; ungültig |
| STAT_3_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_3_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_3_INTERNER_FEHLERCODE_WERT | HEX | low | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_3_ZAEHLER_INAKTIV | 0-n | low | unsigned char | - | - | - | - | - | Zähler für Inaktiv-Ereignisse |

<a id="table-res-0xdc97-d"></a>
### RES_0XDC97_D

Dimensions: 63 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_1_PLAUSI_DRUCK | 0-n | low | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_1_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_1_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_1_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_1_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_1_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_1_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_1_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_1_RADPOSITION_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_1_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (-9.999 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE0 (-99 °C =&gt; ungueltig) |
| STAT_1_RADPOSITION_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_1_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE1 (-9.999 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE1 (-99 °C =&gt; ungueltig) |
| STAT_1_RADPOSITION_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_1_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE2 (-9.999 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE2 (-99 °C =&gt; ungueltig) |
| STAT_1_RADPOSITION_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_1_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE3 (-9.999 bar =&gt; ungueltig) |
| STAT_1_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE3 (-99 °C =&gt; ungueltig) |
| STAT_1_ZAEHLER_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Zähler für Kalibrierereignisse |
| STAT_2_PLAUSI_DRUCK | 0-n | low | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_2_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_2_DATUM_TEXT | TEXT | high | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_2_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_2_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_2_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_2_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_2_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_2_RADPOSITION_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_2_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (-9.999 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE0 (-99 °C =&gt; ungueltig) |
| STAT_2_RADPOSITION_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_2_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE1 (-9.999 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE1 (-99 °C =&gt; ungueltig) |
| STAT_2_RADPOSITION_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_2_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE2 (-9.999 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE2 (-99 °C =&gt; ungueltig) |
| STAT_2_RADPOSITION_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_2_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE3 (-9.999 bar =&gt; ungueltig) |
| STAT_2_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE3 (-99 °C =&gt; ungueltig) |
| STAT_2_ZAEHLER_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Zähler für Kalibrierereignisse |
| STAT_3_PLAUSI_DRUCK | 0-n | low | unsigned char | - | TAB_PLAUSI_DRUCK | - | - | - | Eingefüllte Drücke bestanden ja oder nein |
| STAT_3_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_KALIBRIERUNG | - | - | - | Statusbyte über Erfolg- Misserfolg der Kalibrierung |
| STAT_3_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_3_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Kalibrierereignis. 99.99.99 =&gt; ungültig |
| STAT_3_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_3_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_3_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_3_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_3_RADPOSITION_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE0 |
| STAT_3_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert  Radelektronik RE0 (-9.999 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE0 (-99 °C =&gt; ungueltig) |
| STAT_3_RADPOSITION_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE1 |
| STAT_3_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE1 (-9.999 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE1 (-99 °C =&gt; ungueltig) |
| STAT_3_RADPOSITION_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE2 |
| STAT_3_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE2 (-9.999 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE2 (-99 °C =&gt; ungueltig) |
| STAT_3_RADPOSITION_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition Radelektronik RE3 |
| STAT_3_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert Radelektronik RE3 (-9.999 bar =&gt; ungueltig) |
| STAT_3_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert Radelektronik RE3 (-99 °C =&gt; ungueltig) |
| STAT_3_ZAEHLER_KALIBRIERUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Zähler für Kalibrierereignisse |

<a id="table-res-0xdc98-d"></a>
### RES_0XDC98_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | low | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | low | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Drehrichtung des Rades  0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | low | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | low | unsigned char | - | TAB_RE_SENDEMODE | - | - | - | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_WERT | HEX | low | unsigned int | - | - | - | - | - | Fehlercode Radelektronik |
| STAT_ROLLSWITCH | 0-n | low | unsigned char | - | TAB_RE_ROLLSWITCH | - | - | - | Status Rollswitch |
| STAT_TELEGRAMMTYP | 0-n | low | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc99-d"></a>
### RES_0XDC99_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | low | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | low | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Drehrichtung des Rades  0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | low | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | low | unsigned char | - | TAB_RE_SENDEMODE | - | - | - | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_WERT | HEX | low | unsigned int | - | - | - | - | - | Fehlercode Radelektronik |
| STAT_ROLLSWITCH | 0-n | low | unsigned char | - | TAB_RE_ROLLSWITCH | - | - | - | Status Rollswitch |
| STAT_TELEGRAMMTYP | 0-n | low | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9a-d"></a>
### RES_0XDC9A_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | low | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | low | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Drehrichtung des Rades  0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | low | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | low | unsigned char | - | TAB_RE_SENDEMODE | - | - | - | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_WERT | HEX | low | unsigned int | - | - | - | - | - | Fehlercode Radelektronik |
| STAT_ROLLSWITCH | 0-n | low | unsigned char | - | TAB_RE_ROLLSWITCH | - | - | - | Status Rollswitch |
| STAT_TELEGRAMMTYP | 0-n | low | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9b-d"></a>
### RES_0XDC9B_D

Dimensions: 20 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | low | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | low | unsigned int | - | TAB_RDC_RAD_POSITION_NR_UINT | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | low | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | low | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Drehrichtung des Rades  0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | 0-n | low | unsigned char | - | TAB_RDC_RAD_DREHRICHTUNG | - | - | - | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_RE_HERSTELLER | 0-n | low | unsigned char | - | TAB_RE_HERSTELLER | - | - | - | RE-Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | 0-n | low | unsigned char | - | TAB_RE_SENDEMODE | - | - | - | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_WERT | HEX | low | unsigned int | - | - | - | - | - | Fehlercode Radelektronik |
| STAT_ROLLSWITCH | 0-n | low | unsigned char | - | TAB_RE_ROLLSWITCH | - | - | - | Status Rollswitch |
| STAT_TELEGRAMMTYP | 0-n | low | unsigned char | - | TAB_RE_TELEGRAMMTYP | - | - | - | Telegrammtyp |

<a id="table-res-0xdc9c-d"></a>
### RES_0XDC9C_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-res-0xdc9d-d"></a>
### RES_0XDC9D_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-res-0xdc9e-d"></a>
### RES_0XDC9E_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-res-0xdc9f-d"></a>
### RES_0XDC9F_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARN_RUECKNAHME | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Zähler für Warnungsrücknahmen durch Luftnachfüllen oder Radtausch. |

<a id="table-res-0xdcd9-d"></a>
### RES_0XDCD9_D

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER_RE0_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE0 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE0 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE0_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE0 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE1 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE1 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE1_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE1 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE2 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE2 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE2_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE2 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE3 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE3 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE3_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE3 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE4_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE4 |
| STAT_REIFENDRUCK_RE4_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE4 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE4_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE4 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE4_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE4 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE5_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE5 |
| STAT_REIFENDRUCK_RE5_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE5 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE5_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE5 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE5_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE5 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE6_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE6 |
| STAT_REIFENDRUCK_RE6_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE6 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE6_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE6 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE6_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE6 (255 =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE7_WERT | HEX | low | unsigned long | - | - | - | - | - | Identifier Radelektronik RE7 |
| STAT_REIFENDRUCK_RE7_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifendruckwert Radelektronik RE7 (-9.999 bar =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE7_WERT | - | low | signed int | - | - | 1.0 | 1.0 | 0.0 | Restlebensdauer Radelektronik RE7 in Monaten (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_RE7_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Empfangszaehler Radelektronik RE7 (255 =&gt; ungueltig) |

<a id="table-res-0xdcf1-d"></a>
### RES_0XDCF1_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-res-0xdcf2-d"></a>
### RES_0XDCF2_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-res-0xdcf3-d"></a>
### RES_0XDCF3_D

Dimensions: 31 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DATUM_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Datum zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_UHRZEIT_TEXT | TEXT | low | string[9] | - | - | 1.0 | 1.0 | 0.0 | Uhrzeit zum Warnereignis. 99.99.99 =&gt; ungültig |
| STAT_KILOMETERSTAND_WERT | km | low | signed long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand (-999999 km =&gt; ungueltig) |
| STAT_SYSTEMFLAGS_WERT | HEX | low | unsigned long | - | - | - | - | - | Systemflags |
| STAT_BEFUELL_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur beim Befüllen |
| STAT_BEFUELL_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Befüllen |
| STAT_AUSSENTEMPERATUR_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur bei Warnereignis |
| STAT_AUSSENDRUCK_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Aussendruck beim Warnereignis |
| STAT_RADELEKTRONIK_STATUS_PANNENRAD_WERT | HEX | low | unsigned char | - | - | - | - | - | Radelektronik-Status des Pannenauslösenden Rades |
| STAT_RADPOSITION_PANNENRAD | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition des Pannenauslösenden Rades |
| STAT_RADPOSITON_RE0 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE0 |
| STAT_BEFUELLDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE0 |
| STAT_BEFUELLTEMPERATUR_RE0_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE0 |
| STAT_REIFENDRUCK_RE0_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE0 |
| STAT_REIFENTEMPERATUR_RE0_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE0 |
| STAT_RADPOSITON_RE1 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE1 |
| STAT_BEFUELLDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE1 |
| STAT_BEFUELLTEMPERATUR_RE1_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE1 |
| STAT_REIFENDRUCK_RE1_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE1 |
| STAT_REIFENTEMPERATUR_RE1_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE1 |
| STAT_RADPOSITON_RE2 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE2 |
| STAT_BEFUELLDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE2 |
| STAT_BEFUELLTEMPERATUR_RE2_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE2 |
| STAT_REIFENDRUCK_RE2_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE2 |
| STAT_REIFENTEMPERATUR_RE2_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE2 |
| STAT_RADPOSITON_RE3 | 0-n | low | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition RE3 |
| STAT_BEFUELLDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Befuelldruckwert RE3 |
| STAT_BEFUELLTEMPERATUR_RE3_WERT | °C | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Befuelltemperaturwert RE3 |
| STAT_REIFENDRUCK_RE3_WERT | bar | low | signed int | - | - | 1.0 | 1000.0 | 0.0 | Reifenddruck RE3 |
| STAT_REIFENTEMPERATUR_RE3_WERT | ° | low | signed char | - | - | 1.0 | 1.0 | 0.0 | Reifentemperatur RE3 |
| STAT_ZAEHLER_WARNEREIGNIS_WERT | - | low | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zaehler Warnereignisse |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 111 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FS_LOESCHEN_PERMANENT | 0x1060 | - | Job zum Löschen der Permanent-DTCs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FEHLERSPEICHER_ENDE_WERKSABLAUF | 0x1061 | - | Löschen von Einzelfehlern und Permanent-DTCs unterbindet | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x1061_R |
| START_ADAPTIVDATEN_RUECKSETZEN | 0xA051 | - | Start und Status Ruecksetzen Adaptivdaten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA051_R |
| STEUERN_AX_AY_ABGLEICH | 0xA052 | - | Starten und Status Abgleich Beschleunigungssensoren | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA052_R |
| START_ADAPTIVDATEN_WERKSMODUS | 0xA053 | - | Starten und Status Standardisierung Adaptivdaten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA053_R |
| STEUERN_ADAPTIVDATEN_SLW_RESET | 0xA05B | - | Start und Status Summenlenkwinkel Reset | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA05B_R |
| DSC_ENTLUEFTUNG | 0xA061 | - | Starten, Stoppen und Status Entlüftung | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA061_R | RES_0xA061_R |
| DSC_VENTILE_PULS | 0xA064 | - | Starten, Stoppen und Status Puls Ventile (max. 6 gleichzeitig) | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA064_R | RES_0xA064_R |
| RADDREHZAHLSENSORPRUEFUNG | 0xA065 | - | Starten, Stoppen und Status Funktionsprüfung Raddrehzahlsensor | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA065_R | RES_0xA065_R |
| DSC_PUMPENFUNKTIONSPRUEFUNG | 0xA066 | - | Starten, Stoppen und Status Funktionsprüfung Pumpe | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA066_R | RES_0xA066_R |
| BPWS_INITIALISIERUNG | 0xA067 | - | Starten, Stoppen und Status Initialisierung Nullstellung Bremspedalwegsensor | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA067_R | RES_0xA067_R |
| RPA_RESET_STATISTIK | 0xA068 | - | Reset RPA Lerndaten Statistik | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DSC_VAKUUMBEFUELLUNG | 0xA06D | - | Starten (Weiterschalten), Stoppen und Status Vakuumbefüllung | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA06D_R | RES_0xA06D_R |
| DSC_DRUCKSENSOREN_KALIBRIERUNG | 0xA070 | - | Starten und Stoppen Kalibrierung DSC Drucksensoren | - | - | - | - | - | - | - | - | - | 31 | - | - |
| RPA_RESET_STANDARDISIERUNG | 0xA074 | - | Reset RPA Standardisierung | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DAC_RESET | 0xA087 | - | Reset der Lernwerte für die Driver Attention Control (Müdigkeitserkennung) | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DAC_AUSLOESUNG | 0xA088 | - | Auslösung einer Müdigkeitswarnung der Driver Attention Control | - | - | - | - | - | - | - | - | - | 31 | - | - |
| VENTILE_KALIBRIERUNG | 0xA08F | - | VENTILE_KALIBRIERUNG | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA08F_R | RES_0xA08F_R |
| IPB_LED | 0xA123 | - | Der Service schaltet die IPB Switch LED ein-/aus und gibt den LED Zustand aus. | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA123_R |
| FLM_RESET | 0xA130 | - | Field Load Manager (FLM) Daten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA130_R |
| EPB_ACTION_REQUEST | 0xA193 | - | Feststellen und Lösen der EPB mit Außerkraftsetzung durch Security-Verriegelung. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA193_R | RES_0xA193_R |
| EXTERNE_ANFORDERUNG_GKU_IPB_ZAEHLER_RUECKSETZEN | 0xA1AA | - | Zaehler fuer Uebernahmen durch externe Anforderung Getriebe ruecksetzen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| EXTERNE_ANFORDERUNG_EPB_ZAEHLER_RUECKSETZEN | 0xA1BE | - | Zähler für externe Anforderung Getriebe rücksetzen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DSC_PUMPENFUNKTIONSTEST | 0xA222 | - | Starten, Stoppen und Status Funktionstest Pumpe | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA222_R |
| STEUERN_ANTI_POWER_HOP_FUNKTION_ZAEHLER_RUECKSETZEN | 0xA2A2 | - | Mit diesem Diagnosejob kann der Zaehler der Anti-Power-HOP-Funktion zurückgesetzt werden. | - | - | - | - | - | - | - | - | - | 31 | - | - |
| EMF_VERFAHREN | 0xA803 | - | Anfahren Position | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA803_R | RES_0xA803_R |
| STEUERN_EEPROM_SCHREIBEN | 0xAB5B | - | Start und Status Abspeichern Lerndaten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAB5B_R |
| START_ADAPTIVDATEN_WERKSMODUS_2 | 0xABA3 | - | Initialisierung der Lernwerte der Funktion  Eigenlenkverhalten . | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xABA3_R |
| GMK_DATEN | 0xD09A | - | Auslesen GMK Daten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD09A_D |
| STATUS_BREMSPEDALWINKELSENSOR | 0xD0D2 | - | Bremspedalwegsensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD0D2_D |
| CBS_BREMSE_DETAILS | 0xD272 | - | CBS-Daten der Bremsen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD272_D |
| FES_COORDINT_SW_FEHLER_INFO | 0xD62E | STAT_FES_COORDINT_SW_FEHLER_INFO_WERT | FES COORDINT SW Fehler | - | - | high | signed long | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLM_LESEN | 0xD6D6 | - | Field Load Manager (FLM) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6D6_D |
| EMF_LERNDATEN_STATISTIK | 0xD804 | - | Auslesen Lerndaten Statistik | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD804_D |
| EMF_AKTUATOR_KOMBISATTEL | 0xD805 | - | Auslesen Daten Aktuator | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD805_D |
| EMF_LERNDATEN_TASTER | 0xD808 | - | Auslesen Lerndaten Taster | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD808_D |
| EMF_LERNDATEN_AKTUATOR | 0xD80A | - | Auslesen Lerndaten Aktuator | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD80A_D |
| EMF_KLEMMEN_KOMBISATTEL | 0xD80C | - | Auslesen Spannung Steuergerät | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD80C_D |
| EMF_TASTER | 0xD80D | - | Auslesen Taster | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD80D_D |
| EMF_MONTAGE_MODE | 0xD80F | - | Auslesen und Vorgeben Montagemodus (Sperrung Bedienung) | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD80F_D | RES_0xD80F_D |
| EXTERNE_ANFORDERUNG_GKU_IPB_ZAEHLER_LESEN | 0xD81A | STAT_AKTUELLER_ZAEHLERSTAND_GKU_WERT | Gibt Anzahl der IPB-Uebernahmen durch externe Getriebe-Anforderungen zurueck | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_LESEN_ANTI_POWER_HOP_FUNKTION_ZAEHLER_LESEN | 0xD8EB | STAT_ZAEHLER_ANTI_POWER_HOP_FUNKTION_WERT | Gibt an, wie oft die Anti-Power-HOP-Funktion aktiv war. | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_MODUS_ROLLENPRUEFSTAND | 0xDB5B | STAT_ROLLENMODUS_NR | Statusabfrage Rollenmodus aktiv im ICM | 0-n | - | - | signed char | TAB_STATUS_ROLLENMODUS | - | - | - | - | 22 | - | - |
| STEUERN_MODUS_ROLLENPRUEFSTAND | 0xDB98 | - | Vorgeben Rollenmodus | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDB98_D | - |
| STATUS_GIERRATE | 0xDBD9 | - | Auslesen Gierrate | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBD9_D |
| STATUS_QUERBESCHLEUNIGUNG | 0xDBDA | - | Auslesen Querbeschleunigung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBDA_D |
| STATUS_LAENGSBESCHLEUNIGUNG | 0xDBDB | - | Auslesen Laengsbeschleunigung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBDB_D |
| BREMSBELAGSSENSOR | 0xDBDF | - | Auslesen Bremsbelagssensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBDF_D |
| LMV_FUNKTION | 0xDBE1 | - | Auslesen und Vorgeben Aktivierung Funktion Längsantriebsmomentenverteilung (Ansteuerung Verteilergetriebe) aktueller Klemme15 Zyklus | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDBE1_D | RES_0xDBE1_D |
| REKU_FUNKTION | 0xDBE2 | - | Auslesen und Vorgeben Aktivierung Funktion Rekuperation (Bremsenergierückgewinnung) aktueller Klemme15 Zyklus | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDBE2_D | RES_0xDBE2_D |
| REIFENPANNENANZEIGE | 0xDBE3 | - | Reifenpannenanzeige | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE3_D |
| GESCHWINDIGKEIT_RAD | 0xDBE4 | - | Auslesen Raddrehzahlfühler | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE4_D |
| DSC_DRUCKSENSOREN | 0xDBE5 | - | Auslesen Drucksensoren | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE5_D |
| DSC_KLEMMEN | 0xDBE7 | - | Auslesen Spannung Steuergerät | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBE7_D |
| DSC_PUMPE | 0xDBE8 | - | Auslesen und Vorgeben Ansteuerung Pumpe | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDBE8_D | RES_0xDBE8_D |
| DSC_VENTILE | 0xDBE9 | - | Auslesen und Vorgeben Ansteuerung Ventile | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDBE9_D | RES_0xDBE9_D |
| VAKUUMSENSOR | 0xDBF4 | - | Auslesen Vakuumsensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBF4_D |
| BREMSPEDALWEGSENSOR | 0xDBF5 | - | Auslesen Bremspedalwegsensor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBF5_D |
| BREMSREKUPERATIONSMOMENT | 0xDBF6 | - | Auslesen Radmoment Bremsrekuperation | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDBF6_D |
| STATUS_ADAPTIVDATEN_ZUSTAND | 0xDC13 | - | Auslesen Status Adaptivdaten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC13_D |
| RPA_LERNDATEN_STATISTIK | 0xDC14 | - | Auslesen Lerndaten Statisik | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC14_D |
| RPA_LERNDATEN_STD | 0xDC15 | - | Auslesen Lerndaten Standardisierung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC15_D |
| DSC_BREMSLICHTSCHALTER | 0xDC1E | STAT_SCHALTER_BREMSLICHT_EIN | Auslesen Bremslichtschalter 1= ein (leuchtet); 0= aus | 0/1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| BREMSFLUESSIGKEITSSCHALTER | 0xDC1F | STAT_BREMSFLUESSIGKEIT_NIVEAU_SCHALTER_EIN | Auslesen Niveau Bremsflüssigkeit 1 = Bremsflüssigkeit vorhanden;  0 = Bremsflüssigkeit leer oder Unterbrechung | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| STATUS_GBRPLUS | 0xDC3A | - | Auslesen Daten Grenzbereichsrückmeldung (GBR) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC3A_D |
| STATUS_LLP | 0xDC42 | - | Auslesen Daten Lenkleistungsprädiktion | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC42_D |
| ABS_FUNKTION | 0xDC6C | - | Auslesen Status Funktion Antiblockiersystem (ABS) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6C_D |
| ASC_FUNKTION | 0xDC6D | - | Auslesen Status Funktion Antriebsschlupfregelung (ASC) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6D_D |
| FDR_FUNKTION | 0xDC6E | - | Auslesen Status Funktion Fahrzeugstabilisierung (FDR) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6E_D |
| PBRK_FUNKTION | 0xDC6F | - | Auslesen Status Funktion Parkbremse (PBRK) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC6F_D |
| HDC_FUNKTION | 0xDC70 | - | Auslesen Status Funktion Bergabfahrassistent (HDC) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC70_D |
| ADAPTIVDATEN_SBS | 0xDC89 | - | ADAPTIVDATEN_SBS | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDC89_D | RES_0xDC89_D |
| ADAPTIVDATEN_AAEPS | 0xDC8A | - | Auslesen Adaptivdaten | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDC8A_D | RES_0xDC8A_D |
| ADAPTIVDATEN_EV | 0xDC8B | - | ADAPTIVDATEN_EV | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDC8B_D | RES_0xDC8B_D |
| ADAPTIVDATEN_TSC | 0xDC8C | - | ADAPTIVDATEN_TSC | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDC8C_D | RES_0xDC8C_D |
| ADAPTIVDATEN_ZFM | 0xDC8D | - | ADAPTIVDATEN_ZFM | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDC8D_D | RES_0xDC8D_D |
| MIRROR_AAEPS | 0xDC8F | - | MIRROR_AAEPS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC8F_D |
| MIRROR_EV | 0xDC90 | - | MIRROR_EV | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC90_D |
| MIRROR_SBS | 0xDC91 | - | MIRROR_SBS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC91_D |
| MIRROR_TSC | 0xDC92 | STAT_TSC_FAKTOR_SOLL_HANDMOMENT_WERT | Faktor Soll-Handmoment | - | - | high | motorola float | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| MIRROR_ZFM | 0xDC93 | STAT_ZFMFS_OFS_AXM_WERT | Offset Längsbeschleunigung Motormoment | - | - | high | motorola float | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_RDC_VERSION | 0xDC94 | STAT_RDC_VERSION_WERT | Zeigt die aktuelle Softwareversion vom RDC an. | - | - | low | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_RDC_LESEN | 0xDC95 | - | STATUS_RDC_LESEN | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC95_D |
| RDC_HS_INAKTIVEREIGNIS | 0xDC96 | - | RDC_HS_INAKTIVEREIGNIS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC96_D |
| RDC_HS_KALIBRIEREREIGNIS | 0xDC97 | - | RDC_HS_KALIBRIEREREIGNIS | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC97_D |
| RDC_MESSDATENBLOCK_1 | 0xDC98 | - | RDC_MESSDATENBLOCK_1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC98_D |
| RDC_MESSDATENBLOCK_2 | 0xDC99 | - | RDC_MESSDATENBLOCK_2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC99_D |
| RDC_MESSDATENBLOCK_3 | 0xDC9A | - | RDC_MESSDATENBLOCK_3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9A_D |
| RDC_MESSDATENBLOCK_4 | 0xDC9B | - | RDC_MESSDATENBLOCK_4 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9B_D |
| RDC_HS_WARNEREIGNIS_1 | 0xDC9C | - | RDC_HS_WARNEREIGNIS_1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9C_D |
| RDC_HS_WARNEREIGNIS_2 | 0xDC9D | - | RDC_HS_WARNEREIGNIS_2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9D_D |
| RDC_HS_WARNEREIGNIS_3 | 0xDC9E | - | RDC_HS_WARNEREIGNIS_3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9E_D |
| RDC_HS_WARNEREIGNIS_RUECKNAHME | 0xDC9F | - | RDC_HS_WARNEREIGNIS_RUECKNAHME | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDC9F_D |
| STEUERN_RADELEKTRONIK_VORGEBEN | 0xDCC0 | - | Radelektronik vorgeben. Der Job weist der Radelektronik die durch das 1.Argument angewählt wurde, ihre Position am Fahrzeug zu (z.B. vorn rechts). Die Radelektronik kennt sonst ihre Position im Fahrzeug nicht. Sie kennt nur ihre ID. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC0_D | - |
| STEUERN_DIGITAL_RDC | 0xDCC6 | - | Setzen diverser Bandmodi Achtung: Busdiagnose und Tests im Stand nur mit RDC Generation2 | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC6_D | - |
| STATUS_RE_LESEN_DRUCKCODIERUNG | 0xDCD9 | - | Auslesen Druckcodierung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD9_D |
| STEUERN_SOLLDRUCK_VORGEBEN | 0xDCEE | - | Vorgabe Sollwert Reifendruck | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCEE_D | - |
| RDC_HS_WARNEREIGNIS_WEICH_1 | 0xDCF1 | - | RDC_WARNEREIGNIS_WEICH_1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF1_D |
| RDC_HS_WARNEREIGNIS_WEICH_2 | 0xDCF2 | - | RDC_HS_WARNEREIGNIS_WEICH_2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF2_D |
| RDC_HS_WARNEREIGNIS_WEICH_3 | 0xDCF3 | - | RDC_HS_WARNEREIGNIS_WEICH_3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCF3_D |
| AUSGANG_LLP | 0xDD0C | - | Vorgabe geschätzte Lenkleistung | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDD0C_D | - |
| STATUS_AUTO_EPB_ZAEHLER | 0xDD1B | STAT_AUTO_EPB_ZAEHLER_WERT | Gibt an, wie oft die Wegrollsicherung aktiv war. | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| EXTERNE_ANFORDERUNG_EPB_ZAEHLER_LESEN | 0xE354 | STAT_ZAEHLERSTAND_EPB_AKTIVIERUNG_WERT | Gibt Anzahl der EPB-Aktivierungen durch externe Getriebe-Anforderungen zurück | - | - | high | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _SW_IDENTIFIKATION | 0x4000 | STAT_SW_DATA | 11 Bytes SW-Identifikation | DATA | - | high | data[11] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FAHRZEUGZUSTAND | 0x5002 | STAT_FAHRZEUGZUSTAND_WERT | Abbild des Flexraysignals ST_VEH_CON | HEX | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| ANTRIEBSZUSTAND | 0x5004 | STAT_ANTRIEBSZUSTAND_WERT | Abbild des Flexraysignals ST_DRV_VEH | HEX | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| SPANNUNGSMASTER_VERFUEGBAR | 0x5008 | STAT_SPANNUNGSMASTER_VERFUEGBAR_WERT | Spannungsmaster verfügbar (siehe Beschreibung Spannungsschwellenclient) und Entscheidungslogik Fehlerursache (Bit 0: Verfügbarkeit der Spannungsmaster; Bit 4 = 1: DSC interner Fehler als Ursache; Bit 5 = 1: BBx Fehler oder RDCI Fehler als Ursache; Bits 1,2,3,6,7 nicht genutzt)  | HEX | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| FUNKTIONSZUSTAND | 0x500B | STAT_FUNKTIONSZUSTAND_WERT | Funktionszustand der Regler: ABS, ASC, FDR, GMV, ECBA, IBrake, Anfahrassistent, Autohold, EMF-Zustand, Abbild des Flexraysignals ST_BRG_DV, Fahrtrichtung | HEX | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| INTERNER_FUNKTIONSZUSTAND | 0x500C | STAT_INTERNER_FUNKTIONSZUSTAND_WERT | Steuergeräte interner Zustand | HEX | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| FEHLERSPEICHERSPERRE_AKTIV | 0x500F | STAT_FEHLERSPEICHERSPERRE_AKTIV | Abbild des Flexraysignals  ST_ILK_ERRM_FZM  (Fehlerspeichersperre) | 0/1 | - | high | unsigned char | - | - | - | - | - | 22 | - | - |
| NETZWERK_ROHDATEN | 0x5010 | STAT_ROHDATEN_WERT | NETZWERK_ROHDATEN UWB | HEX | - | high | signed long | - | - | - | - | - | 22 | - | - |

<a id="table-tab-0x2840"></a>
### TAB_0X2840

Dimensions: 1 rows × 21 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | 0x0001 | 0x0002 | 0x0003 | 0x0004 | 0x0005 | 0x0006 | 0x0007 | 0x0008 | 0x0009 | 0x000A | 0x000B | 0x000C | 0x000D | 0x000E | 0x000F | 0x0010 | 0x0011 | 0x0012 | 0x0013 | 0x0014 |

<a id="table-tab-0x2858"></a>
### TAB_0X2858

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x0015 | 0x0016 | 0x0017 | 0x0018 | 0x0019 | 0x001A | 0x001B | 0x001C |

<a id="table-tab-0x2859"></a>
### TAB_0X2859

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x001D | 0x001E | 0x001F | 0x0020 | 0x0021 | 0x0022 | 0x0023 | 0x0024 |

<a id="table-tab-abs-funktion"></a>
### TAB_ABS_FUNKTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verfügbar |
| 1 | verfügbar |
| 2 | verfügbar Rückfallebene |
| 0xFF | ungültig |

<a id="table-tab-adaptivdaten-aaeps"></a>
### TAB_ADAPTIVDATEN_AAEPS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bestaetigung EPS Positionsoffset |
| 0x01 | Korrekturzaehlerwert EPS Positionsoffset |
| 0xFF | unbekannt |

<a id="table-tab-adaptivdaten-ev"></a>
### TAB_ADAPTIVDATEN_EV

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | VCH Lernwerttoleranz (Beide Kurven) |
| 0x01 | VCH Lernwerttoleranz (Linke Kurve) |
| 0x02 | VCH Lernwerttoleranz (Rechte Kurve) |
| 0x03 | VCH Lernwert (beide Kurven) |
| 0x04 | VCH Lernwert (Linke Kurve) |
| 0x05 | VCH Lernwert (Rechte Kurve) |
| 0xFF | unbekannt |

<a id="table-tab-adaptivdaten-lernen"></a>
### TAB_ADAPTIVDATEN_LERNEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Adaptivdaten nicht im Lernbereich |
| 0x01 | Adaptivdaten im Lernbereich |
| 0xFF | unbekannter Zustand |

<a id="table-tab-adaptivdaten-reset"></a>
### TAB_ADAPTIVDATEN_RESET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Adaptivdaten nicht auf Defaultwerte gesetzt |
| 0x01 | Adaptivdaten auf Defaultwerte gesetzt |
| 0xFF | unbekannter Zustand |

<a id="table-tab-adaptivdaten-sbs"></a>
### TAB_ADAPTIVDATEN_SBS

Dimensions: 45 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Offsetwert des Laengsbeschleunigungssensors 1 |
| 0x01 | Signaltoleranz des Laengsbeschleunigungsnutzsignals |
| 0x02 | Empfindlichkeit des Laengsbeschleunigungssensors 1 |
| 0x03 | Offsetwert des Querbeschleunigungssensors 1 |
| 0x04 | Signaltoleranz des Querbeschleunigungsnutzsignals 1 |
| 0x05 | Offsetwert des Querbeschleunigungssensors 2 |
| 0x06 | Signaltoleranz des Querbeschleunigungsnutzsignals 2 |
| 0x07 | Offsetwert des Vertikalbeschleunigungssensors 1 |
| 0x08 | Signaltoleranz des Vertikalbeschleunigungssensors 1 |
| 0x09 | Empfindlichkeit Vertikalbeschleunigungssensor 1 |
| 0x0A | Lenkwinkeloffset aus Langzeitabgleich Ritzel bezogen |
| 0x0B | Lenkwinkeloffset aus Langzeitabgleich Rad bezogen |
| 0x0C | Lenkwinkeloffset aus Abgleich über Gierrate Ritzel bezogen |
| 0x0D | Lenkwinkeloffset aus Abgleich über Gierrate Rad bezogen |
| 0x0E | Lenkwinkeltoleranz Ritzel bezogen |
| 0x0F | Lenkwinkeltoleranz Rad bezogen |
| 0x10 | Radtoleranz hinten links |
| 0x11 | Radtoleranz hinten rechts |
| 0x12 | Radtoleranz vorne links |
| 0x13 | Radtoleranz vorne rechts |
| 0x15 | Offsetwert des Nickratensensors 1 aus Stillstandsabgleich |
| 0x14 | Offsetwert des Nickratensensors 1 aus Fahrtabgleich |
| 0x16 | Signaltoleranz des Nickratensensors 1 |
| 0x17 | Korrekturfaktor für die Nickrate zur Kompensation des Gierratenuebersprechens |
| 0x18 | Offsetwert des Rollratensensors 1 |
| 0x19 | Signaltoleranz des Rollratennutzsignals 1 |
| 0x1A | Empfindlichkeit Rollratensensor 1 |
| 0x1B | Korrekturfaktor für die Rollrate zur Kompensation des Gierratenuebersprechens |
| 0x1C | Offsetwert des Gierratensensors 1 aus Fahrtabgleich |
| 0x1D | Offsetwert des Gierratensensors 1 aus Stillstandsabgleich |
| 0x1E | Signaltoleranz des Gierratennutzsignals 1 |
| 0x1F | Empfindlichkeit Gierratensensor 1 |
| 0x20 | Offsetwert des Gierratensensors 2 aus Fahrtabgleich |
| 0x21 | Offsetwert des Gierratensensors 2 aus Stillstandsabgleich |
| 0x22 | Signaltoleranz des Gierratennutzsignals 2 |
| 0x23 | Empfindlichkeit Gierratensensor 2 |
| 0x24 | Lernwert für die Lenkwinkelkodierueberwachung |
| 0x25 | Lernwert für die Vorzeichenueberwachung Querbeschleunigung 1 |
| 0x26 | Lernwert für die Vorzeichenueberwachung Querbeschleunigung 2 |
| 0x27 | Lernwert für die Vorzeichenueberwachung Gierrate 1 |
| 0x28 | Lernwert für die Vorzeichenueberwachung Gierrate 2 |
| 0x29 | Lernwert für die Vorzeichenueberwachung Gierrate aus Radgeschwindigkeiten |
| 0x2A | Lernwert für SensorclusterSeriennummer Teil 1 |
| 0x2B | Lernwert für SensorclusterSeriennummer Teil 2 |
| 0x2C | Lernwert für Speicherung des BandendeRollenmodus über Klemmenwechsel hinaus |

<a id="table-tab-adaptivdaten-tsc"></a>
### TAB_ADAPTIVDATEN_TSC

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Faktor Soll-Handmoment |
| 0xFF | unbekannt |

<a id="table-tab-adaptivdaten-werk"></a>
### TAB_ADAPTIVDATEN_WERK

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Adaptivdaten nicht auf Werksdaten gesetzt |
| 0x01 | Adaptivdaten auf Werksdaten gesetzt |
| 0xFF | unbekannter Zustand |

<a id="table-tab-adaptivdaten-zfm"></a>
### TAB_ADAPTIVDATEN_ZFM

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Offset der Laengsbeschleunigung aus Motormoment |
| 0xFF | unbekannt |

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

<a id="table-tab-ax-ay-abgleich"></a>
### TAB_AX_AY_ABGLEICH

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Abgleich ax_ay muss noch erfolgen |
| 0x01 | Abgleich ax_ay erfolgt |
| 0xFF | unbekannter Zustand |

<a id="table-tab-bbv-sensor"></a>
### TAB_BBV_SENSOR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | 1. Stufe erreicht |
| 0x02 | 2. Stufe erreicht |
| 0xFF | nicht verfügbar |

<a id="table-tab-bpws-detail-initialisierung"></a>
### TAB_BPWS_DETAIL_INITIALISIERUNG

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler - Bremspedal während NP1-Messung betätigt |
| 0x02 | Fehler - Bremspedal während NP2-Messung betätigt |
| 0x03 | Fehler - NP1 und NP2 weichen voneinander ab ( \|NP1 - NP2\| &gt; Delta_NP ) |
| 0x04 | Fehler - Druckaufbau zu kurz (&lt; t_Betätigung) |
| 0x05 | Fehler - Druckaufbau zu gering (&lt; p_min) |
| 0x06 | Fehler - Messwert schwankt innerhalb der NP1 - Messung |
| 0x07 | Fehler - Messwert schwankt innerhalb der NP2 - Messung |
| 0x08 | Fehler - t_max überschritten (Betätigung zu spät oder zu lang) |
| 0x09 | Fehler - Abweichung zur Soll-Nullstellung zu groAY |
| 0x0A | Fehler - Bremspedal zu gering betätigt |
| 0x0B | Fehler - Fahrzeug steht nicht |
| 0x0C | Fehler - Verbrennungsmotor läuft nicht bzw. Unterdruck im Bremskraftverstärker zu gering |
| 0x0D | Fehler - Bremslichtschalter oder Vordruck nicht unbetätigt bei Start der Routine |
| 0x0E | Fehler - elektrischer Fehler des Bremspedalwegsensors ist aktiv |
| 0xFF | nicht definiert |

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

<a id="table-tab-drehrichtung"></a>
### TAB_DREHRICHTUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stand |
| 0x01 | Vorwaerts |
| 0x02 | Rueckwaerts |
| 0x03 | nicht definiert |

<a id="table-tab-dsc-phase-entlueftung"></a>
### TAB_DSC_PHASE_ENTLUEFTUNG

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine |
| 0x01 | VL |
| 0x02 | VR |
| 0x03 | HL |
| 0x04 | HR |
| 0x05 | KREIS1 |
| 0x06 | KREIS2 |
| 0x07 | VORBEREITUNG |
| 0x08 | NACHBEREITUNG |
| 0xFF | Wert ungültig |

<a id="table-tab-dsc-phase-vakuumbefuellung"></a>
### TAB_DSC_PHASE_VAKUUMBEFUELLUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nv |
| 0x01 | evakuieren |
| 0x02 | fuellen |
| 0x03 | nivellieren |

<a id="table-tab-dsc-phase-ventile-kalibrierung"></a>
### TAB_DSC_PHASE_VENTILE_KALIBRIERUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nv |
| 0x01 | Einlassventile |
| 0x02 | Auslassventile |
| 0x03 | Vorladeventile |
| 0x04 | Trennventile |

<a id="table-tab-dsc-ventile"></a>
### TAB_DSC_VENTILE

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nv |
| 1 | Pumpe |
| 2 | EVVL |
| 3 | EVVR |
| 4 | EVHL |
| 5 | EVHR |
| 7 | AVVL |
| 8 | AVVR |
| 9 | AVHL |
| 10 | AVHR |
| 11 | VLV1 |
| 12 | VLV2 |
| 13 | TV1 |
| 14 | TV2 |

<a id="table-tab-emf-hu-mode"></a>
### TAB_EMF_HU_MODE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aktiv |
| 0x01 | Stufe 1 |
| 0x02 | Stufe 2 |
| 0x03 | Stufe 3 |
| 0x04 | Stufe 4 |
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

Dimensions: 15 rows × 2 columns

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
| 13 | AssemblyCheckLeft |
| 14 | AssemblyCheckRight |

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

<a id="table-tab-epb-action"></a>
### TAB_EPB_ACTION

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0052656C | Lösen |
| 0x01417070 | Feststellen |

<a id="table-tab-errid-fascbas"></a>
### TAB_ERRID_FASCBAS

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasCbas_0 |
| 1 | FasCbas_1_SIB_ANTRIEBSFREIGABE |
| 2 | FasCbas_2_SIB_BREMSENFREIGABE |
| 3 | FasCbas_3_SIB_GESCHWINDIGKEITSABBAU |
| 4 | FasCbas_4_SIB_SIK_KOORDINATION |
| 5 | FasCbas_5 |
| 6 | FasCbas_6 |
| 7 | FasCbas_7 |
| 8 | FasCbas_8 |
| 9 | FasCbas_9 |
| 10 | FasCbas_10 |
| 11 | FasCbas_11 |
| 12 | FasCbas_12 |
| 13 | FasCbas_13 |
| 14 | FasCbas_14 |
| 15 | FasCbas_15 |

<a id="table-tab-errid-fascebc"></a>
### TAB_ERRID_FASCEBC

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasCebc_0 |
| 1 | FasCebc_1_SIP_AUSGABE |
| 2 | FasCebc_2_SIP_BREMSVERFUEGBARKEIT_APDC |
| 3 | FasCebc_3_SIP_GESCHWINDIGKEIT |
| 4 | FasCebc_4_SIP_GESCHWINDIGKEIT_APDC |
| 5 | FasCebc_5_SIP_SIK_KOORDINATION |
| 6 | FasCebc_6_USI_ABBAU_BREMSMOMENT |
| 7 | FasCebc_7_USI_ANFAHREN_FAHRERAUSSTIEG |
| 8 | FasCebc_8_USI_ANTRIEBSFREIGABE |
| 9 | FasCebc_9_USI_BREMSENFREIGABE |
| 10 | FasCebc_10_USI_PRIO_BESCHLEUNIGUNGSWUNSCH |
| 11 | FasCebc_11_USI_SIK_KOORDINATION |
| 12 | FasCebc_12_USI_UEBERNAHME_SSM |
| 13 | FasCebc_13 |
| 14 | FasCebc_14 |
| 15 | FasCebc_15 |
| 16 | FasCebc_16 |
| 17 | FasCebc_17 |
| 18 | FasCebc_18 |
| 19 | FasCebc_19 |
| 20 | FasCebc_20 |
| 21 | FasCebc_21 |
| 22 | FasCebc_22 |
| 23 | FasCebc_23 |
| 24 | FasCebc_24 |
| 25 | FasCebc_25 |

<a id="table-tab-errid-fascfi"></a>
### TAB_ERRID_FASCFI

Dimensions: 256 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasCfi_0 |
| 1 | FasCfi_1_Net_AbstndHindnsFhrschlauchHntn |
| 2 | FasCfi_2_Net_AbstndHindnsFhrschlauchVorn |
| 3 | FasCfi_3_Net_AbstndSensSeiteVornLi |
| 4 | FasCfi_4_Net_AbstndSensSeiteVornRe |
| 5 | FasCfi_5_Net_BdngTastrParkn |
| 6 | FasCfi_6_Net_FMM_Taster_STA |
| 7 | FasCfi_7_Net_FMM_Taster_RES |
| 8 | FasCfi_8_Net_FMM_Taster_IO |
| 9 | FasCfi_9_Net_FMM_Taster_Wippe_V |
| 10 | FasCfi_10_Net_BremsasistWngFrntraumuebwachg |
| 11 | FasCfi_11_Net_FhrspurrandLi |
| 12 | FasCfi_12_Net_FhrspurrandRe |
| 13 | FasCfi_13_Net_FhrzstndFzg |
| 14 | FasCfi_14_Net_GschwFzgLngs |
| 15 | FasCfi_15_Net_GschwRadKompHL |
| 16 | FasCfi_16_Net_GschwRadKompHR |
| 17 | FasCfi_17_Net_GschwRadKompVL |
| 18 | FasCfi_18_Net_GschwRadKompVR |
| 19 | FasCfi_19_Net_IstBremsmomSum |
| 20 | FasCfi_20_Net_IstLenkmomFhrrStellgld |
| 21 | FasCfi_21_Net_IstRadmomAntrbstrngSum |
| 22 | FasCfi_22_Net_IstRadmomAntrbstrngSumSchlepmomOb |
| 23 | FasCfi_23_Net_IstRadmomAntrbstrngSumTrghtverlust |
| 24 | FasCfi_24_Net_IstWnklFhrpedal |
| 25 | FasCfi_25_Net_LngsbschlGschztFzggschw |
| 26 | FasCfi_26_Net_QuFktAktvgParkbrems |
| 27 | FasCfi_27_Net_QuFktFDR |
| 28 | FasCfi_28_Net_QuFktKoordSollbremsmomEcba |
| 29 | FasCfi_29_Net_QuFktUmgebDetktParkn |
| 30 | FasCfi_30_Net_QuServAnzgFas |
| 31 | FasCfi_31_Net_QuServBdngTempmat |
| 32 | FasCfi_32_Net_QuServECBA |
| 33 | FasCfi_33_Net_QuServLenkmomKoord |
| 34 | FasCfi_34_Net_SollRadmomAntrbstrngSumKoord |
| 35 | FasCfi_35_Net_SollVrzrgBremsBremsasistFrntraumuebwachg |
| 36 | FasCfi_36_Net_StAntrbFzg |
| 37 | FasCfi_37_Net_StBlink |
| 38 | FasCfi_38_Net_StBremsgFhrr |
| 39 | FasCfi_39_Net_StFhrtrichtngFhrrwnsch |
| 40 | FasCfi_40_Net_StGangwahlAntrb |
| 41 | FasCfi_41_Net_StGurtschlosSchltrFA |
| 42 | FasCfi_42_Net_StKlem |
| 43 | FasCfi_43_Net_StKraftschlusAntrbstrng |
| 44 | FasCfi_44_Net_StSchntstFhrrasistsys |
| 45 | FasCfi_45_Net_StTuerkontkFATAbgsichr |
| 46 | FasCfi_46_Net_StVideoBestaetngBremseigrifObj |
| 47 | FasCfi_47 |
| 48 | FasCfi_48 |
| 49 | FasCfi_49 |
| 50 | FasCfi_50 |
| 51 | FasCfi_51 |
| 52 | FasCfi_52 |
| 53 | FasCfi_53 |
| 54 | FasCfi_54 |
| 55 | FasCfi_55_Fun_Aktive_Gefahrenbremsung_Ausgelöst |
| 56 | FasCfi_56_Fun_Aktive_Gefahrenbremsung_Max_Anzahl_Ueberschritten |
| 57 | FasCfi_57_Fun_Anfahrbereitschaft |
| 58 | FasCfi_58_Fun_Angezeigte_Geschwindigkeit |
| 59 | FasCfi_59_Fun_Betriebsmodus_Motorelektronik |
| 60 | FasCfi_60_Fun_Codierung |
| 61 | FasCfi_61_Fun_Fahrpedal_getreten |
| 62 | FasCfi_62_Fun_Fahrtrichtung_1 |
| 63 | FasCfi_63_Fun_Fahrtrichtung_2 |
| 64 | FasCfi_64_Fun_Funktionale_Deaktivierung_XCC |
| 65 | FasCfi_65_Fun_Kombi_Schnittstelle_XCC |
| 66 | FasCfi_66_Fun_PMALQ_Getriebe_Freigabe |
| 67 | FasCfi_67_Fun_PMALQ_Getriebe_Gangwahl |
| 68 | FasCfi_68_Fun_PMALQ_Getriebe_Getriebefehler |
| 69 | FasCfi_69_Fun_PMALQ_QF_Aktivierung |
| 70 | FasCfi_70_Fun_PMALQ_QF_Plausibilisierung_Seitenwahl |
| 71 | FasCfi_71_Fun_PMALQ_QF_Schaltaufforderung |
| 72 | FasCfi_72_Fun_PMALQ_QF_Unerlaubte_Deaktivierung |
| 73 | FasCfi_73_Fun_Segelabbruch |
| 74 | FasCfi_74_Fun_Uebernahme_SSM |
| 75 | FasCfi_75_Fun_Verzoegerungsanforderung_FCW_CCM |
| 76 | FasCfi_76_Fun_Verzögerungsanforderung_pFGS |
| 77 | FasCfi_77_Fun_KAFAS_Kalibrierung |
| 78 | FasCfi_78_Fun_Frontschutz_Akutwarnung_ausgeloest |
| 79 | FasCfi_79_Fun_Frontschutz_Anbremsen_Stufe_1_ausgeloest |
| 80 | FasCfi_80_Fun_Frontschutz_Anbremsen_Stufe_2_ausgeloest |
| 81 | FasCfi_81 |
| 82 | FasCfi_82 |
| 83 | FasCfi_83 |
| 84 | FasCfi_84_Net_AbstndSensSeiteVornLi_BBS_Sensorik_PMA_Links |
| 85 | FasCfi_85_Net_AbstndSensSeiteVornRe_BBS_Sensorik_PMA_Rechts |
| 86 | FasCfi_86_Net_BdngTastrParkn_BBS_Bedienelement_Parken |
| 87 | FasCfi_87_Net_GiergschwFzg_Qu |
| 88 | FasCfi_88_Net_GschwFzgLngs_Qu |
| 89 | FasCfi_89_Net_GschwRadKompHL_Qu |
| 90 | FasCfi_90_Net_GschwRadKompHR_Qu |
| 91 | FasCfi_91_Net_GschwRadKompVL_Qu |
| 92 | FasCfi_92_Net_GschwRadKompVR_Qu |
| 93 | FasCfi_93_Net_IstBremsmomSum_Qu |
| 94 | FasCfi_94_Net_IstGschwTacho_Qu |
| 95 | FasCfi_95_Net_IstLenkmomFhrrStellgld_Qu |
| 96 | FasCfi_96_Net_IstLenkwnklFhrr_Qu |
| 97 | FasCfi_97_Net_IstLngsneigFhrbahn_Qu |
| 98 | FasCfi_98_Net_IstQuerneigFhrbahn_Qu |
| 99 | FasCfi_99_Net_IstRadmomAntrbstrngSum_Qu |
| 100 | FasCfi_100_Net_IstWnklFhrpedal_Qu |
| 101 | FasCfi_101_Net_LenkwnklVachsRad_Qu |
| 102 | FasCfi_102_Net_LngsbschlGschztFzggschw_Qu |
| 103 | FasCfi_103 |
| 104 | FasCfi_104_Net_MassGwchtFzg_Qu |
| 105 | FasCfi_105_Net_ParknStParkluckMessg_BBS_Parkfunktion_Parklueckenvermessung |
| 106 | FasCfi_106_Net_QuAnfrdVrzrgHydfkt_BBS_Parkbremse |
| 107 | FasCfi_107 |
| 108 | FasCfi_108_Net_QuFktABS_BBS_Bremsaktuator_Funktion_ABS |
| 109 | FasCfi_109_Net_QuFktAktvgParkbrems_BBS_Parkbremse |
| 110 | FasCfi_110_Net_QuFktASC_BBS_Bremsaktuator_Funktion_ASC |
| 111 | FasCfi_111_Net_QuFktCCM_BBS_Sensorik_KAFAS_Funktion_FCW-CCM |
| 112 | FasCfi_112_Net_QuFktFDR_BBS_Bremsaktuator_Funktion_FDR |
| 113 | FasCfi_113_Net_QuFktFGS_BBS_Sensorik_KAFAS_Funktion_pFGS |
| 114 | FasCfi_114_Net_QuFktParknQuerfuhrgZstnd_BBS_Parkfunktion_Querfuehrung |
| 115 | FasCfi_115_Net_QuFktUmgebDetktParkn_BBS_Parkfunktion_Umfelderfassung |
| 116 | FasCfi_116_Net_QuHandOffErkngSens_BBS_Sensorik_Lenkrad_Hands_Off_Erkennung |
| 117 | FasCfi_117_Net_QuServAnzgFas_BBS_Kombiinstrument |
| 118 | FasCfi_118_Net_QuServBdngTempmat_BBS_Bedienelement_Tempomat |
| 119 | FasCfi_119_Net_QuServECBA_BBS_Bremsaktuator_ECBA_Schnittstelle |
| 120 | FasCfi_120_Net_QuServECBA_BBS_Bremsaktuator_Stillstandsmanagement |
| 121 | FasCfi_121 |
| 122 | FasCfi_122_Net_QuServFahrspurerkng_BBS_Sensorik_KAFAS_Fahrspurerkennung |
| 123 | FasCfi_123_Net_QuServFrntraumuebwachg_BBS_Sensorik_FRR |
| 124 | FasCfi_124 |
| 125 | FasCfi_125_Net_QuServLenkmomKoord_BBS_Koordinator_Lenkmoment |
| 126 | FasCfi_126_Net_QuServObjdtKafas_BBS_Sensorik_KAFAS |
| 127 | FasCfi_127_Net_QuServParamgDBC_BBS_Bremsaktuator_Funktion_DBC |
| 128 | FasCfi_128_Net_QuServRadmomAntrbstrngSumFAS_BBS_Antriebsaktuator |
| 129 | FasCfi_129_Net_QuServVorbefulgBrems_BBS_Bremsaktuator_Funktion_Vorbefuellung |
| 130 | FasCfi_130_Net_QuServWngBremsasist_BBS_Kombiinstrument_Auffahrwarnung |
| 131 | FasCfi_131_Net_SollRadlenkwnklVachsParkasist_Qu |
| 132 | FasCfi_132_Net_StFktbleuchtgHDC_BBS_Bedienelement_HDC_Funktionsbeleuchtung |
| 133 | FasCfi_133_Net_StFktBremsasistFrntraumuebwachg_BBS_Sensorik_FRR_Funktion_Anbremsen |
| 134 | FasCfi_134_Net_StFktBremsasistFrntraumuebwachg_BBS_Sensorik_FRR_Funktion_Bremsenkonditionierung |
| 135 | FasCfi_135_Net_StFktBremsasistFrntraumuebwachg_BBS_Sensorik_FRR_Warnung |
| 136 | FasCfi_136_Net_StGurtschlosSchltrFA_BBS_Gurtschloss_Fahrer |
| 137 | FasCfi_137_Net_StKraftschlusAntrbstrng_BBS_Antriebsaktuator_Kraftschluss |
| 138 | FasCfi_138_Net_StTastrHDC_BBS_Bedienelement_HDC_Taster |
| 139 | FasCfi_139_Net_QuFktKoordSollbremsmomEcba_BBS_Koordinator_Bremsmoment |
| 140 | FasCfi_140 |
| 141 | FasCfi_141 |
| 142 | FasCfi_142 |
| 143 | FasCfi_143_Net_FMM_Taster_LIM |
| 144 | FasCfi_144_Net_FMM_Taster_SET |
| 145 | FasCfi_145_Net_FMM_Taster_ABST1 |
| 146 | FasCfi_146_Net_FMM_Taster_ABST2 |
| 147 | FasCfi_147_Net_AbschltgGrndSysParkasist |
| 148 | FasCfi_148_Net_AbsenkgSchwlwertBremsasistAuffhrwngFrnt |
| 149 | FasCfi_149_Net_AbsenkgSchwlwertBremsasistFGS |
| 150 | FasCfi_150_Net_AbsenkgSchwlwertBremsasistFrntraumuebwachg |
| 151 | FasCfi_151 |
| 152 | FasCfi_152_Net_AbstndObjMin |
| 153 | FasCfi_153_Net_AbstndRadBrdstnHntn |
| 154 | FasCfi_154_Net_AbstndRadBrdstnVorn |
| 155 | FasCfi_155_Net_AnfrgZstndFktParkn2 |
| 156 | FasCfi_156_Net_AnzgStund |
| 157 | FasCfi_157_Net_AuffhrwngFrntSollAbsenkgLuftspielSchwlwertBremsasist |
| 158 | FasCfi_158 |
| 159 | FasCfi_159 |
| 160 | FasCfi_160_Net_BestaetngAnzgDisclmr |
| 161 | FasCfi_161_Net_Detektion_Modus_KAFAS |
| 162 | FasCfi_162_Net_FgsSollAbsenkgLuftspielSchwlwertBremsAsist |
| 163 | FasCfi_163_Net_FhlrFhrrAufmerksUebwachg |
| 164 | FasCfi_164_Net_FhrspurrandErweitLi |
| 165 | FasCfi_165_Net_FhrspurrandErweitRe |
| 166 | FasCfi_166_Net_GiergschwFzg |
| 167 | FasCfi_167_Net_GradtIstWnklFhrpedal |
| 168 | FasCfi_168_Net_IstAntrbElektFzg |
| 169 | FasCfi_169_Net_IstGschwTacho |
| 170 | FasCfi_170_Net_IstKrumgFhrspur |
| 171 | FasCfi_171_Net_IstLenkwnklFhrr |
| 172 | FasCfi_172_Net_IstLngsneigFhrbahn |
| 173 | FasCfi_173_Net_IstModSchltrFhrdyn |
| 174 | FasCfi_174_Net_IstQuerneigFhrbahn |
| 175 | FasCfi_175_Net_IstRadmomAntrbstrngSumMax |
| 176 | FasCfi_176_Net_IstRadmomAntrbstrngSumSchlepmomUnten |
| 177 | FasCfi_177_Net_IstWnklKursFzgFhrspur |
| 178 | FasCfi_178_Net_KennzhlGschwFzgSchwpkt |
| 179 | FasCfi_179_Net_LenkwnklVachseffkt |
| 180 | FasCfi_180_Net_LenkwnklVachsRad |
| 181 | FasCfi_181 |
| 182 | FasCfi_182_Net_MassGwchtFzg |
| 183 | FasCfi_183_Net_ParamsgDbcTrigrNiviSchwlwert |
| 184 | FasCfi_184_Net_ParknAnfrdSeiteWahl |
| 185 | FasCfi_185_Net_ParknAuswahlSeite |
| 186 | FasCfi_186_Net_ParknHandlghinwStrtPos |
| 187 | FasCfi_187_Net_ParknQuerfuhrgAbschltgGrund |
| 188 | FasCfi_188_Net_ParknQuerfuhrgAbstndFhrtrichtngAendg |
| 189 | FasCfi_189_Net_ParknQuerfuhrgAnfrdFhrtrichtngAendg |
| 190 | FasCfi_190_Net_ParknQuerfuhrgMod |
| 191 | FasCfi_191_Net_ParknStParkluckMessg |
| 192 | FasCfi_192_Net_ParknStStrt |
| 193 | FasCfi_193_Net_QuAnfrdVrzrgHydfkt |
| 194 | FasCfi_194 |
| 195 | FasCfi_195_Net_QuFktABS |
| 196 | FasCfi_196_Net_QuFktASC |
| 197 | FasCfi_197_Net_QuFktCCM |
| 198 | FasCfi_198_Net_QuFktFGS |
| 199 | FasCfi_199_Net_QuFktHDC |
| 200 | FasCfi_200_Net_QuFktParknQuerfuhrgZstnd |
| 201 | FasCfi_201_Net_QuFktPma |
| 202 | FasCfi_202_Net_QuHandOffErkngSens |
| 203 | FasCfi_203_Net_QuServFahrspurerkng |
| 204 | FasCfi_204_Net_QuServFrntraumuebwachg |
| 205 | FasCfi_205 |
| 206 | FasCfi_206_Net_QuServObjdtKafas |
| 207 | FasCfi_207_Net_QuServParamgDBC |
| 208 | FasCfi_208_Net_QuServRadmomAntrbstrngSumFAS |
| 209 | FasCfi_209_Net_QuServVorbefulgBrems |
| 210 | FasCfi_210_Net_QuServWngBremsasist |
| 211 | FasCfi_211_Net_SollAbsenkgLuftspielBremsanlageFrntraumuebwachg |
| 212 | FasCfi_212_Net_SollAnzgWnschgschwHDC |
| 213 | FasCfi_213_Net_SollRadlenkwnklVachsParkasist |
| 214 | FasCfi_214_Net_SollVrzrgCCM |
| 215 | FasCfi_215_Net_SollVrzrgFGS |
| 216 | FasCfi_216_Net_StAktvgFktParkn2 |
| 217 | FasCfi_217_Net_StAkutwngNivi |
| 218 | FasCfi_218_Net_StAnhngr |
| 219 | FasCfi_219_Net_StAnzgAbstndInfo |
| 220 | FasCfi_220_Net_StAnzgEffntdyncs |
| 221 | FasCfi_221 |
| 222 | FasCfi_222_Net_StAnzgUhrzeitDat |
| 223 | FasCfi_223_Net_StBlinkSymNivi |
| 224 | FasCfi_224_Net_StFhrlichtGrund |
| 225 | FasCfi_225_Net_StFktbleuchtgHDC |
| 226 | FasCfi_226_Net_StFktBremsasistFrntraumuebwachg |
| 227 | FasCfi_227_Net_StNebelschlusleucht |
| 228 | FasCfi_228_Net_StObjEinfEigschfNivi2 |
| 229 | FasCfi_229_Net_StObjEinfTypNivi2 |
| 230 | FasCfi_230_Net_StObjFernberchMittEigschfNivi2 |
| 231 | FasCfi_231_Net_StObjFernberchMittTypNivi2 |
| 232 | FasCfi_232_Net_StObjNahberchMittEigschfNivi2 |
| 233 | FasCfi_233_Net_StObjNahberchMittTypNivi2 |
| 234 | FasCfi_234_Net_StObjQuerLiEigschfNivi2 |
| 235 | FasCfi_235_Net_StObjQuerLiTypNivi2 |
| 236 | FasCfi_236_Net_StObjQuerReEigschfNivi2 |
| 237 | FasCfi_237_Net_StObjQuerReTypNivi2 |
| 238 | FasCfi_238_Net_StPFgs |
| 239 | FasCfi_239_Net_StrgIbrake |
| 240 | FasCfi_240_Net_StSglnAntrb2 |
| 241 | FasCfi_241_Net_StTastrHDC |
| 242 | FasCfi_242_Net_StUebwachgFreiraum |
| 243 | FasCfi_243_Net_StVerfgbkEigrifAntrbstrngFAS |
| 244 | FasCfi_244_Net_StVerkhrsinKafas |
| 245 | FasCfi_245 |
| 246 | FasCfi_246_Net_UmweltbdinggFhrspurerkng |
| 247 | FasCfi_247_Net_Verkhrsin |
| 248 | FasCfi_248_Net_VerkhrstauWahrsch |
| 249 | FasCfi_249_Net_VerlustZielobjKafas |
| 250 | FasCfi_250_Net_VorbefulgNiviBrems |
| 251 | FasCfi_251_Net_VrzrgKolisverhdrgBremsasistFrntraumuebwachg |
| 252 | FasCfi_252_Net |
| 253 | FasCfi_253_Net_WngFrntraumuebwachgAuffhrwngFrnt |
| 254 | FasCfi_254_Net_WngFrntraumuebwachgFGS |
| 255 | FasCfi_255 |

<a id="table-tab-errid-fascfo"></a>
### TAB_ERRID_FASCFO

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasCfo_0 |
| 1 | FasCfo_1_SIK_ANZEIGENSTEUERUNG |
| 2 | FasCfo_2_SIK_MOMENTE |
| 3 | FasCfo_3_SIK_PLAUSIBILITAET |
| 4 | FasCfo_4 |
| 5 | FasCfo_5 |
| 6 | FasCfo_6 |
| 7 | FasCfo_7 |
| 8 | FasCfo_8 |
| 9 | FasCfo_9 |
| 10 | FasCfo_10 |
| 11 | FasCfo_11 |
| 12 | FasCfo_12 |
| 13 | FasCfo_13 |
| 14 | FasCfo_14 |
| 15 | FasCfo_15 |

<a id="table-tab-errid-fasdsp"></a>
### TAB_ERRID_FASDSP

Dimensions: 51 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasDsp_0 |
| 1 | FasDsp_1_Net_Anzahl_Fahrspuren_Erweitert |
| 2 | FasDsp_2_Net_AnzhlFhrspurnNavGrph |
| 3 | FasDsp_3_Net_Bedingung_Begrenzung_Geschwindigkeit |
| 4 | FasDsp_4_Net_Begrenzung_Geschwindigkeit_Bedingt |
| 5 | FasDsp_5_Net_Begrenzung_Geschwindigkeit_Nav-Graph |
| 6 | FasDsp_6_Net_Eigenschaft_Karte_Nav-Graph |
| 7 | FasDsp_7_Net_Gradient_Nav-Graph |
| 8 | FasDsp_8_Net_Gültigkeit_Zeit_Ende |
| 9 | FasDsp_9_Net_Gültigkeit_Zeit_Start |
| 10 | FasDsp_10_Net_Index_Segment_Löschen_Nav-Graph |
| 11 | FasDsp_11_Net_Index_Segment_Nav-Graph |
| 12 | FasDsp_12_Net_Index_Segment_Nav-Graph_Fahrspur |
| 13 | FasDsp_13_Net_Index_Segment_Nav-Graph_Geschwindigkeit |
| 14 | FasDsp_14_Net_Index_Segment_Nav-Graph_Karte_Daten |
| 15 | FasDsp_15_Net_Index_Vater-Segment_Nav-Graph |
| 16 | FasDsp_16_Net_Information_Erweitert_Fahrspuren_1 |
| 17 | FasDsp_17_Net_Länge_Segment_Nav-Graph |
| 18 | FasDsp_18_Net_Radius_Segment_Nav-Graph |
| 19 | FasDsp_19_Net_Radius_Segment_Nav-Graph_Geschwindigkeit |
| 20 | FasDsp_20_Net_Status_Anzahl_Pakete |
| 21 | FasDsp_21_Net_Status_Übereinstimmung_Index_Segment |
| 22 | FasDsp_22_Net_Status_Übereinstimmung_Position_Relativ |
| 23 | FasDsp_23_Net_Status_Version_Protokoll_Navigation |
| 24 | FasDsp_24_Net_Steuerung_Löschen_Nav-Graph |
| 25 | FasDsp_25_Net_StLandcodrgNav |
| 26 | FasDsp_26_Net_Typ_Straße_Nav-Graph |
| 27 | FasDsp_27_Net_Zähler_Nav-Graph_Sync |
| 28 | FasDsp_28_Net_Zusatzinformation_Nav-Graph_Sync |
| 29 | FasDsp_29_Net_Zusatzinformation_Segment_Nav-Graph |
| 30 | FasDsp_30 |
| 31 | FasDsp_31 |
| 32 | FasDsp_32 |
| 33 | FasDsp_33 |
| 34 | FasDsp_34 |
| 35 | FasDsp_35 |
| 36 | FasDsp_36 |
| 37 | FasDsp_37 |
| 38 | FasDsp_38 |
| 39 | FasDsp_39 |
| 40 | FasDsp_40_Fun_Navigationsdaten_Baumstruktur |
| 41 | FasDsp_41 |
| 42 | FasDsp_42 |
| 43 | FasDsp_43 |
| 44 | FasDsp_44 |
| 45 | FasDsp_45 |
| 46 | FasDsp_46 |
| 47 | FasDsp_47 |
| 48 | FasDsp_48 |
| 49 | FasDsp_49 |
| 50 | FasDsp_50 |

<a id="table-tab-errid-fasscg"></a>
### TAB_ERRID_FASSCG

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | FasScg_0 |
| 1 | FasScg_1_SIS_ANTRIEBSFREIGABE |
| 2 | FasScg_2_SIS_BREMSENFREIGABE |
| 3 | FasScg_3_SIS_FLUCHTFUNKTION |
| 4 | FasScg_4_SIS_SIK_KOORDINATION |
| 5 | FasScg_5 |
| 6 | FasScg_6 |
| 7 | FasScg_7 |
| 8 | FasScg_8 |
| 9 | FasScg_9 |
| 10 | FasScg_10 |
| 11 | FasScg_11 |
| 12 | FasScg_12 |
| 13 | FasScg_13 |
| 14 | FasScg_14 |
| 15 | FasScg_15 |

<a id="table-tab-fahrerlebnis-filter"></a>
### TAB_FAHRERLEBNIS_FILTER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Alle Modi erlaubt |
| 1 | Nur Basis erlaubt |
| 2 | Nur Basis, Race, Traction erlaubt |
| 3 | Nur Basis, Traction erlaubt |
| 4 | Traction, Sport+, Race nicht erlaubt |

<a id="table-tab-fahrerlebnis-modus"></a>
### TAB_FAHRERLEBNIS_MODUS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Anforderung an den Modus |
| 0x01 | Modus Traction gefordert |
| 0x02 | Modus Komfort gefordert |
| 0x03 | Modus Basis gefordert |
| 0x04 | Modus Sport gefordert |
| 0x05 | Modus Sport+ gefordert |
| 0x06 | Modus Race gefordert |
| 0x07 | Modus ECO gefordert |
| 0x08 | Modus ECO+ gefordert |
| 0xFF | Signal ungueltig |

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

<a id="table-tab-ja-nein"></a>
### TAB_JA_NEIN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nein |
| 1 | ja |

<a id="table-tab-kalibrierung"></a>
### TAB_KALIBRIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RDCi stopped with Failed |
| 0x01 | RDCi finished with Success |
| 0xFF | RDCi is Ongoing |

<a id="table-tab-letztesbremsenevent-links"></a>
### TAB_LETZTESBREMSENEVENT_LINKS

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | IDLE |
| 0x01 | Dynamic Brake function |
| 0x02 | Diagnose |
| 0x03 | ReClamp Request |
| 0x04 | Static Apply Release |
| 0x05 | Drive Away Rlease |
| 0x06 | Engine Stall Apply |
| 0x07 | External Clamp Request |
| 0x08 | External Release request |
| 0x09 | Hardware Test |
| 0x0A | Brake Pad Adjustment |

<a id="table-tab-letztesbremsenevent-rechts"></a>
### TAB_LETZTESBREMSENEVENT_RECHTS

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | IDLE |
| 0x01 | Dynamic Brake function |
| 0x02 | Diagnose |
| 0x03 | ReClamp Request |
| 0x04 | Static Apply Release |
| 0x05 | Drive Away Rlease |
| 0x06 | Engine Stall Apply |
| 0x07 | External Clamp Request |
| 0x08 | External Release request |
| 0x09 | Hardware Test |
| 0x0A | Brake Pad Adjustment |

<a id="table-tab-mode-old"></a>
### TAB_MODE_OLD

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x01 | aktiv |

<a id="table-tab-plausi-druck"></a>
### TAB_PLAUSI_DRUCK

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Failed |
| 0x01 | Passed |
| 0xFF | Ongoing |

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

<a id="table-tab-rdc-aktiv-inaktiv"></a>
### TAB_RDC_AKTIV_INAKTIV

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | inaktiv |
| 0x01 | aktiv |
| 0x02 | Tankstop |
| 0x03 | Gateway oder Antennenfehler |
| 0x04 | Weiche Warnung aktiv |
| 0xFF | Signal unbekannt |

<a id="table-tab-rdc-bandmode-active"></a>
### TAB_RDC_BANDMODE_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bandmode inaktiv |
| 1 | Bandmode aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-bekannt-nicht-bekannt"></a>
### TAB_RDC_BEKANNT_NICHT_BEKANNT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bekannt |
| 1 | bekannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-cal-active"></a>
### TAB_RDC_CAL_ACTIVE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kalibrieranforderung inaktiv |
| 1 | Kalibrieranforderung aktiv |
| 2 | Kalibrierung abgewiesen |
| 255 | nicht definiert |

<a id="table-tab-rdc-changed"></a>
### TAB_RDC_CHANGED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht geändert |
| 1 | geändert |
| 255 | Signal unbekannt |

<a id="table-tab-rdc-confirmed"></a>
### TAB_RDC_CONFIRMED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bestätigt |
| 1 | bestätigt |
| 255 | nicht definiert |

<a id="table-tab-rdc-detected"></a>
### TAB_RDC_DETECTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht erkannt |
| 1 | erkannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-dtc-active"></a>
### TAB_RDC_DTC_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DTC inaktiv |
| 1 | DTC aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-on-off"></a>
### TAB_RDC_ON_OFF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | aus |
| 1 | ein |
| 9 | nicht bedient |
| 255 | nicht definiert |

<a id="table-tab-rdc-rad-drehrichtung"></a>
### TAB_RDC_RAD_DREHRICHTUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Stillstand |
| 1 | rechts |
| 2 | links |
| 3 | unbekannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-rad-position-nr"></a>
### TAB_RDC_RAD_POSITION_NR

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | vorne links |
| 1 | vorne rechts |
| 2 | hinten links |
| 3 | hinten rechts |
| 5 | unbekannt 1 |
| 4 | Reserverad (nur RDC Gen2) |
| 6 | unbekannt 2 |
| 7 | unbekannt 3 |
| 8 | unbekannt 4 |
| 9 | unbekannt 5 (nur RDC Gen2) |

<a id="table-tab-rdc-rad-position-nr-uint"></a>
### TAB_RDC_RAD_POSITION_NR_UINT

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | vorne links |
| 1 | vorne rechts |
| 2 | hinten links |
| 3 | hinten rechts |
| 5 | unbekannt 1 |
| 4 | Reserverad (nur RDC Gen2) |
| 6 | unbekannt 2 |
| 7 | unbekannt 3 |
| 8 | unbekannt 4 |
| 9 | unbekannt  (nur RDC Gen2) |

<a id="table-tab-rdc-started"></a>
### TAB_RDC_STARTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht gestartet |
| 1 | gestartet |
| 255 | nicht definiert |

<a id="table-tab-rdc-steuerfunktionen"></a>
### TAB_RDC_STEUERFUNKTIONEN

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | BANDMODE |
| 2 | ER_FAHRT |
| 3 | ER_STAND |
| 4 | TEST_ER_FAHRT |
| 5 | TEST_ER_STAND |
| 6 | RDCBUS_DIAG |
| 7 | SOLLDRUCK_SCHREIBEN |
| 8 | CAL_REQUEST |
| 9 | ER_FAHRT_OHNE_TRIGGER |
| 10 | TEST_ER_FAHRT_OHNE_TRIGGER |
| 11 | EINSCHALTEN_APPLIKATIONSBOTSCHAFT |

<a id="table-tab-rdc-timeout"></a>
### TAB_RDC_TIMEOUT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Timeout |
| 1 | Timeout |
| 255 | nicht definiert |

<a id="table-tab-rdc-vehicle-running"></a>
### TAB_RDC_VEHICLE_RUNNING

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug fährt |
| 255 | nicht definiert |

<a id="table-tab-re-hersteller"></a>
### TAB_RE_HERSTELLER

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bedient |
| 1 | Autonet |
| 2 | BERU |
| 3 | Conti |
| 4 | TRW |
| 5 | Schrader |
| 15 | Hersteller unbekannt |

<a id="table-tab-re-rollswitch"></a>
### TAB_RE_ROLLSWITCH

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Rollswitch nicht gesetzt |
| 1 | Rollswitch gesetzt |
| 16 | Rollswitch Toggle |

<a id="table-tab-re-sendemode"></a>
### TAB_RE_SENDEMODE

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Mode 0a/0b |
| 1 | Mode 1a/b/c/d |
| 2 | Mode 2 |
| 3 | Mode 3 |
| 4 | Mode 4 |
| 8 | Mode 0a/0b  LF triggered telegram |
| 9 | Mode 1a/b/c/d  LF triggered telegram |
| 10 | Mode 2  LF triggered telegram |
| 11 | Mode 3  LF triggered telegram |
| 12 | Mode 4  LF triggered telegram |

<a id="table-tab-re-telegrammtyp"></a>
### TAB_RE_TELEGRAMMTYP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AK35 default |
| 130 | BERU G3 only |
| 136 | AK35 BERU long |
| 160 | AK35 BERU medium |
| 193 | AK35 BERU short |
| 255 | nicht definiert |

<a id="table-tab-rollenmodus"></a>
### TAB_ROLLENMODUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Rücksetzen |
| 1 | Setzen Werksrollenmodus |
| 2 | Setzen Rollenmodus Innenraum |

<a id="table-tab-sbs-gueltigkeit-uint"></a>
### TAB_SBS_GUELTIGKEIT_UINT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Initialisierung |
| 1 | Signalwert ist gültig und abgesichert |
| 2 | Signalwert ist gültig |
| 3 | Signalwert ist nicht vertrauenswürdig |
| 4 | Ersatzweret ist im Nutzsignal gesetzt |
| 5 | Signal zu oft entprellt |
| 6 | Signalwert ist ungültig |
| 7 | Sensor nicht vorhanden oder Signal ungültig |
| 65535 | unbekannter Zustand |

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

<a id="table-tab-shutdownlevel-old"></a>
### TAB_SHUTDOWNLEVEL_OLD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO_SHUTDOWN |
| 0x01 | RESTRICTED_HYDRAULIC_MODE |
| 0x02 | ELECTROMECHANIC_MODE |
| 0x03 | COMPLETE_SHUTDOWN |

<a id="table-tab-status-nm"></a>
### TAB_STATUS_NM

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NM_SLEEP |
| 0x01 | NM_PREPARE_BUS_SLEEP |
| 0x02 | NM_READY_FOR_SLEEP |
| 0x03 | NM_NORMAL_STAT |
| 0x04 | NM_POWERON_REPEAT_REQUEST |
| 0x05 | NM_STATE_SYNCHRONIZE |
| 0xFF | Wert ungültig |

<a id="table-tab-status-rollenmodus"></a>
### TAB_STATUS_ROLLENMODUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Rolle |
| 0x01 | 1-Achsrolle Vorderachse (Fzg mit Kombi-Menue) oder Bandenderolle |
| 0x02 | 1-Achsrolle Hinterachse |
| 0x03 | 2-Achsrolle |
| 0x04 | Bandenderolle (Werk) |
| 0x0E | ungueltig |

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

<a id="table-tab-ventile-kalibrierung-1"></a>
### TAB_VENTILE_KALIBRIERUNG_1

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Fehler Spannungswert außerhalb des definierten Bereichs (&lt; 11 V oder &gt; 16 V) |
| 2 | Aktuelle Daten über erlaubtem Max-Wert |
| 4 | Aktuelle Daten unter erlaubtem Min-Wert |
| 8 | TMC-Druck größer 0 bar |
| 10 | Fahrzeug nicht im Stillstand |
| 20 | Drucksensor nicht kalibriert |
| 40 | Drucksensor ist defekt |
| 80 | Pumpe läuft während Kalibrierung |

<a id="table-tab-ventile-kalibrierung-2"></a>
### TAB_VENTILE_KALIBRIERUNG_2

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Interner Kommunikationsfehler: Daten der BFU inkorrekt |
| 2 | Kommunikationsfehler: Anfrage abgelehnt |
| 4 | Kalibrierungszeit überschritten |
| 8 | Diagnoseverbindung gestört |
| 10 | HCU Temperatur zu hoch (&gt; 70 °C) |
| 20 | Kalibrierung abgebrochen |
| 40 | HCU Temperatur zu gering (&lt; 10 °C) |
| 80 | Benötigte Komponente(n) nicht verfügbar |

<a id="table-tab-ventile-kalibrierung-3"></a>
### TAB_VENTILE_KALIBRIERUNG_3

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Fahrzeuggeschwindigkeit unter den erlaubten Min-Wert gefallen |
| 2 | Aktive Diagnose-Session wurde während der Kalibrierung erkannt |
| 4 | Kalibrierung wurde von anderer (aktiver, nicht autorisierter) Komponente unterbrochen |
| 8 | Keine gültige Kalibrierung gefunden |
| 10 | Bremslichtschaltung wurde nicht bestätigt |
| 20 | Kalibrierungsergebnis kann nicht in den EEPROM geschrieben werden |
| 40 | Kalibrierung durch den Komponenten-Service-Handler (SVC) abgebrochen |
| 80 | Temperatursignal nicht verfügbar |
