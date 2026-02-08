# dwa_12.prg

- Jobs: [77](#jobs)
- Tables: [63](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CANSINE II |
| ORIGIN | BMW EI-701 Mayer |
| REVISION | 1.007 |
| AUTHOR | BMW EI-701 Mayer, BERTRANDT EI-701 Knorr, Metasystem R&D Cattan |
| COMMENT | N/A |
| PACKAGE | 1.39 |
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
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [STATUS_WECKEN_WACHHALTEN_HISTORIE_LESEN](#job-status-wecken-wachhalten-historie-lesen) - JobHeaderFormat 0x4636 DWA_INFORING_SPEICHER
- [STATUS_DWA_ALARMSPEICHER](#job-status-dwa-alarmspeicher) - JobHeaderFormat 0xDCBE DWA_ALARMSPEICHER
- [STATUS_DWA_PANIKSPEICHER](#job-status-dwa-panikspeicher) - JobHeaderFormat 0x4630 DWA_PANIKSPEICHER
- [STATUS_DWA_DEAKTIVIERUNG_IRS_NG](#job-status-dwa-deaktivierung-irs-ng) - JobHeaderFormat 0x4634 DWA_SENSINSPEICHER
- [STATUS_DWA_MUW_ALARM_LEVELS](#job-status-dwa-muw-alarm-levels) - JobHeaderFormat 0xDCBB DIAG_DID_DCBB_DWA_MUW_ALARMS
- [STATUS_DWA_MUW_FALSE_WAKEUP_LEVELS](#job-status-dwa-muw-false-wakeup-levels) - JobHeaderFormat 0xDCBA DIAG_DID_DCBA_DWA_MUW_FWUP
- [STEUERN_WECKEN_WACHHALTEN_HISTORIE_LOESCHEN](#job-steuern-wecken-wachhalten-historie-loeschen) - JobHeaderFormat 0x4637 DWA_INFORINGSPEICHER_LOESCHEN
- [STEUERN_DWA_ALARMSPEICHER_LOESCHEN](#job-steuern-dwa-alarmspeicher-loeschen) - JobHeaderFormat 0xAA7D DWA_ALARMSPEICHER_LOESCHEN
- [STEUERN_DWA_MUW_ALARM_LEVELS_RESET](#job-steuern-dwa-muw-alarm-levels-reset) - JobHeaderFormat 0x4647 DIAG_DID_4647_RESET_DWA_MUW_ALARMS
- [STEUERN_DWA_MUW_FALSE_WAKEUP_LEVELS_RESET](#job-steuern-dwa-muw-false-wakeup-levels-reset) - JobHeaderFormat 0x4648 DIAG_DID_4648_RESET_DWA_MUW_FWUP
- [STEUERN_DWA_PANIKSPEICHER_LOESCHEN](#job-steuern-dwa-panikspeicher-loeschen) - JobHeaderFormat 0x4631 DWA_PANIKSPEICHER_LOESCHEN
- [STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN](#job-steuern-dwa-deaktivierung-irs-ng-loeschen) - JobHeaderFormat 0x4635 DWA_SENSINSPEICHER_LOESCHEN
- [STEUERN_DWA_MUW_ALARMZAEHLER_LOESCHEN](#job-steuern-dwa-muw-alarmzaehler-loeschen) - JobHeaderFormat 0x464C DIAG_DID_464C_RESET_DWA_MUW_ALARMZAEHLER
- [STEUERN_OBD_UEBERWACHUNG](#job-steuern-obd-ueberwachung) - JobHeaderFormat 0x4653 DIAG_DID_4653_WRITE_OBD_UEBERWACHUNG
- [_STATUS_DWA_DATEOFEM](#job-status-dwa-dateofem) - JobHeaderFormat 0x463F DIAG_DID_463F_READ_DATEOFEM
- [_STATUS_DWA_ICT_TEST_RESULTS](#job-status-dwa-ict-test-results) - JobHeaderFormat 0x4651 DIAG_DID_4651_ICT_TEST_RESULTS
- [_STATUS_DWA_MONITOR](#job-status-dwa-monitor) - JobHeaderFormat 0x4632 DIAG_DID_4632_READ_MONITOR
- [_STATUS_DWA_MUW_ERROR_MEMORY](#job-status-dwa-muw-error-memory) - JobHeaderFormat 0xDCC0 DIAG_DID_DCC0_DWA_MUW_DTCS
- [_STATUS_DWA_MUW_RESET_ANZAHL](#job-status-dwa-muw-reset-anzahl) - JobHeaderFormat 0x464A DIAG_DID_464A_READ_DWA_MUW_RST_NUM
- [_STATUS_DWA_ORDER_NUM](#job-status-dwa-order-num) - JobHeaderFormat 0x4641 DIAG_DID_4641_READ_ORDER_NUM
- [_STATUS_DWA_PIN_TEST_RES](#job-status-dwa-pin-test-res) - JobHeaderFormat 0x4643 DIAG_DID_4643_READ_PIN_TEST_RES
- [_STATUS_DWA_RESET_ANZAHL_LESEN](#job-status-dwa-reset-anzahl-lesen) - Abfrage Resets DWA JobHeaderFormat 0x4638 DIAG_DID_4638_READ_RESET_NUM_DWA
- [_STATUS_DWA_SLEEP](#job-status-dwa-sleep) - JobHeaderFormat 0x4651 DIAG_DID_4651_SLEEP
- [_STATUS_DWA_SQUARES_SN](#job-status-dwa-squares-sn) - JobHeaderFormat 0x463D DIAG_DID_463D_READ_SQUARES_SN
- [_STATUS_DWA_SW_ID](#job-status-dwa-sw-id) - JobHeaderFormat 0x463A DIAG_DID_463A_SW_ID
- [_STATUS_DWA_TESTRESULTS](#job-status-dwa-testresults) - JobHeaderFormat 0x463B DIAG_DID_DCC2_READ_TEST_RESULTS
- [_STEUERN_DWA_CKM_RESET](#job-steuern-dwa-ckm-reset) - JobHeaderFormat 0x4646 DIAG_DID_4646_RESET_CKM
- [_STEUERN_DWA_DATEOFEM](#job-steuern-dwa-dateofem) - JobHeaderFormat 0x4640 DIAG_DID_4640_WRITE_DATEOFEM, writes the date on 5 digits: yymdd
- [_STEUERN_DWA_EXT_BAT](#job-steuern-dwa-ext-bat) - JobHeaderFormat 0x4650 DIAG_DID_4650_SET_EXT_BAT, activates/deactivates the Vbat input
- [_STEUERN_DWA_MONITOR_LOESCHEN](#job-steuern-dwa-monitor-loeschen) - JobHeaderFormat 0x4633 DIAG_DID_4633_MONITOR_RESET
- [_STEUERN_DWA_MUW_ERROR_MEMORY_RESET](#job-steuern-dwa-muw-error-memory-reset) - JobHeaderFormat 0x4649 DIAG_DID_4649_RESET_DWA_MUW_DTCS
- [_STEUERN_DWA_MUW_RESET_ANZAHL_LOESCHEN](#job-steuern-dwa-muw-reset-anzahl-loeschen) - JobHeaderFormat 0x464B DIAG_DID_464B_RESET_DWA_MUW_RST_NUM
- [_STEUERN_DWA_ORDER_NUM](#job-steuern-dwa-order-num) - JobHeaderFormat 0x4642 DIAG_DID_4642_WRITE_ORDER_NUM Change the SERIAL NUMBER of the square the PCB is installed in. It is saved in NVRAM
- [_STEUERN_DWA_RESET_ANZAHL_LOESCHEN](#job-steuern-dwa-reset-anzahl-loeschen) - JobHeaderFormat 0x4639 DIAG_DID_4639_DWA_RESET_NUM_LOESCHEN
- [_STEUERN_DWA_SECONDARY_ST_INHIBIT](#job-steuern-dwa-secondary-st-inhibit) - JobHeaderFormat 0x464F DIAG_DID_464F_SET_SECONDARY_ST_INHIBIT, activates/deactivates piezo secondary ST
- [_STEUERN_DWA_SERIENNUMMER](#job-steuern-dwa-seriennummer) - JobHeaderFormat 0x4645 DIAG_DID_4645_WRITE_SERIAL_NUMBER Change the SERIAL NUMBER of the CANSINE in NVRAM. The serial number shall then be read with job 'seriennummer_lesen' The S.N. is composed of 10 bytes: - the last two digits of year (2 bytes) - e.g. 0x01 0x02 for the year 2012 - two digits for month id (2 bytes) - e.g. 0x00 0x01 for Jan 0x01 0x02 for Dec - two digits for the day (2 bytes) - e.g. 0x03 0x00 for the day 30 - the progressive decimal number (4 bytes) ---&gt; step of 1000, from '0' to '9' ---&gt; step of 0100, from '0' to '9' ---&gt; step of 0010, from '0' to '9' ---&gt; step of 0001, from '0' to '9' Enter each byte separated by semicolon with hex notation (0xNN) example: 0x00 0x08 0x01 0x01 0x02 0x07 0x00 0x00 0x00 0x01 (in the example, semicolons are not shown because of conflicts with the SGBD sintax)
- [_STEUERN_DWA_SOUNDS](#job-steuern-dwa-sounds) - JobHeaderFormat 0x464E DIAG_DID_464E_SET_DWA_SOUNDS, activates/deactivates USA/ECE & buzzers
- [_STEUERN_DWA_SVK_HISTORY](#job-steuern-dwa-svk-history) - JobHeaderFormat 0x464D DIAG_DID_464D_WRITE_DWA_SVK_HISTORY
- [_STEUERN_DWA_TESTRESULTS](#job-steuern-dwa-testresults) - JobHeaderFormat 0x463C DIAG_DID_463C_WRITE_TEST_RESULTS - these results are written in production
- [_STEUERN_DWA_TRIGGER_DTC_STORE](#job-steuern-dwa-trigger-dtc-store) - JobHeaderFormat 0x4652 DIAG_DID_4652_TRIGGER_DTC_STORE, triggers the storing of DTC's in nvram

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
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann 'Information nicht verfuegbar' |
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

<a id="job-cps-lesen"></a>
### CPS_LESEN

Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPS | string | Codierpruefstempel 7-stellig |
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

<a id="job-status-wecken-wachhalten-historie-lesen"></a>
### STATUS_WECKEN_WACHHALTEN_HISTORIE_LESEN

JobHeaderFormat 0x4636 DWA_INFORING_SPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INFORING_ENTRIES_ANZAHL_WERT | unsigned char | Anzahl der Inforingspeichereinträge 0..6 |
| STAT_INFORING_MEMORY_READ_ERR | unsigned char | error code |
| STAT_ERR_CLASS_WERT | unsigned char | Inforing entry class |
| STAT_ERR_CLASS_TEXT | string | Inforing entry class |
| STAT_ERR_URSACHE_1_WERT | unsigned long | Internal CAN/internal wake reasons at entry storage |
| STAT_ERR_URSACHE_2_WERT | unsigned long | Internal CAN/internal wake reasons at sleep prevention storage - 5min |
| STAT_ERR_URSACHE_3_WERT | unsigned long | Internal CAN/internal wake reasons at sleep prevention storage - 10min |
| STAT_ERR_URSACHE_4_WERT | unsigned long | Internal CAN/internal wake reasons at sleep prevention storage - 15min |
| STAT_ERR_KM_STAND_WERT | unsigned long | Kilometers at entry storage |
| STAT_ERR_RELATIVE_ZEIT_WERT | unsigned long | Relative time at entry storage |
| STAT_ERR_RELATIVE_ZEIT_EINH | string | Relativ Zeit Einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-alarmspeicher"></a>
### STATUS_DWA_ALARMSPEICHER

JobHeaderFormat 0xDCBE DWA_ALARMSPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALARM_ANZAHL_WERT | unsigned char | Anzahl der Alarmspeichereinträge 0..10 |
| STAT_ALARM_ANZAHL_EINH | string | Anzahl der Alarmspeichereinträge 0..10 |
| STAT_ALARM_MEMORY_READ_ERR | unsigned char | error code, only if an error occurred during job execution |
| STAT_ALARM_ID_WERT | unsigned char | Alarm ID |
| STAT_ALARM_ID_TEXT | string | Alarm ID |
| STAT_FENSTERPOS_FAT_WERT | unsigned char | Fensterposition FAT |
| STAT_FENSTERPOS_BFT_WERT | unsigned char | Status Fensterposition BFT |
| STAT_FENSTERPOS_FATH_WERT | unsigned char | Status Fensterposition FATH |
| STAT_FENSTERPOS_BFTH_WERT | unsigned char | Status Fensterposition BFTH |
| STAT_FENSTERPOS_HCKS_WERT | unsigned char | Status Fensterposition HCKS |
| STAT_SHDPOS_SHD_WERT | unsigned char | Status Position SHD |
| STAT_SHDPOS_SHD_NEIGUNG_WERT | unsigned char | Status Position SHD-Neigung |
| STAT_FENSTER_SHD_POS_EINH | string | Status Position SHD |
| STAT_STANDLUEFTEN_WERT | unsigned char | Status Standlüftung |
| STAT_STANDLUEFTEN_TEXT | string | Status Standlüftung |
| STAT_GEBLAESE_WERT | unsigned char | Status Geblaese |
| STAT_GEBLAESE_TEXT | string | Status Geblaese |
| STAT_STANDHEIZUNG_WERT | unsigned char | Status Standheizung |
| STAT_STANDHEIZUNG_TEXT | string | Status Standheizung |
| STAT_INTERNTEMP_WERT | char | INNENTEMPERATUR -40°C / +85°C |
| STAT_AUSSENTEMP_WERT | char | AUSSENTEMP -40°C / +85°C |
| STAT_TEMPERATUR_EINH | string | Temperature Einheit |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| STAT_KILOMETER_WERT | unsigned long | Kilometerstand |
| STAT_ALARMS_NUMBER_IN_ARMING_CYCLE | unsigned char | Alarmhistorie, alarmnummer |
| STAT_FAHRERTUER_WERT | unsigned char | 0:closed 1:open |
| STAT_BEIFAHRERTUER_WERT | unsigned char | 0:closed 1:open |
| STAT_FAHRERTUER_HINTEN_WERT | unsigned char | 0:closed 1:open |
| STAT_BEIFAHRERT_HINTEN_WERT | unsigned char | 0:closed 1:open |
| STAT_HECKKLAPPE_WERT | unsigned char | 0:closed 1:open |
| STAT_MOTORHAUBE_WERT | unsigned char | 0:closed 1:open |
| STAT_HECKSCHEIBE_WERT | unsigned char | 0:closed 1:open |
| STAT_TUEREN_TEXT | string | 0:closed 1:open |
| STAT_SINEVOLTAGE | unsigned char | Spannungsueberwachung |
| STAT_SINEVOLTAGE_EINH | string | Spannungsueberwachung |
| STAT_POS_CABRIO_DACH_WERT | unsigned char | Position Cabrio Dach: 0:komplett geschlossen und verriegelt 1:Zwischenstellung 2:Komplett geoffnet und verriegelt 3:beladeposition 4:Hardtop aufgesetzt 5:Komplett geschlossen |
| STAT_POS_CABRIO_DACH_TEXT | string | einheit |
| STAT_OP_CABRIO_DACH_WERT | unsigned char | Operation Cabrio Dach: 0:keine Bedienung 1:oeffnen 2:schliessen 3:beladenposition_anfahren 15:Signal ungueltig |
| STAT_OP_CABRIO_DACH_TEXT | string | einheit |
| STAT_FAHRERF_DRIVE_WERT | unsigned char | 0:gestoppt 1:Bewegung |
| STAT_FAHRERF_DRIVE_TEXT | string | einheit |
| STAT_BEIFAHRERF_DRIVE_WERT | unsigned char | 0:gestoppt 1:Bewegung |
| STAT_BEIFAHRERF_DRIVE_TEXT | string | einheit |
| STAT_FAHRERF_HINTEN_DRV_WERT | unsigned char | 0:gestoppt 1:Bewegung |
| STAT_FAHRERF_HINTEN_DRV_TEXT | string | einheit |
| STAT_BEIFAHRERF_HINT_DRV_WERT | unsigned char | 0:gestoppt 1:Bewegung |
| STAT_BEIFAHRERF_HINT_DRV_TEXT | string | einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-panikspeicher"></a>
### STATUS_DWA_PANIKSPEICHER

JobHeaderFormat 0x4630 DWA_PANIKSPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PANIK_ANZAHL_WERT | unsigned char | Anzahl der Panikspeichereinträge 0..10 |
| STAT_PANIK_SPEICHER_LESEN_FEHLER | unsigned char | Fehler Nummer, nur wenn Fehler im Job Durchführung |
| STAT_JAHRE_WERT | unsigned int | Jahre |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-deaktivierung-irs-ng"></a>
### STATUS_DWA_DEAKTIVIERUNG_IRS_NG

JobHeaderFormat 0x4634 DWA_SENSINSPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IRS_NG_DEAKTIVIERUNG_ANZAHL_WERT | unsigned char | Anzahl der Sensor Inhibit speichereinträge 0..10 |
| STAT_IRS_NG_DEAKTIV_SPEICHER_LESEN_FEHLER | unsigned char | Fehler Nummer, nur wenn Fehler im Job Durchführung |
| STAT_JAHRE_WERT | unsigned int | Jahre |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-muw-alarm-levels"></a>
### STATUS_DWA_MUW_ALARM_LEVELS

JobHeaderFormat 0xDCBB DIAG_DID_DCBB_DWA_MUW_ALARMS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_KOMM_FEHLER | string | muw vr kommunikation fehler kode |
| STAT_MUW_VR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VR_ALARM_LEVEL_1_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 1 |
| STAT_MUW_VR_ALARM_LEVEL_1_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 1 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_2_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 2 |
| STAT_MUW_VR_ALARM_LEVEL_2_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 2 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_3_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 3 |
| STAT_MUW_VR_ALARM_LEVEL_3_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 3 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_4_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 4 |
| STAT_MUW_VR_ALARM_LEVEL_4_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 4 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_5_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 5 |
| STAT_MUW_VR_ALARM_LEVEL_5_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 5 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_6_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 6 |
| STAT_MUW_VR_ALARM_LEVEL_6_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 6 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_7_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 7 |
| STAT_MUW_VR_ALARM_LEVEL_7_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 7 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_8_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 8 |
| STAT_MUW_VR_ALARM_LEVEL_8_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 8 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_9_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 9 |
| STAT_MUW_VR_ALARM_LEVEL_9_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 9 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_VR_ALARM_LEVEL_10_WERT | unsigned char | AlarmsWert am MUW vorne rechts bei Alarm 10 |
| STAT_MUW_VR_ALARM_LEVEL_10_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW vorne rechts bei Alarm 10 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HR_KOMM_FEHLER | string | muw hr kommunikation fehler kode |
| STAT_MUW_HR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HR_ALARM_LEVEL_1_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 1 |
| STAT_MUW_HR_ALARM_LEVEL_1_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 1 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_2_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 2 |
| STAT_MUW_HR_ALARM_LEVEL_2_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 2 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_3_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 3 |
| STAT_MUW_HR_ALARM_LEVEL_3_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 3 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_4_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 4 |
| STAT_MUW_HR_ALARM_LEVEL_4_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 4 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_5_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 5 |
| STAT_MUW_HR_ALARM_LEVEL_5_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 5 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_6_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 6 |
| STAT_MUW_HR_ALARM_LEVEL_6_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 6 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_7_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 7 |
| STAT_MUW_HR_ALARM_LEVEL_7_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 7 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_8_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 8 |
| STAT_MUW_HR_ALARM_LEVEL_8_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 8 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_9_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 9 |
| STAT_MUW_HR_ALARM_LEVEL_9_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 9 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HR_ALARM_LEVEL_10_WERT | unsigned char | AlarmsWert am MUW hinten rechts bei Alarm 10 |
| STAT_MUW_HR_ALARM_LEVEL_10_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten rechts bei Alarm 10 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HL_KOMM_FEHLER | string | muw hl kommunikation fehler kode |
| STAT_MUW_HL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HL_ALARM_LEVEL_1_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 1 |
| STAT_MUW_HL_ALARM_LEVEL_1_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten links bei Alarm 1 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_2_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 2 |
| STAT_MUW_HL_ALARM_LEVEL_2_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten links bei Alarm 2 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_3_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 3 |
| STAT_MUW_HL_ALARM_LEVEL_3_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten links bei Alarm 3 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_4_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 4 |
| STAT_MUW_HL_ALARM_LEVEL_4_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten links bei Alarm 4 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_5_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 5 |
| STAT_MUW_HL_ALARM_LEVEL_5_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten links bei Alarm 5 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_6_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 6 |
| STAT_MUW_HL_ALARM_LEVEL_6_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten links bei Alarm 6 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_7_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 7 |
| STAT_MUW_HL_ALARM_LEVEL_7_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten links bei Alarm 7 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_8_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 8 |
| STAT_MUW_HL_ALARM_LEVEL_8_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten links bei Alarm 8 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_9_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 9 |
| STAT_MUW_HL_ALARM_LEVEL_9_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten links bei Alarm 9 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HL_ALARM_LEVEL_10_WERT | unsigned char | AlarmsWert am MUW hinten links bei Alarm 10 |
| STAT_MUW_HL_ALARM_LEVEL_10_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten links bei Alarm 10 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_VL_KOMM_FEHLER | string | muw vl kommunikation fehler kode |
| STAT_MUW_VL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VL_ALARM_LEVEL_1_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 1 |
| STAT_MUW_VL_ALARM_LEVEL_1_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW vorne links bei Alarm 1 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_2_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 2 |
| STAT_MUW_VL_ALARM_LEVEL_2_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW vorne links bei Alarm 2 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_3_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 3 |
| STAT_MUW_VL_ALARM_LEVEL_3_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW vorne links bei Alarm 3 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_4_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 4 |
| STAT_MUW_VL_ALARM_LEVEL_4_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW vorne links bei Alarm 4 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_5_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 5 |
| STAT_MUW_VL_ALARM_LEVEL_5_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW vorne links bei Alarm 5 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_6_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 6 |
| STAT_MUW_VL_ALARM_LEVEL_6_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW vorne links bei Alarm 6 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_7_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 7 |
| STAT_MUW_VL_ALARM_LEVEL_7_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW vorne links bei Alarm 7 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_8_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 8 |
| STAT_MUW_VL_ALARM_LEVEL_8_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW vorne links bei Alarm 8 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_9_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 9 |
| STAT_MUW_VL_ALARM_LEVEL_9_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW vorne links bei Alarm 9 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_VL_ALARM_LEVEL_10_WERT | unsigned char | AlarmsWert am MUW vorne links bei Alarm 10 |
| STAT_MUW_VL_ALARM_LEVEL_10_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW vorne links bei Alarm 10 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HI_KOMM_FEHLER | string | muw hi kommunikation fehler kode |
| STAT_MUW_HI_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HI_ALARM_LEVEL_1_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 1 |
| STAT_MUW_HI_ALARM_LEVEL_1_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 1 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_2_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 2 |
| STAT_MUW_HI_ALARM_LEVEL_2_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 2 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_3_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 3 |
| STAT_MUW_HI_ALARM_LEVEL_3_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 3 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_4_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 4 |
| STAT_MUW_HI_ALARM_LEVEL_4_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 4 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_5_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 5 |
| STAT_MUW_HI_ALARM_LEVEL_5_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 5 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_6_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 6 |
| STAT_MUW_HI_ALARM_LEVEL_6_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 6 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_7_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 7 |
| STAT_MUW_HI_ALARM_LEVEL_7_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 7 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_8_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 8 |
| STAT_MUW_HI_ALARM_LEVEL_8_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 8 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_9_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 9 |
| STAT_MUW_HI_ALARM_LEVEL_9_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 9 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HI_ALARM_LEVEL_10_WERT | unsigned char | AlarmsWert am MUW hinten zentral bei Alarm 10 |
| STAT_MUW_HI_ALARM_LEVEL_10_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten zentral bei Alarm 10 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_10_EINH | string | °C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-muw-false-wakeup-levels"></a>
### STATUS_DWA_MUW_FALSE_WAKEUP_LEVELS

JobHeaderFormat 0xDCBA DIAG_DID_DCBA_DWA_MUW_FWUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_KOMM_FEHLER | string | muw vr kommunikation fehler kode |
| STAT_MUW_VR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_1_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 1 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_1_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 1 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_2_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 2 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_2_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 2 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_3_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 3 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_3_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 3 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_4_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 4 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_4_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 4 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_5_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 5 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_5_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 5 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_6_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 6 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_6_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 6 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_7_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 7 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_7_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 7 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_8_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 8 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_8_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 8 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_9_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 9 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_9_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 9 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_10_WERT | unsigned char | FalseWakeupWert am MUW vorne rechts bei False Wakeup 10 |
| STAT_MUW_VR_FALSE_WAKEUP_LEVEL_10_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW vorne rechts bei False Wakeup 10 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HR_KOMM_FEHLER | string | muw hr kommunikation fehler kode |
| STAT_MUW_HR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_1_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 1 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_1_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 1 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_2_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 2 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_2_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 2 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_3_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 3 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_3_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 3 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_4_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 4 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_4_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 4 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_5_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 5 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_5_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 5 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_6_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 6 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_6_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 6 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_7_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 7 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_7_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 7 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_8_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 8 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_8_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 8 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_9_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 9 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_9_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 9 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_10_WERT | unsigned char | FalseWakeupWert am MUW hinten rechts bei False Wakeup 10 |
| STAT_MUW_HR_FALSE_WAKEUP_LEVEL_10_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten rechts bei False Wakeup 10 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HL_KOMM_FEHLER | string | muw hl kommunikation fehler kode |
| STAT_MUW_HL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_1_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 1 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_1_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 1 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_2_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 2 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_2_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 2 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_3_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 3 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_3_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 3 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_4_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 4 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_4_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 4 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_5_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 5 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_5_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 5 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_6_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 6 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_6_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 6 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_7_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 7 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_7_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 7 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_8_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 8 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_8_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 8 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_9_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 9 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_9_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 9 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_10_WERT | unsigned char | FalseWakeupWert am MUW hinten links bei False Wakeup 10 |
| STAT_MUW_HL_FALSE_WAKEUP_LEVEL_10_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten links bei False Wakeup 10 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_VL_KOMM_FEHLER | string | muw vl kommunikation fehler kode |
| STAT_MUW_VL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_1_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 1 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_1_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 1 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_2_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 2 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_2_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 2 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_3_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 3 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_3_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 3 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_4_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 4 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_4_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 4 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_5_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 5 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_5_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 5 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_6_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 6 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_6_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 6 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_7_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 7 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_7_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 7 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_8_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 8 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_8_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 8 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_9_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 9 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_9_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 9 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_10_WERT | unsigned char | FalseWakeupWert am MUW vorne links bei False Wakeup 10 |
| STAT_MUW_VL_FALSE_WAKEUP_LEVEL_10_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW vorne links bei False Wakeup 10 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_10_EINH | string | °C |
| STAT_MUW_HI_KOMM_FEHLER | string | muw hi kommunikation fehler kode |
| STAT_MUW_HI_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_1_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 1 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_1_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_1_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 1 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_1_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_2_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 2 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_2_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_2_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 2 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_2_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_3_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 3 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_3_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_3_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 3 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_3_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_4_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 4 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_4_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_4_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 4 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_4_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_5_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 5 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_5_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_5_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 5 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_5_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_6_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 6 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_6_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_6_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 6 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_6_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_7_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 7 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_7_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_7_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 7 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_7_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_8_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 8 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_8_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_8_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 8 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_8_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_9_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 9 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_9_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_9_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 9 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_9_EINH | string | °C |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_10_WERT | unsigned char | FalseWakeupWert am MUW hinten zentral bei False Wakeup 10 |
| STAT_MUW_HI_FALSE_WAKEUP_LEVEL_10_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_10_WERT | int | Temperaturswert am MUW hinten zentral bei False Wakeup 10 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_10_EINH | string | °C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-wecken-wachhalten-historie-loeschen"></a>
### STEUERN_WECKEN_WACHHALTEN_HISTORIE_LOESCHEN

JobHeaderFormat 0x4637 DWA_INFORINGSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-alarmspeicher-loeschen"></a>
### STEUERN_DWA_ALARMSPEICHER_LOESCHEN

JobHeaderFormat 0xAA7D DWA_ALARMSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-muw-alarm-levels-reset"></a>
### STEUERN_DWA_MUW_ALARM_LEVELS_RESET

JobHeaderFormat 0x4647 DIAG_DID_4647_RESET_DWA_MUW_ALARMS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_RESET_KOMM_FEHLER | string | MUW vorne rechts kommunikation fehler kode |
| STAT_MUW_VR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HR_RESET_KOMM_FEHLER | string | MUW hinten rechts kommunikation fehler kode |
| STAT_MUW_HR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HL_RESET_KOMM_FEHLER | string | MUW hinten links kommunikation fehler kode |
| STAT_MUW_HL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_VL_RESET_KOMM_FEHLER | string | MUW vorne links kommunikation fehler kode |
| STAT_MUW_VL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HI_RESET_KOMM_FEHLER | string | MUW hinten zentral kommunikation fehler kode |
| STAT_MUW_HI_RESET_KOMM_FEHLER_EINH | string | einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-muw-false-wakeup-levels-reset"></a>
### STEUERN_DWA_MUW_FALSE_WAKEUP_LEVELS_RESET

JobHeaderFormat 0x4648 DIAG_DID_4648_RESET_DWA_MUW_FWUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_RESET_KOMM_FEHLER | string | MUW vorne rechts kommunikation fehler kode |
| STAT_MUW_VR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HR_RESET_KOMM_FEHLER | string | MUW hinten rechts kommunikation fehler kode |
| STAT_MUW_HR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HL_RESET_KOMM_FEHLER | string | MUW hinten links kommunikation fehler kode |
| STAT_MUW_HL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_VL_RESET_KOMM_FEHLER | string | MUW vorne links kommunikation fehler kode |
| STAT_MUW_VL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HI_RESET_KOMM_FEHLER | string | MUW hinten zentral kommunikation fehler kode |
| STAT_MUW_HI_RESET_KOMM_FEHLER_EINH | string | einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-panikspeicher-loeschen"></a>
### STEUERN_DWA_PANIKSPEICHER_LOESCHEN

JobHeaderFormat 0x4631 DWA_PANIKSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-deaktivierung-irs-ng-loeschen"></a>
### STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN

JobHeaderFormat 0x4635 DWA_SENSINSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-muw-alarmzaehler-loeschen"></a>
### STEUERN_DWA_MUW_ALARMZAEHLER_LOESCHEN

JobHeaderFormat 0x464C DIAG_DID_464C_RESET_DWA_MUW_ALARMZAEHLER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_ALARMZAEHLER_LOESCHEN_KOMM_FEHLER | string | MUW vorne rechts kommunikation fehler kode |
| STAT_MUW_HR_ALARMZAEHLER_LOESCHEN_KOMM_FEHLER | string | MUW hinten rechts kommunikation fehler kode |
| STAT_MUW_HL_ALARMZAEHLER_LOESCHEN_KOMM_FEHLER | string | MUW hinten links kommunikation fehler kode |
| STAT_MUW_VL_ALARMZAEHLER_LOESCHEN_KOMM_FEHLER | string | MUW vorne links kommunikation fehler kode |
| STAT_MUW_HI_ALARMZAEHLER_LOESCHEN_KOMM_FEHLER | string | MUW hinten zentral kommunikation fehler kode |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-obd-ueberwachung"></a>
### STEUERN_OBD_UEBERWACHUNG

JobHeaderFormat 0x4653 DIAG_DID_4653_WRITE_OBD_UEBERWACHUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OBD_UEBERWACHUNG_ENABLE | unsigned char | '0' switch off the OBD ueberwachung, '1' uses coding to control OBD ueberwachung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-dateofem"></a>
### _STATUS_DWA_DATEOFEM

JobHeaderFormat 0x463F DIAG_DID_463F_READ_DATEOFEM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_DATE_OF_ECU_MANUFACTURING_BYTE0_WERT | unsigned char | Date of ECU manufacturing byte 0 |
| STAT_DWA_DATE_OF_ECU_MANUFACTURING_BYTE1_WERT | unsigned char | Date of ECU manufacturing byte 1 |
| STAT_DWA_DATE_OF_ECU_MANUFACTURING_BYTE2_WERT | unsigned char | Date of ECU manufacturing byte 2 |
| STAT_DWA_DATE_OF_ECU_MANUFACTURING_BYTE3_WERT | unsigned char | Date of ECU manufacturing byte 3 |
| STAT_DWA_DATE_OF_ECU_MANUFACTURING_BYTE4_WERT | unsigned char | Date of ECU manufacturing byte 4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-ict-test-results"></a>
### _STATUS_DWA_ICT_TEST_RESULTS

JobHeaderFormat 0x4651 DIAG_DID_4651_ICT_TEST_RESULTS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_ICT_TEST_RESULT_1_WERT | unsigned char | Ict Test Result #1 |
| STAT_DWA_ICT_TEST_RESULT_2_WERT | unsigned char | Ict Test Result #2 |
| STAT_DWA_ICT_TEST_RESULT_3_WERT | unsigned char | Ict Test Result #3 |
| STAT_DWA_ICT_TEST_RESULT_4_WERT | unsigned char | Ict Test Result #4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-monitor"></a>
### _STATUS_DWA_MONITOR

JobHeaderFormat 0x4632 DIAG_DID_4632_READ_MONITOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_COUNTER2_NUM | unsigned long | DWA Task2 activations number |
| STAT_DWA_COUNTER10_NUM | unsigned long | DWA Task10 activations number |
| STAT_DWA_COUNTER_MEM_NUM | unsigned long | DWA TaskMem activations number |
| STAT_DWA_COUNTER_WDM_NUM | unsigned long | DWA TaskWdm activations number |
| STAT_DWA_COUNTER_EINH | string | einheit |
| STAT_DWA_TILT_ST_REF_X | int | Tilt sensor selftest X base mgs |
| STAT_DWA_TILT_ST_OUT_X | int | Tilt sensor selftest X output mgs |
| STAT_DWA_TILT_ST_DELTA_X | int | Tilt sensor selftest X delta mgs |
| STAT_DWA_TILT_ST_REF_Y | int | Tilt sensor selftest Y base mgs |
| STAT_DWA_TILT_ST_OUT_Y | int | Tilt sensor selftest Y output mgs |
| STAT_DWA_TILT_ST_DELTA_Y | int | Tilt sensor selftest Y delta mgs |
| STAT_DWA_TILT_ST_THR_MIN_XY | int | Tilt sensor selftest XY min threshold mgs - if(value &lt; min) -&gt; error |
| STAT_DWA_TILT_ST_THR_MAX_XY | int | Tilt sensor selftest XY max threshold mgs - if(value &gt; max) -&gt; error |
| STAT_DWA_TILT_ST_REF_Z | int | Tilt sensor selftest Z base mgs |
| STAT_DWA_TILT_ST_OUT_Z | int | Tilt sensor selftest Z output mgs |
| STAT_DWA_TILT_ST_DELTA_Z | int | Tilt sensor selftest Z delta mgs |
| STAT_DWA_TILT_ST_THR_MIN_Z | int | Tilt sensor selftest Z min threshold mgs - if(value &gt; min) -&gt; error (NEGATIVE VALUES) |
| STAT_DWA_TILT_ST_THR_MAX_Z | int | Tilt sensor selftest Z max threshold mgs - if(value &lt; max) -&gt; error (NEGATIVE VALUES) |
| STAT_DWA_LDSPK_VPP_AI_LAST_OPEN_RES | unsigned char | Last open circuit 8bit value read during piezo Vpp Ai selftest (dyn or static) in ADC counts (0xFE means invalid) |
| STAT_DWA_LDSPK_VPP_AI_LAST_SHORT_RES | unsigned char | Last short circuit 8bit value read during piezo Vpp Ai selftest (dyn or static) in ADC counts (0xFE means invalid) |
| STAT_DWA_LDSPK_PD_CUR_AI_LAST_OPEN_RES | unsigned char | Last open circuit 8bit value read during primary Pd Cur Ai selftest (dyn or static) in ADC counts (0xFE means invalid) |
| STAT_DWA_LDSPK_PD_CUR_AI_LAST_SHORT_RES | unsigned char | Last open circuit 8bit value read during primary Pd Cur Ai selftest (dyn or static) in ADC counts (0xFE means invalid) |
| STAT_DWA_LED_AI_LAST_OPEN_RES | unsigned int | Last open circuit 10bit value read during Led Ai selftest (dyn or static) in ADC counts (0xFFFE means invalid) |
| STAT_DWA_LED_AI_LAST_SHORT_RES | unsigned int | Last open circuit 10bit value read during Led Ai selftest (dyn or static) in ADC counts (0xFFFE means invalid) |
| STAT_DWA_VBAT_TOO_LOW_AT_ARM_RES | unsigned char | Last Vbat too low at arming value in multiples of 100mV - 0xFF means invalid |
| STAT_DWA_VBAT_TOO_LOW_AT_ST_RES | unsigned char | Last Vbat too low at selftest value in multiples of 100mV - 0xFF means invalid |
| STAT_DWA_VBAT_TOO_HIGH_AT_ARM_RES | unsigned char | Last Vbat too high at arming value in multiples of 100mV - 0x00 means invalid |
| STAT_DWA_INT_BAT_TOO_LOW_AT_ARM_RES | unsigned char | Last Internal Battery too low at arming value (8bit) - 0xFF means invalid |
| STAT_DWA_INT_BAT_TOO_HIGH_AT_ARM_RES | unsigned char | Last Internal Battery too high at arming value (8bit) - 0x00 means invalid |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-muw-error-memory"></a>
### _STATUS_DWA_MUW_ERROR_MEMORY

JobHeaderFormat 0xDCC0 DIAG_DID_DCC0_DWA_MUW_DTCS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_KOMM_FEHLER | string | muw vr kommunikation fehler kode |
| STAT_MUW_VR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VR_COUNT_DTC_01_WERT | unsigned char | DTC count am MUW vorne rechts 01 |
| STAT_MUW_VR_COUNT_DTC_01_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_01_WERT | int | Temperaturswert am MUW vorne rechts 01 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_01_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_02_WERT | unsigned char | DTC count am MUW vorne rechts 02 |
| STAT_MUW_VR_COUNT_DTC_02_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_02_WERT | int | Temperaturswert am MUW vorne rechts 02 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_02_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_03_WERT | unsigned char | DTC count am MUW vorne rechts 03 |
| STAT_MUW_VR_COUNT_DTC_03_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_03_WERT | int | Temperaturswert am MUW vorne rechts 03 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_03_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_04_WERT | unsigned char | DTC count am MUW vorne rechts 04 |
| STAT_MUW_VR_COUNT_DTC_04_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_04_WERT | int | Temperaturswert am MUW vorne rechts 04 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_04_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_05_WERT | unsigned char | DTC count am MUW vorne rechts 05 |
| STAT_MUW_VR_COUNT_DTC_05_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_05_WERT | int | Temperaturswert am MUW vorne rechts 05 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_05_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_06_WERT | unsigned char | DTC count am MUW vorne rechts 06 |
| STAT_MUW_VR_COUNT_DTC_06_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_06_WERT | int | Temperaturswert am MUW vorne rechts 06 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_06_EINH | string | °C |
| STAT_MUW_VR_COUNT_DTC_07_WERT | unsigned char | DTC count am MUW vorne rechts 07 |
| STAT_MUW_VR_COUNT_DTC_07_EINH | string | - |
| STAT_MUW_VR_TEMPERATURE_LEVEL_07_WERT | int | Temperaturswert am MUW vorne rechts 07 |
| STAT_MUW_VR_TEMPERATURE_LEVEL_07_EINH | string | °C |
| STAT_MUW_HR_KOMM_FEHLER | string | muw hr kommunikation fehler kode |
| STAT_MUW_HR_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HR_COUNT_DTC_01_WERT | unsigned char | DTC count am MUW hinten rechts 01 |
| STAT_MUW_HR_COUNT_DTC_01_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_01_WERT | int | Temperaturswert am MUW hinten rechts 01 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_01_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_02_WERT | unsigned char | DTC count am MUW hinten rechts 02 |
| STAT_MUW_HR_COUNT_DTC_02_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_02_WERT | int | Temperaturswert am MUW hinten rechts 02 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_02_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_03_WERT | unsigned char | DTC count am MUW hinten rechts 03 |
| STAT_MUW_HR_COUNT_DTC_03_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_03_WERT | int | Temperaturswert am MUW hinten rechts 03 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_03_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_04_WERT | unsigned char | DTC count am MUW hinten rechts 04 |
| STAT_MUW_HR_COUNT_DTC_04_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_04_WERT | int | Temperaturswert am MUW hinten rechts 04 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_04_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_05_WERT | unsigned char | DTC count am MUW hinten rechts 05 |
| STAT_MUW_HR_COUNT_DTC_05_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_05_WERT | int | Temperaturswert am MUW hinten rechts 05 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_05_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_06_WERT | unsigned char | DTC count am MUW hinten rechts 06 |
| STAT_MUW_HR_COUNT_DTC_06_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_06_WERT | int | Temperaturswert am MUW hinten rechts 06 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_06_EINH | string | °C |
| STAT_MUW_HR_COUNT_DTC_07_WERT | unsigned char | DTC count am MUW hinten rechts 07 |
| STAT_MUW_HR_COUNT_DTC_07_EINH | string | - |
| STAT_MUW_HR_TEMPERATURE_LEVEL_07_WERT | int | Temperaturswert am MUW hinten rechts 07 |
| STAT_MUW_HR_TEMPERATURE_LEVEL_07_EINH | string | °C |
| STAT_MUW_HL_KOMM_FEHLER | string | muw hl kommunikation fehler kode |
| STAT_MUW_HL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HL_COUNT_DTC_01_WERT | unsigned char | DTC count am MUW hinten links 01 |
| STAT_MUW_HL_COUNT_DTC_01_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_01_WERT | int | Temperaturswert am MUW hinten links 01 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_01_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_02_WERT | unsigned char | DTC count am MUW hinten links 02 |
| STAT_MUW_HL_COUNT_DTC_02_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_02_WERT | int | Temperaturswert am MUW hinten links 02 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_02_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_03_WERT | unsigned char | DTC count am MUW hinten links 03 |
| STAT_MUW_HL_COUNT_DTC_03_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_03_WERT | int | Temperaturswert am MUW hinten links 03 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_03_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_04_WERT | unsigned char | DTC count am MUW hinten links 04 |
| STAT_MUW_HL_COUNT_DTC_04_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_04_WERT | int | Temperaturswert am MUW hinten links 04 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_04_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_05_WERT | unsigned char | DTC count am MUW hinten links 05 |
| STAT_MUW_HL_COUNT_DTC_05_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_05_WERT | int | Temperaturswert am MUW hinten links 05 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_05_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_06_WERT | unsigned char | DTC count am MUW hinten links 06 |
| STAT_MUW_HL_COUNT_DTC_06_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_06_WERT | int | Temperaturswert am MUW hinten links 06 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_06_EINH | string | °C |
| STAT_MUW_HL_COUNT_DTC_07_WERT | unsigned char | DTC count am MUW hinten links 07 |
| STAT_MUW_HL_COUNT_DTC_07_EINH | string | - |
| STAT_MUW_HL_TEMPERATURE_LEVEL_07_WERT | int | Temperaturswert am MUW hinten links 07 |
| STAT_MUW_HL_TEMPERATURE_LEVEL_07_EINH | string | °C |
| STAT_MUW_VL_KOMM_FEHLER | string | muw vl kommunikation fehler kode |
| STAT_MUW_VL_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_VL_COUNT_DTC_01_WERT | unsigned char | DTC count am MUW vorne links 01 |
| STAT_MUW_VL_COUNT_DTC_01_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_01_WERT | int | Temperaturswert am MUW vorne links 01 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_01_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_02_WERT | unsigned char | DTC count am MUW vorne links 02 |
| STAT_MUW_VL_COUNT_DTC_02_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_02_WERT | int | Temperaturswert am MUW vorne links 02 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_02_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_03_WERT | unsigned char | DTC count am MUW vorne links 03 |
| STAT_MUW_VL_COUNT_DTC_03_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_03_WERT | int | Temperaturswert am MUW vorne links 03 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_03_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_04_WERT | unsigned char | DTC count am MUW vorne links 04 |
| STAT_MUW_VL_COUNT_DTC_04_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_04_WERT | int | Temperaturswert am MUW vorne links 04 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_04_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_05_WERT | unsigned char | DTC count am MUW vorne links 05 |
| STAT_MUW_VL_COUNT_DTC_05_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_05_WERT | int | Temperaturswert am MUW vorne links 05 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_05_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_06_WERT | unsigned char | DTC count am MUW vorne links 06 |
| STAT_MUW_VL_COUNT_DTC_06_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_06_WERT | int | Temperaturswert am MUW vorne links 06 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_06_EINH | string | °C |
| STAT_MUW_VL_COUNT_DTC_07_WERT | unsigned char | DTC count am MUW vorne links 07 |
| STAT_MUW_VL_COUNT_DTC_07_EINH | string | - |
| STAT_MUW_VL_TEMPERATURE_LEVEL_07_WERT | int | Temperaturswert am MUW vorne links 07 |
| STAT_MUW_VL_TEMPERATURE_LEVEL_07_EINH | string | °C |
| STAT_MUW_HI_KOMM_FEHLER | string | muw hi kommunikation fehler kode |
| STAT_MUW_HI_KOMM_FEHLER_EINH | string | - |
| STAT_MUW_HI_COUNT_DTC_01_WERT | unsigned char | DTC count am MUW hinten zentral 01 |
| STAT_MUW_HI_COUNT_DTC_01_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_01_WERT | int | Temperaturswert am MUW hinten zentral 01 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_01_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_02_WERT | unsigned char | DTC count am MUW hinten zentral 02 |
| STAT_MUW_HI_COUNT_DTC_02_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_02_WERT | int | Temperaturswert am MUW hinten zentral 02 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_02_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_03_WERT | unsigned char | DTC count am MUW hinten zentral 03 |
| STAT_MUW_HI_COUNT_DTC_03_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_03_WERT | int | Temperaturswert am MUW hinten zentral 03 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_03_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_04_WERT | unsigned char | DTC count am MUW hinten zentral 04 |
| STAT_MUW_HI_COUNT_DTC_04_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_04_WERT | int | Temperaturswert am MUW hinten zentral 04 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_04_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_05_WERT | unsigned char | DTC count am MUW hinten zentral 05 |
| STAT_MUW_HI_COUNT_DTC_05_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_05_WERT | int | Temperaturswert am MUW hinten zentral 05 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_05_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_06_WERT | unsigned char | DTC count am MUW hinten zentral 06 |
| STAT_MUW_HI_COUNT_DTC_06_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_06_WERT | int | Temperaturswert am MUW hinten zentral 06 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_06_EINH | string | °C |
| STAT_MUW_HI_COUNT_DTC_07_WERT | unsigned char | DTC count am MUW hinten zentral 07 |
| STAT_MUW_HI_COUNT_DTC_07_EINH | string | - |
| STAT_MUW_HI_TEMPERATURE_LEVEL_07_WERT | int | Temperaturswert am MUW hinten zentral 07 |
| STAT_MUW_HI_TEMPERATURE_LEVEL_07_EINH | string | °C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-muw-reset-anzahl"></a>
### _STATUS_DWA_MUW_RESET_ANZAHL

JobHeaderFormat 0x464A DIAG_DID_464A_READ_DWA_MUW_RST_NUM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_KOMM_FEHLER | string | muw vr kommunikation fehler kode |
| STAT_MUW_VR_INTERN_RESET_ANZAHL_WERT | unsigned char | Number of internal resets performed by MUW Front Right |
| STAT_MUW_VR_EXTERN_RESET_ANZAHL_WERT | unsigned char | Number of external resets performed by MUW Front Right |
| STAT_MUW_HR_KOMM_FEHLER | string | muw hr kommunikation fehler kode |
| STAT_MUW_HR_INTERN_RESET_ANZAHL_WERT | unsigned char | Number of internal resets performed by MUW Rear Right |
| STAT_MUW_HR_EXTERN_RESET_ANZAHL_WERT | unsigned char | Number of external resets performed by MUW Rear Right |
| STAT_MUW_HL_KOMM_FEHLER | string | muw hl kommunikation fehler kode |
| STAT_MUW_HL_INTERN_RESET_ANZAHL_WERT | unsigned char | Number of internal resets performed by MUW Rear Left |
| STAT_MUW_HL_EXTERN_RESET_ANZAHL_WERT | unsigned char | Number of external resets performed by MUW Rear Left |
| STAT_MUW_VL_KOMM_FEHLER | string | muw vl kommunikation fehler kode |
| STAT_MUW_VL_INTERN_RESET_ANZAHL_WERT | unsigned char | Number of internal resets performed by MUW Front Left |
| STAT_MUW_VL_EXTERN_RESET_ANZAHL_WERT | unsigned char | Number of external resets performed by MUW Front Left |
| STAT_MUW_HI_KOMM_FEHLER | string | muw hi kommunikation fehler kode |
| STAT_MUW_HI_INTERN_RESET_ANZAHL_WERT | unsigned char | Number of internal resets performed by MUW Rear Central |
| STAT_MUW_HI_EXTERN_RESET_ANZAHL_WERT | unsigned char | Number of external resets performed by MUW Rear Central |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-order-num"></a>
### _STATUS_DWA_ORDER_NUM

JobHeaderFormat 0x4641 DIAG_DID_4641_READ_ORDER_NUM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_ORDER_NUMBER_0_WERT | unsigned char | Production Order Number byte#0 |
| STAT_DWA_ORDER_NUMBER_1_WERT | unsigned char | Production Order Number byte#1 |
| STAT_DWA_ORDER_NUMBER_2_WERT | unsigned char | Production Order Number byte#2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-pin-test-res"></a>
### _STATUS_DWA_PIN_TEST_RES

JobHeaderFormat 0x4643 DIAG_DID_4643_READ_PIN_TEST_RES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_PIN_23_WERT | unsigned char | Microcontroller pin 23 status |
| STAT_DWA_PIN_22_WERT | unsigned char | Microcontroller pin 22 status |
| STAT_DWA_PIN_21_WERT | unsigned char | Microcontroller pin 21 status |
| STAT_DWA_PIN_20_WERT | unsigned char | Microcontroller pin 20 status |
| STAT_DWA_PIN_19_WERT | unsigned char | Microcontroller pin 19 status |
| STAT_DWA_PIN_18_WERT | unsigned char | Microcontroller pin 18 status |
| STAT_DWA_PIN_17_WERT | unsigned char | Microcontroller pin 17 status |
| STAT_DWA_PIN_16_WERT | unsigned char | Microcontroller pin 16 status |
| STAT_DWA_PIN_14_WERT | unsigned char | Microcontroller pin 14 status |
| STAT_DWA_PIN_13_WERT | unsigned char | Microcontroller pin 13 status |
| STAT_DWA_PIN_12_WERT | unsigned char | Microcontroller pin 12 status |
| STAT_DWA_PIN_11_WERT | unsigned char | Microcontroller pin 11 status |
| STAT_DWA_PIN_8_WERT | unsigned char | Microcontroller pin 8 status |
| STAT_DWA_PIN_7_WERT | unsigned char | Microcontroller pin 7 status |
| STAT_DWA_PIN_6_WERT | unsigned char | Microcontroller pin 6 status |
| STAT_DWA_PIN_2_WERT | unsigned char | Microcontroller pin 2 status |
| STAT_DWA_PINS_EINH | string | Microcontroller pin status descr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-reset-anzahl-lesen"></a>
### _STATUS_DWA_RESET_ANZAHL_LESEN

Abfrage Resets DWA JobHeaderFormat 0x4638 DIAG_DID_4638_READ_RESET_NUM_DWA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_PORF_RESET_NUM | unsigned char | DWA number of power on resets (hw bit PORF) performed since last delete, unaffected by system reset |
| STAT_DWA_LVRF_RESET_NUM | unsigned char | DWA number of low voltage resets (hw bit LVRF) performed since last delete, unaffected by system reset |
| STAT_DWA_ILAF_RESET_NUM | unsigned char | DWA number of illegal address access resets (hw bit ILAF) performed since last delete, unaffected by system reset |
| STAT_DWA_OTHER_RESET_NUM | unsigned char | DWA number of unknown resets performed since last delete |
| STAT_DWA_RESET_NUM_EINH | string | DWA number of resets measurement unit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-sleep"></a>
### _STATUS_DWA_SLEEP

JobHeaderFormat 0x4651 DIAG_DID_4651_SLEEP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_SLEEP | unsigned char | '1': status is 'sleep trigger active' - '0': status is 'sleep trigger inactive' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-squares-sn"></a>
### _STATUS_DWA_SQUARES_SN

JobHeaderFormat 0x463D DIAG_DID_463D_READ_SQUARES_SN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-sw-id"></a>
### _STATUS_DWA_SW_ID

JobHeaderFormat 0x463A DIAG_DID_463A_SW_ID

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_SW_ID_2 | unsigned char | Cans2 Sw id byte 2 |
| STAT_DWA_SW_ID_1 | unsigned char | Cans2 Sw id byte 1 |
| STAT_DWA_SW_ID_0 | unsigned char | Cans2 Sw id byte 0 |
| STAT_DWA_SW_ID_EINH | string | einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-testresults"></a>
### _STATUS_DWA_TESTRESULTS

JobHeaderFormat 0x463B DIAG_DID_DCC2_READ_TEST_RESULTS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_TEST_RESULT_1_WERT | unsigned char | Production Test Result #1 |
| STAT_DWA_TEST_RESULT_1_EINH | string | Production Test Result #1 |
| STAT_DWA_TEST_RESULT_2_WERT | unsigned char | Production Test Result #2 |
| STAT_DWA_TEST_RESULT_2_EINH | string | Production Test Result #2 |
| STAT_DWA_TEST_RESULT_3_WERT | unsigned char | Production Test Result #3 |
| STAT_DWA_TEST_RESULT_3_EINH | string | Production Test Result #3 |
| STAT_DWA_TEST_RESULT_4_WERT | unsigned char | Production Test Result #4 |
| STAT_DWA_TEST_RESULT_4_EINH | string | Production Test Result #4 |
| STAT_DWA_TEST_RESULT_5_WERT | unsigned char | Production Test Result #5 |
| STAT_DWA_TEST_RESULT_5_EINH | string | Production Test Result #5 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-ckm-reset"></a>
### _STEUERN_DWA_CKM_RESET

JobHeaderFormat 0x4646 DIAG_DID_4646_RESET_CKM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-dateofem"></a>
### _STEUERN_DWA_DATEOFEM

JobHeaderFormat 0x4640 DIAG_DID_4640_WRITE_DATEOFEM, writes the date on 5 digits: yymdd

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATE_BYTE_0 | int | year, e.g. '0x10' for 2010 |
| DATE_BYTE_1 | int | month (0x01=Jan,..., 0x12=Dec) |
| DATE_BYTE_2 | int | day, e.g. 0x28 means 28 |
| DATE_BYTE_3 | int | unused, for future expansions |
| DATE_BYTE_4 | int | unused, for future expansions |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-ext-bat"></a>
### _STEUERN_DWA_EXT_BAT

JobHeaderFormat 0x4650 DIAG_DID_4650_SET_EXT_BAT, activates/deactivates the Vbat input

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EXT_BAT_ON | unsigned char | '0' switch off the external battery, '1' switch on external battery |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-monitor-loeschen"></a>
### _STEUERN_DWA_MONITOR_LOESCHEN

JobHeaderFormat 0x4633 DIAG_DID_4633_MONITOR_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-muw-error-memory-reset"></a>
### _STEUERN_DWA_MUW_ERROR_MEMORY_RESET

JobHeaderFormat 0x4649 DIAG_DID_4649_RESET_DWA_MUW_DTCS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_RESET_KOMM_FEHLER | string | MUW vorne rechts kommunikation fehler kode |
| STAT_MUW_VR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HR_RESET_KOMM_FEHLER | string | MUW hinten rechts kommunikation fehler kode |
| STAT_MUW_HR_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HL_RESET_KOMM_FEHLER | string | MUW hinten links kommunikation fehler kode |
| STAT_MUW_HL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_VL_RESET_KOMM_FEHLER | string | MUW vorne links kommunikation fehler kode |
| STAT_MUW_VL_RESET_KOMM_FEHLER_EINH | string | einheit |
| STAT_MUW_HI_RESET_KOMM_FEHLER | string | MUW hinten zentral kommunikation fehler kode |
| STAT_MUW_HI_RESET_KOMM_FEHLER_EINH | string | einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-muw-reset-anzahl-loeschen"></a>
### _STEUERN_DWA_MUW_RESET_ANZAHL_LOESCHEN

JobHeaderFormat 0x464B DIAG_DID_464B_RESET_DWA_MUW_RST_NUM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUW_VR_RESET_RST_ANZAHL_KOMM_FEHLER | string | MUW vorne rechts kommunikation fehler kode |
| STAT_MUW_HR_RESET_RST_ANZAHL_KOMM_FEHLER | string | MUW hinten rechts kommunikation fehler kode |
| STAT_MUW_HL_RESET_RST_ANZAHL_KOMM_FEHLER | string | MUW hinten links kommunikation fehler kode |
| STAT_MUW_VL_RESET_RST_ANZAHL_KOMM_FEHLER | string | MUW vorne links kommunikation fehler kode |
| STAT_MUW_HI_RESET_RST_ANZAHL_KOMM_FEHLER | string | MUW hinten zentral kommunikation fehler kode |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-order-num"></a>
### _STEUERN_DWA_ORDER_NUM

JobHeaderFormat 0x4642 DIAG_DID_4642_WRITE_ORDER_NUM Change the SERIAL NUMBER of the square the PCB is installed in. It is saved in NVRAM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ON_BYTE0 | int | byte0 |
| ON_BYTE1 | int | byte1 |
| ON_BYTE2 | int | byte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-reset-anzahl-loeschen"></a>
### _STEUERN_DWA_RESET_ANZAHL_LOESCHEN

JobHeaderFormat 0x4639 DIAG_DID_4639_DWA_RESET_NUM_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-secondary-st-inhibit"></a>
### _STEUERN_DWA_SECONDARY_ST_INHIBIT

JobHeaderFormat 0x464F DIAG_DID_464F_SET_SECONDARY_ST_INHIBIT, activates/deactivates piezo secondary ST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PIEZO_SEC_ST_INH | unsigned char | '0' ST active, '1' ST inactive |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-seriennummer"></a>
### _STEUERN_DWA_SERIENNUMMER

JobHeaderFormat 0x4645 DIAG_DID_4645_WRITE_SERIAL_NUMBER Change the SERIAL NUMBER of the CANSINE in NVRAM. The serial number shall then be read with job 'seriennummer_lesen' The S.N. is composed of 10 bytes: - the last two digits of year (2 bytes) - e.g. 0x01 0x02 for the year 2012 - two digits for month id (2 bytes) - e.g. 0x00 0x01 for Jan 0x01 0x02 for Dec - two digits for the day (2 bytes) - e.g. 0x03 0x00 for the day 30 - the progressive decimal number (4 bytes) ---&gt; step of 1000, from '0' to '9' ---&gt; step of 0100, from '0' to '9' ---&gt; step of 0010, from '0' to '9' ---&gt; step of 0001, from '0' to '9' Enter each byte separated by semicolon with hex notation (0xNN) example: 0x00 0x08 0x01 0x01 0x02 0x07 0x00 0x00 0x00 0x01 (in the example, semicolons are not shown because of conflicts with the SGBD sintax)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SN_BYTE0 | unsigned char | byte0 |
| SN_BYTE1 | unsigned char | byte1 |
| SN_BYTE2 | unsigned char | byte2 |
| SN_BYTE3 | unsigned char | byte3 |
| SN_BYTE4 | unsigned char | byte4 |
| SN_BYTE5 | unsigned char | byte5 |
| SN_BYTE6 | unsigned char | byte6 |
| SN_BYTE7 | unsigned char | byte7 |
| SN_BYTE8 | unsigned char | byte8 |
| SN_BYTE9 | unsigned char | byte9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-sounds"></a>
### _STEUERN_DWA_SOUNDS

JobHeaderFormat 0x464E DIAG_DID_464E_SET_DWA_SOUNDS, activates/deactivates USA/ECE & buzzers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOUND_TYPE | unsigned char | '0' no change, '1' ECE sound, '2' USA sound, '3' default |
| ACTIVATE_BUZZER | unsigned char | '0': no change, '1': deactivates, '2': activates, '3': default |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-svk-history"></a>
### _STEUERN_DWA_SVK_HISTORY

JobHeaderFormat 0x464D DIAG_DID_464D_WRITE_DWA_SVK_HISTORY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BYTE_00 | unsigned char |  |
| ARG_BYTE_01 | unsigned char |  |
| ARG_BYTE_02 | unsigned char |  |
| ARG_BYTE_03 | unsigned char |  |
| ARG_BYTE_04 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-testresults"></a>
### _STEUERN_DWA_TESTRESULTS

JobHeaderFormat 0x463C DIAG_DID_463C_WRITE_TEST_RESULTS - these results are written in production

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TR_BYTE_0 | int | test #0 |
| TR_BYTE_1 | int | test #1 |
| TR_BYTE_2 | int | test #2 |
| TR_BYTE_3 | int | test #3 |
| TR_BYTE_4 | int | test #4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-trigger-dtc-store"></a>
### _STEUERN_DWA_TRIGGER_DTC_STORE

JobHeaderFormat 0x4652 DIAG_DID_4652_TRIGGER_DTC_STORE, triggers the storing of DTC's in nvram

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
- [LIEFERANTEN](#table-lieferanten) (134 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (203 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (162 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XAA76](#table-arg-0xaa76) (1 × 14)
- [ARG_0XAA79](#table-arg-0xaa79) (1 × 14)
- [ARG_0XDCA8](#table-arg-0xdca8) (2 × 12)
- [ARG_0XDCB5](#table-arg-0xdcb5) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (44 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (19 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0XAA76](#table-res-0xaa76) (1 × 13)
- [RES_0XAA7E](#table-res-0xaa7e) (6 × 13)
- [RES_0XAA7F](#table-res-0xaa7f) (6 × 13)
- [RES_0XDCA2](#table-res-0xdca2) (7 × 10)
- [RES_0XDCA8](#table-res-0xdca8) (1 × 10)
- [RES_0XDCA9](#table-res-0xdca9) (3 × 10)
- [RES_0XDCB0](#table-res-0xdcb0) (9 × 10)
- [RES_0XDCB6](#table-res-0xdcb6) (3 × 10)
- [RES_0XDCB7](#table-res-0xdcb7) (5 × 10)
- [RES_0XDCB8](#table-res-0xdcb8) (15 × 10)
- [RES_0XDCB9](#table-res-0xdcb9) (5 × 10)
- [RES_0XDCBC](#table-res-0xdcbc) (5 × 10)
- [RES_0XDCDD](#table-res-0xdcdd) (9 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (24 × 16)
- [TAB_ALARM_WERT_TO_TEXT](#table-tab-alarm-wert-to-text) (33 × 2)
- [TAB_CONTACT_STAT_WERT_TO_TEXT](#table-tab-contact-stat-wert-to-text) (2 × 2)
- [TAB_DWA_INTERN](#table-tab-dwa-intern) (22 × 2)
- [TAB_DWA_KLAPPENKONTAKT](#table-tab-dwa-klappenkontakt) (4 × 2)
- [TAB_DWA_LED](#table-tab-dwa-led) (5 × 2)
- [TAB_DWA_SCHNELLTEST](#table-tab-dwa-schnelltest) (3 × 2)
- [TAB_DWA_SELBSTTEST](#table-tab-dwa-selbsttest) (4 × 2)
- [TAB_DWA_SELBSTTEST_ERG](#table-tab-dwa-selbsttest-erg) (3 × 2)
- [TAB_DWA_SINE_INTERN](#table-tab-dwa-sine-intern) (5 × 2)
- [TAB_GEBLAESE_WERT_TO_TEXT](#table-tab-geblaese-wert-to-text) (3 × 2)
- [TAB_IRING_CLASS_WERT_TO_TEXT](#table-tab-iring-class-wert-to-text) (3 × 2)
- [TAB_MUW_FUNKTIONSTEST](#table-tab-muw-funktionstest) (4 × 2)
- [TAB_MUW_FUNKTIONSTEST_2](#table-tab-muw-funktionstest-2) (4 × 2)
- [TAB_MUW_INTERN](#table-tab-muw-intern) (3 × 2)
- [TAB_MUW_KOMM_FEHLER](#table-tab-muw-komm-fehler) (7 × 2)
- [TAB_MUW_SELBSTTEST](#table-tab-muw-selbsttest) (5 × 2)
- [TAB_SINE_BATT_LEVEL](#table-tab-sine-batt-level) (5 × 2)
- [TAB_STANDHEIZUNG_WERT_TO_TEXT](#table-tab-standheizung-wert-to-text) (4 × 2)
- [TAB_STANDLUEFTEN_WERT_TO_TEXT](#table-tab-standlueften-wert-to-text) (4 × 2)
- [TAB_STAT_OP_CABRIO_ROOF_WERT_TO_TEXT](#table-tab-stat-op-cabrio-roof-wert-to-text) (5 × 2)
- [TAB_STAT_OP_WINDOW_WERT_TO_TEXT](#table-tab-stat-op-window-wert-to-text) (2 × 2)
- [TAB_STAT_POS_CABRIO_ROOF_WERT_TO_TEXT](#table-tab-stat-pos-cabrio-roof-wert-to-text) (9 × 2)
- [TAB_ZUHEIZER_WERT_TO_TEXT](#table-tab-zuheizer-wert-to-text) (4 × 2)
- [TAB_ZV_ST_CLSY](#table-tab-zv-st-clsy) (9 × 2)

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

Dimensions: 134 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen =&gt; Delphi |
| 0x000002 | Kostal |
| 0x000003 | Hella |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako |
| 0x000008 | Bosch |
| 0x000009 | Loewe =&gt; Lear |
| 0x000010 | VDO |
| 0x000011 | Valeo |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine |
| 0x000018 | Continental Teves |
| 0x000019 | Elektromatik Suedafrika |
| 0x000020 | Becker |
| 0x000021 | Preh |
| 0x000022 | Alps |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi PHI |
| 0x000028 | DODUCO =&gt; BERU |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer |
| 0x000033 | Jatco |
| 0x000034 | Fuba |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE |
| 0x000041 | Megamos |
| 0x000042 | TRW |
| 0x000043 | Wabco |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC (Hella Electronics Corporation) |
| 0x000046 | Gemel |
| 0x000047 | ZF |
| 0x000048 | GMPT |
| 0x000049 | Harman Kardon |
| 0x000050 | Remes |
| 0x000051 | ZF Lenksysteme |
| 0x000052 | Magneti Marelli |
| 0x000053 | Borg Instruments |
| 0x000054 | GETRAG |
| 0x000055 | BHTC (Behr Hella Thermocontrol) |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon |
| 0x000058 | Autoliv |
| 0x000059 | Haberl |
| 0x000060 | Magna Steyr |
| 0x000061 | Marquardt |
| 0x000062 | AB-Elektronik |
| 0x000063 | Siemens VDO Borg |
| 0x000064 | Hirschmann Electronics |
| 0x000065 | Hoerbiger Electronics |
| 0x000066 | Thyssen Krupp Automotive Mechatronics |
| 0x000067 | Gentex GmbH |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steering Europe |
| 0x000071 | NSI B.V |
| 0x000072 | AISIN AW CO.LTD |
| 0x000073 | Shorlock |
| 0x000074 | Schrader |
| 0x000075 | BERU Electronics GmbH |
| 0x000076 | CEL |
| 0x000077 | Audio Mobil |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | AKsys GmbH |
| 0x000086 | META System |
| 0x000087 | Hülsbeck & Fürst GmbH & Co KG |
| 0x000088 | Mann & Hummel Automotive GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.A. |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp. |
| 0x000094 | KÜSTER Automotive Control |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental Automotive |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls |
| 0x00009A | Takata- Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN-Driveline |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | PEIKER acustics GmbH |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | ADC Automotive Distance Control Systems GmbH |
| 0x0000A5 | Funkwerk Dabendorf GmbH |
| 0x0000A6 | Lame |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Wanyu |
| 0x0000A9 | Thyssen Krupp Presta |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA |
| 0x0000AF | Alfmeier |
| 0x0000B0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0x0000B1 | Omron Automotive Electronics Europe Group |
| 0x0000B2 | ASK |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive World Headquarters |
| 0x0000B6 | Hans Widmaier |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | KYOCERA Display Corporation |
| 0x0000B9 | MAGNA Powertrain AG & Co KG |
| 0x0000BA | BorgWarner |
| 0x0000BB | BMW - Fahrzeugsimulator |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 19 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
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

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 203 rows × 3 columns

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
| 0x2300 | Aussenspiegel Beifahrer | - |
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
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
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
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
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
| 0x5768 | Fussgängerschutz Sensor links | 0 |
| 0x5770 | Fussgängerschutz Sensor rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0x5A00 | Innenlichtelektronik | 1 |
| 0x5A20 | Innenlichteinheit 2 | 1 |
| 0x5A30 | Innenlichteinheit 3 | 1 |
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Fahrertür vorne oben | 1 |
| 0x5E06 | Innenbeleuchtung Fahrertür vorne Mitte | 1 |
| 0x5E07 | Innenbeleuchtung Fahrertür vorne unten | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Fahrertür hinten oben | 1 |
| 0x5E0A | Innenbeleuchtung Fahrertür hinten unten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Beifahrertür vorne oben | 1 |
| 0x5E0D | Innenbeleuchtung Beifahrertür vorne Mitte | 1 |
| 0x5E0E | Innenbeleuchtung Beifahrertür vorne unten | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Beifahrertür hinten oben | 1 |
| 0x5E11 | Innenbeleuchtung Beifahrertür hinten unten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung I-Tafel Fahrer oben | 1 |
| 0x5E14 | Innenbeleuchtung I-Tafel Fahrer unten | 1 |
| 0x5E15 | Innenbeleuchtung I-Tafel oben Mitte | 1 |
| 0x5E16 | Innenbeleuchtung I-Tafel unten Mitte | 1 |
| 0x5E17 | Innenbeleuchtung I-Tafel oben Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung I-Tafel unten Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
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
| 0x7000 | Abschattungs-Elektronik-Dach | 1 |
| 0x7040 | Frontwischermotor | 1 |
| 0x7100 | NFC Leser Innenraum vorne | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 162 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | Daimler AG |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars (Ford Group) |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis GmbH |
| 0x0014 | Microchip Technology Inc |
| 0x0015 | Centro Ricerche FIAT |
| 0x0016 | Renesas Technology Europe GmbH - Mitsubishi |
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
| 0x0028 | Renesas Technology Europe Ltd  - Hitachi |
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
| 0x005B | VOLVO Technology Schweden |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic GmbH & Co. KG |
| 0x0061 | Flextronics / Sidler Automotive GmbH & Co. KG |
| 0x0062 | EAO Automotive GmbH & Co. KG |
| 0x0063 | helag-electronic gmbh |
| 0x0064 | Magna Electronics |
| 0x0065 | INTEVA Products, LLC |
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
| 0x007B | Bury GmbH & Co. KG |
| 0x007A | Kromberg & Schubert GmbH & Co. KG |
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
| 0x0093 | Phoenix International |
| 0x0094 | John Deere |
| 0x0095 | Grayhill Inc |
| 0x0096 | AppliedSensor GmbH |
| 0x0097 | UST Umweltsensortechnik GmbH |
| 0x0098 | Digades GmbH |
| 0x009A | TriMark Corporation |
| 0x009B | KB Auto Tech Co., Ltd. |
| 0x0099 | Thomson Linear Motion |
| 0x009C | Methode Electronics, Inc |
| 0x0101 | Huber Automotive AG |
| 0x009D | Danlaw, Inc. |
| 0x0100 | Isabellenhuette Heusler GmbH & Co. KG |
| 0x0102 | Precision Motors Deutsche Minebea GmbH |
| 0x009F | Fujikoki Corporation |
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
| 0xFFFF | unbekannter Hersteller |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
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

<a id="table-arg-0xaa76"></a>
### ARG_0XAA76

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL | + | - | 0-n | - | char | - | TAB_DWA_SELBSTTEST | - | - | - | - | - | optionales Argument; 0: Abbruch; 1: Selbsttest komplettes DWA-System; 2: Selbsttest Innenraumschutz; 3 Selbsttest Neigungsgeber; DEFAULT: 1 |

<a id="table-arg-0xaa79"></a>
### ARG_0XAA79

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | + | - | 0/1 | - | int | - | - | - | - | - | - | - | 0 oder kein Argument: DWA entschärfen; 1: DWA schärfen |

<a id="table-arg-0xdca8"></a>
### ARG_0XDCA8

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | int | - | TAB_DWA_LED | - | - | - | 0.0 | 3.0 | Ansteuerung der DWA-LED 0: Aus  1: Dauer-Ein  2: Blinken  3: Blitzen |
| ZEIT | ms | - | int | - | - | - | - | - | - | - | Angabe der Zeit in ms |

<a id="table-arg-0xdcb5"></a>
### ARG_0XDCB5

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | int | - | TAB_DWA_SCHNELLTEST | - | - | - | - | - | 0: Vorgang abbrechen; 1: Schnelltest leise 2: Schnelltest normal |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 44 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x025000 | Energiesparmode aktiv | 0 |
| 0x02ff50 | Test-DTC, DM_TEST_APPL | 1 |
| 0x804C00 | DWA, Piezo-Schallgeber: interne Leitungsunterbrechung im Sekundärkreis | 0 |
| 0x804C01 | DWA, Piezo-Schallgeber: interner Kurzschluss im Sekundärkreis | 0 |
| 0x804C02 | DWA, Piezo-Schallgeber: interne Leitungsunterbrechung im Primärkreis | 0 |
| 0x804C03 | DWA, Spiegel-LED: defekt oder Leitungsunterbrechung | 0 |
| 0x804C04 | DWA, Spiegel-LED: Kurzschluss nach Masse | 0 |
| 0x804C05 | DWA-Alarm, Details im Alarmspeicher | 1 |
| 0x804C06 | DWA, MUW_Sensor VR: keine Kommunikation | 0 |
| 0x804C07 | DWA, MUW_Sensor HR: keine Kommunikation | 0 |
| 0x804C08 | DWA, MUW_Sensor HL: keine Kommunikation | 0 |
| 0x804C09 | DWA, MUW_Sensor VL: keine Kommunikation | 0 |
| 0x804C0a | DWA, MUW_Sensor HI: keine Kommunikation | 0 |
| 0x804c0b | DWA, MUW_Sensor VR: Fehlermeldung | 0 |
| 0x804c0c | DWA, MUW_Sensor HR: Fehlermeldung | 0 |
| 0x804c0d | DWA, MUW_Sensor HL: Fehlermeldung | 0 |
| 0x804c0e | DWA, MUW_Sensor VL: Fehlermeldung | 0 |
| 0x804c0f | DWA, MUW_Sensor HI: Fehlermeldung | 0 |
| 0x804c10 | DWA, MUW_Sensor LIN-Bus: LIN-Bus gestört | 0 |
| 0x804c11 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x804c12 | Codierung: Fehler bei Codierung aufgetreten | 0 |
| 0x804c13 | Codierung: Signatur für Daten ungültig | 0 |
| 0x804c14 | Codierung: Codierung passt nicht zum Fahrzeug | 0 |
| 0x804c15 | Codierung: Unplausible Daten während Transaktion | 0 |
| 0x804c16 | DWA, Interne Versorgung: Unterspannung | 0 |
| 0x804c17 | DWA, Interne Versorgung: Überspannung | 0 |
| 0x804c19 | DWA, Neigungs-Sensor: interner Fehler beim Selbst-Test | 0 |
| 0x804c1a | DWA, interner Schaltkreis Spannungsversorgung: fehlerhaft | 0 |
| 0x804C1b | DWA, Piezo-Schallgeber: interner Kurzschluss im Primärkreis | 0 |
| 0x804c53 | Unterspannung erkannt | 1 |
| 0x804c54 | Überspannung erkannt | 1 |
| 0xDD0468 | Body-CAN: Control Module Bus Off | 0 |
| 0xdd0bff | Test-DTC, DM_TEST_COM | 1 |
| 0xDD1402 | ZEITBOTSCHAFTTIMEOUT_ZGW | 1 |
| 0xdd1403 | Botschaft (12F, Klemmen): Ausfall, Signal ungültig | 1 |
| 0xdd1404 | Botschaft (2FC, ZV und Klappenzustand): Ausfall, Signal ungültig | 1 |
| 0xdd1405 | Botschaft (3D6, Konfiguration DWA CKM): Signal ungültig | 1 |
| 0xdd1406 | Botschaft (256, Challenge Passive Access): Ausfall, Signal ungültig | 1 |
| 0xdd1407 | Botschaft (2A0, Steuerung Zentralverriegelung): Ausfall, Signal ungültig | 1 |
| 0xdd1408 | Botschaft (0EC, Status Zentralverriegelung Tür Schloss): Ausfall, Signal ungültig | 1 |
| 0xdd1409 | Botschaft (23A, Status Funkschlüssel): Signal ungültig | 1 |
| 0xdd140a | Botschaft (2F8, Uhrzeit Datum): Ausfall, Signal ungültig | 1 |
| 0xdd140b | Botschaft (26E, Steuerung FH SHD Zentrale (Komfort)): Ausfall, Signal ungültig | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 19 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x001001 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 |
| 0x002001 | NVM_E_WRITE_FAILED | 0 |
| 0x002002 | NVM_E_READ_FAILED | 0 |
| 0x002003 | NVM_E_CONTROL_FAILED | 0 |
| 0x002004 | NVM_E_ERASE_FAILED | 0 |
| 0x002006 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x002007 | NVM_E_READ_ALL_FAILED | 0 |
| 0x002010 | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x804c18 | DEM_EVENT_POLARITY_INVERSION | 0 |
| 0x804c1c | LIN_SENSOR_VR_IS_DTCS | 0 |
| 0x804c1d | LIN_SENSOR_HR_IS_DTCS | 0 |
| 0x804c1e | LIN_SENSOR_HL_IS_DTCS | 0 |
| 0x804c1f | LIN_SENSOR_VL_IS_DTCS | 0 |
| 0x804c20 | LIN_SENSOR_HI_IS_DTCS | 0 |
| 0x804c51 | PANIK | 0 |
| 0x804c52 | DWA: Deaktivierung des Innenraumschutzes und Neigungsgeber | 0 |
| 0x804c55 | DEM_EVENT_LIN_SENSORS_VBAT_LOW_INHIBITED | 0 |
| 0xE89400 | VSM_EVENT_VEHICLESTATE | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0xaa76"></a>
### RES_0XAA76

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_SELBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_DWA_SELBSTTEST_ERG | - | - | - | 0: Selbsttest NIO  1: Selbsstest IO 2: Selbsttest läuft |

<a id="table-res-0xaa7e"></a>
### RES_0XAA7E

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_SELBSTTEST | - | - | + | 0-n | - | char | - | TAB_MUW_SELBSTTEST | - | - | - | Status der Ausführung |
| STAT_MUW_VL_SEBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Ergebnis Selbsttest MUW vorne links |
| STAT_MUW_VR_SEBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Ergebnis Selbsttest MUW vorne rechts |
| STAT_MUW_HL_SEBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Ergebnis Selbsttest MUW hinten links |
| STAT_MUW_HR_SEBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Ergebnis Selbsttest MUW hinten rechts |
| STAT_MUW_HI_SEBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Ergebnis Selbsttest MUW hinten zentral |

<a id="table-res-0xaa7f"></a>
### RES_0XAA7F

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_VL_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST | - | - | - | Status MUW vorne links  0: MUW würde nicht auslösen  1: MUW würde auslösen 2: MUW fehlerhaft |
| STAT_MUW_VR_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST | - | - | - | Status MUW vorne rechts  0: MUW würde nicht auslösen  1: MUW würde auslösen 2: MUW fehlerhaft |
| STAT_MUW_HL_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST | - | - | - | Status MUW hinten links  0: MUW würde nicht auslösen  1: MUW würde auslösen 2: MUW fehlerhaft |
| STAT_MUW_HR_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST | - | - | - | Status MUW hinten rechts  0: MUW würde nicht auslösen  1: MUW würde auslösen 2: MUW fehlerhaft |
| STAT_MUW_HI_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST | - | - | - | Status MUW hinten zentral  0: MUW würde nicht auslösen  1: MUW würde auslösen 2: MUW fehlerhaft |
| STAT_MUW_FUNKTIONSTEST_NR | - | - | + | 0-n | - | char | - | TAB_MUW_FUNKTIONSTEST_2 | - | - | - | Aktueller Status des Jobs |

<a id="table-res-0xdca2"></a>
### RES_0XDCA2

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LEITUNG_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status der Leitungsüberwachung |
| STAT_UNTERSPANNUNG_EXT_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Unterspannungsüberwachung der externen Batterie |
| STAT_EEPROM_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Überwachnung EEPROM |
| STAT_AKTIVER_SCHUTZ_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Aktiver Schutz |
| STAT_WAKE_UP_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Überwachung der WakeUp-Zeit |
| STAT_SIRENE_AKUSTIK_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Sirenenschaltkreis (Akustik) |
| STAT_TILT_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | - | - | - | Status Neigungsgeber |

<a id="table-res-0xdca8"></a>
### RES_0XDCA8

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_LED_NR | 0-n | - | char | - | TAB_DWA_LED | - | - | - | 0: Aus 1: Dauer-Ein 2: Blinken 3: Blitzen |

<a id="table-res-0xdca9"></a>
### RES_0XDCA9

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NEIGUNG_X_ACHSE_WERT | Grad | - | int | - | - | - | - | - | Neigungswinkel X-Achse in Grad |
| STAT_NEIGUNG_Y_ACHSE_WERT | Grad | - | int | - | - | - | - | - | Neigungswinkel Y-Achse in Grad |
| STAT_NEIGUNG_Z_ACHSE_WERT | Grad | - | int | - | - | - | - | - | Neigungswinkel Z-Achse in Grad |

<a id="table-res-0xdcb0"></a>
### RES_0XDCB0

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_ALARM_BFT_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Beifahrertür; 1= DWA-Alarm ausgelöst durch Beifahrertür |
| STAT_DWA_ALARM_BFTH_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Beifahrertür hinten ; 1= DWA-Alarm ausgelöst durch Beifahrertür hinten |
| STAT_DWA_ALARM_DISTRIBUTION_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Distribution ; 1= DWA-Alarm ausgelöst durch Distribution |
| STAT_DWA_ALARM_FAT_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Fahrertür; 1= DWA-Alarm ausgelöst durch Fahrertür |
| STAT_DWA_ALARM_FATH_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Fahrertür hinten; 1= DWA-Alarm ausgelöst durch Fahrertür hinten |
| STAT_DWA_ALARM_HECKKLAPPE_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Heckklappe; 1= DWA-Alarm ausgelöst durch Heckklappe |
| STAT_DWA_ALARM_IRS_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Innenraumschutz; 1= DWA-Alarm ausgelöst durch Innenraumschutz |
| STAT_DWA_ALARM_MOTORHAUBE_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Motorhaube; 1= DWA-Alarm ausgelöst durch Motorhaube |
| STAT_DWA_ALARM_NEIGUNGSGEBER_AUSGELOEST_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch Neigungsgeber; 1= DWA-Alarm ausgelöst durch Neigungsgeber |

<a id="table-res-0xdcb6"></a>
### RES_0XDCB6

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ALARME_IRS_VORNE_WERT | - | - | int | - | - | - | - | - | Anzahl Alarme Innenraumschutz vorne |
| STAT_ALARME_IRS_HINTEN_WERT | - | - | int | - | - | - | - | - | Anzahl Alarme Innenraumschutz hinten |
| STAT_ALARME_ANZAHL_WERT | - | - | int | - | - | - | - | - | Anzahl der ausgelösten Alarme Gesamtsystem |

<a id="table-res-0xdcb7"></a>
### RES_0XDCB7

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_VL_TEMP_WERT | °C | - | int | - | - | - | 10.0 | - | Temperatur MUW vorne links |
| STAT_MUW_VR_TEMP_WERT | °C | - | int | - | - | - | 10.0 | - | Temperatur MUW vorne rechts |
| STAT_MUW_HL_TEMP_WERT | °C | - | int | - | - | - | 10.0 | - | Temperatur MUW hinten links |
| STAT_MUW_HR_TEMP_WERT | °C | - | int | - | - | - | 10.0 | - | Temperatur MUW hinten rechts |
| STAT_MUW_HI_TEMP_WERT | °C | - | int | - | - | - | 10.0 | - | Temperatur MUW hinten zentral |

<a id="table-res-0xdcb8"></a>
### RES_0XDCB8

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_VL_KOMM_FEHLER_NR | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Kommunikationsfehler des MUWs vorne links |
| STAT_MUW_VR_KOMM_FEHLER_NR | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Kommunikationsfehler des MUWs vorne rechts |
| STAT_MUW_HL_KOMM_FEHLER_NR | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Kommunikationsfehler des MUWs hinten links |
| STAT_MUW_HR_KOMM_FEHLER_NR | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Kommunikationsfehler des MUWs hinten rechts |
| STAT_MUW_HI_KOMM_FEHLER_NR | 0-n | - | char | - | TAB_MUW_KOMM_FEHLER | - | - | - | Kommunikationsfehler des MUWs hinten zentral |
| STAT_MUW_VL_INTERNER_STATUS | 0-n | - | char | - | TAB_MUW_INTERN | - | - | - | Interner Status des Sensors vorne links |
| STAT_MUW_VR_INTERNER_STATUS | 0-n | - | char | - | TAB_MUW_INTERN | - | - | - | Interner Status des Sensors vorne rechts |
| STAT_MUW_HL_INTERNER_STATUS | 0-n | - | char | - | TAB_MUW_INTERN | - | - | - | Interner Status des Sensors hinten links |
| STAT_MUW_HR_INTERNER_STATUS | 0-n | - | char | - | TAB_MUW_INTERN | - | - | - | Interner Status des Sensors hinten rechts |
| STAT_MUW_HI_INTERNER_STATUS | 0-n | - | char | - | TAB_MUW_INTERN | - | - | - | Interner Status des Sensors hinten zentral |
| STAT_MUW_VL_ALARMZAEHLER_WERT | - | - | int | - | - | - | - | - | Anzahl der Alarme des MUWs vorne links |
| STAT_MUW_VR_ALARMZAEHLER_WERT | - | - | int | - | - | - | - | - | Anzahl der Alarme des MUWs vorne rechts |
| STAT_MUW_HL_ALARMZAEHLER_WERT | - | - | int | - | - | - | - | - | Anzahl der Alarme des MUWs hinten links |
| STAT_MUW_HR_ALARMZAEHLER_WERT | - | - | int | - | - | - | - | - | Anzahl der Alarme des MUWs hinten rechts |
| STAT_MUW_HI_ALARMZAEHLER_WERT | - | - | int | - | - | - | - | - | Anzahl der Alarme des MUWs hinten zentral |

<a id="table-res-0xdcb9"></a>
### RES_0XDCB9

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_VL_NOISE_LEVEL_WERT | mV | - | int | - | - | - | - | - | Grundrauschen von MUW vorne links |
| STAT_MUW_VR_NOISE_LEVEL_WERT | mV | - | int | - | - | - | - | - | Grundrauschen von MUW vorne rechts |
| STAT_MUW_HL_NOISE_LEVEL_WERT | mV | - | int | - | - | - | - | - | Grundrauschen von MUW hinten links |
| STAT_MUW_HR_NOISE_LEVEL_WERT | mV | - | int | - | - | - | - | - | Grundrauschen von MUW hinten rechts |
| STAT_MUW_HI_NOISE_LEVEL_WERT | mV | - | int | - | - | - | - | - | Grundrauschen von MUW hinten zentral |

<a id="table-res-0xdcbc"></a>
### RES_0XDCBC

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_MUW_VL_SPANNUNG_WERT | V | - | unsigned char | - | - | - | 10.0 | - | Spannung des Sensors vorne links |
| STAT_MUW_VR_SPANNUNG_WERT | V | - | unsigned char | - | - | - | 10.0 | - | Spannung des Sensors vorne rechts |
| STAT_MUW_HL_SPANNUNG_WERT | V | - | unsigned char | - | - | - | 10.0 | - | Spannung des Sensors hinten links |
| STAT_MUW_HR_SPANNUNG_WERT | V | - | unsigned char | - | - | - | 10.0 | - | Spannung des Sensors hinten rechts |
| STAT_MUW_HI_SPANNUNG_WERT | V | - | unsigned char | - | - | - | 10.0 | - | Spannung des Sensors hinten zentral |

<a id="table-res-0xdcdd"></a>
### RES_0XDCDD

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KONTAKT_FAHRERTUER_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Fahrertür |
| STAT_KONTAKT_BEIFAHRERTUER_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Beifahrertür |
| STAT_KONTAKT_FAHRERTUER_HINTEN_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Fahrertür hinten |
| STAT_KONTAKT_BEIFAHRERTUER_HINTEN_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Beifahrertür hinten |
| STAT_KONTAKT_MOTORHAUBE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Motorhaube |
| STAT_KONTAKT_HECKKLAPPE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Heckklappe |
| STAT_KONTAKT_HECKSCHEIBE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | - | - | - | Kontakt Heckscheibe |
| STAT_ZV_NR | 0-n | - | unsigned char | - | TAB_ZV_ST_CLSY | - | - | - | Status Zentralverriegelung |
| STAT_RESERVE_WERT | HEX | - | unsigned long | - | - | - | - | - | Reserve (noch nicht belegt) |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 24 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DWA_SINE_ANSTEUERUNG | 0xAA70 | - | Ansteuerung der Sirene für maximal 5 Sekunden | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_SINE_BATT_LEVEL_RESET | 0xAA71 | - | Reset des Batterie-Levels. Nur nach Austausch der Batterie durchführen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_SELBSTTEST | 0xAA76 | - | Selbsttest DWA-System. Gefundene Fehler werden im Fehlerspeicher abgelegt | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAA76 | RES_0xAA76 |
| DWA_SCHAERFEN | 0xAA79 | - | 0: DWA entschärfen 1: DWA schärfen | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAA79 | - |
| DWA_ALARM_ANZAHL_LOESCHEN | 0xAA7A | - | Anzahl Alarme löschen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_MUW_SELBSTTEST | 0xAA7E | - | Selbsttest der angeschlossenen MUWs  Defekte MUWs werden im Fehlerspeicher eingetragen | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAA7E |
| DWA_MUW_FUNKTIONSTEST | 0xAA7F | - | Funktionstest der MUWs. Anzeige, welcher MUW würde auslösen | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xAA7F |
| DWA_SINE | 0xDCA2 | - | Status der Sirene / Neigungsgeber | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCA2 |
| DWA_SINE_BATT_LEVEL | 0xDCA3 | STAT_SIRENE_INTERNER_BATTERIE_LEVEL_NR | Status Auslesen der internen Batterie (Güte der Batterie?) | 0-n | - | - | char | TAB_SINE_BATT_LEVEL | - | - | - | - | 22 | - | - |
| DWA_LED | 0xDCA8 | - | Status/Steuern DWA-LED. Für Details siehe Sub-Tabelle(n) | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDCA8 | RES_0xDCA8 |
| DWA_SINE_NEIGUNG | 0xDCA9 | - | Neigungswinkel (X-, Y- und Z-Achse) des Fahrzeugs. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCA9 |
| DWA_INTERN | 0xDCAC | STAT_DWA_INTERN_NR | Abfrage Status DWA | 0-n | - | - | int | TAB_DWA_INTERN | - | - | - | - | 22 | - | - |
| DWA_ALARM_AUSGELOEST | 0xDCB0 | - | Status, welcher Alarm ausgelöst hat | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB0 |
| DWA_SCHNELLTEST | 0xDCB5 | - | Aktiviert den DWA-Schnelltest Modus (Sensoren werden geschaerft) 0: Vorgang beenden 1: leise  2: normale Lautstärke | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCB5 | - |
| DWA_ALARM_ANZAHL | 0xDCB6 | - | Anzahl durch Innenraumschutz ausgelöste Alarme | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB6 |
| DWA_MUW_TEMPERATUR | 0xDCB7 | - | Ausgabe der internen Temperatur der Mirkowellensensoren (MUWs) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB7 |
| DWA_MUW_INTERN | 0xDCB8 | - | Interner Status der Mirkowellensensoren (MUW) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB8 |
| DWA_MUW_NOISE_LEVEL | 0xDCB9 | - | Grundrauschen der MUWs. Ausgegeben wird ein Spannungswert | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB9 |
| DWA_MUW_FALSE_WAKEUP_LEVELS | 0xDCBA | - | Status / Reset False WakeUp-Levels | - | - | - | - | - | - | - | - | - | - | - | - |
| DWA_MUW_ALARM_LEVELS | 0xDCBB | - | Status / Reset der letzten MUW-Alarme | - | - | - | - | - | - | - | - | - | - | - | - |
| DWA_MUW_SPANNUNG | 0xDCBC | - | Status Spannungsversorgung der Mikrowellensensoren MUW | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCBC |
| DWA_TEMPERATUR | 0xDCBD | STAT_DWA_TEMPERATUR_WERT | Status Temperatur der DWA | °C | - | - | int | - | - | 10.0 | - | - | 22 | - | - |
| DWA_SPANNUNG | 0xDCBF | STAT_DWA_SPANNUNG_WERT | Auslesen der DWA-Spannung | Volt | - | - | unsigned char | - | - | 10.0 | - | - | 22 | - | - |
| DWA_KLAPPENKONTAKTE | 0xDCDD | - | Status der eingelesenen Klappenkontakte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCDD |

<a id="table-tab-alarm-wert-to-text"></a>
### TAB_ALARM_WERT_TO_TEXT

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x10 | Alarm CANSINE2: MUW VR, Leitungsunterbrechung/-Kurzschluss |
| 0x11 | Alarm CANSINE2: MUW HR, Leitungsunterbrechung/-Kurzschluss |
| 0x12 | Alarm CANSINE2: MUW HL, Leitungsunterbrechung/-Kurzschluss |
| 0x13 | Alarm CANSINE2: MUW VL, Leitungsunterbrechung/-Kurzschluss |
| 0x14 | Alarm CANSINE2: MUW Hi, Leitungsunterbrechung/-Kurzschluss |
| 0x15 | Alarm CANSINE2: MUW VR, Innenraumschutz |
| 0x16 | Alarm CANSINE2: MUW HR, Innenraumschutz |
| 0x17 | Alarm CANSINE2: MUW HL, Innenraumschutz |
| 0x18 | Alarm CANSINE2: MUW VL, Innenraumschutz |
| 0x19 | Alarm CANSINE2: MUW Hi, Innenraumschutz |
| 0x30 | Alarm CANSINE2: Türkontakt, Fahrertuer vorne |
| 0x31 | Alarm CANSINE2: Türkontakt, Fahrertuer vorne, Daueralarm |
| 0x32 | Alarm CANSINE2: Türkontakt, Beifahrertuer vorne |
| 0x33 | Alarm CANSINE2: Türkontakt, Beifahrertuer vorne, Daueralarm |
| 0x34 | Alarm CANSINE2: Türkontakt, Fahrertuer hinten |
| 0x35 | Alarm CANSINE2: Türkontakt, Fahrertuer hinten, Daueralarm |
| 0x36 | Alarm CANSINE2: Türkontakt, Beifahrertuer hinten |
| 0x37 | Alarm CANSINE2: Türkontakt, Beifahrertuer hinten, Daueralarm |
| 0x38 | Alarm CANSINE2: Kontakt, Heckklappe |
| 0x39 | Alarm CANSINE2: Kontakt, Heckklappe, Daueralarm |
| 0x3A | Alarm CANSINE2: Kontakt, Motorhaube |
| 0x3B | Alarm CANSINE2: Kontakt, Motorhaube, Daueralarm |
| 0x3C | Alarm CANSINE2: Kontakt, Heckscheibe |
| 0x3D | Alarm CANSINE2: Kontakt, Heckscheibe, Daueralarm |
| 0x70 | Alarm CANSINE2: Leitungsunterbrechung |
| 0xB1 | Alarm CANSINE2: OBD-Kommunikation Ethernet |
| 0xB2 | Alarm CANSINE2: OBD-Kommunikation D-CAN |
| 0xD0 | Alarm CANSINE2: Tilt Sensor X+ |
| 0xD1 | Alarm CANSINE2: Tilt Sensor X- |
| 0xD2 | Alarm CANSINE2: Tilt Sensor Y+ |
| 0xD4 | Alarm CANSINE2: Tilt Sensor Y- |
| 0xD8 | Alarm CANSINE2: Tilt Sensor Z+ |
| 0xE0 | Alarm CANSINE2: Tilt Sensor Z- |

<a id="table-tab-contact-stat-wert-to-text"></a>
### TAB_CONTACT_STAT_WERT_TO_TEXT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Closed |
| 0x01 | Open |

<a id="table-tab-dwa-intern"></a>
### TAB_DWA_INTERN

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DWA entschärft |
| 0x01 | DWA wird entschärft |
| 0x02 | DWA in Schärfung |
| 0x03 | DWA geschärft |
| 0x04 | DWA geschärft - Klappenkontakte noch ausgeblendet |
| 0x05 | DWA geschärft - Hotelstellung aktiv |
| 0x06 | DWA geschärft - IRS nicht aktiv |
| 0x07 | DWA geschärft - Neigungssensor nicht aktiv |
| 0x08 | DWA geschärft - IRS und Neigungsgebersensor nicht aktiv |
| 0x09 | DWA geschärft - IRS und Neigungsgebersensor durch Benutzer deaktiviert |
| 0x0A | DWA geschärft - Distributionsmodus |
| 0x0B | DWA Alarm |
| 0x0C | DWA Pause nach Alarm |
| 0x0D | DWA Panik Alarm Mode |
| 0x0E | DWA Transportmode |
| 0x0F | DWA Werkstattmode |
| 0x10 | DWA Fertigungsmode |
| 0x11 | DWA Energiesparmode wird beendet |
| 0x12 | DWA Powerdown Mode |
| 0x13 | DWA Schnelltest aktiv |
| 0x14 | DWA Selbsttest aktiv |
| 0xFF | unbekannter Status |

<a id="table-tab-dwa-klappenkontakt"></a>
### TAB_DWA_KLAPPENKONTAKT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | geschlossen |
| 0x01 | offen |
| 0x02 | unplausibel |
| 0x03 | ungültig |

<a id="table-tab-dwa-led"></a>
### TAB_DWA_LED

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Dauer-Ein |
| 0x02 | Blinken |
| 0x03 | Blitzen |
| 0xFF | unbekannter Zustand |

<a id="table-tab-dwa-schnelltest"></a>
### TAB_DWA_SCHNELLTEST

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Abbrechen |
| 0x01 | Schnelltest leise |
| 0x02 | Schnelltest normal |

<a id="table-tab-dwa-selbsttest"></a>
### TAB_DWA_SELBSTTEST

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Abbruch |
| 0x01 | Selbsttest Komplettes DWA-System |
| 0x02 | Selbsttest Innenraumschutz |
| 0x03 | Selbsttest Neigungssgeber |

<a id="table-tab-dwa-selbsttest-erg"></a>
### TAB_DWA_SELBSTTEST_ERG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Selbsttest NIO |
| 0x01 | Selbsttest IO |
| 0x02 | Selbsttest läuft |

<a id="table-tab-dwa-sine-intern"></a>
### TAB_DWA_SINE_INTERN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler aktiv |
| 0x02 | Fehler war aktiv |
| 0x03 | ungültig |
| 0x04 | nicht unterstüzt |

<a id="table-tab-geblaese-wert-to-text"></a>
### TAB_GEBLAESE_WERT_TO_TEXT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Off |
| 0x01 | On |
| 0x03 | Signal ungültig |

<a id="table-tab-iring-class-wert-to-text"></a>
### TAB_IRING_CLASS_WERT_TO_TEXT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Sleep_Prevention |
| 0x02 | Wakeup |
| 0x03 | Local_Awake |

<a id="table-tab-muw-funktionstest"></a>
### TAB_MUW_FUNKTIONSTEST

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MUW würde nicht auslösen |
| 0x01 | MUW würde auslösen |
| 0x02 | MUW fehlerhaft |
| 0xFF | ungültiger Wert |

<a id="table-tab-muw-funktionstest-2"></a>
### TAB_MUW_FUNKTIONSTEST_2

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Funktionstest nicht aktiv |
| 0x01 | Funktionstest läuft |
| 0x02 | Funktionstest konnte nicht gestartet werden |
| 0xFF | ungültiger Wert |

<a id="table-tab-muw-intern"></a>
### TAB_MUW_INTERN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sensor nicht aktiv |
| 0x01 | Sensor aktiv |
| 0xFF | ungültiger Wert |

<a id="table-tab-muw-komm-fehler"></a>
### TAB_MUW_KOMM_FEHLER

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | DWA Bus permanent gestört |
| 0x02 | MUW Timeout |
| 0x03 | Antwort vom falschen Sensor |
| 0x04 | Falsche Checksumme in der Antwort des Sensors |
| 0xFE | Sensor nicht konfiguriert |
| 0xFF | unbekannter Status |

<a id="table-tab-muw-selbsttest"></a>
### TAB_MUW_SELBSTTEST

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Selbsttest läuft |
| 0x02 | Selbsttest erfolgreich abgeschlossen |
| 0x03 | Selbsttest mir Fehlern abgeschlossen |
| 0xFF | ungültiger Wert |

<a id="table-tab-sine-batt-level"></a>
### TAB_SINE_BATT_LEVEL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Status vorhanden |
| 0x01 | Batterie Sirene leer |
| 0x02 | Batterie Sirene gut |
| 0x03 | Batterie Sirene neu |
| 0xFF | ungültiger Wert |

<a id="table-tab-standheizung-wert-to-text"></a>
### TAB_STANDHEIZUNG_WERT_TO_TEXT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / Nicht verfügbar |
| 0x01 | Off |
| 0x02 | On |
| 0x03 | Signal ungültig |

<a id="table-tab-standlueften-wert-to-text"></a>
### TAB_STANDLUEFTEN_WERT_TO_TEXT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / Nicht verfügbar |
| 0x01 | Off |
| 0x02 | On |
| 0x03 | Signal ungültig |

<a id="table-tab-stat-op-cabrio-roof-wert-to-text"></a>
### TAB_STAT_OP_CABRIO_ROOF_WERT_TO_TEXT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Bedienung |
| 0x01 | öffnen |
| 0x02 | schließen |
| 0x03 | Beladeposition anfahren |
| 0x0F | Signal ungültig |

<a id="table-tab-stat-op-window-wert-to-text"></a>
### TAB_STAT_OP_WINDOW_WERT_TO_TEXT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | gestoppt |
| 0x01 | bewegung |

<a id="table-tab-stat-pos-cabrio-roof-wert-to-text"></a>
### TAB_STAT_POS_CABRIO_ROOF_WERT_TO_TEXT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Komplett geschlossen und verriegelt |
| 0x01 | Zwischenstellung |
| 0x02 | Komplett geöffnet und verriegelt |
| 0x03 | Beladeposition |
| 0x04 | Hardtop aufgesetzt |
| 0x05 | Komplett geschlossen |
| 0x06 | Komplett geöffnet |
| 0x07 | Notverriegelung durchgeführt |
| 0x0F | Signal ungültig |

<a id="table-tab-zuheizer-wert-to-text"></a>
### TAB_ZUHEIZER_WERT_TO_TEXT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / Nicht verfügbar |
| 0x01 | ZH ausschalten / aus |
| 0x02 | ZH einschalten / ein |
| 0x03 | Signal ungültig |

<a id="table-tab-zv-st-clsy"></a>
### TAB_ZV_ST_CLSY

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Status empfangen |
| 0x01 | Mindestens eine Tür ist entriegelt |
| 0x02 | Mindestens eine Tür ist verriegelt |
| 0x03 | Mindestens eine Tür ist entriegelt und Mindestens eine Tür ist verriegelt |
| 0x04 | Interner ZV-Master ist gesichert |
| 0x05 | Interner ZV-Master ist gesichert und Mindestens eine Tür ist entriegelt |
| 0x06 | Interner ZV-Master ist gesichert und Mindestens eine Tür ist verriegelt |
| 0x07 | Interner ZV-Master ist gesichert und Mindestens eine Tür ist entriegelt und Mindestens eine Tür ist verriegelt |
| 0xFF | Signal ungültig |
