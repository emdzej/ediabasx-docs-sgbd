# fzd_f15.prg

- Jobs: [86](#jobs)
- Tables: [162](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Funktionszentrum Dach  56 0F1CF0 |
| ORIGIN | BMW EI-601 Herter |
| REVISION | 6.000 |
| AUTHOR | Valeo EI-601 Veith, Valeo EI-601 Sava |
| COMMENT | - |
| PACKAGE | 1.40 |
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
- [STATUS_DWA_ALARMSPEICHER](#job-status-dwa-alarmspeicher) - Auslesen des Alarmspeichers der Diebstahlwarnlage JobHeaderFormat 0x6010 STATUS_DWA_ALARMSPEICHER
- [STEUERN_DWA_ALARMSPEICHER_LOESCHEN](#job-steuern-dwa-alarmspeicher-loeschen) - Löscht den Alarmspeicher der Diebstahlwarnanlage JobHeaderFormat 0x6010 STEUERN_DWA_ALARMSPEICHER_LOESCHEN
- [STATUS_DWA_PANIKSPEICHER](#job-status-dwa-panikspeicher) - Auslesen der Panikspeicher-Einträge der Diebstahlwarnlage JobHeaderFormat 0x6011 STATUS_DWA_PANIKSPEICHER
- [STEUERN_DWA_PANIKSPEICHER_LOESCHEN](#job-steuern-dwa-panikspeicher-loeschen) - Löscht den Panikspeicher der Diebstahlwarnanlage JobHeaderFormat 0x6011 STEUERN_DWA_PANIKSPEICHER_LOESCHEN
- [STATUS_DWA_DEAKTIVIERUNG_IRS_NG](#job-status-dwa-deaktivierung-irs-ng) - Auslesen der Deaktivierungsspeicher-Einträge für IRS und NG JobHeaderFormat 0x6017 STATUS_DWA_DEAKTIVIERUNG_IRS_NG
- [STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN](#job-steuern-dwa-deaktivierung-irs-ng-loeschen) - Löscht den Deaktivierungsspeicher des IRS und NG JobHeaderFormat 0x6016 STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN
- [STATUS_SHD_ESH_DENORMIERUNGS_LOGGER_LESEN](#job-status-shd-esh-denormierungs-logger-lesen) - Umsetzung: MT  STATUS_SHD_ESH_DENORMIERUNGS_LOGGER_LESEN
- [STEUERN_SHD_ESH_DENORMIERUNGS_LOGGER_LOESCHEN](#job-steuern-shd-esh-denormierungs-logger-loeschen) - Löscht die Denormierungslogger von Schiebedach und elektrischer Schiebehimmel Umsetzung: MT  STEUERN_SHD_ESH_DENORMIERUNGS_LOGGER_LOESCHEN
- [STATUS_SHD_ESH_MOTORSTOP_LOGGER_LESEN](#job-status-shd-esh-motorstop-logger-lesen) - Liest die aufgezeichneten Daten des Loggers für Abbruch Motorlauf. Die letzten 10 Ereignisse werden für jeden Ort gespeichert Umsetzung: MT  STATUS_SHD_ESH_MOTORSTOP_LOGGER_LESEN
- [STEUERN_SHD_ESH_MOTORSTOP_LOGGER_LOESCHEN](#job-steuern-shd-esh-motorstop-logger-loeschen) - Löscht den Logger für Abbruch / Ende Motorlauf Umsetzung: MT  STEUERN_SHD_ESH_MOTORSTOP_LOGGER_LOESCHEN
- [STATUS_SHD_ESH_REVERSIER_LOGGER_LESEN](#job-status-shd-esh-reversier-logger-lesen) - Auslesen der Reversierlogger Schiebedach und elektrischer Schiebehimmel Umsetzung: MT  STATUS_SHD_ESH_REVERSIER_LOGGER_LESEN
- [STEUERN_SHD_ESH_REVERSIER_LOGGER_LOESCHEN](#job-steuern-shd-esh-reversier-logger-loeschen) - Löscht die Logger von Schiebedach und / oder elektrsicher Schiebehimmel Umsetzung: MT  STEUERN_SHD_ESH_REVERSIER_LOGGER_LOESCHEN
- [_READ_RESETCOUNTER](#job-read-resetcounter) - Read resetcounter JobHeaderFormat 0x600D _READ_RESETCOUNTER
- [_RESET_RESETCOUNTER](#job-reset-resetcounter) - Reset resetcounter JobHeaderFormat 0x600E _RESET_RESETCOUNTER
- [_DWA_TRIGGER_STATUS](#job-dwa-trigger-status) - Status Digital Input/Output JobHeaderFormat 0x600F _DWA_TRIGGER_STATUS
- [_WRITE_USIS_SERIAL_IO](#job-write-usis-serial-io) - Status Analog Input/Output JobHeaderFormat 0xF500 _WRITE_USIS_SERIAL_IO
- [_USIS_DATA_SELFTESTS_RESULT](#job-usis-data-selftests-result) - Status USIS selftest results JobHeaderFormat 0x6020 _USIS_DATA_SELFTESTS_RESULT
- [_USIS_DATA_TOTALARMCOUNTER_READ](#job-usis-data-totalarmcounter-read) - Status USIS total alarm counter JobHeaderFormat 0x6021 _USIS_DATA_TOTALARMCOUNTER_READ
- [_USIS_DATA_ALARMMEMORY_READ](#job-usis-data-alarmmemory-read) - Status USIS alarm memory JobHeaderFormat 0x6022 _USIS_DATA_ALARMMEMORY_READ
- [_USIS_DATA_ECHODOPPLERCOUNTER_READ](#job-usis-data-echodopplercounter-read) - Status echo-doppler-counter JobHeaderFormat 0x6023 _USIS_DATA_ECHODOPPLERCOUNTER_READ
- [_USIS_DATA_ENVIRONMENT_READ](#job-usis-data-environment-read) - Status environment JobHeaderFormat 0x6024 _USIS_DATA_ENVIRONMENT_READ
- [_USIS_CMD_ALARMMEMORY_RESET](#job-usis-cmd-alarmmemory-reset) - Reset alarmmemory JobHeaderFormat 0x6025 _USIS_CMD_ALARMMEMORY_RESET
- [_USIS_CMD_ECHODOPPLERCOUNTER_RESET](#job-usis-cmd-echodopplercounter-reset) - Reset echo-doppler-counter JobHeaderFormat 0x6026 _USIS_CMD_ECHODOPPLERCOUNTER_RESET
- [_USIS_CMD_ENVIRONMENT_SET](#job-usis-cmd-environment-set) - Write the environment JobHeaderFormat 0x6027 _USIS_CMD_ENVIRONMENT_SET
- [_USIS_DATA_ANPASSUNG_VALUE_READ](#job-usis-data-anpassung-value-read) - Read Adaptation USIS-Data JobHeaderFormat 0x6028 _USIS_DATA_ANPASSUNG_VALUE_READ
- [_USIS_DATA_ANPASSUNG_VALUE_SET](#job-usis-data-anpassung-value-set) - Write Adaptation USIS-Data JobHeaderFormat 0x6029 _USIS_DATA_ANPASSUNG_VALUE_SET
- [_USIS_CMD_TOTALALARMCOUNTER_RESET](#job-usis-cmd-totalalarmcounter-reset) - Reset total alarm counter JobHeaderFormat 0x602A _USIS_CMD_TOTALALARMCOUNTER_RESET
- [_DISABLE_DTC](#job-disable-dtc) - reset WD JobHeaderFormat 0xF501 _DISABLE_DTC
- [_SLIDER_DATA_OUTPUT](#job-slider-data-output) - reset WD JobHeaderFormat 0xF502 _SLIDER_DATA_OUTPUT
- [_READ_DIO](#job-read-dio) - Status Digital Input/Output JobHeaderFormat 0x6000 _READ_DIO
- [_WRITE_DIO](#job-write-dio) - Steuern Digital Input/Output JobHeaderFormat 0x6001 _WRITE_DIO
- [_READ_AIO](#job-read-aio) - Status Analog Input/Output JobHeaderFormat 0x6002 _READ_AIO
- [_READ_FIO](#job-read-fio) - Status Frequenz Input/Output JobHeaderFormat 0x6003 _READ_FIO
- [_WRITE_FIO](#job-write-fio) - Steuern Frequenz Input/Output JobHeaderFormat 0x6004 _SCHREIBEN_FIO
- [_READ_EEP](#job-read-eep) - Status EEPROM JobHeaderFormat 0x6005 _READ_EEP
- [_WRITE_EEP](#job-write-eep) - Steuern EEPROM JobHeaderFormat 0x6006 _WRITE_EEP
- [_CONTROL_EEP](#job-control-eep) - Steuern EEPROM JobHeaderFormat 0x6007 _CONTROL_EEP
- [_READ_VERSION](#job-read-version) - Status Version JobHeaderFormat 0x6008 _READ_VERSION
- [_READ_PCB_DATA](#job-read-pcb-data) - Status PCB JobHeaderFormat 0x6009 _READ_PCB_DATA
- [_WRITE_PCB_DATA](#job-write-pcb-data) - Steuern PCB JobHeaderFormat 0x600A _WRITE_PCB_DATA
- [_READ_ASSEMBLY_DATA](#job-read-assembly-data) - Status assembly JobHeaderFormat 0x600B _READ_ASSEMBLY_DATA
- [_WRITE_ASSEMBLY_DATA](#job-write-assembly-data) - Steuern assembly JobHeaderFormat 0x600C _WRITE_ASSEMBLY_DATA
- [_READ_CPU_LOAD](#job-read-cpu-load) - Read CPU load JobHeaderFormat 0x6030 _READ_CPU_LOAD
- [_RESET_CPU_LOAD](#job-reset-cpu-load) - Reset CPU load Job HeaderFormat 0x6031 _RESET_CPU_LOAD
- [_VALEO_WRITE_ENABLE](#job-valeo-write-enable) - Enable write JobHeaderFormat 0x6032 _VALEO_WRITE_ENABLE
- [_READ_TASK_STACK](#job-read-task-stack) - Read task stack JobHeaderFormat 0x6034 _READ_TASK_STACK
- [STATUS_SHD_ESH_BEWERTUNG_KENNLINIE](#job-status-shd-esh-bewertung-kennlinie) - Auslesen der gespeicherten Kennlinien/Adaptionsdaten fuer den Einklemmschutz

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

<a id="job-status-dwa-alarmspeicher"></a>
### STATUS_DWA_ALARMSPEICHER

Auslesen des Alarmspeichers der Diebstahlwarnlage JobHeaderFormat 0x6010 STATUS_DWA_ALARMSPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALARM_ANZAHL | unsigned char | Anzahl der Alarmspeichereinträge |
| STAT_ALARM_ANZAHL_TEXT | string | Anzahl der Alarmspeichereinträge |
| STAT_ALARM_ID | unsigned char | Alarm ID siehe Tabelle TAB_DWA_ALARMSPEICHER |
| STAT_ALARM_ID_TEXT | string | Alarm ID siehe Tabelle TAB_DWA_ALARMSPEICHER |
| STAT_ALARM_ANZAHL_ZYKLUS | unsigned char | Anzahl Alarme während eines Alarmzyklus |
| STAT_ALARM_ANZAHL_ZYKLUS_TEXT | string | Anzahl Alarme während eines Alarmzyklus |
| STAT_POS_FENSTER_FAT_WERT | unsigned char | Status Fensterposition FAhrerTür |
| STAT_POS_FENSTER_FAT_EINH | string | Status Fensterposition FAhrerTür |
| STAT_POS_FENSTER_FAT | unsigned char | Status Fensterposition FAhrerTür (Abkürzung FAT) |
| STAT_POS_FENSTER_FAT_TEXT | string | Status Fensterposition FAhrerTür (Abkürzung FAT) siehe Tabelle TAB_DWA_STATUS_FENSTER_POSITION |
| STAT_POS_FENSTER_FAT_ROH_WERT | unsigned char | Status Fensterposition FAhrerTür als Rohwert |
| STAT_POS_FENSTER_FAT_ROH_EINH | string | Status Fensterposition FAhrerTür als Rohwert |
| STAT_POS_FENSTER_BFT_WERT | unsigned char | Status Fensterposition BeiFahrerTür |
| STAT_POS_FENSTER_BFT_EINH | string | Status Fensterposition BeiFahrerTür |
| STAT_POS_FENSTER_BFT | unsigned char | Status Fensterposition BeiFahrerTür (Abkürzung BFT) |
| STAT_POS_FENSTER_BFT_TEXT | string | Status Fensterposition BeiFahrerTür (Abkürzung BFT) siehe Tabelle TAB_DWA_STATUS_FENSTER_POSITION |
| STAT_POS_FENSTER_BFT_ROH_WERT | unsigned char | Status Fensterposition BeiFahrerTür als Rohwert |
| STAT_POS_FENSTER_BFT_ROH_EINH | string | Status Fensterposition BeiFahrerTür als Rohwert |
| STAT_POS_FENSTER_FATH_WERT | unsigned char | Status Fensterposition FAhrerTür Hinten |
| STAT_POS_FENSTER_FATH_EINH | string | Status Fensterposition FAhrerTür Hinten |
| STAT_POS_FENSTER_FATH | unsigned char | Status Fensterposition FAhrerTür Hinten (Abkürzung FATH) |
| STAT_POS_FENSTER_FATH_TEXT | string | Status Fensterposition FAhrerTür Hinten (Abkürzung FATH) siehe Tabelle TAB_DWA_STATUS_FENSTER_POSITION |
| STAT_POS_FENSTER_FATH_ROH_WERT | unsigned char | Status Fensterposition FAhrerTür Hinten als Rohwert |
| STAT_POS_FENSTER_FATH_ROH_EINH | string | Status Fensterposition FAhrerTür Hinten als Rohwert |
| STAT_POS_FENSTER_BFTH_WERT | unsigned char | Status Fensterposition BeiFahrerTür Hinten |
| STAT_POS_FENSTER_BFTH_EINH | string | Status Fensterposition BeiFahrerTür Hinten |
| STAT_POS_FENSTER_BFTH | unsigned char | Status Fensterposition BeiFahrerTür Hinten (Abkürzung BFTH) |
| STAT_POS_FENSTER_BFTH_TEXT | string | Status Fensterposition BeiFahrerTür Hinten (Abkürzung BFTH) siehe Tabelle TAB_DWA_STATUS_FENSTER_POSITION |
| STAT_POS_FENSTER_BFTH_ROH_WERT | unsigned char | Status Fensterposition BeiFahrerTür Hinten als Rohwert |
| STAT_POS_FENSTER_BFTH_ROH_EINH | string | Status Fensterposition BeiFahrerTür Hinten als Rohwert |
| STAT_POS_SHD_WERT | unsigned char | Status Position SchiebeHebeDach (Abkürzung SHD) |
| STAT_POS_SHD_EINH | string | Status Position SchiebeHebeDach (Abkürzung SHD) |
| STAT_POS_SHD_NEIGUNG_WERT | unsigned char | Status Position SchiebeHebeDach-Neigung |
| STAT_POS_SHD_NEIGUNG_EINH | string | Status Position SchiebeHebeDach-Neigung |
| STAT_POS_ESH_WERT | unsigned char | Status Position Elektrischer SchiebeHimmel (Abkürzung ESH) |
| STAT_POS_ESH_EINH | string | Status Position Elektrischer SchiebeHimmel (Abkürzung ESH) |
| STAT_POS_ESH_NEIGUNG_WERT | unsigned char | Status Position Elektrischer SchiebeHimmel bei SHD-Neigung |
| STAT_POS_ESH_NEIGUNG_EINH | string | Status Position Elektrischer SchiebeHimmel bei SHD-Neigung |
| STAT_STANDLUEFTUNG | unsigned char | Status Standlüftung. Siehe Tabelle TAB_DWA_STANDLUEFTUNG |
| STAT_STANDLUEFTUNG_TEXT | string | Status Standlüftung table TAB_DWA_STANDLUEFTUNG |
| STAT_STANDKLIMA | unsigned char | Status Standklima. Siehe Tabelle TAB_DWA_STANDKLIMA |
| STAT_STANDKLIMA_TEXT | string | Status Standklima table TAB_DWA_STANDKLIMA |
| STAT_STANDHEIZUNG | unsigned char | Status Standheizung Siehe Tabelle TAB_DWA_STANDHEIZUNG |
| STAT_STANDHEIZUNG_TEXT | string | Status Standheizung Siehe Tabelle TAB_DWA_STANDHEIZUNG |
| STAT_TEMP_INNEN_WERT | char | Innentemperatur (-40°C / +85°C) |
| STAT_TEMP_INNEN_EINH | string | Innentemperatur (-40°C / +85°C) |
| STAT_TEMP_AUSSEN_WERT | char | Aussentemperatur (-40°C / +85°C) |
| STAT_TEMP_AUSSEN_EINH | string | Aussentemperatur (-40°C / +85°C) |
| STAT_JAHR_WERT | unsigned char | Jahr |
| STAT_JAHR_EINH | string | Jahr |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_MONAT_EINH | string | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_TAG_EINH | string | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_STUNDE_EINH | string | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| STAT_MINUTE_EINH | string | Minute |
| STAT_KILOMETER_WERT | unsigned long | Kilometerstand |
| STAT_KILOMETER_EINH | string | Kilometerstand |
| STAT_KLAPPENKONTAKT_FAT | unsigned char | Zustand Klappenkontakt FAhrerTür Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_FAT_TEXT | string | Zustand Klappenkontakt FAhrerTür Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_BFT | unsigned char | Zustand Klappenkontakt BeiFahrerTür. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_BFT_TEXT | string | Zustand Klappenkontakt BeiFahrerTür. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_FATH | unsigned char | Zustand Klappenkontakt FAhrerTür Hinten. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_FATH_TEXT | string | Zustand Klappenkontakt FAhrerTür Hinten. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_BFTH | unsigned char | Zustand Klappenkontakt BeiFahrerTür Hinten. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_BFTH_TEXT | string | Zustand Klappenkontakt BeiFahrerTür Hinten. Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_HECKKLAPPE | unsigned char | Zustand Klappenkontakt Heckklappe Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_HECKKLAPPE_TEXT | string | Zustand Klappenkontakt Heckklappe Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_HECKSCHEIBE | unsigned char | Zustand Klappenkontakt Heckscheibe Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_HECKSCHEIBE_TEXT | string | Zustand Klappenkontakt Heckscheibe Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_MOTORHAUBE | unsigned char | Zustand Klappenkontakt Motorhaube Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_KLAPPENKONTAKT_MOTORHAUBE_TEXT | string | Zustand Klappenkontakt Motorhaube Siehe Tabelle TAB_DWA_KLAPPENKONTAKT |
| STAT_SINEVOLTAGE_WERT | unsigned char | Spannungsueberwachung |
| STAT_SINEVOLTAGE_EINH | string | Spannungsueberwachung |
| STAT_DWA_INTERN_HECKKLAPPE | unsigned char | Heckklappe verriegelt? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_HECKKLAPPE_TEXT | string | Heckklappe verriegelt? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_HECKSCHEIBE | unsigned char | Heckscheibe verriegelt? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_HECKSCHEIBE_TEXT | string | Heckscheibe verriegelt? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_ABWAHL_NG_US | unsigned char | NeigungsGeber und UltraschallSensoren durch Funkschlüssel deaktiviert? Siehe Tabelle TAB_DWA_PRUEFUNG_INV |
| STAT_DWA_INTERN_ABWAHL_NG_US_TEXT | string | NeigungsGeber und UltraschallSensoren durch Funkschlüssel deaktiviert? Siehe Tabelle TAB_DWA_PRUEFUNG_INV |
| STAT_DWA_INTERN_DWA | unsigned char | DWA geschärft? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_DWA_TEXT | string | DWA geschärft? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_PANIKALARM | unsigned char | Panik Alarm ausgelöst? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_DWA_INTERN_PANIKALARM_TEXT | string | Panik Alarm ausgelöst? Siehe Tabelle TAB_DWA_PRUEFUNG |
| STAT_REFERENZIERUNG_MOTORHAUBE | unsigned char | Status Referenzierung Motorhaube Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_MOTORHAUBE_TEXT | string | Status Referenzierung Motorhaube Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_FAT | unsigned char | Status Referenzierung FAhrerTür. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_FAT_TEXT | string | Status Referenzierung FAhrerTür. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_BFT | unsigned char | Status Referenzierung BeiFahrerTür. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_BFT_TEXT | string | Status Referenzierung BeiFahrerTür. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_FATH | unsigned char | Status Referenzierung FAhrerTür Hinten. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_FATH_TEXT | string | Status Referenzierung FAhrerTür Hinten. Siehe Tabelle TAB_DWA_REFERENZIERUNG |
| STAT_REFERENZIERUNG_BFTH | unsigned char | Status Referenzierung BeiFahrerTür Hinten Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_BFTH_TEXT | string | Status Referenzierung BeiFahrerTür Hinten Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_HECKKLAPPE | unsigned char | Status Referenzierung Heckklappe. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_HECKKLAPPE_TEXT | string | Status Referenzierung Heckklappe table TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_HECKSCHEIBE | unsigned char | Status Referenzierung Heckscheibe Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_HECKSCHEIBE_TEXT | string | Status Referenzierung Heckscheibe Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_LEITUNG | unsigned char | Status Referenzierung Leitungsüberwachung. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_LEITUNG_TEXT | string | Status Referenzierung Leitungsüberwachung. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_USIS | unsigned char | Status Referenzierung USIS. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_STAT_USIS_TEXT | string | Status Referenzierung USIS. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_NGS | unsigned char | Status Referenzierung NGS. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_NGS_TEXT | string | Status Referenzierung NGS. Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_OBD_HIGH_SPEED_CAN | unsigned char | Status Referenzierung high speed CAN Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_OBD_HIGH_SPEED_CAN_TEXT | string | Status Referenzierung high speed CAN Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_OBD_DIAGNOSE | unsigned char | Status Referenzierung Diagnose Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_REFERENZIERUNG_OBD_DIAGNOSE_TEXT | string | Status Referenzierung Diagnose Siehe Tabelle TAB_DWA REFERENZIERUNG |
| STAT_UEBERWACHUNG_MOTORHAUBE | unsigned char | Status Überwachung MotorHaube Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_MOTORHAUBE_TEXT | string | Status Überwachung MotorHaube Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_FAT | unsigned char | Status Überwachung FAhrerTür Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_FAT_TEXT | string | Status Überwachung FAhrerTür Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_BFT | unsigned char | Status Überwachung BeiFahrerTür. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_BFT_TEXT | string | Status Überwachung BeiFahrerTür. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_FATH | unsigned char | Status Überwachung FAhrerTür Hinten. Siehe Table TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_FATH_TEXT | string | Status Überwachung FAhrerTür Hinten. Siehe Table TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_BFTH | unsigned char | Status Überwachung BeiFahrerTür Hinten Siehe Table TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_BFTH_TEXT | string | Status Überwachung BeiFahrerTür Hinten Siehe Table TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_HECKKLAPPE | unsigned char | Status Überwachung Heckklappe. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_HECKKLAPPE_TEXT | string | Status Überwachung Heckklappe. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_HECKSCHEIBE | unsigned char | Status Überwachung Heckscheibe. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_HECKSCHEIBE_TEXT | string | Status Überwachung Heckscheibe. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_LEITUNG | unsigned char | Status Überwachung Leitungsüberwachung. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_LEITUNG_TEXT | string | Status Überwachung Leitungsüberwachung. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_USIS | unsigned char | Status Überwachung USIS. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_STAT_USIS_TEXT | string | Status Überwachung USIS. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_NGS | unsigned char | Status Überwachung NGS. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_NGS_TEXT | string | Status Überwachung NGS. Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_OBD_HIGH_SPEED_CAN | unsigned char | Status Überwachung OBD high speed CAN Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_OBD_HIGH_SPEED_CAN_TEXT | string | Status Überwachung OBD high speed CAN Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_OBD_DIAGNOSE | unsigned char | Status Überwachung OBD Diagnose Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_UEBERWACHUNG_OBD_DIAGNOSE_TEXT | string | Status Überwachung OBD Diagnose Siehe Tabelle TAB_DWA_UEBERWACHUNG |
| STAT_BLOWER | unsigned char | Status Gebläse table TAB_DWA_STATUS_GEBLAESE |
| STAT_BLOWER_TEXT | string | Status Gebläse table TAB_DWA_STATUS_GEBLAESE |
| STAT_RESTWAERME_FUNKTION | unsigned char | Status Restwärme Funktion table TAB_DWA_STATUS_RESTWAERME |
| STAT_RESTWAERME_FUNKTION_TEXT | string | Status Restwärmefunktion table TAB_DWA_STATUS_RESTWAERME |
| STAT_OBD_HIGH_SPEED_CAN | unsigned char | Status OBD High speed CAN table TAB_DWA_STATUS_OBD_HIGH_SPEED_CAN |
| STAT_OBD_HIGH_SPEED_CAN_TEXT | string | Status OBD High speed CAN table TAB_DWA_STATUS_OBD_HIGH_SPEED_CAN |
| STAT_OBD_DIAGNOSE | unsigned char | Status OBD Diagnose table TAB_DWA_STATUS_OBD_DIAGNOSE |
| STAT_OBD_DIAGNOSE_TEXT | string | Status OBD Diagnose table TAB_DWA_STATUS_OBD_DIAGNOSE |
| STAT_USIS_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| STAT_USIS_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| STAT_USIS_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| STAT_USIS_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| STAT_USIS_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| STAT_USIS_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| STAT_USIS_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total number of doppler analysis (both channels, in the activation period) |
| STAT_USIS_TOTAL_ECHO_ANALYSIS | unsigned long | Total number of echo analysis (in the activation period) |
| STAT_USIS_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Echo time (in the activation period) |
| STAT_USIS_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Echo time (in the activation period) |
| STAT_USIS_ECHO_DELTA | unsigned char | echo delta (actual channel) |
| STAT_USIS_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | maximum drift from echo delta (actual channel) zone: 0 = near 1 = far Bit7 |
| STAT_USIS_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | maximum drift from echo delta (actual channel) zone: 0 = near 1 = far Bit7 |
| STAT_USIS_ECHO_DELTA_DRIFT_MAX_DATA | unsigned char | maximum drift from echo delta (actual channel) data Bit6..Bit0 |
| STAT_USIS_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned long | maximum drift from echo delta (actual channel) data in V |
| STAT_USIS_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in V |
| STAT_USIS_ECHO_DELTA_NUM_ECHO_SAMPLES_ZONE_NEAR | unsigned char | Number of echo samples over echo delta (actual channel) zone near Bit7, Bit6, Bit5, Bit4 |
| STAT_USIS_ECHO_DELTA_NUM_ECHO_SAMPLES_ZONE_FAR | unsigned char | Number of echo samples over echo delta (actual channel) zone far Bit3, Bit2, Bit1, Bit0 |
| STAT_USIS_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| STAT_USIS_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| STAT_USIS_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| STAT_USIS_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| STAT_USIS_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| STAT_USIS_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| STAT_USIS_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| STAT_USIS_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| STAT_USIS_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| STAT_USIS_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _USIS_REQUEST | binary | Hex-Auftrag an SG |
| _USIS_RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-alarmspeicher-loeschen"></a>
### STEUERN_DWA_ALARMSPEICHER_LOESCHEN

Löscht den Alarmspeicher der Diebstahlwarnanlage JobHeaderFormat 0x6010 STEUERN_DWA_ALARMSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-panikspeicher"></a>
### STATUS_DWA_PANIKSPEICHER

Auslesen der Panikspeicher-Einträge der Diebstahlwarnlage JobHeaderFormat 0x6011 STATUS_DWA_PANIKSPEICHER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PANIK_ANZAHL | unsigned char | Anzahl der Panikspeichereinträge |
| STAT_PANIK_ANZAHL_TEXT | string | Anzahl der Panikspeichereinträge |
| STAT_JAHR_WERT | unsigned char | Jahr |
| STAT_JAHR_EINH | string | Jahr |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_MONAT_EINH | string | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_TAG_EINH | string | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_STUNDE_EINH | string | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| STAT_MINUTE_EINH | string | Minute |
| STAT_KILOMETER_WERT | unsigned long | Kilometerstand |
| STAT_KILOMETER_EINH | string | Kilometerstand |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-panikspeicher-loeschen"></a>
### STEUERN_DWA_PANIKSPEICHER_LOESCHEN

Löscht den Panikspeicher der Diebstahlwarnanlage JobHeaderFormat 0x6011 STEUERN_DWA_PANIKSPEICHER_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dwa-deaktivierung-irs-ng"></a>
### STATUS_DWA_DEAKTIVIERUNG_IRS_NG

Auslesen der Deaktivierungsspeicher-Einträge für IRS und NG JobHeaderFormat 0x6017 STATUS_DWA_DEAKTIVIERUNG_IRS_NG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IRS_NG_DEAKTIVIERUNG_ANZAHL | unsigned char | Anzahl der Deaktivierungsspeichereinträge IRS und NG |
| STAT_IRS_NG_DEAKTIVIERUNG_ANZAHL_TEXT | string | Anzahl der Deaktivierungsspeichereinträge IRS und NG |
| STAT_JAHR_WERT | unsigned int | Jahr |
| STAT_JAHR_EINH | string | Jahr |
| STAT_MONAT_WERT | unsigned char | Monat |
| STAT_MONAT_EINH | string | Monat |
| STAT_TAG_WERT | unsigned char | Tag |
| STAT_TAG_EINH | string | Tag |
| STAT_STUNDE_WERT | unsigned char | Stunde |
| STAT_STUNDE_EINH | string | Stunde |
| STAT_MINUTE_WERT | unsigned char | Minute |
| STAT_MINUTE_EINH | string | Minute |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-deaktivierung-irs-ng-loeschen"></a>
### STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN

Löscht den Deaktivierungsspeicher des IRS und NG JobHeaderFormat 0x6016 STEUERN_DWA_DEAKTIVIERUNG_IRS_NG_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-shd-esh-denormierungs-logger-lesen"></a>
### STATUS_SHD_ESH_DENORMIERUNGS_LOGGER_LESEN

Umsetzung: MT  STATUS_SHD_ESH_DENORMIERUNGS_LOGGER_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHD_DENORM_ZAEHLER_WERT | unsigned char | Die Denormierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_SHD_DENORM_ZAEHLER_EINH | string | Die Denormierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_SHD_DENORM_1_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_1_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_1_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_1_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_1_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_1_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_2_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_2_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_2_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_2_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_2_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_2_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_3_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_3_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_3_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_3_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_3_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_3_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_4_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_4_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_4_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_4_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_4_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_4_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_5_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_5_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_SHD_DENORM_5_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_5_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_SHD_DENORM_5_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_SHD_DENORM_5_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_ZAEHLER_WERT | unsigned char | Die Denormierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_ESH_DENORM_ZAEHLER_EINH | string | Die Denormierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_ESH_DENORM_1_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_1_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_1_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_1_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_1_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_1_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_2_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_2_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_2_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_2_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_2_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_2_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_3_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_3_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_3_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_3_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_3_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_3_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_4_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_4_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_4_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_4_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_4_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_4_KM_EINH | string | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_5_URSACHE_NR | unsigned char | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_5_URSACHE_NR_TEXT | string | Denormierungsursache, siehe Tabelle TAB_SHD_ESH_DENORM_URS |
| STAT_ESH_DENORM_5_POS_HALL_WERT | unsigned int | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_5_POS_HALL_EINH | string | Angabe der Hallinkremente (2-Byte) |
| STAT_ESH_DENORM_5_KM_WERT | unsigned long | Kilometerstand (3-Byte) |
| STAT_ESH_DENORM_5_KM_EINH | string | Kilometerstand (3-Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-shd-esh-denormierungs-logger-loeschen"></a>
### STEUERN_SHD_ESH_DENORMIERUNGS_LOGGER_LOESCHEN

Löscht die Denormierungslogger von Schiebedach und elektrischer Schiebehimmel Umsetzung: MT  STEUERN_SHD_ESH_DENORMIERUNGS_LOGGER_LOESCHEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | unsigned char | Mögliche Parameter: (entsprechend table TAB_SHD_ESH) 0x00 kein Element löschen 0xA1 SHD löschen 0xA2 ESH löschen 0xB0 SHD + ESH löschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-shd-esh-motorstop-logger-lesen"></a>
### STATUS_SHD_ESH_MOTORSTOP_LOGGER_LESEN

Liest die aufgezeichneten Daten des Loggers für Abbruch Motorlauf. Die letzten 10 Ereignisse werden für jeden Ort gespeichert Umsetzung: MT  STATUS_SHD_ESH_MOTORSTOP_LOGGER_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHD_STOPREASON_1_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_1_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_2_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_2_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_3_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_3_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_4_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_4_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_5_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_5_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_6_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_6_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_7_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_7_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_8_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_8_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_9_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_9_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_10_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_SHD_STOPREASON_10_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_1_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_1_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_2_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_2_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_3_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_3_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_4_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_4_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_5_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_5_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_6_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_6_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_7_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_7_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_8_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_8_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_9_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_9_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_10_NR | unsigned char | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| STAT_ESH_STOPREASON_10_NR_TEXT | string | Grund des Motorstops siehe Tabelle TAB_FH_SHD_ESH_MOTORSTOPREASON |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-shd-esh-motorstop-logger-loeschen"></a>
### STEUERN_SHD_ESH_MOTORSTOP_LOGGER_LOESCHEN

Löscht den Logger für Abbruch / Ende Motorlauf Umsetzung: MT  STEUERN_SHD_ESH_MOTORSTOP_LOGGER_LOESCHEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | unsigned char | Mögliche Parameter: (entsprechend table TAB_SHD_ESH) 0x00 kein Element löschen 0xA1 SHD löschen 0xA2 ESH löschen 0xB0 SHD + ESH löschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-shd-esh-reversier-logger-lesen"></a>
### STATUS_SHD_ESH_REVERSIER_LOGGER_LESEN

Auslesen der Reversierlogger Schiebedach und elektrischer Schiebehimmel Umsetzung: MT  STATUS_SHD_ESH_REVERSIER_LOGGER_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHD_REVERSIEREN_ZAEHLER_WERT | unsigned char | Die Reversierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_SHD_REVERSIEREN_ZAEHLER_EINH | string | Die Reversierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_SHD_REVERSIEREN_1_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_1_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_1_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_1_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_1_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_1_KM_EINH | string | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_1_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_1_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_1_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_1_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_1_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_1_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_2_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_2_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_2_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_2_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_2_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_2_KM_EINH | string | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_2_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_2_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_2_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb)  in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_2_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb)  in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_2_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_2_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_3_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_3_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_3_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_3_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_3_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_3_KM_EINH | string | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_3_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_3_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_3_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb)  in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_3_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb)  in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_3_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_3_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_4_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_4_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_4_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_4_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_4_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_4_KM_EINH | string | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_4_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_4_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_4_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_4_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_4_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_4_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_5_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_5_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_SHD_REVERSIEREN_5_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_5_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_SHD_REVERSIEREN_5_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_5_KM_EINH | string | Angabe Kilometerstand |
| STAT_SHD_REVERSIEREN_5_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_5_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_SHD_REVERSIEREN_5_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_5_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_SHD_REVERSIEREN_5_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_REVERSIEREN_5_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_ZAEHLER_WERT | unsigned char | Die Reversierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_ESH_REVERSIEREN_ZAEHLER_EINH | string | Die Reversierhäufigkeit wird bei jedem Reversier inkrementiert |
| STAT_ESH_REVERSIEREN_1_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_1_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_1_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_1_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_1_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_1_KM_EINH | string | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_1_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_1_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_1_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_1_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_1_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_1_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_2_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_2_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_2_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_2_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_2_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_2_KM_EINH | string | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_2_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_2_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_2_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_2_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_2_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_2_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_3_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_3_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_3_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_3_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_3_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_3_KM_EINH | string | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_3_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_3_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_3_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_3_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_3_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_3_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_4_URSACHE_NR | unsigned char | Reversier-Ursache (1Byte)  Liste erstellen mit vereinheitlichten Werten und nachfolgend einem Bereich der vom Lieferanten belegt werden kann. Tabellenname und Tabelle muss vom Lieferant festgelegt und befüllt werden |
| STAT_ESH_REVERSIEREN_4_URSACHE_NR_TEXT | string | Reversier-Ursache (1Byte)  Liste erstellen mit vereinheitlichten Werten und nachfolgend einem Bereich der vom Lieferanten belegt werden kann. Tabellenname und Tabelle muss vom Lieferant festgelegt und befüllt werden |
| STAT_ESH_REVERSIEREN_4_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_4_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_4_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_4_KM_EINH | string | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_4_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_4_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_4_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_4_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_4_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_4_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_5_URSACHE_NR | unsigned char | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_5_URSACHE_NR_TEXT | string | Reversierursache, siehe Tabelle TAB_SHD_ESH_REVERSIER_URS |
| STAT_ESH_REVERSIEREN_5_POS_HALL_WERT | unsigned int | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_5_POS_HALL_EINH | string | Angabe Hallinkremente |
| STAT_ESH_REVERSIEREN_5_KM_WERT | unsigned long | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_5_KM_EINH | string | Angabe Kilometerstand |
| STAT_ESH_REVERSIEREN_5_ATEMP_WERT | char | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_5_ATEMP_EINH | string | Aussentemperatur (aus CAN-Signal) |
| STAT_ESH_REVERSIEREN_5_SPANNUNG_WERT | unsigned char | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_5_SPANNUNG_EINH | string | Betriebsspannung (Ausgang zu Antrieb) in 0,1 Volt-Schritten |
| STAT_ESH_REVERSIEREN_5_GESCHWINDIGKEIT_WERT | unsigned char | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_REVERSIEREN_5_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-shd-esh-reversier-logger-loeschen"></a>
### STEUERN_SHD_ESH_REVERSIER_LOGGER_LOESCHEN

Löscht die Logger von Schiebedach und / oder elektrsicher Schiebehimmel Umsetzung: MT  STEUERN_SHD_ESH_REVERSIER_LOGGER_LOESCHEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | unsigned char | Mögliche Parameter: (entsprechend table TAB_SHD_ESH) 0x00 kein Element löschen 0xA1 SHD löschen 0xA2 ESH löschen 0xB0 SHD + ESH löschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-resetcounter"></a>
### _READ_RESETCOUNTER

Read resetcounter JobHeaderFormat 0x600D _READ_RESETCOUNTER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| POWER_ON_RESET_COUNT | unsigned int | Value of Power-On resetcounter |
| WATCHDOG_RESET_COUNT | unsigned int | Value of Watchdog resetcounter |
| SLOT_1_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_1_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_1_YEAR | unsigned char | Year for reset |
| SLOT_1_MONTH | unsigned char | Month for reset |
| SLOT_1_DAY | unsigned char | Day for reset |
| SLOT_1_HOUR | unsigned char | Hour for reset |
| SLOT_1_MINUTE | unsigned char | Minute for reset |
| SLOT_1_MILAGE | unsigned long | Milage for reset |
| SLOT_2_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_2_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_2_YEAR | unsigned char | Year for reset |
| SLOT_2_MONTH | unsigned char | Month for reset |
| SLOT_2_DAY | unsigned char | Day for reset |
| SLOT_2_HOUR | unsigned char | Hour for reset |
| SLOT_2_MINUTE | unsigned char | Minute for reset |
| SLOT_2_MILAGE | unsigned long | Milage for reset |
| SLOT_3_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_3_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_3_YEAR | unsigned char | Year for reset |
| SLOT_3_MONTH | unsigned char | Month for reset |
| SLOT_3_DAY | unsigned char | Day for reset |
| SLOT_3_HOUR | unsigned char | Hour for reset |
| SLOT_3_MINUTE | unsigned char | Minute for reset |
| SLOT_3_MILAGE | unsigned long | Milage for reset |
| SLOT_4_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_4_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_4_YEAR | unsigned char | Year for reset |
| SLOT_4_MONTH | unsigned char | Month for reset |
| SLOT_4_DAY | unsigned char | Day for reset |
| SLOT_4_HOUR | unsigned char | Hour for reset |
| SLOT_4_MINUTE | unsigned char | Minute for reset |
| SLOT_4_MILAGE | unsigned long | Milage for reset |
| SLOT_5_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_5_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_5_YEAR | unsigned char | Year for reset |
| SLOT_5_MONTH | unsigned char | Month for reset |
| SLOT_5_DAY | unsigned char | Day for reset |
| SLOT_5_HOUR | unsigned char | Hour for reset |
| SLOT_5_MINUTE | unsigned char | Minute for reset |
| SLOT_5_MILAGE | unsigned long | Milage for reset |
| SLOT_6_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_6_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_6_YEAR | unsigned char | Year for reset |
| SLOT_6_MONTH | unsigned char | Month for reset |
| SLOT_6_DAY | unsigned char | Day for reset |
| SLOT_6_HOUR | unsigned char | Hour for reset |
| SLOT_6_MINUTE | unsigned char | Minute for reset |
| SLOT_6_MILAGE | unsigned long | Milage for reset |
| SLOT_7_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_7_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_7_YEAR | unsigned char | Year for reset |
| SLOT_7_MONTH | unsigned char | Month for reset |
| SLOT_7_DAY | unsigned char | Day for reset |
| SLOT_7_HOUR | unsigned char | Hour for reset |
| SLOT_7_MINUTE | unsigned char | Minute for reset |
| SLOT_7_MILAGE | unsigned long | Milage for reset |
| SLOT_8_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_8_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_8_YEAR | unsigned char | Year for reset |
| SLOT_8_MONTH | unsigned char | Month for reset |
| SLOT_8_DAY | unsigned char | Day for reset |
| SLOT_8_HOUR | unsigned char | Hour for reset |
| SLOT_8_MINUTE | unsigned char | Minute for reset |
| SLOT_8_MILAGE | unsigned long | Milage for reset |
| SLOT_9_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_9_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_9_YEAR | unsigned char | Year for reset |
| SLOT_9_MONTH | unsigned char | Month for reset |
| SLOT_9_DAY | unsigned char | Day for reset |
| SLOT_9_HOUR | unsigned char | Hour for reset |
| SLOT_9_MINUTE | unsigned char | Minute for reset |
| SLOT_9_MILAGE | unsigned long | Milage for reset |
| SLOT_10_RESET_REASON | unsigned char | Value of reset reason |
| SLOT_10_RESET_REASON_TEXT | string | Value of reset reason table _TAB_RESET_REASON TEXT |
| SLOT_10_YEAR | unsigned char | Year for reset |
| SLOT_10_MONTH | unsigned char | Month for reset |
| SLOT_10_DAY | unsigned char | Day for reset |
| SLOT_10_HOUR | unsigned char | Hour for reset |
| SLOT_10_MINUTE | unsigned char | Minute for reset |
| SLOT_10_MILAGE | unsigned long | Milage for reset |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-reset-resetcounter"></a>
### _RESET_RESETCOUNTER

Reset resetcounter JobHeaderFormat 0x600E _RESET_RESETCOUNTER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-dwa-trigger-status"></a>
### _DWA_TRIGGER_STATUS

Status Digital Input/Output JobHeaderFormat 0x600F _DWA_TRIGGER_STATUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MH_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| MH_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| FT_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| FT_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| BFT_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| BFT_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| FTH_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| FTH_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| BFTH_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| BFTH_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| HK_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| HK_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| HS_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| HS_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| VORHALT_TUER_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| VORHALT_TUER_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| LEITUNGSUEBERWACHUNG_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| LEITUNGSUEBERWACHUNG_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| EIGENUEBERWACHUNG_SINE_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| EIGENUEBERWACHUNG_SINE_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| USIS_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| USIS_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| NGS_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| NGS_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| AUTHENTISIERUNG_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| AUTHENTISIERUNG_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| OBD_CAN_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| OBD_CAN_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| OBD_DIAG_ID | unsigned char | table _TAB_DWA_TRIGGER_STATUS ID |
| OBD_DIAG_TEXT | string | table _TAB_DWA_TRIGGER_STATUS TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-usis-serial-io"></a>
### _WRITE_USIS_SERIAL_IO

Status Analog Input/Output JobHeaderFormat 0xF500 _WRITE_USIS_SERIAL_IO

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINE | unsigned char | Select routine subfunction: 0x01  start routine 0x02  stop routine 0x03  request routine |
| MODE | unsigned char | Select USIS-mode 0x01 echo mode 0x02 doppler mode 0x03 functional Logger Only with subfunction 0x01 start routine |
| ACTIVATION | unsigned char | Select Activation-mode 0x00 auto 0x01 normal 0x02 open windows 0x03 heater on Only with subfunction 0x01 start routine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | unsigned char | Only with subfunction 0x03 request routine table _TAB_SERIAL_INTERFACE TEXT |
| STAT_MODE | unsigned char | Only with subfunction 0x03 request routine table _TAB_USIS_MODE TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-selftests-result"></a>
### _USIS_DATA_SELFTESTS_RESULT

Status USIS selftest results JobHeaderFormat 0x6020 _USIS_DATA_SELFTESTS_RESULT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ULTRASONIC_SENSOR_DRIVER | string | Result of ultrasonic sensor table _TAB_USIS_SELFTEST_RESULT TEXT |
| RX_SENSOR_CHANNEL_A | string | Result of RX sensor channel A table _TAB_USIS_SELFTEST_RESULT TEXT |
| RX_SENSOR_CHANNEL_B | string | Result of RX sensor channel B table _TAB_USIS_SELFTEST_RESULT TEXT |
| TX_SENSOR | string | Result of TX sensor table _TAB_USIS_SELFTEST_RESULT TEXT |
| SHUNT_TEST | string | Result of shunt test table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_ECHO_A | string | Result of analog chain echo A table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_ECHO_B | string | Result of analog chain echo B table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_DOPPLER_A_0 | string | Result of analog chain doppler A - 0 table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_DOPPLER_A_90 | string | Result of analog chain doppler A - 90 table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_DOPPLER_B_0 | string | Result of analog chain doppler B - 0 table _TAB_USIS_SELFTEST_RESULT TEXT |
| ANALOG_CHAIN_DOPPLER_B_90 | string | Result of analog chain doppler B - 90 table _TAB_USIS_SELFTEST_RESULT TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-totalarmcounter-read"></a>
### _USIS_DATA_TOTALARMCOUNTER_READ

Status USIS total alarm counter JobHeaderFormat 0x6021 _USIS_DATA_TOTALARMCOUNTER_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TOTAL_ALARM_COUNTER_CHANNEL_A | unsigned char | Total alarmcounter channel A |
| TOTAL_ALARM_COUNTER_CHANNEL_B | unsigned char | Total alarmcounter channel B |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-alarmmemory-read"></a>
### _USIS_DATA_ALARMMEMORY_READ

Status USIS alarm memory JobHeaderFormat 0x6022 _USIS_DATA_ALARMMEMORY_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SLOT_1_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| SLOT_1_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| SLOT_1_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| SLOT_1_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| SLOT_1_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| SLOT_1_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| SLOT_1_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total doppler analysis |
| SLOT_1_TOTAL_ECHO_ANALYSIS | unsigned long | Total echo analysis |
| SLOT_1_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Total echo analysis |
| SLOT_1_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Total echo analysis |
| SLOT_1_ECHO_DELTA | unsigned char | Echo delta |
| SLOT_1_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_1_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_1_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned long | maximum drift from echo delta (actual channel) data in mV |
| SLOT_1_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in mV |
| SLOT_1_ECHO_DELTA_NUM_ECHO_SAMPLES | unsigned char | Number echo samples over echo delta |
| SLOT_1_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| SLOT_1_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| SLOT_1_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_1_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_1_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| SLOT_1_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| SLOT_1_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| SLOT_1_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| SLOT_1_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| SLOT_1_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| SLOT_2_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| SLOT_2_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| SLOT_2_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| SLOT_2_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| SLOT_2_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| SLOT_2_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| SLOT_2_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total doppler analysis |
| SLOT_2_TOTAL_ECHO_ANALYSIS | unsigned long | Total echo analysis |
| SLOT_2_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Total echo analysis |
| SLOT_2_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Total echo analysis |
| SLOT_2_ECHO_DELTA | unsigned char | Echo delta |
| SLOT_2_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_2_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_2_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned long | maximum drift from echo delta (actual channel) data in mV |
| SLOT_2_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in mV |
| SLOT_2_ECHO_DELTA_NUM_ECHO_SAMPLES | unsigned char | Number echo samples over echo delta |
| SLOT_2_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| SLOT_2_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| SLOT_2_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_2_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_2_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| SLOT_2_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| SLOT_2_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| SLOT_2_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| SLOT_2_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| SLOT_2_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| SLOT_3_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| SLOT_3_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| SLOT_3_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| SLOT_3_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| SLOT_3_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| SLOT_3_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| SLOT_3_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total doppler analysis |
| SLOT_3_TOTAL_ECHO_ANALYSIS | unsigned long | Total echo analysis |
| SLOT_3_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Total echo analysis |
| SLOT_3_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Total echo analysis |
| SLOT_3_ECHO_DELTA | unsigned char | Echo delta |
| SLOT_3_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_3_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_3_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned char | maximum drift from echo delta (actual channel) data in mV |
| SLOT_3_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in mV |
| SLOT_3_ECHO_DELTA_NUM_ECHO_SAMPLES | unsigned char | Number echo samples over echo delta |
| SLOT_3_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| SLOT_3_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| SLOT_3_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_3_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_3_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| SLOT_3_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| SLOT_3_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| SLOT_3_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| SLOT_3_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| SLOT_3_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| SLOT_4_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| SLOT_4_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| SLOT_4_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| SLOT_4_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| SLOT_4_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| SLOT_4_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| SLOT_4_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total doppler analysis |
| SLOT_4_TOTAL_ECHO_ANALYSIS | unsigned long | Total echo analysis |
| SLOT_4_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Total echo analysis |
| SLOT_4_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Total echo analysis |
| SLOT_4_ECHO_DELTA | unsigned char | Echo delta |
| SLOT_4_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_4_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_4_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned long | maximum drift from echo delta (actual channel) data in mV |
| SLOT_4_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in mV |
| SLOT_4_ECHO_DELTA_NUM_ECHO_SAMPLES | unsigned char | Number echo samples over echo delta |
| SLOT_4_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| SLOT_4_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| SLOT_4_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_4_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_4_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| SLOT_4_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| SLOT_4_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| SLOT_4_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| SLOT_4_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| SLOT_4_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| SLOT_5_ALARM_TYPE_SOURCE_ID | unsigned char | Alarm source as value table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE WERT |
| SLOT_5_ALARM_TYPE_SOURCE_TEXT | string | Alarm source as Text table _TAB_USIS_ALARM_TYPE_ALARM_SOURCE TEXT |
| SLOT_5_ALARM_TYPE_ACTIVATION_MODE_ID | unsigned char | Activation mode as value table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE WERT |
| SLOT_5_ALARM_TYPE_ACTIVATION_MODE_TEXT | string | Activation mode as Text table _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE TEXT |
| SLOT_5_THERMAL_ENVIRONMENT_ID | unsigned char | Thermal environment as value table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| SLOT_5_THERMAL_ENVIRONMENT_TEXT | string | Thermal environment as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| SLOT_5_TOTAL_DOPPLER_ANALYSIS | unsigned int | Total doppler analysis |
| SLOT_5_TOTAL_ECHO_ANALYSIS | unsigned long | Total echo analysis |
| SLOT_5_TOTAL_ECHO_ANALYSIS_TIME_200MS | string | Total echo analysis |
| SLOT_5_TOTAL_ECHO_ANALYSIS_TIME_300MS | string | Total echo analysis |
| SLOT_5_ECHO_DELTA | unsigned char | Echo delta |
| SLOT_5_ECHO_DELTA_DRIFT_MAX_ZONE | unsigned char | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_5_ECHO_DELTA_DRIFT_MAX_ZONE_TEXT | string | Max drift from echo delta (actual channel)  zone: 0 = near 1 = far |
| SLOT_5_ECHO_DELTA_DRIFT_MAX_DATA_WERT | unsigned long | maximum drift from echo delta (actual channel) data in mV |
| SLOT_5_ECHO_DELTA_DRIFT_MAX_DATA_EINH | string | maximum drift from echo delta (actual channel) data in mV |
| SLOT_5_ECHO_DELTA_NUM_ECHO_SAMPLES | unsigned char | Number echo samples over echo delta |
| SLOT_5_DOPPLER_VALUES_ECHO_GAIN | unsigned char | Doppler values of echo gain Bit7, Bit6 |
| SLOT_5_DOPPLER_VALUES_ECHO_GAIN_TEXT | string | Doppler values of echo gain Bit7, Bit6 |
| SLOT_5_DOPPLER_VALUES_DOPPLER_GAIN | unsigned char | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_5_DOPPLER_VALUES_DOPPLER_GAIN_TEXT | string | Doppler values of doppler gain Bit5, Bit4 |
| SLOT_5_DOPPLER_VALUES_DOPPLER_SUB_ANALYSIS | unsigned char | Doppler values of doppler sub-analysis Bit3 to Bit0 |
| SLOT_5_DOPPLER_PEAK_VOLTAGE_MAX | unsigned int | Doppler Max peak voltage |
| SLOT_5_DOPPLER_PEAK_VOLTAGE_MAX_EINH | string | Unit of Doppler Max peak voltage (mV) |
| SLOT_5_DOPPLER_PERIOD_MAX | unsigned char | Maximum of doppler period |
| SLOT_5_DOPPLER_PERIOD_MIN | unsigned char | Minimum of doppler period |
| SLOT_5_DOPPLER_PERIOD_EINH | string | Unit of doppler period |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-echodopplercounter-read"></a>
### _USIS_DATA_ECHODOPPLERCOUNTER_READ

Status echo-doppler-counter JobHeaderFormat 0x6023 _USIS_DATA_ECHODOPPLERCOUNTER_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECHO_COUNTER | unsigned int | Echo ticks |
| DOPPLER_COUNTER | unsigned int | Echo doppler trigger |
| ECHO_DOPPLER_HISTORY | unsigned int | History of echo doppler trigger |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-environment-read"></a>
### _USIS_DATA_ENVIRONMENT_READ

Status environment JobHeaderFormat 0x6024 _USIS_DATA_ENVIRONMENT_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ACTIVATION_ID | unsigned char | Activation ID table _TAB_USIS_DATA_ENVIRONMENT_READ_ACTIVATION WERT |
| ACTIVATION_TEXT | string | Activation as text table _TAB_USIS_DATA_ENVIRONMENT_READ_ACTIVATION TEXT |
| THERMAL_STEP_ID | unsigned char | Thermal step as ID table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB WERT |
| THERMAL_STEP_TEXT | string | Thermal step as text table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-cmd-alarmmemory-reset"></a>
### _USIS_CMD_ALARMMEMORY_RESET

Reset alarmmemory JobHeaderFormat 0x6025 _USIS_CMD_ALARMMEMORY_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-cmd-echodopplercounter-reset"></a>
### _USIS_CMD_ECHODOPPLERCOUNTER_RESET

Reset echo-doppler-counter JobHeaderFormat 0x6026 _USIS_CMD_ECHODOPPLERCOUNTER_RESET

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CHANNEL_ID | unsigned char | Channel Possible parameters (according to table _TAB_USIS_CMD_ECHODOPPLERCOUNTER_RESET) 0x01 echo counter 0x02 doppler counter 0x03 echo/doppler transitions history |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-cmd-environment-set"></a>
### _USIS_CMD_ENVIRONMENT_SET

Write the environment JobHeaderFormat 0x6027 _USIS_CMD_ENVIRONMENT_SET

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTIVATION | unsigned char | Activation Possible parameters (according to table _TAB_USIS_DATA_ENVIRONMENT_READ_ACTIVATION) 0x00  no change 0x01  Normal mode 0x02  Window or roof opened 0x03  Air condition on |
| THERMAL_STEP | unsigned char | Thermal step Possible parameters (according to table _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB) 0x00  -40°C .. -15°C 0x01  -15°C .. + 5°C 0x02  + 5°C .. +45°C 0x03  +45°C .. +65°C 0x04  +65°C .. +85°C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-anpassung-value-read"></a>
### _USIS_DATA_ANPASSUNG_VALUE_READ

Read Adaptation USIS-Data JobHeaderFormat 0x6028 _USIS_DATA_ANPASSUNG_VALUE_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSITIVITY_INDEX | unsigned char | Sensitivity index |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-data-anpassung-value-set"></a>
### _USIS_DATA_ANPASSUNG_VALUE_SET

Write Adaptation USIS-Data JobHeaderFormat 0x6029 _USIS_DATA_ANPASSUNG_VALUE_SET

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSITIVITY_INDEX | unsigned char | Sensitivity index 0x00 bis 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-usis-cmd-totalalarmcounter-reset"></a>
### _USIS_CMD_TOTALALARMCOUNTER_RESET

Reset total alarm counter JobHeaderFormat 0x602A _USIS_CMD_TOTALALARMCOUNTER_RESET

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CHANNEL | unsigned char | Channel Possible parameters (according to table _TAB_USIS_CMD_TOTALALARMCOUNTER_RESET) 0x01  A channel 0x02  B channel 0x03  both channel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-disable-dtc"></a>
### _DISABLE_DTC

reset WD JobHeaderFormat 0xF501 _DISABLE_DTC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINE | unsigned char | Select routine subfunction: 0x01  start routine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-slider-data-output"></a>
### _SLIDER_DATA_OUTPUT

reset WD JobHeaderFormat 0xF502 _SLIDER_DATA_OUTPUT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINE | unsigned char | Select routine subfunction: 0x01  start routine 0x02  stop routine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-dio"></a>
### _READ_DIO

Status Digital Input/Output JobHeaderFormat 0x6000 _READ_DIO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_DIAG_SHD_M1 | unsigned char | Status SHD motor 1 |
| STAT_I_DIAG_SHD_M2 | unsigned char | Status SHD motor 2 |
| STAT_I_DIAG_ESH_M1 | unsigned char | Status ESH motor 1 |
| STAT_I_DIAG_ESH_M2 | unsigned char | Status ESH motor 2 |
| STAT_I_SHD_HALL1 | unsigned char | Status SHD HALL-sensor 1 |
| STAT_I_SHD_HALL2 | unsigned char | Status SHD HALL-sensor 2 |
| STAT_I_ESH_HALL1 | unsigned char | Status ESH HALL-sensor 1 |
| STAT_I_ESH_HALL2 | unsigned char | Status ESH HALL-sensor 2 |
| STAT_I_PUSH_ROOF | unsigned char | Status Push-button |
| STAT_I_SLIDERA | unsigned char | Status Slider A |
| STAT_I_SLIDERC | unsigned char | Status Slider C |
| STAT_I_SLIDERD | unsigned char | Status Slider D |
| STAT_I_SLIDERF | unsigned char | Status Slider F |
| STAT_I_CONF_MINI | unsigned char | Status DWA-LED |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-dio"></a>
### _WRITE_DIO

Steuern Digital Input/Output JobHeaderFormat 0x6001 _WRITE_DIO

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINE | unsigned char | Select routine subfunction: 0x00  return control to ECU 0x03  short term adjustment |
| IDENTIFIER | unsigned char | Port 0x01  CMD_DWA_LED 0x02  CMD_OPEN_LOAD_DWA_LED 0x03  CMD_SHD_M1 0x04  CMD_SHD_M2 0x05  CMD_ESH_M1 0x06  CMD_ESH_M2 0x07  CMD_30F_SW_HALL 0x0A  CMD_TXON 0x0B  CMD_SHUNT 0x0C  CMD_TXD 12 0x0D  CMD_TXECO1 0x0E  CMD_TXECO2 0x0F  CMD_RXENA 0x10  CMD_GDOP 0x11  CMD_GH1 0x12  CMD_OPHFSUP 0x13  CMD_GH2 0x1E  CMD_CONF_VAR 0x1F  CMD_GL1 0x20  CMD_GL2 0x21  CMD_OPLFSUP table _TAB_PORT_DIO_WRITE TEXT |
| VALUE | unsigned char | Only with subfunction 0x03 ShortThermAdjust Value to set 0x00  output low 0x01  output high |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_WARNING | string | Leer, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-aio"></a>
### _READ_AIO

Status Analog Input/Output JobHeaderFormat 0x6002 _READ_AIO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_DIAG_SHD_HALL1 | unsigned int | Value of SHD Hall 1 |
| STAT_AD_DIAG_SHD_HALL2 | unsigned int | Value of SHD Hall 2 |
| STAT_AD_DIAG_ESH_HALL1 | unsigned int | Value of ESH Hall 1 |
| STAT_AD_DIAG_ESH_HALL2 | unsigned int | Value of ESH Hall 2 |
| STAT_AD_30_F27_VBF | unsigned int | Value of vBat (card voltage) |
| STAT_AD_R1PH0 | unsigned int | Value of R1PH0 |
| STAT_AD_R1PH90 | unsigned int | Value of R1PH90 |
| STAT_AD_R2PH0 | unsigned int | Value of R2PH0 |
| STAT_AD_R2PH90 | unsigned int | Value of R2PH90 |
| STAT_AD_ECO1 | unsigned int | Value of ECO1 |
| STAT_AD_ECO2 | unsigned int | Value of ECO2 |
| STAT_AD_TEMP | unsigned int | Value of TEMP |
| STAT_AD_30_F30_VBF | unsigned int | Value of VBAT_EL -&gt; Roof voltage |
| STAT_AD_CONF_VAR | unsigned int | Value of VARIANT |
| AD_US_EMITTER | unsigned int | Value of AD_US_EMITTER |
| STAT_AD_DIAG_DWA_LED | unsigned int | Value of STAT_AD_DIAG_DWA_LED |
| STAT_AD_30F_SW_HALL | unsigned int | Value of STAT_AD_30F_SW_HALL |
| STAT_AD_I_PUSH_ROOF_M | unsigned int | Value of STAT_AD_I_PUSH_ROOF_M -&gt; available only for Mini Variants |
| STAT_AD_I_SLIDERA_M | unsigned int | Value of STAT_AD_I_SLIDERA_M -&gt; available only for Mini Variants |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-fio"></a>
### _READ_FIO

Status Frequenz Input/Output JobHeaderFormat 0x6003 _READ_FIO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHD_HALL_1 | unsigned int | Value of SHD Hall 1 |
| STAT_SHD_HALL_2 | unsigned int | Value of SHD Hall 1 |
| STAT_ESH_HALL_1 | unsigned int | Value of ESH Hall 1 |
| STAT_ESH_HALL_2 | unsigned int | Value of ESH Hall 1 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-fio"></a>
### _WRITE_FIO

Steuern Frequenz Input/Output JobHeaderFormat 0x6004 _SCHREIBEN_FIO

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINE | unsigned char | Select routine subfunction: 0x00  return control to ECU 0x03  short term adjustment |
| IDENTIFIER | unsigned char | Port 0x01  PWM_SLIDER_LED 0x02  F80 table _TAB_PORT_FIO_WRITE TEXT |
| VALUE | unsigned int | Only with subfunction 0x03 ShortThermAdjust Value to set |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_WARNING | string | Leer, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-eep"></a>
### _READ_EEP

Status EEPROM JobHeaderFormat 0x6005 _READ_EEP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | unsigned int | Address of data to read 0x0000 ... 0x1FFF |
| SIZE | unsigned char | Size of data to read 1 ... 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | unsigned char | Value of data to read |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-eep"></a>
### _WRITE_EEP

Steuern EEPROM JobHeaderFormat 0x6006 _WRITE_EEP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | unsigned int | Start address of data to write 0x0000 ... 0x1FFF |
| DATA | unsigned char | Data to write |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-control-eep"></a>
### _CONTROL_EEP

Steuern EEPROM JobHeaderFormat 0x6007 _CONTROL_EEP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | unsigned char | Lock / unlock EEPROM 0x00  Unlock 0x01  Lock Default: 0x01 Lock table _TAB_SWITCH_EEP TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_WARNING | string | Leer, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-version"></a>
### _READ_VERSION

Status Version JobHeaderFormat 0x6008 _READ_VERSION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DWA_VERSION | string | Antiteft SW version |
| USIS_VERSION | string | USIS SW version |
| MOTOR_DRIVER_VERSION | string | USIS SW version |
| MOTOR_SR_CLIENT_VERSION | string | SR-client version |
| MOTOR_SR_CLIENT_DATE | string | SR-client version |
| DWA_MAJOR_VERSION | string | Antiteft SW version (major) |
| DWA_MINOR_VERSION | string | Antitheft SW version (minor) |
| DWA_PATCH_VERSION | string | Antitheft SW version (patch) |
| USIS_MAJOR_VERSION | unsigned char | USIS version (major) |
| USIS_MINOR_VERSION | unsigned char | USIS version (minor) |
| USIS_PATCH_VERSION | unsigned char | USIS version (patch) |
| MOTOR_DRIVER_MAJOR_VERSION | unsigned char | Motordriver version (major) |
| MOTOR_DRIVER_MINOR_VERSION | unsigned char | Motordriver version (minor) |
| MOTOR_DRIVER_PATCH1_VERSION | unsigned char | Motordriver version (patch1) |
| MOTOR_DRIVER_PATCH2_VERSION | unsigned char | Motordriver version (patch2) |
| MOTOR_SR_CLIENT_MAJOR_VERSION | unsigned char | SR-client version (major) |
| MOTOR_SR_CLIENT_MINOR_VERSION | unsigned char | SR-client version (minor) |
| MOTOR_SR_CLIENT_PATCH_VERSION | unsigned char | SR-client version (patch) |
| MOTOR_SR_CLIENT_DATE_DAY | unsigned char | SR-client date (day) |
| MOTOR_SR_CLIENT_DATE_MONTH | unsigned char | SR-client date (month) |
| MOTOR_SR_CLIENT_DATE_YEAR | unsigned long | SR-client date (long) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-pcb-data"></a>
### _READ_PCB_DATA

Status PCB JobHeaderFormat 0x6009 _READ_PCB_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FACTORY_DATE_YY | unsigned char | Manufacturing year |
| FACTORY_DATE_MM | unsigned char | Manufacturing month |
| FACTORY_DATE_DD | unsigned char | Manufacturing day |
| HW_VERSION | unsigned char | HW version |
| PCB_PART_REF | unsigned long | PCB Part Reference |
| PCB_SERIAL_NUMBER | unsigned long | PCB Serial number |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-pcb-data"></a>
### _WRITE_PCB_DATA

Steuern PCB JobHeaderFormat 0x600A _WRITE_PCB_DATA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FACTORY_DATE_YY | unsigned char | production date: year |
| FACTORY_DATE_MM | unsigned char | production date: month |
| FACTORY_DATE_DD | unsigned char | production date: day |
| HW_VERSION | unsigned int | HW version |
| PCB_PART_REF | unsigned long | serial number of the PCB to be set at 000 at beginning of each day |
| PCB_SERIAL_NUMBER | unsigned long | serial number of the PCB to be set at 000 at beginning of each day |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-assembly-data"></a>
### _READ_ASSEMBLY_DATA

Status assembly JobHeaderFormat 0x600B _READ_ASSEMBLY_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FACTORY_DATE_YY | string | ECUSerialNumber: year ASCII 2 bytes - expample 11 = 2011 |
| FACTORY_DATE_DDD | string | ECUSerialNumber: day of the year ASCII 3 bytes - expample "121" |
| FACTORY_LINE_SHIFT | unsigned char | ECUSerialNumber: line/shift ASCII 1 byte: code with characters with 4 shifts: A = shift 1 / line 1 B = shift 2 / line 1 C = shift 3 / line 1 D = shift 4 / line 1 E = shift 1 / line 2 |
| FACTORY_DATE_COUNTER | string | ECUSerialNumber: counter ASCII 4 byte |
| STEP_COUNTER | unsigned char | Stepp counter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-assembly-data"></a>
### _WRITE_ASSEMBLY_DATA

Steuern assembly JobHeaderFormat 0x600C _WRITE_ASSEMBLY_DATA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FACTORY_DATE_YY | string | ECUSerialNumber: year ASCII 2 bytes - expample 11 = 2011 |
| FACTORY_DATE_DDD | string | ECUSerialNumber: day of the year ASCII 3 bytes - expample "121" |
| FACTORY_LINE_SHIFT | unsigned char | ECUSerialNumber: line/shift ASCII 1 byte: code with characters with 4 shifts: A = shift 1 / line 1 B = shift 2 / line 1 C = shift 3 / line 1 D = shift 4 / line 1 E = shift 1 / line 2 |
| FACTORY_DATE_COUNTER | string | ECUSerialNumber: counter ASCII 4 byte |
| STEP_COUNTER | unsigned char | Stepp counter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-cpu-load"></a>
### _READ_CPU_LOAD

Read CPU load JobHeaderFormat 0x6030 _READ_CPU_LOAD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MAX | unsigned char | Max value of CPU load |
| MIN | unsigned char | Min value of CPU load |
| ACTUALE | unsigned char | Actuale value of CPU load |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-reset-cpu-load"></a>
### _RESET_CPU_LOAD

Reset CPU load Job HeaderFormat 0x6031 _RESET_CPU_LOAD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-valeo-write-enable"></a>
### _VALEO_WRITE_ENABLE

Enable write JobHeaderFormat 0x6032 _VALEO_WRITE_ENABLE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY | unsigned int | enable all Valeo Diag Write jobs: _WRITE_xx until reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-read-task-stack"></a>
### _READ_TASK_STACK

Read task stack JobHeaderFormat 0x6034 _READ_TASK_STACK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NO_OF_TASKS | unsigned char | No. of Task |
| TASK_ID | unsigned char | Task ID |
| TASK_TOTAL_STACK | unsigned char | Task total Stack |
| TASK_USED_STACK | unsigned char | Task used stack |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-shd-esh-bewertung-kennlinie"></a>
### STATUS_SHD_ESH_BEWERTUNG_KENNLINIE

Auslesen der gespeicherten Kennlinien/Adaptionsdaten fuer den Einklemmschutz

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | string | 0xA1: Schiebedach 0xA2: Elektrischer Schiebehimmel |
| DERIVAT | string | Entwicklungsbezeichnung F25, F56, I01 |
| BEREICH | string | Argument siehe Tabelle TAB_FH_SHD_ESH_LAGE_NR_ARG_ENTW 0x01: Ausstelllage 0x02: Schiebelage |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KENNLINIENDATEN | binary | Drehzahlwert über dem Verfahrweg |
| STAT_KENNLINIENDATEN_DATA_EINH | string | Drehzahlwert über dem Verfahrweg |
| STAT_SCHLIESSZEIT | unsigned int | Schliesszeit beim Initialisierungsvorgang. Auflösung 10ms Schritte |
| STAT_SCHLIESSZEIT_EINH | string | Schliesszeit beim Initialisierungsvorgang. Auflösung 10ms Schritte |
| STAT_BN_SPANNUNG | unsigned char | Spannung die am FH während dem Initialisieren anliegt. Auflösung 100mV Schritte |
| STAT_BN_SPANNUNG_EINH | string | Spannung die am FH während dem Initialisieren anliegt. Auflösung 100mV Schritte |
| STAT_SPIEL_WERT | unsigned char | Anzahl Hall Inkremente |
| STAT_SPIEL_EINH | string | Anzahl Hall Inkremente |
| STAT_GUELTIGKEIT | unsigned char | 0x00 Kennlinie ungültig 0x01 Kennlinie gültig |
| STAT_BEWERTUNG | unsigned char | 0x00 Kennlinie in Ordnung 0x01 Kennlinie nicht in Ordnung |
| STAT_REGELVERLETZUNG | unsigned char | zu klären |
| STAT_REGELVERLETZUNG_EINH | string | zu klären |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (134 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (203 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (181 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0X4100](#table-arg-0x4100) (2 × 12)
- [ARG_0X4101](#table-arg-0x4101) (3 × 12)
- [ARG_0X4103](#table-arg-0x4103) (1 × 12)
- [ARG_0X6013](#table-arg-0x6013) (1 × 12)
- [ARG_0X6014](#table-arg-0x6014) (1 × 12)
- [ARG_0X6015](#table-arg-0x6015) (1 × 12)
- [ARG_0XA17C](#table-arg-0xa17c) (2 × 14)
- [ARG_0XA183](#table-arg-0xa183) (3 × 14)
- [ARG_0XA184](#table-arg-0xa184) (3 × 14)
- [ARG_0XA185](#table-arg-0xa185) (2 × 14)
- [ARG_0XA186](#table-arg-0xa186) (3 × 14)
- [ARG_0XA187](#table-arg-0xa187) (2 × 14)
- [ARG_0XA188](#table-arg-0xa188) (3 × 14)
- [ARG_0XAA76](#table-arg-0xaa76) (1 × 14)
- [ARG_0XAA79](#table-arg-0xaa79) (1 × 14)
- [ARG_0XAA7B](#table-arg-0xaa7b) (6 × 14)
- [ARG_0XD17C](#table-arg-0xd17c) (1 × 12)
- [ARG_0XD17D](#table-arg-0xd17d) (1 × 12)
- [ARG_0XD17E](#table-arg-0xd17e) (3 × 12)
- [ARG_0XD19E](#table-arg-0xd19e) (2 × 12)
- [ARG_0XD1BF](#table-arg-0xd1bf) (1 × 12)
- [ARG_0XD1C1](#table-arg-0xd1c1) (1 × 12)
- [ARG_0XDCA8](#table-arg-0xdca8) (2 × 12)
- [ARG_0XDCAA](#table-arg-0xdcaa) (6 × 12)
- [ARG_0XDCB5](#table-arg-0xdcb5) (1 × 12)
- [ARG_0XDD16](#table-arg-0xdd16) (1 × 12)
- [ARG_0XF000](#table-arg-0xf000) (3 × 14)
- [ARG_6013](#table-arg-6013) (6 × 2)
- [ARG_6014](#table-arg-6014) (42 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (85 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (57 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RES_0X4100](#table-res-0x4100) (2 × 10)
- [RES_0X4101](#table-res-0x4101) (4 × 10)
- [RES_0X4103](#table-res-0x4103) (1 × 10)
- [RES_0X4107](#table-res-0x4107) (8 × 10)
- [RES_0X4108](#table-res-0x4108) (8 × 10)
- [RES_0X4109](#table-res-0x4109) (8 × 10)
- [RES_0X6012](#table-res-0x6012) (19 × 10)
- [RES_0X6013](#table-res-0x6013) (10 × 10)
- [RES_0X6014](#table-res-0x6014) (14 × 10)
- [RES_0X6015](#table-res-0x6015) (5 × 10)
- [RES_0XA17C](#table-res-0xa17c) (3 × 13)
- [RES_0XA183](#table-res-0xa183) (1 × 13)
- [RES_0XA184](#table-res-0xa184) (1 × 13)
- [RES_0XA185](#table-res-0xa185) (1 × 13)
- [RES_0XA186](#table-res-0xa186) (1 × 13)
- [RES_0XA187](#table-res-0xa187) (1 × 13)
- [RES_0XA188](#table-res-0xa188) (1 × 13)
- [RES_0XAA76](#table-res-0xaa76) (1 × 13)
- [RES_0XD180](#table-res-0xd180) (6 × 10)
- [RES_0XD192](#table-res-0xd192) (2 × 10)
- [RES_0XD196](#table-res-0xd196) (15 × 10)
- [RES_0XD1A6](#table-res-0xd1a6) (15 × 10)
- [RES_0XD1B9](#table-res-0xd1b9) (6 × 10)
- [RES_0XD1BA](#table-res-0xd1ba) (15 × 10)
- [RES_0XD1BB](#table-res-0xd1bb) (6 × 10)
- [RES_0XD1BC](#table-res-0xd1bc) (6 × 10)
- [RES_0XD1BD](#table-res-0xd1bd) (15 × 10)
- [RES_0XD1BE](#table-res-0xd1be) (27 × 10)
- [RES_0XD1C0](#table-res-0xd1c0) (27 × 10)
- [RES_0XDCA2](#table-res-0xdca2) (7 × 10)
- [RES_0XDCA8](#table-res-0xdca8) (1 × 10)
- [RES_0XDCA9](#table-res-0xdca9) (2 × 10)
- [RES_0XDCAA](#table-res-0xdcaa) (6 × 10)
- [RES_0XDCB0](#table-res-0xdcb0) (19 × 10)
- [RES_0XDCDD](#table-res-0xdcdd) (9 × 10)
- [RES_0XDD16](#table-res-0xdd16) (1 × 10)
- [RES_0XF000](#table-res-0xf000) (1 × 13)
- [SG_FUNKTIONEN](#table-sg-funktionen) (57 × 16)
- [TAB_DWA_ALARMSPEICHER](#table-tab-dwa-alarmspeicher) (21 × 2)
- [TAB_DWA_INTERN](#table-tab-dwa-intern) (22 × 2)
- [TAB_DWA_KLAPPENKONTAKT](#table-tab-dwa-klappenkontakt) (4 × 2)
- [TAB_DWA_LED](#table-tab-dwa-led) (5 × 2)
- [TAB_DWA_PRUEFUNG](#table-tab-dwa-pruefung) (3 × 2)
- [TAB_DWA_PRUEFUNG_INV](#table-tab-dwa-pruefung-inv) (3 × 2)
- [TAB_DWA_REFERENZIERUNG](#table-tab-dwa-referenzierung) (3 × 2)
- [TAB_DWA_SCHNELLTEST](#table-tab-dwa-schnelltest) (3 × 2)
- [TAB_DWA_SELBSTTEST](#table-tab-dwa-selbsttest) (4 × 2)
- [TAB_DWA_SELBSTTEST_ERG](#table-tab-dwa-selbsttest-erg) (3 × 2)
- [TAB_DWA_SINE_INTERN](#table-tab-dwa-sine-intern) (5 × 2)
- [TAB_DWA_STANDHEIZUNG](#table-tab-dwa-standheizung) (4 × 2)
- [TAB_DWA_STANDKLIMA](#table-tab-dwa-standklima) (4 × 2)
- [TAB_DWA_STANDLUEFTUNG](#table-tab-dwa-standlueftung) (4 × 2)
- [TAB_DWA_STATUS_GEBLAESE](#table-tab-dwa-status-geblaese) (3 × 2)
- [TAB_DWA_STATUS_OBD_DIAGNOSE](#table-tab-dwa-status-obd-diagnose) (3 × 2)
- [TAB_DWA_STATUS_OBD_HIGH_SPEED_CAN](#table-tab-dwa-status-obd-high-speed-can) (3 × 2)
- [TAB_DWA_STATUS_RESTWAERME](#table-tab-dwa-status-restwaerme) (3 × 2)
- [TAB_DWA_UEBERWACHUNG](#table-tab-dwa-ueberwachung) (3 × 2)
- [TAB_DWA_USIS_EMPF](#table-tab-dwa-usis-empf) (5 × 2)
- [TAB_FH_PANIKMODUS](#table-tab-fh-panikmodus) (4 × 2)
- [TAB_FH_SHD_ESH_BEWEGUNG](#table-tab-fh-shd-esh-bewegung) (10 × 2)
- [TAB_FH_SHD_ESH_EINLERNEN](#table-tab-fh-shd-esh-einlernen) (5 × 2)
- [TAB_FH_SHD_ESH_EINLERNVORGANG](#table-tab-fh-shd-esh-einlernvorgang) (14 × 2)
- [TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE](#table-tab-fh-shd-esh-emergency-panic-nr-mode) (3 × 2)
- [TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE_ARG](#table-tab-fh-shd-esh-emergency-panic-nr-mode-arg) (3 × 2)
- [TAB_FH_SHD_ESH_FREIGABE](#table-tab-fh-shd-esh-freigabe) (4 × 2)
- [TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND](#table-tab-fh-shd-esh-hall-fehlerzustand) (6 × 2)
- [TAB_FH_SHD_ESH_INIT](#table-tab-fh-shd-esh-init) (9 × 2)
- [TAB_FH_SHD_ESH_LAGE_NR](#table-tab-fh-shd-esh-lage-nr) (3 × 2)
- [TAB_FH_SHD_ESH_LAGE_NR_ARG](#table-tab-fh-shd-esh-lage-nr-arg) (2 × 2)
- [TAB_FH_SHD_ESH_LAGE_NR_ARG_ENTW](#table-tab-fh-shd-esh-lage-nr-arg-entw) (2 × 2)
- [TAB_FH_SHD_ESH_MOTORSTOPREASON](#table-tab-fh-shd-esh-motorstopreason) (22 × 2)
- [TAB_FH_SHD_ESH_MOTORTEMPERATUR](#table-tab-fh-shd-esh-motortemperatur) (4 × 2)
- [TAB_FH_SHD_ESH_MT_LIEFERANT](#table-tab-fh-shd-esh-mt-lieferant) (9 × 2)
- [TAB_FH_SHD_ESH_POSITION](#table-tab-fh-shd-esh-position) (15 × 2)
- [TAB_FH_SHD_ESH_SERVICEPOSITION](#table-tab-fh-shd-esh-serviceposition) (4 × 2)
- [TAB_FH_SHD_ESH_SFK1](#table-tab-fh-shd-esh-sfk1) (7 × 2)
- [TAB_FH_SHD_ESH_STATUS_ROUTINE](#table-tab-fh-shd-esh-status-routine) (8 × 2)
- [TAB_FH_SHD_ESH_STAT_EEPROM](#table-tab-fh-shd-esh-stat-eeprom) (3 × 2)
- [TAB_FH_SHD_ESH_TASTER_RICHTUNG](#table-tab-fh-shd-esh-taster-richtung) (6 × 2)
- [TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV](#table-tab-fh-shd-esh-thermomonitor-aktiv) (4 × 2)
- [TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV_ARG](#table-tab-fh-shd-esh-thermomonitor-aktiv-arg) (4 × 2)
- [TAB_FH_SHD_ESH_VERFAHREN](#table-tab-fh-shd-esh-verfahren) (8 × 2)
- [TAB_FH_SHD_ESH_WACHHALTEN](#table-tab-fh-shd-esh-wachhalten) (3 × 2)
- [TAB_FH_SHD_ESH_ZUSTAND_TUER](#table-tab-fh-shd-esh-zustand-tuer) (5 × 2)
- [TAB_RELAIS_NUMBER](#table-tab-relais-number) (2 × 2)
- [TAB_RELAIS_RICHTUNG](#table-tab-relais-richtung) (2 × 2)
- [TAB_SHD_ESH](#table-tab-shd-esh) (3 × 2)
- [TAB_SHD_ESH_DENORM_URS](#table-tab-shd-esh-denorm-urs) (11 × 2)
- [TAB_SHD_ESH_ENTW](#table-tab-shd-esh-entw) (3 × 2)
- [TAB_SHD_ESH_REVERSIER_URS](#table-tab-shd-esh-reversier-urs) (6 × 2)
- [TAB_SHD_ESH_STRICT](#table-tab-shd-esh-strict) (1 × 2)
- [TAB_SINE_BATT_LEVEL](#table-tab-sine-batt-level) (4 × 2)
- [TAB_ZV_ST_CLSY](#table-tab-zv-st-clsy) (9 × 2)
- [_TAB_RESET_REASON](#table-tab-reset-reason) (4 × 2)
- [_TAB_DWA_TRIGGER_STATUS](#table-tab-dwa-trigger-status) (8 × 2)
- [TAB_DWA_STATUS_FENSTER_POSITION](#table-tab-dwa-status-fenster-position) (4 × 2)
- [_TAB_USIS_MODE](#table-tab-usis-mode) (4 × 2)
- [_TAB_SERIAL_INTERFACE](#table-tab-serial-interface) (3 × 2)
- [_TAB_USIS_SELFTEST_RESULT](#table-tab-usis-selftest-result) (3 × 2)
- [_TAB_USIS_ALARM_TYPE_ALARM_SOURCE](#table-tab-usis-alarm-type-alarm-source) (5 × 2)
- [_TAB_USIS_ALARM_TYPE_ACTIVATION_MODE](#table-tab-usis-alarm-type-activation-mode) (5 × 2)
- [_TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB](#table-tab-usis-data-environment-thermal-steb) (6 × 2)
- [_TAB_USIS_DATA_ENVIRONMENT_READ_ACTIVATION](#table-tab-usis-data-environment-read-activation) (5 × 2)
- [_TAB_USIS_CMD_ECHODOPPLERCOUNTER_RESET](#table-tab-usis-cmd-echodopplercounter-reset) (3 × 2)
- [_TAB_USIS_CMD_TOTALALARMCOUNTER_RESET](#table-tab-usis-cmd-totalalarmcounter-reset) (3 × 2)
- [_TAB_USIS_ECHO_DELTA_DRIFT_ZONE](#table-tab-usis-echo-delta-drift-zone) (2 × 2)
- [_TAB_USIS_GAIN](#table-tab-usis-gain) (4 × 2)
- [_TAB_PORT_DIO_WRITE](#table-tab-port-dio-write) (21 × 2)
- [_TAB_PORT_FIO_WRITE](#table-tab-port-fio-write) (2 × 2)
- [_TAB_SWITCH_EEP](#table-tab-switch-eep) (2 × 2)

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

Dimensions: 181 rows × 2 columns

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

<a id="table-arg-0x4100"></a>
### ARG_0X4100

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | high | unsigned char | - | TAB_SHD_ESH_ENTW | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle |
| AKTION | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV_ARG | 1.0 | 1.0 | 0.0 | - | - | Auswahl Thermomonitor aktiv siehe Tabelle TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV_ARG |

<a id="table-arg-0x4101"></a>
### ARG_0X4101

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | high | unsigned char | - | TAB_SHD_ESH_ENTW | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle |
| FREIGABE_GLOBAL | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auswahl Freigabe Global 0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |
| FREIGABE_PANIK | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Auswahl Freigabe Panikl 0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |

<a id="table-arg-0x4103"></a>
### ARG_0X4103

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BEREICH | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE_ARG | - | - | - | - | - | Modus siehe Tabelle TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE_ARG |

<a id="table-arg-0x6013"></a>
### ARG_0X6013

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Löschen Alarmspeicher SINE 1:Löschen; 0:nicht Löschen |

<a id="table-arg-0x6014"></a>
### ARG_0X6014

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Löschen Fehlerspeicher SINE 1:Löschen; 0:nicht Löschen |

<a id="table-arg-0x6015"></a>
### ARG_0X6015

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Löschen Verpolzähler SINE 1:Löschen; 0:nicht Löschen |

<a id="table-arg-0xa17c"></a>
### ARG_0XA17C

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH_STRICT | - | - | - | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| AKTION | + | - | 0-n | - | char | - | TAB_FH_SHD_ESH_EINLERNEN | - | - | - | - | - | Anlernart des Elements siehe Tabelle: TAB_FH_SHD_ESH_EINLERNEN |

<a id="table-arg-0xa183"></a>
### ARG_0XA183

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| RICHTUNG | + | - | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0x00: Öffnen 0x01: Gehoben bzw. Zwangsspalt |
| ZEIT | + | - | ms | - | unsigned int | - | - | 1.0 | 100.0 | 0.0 | 0.0 | 1000.0 | Angabe der Ansteuerzeit in ms |

<a id="table-arg-0xa184"></a>
### ARG_0XA184

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| FUNKTION | + | - | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_SFK1 | 1.0 | 1.0 | 0.0 | - | - | Sonderfunktionspositionen siehe Tabelle TAB_FH_SHD_ESH_SFK1 |
| RICHTUNG | + | - | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | 0x00: Ursprungsposition anfahren 0x01: Position anfahren |

<a id="table-arg-0xa185"></a>
### ARG_0XA185

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| POSITION | + | - | Ink | - | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Wert 500 für Schiebehebedach ist die Geschlossen-Position |

<a id="table-arg-0xa186"></a>
### ARG_0XA186

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| POSITION | + | - | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | 0%:offen 100%: geschlossen |
| BEREICH | + | - | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_LAGE_NR_ARG | 1.0 | 1.0 | 0.0 | - | - | Argument siehe Tabelle TAB_FH_SHD_ESH_LAGE_NR_ARG |

<a id="table-arg-0xa187"></a>
### ARG_0XA187

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| POSITION | + | - | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_SERVICEPOSITION | 1.0 | 1.0 | 0.0 | - | - | Position des Elements siehe Tabelle TAB_FH_SHD_ESH_SERVICEPOSITION |

<a id="table-arg-0xa188"></a>
### ARG_0XA188

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | - | unsigned char | - | TAB_SHD_ESH_STRICT | - | - | - | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| RICHTUNG | + | - | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_TASTER_RICHTUNG | 1.0 | 1.0 | 0.0 | - | - | Bewegungsrichtung des Elements siehe Tabelle TAB_FH_SHD_ESH_TASTER_RICHTUNG |
| ZEIT | + | - | ms | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | 0.0 | - | Angabe der Zeit in ms |

<a id="table-arg-0xaa76"></a>
### ARG_0XAA76

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL | + | - | 0-n | - | char | - | TAB_DWA_SELBSTTEST | 1.0 | 1.0 | 0.0 | - | - | optionales Argument; 0: Abbruch; 1: Selbsttest komplettes DWA-System; 2: Selbsttest Innenraumschutz; 3 Selbsttest Neigungsgeber; DEFAULT: 1 |

<a id="table-arg-0xaa79"></a>
### ARG_0XAA79

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | + | - | 0/1 | - | int | - | - | 1.0 | 1.0 | 0.0 | - | - | 0 oder kein Argument: DWA entschärfen; 1: DWA schärfen |

<a id="table-arg-0xaa7b"></a>
### ARG_0XAA7B

Dimensions: 6 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OPT_ENTSCHAERFEN | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwert zurücksetzen |
| AKUST_ENTSCHAERFEN | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwert zurücksetzen |
| OPT_SCHAERFEN | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwert zurücksetzen |
| AKUST_SCHAERFEN | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwert zurücksetzen |
| OPT_SCHAERFEN_KLAPPE | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwert zurücksetzen |
| AKUST_SCHAERFEN_KLAPPE | + | - | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0: keine Aktion  1: Auf Codierwerte zurücksetzen |

<a id="table-arg-0xd17c"></a>
### ARG_0XD17C

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |

<a id="table-arg-0xd17d"></a>
### ARG_0XD17D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |

<a id="table-arg-0xd17e"></a>
### ARG_0XD17E

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| AKTION | 0-n | - | unsigned char | - | TAB_RELAIS_RICHTUNG | 1.0 | 1.0 | 0.0 | - | - | Das Relais wird mit Schutzfunktion Timeout 4s direkt angesteuert siehe Tabelle TAB_RELAIS_RICHTUNG |
| RELAIS_NUMBER | 0-n | high | unsigned char | - | TAB_RELAIS_NUMBER | 1.0 | 1.0 | 0.0 | - | - | angesteuertes Relais siehe Tabelle TAB_RELAIS_NUMBER |

<a id="table-arg-0xd19e"></a>
### ARG_0XD19E

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | 0-n | - | unsigned char | - | TAB_SHD_ESH | 1.0 | 1.0 | 0.0 | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH |
| AKTION | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Steuern Hallversorgung 0x00: Aus 0x01: Ein |

<a id="table-arg-0xd1bf"></a>
### ARG_0XD1BF

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Statistikzähler löschen |

<a id="table-arg-0xd1c1"></a>
### ARG_0XD1C1

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Statistikzähler löschen |

<a id="table-arg-0xdca8"></a>
### ARG_0XDCA8

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | int | - | TAB_DWA_LED | 1.0 | 1.0 | 0.0 | 0.0 | 3.0 | Ansteuerung der DWA-LED 0: Aus  1: Dauer-Ein  2: Blinken  3: Blitzen |
| ZEIT | ms | - | int | - | - | 1.0 | 1.0 | 0.0 | - | - | Angabe der Zeit in ms |

<a id="table-arg-0xdcaa"></a>
### ARG_0XDCAA

Dimensions: 6 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OPT_ENTSCHAERFEN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Optische Bestätigung bei entschärfen Aus  1= Optische Bestätigung bei entschärfen Ein |
| AKUST_ENTSCHAERFEN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Akustische Bestätigung bei entschärfen Aus  1= Akustische Bestätigung bei entschärfen Ein |
| OPT_SCHAERFEN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Optische Bestätigung bei schärfen Aus  1= Optische Bestätigung bei schärfen Ein |
| AKUST_SCHAERFEN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Akustische Bestätigung bei schärfen Aus  1= Akustische Bestätigung bei schärfen Ein |
| OPT_SCHAERFEN_KLAPPE | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Optische Bestätigung bei schärfen über Klappe Aus  1= Optische Bestätigung bei schärfen über Klappe Ein |
| AKUST_SCHAERFEN_KLAPPE | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 1.0 | 0= Akustische Bestätigung bei schärfen über Klappe Aus  1= Akustische Bestätigung bei schärfen über Klappe Ein |

<a id="table-arg-0xdcb5"></a>
### ARG_0XDCB5

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0-n | - | int | - | TAB_DWA_SCHNELLTEST | 1.0 | 1.0 | 0.0 | - | - | 0: Vorgang abbrechen; 1: Schnelltest leise 2: Schnelltest normal |

<a id="table-arg-0xdd16"></a>
### ARG_0XDD16

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OBD_UEBERWACHUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0 = OBD-Überwachung nicht aktiv 1 = OBD-Überwachung aktiv |

<a id="table-arg-0xf000"></a>
### ARG_0XF000

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ELEMENT | + | - | 0-n | high | unsigned char | - | TAB_SHD_ESH_ENTW | - | - | - | - | - | Auswahl Element siehe Tabelle TAB_SHD_ESH_ENTW |
| AUSGABE_KONFIG_1 | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ein- und Ausschalten der Debugausgabe über den CAN-Bus 0x00 = Ausgabe SHD deaktiviert 0x01 = Ausgabe SHD aktiviert |
| AUSGABE_KONFIG_2 | + | - | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Ein- und Ausschalten der Debugausgabe über den CAN-Bus 0x00 = Ausgabe ESH deaktiviert 0x01 = Ausgabe ESH aktiviert |

<a id="table-arg-6013"></a>
### ARG_6013

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x44 | Spannungsmanipulation |
| 0x45 | Bus auf UBat |
| 0x46 | Bus auf Masse |
| 0x47 | Bus-Manipulation |
| 0x48 | Neigungsgeber-Alarm: keine Antwort von FZD |
| 0xFF | kein Eintrag |

<a id="table-arg-6014"></a>
### ARG_6014

Dimensions: 42 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DTC nicht aktiv |
| 0x01 | DTC aktiv in der Vergangenheit |
| 0x02 | DTC aktiv in der Vergangenheit |
| 0x03 | DTC aktiv in der Vergangenheit |
| 0x04 | DTC aktiv in der Vergangenheit |
| 0x05 | DTC aktiv in der Vergangenheit |
| 0x06 | DTC aktiv in der Vergangenheit |
| 0x07 | DTC aktiv in der Vergangenheit |
| 0x08 | DTC aktiv in der Vergangenheit |
| 0x09 | DTC aktiv in der Vergangenheit |
| 0x0A | DTC aktiv in der Vergangenheit |
| 0x0B | DTC aktiv in der Vergangenheit |
| 0x0C | DTC aktiv in der Vergangenheit |
| 0x0D | DTC aktiv in der Vergangenheit |
| 0x0E | DTC aktiv in der Vergangenheit |
| 0x0F | DTC aktiv in der Vergangenheit |
| 0x10 | DTC aktiv in der Vergangenheit |
| 0x11 | DTC aktiv in der Vergangenheit |
| 0x12 | DTC aktiv in der Vergangenheit |
| 0x13 | DTC aktiv in der Vergangenheit |
| 0x14 | DTC aktiv in der Vergangenheit |
| 0x15 | DTC aktiv in der Vergangenheit |
| 0x16 | DTC aktiv in der Vergangenheit |
| 0x17 | DTC aktiv in der Vergangenheit |
| 0x18 | DTC aktiv in der Vergangenheit |
| 0x19 | DTC aktiv in der Vergangenheit |
| 0x1A | DTC aktiv in der Vergangenheit |
| 0x1B | DTC aktiv in der Vergangenheit |
| 0x1C | DTC aktiv in der Vergangenheit |
| 0x1D | DTC aktiv in der Vergangenheit |
| 0x1E | DTC aktiv in der Vergangenheit |
| 0x1F | DTC aktiv in der Vergangenheit |
| 0x20 | DTC aktiv in der Vergangenheit |
| 0x21 | DTC aktiv in der Vergangenheit |
| 0x22 | DTC aktiv in der Vergangenheit |
| 0x23 | DTC aktiv in der Vergangenheit |
| 0x24 | DTC aktiv in der Vergangenheit |
| 0x25 | DTC aktiv in der Vergangenheit |
| 0x26 | DTC aktiv in der Vergangenheit |
| 0x27 | DTC aktiv in der Vergangenheit |
| 0x28 | DTC ist aktiv |
| 0xFF | unbekannter Wert |

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
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 85 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x025600 | Energiesparmode aktiv | 0 |
| 0x02FF56 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x030200 | SHD, Relais Öffnen, fehlende Aussgangsspannung: Relaiskleber oder Sicherung defekt oder Kurzschluss nach Masse | 0 |
| 0x030201 | SHD, Relais Schliessen, keine Aussgangsspannung: Relaiskleber oder Sicherung defekt oder Kurzschluss nach Masse | 0 |
| 0x030202 | SHD, Relais Öffnen: Kurzschluss nach Ubatt oder Relaiskleber | 0 |
| 0x030203 | SHD, Relais Schliessen: Kurzschluss nach Ubatt oder Relaiskleber | 0 |
| 0x030205 | SHD, Hallelement A: Hallelement defekt oder Leitungsunterbrechung | 0 |
| 0x030206 | SHD, Hallelement B: Hallelement defekt oder Leitungsunterbrechung | 0 |
| 0x030207 | SHD, Hallelemente A und B: Motoreinheit defekt oder Leitungsunterbrechung | 0 |
| 0x030208 | SHD: Hallelemente A und B: Kurzschluss Motorzuleitung nach Ubatt oder Relaiskleber oder Einheit mechanisch bewegt | 0 |
| 0x030209 | SHD, Hallelemente A und B: Kurzschluss zwischen Zuleitung oder Motoreinheit defekt | 0 |
| 0x03020A | SHD, Hallelement A: Kurzschluss nach Masse | 0 |
| 0x03020B | SHD, Hallelement B: Kurzschluss nach Masse | 0 |
| 0x03020C | SHD, Hallelement A: Kurzschluss nach Ubatt | 0 |
| 0x03020D | SHD, Hallelement B: Kurzschluss nach Ubatt | 0 |
| 0x03020E | SHD, Hallelement A: Leitungsunterbrechung | 0 |
| 0x03020F | SHD, Hallelement B: Leitungsunterbrechung | 0 |
| 0x030210 | SHD: Hallelemente zeigen falsche Drehrichtung: Verpolung Stecker oder Kabelbaum | 0 |
| 0x030211 | SHD, Bewegung falscher Motor: Verpolung Stecker oder Kabelbaum | 0 |
| 0x030212 | SHD: Timeout Ansteuerung, keine Blockerkennung | 0 |
| 0x030214 | SHD: Nullposition überfahren, Normierungsverlust | 0 |
| 0x030215 | SHD: ungültige Kennlinie, keine Normierung vorhanden | 0 |
| 0x030216 | SHD: Motortemperatur 90% Schwelle überschritten | 1 |
| 0x030217 | SHD: Motorlauf wegen Übertemperatur unterbrochen | 1 |
| 0x030218 | SHD: Kein Motorstart wegen Überspannung oder Unterspannung | 1 |
| 0x030219 | SHD: Checksumme Codierung fehlerhaft | 0 |
| 0x03021C | SHD: Keine Initialisierung aufgrund ungültiger Randbedingungen (Motortreiber) | 1 |
| 0x03021D | SHD: Abschaltung Hallvorsorgung wegen Überspannung | 1 |
| 0x03021E | SHD: Motoransteuerung nicht möglich,  keine Spannung am Relaiseingang | 0 |
| 0x030220 | SHD: System nicht normiert | 0 |
| 0x030280 | ESH, Relais Öffnen, fehlende Aussgangsspannung: Relaiskleber oder Sicherung defekt oder Kurzschluss nach Masse | 0 |
| 0x030281 | ESH, Relais Schliessen, keine Aussgangsspannung: Relaiskleber oder Sicherung defekt oder Kurzschluss nach Masse | 0 |
| 0x030282 | ESH, Relais Öffnen: Kurzschluss nach Ubatt oder Relaiskleber | 0 |
| 0x030283 | ESH, Relais Schliessen: Kurzschluss nach Ubatt oder Relaiskleber | 0 |
| 0x030285 | ESH, Hallelement A: Hallelement defekt oder Leitungsunterbrechung | 0 |
| 0x030286 | ESH, Hallelement B: Hallelement defekt oder Leitungsunterbrechung | 0 |
| 0x030287 | ESH, Hallelemente A und B: Motoreinheit defekt oder Leitungsunterbrechung | 0 |
| 0x030288 | ESH: Hallelemente A und B: Kurzschluss Motorzuleitung nach Ubatt oder Relaiskleber oder Einheit mechanisch bewegt | 0 |
| 0x030289 | ESH, Hallelemente A und B: Kurzschluss zwischen Zuleitung oder Motoreinheit defekt | 0 |
| 0x03028A | ESH, Hallelement A: Kurzschluss nach Masse | 0 |
| 0x03028B | ESH, Hallelement B: Kurzschluss nach Masse | 0 |
| 0x03028C | ESH, Hallelement A: Kurzschluss nach Ubatt | 0 |
| 0x03028D | ESH, Hallelement B: Kurzschluss nach Ubatt | 0 |
| 0x03028E | ESH, Hallelement A: Leitungsunterbrechung | 0 |
| 0x03028F | ESH, Hallelement B: Leitungsunterbrechung | 0 |
| 0x030290 | ESH: Hallelemente zeigen falsche Drehrichtung: Verpolung Stecker oder Kabelbaum | 0 |
| 0x030291 | ESH, Bewegung falscher Motor: Verpolung Stecker oder Kabelbaum | 0 |
| 0x030292 | ESH: Timeout Ansteuerung, keine Blockerkennung | 0 |
| 0x030294 | ESH: Nullposition überfahren, Normierungsverlust | 0 |
| 0x030295 | ESH: ungültige Kennlinie, keine Normierung vorhanden | 0 |
| 0x030296 | ESH: Motortemperatur 90% Schwelle überschritten | 1 |
| 0x030297 | ESH: Motorlauf wegen Übertemperatur unterbrochen | 1 |
| 0x030298 | ESH: Kein Motorstart wegen Überspannung oder Unterspannung | 1 |
| 0x030299 | ESH: Checksumme Codierung fehlerhaft | 0 |
| 0x03029C | ESH: Keine Initialisierung aufgrund ungültiger Randbedingungen (Motortreiber) | 1 |
| 0x03029D | ESH: Abschaltung Hallvorsorgung wegen Überspannung | 1 |
| 0x03029E | ESH: Motoransteuerung nicht möglich,  keine Spannung am Relaiseingang | 0 |
| 0x0302A0 | ESH: System nicht normiert | 0 |
| 0x801A00 | Diebstahlwarnanlage, Ultraschall-Senorik: ein oder zwei Kanäle defekt | 0 |
| 0x801A01 | Diebstahlwarnanlage: LED oder Leitung LED Kurzschluss nach Plus | 0 |
| 0x801A02 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x801A03 | Schiebedach, Bedienschalter: unzulässige Kombination der Schaltereingänge | 0 |
| 0x801A05 | Codierung: Fehler bei Codierung aufgetreten | 0 |
| 0x801A06 | Codierung: Signatur für Daten ungültig | 0 |
| 0x801A07 | Codierung: Codierung passt nicht zum Fahrzeug | 0 |
| 0x801A08 | Codierung: Unplausible Daten während Transaktion | 0 |
| 0x801A32 | Schiebedach, Bedienschalter: Taster hängt | 1 |
| 0x801A38 | Unterspannung erkannt | 1 |
| 0x801A39 | Überspannung erkannt | 1 |
| 0x801A4B | SINE: Externe Versorgung Unterspannung | 1 |
| 0x801A4C | SINE: Interne Versorgung Unterspannung | 1 |
| 0x801A4D | SINE: EEPROM fehlerhaft | 0 |
| 0x801A4E | SINE: Aktiver Schutz fehlerhaft | 0 |
| 0x801A4F | SINE: Aufweckzeit fehlerhaft | 0 |
| 0x801A50 | SINE: Sirenenschaltkreis defekt | 0 |
| 0x801A51 | SINE: Neigungsgeber defekt | 0 |
| 0x801A52 | SINE: Kodierdaten Schreibfehler | 0 |
| 0x801A53 | SINE: Selbsttest timeout | 0 |
| 0x801A54 | Diebstahlwarnanlage: DWA-LED: Kurzschluß nach Masse | 0 |
| 0x801A55 | Diebstahlwarnanlage: Alarm - Details im Alarmspeicher | 1 |
| 0x801A56 | Diebstahlwarnanlage: Panikalarm - Details im Panikspeicher | 1 |
| 0xDE8468 | BODY-CAN Control Module Bus OFF | 0 |
| 0xDE8BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xDE8C5E | LIN: Sine antwortet nicht | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

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

Dimensions: 57 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x03021A | SHD: Einklemmfall im Panik-Modus erkannt | 1 |
| 0x03021B | SHD: Reversierung im Emergency-Modus | 1 |
| 0x03021F | SHD: Keine OSEK Rechenzeit für Einklemmschutzalgorithmus zugeteilt, Motor gestoppt | 0 |
| 0x030221 | SHD: Manueller Initialisierungsvorgang | 1 |
| 0x030222 | SHD: Automatischer Initialisierungsvorgang | 1 |
| 0x03029A | ESH: Einklemmfall im Panik-Modus erkannt | 1 |
| 0x03029B | ESH: Reversierung im Emergency-Modus | 1 |
| 0x03029F | ESH: Keine OSEK Rechenzeit für Einklemmschutzalgorithmus zugeteilt, Motor gestoppt | 0 |
| 0x0302A1 | ESH: Manueller Initialisierungsvorgang | 1 |
| 0x0302A2 | ESH: Automatischer Initialisierungsvorgang | 1 |
| 0x801A09 | FZD: Überlauf Resetcounter (&gt;100x) | 0 |
| 0x801A0A | FLS_E_ERASE_FAILED | 0 |
| 0x801A0B | FLS_E_READ_FAILED | 0 |
| 0x801A0C | FLS_E_WRITE_FAILED | 0 |
| 0x801A0D | FLS_E_COMPARE_FAILED | 0 |
| 0x801A0E | NVM_E_INTEGRITY_FAILED | 0 |
| 0x801A0F | NVM_E_REQ_FAILED | 0 |
| 0x801A10 | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x801A11 | NVM_E_READ_FAILED | 0 |
| 0x801A12 | NVM_E_READ_ALL_FAILED | 0 |
| 0x801A13 | NVM_E_ERASE_FAILED | 0 |
| 0x801A14 | NVM_E_CONTROL_FAILED | 0 |
| 0x801A15 | NVM_E_WRITE_FAILED | 0 |
| 0x801A16 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x801A17 | COMM_E_NET_START_IND_CHANNEL_0 | 0 |
| 0x801A18 | COMM_E_START_Tx_TIMEOUT_C0 | 0 |
| 0x801A19 | COMM_E_STOP_Tx_TIMEOUT_C0 | 0 |
| 0x801A1A | IPDUM_E_TRANSMIT_FAILED | 0 |
| 0x801A1B | LINIF_E_NC_NO_RESPONSE | 0 |
| 0x801A1C | LINIF_E_RESPONSE | 0 |
| 0x801A1D | MCU_E_CLOCK_FAILURE | 0 |
| 0x801A1E | MCU_E_LOCK_FAILURE | 0 |
| 0x801A1F | ECUM_E_ALL_RUN_REQUESTS_KILLED | 0 |
| 0x801A20 | CAN_E_TIMEOUT | 0 |
| 0x801A21 | CANIF_E_FULL_TX_BUFFER | 0 |
| 0x801A22 | CANIF_E_INVALID_RXPDUID | 0 |
| 0x801A23 | CANIF_E_INVALID_TXPDUID | 0 |
| 0x801A24 | CANIF_E_STOPPED | 0 |
| 0x801A25 | CANNM_E_CANIF_TRANSMIT_ERROR | 0 |
| 0x801A26 | CANNM_E_INIT_FAILED | 0 |
| 0x801A27 | CANTP_E_COMM | 0 |
| 0x801A28 | CNM_E_NETWORK_TIMEOUT | 0 |
| 0x801A29 | CNM_E_TX_PATH_FAILED | 0 |
| 0x801A2A | WDG_E_DISABLE_REJECTED | 0 |
| 0x801A2B | WDG_E_MODE_SWITCH_FAILED | 0 |
| 0x801A2C | WDGM_E_ALIVE_SUPERVISION | 0 |
| 0x801A2D | WDGM_E_SET_MODE | 0 |
| 0x801A2E | DM_Queue_DELETED | 0 |
| 0x801A2F | DM_Queue_FULL | 0 |
| 0x801A30 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 |
| 0x801A57 | Diebstahlwarnanlage: Deaktivierung IRS und Neigungsgeber per Kundenfunktion | 1 |
| 0x801A58 | EEPROM has an access error of type 1 | 1 |
| 0x801A59 | EEPROM has an access error of type 2 | 1 |
| 0x801A5A | EEPROM has an access error of type 3 | 1 |
| 0x801A5B | EEPROM has an access error of type 4 | 1 |
| 0xDE9500 | Botschaft (Fahrzeugzustand, 0x3A0) fehlt | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0x4100"></a>
### RES_0X4100

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHD_THERMOMONITOR_AKTIV | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV | - | - | - | Status Thermomonitor aktiv siehe Tabelle TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV |
| STAT_ESH_THERMOMONITOR_AKTIV | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV | 1.0 | 1.0 | 0.0 | Status Thermomonitor aktiv siehe Tabelle TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV |

<a id="table-res-0x4101"></a>
### RES_0X4101

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHD_FREIGABE_GLOBAL | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Freigabe Global  0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |
| STAT_ESH_FREIGABE_GLOBAL | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Freigabe Global  0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |
| STAT_SHD_FREIGABE_PANIK | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Freigabe Panik  0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |
| STAT_ESH_FREIGABE_PANIK | 0/1 | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Freigabe Panik  0x00 Freigabe nicht aktiv 0x01 Freigabe aktiv |

<a id="table-res-0x4103"></a>
### RES_0X4103

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BEREICH | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE | - | - | - | Status Modus siehe Tabelle TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE |

<a id="table-res-0x4107"></a>
### RES_0X4107

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KENNLINIENDATEN_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg erster Block |
| STAT_KENNLINIENDATEN_2_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg zweiter Block |
| STAT_SCHLIESSZEIT_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Schliesszeit beim Initialisierungsvorgang. Auflösung 10ms Schritte |
| STAT_BN_SPANNUNG_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung die am Fensterheber während dem Initialisieren anliegt. Auflösung 100mV Schritte |
| STAT_SPIEL_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hall Inkremente |
| STAT_GUELTIGKEIT | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie ungültig 0x01 Kennlinie gültig |
| STAT_BEWERTUNG | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie in Ordnung  0x01 Kennlinie nicht in Ordnung |
| STAT_REGELVERLETZUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | zu klären |

<a id="table-res-0x4108"></a>
### RES_0X4108

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KENNLINIENDATEN_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg erster Block |
| STAT_KENNLINIENDATEN_2_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg zweiter Block |
| STAT_SCHLIESSZEIT_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Schliesszeit beim Initialisierungsvorgang. Auflösung 10ms Schritte |
| STAT_BN_SPANNUNG_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung die am Fensterheber während dem Initialisieren anliegt. Auflösung 100mV Schritte |
| STAT_SPIEL_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hall Inkremente |
| STAT_GUELTIGKEIT | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie ungültig 0x01 Kennlinie gültig |
| STAT_BEWERTUNG | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie in Ordnung 0x01 Kennlinie nicht in Ordnung |
| STAT_REGELVERLETZUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | zu klären |

<a id="table-res-0x4109"></a>
### RES_0X4109

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KENNLINIENDATEN_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg erster Block |
| STAT_KENNLINIENDATEN_2_DATA | DATA | high | data[128] | - | - | 1.0 | 1.0 | 0.0 | Drehzahlwert über dem Verfahrweg zweiter Block |
| STAT_SCHLIESSZEIT_WERT | s | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Schliesszeit beim Initialisierungsvorgang. Auflösung 10ms Schritte |
| STAT_BN_SPANNUNG_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung die am Fensterheber während dem Initialisieren anliegt. Auflösung 100mV Schritte |
| STAT_SPIEL_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hall Inkremente |
| STAT_GUELTIGKEIT | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie ungültig 0x01 Kennlinie gültig |
| STAT_BEWERTUNG | 0/1 | high | unsigned char | - | - | - | - | - | 0x00 Kennlinie in Ordnung  0x01 Kennlinie nicht in Ordnung |
| STAT_REGELVERLETZUNG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | zu klären |

<a id="table-res-0x6012"></a>
### RES_0X6012

Dimensions: 19 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FZD_ALARM_MOTORHAUBE_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Klappenkontakt MotorHaube |
| STAT_FZD_ALARM_FAT_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Klappenkontakt FAhrerTür |
| STAT_FZD_ALARM_BFT_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Klappenkontakt BeiFahrerTür |
| STAT_FZD_ALARM_FATH_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Klappenkontakt FAhrerTür Hinten |
| STAT_FZD_ALARM_BFTH_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Klappenkontakt BeiFahrerTür Hinten |
| STAT_FZD_ALARM_HECKKLAPPE_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Heckklappe |
| STAT_FZD_ALARM_HECKSCHEIBE_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Heckscheibe |
| STAT_FZD_ALARM_OBD_KOMMUNIKATION_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme OBD-Kommunikation |
| STAT_FZD_ALARM_LEITUNGSUEBERWACHUNG_SINE_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Leitungsüberwachung LIN-SINE |
| STAT_FZD_ALARM_MANIPULATION_AUTH_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Manipulationsschutz Authentifizierung |
| STAT_FZD_ALARM_USIS_KANAL_A_UND_B_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl USIS-Alarme gleichzeitig auf Kanal A und B (rechts + links) |
| STAT_FZD_ALARM_USIS_KANAL_A_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl USIS-Alarme nur auf Kanal A (rechts) |
| STAT_FZD_ALARM_USIS_KANAL_B_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl USIS-Alarme nur auf Kanal B (links) |
| STAT_SINE_ALARM_NEIGUNGSGEBER_X_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Neigungsgeber X-Achse |
| STAT_SINE_ALARM_NEIGUNGSGEBER_Y_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Neigungsgeber Y-Achse |
| STAT_SINE_ALARM_NEIGUNGSGEBER_X_UND_Y_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Neigungsgeber X- und Y-Achse |
| STAT_SINE_ALARM_SPANNUNG_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Unterbrechung Spannungsversorgung der LIN-SINE |
| STAT_SINE_ALARM_LIN_TELEGRAMM_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme LIN-Bus: kein Telegramm absetzbar |
| STAT_FZD_ALARM_PANIKALARM_WERT | count | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl Alarme Panikalarm |

<a id="table-res-0x6013"></a>
### RES_0X6013

Dimensions: 10 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ALARM_1_ID | 0-n | high | unsigned char | - | ARG_6013 | - | - | - | Alarmcode LIN-SINE |
| STAT_ALARM_1_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Alarm |
| STAT_ALARM_2_ID | 0-n | high | unsigned char | - | ARG_6013 | - | - | - | Alarmcode LIN-SINE |
| STAT_ALARM_2_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Alarm |
| STAT_ALARM_3_ID | 0-n | high | unsigned char | - | ARG_6013 | 1.0 | 1.0 | 0.0 | Alarmcode LIN-SINE |
| STAT_ALARM_3_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Alarm |
| STAT_ALARM_4_ID | 0-n | high | unsigned char | - | ARG_6013 | 1.0 | 1.0 | 0.0 | Alarmcode LIN-SINE |
| STAT_ALARM_4_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Alarm |
| STAT_ALARM_5_ID | 0-n | high | unsigned char | - | ARG_6013 | 1.0 | 1.0 | 0.0 | Alarmcode LIN-SINE |
| STAT_ALARM_5_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Alarm |

<a id="table-res-0x6014"></a>
### RES_0X6014

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LOW_EXTERN_BAT_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D11  externe Spannung niedrig |
| STAT_LOW_EXTERN_BAT_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D11  externe Spannung niedrig |
| STAT_LOW_INTERN_BAT_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D12  interne Spannung niedrig |
| STAT_LOW_INTERN_BAT_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D12  interne Spannung niedrig |
| STAT_EEPROM_ID | 0-n | high | unsigned char | - | ARG_6014 | 1.0 | 1.0 | 0.0 | Status DTC 0x9D13  EEPROM KO |
| STAT_EEPROM_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D13  EEPROM KO |
| STAT_AKTIV_SCHUTZ_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D14  Aktiver Schutz KO |
| STAT_AKTIV_SCHUTZ_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D14  Aktiver Schutz KO |
| STAT_AUFWACHZEIT_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D15  falsche Aufstartzeit |
| STAT_AUFSTARTZEIT_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D15  falsche Aufstartzeit |
| STAT_KLANGSCHALTKREIS_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D16  Klangschaltkreis KO |
| STAT_KLANGSCHALTKREIS_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D16  Klangschaltkreis KO |
| STAT_NEIGUNGSGEBER_ID | 0-n | high | unsigned char | - | ARG_6014 | - | - | - | Status DTC 0x9D1F  Neigungsgeber KO |
| STAT_NEIGUNGSGEBER_TEMP_WERT | ° | high | char | - | - | 1.0 | 1.0 | 0.0 | Temperatur bei Eintragung DTC 0x9D1F  Neigungsgeber KO |

<a id="table-res-0x6015"></a>
### RES_0X6015

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_MAXIMAL_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Aufgetretene Maximalspannung bei Verpolung |
| STAT_ZEIT_UNTER_1V_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit mit Spannung &lt; -1V |
| STAT_ZEIT_UNTER_2V_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit mit Spannung &lt; -2V |
| STAT_ZEIT_UNTER_3V_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit mit Spannung &lt; -3V |
| STAT_ZEIT_UNTER_4V_WERT | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit mit Spannung &lt; -4V |

<a id="table-res-0xa17c"></a>
### RES_0XA17C

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |
| STAT_SHD_VORGANG_NR | + | - | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_EINLERNVORGANG | 1.0 | 1.0 | 0.0 | Zuordnung siehe Tabelle TAB_FH_SHD_EINLERNVORGANG |
| STAT_ESH_VORGANG_NR | + | - | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_EINLERNVORGANG | 1.0 | 1.0 | 0.0 | Zuordnung siehe Tabelle TAB_FH_SHD_EINLERNVORGANG |

<a id="table-res-0xa183"></a>
### RES_0XA183

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xa184"></a>
### RES_0XA184

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xa185"></a>
### RES_0XA185

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xa186"></a>
### RES_0XA186

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xa187"></a>
### RES_0XA187

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xa188"></a>
### RES_0XA188

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | 1.0 | 1.0 | 0.0 | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-res-0xaa76"></a>
### RES_0XAA76

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_SELBSTTEST_NR | - | - | + | 0-n | - | char | - | TAB_DWA_SELBSTTEST_ERG | 1.0 | 1.0 | 0.0 | 0: Selbsttest NIO  1: Selbsstest IO 2: Selbsttest läuft |

<a id="table-res-0xd180"></a>
### RES_0XD180

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HALL_A_SCHALTZUSTAND_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall A Schaltzustand 0x00: Aus 0x01: Ein |
| STAT_HALL_A_VERSORGUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall A Versorgung 0x00: Aus 0x01: Ein |
| STAT_HALL_A_FEHLERZUSTAND_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND | 1.0 | 1.0 | 0.0 | Fehlerzustand Hallanschluss siehe Tabelle TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND |
| STAT_HALL_B_SCHALTZUSTAND_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall B Schaltzustand 0x00: Aus 0x01: Ein |
| STAT_HALL_B_VERSORGUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall B Versorgung 0x00: Aus 0x01: Ein |
| STAT_HALL_B_FEHLERZUSTAND_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND | 1.0 | 1.0 | 0.0 | Fehlerzustand Hallanschluss siehe Tabelle TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND |

<a id="table-res-0xd192"></a>
### RES_0XD192

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_SHD_ESH_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_VERFAHREN | 1.0 | 1.0 | 0.0 | Tasteranforderung siehe Tabelle TAB_FH_ESH_VERFAHREN |
| STAT_TASTER_RESERVE | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | noch unbelgt |

<a id="table-res-0xd196"></a>
### RES_0XD196

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHD_INIT_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_INIT | 1.0 | 1.0 | 0.0 | Initialisierungsergebnis siehe Tabelle TAB_FH_SHD_ESH_INIT |
| STAT_SHD_BEWEGUNG_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_BEWEGUNG | 1.0 | 1.0 | 0.0 | Bewegung des Elements siehe Tabelle TAB_FH_SHD_ESH_BEWEGUNG |
| STAT_SHD_POSITION_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_POSITION | 1.0 | 1.0 | 0.0 | Aktuelle Position des Glasdeckels siehe Tabelle TAB_FH_SHD_ESH_POSITION |
| STAT_SHD_POSITION_HALL_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktuelle Position in Hall-Pulsen (500 bedeutet komplett geschlossen) |
| STAT_SHD_POSITION_HALL_MIN_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Position in Hall-Pulsen |
| STAT_SHD_POSITION_HALL_MAX_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Position in Hall-Pulsen |
| STAT_SHD_POSITION_MM_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | Schlittenweg in mm zwischen MIN und MAX in Millimeter (0 bedeut komplett geschlossen) |
| STAT_SHD_POSITION_MM_MIN_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | Minimale Position in Millimeter |
| STAT_SHD_POSITION_MM_MAX_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | Maximale Position in Millimeter |
| STAT_SHD_POSITION_PROZENT_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | % vom maximalen Verfahrweg 0% bedeutet offen /100% bedeutet geschlossen |
| STAT_SHD_LAGE_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_LAGE_NR | 1.0 | 1.0 | 0.0 | Lage Glasdeckel siehe Tabelle TAB_FH_SHD_ESH_LAGE_NR |
| STAT_SHD_ZUSTAND_TUER_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_ZUSTAND_TUER | 1.0 | 1.0 | 0.0 | Status Türkontakt, der den Motortreiber zur Verfügung steht. siehe Tabelle TAB_FH_SHD_ESH_ZUSTAND_TUER |
| STAT_SHD_FREIGABE_AKTIV_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_FREIGABE | 1.0 | 1.0 | 0.0 | Freigabezustand siehe Tabelle TAB_FH_SHD_ESH_FREIGABE |
| STAT_SHD_PANIKMODUS_AKTIV_NR | 0-n | - | unsigned char | - | TAB_FH_PANIKMODUS | 1.0 | 1.0 | 0.0 | Status Verknüpfung Freigabe Panikmodus |
| STAT_SHD_RESERVE | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve |

<a id="table-res-0xd1a6"></a>
### RES_0XD1A6

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SHD_RESERVE_1 | 0-n | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Von SHD nicht benutzt! |
| STAT_SHD_MOTORTEMPERATUR_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_MOTORTEMPERATUR | - | - | - | Motortemperaturbereiche siehe Tabelle TAB_FH_SHD_ESH_MOTORTEMPERATUR |
| STAT_SHD_AUSSENTEMPERATUR_WERT | °C | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Aussentemperatur (Codierung analog CAN-Signal) |
| STAT_SHD_MT_LIEFERANT_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_MT_LIEFERANT | 1.0 | 1.0 | 0.0 | Lieferant des Motortreibers siehe Tabelle TAB_FH_SHD_ESH_MT_LIEFERANT |
| STAT_SHD_MT_SW_VERSION | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | SW-Version Byte 0 = Patchlevelnumber Byte 1 = Minorversionnumber Byte2 = Majorversionnumber Byte3 = unused |
| STAT_SHD_EEPROM_PRUEFSUMME_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STAT_EEPROM | 1.0 | 1.0 | 0.0 | Status EEPROM Checksumme siehe Tabelle TAB_FH_SHD_ESH_STAT_EEPROM |
| STAT_SHD_RESERVE_2 | 0-n | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Von SHD vorerst nicht benutzt! |
| STAT_SHD_WACHHALTEN | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_WACHHALTEN | - | - | - | Status Einschlaf-Verhinderung siehe Tabelle TAB_FH_SHD_ESH_WACHHALTEN |
| STAT_SHD_FZG_GESCHWINDIGKEIT | 0-n | - | unsigned char | - | - | - | - | - | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_SHD_RELATIVZEIT | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Aktuelle Relativ-Zeit (wie vom Bus erhalten) |
| STAT_SHD_TEMPERATUR_UEBERWACHUNG | 0/1 | - | unsigned char | - | - | - | - | - | Status Aktivierung Temperaturüberwachung  0x00: Aus 0x01: Ein |
| STAT_SHD_EKS_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | Status Aktivierung EKS 0x00: Aus 0x01: Ein |
| STAT_SHD_FREIGABE_DEAKTIVIERT | 0/1 | - | unsigned char | - | - | - | - | - | Status Verknüpfung Freigabe 0x00: Aus 0x01: Ein |
| STAT_SHD_PANIKMODUS_DEAKTIVIERT | 0/1 | - | unsigned char | - | - | - | - | - | Status Verknüpfung Freigabe Panikmodus 0x00: Aus 0x01: Ein |
| STAT_SHD_RESERVE | 0-n | - | unsigned long | - | - | - | - | - | Reserve für Erweiterungen |

<a id="table-res-0xd1b9"></a>
### RES_0XD1B9

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RELAIS_A_ANSTEUERUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Ansteuerung Relais A 0x00: Aus 0x01: Ein |
| STAT_RELAIS_A_RUECK_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Rückleseleitung Relais A 0x00: Aus 0x01: Ein |
| STAT_RELAIS_B_ANSTEUERUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Ansteuerung Relais B 0x00: Aus 0x01: Ein |
| STAT_RELAIS_B_RUECK_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Status Rückleseleitung Relais B 0x00: Aus 0x01: Ein |
| STAT_RELAIS_A_VERSORGUNG_WERT | V | - | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Eingangsspannung am Relais (Klemmenspannung des Motors) . Auflösung 0,01 V |
| STAT_RELAIS_B_VERSORGUNG_WERT | V | - | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Eingangsspannung am Relais (Klemmenspannung des Motors) . Auflösung 0,01 V |

<a id="table-res-0xd1ba"></a>
### RES_0XD1BA

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ESH_INIT_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_INIT | 1.0 | 1.0 | 0.0 | Initialisierungsergebnis siehe Tabelle TAB_FH_SHD_ESH_INIT |
| STAT_ESH_BEWEGUNG_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_BEWEGUNG | 1.0 | 1.0 | 0.0 | Bewegung des Elements siehe Tabelle TAB_FH_SHD_ESH_BEWEGUNG |
| STAT_ESH_POSITION_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_POSITION | 1.0 | 1.0 | 0.0 | Aktuelle Position des Schiebehimmels siehe Tabelle TAB_FH_SHD_ESH_POSITION |
| STAT_ESH_POSITION_HALL_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Aktuelle Position in Hall-Pulsen (500 bedeutet komplett geschlossen) |
| STAT_ESH_POSITION_HALL_MIN_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Minimale Position in Hall-Pulsen |
| STAT_ESH_POSITION_HALL_MAX_WERT | Ink | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Maximale Position in Hall-Pulsen |
| STAT_ESH_POSITION_MM_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | liefert den Schlittenweg in mm zwischen MIN und MAX in Millimeter (0 bedeut komplett geschlossen) |
| STAT_ESH_POSITION_MM_MIN_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | Minimale Position in Millimeter |
| STAT_ESH_POSITION_MM_MAX_WERT | mm | - | int | - | - | 1.0 | 1.0 | 0.0 | Maximale Position in Millimeter |
| STAT_ESH_POSITION_PROZENT_WERT | % | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | % vom maximalen Verfahrweg 0% offen / 100% geschlossen |
| STAT_ESH_LAGE_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_LAGE_NR | 1.0 | 1.0 | 0.0 | Lage Schiebehimmel siehe Tabelle TAB_FH_SHD_ESH_LAGE_NR |
| STAT_ESH_ZUSTAND_TUER_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_ZUSTAND_TUER | 1.0 | 1.0 | 0.0 | Status Türkontakt, der den Motortreiber zur Verfügung steht. siehe Tabelle TAB_FH_SHD_ESH_ZUSTAND_TUER |
| STAT_ESH_FREIGABE_AKTIV_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_FREIGABE | 1.0 | 1.0 | 0.0 | Freigabezustand siehe Tabelle TAB_FH_SHD_ESH_FREIGABE |
| STAT_ESH_PANIKMODUS_AKTIV_NR | 0-n | - | unsigned char | - | TAB_FH_PANIKMODUS | 1.0 | 1.0 | 0.0 | Status Verknüpfung Freigabe Panikmodus |
| STAT_ESH_RESERVE | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve |

<a id="table-res-0xd1bb"></a>
### RES_0XD1BB

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HALL_A_SCHALTZUSTAND_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall A Schaltzustand 0x00: Aus 0x01: Ein |
| STAT_HALL_A_VERSORGUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall A Versorgung 0x00: Aus 0x01: Ein |
| STAT_HALL_A_FEHLERZUSTAND_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND | 1.0 | 1.0 | 0.0 | Fehlerzustand Hallanschluss siehe Tabelle TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND |
| STAT_HALL_B_SCHALTZUSTAND_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall B Schaltzustand 0x00: Aus 0x01: Ein |
| STAT_HALL_B_VERSORGUNG_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Hall B Versorgung 0x00: Aus 0x01: Ein |
| STAT_HALL_B_FEHLERZUSTAND_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND | 1.0 | 1.0 | 0.0 | Fehlerzustand Hallanschluss siehe Tabelle TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND |

<a id="table-res-0xd1bc"></a>
### RES_0XD1BC

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RELAIS_A_ANSTEUERUNG_EIN | 0/1 | - | unsigned char | - | - | - | - | - | Status Ansteuerung Relais A 0x00: Aus 0x01: Ein |
| STAT_RELAIS_A_RUECK_EIN | 0/1 | - | unsigned char | - | - | - | - | - | Status Rückleseleitung Relais A 0x00: Aus 0x01: Ein |
| STAT_RELAIS_B_ANSTEUERUNG_EIN | 0/1 | - | unsigned char | - | - | - | - | - | Status Ansteuerung Relais B 0x00: Aus 0x01: Ein |
| STAT_RELAIS_B_RUECK_EIN | 0/1 | - | unsigned char | - | - | - | - | - | Status Rückleseleitung Relais B 0x00: Aus 0x01: Ein |
| STAT_RELAIS_A_VERSORGUNG_WERT | V | - | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Eingangsspannung am Relais (Klemmenspannung des Motors) . Auflösung 0,01 V |
| STAT_RELAIS_B_VERSORGUNG_WERT | V | - | unsigned int | - | - | 1.0 | 100.0 | 0.0 | Eingangsspannung am Relais (Klemmenspannung des Motors) . Auflösung 0,01 V |

<a id="table-res-0xd1bd"></a>
### RES_0XD1BD

Dimensions: 15 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ESH_RESERVE_1 | 0-n | - | unsigned char | - | - | - | - | - | Von ESH nicht benutzt! |
| STAT_ESH_MOTORTEMPERATUR_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_MOTORTEMPERATUR | - | - | - | Motortemperaturbereiche, siehe Tabelle TAB_FH_SHD_ESH_MOTORTEMPERATUR |
| STAT_ESH_AUSSENTEMPERATUR_WERT | °C | - | unsigned char | - | - | 0.5 | 1.0 | -40.0 | Aussentemperatur (Codierung analog CAN-Signal) |
| STAT_ESH_MT_LIEFERANT_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_MT_LIEFERANT | - | - | - | Lieferant des Motortreibers, siehe Tabelle TAB_FH_SHD_ESH_MT_LIEFERANT |
| STAT_ESH_MT_SW_VERSION | 0-n | - | unsigned long | - | - | - | - | - | SW-Version Byte 0 = Patchlevelnumber Byte 1 = Minorversionnumber Byte2 = Majorversionnumber Byte3 = unused |
| STAT_ESH_EEPROM_PRUEFSUMME_NR | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_STAT_EEPROM | - | - | - | Status EEPROM Checksumme, siehe Tabelle TAB_FH_SHD_ESH_STAT_EEPROM |
| STAT_ESH_RESERVE_2 | 0-n | - | unsigned char | - | - | - | - | - | Von SHD vorerst nicht benutzt! |
| STAT_ESH_WACHHALTEN | 0-n | - | unsigned char | - | TAB_FH_SHD_ESH_WACHHALTEN | - | - | - | Status Einschlaf-Verhinderung, siehe Tabelle TAB_FH_SHD_ESH_WACHHALTEN |
| STAT_ESH_FZG_GESCHWINDIGKEIT | 0-n | - | unsigned char | - | - | - | - | - | Fahrzeuggeschwindigkeit (Codierung analog CAN-Signal) |
| STAT_ESH_RELATIVZEIT | 0-n | - | unsigned long | - | - | - | - | - | Aktuelle Relativ-Zeit (wie vom Bus erhalten) |
| STAT_ESH_TEMPERATUR_UEBERWACHUNG | 0/1 | - | unsigned char | - | - | - | - | - | Status Aktivierung Temperaturüberwachung 0x00: Aus 0x01: Ein |
| STAT_ESH_EKS_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | Status Aktivierung EKS 0x00: Aus 0x01: Ein |
| STAT_ESH_FREIGABE_DEAKTIVIERT | 0/1 | - | unsigned char | - | - | - | - | - | Status Verknüpfung Freigabe 0x00: Aus 0x01: Ein |
| STAT_ESH_PANIKMODUS_DEAKTIVIERT | 0/1 | - | unsigned char | - | - | - | - | - | Status Verknüpfung Freigabe Panikmodus 0x00: Panikmodus aktiv 0x01: Panikmodus deaktiviert |
| STAT_ESH_RESERVE | 0-n | - | unsigned long | - | - | - | - | - | Reserve für Erweiterungen |

<a id="table-res-0xd1be"></a>
### RES_0XD1BE

Dimensions: 27 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NACHNORMIERUNG_AUTOMATISCH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl automatische Nachnormierungen |
| STAT_NACHNORMIERUNG_MANUELL | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl manuelle Nachnormierungen |
| STAT_VERFAHREN_EMERGENCY | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Verfahren im Emergnecy Close |
| STAT_PANIC | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Verfahren im Panic Mode |
| STAT_REVERSIER_NORMALMODUS | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Reversiervorgänge im Normalmode |
| STAT_REVERSIERER_EMERGENCY | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Reversiervorgänge im Emergency Mode |
| STAT_ABBRUCH_MOTORLAUF | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Abbrüche des Motorlaufs |
| STAT_VORGANG_OEFFNEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 0-80 km/h |
| STAT_VORGANG_HEBEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 0-80 km/h |
| STAT_VORGANG_SCHLIESSEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 0-80 km/h |
| STAT_VORGANG_OEFFNEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 80-120 km/h |
| STAT_VORGANG_HEBEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 80-120  km/h |
| STAT_VORGANG_SCHLIESSEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 80-120 km/h |
| STAT_VORGANG_OEFFNEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 120-160 km/h |
| STAT_VORGANG_HEBEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 120-160 km/h |
| STAT_VORGANG_SCHLIESSEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 120-160 km/h |
| STAT_VORGANG_OEFFNEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich &gt; 160 km/h |
| STAT_VORGANG_HEBEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich &gt; 160 km/h |
| STAT_VORGANG_SCHLIESSEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich &gt; 160 km/h |
| STAT_BETAETIGUNG_BEI_MINUS_10_GRAD | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Betätigungen bei minus 10 Grad |
| STAT_REVERSIER_BEI_0_GRAD | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Reversiervorgänge bei kleiner 0 Grad |
| STAT_RESERVE_1 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 1 |
| STAT_RESERVE_2 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 2 |
| STAT_RESERVE_3 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 3 |
| STAT_RESERVE_4 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 4 |
| STAT_RESERVE_5 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 5 |
| STAT_RESERVE_6 | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Reserve 6 |

<a id="table-res-0xd1c0"></a>
### RES_0XD1C0

Dimensions: 27 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NACHNORMIERUNG_AUTOMATISCH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl automatische Nachnormierungen |
| STAT_NACHNORMIERUNG_MANUELL | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl manuelle Nachnormierungen |
| STAT_VERFAHREN_EMERGENCY | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Verfahren im Emergnecy Close |
| STAT_PANIC | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Verfahren im Panic Mode |
| STAT_REVERSIER_NORMALMODUS | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Reversiervorgänge im Normalmode |
| STAT_REVERSIERER_EMERGENCY | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Reversiervorgänge im Emergency Mode |
| STAT_ABBRUCH_MOTORLAUF | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Abbrüche des Motorlaufs |
| STAT_VORGANG_OEFFNEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 0-80 km/h |
| STAT_VORGANG_HEBEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 0-80 km/h |
| STAT_VORGANG_SCHLIESSEN_80_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 0-80 km/h |
| STAT_VORGANG_OEFFNEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 80-120 km/h |
| STAT_VORGANG_HEBEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 80-120  km/h |
| STAT_VORGANG_SCHLIESSEN_120_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 80-120 km/h |
| STAT_VORGANG_OEFFNEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich 120-160 km/h |
| STAT_VORGANG_HEBEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich 120-160 km/h |
| STAT_VORGANG_SCHLIESSEN_160_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich 120-160 km/h |
| STAT_VORGANG_OEFFNEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Öffnen im Bereich &gt; 160 km/h |
| STAT_VORGANG_HEBEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Heben/Lüfterposition im Bereich &gt; 160 km/h |
| STAT_VORGANG_SCHLIESSEN_300_KMH | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl Vorgänge Schliessen im Bereich &gt; 160 km/h |
| STAT_BETAETIGUNG_BEI_MINUS_10_GRAD | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Betätigungen bei minus 10 Grad |
| STAT_REVERSIER_BEI_0_GRAD | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Reversiervorgänge bei kleiner 0 Grad |
| STAT_RESERVE_1 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 1 |
| STAT_RESERVE_2 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 2 |
| STAT_RESERVE_3 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 3 |
| STAT_RESERVE_4 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 4 |
| STAT_RESERVE_5 | 0-n | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve 5 |
| STAT_RESERVE_6 | 0-n | - | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Reserve 6 |

<a id="table-res-0xdca2"></a>
### RES_0XDCA2

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LEITUNG_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status der Leitungsüberwachung |
| STAT_UNTERSPANNUNG_EXT_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Unterspannungsüberwachung der externen Batterie |
| STAT_EEPROM_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Überwachnung EEPROM |
| STAT_AKTIVER_SCHUTZ_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Aktiver Schutz |
| STAT_WAKE_UP_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Überwachung der WakeUp-Zeit |
| STAT_SIRENE_AKUSTIK_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Sirenenschaltkreis (Akustik) |
| STAT_TILT_NR | 0-n | - | char | - | TAB_DWA_SINE_INTERN | 1.0 | 1.0 | 0.0 | Status Neigungsgeber |

<a id="table-res-0xdca8"></a>
### RES_0XDCA8

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_LED_NR | 0-n | - | char | - | TAB_DWA_LED | 1.0 | 1.0 | 0.0 | 0: Aus 1: Dauer-Ein 2: Blinken 3: Blitzen |

<a id="table-res-0xdca9"></a>
### RES_0XDCA9

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NEIGUNG_X_ACHSE_WERT | Grad | - | int | - | - | 1.0 | 1.0 | 0.0 | Neigungswinkel X-Achse in Grad |
| STAT_NEIGUNG_Y_ACHSE_WERT | Grad | - | int | - | - | 1.0 | 1.0 | 0.0 | Neigungswinkel Y-Achse in Grad |

<a id="table-res-0xdcaa"></a>
### RES_0XDCAA

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_CKM_OPT_ENTSCHAERFEN_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Optische Bestätigung bei entschärfen Aus; 1=  Optische Bestätigung bei entschärfen Ein |
| STAT_DWA_CKM_AKUST_ENTSCHAERFEN_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Akustische Bestätigung bei entschärfen Aus 1= Akustische Bestätigung bei entschärfen Ein |
| STAT_DWA_CKM_OPT_SCHAERFEN_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Optische Bestätigung bei schärfen Aus; 1=  Optische Bestätigung bei schärfen Ein |
| STAT_DWA_CKM_AKUST_SCHAERFEN_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Akustische Bestätigung bei schärfen Aus 1= Akustische Bestätigung bei schärfen Ein |
| STAT_DWA_CKM_OPT_SCHAERFEN_KLAPPE_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Optische Bestätigung bei schärfen über Klappe Aus; 1=  Optische Bestätigung bei schärfen über Klappe Ein |
| STAT_DWA_CKM_AKUST_SCHAERFEN_KLAPPE_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= Akustische Bestätigung bei schärfen über Klappe Aus 1= Akustische Bestätigung bei schärfen über Klappe Ein |

<a id="table-res-0xdcb0"></a>
### RES_0XDCB0

Dimensions: 19 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DWA_ALARM_MOTORHAUBE_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Motorhaube; 1= DWA-Alarm ausgelöst durch Motorhaube |
| STAT_DWA_ALARM_FAT_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Fahrertür; 1= DWA-Alarm ausgelöst durch Fahrertür |
| STAT_DWA_ALARM_BFT_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Beifahrertür; 1= DWA-Alarm ausgelöst durch Beifahrertür |
| STAT_DWA_ALARM_FATH_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Fahrertür hinten; 1= DWA-Alarm ausgelöst durch Fahrertür hinten |
| STAT_DWA_ALARM_BFTH_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Beifahrertür hinten ; 1= DWA-Alarm ausgelöst durch Beifahrertür hinten |
| STAT_DWA_ALARM_HECKKLAPPE_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Heckklappe; 1= DWA-Alarm ausgelöst durch Heckklappe |
| STAT_DWA_ALARM_HECKSCHEIBE_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Heckscheibe; 1= DWA-Alarm ausgelöst durch Heckscheibe |
| STAT_DWA_ALARM_OBD_KOMMUNIKATION_EIN | 0/1 | - | char | - | - | - | - | - | 0= DWA-Alarm nicht ausgelöst durch OBD-Kommunikation; 1= DWA-Alarm ausgelöst durch OBD-Kommunikation |
| STAT_DWA_ALARM_LEITUNGSUEBERWACHUNG_SINE_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Leitungsüberwachung SINE; 1= DWA-Alarm ausgelöst durch Leitungsüberwachung SINE |
| STAT_DWA_ALARM_MANIPULATION_AUTH_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Manipulation Authentisierung; 1= DWA-Alarm ausgelöst durch Manipulation Authentisierung |
| STAT_DWA_ALARM_USIS_A_UND_B_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Innenraumschutz A und B; 1= DWA-Alarm ausgelöst durch Innenraumschutz A und B |
| STAT_DWA_ALARM_USIS_A_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Innenraumschutz A; 1= DWA-Alarm ausgelöst durch Innenraumschutz A |
| STAT_DWA_ALARM_USIS_B_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Innenraumschutz B; 1= DWA-Alarm ausgelöst durch Innenraumschutz B |
| STAT_DWA_ALARM_NEIGUNGSGEBER_X_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Neigungsgeber X-Achse; 1= DWA-Alarm ausgelöst durch Neigungsgeber X-Achse |
| STAT_DWA_ALARM_NEIGUNGSGEBER_Y_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Neigungsgeber Y-Achse; 1= DWA-Alarm ausgelöst durch Neigungsgeber Y-Achse |
| STAT_DWA_ALARM_NEIGUNGSGEBER_X_UND_Y_AUSGELOEST_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Neigungsgeber X- und Y-Achse; 1= DWA-Alarm ausgelöst durch Neigungsgeber X- und Y-Achse |
| STAT_DWA_ALARM_SINE_SPANNUNG_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch SINE Spannungsversorgung; 1= DWA-Alarm ausgelöst durch SINE Spannungsversorgung |
| STAT_DWA_ALARM_SINE_LIN_TELEGRAMM_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch SINE kein LIN-Telegramm absetzbar; 1= DWA-Alarm ausgelöst durch SINE kein LIN-Telegramm absetzbar |
| STAT_DWA_ALARM_PANIKALARM_EIN | 0/1 | - | char | - | - | 1.0 | 1.0 | 0.0 | 0= DWA-Alarm nicht ausgelöst durch Panikalarm; 1= DWA-Alarm ausgelöst durch Panikalarm |

<a id="table-res-0xdcdd"></a>
### RES_0XDCDD

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KONTAKT_FAHRERTUER_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Fahrertür |
| STAT_KONTAKT_BEIFAHRERTUER_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Beifahrertür |
| STAT_KONTAKT_FAHRERTUER_HINTEN_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Fahrertür hinten |
| STAT_KONTAKT_BEIFAHRERTUER_HINTEN_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Beifahrertür hinten |
| STAT_KONTAKT_MOTORHAUBE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Motorhaube |
| STAT_KONTAKT_HECKKLAPPE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Heckklappe |
| STAT_KONTAKT_HECKSCHEIBE_NR | 0-n | - | unsigned char | - | TAB_DWA_KLAPPENKONTAKT | 1.0 | 1.0 | 0.0 | Kontakt Heckscheibe |
| STAT_ZV_NR | 0-n | - | unsigned char | - | TAB_ZV_ST_CLSY | 1.0 | 1.0 | 0.0 | Status Zentralverriegelung |
| STAT_RESERVE_WERT | HEX | - | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Reserve (noch nicht belegt) |

<a id="table-res-0xdd16"></a>
### RES_0XDD16

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OBD_UEBERWACHUNG | 0/1 | high | unsigned char | - | - | - | - | - | 0 = OBD-Überwachung nicht aktiv 1 = OBD-Überwachung aktiv |

<a id="table-res-0xf000"></a>
### RES_0XF000

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ROUTINE | + | + | + | 0-n | high | unsigned char | - | TAB_FH_SHD_ESH_STATUS_ROUTINE | - | - | - | Ausführungsstatus siehe Tabelle TAB_FH_SHD_ESH_STATUS_ROUTINE |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 57 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SHD_ESH_EINLERNEN | 0xA17C | - | Einlernen des Schiebedachs und elektrischer Schiebehimmel Argument siehe Sub-Tabelle | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA17C | RES_0xA17C |
| SHD_ESH_VERFAHREN_ZEIT | 0xA183 | - | Verfährt die angegebene Scheibe für eine bestimmte Zeit unter Berücksichtigung der angegebenen Funktionen | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA183 | RES_0xA183 |
| SHD_ESH_VERFAHREN_SONDERFUNKTION | 0xA184 | - | Führt die angegebene Automatikfunktion aus | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA184 | RES_0xA184 |
| SHD_ESH_VERFAHREN_HALL | 0xA185 | - | Verfährt die angegebene Scheibe auf eine bestimmte Position unter Angabe der Zielposition in Hallinkrementen | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA185 | RES_0xA185 |
| SHD_ESH_VERFAHREN_PROZENT | 0xA186 | - | Angabe der Zielposition in Prozent | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA186 | RES_0xA186 |
| SHD_ESH_VERFAHREN_SERVICE_POSITION | 0xA187 | - | Verfährt Scheibe bestimmte Position. Achtung! Nach Ausführen des Jobs ist das System denormiert! | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA187 | RES_0xA187 |
| SHD_ESH_TASTER_STEUERN | 0xA188 | - | Simulation des Tasters (Tastendruck) | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA188 | RES_0xA188 |
| DWA_SINE_ANSTEUERUNG | 0xAA70 | - | Ansteuerung der Sirene für maximal 5 Sekunden | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_SINE_BATT_LEVEL_RESET | 0xAA71 | - | Reset des Batterie-Levels. Nur nach Austausch der Batterie durchführen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_SELBSTTEST | 0xAA76 | - | Selbsttest DWA-System. Gefundene Fehler werden im Fehlerspeicher abgelegt | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAA76 | RES_0xAA76 |
| DWA_SCHAERFEN | 0xAA79 | - | 0: DWA entschärfen 1: DWA schärfen | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAA79 | - |
| DWA_ALARM_ANZAHL_LOESCHEN | 0xAA7A | - | Anzahl Alarme löschen | - | - | - | - | - | - | - | - | - | 31 | - | - |
| DWA_CAR_KEY_MEMORY_RESET | 0xAA7B | - | Reset des CarKeyMemorys auf die ursprünglichen Codierwerte | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAA7B | - |
| SHD_ESH_NORMIERUNG_LOESCHEN | 0xD17C | - | Denormiert die angebene Scheibe | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD17C | - |
| SHD_ESH_KENNLINIE_LOESCHEN | 0xD17D | - | Löscht die Kennlinie. Es wird nur die Kennlinie gelöscht. Die Normierung bleibt erhalten | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD17D | - |
| SHD_ESH_RELAIS_STEUERN | 0xD17E | - | Steuert das/die Relais zum Verfahren des SHD / ESH an | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD17E | - |
| SHD_HALLSENSOREN | 0xD180 | - | Status der Hallsensoren | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD180 |
| SHD_ESH_TASTER | 0xD192 | - | Status / Simulation Taster Schiebedach | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD192 |
| ESH_VORHANDEN | 0xD193 | STAT_VORHANDEN_ESH | 0x00: elektrischer Schiebehimmel nicht vorhanden 0x01: elektrischer Schiebehimmel vorhanden | 0/1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHD_ESH_TASTER_VORHANDEN | 0xD194 | STAT_VORHANDEN_TASTER_SHD_ESH | 0x00: Kein SHD-Taster vorhanden 0x01: SHD-Taster vorhanden | 0/1 | - | - | char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHD_VORHANDEN | 0xD195 | STAT_VORHANDEN_SHD | 1: Schiebedach vorhanden | 0/1 | - | - | char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| SHD_BEWEGUNG | 0xD196 | - | Status Bewegung Schiebedach | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD196 |
| SHD_ESH_HALLVERSORGUNG | 0xD19E | - | Schaltet die Hallversorgung ein / aus | - | - | - | - | - | - | - | - | - | 2F | ARG_0xD19E | - |
| SHD_STATUS_DETAIL | 0xD1A6 | - | Erweiterter Status Schiebedach | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1A6 |
| SHD_RELAIS | 0xD1B9 | - | Status Relais Schiebedach | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1B9 |
| ESH_BEWEGUNG | 0xD1BA | - | Status elektrischer Schiebehimmel Bewegung | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1BA |
| ESH_HALLSENSOREN | 0xD1BB | - | Status Hallsensoren elektrischer Schiebehimmel | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1BB |
| ESH_RELAIS | 0xD1BC | - | Status Relais elektrischer Schiebehimmel | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1BC |
| ESH_STATUS_DETAIL | 0xD1BD | - | Erweiterte Informationen elektrischer Schiebehimmel | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1BD |
| SHD_STATISTIKZAEHLER_LESEN | 0xD1BE | - | Auslesen des Statistikzählers Schiebedach | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1BE |
| SHD_STATISTIKZAEHLER_LOESCHEN | 0xD1BF | - | Löscht den Statistikzähler Schiebedach | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD1BF | - |
| ESH_STATISTIKZAEHLER_LESEN | 0xD1C0 | - | Auslesen des Statistikzähler elektrischer Schiebehimmel | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD1C0 |
| ESH_STATISTIKZAEHLER_LOESCHEN | 0xD1C1 | - | Löscht den Statistikzähler elektrischer Schiebehimmel | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD1C1 | - |
| DWA_SINE_LIN | 0xDCA1 | STAT_VORHANDEN_LIN_SIRENE | 0: Keine LIN-Sirene verbaut 1: LIN-Sirene verbaut | 0/1 | - | - | char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DWA_SINE | 0xDCA2 | - | Status der Sirene / Neigungsgeber | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCA2 |
| DWA_SINE_BATT_LEVEL | 0xDCA3 | STAT_SIRENE_INTERNER_BATTERIE_LEVEL_NR | Status interne Batterie: Siehe Tabelle TAB_SINE_BATT_LEVEL | 0-n | - | high | unsigned char | TAB_SINE_BATT_LEVEL | - | - | - | - | 22 | - | - |
| DWA_LED | 0xDCA8 | - | Status/Steuern DWA-LED. Für Details siehe Sub-Tabelle(n) | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDCA8 | RES_0xDCA8 |
| DWA_SINE_NEIGUNG | 0xDCA9 | - | Neigungswinkel (X- und Y-Achse) des Fahrzeugs. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCA9 |
| DWA_CAR_KEY_MEMORY | 0xDCAA | - | Status / Steuern CarKeyMemory-Funktionalität der DWA | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDCAA | RES_0xDCAA |
| DWA_INTERN | 0xDCAC | STAT_DWA_INTERN_NR | 0: entschärft; | 0-n | - | - | int | TAB_DWA_INTERN | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DWA_ALARM_AUSGELOEST | 0xDCB0 | - | Status, welcher Alarm ausgelöst hat | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCB0 |
| DWA_VORHANDEN | 0xDCB1 | STAT_VORHANDEN_DWA | 0: Keine DWA verbaut 1: DWA verbaut | 0/1 | - | - | char | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DWA_USIS_EMPFINDLICHKEIT | 0xDCB2 | STAT_IRS_SENS_EMPFINDLICHKEIT_NR | Aktuelle Empflindlichkeitsstufe | 0-n | - | - | int | TAB_DWA_USIS_EMPF | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| DWA_SCHNELLTEST | 0xDCB5 | - | Aktiviert den DWA-Schnelltest Modus (Sensoren werden geschaerft) 0: Vorgang beenden 1: leise 2: normale Lautstärke | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCB5 | - |
| DWA_KLAPPENKONTAKTE | 0xDCDD | - | Status der eingelesenen Klappenkontakte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCDD |
| OBD_UEBERWACHUNG | 0xDD16 | - | Status der OBD-Überwachung | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xDD16 | RES_0xDD16 |
| SHD_ESH_THERMOMONITOR | 0x4100 | - | Konfiguriert die Thermomonitor Funktion | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x4100 | RES_0x4100 |
| SHD_ESH_FREIGABE_AKTIV | 0x4101 | - | Status der Freigabe | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x4101 | RES_0x4101 |
| SHD_ESH_EMERGENCY_PANIC | 0x4103 | - | gezielter Einsatz des Emergency- oder Panik-Modus | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x4103 | RES_0x4103 |
| ESH_BEWERTUNG_KENNLINIE_SCHIEBELAGE | 0x4107 | - | ESH_BEWERTUNG_KENNLINIE_SCHIEBELAGE | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4107 |
| SHD_BEWERTUNG_KENNLINIE_AUSSTELLLAGE_1 | 0x4108 | - | SHD_BEWERTUNG_KENNLINIE_AUSSTELLLAGE_1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4108 |
| SHD_BEWERTUNG_KENNLINIE_SCHIEBELAGE_1 | 0x4109 | - | SHD_BEWERTUNG_KENNLINIE_SCHIEBELAGE_1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4109 |
| DWA_ALARM_ANZAHL | 0x6012 | - | Anzahl ausgelöster Alarme | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x6012 |
| DWA_SINE_ALARMSPEICHER | 0x6013 | - | Lesen / schreiben des Alarmspeichers SINE | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x6013 | RES_0x6013 |
| DWA_SINE_FEHLERSPEICHER | 0x6014 | - | Lesen / Schreiben Fehlerspeicher SINE | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0x6014 | RES_0x6014 |
| DWA_SINE_VERPOLZAEHLER | 0x6015 | - | Lesen / Schreiben SINE Verpolzähler | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0x6015 | RES_0x6015 |
| _SHD_ESH_DEBUG_OUTPUT_KONF | 0xF000 | - | Umsetzung: MT | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF000 | RES_0xF000 |

<a id="table-tab-dwa-alarmspeicher"></a>
### TAB_DWA_ALARMSPEICHER

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Alarm FZD: Klappenkontakt Motorhaube |
| 0x01 | Alarm FZD: Klappenkontakt Fahrertür |
| 0x02 | Alarm FZD: Klappenkontakt Beifahrertür |
| 0x03 | Alarm FZD: Klappenkontakt Fahrertür Hinten |
| 0x04 | Alarm FZD: Klappenkontakt Beifahrertür Hinten |
| 0x05 | Alarm FZD: Klappenkontakt Heckklappe |
| 0x06 | Alarm FZD: Klappenkontakt Heckscheibe |
| 0x07 | Alarm FZD: Klappenkontakt VORHALT |
| 0x08 | Alarm FZD: Leitungsüberwachung LIN-SINE |
| 0x09 | Alarm FZD: Manipulation Authentisierung |
| 0x0A | Alarm FZD: Ultraschall Kanal A + B (rechts + links) |
| 0x0B | Alarm FZD: Ultraschall Kanal A (rechts) |
| 0x0C | Alarm FZD: Ultraschall Kanal B (links) |
| 0x0D | Alarm SINE: Neigungssensor: Neigung X-Achse |
| 0x0E | Alarm SINE: Neigungssensor: Neigung Y-Achse |
| 0x0F | Alarm SINE: Neigungssensor: Neigung X/Y-Achse |
| 0x10 | Alarm SINE: Unterbrechung Spannungsversorgung |
| 0x11 | Alarm SINE: LIN-Bus: kein Telegramm absetzbar |
| 0x12 | Alarm FZD: OBD-Kommunikation Ethernet |
| 0x13 | Alarm FZD: OBD-Kommunikation D-CAN |
| 0xFF | Unbekannter Alarm |

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

<a id="table-tab-dwa-pruefung"></a>
### TAB_DWA_PRUEFUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NEIN |
| 0x01 | JA |
| 0xFF | Signal ungültig |

<a id="table-tab-dwa-pruefung-inv"></a>
### TAB_DWA_PRUEFUNG_INV

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | JA |
| 0x01 | NEIN |
| 0xFF | Signal ungültig |

<a id="table-tab-dwa-referenzierung"></a>
### TAB_DWA_REFERENZIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht referenziert |
| 0x01 | referenziert |
| 0xFF | Signal ungültig |

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

<a id="table-tab-dwa-standheizung"></a>
### TAB_DWA_STANDHEIZUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / nicht verfügbar |
| 0x01 | Standheizung AUS |
| 0x02 | Standheizung EIN |
| 0x03 | Signal ungültig |

<a id="table-tab-dwa-standklima"></a>
### TAB_DWA_STANDKLIMA

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / nicht verfügbar |
| 0x01 | Standklimatisierung AUS |
| 0x02 | Standklimatisierung EIN |
| 0x03 | Signal ungültig |

<a id="table-tab-dwa-standlueftung"></a>
### TAB_DWA_STANDLUEFTUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion / nicht verfügbar |
| 0x01 | Standlüftung AUS |
| 0x02 | Standlüftung EIN |
| 0x03 | Signal ungültig |

<a id="table-tab-dwa-status-geblaese"></a>
### TAB_DWA_STATUS_GEBLAESE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Gebläse AUS |
| 0x01 | Gebläse EIN |
| 0x03 | Signal ungültig |

<a id="table-tab-dwa-status-obd-diagnose"></a>
### TAB_DWA_STATUS_OBD_DIAGNOSE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiv |
| 0x01 | aktiv |
| 0x03 | Ungültiger Wert |

<a id="table-tab-dwa-status-obd-high-speed-can"></a>
### TAB_DWA_STATUS_OBD_HIGH_SPEED_CAN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiv |
| 0x01 | Aktiv |
| 0xFF | Ungültiger Wert |

<a id="table-tab-dwa-status-restwaerme"></a>
### TAB_DWA_STATUS_RESTWAERME

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Restwärme AUS |
| 0x01 | Restwärme EIN |
| 0x03 | Signal ungültig |

<a id="table-tab-dwa-ueberwachung"></a>
### TAB_DWA_UEBERWACHUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht überwacht |
| 0x01 | überwacht |
| 0xFF | Signal ungültig |

<a id="table-tab-dwa-usis-empf"></a>
### TAB_DWA_USIS_EMPF

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Innenraumschutz (IRS) inaktiv |
| 0x01 | IRS Normalmode |
| 0x02 | Fenster / Dach offen |
| 0x03 | Klimaanlage / Zuheizer |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-panikmodus"></a>
### TAB_FH_PANIKMODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Panikmodus nicht freigeschalten |
| 0x01 | Panikmodus freigeschalten |
| 0x03 | Freigabe Panikmodus ungültig |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-bewegung"></a>
### TAB_FH_SHD_ESH_BEWEGUNG

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Element steht |
| 0x01 | Element fährt auf |
| 0x02 | Reversieren Mautlauf |
| 0x03 | Reversieren Emergency-Mode |
| 0x04 | Element fährt zu |
| 0x05 | Element fährt zu Emergency-Mode |
| 0x06 | Element fährt zu Panic-Mode |
| 0x07 | Einlernvorgang aktiv |
| 0x08 | stellt aus |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-einlernen"></a>
### TAB_FH_SHD_ESH_EINLERNEN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Einlernen ohne Kraftbegrenzung |
| 0x02 | Einlernen mit Kraftbegrenzung |
| 0x03 | Einlernen mit Kraftbegrenzung und Not Stop |
| 0x04 | Reserviert für Manuelles Einlernen |
| 0x05 | Normieren (nur für FH) |

<a id="table-tab-fh-shd-esh-einlernvorgang"></a>
### TAB_FH_SHD_ESH_EINLERNVORGANG

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung nicht gestartet |
| 0x01 | Initialisierung läuft |
| 0x02 | Initialisierung erfolgreich abgeschlossen |
| 0x03 | Abbruch durch Benutzer, Notstop |
| 0x04 | Abbruch durch Benutzer, Diagnose |
| 0x05 | Abbruch durch Reversieren |
| 0x06 | Fehler: Initialisierung |
| 0x07 | Fehler: keine FH-Freigabe |
| 0x08 | Fehler: Vorgang kann nicht gestartet werden, weil Tür offen |
| 0x09 | Fehler: Vorgang kann nicht gestartet werden, weil Verdeck/VHT offen |
| 0x0A | Fehler: Vorgang kann nicht gestartet werden, weil SG nicht codiert |
| 0xF0 | Fehler: allgemeiner Fehler |
| 0xFE | Element nicht unterstützt |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-emergency-panic-nr-mode"></a>
### TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | normal Verfahren |
| 0x01 | Emergency Modus |
| 0x02 | Panic Modus |

<a id="table-tab-fh-shd-esh-emergency-panic-nr-mode-arg"></a>
### TAB_FH_SHD_ESH_EMERGENCY_PANIC_NR_MODE_ARG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | normal verfahren |
| 0x01 | Emergency Modus |
| 0x02 | Panic Modus |

<a id="table-tab-fh-shd-esh-freigabe"></a>
### TAB_FH_SHD_ESH_FREIGABE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Freigabe |
| 0x01 | Freigabe vorhanden |
| 0x03 | Freigabe ungültig |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-hall-fehlerzustand"></a>
### TAB_FH_SHD_ESH_HALL_FEHLERZUSTAND

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Leitungsunterbrechung |
| 0x02 | Kurzschluss nach Masse |
| 0x03 | Kurzschluss nach Ubatt |
| 0x04 | Kurzschluss nach Ubatt oder Leitungsunterbrechung |
| 0xFF | ungültiger Zustand |

<a id="table-tab-fh-shd-esh-init"></a>
### TAB_FH_SHD_ESH_INIT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Element normiert, Adaptionsdaten Schließen gültig, Adaptionsdaten Senken gültig |
| 0x02 | Element denormiert, Adaptionsdaten Schließen gültig, Adaptionsdaten Senken gültig |
| 0x03 | Element normiert, Adaptionsdaten Schließen ungültig, Adaptionsdaten Senken gültig |
| 0x04 | Element denormiert, Adaptionsdaten Schließen ungültig, Adaptionsdaten Senken gültig |
| 0x05 | Element normiert, Adaptionsdaten Schließen gültig, Adaptionsdaten Senken ungültig |
| 0x06 | Element denormiert, Adaptionsdaten Schließen gültig, Adaptionsdaten Senken ungültig |
| 0x07 | Element normiert, Adaptionsdaten Schließen ungültig, Adaptionsdaten Senken ungültig |
| 0x08 | Element denormiert, Adaptionsdaten Schließen ungültig, Adaptionsdaten Senken ungültig |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-lage-nr"></a>
### TAB_FH_SHD_ESH_LAGE_NR

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Ausstelllage |
| 0x02 | Schiebelage |
| 0xFF | Funktion nicht unterstützt |

<a id="table-tab-fh-shd-esh-lage-nr-arg"></a>
### TAB_FH_SHD_ESH_LAGE_NR_ARG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Ausstelllage |
| 0x02 | Schiebelage |

<a id="table-tab-fh-shd-esh-lage-nr-arg-entw"></a>
### TAB_FH_SHD_ESH_LAGE_NR_ARG_ENTW

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Ausstelllage |
| 0x02 | Schiebelage |

<a id="table-tab-fh-shd-esh-motorstopreason"></a>
### TAB_FH_SHD_ESH_MOTORSTOPREASON

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Motor läuft |
| 0x01 | Position erreicht |
| 0x02 | Bewegung abgebrochen durch Bedienkozept |
| 0x03 | Normierung gefunden |
| 0x04 | Nachnormierung durchgeführt |
| 0x05 | Einklemmen erkannt |
| 0x06 | Reversierposition erreicht |
| 0x07 | Blockieren erkannt |
| 0x08 | Motor steht |
| 0x09 | Sicherheitszeitüberlauf |
| 0x0A | Drehriuchtung passt nicht zur Hallauswertung |
| 0x0B | falsche Zielposition (zu niedrig) |
| 0x0C | falsche Zielposition (zu hoch) |
| 0x0D | Motor zu warm |
| 0x0E | Fehler in der Motoransteuerungs-HW |
| 0x0F | Motorkurzschluss |
| 0x10 | Reset während Motorbewegung |
| 0x11 | HALL Plus verloren |
| 0x12 | Motorspannung nicht im Betriebsbereich |
| 0x13 | Fehler in Hallsensoren-HW |
| 0x14 | keine OSEK-Rechenzeit für EkS-Algorythmus zugeteilt |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-motortemperatur"></a>
### TAB_FH_SHD_ESH_MOTORTEMPERATUR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Motortemperatur OK |
| 0x02 | Motortemperatur 90% des maximal zulässigen Wertes erreicht |
| 0x03 | Motortemperatur 100% des maximal zulässigen Wertes erreicht |
| 0xFF | Motortemperatur ungültig |

<a id="table-tab-fh-shd-esh-mt-lieferant"></a>
### TAB_FH_SHD_ESH_MT_LIEFERANT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Brose |
| 0x02 | Küster |
| 0x03 | Magna |
| 0x04 | Webasto |
| 0x05 | Inalfa |
| 0x06 | Arvin Meritor |
| 0x07 | Lames |
| 0xFE | Dummy Motortreiber |
| 0xFF | ungültiger Hersteller |

<a id="table-tab-fh-shd-esh-position"></a>
### TAB_FH_SHD_ESH_POSITION

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Element in Bewegung |
| 0x01 | Element komplett geschlossen |
| 0x02 | Element komplett offen |
| 0x03 | Element steht in Zwischenpositon |
| 0x04 | Element steht auf Position Kurzhub  nur FH |
| 0x05 | Element steht auf Position Langhub  nur FH |
| 0x06 | Element steht auf Position Cabrio nur FH |
| 0x07 | Element steht in Ausstellage nur SHD/PDK |
| 0x08 | Element steht in Komfortposition nur PDK |
| 0x09 | Element steht in Anti-Wummer Position nur SHD |
| 0x0A | Element steht in Crash-Position |
| 0xA0 | Element steht in Demontageposition |
| 0xA1 | Element steht in Serviceposition A |
| 0xA2 | Element steht in Serviceposition B |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-serviceposition"></a>
### TAB_FH_SHD_ESH_SERVICEPOSITION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Montageposition |
| 0x01 | Demontageposition |
| 0x02 | Serviceposition A |
| 0x03 | Serviceposition B |

<a id="table-tab-fh-shd-esh-sfk1"></a>
### TAB_FH_SHD_ESH_SFK1

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzhub |
| 0x01 | Langhub/Einstiegshilfe |
| 0x02 | Cabrio Position |
| 0x03 | Crash Position |
| 0x04 | Windabweiser |
| 0x05 | Komfort-Position |
| 0x06 | Anti-Wummer-Position |

<a id="table-tab-fh-shd-esh-status-routine"></a>
### TAB_FH_SHD_ESH_STATUS_ROUTINE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Service noch nicht angefordert |
| 0x01 | Pending (Auftrag angenommen, aber noch nicht gestartet) |
| 0x02 | Routine kann nicht ausgeführt werden |
| 0x03 | Routine wird ausgeführt |
| 0x04 | Routine erfolgreich beendet |
| 0x05 | Routine beendet mit Fehler |
| 0x06 | Routine abgebrochen |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-stat-eeprom"></a>
### TAB_FH_SHD_ESH_STAT_EEPROM

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Checksumme IO |
| 0x02 | Checksumme NIO |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-taster-richtung"></a>
### TAB_FH_SHD_ESH_TASTER_RICHTUNG

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Betätigung |
| 0x01 | Öffnen |
| 0x02 | Schliessen |
| 0x03 | Maut-Öffnen |
| 0x04 | Maut-Schliessen |
| 0x05 | Heben |

<a id="table-tab-fh-shd-esh-thermomonitor-aktiv"></a>
### TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Normalbetrieb |
| 0x01 | Thermo 90 aktiv |
| 0x02 | Thermo 100 aktiv |
| 0xFF | ungültig |

<a id="table-tab-fh-shd-esh-thermomonitor-aktiv-arg"></a>
### TAB_FH_SHD_ESH_THERMOMONITOR_AKTIV_ARG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Normalbetrieb |
| 0x01 | Thermo 90 aktiv |
| 0x02 | Thermo 100 aktiv |
| 0xFF | ungültig |

<a id="table-tab-fh-shd-esh-verfahren"></a>
### TAB_FH_SHD_ESH_VERFAHREN

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Aktion |
| 0x01 | Öffnen |
| 0x02 | Schliessen |
| 0x03 | Maut öffnen |
| 0x04 | Maut schliessen |
| 0x05 | Heben / Ausstellen |
| 0xFE | Element nicht unterstützt |
| 0xFF | ungültiger Wert |

<a id="table-tab-fh-shd-esh-wachhalten"></a>
### TAB_FH_SHD_ESH_WACHHALTEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
| 0xFF | ungültig |

<a id="table-tab-fh-shd-esh-zustand-tuer"></a>
### TAB_FH_SHD_ESH_ZUSTAND_TUER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Tür geschlossen |
| 0x01 | Tür offen |
| 0x02 | Tür in Vorraste |
| 0x03 | Türstatus ungültig |
| 0xFF | Signal ungültig |

<a id="table-tab-relais-number"></a>
### TAB_RELAIS_NUMBER

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Relais 1 |
| 0x02 | Relais 2 |

<a id="table-tab-relais-richtung"></a>
### TAB_RELAIS_RICHTUNG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Relais auf Ubatt |
| 0x01 | Relais auf Masse |

<a id="table-tab-shd-esh"></a>
### TAB_SHD_ESH

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xA1 | SHD |
| 0xA2 | ESH |
| 0xB0 | SHD + ESH |

<a id="table-tab-shd-esh-denorm-urs"></a>
### TAB_SHD_ESH_DENORM_URS

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | PDD_DIAG_NORMALIZED normiert |
| 0x01 | PDD_DIAG_INITSTART einlernen über Diagnose oder Taster |
| 0x02 | PDD_DIAG_DIAGCOMMAND Absichtliche Entnormierung über Diagnose |
| 0x03 | PDD_DIAG_ERRCODING zur Zeit nicht benutzt |
| 0x04 | PDD_DIAG_HALLOFF zur Zeit nicht benutzt |
| 0x05 | PDD_DIAG_POSITIONERRI Motortreiber wurde nicht ordnungsgemäß beendet |
| 0x06 | PDD_DIAG_POSITIONERRM zur Zeit nicht benutzt |
| 0x07 | PDD_DIAG_AFTERRESET Beim Start des Motortreibers wurde keine gültige Position im EEPROM gefunden |
| 0x08 | PDD_DIAG_ERRHALL Notabschaltung wegen Überspannung an den Hallsensoren |
| 0x09 | PDD_DIAG_UNKNOWN |
| 0xFF | PDD_DIAG_DENORM_INVALID ungültig (Initialisierungswert) |

<a id="table-tab-shd-esh-entw"></a>
### TAB_SHD_ESH_ENTW

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xA1 | SHD |
| 0xA2 | ESH |
| 0xB0 | SHD + ESH |

<a id="table-tab-shd-esh-reversier-urs"></a>
### TAB_SHD_ESH_REVERSIER_URS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | PDD_DIAG_NOT_REV nicht reversiert |
| 0x01 | PDD_DIAG_PINCH einklemmen erkannt |
| 0x02 | PDD_DIAG_EMERGENCY_PINCH einklemmen im Emergency Mode |
| 0x03 | PDD_DIAG_STALL blockieren erkannt |
| 0x04 | PDD_DIAG_PANIC_STALL blockieren im Panic Mode |
| 0xFF | PDD_DIAG_INVALID ungültig (Initialisierungswert) |

<a id="table-tab-shd-esh-strict"></a>
### TAB_SHD_ESH_STRICT

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xB0 | SHD+ESH |

<a id="table-tab-sine-batt-level"></a>
### TAB_SINE_BATT_LEVEL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Batterie leer |
| 0x01 | Batterie gut |
| 0x02 | Batterie neu |
| 0xFF | Ungültiges Signal |

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

<a id="table-tab-reset-reason"></a>
### _TAB_RESET_REASON

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | slot empty |
| 0x01 | power on reset |
| 0x02 | WD reset |
| 0xFF | invalid value |

<a id="table-tab-dwa-trigger-status"></a>
### _TAB_DWA_TRIGGER_STATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht kodiert in EEPROM |
| 0x01 | Deaktiviert durch den Nutzer ueber den Funkschluessel |
| 0x02 | Deaktiviert wegen Unterspannung |
| 0x03 | Nicht ueberwacht in der DWA |
| 0x04 | Referenzierungsphase |
| 0x05 | Aktiviert und in der Alarmtabelle |
| 0x06 | Fehler in der Referenzierungsphase |
| 0xFF | Ungueliger Wert |

<a id="table-tab-dwa-status-fenster-position"></a>
### TAB_DWA_STATUS_FENSTER_POSITION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fenster geschlossen |
| 0x01 | Zwischenstellung |
| 0x02 | Fenster offen |
| 0x03 | Signal ungÃ¼ltig |

<a id="table-tab-usis-mode"></a>
### _TAB_USIS_MODE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | inactive |
| 0x01 | echo mode |
| 0x02 | doppler mode |
| 0xFF | invalid value |

<a id="table-tab-serial-interface"></a>
### _TAB_SERIAL_INTERFACE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | serial interface inactive |
| 0x01 | serial interface inactive (routine active) |
| 0xFF | invalid value |

<a id="table-tab-usis-selftest-result"></a>
### _TAB_USIS_SELFTEST_RESULT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | no error |
| 0x01 | error |
| 0xFF | invalid value |

<a id="table-tab-usis-alarm-type-alarm-source"></a>
### _TAB_USIS_ALARM_TYPE_ALARM_SOURCE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | no alarm |
| 0x01 | A channel |
| 0x02 | B channel |
| 0x03 | both channel |
| 0xFF | invalid value |

<a id="table-tab-usis-alarm-type-activation-mode"></a>
### _TAB_USIS_ALARM_TYPE_ACTIVATION_MODE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Not active |
| 0x01 | Normal mode |
| 0x02 | Window or roof open |
| 0x03 | Air conditioning on |
| 0xFF | invalid value |

<a id="table-tab-usis-data-environment-thermal-steb"></a>
### _TAB_USIS_DATA_ENVIRONMENT_THERMAL_STEB

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | -40°C .. -15°C |
| 0x01 | -15°C .. + 5°C |
| 0x02 | +5°C .. +45°C |
| 0x03 | +45°C .. +65°C |
| 0x04 | +65°C .. +85°C |
| 0xFF | invalid value |

<a id="table-tab-usis-data-environment-read-activation"></a>
### _TAB_USIS_DATA_ENVIRONMENT_READ_ACTIVATION

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | no change |
| 0x01 | Normal mode |
| 0x02 | Window or roof open |
| 0x03 | Air conditioning on |
| 0xFF | invalid value |

<a id="table-tab-usis-cmd-echodopplercounter-reset"></a>
### _TAB_USIS_CMD_ECHODOPPLERCOUNTER_RESET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | echo counter |
| 0x02 | doppler counter |
| 0x03 | echo/doppler transitions history |

<a id="table-tab-usis-cmd-totalalarmcounter-reset"></a>
### _TAB_USIS_CMD_TOTALALARMCOUNTER_RESET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | A channel |
| 0x02 | B channel |
| 0x03 | both channels |

<a id="table-tab-usis-echo-delta-drift-zone"></a>
### _TAB_USIS_ECHO_DELTA_DRIFT_ZONE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | near the FZD (Zone #1) |
| 0x01 | far away from FZD (Zone #2) |

<a id="table-tab-usis-gain"></a>
### _TAB_USIS_GAIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | gain low |
| 0x01 | gain medium low |
| 0x02 | gain medium high |
| 0x03 | gain high |

<a id="table-tab-port-dio-write"></a>
### _TAB_PORT_DIO_WRITE

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | CMD_DWA_LED |
| 0x02 | CMD_OPEN_LOAD_DWA_LED |
| 0x03 | CMD_SHD_M1 |
| 0x04 | CMD_SHD_M2 |
| 0x05 | CMD_ESH_M1 |
| 0x06 | CMD_ESH_M2 |
| 0x07 | CMD_30F_SW_HALL |
| 0x0A | CMD_TXON |
| 0x0B | CMD_SHUNT |
| 0x0C | CMD_TXD 12 |
| 0x0D | CMD_TXECO1 |
| 0x0E | CMD_TXECO2 |
| 0x0F | CMD_RXENA |
| 0x10 | CMD_GDOP |
| 0x11 | CMD_GH1 |
| 0x12 | CMD_OPHFSUP |
| 0x13 | CMD_GH2 |
| 0x1E | CMD_CONF_VAR |
| 0x1F | CMD_GL1 |
| 0x20 | CMD_GL2 |
| 0x21 | CMD_OPLFSUP |

<a id="table-tab-port-fio-write"></a>
### _TAB_PORT_FIO_WRITE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | PWM_SLIDER_LED |
| 0x02 | F80 |

<a id="table-tab-switch-eep"></a>
### _TAB_SWITCH_EEP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Unlock |
| 0x01 | Lock |
