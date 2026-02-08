# rdc_03.prg

- Jobs: [32](#jobs)
- Tables: [61](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | RDC-SGBD |
| ORIGIN | BMW EF-331 Florian_Koerner |
| REVISION | 1.000 |
| AUTHOR | Vector PSF2 Vl, Beru BES2 Rapp |
| COMMENT | N/A |
| PACKAGE | 1.12 |
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
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
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
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
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
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
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

Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF = Status der aktiven Fehlermeldung nicht feststellbar |
| STAT_ROE_AKTIV_TEXT | string | Interpretation von STAT_ROE_AKTIV table UDS_TAB_ROE_AKTIV TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-start"></a>
### STEUERN_ROE_START

Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-stop"></a>
### STEUERN_ROE_PERSISTENT_STOP

Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-start"></a>
### STEUERN_ROE_PERSISTENT_START

Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (116 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (61 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [IORTTEXTE](#table-iorttexte) (12 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (7 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (23 × 16)
- [RES_0X0E50](#table-res-0x0e50) (3 × 11)
- [RES_0X0E51](#table-res-0x0e51) (3 × 11)
- [RES_0X0E52](#table-res-0x0e52) (3 × 11)
- [RES_0XDCCF](#table-res-0xdccf) (9 × 10)
- [RES_0XDCCA](#table-res-0xdcca) (40 × 10)
- [RES_0XDCD1](#table-res-0xdcd1) (9 × 10)
- [RES_0XDCD2](#table-res-0xdcd2) (5 × 10)
- [RES_0XDCCB](#table-res-0xdccb) (40 × 10)
- [RES_0XDCCE](#table-res-0xdcce) (32 × 10)
- [RES_0XDCC4](#table-res-0xdcc4) (13 × 10)
- [RES_0XDCCC](#table-res-0xdccc) (32 × 10)
- [RES_0XDCC2](#table-res-0xdcc2) (13 × 10)
- [RES_0XDCC8](#table-res-0xdcc8) (5 × 10)
- [ARG_0XDCC0](#table-arg-0xdcc0) (2 × 12)
- [RES_0XDCC1](#table-res-0xdcc1) (13 × 10)
- [RES_0XDCC3](#table-res-0xdcc3) (13 × 10)
- [RES_0XDCCD](#table-res-0xdccd) (32 × 10)
- [ARG_0XDCC6](#table-arg-0xdcc6) (2 × 12)
- [TAB_RDC_STEUERFUNKTIONEN](#table-tab-rdc-steuerfunktionen) (10 × 2)
- [TAB_RDC_SET_RESET](#table-tab-rdc-set-reset) (2 × 2)
- [RES_0XDCD3](#table-res-0xdcd3) (5 × 10)
- [RES_0XDCC5](#table-res-0xdcc5) (32 × 10)
- [TAB_RDC_BEKANNT_NICHT_BEKANNT](#table-tab-rdc-bekannt-nicht-bekannt) (3 × 2)
- [TAB_RDC_CONFIRMED](#table-tab-rdc-confirmed) (3 × 2)
- [TAB_RDC_DTC_ACTIVE](#table-tab-rdc-dtc-active) (3 × 2)
- [TAB_RDC_CAL_ACTIVE](#table-tab-rdc-cal-active) (3 × 2)
- [TAB_RDC_LIN_STATUS](#table-tab-rdc-lin-status) (3 × 2)
- [TAB_RDC_TIMEOUT](#table-tab-rdc-timeout) (3 × 2)
- [TAB_RDC_BANDMODE_ACTIVE](#table-tab-rdc-bandmode-active) (3 × 2)
- [TAB_RDC_STARTED](#table-tab-rdc-started) (3 × 2)
- [TAB_RDC_ON_OFF](#table-tab-rdc-on-off) (3 × 2)
- [TAB_RDC_VEHICLE_RUNNING](#table-tab-rdc-vehicle-running) (3 × 2)
- [TAB_RDC_DETECTED](#table-tab-rdc-detected) (3 × 2)
- [TAB_RDC_KEY_PRESSED](#table-tab-rdc-key-pressed) (3 × 2)
- [RES_0XDCC9](#table-res-0xdcc9) (40 × 10)
- [RES_0XDCC7](#table-res-0xdcc7) (13 × 10)
- [TAB_RDC_RAD_POSITION_NR](#table-tab-rdc-rad-position-nr) (10 × 2)
- [TAB_RDC_CHANGED](#table-tab-rdc-changed) (3 × 2)
- [TAB_RDC_AKTIV_INAKTIV](#table-tab-rdc-aktiv-inaktiv) (3 × 2)
- [RES_0XDCD0](#table-res-0xdcd0) (9 × 10)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 66 rows × 2 columns

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
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 116 rows × 2 columns

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

Dimensions: 24 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
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

Dimensions: 11 rows × 3 columns

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
| 0xXY | -- | unbekannter Diagnose-Mode |

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 61 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x022000 | Energiesparmode aktiv | 1 |
| 0x02FF20 | DM_TEST_APPL | 1 |
| 0x481F80 | RDC-Steuergeraet im Bandmodus | 0 |
| 0x481F81 | Steuergeraet defekt (EEPROM-Fehler) | 0 |
| 0x481F84 | Raderkennung nicht moeglich | 0 |
| 0x481F86 | RDC-Sender vorne links Datenuebertragung gestoert | 0 |
| 0x481F87 | RDC-Sender vorne rechts Datenuebertragung gestoert | 0 |
| 0x481F88 | RDC-Sender hinten links Datenuebertragung gestoert | 0 |
| 0x481F89 | RDC-Sender hinten rechts Datenuebertragung gestoert | 0 |
| 0x481F8A | RDC-Antenne Datenuebertragung gestoert | 0 |
| 0x481F8B | Radelektronik vorne links kein Empfang | 0 |
| 0x481F8C | Radelektronik vorne rechts kein Empfang | 0 |
| 0x481F8D | Radelektronik hinten links kein Empfang | 0 |
| 0x481F8E | Radelektronik hinten rechts kein Empfang | 0 |
| 0x481F94 | RDC-Antenne defekt (RAM-Fehler) | 0 |
| 0x481F99 | RDC-Antenne defekt (ROM-Fehler) | 0 |
| 0x481F9E | RDC-Antenne falsches Bauteil | 0 |
| 0x481F9F | RDC-Antenne falsches Bauteil (CRC) | 0 |
| 0x481FA0 | Radelektronik vorne links defekt | 0 |
| 0x481FA1 | Radelektronik vorne rechts defekt | 0 |
| 0x481FA2 | Radelektronik hinten links defekt | 0 |
| 0x481FA3 | Radelektronik hinten rechts defekt | 0 |
| 0x481FA4 | Radelektronik (Position unbekannt) defekt | 0 |
| 0x481FA5 | Unterspannung KL30 | 1 |
| 0x481FA6 | Steuergeraet defekt (Betriebsspannung) | 0 |
| 0x481FA7 | Ueberspannung KL30 (Schutzschaltung ausgeloest) | 1 |
| 0x481FA8 | Steuergeraet defekt (ROM-Fehler) | 0 |
| 0x481FA9 | Steuergeraet defekt (RAM-Fehler) | 0 |
| 0x481FAA | Ueberspannung KL30 | 1 |
| 0x481FB0 | RDC-Sender vorne links Leitungsunterbrechung | 0 |
| 0x481FB1 | RDC-Sender vorne rechts Leitungsunterbrechung | 0 |
| 0x481FB2 | RDC-Sender hinten links Leitungsunterbrechung | 0 |
| 0x481FB3 | RDC-Sender hinten rechts Leitungsunterbrechung | 0 |
| 0x481FB4 | RDC-Antenne Leitungsunterbrechung | 0 |
| 0x481FB5 | RDC-Sender vorne links Kurzschluss | 0 |
| 0x481FB6 | RDC-Sender vorne rechts Kurzschluss | 0 |
| 0x481FB7 | RDC-Sender hinten links Kurzschluss | 0 |
| 0x481FB8 | RDC-Sender hinten rechts Kurzschluss | 0 |
| 0x481FB9 | RDC-Antenne Kurzschluss | 0 |
| 0x481FBA | RDC-Sender vorne links defekt (LF-Triggerspule) | 0 |
| 0x481FBB | RDC-Sender vorne rechts defekt (LF-Triggerspule) | 0 |
| 0x481FBC | RDC-Sender hinten links defekt (LF-Triggerspule) | 0 |
| 0x481FBD | RDC-Sender hinten rechts defekt (LF-Triggerspule) | 0 |
| 0x481FBE | Funkverbindung durch Fremdeinfluss gestoert | 1 |
| 0x481FC0 | Signatur über Nettocodierdaten ist ungueltig | 0 |
| 0x481FC1 | Steuergeraet ist nicht für das Fahrzeug codiert, in welchem es verbaut ist | 0 |
| 0x481FC2 | Steuergerät ist nicht codiert | 0 |
| 0x481FC3 | Fehler während der Codierdaten Transaktion aufgetreten | 0 |
| 0x481FC4 | Die waehrend einer Codierdaten Transaktion gesendeten Daten sind unplausibel | 0 |
| 0xD1040B | K-CAN Bus | 1 |
| 0xD10414 | K-CAN Control Module Bus OFF | 1 |
| 0xD10BFF | DM_TEST_COM | 1 |
| 0xD11400 | Botschaft (Klemmen, 0x12F) fehlt, Empfänger RDC (K-CAN), Sender CAS (FlexRay) | 1 |
| 0xD11401 | Botschaft (Aussentemperatur, 0x2CA) fehlt, Empfänger RDC (K-CAN), Sender KOMBI (FlexRay) | 1 |
| 0xD11402 | Botschaft (Kilometerstand, 0x330) fehlt, Empfänger RDC (K-CAN), Sender KOMBI (FlexRay) | 1 |
| 0xD11403 | Botschaft (Daten Antriebsstrang, 0x3F9) fehlt, Empfänger RDC (K-CAN), Sender DME1 (FlexRay) | 1 |
| 0xD11404 | Botschaft (Uhrzeit/Datum, 0x2F8) fehlt, Empfänger RDC (K-CAN), Sender KOMBI (FlexRay) | 1 |
| 0xD11405 | Botschaft (Geschwindigkeit Fahrzeug, 0x1A1) fehlt, Empfänger RDC (K-CAN), Sender ICM_QL (FlexRay) | 1 |
| 0xD11406 | Botschaft (Einheiten, 0x2F7) fehlt, Empfänger RDC (K-CAN), Sender KOMBI (FlexRay) | 1 |
| 0xD14302 | CAN Zeitueberschreitung | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

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

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x1701 | Systemzeit | sec | high | unsigned int | - | 1 | 1 | 0 |
| 0x1704 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 1 | 0 |
| 0x1703 | Temperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x1705 | EmpfangsId | dez | high | unsigned int | - | 1 | 1 | 0 |
| 0x0005 | SendeId | dez | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFF | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 12 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x200001 | DM_Queue_Full | 1 |
| 0x200002 | DM_Queue_Deleted | 1 |
| 0x200003 | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 1 |
| 0x200004 | Ausfall Botschaft Fahrzeugzustand | 1 |
| 0x200010 | EEPROM-Fehler (Wrong Config ID) | 0 |
| 0x200011 | EEPROM-Fehler (Write Failed) | 0 |
| 0x200012 | EEPROM-Fehler (Read Failed) | 0 |
| 0x200013 | EEPROM-Fehler (Control Failed) | 0 |
| 0x200014 | EEPROM-Fehler (Erase Failed) | 0 |
| 0x200015 | EEPROM-Fehler (Write All Failed) | 0 |
| 0x200016 | EEPROM-Fehler (Read All Failed) | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x1701 | Systemzeit | sec | high | unsigned int | - | 1 | 1 | 0 |
| 0x1704 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 1 | 0 |
| 0x1703 | Temperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x1705 | EmpfangsId | dez | high | unsigned int | - | 1 | 1 | 0 |
| 0x0005 | SendeId | dez | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFF | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 23 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STATUS_HS_INAKTIVEREIGNIS1_LESEN | 0xDCCF | - | Auslesen eines Inaktiveignisses des Historienspeichers. Inaktivereignis 1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCF |
| STATUS_HS_INAKTIVEREIGNIS2_LESEN | 0xDCD0 | - | Auslesen eines Inaktiveignisses des Historienspeichers. Inaktivereignis 2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD0 |
| STATUS_HS_INAKTIVEREIGNIS3_LESEN | 0xDCD1 | - | Auslesen eines Inaktiveignisses des Historienspeichers. Inaktivereignis 3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD1 |
| STATUS_HS_KALIBRIEREREIGNIS1_LESEN | 0xDCCC | - | Auslesen eines Kalibriereignisses des Historienspeichers. Kalibrierereignis 1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCC |
| STATUS_HS_KALIBRIEREREIGNIS2_LESEN | 0xDCCD | - | Auslesen eines Kalibriereignisses des Historienspeichers. Kalibrierereignis 2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCD |
| STATUS_HS_KALIBRIEREREIGNIS3_LESEN | 0xDCCE | - | Auslesen eines Kalibriereignisses des Historienspeichers. Kalibrierereignis 3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCE |
| STATUS_HS_WARNEREIGNIS1_LESEN | 0xDCC9 | - | Auslesen eines Warneignisses des Historienspeichers. Warnereignis 1 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC9 |
| STATUS_HS_WARNEREIGNIS2_LESEN | 0xDCCA | - | Auslesen eines Warneignisses des Historienspeichers. Warnereignis 2 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCA |
| STATUS_HS_WARNEREIGNIS3_LESEN | 0xDCCB | - | Auslesen eines Warneignisses des Historienspeichers. Warnereignis 3 | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCCB |
| STATUS_HS_WARNUNGSZAEHLER_LESEN | 0xDCC8 | - | Auslesen der Warnungszaehler des Historienspeichers | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC8 |
| STATUS_HS_ZAEHLER_WEICHE_WARNUNG_LESEN | 0xDCD3 | - | Auslesen der Zaehler aus dem Historienspeicher, welche die Auftretenshaeufigkeit der weichen Warnung wiedergeben. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD3 |
| STATUS_IO_RDC_LESEN | 0xDCC5 | - | Status Abfrage | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC5 |
| STATUS_MESSDATENBLOCK1_LESEN | 0xDCC1 | - | Mit dem Job STATUS_MESSDATENBLOCK1_LESEN werden die Daten aus den Messdatenblock 1 gelesen. Die Zuordnung der Blöcke zu den Radpositionen variiert und wird vom SG zugewiesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC1 |
| STATUS_MESSDATENBLOCK2_LESEN | 0xDCC2 | - | Mit dem Job STATUS_MESSDATENBLOCK2_LESEN werden die Daten aus den Messdatenblock 2 gelesen. Die Zuordnung der Blöcke zu den Radpositionen variiert und wird vom SG zugewiesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC2 |
| STATUS_MESSDATENBLOCK3_LESEN | 0xDCC3 | - | Mit dem Job STATUS_MESSDATENBLOCK3_LESEN werden die Daten aus den Messdatenblock 3 gelesen. Die Zuordnung der Blöcke zu den Radpositionen variiert und wird vom SG zugewiesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC3 |
| STATUS_MESSDATENBLOCK4_LESEN | 0xDCC4 | - | Mit dem Job STATUS_MESSDATENBLOCK4_LESEN werden die Daten aus den Messdatenblock 4 gelesen. Die Zuordnung der Blöcke zu den Radpositionen variiert und wird vom SG zugewiesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC4 |
| STATUS_MESSDATENBLOCK5_LESEN | 0xDCC7 | - | Mit dem Job STATUS_MESSDATENBLOCK5_LESEN werden die Daten aus den Messdatenblock 5 gelesen. Die Zuordnung der Blöcke zu den Radpositionen variiert und wird vom SG zugewiesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCC7 |
| STATUS_WEICHE_WARNUNG_LESEN | 0xDCD2 | - | Mit dem Job STATUS_WEICHE_WARNUNG_LESEN wird der aktuelle Status der weichen Warnung ausgelesen. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDCD2 |
| STEUERN_DIGITAL_RDC | 0xDCC6 | - | Setzen diverser Bandmodi  Achtung: Busdiagnose und Tests im Stand nur mit RDC Generation2 | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC6 | - |
| STEUERN_RADELEKTRONIK_VORGEBEN | 0xDCC0 | - | Radelektronik vorgeben. Der Job weist der Radelektronik die durch das 1.Argument angewählt wurde, ihre Position am Fahrzeug zu (z.B. vorn rechts). Die Radelektronik kennt sonst ihre Position im Fahrzeug nicht. Sie kennt nur ihre ID. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDCC0 | - |
| TIME_2MS | 0x0E50 | - | - | - | - | - | - | - | - | - | - | 32 | 22 | - | RES_0x0E50 |
| TIME_10MS | 0x0E51 | - | - | - | - | - | - | - | - | - | - | 32 | 22 | - | RES_0x0E51 |
| TIME_20MS | 0x0E52 | - | - | - | - | - | - | - | - | - | - | 32 | 22 | - | RES_0x0E52 |

<a id="table-res-0x0e50"></a>
### RES_0X0E50

Dimensions: 3 rows × 11 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | BESCHREIBUNG | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIME_AVG_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | liest die durchschnittliche Zykluszeit der 2ms Task aus | durchschnittliche Zykluszeit der 2ms Task |
| STAT_TIME_MIN_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | liest die Minimale Zykluszeit der 2ms Task aus | minimale Zykluszeit der 2ms Task |
| STAT_TIME_MAX_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | liest die maximale Zykluszeit der 2ms Task aus | maximale Zykluszeit der 2ms Task |

<a id="table-res-0x0e51"></a>
### RES_0X0E51

Dimensions: 3 rows × 11 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | BESCHREIBUNG | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIME_AVG_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die durchschnittliche Zykluszeit der 10ms Task aus | durchschnittliche Zykluszeit der 10ms Task |
| STAT_TIME_MIN_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die minimale Zykluszeit der 10ms Task aus | minimale Zykluszeit der 10ms Task |
| STAT_TIME_MAX_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die maximale Zykluszeit der 10ms Task aus | maximale Zykluszeit der 10ms Task |

<a id="table-res-0x0e52"></a>
### RES_0X0E52

Dimensions: 3 rows × 11 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | BESCHREIBUNG | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIME_AVG_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die durchschnittliche Zykluszeit der 10ms Task aus | durchschnittliche Zykluszeit der 20ms Task |
| STAT_TIME_MIN_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die minimale Zykluszeit der 10ms Task aus | minimale Zykluszeit der 20ms Task |
| STAT_TIME_MAX_WERT | ms | high | unsigned int | - | - | 0.00125 | - | - | Liest die maximale Zykluszeit der 10ms Task aus | maximale Zykluszeit der 20ms Task |

<a id="table-res-0xdccf"></a>
### RES_0XDCCF

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | 0-n | - | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |

<a id="table-res-0xdcca"></a>
### RES_0XDCCA

Dimensions: 40 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-res-0xdcd1"></a>
### RES_0XDCD1

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | 0-n | - | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |

<a id="table-res-0xdcd2"></a>
### RES_0XDCD2

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WEICHE_WARNUNG_UNSPEZIFISCH_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Reifenfuelldruck auf allen Radpositionen pruefen, 0 = inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_WEICHE_WARNUNG_VL_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Reifenfuelldruck vorne links pruefen, 0 = inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_WEICHE_WARNUNG_VR_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Reifenfuelldruck vorne rechts pruefen, 0 = inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_WEICHE_WARNUNG_HR_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Reifenfuelldruck hinten rechts pruefen, 0 = inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_WEICHE_WARNUNG_HL_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Reifenfuelldruck hinten links pruefen, 0 = inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-res-0xdccb"></a>
### RES_0XDCCB

Dimensions: 40 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-res-0xdcce"></a>
### RES_0XDCCE

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-res-0xdcc4"></a>
### RES_0XDCC4

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | - | int | - | - | - | 1000 | - | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | - | char | - | - | - | - | - | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | - | int | - | - | - | 1000 | - | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | - | unsigned int | - | - | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | - | unsigned char | - | - | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent. |
| STAT_RSSI_PEGEL | 0-n | - | int | - | - | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | - | unsigned int | - | - | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor |
| STAT_RADELEKTRONIK_STATUS | 0-n | - | unsigned char | - | - | - | - | - | Status Meldung der Radelektronik des angewählten Rads ACHTUNG: Rückgabe in STAT_RADELEKTRONIK_ID_TEXT!! |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | - | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad , 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-res-0xdccc"></a>
### RES_0XDCCC

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-res-0xdcc2"></a>
### RES_0XDCC2

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen., Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | - | int | - | - | - | 1000 | - | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | - | char | - | - | - | - | - | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | - | int | - | - | - | 1000 | - | Vorgegebener Solldruck des ausgewählten Rad |
| STAT_GUTEMPFAENGE | 0-n | - | unsigned int | - | - | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | - | unsigned char | - | - | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | - | int | - | - | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | - | unsigned int | - | - | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | - | unsigned char | - | - | - | - | - | Status Meldung der Radelektronik des angewählten Rad |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | - | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad , 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-res-0xdcc8"></a>
### RES_0XDCC8

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_HARTE_WARNUNG_VL | 0-n | - | unsigned char | - | - | - | - | - | Zaehler der harten Warnungen vorne links |
| STAT_ZAEHLER_HARTE_WARNUNG_VR | 0-n | - | unsigned char | - | - | - | - | - | Zaehler der harten Warnungen vorne rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_HL | 0-n | - | unsigned char | - | - | - | - | - | Zaehler der harten Warnungen hinten links |
| STAT_ZAEHLER_HARTE_WARNUNG_HR | 0-n | - | unsigned char | - | - | - | - | - | Zaehler der harten Warnungen hinten rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_XX | 0-n | - | unsigned char | - | - | - | - | - | Zaehler der harten Warnungen waehrend ER Verlust |

<a id="table-arg-0xdcc0"></a>
### ARG_0XDCC0

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RE_ID | - | - | unsigned long | - | - | - | - | - | - | - | ID der Radelektronik |
| RE_POS | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | 0 | 9 | Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts, 4 = Reserverad(nur RDC Gen2), 5, 6, 7, 8, 9 = Radposition nicht bekannt |

<a id="table-res-0xdcc1"></a>
### RES_0XDCC1

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | - | int | - | - | - | 1000 | - | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | - | char | - | - | - | - | - | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | - | int | - | - | - | 1000 | - | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | - | unsigned int | - | - | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | - | unsigned char | - | - | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | - | int | - | - | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | - | int | - | - | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | - | unsigned char | - | - | - | - | - | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | - | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-res-0xdcc3"></a>
### RES_0XDCC3

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | - | int | - | - | - | 1000 | - | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | - | char | - | - | - | - | - | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | - | int | - | - | - | 1000 | - | Vorgegebener Solldruck des ausgewählten Rad |
| STAT_GUTEMPFAENGE | 0-n | - | unsigned int | - | - | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | - | unsigned char | - | - | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | - | int | - | - | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | - | unsigned int | - | - | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | - | unsigned char | - | - | - | - | - | Status Meldung der Radelektronik des angewählten Rads |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | - | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad , 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-res-0xdccd"></a>
### RES_0XDCCD

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-arg-0xdcc6"></a>
### ARG_0XDCC6

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FUNKTIONSNR | 0-n | - | unsigned char | - | TAB_RDC_STEUERFUNKTIONEN | - | - | - | - | - | 1 =  BANDMODE  -  Bandmode; 2 =  ER_FAHRT  - Eigenraderkennung bei Fahrt; 3 =  ER_STAND  - Eigenraderkennung im Stand (Gen2); 4 -  TEST_ER_FAHRT  - Empfang der Eigenraeder bei Fahrt pruefen; 5 -   TEST_ER_STAND  - Empfang der Eigenraeder im Stand pruefen (Gen2); 6 -  RDCBUS_DIAG - Stromdiagnose LIN-Teilnehmer (Gen2); 7 -  SOLLDRUCK_SCHREIBEN  - aktuelle Reifendruckwerte als Sollwert; 8 -  CAL_REQUEST  - Kalibrieranforderung; 9 -  ER_FAHRT_OHNE_TRIGGER  - Eigenraderkennung bei Fahrt ohne Auswertung Triggerbit (Gen3); 10 -  TEST_ER_FAHRT_OHNE_TRIGGER  - Empfang der Eigenraeder bei Fahrt pruefen ohne Auswertung Triggerbit (Gen3) |
| AKTIONSNR | 0-n | - | unsigned char | - | TAB_RDC_SET_RESET | - | - | - | - | - | 1 - SET; 0 - RESET |

<a id="table-tab-rdc-steuerfunktionen"></a>
### TAB_RDC_STEUERFUNKTIONEN

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | BANDMODE |
| 2 | ER_FAHRT |
| 3 | ER_STAND (nur RDC Gen2) |
| 4 | TEST_ER_FAHRT |
| 5 | TEST_ER_STAND (nur RDC Gen2) |
| 6 | RDCBUS_DIAG (nur RDC Gen2) |
| 7 | SOLLDRUCK_SCHREIBEN |
| 8 | CAL_REQUEST |
| 9 | ER_FAHRT_OHNE_TRIGGER (nur RDC Gen3) |
| 10 | TEST_ER_FAHRT_OHNE_TRIGGER (nur RDC Gen3) |

<a id="table-tab-rdc-set-reset"></a>
### TAB_RDC_SET_RESET

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Zurücksetzen |
| 1 | Setzen |

<a id="table-res-0xdcd3"></a>
### RES_0XDCD3

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZAEHLER_WEICHE_WARNUNG_VL | 0-n | - | unsigned char | - | - | - | - | - | Zaehler weiche Warnung vorne links |
| STAT_ZAEHLER_WEICHE_WARNUNG_VR | 0-n | - | unsigned char | - | - | - | - | - | Zaehler weiche Warnung vorne rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_HL | 0-n | - | unsigned char | - | - | - | - | - | Zaehler weiche Warnung hinten links |
| STAT_ZAEHLER_WEICHE_WARNUNG_HR | 0-n | - | unsigned char | - | - | - | - | - | Zaehler weiche Warnung hinten rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_XX | 0-n | - | unsigned char | - | - | - | - | - | Zaehler weiche Warnung waehrend ER Verlust |

<a id="table-res-0xdcc5"></a>
### RES_0XDCC5

Dimensions: 32 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | 0-n | - | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Alle Eigenraeder sind bekannt: 0 = nicht bekannt; 1 = bekannt |
| STAT_RADPOS_ER_BEKANNT | 0-n | - | unsigned char | - | TAB_RDC_BEKANNT_NICHT_BEKANNT | - | - | - | Radpositionen aller Eigenraeder sind bekannt: 0 = nicht bekannt; 1 = bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | 0-n | - | unsigned char | - | TAB_RDC_CONFIRMED | - | - | - | Alle Radpositionen sind ueberprueft und bestaetigt: 0 = nicht bestätigt; 1 = bestätigt |
| STAT_DTC_INACTIVE | 0-n | - | unsigned char | - | TAB_RDC_DTC_ACTIVE | - | - | - | Aktiver DTC Fehler mit Warnlampe im Fehlerspeicher vorhanden: 0 = DTC inaktiv; 1 = DTC aktiv |
| STAT_KAL_ANFORDERUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_CAL_ACTIVE | - | - | - | Kalibrieranforderung steht an: 0 = Kalibrieranforderung inaktiv; 1 = Kalibrieranforderung aktiv |
| STAT_LIN_ON | 0-n | - | unsigned char | - | TAB_RDC_LIN_STATUS | - | - | - | Status LIN Bus: 0 = LIN aus; 1 = LIN an |
| STAT_RAD_ZUORDNUNG_TIMEOUT | 0-n | - | unsigned char | - | TAB_RDC_TIMEOUT | - | - | - | Radzuordnung konnte nicht abgeschlossen werden: 0 = kein Timeout; 1 = Timeout |
| STAT_BANDMODE_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_BANDMODE_ACTIVE | - | - | - | Abfrage ob Bandmode im RDC aktiviert ist: 0 = Bandmode inaktiv ; 1 = Bandmode aktiv |
| STAT_ER_ERKENNUNG_STAND | 0-n | - | unsigned char | - | TAB_RDC_STARTED | - | - | - | Eigenraderkennung im Stand wurde gestartet: 0 = nicht gestartet , 1 = gestartet |
| STAT_ER_ERKENNUNG_FAHRT | 0-n | - | unsigned char | - | TAB_RDC_STARTED | - | - | - | Eigenraderkennung waehrend der Fahrt wurde gestartet: 0 = nicht gestartet 1 = gestartet |
| STAT_TEST_EIGENRAD_FAHRT | 0-n | - | unsigned char | - | TAB_RDC_STARTED | - | - | - | Test-Eigenraderkennung in Fahrt wurde gestartet: 0 = nicht gestartet , 1 = gestartet |
| STAT_TEST_EIGENRAD_STAND | 0-n | - | unsigned char | - | TAB_RDC_STARTED | - | - | - | Test-Eigenraderkennung im Stand wurde gestartet: 0 = nicht gestartet, 1 = gestartet |
| STAT_BUS_DIAGNOSE_EIN | 0-n | - | unsigned char | - | TAB_RDC_STARTED | - | - | - | Komponenten Bus Diagnose wurde gestartet : 0 = Bus Diagnose nicht gestartet ; 1 = Bus Diagnose gestartet |
| STAT_ER_FAHRT_VTHRS_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert : 0 = inaktiv , 1 = aktiv |
| STAT_BM_TIMEOUT_ACTIVE | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Bandmode Timeout laeuft : 0 = inaktiv , 1 = aktiv |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung unspezifisch, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_VL_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung vorne links, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_VR_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung vorne rechts, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_HL_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung hinten links, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_HARTE_WARNUNG_HR_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Harte Warnung hinten rechts, aktiv: 0 = inaktiv ; 1 = aktiv |
| STAT_KL_15_EIN | 0-n | - | unsigned char | - | TAB_RDC_ON_OFF | - | - | - | Klemme 15 EIN : 0 = AUS, 1 = EIN |
| STAT_MOTOR_LAEUFT_EIN | 0-n | - | unsigned char | - | TAB_RDC_ON_OFF | - | - | - | Motor läuft : 0 = Aus ; 1 = EIN |
| STAT_FZG_FAEHRT | 0-n | - | unsigned char | - | TAB_RDC_VEHICLE_RUNNING | - | - | - | Signal Fahrzeug fährt : 0 = steht , 1 = fährt |
| STAT_ERKENNUNG_ALLE_RE | 0-n | - | unsigned char | - | TAB_RDC_DETECTED | - | - | - | Alle Radelektroniken erkannt : 0 = nicht erkannt 1 = erkannt |
| STAT_ERKENNUNG_ZUVIELE_RE | 0-n | - | unsigned char | - | TAB_RDC_DETECTED | - | - | - | Zu viele Radelektroniken erkannt : 0 = nicht erkannt , 1 = erkannt |
| STAT_STOERSENDER_SCI_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Funkstoerung vorhanden : 0 = inaktiv , 1 = aktiv |
| STAT_STOERSENDER_FF_SCI_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Funkstoerung hat zu mehrfachen Telegrammausfaellen gefuehrt : 0 = inaktiv , 1 = aktiv |
| STAT_STOERSENDER_ZEIT_SCI_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Funkstoerung ist laenger vorhanden als die erlaubte Totzeit: 0 = inaktiv , 1 = aktiv |
| STAT_RESET_KEY_STATE | 0-n | - | unsigned char | - | TAB_RDC_KEY_PRESSED | - | - | - | Zustand des Initialisierungstasters  (0: Taster nicht betaetigt - 1: Taster betaetigt |
| STAT_ANT_UEBER_STROM_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Ueberstrom an Empfangsantenne erkannt: 0 = inaktiv , 1 = aktiv |
| STAT_ANT_UEBER_SPANNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Ueberspannung an Empfangsantenne erkannt : 0 = inaktiv , 1 = aktiv |
| STAT_FREQUENZ_WERT | MHz | - | unsigned int | - | - | - | - | - | Gibt die aktuelle RF-Frequenz zurück. Die Frequenz ist abhaengig von der Codierung. (315 oder 433). Angabe in MHz |

<a id="table-tab-rdc-bekannt-nicht-bekannt"></a>
### TAB_RDC_BEKANNT_NICHT_BEKANNT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bekannt |
| 1 | bekannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-confirmed"></a>
### TAB_RDC_CONFIRMED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bestätigt |
| 1 | bestätigt |
| 255 | nicht definiert |

<a id="table-tab-rdc-dtc-active"></a>
### TAB_RDC_DTC_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DTC inaktiv |
| 1 | DTC aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-cal-active"></a>
### TAB_RDC_CAL_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kalibrieranforderung inaktiv |
| 1 | Kalibrieranforderung aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-lin-status"></a>
### TAB_RDC_LIN_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | LIN aus |
| 1 | LIN ein |
| 255 | nicht definiert |

<a id="table-tab-rdc-timeout"></a>
### TAB_RDC_TIMEOUT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Timeout |
| 1 | Timeout |
| 255 | nicht definiert |

<a id="table-tab-rdc-bandmode-active"></a>
### TAB_RDC_BANDMODE_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bandmode inaktiv |
| 1 | Bandmode aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-started"></a>
### TAB_RDC_STARTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht gestartet |
| 1 | gestartet |
| 255 | nciht definiert |

<a id="table-tab-rdc-on-off"></a>
### TAB_RDC_ON_OFF

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | aus |
| 1 | ein |
| 255 | nicht definiert |

<a id="table-tab-rdc-vehicle-running"></a>
### TAB_RDC_VEHICLE_RUNNING

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug fährt |
| 255 | nicht definiert |

<a id="table-tab-rdc-detected"></a>
### TAB_RDC_DETECTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht erkannt |
| 1 | erkannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-key-pressed"></a>
### TAB_RDC_KEY_PRESSED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Taster nicht betätigt |
| 1 | Taster betätigt |
| 255 | nicht definiert |

<a id="table-res-0xdcc9"></a>
### RES_0XDCC9

Dimensions: 40 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | 0-n | - | unsigned char | - | - | - | - | - | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | bar | - | int | - | - | - | 1000 | - | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | °C | - | char | - | - | - | - | - | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | 0-n | - | int | - | - | - | - | - | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |

<a id="table-res-0xdcc7"></a>
### RES_0XDCC7

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RE_IDENTIFIER | 0-n | - | unsigned long | - | - | - | - | - | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | 0-n | - | unsigned char | - | TAB_RDC_RAD_POSITION_NR | - | - | - | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen., Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | bar | - | int | - | - | - | 1000 | - | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | °C | - | char | - | - | - | - | - | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | bar | - | int | - | - | - | 1000 | - | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | 0-n | - | unsigned int | - | - | - | - | - | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | 0-n | - | unsigned char | - | - | - | - | - | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | 0-n | - | int | - | - | - | - | - | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | 0-n | - | unsigned int | - | - | - | - | - | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | 0-n | - | unsigned char | - | - | - | - | - | Status Meldung der Radelektronik des angewählten Rads |
| STAT_HARTE_WARNUNG_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | 0-n | - | unsigned char | - | TAB_RDC_CHANGED | - | - | - | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | 0-n | - | unsigned char | - | TAB_RDC_AKTIV_INAKTIV | - | - | - | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |

<a id="table-tab-rdc-rad-position-nr"></a>
### TAB_RDC_RAD_POSITION_NR

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | vorne links |
| 1 | vorne rechts |
| 2 | hinten links |
| 3 | hinten rechts |
| 4 | Reserverad (nur RDC Gen2) |
| 5 | unbekannt 1 |
| 6 | unbekannt 2 |
| 7 | unbekannt 3 |
| 8 | unbekannt 4 |
| 9 | unbekannt 5 (nur RDC Gen2) |

<a id="table-tab-rdc-changed"></a>
### TAB_RDC_CHANGED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht geändert |
| 1 | geändert |
| 255 | Signal unbekannt |

<a id="table-tab-rdc-aktiv-inaktiv"></a>
### TAB_RDC_AKTIV_INAKTIV

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |
| 255 | Signal unbekannt |

<a id="table-res-0xdcd0"></a>
### RES_0XDCD0

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | km | - | long | - | - | - | - | - | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | - | - | string | - | - | - | - | - | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | s | - | unsigned long | - | - | - | - | - | Zeit in Sekunden seit Start der Systemzeit. Wertebereich: 0 - 4294967294.  Wert 0xffffffff =&gt; ungültig |
| STAT_WARNSTATUS1 | 0-n | - | unsigned int | - | - | - | - | - | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | 0-n | - | unsigned int | - | - | - | - | - | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | 0-n | - | unsigned int | - | - | - | - | - | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | 0-n | - | unsigned int | - | - | - | - | - | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR_WERT | °C | - | char | - | - | - | - | - | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
