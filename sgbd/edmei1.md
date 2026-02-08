# edmei1.prg

- Jobs: [65](#jobs)
- Tables: [98](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektrische Digitale Motorelektronik |
| ORIGIN | BMW EA-451 Reinhard_Schleimer |
| REVISION | 15.001 |
| AUTHOR | Delphi Systems Serge_Anen, Delphi Systems Michel_LEONARD |
| COMMENT | - |
| PACKAGE | 1.986 |
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
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)
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
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223320 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen
- [IDENT_IBS](#job-ident-ibs) - 0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_AEP_INFO_1](#job-status-systemcheck-aep-info-1) - 0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_AEP_INFO_2](#job-status-systemcheck-aep-info-2) - 0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - 0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen
- [STATUS_BZEDIAG](#job-status-bzediag) - 0x22403B STATUS_BZEDIAG BZE Infospeicher
- [STATUS_BZEDIAG2](#job-status-bzediag2) - Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $2E 5F F5 04 Loeschen von pminfo1 index 23-30
- [STATUS_EWS](#job-status-ews) - Zurücklesen verschiedener interner Stati für EWS UDS   : $22   ReadDataByIdentifier UDS   : $C000 Sub-Parameter
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben UDS   : $2E   WriteDataByIdentifier UDS   : $C001 Sub-Parameter
- [STATUS_EWS4_SK](#job-status-ews4-sk) - Lesen des SecretKey des Server sowie Client für EWS4 UDS   : $22   ReadDataByIdentifier UDS   : $C002 Sub-Parameter
- [STEUERN_VERBRAUCHERSTROM_EFII](#job-steuern-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier
- [STEUERN_ENDE_VERBRAUCHERSTROM_EFII](#job-steuern-ende-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier
- [STATUS_VERBRAUCHERSTROM_EFII](#job-status-verbraucherstrom-efii) - Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - 0x332C STATUS_RUHESTROMMESSUNG Auslesen Ruhestromprüfung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - UDS $31 01 F030 Batterietausch registrieren
- [STEUERN_MONTAGEMODUS](#job-steuern-montagemodus) - 0x3101F043 STEUERN_MONTAGEMODUS Ansteuern Montage-Modus.
- [STEUERN_ENDE_MONTAGEMODUS](#job-steuern-ende-montagemodus) - 0x3102F043 STEUERN_ENDE_MONTAGEMODUS Ende Montage-Modus
- [STATUS_MONTAGEMODUS](#job-status-montagemodus) - 0x3103F043 STATUS_MONTAGEMODUS Auslesen Montage-Modus
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - 0x312C STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_INTERLOCK](#job-status-interlock) - 0x31 03 10 61 STATUS OF INTERLOCK BIT Auslesen interlock status bit

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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) oder VERBAUORT eines bestimmten Sensors (table VerbauortTabelle ORT) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_VERBAUORT_NR | long | Verbauort-Nummer des Sensors |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn Teilenummer vom Sensor nicht verfuegbar dann '--' |
| SENSOR_LIN_2_0_FORMAT | int | 1: Die optionalen Daten des Sensors (Hersteller, Seriennummer, ...) werden in LIN_2_Format geliefert 0: Optionale Daten nicht im LIN_2_Format (nur Defaultwerte werden ausgegeben) |
| SENSOR_HERSTELLER_NR | long | Lieferantennummer des Herstellers wenn Hersteller-Nummer nicht verfuegbar, dann 0 |
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann '--' |
| SENSOR_FUNKTIONS_NR | long | Funktionsnummer des Sensors wenn Funktions-Nummer nicht verfuegbar, dann 0 |
| SENSOR_VARIANTEN_NR | long | Variantennummer des Sensors wenn Varianten-Nummer nicht verfuegbar, dann 0 |
| SENSOR_PROD_DATUM | string | Produnktionsdatum (DD.MM.YY) des Sensors wenn Produktions-Datum nicht verfuegbar, dann '--' |
| SENSOR_SERIEN_NR | string | Seriennummer des Sensors wenn Serien-Nummer nicht verfuegbar, dann '--' |
| SENSOR_SW_RELEASE_NR | string | Softwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| SENSOR_HW_RELEASE_NR | string | Hardwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

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
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Information zur Restlaufleistung |
| ST_UN_CBS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_CBS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | % |
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
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| STATUS_MESSUNG | int | Statusbyte |
| STATUS_MESSUNG_TEXT | string | Statusbyte im Klartext |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, Sic, Sic_v, TUV, AU, Ueb, Efk Werte externe Umfaenge: Oel, NOx_a, Br_v, Br_h Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 0xFFh (255 dez) Defaultwert: 100 (0x64h) Bremsflüssigkeit: 150 (0x96h) erlaubt |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 0x0F (15 dez) Defaultwert: 0x0Fh (15 dez) |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 0x3F (63 dez) Defaultwert: 0x3Fh (63 dez) |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
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

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223320 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Status fuer Codierung Laenderfaktor 1 Min: 0 Max: 2.55 |
| STAT_LAENDERFAKTOR_2_WERT | real | Status fuer Codierung Laenderfaktor 2 Min: 0 Max: 2.55 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### STATUS_VERBREDINFO

0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_E1_TAG | unsigned long | Ereignis 1 Tag (Verbredinfo[0]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_MONAT | unsigned long | Ereignis 1 Monat (Verbredinfo[1]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_DAUER_WERT | unsigned long | Ereignis 1 Dauer der Verbraucherreduzierung (Verbredinfo[2]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E1_DAUER_EINH | string | Minute |
| STAT_E1_LRSA | unsigned long | Ereignis 1 Leistungsreduktionstufe A (Verbredinfo[3]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSB | unsigned long | Ereignis 1 Leistungsreduktionstufe B (Verbredinfo[4]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_WCFA | unsigned long | Ereignis 1 Worst Case Fahrerprofil A (Verbredinfo[5]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E1_WCFB | unsigned long | Ereignis 1 Worst Case Fahrerprofil B (Verbredinfo[6]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E2_TAG | unsigned long | Ereignis 2 Tag (Verbredinfo[7]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_MONAT | unsigned long | Ereignis 2 Monat (Verbredinfo[8]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_DAUER_WERT | unsigned long | Ereignis 2 Dauer der Verbraucherreduzierung (Verbredinfo[9]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E2_DAUER_EINH | string | Minute |
| STAT_E2_LRSA | unsigned long | Ereignis 2 Leistungsreduktionstufe A (Verbredinfo[10]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSB | unsigned long | Ereignis 2 Leistungsreduktionstufe B (Verbredinfo[11]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_WCFA | unsigned long | Ereignis 2 Worst Case Fahrerprofil A (Verbredinfo[12]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E2_WCFB | unsigned long | Ereignis 2 Worst Case Fahrerprofil B (Verbredinfo[13]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E3_TAG | unsigned long | Ereignis 3 Tag (Verbredinfo[14]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_MONAT | unsigned long | Ereignis 3 Monat (Verbredinfo[15]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_DAUER_WERT | unsigned long | Ereignis 3 Dauer der Verbraucherreduzierung (Verbredinfo[16]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E3_DAUER_EINH | string | Minute |
| STAT_E3_LRSA | unsigned long | Ereignis 3 Leistungsreduktionstufe A (Verbredinfo[17]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSB | unsigned long | Ereignis 3 Leistungsreduktionstufe B (Verbredinfo[18]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_WCFA | unsigned long | Ereignis 3 Worst Case Fahrerprofil A (Verbredinfo[19]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E3_WCFB | unsigned long | Ereignis 3 Worst Case Fahrerprofil B (Verbredinfo[20]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[21]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[22]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[23]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[24]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[25]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_WCFA | unsigned long | Ereignis 4 Worst Case Fahrerprofil A (Verbredinfo[26]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_WCFB | unsigned long | Ereignis 4 Worst Case Fahrerprofil B (Verbredinfo[27]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_ANZAHL_SCHLECHTE_LABI_GESAMT | unsigned long | Anzahl erkannter schlechter Ladebilanzen (Verbredinfo[28]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ident-ibs"></a>
### IDENT_IBS

0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig vehicle Manufacturer ECU hardware Number Part2 |
| SERIENNUMMER | unsigned long | BMW-Seriennummer SNIBS   Min: 0 Max: 4294967295 |
| ZIF_PROGRAMMSTAND | unsigned long | Programm referenz IBSWBASE   Min: 0 Max: 255 |
| ZIF_STATUS | unsigned long | IBS Software Aenderungs Status (Programm Revision) IBSWCHANG   Min: 0 Max: 255 |
| HW_REF | unsigned long | IBS Hardware Version (Hardware Referenz) IBHWVERSI   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-1"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_1

0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | PMINFO1[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | PMINFO1[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | PMINFO1[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | PMINFO1[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | PMINFO1[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | PMINFO1[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | PMINFO1[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | PMINFO1[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | PMINFO1[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | PMINFO1[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | PMINFO1[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | PMINFO1[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | PMINFO1[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | PMINFO1[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | PMINFO1[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | PMINFO1[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | PMINFO1[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | PMINFO1[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | PMINFO1[22] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | h |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_RUHESTROM_AKTUELL_EINH | string | - |
| STAT_RUHESTROM_VOR_1_ZYKLUS_EINH | string | - |
| STAT_RUHESTROM_VOR_2_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_3_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_4_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_5_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_6_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_7_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_8_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_9_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_10_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_11_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_12_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_13_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_14_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_15_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_16_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_17_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_18_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_19_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_20_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_21_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_22_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_23_ZYKLEN_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-2"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_2

0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | PMINFO2[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | PMINFO2[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | PMINFO2[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | PMINFO2[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | PMINFO2[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | PMINFO2[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | PMINFO2[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | PMINFO2[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | PMINFO2[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | PMINFO2[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | PMINFO2[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | PMINFO2[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | PMINFO2[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | PMINFO2[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | PMINFO2[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | PMINFO2[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | PMINFO2[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | PMINFO2[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | PMINFO2[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | PMINFO2[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | PMINFO2[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | PMINFO2[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | PMINFO2[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | PMINFO2[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | PMINFO2[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | PMINFO2[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | PMINFO2[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | PMINFO2[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-ibs"></a>
### STATUS_MESSWERTE_IBS

0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_T_BATT_WERT | real | Batterietemperatur T_BATT   Einheit: C   Min: -3276.8 Max: 3276.7 |
| STAT_T_BATT_EINH | string | degreeC |
| STAT_U_BATT_WERT | real | Batteriespannung von IBS gemessen U_BATT   Einheit: V   Min: 6 Max: 22.3837 |
| STAT_U_BATT_EINH | string | V |
| STAT_I_BATT_WERT | real | Batteriestrom von IBS gemessen I_BATT   Einheit: A   Min: -200 Max: 5042.8 |
| STAT_I_BATT_EINH | string | A |
| STAT_IBSINFO_01 | unsigned long | DREC_IBSINFO_01 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_02 | unsigned long | DREC_IBSINFO_02 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_03 | unsigned long | DREC_IBSINFO_03 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_04 | unsigned long | Ausgabe 1 Byte in hex, ohne Umrechnung 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_05 | unsigned long | DREC_IBSINFO_05 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_06 | unsigned long | DREC_IBSINFO_06 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_07 | unsigned long | DREC_IBSINFO_07 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_08 | unsigned long | DREC_IBSINFO_08 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_09 | unsigned long | DREC_IBSINFO_09 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_10 | unsigned long | DREC_IBSINFO_10 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_11 | unsigned long | DREC_IBSINFO_11 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_12 | unsigned long | DREC_IBSINFO_12 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_13 | unsigned long | DREC_IBSINFO_13 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_14 | unsigned long | DREC_IBSINFO_14 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_15 | unsigned long | DREC_IBSINFO_15 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_16 | unsigned long | DREC_IBSINFO_16 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_17 | unsigned long | DREC_IBSINFO_17 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_18 | unsigned long | DREC_IBSINFO_18 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_19 | unsigned long | DREC_IBSINFO_19 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_20 | unsigned long | DREC_IBSINFO_20 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_21 | unsigned long | DREC_IBSINFO_21 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_22 | unsigned long | DREC_IBSINFO_22 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag"></a>
### STATUS_BZEDIAG

0x22403B STATUS_BZEDIAG BZE Infospeicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIEKAPAZITAET_AKTUEL_WERT | unsigned long | aktueller Wert C_ist (verfügbare Kapazität) - auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_AKTUEL_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_WERT | unsigned long | C_ist vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_WERT | unsigned long | C_ist vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_WERT | unsigned long | C_ist vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_WERT | unsigned long | C_ist vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_WERT | unsigned long | C_ist vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_EINH | string | Ah |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_WERT | real | Qualitaetsindex C_ist 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_EINH | string | percent |
| STAT_LADEZUSTAND_AKTUELL_WERT | unsigned long | Aktueller Wert C_akt (Ladezustand)- auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_AKTUELL_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_1_TAG_WERT | unsigned long | C_akt vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_1_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_2_TAG_WERT | unsigned long | C_akt vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_2_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_3_TAG_WERT | unsigned long | C_akt vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_3_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_4_TAG_WERT | unsigned long | C_akt vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_4_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_5_TAG_WERT | unsigned long | C_akt vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_5_TAG_EINH | string | Ah |
| STAT_Q_LADEZUSTAND_AKTUELL_WERT | real | Qualitaetsindex C_akt 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_LADEZUSTAND_AKTUELL_EINH | string | percent |
| STAT_STROMAUFNAHME_AKTUELL_WERT | unsigned long | nominierte Stromaufnahme aktuell 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_1_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 1 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_1_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_2_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 2 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_2_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_3_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 3 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_3_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_4_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 4 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_4_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_5_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 5 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_5_MONAT_EINH | string | A |
| STAT_Q_STROMAUFNAHME_AKTUELL_WERT | real | Qualitaetsindex normierte Stromaufnahme 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_Q_BATTERIEZELLE_DEFEKT_WERT | real | Zelldefekt-Signal als Quali-Index 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEZELLE_DEFEKT_EINH | string | percent |
| STAT_ANZ_BATTERIEWECHSEL | unsigned long | Anzahl der bisher getaetigten Batteriewechsel (0 = Originalbatterie) 4BIT_in_0bis15   Min: 0 Max: 15 |
| STAT_LETZTER_BATTERIEWECHSEL_TEXT | string | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) B_bzd_wrgbat |
| STAT_LETZTER_BATTERIEWECHSEL_WERT | int | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) B_bzd_wrgbat |
| STAT_BATTERIEZUSTAND_TEXT | string | Zustand der Batterie / Tauschempfehlung Bzd_btzust |
| STAT_BATTERIEZUSTAND_WERT | int | Zustand der Batterie / Tauschempfehlung Bzd_btzust |
| STAT_WASSERVERLUST_TEXT | string | Anzeige Wasserverlust ueberschreitet Grenzwert B_qvch2o |
| STAT_WASSERVERLUST_WERT | int | Anzeige Wasserverlust ueberschreitet Grenzwert B_qvch2o |
| STAT_TIEFENTLADUNG_TEXT | string | Anzeige Batterie wurde tiefentladen B_bzd_te |
| STAT_TIEFENTLADUNG_WERT | int | Anzeige Batterie wurde tiefentladen B_bzd_te |
| STAT_IBS_BZE_TEXT | string | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_IBS_BZE_WERT | int | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Sommer Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_EINH | string | V |
| STAT_PROGNOSE_KALTSTART_WINTER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_WINTER_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_U_WERT | real | Praedizierter Klemmspannungswert Warmstart Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_VORHALT_WERT | real | Vorhalt praedizierter Klemmspannungswert Warmstart Sommer/Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_VORHALT_EINH | string | V |
| STAT_R_BATTERIE_INITIAL_WERT | real | Initialer Innenwiderstand der Fzg.-Batterie nach Einbau / Tausch Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_INITIAL_EINH | string | mOhm |
| STAT_R_BATTERIE_AKTUELL_WERT | real | aktueller Innenwiderstand der Fzg.-Batterie Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_AKTUELL_EINH | string | mOhm |
| STAT_TREND_WARMSTART_U_WERT | real | Trendwert Klemmspannungsprognose Warmstart Bzd_wcstrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_U_EINH | string | V |
| STAT_TREND_WARMSTART_SOWI_U_WERT | real | Vorhalt Trendwert Klemmspannungsprognose Warmstart Sommer/Winter Bzd_wcwtrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_SOWI_U_EINH | string | V |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_WERT | real | Klimaprofil: Wert vor 0 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_WERT | real | Klimaprofil: Wert vor 1 Monat Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_WERT | real | Klimaprofil: Wert vor 2 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_WERT | real | Klimaprofil: Wert vor 3 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_WERT | real | Klimaprofil: Wert vor 4 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_WERT | real | Klimaprofil: Wert vor 5 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_WERT | real | Klimaprofil: Wert vor 6 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_WERT | real | Klimaprofil: Wert vor 7 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_WERT | real | Klimaprofil: Wert vor 8 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_WERT | real | Klimaprofil: Wert vor 9 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_WERT | real | Klimaprofil: Wert vor 10 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_WERT | real | Klimaprofil: Wert vor 11 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_EINH | string | degreeC |
| STAT_WASSERVERLUSTABS_WERT | real | Wasserverlust Qv_h2o_zg   Einheit: g/Ah   Min: 0 Max: 10 |
| STAT_WASSERVERLUSTABS_EINH | string | grammPerAmpereHour |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_AKTUELL | unsigned long | Vorhalt Sulfatierungsrate (Standzeit bei niedrigem Ladezustand) seit letztem fahrt 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_GESAMT | unsigned long | Vorhalt Sulfatierungsindex (Standzeit in niedrigem Ladezustand) fahrzeugslebendauer 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_ist 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_akt 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_WERT | unsigned long | Absolutzeit juengster Historieneintrag nominierte Stromaufnahme 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_WERT | unsigned long | Absolutzeit juengster Historieneintrag Klima 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_EINH | string | d |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_WERT | unsigned long | Absolutzeit letzte Trendwertermittlung 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_EINH | string | d |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_WERT | unsigned long | Zeit seit letztem Batterietausch 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_EINH | string | d |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_WERT | unsigned long | Entladung waehrend Motor aus &lt; -10Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen -10Ah und 0Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 0Ah und 5Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 5Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 10Ah und 15Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 15Ah und 25Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 25Ah und 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_WERT | unsigned long | Entladung waehrend Motor aus &gt; 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_WERT | unsigned long | Ladung waehrend Motor ein &lt; -20Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -20Ah und -10Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -10Ah und 0Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 0Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 10Ah und 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_WERT | unsigned long | Ladung waehrend Motor ein &gt; 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_EINH | string | Ah |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag2"></a>
### STATUS_BZEDIAG2

Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTLADUNG_MSA_BEREICH1 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 1) |
| STAT_ENTLADUNG_MSA_BEREICH2 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 2) |
| STAT_ENTLADUNG_MSA_BEREICH3 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 3) |
| STAT_ENTLADUNG_MSA_BEREICH4 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 4) |
| STAT_ENTLADUNG_MSA_BEREICH5 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 5) |
| STAT_ENTLADUNG_MSA_BEREICH6 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 6) |
| STAT_ENTLADUNG_MSA_BEREICH7 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 7) |
| STAT_ENTLADUNG_MSA_BEREICH8 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 8) |
| STAT_TIEFENTLADUNG_AKTUELL | real | Index für Schädigungsgrad der aktuellen Tiefentladung |
| STAT_TIEFENTLADUNG_GESAMT | real | Index für den Schädigungsgrad aller Tiefentladungen |
| STAT_SOH_CIST | real | Alterungsindex auf Basis C_ist |
| STAT_SOH_WASSERVERLUST | real | Alterungsindex auf Basis Qv_h2o_zg |
| STAT_SOH_STANDZEIT | real | Alterungsindex auf Basis Bzd_sulfind |
| STAT_SOH_ZYKLEN | real | Alterungsindex auf Basis SoC-abhängiger Zyklenzähler |
| STAT_SOH_ENTLADUNG_STAND | real | Alterungsindex auf Basis Entladehistogramm im Stand |
| STAT_SOH_LADUNG_FAHRT | real | Alterungsindex auf Basis Ladehistogramm während der Fahrt |
| STAT_SOH_ENTLADUNG_MSA | real | Alterungsindex auf Basis Entladehistogramm im MSA-Stopp |
| STAT_SOH_TIEFENTLADUNG | real | Alterungsindex auf Basis Bzd_tiefentlabs |
| STAT_SOH_BATTERIE | real | Index für den aktuellen Alterungszustand der Batterie (SoH) |
| STAT_VOLLZYKLEN_GEWICHTET | real | Vollzyklenzähler der Batterie. Entladung wird je nach SoC gewichtet |
| STAT_ENTLADUNG_GEWICHTET_WERT | real | gewichteter Enladezähler abhängig vom SoC |
| STAT_ENTLADUNG_GEWICHTET_EINH | string | Einheit des gewichteten Enladezählers (Ah) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$2E 5F F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-status-ews"></a>
### STATUS_EWS

Zurücklesen verschiedener interner Stati für EWS UDS   : $22   ReadDataByIdentifier UDS   : $C000 Sub-Parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört) 1 Freigabe erteilt (Challenge-Response erfolgreich) 2 Freigabe abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string | Text zu Status Wert |
| STAT_DH_ACTIVE | int | 0 Diffie-Hellman-Abgleich nicht aktiv 1 Diffie-Hellman-Abgleich aktiv |
| STAT_E_LABEL_ACTIVE | int | 0 E-Label ist nicht aktiv 1 E-Label ist aktiv |
| STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string | Freie Plaetze |
| STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string | Freie Plaetze |
| STAT_VERSION | int | 0x01 Direktschreiben des SecretKey 0x02 Direktschreiben des SecretKey und DH-Abgleich |
| _STAT_VERSION_TXT | string | Version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben UDS   : $2E   WriteDataByIdentifier UDS   : $C001 Sub-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK UNLOCK_CLIENT_SK |
| DATEN | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

Lesen des SecretKey des Server sowie Client für EWS4 UDS   : $22   ReadDataByIdentifier UDS   : $C002 Sub-Parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | SecretKey Server |
| STAT_EWS4_CLIENT_SK | binary | SecretKey Client |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-verbraucherstrom-efii"></a>
### STEUERN_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STARTTRIGGERWERT | long | Ecos2 Start Trigger Wert [mA] |
| AUSSCHALTTRIGGER | long | Ecos2 Ende Trigger Wert [mA] |
| TOTZEIT | int | Ecos2 Strommessung holdoff Zeit [ms] |
| MESSZEIT | int | Ecos2 Messzeit [ms] |
| UNTERE_TOLERANZ | long | Ecos2 untere Stromschwelle [mA] |
| OBERE_TOLERANZ | long | Ecos2 obere Stromschwelle [mA] |
| MESSPUNKTE | int | Ecos2 Anzahl Messpunkte [-] |
| TRIGGERFILTER | int | Ecos2 Triggerfilter [ms] |
| MESSWERTFILTER | int | Ecos2 Messfilter [ms] |
| TIMEOUT | int | Ecos2 timeout Zeit [s] |
| POSTTRIGGER | int | Ecos2 Nachtrigger Aufzeichnung [ms] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-verbraucherstrom-efii"></a>
### STEUERN_ENDE_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verbraucherstrom-efii"></a>
### STATUS_VERBRAUCHERSTROM_EFII

Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_WERT | unsigned int | Ecos2 Funktionsstati Wert |
| STAT_STATUS_EINH | string | percent |
| STAT_STATUS_TEXT | string | Ecos2 Funktionsstati Text |
| STAT_BEWERTUNG | char | Ecos2 Resultat Bewertung |
| STAT_GRUNDWERT_WERT | real | Ecos2 Strom Grundwert in A |
| STAT_GRUNDWERT_EINH | string | Strom in A |
| STAT_DIFFERENZWERT_WERT | real | Ecos2 Strom Messwert in A |
| STAT_DIFFERENZWERT_EINH | string | Strom in A |
| STAT_TRANSIENT | binary | Transienten Array |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

0x332C STATUS_RUHESTROMMESSUNG Auslesen Ruhestromprüfung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM (Eco_jobstat1) 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RUHESTROM_WERT | int | Status_Fehlerspeicher_Ruhestromwert |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom (Eco_result1) Eco_result1   Einheit: A   Min: 0 Max: 81.9187 |
| STAT_STAT_RUHESTROM_EINH | string | A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

UDS $31 01 F030 Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-montagemodus"></a>
### STEUERN_MONTAGEMODUS

0x3101F043 STEUERN_MONTAGEMODUS Ansteuern Montage-Modus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-montagemodus"></a>
### STEUERN_ENDE_MONTAGEMODUS

0x3102F043 STEUERN_ENDE_MONTAGEMODUS Ende Montage-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-montagemodus"></a>
### STATUS_MONTAGEMODUS

0x3103F043 STATUS_MONTAGEMODUS Auslesen Montage-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_MONTAGEMODUS_TEXT | string | FUNKTIONSSTATUS MONTAGEMODUS 1BYTE FUNKTIONSSTATUS |
| STAT_FS_MONTAGEMODUS_WERT | int | FUNKTIONSSTATUS MONTAGEMODUS 1BYTE FUNKTIONSSTATUS |
| STAT_ST_MONTAGE_MODUS_TEXT | string | Status Montage-Modus aktiv/inaktiv 1BYTE STATUS MONTAGE_MODUS |
| STAT_ST_MONTAGE_MODUS_WERT | int | Status Montage-Modus aktiv/inaktiv 1BYTE STATUS MONTAGE_MODUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

0x312C STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Eco_max_i   Einheit: A   Min: 0 Max: 0.3187 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Eco_msb   Einheit: s   Min: 0 Max: 12.75 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Eco_mz   Einheit: s   Min: 0 Max: 12.75 |
| TO_WERT | unsigned long | Ecos Messung Timeout (Eco_timo) Eco_timo   Einheit: s   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-status-interlock"></a>
### STATUS_INTERLOCK

0x31 03 10 61 STATUS OF INTERLOCK BIT Auslesen interlock status bit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_INTERLOCK_TEXT | string | Status of INTERLOCK bit Unlocked/Locked 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
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
- [VERBAUORTTABELLE](#table-verbauorttabelle) (361 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (224 × 2)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [CBSKENNUNG](#table-cbskennung) (12 × 3)
- [ARG_0X4114_D](#table-arg-0x4114-d) (1 × 12)
- [ARG_0X4115_D](#table-arg-0x4115-d) (1 × 12)
- [ARG_0X4116_D](#table-arg-0x4116-d) (1 × 12)
- [ARG_0X4117_D](#table-arg-0x4117-d) (1 × 12)
- [ARG_0X4119_D](#table-arg-0x4119-d) (1 × 12)
- [ARG_0X411A_D](#table-arg-0x411a-d) (1 × 12)
- [ARG_0X411B_D](#table-arg-0x411b-d) (1 × 12)
- [ARG_0X4140_D](#table-arg-0x4140-d) (1 × 12)
- [ARG_0X4141_D](#table-arg-0x4141-d) (1 × 12)
- [ARG_0X4142_D](#table-arg-0x4142-d) (1 × 12)
- [ARG_0X4143_D](#table-arg-0x4143-d) (1 × 12)
- [ARG_0X4144_D](#table-arg-0x4144-d) (1 × 12)
- [ARG_0X4145_D](#table-arg-0x4145-d) (1 × 12)
- [ARG_0X60C3_D](#table-arg-0x60c3-d) (1 × 12)
- [ARG_0X63F0_D](#table-arg-0x63f0-d) (1 × 12)
- [ARG_0XADC2_R](#table-arg-0xadc2-r) (1 × 14)
- [ARG_0XADC6_R](#table-arg-0xadc6-r) (1 × 14)
- [ARG_0XADC7_R](#table-arg-0xadc7-r) (1 × 14)
- [ARG_0XADC8_R](#table-arg-0xadc8-r) (1 × 14)
- [ARG_0XADF3_R](#table-arg-0xadf3-r) (2 × 14)
- [ARG_0XDE23_D](#table-arg-0xde23-d) (1 × 12)
- [ARG_0XDEE3_D](#table-arg-0xdee3-d) (1 × 12)
- [ARG_0XDEFC_D](#table-arg-0xdefc-d) (1 × 12)
- [ARG_0XDF4E_D](#table-arg-0xdf4e-d) (1 × 12)
- [ARG_0XF000_R](#table-arg-0xf000-r) (1 × 14)
- [ARG_0XF086_R](#table-arg-0xf086-r) (1 × 14)
- [ARG_0XF087_R](#table-arg-0xf087-r) (1 × 14)
- [BETRIEBSART_EM](#table-betriebsart-em) (6 × 2)
- [BF_AKKS_ERROR](#table-bf-akks-error) (3 × 10)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (336 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (58 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (29 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (16 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0X409D_D](#table-res-0x409d-d) (47 × 10)
- [RES_0X409E_D](#table-res-0x409e-d) (16 × 10)
- [RES_0XA1D0_R](#table-res-0xa1d0-r) (2 × 13)
- [RES_0XADC2_R](#table-res-0xadc2-r) (2 × 13)
- [RES_0XADC6_R](#table-res-0xadc6-r) (2 × 13)
- [RES_0XADC7_R](#table-res-0xadc7-r) (1 × 13)
- [RES_0XADC8_R](#table-res-0xadc8-r) (1 × 13)
- [RES_0XADF3_R](#table-res-0xadf3-r) (2 × 13)
- [RES_0XDE9C_D](#table-res-0xde9c-d) (3 × 10)
- [RES_0XDEE1_D](#table-res-0xdee1-d) (6 × 10)
- [RES_0XDEE2_D](#table-res-0xdee2-d) (18 × 10)
- [RES_0XDEFD_D](#table-res-0xdefd-d) (51 × 10)
- [RES_0XDEFE_D](#table-res-0xdefe-d) (16 × 10)
- [RES_0XDF53_D](#table-res-0xdf53-d) (9 × 10)
- [RES_0XDF54_D](#table-res-0xdf54-d) (5 × 10)
- [RES_0XDF55_D](#table-res-0xdf55-d) (2 × 10)
- [RES_0XDF56_D](#table-res-0xdf56-d) (32 × 10)
- [RES_0XDF5E_D](#table-res-0xdf5e-d) (3 × 10)
- [RES_0XF000_R](#table-res-0xf000-r) (1 × 13)
- [RES_0XF086_R](#table-res-0xf086-r) (2 × 13)
- [RES_0XF087_R](#table-res-0xf087-r) (2 × 13)
- [RES_0XF0D5_R](#table-res-0xf0d5-r) (6 × 13)
- [SG_FUNKTIONEN](#table-sg-funktionen) (67 × 16)
- [TABLE_STATUS_ECO2_FUNKTIONSSTATI](#table-table-status-eco2-funktionsstati) (11 × 2)
- [TAB_12VLADEN_LADEFEHLER](#table-tab-12vladen-ladefehler) (7 × 2)
- [TAB_AEP_DIAG_GRUND_LADEENDE](#table-tab-aep-diag-grund-ladeende) (17 × 2)
- [TAB_ANSTEUERUNG_LUEFTER_RELAIS](#table-tab-ansteuerung-luefter-relais) (3 × 2)
- [TAB_ENTLUEFTUNGSROUTINE_STATUS](#table-tab-entlueftungsroutine-status) (5 × 2)
- [TAB_KAELTEMITTEL_ABSPERRVENTIL_OEFFNEN_SCHLIESSEN](#table-tab-kaeltemittel-absperrventil-oeffnen-schliessen) (3 × 2)
- [TAB_LUEFTER](#table-tab-luefter) (6 × 2)
- [TAB_ST_DIAG_EWP21](#table-tab-st-diag-ewp21) (5 × 2)
- [TAB_ZYKNL_GRUND_LADEENDE](#table-tab-zyknl-grund-ladeende) (8 × 2)
- [_MOTORUDSCODIERUNG_RUHESTROM](#table-motorudscodierung-ruhestrom) (16 × 2)
- [TABLE_STATUS_LETZTER_BATTERIEWECHSEL](#table-table-status-letzter-batteriewechsel) (2 × 2)
- [TABLE_STATUS_BATTERIEZUSTAND](#table-table-status-batteriezustand) (4 × 2)
- [TABLE_STATUS_WASSERVERLUST](#table-table-status-wasserverlust) (2 × 2)
- [TABLE_STATUS_TIEFENTLADUNG](#table-table-status-tiefentladung) (2 × 2)
- [TABLE_STATUS_IBS_BZE](#table-table-status-ibs-bze) (2 × 2)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [IBS_DEAK](#table-ibs-deak) (10 × 2)
- [TAB_AE_FUNKSTAT_MONTAGEMODUS](#table-tab-ae-funkstat-montagemodus) (12 × 2)
- [TAB_AE_STAT_MONTAGEMODUS](#table-tab-ae-stat-montagemodus) (4 × 2)
- [TAB_STATUS_INTERLOCK](#table-tab-status-interlock) (2 × 2)

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 361 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
| 0x03A0 | Druck- Temperatursensor Tank | 1 |
| 0x03C0 | EAC-Sensor | - |
| 0x0400 | Schaltzentrum Lenksäule | - |
| 0x0500 | DSC Sensor-Cluster | - |
| 0x0600 | Nahbereichsradarsensor links | - |
| 0x0700 | Nahbereichsradarsensor rechts | - |
| 0x0800 | Funkempfänger | - |
| 0x0900 | Elektrische Lenksäulenverriegelung | - |
| 0x0A00 | Regen- Lichtsensor | - |
| 0x290A00 | DSC Hydraulikblock | - |
| 0x0B00 | Nightvision Kamera | - |
| 0x0C00 | TLC Kamera | - |
| 0x0D00 | Spurwechselradarsensor hinten links | - |
| 0x0E00 | Heckklima Bedienteil rechts | 1 |
| 0x0F00 | Rearview Kamera hinten | 1 |
| 0x0F80 | Frontview Kamera vorne | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1210 | Sideview Kamera Kotflügel vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1310 | Sideview Kamera Kotflügel vorne rechts | 1 |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A20 | Schalterblock Sitzheizung hinten links | 1 |
| 0x1A40 | Schalterblock Sitzheizung hinten rechts | 1 |
| 0x1A60 | Sitzheizung Fahrer | 1 |
| 0x1A80 | Sitzheizung Beifahrer | 1 |
| 0x1AA0 | Sitzheizung Fahrer hinten | 1 |
| 0x1AC0 | Sitzheizung Beifahrer hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1C80 | Sitzverstellschalter Beifahrer über Fond | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1E40 | Heckklappenemblem | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2110 | DWA Mikrowellensensor vorne rechts | 1 |
| 0x2120 | DWA Mikrowellensensor hinten rechts | 1 |
| 0x2130 | DWA Mikrowellensensor hinten links | 1 |
| 0x2140 | DWA Mikrowellensensor vorne links | 1 |
| 0x2150 | DWA Mikrowellensensor hinten | 1 |
| 0x2180 | DWA Ultraschallsensor | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2210 | Aussenspiegel Fahrer | 1 |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2310 | Aussenspiegel Beifahrer | 1 |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
| 0x2D00 | Smart Opener | 1 |
| 0x2E00 | LED-Hauptlicht-Modul links | 1 |
| 0x2F00 | LED-Hauptlicht-Modul rechts | 1 |
| 0x0910 | Elektrische Lenksäulenverriegelung | 1 |
| 0x3200 | Funkempfänger | 1 |
| 0x3300 | Funkempfänger 2 | 1 |
| 0x3400 | Türgriffelektronik Fahrer | - |
| 0x3500 | Türgriffelektronik Beifahrer | - |
| 0x3600 | Türgriffelektronik Fahrer hinten | - |
| 0x3700 | Türgriffelektronik Beifahrer hinten | - |
| 0x3800 | Telestart-Handsender 1 | - |
| 0x3900 | Telestart-Handsender 2 | - |
| 0x3A00 | Fond-Fernbedienung | - |
| 0x3B00 | Elektrische Wasserpumpe | 1 |
| 0x3B10 | Elektrische Wasserpumpe 1 | 1 |
| 0x3B20 | Elektrische Wasserpumpe 2 | 1 |
| 0x3B30 | Elektrische Wasserpumpe 22 | 1 |
| 0x3B40 | Elektrische Wasserpumpe 23 | 1 |
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3D10 | Aktiver Kühlluftklappensteller oberer Kühllufteinlass | 1 |
| 0x3D20 | Aktiver Kühlluftklappensteller unterer Kühllufteinlass | 1 |
| 0x3D80 | Lüfter | 1 |
| 0x3D88 | Lüfter 2 | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3E80 | DCDC Versorgung Zustartbatterie | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4600 | Nackenwärmer | 1 |
| 0x4700 | Nackenwärmer Bedienschalter | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4C80 | Klimabedienteil 3. Sitzreihe | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6180 | LIN-Zusatzwasserpumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x6500 | Sense-Touch-Modul links | 1 |
| 0x6600 | Sense-Touch-Modul rechts | 1 |
| 0x6700 | Hochdruck- Temperatursensor 1 | 1 |
| 0x6710 | Niederdruck- Temperatursensor 1 | 1 |
| 0x6720 | Elektrisches Expansionsventil | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
| 0x570C | Satellit Upfront mitte | 0 |
| 0x5710 | Satellit Tür links | 0 |
| 0x5718 | Satellit Tür rechts | 0 |
| 0x5720 | Satellit B-Säule links X | 0 |
| 0x5728 | Satellit B-Säule rechts X | 0 |
| 0x5730 | Satellit B-Säule links Y | 0 |
| 0x5738 | Satellit B-Säule rechts Y | 0 |
| 0x5740 | Satellit Zentralsensor X | 0 |
| 0x5748 | Satellit Zentralsensor Y | 0 |
| 0x5750 | Satellit Zentralsensor Low g Y | 0 |
| 0x5758 | Satellit Zentralsensor Low g Z | 0 |
| 0x5760 | Satellit Zentralsensor Roll Achse | 0 |
| 0x5768 | Fussgängerschutz Sensor vorne links | 0 |
| 0x5770 | Fussgängerschutz Sensor vorne rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor vorne mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5782 | Fussgängerschutz Zusatzsensor Beschleunigung links | 0 |
| 0x5784 | Fussgängerschutz Zusatzsensor Beschleunigung rechts | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x57C0 | Satellit Drucksensor Schlauch PTS 1 vorne links p | 0 |
| 0x57C4 | Satellit Drucksensor Schlauch PTS 1 vorne rechts p | 0 |
| 0x57C8 | Satellit Drucksensor Schlauch PTS 2 vorne links p | 0 |
| 0x57CC | Satellit Drucksensor Schlauch PTS 2 vorne rechts p | 0 |
| 0x57D0 | Beschleunigungssensor vorne links X | 0 |
| 0x57D4 | Beschleunigungssensor vorne mitte X | 0 |
| 0x57D8 | Beschleunigungssensor vorne rechts X | 0 |
| 0x57DC | Beschleunigungssensor hinten mitte X | 0 |
| 0x57E0 | Sitzbelegungserkennung Beifahrer CIS/Bladder | 1 |
| 0x57E4 | Sitzbelegungserkennung 2. Sitzreihe links CIS/Bladder | 1 |
| 0x57E8 | Sitzbelegungserkennung 2. Sitzreihe rechts CIS/Bladder | 1 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0x5A00 | Innenlichtelektronik | 1 |
| 0x5A01 | Innenbeleuchtung - Lichtschwert links | 1 |
| 0x5A02 | Innenbeleuchtung - Lichtschwert rechts | 1 |
| 0x5A03 | Innenbeleuchtung - Lautsprecher Hutablage rechts | 1 |
| 0x5A04 | Innenbeleuchtung - Lautsprecher Hutablage links | 1 |
| 0x5A05 | Innenbeleuchtung - Lautsprecher hinten links | 1 |
| 0x5A06 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne links | 1 |
| 0x5A07 | Innenbeleuchtung - Lautsprecher Hochtöner vorne links | 1 |
| 0x5A08 | Innenbeleuchtung - Lautsprecher hinten rechts | 1 |
| 0x5A09 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne rechts | 1 |
| 0x5A0A | Innenbeleuchtung - Lautsprecher Hochtöner vorne rechts | 1 |
| 0x5A0B | Innenbeleuchtung - Lautsprecher Centerspeaker | 1 |
| 0x5A0C | Innenbeleuchtung - Panoramadach LED Modul 1 (hinteres Glasfestelement) | 1 |
| 0x5A0D | Innenbeleuchtung - Panoramadach LED Modul 2 (hinteres Glasfestelement) | 1 |
| 0x5A0E | Innenbeleuchtung - Panoramadach LED Modul 3 (hinteres Glasfestelement) | 1 |
| 0x5A0F | Innenbeleuchtung - Panoramadach LED Modul 4 (hinteres Glasfestelement) | 1 |
| 0x5A10 | Innenbeleuchtung - Panoramadach LED Modul 5 (vorderes Glasschiebedach) | 1 |
| 0x5A11 | Innenbeleuchtung - Panoramadach LED Modul 6 (vorderes Glasschiebedach) | 1 |
| 0x5A12 | Innenbeleuchtung - Panoramadach LED Modul 7 (vorderes Glasschiebedach) | 1 |
| 0x5A13 | Innenbeleuchtung - Panoramadach LED Modul 8 (vorderes Glasschiebedach) | 1 |
| 0x5A14 | Touch Command Snap-In Adapter - Mittelkonsole Fond | 1 |
| 0x5A20 | Innenlichteinheit 2 | 1 |
| 0x5A30 | Innenlichteinheit 3 | 1 |
| 0x5A40 | Innenlichteinheit 4 | 1 |
| 0x5A50 | Innenlichteinheit 5 | 1 |
| 0x5AFF | unbekannter Verbauort | - |
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
| 0x5B60 | Fondcontroller | 1 |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Konturlinie Fahrertür vorne | 1 |
| 0x5E06 | Innenbeleuchtung Dekor indirekt Fahrertür vorne | 1 |
| 0x5E07 | Innenbeleuchtung Türöffner Fahrertür vorne | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Konturlinie Fahrertür hinten | 1 |
| 0x5E0A | Innenbeleuchtung Dekor indirekt Fahrertür hinten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Konturlinie Beifahrertür vorne | 1 |
| 0x5E0D | Innenbeleuchtung Dekor indirekt Beifahrertür vorne | 1 |
| 0x5E0E | Innenbeleuchtung Türöffner Beifahrertür vorne | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Konturlinie Beifahrertür hinten | 1 |
| 0x5E11 | Innenbeleuchtung Dekor indirekt Beifahrertür hinten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung Konturlinie I-Tafel Fahrer | 1 |
| 0x5E14 | Innenbeleuchtung Dekor indirekt I-Tafel Fahrer | 1 |
| 0x5E15 | Innenbeleuchtung Konturlinie I-Tafel Mitte | 1 |
| 0x5E16 | Innenbeleuchtung Dekor indirekt I-Tafel Mitte | 1 |
| 0x5E17 | Innenbeleuchtung Konturlinie I-Tafel Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung Dekor indirekt I-Tafel Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack Ablagefach | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0x5E21 | Innenbeleuchtung Türöffner Fahrertür hinten | 1 |
| 0x5E22 | Innenbeleuchtung Türöffner Beifahrertür hinten | 1 |
| 0x5E23 | Innenbeleuchtung Fußraum Fahrer 3SR | 1 |
| 0x5E24 | Innenbeleuchtung Fußraum Beifahrer 3SR | 1 |
| 0x5E25 | Innenbeleuchtung Kartentasche Fahrertür 3SR | 1 |
| 0x5E26 | Innenbeleuchtung Kartentasche Beifahrertür 3SR | 1 |
| 0x5E27 | Innenbeleuchtung Konturlinie Fahrertür 3SR | 1 |
| 0x5E28 | Innenbeleuchtung Konturlinie Beifahrertür 3SR | 1 |
| 0x5E29 | Innenbeleuchtung Dekor indirekt Fahrertür 3SR | 1 |
| 0x5E2A | Innenbeleuchtung Dekor indirekt Beifahrertür 3SR | 1 |
| 0x5E2B | Innenbeleuchtung Konturlinie Mittelkonsole Fahrer vorne | 1 |
| 0x5E2C | Innenbeleuchtung Konturlinie Mittelkonsole Fahrer hinten | 1 |
| 0x5E2D | Innenbeleuchtung Konturlinie Mittelkonsole Beifahrer vorne | 1 |
| 0x5E2E | Innenbeleuchtung Konturlinie Mittelkonsole Beifahrer hinten | 1 |
| 0x5E2F | Innenbeleuchtung Dekor indirekt Mittelkonsole Fahrer vorne | 1 |
| 0x5E30 | Innenbeleuchtung Dekor indirekt Mittelkonsole Fahrer hinten | 1 |
| 0x5E31 | Innenbeleuchtung Dekor indirekt Mittelkonsole Beifahrer vorne | 1 |
| 0x5E32 | Innenbeleuchtung Dekor indirekt Mittelkonsole Beifahrer hinten | 1 |
| 0x5E33 | Innenbeleuchtung Backpanel Fahrersitz 2SR | 1 |
| 0x5E34 | Innenbeleuchtung Backpanel Beifahrersitz 2SR | 1 |
| 0x5E35 | Innenbeleuchtung Panoramadach Glasdeckel Front links vorne | 1 |
| 0x5E36 | Innenbeleuchtung Panoramadach Glasdeckel Front links hinten | 1 |
| 0x5E37 | Innenbeleuchtung Panoramadach Glasdeckel Front rechts vorne | 1 |
| 0x5E38 | Innenbeleuchtung Panoramadach Glasdeckel Front rechts hinten | 1 |
| 0x5E39 | Innenbeleuchtung Panoramadach Glasdeckel Fond links vorne | 1 |
| 0x5E3A | Innenbeleuchtung Panoramadach Glasdeckel Fond links hinten | 1 |
| 0x5E3B | Innenbeleuchtung Panoramadach Glasdeckel Fond rechts vorne | 1 |
| 0x5E3C | Innenbeleuchtung Panoramadach Glasdeckel Fond rechts hinten | 1 |
| 0x5E3D | Innenbeleuchtung Lichtschwert links | 1 |
| 0x5E3E | Innenbeleuchtung Lichtschwert rechts | 1 |
| 0x5E3F | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne vorne | 1 |
| 0x5E40 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne hinten | 1 |
| 0x5E41 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten vorne | 1 |
| 0x5E42 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten hinten | 1 |
| 0x5E43 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne vorne | 1 |
| 0x5E44 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne hinten | 1 |
| 0x5E45 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten vorne | 1 |
| 0x5E46 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten hinten | 1 |
| 0x5E47 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Fahrer vorne | 1 |
| 0x5E48 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Fahrer hinten | 1 |
| 0x5E49 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Beifahrer vorne | 1 |
| 0x5E4A | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Beifahrer hinten | 1 |
| 0x5E4B | Innenbeleuchtung Cupholder vorne | 1 |
| 0x5E4C | Innenbeleuchtung Cupholder hinten | 1 |
| 0x5E4D | Innenbeleuchtung Kartentasche Fahrertür hinten 2 | 1 |
| 0x5E4E | Innenbeleuchtung Kartentasche Beifahrertür hinten 2 | 1 |
| 0x5E4F | Innenbeleuchtung Dekor hinterleuchtet I-Tafel Beifahrer oben | 1 |
| 0x5E50 | Innenbeleuchtung Dekor hinterleuchtet I-Tafel Beifahrer unten | 1 |
| 0x5E51 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne oben | 1 |
| 0x5E52 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne unten | 1 |
| 0x5E53 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten oben | 1 |
| 0x5E54 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten unten | 1 |
| 0x5E55 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne oben | 1 |
| 0x5E56 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne unten | 1 |
| 0x5E57 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten oben | 1 |
| 0x5E58 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten unten | 1 |
| 0x5E59 | Innenbeleuchtung Hochtöner Fahrertür vorne | 1 |
| 0x5E5A | Innenbeleuchtung Hochtöner Beifahrertür vorne | 1 |
| 0x5E5B | Innenbeleuchtung Mitteltöner Fahrertür vorne | 1 |
| 0x5E5C | Innenbeleuchtung Mitteltöner Beifahrertür vorne | 1 |
| 0x5E5D | Innenbeleuchtung Mitteltöner Fahrertür hinten | 1 |
| 0x5E5E | Innenbeleuchtung Mitteltöner Beifahrertür hinten | 1 |
| 0x5E5F | Innenbeleuchtung Centerspeaker | 1 |
| 0x5E60 | Innenbeleuchtung Fireplace Mittelkonsole vorne | 1 |
| 0x5E61 | Innenbeleuchtung Fireplace Mittelkonsole hinten | 1 |
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
| 0x5EC0 | Thermocupholder | 1 |
| 0x5F00 | Integrierte Fensterheber Elektronik Fahrer | 1 |
| 0x5F10 | Integrierte Fensterheber Elektronik Beifahrer | 1 |
| 0x5F20 | Integrierte Fensterheber Elektronik Fahrer hinten | 1 |
| 0x5F30 | Integrierte Fensterheber Elektronik Beifahrer hinten | 1 |
| 0x5F40 | Schalterblock Sitzmemory Fahrer | 1 |
| 0x5F50 | Schalterblock Sitzmemory Beifahrer | 1 |
| 0x5F60 | Schalterblock Sitzmemory Fahrer hinten | 1 |
| 0x5F70 | Schalterblock Sitzmemory Beifahrer hinten | 1 |
| 0x5F80 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x5F90 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x5FA0 | Bedieneinheit Mittelkonsole | 1 |
| 0x5FB0 | WB und SARAH Schalter | 1 |
| 0x5FC0 | ABW-Türschloss Fahrer | 1 |
| 0x5FD0 | ABW-Türschloss Beifahrer | 1 |
| 0x7000 | Abschattungs-Elektronik-Dach | 1 |
| 0x7040 | Frontwischermotor | 1 |
| 0x7100 | NFC Leser Innenraum vorne | 1 |
| 0x7108 | NFC Leser Türgriff Fahrer | 1 |
| 0x7200 | Spurwechselradarsensor vorne rechts | 1 |
| 0x7208 | Spurwechselradarsensor vorne links | 1 |
| 0x7210 | Spurwechselradarsensor hinten rechts (Master) | 1 |
| 0x7218 | Spurwechselradarsensor hinten links | 1 |
| 0x7300 | Tanksensor links | 1 |
| 0x7310 | Tanksensor rechts | 1 |
| 0x7400 | Cargo Steuergeraet | 1 |
| 0x7500 | CID-Klappe | 1 |
| 0x7600 | Handschuhkasten | 1 |
| 0x7620 | Sternenhimmel Steuergerät | 1 |
| 0x7640 | Partition Wall Steuergerät | 1 |
| 0x7680 | Durchreiche Partition Wall | 1 |
| 0x76A0 | Bedienelement Dach | 1 |
| 0x7700 | Booster | 1 |
| 0x7800 | Dualspeicher | 1 |
| 0x7900 | Tablet | - |
| 0x7A00 | Beschleunigungssensor vorne links | 1 |
| 0x7A08 | Beschleunigungssensor vorne rechts | 1 |
| 0x7A10 | Beschleunigungssensor hinten links | 1 |
| 0x7A18 | Beschleunigungssensor hinten rechts | 1 |
| 0x7A20 | Abdeckrollo-Steuergerät | 1 |
| 0x7A28 | Schalterblock Gepäckraum | 1 |
| 0x7A30 | Unteres Heckklappenschloss links | 1 |
| 0x7A38 | Unteres Heckklappenschloss rechts | 1 |
| 0x7A40 | Elektrische Getriebeoelpumpe | 1 |
| 0x7B00 | ISC - Inertial Sensor Cluster | 1 |
| 0x7C00 | elektrischer Durchlaufheizer Hochvoltspeicher | 1 |
| 0xF000 | Motorrad Tachometer | 1 |
| 0xF010 | Motorrad Drehzahlmesser | 1 |
| 0xF020 | Motorrad Leistungsanzeige | 1 |
| 0xF030 | Motorrad Tankanzeige | 1 |
| 0xF040 | Motorrad 5Wege-Kombischalter links | 1 |
| 0xF050 | Motorrad Kombischalter rechts | 1 |
| 0xF060 | Motorrad Favoritentasterblock | 1 |
| 0xF070 | Motorrad Scheinwerfer | 1 |
| 0xF080 | Motorrad Radiobedienteil | 1 |
| 0xF090 | Motorrad Kombischalter links | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 224 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | Daimler AG |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars |
| 0x0008 | Ford Motor Company |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis GmbH |
| 0x0014 | Microchip Technology Inc |
| 0x0015 | Centro Ricerche FIAT |
| 0x0016 | Renesas Technology Europe GmbH (formerly Mitsubishi) |
| 0x0017 | Atmel Germany GmbH |
| 0x0018 | Magneti Marelli S.p. A |
| 0x0019 | NEC Electronics GmbH |
| 0x001A | Fujitsu Microelectronics Europe GmbH |
| 0x001B | Adam Opel AG |
| 0x001C | Infineon Technologies AG |
| 0x001D | AMI Semiconductor Belguim BVBA |
| 0x001E | Vector Informatik GmbH |
| 0x001F | Brose Fahrzeugteile GmbH & Co |
| 0x0020 | Zentrum Mikroelektronik Dresden AG |
| 0x0021 | ihr GmbH |
| 0x0022 | Visteon Deutschland GmbH |
| 0x0023 | Elmos Semiconductor AG |
| 0x0024 | ON Semiconductor Germany GmbH |
| 0x0025 | Denso Corporation |
| 0x0026 | C&S Group GmbH |
| 0x0027 | Renault SA |
| 0x0028 | Renesas Technology Europe Ltd (formerly Hitachi) |
| 0x0029 | Yazaki Europe Ltd |
| 0x002A | Trinamic Microchips GmbH |
| 0x002B | Allegro Microsystems, Inc |
| 0x002C | Toyota Motor Engineering and Manufacturing Europe N.V / S.A |
| 0x002D | PSA Peugeot Citroën |
| 0x002E | Forschungs - und Transferzentrum e.V. der Westsächsische Hochschule Zwickau |
| 0x002F | Micron Electronic Devices AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA & Co. |
| 0x0037 | Continental Automotive |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH - Robert Bosch |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electrics Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | DST Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies, Inc. |
| 0x0055 | Lear Corporation  |
| 0x0056 | KOSTAL Ireland GmbH |
| 0x0057 | LIPOWSKY Industrie-Elektronik GmbH  |
| 0x0058 | Sanken Electric Co.,Ltd |
| 0x0059 | Elektrobit Automotive GmbH |
| 0x005A | VIMERCATI S.p.A. |
| 0x005B | VOLVO Group Trucks |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic GmbH & Co. KG |
| 0x0061 | Flextronics / Sidler Automotive GmbH & Co. KG |
| 0x0062 | EAO Automotive GmbH & Co. KG |
| 0x0063 | helag-electronic gmbh |
| 0x0064 | Magna Electronics |
| 0x0065 | INTEVA Products, LLC (formerly Arvinmeritor 2011-03-29) |
| 0x0066 | Valeo SA |
| 0x0067 | Defond Holding / BJAutomotive / DAC |
| 0x0068 | Industrie Saleri S. p. A. |
| 0x0069 | ROHM Semicon GmbH |
| 0x0070 | Alfmeier Präzision AG |
| 0x0071 | Sanden Corporation |
| 0x0072 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x0073 | ebm-papst St. Georgen GmbH & Co. KG |
| 0x0074 | CATEM |
| 0x0075 | OMRON Automotive Electronics Technology GmbH |
| 0x0076 | Johnson Electric International |
| 0x0077 | A123 Systems |
| 0x0078 | IPG Automotive GmbH, Karlsruhe |
| 0x0079 | Daesung Electric Co. Ltd. |
| 0x007A | Kromberg & Schubert GmbH & Co. KG |
| 0x007B | Bury GmbH & Co. KG |
| 0x007E | Measurement Specialties Inc (MEAS) |
| 0x007F | MRS Electronic GmbH |
| 0x0082 | Dale Electronics Inc |
| 0x0083 | Mirror Controls international |
| 0x0084 | Keboda Technology Co. Ltd. |
| 0x0085 | SPD Control Systems Corporation |
| 0x0087 | Röchling Automotive AG & Co. KG |
| 0x0088 | AEV s.r.o |
| 0x0089 | Kongsberg Automotive AB/Mullsjö Works |
| 0x008A | May & Scofield Ltd |
| 0x008C | C&S Technology Inc |
| 0x008D | RDC Semiconductor Co., Ltd |
| 0x008E | Webasto AG |
| 0x008F | Accel Elektronika UAB |
| 0x0090 | FICOSA International S.A. |
| 0x0091 | Mahle |
| 0x0093 | Phoenix International |
| 0x0094 | John Deere |
| 0x0095 | Grayhill Inc |
| 0x0096 | AppliedSensor GmbH |
| 0x0097 | UST Umweltsensortechnik GmbH |
| 0x0098 | Digades GmbH |
| 0x0099 | Thomson Linear Motion |
| 0x009A | TriMark Corporation |
| 0x009B | KB Auto Tech Co., Ltd. |
| 0x009C | Methode Electronics, Inc |
| 0x009D | Danlaw, Inc. |
| 0x009E | Federal-Mogul Corporation |
| 0x009F | Fujikoki Corporation |
| 0x00A0 | MENTOR Gmbh & Co. Praezisions-Bauteile KG |
| 0x00A1 | Toyota Industries Corporation |
| 0x00A2 | Strattec Security Corp. |
| 0x00A3 | TE Connectivity |
| 0x00A4 | Westfalia Automotive GmbH |
| 0x00A5 | Woco Industrietechnik GmbH |
| 0x00A6 | Minebea Co., Ltd |
| 0x00A7 | Magna |
| 0x00A8 | Dong IL Technology |
| 0x00A9 | Wilo SE |
| 0x00AA | Remy International, Inc. |
| 0x00AB | ACCUmotive |
| 0x00AC | Carling Technologies |
| 0x00B0 | Hanon Systems Korea |
| 0x00B1 | Eberspächer Controls Esslingen GmbH & Co. KG |
| 0x00B2 | WABCO Development GmbH |
| 0x00B3 | Sensirion AG |
| 0x00B4 | OSHINO Electronics Estonia OÜ |
| 0x00B5 | Fishman Thermo Technologies  LTD |
| 0x00B6 | Novalog Ltd |
| 0x00B7 | Hanon Systems USA |
| 0x00B8 | Leggett & Platt Automotive Group |
| 0x00B9 | Tremec |
| 0x00BA | Check Corporation |
| 0x00BB | Federal-Mogul Corporation |
| 0x00BC | fischer automotive systems |
| 0x00BD | Hi-Lex Europe GmbH |
| 0x00BE | SGX Sensortech |
| 0x00BF | AGM Automotive |
| 0x00C0 | Melecs |
| 0x00C1 | Robertshaw Controls Company |
| 0x0100 | Isabellenhuette Heusler GmbH & Co. KG |
| 0x0101 | Huber Automotive AG |
| 0x0102 | Precision Motors Deutsche Minebea GmbH |
| 0x0103 | TK Holdings Inc., Electronics |
| 0x0104 | Cobra Automotive Technologies S.P.A. |
| 0x0105 | Embed Limited |
| 0x0106 | Kissling Elektrotechnik GmbH |
| 0x0107 | Autoliv B.V. & Co. KG |
| 0x0108 | PST Electronics |
| 0x0109 | BCA Leisure Ltd |
| 0x010A | APAG Elektronik AG |
| 0x010B | RAFI GmbH & Co. KG |
| 0x010C | Sonceboz AutomotiveSA |
| 0x010D | i2s Intelligente Sensorsysteme Dresden GmbH |
| 0x010E | AGM Automotive, Inc. |
| 0x010F | S&T Motiv |
| 0x0111 | UG Systems GmbH & Co. KG |
| 0x0113 | CHANGJIANG AUTOMOBILE ELECTRONIC SYSTEM CO.,LTD |
| 0x0114 | MES S.A. |
| 0x0115 | SL Corporation |
| 0x0116 | Dura Automotive Systems |
| 0x0118 | Delta Electronics, Inc. |
| 0x0119 | Penny and Giles Controls Ltd |
| 0x011A | Curtiss Wright Controls Industrial |
| 0x011B | HKR Seuffer Automotive GmbH & Co. KG |
| 0x011C | DMK U.S.A. Inc |
| 0x0120 | Littelfuse |
| 0x0121 | Hyundai MOBIS |
| 0x0122 | Alpine Electronics of America |
| 0x0123 | Ford Motor Company |
| 0x0124 | Hangzhou Sanhua Research Inst. Co, Ltd. |
| 0x0125 | Delvis |
| 0x0126 | Louko |
| 0x0127 | Etratech |
| 0x0128 | HiRain |
| 0x0129 | elobau GmbH & Co. KG |
| 0x012A | I.G.Bauerhin GmbH |
| 0x012B | HANS WIDMAIER  |
| 0x012C | Gentherm Inc |
| 0x012D | LINAK A/S |
| 0x012E | Casco Products Corporation |
| 0x012F | Bühler Motor GmbH |
| 0x0130 | SphereDesign GmbH |
| 0x0131 | Cooper Standard |
| 0x0132 | KÜSTER Automotive Control Systems GmbH |
| 0x0133 | SEWS-Components Europe B.V. |
| 0x0134 | OLHO tronic GmbH |
| 0x0135 | LG Electronics |
| 0x0136 | Eberspächer Controls GmbH & Co. KG |
| 0x0137 | AISIN Seiki Co., Ltd. |
| 0x0138 | Elektrosil Systeme der Elektronik GmbH |
| 0x0139 | Nidec Corporation |
| 0x013A | ISSI – Integrated Silicon Solution Inc |
| 0x013B | Twin Disc, Incorporated |
| 0x013C | SPAL Automotive Srl |
| 0x013D | OTTO Engineering, Inc. |
| 0xFFFF | unbekannter Hersteller |

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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 12 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x05 | Bsi | Service Inclusive |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0D | NOx_a | NOx-Additiv |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |

<a id="table-arg-0x4114-d"></a>
### ARG_0X4114_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| E_A_TMEL | V | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | Engine Temperatur |

<a id="table-arg-0x4115-d"></a>
### ARG_0X4115_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BATTERY_VOLTAGE_RAW | V | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | Batterie Voltage Raw |

<a id="table-arg-0x4116-d"></a>
### ARG_0X4116_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_U_PWG1 | - | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | 5 V Supply 1 |

<a id="table-arg-0x4117-d"></a>
### ARG_0X4117_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_U_PWG2 | V | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | 5 V Supply 2 |

<a id="table-arg-0x4119-d"></a>
### ARG_0X4119_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VOLTAGE_FUN_2 | V | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | Voltage Fun 2 |

<a id="table-arg-0x411a-d"></a>
### ARG_0X411A_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ECU_MICRO_TEMPERATUR | °C | high | signed int | - | - | 2.03 | 1.0 | 596.0 | -293.0 | 327.0 | Ecu Micro Temperatur |

<a id="table-arg-0x411b-d"></a>
### ARG_0X411B_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| E_A_TMEL_2 | V | high | signed int | - | - | 128.0 | 1.0 | 0.0 | - | - | Motortemperatur 2 |

<a id="table-arg-0x4140-d"></a>
### ARG_0X4140_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_S_ELRLY | 0/1 | high | signed int | - | - | - | - | - | - | - | Status Electric Fun Relais |

<a id="table-arg-0x4141-d"></a>
### ARG_0X4141_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_T_ELUE | % | high | unsigned int | - | - | 65535.0 | 100.0 | 0.0 | - | - | Status Electric Fan Module |

<a id="table-arg-0x4142-d"></a>
### ARG_0X4142_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_T_EWP | % | high | unsigned int | - | - | 65535.0 | 100.0 | 0.0 | - | - | Water Pump |

<a id="table-arg-0x4143-d"></a>
### ARG_0X4143_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_S_KV1 | 0/1 | high | unsigned int | - | - | - | - | - | - | - | Kältemittelabsperrventilansteuerungsjobparameterbeschreibung |

<a id="table-arg-0x4144-d"></a>
### ARG_0X4144_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_S_KV2 | 0/1 | high | unsigned int | - | - | - | - | - | - | - | Expansion Valve 2 |

<a id="table-arg-0x4145-d"></a>
### ARG_0X4145_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A_S_MEL | 0/1 | high | unsigned int | - | - | - | - | - | - | - | Fan Relais 2 |

<a id="table-arg-0x60c3-d"></a>
### ARG_0X60C3_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SW_TV_GLF | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Komponentenansteuerung: Gesteuerte Luftfuehrung Klappe 1 |

<a id="table-arg-0x63f0-d"></a>
### ARG_0X63F0_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DIAG_AEP_GRUND_LADEENDE | 0-n | high | unsigned char | - | TAB_AEP_DIAG_GRUND_LADEENDE | - | - | - | - | - | Auswahl des Grundes für Ladeende |

<a id="table-arg-0xadc2-r"></a>
### ARG_0XADC2_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUESOLL_WERT | + | - | - | high | unsigned char | - | - | 1.0 | 0.3906 | 0.0 | 0.0 | 99.6094 | Vorgabe der Lüfterdrehzahl (0 - 99.6 %) |

<a id="table-arg-0xadc6-r"></a>
### ARG_0XADC6_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUEZLSOLL_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 0.3906 | 0.0 | 0.0 | 99.6094 | Ansteuerung Zusatzlüfter (0 - 99.6094%) |

<a id="table-arg-0xadc7-r"></a>
### ARG_0XADC7_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELUERELSOLL_NR | + | - | 0-n | high | unsigned char | - | TAB_ANSTEUERUNG_LUEFTER_RELAIS | - | - | - | - | - | Auswahl Ansteuerung Relais E-Lüfter |

<a id="table-arg-0xadc8-r"></a>
### ARG_0XADC8_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELUERELZLSOLL_NR | + | - | 0-n | high | unsigned char | - | TAB_ANSTEUERUNG_LUEFTER_RELAIS | - | - | - | - | - | Auswahl Ansteuerung Relais Zusatzlüfter |

<a id="table-arg-0xadf3-r"></a>
### ARG_0XADF3_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DREHZAHL_WERT | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | geforderte Drehzahl (0-100%) nur möglich, falls Temperatur des Jobs job STATUS_TEMP_EMASCHINE zwischen 15 und 45 °C |
| ZEIT_ANSTEUERUNG_WERT | + | - | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 500.0 | geforderte Ansteuerzeit (0-500s) |

<a id="table-arg-0xde23-d"></a>
### ARG_0XDE23_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OEFFNEN_SCHLIESSEN | 0-n | high | unsigned char | - | TAB_KAELTEMITTEL_ABSPERRVENTIL_OEFFNEN_SCHLIESSEN | - | - | - | - | - | Vorgabe: 0 - Job inaktiv; 1  - Job aktiv & Ventil öffnen; 2 - Job aktiv & Ventil schliessen |

<a id="table-arg-0xdee3-d"></a>
### ARG_0XDEE3_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ausführen des Rücksetzens der Statistikzähler: 0 = kein Rücksetzen; 1 = Rücksetzen |

<a id="table-arg-0xdefc-d"></a>
### ARG_0XDEFC_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DUMMY | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | wegen Kompatibilität zu ToolSet32 |

<a id="table-arg-0xdf4e-d"></a>
### ARG_0XDF4E_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00 = CBS-Daten werden nicht gelsöcht 0x01 = CBS-Daten werden gelöscht |

<a id="table-arg-0xf000-r"></a>
### ARG_0XF000_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DIAG_AEP_BATTERYGUARD | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0: keine Anforderung 1: Anforderung Battery Guard Call |

<a id="table-arg-0xf086-r"></a>
### ARG_0XF086_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSART_EM1 | + | - | 0-n | high | unsigned char | - | BETRIEBSART_EM | - | - | - | - | - | E-Maschine 1 Betriebsart vorgeben |

<a id="table-arg-0xf087-r"></a>
### ARG_0XF087_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BETRIEBSART_EM2 | + | - | 0-n | high | unsigned char | - | BETRIEBSART_EM | - | - | - | - | - | E-Maschine 2 Betriebsart vorgeben |

<a id="table-betriebsart-em"></a>
### BETRIEBSART_EM

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0 | Standby |
| 0x3 | DC-Spannungsregelung |
| 0x5 | Drehzahlregelung mit Momentenvorsteuerung |
| 0x6 | IHVBCTL - mit Momentenvorsteuerung |
| 0xA | Freilauf |
| 0xFF | unbekannt |

<a id="table-bf-akks-error"></a>
### BF_AKKS_ERROR

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AKKS_ERROR | 0/1 | high | unsigned char | 0x01 | - | - | - | - | indicates if an error is present |
| STAT_AKKS_DIAG_DONE_NO_MESS | 0/1 | high | unsigned char | 0x02 | - | - | - | - | indicates the no message diagnostic required time is over |
| STAT_AKKS_DIAG_DONE_LOW_FLAP | 0/1 | high | unsigned char | 0x04 | - | - | - | - | indicates the low flap diagnostic required time is over |

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

Dimensions: 336 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021200 | Energiesparmode aktiv | 0 | - |
| 0x02FF12 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur fuer Testzwecke | 0 | - |
| 0x1F2601 | DME Kodierung: fehlt | 0 | - |
| 0x1F2604 | DME Kodierung: Fahrgestellnummer fehlt oder falsch | 0 | - |
| 0x1F2701 | DME Kodierung: Schreibfehler | 0 | - |
| 0x1F2702 | DME Kodierung: Signaturpruefung fehlerhaft | 0 | - |
| 0x1F2704 | DME Kodierung: Daten unplausibel | 0 | - |
| 0x21E700 | Powermanagement: Niedervoltbatterie defekt waehrend Transport | 0 | - |
| 0x21E701 | Powermanagement: Niedervoltbatterie entladen wahrend Transport | 0 | - |
| 0x21E702 | Powermanagement: Niedervoltbatterie Bordnetzinstabilitaet | 0 | - |
| 0x21E704 | Powermanagement: Niedervoltbatterie wird nicht geladen; interne Fehlererkennung | 0 | - |
| 0x21E705 | Zyklisches Nachladen konnte nicht erfolgreich durchgefuehrt werden. | 0 | - |
| 0x21E706 | Powermanagement: Ruhestromverletzung | 0 | - |
| 0x21E707 | Powermanagement: Niedervoltbatterie tiefentlanden | 0 | - |
| 0x21E708 | Powermanagement: Niedervolt Bordnetz Ueberspannung | 0 | - |
| 0x21E709 | Powermanagement: Niedervolt Bordnetz Unterspannung | 0 | - |
| 0x21E70A | Powermanagement: Elektrische Verbraucher eingeschraenkt | 0 | - |
| 0x21E70C | Bremspedal: Plausibilitaetsfehler | 0 | - |
| 0x21E70D | Powermanagement Batteriezustandserkennung: Batteriedefekt | 0 | - |
| 0x21E70E | Powermanagement Batteriezustandserkennung: Tiefentladung | 0 | - |
| 0x21E70F | Kritische Uebertemperatur der Batterie (Low) | 0 | - |
| 0x21E710 | Kritische Uebertemperatur der Batterie (High). | 0 | - |
| 0x21E711 | Ersatzreaktion 3 der EM2 | 0 | - |
| 0x21E712 | Anforderung von AE: Kraftstoffreserveanzeige deaktivieren | 0 | - |
| 0x21E713 | Anforderung von AE: 0-Stromregelung aktivieren | 0 | - |
| 0x21E714 | Anforderung von AE: Deaktivierung von MSA ohne Einschaltaufforderer und CCM | 0 | - |
| 0x21E715 | Anforderung von AE: Deaktivierung von MSA ohne Einschaltaufforderer und mit CCM | 0 | - |
| 0x21E716 | Anforderung von AE: MSA-Einschaltauforderer | 0 | - |
| 0x21E717 | Anforderung von AE: Deaktivierung von MSA mit Einschaltaufforderer aber ohne CCM | 0 | - |
| 0x21E718 | Anforderung von AE: Deaktivierung von MSA mit Einschaltaufforderer und CCM | 0 | - |
| 0x21E719 | Anforderung von AE: MSA VM Einschaltverhinderer | 0 | - |
| 0x21E71A | Anforderung von AE: Deaktivierung LLR ueber EM | 0 | - |
| 0x21E71B | Ereignisfehlerspeicher auf Grund einer Anforderung der AE: Kraftschluss Getriebe 2 oeffnen | 0 | - |
| 0x21E71C | Ereignisfehlerspeicher auf Grund einer Anforderung der AE: Kraftschluss Getriebe 2 oeffnen auf Grund zu hoher elektrischer Geschwindigkeit | 0 | - |
| 0x21E71D | Ereignisfehlerspeicher auf Grund einer Anforderung der AE: Kraftschluss Getriebe 2 geschlossen halten | 0 | - |
| 0x21E71E | Diagnostizierter Steuergeraeteausfall der AE vom Notlaufmanager | 0 | - |
| 0x21E71F | Ausfall des Verbrennungsmotors auf Grund eines internen Fehlers | 0 | - |
| 0x21E720 | Diagnostizierter Steuergeraeteausfall des EGS vom Notlaufmanager | 0 | - |
| 0x21E721 | F_M_BMW_LHM_GBX1LIM1_FAULTTYPE | 0 | - |
| 0x21E722 | F_M_BMW_LHM_GBX1LIM2_FAULTTYPE | 0 | - |
| 0x21E723 | F_M_BMW_LHM_GBX1LIM3_FAULTTYPE | 0 | - |
| 0x21E724 | Diagnostizierter Steuergeraeteausfall der rDME vom Notlaufmanager | 0 | - |
| 0x21E725 | Elektroluefter Eigendiagnose Stufe 1: Kommunikationsfehler | 0 | - |
| 0x21E726 | Elektroluefter Eigendiagnose Stufe 2: Drehzahlreduzierung | 0 | - |
| 0x21E727 | Elektroluefter Eigendiagnose Stufe 3: Eingeschraenkter Lauf | 0 | - |
| 0x21E728 | Elektroluefter Eigendiagnose Stufe 4: Stillstand | 0 | - |
| 0x21E729 | Elektroluefter Eigendiagnose Stufe 5: Stillstand 2 | 0 | - |
| 0x21E72A | Elektroluefter Eigendiagnose Stufe 6: Stillstand 3 | 0 | - |
| 0x21E72B | Elektroluefter: Typ nicht plausibel | 0 | - |
| 0x21E72C | Kritische Uebertemperatur der Batterie (High). | 0 | - |
| 0x21E72D | Kritische Uebertemperatur der Batterie (Low) | 0 | - |
| 0x21E731 | Diagnose Gateway: Kommunikationsfehler | 0 | - |
| 0x21E740 | Kuehlmittelpumpe: Temperaturschwelle 1 ueberschritten | 0 | - |
| 0x21E741 | Kuehlmittelpumpe: Temperaturschwelle 2 ueberschritten | 0 | - |
| 0x21E743 | Kuehlmittelpumpe: Drehzahl ausserhalb Gueltigkeitsbereich | 0 | - |
| 0x21E744 | Kuehlmittelpumpe: Trockenlauf | 0 | - |
| 0x21E745 | Kuehlmittelpumpe: Ueberspannung | 0 | - |
| 0x21E746 | Kuehlmittelpumpe: Ueberstrom | 0 | - |
| 0x21E747 | Kuehlmittelpumpe: Uebertemperatur | 0 | - |
| 0x21E748 | Kuehlmittelpumpe: Unterspannung | 0 | - |
| 0x21E749 | Gaspedal und Bremspedalstellung: Plausibilitaetsfehler | 0 | - |
| 0x21E757 | Elektroluefter Check-Control-Meldung (ID 568): Motorluefter Defekt Fahrzeug sofort abstellen | 0 | - |
| 0x21E770 | condition based services | 0 | - |
| 0x21E771 | condition based services | 0 | - |
| 0x21E792 | Kuehlerjalousie LIN Kommunikation: Kommunikationsfehler gemeldet | 0 | - |
| 0x21E793 | Kuehlerjalousie LIN Kommunikation: Botschaftsausfall | 0 | - |
| 0x21E794 | Kuehlerjalousie oben Steller intern: elektrischer Fehler | 0 | - |
| 0x21E795 | Kuehlerjalousie oben unterer Anschlag: wird nicht erkannt | 0 | - |
| 0x21E796 | Kuehlerjalousie oben oberer Anschlag: wird nicht erkannt | 0 | - |
| 0x21E797 | Kuehlerjalousie oben oberer Anschlag: zu frueh erkannt | 0 | - |
| 0x21E798 | Kuehlerjalousie LIN Kommunikation: Signal fehlerhaft | 0 | - |
| 0x21E799 | Kuehlerjalousie oben Uebertemperatur Steller: Grenzwert ueberschritten | 0 | - |
| 0x21E79A | Kuehlerjalousie oben Versorgungsspannung Steller: Spannungsfehler | 0 | - |
| 0x21E800 | E-Antrieb Kuehlsystem: Abschaltung el. Kuehlmittelpumpe wegen Blockierung | 0 | - |
| 0x21E801 | E-Antrieb Kuehlsystem leistungsreduzierter Betrieb: Kuehlmittelverlust durch el. Kuehlmittelpumpe erkannt | 0 | - |
| 0x21E802 | E-Antrieb Kuehlsystem: Keine Kommunikation mit el. Kuehlmittelpumpe | 0 | - |
| 0x21E803 | E-Antrieb Kuehlsystem: Abschaltung el. Kuehlmittelpumpe wegen Uebertemperatur | 0 | - |
| 0x21E804 | E-Antrieb Kuehlsystem: Betrieb el. Kuehlmittelpumpe gestoert | 0 | - |
| 0x21E900 | Elektroluefter Relais Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x21E901 | Elektroluefter Relais Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x21E902 | Elektroluefter Relais Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x21E903 | Elektroantrieb Kuehlsystem: Ansteuerungsleitung elektrischer Kuehlmittelpumpe unterbrochen | 0 | - |
| 0x21E904 | Elektroantrieb Kuehlsystem: Ansteuerungsleitung elektrischer Kuehlmittelpumpe Kurzschluss nach Masse | 0 | - |
| 0x21E905 | Elektroantrieb Kuehlsystem: Ansteuerungsleitung elektrischer Kuehlmittelpumpe Kurzschluss nach Plus | 0 | - |
| 0x21E906 | Elektroluefter Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x21E907 | Elektroluefter Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x21E908 | Elektroluefter Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x21E909 | Steuergeraet: interner Fehler Analog Digital Wandler | 0 | - |
| 0x21E90B | Ueberspannung erkannt | 0 | - |
| 0x21E90C | Unterspannung erkannt | 0 | - |
| 0x21E90D | Ebene 3 Ueberwachung: Watchdog Falsche Anfrage | 0 | - |
| 0x21E916 | Fahrpedalmodul : ESM Plausibilitaets Fehler | 0 | - |
| 0x21E917 | Ebene 3 Ueberwachung: Programm Ablauf Fehler | 0 | - |
| 0x21E918 | Elektronische Wegfahrsperre : Flexray-Bus Response Framefehler | 0 | - |
| 0x21E919 | Elektronische Wegfahrsperre : Flexray-Bus Response Timeoutfehler | 0 | - |
| 0x21E91B | Ebene 2 Ueberwachung: Fehler Sicherheitskonzept | 0 | - |
| 0x21E91C | Ebene2-Ueberwachung: Fehler Istmoment der AE | 0 | - |
| 0x21E91D | Elektronische Wegfahrsperre : Fehler Datenablage Plausibilitatsfehler | 0 | - |
| 0x21E91E | Elektronische Wegfahrsperre : CAN-Bus Response Timeoutfehler | 0 | - |
| 0x21E91F | Elektronische Wegfahrsperre : CAN Bus Response Framefehler | 0 | - |
| 0x21E920 | Elektronische Wegfahrsperre : Kein Secret Key programmiert | 0 | - |
| 0x21E921 | Elektronische Wegfahrsperre : Nicht authentische Response empfangen | 0 | - |
| 0x21E922 | Elektronische Wegfahrsperre : CAN Bus Challenge oder Keyfaktor Framefehler | 0 | - |
| 0x21E923 | Elektronische Wegfahrsperre : Secret Key Write Error | 0 | - |
| 0x21E925 | Fahrpedalmodul: Pedalwertgeber Sensor 2 unter Schwellwert | 0 | - |
| 0x21E926 | Fahrpedalmodul: Pedalwertgeber Sensor 2 ueber Schwellwert | 0 | - |
| 0x21E927 | Fahrpedalmodul: Pedalwertgeber Sensor 1 unter Schwellwert | 0 | - |
| 0x21E928 | Fahrpedalmodul: Pedalwertgeber Sensor 1 ueber Schwellwert | 0 | - |
| 0x21E929 | Montagemodus aktiv | 0 | - |
| 0x21E92A | Steuergeraet: interner Fehler Daten inkonsistent | 0 | - |
| 0x21E92B | Steuergeraet: interner Fehler EEPROM Zugriff nicht moeglich | 0 | - |
| 0x21E92C | Fahrpedalmodul: Pedalwertgeber Sensor 1 Korrelationsfehler | 0 | - |
| 0x21E92D | Fahrpedalmodul: Pedalwertgeber Sensor 2 Korrelationsfehler | 0 | - |
| 0x21E92E | Gaspedal und Bremspedalstellung: Kompatibilitaetsfehler Notlauf | 0 | - |
| 0x21E92F | Gaspedal und Bremspedalstellung: Kompatibilitaetsfehler Leistungseinschraenkung | 0 | - |
| 0x21E930 | Fahrpedalmodul: Pedal klemmt | 0 | - |
| 0x21E932 | Fahrpedalmodul: Pedalwertgeber Sensor 1 Kurzschluss nach Plus | 0 | - |
| 0x21E933 | Fahrpedalmodul: Pedalwertgeber Sensor 1 Kurzschluss nach Masse | 0 | - |
| 0x21E935 | Fahrpedalmodul: Pedalwertgeber Sensor 2 Kurzschluss nach Plus | 0 | - |
| 0x21E936 | Fahrpedalmodul: Pedalwertgeber Sensor 2 Kurzschluss nach Masse | 0 | - |
| 0x21E93A | Ebene 3: Fehler Monitor Sequenz | 0 | - |
| 0x21E93B | Steuergeraet interner Fehler: Spannungsregler 1 Spannung ausserhalb gueltigem Bereich | 0 | - |
| 0x21E93C | Steuergeraet interner Fehler: Spannungsregler 1 Uebertemperatur Abschaltung | 0 | - |
| 0x21E93D | Steuergeraet interner Fehler: Spannungsregler 2 Spannung ausserhalb gueltigem Bereich | 0 | - |
| 0x21E93E | Steuergeraet interner Fehler: Spannungsregler 2 Uebertemperatur Abschaltung | 0 | - |
| 0x21E93F | Ebene 2 Ueberwachung: Ueberwachung Sollmomente | 0 | - |
| 0x21E940 | Ebene 2 Ueberwachung: Ueberwachung Stillstand | 0 | - |
| 0x21E942 | Ebene 2 Ueberwachung: Ueberwachung Beschleunigung | 0 | - |
| 0x21E947 | Systemzeit ungueltig | 0 | - |
| 0x21E94B | Temperatursensor 1: Kurzschluss nach Plus | 0 | - |
| 0x21E94C | Temperatursensor 1: Kurzschluss nach Masse | 0 | - |
| 0x21E94D | Temperatursensor 1: zu schnelle Temperaturaenderung | 0 | - |
| 0x21E950 | Zusatzluefter Motorraum Relais Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x21E951 | Zusatzluefter Motorraum Relais Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x21E952 | Zusatzluefter Motorraum Relais Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x21E953 | Absperrbares Expansionsventil: Leitungsunterbrechung | 0 | - |
| 0x21E954 | Absperrbares Expansionsventil: Kurzschluss nach Masse | 0 | - |
| 0x21E955 | Absperrbares Expansionsventil: Kurzschluss nach Plus | 0 | - |
| 0x21E956 | Absperrventil: Leitungsunterbrechung | 0 | - |
| 0x21E957 | Absperrventil: Kurzschluss nach Masse | 0 | - |
| 0x21E958 | Absperrventil: Kurzschluss nach Plus | 0 | - |
| 0x21E959 | Ebene 2 Ueberwachung: Fahreranwesenheit Fehler Herstellung Fahrbereitschaft | 0 | - |
| 0x21E95A | Ebene 2 Ueberwachung: Fehler Raddurchmesser | 0 | - |
| 0x21E95C | Ebene 3 Ueberwachung: Kommunikationsfehler | 0 | - |
| 0x21E95D | Ebene 2 Ueberwachung: Monitor Fehler | 0 | - |
| 0x21E95E | Ebene 3 Ueberwachung: Monitor Fehler | 0 | - |
| 0x21E95F | Ebene 3 Ueberwachung: Reset fehlerhaft | 0 | - |
| 0x21E960 | Ebene 3 Ueberwachung: falsch programmiert oder falsche Pruefsumme bei Aufstart | 0 | - |
| 0x21E961 | Ebene 3 Ueberwachung: Fehler Pedal Test | 0 | - |
| 0x21E962 | Ebene 3 Ueberwachung: Abschaltung | 0 | - |
| 0x21E963 | Ebene 3 Ueberwachung: interner Fehler | 0 | - |
| 0x21E964 | Ebene 3 Ueberwachung: ROM Pruefsumme | 0 | - |
| 0x21E965 | Ebene 3 Ueberwachung: Programmspeicher Fehler | 0 | - |
| 0x21E966 | Ebene 3 Ueberwachung: Datenspeicher Fehler | 0 | - |
| 0x21E967 | Ebene 3 Ueberwachung: Arbeitsspeicher (RAM) Fehler | 0 | - |
| 0x21E968 | Ebene 3 Ueberwachung: Zeit fehlerhaft | 0 | - |
| 0x21E969 | Pedal: Externer Spannungsregler: konstante Spannung | 0 | - |
| 0x21E96A | Pedal: ESM Spannungsfehler | 0 | - |
| 0x21E96B | ECC Fehler | 0 | - |
| 0x21E96C | ESM L2 RAM Checksum Fehler | 0 | - |
| 0x21E96D | Momentenreduzierung Verbrennungsmotor bei Ueberhitzung Motorraum | 0 | - |
| 0x21E96E | Abschalten Verbrennungsmotor bei Ueberhitzung Motorraum | 0 | - |
| 0x21E96F | Fahrbereitschaft nach Fahreranforderung nicht herstellbar | 0 | - |
| 0x21E970 | Kupplung Plausibilitaet: Uebertragbares Moment zu niedrig Kupplung leicht geschaedigt | 0 | - |
| 0x21E971 | Kupplung Plausibilitaet: Uebertragbares Moment zu niedrig Kupplung geschaedigt | 0 | - |
| 0x21E972 | Kupplung Plausibilitaet: Uebertragbares Moment zu niedrig Kupplung leicht geschaedigt | 0 | - |
| 0x21E973 | Temperatursensor 2: Kurzschluss nach Plus | 0 | - |
| 0x21E974 | Temperatursensor 2: Kurzschluss nach Masse | 0 | - |
| 0x21E975 | Temperatursensor 2: zu schnelle Temperaturaenderung | 0 | - |
| 0x21E976 | Temperatursensor 2: Temperatur zu hoch | 0 | - |
| 0x21E977 | Temperatursensor 2: Temperatur zu niedrig | 0 | - |
| 0x21E978 | Temperatursensor 1: Temperatur zu hoch | 0 | - |
| 0x21E979 | Temperatursensor 1: Temperatur zu niedrig | 0 | - |
| 0x21E980 | Temperatursensor 1: Kurzschluss nach Plus | 0 | - |
| 0x21E981 | Temperatursensor 1: Kurzschluss nach Masse | 0 | - |
| 0x21E982 | Temperatursensor 1: Temperatur zu hoch | 0 | - |
| 0x21E983 | Temperatursensor 1: Temperatur zu niedrig | 0 | - |
| 0x21E984 | Temperatursensor 1: zu schnelle Temperaturaenderung | 0 | - |
| 0x21E985 | Absperrbares Expansionsventil: Leitungsunterbrechung | 0 | - |
| 0x21E986 | Absperrbares Expansionsventil: Kurzschluss nach Masse | 0 | - |
| 0x21E987 | Absperrbares Expansionsventil: Kurzschluss nach Plus | 0 | - |
| 0x21E988 | Absperrbares Expansionsventil: Leitungsunterbrechung | 0 | - |
| 0x21E989 | Absperrbares Expansionsventil: Kurzschluss nach Masse | 0 | - |
| 0x21E98A | Absperrbares Expansionsventil: Kurzschluss nach Plus | 0 | - |
| 0x224100 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Bauteilschutz - Degradierung wegen Uebertemperatur | 0 | - |
| 0x224101 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Bauteilschutz - Abschaltung wegen Uebertemperatur | 0 | - |
| 0x224102 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Bauteilschutz - Degradierung wegen Ueberstrom | 0 | - |
| 0x224103 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Bauteilschutz - Abschaltung wegen Ueberstrom | 0 | - |
| 0x224104 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Bauteilschutz - Abschaltung wegen Blockierung | 0 | - |
| 0x224105 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Spannungsversorgung - Ueber-/oder Unterspannung | 0 | - |
| 0x224106 | EWP22 Kuehlmittelpumpe-Hochvoltspeicher - Interner elektrischer Fehler | 0 | - |
| 0x224107 | EWP22 Kuehlsystem-Hochvoltspeicher - Bauteilschutz - Erkennung Kuehlmittelverlust | 0 | - |
| 0x22410A | EWP23 Kuehlmittelpumpe-Leistungselektronik - Bauteilschutz - Degradierung wegen Uebertemperatur | 0 | - |
| 0x22410B | EWP23 Kuehlmittelpumpe-Leistungselektronik - Bauteilschutz - Abschaltung wegen Uebertemperatur | 0 | - |
| 0x22410C | EWP23 Kuehlmittelpumpe-Leistungselektronik - Bauteilschutz - Degradierung wegen Ueberstrom | 0 | - |
| 0x22410D | EWP23 Kuehlmittelpumpe-Leistungselektronik - Bauteilschutz - Abschaltung wegen Ueberstrom | 0 | - |
| 0x22410E | EWP23 Kuehlmittelpumpe-Leistungselektronik - Bauteilschutz - Abschaltung wegen Blockierung | 0 | - |
| 0x22410F | EWP23 Kuehlmittelpumpe-Leistungselektronik - Spannungsversorgung - Ueber-/oder Unterspannung | 0 | - |
| 0x224110 | EWP23 Kuehlmittelpumpe-Leistungselektronik - Interner elektrischer Fehler | 0 | - |
| 0x224111 | EWP23 Kuehlsystem-Leistungselektronik - Bauteilschutz - Erkennung Kuehlmittelverlust | 0 | - |
| 0x3A0000 | Elektrische Wasserpumpe EWP23 LIN Kommunikation: Botschaftsausfall | 0 | - |
| 0x3A0001 | Elektrische Wasserpumpe EWP22 LIN Kommunikation: Botschaftsausfall | 0 | - |
| 0xCD840A | FA_CAN : CAN Baustein Abschaltung | 0 | - |
| 0xCD841F | A_FXR : FlexRay Baustein Abschaltung | 0 | - |
| 0xCD8486 | A_CAN : CAN Baustein Abschaltung | 0 | - |
| 0xCD8BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur fuer Testzwecke | 0 | - |
| 0xCD8C00 | LIN Bus: Kommunikationsfehler | 0 | - |
| 0xCD8C01 | Intelligenter Batteriesensor LIN Kommunikation: Zeitueberschreitung | 0 | - |
| 0xCD8C04 | Intelligenter Batteriesensor Signal: Bus-Fehler | 0 | - |
| 0xCD8C05 | Intelligenter Batteriesensor Funktion: Stromfehler | 0 | - |
| 0xCD8C06 | Intelligenter Batteriesensor Kompatibilitaet: Version nicht plausibel | 0 | - |
| 0xCD8C07 | Intelligenter Batteriesensor Eigendiagnose: Interner Fehler | 0 | - |
| 0xCD8C08 | Intelligenter Batteriesensor Funktion: Temperaturfehler | 0 | - |
| 0xCD8C09 | Intelligenter Batteriesensor Funktion: Spannungsfehler | 0 | - |
| 0xCD8C0A | Intelligenter Batteriesensor Wake-up-Leitung: Leitungsunterbrechung | 0 | - |
| 0xCD8C0B | Intelligenter Batteriesensor Wake-up-Leitung: Kurzschluss | 0 | - |
| 0xCD8C0D | Fehler Moment fuer Katheizen obere Schwelle | 0 | - |
| 0xCD8C0F | Kraftschluss der verbrennungsmotorischen Achse aufheben | 0 | - |
| 0xCD8C12 | Hybrid Anforderung Momentenbegrenzung Stufe1 | 0 | - |
| 0xCD8C13 | Hybrid Anforderung Momentenbegrenzung Stufe2 | 0 | - |
| 0xCD8C14 | Hybrid Anforderung Momentenbegrenzung Stufe3 | 0 | - |
| 0xCD8C15 | Zusatzluefter elektrisch: Fehlfunktion | 0 | - |
| 0xCD8C17 | Zusatzluefter Stufe 1: falscher Luefter verbaut | 0 | - |
| 0xCD8C18 | Zusatzluefter Stufe 2: blockiert / schwergaenig  | 0 | - |
| 0xCD8C19 | Zusatzluefter Stufe 3: Luefter nicht angelaufen | 0 | - |
| 0xCD8C1A | Zusatzluefter Stufe 4: Luefter schaltet nicht ab | 0 | - |
| 0xCD8C1B | Zusatzluefter Stufe 5 Plausibilitaet: Drehzahl zu niedrig | 0 | - |
| 0xCD8C1C | Zusatzluefter Stufe 6 Plausibilitaet: Plausibilisierung nicht erfolgt | 0 | - |
| 0xCD8C20 | Deaktivierung ZSE-Startsystem | 0 | - |
| 0xCD8C24 | Standby der EM1 in der Software der DME aktivieren | 0 | - |
| 0xCD8C25 | Deaktivierung EM1 als Startsystem | 0 | - |
| 0xCD8C29 | Standby der EM2 in der Software der DME aktivieren | 0 | - |
| 0xCD8C2A | Deaktivierung des Verbrennungsmotors aufgrund eines internen Fehlers | 0 | - |
| 0xCD8C2B | Deaktivierung eines Zylinders des Verbrennungsmotors aufgrund eines internen Fehlers | 0 | - |
| 0xCD8C2C | Anforderung eines Service Requests | 0 | - |
| 0xCD8C2D | Hohe Momentenbegrenzung des Verbrennungsmotors aufgrund eines internen Fehlers detektiert | 0 | - |
| 0xCD8C2E | Niedrige Momentenbegrenzung des Verbrennungsmotors aufgrund eines internen Fehlers detektiert | 0 | - |
| 0xCD8C2F | Ueberdrehzahl zwischen Verbrennungsmotor und Getriebe erkannt (Verbrennungsmotor an) | 0 | - |
| 0xCD8C30 | Ueberdrehzahl zwischen Verbrennungsmotor und Getriebe erkannt (Ueberschreitung kritische Geschwindigkeit) | 0 | - |
| 0xCD8C31 | Aufheben der Fahrbereitschaft | 0 | - |
| 0xCD8C35 | Startaggregat Ritzelstarter: Anzahl MSA-Reflexstarts ueberschritten | 0 | - |
| 0xCD8C36 | Startaggregat Ritzelstarter: Anzahl Motorstarts ueberschritten | 0 | - |
| 0xCD8C39 | Nullgangsensor Adaption: nicht gelernt (MSA deaktiviert) | 0 | - |
| 0xCD8C3A | Deaktivierung des Verbrennungsmotors aufgrund einer Ueberdrehzahl | 0 | - |
| 0xCD8C3B | Check-Control-Meldung: Drehzahl! Herunterschalten | 0 | - |
| 0xCD8C3C | Momentenreduzierung bei Ueberlastung Kuehlsystem | 0 | - |
| 0xCD8C40 | CC-Meldung AU-Test aktivieren nicht moeglich | 0 | - |
| 0xCD8C41 | CC-Meldung AU-Test aktiviert | 0 | - |
| 0xCD8C42 | Fehlerspeichereintrag ist deaktiviert | 0 | - |
| 0xCD8C43 | Fehlerspeichereintrag ist deaktiviert | 0 | - |
| 0xCD8C44 | Meldung im Kombi wurde ausgeloest da REX Zustart nicht moeglich ist | 0 | - |
| 0xCD8C49 | Ausloesung der CCM904. | 0 | - |
| 0xCD8C4D | Notlauf im Hybridsteuergeraet erfordert Drehzahlbegrenzung Stufe 1 vom Verbrennungsmotor. | 0 | - |
| 0xCD8C4E | Notlauf im Hybridsteuergeraet erfordert Drehzahlbegrenzung Stufe 2 vom Verbrennungsmotor. | 0 | - |
| 0xCD8C4F | Notlauf im Hybridsteuergeraet erfordert Drehzahlbegrenzung Stufe 3 vom Verbrennungsmotor. | 0 | - |
| 0xCD8C50 | Eine bedatbare Anzahl von Zylindern ist ausgefallen | 0 | - |
| 0xCD8C51 | Anforderung von der AE an die eDME die Leerlaufdrehzahl anzuheben | 0 | - |
| 0xCD8C52 | Freigabe des SGR-Starts durch die AE | 0 | - |
| 0xCD8C55 | Anforderung von AE: MSA VM Ausschaltaufforderer | 0 | - |
| 0xCD8C56 | Anforderung von AE: MSA-Abschaltverhinderer | 0 | - |
| 0xCD9400 | A_CAN Botschaft (Ladestatus 0x3E9): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9403 | A_CAN Botschaft (Ist Daten Komfort Ladeelektronik Langzeit 0x211): fehlt | 0 | - |
| 0xCD9405 | A_CAN Botschaft (Ist Daten E-Motor Traktion 0x100): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD940E | A_CAN Botschaft (Daten Antrieb Elektrisch 0x32F): fehlt | 0 | - |
| 0xCD940F | A_CAN Botschaft (Daten Hochvoltspeicher 0x431): fehlt | 0 | - |
| 0xCD9412 | FA_CAN Botschaft (Nachlaufzeit Stromversorgung BN2020 0x3BE): fehlt | 0 | - |
| 0xCD9416 | FA_CAN Botschaft (Kilometerstand/Reichweite 0x330): fehlt | 0 | - |
| 0xCD941C | A_CAN Botschaft (Modus Spannungsgesteuert 0x432): fehlt | 0 | - |
| 0xCD9421 | A_CAN Botschaft (Status DCDC 0x429): fehlt | 0 | - |
| 0xCD9424 | A_CAN Botschaft (Status Hochvoltspeicher 1 0x1FA): fehlt | 0 | - |
| 0xCD942A | A_CAN Botschaft (Status Hochvoltspeicher 2 0x112): fehlt | 0 | - |
| 0xCD942B | FA_CAN Botschaft (ZV und Klappenzustand 0x2FC): fehlt | 0 | - |
| 0xCD942F | FA_CAN Botschaft (Uhrzeit/Datum 0x2F8): fehlt | 0 | - |
| 0xCD9431 | FA_CAN Botschaft (Ist Daten Verbrennungsmotor Range Extender 0x0A9): fehlt | 0 | - |
| 0xCD9435 | FA_CAN Botschaft (Fahrzeugzustand 0x3A0): fehlt | 0 | - |
| 0xCD9437 | FA_CAN Botschaft (Relativzeit BN2020 0x328): fehlt | 0 | - |
| 0xCD9438 | FA_CAN Botschaft (Freigabe Kuehlung Hochvoltspeicher 0x37B): fehlt | 0 | - |
| 0xCD9439 | FA_CAN Botschaft (Anforderung Klimaanlage 0x2F9): fehlt | 0 | - |
| 0xCD943A | FA_CAN Botschaft (Anforderung Klima Hybrid 0x299): fehlt | 0 | - |
| 0xCD943F | FA_CAN Botschaft (Status Anzeige Kombi 0x1B3): fehlt | 0 | - |
| 0xCD9442 | A_CAN Botschaft (Status Betriebsart Hybrid 2 0x41C): fehlt | 0 | - |
| 0xCD9443 | A_FlexRay Botschaft (Klemmen 116.0.2): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9444 | FA_CAN Botschaft (Status Tuersensoren Abgesichert 0x1E1): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9445 | FA_CAN : Kommunikationsstoerung Botschaft (Status Sperre Fehlerspeicher) | 0 | - |
| 0xCD9446 | FA_CAN Botschaft (Klemmen 0x12F): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9447 | A_FlexRay Botschaft (Laengsbeschleunigung Schwerpunkt 55.0.2): fehlt | 0 | - |
| 0xCD944A | A_FlexRay Botschaft (Konfiguration Schalter Fahrdynamik 272.0.8): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD944B | A_FlexRay Botschaft (Ist Drehzahl Rad 46.0.1): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD944C | FA_CAN Botschaft (Ist Daten Langzeit Verbrennungsmotor Range Extender 0x2B0): fehlt | 0 | - |
| 0xCD944D | A_FlexRay Botschaft (Geschwindigkeit Fahrzeug / Geschwindigkeit Fahrzeug 2 55.0.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9450 | A_FlexRay Botschaft (Querbeschleunigung Schwerpunkt 55.0.2): fehlt | 0 | - |
| 0xCD9453 | A_FlexRay Botschaft (Anforderung 2 Radmoment Antriebstrang Summe FAS 131.0.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9454 | A_FlexRay Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation 47.0.2): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9455 | A_FlexRay Botschaft (Status Gurt Kontakt Sitzbelegung 275.0.8): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9456 | FA_CAN Botschaft (Aussentemperatur 0x2CA): fehlt | 0 | - |
| 0xCD9457 | A_CAN Botschaft (Ist Daten Kurzzeit E-Motor 1 0x0A8): fehlt | 0 | - |
| 0xCD9458 | A_CAN Botschaft (Abgesichert Ist Daten Kurzzeit E-Motor 1 0x0CD): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9459 | FA_CAN Botschaft (Zustand Fahrzeug 0x03C): fehlt | 0 | - |
| 0xCD945B | FA_CAN Botschaft (Daten Hybrid 0x2DB): fehlt | 0 | - |
| 0xCD945C | A_CAN Botschaft (Information E-Motor 1 0x29B): fehlt | 0 | - |
| 0xCD945D | FA_CAN Botschaft (Betriebsart Drehzahl Drehmoment Hybrid 0x331): fehlt | 0 | - |
| 0xCD945E | A_CAN Botschaft (Moeglichkeit Motorstart Motorstop 0x3EC): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD945F | A_CAN Botschaft (Anforderung Betriebsstrategie AE 0x0BB): fehlt | 0 | - |
| 0xCD9460 | A_FlexRay Botschaft (Anforderung Leistung Elektrisch EPS 234.0.2): fehlt | 0 | - |
| 0xCD9461 | A_CAN Botschaft (Vorgabe Drehmoment Betriebsstrategie 0x0AD): fehlt | 0 | - |
| 0xCD9462 | A_CAN Botschaft (Status Antrieb Hybrid 0x3A4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9463 | A_CAN Botschaft (Status Daten E-Motor 1 0x29D): fehlt | 0 | - |
| 0xCD9464 | A_CAN Botschaft (Status Information Verbrennungsmotor 0x2C0): fehlt | 0 | - |
| 0xCD9465 | A_CAN Botschaft (Status E-Motor Traktion 0x2B7): fehlt | 0 | - |
| 0xCD9466 | A_CAN Botschaft (Status E-Motor Traktion Langzeit 0x192): fehlt | 0 | - |
| 0xCD9467 | A_CAN Botschaft (Status Betriebsart E-Motor Traktion 0x2E8): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9468 | A_FlexRay Botschaft (Status Fahrzeugstillstand Parkbremse 263.0.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9469 | A_FlexRay Botschaft (Status Fahrzeugstillstand 263.0.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD946C | A_FlexRay Botschaft (Konfiguration Schalter Fahrdynamik 2 272.0.8): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9472 | A_CAN Botschaft (Daten Anzeige Getriebestrang 0x3FD): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9476 | A_CAN Botschaft (Ist Daten Ladeelektronik 0x108): fehlt | 0 | - |
| 0xCD9477 | A_FlexRay Botschaft (Qualifier Service ECBA 63.1.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9478 | FA_CAN Botschaft (Radmoment Elektrisch Fahren 2 0x0C3): fehlt | 0 | - |
| 0xCD9479 | A_FlexRay Botschaft (Ist Bremsmoment Summe / Status Parametrisierung I-Brake 43.3.4): fehlt | 0 | - |
| 0xCD947A | A_FlexRay Botschaft (Neigung Fahrbahn / Lenkwinkel Vorderachse Effektiv 56.0.2): fehlt | 0 | - |
| 0xCD947B | FA_CAN Botschaft (Ist Daten Ladeelektronik 0x108): fehlt | 0 | - |
| 0xCD947C | FA_CAN Botschaft (Tankinhalt/Reichweite 0x373): fehlt | 0 | - |
| 0xCD947D | FA_CAN Botschaft (Schlafbereitschaft Global FZM 0x3A5): fehlt | 0 | - |
| 0xCD947E | FA_CAN Botschaft (Steuerung Crash 0x19B): fehlt | 0 | - |
| 0xCD947F | FA_CAN Botschaft (Daten Anzeige Getriebestrang 0x3FD): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9483 | A_FlexRay Botschaft (Masse/Gewicht Fahrzeug 108.0.2): fehlt | 0 | - |
| 0xCD9484 | A_FlexRay Botschaft (Diagnose OBD Motor 247.1.2): fehlt | 0 | - |
| 0xCD9485 | A_FlexRay Botschaft (Status Stabilisierung DSC / Status Stabilisierung DSC 2 47.0.2): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9486 | A_FlexRay Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Laengsmoment Vorderachse Hinterachse 43.0.4): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD9487 | A_CAN Botschaft (Vorgabe Drehmoment Traktion Langzeit 0x13E): fehlt | 0 | - |
| 0xCD9488 | A_CAN Botschaft (Vorgabe Drehmoment Betriebsstrategie Traktion 0x13D): fehlt | 0 | - |
| 0xCD9489 | FA_CAN Botschaft (Daten Position Getriebestrang 0x212): fehlt oder Alive-Zaehler Pruefsumme falsch | 0 | - |
| 0xCD948A | FA_CAN Botschaft (Status Klima Luftverteilung FA 0x2E6): fehlt | 0 | - |
| 0xCD948B | FA_CAN Botschaft (Regensensor-Wischergeschwindigkeit 0x226): fehlt | 0 | - |
| 0xCD948C | A_FlexRay Botschaft (Bedienung Taster Elektrisches Fahrzeug 137.0.2): fehlt | 0 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 58 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1800 | Pedal Position | % | high | unsigned int | - | 1 | 128 | 0 |
| 0x1801 | Raw information signal from Pedal track 1 | cnt | high | signed int | - | 1 | 1 | 0 |
| 0x1802 | Absolutgeschwindigkeit des Fahrzeugschwerpunktes | km/h | high | unsigned int | - | 1 | 64 | 0 |
| 0x1809 | ENV_BMWL_ST_ERR_DCDC_CNV | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x180a | Aktuelle Motorlast | % | high | unsigned char | - | 100 | 255 | 0 |
| 0x180b | Temperatur Motor Antrieb | C | high | unsigned char | - | 1 | 1 | 48 |
| 0x180c | Ist Drehzahl Motor Kurbelwelle | RPM | high | unsigned int | - | 1 | 4 | 0 |
| 0x180d | Ladezustand Hochvoltspeicher | % | high | unsigned int | - | 1 | 10 | 0 |
| 0x180e | Aktueller Drosselklappenwinkel | % | high | unsigned char | - | 1 | 1 | 0 |
| 0x180f | Steuergeraetetemperatur | A grad | high | signed int | - | 1 | 100 | 0 |
| 0x4500 | Status DCDC-Wandler | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4501 | Auslastung DC/DC Converter | - | high | unsigned char | - | 0.5 | 1 | 0 |
| 0x4502 | Relativzaehler fuer Ladezustand SoC | - | high | unsigned int | - | 100 | 65536 | 0 |
| 0x4503 | Zaehler Genauigkeit Ladeztustandsbestimmung | - | high | unsigned int | - | 18 | 989 | 0 |
| 0x4504 | Batteriespannung vom IBS gemessen | V | high | unsigned int | - | 1 | 4000 | 6 |
| 0x4505 | Batteriestrom vom IBS gemessen | mA | high | unsigned int | - | 1 | 12.5 | -200 |
| 0x4506 | IBS Status-/Fehlerbyte | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4507 | IBS Status-/Fehlerbyte | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4509 | Sollwert Drehzahl Zusatzwasserpumpe LIN | Upm | high | unsigned char | - | 1 | 1 | 0 |
| 0x450a | Istwert Drehzahl Zusatzwasserpumpe LIN | Upm | high | unsigned char | - | 1 | 1 | 0 |
| 0x450c | Fahrzeuggeschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 0x450d | Umgebungstemperatur | A grad | high | signed int | - | 1 | 10 | 0 |
| 0x450f | Main battery voltage | V | high | signed int | - | 1 | 128 | 0 |
| 0x4510 | Hauptuefteransteuerung in Prozent | % | high | unsigned char | - | 100 | 256 | 0 |
| 0x4511 | Batterietemperatur vom IBS gemessen | grad | high | signed int | - | 1 | 10 | 0 |
| 0x4512 | Relativzeit | s | high | unsigned long | - | 1 | 1 | 0 |
| 0x4513 | Ist Kuehlmittel Temperatur Motorsteuerung Elektrisch | A grad | high | unsigned char | - | 1 | 1 | -48 |
| 0x4515 | Zeigt die Zustaende des Zustandsautomaten an | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x4516 | Temperatur Zusatzwasserpumpe LIN | A grad | high | signed int | - | 1 | 100 | 0 |
| 0x4517 | Spannung Zusatzwasserpumpe LIN | V | high | unsigned char | - | 1 | 10 | 0 |
| 0x4518 | Solldrehzahl elektrische Wasserpumpe zur Kuehlung E-Maschine und EME | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4519 | Status Rueckmeldung der EWP21 (0 = i.O.; 3 = n.i.O.) | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x451a | Bordnetzspannung | - | high | unsigned int | - | 0.0942 | 1 | 0 |
| 0x451b | Ist-Temperatur Leistungselektronik fuer WMK | - | high | signed int | - | 1 | 100 | 0 |
| 0x451c | Vorgabe Generator-Sollspannung (Ausgabewert) | - | high | unsigned int | - | 1 | 10 | 0 |
| 0x451d | T2 Histogramm (80 - 200 mA) als Umweltbed. bei Ruhestromverletzung | - | high | unsigned char | - | 224 | 15 | 0 |
| 0x451e | T3 Histogramm (200 - 1000 mA) als Umweltbed. bei Ruhestromverletzung | - | high | unsigned char | - | 224 | 15 | 0 |
| 0x451f | T4 Histogramm (&gt; 1000 Ah) als Umweltbed. bei Ruhestromverletzung | - | high | unsigned char | - | 224 | 15 | 0 |
| 0x4520 | Abstellzeit in Minuten | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x4521 | Saisontemperatur | A grad | high | signed int | - | 1 | 10 | 0 |
| 0x4522 | Strom DCDC-Wandler | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4523 | Entlademenge waehrend Zeit mit erhoehtem Ruhestrom | - | high | unsigned int | - | 18 | 989 | 0 |
| 0x4524 | HiByte Stat_sv_reg fuer Umweltbedingung | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x4525 | FuSi Ebene 2: Status Momentenueberwachung | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x4526 | FuSi Ebene 2: Status Fahreranwesenheit / Fahrbereitschaft | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x4527 | FuSi Ebene 2: Fahrstufe Status | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x4528 | FuSi Ebene 2: Gueltigkeit Eingangssignale | - | high | unsigned long | - | 1 | 1 | 0 |
| 0x4529 | FuSi Ebene 2: Maximal zulaessiges Zugmoment | Nm | high | signed int | - | 1 | 10 | 0 |
| 0x452a | FuSi Ebene 2: Sollmoment der EM1 | Nm | high | signed int | - | 1 | 10 | 0 |
| 0x452b | FuSi Ebene 2: Target torque value from the eDME controll unit for electric motor | Nm | high | signed int | - | 1 | 10 | 0 |
| 0x452c | FuSi Ebene 2: Maximal zulaessiges Schubmoment | Nm | high | signed int | - | 1 | 10 | 0 |
| 0x452d | FuSi Ebene 2: Gefilterte Geschwindigkeit der U-Funktion | km/h | high | signed int | - | 1 | 10 | 0 |
| 0x452e | Gefilterte Fahrzeuggeschwindigkeit (DSC) | - | high | signed int | - | 1 | 10 | 0 |
| 0x452f | FuSi Ebene 2: gas pedal position | % | high | signed int | - | 100 | 4096 | 0 |
| 0x4530 | FuSi Ebene 2: variable for the CAN signal TAR_2_WMOM_PT_SUM_DRS | Nm | high | signed int | - | 1 | 1 | 0 |
| 0x4531 | FuSi Ebene 2: Minimales Moment laut Anforderung von EF | Nm | high | signed int | - | 1 | 10 | 0 |
| 0x4532 | FuSi Ebene 2: Radmomentenanforderung DSC | Nm | high | signed int | - | 1 | 10 | 0 |
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

Dimensions: 29 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x21E730 | BMW dummy FIS. Wird nie gesetzt | 0 | - |
| 0x21E755 | Elektrolüfter: PWM Sammelleitungsfehler | 0 | - |
| 0x21E756 | Elektrolüfter: Ansteuerung gelbe CC-Meldung | 0 | - |
| 0x21E758 | Elektrolüfter, Relais: Sammelleitungsfehler | 0 | - |
| 0x21E767 | Fehlerort 1 fur FSP Testfunktion Layer: No symptom | 0 | - |
| 0x21E768 | Fehlerort 2 fur FSP Testfunktion Layer: No symptom | 0 | - |
| 0x21E938 | Leiterplatte: Übertemperatur | 0 | - |
| 0x21E939 | Leiterplatte: Temperatur zu niedrig, unplausibel | 0 | - |
| 0x21E947 | Systemzeit ungueltig | 1 | - |
| 0x21E948 | Zusatzlüfter Motorraum, Senseleitung: Leitungsunterbrechung | 0 | - |
| 0x21E949 | Zusatzlüfter Motorraum, Senseleitung: Kurzschluss nach Masse | 0 | - |
| 0x21E94A | Zusatzlüfter Motorraum, Senseleitung: Kurzschluss nach Plus | 0 | - |
| 0x21E94E | eDME: Temperatur zu hoch | 0 | - |
| 0x21E94F | eDME: Temperatur zu niedrig | 0 | - |
| 0x230004 | Kommunikation Einschlafkoordinator Zeitüberschreitung | 0 | - |
| 0x230008 | Kommunikation Einschlafkoordinator: Nachricht unplausibel | 0 | - |
| 0x4823CE | Puffer für ausgehende Fehlermeldungen ist voll | 1 | - |
| 0x4823CF | Fehler konnte nach maximaler Anzahl von Versuchen nicht gesendet werden | 1 | - |
| 0xCD8C0C | Check-Control-Meldung: Batterie OK (im Transportmodus) | 0 | - |
| 0xCD8C15 | Zusatzlüfter Motorraum: Sammelfehler Spannungsmessleitung | 0 | - |
| 0xCD8C16 | Zusatzlüfter, Relais, Ansteuerung: Sammelfehler | 0 | - |
| 0xCD8C3C | Momentenreduzierung bei Überlastung Kühlsystem | 0 | - |
| 0xCD8C3D | Check-Control-Meldung: Motor zu heiß! Gemäßigt fahren | 0 | - |
| 0xCD8C3E | Check-Control-Meldung: Motor überhitzt! Vorsichtig halten | 0 | - |
| 0xCD8C3F | Check-Control-Meldung: Motor zu heiß! Drehzahl reduzieren | 0 | - |
| 0xCD8C4B | Ausloesung der CCM569 abhängig von der Ausloesung der CCM569. Diese CCM sperrt ueber das Kombi die Ausloesung der EGS-Passivmeldung | 0 | - |
| 0xCD8C4C | Anforderung des Dauergongs (CCM) vom Kombi ueber die FID Schnittstelle. | 0 | - |
| 0xCD8C53 | Anforderung Rennstart-CC-Meldung | 0 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 16 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4501 | ALS_DCDC_RAW | % | High | unsigned char | - | 0.5 | 1.0 | 0.0 |
| 0x4502 | SOC_REL | % | High | unsigned int | - | 100.0 | 65535.0 | 0.0 |
| 0x4503 | SOC_QUALI | Ah | High | unsigned int | - | 18.0 | 989.0 | 0.0 |
| 0x4504 | U_BATT | V | High | unsigned int | - | 1.0 | 4000.0 | 6.0 |
| 0x4505 | I_BATT | A | High | unsigned int | - | 1.0 | 12.5 | 200.0 |
| 0x4511 | T_BATT | ° | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x451C | ENV_U_GEN | - | High | unsigned int | - | 1.0 | 10.0 | 0.0 |
| 0x451D | ENV_T2HISTSHORT | - | High | unsigned char | - | 224.0 | 15.0 | 0.0 |
| 0x451E | ENV_T3HISTSHORT | - | High | unsigned char | - | 224.0 | 115.0 | 0.0 |
| 0x451F | ENV_T4HISTSHORT | - | High | unsigned char | - | 224.0 | 15.0 | 0.0 |
| 0x4520 | ENV_TN_ABSTELLM | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x4521 | ENV_T_SAISON | - | High | signed int | - | 1.0 | 10.0 | 0.0 |
| 0x4522 | ENV_I_DCDC | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x4523 | ENV_Q_IRUHE2 | - | High | unsigned int | - | 18.0 | 989.0 | 0.0 |
| 0x4524 | ENV_STAT_SV_REG2 | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0x409d-d"></a>
### RES_0X409D_D

Dimensions: 47 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand beim Parken |
| STAT_SYSTEMZEIT_PARKEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeitstempel beim Parken |
| STAT_12V_BATTERIE_SOC_PARKEN_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ladezustand der 12V-Batterie beim Ablegen des Fahrzeuges |
| STAT_E1_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 1 (letzter) - Kilometerstand beim Parken |
| STAT_E2_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 2 - Kilometerstand beim Parken |
| STAT_E3_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 3 - Kilometerstand beim Parken |
| STAT_E4_KM_STAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 4 - Kilometerstand beim Parken |
| STAT_E1_SYSTEMZEIT_PARKEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 1 (letzter) - Zeitstempel beim Parken |
| STAT_E2_SYSTEMZEIT_PARKEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 2 - Zeitstempel beim Parken |
| STAT_E3_SYSTEMZEIT_PARKEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 3 - Zeitstempel beim Parken |
| STAT_E4_SYSTEMZEIT_PARKEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 4 - Zeitstempel beim Parken |
| STAT_E1_12V_BATTERIE_SOC_PARKEN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 1 (letzter) - Ladezustand der 12V-Batterie beim Parken |
| STAT_E2_12V_BATTERIE_SOC_PARKEN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 2 - Ladezustand der 12V-Batterie beim Parken |
| STAT_E3_12V_BATTERIE_SOC_PARKEN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 3 - Ladezustand der 12V-Batterie beim Parken |
| STAT_E4_12V_BATTERIE_SOC_PARKEN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 4 - Ladezustand der 12V-Batterie beim Parken |
| STAT_E1_SYSTEMZEIT_LADEBEGINN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 1 ( letzter) - Zeitstempel beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E2_SYSTEMZEIT_LADEBEGINN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 2 - Zeitstempel beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E3_SYSTEMZEIT_LADEBEGINN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 3 - Zeitstempel beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E4_SYSTEMZEIT_LADEBEGINN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Satz 4 - Zeitstempel beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E1_12V_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 1 (letzter) - Ladezustand der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E2_12V_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 2 - Ladezustand der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E3_12V_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 3 - Ladezustand der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E4_12V_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 4 - Ladezustand der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E1_HV_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 1 (letzter) - Ladezustand der Hochvolt-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E2_HV_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 2 - Ladezustand der Hochvolt-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E3_HV_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 3 - Ladezustand der Hochvolt-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E4_HV_BATTERIE_SOC_LADEBEGINN_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 4 - Ladezustand der Hochvolt-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E1_12V_BATTERIE_TEMP_LADEBEGINN_WERT | °C | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Satz 1 (letzter) - Temperatur der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E2_12V_BATTERIE_TEMP_LADEBEGINN_WERT | °C | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Satz 2 - Temperatur der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E3_12V_BATTERIE_TEMP_LADEBEGINN_WERT | °C | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Satz 3 - Temperatur der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E4_12V_BATTERIE_TEMP_LADEBEGINN_WERT | °C | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Satz 4 - Temperatur der 12V-Batterie beim Starten des 12V-Batterie Ladevorgangs |
| STAT_E1_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Satz 1 (letzter) - Ladedauer (Zeitunterschied zwischen Ladebegin und Ladeende) |
| STAT_E2_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Satz 2 - Ladedauer (Zeitunterschied zwischen Ladebegin und Ladeende) |
| STAT_E3_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Satz 3 - Ladedauer (Zeitunterschied zwischen Ladebegin und Ladeende) |
| STAT_E4_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Satz 4 - Ladedauer (Zeitunterschied zwischen Ladebegin und Ladeende) |
| STAT_E1_12V_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 1 (letzter) - Ladezustand der 12V-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E2_12V_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 2 - Ladezustand der 12V-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E3_12V_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 3 - Ladezustand der 12V-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E4_12V_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 4 - Ladezustand der 12V-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E1_HV_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 1 (letzter) - Ladezustand der Hochvolt-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E2_HV_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 2 - Ladezustand der Hochvolt-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E3_HV_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 3 - Ladezustand der Hochvolt-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E4_HV_BATTERIE_SOC_LADEENDE_WERT | % | high | unsigned char | - | - | 1.0 | 2.0 | 0.0 | Satz 4 - Ladezustand der Hochvolt-Batterie beim Beenden des 12V-Batterie Ladevorgangs (=Ladezustand beim Starten wenn Laden nicht möglich) |
| STAT_E1_12VLADEFEHLER | 0-n | high | unsigned char | - | TAB_12VLADEN_LADEFEHLER | - | - | - | Satz 1 (letzter) - Ladeendegrund |
| STAT_E2_12VLADEFEHLER | 0-n | high | unsigned char | - | TAB_12VLADEN_LADEFEHLER | - | - | - | Satz 2 - Ladeendegrund |
| STAT_E3_12VLADEFEHLER | 0-n | high | unsigned char | - | TAB_12VLADEN_LADEFEHLER | - | - | - | Satz 3 - Ladeendegrund |
| STAT_E4_12VLADEFEHLER | 0-n | high | unsigned char | - | TAB_12VLADEN_LADEFEHLER | - | - | - | Satz 4 - Ladeendegrund |

<a id="table-res-0x409e-d"></a>
### RES_0X409E_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_A_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (2 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_B_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich B.   K_STDZEITLADEHISTGRZ1 (2 Tage) &lt; Bereich B &lt;= K_STDZEITLADEHISTGRZ2 (4 Tage)  (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_C_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich C.  K_STDZEITLADEHISTGRZ2 (4 Tage) &lt; Bereich C &lt;= K_STDZEITLADEHISTGRZ3 (6 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_D_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich D.  K_STDZEITLADEHISTGRZ3 (6 Tage) &lt; Bereich D &lt;= K_STDZEITLADEHISTGRZ4 (10 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_E_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich E.  K_STDZEITLADEHISTGRZ4 (10 Tage) &lt; Bereich E &lt;= K_STDZEITLADEHISTGRZ5 (14 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_F_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich F.  K_STDZEITLADEHISTGRZ5 (14 Tage) &lt; Bereich F &lt;= K_STDZEITLADEHISTGRZ6 (21 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_G_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich G.  K_STDZEITLADEHISTGRZ6 (21 Tage) &lt; Bereich G &lt;= K_STDZEITLADEHISTGRZ7 (28 Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_STANDZEIT_BIS_LADEBEGINN_BEREICH_H_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich H.  K_STDZEITLADEHISTGRZ7 (28 Tage) &lt; Bereich H (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_A_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich A.  Bereich A &lt;= K_NLDDAUERHISTGRZ1 (3 Minuten)  (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_B_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich B.   K_NLDDAUERHISTGRZ1 (3 Minuten) &lt; Bereich B &lt;= K_NLDDAUERHISTGRZ2 (6 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_C_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich C.   K_NLDDAUERHISTGRZ2 (6 Minuten) &lt; Bereich C &lt;= K_NLDDAUERHISTGRZ3 (10 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_D_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich D.   K_NLDDAUERHISTGRZ3 (10 Minuten) &lt; Bereich D &lt;= K_NLDDAUERHISTGRZ4 (15 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_E_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich E.   K_NLDDAUERHISTGRZ4 (15 Minuten) &lt; Bereich E &lt;= K_NLDDAUERHISTGRZ5 (20 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_F_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich F.   K_NLDDAUERHISTGRZ5 (20 Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ6 (28 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_G_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G.   K_NLDDAUERHISTGRZ6 (28 Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ7 (45 Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_HFK_LADEDAUER_BEREICH_H_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich H. K_NLDDAUERHISTGRZ7 (45 Minuten) &lt; Bereich H (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |

<a id="table-res-0xa1d0-r"></a>
### RES_0XA1D0_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE_STATUS | - | - | + | 0-n | high | unsigned char | - | TAB_ENTLUEFTUNGSROUTINE_STATUS | - | - | - | Status der Routine. Siehe Tabelle TAB_ENTLUEFTUNGSROUTINE_STATUS |
| STAT_RESTZEIT_WERT | - | - | + | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Restzeit der Routine in Sekunden |

<a id="table-res-0xadc2-r"></a>
### RES_0XADC2_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUE_AKTIV | - | - | + | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | aktueller Zustand des E-Lüfter ( 0 = aus, 1 = ein ) |
| STAT_ELUESOLL_WERT | - | - | + | % | high | unsigned char | - | - | 0.3906 | 1.0 | 0.0 | aktuelle Drehzahl des E-Lüfters (in %) |

<a id="table-res-0xadc6-r"></a>
### RES_0XADC6_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUEZL_AKTIV | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | aktueller Zustand des E-Lüfter ( 0 = aus, 1 = ein ) |
| STAT_ELUESOLL_WERT | - | - | + | % | high | unsigned char | - | - | 0.3906 | 1.0 | 0.0 | aktuelle Drehzahl des E-Lüfters (in %) |

<a id="table-res-0xadc7-r"></a>
### RES_0XADC7_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUERELSOLL_NR | - | - | + | 0-n | high | unsigned char | - | TAB_LUEFTER | - | - | - | Status vom Relais E-Lüfter |

<a id="table-res-0xadc8-r"></a>
### RES_0XADC8_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ELUERELZLSOLL_NR | - | - | + | 0-n | high | unsigned char | - | TAB_LUEFTER | - | - | - | Status vom Relais des Zusatzlüfters |

<a id="table-res-0xadf3-r"></a>
### RES_0XADF3_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANSTEUERUNG_ERFOLGREICH_EIN | - | - | + | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ansteuerung  der LIN Wasserpumpe EME (0 - Job inaktiv; 1 - Job aktiv) |
| STAT_ST_DIAG_EWP21_NR | - | - | + | 0-n | high | unsigned char | - | TAB_ST_DIAG_EWP21 | - | - | - | Status der Elektrischen Wasserpumpe (PWM) |

<a id="table-res-0xde9c-d"></a>
### RES_0XDE9C_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_PEDALWERT1_WERT | V | high | unsigned int | - | - | 0.0049 | 1.0 | 0.0 | Spannung gemessen am Pedalwertgeber 1 |
| STAT_SPANNUNG_PEDALWERT2_WERT | V | high | unsigned int | - | - | 0.0049 | 1.0 | 0.0 | Spannung gemessen am Pedalwertgeber 2 |
| STAT_PEDALWERT_WERT | % | high | unsigned int | - | - | 0.0625 | 1.0 | 0.0 | Aus Pedalwertgeber 1 und 2 ermittelter Pedalwert |

<a id="table-res-0xdee1-d"></a>
### RES_0XDEE1_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BETRIEB_KILOMETER_WERT | km | high | unsigned long | - | - | 0.001 | 1.0 | 0.0 | Gefahrene Kilometer |
| STAT_LAUFZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Laufzeit Range Extender Motor |
| STAT_BETRIEB_ERSTSTARTS_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Erststart-Vorgänge |
| STAT_BETRIEB_MSA_STARTS_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl MSA - Startvorgänge |
| STAT_REX_BETRIEB_WARTUNG_STARTS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Number of special rex starts (exhaust-gas test or SGBD) |
| STAT_REX_BETRIEB_BEZUGSKILOMETER_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gefahrene Kilometer (elektrisch) die von der Statistik erfasst wurden |

<a id="table-res-0xdee2-d"></a>
### RES_0XDEE2_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REX_ZEIT_IN_DREHZAHL_1_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 1 |
| STAT_REX_ZEIT_IN_DREHZAHL_2_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 2 |
| STAT_REX_ZEIT_IN_DREHZAHL_3_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 3 |
| STAT_REX_ZEIT_IN_DREHZAHL_4_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 4 |
| STAT_REX_ZEIT_IN_DREHZAHL_5_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 5 |
| STAT_REX_ZEIT_IN_DREHZAHL_6_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 6 |
| STAT_REX_ZEIT_IN_DREHZAHL_7_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 7 |
| STAT_REX_ZEIT_IN_DREHZAHL_8_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 8 |
| STAT_REX_ZEIT_IN_DREHZAHL_9_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 9 |
| STAT_REX_ZEIT_IN_DREHZAHL_10_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 10 |
| STAT_REX_ZEIT_IN_DREHZAHL_11_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 11 |
| STAT_REX_ZEIT_IN_DREHZAHL_12_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 12 |
| STAT_REX_ZEIT_IN_DREHZAHL_13_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 13 |
| STAT_REX_ZEIT_IN_DREHZAHL_14_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 14 |
| STAT_REX_ZEIT_IN_DREHZAHL_15_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 15 |
| STAT_REX_ZEIT_IN_DREHZAHL_16_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 16 |
| STAT_REX_ZEIT_IN_DREHZAHL_17_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 17 |
| STAT_REX_ZEIT_IN_DREHZAHL_18_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Betriebszeit in Drehzahlbereich 18 |

<a id="table-res-0xdefd-d"></a>
### RES_0XDEFD_D

Dimensions: 51 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PARKEN_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Systemzeit beim Parken |
| STAT_PARKEN_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Kilometerstand beim Parken |
| STAT_PARKEN_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | SOC 12V Batterie beim Parken |
| STAT_E1_PARKEN_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 1. Ereignis (letzte): Systemzeit beim Parken |
| STAT_E1_PARKEN_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 1. Ereignis (letzte): Kilometerstand beim Parken |
| STAT_E1_PARKEN_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 1. Ereignis (letzte): SOC 12V Batterie beim Parken |
| STAT_E1_START_ZYKNL_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 1. Ereignis (letzte): Systemzeit beim Start des zyklischen Nachladens |
| STAT_E1_START_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 1. Ereignis (letzte): SOC 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E1_START_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 1. Ereignis (letzte): SOC HV-Batterie beim Start des zyklischen Nachladens |
| STAT_E1_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -128.0 | 1. Ereignis (letzte): Temperatur der 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E1_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 1.0 | 1. Ereignis (letzte): Dauer des zyklischen Nachladens |
| STAT_E1_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 1. Ereignis (letzte): SOC 12V Batterie beim Ende des zyklischen Nachladens |
| STAT_E1_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 1. Ereignis (letzte): SOC HV-Batterie beim Ende des zyklischen Nachladens |
| STAT_E1_GRUND_LADEENDE | 0-n | high | unsigned char | - | TAB_ZYKNL_GRUND_LADEENDE | - | - | - | 1. Ereignis (letzte): Grund Ladeende |
| STAT_E1_ZYKNL_PROGNOSE_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 1. Ereignis (letzte): Prognose, ob weiteres zykl. NL möglich (0 = nein, 1 = ja) |
| STAT_E2_PARKEN_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 2. Ereignis: Systemzeit beim Parken |
| STAT_E2_PARKEN_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 2. Ereignis: Kilometerstand beim Parken |
| STAT_E2_PARKEN_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 2. Ereignis: SOC 12V Batterie beim Parken |
| STAT_E2_START_ZYKNL_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 2. Ereignis: Systemzeit beim Start des zyklischen Nachladens |
| STAT_E2_START_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 2. Ereignis: SOC 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E2_START_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 2. Ereignis: SOC HV-Batterie beim Start des zyklischen Nachladens |
| STAT_E2_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -128.0 | 2. Ereignis: Temperatur der 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E2_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 1.0 | 2. Ereignis: Dauer des zyklischen Nachladens |
| STAT_E2_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 2. Ereignis: SOC 12V Batterie beim Ende des zyklischen Nachladens |
| STAT_E2_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 2. Ereignis: SOC HV-Batterie beim Ende des zyklischen Nachladens |
| STAT_E2_GRUND_LADEENDE | 0-n | high | unsigned char | - | TAB_ZYKNL_GRUND_LADEENDE | - | - | - | 2. Ereignis: Grund Ladeende |
| STAT_E2_ZYKNL_PROGNOSE_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 2. Ereignis: Prognose, ob weiteres zykl. NL möglich (0 = nein, 1 = ja) |
| STAT_E3_PARKEN_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 3. Ereignis: Systemzeit beim Parken |
| STAT_E3_PARKEN_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 3. Ereignis: Kilometerstand beim Parken |
| STAT_E3_PARKEN_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 3. Ereignis: SOC 12V Batterie beim Parken |
| STAT_E3_START_ZYKNL_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 3. Ereignis: Systemzeit beim Start des zyklischen Nachladens |
| STAT_E3_START_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 3. Ereignis: SOC 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E3_START_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 3. Ereignis: SOC HV-Batterie beim Start des zyklischen Nachladens |
| STAT_E3_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -128.0 | 3. Ereignis: Temperatur der 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E3_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 1.0 | 3. Ereignis: Dauer des zyklischen Nachladens |
| STAT_E3_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 3. Ereignis: SOC 12V Batterie beim Ende des zyklischen Nachladens |
| STAT_E3_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 3. Ereignis: SOC HV-Batterie beim Ende des zyklischen Nachladens |
| STAT_E3_GRUND_LADEENDE | 0-n | high | unsigned char | - | TAB_ZYKNL_GRUND_LADEENDE | - | - | - | 3. Ereignis: Grund Ladeende |
| STAT_E3_ZYKNL_PROGNOSE_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 3. Ereignis: Prognose, ob weiteres zykl. NL möglich (0 = nein, 1 = ja) |
| STAT_E4_PARKEN_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 4. Ereignis: Systemzeit beim Parken |
| STAT_E4_PARKEN_KILOMETERSTAND_WERT | km | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 4. Ereignis: Kilometerstand beim Parken |
| STAT_E4_PARKEN_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 4. Ereignis: SOC 12V Batterie beim Parken |
| STAT_E4_START_ZYKNL_SYSTEMZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | 4. Ereignis: Systemzeit beim Start des zyklischen Nachladens |
| STAT_E4_START_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 4. Ereignis: SOC 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E4_START_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 4. Ereignis: SOC HV-Batterie beim Start des zyklischen Nachladens |
| STAT_E4_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -128.0 | 4. Ereignis: Temperatur der 12V Batterie beim Start des zyklischen Nachladens |
| STAT_E4_LADEDAUER_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 1.0 | 4. Ereignis: Dauer des zyklischen Nachladens |
| STAT_E4_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 4. Ereignis: SOC 12V Batterie beim Ende des zyklischen Nachladens |
| STAT_E4_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | % | high | unsigned char | - | - | 0.5 | 1.0 | 0.0 | 4. Ereignis: SOC HV-Batterie beim Ende des zyklischen Nachladens |
| STAT_E4_GRUND_LADEENDE | 0-n | high | unsigned char | - | TAB_ZYKNL_GRUND_LADEENDE | - | - | - | 4. Ereignis: Grund Ladeende |
| STAT_E4_ZYKNL_PROGNOSE_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 4. Ereignis: Prognose, ob weiteres zykl. NL möglich (0 = nein, 1 = ja) |

<a id="table-res-0xdefe-d"></a>
### RES_0XDEFE_D

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_A_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_B_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich B.  K_STDZEITLADEHISTGRZ1 (Tage) &lt; Bereich B &lt;= K_STDZEITLADEHISTGRZ2 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_C_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich B.  K_STDZEITLADEHISTGRZ2 (Tage) &lt; Bereich C &lt;= K_STDZEITLADEHISTGRZ3 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_D_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich D.  K_STDZEITLADEHISTGRZ3 (Tage) &lt; Bereich D &lt;= K_STDZEITLADEHISTGRZ4 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_E_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich E.  K_STDZEITLADEHISTGRZ4 (Tage) &lt; Bereich E &lt;= K_STDZEITLADEHISTGRZ5 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_F_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich F.  K_STDZEITLADEHISTGRZ5 (Tage) &lt; Bereich F &lt;= K_STDZEITLADEHISTGRZ6 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_G_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich G.  K_STDZEITLADEHISTGRZ6 (Tage) &lt; Bereich G &lt;= K_STDZEITLADEHISTGRZ7 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_H_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich H.  K_STDZEITLADEHISTGRZ7 (Tage) &lt; Bereich H  (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_A_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_NLDDAUERHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_B_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich B. K_NLDDAUERHISTGRZ1 (Tage) &lt; Bereich B &lt;= K_NLDDAUERHISTGRZ2 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_C_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich C. K_NLDDAUERHISTGRZ2 (Tage) &lt; Bereich C &lt;= K_NLDDAUERHISTGRZ3 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_D_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich D. K_NLDDAUERHISTGRZ3 (Tage) &lt; Bereich D &lt;= K_NLDDAUERHISTGRZ4 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_E_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich E. K_NLDDAUERHISTGRZ4 (Tage) &lt; Bereich E &lt;= K_NLDDAUERHISTGRZ5 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_F_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich F. K_NLDDAUERHISTGRZ5 (Tage) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ6 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_G_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G. K_NLDDAUERHISTGRZ6 (Tage) &lt; Bereich G &lt;= K_NLDDAUERHISTGRZ7 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |
| STAT_LADUNGSDAUER_BEREICH_H_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich H. K_NLDDAUERHISTGRZ7 (Tage) &lt; Bereich H  (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) |

<a id="table-res-0xdf53-d"></a>
### RES_0XDF53_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REX_TEMPERATUR_MOTOR_KUEHLMITTEL_1_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Kühlmittel 1 |
| STAT_REX_TEMPERATUR_MOTOR_KUEHLMITTEL_2_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Kühlmittel 2 |
| STAT_REX_TEMPERATUR_MOTOR_KUEHLMITTEL_3_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Kühlmittel 3 |
| STAT_REX_TEMPERATUR_MOTOROEL_1_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Motoröl 1 |
| STAT_REX_TEMPERATUR_MOTOROEL_2_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Motoröl 2 |
| STAT_REX_TEMPERATUR_MOTOROEL_3_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik REX Motoröl 3 |
| STAT_REX_TEMPERATUR_UMGEBUNG_1_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik Umgebungstemperatur 1 |
| STAT_REX_TEMPERATUR_UMGEBUNG_2_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik Umgebungstemperatur 2 |
| STAT_REX_TEMPERATUR_UMGEBUNG_3_WERT | s | high | unsigned long | - | - | 0.1 | 1.0 | 0.0 | Temperaturstatistik Umgebungstemperatur 3 |

<a id="table-res-0xdf54-d"></a>
### RES_0XDF54_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REX_FAHRT_KILOMETER_KLASSE_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Zyklen in Kilometer Klasse 1 |
| STAT_REX_FAHRT_KILOMETER_KLASSE_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Zyklen in Kilometer Klasse 2 |
| STAT_REX_FAHRT_KILOMETER_KLASSE_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Zyklen in Kilometer Klasse 3 |
| STAT_REX_FAHRT_KILOMETER_KLASSE_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Zyklen in Kilometer Klasse 4 |
| STAT_REX_FAHRT_KILOMETER_KLASSE_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Zyklen in Kilometer Klasse 5 |

<a id="table-res-0xdf55-d"></a>
### RES_0XDF55_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZYKLEN_GESAMT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für alle Fahrzyklen |
| STAT_ZYKLEN_REX_BETRIEB_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Zähler für alle Fahrzyklen, wo der REX gelaufen ist. |

<a id="table-res-0xdf56-d"></a>
### RES_0XDF56_D

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REX_START_SOC_1_KM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 1 |
| STAT_REX_START_SOC_2_KM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 1 |
| STAT_REX_START_SOC_3_KM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 1 |
| STAT_REX_START_SOC_4_KM_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 1 |
| STAT_REX_START_SOC_1_KM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 2 |
| STAT_REX_START_SOC_2_KM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 2 |
| STAT_REX_START_SOC_3_KM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 2 |
| STAT_REX_START_SOC_4_KM_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 2 |
| STAT_REX_START_SOC_1_KM_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 3 |
| STAT_REX_START_SOC_2_KM_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 3 |
| STAT_REX_START_SOC_3_KM_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 3 |
| STAT_REX_START_SOC_4_KM_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 3 |
| STAT_REX_START_SOC_1_KM_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 4 |
| STAT_REX_START_SOC_2_KM_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 4 |
| STAT_REX_START_SOC_3_KM_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 4 |
| STAT_REX_START_SOC_4_KM_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 4 |
| STAT_REX_START_SOC_1_KM_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 5 |
| STAT_REX_START_SOC_2_KM_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 5 |
| STAT_REX_START_SOC_3_KM_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 5 |
| STAT_REX_START_SOC_4_KM_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 5 |
| STAT_REX_START_SOC_1_KM_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 6 |
| STAT_REX_START_SOC_2_KM_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 6 |
| STAT_REX_START_SOC_3_KM_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 6 |
| STAT_REX_START_SOC_4_KM_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 6 |
| STAT_REX_START_SOC_1_KM_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 7 |
| STAT_REX_START_SOC_2_KM_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 7 |
| STAT_REX_START_SOC_3_KM_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 7 |
| STAT_REX_START_SOC_4_KM_7_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 7 |
| STAT_REX_START_SOC_1_KM_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 1, elektrisch gefahrene Kilometer Klasse 8 |
| STAT_REX_START_SOC_2_KM_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 2, elektrisch gefahrene Kilometer Klasse 8 |
| STAT_REX_START_SOC_3_KM_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 3, elektrisch gefahrene Kilometer Klasse 8 |
| STAT_REX_START_SOC_4_KM_8_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX Starts für SOC Klasse 4, elektrisch gefahrene Kilometer Klasse 8 |

<a id="table-res-0xdf5e-d"></a>
### RES_0XDF5E_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REX_BETRIEB_LANGZEITSTART_IO_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl erfolgreich durchgelaufene Langzeitstarts |
| STAT_REX_BETRIEB_LANGZEITSTART_NIO_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl abgebrochene Langzeitstarts |
| STAT_REX_BETRIEB_TANK_LEER_STOPS_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl REX-Ablegen aufgrund eines leeren Tanks |

<a id="table-res-0xf000-r"></a>
### RES_0XF000_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DIAG_AEP_TEST_BATTERY_GUARD_EIN | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | Aktueller Zustand Test: 0 = Keine Anforderung; 1 = Anforderung Battery Guard Call |

<a id="table-res-0xf086-r"></a>
### RES_0XF086_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_BETRIEBSARTEN_EM1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Funktionsstatus Tester-Vorgabe fuer E-Maschine 1 Betriebsart |
| STAT_BETRIEBSARTEN_EM1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | E-Maschine 1 Betriebsart lesen |

<a id="table-res-0xf087-r"></a>
### RES_0XF087_R

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_BETRIEBSARTEN_EM2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Funktionsstatus Tester-Vorgabe fuer E-Maschine 2 Betriebsart |
| STAT_BETRIEBSARTEN_EM2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | E-Maschine 2 Betriebsart lesen |

<a id="table-res-0xf0d5-r"></a>
### RES_0XF0D5_R

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_AKKS_SMOTPOAKKSLIN_WERT | - | - | + | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Sollposition in Schritten |
| STAT_AKKS_IS_POS_LIN_WERT | - | - | + | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Istposition in Schritten |
| STAT_AKKS_DSRD_POS_ANGLE_WERT | - | - | + | - | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Sollposition in Grad |
| STAT_AKKS_ACT_POS_ANGLE_WERT | - | - | + | - | high | signed char | - | - | 1.0 | 1.0 | 0.0 | Istposition in Grad |
| - | - | - | + | Bit | high | BITFIELD | - | BF_AKKS_ERROR | - | - | - | Diagnosestatus allgemein |
| STAT_VRSAKKLIN_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Varianteninfo vom Steller |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 67 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ENTLUEFTUNG_KUEHLSYSTEM | 0xA1D0 | - | Entlüftungsroutine für Kühlsystem, nur für F56 BEV | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA1D0_R |
| ELUE | 0xADC2 | - | Ansteuerung E-Lüfter | - | - | - | - | - | - | - | - | - | 31 | ARG_0xADC2_R | RES_0xADC2_R |
| ELUE_ZUSATZLUEFTER | 0xADC6 | - | Ansteuerung Zusatzlüfter | - | - | - | - | - | - | - | - | - | 31 | ARG_0xADC6_R | RES_0xADC6_R |
| ELUE_RELAIS | 0xADC7 | - | Ansteuerung Relais E-Lüfter | - | - | - | - | - | - | - | - | - | 31 | ARG_0xADC7_R | RES_0xADC7_R |
| ELUE_ZUSATZLUEFTER_RELAIS | 0xADC8 | - | Ansteuerung Relais Zusatzlüfter | - | - | - | - | - | - | - | - | - | 31 | ARG_0xADC8_R | RES_0xADC8_R |
| EME_EWAP | 0xADF3 | - | Ansteuerung der LIN Wasserpumpe EME mit Vorgabe der Drehzahl und Ansteuerzeit | - | St_diag_ewp_21 | - | - | - | - | - | - | - | 31 | ARG_0xADF3_R | RES_0xADF3_R |
| MCAMOS | 0xADFA | - | Rückwarenanalyse von Teilen aus dem Werk in Serie | - | - | - | - | - | - | - | - | - | 31 | - | - |
| 12V_NACHLADEHISTORIE_LOESCHEN | 0xAE02 | - | Löschen des Historienspeichers für die letzen 4 Ladevorgänge der 12V-Batterie aus der Hochvolt-Batterie (Ringspeicher mit je 4 Sätze) | - | - | - | - | - | - | - | - | - | 31 | - | - |
| 12V_NACHLADEHISTOGRAMM_LOESCHEN | 0xAE03 | - | Löschen von Histogramm und Zähler aller Ladevorgänge der 12V-Batterie aus dem Hochvolt-Sys | - | - | - | - | - | - | - | - | - | 31 | - | - |
| EME_KAELTEMITTEL_ABSPERRVENTIL_ON_OFF | 0xDE22 | STAT_AKAV_ON | Status des Kältemittelabsperrventils; 0 = Ventil geschlossen; 1 = Ventil offen | 0/1 | B_ctr_vent_ven | high | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| EME_KAELTEMITTEL_ABSPERRVENTIL | 0xDE23 | - | Ansteuerung des Kältemittelabsperrventils | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDE23_D | - |
| PEDALWERTGEBER | 0xDE9C | - | Werte vom Pedalwertgeber | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDE9C_D |
| REX_STATISTIK_BETRIEB | 0xDEE1 | - | Auslesen der Betriebs-Statistik vom Range Extender Motor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEE1_D |
| REX_STATISTIK_DREHZAHL | 0xDEE2 | - | Auslesen Drehzahl Statistik vom Range Extender Motor | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEE2_D |
| REX_STATISTIK_RESET | 0xDEE3 | - | Rücksetzen der Statistikzähler vom Range Extender Motor | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDEE3_D | - |
| WARTUNGSLAUF_REX_FAELLIG | 0xDEFC | - | Wartungslauf REX auslösen | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDEFC_D | - |
| ZYKLISCHES_NACHLADEN_INFO | 0xDEFD | - | Auslesen von wichtigen Kenngrößen der letzten 4 Vorgänge des zyklischen Nachladens plus dem letzten Parkvorgang. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEFD_D |
| ZYKLISCHES_NACHLADEN_HISTOGRAMM | 0xDEFE | - | Auslesen der Histogramme über die Standzeit bis zum Beginn des zyklischen Nachladens und der Ladedauern der zyklischen Nachladevorgänge | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDEFE_D |
| CBS_NV_RESET | 0xDF4E | - | CBS-Daten in EDME | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDF4E_D | - |
| REX_STATISTIK_TEMPERATUR | 0xDF53 | - | Temperaturstatistik vom REX-Verbrenner | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF53_D |
| REX_STATISTIK_KILOMETER_KLASSEN | 0xDF54 | - | Statistik mit Anzahl der Fahrten in den jeweiligen Kilometerklassen im REX-Betrieb. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF54_D |
| REX_STATISTIK_ZYKLEN | 0xDF55 | - | Zähler für Fahrzyklen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF55_D |
| REX_STATISTIK_SOC_KILOMETER_KLASSEN | 0xDF56 | - | Anzahl der REX-Starts nach X-Kilometer mit Y SOC bei Fahrtbeginn | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF56_D |
| REX_STATISTIK_ZAEHLER | 0xDF5E | - | Abfrage Zählerstatistik vom REX-Verbund | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDF5E_D |
| STEUERN_INTERLOCK | 0x1061 | - | LOCKED ECU | - | - | - | - | - | - | - | - | - | 31 | - | - |
| 12V_NACHLADEHISTORIE | 0x409D | - | Historie mit wichtigen Kenngrößen der 12V Nachladefunktion. Letzte 4 Datensätze | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x409D_D |
| 12V_NACHLADEHISTOGRAMM | 0x409E | - | Auslesen der Histogramme für 12V Nachladefunktion | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x409E_D |
| STATUS_E_S_KL_15_WUP | 0x4101 | STAT_E_S_KL15_WUP | Wakeup Line (E_S_KL15_WUP) | 0/1 | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_E_A_PWG1_RAW | 0x4102 | STAT_E_A_PWG1_RAW_WERT | Pedal Position Sensor 1 raw | V | - | high | unsigned int | - | 5.0 | 1024.0 | 0.0 | - | 22 | - | - |
| STATUS_E_A_PWG2_RAW | 0x4103 | STAT_E_A_PWG2_RAW_WERT | Pedal Position Sensor 2 raw | V | - | high | unsigned int | - | 5.0 | 1024.0 | 0.0 | - | 22 | - | - |
| STATUS_E_A_TMEL_RAW | 0x4104 | STAT_E_A_TMEL_RAW_WERT | Engine Temperatur raw | V | - | high | unsigned int | - | 5.0 | 4096.0 | 0.0 | - | 22 | - | - |
| STATUS_BATTERIE_VOLTAGE_RAUS | 0x4105 | STAT_BATTERY_VOLTAGE_RAW_WERT | Batterie Voltage raw | V | - | high | unsigned int | - | 5.0 | 4095.0 | 0.0 | - | 22 | - | - |
| STATUS_A_U_PWG1 | 0x4106 | STAT_A_U_PWG1_WERT | 5 V Supply 1 | V | - | high | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| STATUS_A_U_PWG2 | 0x4107 | STAT_A_U_PWG2_WERT | 5 V Supply 2 | V | - | high | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| STATUS_E_A_MEL | 0x4109 | STAT_E_A_MEL_WERT | Voltage Fan 2 raw | V | - | high | unsigned int | - | 12.5113 | 4095.0 | 0.0 | - | 22 | - | - |
| STATUS_ECU_MICRO_TEMPERATUR | 0x410A | STAT_ECU_MICRO_TEMPERATUR_WERT | Ecu micro Temperatur | °C | - | high | signed int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STATUS_E_A_TMEL2_RAW | 0x410B | STAT__WERT | E_A_TMEL2 | V | - | high | unsigned int | - | 5.0 | 1023.0 | 0.0 | - | 22 | - | - |
| _STEUERN_E_A_TMEL | 0x4114 | - | engine Temperatur | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4114_D | - |
| _STEUERN_BATTERY_VOLTAGE_RAW | 0x4115 | - | Battery Voltage Raw | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4115_D | - |
| _STEUERN_A_U_PWG1 | 0x4116 | - | 5 V Supply 1 | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4116_D | - |
| _STEUERN_A_U_PWG2 | 0x4117 | - | 5 V Supply 2 | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4117_D | - |
| _STEUERN_VOLTAGE_FAN_2 | 0x4119 | - | Voltage Fan 2 | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4119_D | - |
| _STEUERN_ECU_MICRO_TEMPERATUR | 0x411A | - | ECU Temperatur | - | - | - | - | - | - | - | - | - | 2F | ARG_0x411A_D | - |
| _STEUERN_TMEL2 | 0x411B | - | Steueren Motortemperatur 2 | - | - | - | - | - | - | - | - | - | 2F | ARG_0x411B_D | - |
| STATUS_A_S_ELRLY | 0x4120 | STAT_A_S_ELRLY | Status Electric Fan Relais | 0/1 | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_A_T_ELUE | 0x4121 | STAT_A_T_ELUE_WERT | Status Electric Fan Module | % | - | high | unsigned int | - | 100.0 | 65535.0 | 0.0 | - | 22 | - | - |
| STATUS_A_T_EWP | 0x4122 | STAT_A_T_EWAP_WERT | Water Pump | % | - | high | unsigned int | - | 100.0 | 65535.0 | 0.0 | - | 22 | - | - |
| STATUS_A_S_KV1 | 0x4123 | STAT_A_S_KV1 | Expansion Valve | 0/1 | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_A_S_KV2 | 0x4124 | STAT_A_S_KV2 | Shutoff Valve | 0/1 | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| STATUS_A_S_MEL | 0x4125 | STAT_A_S_MEL | Fan Relais 2 | 0/1 | - | high | unsigned int | - | - | - | - | - | 22 | - | - |
| _STEUERN_A_S_ELRLY | 0x4140 | - | Status electric Fan Relais | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4140_D | - |
| _STEUERN_A_T_ELUE | 0x4141 | - | Status Electric Fan Modul | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4141_D | - |
| _STEUERN_A_T_EWP | 0x4142 | - | Water Pump | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4142_D | - |
| STEUERN_A_S_KV1 | 0x4143 | - | Expansion Valve | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4143_D | - |
| _STEUERN_A_S_KV2 | 0x4144 | - | Shutoff Valve | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4144_D | - |
| _STEUERN_A_S_MEL | 0x4145 | - | Fan Relais 2 (A_S_MEL) | - | - | - | - | - | - | - | - | - | 2F | ARG_0x4145_D | - |
| STATUS_E_A_PWG1 | 0x4182 | STAT_E_A_PWG1_FILTERED_WERT | Pedal Position Sensor 1 filtered | % | - | high | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| STATUS_E_A_PWG2_FILTERED | 0x4183 | STAT_E_A_PWG2_FILTERED_WERT | Pedal position sensor 2 filtered | % | - | high | unsigned int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| STATUS_TEMPERATUR_SENSOR_1 | 0x4184 | STAT_TEMPERATUR_TEMPERATURSENSOR_1_WERT | Temperaturwert des ersten Temperatursensors im Motorraum | °C | - | high | signed int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| STATUS_BATTERY_VOLTAGE_FILTERED | 0x4185 | STAT_BATTERY_VOLTAGE_FILTERED_WERT | Battery Voltage filtered | V | - | high | signed int | - | 1.0 | 128.0 | 0.0 | - | 22 | - | - |
| STATUS_TEMPERATUR_SENSOR_2 | 0x418B | STAT_TEMPERATUR_TEMPERATURSENSOR_2_WERT | Temperaturwert des zweiten Temperatursensors im Motorraum | °C | - | high | signed int | - | 1.0 | 100.0 | 0.0 | - | 22 | - | - |
| AKKS_INPUTOUTPUTCONTROL | 0x60C3 | - | AKKS Ansteuerung | - | - | - | - | - | - | - | - | - | 2F | ARG_0x60C3_D | - |
| _AEP_GRUND_LADEENDE | 0x63F0 | - | Anforderung Setzen des letzter Grundes für Ladeende | - | - | - | - | - | - | - | - | - | 2E | ARG_0x63F0_D | - |
| _AEP_TEST_BATTERY_GUARD | 0xF000 | - | Anforderung Aufruf Battery Guard | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF000_R | RES_0xF000_R |
| STEUERN_BETRIEBSART_EM1 | 0xF086 | - | Steuern Betriebsart E-Maschine 1 | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF086_R | RES_0xF086_R |
| STEUERN_BETRIEBSART_EM2 | 0xF087 | - | Steuern Betriebsart E-Maschine 2 | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF087_R | RES_0xF087_R |
| STEUERN_AKKS | 0xF0D5 | - | Steuern der aktiven Kühlklappe | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF0D5_R |

<a id="table-table-status-eco2-funktionsstati"></a>
### TABLE_STATUS_ECO2_FUNKTIONSSTATI

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion nicht gestartet |
| 2 | Stop-Routine erfolgreich abgearbeitet |
| 3 | Funktion wartet auf Freigabe |
| 4 | Parameter unplausibel |
| 5 | Warten auf Trigger |
| 6 | Trigger erkannt |
| 7 | Funktion abgebrochen, Motor laeuft oder keine Rueckmeldung vom IBS |
| 8 | Messung beendet |
| 9 | Funktion abgebrochen, Time Out erreicht |
| 10 | Messung beendet, Time Out erreicht |
| 255 | Ungueltiger Wert |

<a id="table-tab-12vladen-ladefehler"></a>
### TAB_12VLADEN_LADEFEHLER

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Ladezustand der 12V Batterie erreicht |
| 0x02 | Stromakzeptanz der 12V Batterie zu gering |
| 0x03 | Ladezustand HV-BAtterie zu gering |
| 0x04 | Fehler im Hochvolt-System |
| 0x05 | Komponente defekt (AE, DC/DC) |
| 0x06 | Maximalzeit abgelaufen |
| 0x0E | Fehler unbekannt |

<a id="table-tab-aep-diag-grund-ladeende"></a>
### TAB_AEP_DIAG_GRUND_LADEENDE

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 12V Soll-SOC erreicht / Laden erfolgreich - Forecast nächstes Zyklisches Nachladen möglich |
| 0x01 | 12V Batterie - Stromakzeptanz zu gering - Forecast nächstes Zyklisches Nachladen möglich |
| 0x02 | Energiemangel in HV-Batterie - Forecast nächstes Zyklisches Nachladen möglich |
| 0x03 | Abbruch aufgrund HV-Fehler - Forecast nächstes Zyklisches Nachladen möglich |
| 0x04 | Abbruch aufgrund DCDC-Wandler Ausfall - Forecast nächstes Zyklisches Nachladen möglich |
| 0x05 | Maximalzeit abgelaufen - Forecast nächstes Zyklisches Nachladen möglich |
| 0x06 | (nicht belegt)  - Forecast nächstes Zyklisches Nachladen möglich |
| 0x07 | Unbekannt  - Forecast nächstes Zyklisches Nachladen möglich |
| 0x08 | 12V Soll-SOC erreicht / Laden erfolgreich - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x09 | 12V Batterie - Stromakzeptanz zu gering - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0A | Energiemangel in HV-Batterie - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0B | Abbruch aufgrund HV-Fehler - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0C | Abbruch aufgrund DCDC-Wandler Ausfall - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0D | Maximalzeit abgelaufen - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0E | (nicht belegt) - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0x0F | Unbekannt - Forecast nächstes Zyklisches Nachladen nicht möglich |
| 0xFF | Keine Anforderung |

<a id="table-tab-ansteuerung-luefter-relais"></a>
### TAB_ANSTEUERUNG_LUEFTER_RELAIS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Job noch nicht gestartet |
| 0x01 | Relais ausschalten/öffnen |
| 0x02 | Relais einschalten/schließen |

<a id="table-tab-entlueftungsroutine-status"></a>
### TAB_ENTLUEFTUNGSROUTINE_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht gestartet |
| 0x01 | Routine läuft |
| 0x02 | Routine wurde abgebrochen |
| 0x03 | Routine erfolgreich durchgeführt |
| 0xFF | Wert ungültig |

<a id="table-tab-kaeltemittel-absperrventil-oeffnen-schliessen"></a>
### TAB_KAELTEMITTEL_ABSPERRVENTIL_OEFFNEN_SCHLIESSEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Job inaktiv |
| 0x01 | Job aktiv & Ventil öffnen |
| 0x02 | Job aktiv & Ventil schliessen |

<a id="table-tab-luefter"></a>
### TAB_LUEFTER

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Testeransteuerung inaktiv |
| 0x01 | WMK-Anforderung zu hoch, Job nicht ausführbar |
| 0x02 | Relais wird aktiviert |
| 0x03 | Relais wird deaktiviert |
| 0x04 | kein Relaiszustand ausgewählt |
| 0x05 | Fehler (Kl15, Montagemodus, Relaisfehler) |

<a id="table-tab-st-diag-ewp21"></a>
### TAB_ST_DIAG_EWP21

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK, Kurzschluss gegen Plus, Kurzschluss gegen Masse |
| 0x01 | Reduzierte Drehzahl |
| 0x02 | Trockenlauf |
| 0x03 | Übertemperatur, Blockierung, keine ansprechbare Wasserpumpe |
| 0x04 | Offene Verbindung |

<a id="table-tab-zyknl-grund-ladeende"></a>
### TAB_ZYKNL_GRUND_LADEENDE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 12V Batterie Soll SOC erreicht / Laden erfolgreich |
| 0x01 | 12V Batterie - Stromakzeptanz zu gering |
| 0x02 | Energiemangel im HV-Speicher |
| 0x03 | Abbruch wegen HV-Fehler |
| 0x04 | Abbruch wegen DCDC-Ausfall |
| 0x05 | Maximalzeit abgelaufen |
| 0x06 | (nicht belegt) |
| 0x07 | Unbekannt |

<a id="table-motorudscodierung-ruhestrom"></a>
### _MOTORUDSCODIERUNG_RUHESTROM

Dimensions: 16 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ruhestrom kleiner 80mA, keine Aktion des IBS |
| 1 | Ruhestrom = 80...200mA, keine Aktion da Entladung kleiner 1Ah |
| 2 | Ruhestrom = 200...1000mA, keine Aktion da Entladung kleiner 1Ah |
| 3 | Ruhestrom groesser 1000mA, keine Aktion da Entladung kleiner 1Ah |
| 4 | Ruhestrom kleiner 80mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 5 | Ruhestrom = 80...200mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 6 | Ruhestrom = 200...1000mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 7 | Ruhestrom groesser 1000mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 8 | Ruhestrom kleiner 80mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 9 | Ruhestrom = 80...200mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 10 | Ruhestrom = 200...1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 11 | Ruhestrom groesser 1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 12 | Ruhestrom kleiner 80mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 13 | Ruhestrom = 80...200mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 14 | Ruhestrom = 200...1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 15 | Ruhestrom groesser 1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |

<a id="table-table-status-letzter-batteriewechsel"></a>
### TABLE_STATUS_LETZTER_BATTERIEWECHSEL

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wechsel zulässig |
| 1 | Wechsel unzulässig |

<a id="table-table-status-batteriezustand"></a>
### TABLE_STATUS_BATTERIEZUSTAND

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie pruefen |
| 2 | Batterie nicht i.O. |
| 3 | ungueltig |

<a id="table-table-status-wasserverlust"></a>
### TABLE_STATUS_WASSERVERLUST

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wasserverlust i.O. |
| 1 | Wasserverlust nicht i.O. |

<a id="table-table-status-tiefentladung"></a>
### TABLE_STATUS_TIEFENTLADUNG

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie durch Tiefentladung geschädigt |

<a id="table-table-status-ibs-bze"></a>
### TABLE_STATUS_IBS_BZE

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | BZE nicht aktiv |
| 1 | BZE aktiv |

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | Freigabe (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört) |
| 0x01 | Freigabe erteilt (Challenge-Response erfolgreich) |
| 0x02 | Freigabe abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) |
| 0x03 | nicht definiert |

<a id="table-statfreesktxt"></a>
### STATFREESKTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0xFE | Ablage unbegrenzt |
| 0xFF | ungültig |
| 0xXY | freie Ablagen |

<a id="table-statewsvertxt"></a>
### STATEWSVERTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x01 | Direktschreiben des SecretKey |
| 0x02 | Direktschreiben des SecretKey und DH-Abgleich |
| 0xXY | unbekannt |

<a id="table-ibs-deak"></a>
### IBS_DEAK

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet (ohne Ergebnis) |
| 7 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 8 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und Fehler erkannt |

<a id="table-tab-ae-funkstat-montagemodus"></a>
### TAB_AE_FUNKSTAT_MONTAGEMODUS

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

<a id="table-tab-ae-stat-montagemodus"></a>
### TAB_AE_STAT_MONTAGEMODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Montage-Modus ist inaktiv |
| 0x01 | Montage-Modus ist aktiv |
| 0xFE | nicht definiert |
| 0xFF | ungueltiger Wert |

<a id="table-tab-status-interlock"></a>
### TAB_STATUS_INTERLOCK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bit status of Interlocked is set to Unlock |
| 0x01 | Bit status of Interlocked is set to lock |
