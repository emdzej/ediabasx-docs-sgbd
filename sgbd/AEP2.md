# AEP2.prg

- Jobs: [57](#jobs)
- Tables: [29](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | AEP |
| ORIGIN | BMW EI-24 MG |
| REVISION | 1.000 |
| AUTHOR | BMW EI-24 Guzik |
| COMMENT | N/A |
| PACKAGE | 0.29 |
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
- [STATUS_BLOCK_LESEN](#job-status-block-lesen) - Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt
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
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Gibt an ob SG Most Ring wecken darf
- [STATUS_AVERAGE_MESSAGE_RECEPTION_RATE](#job-status-average-message-reception-rate) - Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein
- [STATUS_FOT_TEMPERATUR](#job-status-fot-temperatur) - Gibt an ob SG Most Ring wecken darf
- [STATUS_MOST_3DB](#job-status-most-3db) - xx Status der 3dB Leistungsabsenkung der MOST FOTs.
- [STATUS_ROUTING_ENGINE](#job-status-routing-engine) - Inhalt der Routing Engine
- [STATUS_VERSION_MOST_CONTROLLER](#job-status-version-most-controller) - Return Version of MOST Controller
- [STATUS_VERSORGUNGSSPANNUNG](#job-status-versorgungsspannung) - Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_WAKEUP_STATUS](#job-status-wakeup-status) - Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - Gibt an, ob das SG den MOST-Ring wecken darf.
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - 3dB Leistungsabsenkung der MOST FOTs
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
- [TEL_ROH](#job-tel-roh) - Ausführen eines Telegramms nur mit Übergabe der Daten ignoriert Leerzeichen Format 001122 ....
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - UDS $31 01 F030 Batterietausch registrieren
- [IDENT_IBS](#job-ident-ibs) - $22 40 21 BMW Nr, Seriennummer, SW/HW Index
- [STATUS_IGRINFO_AEP](#job-status-igrinfo-aep) - 0x224016 _STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen
- [STATUS_LEMINFO_AEP](#job-status-leminfo-aep) - 0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen
- [STATUS_MSAINFO_AEP](#job-status-msainfo-aep) - 0x224018 STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen
- [STATUS_SYSTEMCHECK_AEP_INFO_1](#job-status-systemcheck-aep-info-1) - 0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_AEP_INFO_2](#job-status-systemcheck-aep-info-2) - 0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

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

<a id="job-status-block-lesen"></a>
### STATUS_BLOCK_LESEN

Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | long | Nummer des Blockes 0..255 |
| NEU_DEFINIEREN | string | Wenn 'JA' oder 'YES' wird der Block im SG gelöscht und neu ins SG geschrieben Wenn 'NEIN' oder 'NO' wird der Block im SG nicht gelöscht und nicht geschrieben Anschließend wird der Block gelesen |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige Result table SG_Funktionen ARG ID RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Antwort von SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Antwort von SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Antwort von SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |

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
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
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

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Gibt an ob SG Most Ring wecken darf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABILITY_TO_WAKE | int | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| STAT_ABILITY_TO_WAKE_TEXT | int | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-average-message-reception-rate"></a>
### STATUS_AVERAGE_MESSAGE_RECEPTION_RATE

Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSG_CMS_SYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des Kontrollkanals [0-1000] |
| STAT_MSG_CMS_ASYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des async. Kanals. Sollte dieses Gerät nicht Async geflasht werden muss dieser Parameter auf 0 gesetzt sein [0-10000] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fot-temperatur"></a>
### STATUS_FOT_TEMPERATUR

Gibt an ob SG Most Ring wecken darf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FOT_TEMP_CELSIUS | char | Temperatur am FOT des SG in Celsius -128 C bis +127 C hierbei -128 C bedeutet ungültig (0xFF) |
| STAT_FOT_TEMP_FAHRENHEIT | real | Temperatur am FOT des SG in Fahrenheit -196.6 F bis +260.6 F hierbei bedeutet -198.4 F ungültig ( -128 C) Dieses this result is calculated inside the SGBD-Job Fahrenheit = (( Celsius × 9 ) / 5 ) + 32 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-most-3db"></a>
### STATUS_MOST_3DB

xx Status der 3dB Leistungsabsenkung der MOST FOTs.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_3DB | unsigned char | 0 = Lichtleistung abgesenkt, 1 = Volle Lichtleistung Werte aus table TMostLight WERT |
| STAT_MOST_3DB_TEXT | string | 0 = Lichtleistung abgesenkt, 1 = Volle Lichtleistung Werte aus table TMostLight TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-routing-engine"></a>
### STATUS_ROUTING_ENGINE

Inhalt der Routing Engine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MTR_0X00 | string | MTR Registerinhalt 0x00 |
| STAT_MTR_0X10 | string | MTR Registerinhalt 0x10 |
| STAT_MTR_0X20 | string | MTR Registerinhalt 0x20 |
| STAT_MTR_0X30 | string | MTR Registerinhalt 0x30 |
| STAT_MTR_0X40 | string | MTR Registerinhalt 0x40 |
| STAT_MTR_0X50 | string | MTR Registerinhalt 0x50 |
| STAT_MTR_0X60 | string | MTR Registerinhalt 0x60 |
| STAT_MTR_0X70 | string | MTR Registerinhalt 0x70 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-version-most-controller"></a>
### STATUS_VERSION_MOST_CONTROLLER

Return Version of MOST Controller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRANSCEIVER_VERSION | string | Transceiver Version Format DDMMYY |
| STAT_NETSERVICES_VERSION | string | 3 Bytes Netservices Version |
| STAT_NETSERVICES_REVISION | string | 4 Byte Netservices Revision |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-versorgungsspannung"></a>
### STATUS_VERSORGUNGSSPANNUNG

Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MILLI_VOLT_WERT | unsigned int | Spannung in milliVolt |
| STAT_MILLI_VOLT_EINH | string | unit of the result |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-wakeup-status"></a>
### STATUS_WAKEUP_STATUS

Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_STATUS | int | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus WERT |
| STAT_WAKEUP_STATUS_TEXT | string | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ability-to-wake"></a>
### STEUERN_ABILITY_TO_WAKE

Gibt an, ob das SG den MOST-Ring wecken darf.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ABILITY_TO_WAKE | int | 0=off 1=on 2=critical |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-most-3db"></a>
### STEUERN_MOST_3DB

3dB Leistungsabsenkung der MOST FOTs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
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

CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, Sic, Sic_v, TUV, AU, Ueb, Efk Werte externe Umfaenge: Oel, NOx_a, Br_v, Br_h Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
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

<a id="job-tel-roh"></a>
### TEL_ROH

Ausführen eines Telegramms nur mit Übergabe der Daten ignoriert Leerzeichen Format 001122 ....

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TELEGRAMMEINGABE | binary | Daten ohne Header Format 00 11 22 .... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Auftrag an SG |

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

<a id="job-ident-ibs"></a>
### IDENT_IBS

$22 40 21 BMW Nr, Seriennummer, SW/HW Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig |
| SERIENNUMMER | unsigned long | BMW-Seriennummer |
| ZIF_PROGRAMMSTAND | int | Programm referenz |
| ZIF_STATUS | int | Programm Revision |
| HW_REF | int | Hardware Referenz |

<a id="job-status-igrinfo-aep"></a>
### STATUS_IGRINFO_AEP

0x224016 _STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR_AEP0_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_U_BN_SOLL_WERT | real | DREC_IGRINFO[2] 1BYTE in 0 bis 25,5Volt   Einheit: V   Min: 0 Max: 25.5 |
| STAT_U_BN_SOLL_EINH | string | V |
| STAT_IGR_AEP_PR1 | unsigned long | DREC_IGRINFO[3] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_PR2 | unsigned long | DREC_IGRINFO[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QLAD_EINH | string | Ah |
| STAT_IGR_AEP_QLAD_M_WERT | long | Bilanz Medium IGRINFO_1BYTE_in_minus128bis127Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_AEP_QLAD_M_EINH | string | Ah |
| STAT_IGR_AEP_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QELAD_EINH | string | Ah |
| STAT_IGR_AEP_TCODE | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_REG_AEP_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_WERT | unsigned long | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_EINH | string | h |
| STAT_REG_AEP_DAUER_WERT | unsigned long | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-leminfo-aep"></a>
### STATUS_LEMINFO_AEP

0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_AEP_A_WERT | real | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_A_EINH | string | second |
| STAT_ZR_USTAT_AEP_B_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_B_EINH | string | second |
| STAT_ZR_USTAT_AEP_C_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_C_EINH | string | second |
| STAT_ZR_USTAT_AEP_D_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_D_EINH | string | second |
| STAT_ZR_USTAT_AEP_E_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_E_EINH | string | second |
| STAT_ZR_USTAT_AEP_F_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_F_EINH | string | second |
| STAT_ZR_USTAT_AEP_G_WERT | real | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_G_EINH | string | second |
| STAT_ZR_PRIO_AEP_A_WERT | unsigned long | HÃ¤ufigkeit Priobereich A 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_A_EINH | string | second |
| STAT_ZR_PRIO_AEP_B_WERT | unsigned long | HÃ¤ufigkeit Priobereich B 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_B_EINH | string | second |
| STAT_ZR_PRIO_AEP_C_WERT | unsigned long | HÃ¤ufigkeit Priobereich C 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_C_EINH | string | second |
| STAT_ZR_PRIO_AEP_D_WERT | unsigned long | HÃ¤ufigkeit Priobereich D 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_D_EINH | string | second |
| STAT_ZR_PRIO_AEP_E_WERT | unsigned long | HÃ¤ufigkeit Priobereich E 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_E_EINH | string | second |
| STAT_ZR_PRIO_AEP_F_WERT | unsigned long | HÃ¤ufigkeit Priobereich F 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_F_EINH | string | second |
| STAT_ZR_PRIO_AEP_G_WERT | unsigned long | HÃ¤ufigkeit Priobereich G 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_G_EINH | string | second |
| STAT_ZR_PRIO_AEP_H_WERT | unsigned long | HÃ¤ufigkeit Priobereich H 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_H_EINH | string | second |
| STAT_ZR_PRIO_AEP_I_WERT | unsigned long | HÃ¤ufigkeit Priobereich I 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_I_EINH | string | second |
| STAT_ZR_PRIO_AEP_J_WERT | unsigned long | HÃ¤ufigkeit Priobereich J 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_J_EINH | string | second |
| STAT_ZR_PRIO_AEP_K_WERT | unsigned long | HÃ¤ufigkeit Priobereich K 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_K_EINH | string | second |
| STAT_ZR_PRIO_AEP_L_WERT | unsigned long | HÃ¤ufigkeit Priobereich L 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_L_EINH | string | second |
| STAT_ZR_PRIO_AEP_M_WERT | unsigned long | HÃ¤ufigkeit Priobereich M 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_M_EINH | string | second |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-msainfo-aep"></a>
### STATUS_MSAINFO_AEP

0x224018 STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in_0bis5242Ah   Einheit: Ah   Min: 0 Max: 5242.72 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | unsigned long | Gesamtzahl Starts 3BYTE in 0 bis 16777214   Min: 0 Max: 16777214 |
| STAT_ANZAHL_MSASTART_GESAMT | unsigned long | Anzahl MSA Starts 3BYTE in 0 bis 16777214   Min: 0 Max: 16777214 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_EINH | string | V |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | unsigned long | Zeit in MSA 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | second |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_5S_WERT | real | Relative Haeufigkeit der Stops unter 5s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_5S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_ZWISCHEN_5S_20S_WERT | real | Relative Haeufigkeit der Stops zwischen 5s und 20s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_ZWISCHEN_5S_20S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_ZWISCHEN_20S_45S_WERT | real | Relative Haeufigkeit der Stops zwischen 20s und 45s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_ZWISCHEN_20S_45S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UEBER_45S_WERT | real | Relative Haeufigkeit der Stops Ã¼ber 45s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UEBER_45S_EINH | string | percent |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 1 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_MSA_STOP_1_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_TEMP_WERT | real | Temp MSA-Stop 1 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_1_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_1_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 1 MSA_1BYTE_in_0bis25500As   Einheit: As   Min: 0 Max: 25500 |
| STAT_MSA_STOP_1_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_1_DSOC | unsigned long | D_SoC bei MSA-Stop 1 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 2 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_MSA_STOP_2_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_TEMP_WERT | real | Temp MSA-Stop 2 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_2_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_2_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 2 MSA_1BYTE_in_0bis25500As   Einheit: As   Min: 0 Max: 25500 |
| STAT_MSA_STOP_2_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_2_DSOC | unsigned long | D_SoC bei MSA-Stop 2 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 3 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_MSA_STOP_3_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_TEMP_WERT | real | Temp MSA-Stop 3 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_3_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_3_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 3 MSA_1BYTE_in_0bis25500As   Einheit: As   Min: 0 Max: 25500 |
| STAT_MSA_STOP_3_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_3_DSOC | unsigned long | D_SoC bei MSA-Stop 3 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_URSACHE_PMAV_VORHER_1_TEXT | string | vorletzter PMAV 1 MSA 4BIT URSACHE AV |
| STAT_URSACHE_PMAV_VORHER_1_WERT | int | vorletzter PMAV 1 MSA 4BIT URSACHE AV |
| STAT_URSACHE_LETZTER_PMAV_TEXT | string | letzter PMAV MSA 4BIT URSACHE AV |
| STAT_URSACHE_LETZTER_PMAV_WERT | int | letzter PMAV MSA 4BIT URSACHE AV |
| STAT_URSACHE_PMAV_VORHER_3_TEXT | string | vorletzter PMAV 3 MSA 4BIT URSACHE AV |
| STAT_URSACHE_PMAV_VORHER_3_WERT | int | vorletzter PMAV 3 MSA 4BIT URSACHE AV |
| STAT_URSACHE_PMAV_VORHER_2_TEXT | string | vorletzter PMAV 2 MSA 4BIT URSACHE AV |
| STAT_URSACHE_PMAV_VORHER_2_WERT | int | vorletzter PMAV 2 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_1_TEXT | string | Unterschied vorletzter AV 1 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_1_WERT | int | Unterschied vorletzter AV 1 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AKTUELLER_AV_TEXT | string | Ursache aktueller AV MSA 4BIT URSACHE AV |
| STAT_URSACHE_AKTUELLER_AV_WERT | int | Ursache aktueller AV MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_3_TEXT | string | Unterschied vorletzter AV 3 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_3_WERT | int | Unterschied vorletzter AV 3 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_2_TEXT | string | Unterschied vorletzter AV 2 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_2_WERT | int | Unterschied vorletzter AV 2 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_5_TEXT | string | Unterschied vorletzter AV 5 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_5_WERT | int | Unterschied vorletzter AV 5 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_4_TEXT | string | Unterschied vorletzter AV 4 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_4_WERT | int | Unterschied vorletzter AV 4 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_7_TEXT | string | Unterschied vorletzter AV 7 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_7_WERT | int | Unterschied vorletzter AV 7 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_6_TEXT | string | Unterschied vorletzter AV 6 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_6_WERT | int | Unterschied vorletzter AV 6 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_9_TEXT | string | Unterschied vorletzter AV 9 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_9_WERT | int | Unterschied vorletzter AV 9 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_8_TEXT | string | Unterschied vorletzter AV 8 MSA 4BIT URSACHE AV |
| STAT_UNTERSCHIED_AV_VORHER_8_WERT | int | Unterschied vorletzter AV 8 MSA 4BIT URSACHE AV |
| STAT_URSACHE_EA_VORHER_3_TEXT | string | EA vor 3 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_3_WERT | int | EA vor 3 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_2_TEXT | string | EA vor 2 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_2_WERT | int | EA vor 2 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_1_TEXT | string | EA vor 1 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_1_WERT | int | EA vor 1 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_TEXT | string | letzter EA MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_WERT | int | letzter EA MSA 2BIT URSACHE EA |
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
| STAT_E3_WCFB | unsigned long | Ereignis 3 Worst Case Fahrerprofil B (Verbredinfo[19]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[20]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[21]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[22]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[23]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[24]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_WCFA | unsigned long | Ereignis 4 Worst Case Fahrerprofil A (Verbredinfo[25]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_WCFB | unsigned long | Ereignis 4 Worst Case Fahrerprofil B (Verbredinfo[26]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
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
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | AEPINFO1_[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | AEPINFO1_[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | AEPINFO1_[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | AEPINFO1_[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | AEPINFO1_[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | AEPINFO1_[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | AEPINFO1_[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | AEPINFO1_[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | AEPINFO1_[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | AEPINFO1_[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | AEPINFO1_[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | AEPINFO1_[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | AEPINFO1_[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | AEPINFO1_[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | AEPINFO1_[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | AEPINFO1_[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | AEPINFO1_[22] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | h |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | unsigned long | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | unsigned long | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
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
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | AEPINFO2_[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | AEPINFO2_[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | AEPINFO2_[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | AEPINFO2_[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | AEPINFO2_[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | AEPINFO2_[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | AEPINFO2_[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | AEPINFO2_[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | AEPINFO2_[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | AEPINFO2_[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | AEPINFO2_[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | AEPINFO2_[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | AEPINFO2_[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_5 | unsigned long | AEPINFO2_[28] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (64 × 2)
- [LIEFERANTEN](#table-lieferanten) (106 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (20 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (4 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (9 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (69 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (78 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (37 × 2)
- [TMOSTLIGHT](#table-tmostlight) (2 × 2)
- [TWAKEUPSTATUS](#table-twakeupstatus) (3 × 3)
- [CBSKENNUNG](#table-cbskennung) (11 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (1 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (3 × 2)
- [JOBRESULT_EA](#table-jobresult-ea) (64 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [_MOTORUDS_TABLE_MSA_URSACHE_AV](#table-motoruds-table-msa-ursache-av) (16 × 2)
- [_MOTORUDS_TABLE_MSA_URSACHE_EA](#table-motoruds-table-msa-ursache-ea) (4 × 2)
- [_MOTORUDSCODIERUNG_RUHESTROM](#table-motorudscodierung-ruhestrom) (16 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 64 rows × 2 columns

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

Dimensions: 106 rows × 2 columns

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
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

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

Dimensions: 20 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
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

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
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

Dimensions: 9 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 69 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
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
| 0x0F00 | Rearview Kamera hinten | - |
| 0x1000 | Topview Kamera Außenspiegel links | - |
| 0x1100 | Topview Kamera Außenspiegel rechts | - |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | - |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | - |
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
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul links | 1 |
| 0x2A00 | Treibermodul rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
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
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 78 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | DaimlerChrysler |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars (Ford Group) |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis |
| 0x0014 | Microchip |
| 0x0015 | CRF |
| 0x0016 | Renesas Technology Europe GmbH |
| 0x0017 | Atmel |
| 0x0018 | Magnet Marelli |
| 0x0019 | NEC |
| 0x001A | Fujitsu |
| 0x001B | Opel |
| 0x001C | Infineon |
| 0x001D | AMI Semiconductor |
| 0x001E | Vector Informatik |
| 0x001F | Brose |
| 0x0020 | ZMD |
| 0x0021 | ihr |
| 0x0022 | Visteon |
| 0x0023 | ELMOS |
| 0x0024 | ON Semi |
| 0x0025 | Denso |
| 0x0026 | c&s |
| 0x0027 | Renault |
| 0x0028 | Renesas Technology Europe Limited |
| 0x0029 | Yazaki |
| 0x002A | Trinamic Microchips |
| 0x002B | Allegro Microsystems |
| 0x002C | Toyota |
| 0x002D | PSA Peugeot Citroën |
| 0x002E | Westsächsische Hochschule Zwickau |
| 0x002F | Micron AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt Ingenierbüro GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA Hueck & Co. |
| 0x0037 | Continental Temic microelectronic GmbH |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electric Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies |
| 0x0055 | Lear Corporation  |
| 0xFFFF | unbekannter Hersteller |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler gespeichert |
| 0x44 | Fehler momentan vorhanden und bereits gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler momentan vorhanden und bereits gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler momentan vorhanden und bereits gespeichert |
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

<a id="table-tfblockidtexte"></a>
### TFBLOCKIDTEXTE

Dimensions: 37 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | NetworkMaster=0x02 |
| 0x03 | ConnectionMaster=0x03 |
| 0x04 | PowerMaster=0x04 |
| 0x05 | Vehicle=0x05 |
| 0x06 | Diagnose=0x06 |
| 0x07 | VideoSwitch=0x07 |
| 0x10 | ManMachineInterface=0x10 |
| 0x11 | Sprachverarbeitungssystem=0x11 |
| 0x15 | ControlElements=0x15 |
| 0x16 | Security=0x16 |
| 0x20 | AudioMaster=0x20 |
| 0x22 | AudioAmplifier=0x22 |
| 0x23 | HeadPhoneAmplifier=0x23 |
| 0x24 | AuxilliaryInput=0x24 |
| 0x31 | AudioDiscPlayer=0x31 |
| 0x32 | MultiMediaChanger=0x32 |
| 0x40 | AM/FM Tuner=0x40 |
| 0x41 | TMC Tuner=0x41 |
| 0x42 | TVTuner=0x42 |
| 0x43 | ExternSource=0x43 |
| 0x44 | SDARS=0x44 |
| 0x50 | TelefonFix=0x50 |
| 0x51 | PhoneBook=0x51 |
| 0x52 | Navigationssystem=0x52 |
| 0x6F | Monitor=0x6F |
| 0x71 | Climate=0x71 |
| 0x80 | MMI_Terminal=0x80 |
| 0x81 | KOMBI_Terminal=0x81 |
| 0x90 | Telematik=0x90 |
| 0xAB | EDIABAS4MOST=0xAB |
| 0xC9 | Service=0xC9 |
| 0xCA | KombiMiscFkts=0xCA |
| 0xCB | Bordcomputer=0xCB |
| 0xCC | ADASInterface=0xCC |
| 0xE0 | KombiInterface=0xE0 |
| 0xE1 | HUDInterface=0xE1 |
| 0xFD | Sahara=0xFD |

<a id="table-tmostlight"></a>
### TMOSTLIGHT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lichtleistung abgesenkt |
| 1 | Volle Lichtleistung |

<a id="table-twakeupstatus"></a>
### TWAKEUPSTATUS

Dimensions: 3 rows × 3 columns

| WERT | TEXT | TEXT2 |
| --- | --- | --- |
| 0 | not initialised | off |
| 1 | SG will be waked up | on |
| 2 | SG are waked up | critical |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 11 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0D | NOx_a | NOx-Additiv |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-jobresult-ea"></a>
### JOBRESULT_EA

Dimensions: 64 rows × 2 columns

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

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-motoruds-table-msa-ursache-av"></a>
### _MOTORUDS_TABLE_MSA_URSACHE_AV

Dimensions: 16 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ursache AV ausserhalb PM |
| 1 | Batterieladezustand-Erkennung nicht plausibel und FIT-Korrektur |
| 2 | Batterieladezustand-Erkennung nicht plausibel |
| 3 | FIT-Korrektur |
| 4 | Batterieladezustand zu niedrig |
| 5 | Batterieladezustand zu niedrig und (Startspannung zu niedrig ODER Bordnetzstrom zu hoch ODER T_batt zu hoch) |
| 6 | T_batt zu hoch |
| 7 | T_batt zu hoch und (Startspannung zu niedrig ODER Bordnetzstrom zu hoch) |
| 8 | Startspannung zu niedrig |
| 9 | Startspannung zu niedrig und Bordnetzstrom zu hoch |
| 10 | Bordnetzstrom zu hoch |
| 11 | Reserve-Prio 1 |
| 12 | Reserve-Prio 2 |
| 13 | Reserve-Prio 3 |
| 14 | Reserve-Prio 4 |
| 15 | ungueltig |

<a id="table-motoruds-table-msa-ursache-ea"></a>
### _MOTORUDS_TABLE_MSA_URSACHE_EA

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein EA |
| 1 | EA infolge I_BN |
| 2 | EA infolge D_SoC |
| 3 | nicht definiert |

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
| 16 | Ruhestrom = 200...1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 17 | Ruhestrom groesser 1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 18 | Ruhestrom kleiner 80mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 19 | Ruhestrom = 80...200mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 20 | Ruhestrom = 200...1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 21 | Ruhestrom groesser 1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
