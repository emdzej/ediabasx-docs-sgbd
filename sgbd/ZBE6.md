# ZBE6.prg

- Jobs: [30](#jobs)
- Tables: [50](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zentrales Bedienelement |
| ORIGIN | BMW EI-841 Oellinger |
| REVISION | 1.001 |
| AUTHOR | PREH-GMBH EI-840 Braun |
| COMMENT | - |
| PACKAGE | 1.47 |
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
| CPS | string | Codierpruefstempel 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0XD134_D](#table-arg-0xd134-d) (1 × 12)
- [ARG_0XD14D_D](#table-arg-0xd14d-d) (2 × 12)
- [ARG_0XD598_D](#table-arg-0xd598-d) (1 × 12)
- [ARG_0XD60E_D](#table-arg-0xd60e-d) (1 × 12)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (21 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (25 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (4 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (8 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (3 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0XD134_D](#table-res-0xd134-d) (5 × 10)
- [RES_0XD14D_D](#table-res-0xd14d-d) (9 × 10)
- [RES_0XD213_D](#table-res-0xd213-d) (7 × 10)
- [RES_0XD214_D](#table-res-0xd214-d) (7 × 10)
- [RES_0XD215_D](#table-res-0xd215-d) (7 × 10)
- [RES_0XD216_D](#table-res-0xd216-d) (7 × 10)
- [RES_0XD217_D](#table-res-0xd217-d) (7 × 10)
- [RES_0XD218_D](#table-res-0xd218-d) (7 × 10)
- [RES_0XD219_D](#table-res-0xd219-d) (7 × 10)
- [RES_0XD21A_D](#table-res-0xd21a-d) (7 × 10)
- [RES_0XD21B_D](#table-res-0xd21b-d) (9 × 10)
- [RES_0XD21C_D](#table-res-0xd21c-d) (7 × 10)
- [RES_0XD21D_D](#table-res-0xd21d-d) (7 × 10)
- [RES_0XD21E_D](#table-res-0xd21e-d) (7 × 10)
- [RES_0XD21F_D](#table-res-0xd21f-d) (7 × 10)
- [RES_0XD228_D](#table-res-0xd228-d) (6 × 10)
- [RES_0XD60E_D](#table-res-0xd60e-d) (1 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (28 × 16)
- [TAB_ARG_STELLGLIED_POSITIONEN](#table-tab-arg-stellglied-positionen) (5 × 2)
- [TAB_STELLGLIED_POSITIONEN](#table-tab-stellglied-positionen) (6 × 2)
- [TAB_ZBE_TASTEN](#table-tab-zbe-tasten) (9 × 2)
- [TAB_ZBE_VARIANTE](#table-tab-zbe-variante) (5 × 2)

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

Dimensions: 137 rows × 2 columns

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
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin |
| 0x0000BE | Schaeffler Technologies |
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

<a id="table-arg-0xd134-d"></a>
### ARG_0XD134_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | 0-n | - | unsigned char | - | TAB_ARG_STELLGLIED_POSITIONEN | 1.0 | 1.0 | 0.0 | - | - | Ansteuerung des Stellglieds:  NULLSTELLUNG, NORDEN ( nicht bei ZBE Low), OSTEN,  SUEDEN ( nicht bei ZBE Low), WESTEN |

<a id="table-arg-0xd14d-d"></a>
### ARG_0XD14D_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTE | 0-n | - | unsigned char | - | TAB_ZBE_TASTEN | - | - | - | - | - | Ansteuerung der ZBE Tasten. Siehe Tabelle TAB_ZBE_TASTEN |
| AKTION | 0/1 | - | unsigned char | - | - | - | - | - | - | - | 0 = NICHT GEDRUECKT, 1 = GEDRUECKT |

<a id="table-arg-0xd598-d"></a>
### ARG_0XD598_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SIGNALMODE | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | SIGNALMODE:  0 = NICHT BLOCKIERT = Signale werden verschickt,  1 = BLOCKIERT = Signale werden blockiert, keine Auswirkung auf andere Funktionen (Steuergeräte) |

<a id="table-arg-0xd60e-d"></a>
### ARG_0XD60E_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTIVIERUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Aktivierung Touchpad: 0x00 = aus (zurück in den Ausgangszustand) 0x01 = ein |

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
| F_HLZ_VIEW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 21 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x026700 | Energiesparmode aktiv | 0 |
| 0x026708 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x026709 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02670A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02670B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 |
| 0x02670C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x026720 | CAN-Fehler (Sammelfehler) | 0 |
| 0x026723 | Flash Memory Fehler (Sammelfehler) | 0 |
| 0x026726 | Hardwarefehler (Sammelfehler) | 0 |
| 0x026729 | Softwarefehler (Sammelfehler) | 0 |
| 0x02FF67 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0x801400 | Stellglied (Kippen/Rotieren): Unplausible Position erkannt | 0 |
| 0x801405 | Unterspannung erkannt | 1 |
| 0x801406 | Ueberspannung erkannt | 1 |
| 0x801409 | Interner Komponetenfehler Touchfeld | 0 |
| 0x801422 | Interner Steuergerätefehler | 0 |
| 0xE2C41E | IuK-CAN Control Module Bus OFF | 0 |
| 0xE2C468 | BODY-CAN Control Module Bus OFF | 0 |
| 0xE2CBFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 |
| 0xE2D400 | Botschaft (0x202, Dimmung): Ausfall | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x170C | Batteriespannung | mV | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

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

Dimensions: 25 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x670003 | ECUM_E_RAM_CHECK_FAILED | 0 |
| 0x670006 | FLS_E_READ_FAILED | 0 |
| 0x670007 | FLS_E_WRITE_FAILED | 0 |
| 0x670008 | FLS_E_COMPARE_FAILED | 0 |
| 0x67000A | FLS_E_ERASE_FAILED | 0 |
| 0x67000B | FLS_E_UNEXPECTED_FLASH_ID | 0 |
| 0x67000D | FLSTST_E_FLSTST_FAILURE | 0 |
| 0x67000E | MCU_E_CLOCK_FAILURE | 0 |
| 0x67000F | NVM_E_INTEGRITY_FAILED | 0 |
| 0x670010 | NVM_E_LOSS_OF_REDUNDANCY | 0 |
| 0x670011 | NVM_E_QUEUE_OVERFLOW | 0 |
| 0x670012 | NVM_E_REQ_FAILED | 0 |
| 0x670013 | NVM_E_VERIFY_FAILED | 0 |
| 0x670014 | NVM_E_WRITE_PROTECTED | 0 |
| 0x670015 | NVM_E_WRONG_BLOCK_ID | 0 |
| 0x670016 | RAMTST_E_RAM_FAILURE | 0 |
| 0x670037 | MCU_E_QUARTZ_FAILURE | 0 |
| 0x670039 | WDGM_E_MONITORING | 0 |
| 0x67003A | WDGM_E_SET_MODE | 0 |
| 0x670200 | TOUCHPAD_SENSOR_SHORT | 0 |
| 0x670201 | TOUCHPAD_SENSOR_OPEN | 0 |
| 0x670202 | TOUCHPAD_COMMUNICATION_ERROR | 0 |
| 0x670203 | TOUCHPAD_COMMUNICATION_TIMEOUT | 0 |
| 0x670204 | TOUCHPAD_COMMUNICATION_CRCERROR | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x170C | Batteriespannung | mV | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

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

<a id="table-res-0xd134-d"></a>
### RES_0XD134_D

Dimensions: 5 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STELLGLIED_N_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Stellglied-Position Nord: 0 = nicht betätigt, 1 = betätigt;  nicht bei ZBE Low |
| STAT_STELLGLIED_E_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Stellglied-Position Ost: 0 = nicht betätigt, 1 = betätigt |
| STAT_STELLGLIED_S_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Stellglied-Position Süd: 0 = nicht betätigt, 1 = betätigt,  nicht bei ZBE Low |
| STAT_STELLGLIED_W_EIN | 0/1 | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Stellglied-Position West: 0 = nicht betätigt, 1 = betätigt |
| STAT_STELLGLIED_NR | 0-n | - | unsigned char | - | TAB_STELLGLIED_POSITIONEN | 1.0 | 1.0 | 0.0 | Wert des Stellglieds:  0 = Keine Betätigung,  1 = Stellglied gedrückt nach Norden, nicht bei ZBE Low 2 = Stellglied gedrückt nach Osten,  3 = Stellglied gedrückt nach Süden,  nicht bei ZBE Low 4 = Stellglied gedrückt nach Westen |

<a id="table-res-0xd14d-d"></a>
### RES_0XD14D_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTEN | 0-n | high | unsigned char | - | TAB_ZBE_TASTEN | - | - | - | Gibt aus, welche Tasten gedrückt sind. |
| STAT_TASTER_MENU_FAV_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_BACK_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_OPTION_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_RADIO_COM_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_MEDIA_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_NAV_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_TEL_MAP_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |
| STAT_TASTER_PUSH_EIN | 0/1 | high | unsigned char | - | - | - | - | - | 0=Taste nicht betätigt, 1 Taste betätigt |

<a id="table-res-0xd213-d"></a>
### RES_0XD213_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd214-d"></a>
### RES_0XD214_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd215-d"></a>
### RES_0XD215_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd216-d"></a>
### RES_0XD216_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd217-d"></a>
### RES_0XD217_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd218-d"></a>
### RES_0XD218_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd219-d"></a>
### RES_0XD219_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd21a-d"></a>
### RES_0XD21A_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd21b-d"></a>
### RES_0XD21B_D

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RASTEN_IM_UHRZEIGERSINN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Rasten im Uhrzeigersinn |
| STAT_RELATIVZEIT_IM_UHRZEIGERSINN_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit der letzten Drehung gegen den Uhrzeigersinn |
| STAT_RASTEN_GEGEN_UHRZEIGERSINN_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Rasten gegen Uhrzeigersinn |
| STAT_RELATIVZEIT_GEGEN_UHRZEIGERSINN_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzte Drehung gegen den Uhrzeigersinn |
| STAT_UNDERFLOW_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Underflow, Anschlag links |
| STAT_RELATIVZEIT_UNDERFLOW_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Underflow |
| STAT_OVERFLOW_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Overflow, Anschlag rechts |
| STAT_RELATIVZEIT_OVERFLOW_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Overflow |
| STAT_KM_DREH_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand der letzten Drehaktion  |

<a id="table-res-0xd21c-d"></a>
### RES_0XD21C_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd21d-d"></a>
### RES_0XD21D_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd21e-d"></a>
### RES_0XD21E_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd21f-d"></a>
### RES_0XD21F_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANZAHL_DRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Druck |
| STAT_RELATIVZEIT_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Druck |
| STAT_ANZAHL_LANGDRUCK_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Langdruck |
| STAT_RELATIVZEIT_LANGDRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Langdruck |
| STAT_ANZAHL_HAENGER_WERT | - | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Anzahl Hänger |
| STAT_RELATIVZEIT_HAENGER_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit letzter Hänger |
| STAT_KM_DRUCK_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand letzter Druck, Langdruck oder Hänger |

<a id="table-res-0xd228-d"></a>
### RES_0XD228_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RELATIVZEIT_VERBAU_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Zeit des Erstverbau |
| STAT_KM_VERBAU_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand beim Verbau |
| STAT_VIN_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | VIN |
| STAT_RELATIVZEIT_LETZTVERBAU_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | Relativzeit Letztverbau |
| STAT_KM_LETZTVERBAU_DATA | DATA | high | data[4] | - | - | 1.0 | 1.0 | 0.0 | KM-Stand Letztverbau |
| STAT_VIN_LETZTVERBAU_DATA | DATA | high | data[7] | - | - | 1.0 | 1.0 | 0.0 | Fahrgestellnummer Letztverbau |

<a id="table-res-0xd60e-d"></a>
### RES_0XD60E_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TOUCHPAD_AKTIVIERUNG | 0/1 | high | unsigned char | - | - | - | - | - | Status der Aktivierung vom Touchpad: 0x00 = Touchpad nicht aktiviert 0x01 = Touchpad aktiviert |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 28 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| STELLGLIED_POSITIONEN | 0xD134 | - | Stellgliedposition | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD134_D | RES_0xD134_D |
| VARIANTE_ZBE | 0xD137 | STAT_ZBE_VARIANTE_NR | Variante ZBE: 0 = Standardvariante 1 = Asiavariante 2 = Standardvariante mit Touchpad 3 = Asiavariante mit Touchpad 255 = Ungültiger Wert oder ZBE nicht codiert | 0-n | - | High | unsigned char | TAB_ZBE_VARIANTE | - | - | - | - | 22 | - | - |
| ZBE_TASTEN | 0xD14D | - | Ansteuerung der angegebenen Taste. Simuliert eine normale Tastenbetätigung. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD14D_D | RES_0xD14D_D |
| SCHRITTE_ROTRAD | 0xD14E | STAT_REGISTER_ROTRAD_WERT | Ausgabe vom aktuellen Wert für die Stellung des Rotationsrad. Wert 0, wenn Drehgeber nicht konfiguriert wurde | - | - | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| LOGGING_TASTE1 | 0xD213 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD213_D |
| LOGGING_TASTE2 | 0xD214 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD214_D |
| LOGGING_TASTE3 | 0xD215 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD215_D |
| LOGGING_TASTE4 | 0xD216 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD216_D |
| LOGGING_TASTE5 | 0xD217 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD217_D |
| LOGGING_TASTE6 | 0xD218 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD218_D |
| LOGGING_TASTE7 | 0xD219 | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD219_D |
| LOGGING_TASTE8 | 0xD21A | - | Loggingdaten der Tasten. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21A_D |
| LOGGING_DREHSTELLER | 0xD21B | - | Logging des Drehstellers (Drehen, Kippen) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21B_D |
| LOGGING_DREHSTELLER_NORD | 0xD21C | - | Logging der Tasten  | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21C_D |
| LOGGING_DREHSTELLER_OST | 0xD21D | - | Logging der Tasten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21D_D |
| LOGGING_DREHSTELLER_SUED | 0xD21E | - | Logging der Tasten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21E_D |
| LOGGING_DREHSTELLER_WEST | 0xD21F | - | Logging der Tasten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD21F_D |
| LOGGING_VERBAU | 0xD228 | - | Auslesen, wann die Komponente verbaut wurde | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD228_D |
| STEUERN_SIGNALMODE | 0xD598 | - | Stellt ein, ob bei Betätigung der Bedienelemente die Signale auf den CAN nach außen verschickt werden (unterdrückt = Arg 1). Wird bei Klemmenwechsel automatisch deaktiviert (oder bei Arg. 0) | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD598_D | - |
| TOUCHPAD_BERUEHRUNG | 0xD60D | STAT_TOUCHPAD_BERUEHRUNG | Berührungserkennung Touchpad: 0x00 = keine Berührung erkannt 0x01 = Berührung erkannt | 0/1 | - | High | unsigned char | - | - | - | - | - | 22 | - | - |
| TOUCHPAD_AKTIVIERUNG | 0xD60E | - | Aktivierung vom Touchpad | - | - | - | - | - | - | - | - | - | 22;2E | ARG_0xD60E_D | RES_0xD60E_D |
| TOUCHPAD_ANNAEHERUNG | 0xD68D | STAT_TOUCHPAD_ANNAEHERUNG | Annäherungsserkennung Touchpad: 0x00 = keine Annäherung erkannt 0x01 = Annäherung erkannt | 0/1 | - | High | unsigned char | - | - | - | - | - | 22 | - | - |
| SPANNUNG_KLEMME_30B_WERT | 0xDAD9 | STAT_SPANNUNG_KLEMME_30B_WERT | Spannungswert am Steuergerät an Klemme 30B (auf eine Nachkommastelle genau) | V | - | - | int | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |

<a id="table-tab-arg-stellglied-positionen"></a>
### TAB_ARG_STELLGLIED_POSITIONEN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NULLSTELLUNG |
| 1 | NORDEN |
| 2 | OSTEN |
| 3 | SUEDEN |
| 4 | WESTEN |

<a id="table-tab-stellglied-positionen"></a>
### TAB_STELLGLIED_POSITIONEN

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Betätigung |
| 1 | Stellglied nach Norden gedrückt |
| 2 | Stellglied nach Osten gedrückt |
| 3 | Stellglied nach Süden gedrückt |
| 4 | Stellglied nach Westen gedrückt |
| 0xFF | Wert ungültig |

<a id="table-tab-zbe-tasten"></a>
### TAB_ZBE_TASTEN

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | MENU/FAV |
| 0x02 | BACK |
| 0x04 | OPTION |
| 0x08 | RADIO/COM |
| 0x10 | MEDIA |
| 0x20 | NAV |
| 0x40 | TEL/MAP |
| 0x80 | PUSH |
| 0xFF | Ungültiger Wert |

<a id="table-tab-zbe-variante"></a>
### TAB_ZBE_VARIANTE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Standardvariante |
| 0x01 | Standardvariante mit Touchpad |
| 0x02 | Rükovariante  |
| 0x03 | Rükovarinte mit Touchpad |
| 0xFF | Ungültiger Wert oder ZBE nicht codiert |
